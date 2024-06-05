### 스택 구현 ###
```
#include<stdio.h>
#include<stdlib.h> //동적 메모리 할당 및 유틸리티 함수를 사용하기 위해 포함

#define MAX 100 //스택의 최대 크기를 100으로 정의

//스택 구조체의 정의

typedef struct { //새로운 구조체 타입을 정의
    int top; // 스택의 가장 상단 요소의 인덱스를 저장
    int items[MAX]; //스택 요소들을 저장할 배열
} Stack;

//스택 초기화

void initStack(Stack *s) { //스택을 초기화하는 함수
    s->top = -1; //스택이 비어있음을 나타내기 위해 top을 -1로 설정
}

//스택이 비어있는지 확인

int isEmpty(Stack *s) { //스택이 비었는지 확인하는 함수
    return s->top == -1; //top이 -1이면 스택이 비어있음을 의미
}

//스택이 비어있는지 확인

int isFull(Stack *s) { //스택이 비었는지 확인하는 함수
    return s->top == MAX - 1; //top이 -1이면 스택이 비어있음을 의미
}

//스택에 요소를 추가

void push(Stack *s, int item) { //스택에 요소를 추가하는 함수
    if(isFull(s)) { //스택이 가득 찼는지 확인
        printf("Stack is full\n");
    } else {
        s->items[++s->top] = item; //top을 증가시키고 새로운 요소를 추가
    }
}

//스택에서 요소를 제거

int pop(Stack *s) { //스택에서 요소를 제거하는 함수
    if(isEmpty(s)) { //스택이 비었는지 확인
        printf("Stack is empty\n");
        return -1; // 에러 값을 반환
    } else {
        return s->items[s->top--]; //현재 top 요소를 반환하고 top을 감소
    }
}

//스택의 최상단 요소를 확인

int peek(Stack *s) { //스택의 최상단 요소를 확인하는 함수
    if(isEmpty(s)) { //스택이 비었는지 확인
        printf("Stack is empty\n");
        return -1; // 에러 값을 반환
    } else {
        return s->items[s->top]; //현재 top 요소를 반환
    }
}

```

### 큐 구현 ###
```
#include<stdio.h>
#include<stdlib.h>

#define MAX 100

//큐 구조체 정의

typedef struct { //새로운 구조체 타입을 정의.
    int items[MAX]; //큐 요소들을 저장할 배열.
    int front; //큐의 첫 번째 요소의 인덱스를 저장.
    int rear; //큐의 마지막 요소의 인덱스를 저장.
} Queue;

//큐 초기화

void initQueue(Queue *q) { //큐를 초기화하는 함수.
    q->front = -1; //큐가 비어있음을 나타내기 위해 front를 -1로 설정.
    q->rear = -1; //큐가 비어있음을 나타내기 위해 rear를 -1로 설정.
}

//큐가 비었는지 확인

int isEmpty(Queue *q) { //큐가 비었는지 확인하는 함수.
    return q->rear == q->front; //front가 -1이면 큐가 비어있음을 의미.
}

//큐가 가득 찼는지 확인

int isFull(Queue *q) { //큐가 가득 찼는지 확인하는 함수.
    return q->rear == MAX - 1; //rear가 MAX - 1이면 큐가 가득 찼음을 의미.
}

//큐에 요소를 추가

void enqueue(Queue *q, int item) { //큐에 요소를 추가하는 함수.
    if(isFull(q)) { //큐가 가득 찼는지 확인.
        printf("Queue is full\n");
    } else {
        if (q->front == -1) //큐가 비어있으면 front를 0으로 설정.
            q->front = 0;
        q->items[++q->rear] = item; //rear를 증가시키고 새로운 요소를 추가.
    }
}

//큐에서 요소를 제거

int dequeue(Queue *q) { //큐에서 요소를 제거하는 함수.
    if (isEmpty(q)) { //큐가 비었는지 확인.
        printf("Queue is empty\n");
        return -1; // 오류 값을 반환
    } else {
        int item = q->items[q->front]; //front의 요소를 저장.
        if (q->front >= q->rear) { //큐가 비어있는지 확인.
            q->front = -1; //큐가 비어있으면 front와 rear를 -1로 설정.
            q->rear = -1; //제거된 요소를 반환.
        } else {
            q->front++; //// front를 증가시켜 다음 요소를 가리킴.
        }
        return item;
    }
//큐의 첫 번째 요소를 확인

}
int peek(Queue *q) { //큐의 첫 번째 요소를 확인하는 함수
    if (isEmpty(q)) { //큐가 비었는지 확인.
        printf("Queue is empty\n");
        return -1; // 오류 값을 반환
    } else {
        return q->items[q->front]; //front의 요소를 반환.
    }
}
```
