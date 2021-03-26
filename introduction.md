# introduction to GO

## Install
[Download](https://golang.google.cn/dl/) the Go installer and install Go. Check the version of Go using command `go version`. If you need help, use `go help`:
```bash
go verson
go help
```

## Hello World
```go
package main

import "fmt"

func main() {
	fmt.Println("Hello, World!")
}
```
```bash
mkdir hello
cd  hello
go mod init example.com/hello
go run .
```

***Reference***
- <https://golang.google.cn/doc/tutorial/getting-started>
