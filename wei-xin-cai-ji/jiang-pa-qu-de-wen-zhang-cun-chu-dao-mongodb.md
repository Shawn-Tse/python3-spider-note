### 下载&安装

MongoDB:[https://www.mongodb.com/download-center\#atlas](https://www.mongodb.com/download-center#atlas)

现在MongoDB已经是4.0版本，不用在手动配置服务了

### 创建用户和密码

```
> use admin
switched to db admin
> db.createUser({user: 'admin', pwd: '123456', roles: [{role: 'root', db: 'admin'}]})
Successfully added user: {
        "user" : "admin",
        "roles" : [
                {
                        "role" : "root",
                        "db" : "admin"
                }
        ]
}
```





