
## 装 MySQL 踩的坑

8.JOIN 是把两张表按条件并排摆一起，on 写配对条件：A.id = B.a_id
9.LEFT JOIN 保左表全留，右表配不上的填 NULL；INNER JOIN 只留两边都配上的
11.自连接 = 同一张表起两个别名（w1/w2）自己配自己，用来比“相邻行”（180、197）
12.批量造数据：INSERT...SELECT + CROSS JOIN + RAND()
HAVING 是筛组，WHERE 是筛行
反连接 = LEFT JOIN + IS NULL，找“A有B没有”
每组Top N 模板：内层窗口函数排 rnk，外层套壳 WHERE rnk=1
196：DELETE + not in min(id)，MySQL 报错就给子查询套壳
197：自连接 = 同一张表起两个别名自己配自己，datediff 算日期差
varchar int date或datetime
insert into 表名 values()
inner join 不匹配的直接消失,left join 左边保留，右边没有的直接null
反连接 = LEFT JOIN + WHERE 右表.id IS NULL
as是改名,rank是因为是保留字
内层：窗口函数 dense_rank() over(partition by 分组列 order by 排序列 desc) as rnk
外层：套壳 select + where rnk <= N
datediff(a,b)=a-b
git add是决定哪些改动要提交
git commit=是把暂存区的改动保存版本记录
pwd	当前目录
ls	文件夹下有什么	ls / ls -l（竖排带详情）/ ls -a（连隐藏文件）
cd		→ cd /d → cd git操作练习
mkdir	建 文件夹	mkdir ~/linux练习
touch	建 空文件  touch a.txt
cp	复制 	cp a.txt b.txt
mv	移动/改名	mv b.txt c.txt（改名）
rm	删除	rm c.txt
find	找文件	find ~/linux练习 -name "a.txt"
-rw-r--r--解读:-文件类型  rw-主人可读可写 r--同一个组只读 r--其他用户只读 
ls -l ~/文件名/  查看现在什么权限
chmod 644 ~/文件名/ 更改为文件所有者可读可写，组用户和其他用户只能读
chmod 600 ~/文件名/ 文件所有者可读可写。组用户和其他用户不能访问
所有者也不能执行它
tasklist | grep i mysql  找出有mysql的进程 i是大小写
netstat -ano |grep 3306 找出占用3306的端口进程
文件末加"第一周复盘"5 句话
我学会了LInux一些命令pwd ls cd mkdir touch cp mv rm find
印象最深的坑是没有
高频错误没有
下周要改的习惯不认真
Leetcode 做完了你交给我的题目