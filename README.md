HBase 0.95版中文文档翻译
===========



中文版序
--------
HBase新版 0.95 文档和0.90版相比，变化较大，文档补充更新了很多内容，章节调整较大。本翻译文档的部分工作基于颜开工作。英文原文地址在此处(http://hbase.apache.org/book.html). 旧版0.90版由颜开翻译文档在此处(http://www.yankay.com/wp-content/hbase/book.html). 0.95版翻译最后更新请到此处( http://abloz.com/hbase/book.html) 浏览。反馈和参与请到此处 (https://github.com/ablozhou/hbasedoc_cn) 或访问我的blog(http://abloz.com ),或给我发email(ablozhou@gmail.com)。

不定期将翻译成果更新到http://abloz.com/hbase/docbkx/book.html

致礼

周海汉

参与方式：
---------
  # 给本项目管理员Andy<ablozhou@gmail.com>发email，留下gmail邮箱，申请成为项目成员，可以简介一下自己：)
  # 
  # 用svn下载https://github.com/ablozhou/hbasedoc_cn/的文件，工作目录在docbkx_cn
  # 进行翻译，格式化和校对工作
  # 工作过程中不断向svn提交翻译阶段成果。
  # 不时更新工作进度，让大家了解进展。
  # 完成任务提交最终成果。
  # 修改任务进度为100%

最终版生成pdf供下载。

生成html方式
------------
You should install Apache maven environment.

Build on Linux:

In the trunk root directory, run command:
{{{
    $ mvn site
}}}
to generate book.html

or you can run:
{{{
    $ mvn -Donepage site
}}}
to generated onepage html.

the generated html is in target/docbkx


Andy Zhou
2013-1-7
----

{{{
目录

序
1. 入门
1.1. 介绍
1.2. 快速开始
2. 配置
2.1. Java
2.2. 操作系统
2.3. Hadoop
2.4. HBase运行模式:单机和分布式
2.5. ZooKeeper
2.6. 配置文件
2.7. 配置示例
2.8. 重要配置
2.9. Bloom Filter
3. 升级
3.1. 从HBase 0.20.x or 0.89.x 升级到 HBase 0.90.x
3.2. 从 0.90.x 到 0.92.x
4. The HBase Shell
4.1. 使用脚本
4.2. Shell 技巧
5. 数据模型
5.1. 概念视图
5.2. 物理视图
5.3. 表
5.4. 行
5.5. 列族
5.6. Cells
5.7. Data Model Operations
5.8. 版本
5.9. 排序
5.10. 列元数据
5.11. Joins
6. HBase 和 Schema 设计
6.1. Schema 创建
6.2. column families的数量
6.3. Rowkey 设计
6.4. Number 数量
6.5. 支持的数据类型
6.6. Joins
6.7. 生存时间 (TTL)
6.8. 保留删除的单元
6.9. 第二索引和替代查询路径
6.10. 模式设计对决
6.11. 操作和性能配置选项
6.12. 限制
7. HBase 和 MapReduce
7.1. Map-Task 分割
7.2. HBase MapReduce 示例
7.3. 在MapReduce工作中访问其他 HBase 表
7.4. 推测执行
8. HBase安全
8.1. 安全客户端访问 HBase
8.2. 访问控制
9. 架构
9.1. 概述
9.2. 目录表
9.3. 客户端
9.4. 客户请求过滤器
9.5. Master
9.6. RegionServer
9.7. 分区(Regions)
9.8. 批量加载
9.9. HDFS
10. 外部 APIs
10.1. 非Java语言和 JVM交互
10.2. REST
10.3. Thrift
11. 性能调优
11.1. 操作系统
11.2. 网络
11.3. Java
11.4. HBase 配置
11.5. ZooKeeper
11.6. Schema 设计
11.7. 写到 HBase
11.8. 从 HBase读取
11.9. 从 HBase删除
11.10. HDFS
11.11. Amazon EC2
11.12. 案例
12. 故障排除和调试 HBase
12.1. 通用指引
12.2. Logs
12.3. 资源
12.4. 工具
12.5. 客户端
12.6. MapReduce
12.7. NameNode
12.8. 网络
12.9. RegionServer
12.10. Master
12.11. ZooKeeper
12.12. Amazon EC2
12.13. HBase 和 Hadoop 版本相关
12.14. 案例
13. 案例研究
13.1. 概要
13.2. Schema 设计
13.3. 性能/故障排除
14. HBase 运维管理
14.1. HBase 工具和实用程序
14.2. 分区管理
14.3. 节点管理
14.4. HBase 度量(Metrics)
14.5. HBase 监控
14.6. Cluster 复制
14.7. HBase 备份
14.8. 容量规划
15. 创建和开发 HBase
15.1. HBase 仓库
15.2. IDEs
15.3. 创建 HBase
15.4. 发布新版 hbase.apache.org
15.5. 测试
15.6. Maven 创建命令
15.7. 加入
15.8. 开发
15.9. 提交补丁
A. FAQ
B. 深入hbck
B.1. 运行 hbck 以查找不一致
B.2. 不一致(Inconsistencies)
B.3. 局部修补
B.4. 分区重叠修补
C. HBase中的压缩
C.1. CompressionTest 工具
C.2. hbase.regionserver.codecs
C.3. LZO
C.4. GZIP
C.5. SNAPPY
C.6. 修改压缩 Schemes
D. YCSB: Yahoo! 云服务评估和 HBase
 
E. HFile 格式版本 2
E.1. Motivation
E.2. HFile 格式版本 1 概览
E.3. HBase 文件格式带 inline blocks (version 2)
F. HBase的其他信息
F.1. HBase 视频
F.2. HBase 展示 (Slides)
F.3. HBase 论文
F.4. HBase 网站
F.5. HBase 书籍
F.6. Hadoop 书籍
G. HBase 历史
 
H. HBase 和 Apache 软件基金会(ASF)
H.1. ASF开发进程
H.2. ASF 报告板
}}}
