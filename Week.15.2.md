## WSL
```
vi anu.c
i
```
(코딩)
ESC
Shift+zz
```
gcc gknu.c
./a.out
```
gcc -o main gknu.c
./main

## 두수 더하기
1. 함수 이용
2. 배열 이용
3. 구조체 이용
4. 키보드에서 읽어 더하기
5. 파일에서 읽어 더하기

```c
char** ch; // 이중 포인터

int main(int argc, char** argv){
or
int main(int argc, char* argv[]){
```
##### 명령행 매개 변수로 듀 수를 가감승제 계산기 프로그램을 작성하시오.
```c
#include <stdio.h>
#include <stdlib.h>

int main(int c, char** v){
  double n1 = atof(v[1]);
  char o =v[2][0];
  double n2 = atof(v[3]);
  double r=0.0;
  switch(o){
    case '+': r = n1 + n2; break;
    case '-': r = n1 - n2; break;
    case '*': r = n1 * n2; break;
    case '/': r = n1 / n2; break;
    default: return;
  }
  printf("%.2f %c %.2f = %.2f\n", n1, o, n2, r);
  return 0;
}
```
WSL에서 C언어를 컴파일 하기 까지의 과정을 자세히 적으시오
WSL을 관리자 권한으로 실행
```
gcc -o main main.c
./main

cc shim.c
./a.out
``` 
