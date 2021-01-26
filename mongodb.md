# mongodb

关系型 数据库->数据表->数据行

非关系型 数据库->集合->文件(数据)

### 安装

....

### 常用命令

* 基本
  * 查看版本 `db.version()`
  * 查看是否和数据库链接成功了`db.runCommand({ping:1})`，`{ "ok" : 1 }`表示成功
* 命令行清屏`cls`
  
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

  * 查看集合下的数据(query+fields+limit+skip+sort)

    * 所有`db.xx.find()`，带条件`db.xx.find({..})`，获取执行信息`db.xx.find({..}).explain({})`
    * 有多少条`db.xx.find().count()`
    * 第一条`db.xx.findOne()`
    * 只返回部分属性`db.find({..},{k1:true,k2:false,k3:1,k4:0,..})`
    * $where--js方法进行复杂查询`db.xx.find({$where:'this.age>10'})`
    * ---下面的是比较相关---
    * $gt--大于`db.xx.find({age:{$gt:10}})`
    * $gte--大于等于`db.xx.find({age:{$gte:10}})`
    * $eq--等于`db.xx.find({age:{$eq:10}})`，当然不加这个条件时，默认就是等于
    * $lt--小于`db.xx.find({age:{$lt:10}})`
    * $lte--小于等于`db.xx.find({age:{$lte:10}})`
    * $ne--不等于`db.xx.find({age:{$ne:10}})`
    * ---下面的是条件相关---
    * $in--等于(多个)`db.xx.find({age:{$in:[10,20]}})`
    * $and--与`db.xx.find({$and:[{age:{$gt:10}},{age:{$lt:20}}]})`
    * $or--或`db.xx.find({$or:[{age:{$gt:20}},{age:{$lt:10}}]})`
    * $not--非`db.xx.find({age:{$not:{$gt:10,$lt:20}}})`
    * ---下面的是数组相关---
    * 基本--`db.xx.find({arr:['a','b','c']})`(有且只有)，`db.xx.find({arr:'a'})`(含有)
    * $all--含有多项(都要有)`db.xx.find({arr:{$all:['a','b']}})`
    * $in--含有项(可选)`db.xx.find({arr:{$in:['a','b']}})`
    * $size--数组个数`db.xx.find({arr:{$size:n}})`
    * $slice--显示个数`db.xx.find({},{arr:{$slice:n}})`
    * ---下面的是分页排序相关---
    * limit()--每页多少条`db.xx.find().limit(10)`
    * skip()--跳过多少条`db.xx.find().skip(10)`
    * limit+skip--实现分页`db.xx.find().limit(10).skip(10*(2-1))`(第2页)
    * sort()--排序`db.xx.find().sort({age:1})`(1升序,-1降序)

  * 修改

    * `db.xx.update({..},{..})`(全替换)
    * $set--`db.xx.update({..},{$set:{..}})`(单修改)，有嵌套时，`db.xx.update({..},{$set:{a:'x','obj.k':v,'arr.i':v}})`

    * multi--修改多个`db.xx.update({..},{$set:{..}},{multi:true})`，可以简写为`db.xx.update({..},{$set:{..}},false,true)`

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

  * 索引相关
    * 查找`db.xx.getIndexes()`
    * 添加`db.xx.ensureIndex({k:1})`，如果加上unique即`db.xx.ensureIndex({k:1},{unique: true})`,则可让此字段不可重复
    * 删除`db.xx.dropIndex('k_1')`(注意这里不是key名，是name名)
    * 建立全文索引`db.xx.ensureIndex({k:'text'})`，查找时`db.xx.find({$text:{$search:'a'}})`(单个词)，`db.xx.find({$text:{$search:'a b'}})`(多个词)，`db.xx.find({$text:{$search:'\"a b\"'}})`(连词,转义一下)

### 通过js操作

```javascript
//a.js
const adb = connect("xx"); //连接数据库xx，没有的话新建之
//增,删,改
adb.yy.insert({ userName: "", loginTime: Date.now() }); //新建集合 并插入数据

//查
//-方式1
// var result = db.workmate.find();
// while (result.hasNext()) {
//   printjson(result.next());
// }
//-方式2
// var result = db.workmate.find();
// result.forEach((r) => {
//   printjson(r);
// });


//执行
//-方式1 在系统cmd执行mongo，在vscode cmd中执行mongo a.js
//-方式2 在vscode cmd执行mongo，再load('./a.js')
```

