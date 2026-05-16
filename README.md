# 03 — Java Concurrency
**Zorluk:** Intermediate (6/10) | **Java 21** | **Mülakat Hazırlığı**

Java 21 ile thread yönetimi, senkronizasyon, kilitleme mekanizmaları, asenkron programlama ve Virtual Threads.

---

## İçerik

| Konu | Dosya | Kapsanan Konular |
|------|-------|-----------------|
| **Thread Temelleri** | `basics/ThreadBasics.java` | Thread/Runnable/Callable, lifecycle, join, interrupt, daemon, priority, ThreadLocal |
| **Senkronizasyon** | `synchronization/SynchronizationDemo.java` | Race condition, synchronized, volatile, wait/notify, deadlock |
| **Locks** | `locks/LocksDemo.java` | ReentrantLock, tryLock, ReadWriteLock, StampedLock, Condition |
| **Executor Service** | `executors/ExecutorServiceDemo.java` | ThreadPool türleri, Future, invokeAll/Any, ScheduledExecutor, ThreadPoolExecutor |
| **CompletableFuture** | `async/CompletableFutureDemo.java` | thenApply/Compose/Combine, allOf, anyOf, exception handling, async pipeline |
| **Atomic** | `atomic/AtomicDemo.java` | AtomicInteger/Long/Reference/Boolean, CAS, LongAdder, ABA problemi |
| **Concurrent Collections** | `collections/ConcurrentCollectionsDemo.java` | ConcurrentHashMap, CopyOnWriteArrayList, BlockingQueue, CountDownLatch, CyclicBarrier, Semaphore |
| **Virtual Threads** | `virtual/VirtualThreadsDemo.java` | Java 21 Project Loom, platform vs virtual karşılaştırma, Structured Concurrency, pinning |
| **Patterns** | `patterns/ProducerConsumer.java` | Producer-Consumer, BlockingQueue, CountDownLatch |

---

## Thread Lifecycle

```
       start()
NEW ─────────→ RUNNABLE ←──────────────────────┐
                  │                             │
                  │ CPU alır                    │ notify()/interrupt()
                  ↓                             │
              RUNNING ──────────────→ BLOCKED/WAITING/TIMED_WAITING
                  │
                  │ run() biter
                  ↓
             TERMINATED
```

---

## Senkronizasyon Araçları Karşılaştırması

```
Araç                | Kullanım Amacı                        | Özellik
--------------------+---------------------------------------+---------
synchronized        | Basit kritik bölge                    | Otomatik release
ReentrantLock       | Gelişmiş kilit (tryLock, timeout)      | Manuel unlock
ReadWriteLock       | Çok okuyucu / tek yazıcı              | Yüksek okuma performansı
StampedLock         | Optimistic read                       | En performanslı
volatile            | Görünürlük garantisi                  | Atomiklik yok
AtomicInteger/Long  | Lock-free sayaç                       | CAS tabanlı
CountDownLatch      | N görev bitene kadar bekle            | Tek kullanım
CyclicBarrier       | Thread'leri checkpoint'te buluştur    | Yeniden kullanılabilir
Semaphore           | Kaynak erişim sınırlama               | N permit
```

---

## Mülakatta Sık Sorulan Sorular

### Temel
- **Race condition nedir? Örnek ver.**
- **volatile ile synchronized farkı nedir?**
- **Deadlock nasıl oluşur? Nasıl önlenir?**
- **Thread.sleep() vs Object.wait() farkı?**
- **synchronized method vs synchronized block farkı?**

### Orta Seviye
- **ReentrantLock synchronized'dan ne zaman tercih edilir?**
- **ExecutorService türlerini açıkla, ne zaman hangisi kullanılır?**
- **Future vs CompletableFuture farkı nedir?**
- **ConcurrentHashMap neden HashMap'ten thread-safe'dir? Nasıl çalışır?**
- **ThreadLocal nedir, nerede kullanılır?**

### İleri Seviye
- **CAS (Compare and Swap) nedir? ABA problemi nasıl çözülür?**
- **Virtual Thread nedir? Platform thread'den farkı?**
- **Structured Concurrency ne sağlar?**
- **synchronized bloğu virtual thread performansını neden düşürür (pinning)?**
- **ForkJoinPool ne zaman kullanılır?**

---

## Çalıştırma

```bash
mvn compile

# Her demo ayrı çalıştırılabilir
mvn exec:java -Dexec.mainClass="com.concurrency.basics.ThreadBasics"
mvn exec:java -Dexec.mainClass="com.concurrency.synchronization.SynchronizationDemo"
mvn exec:java -Dexec.mainClass="com.concurrency.async.CompletableFutureDemo"
mvn exec:java -Dexec.mainClass="com.concurrency.virtual.VirtualThreadsDemo"
```

---

## Öğrenme Sırası

```
1. ThreadBasics          → Thread nedir, nasıl oluşturulur
2. SynchronizationDemo   → Race condition, synchronized, volatile
3. LocksDemo             → Gelişmiş kilit mekanizmaları
4. ExecutorServiceDemo   → Thread havuzu yönetimi
5. CompletableFutureDemo → Asenkron programlama
6. AtomicDemo            → Lock-free programlama
7. ConcurrentCollections → Thread-safe veri yapıları
8. VirtualThreadsDemo    → Java 21 yeni özellikler
```

---

**Önceki Repo →** [02 - Bank Account Manager](../02_BANK-ACCOUNT-MANAGER)
**Sonraki Repo →** [04 - Design Patterns](../04_DESIGN-PATTERNS)
