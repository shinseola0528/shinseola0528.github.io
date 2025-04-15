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

# JPA의 `@Formula` 어노테이션

`@Formula`는 Hibernate에서 제공하는 기능으로, JPA 표준 스펙에는 포함되어 있지 않습니다. 이 어노테이션을 사용하면 엔티티 필드에 SQL 표현식을 매핑할 수 있습니다. 이를 통해 데이터베이스에 직접 저장되지 않은 계산된 값을 엔티티에서 조회할 수 있습니다.

---

## **`@Formula` 주요 특징**
1. **SQL 표현식 사용 가능**: SQL 표현식을 사용하여 엔티티 필드를 계산합니다.
2. **읽기 전용**: `@Formula`로 정의된 필드는 읽기 전용으로, 값을 업데이트할 수 없습니다.
3. **지연 로딩 지원**: 필요한 경우 `@Formula` 필드를 지연 로딩(Lazy Loading)으로 설정할 수 있습니다.

---

## **사용 예시**
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

---

## **동작 설명**
- `@Formula("price + tax")`: `price`와 `tax` 필드 값을 더한 결과를 `totalPrice` 필드에 매핑합니다.
- 엔티티를 조회할 때 `SELECT price + tax AS totalPrice`와 같은 SQL이 실행됩니다.

---

## **장점**
1. **계산 로직을 데이터베이스로 위임**: 데이터베이스에서 효율적으로 계산된 결과를 가져올 수 있습니다.
2. **코드 간소화**: 엔티티 클래스에서 계산 로직을 제거할 수 있습니다.

## **단점**
1. **의존성**: Hibernate 전용 어노테이션이므로 JPA 표준을 준수하는 프로젝트에서는 사용할 수 없습니다.
2. **복잡성 증가**: SQL 표현식이 복잡할 경우 유지보수가 어려울 수 있습니다.
3. **읽기 전용**: 데이터를 수정할 수 없습니다.

---

## **사용 시 주의점**
1. 데이터베이스 종속적인 SQL 표현식을 사용할 경우, 다른 DBMS로 변경할 때 문제가 발생할 수 있습니다.
2. 복잡한 SQL 계산이 많아지면 성능에 영향을 미칠 수 있으므로 주의해야 합니다.

이러한 점을 고려해 `@Formula`는 주로 계산된 값이 자주 사용되지만, 비즈니스 로직에서 명시적으로 처리하기 어렵거나 비효율적인 경우에 적합합니다.
