## C언어 데이터형
##### 1. char -128 ~ 0 ~ 127 / 256개를 나타냄
##### 2. int
##### 3. float
##### 4. double
##### 5. unsigned int
##### 6. unsigned char 0 ~ 255 // 256개
##### 7. long int
##### 8. short int
##### 8. unsigned long int
##### sizeof(char);
##### sizeof(unsigned long int)
__________________________________________
### 배열 int v[60];
### 구조체 
```c
struct USER{
  int age;
  char name[20];
};
```
### 공용체(union) : 여러 멤버 변수가 같은 메모리 공간을 공유하도록 하는 자료형
##### 한 시점에는 오직 하나의 멤버만 유효한 값을 가짐
##### 구조체와의 차이
| 구분     | struct             | union                         |
| ------ | ------------------ | ----------------------------- |
| 메모리 구조 | 각 멤버가 **자기 공간** 가짐 | 모든 멤버가 **공유 공간** 사용           |
| 크기     | 멤버 크기의 **합**       | 멤버 중 **가장 큰 크기**              |
| 사용 목적  | 여러 데이터를 동시에 보관     | **서로 다른 형태의 데이터 중 하나만** 필요할 때 |
```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[10];
};

int main() {
    union Data data;

    data.i = 10;
    printf("data.i : %d\n", data.i);

    data.f = 220.5;
    printf("data.f : %.1f\n", data.f);

    // 이제 data.i 값은 덮어씌워져 의미가 없음
    printf("data.i : %d\n", data.i);

    return 0;
}
```
###### https://cafe.naver.com/jclang?iframe_url_utf8=%2FArticleRead.nhn%253Fclubid%3D30916880%2526articleid%3D359%2526referrerAllArticles%3Dtrue
참고
