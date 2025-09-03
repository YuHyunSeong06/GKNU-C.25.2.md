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

##### https://github.com/jcshim/deepc/blob/main/01_c_in_linux.md 다음 링크 참고

##### WSL을 관리자 권한으로 실행
##### WSL이 실행이 안될때




