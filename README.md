# articles-read

| 文章      | 类别    | 阅读时间  | 内容概要 | 阅读感受 |
| -------- | ------- | -------- | ------- |  ------- |
| [what-we-got-right-what-we-got-wrong](https://commandcenter.blogspot.com/2024/01/what-we-got-right-what-we-got-wrong.html)  | `go`    | 2/1/2024 | go 语言作者 rob pike 总结语言设计过程中的得失     | |
| [Git’s database internals I: packed object store](https://github.blog/2022-08-29-gits-database-internals-i-packed-object-store/#object-store-queries)  | `git`    | 2/1/2024 | git 内部存储机制: 对象查询以及 packfile 原理; 同时文章也对 git 和常用数据库的存储机制做了比较     | 加深了对 git 存储, 查询, 压缩的理解, 对设计文件系统应用很有启发 |
| [2021-11-26-so-you-want-git-database](https://www.dolthub.com/blog/2021-11-26-so-you-want-git-database/)  | `git` `database`   | 2/2/2024 | 介绍了当前用 git 来做 db 的一些实践, 给出了一些 link 资源, 同时又介绍了一些有版本管理功能的数据库, 包括 doltdb    | 不错的介绍性文章, 把对版本管理数据库的需求讲清楚了, 也给出了一些现有方案; 其中 doltdb 能同时像 git 一样做版本管理, 通过类 git 的命令行管理数据, 又能像 mysql 一样用 sql 操作, 连使用习惯都兼容, 比较惊艳 |
| [git-nosql-database](https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/)  | `git` `database`    | 2/2/2024 | 通过 plumbing 命令演示了创建 blob, tree, commit 来创建一个有版本记录的 nosql store, 并介绍了 git 作为 nosql 的各种优劣, 包括: 性能, 工具, 事务, 并发, 查询, 存储效率等等  | 本文对于 git 作为 nosql 的选型, 优劣给出了很多分析; 总结一下, 优势: 支持层级结构, 版本追踪, 支持存储对象文件, 工具完善(例如可视化); 劣势: 性能慢, 尤其是并发写的场景, 查询限制于通过 object id |
| [turning-git-into-an-application-database](https://nede.dev/blog/turning-git-into-an-application-database)  | `git` `database`    | 2/2/2024 | 作者用 git 作为带有版本管理功能存储, 做了一个简单的应用, 基于 non-base 仓库做 CRUD     |  文章没有提到 git 原理, demo 很简单, 性能也比较一般, 只能算是一个 proof of concept |
| [2022-08-30-gits-database-internals-ii-commit-history-queries/](https://github.blog/2022-08-30-gits-database-internals-ii-commit-history-queries/)  | `git` `database`    | 2/3/2024 | 介绍了 commit 查询时候的诸多优化以及实现, 例如: commit-graph(其实就是一个表) 作为索引, 避免每次解析 object store 来找 parent; 通过 generation number 的使用给判断 reachability 做剪枝, 再例如优化 top sort, 让 git log --graph 的时候增量显示, 而不是全量做一些排序     |  了解了 commit 查询的诸多原理, 在之前的项目里曾尝试使用 git branches --contains, 后因性能问题放弃了, 这篇文章从更底层的角度帮助理解了 git 的 commit 查询, 给之前的判断做映证 |
| [introduction-to-rolling-hash-data-structures-and-algorithms](https://www.geeksforgeeks.org/introduction-to-rolling-hash-data-structures-and-algorithms/)  | `algorithm`    | 2/4/2024 | 介绍了 rolling hash 算法, 使用场景以及优缺点 | rolling hash 类似于滑窗计算, 优势有计算快, 内存使用少, 缺点有易有 hash 冲突;适用于流式去重, 计算, 识别等场景 |
| [testing-distributed-systems-for-linearizability](https://anishathalye.com/testing-distributed-systems-for-linearizability/)  | `distributed system`    | 2/7/2024 | 介绍了 linearizability 的定义以及测试方法 | 了解了 linearizability 的定义, 之前一直分不清和 serializability 的区别, linearizability 相比于 eventual consistency 更严格, 但是没有 serializability 严格, 市面上绝大部分分布式数据库都是按照 linearizability 作为标准; 文章中的测试方法介绍了 ad-hoc 方法和通用的方法, 通用方法需要解一个 NP 问题, 给出了一些开源的实现, 算是抛砖引玉 |
| [supply-chain](https://go.dev/blog/supply-chain)  | `go`    | 2/9/2024 | 介绍了 go 语言有助于软件供应链安全的机制, 包括: 通过 gosum 锁死依赖, 以 vcs 作为 source of truth, 中心的 sumdb 做效验, 禁止 postinstall 机制, 推崇 copy is better than dependencies  | go 相比于 python, c++ 等语言在包管理方面有很大的不同, python 是通过集中式的仓库做包管理, 集中式的仓库增大了攻击面, go 只通过 vcs 来分发软件; 中心式的 sumdb 是个优秀的设计, 其他语言都是在 client 让用户自己维护 checksum, 中心的 sumdb 增加了权威性; copy is better than dependencies 是个惊艳的理念, 一般的语言都会提倡 reusability, go 通过 copy 简化了依赖管理, 加快了构建速度  |
| [不敢把数据库运行在 K8s 上？容器化对数据库性能有影响吗？](https://www.infoq.cn/article/Sh2TJYW1dKI4ZqpakUJJ)  | `database` `k8s` | 2/9/2024 | 文章第一部分简单介绍了几种虚拟化技术原理: runc, kdata container, gvistor, firecracker, 第二部分从 cpu, mem, cni, disk io, network io 等多个角度比较几种虚拟化技术的表现; 第三部分跳出了容器话题, 讲了一些常见的数据库性能问题: To many connections, disk IO hang, OOM, etc  |  第一部分非常 high level 地了解了 runc, kdata container, gvistor, firecracker 的原理; 第二部分 gvistor 在 syscall 多的场景下表现最差, 其余 kdata, firecracker 等性能损失不大; 第三部分比较精彩, 比较深入地从原理角度介绍不同数据库面临的问题, 收获较多  |
| [when-to-use-pointers-in-go](https://medium.com/@meeusdylan/when-to-use-pointers-in-go-44c15fe04eac)  | `go` | 2/16/2024 | 介绍 go pass by ref 和 pass by value 怎么选, 什么时候应该用 pointer  |  pointer 性能好, 但是容易造成 side effect, 难以 debug; 之前个人的感觉式 plain old data 用 pass by value, 大型 struct 用 pointer; 这篇文章又从原理上梳理了一下应该用 pointer 的场景: Copying large structs, Mutability, Signify true absence, 真正需要 pointer 的时候才用, 其余时候考虑时候 pass by value ; go 因为有垃圾回收机制, pointer 相比于 C 语言 overhead 更大; |
| [gits-database-internals-iii-file-history-queries](https://github.blog/2022-08-31-gits-database-internals-iii-file-history-queries/)  | `git` `database` | 2/17/2024 | 刨析 git log 的底层查询实现  | 说到底 git log -- path 的查询本质上还是在对 commit 做遍历, 对 commit 和 parent commit 的 tree 做比较, 如果在 path 路径有改动, 则在 git log 里显示; 在此基础上尽可能做性能优化, 例如 commit-graph, bloom-filter, simplified-history 等技术 |
| [深入理解go sync.Map设计与实现](https://zhuanlan.zhihu.com/p/641411129)  | `go` | 2/19/2024 | 刨析 sync.Map 实现 | [orcaman/concurrent-map](https://github.com/orcaman/concurrent-map) 通过分片实现一个并发的 map, 相对来说比较通用; 相对地, sync.Map 的核心是读写分离, 实现了一个适用于读多写少场景的并发 map |
| [2022-09-02-gits-database-internals-v-scalability](https://github.blog/2022-09-02-gits-database-internals-v-scalability/)  | `git` `database` | 2/20/2024 | 介绍一些分片方式, 根据时间纵向分片, 以及根据 worktree 横向分片, 比如: multi-repo, git submodule | 根据 worktree 切片的方法在公司搞 monorepo 时候已经摸透了, 文章里介绍的根据时间切片方式之前没想到过, 虽然会打断开发, 但也算是一种思路吧 |
| [实现幂等的8种方案](https://blog.csdn.net/m0_71777195/article/details/128897222/)  | `git` `database` | 2/26/2024 | 介绍了实现幂等的方式: ID 生成, 悲观锁, 乐观锁, etc  | 通过防重 + 幂等 能实现 "at most once", 但是没有办法保证 "exactly once", 如果第一次执行请求, 执行到一半服务崩了, 重试的请求发现防重表里已经有了请求 ID, 就不执行了; 针对这种情况的处理方式文章没有讲到, 在我看来可以加分布式锁解决, (1) 检查防重表 (2) 如果没执行过就加锁 (3) 再检查防重表以防 step1 step2 之间有其他线程执行 (4) 执行业务逻辑 (5) 更新防重表, 当然这个分布式锁实现性能消耗比较大; 除了这个实现外还有一些其他思路, 比如类似 raft 的 leader 机制, 保证只有一个 leader 执行写, 通过 log 记录执行记录, 再将 log 复制给 follower, 及时 leader 奔溃, 新选举的 leader 根据 log 继续执行 |
| [Go 语言编程模式实战](https://time.geekbang.org/opencourse/intro/100069501?utm_campaign=geektime_search&utm_content=geektime_search&utm_medium=geektime_search&utm_source=geektime_search&utm_term=geektime_search)  | `go` | 2/28/2024 | 介绍了 go 的几种编程范式, 比如: 委托, 装饰器, pipeline 模式, map/reduce, etc, 以及一些性能方面的 tip | 加深了对 go 编程的理解, 文章中一些性能的 tips 也比较实用, 日常的编程过程中容易忽略 |
| [go语言实现雪花算法](https://zhuanlan.zhihu.com/p/373485947)  | `golang` | 3/1/2024 | 介绍了雪花算法 go 实现 | 在实现 6.840 lab2 时候需要每个 client 对应一个 id, 雪花算法正好合适, 这篇文章结合 [bwmarrin/snowflake](https://github.com/bwmarrin/snowflake) 源码一起看效果更佳 |
| [Debug symbol wiki](https://en.wikipedia.org/wiki/Debug_symbol)  | `os` | 3/8/2024 | 介绍了什么是 debug symbol | 复习一下 debug symbol 概念; debug symbol 包含 var name, line num, class num, filename 等等, 基本相当于源代码, 体积较大 |
| [Core dump wiki](https://en.wikipedia.org/wiki/Core_dump)  | `os` | 3/8/2024 | 介绍了什么是 core dump | 复习一下 core dump 概念, 内存在 crash 时刻的 dump, 以及寄存器的状态, 但是没法识别变量和数据结构, 需要 symbol table 才能 debug |
| [python 实现惰性求值](https://zhuanlan.zhihu.com/p/420508064)  | `functional programming` | 3/12/2024 | 介绍 python 实现 FP 里的惰性求值(python 原生并不支持惰性求值) |  |
| [惰性求值 wiki](https://zh.wikipedia.org/zh-cn/%E6%83%B0%E6%80%A7%E6%B1%82%E5%80%BC)  | `functional programming` | 3/12/2024 | 惰性求值定义 |  |
| [闭包 wiki](https://zh.wikipedia.org/zh-cn/%E9%97%AD%E5%8C%85_(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6))  | `functional programming` | 3/17/2024 | 闭包定义 | 使用场景: 高阶函数, 装饰器, 柯里化, etc |
| [用 js 实现柯里化](https://zhuanlan.zhihu.com/p/355859667)  | `functional programming` | 3/17/2024 | 柯里化在 js 语言里的实现 |  |
| [排序算法复习](https://leetcode.cn/problems/sort-an-array/solutions/179489/fu-xi-ji-chu-pai-xu-suan-fa-java-by-liweiwei1419)  | `algorithm` | 3/17/2024 | 介绍了多种排序算法, 例如: 选择排序, 冒泡排序, 快速排序, 归并排序, 插入排序 | 平时开发过程中直接调用库, 很多排序算法的细节和取舍都忘了, 这次正好复习一下; 重点复习归并排序和快速排序, 选择排序在小范围数组内(或者接近有序)也比较不错, 其他几种了解即可 |
| [mergesort 对比 quicksort](https://stackoverflow.com/questions/70402/why-is-quicksort-better-than-mergesort)  | `algorithm` | 3/17/2024 | mergesort vs quicksort, quicksort 的优势 | mergesort 是稳定排序(保留函数相对位置), 需要额外的空间存临时数组, quicksort 不需要额外的空间, 而且可以更好地利用 cpu 缓存(inplace 以及顺序遍历), 所以在很多编程语言默认的排序都是快速排序, 快速排序通过随机选 pivot, 一般也不会回退到 O(N^2) |
| [无锁 HASHMAP 的原理与实现](https://coolshell.cn/articles/9703.html)  | `algorithm` | 3/19/2024 | 介绍了无锁 hashmap 的实现思路, 以及细节, 包括插入, 删除, rehash | 无锁的 hashmap 的插入, 删除都是基于 CAS 实现, rehash 部分一些细节没有看地很懂, 大概是保证 rehash 前就维护一个链表保证节点之间有序, rehash 之后因为还是原来的顺序, 节点之间相对问题不变, 只要改哨兵节点就行了; 顺便复习了一下 java hashmap 的实现, (1) 对 key 算 hashcode 得到整形, (2) 对数组长度取 mod 得到索引 (3) 然后维护索引对应的链表; rehash 取决于冲突的 slot 是否超过负载因子(默认 0.75)和数组长度的乘机, 所以负载因为越大, 空间利用率约高, 因子约小, hash 冲突越少  |
| [我做系统架构的一些原则](https://coolshell.cn/articles/21672.html)  | `architecture` | 3/19/2024 | 介绍了一些系统架构方面的原则  | 比较有感触的点有: "完备性会比性能更重要", "绝大多数情况下，如无非常特殊要求，选 Java基本是不会错的", "不要依赖自己的经验，要依赖于数据和学习", "制定并遵循服从标准、规范和最佳实践", "激进胜于保守，创新与实用并不冲突", etc  |
| [全文图解 Golang 调度器 GMP 原理与调度](https://zhuanlan.zhihu.com/p/288017699)  | `golang` | 3/21/2024 | 详细介绍了 GMP 模型, 以及给出了很多具体的调度场景  | 一些要点: Goroutine 较轻量, 大概只占几 KB; 调度模型原先有一个全局的任务队列, GMP 模型里每个 M 都有个本地 P 队列, 通过分片的思路减少竞争; goroutine 的最大切片是 10ms, 避免 starving |
| [What is Load Average in Linux?](https://www.digitalocean.com/community/tutorials/load-average-in-linux#getting-familiar-with-the-load-average-in-linux)  | `linux` | 3/22/2024 | 介绍 sys load 这个概念, 以及可以通过 uptime | sys load 是过去一段区间内正在运行以及在 waitlist 上的进程数, 体现了当前系统的负载量以及排队情况; 相对地 cpu 负载是 cpu 视角, 体现 cpu 的使用率 |
| [Python 内存管理](https://www.cnblogs.com/TMesh/p/11731010.html)  | `python` | 3/25/2024 | 垃圾回收, 分代回收, 引用计数, 小整数池, 内存池 |  |
| [编程范式游记](https://time.geekbang.org/column/intro/100031901?utm_campaign=geektime_search&utm_content=geektime_search&utm_medium=geektime_search&utm_source=geektime_search&utm_term=geektime_search&tab=catalog)  | `PL` | 3/26/2024 | 介绍了各种编程范式以及其演进, 从 C 开始介绍, 引申出 C++ 的泛型编程, 再到函数式编程, OOP, 原型编程, 算是 high level 地把编程范式理了一遍, 最后总结编程的本质: 逻辑和控制的解耦(其实就是业务和非业务解耦) | 类型式内存的抽象; 泛型, 高阶函数, 装饰器等特性都是为了抽象, 让代码更通用; 函数式编程优势: 没有状态就没有伤害, 结果确定, 容易做并行, 劣势: 复制严重 ; 函数式编程是声明式编程, 比如 map/reduce 而不是 for/while; 原型编程其实式用了委托的思想;  |
| [AppImage introduction](https://docs.appimage.org/introduction/index.html)  | `packaging` | 3/29/2024 | 介绍了一种 linux 下的打包格式, 思路就是打一个 allinone 的包(包含 runtime lib)来解决依赖管理问题, 以及兼容性问题, 可以做到同一个 appImage 在不同发行版之间兼容 | 设计思路上类似静态编译, 但是一个是编译期, 一个是打包期 |
| [diagnostics](https://go.dev/doc/diagnostics)  | `go` | 3/302024 | 介绍 go 语言的 profiling, debug tools, tracing 工具 | 偏工手册类型的介绍, 用到时候翻翻; 其他感受: go 所有调试的工具都集成在了标准库和 go 命令行里, 标准化做地不错 |
| [settings-sync](https://code.visualstudio.com/docs/editor/settings-sync)  | `vscode` | 4/7/2024 | 介绍 vscode 同步配置功能 | 一直以来都是 vscode 用户, 之前每次换开发机都是手动配置, 比较低效, 用了 settings sync 功能方便很多; 按照文档里的实际操作一遍, 在 vscode web 上同步本地上传的 settings, 有一些 extentions 因为不兼容 vscode web 没同步成功(比如: copilot), 所以 settings sync 也会受兼容性影响, 总体而言可用  |
| [Go Channel 详解](https://colobu.com/2016/04/14/Golang-Channels/)  | `go` | 4/18/2024 | 介绍 go channel 的使用方式, 特性, 例如: send, receive, buffered channel, close,  timer, timeout 以及如何和 select 搭配使用 |   |
| [fish tutorial](https://fishshell.com/docs/3.0/tutorial.html)  | `shell` | 4/22/2024 | 介绍 fish 相关特性, 覆盖比较权限 | 趁入职新公司的机会尝试 fish, fish 相比 bash 高亮, 填充等特性更好; 相比于 zsh, 更加开箱即用; 相比于 nushell 更加符合 posix 规范, 但是需要注意的是即便比 nushell 更加保守, 但 fish 也不是完全兼容 posix shell 语法 |
| [gitlab remote development](https://docs.gitlab.com/ee/user/project/remote_development/)  | `cloud ide` | 4/23/2024 | 介绍基于 gitlab 做云开发相关功能  | 读下来有一点困惑的是 gitlab 看上去是通过 https 连到环境里, 而不是 ssh, 目前其他主流的工具都是通过 ssh; 具体配置的时候通过在环境侧配置 cert/pem 以及 gitlab endpoint, 然后通过 web ide 连接 host:3443 端口建立连接; 这个流程里只有 https 完全没有 ssh, 这个让我对实现原理有一些困惑 |
| [冒烟测试](https://www.cnblogs.com/amberdyy/p/8434714.html)  | `software testing` | 4/24/2024 | 介绍了冒烟测试的概念, Smoke Testing 在软件测试中的意义，应该说取的是其原始概念中的目的而非手段。通过 Smoke Testing，在软件代码正式编译并交付测试之前，先尽量消除其表面的错误，减少后期测试的负担。因此可以说，Smoke Testing 是预测试,  冒烟测试就是新版本送测后的测试，以决定是否要继续测试乃至发布。回归测试就是解决一个问题后的测试，方向是判断新的代码是否引入了新问题。冒烟测试一般用于每日构建(Nightly build)，构建服务器首先从CVS服务器上，下载最新的源代码，然后编译单元测试，运行单元测试通过后，编译可执行文件，可执行文件若可运行，并能执行最基本的功能，则认为通过了冒烟测试。而回归测试，是软件维护阶段对软件修改后进行的测试。两种测试用在软件生命的不同周期。| 收获: 什么是冒烟测试, 以及和回归测试的区别 |
| [CCache 计算缓存原理](https://ccache.dev/manual/4.9.1.html#_how_ccache_works)  | `cmake` | 4/24/2024 | 介绍了 ccache 计算缓存命中的方式, 有三种模式: preprocessor, direct, depend; 通用的 hash 输入有编译器信息, 例如: 编译器体积大小, 修改时间, 源文件后缀(.cc or .ii); preprocessor 模式会运行预处理器后计算 hash, 有较大的 cost, 计算 hash 的输入有预处理后的文件, 除了影响 preprocess 阶段的其他所有编译选项(-I 因为值只影响 preprocess 阶段, 所以可以排除), 以及 preprocessor 产生的 stderr; direct 对编译选项以及源文件计算 hash, 通过比较 include files 的 hash 和缓存时刻的 hash 有没有变化判断缓存是否命中, 如果缓存时刻的 hash 相关 meta 找不到, fallback 到 prerocessor 模式; depend 模式完全不跑 preprocessor, 通过 direct 模式的信息加上 -MD/-MMD 生成的依赖清单做 hash, 好处是 cost 较小, 以及适合 dist cc 这种远程编译场景, 坏处是 hit rate 变低, 因为任何 preprocessor 编译选项都导致 cache miss, 另外: -MD 会带上 system include file, -MDD 不会  | 相比于 bazel 缓存, ccache 是个编译器级别的缓存, 对编译选项识别准确, 对应的, bazel 压根对编译选项无感, 在 action 层面的东西, 不管是什么编译选项, 作为 action 的一个输入, 变动就重编译 |
| [为什么你该试试 Sccache?](https://cloud.tencent.com/developer/article/2217552)  | `ccache` | 4/25/2024 | 简单介绍了 sccache 原理, 和 rust-cache 比较, 以及 github action service 原理  |  |
| [一文掌握 Go 并发模式 Context 上下文](https://juejin.cn/post/7233981178101186619)  | `go` | 4/24/2024 | 介绍 go context 使用方式, 以及使用场景, 例如: 超时控制, 传递取消信号, 结束任务 | 读完的感受就是 go 对并发的支持是真好... |
| [浅谈Linux Cgroups机制](https://zhuanlan.zhihu.com/p/81668069)  | `linux` | 4/27/2024 | 介绍 cgroup 各个子系统: cpu, cpuacct, cpuset, memory, blkio; 以及两个通过 cgroup 限制 cpu(cpu.cfs_period_us, cpu.cfs_quota_us), mem(memory.limit_in_bytes) 的操作示例 |  |
| [cgroup cpu 子系统的总结](https://blog.csdn.net/weixin_46040684/article/details/121855201)  | `linux` | 4/27/2024 | 介绍了 cpu 系系统, 以及给出通过修改 cpu.shares 控制 cpu 使用占比的操作示例 |  |
| [incredibuild introduction](https://docs.incredibuild.com/lin/latest/linux/introduction.html?tocpath=Getting%20Started%7C_____1)  | `build system` | 4/29/2024 | incredibuild 介绍, incredibuild 无需代码修改, 通过一层 wrapper 触发分布式编译, 将构建分发到多台服务器上, 组成上分为 coordinator 以及 agent; 同时配有 monitor 作为 profiling  | 我个人对分布式编译的看法是收益越来越小了, 因为现在云上单机就能有几百个 cpu; 分布式编译主要还是适用于超大型项目, 比如: 整车集成, 单代码就有几百 G, 单机怎么都不够 |
| [现在的编译器对 CPU 需求如何，在相同的 CPU 框架下是主频高编译的快还是核心多编译的快？](https://www.zhihu.com/question/306760258)  | `build system` | 4/29/2024 | 取决于项目的并行度, 编译选项, 具体哪个快需要做测试; 简化的公式, freq * core num, 具体还是取决于项目的并行度, 有 critical path 时候 freq 高有优势, 并行情况 core num 更重要 |
| [linux 的 tmpfs 和/dev/shm目录的详细介绍](https://zhuanlan.zhihu.com/p/650723391)  | `linux` | 4/30/2024 | 介绍 linux tmpfs 和 dev/shm, tmpfs 是利用内存作为 vfs 的技术, /dev/shm 就是一个 tmpfs  |
| [bazel vs cmake benchmarking](https://www.kai-wolf.me/blog/2021/04/16/bazel-cmake-performance-comparisons/)  | `build system` | 4/30/2024 | bazel 和 cmake 的效率对比, 给出了直观的可视化图表 | |
| [Ninja 加速](https://zhuanlan.zhihu.com/p/634589665/)  | `build system` | 4/30/2024 | 简单介绍了 ninja 构建系统的原理, 如何通过 cmake 生成 ninja 配置文件, ninja 的并行实现原理, ninja 相比于 make 任务并行度更加高 | |
| [详解子网技术](https://blog.csdn.net/baijaiyu/article/details/129023242)  | `linux` | 5/2/2024 | 介绍了IP地址的划分, 网络编号的规定, 主机编号的规定, 什么是子网技术, 为什么要划分子网, 子网掩码, 子网划分的方法  | 最近在学习容器网络技术, 需要很多网络相关的知识, 很多欠缺的都需要补充 |
| [docker-and-the-pid-1-zombie-reaping-problem](https://blog.phusion.nl/2015/01/20/docker-and-the-pid-1-zombie-reaping-problem/)  | `docker` | 5/2/2024 | 介绍了 docker 僵尸进程问题, 没有被父进程 waitpid 收割的进程称为僵尸进程, 一般操作系统的 pid1 systemd 负责回收僵尸进程, 在 docker 内也是需要 pid1 进程回收僵尸进程, 如果没有被收割, docker 内的僵尸进程就会占用主机的 pid 资源, 可能会把 pid 表占满, 所以如果 docker 内如果是多进程应用, 需要有一个类似 [tini](https://github.com/krallin/tini) 的轻量 init 程序负责收割僵尸进程, 此外 pid1 的程序也需要作为 signal handler, 当用户 ctrl-c 发送 signterm 之后, pid1 需要向容器内各个进程发送信号要求退出, 不然用户会发现 docker stop 卡在那, tini 也有 signal handler 的功能  | 之前面试时候有被问到过类似的问题, 当时还以为容器内的僵尸进程会被主机的 systemd 回收, 这次才真正把问题搞明白  |
| [docker-init-zombies-why-does-it-matter](https://stackoverflow.com/questions/49162358/docker-init-zombies-why-does-it-matter)  | `docker` | 5/2/2024 | docker 目前原生支持 init 参数自动一个 tini 程序收割僵尸进程以及 signal handler, 来解决 `docker-and-the-pid-1-zombie-reaping-problem` 提到的问题 |   |
| [C++ 加快编译速度的方法](https://blog.csdn.net/xhtchina/article/details/112801885)  | `C++` | 5/2/2024 | C++ 编译慢主要每个编译单元都要读取大量头文件, 导致大量 IO, 以及链接只能串行; 可以从几个方向做优化, 代码层面实现和接口分离, 减少预处理器的负担, 以及头文件模块化, 单个文件改动减少重编译的量, 具体措施: (1) 在头文件中使用前置声明，而不是直接包含头文件 (2) 使用Pimpl 模式 (3) 高度模块化 (4) 删除冗余的头文件 (5) 注意 inline 和 template 中包含实现 (6) shared lib 比 header lib 节省时间, 链接也 static lib 快; 综合技巧, (1) 预编译头文件, (2) Unity Build (3) Ccache (4) 不要有太多的Additional Include Directories 避免大量搜索; 资源层面 (1) 并行编译 (2) 更好的磁盘 (3) 分布式编译  |   |
| [docker-init-zombies-why-does-it-matter](https://stackoverflow.com/questions/49162358/docker-init-zombies-why-does-it-matter)  | `docker` | 5/2/2024 | docker 目前原生支持 init 参数自动一个 tini 程序收割僵尸进程以及 signal handler, 来解决 `docker-and-the-pid-1-zombie-reaping-problem` 提到的问题 |   |
| [why-does-c-compilation-take-so-long](https://stackoverflow.com/questions/318398/why-does-c-compilation-take-so-long)  | `docker` | 5/3/2024 | 1, 同一个 header 文件会被多个编译单元重复解析, 预处理, 同时造成大量 io; 2, link 没法并行; 3, parse 耗时; 4, C++ 编译器会做优化, 增加编译期耗时,  e.g. O2, O3; 5, template 被预处理本身就很复杂, 并且每个使用 template 的编译单元都需要处理一遍 template|   |
| [GO 笔记之详解 GO 的编译执行流程](https://zhuanlan.zhihu.com/p/62922404)  | `go` | 5/11/2024 | go 语言构建过程, 可以通过 go build 加参数把详细的编译过程打印出来, 编译过程和 C++ 有类似, 但是少了预处理流程 |   |
| [Go 语言编译优化](https://zhuanlan.zhihu.com/p/359910206)  | `go` | 5/11/2024 | upx 代壳压缩二进制能减少 60% - 70% 体积; 通过编译选项去除调试信息以及符号表, 能减少 20% 体积 |   |
| [Go 的编译为什么快](https://blog.csdn.net/qq_34417408/article/details/109716015)  | `go` | 5/11/2024 | 文章把 go 和 C++ 编译做对比, 解释了为什么 go 编译比 C++ 快; 1, import 不需要重复编译, 而 include 需要, 2, go 语法简单, 编译器语义和语法解析更快, 3, 没有模板的负担(go 1.18 之后也支持泛型了) |   |
| [golang 的编译速度真是震撼](https://zhuanlan.zhihu.com/p/20086295#!)  | `go` | 5/11/2024 | 直观对比了 C++ 和 go 的编译速度, 原来需要编译 10 - 20 mins 的项目, go 只需要 20s | |
| [golang 微服务编译速度过慢？](https://zhuanlan.zhihu.com/p/667714896)  | `go` | 5/11/2024 | Go语言编译慢的原因和优化方法。主要内容包括: 通过设置 GOMODCACHE 环境变量, 可将依赖缓存到本地,避免重复下载。设置 GOCACHE 环境变量, 存放编译中间文件, 重用以提升编译速度。使用 gcflags 关闭优化(如函数内联), 可缩短编译时间, 但会影响运行时性能。配置网络代理, 提高依赖下载速度。挂载相关缓存目录到宿主机, 方便容器重建时复用 |   |
| [go 是否支持增量构建？](https://tonybai.com/2022/03/21/go-native-support-incremental-build/)  | `go` | 5/13/2024 | go 是以 package 为编译单元做增量构建的, 不同的 package 构建出 .a, 当 package 中某个文件修改之后, 只会构建对应 package 的 .a, 以及下游 package, 如果是 go build main 的话需要重新做链接; 这篇文章通过示例演示增量构建 |   |
| [go 编译提速优化？](https://blog.fishedee.com/2016/04/30/golang%E7%BC%96%E8%AF%91%E6%8F%90%E9%80%9F%E4%BC%98%E5%8C%96/#%E6%A6%82%E8%BF%B0)  | `go` | 5/13/2024 | 介绍通过 go install 实现增量构建(比较过时, 新版 go 中的 go build 已经实现了增量构建), 依赖以及 indirect 依赖的导出符号数量会影响链接速度, 可以通过减少依赖的导出符号减少链接时间  |   |
| [cmake-with-subdirectories](https://stackoverflow.com/questions/42744315/cmake-with-subdirectories)  | `build system` | 5/18/2024 | 介绍了 cmake 的组织方式, 例如: 全局维护一个 cmakelist.txt vs 每个子目录维护一个 cmakelist.txt, 每个子目录维护一个 cmakelist.txt 然后通过 add_subdirectory 更加推荐一些, 避免冲突, 而且每个 cmakelist.txt 都有一个独立的变量域  |   |
| [使用 pkg-config 让 C++ 工程编译配置更灵活](https://zhuanlan.zhihu.com/p/417285806)  | `build system` | 5/18/2024 | pkg-config 介绍  |   |
| [GNU Autotools 介绍](https://zhuanlan.zhihu.com/p/77904822)  | `build system` | 5/18/2024 |  |   |
| [what-are-the-differences-between-autotools-cmake-and-scons](https://stackoverflow.com/questions/4071880/what-are-the-differences-between-autotools-cmake-and-scons)  | `build system` | 5/18/2024 |  |   |
| [C 语言中的强符号与弱符号](https://blog.csdn.net/astrotycoon/article/details/8008629)  | `build system` | 5/18/2024 | 介绍了强弱符号的概念, 给出了示例演示各种场景, weak vs strong, week vs week, strong vs strong |   |
| [epoll、poll、select 的原理和区别](https://blog.csdn.net/wwwvipp/article/details/119888373)  | `linux` | 5/18/2024 | epoll 条件触发, 红黑树注册回调, 事件驱动, 只遍历/拷贝有事件的 fd, 用户态内核态之间拷贝较少; select, poll 都是遍历拷贝所有 fd, 性能较差, select 受进程 fd 数量限制, poll 为链表结构不受 fd 限制 |   |

## To read

- [为什么你应该用 sccache](https://cloud.tencent.com/developer/article/2217552)
- [深入浅出：Go语言编译原理与过程解析](https://cloud.tencent.com/developer/article/2401918)
- [sccache github](https://github.com/mozilla/sccache)
- [Modern cmake](https://modern-cmake-cn.github.io/Modern-CMake-zh_CN)
- [Gitpod 介绍](https://www.gitpod.io/)
- [Docker 容器网络详解](https://www.cnblogs.com/zuxing/articles/8780661.html)
