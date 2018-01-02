# Double Free Bug

Double Free Bug, 또는 free()함수의 unlink 과정에서 발생하기 때문에 unlink corruption이라고도 부른다.

heap의 free chunk는 다음과 같은 메모리 구조로 구성되어있다.

    --malloc.c         #malloc 자료구조
    /*
      Type declarations
    */
    struct malloc_chunk
    {
      INTERNAL_SIZE_T prev_size; /* Size of previous chunk (if free). */
      INTERNAL_SIZE_T size;      /* Size in bytes, including overhead. */
      struct malloc_chunk* fd;   /* double links -- used only if free. */
      struct malloc_chunk* bk;
    };

| Memory Structure     |
| :------------- |
| pre-block size       |
| block size       |
| fd pointer       |
| bk pointer       |

fd, bk 포인터는 각각 앞, 뒤 free chunk의 주소를 가리키고 있다.

unlink 매크로는 다음과 같이 구현된다.

    #define unlink(P, BK, FD)                                                     
    {                                                                             
      BK = P->bk;                                                                 
      FD = P->fd;                                                                 
      FD->bk = BK;                                                                
      BK->fd = FD;                                                                
    }

따라서 fd와 bk에 원하는 값을 넣을 수 있다면, 원하는 메모리 주소에 원하는 값을 쓰는 것이 가능해진다.

예를 들어,

    block->fd = &ret_address-12
    block->bk = &addr
    addr+8 = shellcode

위와 같이 페이로드를 구성하면, unlink 시에 리턴 어드레스가 쉘 코드를 덮어쓰게 된다.

---

Reference

http://www.hackerschool.org/HS_Boards/data/Lib_system/doublefree.txt
