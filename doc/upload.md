## java版本
依赖(这里使用了hutool工具包,更简便)
```xml
<dependency>
	<groupId>cn.hutool</groupId>
	<artifactId>hutool-all</artifactId>
	<version>4.4.3</version>
</dependency>
```
上传代码
```java
public static void main(String[] args) {
    //文件地址
    File file = new File("D:\\git\\2.jpg");
    //声明参数集合
    HashMap<String, Object> paramMap = new HashMap<>();
    //文件
    paramMap.put("file", file);
    //输出
    paramMap.put("output","json");
    //自定义路径
    paramMap.put("path","image");
    //场景
    paramMap.put("scene","image");
    //上传
    String result= HttpUtil.post("http://xxxxx:xxxx/upload", paramMap);
    //输出json结果
    System.out.println(result);
}
```
# 断点续传示例

## golang版本
```go
package main

import (
    "os"
    "fmt"
    "github.com/eventials/go-tus"
)

func main() {
    f, err := os.Open("100m")
    if err != nil {
        panic(err)
    }
    defer f.Close()
    // create the tus client.
    client, err := tus.NewClient("http://10.1.5.9:8080/big/upload/", nil)
    fmt.Println(err)
    // create an upload from a file.
    upload, err := tus.NewUploadFromFile(f)
    fmt.Println(err)
    // create the uploader.
    uploader, err := client.CreateUpload(upload)
    fmt.Println(err)
    // start the uploading process.
   fmt.Println( uploader.Upload())

}

````
