# npm

node.js的包管理工具

### 安装Node.JS（已集成npm）

查看node版本`node -v`

查看npm版本`npm -v`

### 全局安装NPM(或升级)

1. 网络好就`npm i npm -g`
2. 换国内镜像`npm i -g cnpm --registry=https://registry.npm.taobao.org`，然后`cnpm i npm -g`

### 常用命令

1. 创建一个文件夹并进入`mkdir xx&cd xx`
2. 安装相关
   1. `npm init`  // 在项目中引导创建一个package.json文件
   2. `npm i` // 根据package.json文件安装所有有关的依赖包
   3. `npm i xx` // 安装包，默认会安装最新的版本,本地安装
   4. `npm i xx -g` // 全局安装
   5. `npm i xx@1.0.0` // 安装指定版本
   6. `npm i xx --save` // 安装包信息将加入到dependencies（生产阶段的依赖）
   7. `npm i xx --save-dev` // 安装包信息将加入到devDependencies（开发阶段的依赖）

3. 卸载如`npm uninstall yarn -g`

4. 运行如`npm run xx`

5. 查看某个模块全部版本`npm view xx versions`

6. 查询和设置安装源

   ```
   npm config get registry
   npm config set registry=https://registry.npm.taobao.org
   ```

7. 查找全局安装位置`npm config get prefix`

### 发布和取消
1. `npm adduser`
2. `npm publish`
3. `npm unpublish xx --force`

