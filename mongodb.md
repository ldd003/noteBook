# mongodb

关系型 数据库->数据表->数据行

非关系型 数据库->集合->文件(数据)

### 安装

....

### 常用命令

* 基本
  * 查看版本 `db.version()`
  * 查看是否和数据库链接成功了`db.runCommand({ping:1})`，`{ "ok" : 1 }`表示成功

* 库

  * 查看已有数据库`show dbs`
  * 进入(使用or新增)`use xx`
  * 显示当前所在库`db`

  * 删除`db.dropDatabase()`

* 集合

  * 查看当前数据库的集合`show collections`

  * 新增并插入数据`db.xx.insert({..})`，批量`db.xx.insert([{..}])`
  * 删除`db.xx.drop()`

* 文件

  * 查看集合下的数据

    * 所有`db.xx.find()`
    * 第一条`db.xx.findOne()`

  * 修改，

    * `db.xx.update({..},{..})`(全替换)
    * $set--`db.xx.update({..},{$set:{..}})`(单修改)，有嵌套时，`db.xx.update({..},{$set:{a:'x','obj.k':v,'arr.i':v}})`

    * multi--修改多个`db.xx.update({..},{$set:{..},{multi:true}})`，可以简写为`db.xx.update({..},{$set:{..}},false,true)`

    * upsert--修改未匹配到想插入数据`db.xx.update({..},{$set:{..},{upsert:true}})`，可以简写为`db.xx.update({..},{$set:{..}},true)`

    * $unset--删除某个属性`db.xx.update({..},{$unset:{k:''}})`

    * $inc--计算数字`db.xx.update({..},{$inc:{m:n}})`，m的值(v)变成v+n

    * ---下面的是数组相关---

    * $push--追加`db.xx.update({..},{$push:{arr:'arr1'}})`，`db.xx.update({..},{$push:{'obj.k':v}})`，注意obj是得到`{k:[v]}`

    * $each--批量追加`db.xx.update({..},{$push:{arr:{$each:['arr1','arr2']}}})`，`db.xx.update({..},{$push:{'obj.k':{$each:['arr1','arr2']}}})`，这里`obj.k`要是一个数组

    * $pop--删除数组值`db.xx.update({..},{$pop:{arr:1}})`(1表示删除数组末尾，-1表示删除数组开头)

    * $ne--检查一个值是否存在，有则不修改，无则修改`db.xx.update({..,arr:{$ne:'arr1'}},{..})`

    * $addToSet--只针对数组，有则不push，无则push`db.xx.update({..},{$addToSet:{arr:'arr2'}})`，`db.xx.update({..},{$addToSet:{'obj.k':v}})`，这里`obj.k`要是一个数组

    * ---状态返回与安全---

      ```javascript
      var adb = connect("demos");
      
      adb.xx.update({ name: "m" }, { $set: { age: n } });
      var resultMsg = adb.runCommand({ getLastError: 1 });
      
      printjson(resultMsg);
      // {
      //     "connectionId" : 105,
      //     "updatedExisting" : true,
      //     "n" : 0,
      //     "syncMillis" : 0,
      //     "writtenTo" : null,
      //     "writeConcern" : {
      //             "w" : 1,
      //             "wtimeout" : 0
      //     },
      //     "err" : null,
      //     "ok" : 1
      // }
      ```

      ```javascript
      var adb = connect("demos");
      
      var resultMsg = adb.runCommand({
        findAndModify: "xx",
        query: { name: "m" }, 
        update: { $set: { age: n } }, 
        new: true,
      });
      
      printjson(resultMsg);
      // {
      //     "lastErrorObject" : {
      //             "n" : 1,
      //             "updatedExisting" : true
      //     },
      //     "value" : {
      //             "_id" : ObjectId("5f7b2336994bb085c1e1db6d"),
      //             "name" : "m",
      //             "age" : m
      //     },
      //     "ok" : 1
      // }
      ```

      

  * 删除

    * `db.xx.remove({..})`

### 通过js操作

```javascript
//a.js
const adb = connect("xx"); //连接数据库xx，没有的话新建之
adb.yy.insert({ userName: "", loginTime: Date.now() }); //新建集合 并插入数据

//可以
//方式1 在系统cmd执行mongo，在vscode cmd中执行mongo a.js
//方式2 在vscode cmd执行mongo，再load('./a.js')
```

