---
title: SpringBoot Profile 使用屬性檔案設定多環境
description: 使用屬性檔案設定多環境簡單演示
date: 2023-08-25 12:00:00+0000
---


## 先建立多環境properties
在src/main/resources 目錄下新建兩個屬性檔案，分別為 application-dev.properties 和 application-prod.properties，前者適用於開發後者用於正式環境設定檔。

這邊只是演示 (一般不設定Debug等級日誌是因為會有很多日誌資訊，增加起動專案名稱，影響開發效率):

在 dev 環境下，日誌以 Debug 等級或更高等級為輸出到控制台，application-dev.properties :

```
logging.level.root=DEBUG
```

在application-prod.properties則設定 :

```
logging.file.name=f://logs//demo.log
logging.level.root=WARN
```
## 注意事項

logging.file.name 用於指定日誌名稱(可以是精確位置)，也可以是相對於目前目錄的位置。
容易混淆的是 : logging.file.path (這是用來指定日誌的位置)

這兩個屬性不能同時使用，如果同時，預設logging.file.name屬性生效。

接下來在主設定檔application.properties :


## 測試

這樣是吃 Dev log檔案設定會發生變化
```
spring.profiles.active=dev
```

反之
這樣是吃 Prod 
```
spring.profiles.active=prod
```