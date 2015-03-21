安装Azure Toolkit for Eclipse
--------------------------------

##前置条件
* Eclipse IDE for Java EE Developers, Indigo或更新的版本。可通过[http://www.eclipse.org/downloads/](http://www.eclipse.org/downloads/)下载
* JDK v1.6+
* 操作系统 - 目前支持：
	* Windows 8.1
	* Windows 8
	* Windows 7
	* Windows Server 2012
	* Windows Server 2008

* Azure SDK 2.5+， 可通过[http://go.microsoft.com/fwlink/?LinkID=252838](http://go.microsoft.com/fwlink/?LinkID=252838)下载

> Azure SDK只需要在Windows平台上安装

## 安装Azure Toolkit for Eclipse
1. 启动Eclipse
2. 点击**Help**, 然后点击**Install New Software**                                         
![](https://i-msdn.sec.s-msft.com/dynimg/IC590123.png)


3. 在**Available Software**对话框中, 在**Work with**文本框中输入：http://dl.msopentech.com/eclipse
4. 在**Name**面板, 选择**Azure Toolkit for Eclipse**, 不勾选**Contact all update sites during install to find required software**. 如图:                                            
![](https://i-msdn.sec.s-msft.com/dynimg/IC719482.png)


5. 点击**Next**. (If you experience unusual delays when installing the toolkit, ensure that Contact all update sites during install to find required software is unchecked.)
6. 在**Install Details**对话框中，点击**Next**.
7. 在**Review Licenses**对话框中, 接受所有许可证选项
8. 如果提示restart Eclipse to complete installation, 点击**Restart Now**.

>更多详细内容，请参考： [https://msdn.microsoft.com/library/azure/hh694271.aspx](https://msdn.microsoft.com/library/azure/hh694271.aspx)


在Azure上用Eclipse开发你的Hello World程序
--------------------------------------------

##建立Hello world应用程序

1. 启动Eclipse. 在顶部菜单中选择File -> New -> Dynamic Web Project. 在此课程中，项目命名为**MyHelloWorld**. 如下图所示:      
![](https://i-msdn.sec.s-msft.com/dynimg/IC589576.png)

2. 在Eclipse’s Project Explorer视图中, 展开**MyHelloWorld**. 右键点击**WebContent**, 点击**New**, 点击**JSP File**. 
3. 在New JSP File对话框中, 将文件命名为**index.jsp**. 保持父目录为**MyHelloWorld/WebContent**, 如图所示:             
![](https://i-msdn.sec.s-msft.com/dynimg/IC659262.png)



4. 在**Select JSP Template**对话框中, 选择**New JSP File (html)**，点击**Finish**.
当index.jsp在Eclipse中打开后, 将如下代码替换掉原文件<body>标签中的内容,保存index.jsp:
   
`
	<body>
		<b><% out.println("Hello World!"); %></b>
	</body>
`

##在Azure上快速部署你的应用

1. 在Eclipse的Project Explorer中, 点击**MyHelloWorld**.

2. 在Eclipse工具栏, 点击**Publish to Azure Cloud**按钮, 将应用发布到Azure云.

3. 如果这是第一次部署，一个Azure部署项目会被自动创建. 同时你会看到如下提示, 列出将被自动部署的JDK和应用服务器版本,点击**OK**确认:
![](https://i-msdn.sec.s-msft.com/dynimg/IC789598.png)


4. 在发布之前，首先访问[https://manage.windowsazure.cn/publishsettings/index?client=xplat](https://manage.windowsazure.cn/publishsettings/index?client=xplat)，下载发布配置文件到本地，访问上述地址时，需要输入您的Azure帐户的用户名和密码完成认证.

5. 点击**Browse**,在本地目录中找到刚下载的发布配置文件：      
![](https://i-msdn.sec.s-msft.com/dynimg/IC644267.png)

6. 导入发布配置文件成功后，选择发布选项，新建或者重用账号中的存储账号和云服务名称，并注意勾选"Overwrite previous deployment"避免部署错误：   
![](https://i-msdn.sec.s-msft.com/dynimg/IC719488.png)


7. 点击**Publish**发布到Staging环境. 在**Azure Activity Log**中将显示发布状态，如果是第一次部署，发布过程大约会持续几分钟到十几分钟.
![](https://i-msdn.sec.s-msft.com/dynimg/IC719489.png)

8. 发布成功后，状态如下，可点击**Published**直接打开刚部署好的web应用：
![](https://i-msdn.sec.s-msft.com/dynimg/IC719490.png)

> 注意，因为在**Target environment**中选择的是Staging，表示此网站非生产环境，因此DNS名称为http://<guid>.chinacloudapp.cn，比如http://72d5eb5875234b7ca8c7f74c80a2a1f1.chinacloudapp.cn/MyHelloWorld, 如果是选择**Production**生产环境,则DNS名称为cloud service的名称。
