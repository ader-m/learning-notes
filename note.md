
## 装 MySQL 踩的坑
6."“这是在 dev 分支写的”"
7.git commit -m "Day3-5：SQL增删改查、查询五件套、三表设计与多表查询5题\n
8.JOIN 是把两张表按条件并排摆一起，on 写配对条件：A.id = B.a_id\n
9.LEFT JOIN 保左表全留，右表配不上的填 NULL；INNER JOIN 只留两边都配上的\n
10.反连接 = LEFT JOIN + WHERE 右表.id IS NULL，专门找“A有、B没有”（183 题就是它）\n
11.自连接 = 同一张表起两个别名（w1/w2）自己配自己，用来比“相邻行”（180、197）\n
12.批量造数据：INSERT...SELECT + CROSS JOIN + RAND()\n
HAVING 是筛组，WHERE 是筛行\n
反连接 = LEFT JOIN + IS NULL，找“A有B没有”\n
每组Top N 模板：内层窗口函数排 rnk，外层套壳 WHERE rnk=1\n
196：DELETE + not in min(id)，MySQL 报错就给子查询套壳\n
197：自连接 = 同一张表起两个别名自己配自己，datediff 算日期差\n
varchar int date或datetime\n
insert into 表名 values()\n
inner join 不匹配的直接消失,left join 左边保留，右边没有的直接null\n
反连接 = LEFT JOIN + WHERE 右表.id IS NULL\n
as是改名,rank是因为是保留字\n
内层：窗口函数 dense_rank() over(partition by 分组列 order by 排序列 desc) as rnk\n
外层：套壳 select + where rnk <= N\n
datediff(a,b)=a-b\n
git add是决定哪些改动要提交\n
git commit=是把暂存区的改动保存版本记录\n
pwd	我在哪（打印当前目录）	敲一下，看自己在哪\n
ls	这里有什么	ls / ls -l（竖排带详情）/ ls -a（连隐藏文件）\n
cd	去别的地方	cd ~（回家目录）→ cd /d → cd git操作练习\n
mkdir	建文件夹	mkdir ~/linux练习 然后 cd 进去\n
touch	建空文件	touch a.txt\n
cp	复制	cp a.txt b.txt\n
mv	移动/改名	mv b.txt c.txt（改名）\n
rm	删除	rm c.txt（⚠️ Linux 没有回收站，删了就是没了，所以永远先 ls 确认再删）\n
find	找文件	find ~/linux练习 -name "a.txt"\n
