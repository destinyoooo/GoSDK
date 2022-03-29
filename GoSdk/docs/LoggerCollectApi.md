# \LoggerCollectApi

All URIs are relative to *http://localhost*

Method | HTTP request | Description
------------- | ------------- | -------------
[**HttpCollect**](LoggerCollectApi.md#HttpCollect) | **Post** /project/{project}/log_store/{log_store}/putlog | Http协议接入日志



## HttpCollect

> LoggerResponse HttpCollect(ctx, project, logStore).Body(body).LogApiversion(logApiversion).LogBodyrawsize(logBodyrawsize).AccessKeyId(accessKeyId).AccessKeySecret(accessKeySecret).Execute()

Http协议接入日志

### Example

```go
package main

import (
    "context"
    "fmt"
    "os"
    openapiclient "./openapi"
)

func main() {
    project := "project_example" // string | 项目名
    logStore := "logStore_example" // string | 库名
    body := []openapiclient.LoggerLogX{*openapiclient.NewLoggerLogX("Log_example", "Timestamp_example")} // []LoggerLogX | Body内容为json切片
    logApiversion := "logApiversion_example" // string | cls版本,值v1.0.0 (optional)
    logBodyrawsize := TODO // interface{} | 上传日志大小,小于等于1024 (optional)
    accessKeyId := "accessKeyId_example" // string | Key ID (optional)
    accessKeySecret := "accessKeySecret_example" // string | Key Secret (optional)

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

### Path Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
**ctx** | **context.Context** | context for authentication, logging, cancellation, deadlines, tracing, etc.
**project** | **string** | 项目名 | 
**logStore** | **string** | 库名 | 

### Other Parameters

Other parameters are passed through a pointer to a apiHttpCollectRequest struct via the builder pattern


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------


 **body** | [**[]LoggerLogX**](LoggerLogX.md) | Body内容为json切片 | 
 **logApiversion** | **string** | cls版本,值v1.0.0 | 
 **logBodyrawsize** | [**interface{}**](interface{}.md) | 上传日志大小,小于等于1024 | 
 **accessKeyId** | **string** | Key ID | 
 **accessKeySecret** | **string** | Key Secret | 

### Return type

[**LoggerResponse**](LoggerResponse.md)

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints)
[[Back to Model list]](../README.md#documentation-for-models)
[[Back to README]](../README.md)

