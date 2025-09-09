## Lambdas

### Questions: 
    - Why are lambdas used? 
        - to my udnerstanding it is preferred when the logic is straigforward, with some filters, mappings etc
        - if the logic needs more control like breaks based on logic etc, the use age old loops
        - lambdas can also reduce readability and debugging capability if heavily used. 

    - What is a predicate in lambda? 
        - predicate is a functional interface. 
        - predicate takes in a type T as function and returns a boolean.
        - 
```java

public interface Predicate<T> {
    boolean test(T t);
}

Predicate<String> startsWithA = s -> s.startsWith("A");

System.out.println(startsWithA.test("Apple")); //true
```
