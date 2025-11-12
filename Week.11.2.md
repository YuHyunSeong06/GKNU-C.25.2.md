# 자료구조

typedef

변수: char, int float, double, long int, short int, unsigned int, unsigned long int, static, const

□ C에서 꼭 익혀야 하는 핵심 자료구조 5가지

​

1) 배열(Array) / 동적 배열

* 개념: 연속 메모리 블록. 인덱스로 O(1) 접근.

* 언제: 고정 크기·캐시 친화적 순차 데이터.

* 복잡도: 인덱스 `O(1)`, 끝 삽입(여유 有) `O(1)`, 중간 삽입/삭제 `O(n)`.

* 미니 예제
```c
#include <stdio.h>
int main(void){
    int a[5]={3,1,4,1,5};
    for(int i=0;i<5;i++) printf("%d ", a[i]); // 인덱스 O(1)
}
```
> 동적 배열은 `malloc/realloc`로 용량을 늘리며 관리합니다.

​

---

2) 단일 연결 리스트(Singly Linked List)

* 개념: 노드들이 포인터로 연결된 선형 구조.

* 언제: 중간 삽입/삭제가 자주, 크기 가변, 메모리 분산 허용.

* 복잡도: 맨앞 삽입/삭제 `O(1)`, 탐색 `O(n)`.

* 미니 예제

​
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct N { int x; struct N* next; } N;

N* push_front(N* head, int v){
    N* n = (N*)malloc(sizeof *n);
    n->x = v; n->next = head;
    return n;
}

void print(N* p){ for(; p; p=p->next) printf("%d ", p->x); puts(""); }

void free_all(N* p){ while(p){ N* q=p->next; free(p); p=q; } }

int main(void){
    N* head = NULL;
    head = push_front(head, 3);
    head = push_front(head, 2);
    head = push_front(head, 1);
    print(head);          // 출력: 1 2 3
    free_all(head);
    return 0;
}
```
3) 스택(Stack) — LIFO

* 개념: 마지막에 넣은 것을 먼저 꺼냄.

* 언제: 함수 호출 스택, DFS, 되돌리기(undo).

* 복잡도: `push/pop/top` 모두 `O(1)`.

* 배열 기반 미니 예제
```c
#include <stdio.h>

#define N 100
int a[N];
int top = 0;              // 스택의 다음 빈 칸(요소 개수와 같음)

int empty(void){ return top == 0; }
void push(int v){ a[top++] = v; }     // a[top]에 넣고 top 증가
int pop(void){ return a[--top]; }     // top 줄이고 a[top]을 반환

int main(void){
    push(10); push(20);
    printf("%d %d\n", pop(), pop());  // 20 10
    return 0;
}
​

#include <stdio.h>
#define N 100
typedef struct { int a[N]; int top; } Stack;

void init(Stack* s){ s->top=0; }
int empty(Stack* s){ return s->top==0; }
void push(Stack* s,int v){ s->a[s->top++]=v; }
int pop(Stack* s){ return s->a[--s->top]; }

int main(void){
    Stack s; init(&s); push(&s,10); push(&s,20);
    printf("%d %d\n", pop(&s), pop(&s)); // 20 10
}
```
---

​

## 4) 큐(Queue) — FIFO (원형 큐)

​

* **개념**: 먼저 넣은 것을 먼저 꺼냄.

* **언제**: BFS, 작업 대기열, 프로듀서-컨슈머.

* **복잡도**: `enqueue/dequeue/front` 모두 `O(1)`.

* **원형 배열 미니 예제**

​
```c
#include <stdio.h>
#define N 8
typedef struct { int a[N]; int f,r,c; } Queue; // front, rear, count
void initQ(Queue* q){ q->f=q->r=q->c=0; }
int full(Queue* q){ return q->c==N; }
int emptyQ(Queue* q){ return q->c==0; }
void enq(Queue* q,int v){ q->a[q->r]=v; q->r=(q->r+1)%N; q->c++; }
int deq(Queue* q){ int v=q->a[q->f]; q->f=(q->f+1)%N; q->c--; return v; }

int main(void){
    Queue q; initQ(&q); enq(&q,1); enq(&q,2); printf("%d %d\n", deq(&q), deq(&q));
}
```
---

## 5) 이진 트리 (binary tree)
```c
#include <stdio.h>
#include <stdlib.h>

/* 이진 트리 노드 */
typedef struct Node {
    int data;
    struct Node* left;
    struct Node* right;
} Node;

/* 새 노드 생성 */
static Node* make_node(int value) {
    Node* n = (Node*)malloc(sizeof(Node));
    if (!n) { perror("malloc"); exit(1); }
    n->data = value;
    n->left = NULL;   // 왼쪽 자식(없으면 NULL)
    n->right = NULL;  // 오른쪽 자식(없으면 NULL)
    return n;
}
```
/* 중위 순회: (왼) -> (자기) -> (오) */
```c
void inorder(const Node* r) {
    if (!r) return;
    inorder(r->left);
    printf("%d ", r->data);
    inorder(r->right);
}

/* 전체 해제 */
void free_tree(Node* r) {
    if (!r) return;
    free_tree(r->left);
    free_tree(r->right);
    free(r);
}

int main(void) {
    /* 가장 단순한 트리: 3노드
           2
          / \
         1   3
       (NULL 잎 포함)
    */
    Node* root = make_node(2);              // 루트 2 (left=NULL, right=NULL)
    root->left  = make_node(1);             // 왼쪽 1  -> (left=NULL, right=NULL)
    root->right = make_node(3);             // 오른쪽 3 -> (left=NULL, right=NULL)

    printf("Inorder: ");
    inorder(root);                           // 1 2 3
    printf("-> NULL\n");

    free_tree(root);
    return 0;
}
​```
```
## 6) 해시 테이블(Hash Table) — 체이닝 방식

​

* **개념**: 해시함수로 버킷 선택, 충돌은 연결 리스트로 처리.

* **언제**: 평균 `O(1)` 키-값 조회/삽입이 필요할 때.

* **복잡도**(평균): 삽입/검색/삭제 `O(1)`; 최악 `O(n)`.

* **미니 예제**(아주 단순화)

​
