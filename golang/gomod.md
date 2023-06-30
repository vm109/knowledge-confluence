### go mod
- what did you understand by go mod?
- It is a package manager for go project 

- some useful commands in go mod
``` bash
# init - creates a go.mod file with module name and go version
go init <module_name> 

# tidy - removes any unwanted dependencies and adds any missing dependencies
go mod tidy 

# vendor - to maintain a copy of external dependencies within the working module
go mod vendor 

# building go with mod vendor 
# id we are using vendor dependencies in module we need to specify this as go build wont look outside for dependencies
go build -mod vendor 

# cache clean - clears any go mod cache and re-downlads dependencies
go clean -modcache 
```

### GO111MODULE
- with latest go versions GO111MODULE is default to on
- i.e go commands looks for go.mod and module root and folders for dependencies instead of GOPATH
- GO111MODULE=off
- i.e go commands looks for GOPATH for any dependencies 
 - GO111MODULE=auto
- i.e go commands looks for go.mod and module root and folders for dependencies if go.mod is present if not looks at GOPATH