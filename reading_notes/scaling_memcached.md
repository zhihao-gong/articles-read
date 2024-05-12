# Scaling Memcache at Facebook 阅读笔记

## 简介

论文讲述了 facebook 基于开源的单机 memcache 改造, 打造一个分布式低延迟高吞吐高可用缓存集群

### Overview architecture

更新策略: cache aside

<img src="memcached_cache_aside.png" alt="alt text" width="500"/>

总体架构如下:

<img src="memcached_architecture.png" alt="alt text" width="500"/>

## 低延迟

低延迟相关的优化基本在 client 端

### Batch request

尽可能批量/并行发送请求, 减少 round trip, 增加 concurrency

### Client server 交互

Get 请求用 udp, 而不是 tcp, 以此降低延迟, 会有 0.25% 的请求由于丢包(80%), out of order(20%) 等问题出错, 碰到这种情况 client 直接当 cache miss, 算是一种为了低延迟的 tradeoff, 毕竟 memcached 主要作为 cache, 可允许一定程度的不可用性

Set, Delete 请求依然用 tcp, 通过 mcrouter 降低 tcp 链接的数量, 以此节省 cpu, mem, 带宽等资源

注: mcrouter 是一个 client-side proxy, 可以作为 lib 在 client 进程中调用, 也可以作为一个独立的前向代理进程

下图是 tcp 和 udp 在延迟方面的对比, udp 的延迟大概比 tcp 低 20%

<img src="memcached_tcp_vs_udp.png" alt="alt text" width="500"/>

### 限流

Client 端会用滑窗限流, 这里让我有点想不明白的是居然不是在 server 端来做集中限流

Client 端限流没有 server 的负载情况很难全局性做出最佳限流策略

下图是窗口大小对延迟的影响, 窗口约小, 平均延迟越大, 窗口库越大, server 负载越大

<img src="memcached_client_sliding_window.png" alt="alt text" width="500"/>

## 参考

[Scaling Memcache at Facebook](https://pdos.csail.mit.edu/6.824/papers/memcache-fb.pdf)
