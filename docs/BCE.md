# 逻辑架构到应用程序映射指南(BCE)

## 1. 逻辑架构

逻辑架构由三层模型（表示层、业务层、持久化层）构成

### 1.1 表示层

客户端使用React作为表示层，提供用户信息管理系统、用户任务管理系统、问卷管理系统、消息通知系统；

### 1.2 业务层

服务端作为业务层，为表示层的各个子系统提供相应的服务模块。

### 1.3 持久化层

PostgreSQL 提供了数据的持久化服务。

# 2. 框架目录设计

## 2.1 前端框架设计

```bash
src
│
├─assets：							# 素材文件夹
│  ├─css：							# 层叠样式文档
│  ├─github：						# react的github中用到的图片
│  ├─img：							# 网站前端用到的图片
│  │  └─faces：						# 头像图片
│  └─jss：							# ui样式文档
│      └─material-dashboard-react：	# dashboard样式文档
│          ├─components：			# ui组件样式
│          ├─layouts：				# 主界面dashboard框架样式
│          └─views：					# 应用样式
├─components						 # 前端可以利用的material-ui组件
│  ├─Card：							# 卡片
│  ├─CustomButtons：					# 自定义按钮
│  ├─CustomInput：					# 自定义输入框
│  ├─Grid：							# 网格容器
│  ├─MultiChoiceCard：				# 多选部分
│  ├─Navbars：						# 顶部栏
│  ├─QuestionnaireContent：			# 问卷
│  ├─ShortAnswerCard：				# 简答部分
│  ├─Sidebar：						# 侧边栏
│  ├─SingleChoiceCard：				# 单选部分
│  ├─Table：							# 表格
│  ├─TaskCard：						# 任务卡片
│  ├─TaskContent 					 # 任务内容
│  └─Typography：					# 提示提醒
├─layouts：							# 主界面
│  ├─Admin.js：						# url的响应，跳转到主页相关、登录注册、不符合界面
├─variables：						# 常用的全局函数，常量
└─views：							# 子界面，包括主界面框架下的子界面和登录注册界面
    ├─Commission：					# 委托任务界面
    ├─CreatTask：					# 创建任务界面
    ├─Dashboard：					# 侧边栏界面
    ├─LoginPage：					# 登录界面
    ├─Notifications：				# 消息界面
    ├─Questionnaire：				# 创建问卷界面
    ├─QuestionPage：					# 问卷界面
    ├─RecycleBin：					# 回收站界面
    ├─RegisterPage：					# 注册界面
    ├─TaskArray：					# 单个任务界面
    ├─TaskBoard：					# 任务面板界面
    ├─TaskList：						# 任务列表界面
    ├─TaskSquare：					# 任务广场界面
    └─UserProfile：					# 个人信息界面
```



## 2.2 后端框架设计

```bash
src
│  
├─controllers
│      db_controller.go  		# 数据库核心代码
│      msg_controller.go		# 数据库管理消息模块代码
│      qFormat_controller.go	# 数据库管理问卷模块代码
│      record_controller.go		# 数据库管理用户提交的答案模块代码
│      userdb_controller.go		# 数据库管理用户信息的模块代码
├─global
│      config.go				# 全局配置文件，包含一些全局配置信息
│      
├─helper
│      response.go				# 后台返回信息的一些简单模板类
│      
├─main
│      backend.go				# 后台程序，用于生成消息通知
│      main.go					# 主程序
│      msgRounter.go			# 消息相关路由
│      qFormatRouter.go			# 问卷相关路由
│      recordRouter.go			# 用户提交答案相关路由
│      userRouter.go			# 用户信息相关路由
│      
├─models
│      answer.go				# 答案类
│      message.go				# 消息类
│      option.go				# 选项类
│      question.go				# 问题类
│      questionnaireFormat.go	# 问卷类
│      record.go				# 答案记录类
│      taskPreview.go			# 问卷简要信息类
│      user.go					# 用户类
│      
└─test
        qformat_controller_test.go	# 问卷数据库测试文件
        record_controller_test.go	# 用户提交答案数据库测试文件
        user_controller_test.go		# 用户信息数据库测试文件
```

# 3. BCE

- Boundary：与用户的接口，如：界面、网关、代理等。用来隔离系统，通常负责接收并响应系统内外的消息。参与者只能与边界对象互动，不能直接发送消息给控制对象或实体对象。
- Controller：在 Boundary 和 Entity 中衔接的媒介，处理来自 Boundary 的交互请求。
- Entity：代表系统数据，如：用户、任务、资源等。用来保存问题领域的重要信息，封装了跟数据结构和数据存储有关的变化。

Boundary 包含：

- React客户端用户界面
- 服务端 Nginx 反向代理服务器

Controller 包含：

- db_controller：数据库核心管理的controller
- msg_controller：数据库管理消息的controller
- qFormat_controller：数据库管理问卷模块的controller
- record_controller：数据库管理用户提交的答案模块的controller
- userdb_controller：数据库管理用户信息的模块的controller

Entity 包含：

- 用户数据模型：user.go
- 问卷数据模型：taskPreview.go，questionnaireFormat.go， question.go， option.go
- 答案数据模型：answer.go，record.g
- 消息数据模型：message.go



