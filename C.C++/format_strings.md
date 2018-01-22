# format strings

C/C++의 printf()에서 일반적으로 사용하는 `%d`, `%x`, `%c`, `%s`등 외에도 여러 포맷 스트링이 존재한다.

대표적으로 포맷 스트링 버그에서 사용하는 `%n`, `%hn`이 있는데 문제를 풀다가 long long 타입의 변수를 포맷 스트링 버그를 사용해서 공격해야 할 일이 있어서 포맷 스트링을 정리해보는 글

| Specifier      | Argument Type  | Base | Precision | Version |
| :------------- | :------------- | :--- | :-------- | :---       |
| %n             | __int *x__     |      |           |         |
| %hn            | __short *x__   |      |           |         |
| %ln            | __long *x__    |      |           |         |
| %hhn           | __int *x__     |      |           | C99     |
| %jn            | __intmax_t *x__ |      |           | C99     |
| %lln           | __long long__ *x |      |           | C99     |
| %tn            | __ptrdiff_t__ *x |      |           | C99     |
| %zn            | __size_t *x__  |      |           | C99     |

위는 포맷 스트링 버그에 사용할 수 있는 것들을 나타낸 것이고, 아래 레퍼런스에서 전체 포맷 스트링 리스트를 볼 수 있다.

---

### reference

http://www.qnx.com/developers/docs/6.5.0/index.jsp?topic=%2Fcom.qnx.doc.dinkum_en_c99%2Flib_prin.html
