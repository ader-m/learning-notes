
标题AB合并版本


echo "# Day 1 学习笔记

## 装 MySQL 踩的坑
1. 端口 3306 被老的 5.7 占着
2. DBeaver 要开 allowPublicKeyRetrieval
3. 密码全角半角的坑" > note.md
4.笔记：记录 caching_sha2_password 认证原理
5.创建分支
6."“这是在 dev 分支写的”"
7.git commit -m "Day3-5：SQL增删改查、查询五件套、三表设计与多表查询5题"
8.JOIN 是把两张表按条件并排摆一起，on 写配对条件：A.id = B.a_id
9.LEFT JOIN 保左表全留，右表配不上的填 NULL；INNER JOIN 只留两边都配上的
10.反连接 = LEFT JOIN + WHERE 右表.id IS NULL，专门找“A有、B没有”（183 题就是它）
11.自连接 = 同一张表起两个别名（w1/w2）自己配自己，用来比“相邻行”（180、197）
12.批量造数据：INSERT...SELECT + CROSS JOIN + RAND()
HAVING 是筛组，WHERE 是筛行
反连接 = LEFT JOIN + IS NULL，找“A有B没有”
每组Top N 模板：内层窗口函数排 rnk，外层套壳 WHERE rnk=1
196：DELETE + not in min(id)，MySQL 报错就给子查询套壳
197：自连接 = 同一张表起两个别名自己配自己，datediff 算日期差