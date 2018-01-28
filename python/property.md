# property

클래스 변수에 접근할 때에 getter, setter를 사용하는 것은 일반적인 패턴이다.

그러나 코드가 과도하게 복잡해질 수 있는데 이에 대하여 파이썬은 property라는 니트한 솔루션을 제공한다.

```python
class Test:

  @property
  def name(self):
    return self.name

  @name.setter
  def name(self, val):
    self.name = val

>>> t = Test()
>>> t.name
>>> t.name = "asdf"
```
