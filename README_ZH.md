# httprouter 源码解析


**说明：此包是用来将URI映射到handler上的，它只涉到两个元素 
一个是URI一个是处理逻辑，跟post body是否携带数据是没有一毛钱关系的
所以不要混淆**
## 1.基本案例


建议看源码之前，先把代码运行起来，这样有助于理解源码的逻辑。
不妨看看官方demo 

[demo1.1](example/001/main.go)  
```go
 package main

 import (
     "fmt"
     "github.com/julienschmidt/httprouter"
     "net/http"
     "log"
 )

 func Index(w http.ResponseWriter, r *http.Request, _ httprouter.Params) {
     fmt.Fprint(w, "Welcome!\n")
 }

 func Hello(w http.ResponseWriter, r *http.Request, ps httprouter.Params) {
     fmt.Fprintf(w, "hello, %s!\n", ps.ByName("name"))
 }
 func main() {
     router := httprouter.New()
     router.GET("/", Index)
     router.GET("/hello/:name", Hello)

     log.Fatal(http.ListenAndServe(":8080", router))
 }

```






