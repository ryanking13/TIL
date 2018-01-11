# vtable

상속 관계에 있는 클래스들은 `virtual` 키워드를 통하여 함수를 오버라이딩할 수 있다.

다형성(polymorphism) 원리에 의하여 부모 클래스 포인터는 자식 클래스를 가리키고 있을 수도 있기 때문에, virtual 함수는 런타임에 여러 함수로 바뀔 수 있다.

이를 위하여 C++에서는 클래스 별로 `vtable` 이라는 것을 만들어 virtual 함수를 관리한다.

`vtable`은 자신, 상속 클래스와 연결된 virtual 함수 포인터를 기록한 테이블이다.

`vtable`의 주소를 가리키는 포인터는 클래스 인스턴스가 생성될 때에 클래스의 맨 앞 주소에 포함된다.

```c++
class B1 {
public:
  void f0() {}
  virtual void f1() {}
  int int_in_b1;
};

class B2 {
public:
  virtual void f2() {}
  int int_in_b2;
};

class D : public B1, public B2 {
public:
  void d() {}
  void f2() {}  // override B2::f2()
  int int_in_d;
};

B2 *b2 = new B2();
D  *d  = new D();
```

위와 같이 클래스를 정의하면,

```
b2:
  +0: pointer to virtual method table of B2
  +4: value of int_in_b2

virtual method table of B2:
  +0: B2::f2()   
```

B2의 인스턴스는 위와 같은 메모리 구조를 가지며,

```
d:
  +0: pointer to virtual method table of D (for B1)
  +4: value of int_in_b1
  +8: pointer to virtual method table of D (for B2)
 +12: value of int_in_b2
 +16: value of int_in_d

Total size: 20 Bytes.

virtual method table of D (for B1):
  +0: B1::f1()  // B1::f1() is not overridden

virtual method table of D (for B2):
  +0: D::f2()   // B2::f2() is overridden by D::f2()
```

D의 인스턴스는 위와 같은 메모리 구조를 가진다.
