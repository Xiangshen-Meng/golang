### ダウンロード
[Download link.](http://golang.org/doc/install)
```
wget http://golang.org/dl/go1.3.linux-amd64.tar.gz
```
### 解凍
```
tar zxvf go1.3.linux-amd64.tar.gz
```
### 開発環境の設定
```
export GOROOT=$HOME/go
export PATH=$PATH:$GOROOT/bin
export GOPATH=$HOME/xiangshen-meng
```
### テスト
```go
package main
import "fmt"

func main() {
  fmt.Println("Hello world")
}
```
```
go run hello.go
go build hello.go
```
