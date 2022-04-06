go-collect SDK使用方法

#### golang版本

1、SDK获取

Go版本SDK获取：

https://code.cestc.cn/wujideng/sdktest/-/tree/master/Go

https://github.com/destinyoooo/GoSDK

可以将包import

```go
import (
    openapiclient "github.com/destinyoooo/GoSDK"
)
```

或者直接下载整个项目文件到vendor

![](C:\Users\wujid\AppData\Roaming\marktext\images\2022-04-06-14-03-32-image.png)

2、使用方法

```go
func main() {
    project := "project_example" // string | 项目名
    logStore := "logStore_example" // string | 库名
    logApiversion := "logApiversion_example" // string | cls版本,值v1.0.0 (optional)
    logBodyrawsize := TODO // interface{} | 上传日志大小,小于等于1024 (optional)
    accessKeyId := "accessKeyId_example" // string | Key ID (optional)
    accessKeySecret := "accessKeySecret_example" // string | Key Secret (optional)
    var strs []string
    bodys := openapiclient.GetBody(strs)

    configuration := openapiclient.NewConfiguration()
    apiClient := openapiclient.NewAPIClient(configuration)
    resp, r, err := apiClient.LoggerCollectApi.HttpCollect(context.Background(), project, logStore).Body(body).LogApiversion(logApiversion).LogBodyrawsize(logBodyrawsize).AccessKeyId(accessKeyId).AccessKeySecret(accessKeySecret).Execute()
    if err != nil {
        fmt.Fprintf(os.Stderr, "Error when calling `LoggerCollectApi.HttpCollect``: %v\n", err)
        fmt.Fprintf(os.Stderr, "Full HTTP response: %v\n", r)
    }
    // response from `HttpCollect`: LoggerResponse
    fmt.Fprintf(os.Stdout, "Response from `LoggerCollectApi.HttpCollect`: %v\n", resp)
}
```

2、输入字段说明：

| 字段              | 类型       | 说明           |
| --------------- | -------- | ------------ |
| project         | string   | 项目名          |
| logStore        | string   | 库名           |
| logs            | []string | 日志输入         |
| logApiversion   | string   | 版本号，默认v1.0.0 |
| logBodyrawsize  | int      | 小于等于1024     |
| accessKeyId     | string   | AK           |
| accessKeySecret | string   | SK           |

3、使用示例

在需要使用Client时，import "github.com/destinyoooo/GoSDK"

```go
import (
	openapiclient "github.com/destinyoooo/GoSDK"
    "context"
    "fmt"
    "os"
)func main() {
    //apiVersion := "apiVersion_example" // string | cls版本,值v1.0.0 (optional)
    //bodySize := TODO // interface{} | 上传日志大小,小于等于1024 (optional)
    //accessKeyId := "accessKeyId_example" // string | Key ID (optional)
    //accessKeySecret := "accessKeySecret_example" // string | Key Secret (optional)
    project := "aaa" // string | 项目名
    logStore := "test"
    var strs []string
    strs = append(strs, "test1")
    strs = append(strs, "test2")
    strs = append(strs, "test3")
    strs = append(strs, "test4")
    bodys := openapiclient.GetBody(strs)
    logApiversion := "v1.0.0" // string | cls版本,值v1.0.0 (optional)
    logBodyrawsize := 500 // interface{} | 上传日志大小,小于等于1024 (optional)
    accessKeyId := "7UoxDCrPud9GwdiCSTVu"                         // string | Key ID (optional)
    accessKeySecret := "4tYCJuiDBzIErHTcToKHGaM3BvMlGora3rjR21n6" // string | Key Secret (optional)
    configuration := openapiclient.NewConfiguration()
    configuration.Debug = true
    configuration.Servers = openapiclient.ServerConfigurations{
        {
            URL: "http://10.253.xx.xx:xxx",
            Description: "test sss",
        },
    }
    apiClient := openapiclient.NewAPIClient(configuration)
    resp, r, err := apiClient.LoggerCollectApi.HttpCollect(context.Background(), project, logStore).Body(bodys).LogApiversion(logApiversion).LogBodyrawsize(logBodyrawsize).AccessKeyId(accessKeyId).AccessKeySecret(accessKeySecret).Execute()
    if err != nil {
        fmt.Fprintf(os.Stderr, "Error when calling `LoggerCollectApi.HttpCollect``: %v\n", err)
        fmt.Fprintf(os.Stderr, "Full HTTP response: %v\n", r)
    }
    // response from `HttpCollect`: LoggerResponse
    fmt.Fprintf(os.Stdout, "Response from `LoggerCollectApi.HttpCollect`: %v\n", resp)
}
```

可以配置多个server，选择某个server进行日志输入（输入为字符串数组）

```go
    optServers := make(map[string]openapiclient.ServerConfigurations)

    servers := openapiclient.ServerConfigurations{}
    servers = append(servers, openapiclient.ServerConfiguration{
        URL: "http://localhost:8080/apidocs.json",
        Description: "本地测试localhost",
    })
    servers = append(servers, openapiclient.ServerConfiguration{
        URL: "http://10.253.xx.xx:xxx",
        Description: "72collect测试",
    })
    optServers["test1"] = servers
    configuration.OperationServers = optServers
    ctx := context.WithValue(context.Background(), openapiclient.ContextServerIndex, 1)
```
