# yarn

### 安装Node.JS

查看node版本`node -v`

### 全局安装Yarn(或升级)

1. 网络好

```
https://yarnpkg.com/en/docs/install
https://yarnpkg.com/zh-Hans/docs/install
```

2. 网络不好`npm i yarn -g(cnpm i yarn -g)`

### 常用命令

1. 创建一个文件夹并进入`mkdir xx&cd xx`
2. 安装相关
   1. `yarn init`-->在项目中引导创建一个package.json文件
   2. `yarn install`-->根据package.json文件安装所有有关的依赖包
   3. `yarn global add xx`-->全局安装
   4. `yarn add xx@1.0.0`-->安装指定版本
   5. `yarn add xx`-->安装包信息将加入到dependencies（生产阶段的依赖）
   6. `yarn add xx --dev`-->安装包信息将加入到devDependencies（开发阶段的依赖）

3. 卸载

   ```
   yarn remove xx
   yarn global remove xx
   ```

4. 查询和设置安装源

   ```
   yarn config get registry-->默认为https://registry.yarnpkg.com
   yarn config set registry https://registry.npm.taobao.org
   ```