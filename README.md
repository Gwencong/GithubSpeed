# Linux 服务器 github 加速指南

本教程使用v2ray加速国内linux 服务器对github的访问（gitclone、push等），无需root权限

## 1. 本地windows电脑下载并配置v2rayN
这一步的主要目的是导出你的config.json配置文件。
### （1）下载[v2rayN](https://github.com/2dust/v2rayN/releases/download/6.33/v2rayN-With-Core.zip)
注意下载with-core版本，如下截图所示：
<div align="center">
<img src=https://github.com/Gwencong/GithubSpeed/assets/82023743/91ed6dc3-5772-44e4-8c8e-b24c2ae4b8ae width=60%> 
</div>

下载完成后解压，双击运行v2rayN.exe，如果电脑上没有下载.NET，运行v2rayN.exe会报错，按照报错提示下载安装.NET后，可正常运行v2rayN.exe打开v2ray
### （2）配置v2rayN并导出config.json文件
配置订阅过程自行百度完成，完成配置后，测试一下各个节点的速度，然后选择速度最快的节点，右键选择`导出所选服务器为客户端配置`即可导出得到`config.json`的配置文件。
这个文件之后将会上传到linux服务器上。

## 2. linux 服务器下载并配置v2ray
### （1）下载v2ray到服务器
从https://github.com/v2ray/v2ray-core/releases/tag/v4.28.2下载 v2ray-linux-64.zip 文件并上传到linux服务器，然后解压

### （2）用本地导出的config.json替换掉服务器中v2ray目录中的config.json文件

### （3）配置环境变量
在.bashrc文件中增加如下函数：
```bash
# set proxy
function setproxy() {
    export http_proxy=socks5://127.0.0.1:10808
    export https_proxy=socks5://127.0.0.1:10808
    export ftp_proxy=socks5://127.0.0.1:10808
    export no_proxy="172.16.x.x"
}
​
# unset proxy
function unsetproxy() {
    unset http_proxy https_proxy ftp_proxy no_proxy

```
### （4）测试
在终端cd到v2ray目录,运行v2ray，并且另外开一个终端，运行`setproxy`,然后运行`curl google.com`，如果输出一串东西，没有报错就是配置成功了。

