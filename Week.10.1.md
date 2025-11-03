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
##### ^x y enter를 통해 코드를 저장
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
##### gcc -o run test7.c -> ./run test7.c -> 33 11 출력
# 알고리즘 
##### 수학적 알고리즘, 누적합, 정렬, 탑색, 재귀 등 
##### https://cafe.naver.com/jclang?iframe_url_utf8=%2FArticleRead.nhn%253Fclubid%3D30916880%2526articleid%3D366%2526referrerAllArticles%3Dtrue
## psudo code 슈도 코드 
#### 이해하기쉽게 표현한 코드
##### 1부터 10까지 더하고 결과를 화면에 출력하는 슈도 코드
```
sum <- 0
for i <- 1 to 10
        sum <- sum + i
print sum
```
##### 1. 합계를 0으로 시작한다
##### 2. i를 1부터 10까지 하나식 늘려가며, 매번 합게에 i를 더한다.
##### 3. 반복이 끝나면 합계를 출력한다. (결과는 55)

## flow chart (순서도)
###### 타원형 : 시작과 끝
###### 마름모 : 판단
###### 사디리꼴, 아치형 : 출력

## 버블 소트
#### 이웃한 두 원소를 비교해가며 큰 값을 오른쪽 끝으로 떠올리는 (bubble up) 가장 기초적인 정렬 알고리즘
###### 1. 배열의 처음부터 끝까지 이웃한 쌍을 비교
###### 2. 왼쪽 값이 더 크면 두 값을 **교환**
###### 3. 한 바퀴(패스)가 끝나면 **가장 큰 값이 맨 끝**에 자리
###### 4. 끝에 확정된 부분을 제외하고 **남은 구간에 대해 반복**
###### 5. 어떤 패스에서 **교환이 한 번도 없으면** 이미 정렬된 것이므로 **조기 종료**
