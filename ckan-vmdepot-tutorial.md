#使用VMDepot镜像在Azure上快速部署CKAN#

本指南展示了如何通过VMDepot镜像快速进行CKAN部署

###前提条件##
您至少需要一个可用的微软中国Azure公有云在中国的账户


### 在Azure管理控制台中，导入CKAN镜像到本地帐户 ##
打开Azure控制台：[https://manage.windowsazure.cn](https://manage.windowsazure.cn)
选择virutal machines -> images -> Browse VM Depot:
![](aaaa1.png)

在Ubuntu类别下找到CKAN镜像，这是已经发布在VMdepot上一键部署镜像：
![](aaaa2.png)

下面需要将此镜像拷贝到的用户存储账户，可以选择已有的存储帐户，也可新建：
![](aaaa3.png)

拷贝过程将花费几分钟的时间：
![](aaaa4.png)

拷贝完成后，本地CKAN镜像的状态是Pending registration，点击Register注册：
![](aaaa6.png)

填写注册镜像名称：
![](aaaa7.png)

镜像状态变为Available，至此，CKAN镜像已经准备完毕：
![](aaaa8.png)

### 使用本地CKAN镜像创建虚机 ##
在Azure管理控制台中，选择Virtual Machines -> Create a Virtual Machine
![](aaaa9.png)

选择From Gallery：
![](aaaa10.png)

在My Images类别，找到我们刚刚注册的CKAN镜像，点击下一步：
![](aaaa11.png)

填写虚机名称，用户名和认证方式，注意这里的默认用户名为azureuser,点击下一步：
![](aaaa12.png)

创建Cloud Service，在本例中，服务地址为mytestckan.chinacloudapp.cn,
注意需要打开至少三个tcp端口，分别为22，80，443，点击下一步：
![](aaaa13.png)

确认VM Agent已经安装，点击下一步：
![](aaaa14.png)

等待直至虚拟机状态变为Running，至此CKAN镜像部署完毕：
![](aaaa15.png)

在浏览器中输入网址：http://mytestckan.chinacloudapp.cn,可以看到CKAN门户已经可以访问了：
![](aaaa16.png)

### 安装后的配置（必须完成） ##
由于CKAN的特殊要求，每一个新部署的镜像需要调整ckan.site_url参数才能正常工作，
下面演示如何修改此参数：
Windows用户可通过安装ssh客户端，如PuTTY，连接到新建的CKAN虚机；Linux和Mac用户可直接通过ssh命令连接：
![](aaaa18.png)
本例中我们采用用户名密码认证方式登录mytestckan.chinacloudapp.cn

运行以下命令,运行前将YOUR-CKAN-DOMAIN-NAME替换为您实际的网站域名，在本例中为mytestckan.chinacloudapp.cn
sudo sed -i 's/ckanimage.chinacloudapp.cn/YOUR-CKAN-DOMAIN-NAME/' /etc/ckan/default/production.ini

检查命令是否生效：
cat /etc/ckan/default/production.ini |grep ckan.site_url
![](aaaa19.png)
注意，您也许会为您的CKAN门户网站申请不同的域名，请将site_url替换为实际用户访问使用的域名。

重启apache和nginx服务：
sudo service apache2 restart && sudo service nginx restart
![](aaaa20.png)

至此，您的CKAN已经配置完成，可以正常使用了。


### 创建您的第一个数据集 ##
以admin身份登录CKAN门户网站，默认密码是admin，登录后请立即更改密码：
![](aaaa16.png)

点击“数据集” -> 增加数据集
![](aaaa17.png)

输入数据集名称，点击下一步：
![](aaaa21.png)

点击“上传”：
![](aaaa22.png)

选择本地Excel文档：
![](aaaa23.png)

格式选择为“xls”，点击下一步：
![](aaaa24.png)

可以选择补充数据集的额外信息，点击“完成”：
![](aaaa25.png)

至此，CKAN将自动导入Excel表格，并同时生成OData格式数据访问API供应用程序访问。
![](aaaa26.png)

选择“浏览”->“预览”可以查看导入的数据：
![](aaaa27.png)
![](aaaa28.png)

数据导入完成后，可在CKAN门户首页看到新增的数据集：
![](aaaa29.png)


### 定制您的CKAN ##
您也许希望改变此镜像默认的配置如网站标题，介绍文字等，
可以用admin登录后，点击首页右上角“系统管理员设置”，
选择“配置”选项卡：
![](aaaa30.png)
在这里，您可以对网站风格和文字进行定制。
