# goini

> goini是用golang开发的一个超级轻量级的ini库 (**fork于github.com/houzhongjian/goini项目**)，在原有项目基础上加入配置重读功能。

### 安装方式
> go get github.com/keepchen/goini

### 使用方式
```go
package main

import (
    "github.com/houzhongjian/goini"
    "log"
)

func main() {
    //初始化.
    if err := goini.Load("app.conf"); err != nil {
        log.Printf("%+v\n", err)
        return
    }

    goini.GetString("db_host")
    goini.GetInt("db_port")
    goini.GetBool("isUpload")
    ...
  
  	//重读
  	go func() {
      for {
        time.Sleep(time.Second * 3)
        goini.Reload("./test.ini")
      }
    }()

    for {
      time.Sleep(time.Second * 3)
      fmt.Printf("(reload) isUpload: %t\n", goini.GetBool("isUpalod"))
    }
}
```

### 配置文件示例
```
# mysql 配置
db_name = blog
db_host = 127.0.0.1
db_pwd
db_port = 3306

#wechat
appid =sdfsffqr545242


#common
isUpload=true
isShare

#
page_size = 50

```

#### 感谢

最后，感谢[houzhongjian/goini](https://github.com/houzhongjian/goini)项目！

