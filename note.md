
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

浏览器向 http://127.0.0.1:8000/ 发出一个 HTTP 请求，最先接住它的是 uvicorn 这个服务器，它负责监听端口、收下原始的网络数据。uvicorn 把收到的字节解析成 HTTP 请求（方法、路径、请求头等），然后交给它上面挂着的 FastAPI 应用去处理。FastAPI 拿着请求里的路径 / 和请求方法 GET，去自己内部维护的路由表里查——这张表是你用 @app.get("/") 这样的装饰器一条条登记进去的。匹配到之后，FastAPI 调用对应的 read_root 函数，把函数返回的字典 {"message": "Hello World"} 拿到手。接着 FastAPI 把这个 Python 字典序列化成 JSON 字符串，再交回给 uvicorn。最后 uvicorn 把 JSON 包成完整的 HTTP 响应（状态码、响应头、响应体），通过 socket 发回浏览器，浏览器解析后显示出来。

路径参数：在 URL 路径里（/items/5 的 5）
查询参数：在 URL 问号后面（?q=hello 的 hello）
请求体：不在 URL 里，藏在 POST 请求的 body 中

Day16 第2问：username:str 省了什么代码？
在 Pydantic 模型里写 username: str 这一个类型注解，FastAPI+Pydantic 就自动帮你做三件事：①从请求体 JSON 里取出 username；②校验它是不是字符串（不是就拦下返回 422）；③自动生成接口文档里的字段说明。
如果不用 Pydantic，这些得自己手写：data = await request.json() 解析 → if not isinstance(username, str) 判断 → 再手动 return 422 报错。一行类型注解替代了这一坨样板代码。

Day16 第3问：age="abc" 为什么返回 422？
age 声明成 int，Pydantic 想把这个字符串 "abc" 转成整数，转换失败，报类型 int_parsing（无法把字符串解析成整数）。
FastAPI 捕获后返回 422，错误定位 loc: ["body","age"] —— 意思是：出错位置在请求体(body)里的 age 字段。

pydantic里的basemodel 自带数据校验，类型转换，报错格式化
当请求进来，FastAPI 做了四件事：

把请求体里的 JSON 拿出来
按 UserRegister 这个模板逐栏校验
缺栏位 → 422；类型不对 → 422
全过 → 打包成一个 UserRegister 对象塞给 user 变量，调用你的函数

 username:str=Field(min_length=3,max_length=6)字段约束  username:str 只检查是不是字符串
 zipcode字段不够长      会报字段需要大于自己写得到直段约束   loc 是 ["body","address","zipcode"]
 自定义校验器 @field_validator 抛 ValueError 后，FastAPI 怎么知道返回 422 而不是 500？
 @field_validator 在pydantic校验中抛422,  
 在函数体抛500
 validator 在 Pydantic 校验阶段抛 ValueError → Pydantic 用 try/except 接住 → 包装成 ValidationError → FastAPI 有专门处理器接它 → 返回 422。函数体里抛的异常不在校验阶段、没人接 → 500。


 orm o:object r: relational m:mapping 对象映射关系，把面向对象编程的对象与数据库练习起来
 orm 好处是可以少写重复sql,缺点是复杂查询难
 裸sql的好处是灵活强大 缺点是开发效率低，有sql注入风险
 Base.metadata.create_all(engine)
 将类定义变成真实的数据表

foreignkey 数据库的外键 ，告诉数据库这一列的值引用另一张表的某个列
relationship orm的关系对象，写在类里面，通过对象访问关联数据
foreignkey有外键，relationship按外键定义好的关联路径、用对象属性访问关联表（不是随便访问任何表） 两个一起配合：relationship告诉你查哪张关联表，foreignkey告诉你查那张表的哪一列

一对多：一个班级多个学生，一个学生属于一个班级
多对多：一个学生选多个课程，一个课程有多个学生选
多对多要有张中间表，原因是没有单独的列能够存下这种关系

commit() 时 SQLAlchemy 把你 append 进去的关联(student_id + course_id)自动写进 enrollment 表；secondary=enrollment 是告诉它"关联记录放这张表"的参数

Day20: FastAPI + SQLAlchemy 整合 —— 依赖注入 + 完整 CRUD
依赖注入 get_db：每个请求开一个独立 session，yield 交出、finally 关掉，防连接泄漏（不关连接池会耗尽）
为什么分 ItemCreate / ItemOut 两个模式：创建不传 id（id 是库生成的），返回必须带 id；ItemOut 的 from_attributes=True 让 Pydantic 能从 ORM 对象（不是 dict）读属性来序列化
db.get(Item, id) 按主键查，没有返回 None；查不到用 HTTPException(404) 明确告诉前端，而不是让它变 500
POST 完整流程：路由匹配 /items+POST → 依赖注入 get_db 拿 session → Pydantic 按 ItemCreate 校验请求体 → 建 ORM 对象 → add 进 session（待提交队列，还没落库）→ commit 真正写进 MySQL → refresh 拿回自增 id → return → FastAPI 按 response_model=ItemOut 把 ORM 对象序列化成 JSON 才返回
坑：PUT 路由写成 /item 单数（应为 /items 复数），路由装饰器的路径就是客户端必须请求的 URL，写错会 404