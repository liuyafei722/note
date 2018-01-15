# linux 学习笔记 #
#### 星期一, 09. 十月 2017 12:25下午 ####

- tar 解压命令 后面的-zxvf 参数
x : 从 tar 包中把文件提取出
z : 表示 tar 包是被 gzip 压缩过的，所以解压时需要用 gunzip 解压
v : 显示详细信息
f xxx.tar.gz :  指定被处理的文件是 xxx.tar.gz

- .tar 只是打包没有压缩 .tar.gz 是打包并压缩了的文件
- cp 复制
- mv移动
- chmod 修改权限
- cp -r复制命令  -r是为了将其中的文件夹以及子文件夹都复制
- 需要管理员权限来安装一个 .deb 文件。 打开终端后，输入：
	sudo dpkg -i package_file.deb 
    要卸载一个 .deb 文件，在您的软件包管理器中取消选中它。或者在终端中，输入:
	sudo dpkg -r package_name
- deb是debian， ubuntu等linux发行版的软件安装包。
