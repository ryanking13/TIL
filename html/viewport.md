# viewport

> 2018/02/26 - init

모바일 브라우저는 `viewport`라는 가상 window 위에 페이지를 렌더링한다.

다양한 비율의 디바이스가 존재하는 모바일 디바이스 특성상, 해당 디바이스에 알맞은 viewport 크기로 페이지를 렌더링할 필요가 있는데, 이를 위하여 meta 태그를 사용할 수 있다.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

`width=device-width` 로 지정해 줌으로써 디바이스의 크기에 알맞에 viewport가 조정된다.

데스크톱 브라우저의 경우는 해당 meta 태그를 무시한다.

---

### Reference

> https://jongmin92.github.io/2017/02/09/HTML/viewport/
