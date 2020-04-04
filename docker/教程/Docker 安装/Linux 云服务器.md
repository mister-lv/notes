# Linux 云服务器

自己安装服务器还是麻烦了些，现在一般都推荐大家使用云服务器，比较方便，价格也不贵。

目前市场上的云服务器很多，这边比较下腾讯云跟[阿里云](https://www.runoob.com/linux/linux-cloud-server.html#ali)的服务器优惠活动，现在看来腾讯云性价比会高一些。

------

## 腾讯云

年末腾讯云活动已开始，以下几款性价比非常高，有几款是需要抢购的，大家看好时间基本能拿到。

- 1、**1核2G** 99/年，可以用来学习，Linux 知识对技术人员的成才非常重要。
- 2、**2核4G** 488/年。
- 3、另外还有香港的服务器，如果做网站不想去备案，可以考虑，香港速度还是很快的。

每个时间点都有不同的配置跟价格，具体信息，可以点击下面的图片：

[![img](https://www.runoob.com/wp-content/uploads/2019/11/398567A5-9762-4DFF-9D70-DBBFB4AFED6F.jpg)](https://url.cn/5752aIh)

另外企业用户还有更高配置的，价格也很实惠：

[![img](https://www.runoob.com/wp-content/uploads/2019/11/CCFB929C-A3B8-48E8-9F06-276093E45648.jpg)](https://url.cn/5752aIh)

------

## 阿里云

阿里也有一些活动，**不分新老用户，可以领红包参与满减活动，续费也有专门的优惠券**，有需求的也可以关注下。

具体信息，可以点击下面的图片。

**注意**：阿里云**突发性能型的服务器**真的只能自己学习用，如果要用对外提供服务要慎重选择，因为它性能瓶颈限制很大，不过价格便宜就是了。

[![img](https://www.runoob.com/wp-content/uploads/2019/11/B015E281-5E86-406B-A7C8-7BA6E904B6F4.jpg)](https://www.aliyun.com/minisite/goods?userCode=i5mn5r7m&share_source=copy_link)

5 折活动页：

[![img](https://www.runoob.com/wp-content/uploads/2019/11/FD5CE717-3B48-4433-8ADD-20A3D21BC0BC.jpg)](https://www.aliyun.com/minisite/goods?userCode=i5mn5r7m&share_source=copy_link)

------

## 腾讯云服务器使用

本章节以腾讯云服务器为例。

**1、首先点击下图购买（更多服务器的配置信息见下文）：**

[![img](https://www.runoob.com/wp-content/uploads/2019/11/AE3CD782-2C0D-4EB1-9170-437A2B83709F.jpg)](https://url.cn/5752aIh)

**2、登陆腾讯云控制台，查看已购买的服务器：**

![img](https://www.runoob.com/wp-content/uploads/2019/11/812CFA9E-41F6-4EA2-8044-9FBCAB9C0AAE.jpg)

**3、在使用腾讯云服务器前，我们需要先创建一个 SSH 密钥，点击左侧的 \**SSH 密钥\** （使用密钥登录比密码更安全）：**

![img](https://www.runoob.com/wp-content/uploads/2019/11/018E95B9-756E-4B6C-A0A2-CED21B42F25A.jpg)

输入密钥名称，然后点击确定，就会自动生成一个密钥，密钥会自动下载到本地，请保存好下载的密钥，密钥文件名就是你输入的密钥名称。

**4、接着我们勾选已经创建的密钥，点击 \**绑定/解绑实例\** 按钮，弹窗中会出现我们的 ECS 服务器，将其绑定到这个密钥即可：**

![img](https://www.runoob.com/wp-content/uploads/2019/11/963AF776-FE8C-4340-A426-870D962BDC93.jpg)

**5、返回实例列表，点击实例右侧的 \**登录\** 按钮，弹窗中点击立即登录，这是会弹出一个新的浏览器窗口，我们选择密钥登录，密钥文件就是在第三个步骤创建的：**

![img](https://www.runoob.com/wp-content/uploads/2019/11/A23D733A-DA1B-42C9-91E8-12FB84A68400.jpg)

![img](https://www.runoob.com/wp-content/uploads/2019/11/7603BDAC-3103-4379-B0BE-8E669E069AF4.jpg)

![img](https://www.runoob.com/wp-content/uploads/2019/11/D1D8FA9C-4ECD-42A4-B24B-70520F854858.jpg)

当然你可以选择第三方客户端登录（如：SecureCRT），用户名为 ubuntu，其他系统估计略有不同，然后导入对应的 key 即可。