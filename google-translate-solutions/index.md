# 关于谷歌浏览器翻译的解决方案


最近一段时间在使用谷歌浏览器翻译时，经常会出现等了很久没反应或者翻译失败的情况😮‍💨，虽然我可不常用，但也不能完全就没用了吧。

## 解决方法

{{< admonition >}}
网上说是因为谷歌翻译退出了大陆的原因，所以导致 Chrome 浏览器内置翻译无法使用
{{< /admonition >}}

{{< admonition question >}}
为什么我谷歌浏览器有代理，但是翻译还是不行呢？

- 因为浏览器内置api不支持扩展配置的socks5代理，所以只有使用系统代理才能生效。
{{< /admonition >}}

### 1. 使用系统代理

> 在你的代理软件中开启全局模式(系统代理)

**以v2ray为例:**

```code
windows: v2rayN => 在Http代理中选择全局模式开启后图标为红色

mac: v2rayU => 点击v2rayU图标，选择全局模式

```

现在去刷新需要翻译的网页，然后右键翻译就可以正常使用了, 但是这样的话，你的所有软件都会走代理，这样会导致你的代理软件流量占用过大，并且还有可能会导致无法正常使用其他软件或网站，所以<span style="color:red">**这种方法不推荐**</span>。

### 2. 将API加入代理，<span style="color:red">强烈推荐</span>（作者使用方案）

最近新发现的一个方法，可以将谷歌浏览器内置翻译的API加入代理，这样就可以不用开启全局代理了。

**以SwitchyOmega插件为例:**

可以将下面的URL规则添加到代理切换规则中，例如我是这样设置的：

![1665639904655.png](https://a.xuewuzhibu.cn/1/6347a5e9153e2-1.png)

这里更具你在SwitchyOmega中的设置的情景模式来选择，我选择的是`V2ray`, 因为为了便于分辨我在配置SwitchyOmega时，将情景命名为了`V2ray`。

```code
*.translate.googleapis.com
```

修改完成后记得点击左下角的应用选项按钮，然后刷新需要翻译的网页，然后右键翻译就可以正常使用了。

### 3.修改hosts文件

> 通过修改hosts文件，将谷歌翻译的域名指向国内的服务器，这样就可以正常使用了。

#### mac下修改hosts文件

```bash
sudo vim /etc/hosts
```

输入开机密码后，会在vim中打开hosts文件，输入键盘上的`i`键就会进入编辑模式，然后在文件末尾添加以下内容:

```code
# google translate
203.208.40.66 translate.google.com
# google translate api
203.208.40.66 translate.googleapis.com
```

添加完后，按下键盘上的`esc`键，然后输入`:wq`(英文输入法状态下的冒号)保存退出。

查看是否保存成功，可以使用`cat /etc/hosts`命令查看hosts文件内容，如果有刚才添加的内容，就说明保存成功了。

为了保证修改的hosts文件生效，执行以下命令刷新DNS缓存:

```bash
sudo killall -HUP mDNSResponder
```

接着执行`ping`命令查看是否修改成功:

```bash
ping translate.google.com
```

如果和下图一样，就说明修改成功了。

![ping](https://a.xuewuzhibu.cn/1/633909a456bef-1.png)

重启浏览器，然后再去翻译就可以正常使用了。

#### windows下修改hosts文件

> windows下修改hosts文件的方法和mac下的方法类似。

打开`C:\Windows\System32\drivers\etc`目录，找到`hosts`文件，选择`记事本`打开，然后在文件末尾添加以下内容:

```code
# google translate
203.208.40.66 translate.google.com
# google translate api
203.208.40.66 translate.googleapis.com
```

{{< admonition tip "提示" >}}

- 如果遇到无法保存的情况，可以尝试使用管理员身份运行记事本，然后再打开hosts文件。
- 若还是无法保存，可以参考[这篇文章](https://juejin.cn/post/6963514594245476393)，或者自行百度解决方法。

{{< /admonition >}}

保存退出，然后刷新DNS缓存:

```bash
ipconfig /flushdns
```

打开`cmd`命令行工具，执行`ping`命令查看是否修改成功:

```bash
ping translate.google.com
```

如果可以`ping`通，并且`ip`为：`203.208.40.66`，就说明修改成功了。

重启浏览器，然后再去翻译就可以正常使用了。

**如果没有看懂上面的步骤，可以在评论区留言，我会尽快回复。**

