# 1. 数据库物理模型

* User

| Field       | Type    | Key         | Description                      |
| ----------- | ------- | ----------- | -------------------------------- |
| phone       | text    | PRIMARY KEY | 用户的唯一身份标识               |
| remain      | integer |             | 用户的余额                       |
| iscow       | boolean |             | 是否是奶牛                       |
| name        | text    |             | 用户名                           |
| password    | text    |             | 用户密码                         |
| gender      | text    |             | 用户的性别                       |
| age         | integer |             | 用户的年龄                       |
| university  | text    |             | 用户所在的大学，（学生特有属性） |
| company     | text    |             | 用户所在的组织，（奶牛特有属性） |
| description | text    |             | 用户的个人描述                   |
| class       | text    |             | 用户所在的年级，（学生特有属性） |

* qFormat

| Field          | Type    | Key         | Description            |
| -------------- | ------- | ----------- | ---------------------- |
| taskID         | text    | PRIMARY KEY | 任务的唯一身份标识     |
| taskName       | text    |             | 任务名                 |
| InTrash        | integer |             | 任务是否在回收站之中   |
| taskType       | text    |             | 任务的类型             |
| creator        | text    | FOREIGN KEY | 任务的创建者           |
| description    | text    |             | 任务的描述信息         |
| money          | integer |             | 完成任务可以获得的奖励 |
| number         | integer |             | 任务预计完成的数量     |
| finishedNumber | integer |             | 任务已经完成的数量     |
| publishTime    | text    |             | 任务的发布时间         |
| endTime        | text    |             | 任务的结束时间         |
| chooseData     | text    |             | 任务的信息，json字符串 |

* record

| Field  | Type | Key         | Description                |
| ------ | ---- | ----------- | -------------------------- |
| taskID | text | PRIMARY KEY | 任务的ID                   |
| userID | text | PRIMARY KEY | 用户的ID                   |
| data   | text |             | 提交的答案数据，json字符串 |

- message

| Field    | Type    | Key         | Description              |
| -------- | ------- | ----------- | ------------------------ |
| msgID    | text    | PRIMARY KEY | 消息的ID                 |
| state    | integer |             | 消息的状态（已读和未读） |
| receiver | text    | FOREIGN KEY | 消息的接受者             |
| time     | text    |             | 消息的时间               |
| title    | text    |             | 消息的标题               |
| content  | text    |             | 消息的内容               |



