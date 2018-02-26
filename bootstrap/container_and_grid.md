# container and grid

> 2018/02/26 - init

### Containers

Bootstrap에서 페이지에 표시된 content를 wrap하고, grid system을 적용하기 위하여 `container` 클래스를 사용한다.

```html
<div class="container">
<div class="container-fluid">
```

`container` 클래스에는 `.container` 와 `.container-fluid`가 있는데, 전자의 경우 pre-defined된 고정 width이고, 후자의 경우 페이지 width에 맞춰서 늘어난다.

### Grid system

content를 나열하기 위한 Grid system은 `container` 아래에 `.row`-`.col-x-n`를 배치하는 방식을 사용한다.

```html
<div class="row">
  <div class="col-md-6">.col-md-6</div>
  <div class="col-md-6">.col-md-6</div>
</div>
```

`.col-x-n`에서 x에 들어가는 값은 디바이스의 width에 따라 배치를 다르게 하는 데에 사용된다. (sm을 사용할 경우 sm 기준보다 큰 모든 디바이스에 적용된다.)

  - xs - auto
  - sm - small (750px)
  - md - medium (970px)
  - lg - large (1170px)

n에 들어가는 값은 content가 얼마만큼의 span를 차지하는 가를 나타낸다. 한 줄은 12 만큼의 span을 가진다. ([그림](https://www.w3schools.com/bootstrap/bootstrap_grid_basic.asp))

```html
<div class="row">
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
  <div class="col-xs-6 col-sm-3">.col-xs-6 .col-sm-3</div>
</div>
```

위와 같이 지정할 경우, 아주 작은 디바이스에서는 row당 2개, 일정 크기 이상의 디바이스에서는 row당 4개의 content가 표시된다.

---

### Reference

> https://getbootstrap.com/docs/3.3/css/
