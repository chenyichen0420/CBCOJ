## CBCOJ

### What's CBCOJ

CBCOJ is a super lightweight mini OJ that can and only supports login, logout, obtaining questions, submitting reviews, and querying review results.

~~This OJ is not accessible through a browser like other OJs, it is just a pair of accompanying programs where the client interacts with the server.~~

Such descriptions has already became history. Now it has both front-end and back-end, able to reach on 

However, it remains super lightweight as all the codes were written on hand, without using any existing extension libs or softwares.

In addition, I've finished many tests on this OJ. It finishes 100K login requests in about 8 seconds(without any access limitation).

For the front-end, we used Node.js+HTML+css for convenient web page rendering.

For the back-end, we used the more efficient C++ for high-speed and low consumption processing.

These factors gives CBCOJ some significant advantages:

1. High portability
2. Low hardware requirements
3. High access efficiency

You can imaging that there's a lot more benefits other than the above advantages. So it's ULTRA suitable if you want to run a personal/local OJ with nearly zero cost!

### How to use CBCOJ

You should download five files: CBCOJ_Server.exe, CBCOJ_Front.exe, upx.exe, config_server.zip, and config_front.zip.

Put the above three files in the same folder. Then run this command below:

`upx.exe -d CBCOJ_Front.exe`

A different CBCOJ_Front.exe will be automatically generated and directly replace the original one.

Extract config_server.zip into a folder(take `server/` for example), and extract config_front into another(take `front/` for example).

Put CBCOJ_Server.exe under the folder `server/`, and put CBCOJ_Front.exe under the folder  `front/`.

When using, you should start CBCOJ_Server.exe first, fetch the ipv4 of the machine on which CBCOJ_Server.exe runs, it'll be used later.

#### Backend(Judge Server)

The structure of `server/` should be like this:

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

`account.ini` stores the name and password of all accounts. You can set it manually, following the following format:

The first list contains one non-negative integer $n$, representing the number of different accounts.

For the next $n$ lines, each line contains two string consisting entirely of non space visible characters and one integer, separated with spaces.

For any one of these $n$ lines, the first string represents the name of an account, the second string represents the password of the account, the integer represents the user id of the account. Note that user id is repeatable.

`basic_setting.ini` stores some settings of the exe. You may change it following the following format:

The first line contains one integer $n$, representing the number of evaluation threads you want to start.

The second line contains the path of a folder. The submitted code will be temporarily stored here, but it will not be automatically cleaned.

For the next $n$ lines, each line contains a path of a folder. The submitted code will runs in here, so it's strongly recommended to clean these folders before starting the judger program.

`log.txt` is the log file of CBCOJ_Server.exe. You can send it to me if the application crashes for some unknown reason. And it can be cleared or deleted freely.

`rc.txt` stores the latest submission id.

More detailed information can be found in the release statement.

#### Frontend(Webpage Server)

The structure of `front/` should be like this:

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

Since it's the frontend of a website, most files simply serves for the user view, you don't need to care about move of them.

You need to focus on `front/config.json`, `front/public/problem/`, and `front/public/files/`.

the json file is the settings for CBCOJ_Front.exe. The structure is as follow:

```plain
{
	"port": ...,
	"ip": ...,
	"adport": ...,
	"adaccount": [
		...
	]
}
```
