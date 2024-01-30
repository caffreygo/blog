# 基础学习

## 进程通信

![](https://raw.githubusercontent.com/caffreygo/static/main/blog/electron/communication.png)

## nodemon

nodemon 是一种工具，通过在检测到目录中的文件更改时自动重新启动节点应用程序来帮助开发基于 Node.js 的应用程序。

### 配置

| 配置项      | 说明                 |
| ----------- | -------------------- |
| ignore      | 忽略监测的文件或目录 |
| colours     | 输出信息颜色         |
| verbose     | 显示详细执行日志     |
| restartable | 生起命令的字符串     |
| watch       | 监控的文件或目录路径 |
| ext         | 监控文件的扩展名     |
| exec        | 执行的程序           |

下面是配置文件 nodemon.json 示例

```json
{
	"ignore": [
		"node_modules",
		"dist"
	],
	"colours": true,
	"verbose": true,
	"restartable": "rs",
	"watch": [
		"*.*"
	],
	"ext": "html,js"
}
```

现在可以在配置文件 Package.json 中定义执行命令，下面是 electron 项目定义的命令

```json
{
  "name": "electron-camera",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon --exec electron . "
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "electron": "^22.0.2"
  }
}
```

