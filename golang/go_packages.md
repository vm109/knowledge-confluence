### Go Packages
-  What is `init` function in golang?
    - init() function is run before main function.
    - when there is a init() function in another package, init() from imported package will run before init() in main package.
    - `init` function cannot be called exclusively. it is called automatically before the main() function by the go runtime.
    - `init` function usage should be limited for maintaining the code readability.
    
- When is `init` used commonly? 
    - I used init to setup configurations and setting up global variables. 

- How to import packages in a go.mod? 
    - When we defin a go.mod file then then all the folders will be relative to that go.mod file. 
    - importing a package in a go module `testgoapp` which is in folder /pkg/folder1/folder2 would be `testgoapp/pkg/folder1/folder2` assuming go.mod is at the root of `testgoapp`.
    - ```
        import (
            "fmt"
            "testgoapp/pkg/folder1/folder2"
        )
    ```
    - ```
        testgoapp/
            ├── go.mod
            ├── cmd/
            │   └── main.go
            └── pkg/
                └── folder1/
                    └── folder2/
                        └── your_package_files.go
    ```