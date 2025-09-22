## 퀴즈시험

##### 1. 프람프트에서 명령행 매개 변수로 +, -, *, / 를 구현하는 소스코드를 적으시오
ex)calc 10+20
```c
#include <stdio.h>
#include <stdlib.h>

int main( int argc, char*argv[] ) // main() 안에 있는 매개변수는 
{
    int a, b, c;
    char ch;
    a = atoi( argv[ 1 ] );
    b = atoi( argv[ 3 ] );
    ch = argv[ 2 ][ 0 ];
    switch( ch )
    {
         case '+' : c = a + b; break;
         case '-' : c = a - b; break;
         case '*' : c = a * b; break;
         case '/' : c = a / b; break;
    }
    printf( "%d%c%d=%d\n", a, ch, b, c );
}
```
