---
title: 多線程筆記
tags: Concurrent Java
show_author_profile: true
comments : true
---
>返去香港 dllm太子狗 搞到我感冒咁多日 死死下

### ThreadLocal
ThreadLocal一般用在線程隔離中存儲緩存數據。用攔截器或過濾器獲取當前用戶id，然後業務流程走完後要清除數據，一是為了避免內存洩漏無法回收，二是在服務器多線程是復用的。  


ThreadLocalRandom  
多線程下，要生成隨機數可以使用ThreadLocalRandom，性能比多線程爭奪Random好。(因為Random是線程安全的)
```java
int boundedRandomValue = ThreadLocalRandom.current().nextInt(0, 100);
```

### ConcurrentHashMap
ConcurrentHashMap可以保證原子性的讀寫操作是線程安全的(CAS+synchronized)，但是如果先讀再寫這樣就不是原子性的操作，就需要加鎖才能保證線程安全。  
又或者使用本身提供的api`computeIfAbsent` `putIfAbsent`。

### CopyOnWriteArrayList
CopyOnWriteArrayList每次只要add的時候，就會使用`Arrays.copyOf`來創建一個新數組，頻繁add時內存申請釋放消耗也會很大，所以在不是讀多寫少的情況下性能比普通的List還差。



*** 



