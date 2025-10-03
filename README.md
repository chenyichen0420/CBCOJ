**选择语言:** [简体中文](README.md) | [English](readme.en.md)

## CBCOJ

### 开发动态

从版本5.30.080起，后端同时支持Windows（10/11）和Linux系统！

### 什么是CBCOJ

CBCOJ是一款超轻量级迷你在线评测系统，仅支持登录、登出、获取题目、提交评测及查询评测结果功能。

~~该在线判题系统（OJ）无法像其他OJ那样通过浏览器访问，它仅是一组配套程序，用于客户端与服务器之间的交互。~~

此类描述已成为历史。如今它已具备前端与后端，能够实现在线访问。

然而，由于所有代码均为手写，未使用任何现有扩展库或软件，因此它依然保持因完全无冗余而带来的超轻量级。

此外，我已经在本OJ上完成了大量测试。它能在约 8 秒内处理 10 万次登录请求（无任何访问限制）。

对于前端，我们使用 Node.js+HTML+css 来方便网页渲染。

对于后端，我们使用更高效的 C++ 进行高速低性能开销处理。

这些因素为CBCOJ带来了一些显著的优势：

1.高可移植性
2.硬件要求低
3.高访问效率

你可以料想，除了上述优势之外，还有更多的好处。因此，如果您想以几乎零成本运行个人/本地OJ，它非常适合！

### 如何使用CBCOJ

您应该下载五个文件：CBCOJ_Server.exe、CBCOJ_Front.exe、upx.exe、config_Server.zip和config_Front.zip。

将上述三个文件放在同一个文件夹中。然后运行下面的命令：

`upx.exe-d CBCOJ_Front.exe`

这将自动生成一个不同的 CBCOJ_Front.exe，并直接替换原始的 CBCOJ_ Front.exe。

将 config_server.zip 解压缩到一个文件夹中（例如 `server/`），并将config_front解压缩到另一个文件夹（例如 `front/`）。

将 CBCOJ_Server.exe 放在 `Server/` 文件夹下，将 CBCOJ_Front.exe 放在 `Front/` 文件夹中。

使用时，您应该先启动CBCOJ_Server.exe，获取运行CBCOJ_Server.exe的计算机的ipv4，稍后会用到。

#### 后端（评测服务器）

`server/` 的结构应该是这样的：

```plain
{
  'CBCOJ_Server.exe',
  'account.ini',
  'basic_setting.ini',
  'log.txt',
  'rc.txt',
  'records/':{
    ...
  },
  'work/':{
    ...
  },
  'work1/':{
    ...
  }
}
```

`account.ini` 存储所有帐户的名称和密码。您可以按照以下格式手动设置：

第一个列表包含一个非负整数 $n$，表示不同帐户的数量。

对于接下来的 $n$ 行，每行包含两个完全由非空格可见字符组成的字符串和一个用空格分隔的整数。

对于这些 $n$ 行中的任何一行，第一个字符串表示帐户的名称，第二个字符串表示账户的密码，整数表示账户的用户id。请注意，用户id是可重复的。

`basic_setting.ini` 存储了exe的一些设置。您可以按照以下格式进行更改：

第一行包含一个整数 $n$，表示要启动的评测线程的数量。

第二行包含文件夹的路径。提交的代码将临时存储在此处，但不会自动清除。

对于接下来的 $n$ 行，每一行都包含一个文件夹的路径。提交的代码将在此处运行，因此强烈建议在启动判断程序之前清理这些文件夹。

`log.txt` 是 CBCOJ_Server.exe 的日志文件。如果应用程序因未知原因崩溃，您可以将其发送给我。并且可以自由清除或删除。

`rc.txt` 存储最新的提交 id。

更详细的信息可以在发行声明中找到。

#### 前端（网页服务器）

`front/` 的结构应该是这样的：

```plain
{
  'CBCOJ_Front.exe',
  'config.json',
  'admin/':{
    'dashboard.html',
    'login.html',
    'assets/':{
      'admin.css',
      'admin.js'
    }
  },
  'public/':{
    'api/':{
      ...
    },
    'login/':{
      'index.html'
    },
    'submit/':{
      'index.html'
    },
    'files/':{
      ...
    },
    'templates/':{
      'record.html',
      'list.html',
      'content.html',
      'record.css',
      'comview.css',
      'listpagin.css',
      'login.js',
      'maodie.jpg',
      'chun.jpg'
    },
    'problem/':{
      ...
    },
    'records/':{
      ...
    },
    '403.html',
    '404.html',
    'index.html',
    'favicon.ico',
    'robots.txt',
  }
}
```

由于它是网站的前端，大多数文件只是为用户视图服务，您不需要关心他们的大多数。

你需要关心 `front/config.json `、`front/public/logg/` 和 `front/ppublic/files/`。

json 文件是 CBCOJ_Front.exe 的设置。结构如下：

```plain
{
	"port": ...,
	"ip": ...,
	"adport": ...,
	"adaccount": [
		{"username":"username1", "password":"password1"},
		{"username":"username2", "password":"password2"},
		...
	]
}
```

“port” 表示网站主站的端口号。

“adport” 表示网站管理站点的端口号。

“ip” 表示评测机的ip（IPv4）。

“adaaccount” 表示用于访问管理站点的用户名和密码。

在文件夹 `front/public/logg/` 中，您可以配置在后端设置的问题的题面。你应该把 problemname.html 放在文件夹中。

在文件夹 `front/public/files/` 中，您可以在其中放置一些文件。其他人可以通过以下网址访问或下载这些文件：`website/files/filename`。

### 工作原理

#### 前端（网页服务器）

![](https://raw.githubusercontent.com/chenyichen0420/CBCOJ/refs/heads/main/startprc.png)

![](https://raw.githubusercontent.com/chenyichen0420/CBCOJ/refs/heads/main/adminprc.png)

![](https://raw.githubusercontent.com/chenyichen0420/CBCOJ/refs/heads/main/mainprc.png)
