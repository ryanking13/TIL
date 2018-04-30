# 윈도우 cmd autorun

한글 윈도우의 경우는 디폴트 codepage가 cp949로 되어 있어서 필요할 때마다 utf-8로 바꿔줘야 할 때가 많다.

그 외에도 cmd를 켰을 때에 적절한 세팅을 해주고 싶은 경우가 많은데,

리눅스처럼 .rc 파일을 세팅할 수가 없어서 레지스트리를 조작해주어야 한다.

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor
```

위 레지스트리 폴더에서 `Autorun` 문자열을 만들고 값에 명령어를 적어주면 된다.


---

### Reference

> https://superuser.com/questions/269818/change-default-code-page-of-windows-console-to-utf-8
