## bash cmd history

bash 쉘은 터미널에 입력한 커맨드를 계속 기록하는데,

쉘 실행 중에는 RAM에 기록하고 있고, 로그아웃시에 .bash_history에 저장한다.

쉘 실행 중에 이전 커맨드를 확인하고 싶으면

```bash
history
```

를 사용하면 되고,

```bash
history -c
```

로 삭제가 가능하다.
