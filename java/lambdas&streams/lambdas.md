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
    
    - What is a functional interface? 
       - a interface which has exactly one abstract function
       - it can have other deafult functions, but only one abstract function 
       - 
```java
@FunctionalInterface
interface MyPrinter {
    void print(String msg);
}

MyPrinter canonprinter = printMessage -> Systemt.out.println(printMessage);

canonPrinter.print("hello world!I am printed by canon");
```
