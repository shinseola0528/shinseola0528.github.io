---
layout: single
title: "Java에서 final 키워드의 역할"
categories: Java
tag: [Java]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

`final` 키워드는 Java에서 여러 상황에서 사용되며, 해당 대상의 **변경 불가** 또는 **최종화**를 의미합니다. `final` 키워드가 적용될 수 있는 주요 대상과 역할은 다음과 같습니다.

---

## 1. 변수에 사용될 때

- **의미**: 변수를 **상수화**하여 값을 한 번만 할당하도록 합니다.
- **역할**: 변수의 값을 변경하지 못하게 막아 **불변성**을 보장합니다.
- **예제**:
  ```java
  final int MAX_VALUE = 100;
  MAX_VALUE = 200; // 컴파일 에러 발생: 값을 재할당할 수 없습니다.
  ```

---

## 2. 메서드에 사용될 때

- **의미**: 해당 메서드를 **오버라이드**할 수 없게 만듭니다.
- **역할**: 메서드의 동작을 변경하지 못하도록 강제합니다.
- **예제**:

  ```java
  class Parent {
      final void display() {
          System.out.println("This is a final method.");
      }
  }

  class Child extends Parent {
      // void display() { } // 컴파일 에러: final 메서드는 오버라이드 불가
  }
  ```

---

## 3. 클래스에 사용될 때

- **의미**: 해당 클래스를 **상속**할 수 없도록 만듭니다.
- **역할**: 클래스의 설계를 더 이상 확장하지 못하게 제한합니다.
- **예제**:

  ```java
  final class FinalClass {
      void show() {
          System.out.println("This is a final class.");
      }
  }

  class SubClass extends FinalClass { // 컴파일 에러 발생
  }
  ```

---

## 4. 참조 변수에 사용될 때 (객체)

- **의미**: 참조 변수가 가리키는 **객체의 주소값**을 변경할 수 없습니다.
- **역할**: 다른 객체를 참조하지 못하도록 강제합니다. 하지만 객체 내부의 필드는 변경 가능합니다.
- **예제**:
  ```java
  final StringBuilder sb = new StringBuilder("Hello");
  sb.append(" World"); // 가능: 객체 내부 값 수정
  sb = new StringBuilder("New"); // 컴파일 에러: 참조 변수 변경 불가
  ```

---

## 결론

`final` 키워드는 변수, 메서드, 클래스에 적용되어 **변경 불가**라는 의미를 전달합니다.

- **변수**: 값을 재할당할 수 없음.
- **메서드**: 오버라이드 불가.
- **클래스**: 상속 불가.
  객체를 불변하게 설계하거나 보안을 강화할 때 매우 유용하게 사용됩니다.
