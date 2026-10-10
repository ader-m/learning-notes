
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
状态码200 成功
204  成功但没有东西返回
404  找不到    url写错了
403 禁止访问   资源存在 但没权限访问
301  永久重定向  老网址跳新网址
500  服务器内部出错   自己写的代码有bug
502  网关出错  上游服务挂了
http:
get是拿到数据
post 提交数据
put 是改数据
delete 是删除数据
httP流程图
浏览器 -->|请求: 方法+URL+请求头+请求体| 服务器
服务器 -->|响应: 状态码+响应头+响应体| 浏览器

登录四步：登录前 Cookie 里没有身份 → 登录时 Set-Cookie 发通行证 → 之后每次请求浏览器自动带上 → 退出后作废
- user_session 带着 Secure + HttpOnly + SameSite，

1. requests.get/post   get查数据 post提交数据
2. status_code 在哪看；  服务器返回的响应查看
3. params / data / json 分别往哪放（拼 URL / 表单 / 请求体）  params放url里 data和json放在请求体里
4. Session 帮我自动带 Cookie（联系昨天的登录流程）
先有cookie 登录后有set cookie 
请求 后自动带上session  退出登录后作废


1. 腾讯云轻量 + Ubuntu 22.04 + 广州，公网 IP 101.33.207.42
2. 登录用户名是 ubuntu 不是 root
3. ssh ubuntu@IP，输密码屏幕不显示是正常的
4. chmod 600 在真 Linux 上真的变 rw-------
5. 要 root 权限前面加 sudo

systemctl status ssh  可以看到activ(running)····
sudo useradd -m -s /bin/bash devuser 创建第二个用户devuser
sudo passwd devuser     输入decuser用户的新密码
su - devuser  切换为 Devuser 的用户

ps aux |grep sshd |grep -v grep

ps aux:列出所有进程
grep sshd 保留有sshd字样的进程
grep -v grep 踢出有含有grep的sshd的进程

1. pip 装 requests 到 ~/.local（Ubuntu 22.04 的 PEP 668 不让装系统目录）
2. api.ipify.org 报 Connection refused，换 myip.ipip.net + httpbin 就通
3. systemctl 日志看到境外 IP（35.205.78.99 谷歌云）在扫我 SSH 端口
4. useradd 建的 devuser 默认没 sudo 权限，要 sudo usermod -aG sudo

内层 dense_rank() over(partition by 分组列 order by 排序列 desc) as rnk；
外层 select + where rnk <= N
404找不到（url错误）403 禁止访问（资源存在但没权限）500 服务器内部错（代码有 bug）
让内层结果变成带名字的临时表，外层能引用它的别名
LEFT JOIN + where 右表.id is null；
sudo = 借 root 身份执行这一行命令；useradd 建的用户默认不在 sudo 组，要 sudo usermod -aG sudo 用户名