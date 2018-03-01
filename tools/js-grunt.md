# Grunt

> 2018/02/26 - init

> Grunt is a task-based command line build tool for JavaScript projects.

__Grunt__ 는 자바스크립트 프로젝트를 빌드하는 툴이다.

여러 자바스크립트 파일을 합치고, 압축하고, 테스트하고, 문법 검사도 수행할 수 있다.

```
npm install -g grunt-cli
```

위 명령어로 grunt 커맨드라인 툴을 사용할 수 있게 하고,

```
npm install grunt --save
```

grunt 사용을 위해선 해당 프로젝트에 grunt를 설치해야 한다. 또한 grunt 자체만으로 모든 기능이 포함되는 것이 아니고, 플러그인을 따로 설치해주어야 한다.

```
npm isntall grunt-contrib-concat
npm install grunt-contrib-uglify
npm install grunt-contrib-jshint
npm install grunt-contrib-cssmin
...
```

__Gruntfile.js__

```js
module.exports = function(grunt) {
  grunt.initConfig({
  });
  grunt.registerTask('dev', []);
}
```

또한 grunt는 `Gruntfile.js` 파일을 설정파일로 사용하므로, 프로젝트 최상단에 `Gruntfile.js`가 존재해야 한다.

```
grunt dev
```

이외에도 다양한 명령어가 존재.

### Reference

> https://gruntjs.com/

> https://medium.com/sunhyoups-story/grunt%EC%99%80-bower%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EC%9B%B9-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EC%A0%9C%EC%9E%91%ED%95%98%EA%B8%B0-bfa32e6614c1
