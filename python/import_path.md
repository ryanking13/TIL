# import path

> 2019/09/05

파이썬에서 모듈을 찾기 위해 사용하는 import path는 `sys.path`에 기록되어 있다.

아래는 Windows 10, python 3.7.4 환경에서 `sys.path`를 확인한 결과다.

```python
>>> import sys
>>> sys.path
['', 'C:\\Python37\\python37.zip', 'C:\\Python37\\DLLs', 'C:\\Python37\\lib', 'C:\\Python37', 'C:\\Users\\<<username>>\\AppData\\Roaming\\Python\\Python37\\site-packages', 'C:\\Python37\\lib\\site-packages']
```

pip 를 사용하여 외부 패키지를 설치할 경우, `C:\\Python37\\lib\\site-packages`에, `--user` 옵션을 사용하여 설치할 경우,
`C:\\Users\\<<username>>\\AppData\\Roaming\\Python\\Python37\\site-packages`에 설치될 것을 예상할 수 있다.
