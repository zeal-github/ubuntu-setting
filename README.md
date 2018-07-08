# 这篇文档是用来当重装ubuntu时进行的一些配置

先使用git下载本仓库
```
sudo apt-get install git
git clone git@github.com:zeal-github/ubuntu-setting.git
```
>* ### [一、shadowsocks-qt5安装以及全局pac的配置](#一、shadowsocks-qt5安装以及全局pac的配置) 
>* ### [二、安装各种必要软件](#title2)
>* ### [三、美化](#title3)
>* ### [四、设置以上软件的开机启动](#title4)
>* ### [五、其他系统设置](#title5)
>* ### [六、anaconda设置](#六anaconda设置)

## <span id="1">一、shadowsocks-qt5安装以及全局pac的配置</span>
原文链接：[Ubuntu 16安装shadowsocks-qt5并使用PAC全局代理](https://www.litcc.com/2016/12/29/Ubuntu16-shadowsocks-pac/index.html)<br>

### 1、保持系统软件包是最新的
```
sudo apt-get updat
sudo apt-get upgrade
```
### 2、设置ppa源并安装shadowsocks-qt5
```
sudo add-apt-repository ppa:hzwhuang/ss-qt5
sudo apt-get update
sudo apt-get install shadowsocks-qt5
```

[github:shadowsokcs-qt5使用手册](https://github.com/shadowsocks/shadowsocks-qt5/wiki/%E4%BD%BF%E7%94%A8%E6%89%8B%E5%86%8C)
### 3、配置shadowsocks-qt5
这个时候可以直接打开shadowsocks-qt5，然后设置好服务器地址和端口然后打开链接，下面可能需要使用
### 4、配置全局代理
>当直接clone本项目到本地时可以使用项目里自带的autoproxy.pac文件，可跳过这个步骤
* 安装genpac
```
apt-get install python-pip
sudo pip install genpac
pip install --upgrade genpac
```
* 使用genpac下载gfwlist（使用的本地代理和生成本地代理都为 127.0.0.1:1080）<br>
输出默认为:/home/user/autoproxy.pac
```
genpac --pac-proxy "SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" --gfwlist-url=https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt --output="autoproxy.pac"
```
* 设置全局代理(firefox浏览器不知道为什么不能使用全局代理，需要下载插件)
>点击：System settings > Network > Network Proxy，选择 Method 为 Automatic，设置 Configuration URL 为 autoproxy.pac 文件的路径，点击 Apply System Wide。
格式如：file:///home/{user}/autoproxy.pac

-----

## <span id="title2">二、安装各种必要软件 </span>
### 1、chrome浏览器
>直接使用项目里的安装文件，或者当开启代理并且可以正常使用的时候可以直接从官网下载

### 2、安装sougou拼音输入法
>直接使用项目里的安装文件，或者直接搜索 `搜狗linux`<br>
设置黑色皮肤，候选词个数为`8个`<br>
输入法安装后需要重启才能生效

### 3、安装Albert
```
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt update
sudo apt install albert
```
>设置搜索快捷键为 `ctrl+shift+f`
### 4、安装vscode
>可以直接在ubuntu软件应用中安装<br>
如果在vscode的终端无法显示下划线，那么在设置里将【终端字号】改为13

### 5、安装有道词典
>直接在网上搜索即可，有linux版本
---
## <span id="title3">三、美化</span>

原文链接：[不美翻怎么开发!Ubuntu 16.04 LTS深度美化!(2017年度定稿版)](https://www.jianshu.com/p/4bd2d9b1af41)

### 1、久负盛名的扁平化主题--flatabulous-theme
```
sudo add-apt-repository ppa:noobslab/themes
sudo apt-get update
sudo apt-get install flatabulous-theme
```

### 2、图标
>图标的下载完unity-tweak-tool之后可以在里面直接选，不好看再换下面两个
1.  圆形图标--icon-theme-circle
```
sudo add-apt-repository ppa:numix/ppa
sudo apt-get update
sudo apt-get install numix-gtk-theme numix-icon-theme-circle
```
2. （配合扁平化主题）--ultra-flat-icons
```
sudo add-apt-repository ppa:noobslab/icons
sudo apt-get update
sudo apt-get install ultra-flat-icons
```

### 3、指针和字体
```
后续更新，目前觉得没有必要
```

### 4、运用和设置--unity-tweak-tool
```
sudo apt-get install unity-tweak-tool
```
> 安装完毕之后打开unity进行设置
>> 1、设置launch栏的自动隐藏和图标大小以及透明<br>
2、设置好`主题`和`图标`<br>

### 5、终端美化,安装oh-my-zsh
```
sudo apt-get install zsh
sudo apt-get install git
sudo wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
chsh -s /bin/zsh
```
>右键终端进入 `配置文件-配置文件首选项-颜色` 调整透明度

### 6、dock栏美化--docky
```
sudo apt-get install docky
```
>安装后要启动才能生效，如果要固定其他图标到dock栏，可以打来新窗口然后在dock上右键-固定到dock，或者生成快捷链接到桌面然后拖拽到dock<br>
docky 带有一些dock栏插件，比如Gmail，天气等

### 7、桌面插件-- conky-manager
```
sudo apt install conky-all
sudo apt-add-repository -y ppa:teejee2008/ppa
sudo apt update
sudo apt install conky-manager
```
>安装这个manager之后，需要进入里面的插件，然后点击编辑文件，<br>
把 `own_window_type = normal` 改为`own_window_type = desktop`<br>
不然的话一按显示桌面所有的插件就会消失

>移除ppa源可以使用下面命令
>>```
>>sudo apt-get install ppa-purge 
>>sudo ppa-purge ppa:teejee2008/ppa


---

## <span id = "title4" >四、设置以上软件的开机启动</span>
>在搜索栏搜索 `gnome-session`/`启动应用程序` 在里面添加启动项<br>
url地址为/usr/bin/<br>
shdowsocks-qt5 : `ss-qt5`<br>
Albert : albert

---
## <span id = "title5">五、其他系统设置</span>
### 1、更改桌面壁纸
### 2、更改【显示桌面快捷键为】super+D （默认为ctrl+super+t）
>先打开【设置-外观-行为】勾选[添加"显示桌面“图标到启动器]<br>
然后打开【设置-键盘-导航】更改隐藏所有窗口快捷键
### 3、默认的双指滚动方式与windows相反 [链接](https://blog.csdn.net/LanderlYoung/article/details/18313911)
>打开【设置-鼠标和触摸板】最下面，勾选[自然是滚动]<br>
>或者使用下面的两个命令行语句，数字绝对值越小越灵敏.(如果b报错则需要安装第三行的驱动)
```
synclient VertScrollDelta=-103
synclient HorizScrollDelta=-103
#sudo apt-get install xserver-xorg-input-synaptics
```

---

## <span id ="titlesix"></span>六、anaconda设置
### 1、直接到官网下载，速度不慢，然后安装
### 2、如果在终端找不到anaconda的命令，则按照下面进行设置
>加入：export PATH="/Users/yizhen/anaconda/bin（自己安装anaconda的位置）:$PATH"<br>
然后执行source ~/.zshrc即可。


