# Diffie-Hellman 키 교환

> 2018/03/06 - init

암호키를 교환하는 방식 중 한가지.

앨리스와 밥이 통신하는 상황에서,

1. 앨리스가 정수 `p`와 1 ~ p-1 사이의 정수 `g`를 정하여 밥에게 알려준다.
2. 앨리스와 밥은 각각 혼자만 알고 있는 정수 `a`와 `b`를 정한다.
3. 앨리스는 `A` = `g^a mod p`, 밥은 `B` = `g^b mod p`를 계산하고 서로에게 알려준다.
4. 앨리스는 `B^a mod p` =  `(g^b mod p)^a mod p` = `g^ab mod p`를 계산하여 얻는다.
5. 밥은 `A^b mod p` = `(g^a mod p)^b mod p` = `g^ab mod p`를 계산하여 얻는다.
6. `g^ab mod p`가 비밀키 `s`가 된다.

중간자가 있더라도 `a`, `b`를 알 수 없으므로 비밀키를 알 수 없다.

---

### Reference

> https://ko.wikipedia.org/wiki/%EB%94%94%ED%94%BC-%ED%97%AC%EB%A8%BC_%ED%82%A4_%EA%B5%90%ED%99%98
