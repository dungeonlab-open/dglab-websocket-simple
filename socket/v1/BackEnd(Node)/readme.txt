0. 以下代码适用于Linux服务器，使用Node官网的linux包管理下载
https://nodejs.org/en/download/package-manager

推荐使用NVM安装

根据官网的命令行提示选择并安装Node18及以上版本（推荐安装后缀LTS的版本）

逐行复制页面中的Linux命令到服务器中执行，等待提示完成之后，查看安装的版本是否正确，那之后请重启命令窗口或远程窗口。

接下来安装必要的后台运行环境：

1. npm install
进入项目目录后执行 npm install，根据 package.json 自动安装项目依赖（ws、uuid 等）。

2. npm i pm2 -g
全局安装 PM2。由于 Node 程序不支持后台运行，且 Linux 自带后台运行不可靠，强烈推荐使用 PM2 来托管你的服务在后台运行（支持程序崩溃时自动重启）。

3. pm2 start websocketNode.js --name dglab-socket
使用 PM2 启动服务，--name 参数指定一个便于识别的名称。

4. pm2 save
保存当前 PM2 进程列表，服务器重启后可通过 pm2 resurrect 恢复。

常用 PM2 命令：
- pm2 list                查看所有运行中的服务
- pm2 logs dglab-socket   查看服务实时日志
- pm2 stop dglab-socket   停止服务
- pm2 restart dglab-socket 重启服务
- pm2 delete dglab-socket  从 PM2 列表中移除服务
- pm2 startup             设置开机自启（按提示执行输出的命令）