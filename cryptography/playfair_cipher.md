# Playfair cipher algorithm

> 1/28: init

Playfair cipher 알고리즘은 1854년에 만들어졌다.

알파벳 문자열 암호화에 사용되며, 5x5 공간에 패드를 만들어 암호화하느 방식이다.

키 값을 사용하지 않을 경우에는, J를 제외한 나머지 문자로 (혹은 I를 제외하기도 한다) 알파벳 순서대로 패드를 채우고,

키를 사용하는 경우 키를 먼저 패드에 채우고 사용하지 않은 나머지 알파벳을 알파벳 순서대로 채운다.

![](https://upload.wikimedia.org/wikipedia/commons/e/ef/Playfair_Cipher_building_grid_omitted_letters.png)

PLAYFAIREXAMPLE을 키로 사용한 예.


그리고 암호화 시키고자 하는 평문을 두 글자 단위로 나누고,

각 글자가 패드에서 어떤 위치 관계에 존재하느냐에 따라 다른 암호화 방식을 적용한다.

1. 대각선 위치에 존재하는 경우
1. 같은 행에 존재하는 경우
1. 같은 열에 존재하는 경우

---

1. 대각선 위치에 존재하는 경우

![](https://upload.wikimedia.org/wikipedia/commons/f/fb/Playfair_Cipher_04_EG_to_XD.png)

두 글자를 감싸는 직사각형을 만들고, 직사각형의 맡은 편 꼭짓점에 위치하는 글자로 바꾼다.

2. 같은 행, 열에 존재하는 경우

![](https://upload.wikimedia.org/wikipedia/commons/4/44/Playfair_Cipher_02_DE_to_OD.png)

![](https://upload.wikimedia.org/wikipedia/commons/2/29/Playfair_Cipher_10_EX_to_XD.png)

옆으로 한 칸씩 쉬프트한다.

---

위는 일반적인 경우고 쉬프트 방향이나 그 외 여러 방법에서 구현하기 나름인 듯,

ROT13이 꼭 13자리 쉬프트를 할 이유가 없는 것처럼 쉽게 쉽게 변종을 만들어낼 수 있는 것 같다.

---

### Reference

https://en.wikipedia.org/wiki/Playfair_cipher

http://rumkin.com/tools/cipher/playfair.php
