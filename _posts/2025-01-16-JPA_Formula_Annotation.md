---
layout: single
title: "JPA의 @Formula 어노테이션"
categories: Spring
tag: [Java, Spring, DB, JPA]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

`@Formula`는 Hibernate에서 제공하는 기능으로, JPA 표준 스펙에는 포함되어 있지 않음. 이 어노테이션을 사용하면 엔티티 필드에 SQL 표현식을 매핑할 수 있음. 이를 통해 데이터베이스에 직접 저장되지 않은 계산된 값을 엔티티에서 조회할 수 있음.

## 1. `@Formula` 주요 특징

1. SQL 표현식 사용 가능: SQL 표현식을 사용하여 엔티티 필드를 계산함
2. 읽기 전용: `@Formula`로 정의된 필드는 읽기 전용이며, 값을 업데이트할 수 없음
3. 지연 로딩 지원: 필요한 경우 지연 로딩(Lazy Loading)으로 설정 가능

## 2. 사용 예시

```java
import org.hibernate.annotations.Formula;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class Product {
    @Id
    private Long id;

    private int price;
    private int tax;

    @Formula("price + tax")
    private int totalPrice;

    // Getter와 Setter
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public int getPrice() {
        return price;
    }

    public void setPrice(int price) {
        this.price = price;
    }

    public int getTax() {
        return tax;
    }

    public void setTax(int tax) {
        this.tax = tax;
    }

    public int getTotalPrice() {
        return totalPrice;
    }
}
```

## 3. 동작 설명

- `@Formula("price + tax")`: `price`와 `tax` 필드 값을 더한 결과를 `totalPrice` 필드에 매핑함
- 엔티티를 조회할 때 `SELECT price + tax AS totalPrice`와 같은 SQL이 실행됨

## 4. 장점

1. 계산 로직을 데이터베이스로 위임하여 효율적인 연산 가능
2. 엔티티 코드 내 계산 로직 제거로 코드 간소화 가능

## 5. 단점

1. Hibernate 전용 어노테이션이므로 JPA 표준을 준수하지 않음
2. SQL 표현식이 복잡할 경우 유지보수가 어려움
3. 읽기 전용이므로 데이터 수정 불가

## 6. 사용 시 주의점

1. 데이터베이스 종속적인 SQL 표현식을 사용할 경우 이식성 저하 가능
2. 복잡한 SQL 계산이 많아지면 성능 저하 우려 있음

이러한 점을 고려해 `@Formula`는 계산된 값이 자주 사용되며, 명시적 비즈니스 로직으로 처리하기 어렵거나 비효율적인 경우에 적합한 방식임.
