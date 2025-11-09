**Select Language:** [简体中文](README.md) | [English](readme.en.md)

## CBCOJ

### Development News

Starting from version 5.30.080, the backend now supports both Windows (10/11) and Linux!

### What is CBCOJ?

CBCOJ is an extremely lightweight Online Judge system. It focuses on core functionalities: user login/logout, problem retrieval, code submission, and querying evaluation results.

~~Unlike traditional OJs accessed via browsers, CBCOJ originally consisted of paired client-server programs for interaction.~~

This description is now history. CBCOJ has evolved to include both a front-end and a back-end, making it fully accessible through a web browser.

Despite this advancement, CBCOJ remains exceptionally lightweight. Crucially, the entire backend is built from scratch using pure C++, without relying on *any* external libraries or frameworks.

The front-end utilizes Node.js with HTML/CSS for convenient web rendering, while the high-performance back-end handles request processing and code evaluation. This architectural choice brings significant advantages:

1.  **High Portability:** Simple deployment across different environments.
2.  **Minimal Hardware Requirements:** Runs efficiently on very low-resource systems.
3.  **High Access Efficiency:** Optimized for fast request handling. Benchmark tests show the backend can process 100,000 login requests in approximately 8 seconds (without access rate limiting).

These characteristics make CBCOJ an ideal solution for hosting a personal or local OJ with near-zero operational cost.

### How to Use CBCOJ

You will need to download five files: `CBCOJ_Server.exe`, `CBCOJ_Front.exe`, `upx.exe`, `config_server.zip`, and `config_front.zip`.

Place all three `.exe` files in the same directory. Then, run the following command:

`upx.exe -d CBCOJ_Front.exe`

This will decompress `CBCOJ_Front.exe`, generating a new version that replaces the original file.

Extract `config_server.zip` into a dedicated folder (e.g., `server/`), and extract `config_front.zip` into another folder (e.g., `front/`).

Move `CBCOJ_Server.exe` into the `server/` folder and `CBCOJ_Front.exe` into the `front/` folder.

During operation, start `CBCOJ_Server.exe` (the judge server) first. Note the IPv4 address of the machine running the judge server, as it will be needed for front-end configuration.

#### Backend (Judge Server)

The structure of the `server/` directory should resemble:

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

*   `account.ini`: Stores user account information. Manually configure it as follows:
    *   First line: A single integer `n` (number of accounts).
    *   Next `n` lines: Each line contains two strings (username, password) and one integer (user ID), all separated by spaces. Usernames and passwords should consist of non-space visible characters. User IDs can be repeated.
*   `basic_setting.ini`: Configures server settings.
    *   Line 1: Integer `n` (number of evaluation threads).
    *   Line 2: Path to a folder for temporary storage of submitted code (not auto-cleaned).
    *   Next `n` lines: Paths to folders where code execution occurs. It is strongly recommended to clean these folders before starting the judger.
*   `log.txt`: Server log file. Can be sent for crash diagnostics and may be freely cleared or deleted.
*   `rc.txt`: Stores the latest submission ID.

Refer to the release notes for more detailed information.

#### Frontend (Web Server)

The structure of the `front/` directory should resemble:

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
    │   └── ...          # Place publicly accessible files here
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
    │   └── ...          # Store problem descriptions (.html files) here
    ├── records/
    │   └── ...
    ├── 403.html
    ├── 404.html
    ├── index.html
    ├── favicon.ico
    └── robots.txt
```

As this serves the website frontend, most files are for presentation and require no direct modification. Key components for configuration are:

*   `front/config.json`: Main configuration file for the front-end server.
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
    * "port" represents the port number of the main website.
    * "ip" represents the Judge Server's IPv4 address.
    * "adport" represents port number of the administration site.
    * "adaccount" represents the administration site accounts.
*   `front/public/problem/`: Add problem descriptions as `problemname.html` files in this directory.
*   `front/public/files/`: Files placed here are publicly accessible via `http://your_website/files/filename`.
