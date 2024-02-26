# articles-read

| 文章      | 类别    | 阅读时间  | 内容概要 | 阅读感受 |
| -------- | ------- | -------- | ------- |  ------- |
| [what-we-got-right-what-we-got-wrong](https://commandcenter.blogspot.com/2024/01/what-we-got-right-what-we-got-wrong.html)  | `golang`    | 2/1/2024 | go 语言作者 rob pike 总结语言设计过程中的得失     | |
| [Git’s database internals I: packed object store](https://github.blog/2022-08-29-gits-database-internals-i-packed-object-store/#object-store-queries)  | `git`    | 2/1/2024 | git 内部存储机制: 对象查询以及 packfile 原理; 同时文章也对 git 和常用数据库的存储机制做了比较     | 加深了对 git 存储, 查询, 压缩的理解, 对设计文件系统应用很有启发 |
| [2021-11-26-so-you-want-git-database](https://www.dolthub.com/blog/2021-11-26-so-you-want-git-database/)  | `git` `database`   | 2/2/2024 | 介绍了当前用 git 来做 db 的一些实践, 给出了一些 link 资源, 同时又介绍了一些有版本管理功能的数据库, 包括 doltdb    | 不错的介绍性文章, 把对版本管理数据库的需求讲清楚了, 也给出了一些现有方案; 其中 doltdb 能同时像 git 一样做版本管理, 通过类 git 的命令行管理数据, 又能像 mysql 一样用 sql 操作, 连使用习惯都兼容, 比较惊艳 |
| [git-nosql-database](https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/)  | `git` `database`    | 2/2/2024 | 通过 plumbing 命令演示了创建 blob, tree, commit 来创建一个有版本记录的 nosql store, 并介绍了 git 作为 nosql 的各种优劣, 包括: 性能, 工具, 事务, 并发, 查询, 存储效率等等  | 本文对于 git 作为 nosql 的选型, 优劣给出了很多分析; 总结一下, 优势: 支持层级结构, 版本追踪, 支持存储对象文件, 工具完善(例如可视化); 劣势: 性能慢, 尤其是并发写的场景, 查询限制于通过 object id |
| [turning-git-into-an-application-database](https://nede.dev/blog/turning-git-into-an-application-database)  | `git` `database`    | 2/2/2024 | 作者用 git 作为带有版本管理功能存储, 做了一个简单的应用, 基于 non-base 仓库做 CRUD     |  文章没有提到 git 原理, demo 很简单, 性能也比较一般, 只能算是一个 proof of concept |
| [2022-08-30-gits-database-internals-ii-commit-history-queries/](https://github.blog/2022-08-30-gits-database-internals-ii-commit-history-queries/)  | `git` `database`    | 2/3/2024 | 介绍了 commit 查询时候的诸多优化以及实现, 例如: commit-graph(其实就是一个表) 作为索引, 避免每次解析 object store 来找 parent; 通过 generation number 的使用给判断 reachability 做剪枝, 再例如优化 top sort, 让 git log --graph 的时候增量显示, 而不是全量做一些排序     |  了解了 commit 查询的诸多原理, 在之前的项目里曾尝试使用 git branches --contains, 后因性能问题放弃了, 这篇文章从更底层的角度帮助理解了 git 的 commit 查询, 给之前的判断做映证 |
| [introduction-to-rolling-hash-data-structures-and-algorithms](https://www.geeksforgeeks.org/introduction-to-rolling-hash-data-structures-and-algorithms/)  | `algorithm`    | 2/4/2024 | 介绍了 rolling hash 算法, 使用场景以及优缺点 | rolling hash 类似于滑窗计算, 优势有计算快, 内存使用少, 缺点有易有 hash 冲突;适用于流式去重, 计算, 识别等场景 |
| [testing-distributed-systems-for-linearizability](https://anishathalye.com/testing-distributed-systems-for-linearizability/)  | `distributed system`    | 2/7/2024 | 介绍了 linearizability 的定义以及测试方法 | 了解了 linearizability 的定义, 之前一直分不清和 serializability 的区别, linearizability 相比于 eventual consistency 更严格, 但是没有 serializability 严格, 市面上绝大部分分布式数据库都是按照 linearizability 作为标准; 文章中的测试方法介绍了 ad-hoc 方法和通用的方法, 通用方法需要解一个 NP 问题, 给出了一些开源的实现, 算是抛砖引玉 |
| [supply-chain](https://go.dev/blog/supply-chain)  | `golang`    | 2/9/2024 | 介绍了 golang 语言有助于软件供应链安全的机制, 包括: 通过 gosum 锁死依赖, 以 vcs 作为 source of truth, 中心的 sumdb 做效验, 禁止 postinstall 机制, 推崇 copy is better than dependencies  | golang 相比于 python, c++ 等语言在包管理方面有很大的不同, python 是通过集中式的仓库做包管理, 集中式的仓库增大了攻击面, golang 只通过 vcs 来分发软件; 中心式的 sumdb 是个优秀的设计, 其他语言都是在 client 让用户自己维护 checksum, 中心的 sumdb 增加了权威性; copy is better than dependencies 是个惊艳的理念, 一般的语言都会提倡 reusability, golang 通过 copy 简化了依赖管理, 加快了构建速度  |
| [不敢把数据库运行在 K8s 上？容器化对数据库性能有影响吗？](https://www.infoq.cn/article/Sh2TJYW1dKI4ZqpakUJJ)  | `database` `k8s` | 2/9/2024 | 文章第一部分简单介绍了几种虚拟化技术原理: runc, kdata container, gvistor, firecracker, 第二部分从 cpu, mem, cni, disk io, network io 等多个角度比较几种虚拟化技术的表现; 第三部分跳出了容器话题, 讲了一些常见的数据库性能问题: To many connections, disk IO hang, OOM, etc  |  第一部分非常 high level 地了解了 runc, kdata container, gvistor, firecracker 的原理; 第二部分 gvistor 在 syscall 多的场景下表现最差, 其余 kdata, firecracker 等性能损失不大; 第三部分比较精彩, 比较深入地从原理角度介绍不同数据库面临的问题, 收获较多  |
| [when-to-use-pointers-in-go](https://medium.com/@meeusdylan/when-to-use-pointers-in-go-44c15fe04eac)  | `golang` | 2/16/2024 | 介绍 golang pass by ref 和 pass by value 怎么选, 什么时候应该用 pointer  |  pointer 性能好, 但是容易造成 side effect, 难以 debug; 之前个人的感觉式 plain old data 用 pass by value, 大型 struct 用 pointer; 这篇文章又从原理上梳理了一下应该用 pointer 的场景: Copying large structs, Mutability, Signify true absence, 真正需要 pointer 的时候才用, 其余时候考虑时候 pass by value ; golang 因为有垃圾回收机制, pointer 相比于 C 语言 overhead 更大; |
| [gits-database-internals-iii-file-history-queries](https://github.blog/2022-08-31-gits-database-internals-iii-file-history-queries/)  | `git` `database` | 2/17/2024 | 刨析 git log 的底层查询实现  | 说到底 git log -- path 的查询本质上还是在对 commit 做遍历, 对 commit 和 parent commit 的 tree 做比较, 如果在 path 路径有改动, 则在 git log 里显示; 在此基础上尽可能做性能优化, 例如 commit-graph, bloom-filter, simplified-history 等技术 |
| [深入理解Golang sync.Map设计与实现](https://zhuanlan.zhihu.com/p/641411129)  | `golang` | 2/19/2024 | 刨析 sync.Map 实现 | [orcaman/concurrent-map](https://github.com/orcaman/concurrent-map) 通过分片实现一个并发的 map, 相对来说比较通用; 相对地, sync.Map 的核心是读写分离, 实现了一个适用于读多写少场景的并发 map |
| [2022-09-02-gits-database-internals-v-scalability](https://github.blog/2022-09-02-gits-database-internals-v-scalability/)  | `git` `database` | 2/20/2024 | 介绍一些分片方式, 根据时间纵向分片, 以及根据 worktree 横向分片, 比如: multi-repo, git submodule | 根据 worktree 切片的方法在公司搞 monorepo 时候已经摸透了, 文章里介绍的根据时间切片方式之前没想到过, 虽然会打断开发, 但也算是一种思路吧 |
| [实现幂等的8种方案](https://blog.csdn.net/m0_71777195/article/details/128897222/)  | `git` `database` | 2/26/2024 | 介绍了实现幂等的方式: ID 生成, 悲观锁, 乐观锁, etc  | 通过防重 + 幂等 能实现 "at most once", 但是没有办法保证 "exactly once", 如果第一次执行请求, 执行到一半服务崩了, 重试的请求发现防重表里已经有了请求 ID, 就不执行了; 针对这种情况的处理方式文章没有讲到, 在我看来可以加分布式锁解决, (1) 检查防重表 (2) 如果没执行过就加锁 (3) 再检查防重表以防 step1 step2 之间有其他线程执行 (4) 执行业务逻辑 (5) 更新防重表, 当然这个分布式锁实现性能消耗比较大; 除了这个实现外还有一些其他思路, 比如类似 raft 的 leader 机制, 保证只有一个 leader 执行写, 通过 log 记录执行记录, 再将 log 复制给 follower, 及时 leader 奔溃, 新选举的 leader 根据 log 继续执行 |

## To read

- [Go 语言编程模式实战](https://time.geekbang.org/opencourse/intro/100069501?utm_campaign=geektime_search&utm_content=geektime_search&utm_medium=geektime_search&utm_source=geektime_search&utm_term=geektime_search)
- [编程范式游记](https://time.geekbang.org/column/intro/100031901?utm_campaign=geektime_search&utm_content=geektime_search&utm_medium=geektime_search&utm_source=geektime_search&utm_term=geektime_search&tab=catalog)
