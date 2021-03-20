# git

### 一般流程

* github上新建一个项目
* `git init `-->本地文件初始化成git管理项目
* `git add`(git add -u或者git add -A)-->添加到暂存区
* `git commit -m 'xx'`-->提交到当前分支

### 设置用户名和密码

* 查看

  ```
  git config --list
  
  git config user.email 
  git config user.name
  ```

* 设置全局

  ```
  git config --global user.email 'xx'(可以没有引号，下同)
  git config --global user.name 'xx'
  ```

* 设置局部

  ```
  git config user.email 'xx'
  git config user.name 'xx'
  ```

### 远程仓库

* 查看

  ```
  git remote -v
  ```

* 连接

  ```
  git remote add origin git@github.com:ldd0003/xx.git(ssh)
  git remote add origin https://github.com/ldd003/xx.git(https)
  ```

* 提交

  ```
  git push -u origin master-->加了-u，设置默认。此时git push可以代替git push origin master
  ```

* 备注

  ```
  // bug
  fatal:remote origin already exists->git remote rm origin
  ```

  ```
  // https和ssh的区别
  https-->可以随意clone项目 
  ssh-->必须是项目的拥有者或管理员
  
  https-->在首次push的时候，需要验证用户名密码
  ssh-->不需要用户名，需要创建ssh key，创建时未设置密码的话，密码也不需要输入
  ```

### SSH key

* 创建

  ```
  ssh-keygen -t rsa -C "xx"-->可以直接就ssh-keygen
  -t(type)-->指定密钥类型，默认是 rsa ，可以省略
  -C(comment)-->设置注释文字，比如邮箱
  ```

  此时会自动生成.ssh 里面有id_rsa id_rsa和id_rsa.pub

* 测试

  ```
  ssh -T git@github.com
  ```

* 本机管理多个密钥/账户

  ```
  ssh-keygen（除了第一个对话，一直回车创建）
  
  输入.ssh/id_rsa_githubTest（如果有.ssh文件夹，另需要在~路径下时,githubTest为随便取的一个名字）
  ```

  新建config文件：

  ```
  #git1
  Host githubTest
  HostName github.com
  IdentityFile ~/.ssh/id_rsa_githubTests
  ```

### 分支

* 命令

​		`git branch` -->查看

​		`git branch xx` -->新建分支

​		`git checkout xx` -->切换到分支xx

​		`git checkout -b xx` -->新建并切换到分支xx

​		`git push --set-upstream origin xx` -->第一次push到分支的时候，后面可以直接git push

* 备注
  * 只有commit之后，才会是分支所有
  * 如果当前分支有修改，切换到其他分支前，需要commit或者git stash(切回来后git stash pop)

### 别名

* 常用
  * `git config --global alias.st status`
  * `git config --global alias.ci commit`

* 备注
  * 会生成到.gitconfig 对应里面的[alias]

###   其它

* 大小写敏感问题（本地文件名和远程文件名大小写不一致）

  ```javascript
  //让项目大小写敏感
  git config core.ignorecase false
  //修改项目，把对应的文件，大小写，写成想要的。把修改push到远程仓库
  //此时远程仓库有重名（大小写）到文件，删除不想要文件
  git rm --cached path(如src/views/xx) -r
  //把修改push到远程仓库
  ```

  