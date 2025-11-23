**选择语言：** [简体中文](README.md) | [English](readme.en.md)

## CBCOJ

### 开发动态

#### 本地部署

首个正式发布版本已经于此代码仓库中完成配置，相关文档将在 3 周内完善。

#### 在线体验

通常情况下，您可以在**周日晚8点至下周六下午3点**期间访问[此网站](https://cbcoj.loca.lt/)来体验我们的最新功能。

但请注意，此网站仅是一个通过内网穿透生成的临时地址，它可能被重定向到他人的恶意网站，因此**请勿输入任何敏感信息**。

您也可以通过 localtunnel 显示的 "Tunnel Password" 来验证是否为本站点。通常情况下，该密码会是 `222.212.136.221`。关于 localtunnel 的更多详细信息，请访问[其官方网站](https://theboroer.github.io/localtunnel-www/)。

登录时，您可以使用一些临时的测试账户，其用户名和密码相同，为从 1 到 100 的整数。

#### 后端开发

自版本 5.30.080 起，后端已支持 Windows (10/11) 和 Linux 双平台！

自版本 5.35.090 起，后端支持多子任务捆绑测试，这与过去强制捆绑所有测试点的策略不同。

由于学业压力，比赛功能将尽可能在3个月内上线。

#### 前端开发

自版本 5.35.090 起，前端支持多子任务捆绑测试，这与过去强制捆绑所有测试点的策略不同。相关的用户界面设计也已相应调整。

由于学业压力，比赛功能将尽可能在3个月内上线。

### 什么是 CBCOJ？

CBCOJ 是一个极其轻量的在线判题系统。它专注于核心功能：用户登录/注销、题目获取、代码提交以及查询评测结果。

~~与通过浏览器访问的传统 OJ 不同，CBCOJ 最初是由配套的客户端程序与服务器进行交互。~~

这种描述已成为历史。CBCOJ 现已发展为包含完整的前端和后端，可以通过网页浏览器直接访问。

尽管功能增强，CBCOJ 依然保持极致的轻量化。关键在于，其整个**后端完全由纯 C++ 从零开始手写实现，未使用任何外部库或框架**。

前端使用 Node.js 配合 HTML/CSS 进行便捷的网页渲染，而高性能的后端则负责请求处理和代码评测。这种架构选择带来了显著优势：

1.  **高可移植性：** 可在不同环境中轻松部署。
2.  **极低的硬件要求：** 能在资源非常有限的系统上高效运行。
3.  **高访问效率：** 为快速处理请求而优化。基准测试表明，后端可在约 8 秒内处理 10 万个登录请求（未启用访问频率限制）。

这些特性使得 CBCOJ 成为搭建个人或本地 OJ 的理想解决方案，几乎可以实现零成本运营。

### 如何使用 CBCOJ

您需要下载五个文件：`CBCOJ_Server.exe`、`CBCOJ_Front.exe`、`upx.exe`、`config_server.zip` 和 `config_front.zip`。

将三个 `.exe` 文件置于同一目录下。然后，运行以下命令：

`upx.exe -d CBCOJ_Front.exe`

此命令将解压缩 `CBCOJ_Front.exe`，生成的新文件会直接替换原文件。

将 `config_server.zip` 解压到一个专用文件夹（例如 `server/`），将 `config_front.zip` 解压到另一个文件夹（例如 `front/`）。

将 `CBCOJ_Server.exe` 移至 `server/` 文件夹，将 `CBCOJ_Front.exe` 移至 `front/` 文件夹。

运行时，请先启动 `CBCOJ_Server.exe`（判题服务器）。请记下运行判题服务器的机器的 IPv4 地址，后续配置前端时会用到。

#### 后端（判题服务器）

`server/` 目录的结构应类似于：

```
server/
├── CBCOJ_Server.exe
├── account.ini
├── basic_setting.ini
├── log.txt
├── rc.txt
├── records/
│   └── ...
├── work/
│   └── ...
└── work1/
    └── ...
```

*   `account.ini`：存储用户账户信息。请按以下格式手动配置：
    *   第一行：一个整数 `n`（账户数量）。
    *   后续 `n` 行：每行包含两个字符串（用户名、密码）和一个整数（用户ID），均由空格分隔。用户名和密码应由非空格的可见字符组成。用户ID可以重复。
*   `basic_setting.ini`：配置服务器设置。
    *   第 1 行：整数 `n`（评测线程数）。
    *   第 2 行：一个文件夹路径，用于临时存储提交的代码（不会自动清理）。
    *   后续 `n` 行：代码执行所在文件夹的路径。强烈建议在启动判题程序前清理这些文件夹。
*   `log.txt`：服务器日志文件。若程序因未知原因崩溃，可发送此文件以供诊断。可以自由清空或删除。
*   `rc.txt`：存储最新的提交 ID。

更详细的信息请参阅发布说明。

#### 前端（网页服务器）

`front/` 目录的结构应类似于：

```
front/
├── CBCOJ_Front.exe
├── config.json
├── admin/
│   ├── dashboard.html
│   ├── login.html
│   └── assets/
│       ├── admin.css
│       └── admin.js
└── public/
    ├── api/
    │   └── ...
    ├── login/
    │   └── index.html
    ├── submit/
    │   └── index.html
    ├── files/
    │   └── ...          # 将公开访问的文件放在此处
    ├── templates/
    │   ├── record.html
    │   ├── list.html
    │   ├── content.html
    │   ├── record.css
    │   ├── comview.css
    │   ├── listpagin.css
    │   ├── login.js
    │   ├── maodie.jpg
    │   └── chun.jpg
    ├── problem/
    │   └── ...          # 在此目录下存储题目描述文件 (.html)
    ├── records/
    │   └── ...
    ├── 403.html
    ├── 404.html
    ├── index.html
    ├── favicon.ico
    └── robots.txt
```

由于这是网站前端，大部分文件用于页面呈现，无需直接修改。需要配置的关键部分包括：

*   `front/config.json`：前端服务器的主配置文件。
    ```
    {
        "port": ...,
        "ip": ...,
        "adport": ...,
        "adaccount": [
            {"username": "username1", "password": "password1"},
            {"username": "username2", "password": "password2"},
            ...
        ]
    }
    ```
    * "port" 表示主网站端口；
    * "ip" 表示判题服务器的 IPv4 地址；
    * "adport" 表示管理站点端口；
    * "adaccount" 表示管理站点登录账密。
*   `front/public/problem/`：请将题目描述以 `problemname.html` 为名的文件添加到此目录下。
*   `front/public/files/`：放置在此处的文件可以通过 `http://your_website/files/filename` 公开访问或下载。
