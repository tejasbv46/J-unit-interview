# JUnit Interview Prep

A concise, organized guide to JUnit 5 for Java backend / SDE interview preparation and last-minute revision.

## Table of Contents

- [Overview](#overview)
- [Why JUnit?](#why-junit)
- [Prerequisites](#prerequisites)
- [Maven Dependency](#maven-dependency)
- [Project Structure](#project-structure)
- [Quick Example](#quick-example)
  - [Calculator.java](#calculatorjava)
  - [CalculatorTest.java](#calculatortestjava)
- [Assertions (Common)](#assertions-common)
- [Lifecycle Annotations](#lifecycle-annotations)
- [Parameterized Tests](#parameterized-tests)
- [Other Useful Features](#other-useful-features)
- [Mockito and Spring Boot Testing](#mockito-and-spring-boot-testing)
- [Best Practices](#best-practices)
- [Common Interview Questions](#common-interview-questions)
- [Learning Path](#learning-path)

---

## Overview

JUnit is the most widely used unit-testing framework for Java. Mastering JUnit 5 (JUnit Jupiter) helps you write reliable unit tests, catch regressions early, and demonstrate strong testing skills in interviews.

## Why JUnit?

- Automates verification of code behavior.
- Speeds up development and refactoring.
- Encourages Test-Driven Development (TDD).
- Widely adopted across companies and projects.

## Prerequisites

- Java 8 or newer (features like lambda help tests).
- A build tool: Maven or Gradle.

## Maven Dependency

Add JUnit Jupiter to your test scope (Maven example):

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.13.4</version>
    <scope>test</scope>
</dependency>
```

Run tests with `mvn test` (Maven Surefire / Failsafe plugins configured as usual).

## Project Structure

Standard Maven layout:

```
src/
 ├── main/
 │    └── java/
 │         └── (production classes)
 └── test/
      └── java/
           └── (test classes)
```

Place production code in `src/main/java` and tests in `src/test/java`.

## Quick Example

Calculator.java

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

CalculatorTest.java

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {
    @Test
    void testAdd() {
        Calculator c = new Calculator();
        assertEquals(5, c.add(2, 3));
    }
}
```

## Assertions (Common)

- `assertEquals(expected, actual)` — compare values.
- `assertNotEquals(expected, actual)`
- `assertTrue(condition)` / `assertFalse(condition)`
- `assertNull(obj)` / `assertNotNull(obj)`
- `assertSame(expected, actual)` / `assertNotSame(expected, actual)`
- `assertArrayEquals(expectedArray, actualArray)`
- `assertIterableEquals(expected, actual)`
- `assertThrows(Exception.class, () -> { /* code */ })` — verify exceptions.
- `assertDoesNotThrow(() -> { /* code */ })`
- `assertAll(...)` — group multiple assertions and report all failures together.

Examples:

```java
assertThrows(ArithmeticException.class, () -> { int x = 1 / 0; });
assertAll(
    () -> assertEquals(10, sum),
    () -> assertTrue(age > 18),
    () -> assertNotNull(name)
);
```

## Lifecycle Annotations

- `@BeforeEach` — runs before every test method.
- `@AfterEach` — runs after every test method.
- `@BeforeAll` — runs once before all tests (static by default unless using `@TestInstance(PER_CLASS)`).
- `@AfterAll` — runs once after all tests (static by default unless using `@TestInstance(PER_CLASS)`).
- `@DisplayName("...")` — human-readable test name.
- `@Disabled` — skip a test.

Execution order (simple view):

```
@BeforeAll
  @BeforeEach
    test1
  @AfterEach
  @BeforeEach
    test2
  @AfterEach
@AfterAll
```

## Parameterized Tests

Run the same test with different inputs:

- `@ValueSource` — simple values.
- `@CsvSource` — multiple arguments per row.
- `@MethodSource` — supply a stream or collection from a factory method.
- `@EnumSource` — provide enum values.

Example:

```java
@ParameterizedTest
@CsvSource({"2,3,5", "5,6,11", "10,20,30"})
void testAdd(int a, int b, int expected) {
    assertEquals(expected, a + b);
}
```

## Other Useful Features

- Assumptions: `assumeTrue(condition)` — skip tests conditionally.
- `@Nested` — group related tests.
- Test ordering: `@TestMethodOrder(...)` and `@Order(...)` (use sparingly).
- Timeouts: `assertTimeout(Duration.ofSeconds(2), () -> { ... })`.
- Conditional execution: `@EnabledOnOs`, `@DisabledOnOs`, `@EnabledOnJre`, etc.
- Dynamic tests: `@TestFactory` to create tests at runtime.

## Mockito and Spring Boot Testing

- Mockito for mocking dependencies:

```java
@Mock
UserRepository repo;

@InjectMocks
UserService service;
```

- Spring Boot testing slices:

  - `@SpringBootTest` — full integration test with context.
  - `@WebMvcTest` — controller slice tests.
  - `@DataJpaTest` — JPA repository tests.

Use Mockito (or MockBean in Spring tests) to isolate units from external systems like databases or HTTP APIs.

## Best Practices

- Each test should verify one behavior.
- Give tests clear, descriptive names (use `@DisplayName` when helpful).
- Keep tests independent and repeatable.
- Use `@BeforeEach` to avoid duplication.
- Prefer parameterized tests over repeating similar test cases.
- Mock slow or external dependencies.
- Aim for meaningful code coverage, but prioritize valuable tests over high coverage numbers.

## Common Interview Questions

- What is JUnit and why is it used?
- Differences between JUnit 4 and JUnit 5.
- What is a unit test vs. integration test?
- Explain `@Test`, `@BeforeEach`, `@BeforeAll`, `@ParameterizedTest`.
- How to test exceptions (`assertThrows`) and timeouts.
- Difference between `assertEquals()` and `assertSame()`.
- What is mocking and how does Mockito work?
- How to test a Spring Boot REST API?
- What is Test-Driven Development (TDD)?

## Learning Path (Suggested)

1. JUnit basics and project setup
2. `@Test` and assertions
3. Lifecycle annotations
4. Exception testing and timeouts
5. Parameterized tests and `@Nested`
6. Organizing tests with tags and ordering
7. Mockito for dependency mocking
8. Spring Boot testing slices
9. Code coverage tools (e.g., JaCoCo)

---

If you'd like, I can also:

- Add badges (build, coverage) and a CONTRIBUTING section.
- Split examples into a `docs/` folder or add runnable sample project structure.

