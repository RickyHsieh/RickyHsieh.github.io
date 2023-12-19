---
title: HttpEntity<B> 和 ResponseEntity<B>
description: 
date: 2023-12-18 12:00:00+0000
categories:
    - LeetCode
---


## 關於

在Spring框架中，HttpEntity和ResponseEntity是處理HTTP請求和響應的兩個核心概念。
它們都屬於Spring的Web模塊。

### HttpEntity
HttpEntity是一個抽象的概念，表示HTTP請求或響應的整體，包括其中的 headers 和主體内容(body)。它用於封裝HTTP請求的數據，在Spring的RestTemplate中經常用到。你可以使用HttpEntity來設置請求頭和請求主體，然後將它傳遞給RestTemplate以發送HTTP請求。

```java
HttpHeaders headers = new HttpHeaders();
headers.setContentType(MediaType.APPLICATION_JSON);
HttpEntity<String> entity = new HttpEntity<String>("parameters", headers);
```

### ResponseEntity
ResponseEntity是HttpEntity的一個子類別，它表示由服務器發送的含有HTTP狀態碼、header 和 body 的 response 。ResponseEntity特別用於Spring MVC的controller中，可以讓你更精細地控制返回給客戶端的響應。
例如，你可以設置狀態碼、response header和response body。

```java
ResponseEntity<String> responseEntity = new ResponseEntity<String>("Response Body", headers, HttpStatus.OK);
```

HttpEntity是一個更一般的概念，可以代表HTTP請求或響應，而ResponseEntity專門代表一個response。
ResponseEntity繼承自HttpEntity，添加了一些額外的功能，比如設置HTTP狀態碼。
在Spring的REST API中，當你想要完全控制響應時（包括狀態碼和header），通常使用ResponseEntity。
如果你只需要傳遞數據和頭信息，不關心響應的狀態碼，則可以使用HttpEntity。
總的來說，ResponseEntity是用於創建HTTP響應的更專門的工具，而HttpEntity則更多用於客戶端的HTTP請求。在服務器端編程中，當需要對HTTP響應進行精細控制時，應該選擇使用ResponseEntity。