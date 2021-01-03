# vscode

* 常用插件

   ```
  Auto Close Tag
  Auto Rename Tag
  Bracket Pair Colorizer
  Debugger for Chrome
  ESLint
  Git History
  GitLens — Git supercharged
  IntelliSense for CSS class names in HTML
  Live Server
  open in browser
  Prettier - Code formatter
  Search node_modules
  Vetur
   ```

* 配置

  ```json
  {
    //emmet
    //-使非html标签tab补全
    "emmet.triggerExpansionOnTab": true,
    //editor
    //-保存格式化
    "editor.formatOnSave": true,
    //eslint
    //-对这些文件开启eslint检测
    "eslint.validate": ["javascript", "javascriptreact", "vue", "html", "typescript"],
    //prettier
    "[javascript]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[typescript]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[vue]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[html]": {
      "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    //vue
    //-vue模版上ts能提示
    "vetur.experimental.templateInterpolationService": true,
  }
  ```

  

