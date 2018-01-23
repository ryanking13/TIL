# Special Method Names in python

파이썬 클래스에서 미리 이름이 정의된 메소드 중 일반적인 것들을 정리한 문서

### Constructor, Destructor

| Declared     | When Called     |
| :------------- | :------------- |
| x.\_\_init\_\_()       | x = Class()       |
| x.\_\_new\_\_() | x = Class() |
| x.\_\_del\_\_() | del x |

\_\_new\_\_() 는 클래스를 인자로 받아서 인스턴스를 생성하는 데 사용되고,

\_\_init\_\_() 은 인스턴스가 생성된 후에 호출된다.

\_\_del\_\_() 은 유저가 의도적으로 del을 호출하거나, 가비지 컬렉터에 의하여 객체가 소멸하기 전에 호출된다.


### Attributes

| Declared     | When Called     |
| :------------- | :------------- |
| x.\_\_getattribute\_\_('property')       | x.property       |
| x.\_\_getattr\_\_('property') | x.property |
| x.\_\_setattr\_\_('property', value) | x.property = value |
| x.\_\_delattr\_\_('property') | del x.property |
| x.\_\_dir\_\_() | dir(x) |

\_\_getattribute\_\_()는 객체의 attribute, method를 참조할 때 호출된다.

\_\_getattr\_\_()는 존재하지 않는 attribute를 참조할 때 호출된다.

```python
class Dynamo:
    def __getattr__(self, key):
        if key == 'color':         
            return 'PapayaWhip'
        else:
            raise AttributeError   

>>> dyn = Dynamo()
>>> dyn.color                      
'PapayaWhip'
>>> dyn.color = 'LemonChiffon'
>>> dyn.color                      
'LemonChiffon'
```

\_\_dir\_\_() 은 최상위 클래스에 정의되어 있으며 객체의 attribute, method 리스트를 반환하는데, 오버라이딩하여 사용할 수도 있다.

### Class like iterable

| Declared     | When Called     |
| :------------- | :------------- |
| x.\_\_iter\_\_()       | iter(x)       |
| x.\_\_next\_\_() | next(x) |

```python
for i in x:
    i.doSomething()
```

\_\_iter\_\_()와 \_\_next\_\_()가 정의되면 객체는 Iterable이 되고, for와 같은 구문에서 사용할 수 있다.


### Class like function

| Declared     | When Called     |
| :------------- | :------------- |
| x.\_\_call\_\_()       | x() |

\_\_call\_\_()을 정의하면 클래스를 함수처럼 호출할 수 있다.

이를 이용하여 클래스형 데코레이터를 사용할 수도 있다.

### Class like set

| Declared     | When Called     |
| :------------- | :------------- |
| x.\_\_len\_\_()       | len(x) |
| x.\_\_contains\_\_(a)       | a in x |

### Class like dictionary

| Declared     | When Called     |
| :------------- | :------------- |
| x.\_\_getitem\_\_(key)       | x[key] |
| x.\_\_setitem\_\_(key, value)       | x[key] = value |

---

### Reference

http://www.diveintopython3.net/special-method-names.html
