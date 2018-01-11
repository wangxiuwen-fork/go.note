







> 官网 下载地址： https://golang.org/dl/
>
> 中文安装文档: https://go-zh.org/doc/install





若你要从旧版本的Go升级，那么首先必须[卸载已存在的版本](https://go-zh.org/doc/install#uninstall)。

### Linux、Mac OS X 和 FreeBSD 的安装包

[下载此压缩包](http://code.google.com/p/go/downloads/list?q=OpSys-FreeBSD+OR+OpSys-Linux+OR+OpSys-OSX+Type-Archive)并提取到 `/usr/local` 目录，在 `/usr/local/go` 中创建Go目录树。例如：

```
tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz

```

该压缩包的名称可能不同，这取决于你安装的Go版本和你的操作系统以及处理器架构。

（此命令必须作为root或通过 `sudo` 运行。）

要将 `/usr/local/go/bin` 添加到 `PATH` 环境变量， 你需要将此行添加到你的 `/etc/profile`（全系统安装）或 `$HOME/.profile` 文件中：

```
export PATH=$PATH:/usr/local/go/bin

```

#### 安装到指定位置

Go二进制发行版假定它们会被安装到 `/usr/local/go` （或Windows下的 `c:\Go`）中，但也可将Go工具安装到不同的位置。 此时你必须设置 `GOROOT` 环境变量来指出它所安装的位置。

例如，若你将Go安装到你的home目录下，你应当将以下命令添加到 `$HOME/.profile` 文件中：

```
export GOROOT=$HOME/go
export PATH=$PATH:$GOROOT/bin

```

**注**：`GOROOT` 仅在安装到指定位置时才需要设置。