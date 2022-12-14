## Celestia mamaki 验证节点部署

### 第一步 环境准备

#### 1、系统依赖安装：安装用到的依赖包

    sudo apt install curl tar wget clang pkg-config libssl-dev jq build-essential git make ncdu tmux -y

#### 2、golang编译环境安装

##### a、下载Go压缩包

    cd $HOME
    wget "https://go.dev/dl/go1.19.4.linux-amd64.tar.gz"
    sudo rm -rf /usr/local/go
    sudo tar -C /usr/local -zxvf go1.19.4.linux-amd64.tar.gz

##### b、设置golang的环境变量

    echo "export GOROOT=/usr/local/go" |  sudo tee -a /etc/profile
    echo "export GOPATH=$HOME/go" |  sudo tee -a /etc/profile
    echo "export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin" |  sudo tee -a /etc/profile
    echo "export GO111MODULE=on" |  sudo tee -a /etc/profile
    echo "export GOPROXY=https://goproxy.cn" |  sudo tee -a /etc/profile

##### c、使用环境生效

    source /etc/profile

#### 3、设置进程运行的文件句柄数量：防止进程莫名其秒的自动退出

    echo "ulimit -SHn 1048576" |  sudo tee -a /etc/profile
    echo "* hard nofile 1048576" |  sudo tee -a /etc/security/limits.conf
    echo "* soft nofile 1048576" |  sudo tee -a /etc/security/limits.conf
    echo "DefaultLimitNOFILE=1048576" |  sudo tee -a /etc/systemd/user.conf
    echo "DefaultLimitNOFILE=1048576" |  sudo tee -a /etc/systemd/system.conf
    echo "session required pam_limits.so" |  sudo tee -a /etc/pam.d/common-session
    source /etc/profile

### 第二部分 部署celestia-app

#### 1、编译celestia-appd二进制应用

    cd $HOME
    rm -rf celestia-app
    git clone https://github.com/celestiaorg/celestia-app.git
    cd celestia-app/
    APP_VERSION=v0.6.0
    git checkout tags/$APP_VERSION -b $APP_VERSION
    make install
    sudo cp $HOME/go/bin/celestia-appd /usr/local/bin/
    celestia-appd version

#### 2、准备网络创世文件

    cd $HOME
    rm -rf networks
    git clone https://github.com/celestiaorg/networks.git
    MONIKER="AlchemyLabs"  # MONIKER为验证节点的名称, 会显示在浏览器上




## celestia mamaki 测试网接水教程

### 第一步：准备钱包地址

方式一：Keplr钱包

1、安装Keplr钱包

https://www.keplr.app/download

2、将 Celestia 做为网络添加到 Keplr钱包中

http://aviaone.com/celestia-connect-wallet-keplr-testnet-mamaki.html/

方式二：安装节点，通过命令生成钱包，轻节点与验证节点都支持

### 第二步：加入官方DC开始接水

https://discord.com/invite/YsnTPcSfWQ

完成基本认证后进入频道，输入接水命令，即可。图中1为频道，2为接水命令（换成自己的钱包地址），3为接水成功后机器人的回答。成功后获得10TIA。

![image](https://user-images.githubusercontent.com/100336530/204741398-bcebe555-718b-4c69-b337-7a54bebf1dc9.png)

注意：同一DC帐号，同一钱包；不同DC帐号，同一钱包接水都有7天的间隔时间

![image](https://user-images.githubusercontent.com/100336530/204741497-1eab1b82-5a3f-459b-8d58-d5b2735364bd.png)
