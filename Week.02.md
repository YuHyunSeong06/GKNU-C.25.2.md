## 개발자 명령 프롬포트를 이용한 코드
###### 25.09.03 첫번째 수업

##### 도구 -> 명령줄 -> 개발자 명령 프롬포트
##### 덧셈 함수 선언
```
notepad add.c // 텍스트 파일 생성
```
```c
int add(int a,int b){
     return a+b;
}
```
##### 뺄셈 함수 선언
```
notepad sub.c // 텍스트 파일 생성
```
```c
int sub(int a, int b){
     return (a-b);
}
```
##### 각각의 함수 코드 컴파일 및 라이브러리 생성
```
cl /c add.c
cl /c sub.c
// C/C++ 최적화 컴파일러

lib /OUT:my.lib add.obj sub.obj // 라이브러리 생성
dir my.lib // 라이브러리 디렉터리 확인

notepad main.c
```
##### main코드 선언
```c
#include <stdio.h>

int add(int,int);

int sub(int,int);

void main(){
     printf("%d\n",add(2,3));
     printf("%d\n",sub(2,3));
}
```
##### 컴파일
```
cl main.c my.lib // 컴파일
main.exe // 실행
```
##### 퀴즈시험
##### cl /c add.c sub.c // 컴파일
##### lib /OUT:my.lib add.obj sub.obj // lib 만들기
##### cl main.c my.lib // 링크해서 exe 파일 만들기

#### https://github.com/jcshim/deepc/blob/main/01_c_in_linux.md 다음 링크 참고

## WSL(Windows Subsystem for Linux)
#### https://github.com/jcshim/deepc/blob/main/01_wsl.md 다음 링크 참고
##### WSL은 윈도우에서 리눅스를 쉽게 실행해서 개발·학습·테스트에 활용할 수 있는 가볍고 강력한 도구
##### WSL을 관리자 권한으로 실행 후
```
~$ sudo apt-get update
```
##### WSL이 실행되지 않는경우
###### Window powershell 에서 wsl --install

## 개발자 명령 프롬포트를 활용한 심화
##### 명령줄을 통해 계산하는 코드 선언
```
notepad lab1.c
```
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
    }
    printf( "%d%c%d=%d\n", a, ch, b, c );
}
```
##### 컴파일 및 실행
```
cl lab1.c
lab1 30 + 20
30+20=50
```



