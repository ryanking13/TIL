# yeoman

> 2018/02/26

> _THE WEB’S SCAFFOLDING TOOL FOR MODERN WEBAPPS_

웹/앱 개발을 하기 위해서는 백 엔드 + 프론트 엔드 + DB 등 다양한 기술이 조합되어야 한다.

아예 기술 용어로 쓰이는 듯한 MEAN stack이라는 말도 있는 듯.

![](https://cdn-images-1.medium.com/max/1000/0*V5tE2nUtV5HI5P3l.png)

이러한 기술 스택을 일일이 관리해주는 것은 꽤나 까다로운 일이므로, 자동화시켜줄 툴이 필요하며, 그것을 해주는 것이 `yeoman`이다.

![](https://cdn-images-1.medium.com/max/1000/0*xNfl0uugKjmzkenK.png)

`yeoman`은 yo, Grunt, Bower를 합친 툴이며,

![](https://cdn-images-1.medium.com/max/1000/0*ZkKBpchcbk6SiBXL.png)

yo가 제너레이터를 이용하여 기본 코드르 생성하면, bower가 패키지를 다운로드, 관리해주며, grunt로 테스트, 빌트를 하는 방식.

```
npm install -g yo
```

npm을 통해 설치할 수 있고,

```
npm install -g generator-angular-fullstack
```

어떠한 기술 스택을 사용하냐에 따라서 제너레이터가 달라지므로 [yeoman 사이트](http://yeoman.io/generators/)에서 제너레이터를 찾아 추가로 설치해주어야 한다.

```
yo angular-fullstack yourAppName
```

그리고 실행

### Reference

> http://yeoman.io/

> https://medium.com/humming-top/yeoman-%EC%9C%BC%EB%A1%9C-angular-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-dd337b37ef59
