# J-unit-interview
jnuit interview question and last minute prep
If you're preparing for Java backend/SDE interviews, learning JUnit 5 is one of the most valuable testing skills. Here's a complete roadmap from basic to advanced.

1. What is JUnit?

JUnit is the most popular testing framework for Java.

It is used to:

Test Java methods automatically
Find bugs before deployment
Ensure code changes don't break existing features
Support Test-Driven Development (TDD)

Example:

Instead of manually running:

Calculator c = new Calculator();
System.out.println(c.add(2,3));

JUnit automatically checks whether the output is correct.

2. Why use JUnit?

Without JUnit

Run application
Call method
Check output manually
Repeat every time

With JUnit

Write test once
Click Run Tests
JUnit verifies everything automatically

Benefits:

Saves time
Detects bugs early
Makes refactoring safer
Improves code quality
Widely used in companies
3. JUnit Versions
JUnit 3 (old)
JUnit 4
JUnit 5 (current and recommended)

Most companies use JUnit 5.

4. JUnit Architecture

JUnit 5 consists of:

Platform
Runs tests
Jupiter
Main API you write
Vintage
Supports old JUnit 4 tests
5. Maven Dependency
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.13.4</version>
    <scope>test</scope>
</dependency>
6. Folder Structure
src
 ├── main
 │     └── java
 │           Calculator.java
 │
 └── test
       └── java
             CalculatorTest.java

Production code goes in

src/main/java

Tests go in

src/test/java
7. First Example

Calculator

public class Calculator {

    public int add(int a, int b){
        return a+b;
    }

}

Test

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void testAdd() {
        Calculator c = new Calculator();
        assertEquals(5, c.add(2,3));
    }

}
8. What is @Test?

Marks a method as a test.

@Test
void checkAddition(){

}

JUnit automatically runs it.

9. Assertions

Assertions compare expected and actual values.

assertEquals()
assertEquals(10, sum);
assertNotEquals()
assertNotEquals(5, sum);
assertTrue()
assertTrue(age>18);
assertFalse()
assertFalse(list.isEmpty());
assertNull()
assertNull(obj);
assertNotNull()
assertNotNull(obj);
assertSame()

Checks if both references point to the same object.

assertSame(obj1,obj2);
assertNotSame()
assertNotSame(obj1,obj2);
assertArrayEquals()
assertArrayEquals(expected, actual);
assertIterableEquals()
assertIterableEquals(list1,list2);
assertThrows()

Checks exceptions.

assertThrows(
    ArithmeticException.class,
    () -> {
        int x=10/0;
    }
);
assertDoesNotThrow()
assertDoesNotThrow(() -> calculator.divide(10,2));
assertAll()

Runs multiple assertions.

assertAll(
    ()->assertEquals(10,sum),
    ()->assertTrue(age>18),
    ()->assertNotNull(name)
);
10. Lifecycle Annotations
@BeforeEach

Runs before every test.

@BeforeEach
void setup(){

}
@AfterEach

Runs after every test.

@AfterEach
void cleanup(){

}
@BeforeAll

Runs once before all tests.

@BeforeAll
static void init(){

}

Must be static by default.

@AfterAll

Runs once after all tests.

@AfterAll
static void close(){

}

Execution

@BeforeAll

@BeforeEach
Test1
@AfterEach

@BeforeEach
Test2
@AfterEach

@AfterAll
11. @DisplayName
@DisplayName("Addition Test")

Shows a readable name.

12. @Disabled

Skips a test.

@Disabled
@Test
void test(){

}
13. @RepeatedTest
@RepeatedTest(5)
void repeat(){

}

Runs 5 times.

14. @ParameterizedTest

Runs the same test with multiple values.

@ParameterizedTest
@ValueSource(ints={1,2,3,4})
void testPositive(int value){
    assertTrue(value>0);
}
15. @ValueSource
@ValueSource(strings={"Java","JUnit"})
16. @CsvSource
@ParameterizedTest
@CsvSource({
"2,3,5",
"5,6,11",
"10,20,30"
})
void testAdd(int a,int b,int expected){
    assertEquals(expected,a+b);
}
17. @MethodSource
@MethodSource("numbers")

Supplies test data from a method.

18. @EnumSource

Useful for enums.

19. Assumptions

Skip tests based on conditions.

assumeTrue(true);
20. Nested Tests
@Nested
class AdditionTests{

}

Groups related tests.

21. Test Order
@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
@Order(1)
22. Timeout
assertTimeout(Duration.ofSeconds(2),()->{

});
23. Exception Testing
assertThrows(
    IllegalArgumentException.class,
    ()->{
        throw new IllegalArgumentException();
    }
);
24. Tags
@Tag("Smoke")
@Tag("Regression")

Run selected categories of tests.

25. Conditional Tests

Examples:

@EnabledOnOs(OS.WINDOWS)
@DisabledOnOs(OS.LINUX)
@EnabledOnJre(JRE.JAVA_21)
26. Test Instance Lifecycle
@TestInstance(TestInstance.Lifecycle.PER_CLASS)

Allows non-static @BeforeAll.

27. Dynamic Tests
@TestFactory

Generates tests at runtime.

28. Mockito with JUnit

Mockito creates fake objects for dependencies.

Example:

@Mock
UserRepository repository;

@InjectMocks
UserService service;
29. Spring Boot Testing

For Spring Boot:

@SpringBootTest

or

@WebMvcTest

or

@DataJpaTest
30. Code Coverage

Use tools like JaCoCo to measure tested code.

Example:

Coverage

Lines : 90%

Branches : 82%

Methods : 95%
31. Best Practices
One test should verify one behavior.
Give tests meaningful names.
Keep tests independent.
Use @BeforeEach to avoid duplicate setup.
Prefer parameterized tests over repeated code.
Mock external dependencies like databases and APIs.
32. JUnit Interview Questions
What is JUnit?
Why is JUnit used?
Difference between JUnit 4 and JUnit 5?
What is a unit test?
What is @Test?
Explain assertions.
Difference between assertEquals() and assertSame().
What is assertThrows()?
Difference between @BeforeEach and @BeforeAll.
What is @ParameterizedTest?
What is @RepeatedTest?
What is @Nested?
What is @Disabled?
What are Tags?
What is Mockito?
What is code coverage?
What is TDD?
What is mocking?
What is integration testing?
How do you test a Spring Boot REST API?
Learning order for interviews
JUnit basics and project setup
@Test and assertions
Lifecycle annotations (@BeforeEach, @AfterEach, @BeforeAll, @AfterAll)
Exception testing with assertThrows
Parameterized tests (@ValueSource, @CsvSource, @MethodSource)
Test organization (@DisplayName, @Nested, @Tag, ordering)
Timeouts, assumptions, and conditional tests
Mockito for mocking dependencies
Spring Boot testing (@SpringBootTest, @WebMvcTest, @DataJpaTest)
Code coverage with JaCoCo

For most Java backend fresher interviews, mastering topics through parameterized tests and having a working knowledge of Mockito and Spring Boot testing will put you in a strong position.
