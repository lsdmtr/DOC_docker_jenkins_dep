# 一、安装docker和docker CE
首先执行几个命令
```shell
sudo apt install apt-transport-https ca-certificates curl software-properties-common gnupg lsb-release // 安装必要的证书并允许 apt 包管理器使用以下命令通过 HTTPS 使用存储库
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg // 添加Docker官方GPG密钥
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null // 添加docker官方库
sudo apt update // 更新ubuntu源列表
```
如果第二行添加GPG密钥失败，可以尝试国内镜像或者淘宝镜像：
```shell
# 国内镜像
sudo curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add
# 淘宝镜像
sudo curl -fsSL https://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```
安装docker CE：
```shell
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
安装完成以后可以使用如下命令检验是否正确安装
```shell
systemctl start docker #运行 Docker 服务
systemctl enable docker　#使 Docker 服务在每次重启时自动启动
systemctl status docker #查看docker运行状态
docker version # 查看已安装的 Docker 版本
```
# 二、安装docker compose
通过命令直接下载安装：
```shell
# 版本号自己选择
url -L https://get.daocloud.io/docker/compose/releases/download/v2.4.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
# 官方github链接
sudo curl -L https://github.com/docker/compose/releases/download/v2.2.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
检查安装是否成功
```shell
docker-compose --version
```
# 三、拉取镜像
这里用到nginx和jenkins
```shell
docker pull nginx:latest
docker pull jenkins/jenkins:lts
```
拉取jenkins的时候可能需要你登录docker账号，所以需要提前去docker官网注册一个。<br>
安装完成以后查看一下镜像列表看看都正常否:
```shell
docker images
```