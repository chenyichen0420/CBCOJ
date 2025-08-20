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

#### Backend

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

`account.ini` stores the name and password of all accounts. You can set it manually.

`basic_setting.ini` stores some settings of the exe. You may change it in a specific way.

`log.txt` is the log file of CBCOJ_Server.exe. You can send it to me if the application crashes for some unknown reason.

`rc.txt` stores the latest submission id.

More detailed information can be found in the release statement.

#### Frontend

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

More detailed information can be found in the release statement.
