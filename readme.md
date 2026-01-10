**选择语言：** [简体中文](readme.html) | [English](readme-en.html)

## CBCOJ

### 开发动态

#### 本地部署

首个正式发布版本已经于此代码仓库中完成配置，相关文档将寒假中期完善。

#### 在线体验

受机房管理调整，上述服务极不稳定，可能长时间无法访问，敬请下载使用。

#### 后端开发

自版本 5.30.080 起，后端已支持 Windows (10/11) 和 Linux 双平台！

自版本 5.35.090 起，后端支持多子任务捆绑测试，这与过去强制捆绑所有测试点的策略不同。

由于开发策略调整，比赛功能可能在半年后再考虑进行开发。

自版本 6.36.108 起，支持配置多前端+多后端的分布式服务！

#### 前端开发

自版本 5.35.090 起，前端支持多子任务捆绑测试，这与过去强制捆绑所有测试点的策略不同。相关的用户界面设计也已相应调整。

由于开发策略调整，比赛功能可能在半年后再考虑进行开发。

自版本 6.36.108 起，支持配置多前端+多后端的分布式服务！

版本 7.xx.xxx 将会支持前端上传题目，预计在 4 月份上线，敬请期待。

### 什么是 CBCOJ？

CBCOJ 是一个极其轻量的在线判题系统。它专注于核心功能：用户登录/注销、题目获取、代码提交以及查询评测结果。

CBCOJ 网页服务端使用 Node.js 配合 HTML/CSS 进行便捷的网页渲染，而高性能的后端则负责请求处理和代码评测。有如下优点：

1.  **极低的硬件要求：** 能在资源非常有限的系统上高效运行。
2.  **高访问效率：** 为快速处理请求而优化。测试表明，单个前端+单个后端可在 1 秒内处理 300+ 个登录请求（未启用访问频率限制）。

这使得 CBCOJ 成为搭建个人或本地 OJ 的理想方案，几乎可以实现零成本运营。

### 如何使用 CBCOJ

参见各个版本的说明。

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
        "adport": ...,
        "adaccount": [
            {"username": "username1", "password": "password1"},
            {"username": "username2", "password": "password2"},
            ...
        ],
        (待更新6.xx.xxx新配置)
    }
    ```
    * "port" 表示主网站端口；
    * "adport" 表示管理站点端口；
    * "adaccount" 表示管理站点登录账密。
*   `front/public/problem/`：请将题目描述以 `problemname.html` 为名的文件添加到此目录下。
*   `front/public/files/`：放置在此处的文件可以通过 `your_website/files/filename` 公开访问或下载。
