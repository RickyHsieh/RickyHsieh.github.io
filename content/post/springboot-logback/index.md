---
title: SpringBoot 設定日誌
description: 設定日誌
date: 2023-08-25 12:00:00+0000
---

## SpringBoot 使用日誌元件

SpringBoot 預設使用的日誌元件 logback，由log4j創始人設計。

如果要修改日誌的輸出格式，只需要在 src/main/resources目錄下建立名為 logback-spring.xml 或者 logback.xml 的檔案即可。

SpringBoot 會自動讀取該檔案的設定檔，如果需要SpringBoot設定檔中，透過logging.config屬性給出自定義的檔案的名稱。