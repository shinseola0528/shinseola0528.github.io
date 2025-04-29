---
layout: post
title: "[2024년 2회] 정보처리기사 실기 복원 문제 정리"
date: 2025-04-21 12:00:00 +0900
categories: 정보처리기사
tags: [정보처리기사, 실기, 기출문제, 복원문제]
layout: single
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

> 원본: [초보몽키 블로그 - 2024년 2회 정보처리기사 실기](https://chobopark.tistory.com/483)



### 1번 문제

**다음 Java 코드를 읽고 출력되는 결과를 작성하시오.**

```java
class Main {
    public static void main(String[] args) {
        int[] a = new int[]{1, 2, 3, 4};
        int[] b = new int[]{1, 2, 3, 4};
        int[] c = new int[]{1, 2, 3};

        check(a, b);
        check(a, c);
        check(b, c);
    }

    public static void check(int[] a, int[] b) {
        if (a == b) {
            System.out.print("O");
        } else {
            System.out.print("N");
        }
    }
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
Java에서 배열은 참조 타입이기 때문에 a == b는 주소 비교이다. 서로 다른 객체이므로 모두 false가 되어 "N"이 3번 출력된다.
<br><br>
<strong>정답</strong>: NNN
</details>
<br><br>

### 2번 문제

**다음 문제에서 설명하는 용어를 작성하시오.**

데이터를 중복시켜 성능을 향상시키기 위한 기법으로 데이터를 중복 저장하거나 

테이블을 합치는 등으로 성능을 향상시키지만 데이터 무결성이 저하될 수 있는 기법

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
정규화를 일부 해제하는 방식으로 성능을 높이는 대신 무결성이 떨어질 수 있음.
<br><br>
<strong>정답</strong>: 반정규화
</details>
<br><br>
### 3번 문제

아래 SQL의 빈칸에 들어갈 키워드를 작성하시오.

```sql
테이블

사원 [사원번호(PK), 이름, 나이, 부서]
부서 [사원번호(PK), 이름, 주소, 나이]

 
신입 사원이 들어와서 사원 테이블에 추가
INSERT INTO 사원 (사원번호, 이름, 주소, 부서)   [      ①     ] (32431, '정실기', '서울', '영업');
 

위에 신입사원을 검색하면서 부서 테이블에 추가
INSERT INTO 부서 (사원번호, 이름, 나이, 부서)
[    ②     ] 사원번호, 이름, 나이, 23 FROM 사원 WHERE 이름 = '정실기';


전체 사원 테이블 조회
SELECT  *   [    ③   ]   사원;


퇴사로 인해 부서에 해당하는 값을 '퇴사'로 변경
UPDATE 사원   [      ④     ]   부서  =  '퇴사'  WHERE 사원번호  = 32431;
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
SQL 기본 구문인 INSERT VALUES, INSERT SELECT, SELECT FROM, UPDATE SET의 사용 위치 문제이다.
<br><br>
<strong>정답</strong>:<br>
① VALUES<br>
② SELECT<br>
③ FROM<br>
④ SET
</details>
<br><br>
### 4번 문제

주어진 릴레이션 테이블을 보고 Cardinality와 Degree를 작성하시오.
![4.png](../../images/2025-04-21-jeongbochuli-silgi-2024-2nd/4.png)
![4](../../images/2025-04-21-jeongbochuli-silgi-2024-2nd/4.png)


Cardinality: (   ①   )<br>
Degree: (   ②   )

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
Cardinality는 행(Row)의 개수, Degree는 열(Attribute)의 개수이다.
<br><br>
<strong>정답</strong>:<br>
Cardinality: 5<br>
Degree: 4
</details>
<br><br>
### 5번 문제

**다음은 프로토콜에 대한 내용이다. 아래 내용을 읽고 알맞는 답을 작성하시오.**

\- Network layer에서 IP패킷을 암호화하고 인증하는 등의 보안을 위한 표준이다. <br>
\- 기업에서 사설 인터넷망으로 사용할 수 있는 VPN을 구현하는데 사용되는 프로토콜이다.<br>
\- AH(Authentication Header)와 ESP(Encapsulating Security Payload)라는 두 가지 보안 프로토콜을 사용한다.

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
IPSec은 네트워크 계층에서 IP 패킷을 암호화하고 인증하여 데이터 통신의 보안을 확보하는 표준이다.  
VPN을 구축할 때 사용되며, AH를 통한 인증과 ESP를 통한 암호화를 지원하여 강력한 보안을 제공한다.<br>
<strong>정답</strong>: IPSec
</details>
<br><br>
### 6번 문제

**다음은 Python에 대한 문제이다. 아래 코드를 읽고 알맞는 출력 값을 작성하시오.**

```python
def fnCalculation(x,y):
    result = 0;
    for i in range(len(x)):
     temp = x[i:i+len(y)] 
     if temp == y:
       result += 1;
    return result
 
a = "abdcabcabca"
p1 = "ab";
p2 = "ca";
 
out = f"ab{fnCalculation(a,p1)}ca{fnCalculation(a,p2)}"
print(out)
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
문자열 `a`에서 길이가 `len(p1)` 또는 `len(p2)`인 부분 문자열을 슬라이딩하며, `p1` 또는 `p2`와 일치하는 횟수를 센다.  
"ab"는 3번 등장하고, "ca"도 3번 등장하여 결과 문자열은 "ab3ca3"이 된다.
<br><br>
<strong>정답</strong>: ab3ca3
</details>
<br><br>
### 7번 문제

**아래 설명하는 내용을 확인하여 알맞는 알고리즘을 작성하시오.**

\- 대칭키 알고리즘으로 1997년 NIST(미국 국립기술표준원)에서 DES를 대체하기 위해 생성되었다.
\- 128비트, 192비트 또는 256비트의 가변 키 크기와 128비트의 고정 블록 크기를 사용한다.
\- 높은 안전성과 효율성, 속도 등으로 인해 DES 대신 전 세계적으로 많이 사용되고 있다.

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
DES를 대체하기 위해 선정된 대칭키 블록 암호 알고리즘으로, Rijndael 알고리즘이 AES로 표준화되었다.  
128, 192, 256비트의 키 길이와 128비트 고정 블록 크기를 갖고, 보안성과 속도 면에서 우수하여 널리 사용된다.
<br><br>
<strong>정답</strong>: AES
</details>
<br><br>
### 8번 문제

**패킷 교환 방식 중에 연결형과 비연결형에 해당하는 방식을 작성하시오.** 

① 연결형 교환 방식

② 비연결형 교환 방식

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
연결형은 데이터 전송 전에 연결을 설정하고, 전송 순서를 보장하며 수신 확인을 통해 신뢰성을 확보하는 방식이다.  
비연결형은 연결 설정 없이 데이터를 전송하며 속도는 빠르지만 순서 보장이나 오류 제어는 없다.
<br><br>
<strong>정답</strong>:<br>
① TCP<br>
② UDP
</details>
<br><br>
### 9번 문제

**아래 내용을 확인하고 보기에서 알맞는 답을 고르시오.**

실행 순서가 밀접한 관계를 갖는 기능을 모아 모듈로 구성한다.
한 모듈 내부의 한 기능 요소에 의한 출력 자료가 다음 기능 원소의 입력 자료로서 제공되는 형태이다.



**보기**

ㄱ. 기능적(functional)			ㄴ. 우연적(Coincidental)			ㄷ. 통신적(Communication)
ㄹ. 절차적(Procedural)			ㅁ. 시간적(Temporal)				ㅂ. 순차적(sequential)			     ㅅ.  논리적(Logical)

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
기능 간 순서와 흐름이 중요하고, 한 기능의 출력이 다음 기능의 입력으로 사용되는 구조는 <strong>순차적 응집도</strong>에 해당한다.  
이는 모듈 내의 요소들이 순서에 따라 실행되며, 데이터 흐름이 존재하는 형태이다.
<br><br>
<strong>정답</strong>: ㅂ. 순차적(sequential)
</details>
<br><br>
### 10번 문제

**아래는 디자인 패턴에 관한 설명이다. 아래 설명을 읽고 보기에서 알맞는 용어를 작성하시오.**

\- 컬렉션 객체의 내부 구조를 노출하지 않고 순차적으로 접근할 수 있게 하는 패턴이다.   
\- 이 패턴은 객체의 내부 표현 방식에 독립적으로 요소에 접근할 수 있도록 해준다  
\- 반복 프로세스를 캡슐화하여 클라이언트 코드에서는 컬렉션의 구체적인 구현에 종속되지 않도록 한다.

**보기**

| 생성패턴             | 구조패턴      | 행위패턴     |
| ---------------- | --------- | -------- |
| Singleton        | Adapter   | Iterator |
| Factory Method   | Bridge    | Visitor  |
| Abstract Factory | Composite | Observer |

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
Iterator 패턴은 컬렉션 내부 구조를 외부에 노출하지 않고 순차적으로 접근할 수 있도록 한다.  
이를 통해 클라이언트가 반복 처리를 수행할 때 컬렉션의 구체적인 구현 방식에 의존하지 않게 된다.
<br><br>
<strong>정답</strong>: Iterator
</details>
<br><br>
### 11번 문제

**아래 그림을 바탕으로 RIP을 구성하여 최단 경로 비용을 계산하여 흐름에 맞게 작성하시오.**

![11.png](../../images/2025-04-21-jeongbochuli-silgi-2024-2nd/11.png)



**예제**
A → 

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
RIPRIP(Routing Information Protocol)은 거리 벡터 라우팅 방식으로, 목적지까지 이동하는 <strong>비용의 합이 가장 작은 경로</strong>를 선택한다.  
주어진 그래프에서 A → D → C → F로 이동하는 경우의 총 비용은 다음과 같다:

- A → D : 비용 1
- D → C : 비용 2
- C → F : 비용 5

따라서 총 비용은 1 + 2 + 5 = <strong>8</strong>이다.

다른 경로(A → D → C → E → F)는 비용이 6으로 더 짧지만, 문제에서 A → D → C → F 경로를 지정했으므로,  
해당 경로의 누적 비용을 기준으로 계산한다.
<br><br>
<strong>정답</strong>: A → D → C → F (총 비용 8)
</details>
<br><br>
### 12번 문제

**아래의 표를 확인하여 SRT 스케줄링의 평균 대기시간을 계산하여 작성하시오.**

| 프로세스 | 도착 시간 | 서비스 시간 |
|:---------:|:---------:|:-----------:|
| A         | 0         | 8           |
| B         | 1         | 4           |
| C         | 2         | 9           |
| D         | 3         | 5           |

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
SRT(Shortest Remaining Time) 스케줄링은 남은 작업 시간이 가장 짧은 프로세스를 우선 실행하는 선점형 스케줄링이다.  
스케줄링 순서에 따라 각 프로세스의 대기 시간을 계산하면 다음과 같다:<br>
<br>
- A: (완료 17) - (도착 0) - (서비스 8) = 9<br>
- B: (완료 5) - (도착 1) - (서비스 4) = 0<br>
- C: (완료 26) - (도착 2) - (서비스 9) = 15<br>
- D: (완료 10) - (도착 3) - (서비스 5) = 2<br>

따라서 평균 대기 시간은 (9 + 0 + 15 + 2) ÷ 4 = <strong>6.5</strong>이다.
<br><br>
<strong>정답</strong>: 6.5
</details>
<br><br>
### 13번 문제

**다음은 C언어에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력값을 작성하시오.**

```c
#include <stdio.h>

int main() {
    int arr[3][3] = {1,2,3,4,5,6,7,8,9};
    int* parr[2] = {arr[1], arr[2]};
    printf("%d", parr[1][1] + *(parr[1]+2) + **parr);
    return 0;
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
arr 배열은 3×3 배열로 초기화된다.<br>
parr[0]은 arr[1]을 가리키고, parr[1]은 arr[2]를 가리킨다.<br><br>
parr[1][1]은 arr[2][1] → 8<br>
*(parr[1]+2)는 arr[2][2] → 9<br>
**parr는 arr[1][0] → 4<br><br>
따라서 8 + 9 + 4 = 21이 된다.
<br><br>
<strong>정답</strong>: 21
</details>
<br><br>
### 14번 문제

**다음은 Java 언어에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력값을 작성하시오.**


```java
class Main {
    public static void main(String[] args) {
        int a[] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        ODDNumber OE = new ODDNumber();
        System.out.print(OE.sum(a, true) + ", " + OE.sum(a, false));
    }
}

interface Number {
    int sum(int[] a, boolean odd);
}

class ODDNumber implements Number {
    public int sum(int[] a, boolean odd) {
        int result = 0;
        for(int i=0; i < a.length; i++){
            if((odd && a[i] % 2 != 0) || (!odd && a[i] % 2 == 0))
                result += a[i];
        }        
        return result;
    }    
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
`sum(a, true)`는 배열의 홀수 원소만 더한다.<br>
1 + 3 + 5 + 7 + 9 = 25<br><br>
`sum(a, false)`는 배열의 짝수 원소만 더한다.<br>
2 + 4 + 6 + 8 = 20<br><br>
따라서 출력 결과는 "25, 20"이 된다.
<br><br>
<strong>정답</strong>: 25, 20
</details>
<br><br>
### 15번 문제

**다음은 C언어에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력값을 작성하시오.**

```java
#include <stdio.h>
#include <string.h>

void sumFn(char* d, const char* s) {
    while (*s) {
        *d = *s;
        d++;
        s++;
    }
    *d = '\0'; 
}

int main() {
    const char* str1 = "first";
    char str2[50] = "teststring";  
    int result = 0;
    sumFn(str2, str1);

    for (int i = 0; str2[i] != '\0'; i++) {
        result += i;
    }
    printf("%d", result);

    return 0;
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
`sumFn(str2, str1)`을 호출하여 `str2`에 "first"를 복사한다.<br>
그 후 문자열 `str2`의 각 인덱스를 순회하면서 인덱스 값을 모두 더한다.<br><br>
"first"의 길이는 5이며, 인덱스 0~4까지 존재하므로<br>
0 + 1 + 2 + 3 + 4 = 10이 된다.<br><br>
<strong>정답</strong>: 10
</details>
<br><br>
### 16번 문제

**아래는 소프트웨어 설계에 대한 내용이다. 내용을 읽고 괄호안에 알맞는 답을 작성하시오.**

\- 어떤 모듈이 다른 모듈 내부의 논리적인 흐름을 제어하기 위해, 제어를 통신하거나 제어 요소를 전달하는 결합도이다. 
\- 한 모듈이 다른 모듈의 상세한 처리 절차를 알고 있어 이를 통제하는 경우나 처리 기능이 두 모듈에 분리되어 설계된 경우에 발생한다.

(               ) Coupling

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
제어 결합(Control Coupling)은 한 모듈이 다른 모듈의 내부 로직 흐름을 제어하는 형태의 결합이다.<br>
제어 신호나 플래그 등을 전달하여, 호출된 모듈이 어떻게 동작해야 하는지를 결정하게 만드는 경우에 발생한다.<br><br>
<strong>정답</strong>: 제어(Control)
</details>
<br><br>
### 17번 문제

**다음은 Java에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력 값을 작성하시오.**

```java
class Main {
    public static void main(String[] args) {
        String str = "abacabcd";
        boolean[] seen = new boolean[256];
        System.out.print(calculFn(str, str.length()-1, seen));
    }

    public static String calculFn(String str, int index, boolean[] seen) {
        if(index < 0) return "";
        char c = str.charAt(index);
        String result = calculFn(str, index-1, seen);
        if(!seen[c]) {
            seen[c] = true;
            return c + result;
        }
        return result;
    }
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
`calculFn` 함수는 문자열을 뒤에서부터 순회하며, 처음 등장한 문자를 결과 문자열에 추가한다.<br>
중복된 문자는 무시하고 넘어간다.<br><br>
탐색 순서: d → c → b → a<br>
따라서 최종 결과는 "dcba"가 된다.
<br><br>
<strong>정답</strong>: dcba
</details>
<br><br>
### 18번 문제

**다음은 C언어에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력 값을 작성하시오.**

```c
#include <stdio.h>

void swap(int a, int b) {
    int t = a;
    a = b;
    b = t;
}

int main() {
    int a = 11;
    int b = 19;
    swap(a, b);

    switch(a) {
        case 1:
            b += 1;
        case 11:
            b += 2;
        default:
            b += 3;
        break;
    }

    printf("%d", a-b);
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
`swap(a, b)`는 값 전달(call by value)이므로 메인 함수의 `a`, `b`는 변경되지 않는다.<br>
즉, `a = 11`, `b = 19` 상태 유지.<br><br>
`switch(a)`에서 `case 11:`에 해당되어 `b += 2`가 수행되어 `b = 21`이 된다.<br>
`break`가 없으므로 `default:`까지 이어서 `b += 3`이 되어 `b = 24`가 된다.<br><br>
마지막으로 `a - b = 11 - 24 = -13` 이므로 출력 결과는 -13이다.
<br><br>
<strong>정답</strong>: -13
</details>
<br><br>
### 19번 문제

**다음은 C언어의 구조체에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력 값을 작성하시오.**

```c
#include <stdio.h>

struct node {
    int n1;
    struct node *n2;
};

int main() {
    struct node a = {10, NULL};
    struct node b = {20, NULL};
    struct node c = {30, NULL};

    struct node *head = &a;
    a.n2 = &b;
    b.n2 = &c;

    printf("%d\n", head->n2->n1);

    return 0;
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
`head`는 구조체 `a`를 가리킨다.<br>
`a.n2`는 `b`를 가리키고, `b.n2`는 `c`를 가리킨다.<br><br>
따라서 `head->n2->n1`은 `b.n1`을 의미하고, `b.n1`의 값은 20이다.<br><br>
<strong>정답</strong>: 20
</details>
<br><br>
### 20번 문제

**다음은 Java에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력 값을 작성하시오.**

```java
class Main {
    public static void main(String[] args) {
        String str = "ITISTESTSTRING";
        String[] result = str.split("T");
        System.out.print(result[3]);
    }
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
문자열 `"ITISTESTSTRING"`을 `"T"` 기준으로 분리하면 다음과 같은 배열이 생성된다.<br><br>
- result[0] = "I"<br>
- result[1] = "IS"<br>
- result[2] = "ES"<br>
- result[3] = "S"<br><br>
따라서 `result[3]`의 값은 "S"가 되어 출력된다.
<br><br>
<strong>정답</strong>: S
</details>
<br><br>