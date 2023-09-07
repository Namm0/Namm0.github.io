---
title: HTTP調用筆記
tags: http feign ribbon
show_author_profile: true
---

HTTP調用一般可以設置的參數有連結超時(connectTimeout)和讀取超時(readTimeout)。  
1. 讀取超時的話，服務端不會受影響。Tomcat是把服務端受到的請求提交到線程池處理，網絡層的超時和斷開不會影響服務段的執行。  
2. 讀取超時指的是，Socket寫入數據後，等到Socket返回數據的超時時間，其中絕大部分的時間都是服務端處理業務邏輯的時間。  
3. 對於定時任務或者異步任務來說，讀取超時配置可以長一些；但是面向用戶響應或是微服務的同步接口調用，併發量大，應設置一個短的讀取超時，防止下游被拖慢。  
  

以Feign為例子，在配置上有需要注意的地方。  
1. 默認讀取超時為1s。
2. 修改配置的話得同時修改連結超時和讀取超時。  
3. 單獨配置可以覆蓋全局配置。  
4. 同時配置Feign和Ribbon，Feign會覆蓋Ribbon。 

Ribbon會自動重試`DEFAULT_MAX_AUTO_RETRIES_NEXT_SERVER = 1`，如果調用超時，調用別的節點。  
可以修改配置，或者用POST請求。  

基於HTTP1.1協議，因為服務器的性能問題，瀏覽器的最大併發數為2，所以使用HttpClient調用的話，默認配置對於同域名的調用限制在2個併發，即使使用線程池。  
```java
CloseableHttpClient httpClient = HttpClients.custom().setConnectionManager(new PoolingHttpClientConnectionManager()).build();
```



