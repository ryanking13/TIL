# double free bug practice

>  2018/02/12

---

[Protostar - heap3](https://exploit-exercises.com/protostar/heap3/)

```c
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/types.h>
#include <stdio.h>

void winner()
{
  printf("that wasn't too bad now, was it? @ %d\n", time(NULL));
}

int main(int argc, char **argv)
{
  char *a, *b, *c;

  a = malloc(32);
  b = malloc(32);
  c = malloc(32);

  strcpy(a, argv[1]);
  strcpy(b, argv[2]);
  strcpy(c, argv[3]);

  free(c);
  free(b);
  free(a);

  printf("dynamite failed?\n");
}
```

`strcpy`에서 오버플로우를 발생시켜서 푸는 문제다.

Allocated chunk는 아래와 같은 메모리 구조를 갖는다. (32bit 기준)

```
prev_chunk_size(4) + chunk_size(4) + data()
```

힙 메모리 할당은 8byte 단위로 이루어지므로, chunk_size의 하위 3비트는 노는 값이 되는데, 이를 활용하기 위하여 각각의 비트를 플래그로 사용한다.

```
chunk_size(4byte) = real_chunk_size(29) + A(1) + M(1) + P(1)
PREV_INUSE [P] : 이 비트는 이전 청크가 할당되면 설정됩니다.
IS_MMAPPED [M] : 이 비트는 현재 청크가 mmap을 통해 할당되면 설정됩니다.
NON_MAIN_ARENA [A] : 이 비트는 현재 청크가 thread arena에 위치되면 설정됩니다.
```

Free chunk는 아래와 같은 메모리 구조를 갖는다. (32bit 기준)

```
prev_chunk_size(4) + chunk_size(4) + fd(4) + bk(4)
```

Allocated chunk의 P 플래그는 이전 chunk가 free chunk인지 아닌지를 판단하며, 0(free)라면, 본 chunk가 free 될 때에 이전 chunk와 합친다 (unlink).

이를 이용하여 공격을 수행할 수 있다.

`strcpy(a, argv[1])` 부분에서 다음과 같이 overflow 시킨다면,

```
a_data(32) + b_prev_chunk_size(4) + b_chunk_size(4) + b_data()

A*32       + fffffffc(-4)         + fffffffc(-4)    + nop(4)    + new_fd(4) + new_bk(4)
```

b_chunk_size의 P 플래그가 0이므로 `free(b)`에서 unlink가 수행되는 데, 이 때 prev_chunk의 위치는 다음과 같이 계산된다.

```
b - b_prev_chunk_size = b + 4 byte
```

원래는 a를 가리켜야 할 것이, 오버플로우로 인하여 가짜 메모리(fake chunk)를 가리키게 되었다. new_fd, new_bk 값을 넣어줌으로써 우리가 원하는 메모리를 조작할 수 있게 되었다.

```
A*32       + fffffffc(-4)         + fffffffc(-4)    + nop(4)    + puts_got-0xc + winner
```

new_fd 부분에 puts_got-0xc를 넣어주면, unlink 과정에서 b->fd->bk = b->bk 가 되므로, puts의 got을 winner로 덮어 쓸 수 있다.

그러나, 이 방법은 문제가 있는데,

unlink는 b->bk->fd = b->fd 도 수행하는데, b->bk->fd 는 winner+0x8이고, 이는 .text 영역이기 때문에 쓰기가 불가능하다.

따라서, winner를 호출하는 쉘코드를 만들어서 그 공간을 bk 영역이 가르키게 하여야 한다.

쉘코드를 넣는 공간은 남아도는 a의 data영역을 사용하면 된다.

```
nop_slide + push winner + ret + fffffffc(-4)         + fffffffc(-4)    + nop(4)    + puts_got-0xc + a_data_space
```

### Reference

> http://itsaessak.tistory.com/136

> https://www.lazenca.net/pages/viewpage.action?pageId=1147929
