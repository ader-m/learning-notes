
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

Day21: 统一响应格式 + 全局异常处理（项目①规范第一步）
为什么统一响应：前端不用每个接口判断不同返回结构，约定 {code:0成功/非0失败, msg:人看提示, data:真正数据}
resp(code=0,msg="ok",data=None) 辅助函数：成功的接口 return resp(data=db_item)，不再用 response_model（否则会被序列化成单一模型结构，破坏统一）
@app.exception_handler(HTTPException) 接管业务异常（404/403...）→ 包成 {code:状态码,msg:detail,data:null}
@app.exception_handler(RequestValidationError) 接管参数校验失败（422）→ 包成 {code:422,msg:"参数校验失败",data:errors()}
HTTPException 负责业务异常，RequestValidationError 负责 Pydantic 校验失败，两套要分别接管才能全统一
{} 与 {"title":""} 区别：{} 缺 title 字段 → missing → 422；{"title":""} 有字段只是空串，空串也是合法 str → 校验通过返回成功（这是两回事）
Day15→21 复盘（自己口述版）：
 FastAPI 用装饰器把 HTTP方法+URL 绑定到一个函数；Pydantic 校验字段类型，失败返422
 一个类=一张表，一个属性=一列，一个实例=一行
 Depends(get_db) 调用处理函数前先执行 get_db 拿 session，处理完回到 finally 关掉
 resp() 让成功返回统一 {code,msg,data}；@app.exception_handler 让异常也走同一格式，前端不用区分两套结构
 HTTPException 管业务异常(404/403)，RequestValidationError 管参数校验失败(422)

 FastAPI 用装饰器把「HTTP 方法 + URL 路径」绑定到一个 Python 函数
校验字段类型，校验失败返回422
一个类 = 一张表，一个属性 = 一列，一个实例 = 一行。
Depends(get_db) 告诉 FastAPI：调用处理函数前，先执行 get_db。
resp() 让成功返回格式统一：{code, msg, data}。

@app.exception_handler(...) 让异常返回也走同一格式，前端不用区分两套结构。

HTTPException 负责业务异常（404、403 等），RequestValidationError 负责参数校验失败（422）。

Day22: 密码与安全（用户表+注册存哈希+登录verify）
为什么明文存密码不行：库被拖库后所有密码直接暴露，且用户密码复用会撞库别的站
bcrypt 比 md5/sha256 安全：md5/sha256 算得快，易被彩虹表/暴力破解反推；bcrypt 自动加盐+故意算得慢(抗暴力破解)，且单向不可逆(只能明文→哈希，不能反推)
登录不是"解密比对"：把用户输的密码再 hash 一次，和库里存的哈希比对(pwd_context.verify)
SQL 注入原理：拼接 SQL 把用户输入当指令执行，如 'admin' OR '1'='1' 变 WHERE username='admin' OR '1'='1' 永远成立→绕过
ORM 防注入：参数化查询 WHERE username=%(u)s，用户输入只当"数据"永远不当"指令"
踩坑：passlib 1.7.4 与 bcrypt 4.1+ 不兼容 → /register 500；修复 pip install "bcrypt==4.0.1" 后重启 uvicorn
验收：register code:0带id / MySQL hashed_password=$2b$12$...非明文 / login正确密码code:0 / 错误密码code:401（全过）

## Day 23｜JWT 认证（2026-10-19）
目标：登录成功签发 token，后续请求带 token 免传密码，未登录返回 401
核心知识点：
- OAuth2PasswordBearer(tokenUrl="login")：FastAPI 依赖，自动从 Authorization: Bearer <token> 头取 token
- OAuth2PasswordRequestForm：登录用表单(非JSON)，OAuth2 密码流规定（/docs 的 Authorize 按钮只认表单）
- jose 三件套：jwt.encode(payload,密钥,alg) 签发 / jwt.decode 验签+解析 / JWTError 接住所有解析失败(签名错/过期/格式错)
- payload 标准字段：sub=用户身份(用户名/id)，exp=过期时间(jose 自动校验过期，超时就抛 JWTError)
- SECRET_KEY 仅服务器知，泄露可伪造任意用户 token；生产放环境变量不写死
- /login 返回 OAuth2 规定结构 {"access_token":...,"token_type":"bearer"}（统一响应{code,msg,data}的唯一例外，因要和标准协议对接）
- get_current_user 依赖：解析 token→查用户，任何接口 Depends 即受保护，无/错 token 自动 401
JWT 三段：header(算法类型).payload(claims:用户名/过期).signature(密钥对前两段签名)
  - signature 防篡改：改前两段签名对不上；payload 仅 base64url 编码非加密，谁都能看懂→不放密码等敏感信息
无状态认证：服务器不存 session，凭 token 签名有效+未过期即信，重启/多机部署不受影响，不用每次查库确认登录
验收：未登录/me→401 Not authenticated / 带alice正确token→200 / 乱填token→401（全过）
踩坑：PowerShell 里 curl 是 Invoke-WebRequest 别名，不认 -H "字符串"；用 curl.exe 调系统真 curl 才行

## Day 24｜权限控制（2026-10-19）
目标：在 JWT 登录基础上加角色权限——普通用户只能删自己、管理员可删任何人、管理员专属接口仅管理员可见
核心知识点：
- 角色存数据库 user.role 列(VARCHAR 默认 'user')；已存在表加列不能靠 create_all(只建不存在的表)，要手跑 ALTER TABLE user ADD COLUMN role VARCHAR(20) NOT NULL DEFAULT 'user'
- require_admin 依赖：先 Depends(get_current_user) 拿到当前用户，再 if role != "admin" → 403；管理员接口套上即受保护
- delete_user 双分支放行：current_user.id == user_id(删自己) 或 current_user.role == "admin"(管理员) 才放行，否则 403
- 401 vs 403：401=凭证缺失/无效，服务器根本不知你是谁(没登录或 token 错/过期)；403=凭证合法、身份确认了，但角色没这权限，服务器认识你但不让干
- 角色放数据库而非写死代码：改权限只 UPDATE 一行，不用改代码/重部署；权限是"数据"不是"逻辑"，用户/角色多了只能靠数据管理(写死 if user=="alice" 把人和权限绑死，换人就得改代码)
验收：bob GET /admin/users→403 / bob 删别人→403 / bob 删自己→200 / 管理员删别人→200（全过；独立启动服务跑库确认 v_bob/v_carol 行真消失）
踩坑：user 表缺 role 列需先 ALTER + UPDATE alice 为 admin；贴"期望响应"冒充真实运行会被查库识破(真实 200 必 commit 掉一行)

## Day 25｜RESTful 设计规范（2026-10-20）
目标：把 Day20-24 的待办/用户 API 路由按 REST 规范重构——名词复数、/api/v1 前缀、方法对齐语义、列表加分页
核心知识点：
- URL 定位资源用名词复数、带 /api/v1 前缀；动作交给 HTTP 方法(GET/POST/PUT/PATCH/DELETE)，路径里不放动词(放动词=信息重复，膨胀难维护)
- 幂等：PUT/DELETE 幂等(同请求执行多次最终状态一致)、POST 非幂等(每次都是新创建)；网络超时≠失败(请求没到/处理一半崩/已成功但响应丢失三态)，POST 重试会建重复→新建用 POST、改删设计成幂等
- 201 vs 204 vs 200：200 查/改成功有体；201 新建成功(规范上应带 Location 头指新资源 URI，客户端不用自己拼地址)；204 删除无响应体。本计划选方案 A：保留统一响应 {code,msg,data}，只把 HTTP 码改对(201 建、200 删)，业务码与传输码分工不冲突
- 列表三件套：分页 ?page&size → SQL offset=(page-1)*size, limit=size；过滤 ?status= → WHERE；排序 ?sort=-price → -表倒序 ORDER BY price DESC
- 分页必坑：total 必须在 offset/limit 之前 count()，否则数的是切片后条数(永远≤size)，前端分页器废
- 深分页代价(进阶)：OFFSET 线性扫行(第5万页≈数百ms)、COUNT(*) 额外开销、写并发下 offset 窗口漂移导致漏/重数据(解法：游标/keyset 分页 WHERE id>上一页末 LIMIT n，成本与位置无关)
- /api 区分接口与页面、/v1 版本声明做非破坏性演进(老客户端继续 v1、新客户端迁 v2 并行)
验收：/docs 全路由带 /api/v1；POST /api/v1/items 返 201；GET /api/v1/items?page=1&size=2 返 items 恰 2 条 + total + page/size；DELETE 真实生效(独立跑：POST 201 / GET total=10 / DELETE 后 total 10→9 确认行真消失)
踩坑：PowerShell 里 `curl.exe -d "{\"title\":...}"` 双引号包 JSON 会被 PowerShell 吞掉引号和花括号、中文还乱码(GBK 误读)→ 服务器收残 JSON 报 422 JSON decode error；正确写法是 `-d` 用单引号 `'{"title":"milk","price":3.5}'`，或写文件法 `Set-Content body.json -Value '...' -Encoding utf8` + `-d "@body.json"`