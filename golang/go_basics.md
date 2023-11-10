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
   - Embed Interface into a type [ type meaning struct ]: 
      - A interface is a definition of methods which a type should implement to say it is implementing interface.
      - When we embed multiple interfaces into a type then the type is said to implement those methods implicitly.
        example:   
        ```go 
          type interfaceA interface{
            method1()
          }
          type interfaceB interface{
            method2()
          }

          type superStruct struct{
            interfaceA
            interfaceB
          }
        ```
        now in the above example type superStruct is said to implicitly implement method1() and method2() as it is embeding both interfaceA and interfaceB

- Why should we embed interface in a struct? 
  - Composing: To achieve new behavior
  - Polymorphyism: A single struct can flexibly satisfy multiple types at the same time. So we can pass the struct where any of the interface embeded in the struct is expected.
  - composing over inheritance: go encourages lose coupling of base interface from inherited struct type. i.e in inheritance any change to interface has tight coupling on inherited classes. But in composing/embeding interfaces there is no tight coupling. embedded struct will only can use whatever methods the underlying interfaces implement.


- how is `defer` used in go? Are there any use cases? 
  - a defer statement will execute after the execution of present function in which the defer statement is in.
  - to manage resources and to avoid any lekages like file.Close()
  - to signal a goroutine is Done()
  - to signal there is a Panic, by running a deferred function for checking `recover` condition