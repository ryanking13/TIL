# extern "C"

소스 파일을 컴파일 할 때 글로벌 변수, 함수 등을 가리키기 위한 심볼이 생성된다.

C의 경우 함수의 이름이 유니크하기 때문에 함수명을 그대로 사용하거나, 앞에 언더스코어(`_`)를 붙이는 식으로 심볼을 정할 수 있다.

그러나 C++에서는 overloading, overriding에 의해서 같은 이름의 함수가 여럿 존재할 수 있으므로 심볼을 정하는 데 있어서 특정한 규칙이 필요해진다.

이러한 과정을 네임 맹글링(name mangling)이라고 하는데, 이는 특정한 규약 없이 컴파일러마다 서로 다르게 구현된다.

네임 맹글링의 문제는 컴파일된 C++ 코드를 C 코드와 링크(link)하려 할 때 발생하는데, 정해진 규약이 없으므로 함수의 심볼을 알 수 있는 방법이 없다.

따라서 C++ 코드를 작성할 때, 네임 맹글링을 하지 않고 C와 같은 방식으로 컴파일 되도록 지정할 수 있는데, 이 때 extern "C" 키워드를 사용한다.

```c++
// specifying_linkage2.cpp  
// compile with: /c  
// Declare printf with C linkage.  
extern "C" int printf( const char *fmt, ... );  

//  Cause everything in the specified header files  
//   to have C linkage.  
extern "C" {  
   // add your #include statements here  
   #include <stdio.h>  
}  

//  Declare the two functions ShowChar and GetChar  
//   with C linkage.  
extern "C" {  
   char ShowChar( char ch );  
   char GetChar( void );  
}  

//  Define the two functions ShowChar and GetChar  
//   with C linkage.  
extern "C" char ShowChar( char ch ) {  
   putchar( ch );  
   return ch;  
}  

extern "C" char GetChar( void ) {  
   char ch;  

   ch = getchar();  
   return ch;  
}  

// Declare a global variable, errno, with C linkage.  
extern "C" int errno;
```
