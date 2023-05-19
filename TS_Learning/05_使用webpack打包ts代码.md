# 项目初始化

```powershell
npm init -y
```

# webpack.config.js

![1683983918048](D:\Typora\user-image\1683983918048.png)

![1683984144293](D:\Typora\user-image\1683984144293.png)

![1683984150480](D:\Typora\user-image\1683984150480.png)

![1683984170526](D:\Typora\user-image\1683984170526.png)

![1683984301137](D:\Typora\user-image\1683984301137.png)

![1683984413839](D:\Typora\user-image\1683984413839.png)

# 打包

![1683984456741](D:\Typora\user-image\1683984456741.png)

**结果：**

![1683984529116](D:\Typora\user-image\1683984529116.png)

# 优雅地生成html文件

**npm下载包：**

```powershell
cnpm i -D html-webpack-plugin
```

![1683984770905](D:\Typora\user-image\1683984770905.png)

![1683984793714](D:\Typora\user-image\1683984793714.png)

**效果：**

![1683984869500](D:\Typora\user-image\1683984869500.png)

**修改options：**

![1683984941833](D:\Typora\user-image\1683984941833.png)

**模板：**

![1683985015854](D:\Typora\user-image\1683985015854.png)

也就是说，只需要提供一个html模板，剩下的工作有Webpack自动完成。

# 项目优雅重启

```powershell
cnpm i -D webpack-dev-server
```

![1683985244507](D:\Typora\user-image\1683985244507.png)

或者：

```powershell
npm start
```

效果：

![1683985379760](D:\Typora\user-image\1683985379760.png)

# 编译前去除旧文件，保证输出目录中只有新文件

```powershell
cnpm i -D clean-webpack-plugin
```

![1683985616514](D:\Typora\user-image\1683985616514.png)

使用{}是因为这个插件不是默认的。

![1683985646471](D:\Typora\user-image\1683985646471.png)

# 设置引用模块

![1683985747650](D:\Typora\user-image\1683985747650.png)

# babel

作用是提高兼容性(将新版js转换成旧版js)

```powershell
cnpm i -D @babel/core @babel/preset-env babel-loader core-js
```

要放在 ts-loader 前面，因为在数组中，在最后的元素被先执行

![1683986442576](D:\Typora\user-image\1683986442576.png)

![1683986521315](D:\Typora\user-image\1683986521315.png)

`由于 ie 不能识别 =>`，所以如下：

![1683986556476](D:\Typora\user-image\1683986556476.png)

![1683987260003](D:\Typora\user-image\1683987260003.png)

