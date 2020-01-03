# Competitive Programming with go

> 2019/01/03

Go로 Competitive Programming (a.k.a. PS) 하기

## I/O

### Input

> __TL;DR__ <br> `fmt.Scanf` 보다는 `fmt.Scan` 보다는 `fmt.Fscan`

C-style `scanf`에 익숙한 사람이라면 `fmt.Scanf`를 쓰고 싶을테지만,
Go의 `Scanf` 계열은 newline(`\n`)을 whitespace로 무시하지 않고 읽어들인다.

```
// https://golang.org/pkg/fmt/#hdr-Scanning
The handling of spaces and newlines differs from that of C's scanf family: in C, newlines are treated as any other space, and it is never an error when a run of spaces in the format string finds no spaces to consume in the input.
```

따라서, `fmt.Scanf`는 여러 줄을 읽어들일 때 생각한 것과 다른 동작을 할 가능성이 높다.

```go
package main

import "fmt"

func main() {
	var a, b int
	/* [Input]
	1
	2
	*/
	fmt.Scan("%d%d", &a, &b)
	fmt.Printf("%d %d\n", a, b)

	/* [Output Expected]
	1 2
	*/

	/* [Ouput Real]
	1 0
	*/
}
```

여러 줄을 읽고자 한다면 대신 `fmt.Scan`을 쓰자.

```go
package main

import "fmt"

func main() {
	var a, b int
	/* [Input]
	1
	2
	*/
	fmt.Scan(&a, &b)
	fmt.Printf("%d %d\n", a, b)

	/* [Output]
	1
	2
	*/
}
```

한편, 많은 줄을 읽어들여야 하는 경우라면 `fmt.Scan`은 버퍼링을 하지 않아 느리다.

그래서 `bufio` 패키지와 `fmt.Fscan`을 활용해주어야 한다.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"time"
)

func main() {
    a := make([]int, 100000, 100000)
    /* [Input]
	1
    1
    ...
    1
	*/
	start := time.Now()
	for i := 0; i < 100000; i = i + 1 {
		fmt.Scan(&a[i])
	}
	fmt.Printf("fmt.Scan: %v\n", time.Since(start))

	start = time.Now()
	r := bufio.NewReader(os.Stdin)
	for i := 0; i < 100000; i = i + 1 {
		fmt.Fscan(r, &a[i])
	}
	fmt.Printf("fmt.Fscan: %v\n", time.Since(start))
}

```

```
fmt.Scan: 502.6522ms
fmt.Fscan: 28.924ms
```

입력의 형태에 따라 다르겠지만 `bufio`를 활용하는 것이 훨씬 빠른 것을 확인할 수 있다.

__(+) 한 줄 읽기__

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	r := bufio.NewReader(os.Stdin)
	s, _ := r.ReadString('\n')
	fmt.Print(s)
}
```