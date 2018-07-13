



go install/build都是用来编译包和其依赖的包。
区别：
go build只对main包有效，在当前目录编译生成一个可执行的二进制文件（依赖包生成的静态库文件放在$GOPATH/pkg）。
go install一般生成静态库文件放在$GOPATH/pkg目录下，文件扩展名a.
	如果为main包，则会在$GOPATH/bin 生成一个可执行的二进制文件