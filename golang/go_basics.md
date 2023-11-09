### go basics 

- What is `context` in golang? 
  - context package is used to carry request scoped values and variables across functions which are within the request boundary. 
  - It is also used to carry cancellation signals after client stops the request or to signal hard deadlines like cancelling a request after timeout.

- What is `polymorphism` in golang?
  - Polymorhism is multiple implementations of a sinle interface.
  - In golang there is `interface` type.
  - ```go 
      type Animal interface {
        sound() string
      }

      func (d *dog) sound() string {
        return "woof"
      }
    ```
- How is polymorphism achieved in golang? 
  - There are interface types where user can define all the methods of the interface. 
  - If a type is implementing those methods, then the type is said to be implicitly satisy that interface.
  - 

- What is embedding interface and embedding concrete types?