---
layout: post
title: "[2024년 3회] 정보처리기사 실기 복원 문제 정리"
date: 2025-04-21 11:00:00 +0900
categories: 정보처리기사
tag: [정보처리기사, 실기, 기출문제, 복원문제]
layout: single
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

> 원본: [초보몽키 블로그 - 2024년 3회 정보처리기사 실기](https://chobopark.tistory.com/495)



### 1번 문제

**다음은 Java 코드에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력값을 작성하시오.**

```java
public class Main {
    static String[] s = new String[3];

    static void func(String[] s, int size) {
        for (int i = 1; i < size; i++) {
            if (s[i - 1].equals(s[i])) {
                System.out.print("O");
            } else {
                System.out.print("N");
            }
        }
        for (String m : s) {
            System.out.print(m);
        }
    }

    public static void main(String[] args) {
        s[0] = "A";
        s[1] = "A";
        s[2] = new String("A");
        func(s, 3);
    }
}
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
s[2]는 값은 같지만 new String("A")로 생성된 다른 객체이므로 equals는 true, ==는 false. 그러나 여기서는 equals만 쓰므로 모두 같다고 판단되어 O가 2번 출력되고 배열 그대로 출력되므로 OOAAA
<br>
<br>
  <strong>정답</strong>: OOAAA</details>


### 2번 문제

**다음은 파이썬에 대한 문제이다. 아래 코드를 확인하여 알맞는 출력값을 작성하시오.**

```python
def func(lst):
    for i in range(len(lst) // 2):
        lst[i], lst[-i - 1] = lst[-i - 1], lst[i]

lst = [1, 2, 3, 4, 5, 6]
func(lst)
print(sum(lst[::2]) - sum(lst[1::2]))
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
리스트를 반대로 뒤집은 후, 짝수 인덱스와 홀수 인덱스의 합을 비교함. [6,5,4,3,2,1]에서 (6+4+2)-(5+3+1)=12-9=3
<br>
<br>
  <strong>정답</strong>: 3</details>


### 3번 문제

**아래의 employee테이블과 project테이블을 참고하여 보기의 SQL명령어에 알맞는 출력 값을 작성하시오.**

![3.png](../../images/2025-04-21-jeongbochuli-silgi-2024-3rd/3.png)


```sql
SELECT count(*)
FROM employee AS e
JOIN project AS p ON e.project_id = p.project_id
WHERE p.name IN (
  SELECT name
  FROM project p
  WHERE p.project_id IN (
    SELECT project_id
    FROM employee
    GROUP BY project_id
    HAVING count(*) < 2
  )
);
```

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
employee 테이블에서 project_id 기준으로 2명 미만인 프로젝트를 찾고, 해당 이름을 가진 프로젝트의 사원 수를 다시 카운트하는 방식. 결과는 1건
<br>
<br><strong>정답</strong>: 1
</details>


### 4번 문제

**다음은 운영체제 페이지 순서를 참고하여 할당된 프레임의 수가 3개일 때 LRU 알고리즘의 페이지 부재 횟수를 작성하시오.**

- 페이지 참조 순서: `7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1`
- 프레임 수: 3개
- 알고리즘: LRU

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
LRU(Least Recently Used)는 가장 오래 사용하지 않은 페이지를 교체함.<br><table>
  <thead>
    <tr>
      <th>순서</th>
      <th>페이지</th>
      <th>프레임 상태</th>
      <th>결과</th>
      <th>설명</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>1</td><td>7</td><td>[7]</td><td>❌</td><td>새로 삽입</td></tr>
    <tr><td>2</td><td>0</td><td>[7, 0]</td><td>❌</td><td>새로 삽입</td></tr>
    <tr><td>3</td><td>1</td><td>[7, 0, 1]</td><td>❌</td><td>새로 삽입</td></tr>
    <tr><td>4</td><td>2</td><td>[0, 1, 2]</td><td>❌</td><td>7이 가장 오래되어 교체</td></tr>
    <tr><td>5</td><td>0</td><td>[1, 2, 0]</td><td>✔</td><td>0은 이미 있음 → 히트</td></tr>
    <tr><td>6</td><td>3</td><td>[2, 0, 3]</td><td>❌</td><td>1이 가장 오래되어 교체</td></tr>
    <tr><td>7</td><td>0</td><td>[2, 3, 0]</td><td>✔</td><td>0은 이미 있음 → 히트</td></tr>
    <tr><td>8</td><td>4</td><td>[3, 0, 4]</td><td>❌</td><td>2가 가장 오래되어 교체</td></tr>
    <tr><td>9</td><td>2</td><td>[0, 4, 2]</td><td>❌</td><td>3이 가장 오래되어 교체</td></tr>
    <tr><td>10</td><td>3</td><td>[4, 2, 3]</td><td>❌</td><td>0이 가장 오래되어 교체</td></tr>
    <tr><td>11</td><td>0</td><td>[2, 3, 0]</td><td>❌</td><td>4가 가장 오래되어 교체</td></tr>
    <tr><td>12</td><td>3</td><td>[2, 0, 3]</td><td>✔</td><td>3은 이미 있음</td></tr>
    <tr><td>13</td><td>2</td><td>[0, 3, 2]</td><td>✔</td><td>2는 이미 있음</td></tr>
    <tr><td>14</td><td>1</td><td>[3, 2, 1]</td><td>❌</td><td>0이 가장 오래되어 교체</td></tr>
    <tr><td>15</td><td>2</td><td>[3, 1, 2]</td><td>✔</td><td>2는 이미 있음</td></tr>
    <tr><td>16</td><td>0</td><td>[1, 2, 0]</td><td>❌</td><td>3이 가장 오래되어 교체</td></tr>
    <tr><td>17</td><td>1</td><td>[2, 0, 1]</td><td>✔</td><td>1은 이미 있음</td></tr>
    <tr><td>18</td><td>7</td><td>[0, 1, 7]</td><td>❌</td><td>2가 가장 오래되어 교체</td></tr>
    <tr><td>19</td><td>0</td><td>[1, 7, 0]</td><td>✔</td><td>0은 이미 있음</td></tr>
    <tr><td>20</td><td>1</td><td>[7, 0, 1]</td><td>✔</td><td>1은 이미 있음</td></tr>
  </tbody>
</table>
  <br>총 페이지 부재 횟수: 12회
  <br>총 히트 횟수: 8회<br>
  <strong>정답</strong>: 12
</details>


### 5번 문제

**다음은 네트워크 취약점에 대한 문제이다. 아래 내용을 보고 알맞는 용어를 작성하시오.**

**문제 설명**:

- IP 또는 ICMP를 이용하여 다량의 데이터를 특정 사이트로 보내 서비스 불능 상태 유도
- 여러 호스트가 ICMP Echo Reply를 보내게 하여 DoS 발생

<details>
<summary><strong>정답 보기</strong></summary>
<br>
<strong>해설</strong><br>
공격자가 브로드캐스트 주소로 ICMP 패킷을 보내고, 피해자는 수많은 응답으로 서비스 불능 상태가 됨
<br>
<br>
  <strong>정답</strong>: 스머프(공격) 또는 스머핑(Smurfing)</details>


### 6번 문제

**다음은 GoF 디자인 패턴과 관련된 문제이다. 괄호안에 알맞는 용어를 작성하시오.**

**문제**: (        ) 패턴은 클래스나 객체들이 서로 상호작용하는 방법이나 책임 분배 방법을 정의하는 패턴

<details>
	<summary><strong>정답 보기</strong></summary><br>
	<strong>해설</strong><br>
	객체 간의 상호작용과 책임 분배에 초점을 맞춘 패턴군으로, 상태, 전략, 옵저버 등이 포함됨
  <strong>정답</strong>: 행위(Behavioral) 패턴
</details>






