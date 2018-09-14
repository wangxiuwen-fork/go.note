

使用MySQL的链接池可能存在如下问题：在客户端连接池中的一条空闲链接，可能是一条已经被MySQL服务端关闭掉的链接。

看了网上的讨论，可以查看下面的链接[：mysql issues](https://github.com/go-sql-driver/mysql/issues/257#issuecomment-53886663)。然后查看官方的介绍，现在已经有了现成的解决方法。官方地址[：Connection pool and timeouts](https://github.com/go-sql-driver/mysql)

下面是beego中的设置MySQL连接池的方法：

```g
err = orm.RegisterDataBase("default", "mysql", iniConfig.String("mysql"))
if err != nil {
    logs.Error("db register data error:%v", err)
}
mdb, err := orm.GetDB("default")
if err != nil {
    panic(fmt.Errorf("get db error:%s", err))
}
mdb.SetConnMaxLifetime(time.Second * 20)
mdb.SetMaxIdleConns(10)
mdb.SetMaxOpenConns(30)1234567891011
```

如上面的代码，主要用来修改连接池中每个链接的最长生命时间、最大空闲链接数以及最大可以打开的链接。

因为在orm中并没有暴露SetConnMaxLifetime的方法，所以需要获取*DB对象来处理

```go
mdb, err := orm.GetDB("default")
```