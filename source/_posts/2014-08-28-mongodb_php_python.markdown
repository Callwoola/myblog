---
layout: post
title: "mongodb 速度成法"
date: 2014-05-05 22:57:40 +0800
comments: true
author: Neo
categories: [mongodb]
layout: post
description: mongodb 速成法
keywords: mongodb, quick learn,
---

mongo的优点就不说了，我觉得在我认证范围内的业务大部分可以用mongo,这里也主要介绍python 和php的安装和使用 

根据自己的系统选择 解压后在bin里面 有很多个工具

* Mongod.exe 是用来连接到mongo数据库服务器的，即服务器端。

* Mongo.exe 是用来启动

* MongoDB shell的，即客户端。

其他文件:

* mongodump 逻辑备份工具。 

* mongorestore 逻辑恢复工具。 

* mongoexport 数据导出工具。

* mongoimport 数据导入工具。   

`启动 X:/X/bin/mongod.exe  --dbpath=x:/x/data/db`

(例如)
dbpath 是自动的数据库存放位置  

好了那么现在我们就可以进入客户端了 

``` java
>mongo.exe    
```


 4.2）创建collection并插入数据

 在传统关系型数据库中，创建完了库后接下来会创建表，但是在mongoDB中没有“表”的概念，与其对应的一个概念是集合，即collection。

 在shell 命令窗口键入如下命令：

``` java
> db.users.insert({'name':'xumingxiang','sex':'man'}) // 这条命令是向users 集合中插入一条数据。如果集合users不存在，则会先新建一个，然后再插入数据，参数以JSON格式传入。
```
因为我们后面要测试删除数据，所以我们再插入一条数据：

``` java
db.users.insert({'name':xiangshu','sex':'man'})
4.3）
//在上面4.1）和4.2）我们创建了数据库，创建了集合，还插入了两条数据，那么这些操作有没有执行成功呢？我们来查询一下：
```
在shell 命令窗口键入如下命令：

``` java
>show dbs // 显示所有数据库  
>show collections // 显示当前数据库下的所有集合  
>db.users.find() // 显示users集合下的所有数据文档
```




 看我用红色标记的部分。这说明我们之前的操作是成功的。我们还看到系统给每条记录分配了一个惟一主键 _id 。

4.4）更新数据

 现在我们要把第二条数据的sex改成女即“women”

``` java

> db.users.update({'name':'xiangshu'},{'$set':{'sex':'women'}},upsert=true,multi=false)
```

 解释一下几个参数：

 第一：查询的条件

 第二：更新的字段

 第三：如果不存在则插入

 第四：是否允许修改多条记录

4.5)删除记录

 我们现在要把第一条记录即'name'为'xumingxiang'的

``` java
 > db. users.remove({'name':'xumingxiang'})
 我们在检验一下4）5）两步有没有操作成功，在shell 命令窗口键入如下命令：

 > db.users.find() 
```

 从输出的界面我们看到现在只剩下一条'name'为'xiangshu'的了，并且它的'sex'为'women'，这说明4）5)两步操作成功了。

 4.6）删除所有记录
 
``` java
> db.users.remove()
```

 4.7) 删除collection
 
``` java
> db.users.drop() //如果删除成功会返回“true”，否则返回“false”
```

4.8）删除当前数据库

``` java
> db.dropDatabase()
```

mongo 相关命令


``` java
db.AddUser(username,password)  添加用户

db.auth(usrename,password)     设置数据库连接验证

db.cloneDataBase(fromhost)     从目标服务器克隆一个数据库
db.commandHelp(name)           returns the help for the command
db.copyDatabase(fromdb,todb,fromhost)  复制数据库fromdb---源数据库名称，todb---目标数据库名称，fromhost---源数据库服务器地址
db.createCollection(name,{size:3333,capped:333,max:88888})  创建一个数据集，相当于一个表
db.currentOp()                 取消当前库的当前操作
db.dropDataBase()              删除当前数据库
db.eval(func,args)             run code server-side
db.getCollection(cname)        取得一个数据集合，同用法：db['cname'] or
db.getCollenctionNames()       取得所有数据集合的名称列表
db.getLastError()              返回最后一个错误的提示消息
db.getLastErrorObj()           返回最后一个错误的对象
db.getMongo()                  取得当前服务器的连接对象get the server
db.getMondo().setSlaveOk()     allow this connection to read from then nonmaster membr of a replica pair
db.getName()                   返回当操作数据库的名称
db.getPrevError()              返回上一个错误对象
db.getProfilingLevel()         
db.getReplicationInfo()        获得重复的数据
db.getSisterDB(name)           get the db at the same server as this onew
db.killOp()                    停止（杀死）在当前库的当前操作
db.printCollectionStats()      返回当前库的数据集状态
db.printReplicationInfo()
db.printSlaveReplicationInfo()
db.printShardingStatus()       返回当前数据库是否为共享数据库
db.removeUser(username)        删除用户
db.repairDatabase()            修复当前数据库
db.resetError()                
db.runCommand(cmdObj)          run a database command. if cmdObj is a string, turns it into {cmdObj:1}
db.setProfilingLevel(level)    0=off,1=slow,2=all
db.shutdownServer()            关闭当前服务程序
db.version()                   返回当前程序的版本信息
```
 
``` java
db.test.find({id:10})          返回test数据集ID=10的数据集
db.test.find({id:10}).count()  返回test数据集ID=10的数据总数
db.test.find({id:10}).limit(2) 返回test数据集ID=10的数据集从第二条开始的数据集
db.test.find({id:10}).skip(8)  返回test数据集ID=10的数据集从0到第八条的数据集
db.test.find({id:10}).limit(2).skip(8)  返回test数据集ID=1=的数据集从第二条到第八条的数据
db.test.find({id:10}).sort()   返回test数据集ID=10的排序数据集
db.test.findOne([query])       返回符合条件的一条数据
db.test.getDB()                返回此数据集所属的数据库名称
db.test.getIndexes()           返回些数据集的索引信息
db.test.group({key:...,initial:...,reduce:...[,cond:...]})
db.test.mapReduce(mayFunction,reduceFunction,<optional params>)
db.test.remove(query)                      在数据集中删除一条数据
db.test.renameCollection(newName)          重命名些数据集名称
db.test.save(obj)                          往数据集中插入一条数据
db.test.stats()                            返回此数据集的状态
db.test.storageSize()                      返回此数据集的存储大小
db.test.totalIndexSize()                   返回此数据集的索引文件大小
db.test.totalSize()                        返回些数据集的总大小
db.test.update(query,object[,upsert_bool]) 在此数据集中更新一条数据
db.test.validate()                         验证此数据集
db.test.getShardVersion()                  返回数据集共享版本号

```

与sql语法比较


| MongoDB语法   | MySql语法 |
|--------|--------|
|db.test.find({'name':'foobar'}) | select * from test where name='foobar'
|db.test.find()                  | select * from test
|db.test.find({'ID':10}).count() |select count(*) from test where ID=10
|db.test.find().skip(10).limit(20)     |select * from test limit 10,20
|db.test.find({'ID':{$in:[25,35,45]}}) |select * from test where ID in (25,35,45)
|db.test.find().sort({'ID':-1})        |select * from test order by ID desc
|db.test.distinct('name',{'ID':{$lt:20}})  |select distinct(name) from test where ID<20
|db.test.group({key:{'name':true},cond:{'name':'foo'},reduce:function(obj,prev){prev.msum+=obj.marks;},initial:{msum:0}})  |select name,sum(marks) from test group by name
|db.test.find('this.ID<20',{name:1})  |select name from test where ID<20
|db.test.insert({'name':'foobar','age':25})<==>insert into test ('name','age') values('foobar',25)
|db.test.remove({})                |delete * from test
|db.test.remove({'age':20})        |delete test where age=20
|db.test.remove({'age':{$lt:20}})  |elete test where age<20
|db.test.remove({'age':{$lte:20}}) |delete test where age<=20
|db.test.remove({'age':{$gt:20}})  |delete test where age>20
|db.test.remove({'age':{$gte:20}}) |delete test where age>=20
|db.test.remove({'age':{$ne:20}})  |delete test where age!=20
|db.test.update({'name':'foobar'},{$set:{'age':36}}) |update test set age=36 where name='foobar'


可视化的客户端管理工具MongoVUE


使用mongo.exe 管理数据库虽然可行，功能也挺强大，但每次都要敲命令，即繁琐枯燥而且效率低下。下面介绍一款Windows下的可视化操作的管理工具MongoVUE

[下载地址：](http://www.mongovue.com/downloads/)










