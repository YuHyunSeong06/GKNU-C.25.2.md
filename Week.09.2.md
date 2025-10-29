## 명령프롬포트를 활용하여 코딩
##### cd \(경로 이동) -> mkdir anu -> cd anu -> notepad add.c
```c
int add(int a, int b){
  return a + b;
}
```
```c
int sub(int a, int b){
  return a - b;
}
```
```c
int mul(int a, int b){
  return a * b;
}
```
```c
int div(int a, int b){
  return a / b;
}
```
```c
#include <stdio.h>

int add(int, int);
int sub(int, int);
int mul(int, int);
int div(int, int);

void main(int argc, char* argv[]){
	int a,b;

	a=atoi(argv[1]);
	b=atoi(argv[2]);

	printf("%d\n",add(a,b));
	printf("%d\n",sub(a,b));
	printf("%d\n",mul(a,b));
	printf("%d\n",div(a,b));
}
```
