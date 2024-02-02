# articles-read

| 文章      | 类别    | 阅读时间  | 内容概要 | 阅读感受 |
| -------- | ------- | -------- | ------- |  ------- |
| [what-we-got-right-what-we-got-wrong](https://commandcenter.blogspot.com/2024/01/what-we-got-right-what-we-got-wrong.html)  | `golang`    | 2/1/2024 | go 语言作者 rob pike 总结语言设计过程中的得失     | |
| [Git’s database internals I: packed object store](https://github.blog/2022-08-29-gits-database-internals-i-packed-object-store/#object-store-queries)  | `git`    | 2/1/2024 | git 内部存储机制: 对象查询以及 packfile 原理; 同时文章也对 git 和常用数据库的存储机制做了比较     | 加深了对 git 存储, 查询, 压缩的理解, 对设计文件系统应用很有启发 |
| [2021-11-26-so-you-want-git-database](https://www.dolthub.com/blog/2021-11-26-so-you-want-git-database/)  | `git` `database`   | 2/2/2024 | 介绍了当前用 git 来做 db 的一些实践, 给出了一些 link 资源, 同时又介绍了一些有版本管理功能的数据库, 包括 doltdb    | 不错的介绍性文章, 把对版本管理数据库的需求讲清楚了, 也给出了一些现有方案; 其中 doltdb 能同时像 git 一样做版本管理, 通过类 git 的命令行管理数据, 又能像 mysql 一样用 sql 操作, 连使用习惯都兼容, 比较惊艳 |
| [git-nosql-database](https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/)  | `git` `database`    | 2/2/2024 | 通过 plumbing 命令演示了创建 blob, tree, commit 来创建一个有版本记录的 nosql store, 并介绍了 git 作为 nosql 的各种优劣, 包括: 性能, 工具, 事务, 并发, 查询, 存储效率等等  | 本文对于 git 作为 nosql 的选型, 优劣给出了很多分析; 总结一下, 优势: 支持层级结构, 版本追踪, 支持存储对象文件, 工具完善(例如可视化); 劣势: 性能慢, 尤其是并发写的场景, 查询限制于通过 object id |
| [turning-git-into-an-application-database](https://nede.dev/blog/turning-git-into-an-application-database)  | `git` `database`    | 2/2/2024 | 作者用 git 作为带有版本管理功能存储, 做了一个简单的应用, 基于 base 仓库做 CRUD     |  文章没有提到 git 原理, demo 很简单, 性能也比较一般, 只能算是一个 proof of concept |
