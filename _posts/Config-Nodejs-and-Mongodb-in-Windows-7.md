title: 配置Nodejs and Mongodb in Windows 7
date: 2015-10-29 23:07:31
tags: NodeJS
---

### Nodejs安装
<!--more-->
###  Mongodb安装

###  安装Nodejs的mongodb连接驱动

### 连接mongodb


### MongoDB简易操作
在mongodb服务启动以后，新开一个命令窗口，输入`mongo`（这条命令在mongodb的bin目录下，如果没有配置环境变量，请注意输入mongo的当前路径）
```cmd
MongoDB shell version: 3.0.7
connecting to: test
Welcome to the MongoDB shell.
>
```
OK，连接成功。
## 库操作
*  `show dbs`  显示数据库列表
*  `use <dbname>` 进入名称为<dbname>的数据库，大小写敏感；如果<dbname>不存在，mongodb会自动创建
*  `db`  用于查看当前所在的数据库

## 集合操作
*  `db.<dbname>.user.save({})` 
新建名称为`user`的集合
*  `show collections` 
显示数据库中的集合(集合的概念类似于表)
*  `db.user.count()` 
查看集合`user`的记录总数
*  `db.user.insert({"key1":2, name:"zuo", age:356}) ` 
在集合`user`中插入数据
`{"key1":2, name:"zuo", age:356}`

## 查询数据
`find`和`findOne`命令，即用于查询
`db.user.find()`
MongoDB的查询条件中，并没有 >, <, >= , <= 这些运算符，而是使用 "$lt", "$lte", "$gt", "$gte" 
另外，**每个文档有一个名为 "_id" 的成员**(文档的概念类似于记录)，其实，MongoDB会为每个文档都创建这样一个文档成员，我们指定的 "key", "id" 对于MongoDB来说：它们并不是**文档的主键**，MongoDB只认 "_id"，你可以指定，但如果不指定，MongoDB就自动添加。 

## 修改数据
*  `var t2=db.user.findOne({"key1":2})`
//获取待修改的文档
*  `t.name="wang"` ， 赋新值
*  `db.user.update({"key1":2} , t2)` ，更新文档

## 删除数据
*  `db.user.remove({"key1":2})`

## 删除集合
*  `db.user.drop()`或`db.runCommand({"drop", "user"})`

## 删除数据库
* `db.runCommand({"dropDatabase":1})`，用于删除当前数据库

## 获取服务端状态信息
* `db.runCommand({"serverStatus": 1})`