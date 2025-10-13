## WSL 환경에서 C언어를 컴파일하기

##### WSL 환경에서 첫번째로 해야할것
```wsl
ubuntu
~$ sudo apt-get update
~$ sudo apt-get update -y
```
##### 
```Linux
mkdir anu
cd anu
nano main.c
```
```Linux
ls
./a.out
gcc -o main main.c
./ main
```
```c
#include <stdio.h>
int add(int, int)
void main(){
  int a=22, b=33;
  printf("%d\n",add(a,b));
}
```
```
nano add.c
gcc -c *.c
gcc -o main main.o add.o
./main
```
```

