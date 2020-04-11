-----------------------------------------------------------------------------------------------
【注册谷歌云获取300美金快捷通道】 https://console.cloud.google.com/freetrial?referralId=70215fed64754b8b91729319a16ef599 可能有额外奉送美金哦！
-----------------------------------------------------------------------------------------------

1. GCP创建VM实例
    Computer Engine→VM实例→创建实例

2.创建防火墙规则（由于trojan使用443 GCP默认是打开的）这步可以省去！

    VPC网络→防火墙规则→创建防火墙规则

3.解析域名
（教程使用cloudflare进行）
添加A记录，name为@，指向gcp实例外部ip地址；
添加A记录，name为www，指向gcp实例外部ip地址；
添加CNAME记录，name自定义，一般为3个字母，指向自己的域名，获得二级域名。
(可根据自己需要添加多次CNAME记录，在搭建过程中使用二级域名，申请失败导致安装失败)

4. 打开VM实例SSH页

5. 获取管理员权限
    命令：sudo -i

6. 安装trojan

    1）一键安装：
curl -O https://raw.githubusercontent.com/atrandys/trojan/master/trojan_mult.sh && chmod +x trojan_mult.sh && ./trojan_mult.sh

7. 查看和修改trojan服务器密码
vi /usr/src/trojan/server.conf

                注意：
                1.如果提示 curl: command not found ，那是因为你的 VPS 没装 Curl
                    ubuntu/debian 系统安装 Curl 方法: apt-get update -y && apt-get install curl -y
                    centos 系统安装 Curl 方法: yum update -y && yum install curl -y
                    安装好 curl 之后就能安装脚本了
                2.如果提示SELinux状态问题，请按要求输入Y重启VPS，然后再执行本脚本，否则可能https证书申请出错（up安装过程没有遇到这个问题）
                3.安装完成后一定记得通过提示的链接下载压缩文件
                4·如果你真的忘记下载了，那么进入/usr/share/nginx/html/目录下，找到一个乱码文件夹，进入会看到客户端文件，使用sftp下载下来即可。

8. 配置bbr加速
   wget --no-check-certificate -O tcp.sh https://github.com/cx9208/Linux-NetSpeed/raw/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh

推荐安装bbrplus加速
先看自己vps是否安装了加速内核，是否是bbrplus加速内核，不是的话请按脚本提示进行对应的内核及加速模块的卸载和安装。
