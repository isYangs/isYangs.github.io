# 使用本站提供的图床服务


## 写在前面

最开始我也是使用网上的免费图床，但是用了以后发现了很多问题，比如：对免费用户不友好，有限的空间，上传大小限制，而且因为是免费用户的原因图床CDN的速度也很慢，并且不能保证图片是否可以长期存储。通过上述一系列的问题，于是我决定自己搭建一个图床，并且提供给免费大家使用。

## 关于图床

### 提供服务的厂商

- 图床站点服务器：阿里云服务器提供网站服务。
- 图像存储：[又拍云](https://console.upyun.com/register/?invite=XRY707MJ6)云存储(USS)提供图像存储服务。
- 图床程序：采用 [LskyPro付费版](https://www.lsky.pro)

## 图床使用

前往 [注册](https://i.xuewuzhibu.cn/register)或 [登录](https://i.xuewuzhibu.cn/login) 图传现阶段只提供给免费用户使用，默认注册赠送200GB的存储空间。

{{< admonition warning "使用须知" >}}

* 因为图床成本较高，所以后期会添加增值服务，请多包涵
* 如果你想要白嫖😉，现在 [注册](https://i.xuewuzhibu.cn/register)账号后即可赠送200GB的永久存储空间
* 虽然后期会开启增值服务，但是可以保证免费用户的速度依旧是最快的，增值只针对需要大容量存储空间的用户
* 因为图床采用 [又拍云](https://console.upyun.com/register/?invite=XRY707MJ6)云存储(USS)，所以务必在本地做好备份，请谨记数据大于一切

{{< /admonition >}}

### 上传图片
{{< admonition info "默认用户组上传规则" >}}

* 图片大小不超过50MB
* 并发上传不超过5张
* 每分钟可上传500张
* 每小时可上传1000张
* 具体请在 [图床仪表盘](https://i.xuewuzhibu.cn/user/dashboard) 查看

{{< /admonition >}}

上传图片可以通过以下两种方式：

第一种：直接在上传页面选择本地图片上传，上传后会自动生成一个图片链接，可以直接复制使用。

第二种：通过API上传图片，[查看API文档](https://i.xuewuzhibu.cn/page/api-docs.html)


API地址为：<https://i.xuewuzhibu.cn/api/v1/upload>


首先需要在图床后台申请`Token`

{{< image src="https://a.xuewuzhibu.cn/1/63049b56d0566-1.png" caption="申请Token" >}}
{{< image src="https://a.xuewuzhibu.cn/1/63049b56f088c-1.png" caption="创建Token" >}}
{{< image src="https://a.xuewuzhibu.cn/1/63049b550782e-1.png" caption="获取ToKen" >}}

{{< admonition tip "提示" >}}
使用红色「*」符号标注，则表示为必传项。
{{< /admonition >}}
然后在请求头(Header)中添加如下参数：

| 参数 | 类型 | 描述 |
| ---: | :---: | :--- |
|`* Accept` | `String` | 必须设置为 `application/json` |
| `* Authorization` | `String` | `Bearer` 你申请的Token(注意中间的空格) |
| `* Content-Type` | `String` | 需要设置为 `application/json` |

{{< image src="https://a.xuewuzhibu.cn/1/63049b54e9686-1.png" caption="请求头参数" >}}

然后在请求体(Body)中添加如下参数：
| 参数 | 类型 | 描述 |
| :-: | :--: | :--: |
| `* file` | `file` | 图片文件 |

{{< image src="https://a.xuewuzhibu.cn/1/63049b543c9e9-1.png" caption="请求体参数" >}}

最后就可以在图床后台查看到图片

{{< image src="https://a.xuewuzhibu.cn/1/63049b5474b35-1.png" caption="后台图片" >}}

