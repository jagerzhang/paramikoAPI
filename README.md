# paramikoAPI
remote command and file transfer API Base on paramiko and sftp

简单说下用法：
Python

先在Python脚本中载入，需要提前安装paramiko和pysftp插件（推荐pip命令安装）
from xxxx import remoteCtrl

执行远程命令，需要传入远程服务器ip地址、密码、命令、远程ssh端口，用户名和超时时间
myHandler = remoteCtrl()
ret, ret_info = myHandler.command(ip, password, cmd, port, user, timeout )

ret 表示最后一个命令的退出状态，ret_info 则是远程命令的打屏信息（含报错）

进行文件传输，需要传入远程服务器ip地址、密码、源文件路径、目标文件路径、传输动作（pull/push）、用户名、端口和超时时间
myHandler = remoteCtrl()
ret, ret_info = myHandler.transfer(ip, password, src, dst , action, user, port, timeout )

ret 表示传输结果，ret_info 是返回信息

先在Python脚本中载入，需要提前安装paramiko和pysftp插件（推荐pip命令安装）
from xxxx import remoteCtrl
 
执行远程命令，需要传入远程服务器ip地址、密码、命令、远程ssh端口，用户名和超时时间
myHandler = remoteCtrl()
ret, ret_info = myHandler.command(ip, password, cmd, port, user, timeout )
 
ret 表示最后一个命令的退出状态，ret_info 则是远程命令的打屏信息（含报错）
 
进行文件传输，需要传入远程服务器ip地址、密码、源文件路径、目标文件路径、传输动作（pull/push）、用户名、端口和超时时间
myHandler = remoteCtrl()
ret, ret_info = myHandler.transfer(ip, password, src, dst , action, user, port, timeout )

ret 表示传输结果，ret_info 是返回信息
代码很简单，不清楚的请注意代码中的注释，下面啰嗦下文件传输的说明：

①、规定目标文件夹（dst）必须以斜杠 / 结尾，否则识别为文件，而src因是实体存在，所以程序会自动判断是文件还是文件夹。

②、当执行本地文件夹推送至远程文件夹时，将不会保留本地文件夹名称，而是将本地文件夹内的所有文件推送到远程文件夹内，比如：
/data/srcdir/   传送到 /data/dstdir/ ，结果是srcdir下的所有文件会存储在dstdir
若想保留文件夹名称，请保证两端文件夹名称一致即可，比如：
/data/srcdir/   推送到 /data/srcdir/

③、文件传输demo：
将本地的/data/src.tar.gz推送到192.168.0.10服务器的/data/files/dst.tar.gz
Python

myHandler = remoteCtrl()
ret, ret_info = myHandler.transfer('192.168.0.10','123456','/data/src.tar.gz','/data/files/dst.tar.gz', 'push' )

myHandler = remoteCtrl()
ret, ret_info = myHandler.transfer('192.168.0.10','123456','/data/src.tar.gz','/data/files/dst.tar.gz', 'push' )

Ps：若action='pull'则表示将src拉取到本地的dst。
