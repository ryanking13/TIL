# event loop

> 2018/02/12

Node.js는 비동기 방식을 사용하여 여러 작업의 동시 처리가 가능하다.

Node.js는 멀티 스레딩으로 비동기를 구현하는 대신 단일 스레드에 이벤트 루프를 접목시키는 형태로 비동기 방식을 구현하였다.

![](https://cloud.githubusercontent.com/assets/12269489/16215491/b1493856-379d-11e6-9c16-a9a4cf841567.png)

`seTimeout`으로 대표되는 자바스크립트의 비동기 API는 콜백함수를 콜 스택이 아닌 태스크 큐에 삽입한다.

이벤트 루프는 호출 스택을 감시하면서, 호출 스택이 비었을때 태스크 큐에서 함수를 꺼내와 호출 스택에 삽입하고 실행한다.


---

### Reference

> http://meetup.toast.com/posts/89
