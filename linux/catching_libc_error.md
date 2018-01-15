# catching libc error

프로그램 실행 과정에서 발생하는 에러 중, stdout이나 stderr stream을 거치지 않고 나오는 에러가 있다.

```
*** stack smashing detected ***:  terminated
```

대표적인게 SSP로 인해 발생하는 위와 같은 에러인데,

이러한 에러를 캐치, 리다이렉션 하고 싶을 때 사용할 수 있는 방법.

```
LIBC_FATAL_STDERR_=1
```

위 환경변수를 지정해주면 에러를 stderr로 출력되도록 옮길 수 있다.
