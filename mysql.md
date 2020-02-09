# mysql

###安装

...

### 常用命令

* 查询版本 `mysql --version || mysql -V`

* 登录/退出数据库

  * 登录`mysql -u root -p`

    u-用户名

    p-密码

  * 退出`\q(推荐) || exit; || quit;`

* 数据库

  * 显示所有库`show databases;`
  * 创建库``create database `xx`; ``
  * 删除库``drop database `xx`;``
  * 进入库``use `xx` ``

* 某个数据库-》表

  * 显示所有表`show tables;`

  * 创建表``create table `xx`;``

    ```javascript
    create table `xx`(
        `id` int auto_increment not null,
        `count` varchar(8) not null,
        primary key (`id`)
    );
    ```

  * 删除表``drop table `xx`; ``

  * 查询表``select * from `xx`; ``

* 某个表-》数据

  * 插入数据``insert into `xx` values(…);``
  * 查询数据``select * from where `xx` x=y; ``
  * 删除数据``delete from `xx` where x=y;``