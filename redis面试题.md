#  Redis



## 为什么要用redis



1. redis的数据存储在内存中，内存的读取数据比传统的数据库快，性能高。

2. 由于在redis的数据操作快，而且是单线程的，并且实现了IO多路复用，可以承受比较大的并发量。

3.  redis可以持久化，能在服务器宕机时保存数据。

4. redis可以集群保证整个缓存系统的稳定性。

   

   

## redis怎么删除过期键



定期删除 ，每隔100ms 随机抽取设置了过期时间的键进行检查并删除过期键



惰性删除，在查找这个键的时候检查这个键是否过期，再删除。





## redis的内存淘汰机制



1. **volatile-lru**：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
2. **volatile-ttl**：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
3. **volatile-random**：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
4. **allkeys-lru**：从数据集中，移除最近最少使用的key（这个是最常用的）
5. **allkeys-random**：从数据集（server.db[i].dict）中任意选择数据淘汰
6. **no-eviction**：禁止驱逐数据，也就是说当内存不足以容纳新写入数据时，新写入操作会报错。这个应该没人使用吧

1. **volatile-lfu**：从已设置过期时间的数据集(server.db[i].expires)中挑选最不经常使用的数据淘汰
2. **allkeys-lfu**：当内存不足以容纳新写入数据时，在键空间中，移除最不经常使用的key



## redis的持久化方式



RDB  通过fork子进程进行备份数据到rdb文件中，默认

AOF 通过将redis的写操作写入AOF文件中的形式备份数据。





## 避免缓存雪崩



缓存雪崩就是缓存失效导致大量请求落到数据库上而使数据库崩掉的现象。



解决方法： 

1. 用redis集群防止redis宕机

2. 如果缓存雪崩发生，使用本地缓存并限制流量。

3. 利用redis的持久化文件快速重启redis恢复数据。

   

## 避免缓存穿透



缓存穿透是请求多次访问缓存不存在的数据，导致请求都落在数据库上。

解决办法：

1. 用布隆过滤器，把所有可能存在的数据都放在bitmap中进行过滤。
2. 将查询为空的数据也存到缓存中，并设置过期时间。





## 主从复制模式下，主挂了怎么办



redis有哨兵节点，可以监控主节点的故障，并转化主节点。





## Redis IO多路复用



采用Reactor模型的形式，实现一个线程可以处理多个IO。





Redis如何处理高并发



