## 두 수를 더한다. /w, wb, w+

##### my.txt 파일에 두 수를 쓰고 더한 값을 출력하기
```c
#include <stdio.h>

int main() {
    int a, b;

    FILE* f = fopen("my.txt", "w"); // 파일 f 선언  my.txt파일을 쓰기 모드로 연다.
    fprintf(f, "%d\n%d\n", 22, 33);// 두 숫자를 선언한 파일 f 에 저장
    fclose(f);//파일 닫기기

    f = fopen("my.txt", "r"); // 파일 f 선언  my.txt파일을 읽기 모드로 연다.
    fscanf(f, "%d %d", &a, &b);// 파일에서 두 개의 숫자 읽기
    printf("%d\n", a + b);// 더한한 값 출력
    fclose(f); // 파일 닫기

    f = fopen("my.txt", "w"); // 파일 f 선언 my.txt 파일을 쓰기 모드로 연다.
    fprintf(f, "%d\n", a + b); // 더한 값을 f에 저장
    fclose(f); // 파일 닫기
    return 0;

}
```
