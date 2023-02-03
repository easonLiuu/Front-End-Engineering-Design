# **Front-End-Engineering-Design**

## **模块规范**

将`Node v13.2.0`作为高低版本分界线，当版本`>=13.2.0`则定为高版本，当版本`<13.2.0`则定为低版本。高版本使用`Node原生部署方案`，低版本使用`Node编译部署方案`。

### **Node原生部署方案**

在`package.json`中指定`type`，在命令中加上`--es-module-specifier-resolution=node`解决显示文件名称的问题即可

- `_filename`与`__dirname`可用`import.meta`对象重建
- `require`、`module`和`exports`可用`import`与`export`代替
- `json文件`的引用可用`Fs模块`的`readFileSync`与`JSON.parse()`代替

### **Node编译部署方案**

同时使用`require`与`export/import`会报错，所以单个模块无法切换到`ESM`，可用`babel`将代码从`ESM`转换为`CJS`。

执行以下命令安装`babel`相关工具链到`devDependencies`。

```bash
npm i @babel/cli @babel/core @babel/node @babel/preset-env -D
```

这四个`babel`子包很重要，`Node`能不能支持`ESM`的解析就看它们了。

-  **@babel/cli**：提供支持`@babel/core`的命令运行环境
-  **@babel/core**：提供转译函数
-  **@babel/node**：提供支持`ESM`的命令运行环境
-  **@babel/preset-env**：提供预设语法转换集成环境

### 总结

- 基于**Node原生部署方案**改造`Node项目`，适合在`高版本Node环境`中使用

- 基于**Node编译部署方案**改造`Node项目`，适合在`低版本Node环境`或`任何版本Node环境`中使用

  

