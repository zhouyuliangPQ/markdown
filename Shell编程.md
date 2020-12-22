# Shell

## 基础

#! /bin/bash 文件头为解析器

注释以#号开头

```shell
#!/bin/bash
#注释
echo "hello world"
```

- 变量

  - 局部变量

    局部变量只在创建的脚本使用,

  - 环境变量

    环境变量再创建他们的shell及其派生出来的任意子进程中使用

  - 系统变量

    - $0 当前应用的名称
    - $n n=1,2...n 当前程序传入的第几个参数
    - $* 所有传入参数
    - $# 当前程序的参数个数
    - $? 上个命令或程序执行完后的状态,返回0表示执行成功
    - $UID 当前的用户ID
    - $PWD 当前所在目录

  ```shell
  #!/bin/bash
  A=123 #变量的定义,此处为局部变量
  echo $A
  echo $0 #使用系统变量 输出fileName
  echo "转义测试 \$? is $?" #前者输出是字符串,后者输出变量
  ```

- 条件语句

  - if

    ```shell
    #!/bin/bash
    
    if(($1 > 3));then #((符号判断))
    	echo "大于3"		
    else
    	echo "小于3"
    fi
    ##逻辑运算符解析
    # -f 判断文件是否存在 eg: if [-f filename]
    # -d 判断目录是否存在 eg: if [-d dir]
    # -eq 相等
    # -ne 不等
    # -lt 小于
    # -gt 大于
    # -le 小于等于
    # -ge 大于等于
    # -a and 与
    # -o or 或
    # -z 空字符串
    if [! -d /data/exmple];then
    	mkdir -p /data/exmple;
    fi
    
    ```

    写个mysql备份脚本

    ```shell
    #!/bin/bash
    BAK_DIR=/data/backup/`date +%Y_%m_%d` #使用日期作为目录名
    if [$UID -ne 0];then
    	echo "请使用root用户执行脚本"
    	exit
    fi
    if [! -d $BAK_DIR];then
    	mkdir -p $BAK_DIR
    else
    	echo "$BAK_DIR has exist"
    fi
    
    MYSQLCMD = /usr/bin/mysqldum
    
    $MYSQLCMD -uroot -p12345 -d puzzle >xxx.sql
    if [$? -eq 0];then
    	echo -e "成功"
    fi
    ```

    

