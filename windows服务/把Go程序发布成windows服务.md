### [把Go程序发布成windows服务](http://marcofly.iteye.com/blog/1914165)

[go](http://www.iteye.com/blogs/tag/go) 

近日正在考虑用go程序做一个报表计算服务，在G+上看到有老外介绍把go打包的exe发布成window service，遂把该文章翻译过来，一同分享。 
原文地址：<http://sanatgersappa.blogspot.com/2013/07/windows-service-with-go-easy-way.html>（需要fangqiang） 
大致方法： 
**1.**  第一步当然是先将你的go程序打包成exe，比如go web server。 
**2.**  使用NSSM发布windows服务，命令：nssm install MyService d:\MyService.exe，                            MyService是服务名，d:\MyService.exe是程序所在地址。 
**3.**  删除服务，命令：sc delete MyService 
NSSM地址：<http://nssm.cc/>





https://blog.csdn.net/haidisenlin0/article/details/78785374