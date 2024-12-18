---
layout: single
title: "Spring Data JPA 쿼리 메소드 정리"
categories: Spring
tag: [Java, DB, Spring]
toc: true
author_profile: false
sidebar:
  nav: "docs"
---

Spring Data JPA의 **쿼리 메소드**에 대해 정리하겠습니다. 쿼리 메소드는 Spring Data JPA에서 **데이터베이스 쿼리를 작성하는 간편한 방법**입니다. SQL이나 JPQL을 작성하지 않아도 메서드 이름을 기반으로 자동으로 쿼리를 생성해줍니다.

---

## 1. **쿼리 메소드란?**

- **Spring Data JPA**는 메서드 이름에 특정 규칙을 따르면 해당 규칙에 맞는 쿼리를 자동으로 생성해 줍니다.
- SQL이나 JPQL을 직접 작성하지 않아도 됩니다.
- **`findBy`, `readBy`, `queryBy`, `getBy`**로 시작하여 조건을 명시합니다.

---

## 2. **기본 문법**

쿼리 메소드는 **메서드 이름**을 기반으로 쿼리를 생성합니다.

### 형식

```java
[메서드 반환 타입] findBy[엔티티 속성][연산자](타입 파라미터);
```

### 예시

```java
List<User> findByName(String name);
User findByEmailAndAge(String email, int age);
List<User> findByAgeGreaterThan(int age);
```

---

## 3. **연산자와 키워드**

메서드 이름에 사용할 수 있는 **연산자와 키워드**입니다.

| 키워드          | 설명                            | 예시                                           |
| --------------- | ------------------------------- | ---------------------------------------------- |
| `And`           | 두 조건을 **AND**로 연결        | `findByNameAndAge(String name, int age)`       |
| `Or`            | 두 조건을 **OR**로 연결         | `findByNameOrEmail(String name, String email)` |
| `Between`       | 값의 **범위** 조건              | `findByAgeBetween(int start, int end)`         |
| `LessThan`      | **미만** 조건                   | `findByAgeLessThan(int age)`                   |
| `LessThanEqual` | **이하** 조건                   | `findByAgeLessThanEqual(int age)`              |
| `GreaterThan`   | **초과** 조건                   | `findByAgeGreaterThan(int age)`                |
| `Like`          | 부분 문자열 검색 (**LIKE**)     | `findByNameLike(String pattern)`               |
| `Containing`    | **포함 여부** (LIKE %...%)      | `findByNameContaining(String name)`            |
| `StartingWith`  | **시작하는 문자열** (LIKE ...%) | `findByNameStartingWith(String name)`          |
| `EndingWith`    | **끝나는 문자열** (LIKE %...)   | `findByNameEndingWith(String name)`            |
| `OrderBy`       | 정렬 조건                       | `findByNameOrderByAgeAsc(String name)`         |
| `IsNull`        | **NULL** 값 여부                | `findByAgeIsNull()`                            |
| `IsNotNull`     | **NULL 아님** 여부              | `findByAgeIsNotNull()`                         |
| `In`            | 값이 **여러 항목 중 하나**      | `findByAgeIn(List<Integer> ages)`              |
| `NotIn`         | 값이 **여러 항목 중 하나 아님** | `findByAgeNotIn(List<Integer> ages)`           |

---

## 4. **쿼리 메소드 예제**

```java
// 예제 엔티티
@Entity
public class User {
    @Id @GeneratedValue
    private Long id;

    private String name;
    private String email;
    private int age;
}
```

### Repository

```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
    User findByEmailAndAge(String email, int age);
    List<User> findByAgeGreaterThan(int age);
    List<User> findByNameContaining(String keyword);
    List<User> findByAgeBetween(int start, int end);
    List<User> findByNameOrderByAgeAsc(String name);
}
```

### 사용 예시

```java
@Autowired
UserRepository userRepository;

public void exampleUsage() {
    List<User> usersByName = userRepository.findByName("John");
    User userByEmailAndAge = userRepository.findByEmailAndAge("john@example.com", 25);
    List<User> olderUsers = userRepository.findByAgeGreaterThan(30);
    List<User> usersWithKeyword = userRepository.findByNameContaining("Doe");
    List<User> usersByAgeRange = userRepository.findByAgeBetween(20, 40);
    List<User> sortedUsers = userRepository.findByNameOrderByAgeAsc("John");
}
```

---

## 5. **네이티브 쿼리와 @Query**

때로는 복잡한 쿼리를 작성해야 할 때 **@Query** 어노테이션을 사용하여 JPQL이나 네이티브 SQL을 작성할 수 있습니다.

### @Query 사용법

```java
@Query("SELECT u FROM User u WHERE u.name = :name")
List<User> findByNameCustom(@Param("name") String name);
```

### 네이티브 쿼리 사용법

```java
@Query(value = "SELECT * FROM user WHERE name = :name", nativeQuery = true)
List<User> findByNameNative(@Param("name") String name);
```

---

## 6. **주의 사항**

1. 메서드 이름이 너무 길어질 수 있으므로 적절하게 **@Query**를 사용할 것을 고려하세요.
2. 성능상 이슈가 있을 경우 페이징과 정렬을 지원하는 `Pageable`을 사용하세요.
3. 복잡한 조건이 많다면 Specification 또는 QueryDSL을 사용해보세요.

---

## 결론

Spring Data JPA의 **쿼리 메소드**는 코드만으로 간단하게 데이터 조회 로직을 구현할 수 있는 기능입니다. 메서드 이름을 명확하게 작성하면 Spring이 자동으로 쿼리를 생성해주므로 개발 생산성을 높일 수 있습니다.
