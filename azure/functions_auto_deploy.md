# Azure Functions 자동 배포

> 2020/01/11 - init

Github Actions를 이용한 Azure Functions 자동 배포

1. Azure Credential 생성

API 사용을 위한 Credential을 생성한다.

Azure CLI를 통한 로그인은 되어 있지 않다면 먼저 `az login`으로 로그인 할 것.

```sh
az group list
```

```json
[
  //...
  {
    "id": "/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/appname",
    "location": "eastasia",
    "managedBy": null,
    "name": "welstory",
    "properties": {
      "provisioningState": "Succeeded"
    },
    "tags": null,
    "type": null
  }
  //...
]
```

배포할 애플리케이션의 `id`를 확인한다.
위 결과에서는 `/subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/appname`가 된다.

이제 키를 생성하자

```sh
az ad sp create-for-rbac --role contributor --scopes /subscriptions/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee/resourceGroups/appname --sdk-auth
```

```json
{
  "clientId": "<REDACTED>",
  "clientSecret": "<REDACTED>",
  "subscriptionId": "<REDACTED>",
  "tenantId": "<REDACTED>",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

나온 결과를 그대로 Github Secret으로 등록한다.

![](https://github.com/Azure/actions-workflow-samples/raw/master/assets/images/Add-secret-name-value.png)

이제 `.github/workflows`에 Github Actions 스크립트를 작성해주면 된다.

```yml
# From: https://github.com/Azure/actions-workflow-samples/blob/master/FunctionApp/linux-python-functionapp-on-azure.yml
# Action Requires
# 1. Setup the AZURE_CREDENTIALS secrets in your GitHub Repository
# 2. Replace PLEASE_REPLACE_THIS_WITH_YOUR_FUNCTION_APP_NAME with your Azure function app name
# 3. Add this yaml file to your project's .github/workflows/
# 4. Push your local project to your GitHub Repository

name: Azure Functions Deploy

on:
  push:
    branches:
    - master

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: 'Checkout GitHub Action'
      uses: actions/checkout@master

    # If you want to use publish profile credentials instead of Azure Service Principal
    # Please comment this 'Login via Azure CLI' block
    - name: 'Login via Azure CLI'
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}

    - name: Setup Python 3.6
      uses: actions/setup-python@v1
      with:
        python-version: 3.6

    - name: 'Run pip'
      shell: bash
      run: |
        # If your function app project is not located in your repository's root
        # Please change your directory for pip in pushd
        pushd .
        python -m pip install --upgrade pip
        pip install -r requirements.txt --target=".python_packages/lib/python3.6/site-packages"
        popd

    - name: 'Run Azure Functions Action'
      uses: Azure/functions-action@v1
      id: fa
      with:
        app-name: <YOUR_APP_NAME>
        # If your function app project is not located in your repository's root
        # Please consider prefixing the project path in this package parameter
        package: '.'
        # If you want to use publish profile credentials instead of Azure Service Principal
        # Please uncomment the following line
        # publish-profile: ${{ secrets.SCM_CREDENTIALS }}

    #- name: 'use the published functionapp url in upcoming steps'
    #  run: |
    #    echo "${{ steps.fa.outputs.app-url }}"

# For more information on GitHub Actions:
#   https://help.github.com/en/categories/automating-your-workflow-with-github-actions
```

### References 

> https://github.com/Azure/actions-workflow-samples/blob/master/assets/create-secrets-for-GitHub-workflows.md

> https://github.com/Azure/login