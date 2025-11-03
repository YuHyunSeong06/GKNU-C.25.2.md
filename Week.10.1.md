# WSL 환경
## WSL 환경에서 두 수를 더하기
###### wsl -> nano test7.c
```c
#include <stdio.h> // printf();
#include <stdlib.h> // atoi(test 11 33) 11->11 atoi("11"); 11

void main(int argc, char* argv[]){
        int a,b,s;
        a = atoi(argv[1]);
        b = atoi(argv[2]);
        s = a + b;
        printf("%d\n",s);
}
```
##### more test7.c를 통해 코드 상태를 확인
##### gcc test7.c -> ./a.out 11 33 -> 44출력
##### gcc -o run test7.c -> ./run 11 33 -> 44출력
##### 두 가지 방식으로 사용이 가능하다

## swap 함수로 두 수를 교환하기
##### nano test.c
```c
#include <stdio.h> // printf();
#include <stdlib.h> // atoi(test 11 33) 11->11 atoi("11"); 11

void swap(int* a, int* b){ // 받을때는 포인터로 받기
        int p = *a;
        *a = *b;
        *b = p;
}

int main(void){
        int v[2]={11,33};
        swap(&v[0],&v[1]); // 보낼때는 주소로 보내기
        printf("%d %d\n",v[0],v[1]);
}
```
##### gcc -o run test7.c ./run test7.c -> 33 11 출력
