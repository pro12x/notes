# How to create an installable package with Go
### Create a library
1. **Create a new repository for your library**
```shell
# Create a new repository
mkdir my-library

# open the directory
cd my-library
```

2. **Init a module**
```shell
go mod init github.com/your-username/my-library
```
Replace `github.com/my-username/your-library` with your repository URL

3. **Create Go files**
```go
// mylibrary.go
package mylibrary

func Hello() string {
    return "Hello, World!"
}
```

4. **Add the unit tests (required)**
```go
// mylibrary_test.go
package mylibrary

import "testing"

func TestHello(t *testing.T) {
    got := Hello()
    want := "Hello, World!"
    if got != want {
        t.Errorf("got %q want %q", got, want)
    }
}
```

### Publish your library on GitHub
1. **Create a new repository on GitHub**
2. **Initialize the repository**
```shell
git init
git add .
git init commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/your-username/my-library.git
git push -u origin main
```
3. **Create a tagged release
```shell
git tag v0.1.0
git push origin v0.1.0
```

### Make your library installable with `go install`
1. **Create a subdirectory `cmd/my-library-cli`**
```shell
mkdir -p cmd/my-library-cli
```

2. **Inside the subdirectory, create a `main.go` file**
```go
// cmd/my-library-cli/main.go
package main

import (
    "fmt"
    "github.com/your-username/my-library"
)

func main() {
    fmt.Println(mylibrary.Hello())
}
```

3. **Update the module if required**
4. **Stage the changes and commit them**

### Install the package
Everywhere in your system, you can now install your library with the following command:
```shell
go install github.com/your-username/my-library/cmd/my-library-cli@latest
```
This will install the package in the `$GOPATH/bin` directory.

### Use the package
To use your package inside another Go project, you can import it like this:
```go
import "github.com/your-username/my-library"
```
And add the dependency to your `go.mod` file:
```shell
go get github.com/your-username/my-library
# or
got mod tidy
```

### Conclusion
You have successfully created an installable package with Go. You can now use it in your projects or share it with the community.

### Author
- [Franchis Janel MOKOMBA](https://github.com/pro12x)
