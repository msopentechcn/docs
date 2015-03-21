使用Git发布应用到Azure Website
----------------------------

##第一步：安装git
不同的操作系统安装git的方式不同，请参考[http://git-scm.com/book/en/Getting-Started-Installing-Git](http://git-scm.com/book/en/Getting-Started-Installing-Git)

##第二步：建立本地代码仓库
实施以下步骤来创建新的Git代码仓库：

1. 建立名称为**MyGitRepository**的目录，用于存放你的git repository和website文件

2. 打开命令行工具，如GitBash (Windows) 或者Bash (Unix Shell). 在OS X系统中你可以使用Terminal应用程序来访问命令行.

3. 在命令行中，进入**MyGitRepository**所在目录.

	cd MyGitRepository

4. 使用以下命令初始化一个新的Git代码仓库:

	git init

这将建立一个空的Git代码仓库。

##第三步：建立web页面
1. Azure Websites支持多种编程语言. 在本例中，我们采用静态.html文件。更多website支持语言的信息，请访问[Azure Developer Center](http://azure.microsoft.com/develop/overview/).

2. 使用文本编辑器，在Git仓库的根目录下，创建index.html，并编辑内容为如下，保存文件后退出：

	Hello Git!

3. 在命令行中，确认工作在Git仓库的根目录，并运行以下命令将index.html添加到代码仓库中：

	git add index.html 

4. 下一步，提交对代码仓库进行的修改：

	git commit -m "Adding index.html to the repository"

你会看到类似如下输出：

	[master (root-commit) 369a79c] Adding index.html to the repository
 	1 file changed, 1 insertion(+)
 	create mode 100644 index.html

##第四步：启用Website代码仓库

实施以下步骤来启用你的website的代码仓库:

1. 登录到**Azure portal**.

2. 点击**NEW**按钮新建一个你想启用Git代码仓库的website.

3. 等到website创建完毕，选择website:   
![](https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/20150225114757/includes/publishing-with-git/git-select-website.png)

4. 选择**DASHBOARD**这个tab页.

5. 在**quick glance**小节中, 选择**Set up deployment from source control**. 下面的**SET UP DEPLOYMENT**对话框出现：
![](https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/20150225114757/includes/publishing-with-git/git-whereisyoursourcecode.png)


6. 选择**Local Git**, 点击**Next**.

7. 如果这是你第一次在Azure上设置代码仓库，你需要为之创建一个访问凭据，这个访问凭据用来登录和推送变更.
![](https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/20150225114757/includes/publishing-with-git/git_credentials.png)

8. 很快，你的代码仓库就可以使用了.
![](https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/20150225114757/includes/publishing-with-git/git-instructions.png)

##第五步：部署你的应用

以下步骤将本地文件推送到Azure,如果之前没有设置好访问凭据，你需要回到**DASHBOARD** tab页，点击Reset your deployment credentials**重新设置访问凭据.

1. 使用命令行工具,确认你在本地Git仓库的根目录，目录下含有刚才创建的index.html文件.

2. 复制前面步骤中portal返回的git remote add命令，类似以下:

	git remote add azure https://username@needsmoregit.scm.azurewebsites.net:443/NeedsMoreGit.git

3. 使用下列命令将本地代码仓库内容推送到Azure:

	git push azure master	

 期间你将被要求输入口令，这是输入之前设置的或者是重置的凭据即可，将得到类似以下输出:

	Counting objects: 6, done.
	Compressing objects: 100% (2/2), done.
	Writing objects: 100% (6/6), 486 bytes, done.
	Total 6 (delta 0), reused 0 (delta 0)
	remote: New deployment received.
	remote: Updating branch 'master'.
	remote: Preparing deployment for commit id '369a79c929'.
	remote: Preparing files for deployment.
	remote: Deployment successful.
	To https://username@needsmoregit.scm.azurewebsites.net:443/NeedsMoreGit.git
	* [new branch]      master -> master

4. 在portal上, 点击底部的**BROWSE**链接来验证index.html是否被部署成功，成功后一个带有'Hello Git!'信息的页面将出现.
![](https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/20150225114757/includes/publishing-with-git/git-hello-git.png)

5. 使用文本编辑器，将index.html文件中的内容修改为 'Yay!', 保存.

6. 使用下列命令提交更改并推送的远程代码仓库:

    git add index.html
	git commit -m "Celebration"
    git push azure master

7. 当**push**命令完成后，刷新浏览器页面，应该能够看到内容更新：  
![](https://acomdpsstorage.blob.core.windows.net/dpsmedia-prod/azure.microsoft.com/en-us/documentation/articles/web-sites-publish-source-control/20150225114757/includes/publishing-with-git/git-yay.png)

