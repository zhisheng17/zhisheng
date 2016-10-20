爬虫代码：[V2EX帖子爬虫代码](https://github.com/zhisheng17/Python-Projects/blob/master/v2ex/V2EX.py)

> 背景：自己在做一个  V2EX  爬虫的时候，需要把爬取的帖子中的内容（ title  和  content）保存在本地数据库。
> 环境：Pycharm 2016.1  + MySQL 5.7  + Pyspider + MySQL workbench  + python 2.7 32位


###1. windows下安装MySQLdb出现的问题及其解决方法

**你有两个选择：**

+ 安装已编译好的版本（一分钟）
+ 从官网下，自己编译安装（介个…..半小时到半天不等，取决于你的系统环境以及RP）

		 1. 若是系统32位的，有c++编译环境的，自认为RP不错的，可以选择自己编译安装，当然，遇到问题还是难免的，一步步搞还是能搞出来的
		 2. 若是系统64位的，啥都木有的，建议下编译版本的，甭折腾
		


 1. 安装已编译的版本
  http://www.codegood.com/downloads 
	 根据自己安装的 Python 版本下载，32位的下载win32的， 64位的就下载cmd64的，切勿搞错是操作系统，双击安装，搞定， 然后import MySQLdb，查看是否成功。

		我的电脑，win7, 64位，python 2.7   32位版本 

		所以选择  MySQL-python-1.2.3.win32-py2.7.exe
 
 2.  自己编译安装：

		> 1. 安装setuptools
		在安装MySQLdb之前必须安装setuptools，要不然会出现编译错误
		http://pypi.python.org/pypi/setuptools
		http://peak.telecommunity.com/dist/ez_setup.py 使用这个安装（64位系统必须用这个）
		> 2. 安装MySQLdb
        > 下载MySQLdb  http://sourceforge.net/projects/mysql-python/
        > 解压后，cmd进入对应文件夹,如果32位系统且有gcc编译环境，直接 python setup.py build


####**问题汇总**

**1. 64位系统，无法读取注册表的问题**

异常信息如下：

> F:\devtools\MySQL-python-1.2.3>pythonsetup.py build
Traceback (most recent call last):
 File "setup.py", line 15, in <module>
   metadata, options = get_config()
 File "F:\devtools\MySQL-python-1.2.3\setup_windows.py", line7, in get_config
   serverKey = _winreg.OpenKey(_winreg.HKEY_LOCAL_MACHINE, options[' registry_ke
y'] )
WindowsError: [Error 2] The system cannotfind the file specified
 
 <br>
 
**解决方法：**

    其实分析代码，发现只是寻找mysql的安装地址而已  修改setup_windows.py如下
    注解两行，加入一行，为第一步mysql的安装位置
       serverKey = _winreg.OpenKey(_winreg.HKEY_LOCAL_MACHINE,options['registry_key'] )
      mysql_root, dummy = _winreg.QueryValueEx(serverKey,'Location')
      mysql_root = r"F:\devtools\MySQL\MySQL Server 5.5"
 

<br>

**2. 没有gcc编译环境**
    
    unable to find vcvarsall.bat

**解决方法:安装编译环境（一个老外的帖子）**
	
	> 1)  First ofall download MinGW. Youneed g++compiler and MingW make in setup.
	2)  If youinstalled MinGW for example to “C:\MinGW” then add “C:\MinGW\bin”to your PATH in Windows.（安装路径加入环境变量）
	3)  Now startyour Command Prompt and Go the directory where you have your setup.py residing.
	4)  Last andmost important step:
	setup.py install build --compiler=mingw32
	或者在setup.cfg中加入：
	[build]
	    compiler = mingw32



<br>

**3. gcc: /Zl: No suchfile or directory错误**

异常信息如下:

    > F:\devtools\MinGW\bin\gcc.exe -mno-cygwin-mdll -O -Wall -Dversion_info=(1,2,3,'
    > final',0) -D__version__=1.2.3"-IF:\devtools\MySQL\MySQL Server 5.5\include" -IC
    :\Python27\include -IC:\Python27\PC -c_mysql.c -o build\temp.win-amd64-2.7\Rele
    ase\_mysql.o /Zl
    gcc: error: /Zl: No such file or directory
    error: command 'gcc' failed with exitstatus 1 
    参数是vc特有的编译参数，如果使用mingw的话因为是gcc所以不支持。可以在setup_windows.py中去掉
    /Zl  
 
 <br>
 
**解决方法：**
 
    修改setup_windows.py  改为空的
        extra_compile_args = [ '/Zl' ]
            extra_compile_args = [ '' ]


<br>
<br>

### 测试有没有安装成功？

1. 在cmd命令行下执行如下图命令：
![这里写图片描述](http://img.blog.csdn.net/20161020222856240)
 
	如果没有报错的话，则表示成功了。

2. 代码测试（首先得创建数据库表）
```
DROP TABLE IF EXISTS `question`;
CREATE TABLE `question` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `title` VARCHAR(255) NOT NULL,
  `content` TEXT NULL,
  `user_id` INT NOT NULL,
  `created_date` DATETIME NOT NULL,
  `comment_count` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `date_index` (`created_date` ASC));
```

python 代码：

```
#-*-coding:utf8-*-
#created by 10412

import MySQLdb
import random


#测试连接数据库
if __name__ == '__main__':
    db = MySQLdb.connect("localhost", "root", "root", "wenda", charset="utf8")
    try:
        cursor = db.cursor()

        
        #插入数据
        sql = 'insert into question(title, content, user_id, created_date, comment_count) values("怎样能够写出一篇10万+的文章出来？", "看到微信公众号好多大V写出的文章阅读量都是这么多，但是不知道自己可以怎么写，需要注意点什么吗？", 14, now(), 0)'
        cursor.execute(sql)
        qid = cursor.lastrowid
        db.commit()
        print qid
        

        #查询数据
        sql = 'select * from question order by id desc limit 3'
        cursor.execute(sql)
        for each in cursor.fetchall():
            for row in each:
                print row

        db.commit()
    except Exception, e:
        print e
        db.rollback()
    db.close()


```

运行结果如下：

![这里写图片描述](http://img.blog.csdn.net/20161020223314445)

就表明成功了。


### 2.  HTTP 599: SSL certificate problem: unable to get local issuer certificate错误

**解决方法：**

使用 **self.crawl(url, callback=self.index_page, validate_cert=False)**

参考我写的博客文章 ： [《**PySpider HTTP 599: SSL certificate problem: unable to get local issuer certificate错误**》](http://blog.csdn.net/tzs_1041218129/article/details/52853465)

### 3. V2EX 网站更新，目前全站都是用的 Https, 自然在代码中也必须用 Https, 否则一直没用。自己在这个坑里蹲了很久。