通过Java Azure Storage SDK编写应用程序
-----------------------------------

详见：
[http://azure.microsoft.com/en-us/documentation/articles/storage-java-how-to-use-blob-storage/](http://azure.microsoft.com/en-us/documentation/articles/storage-java-how-to-use-blob-storage/)


##下载Java Azure Storage SDK

1. 使用git客户端下载：

	git clone https://github.com/Azure/azure-storage-java.git


2. 下载完成后，在代码仓库目录有pom.xml，可将此导入到Eclipse工程中.


##在Eclipse中导入下载的项目
file -> import -> Maven -> Existing Maven Projects

选择Microsoft-azure-storage-samples，点击确定导入。


##修改Utilities.java
将35行修改为：

	private static final String accountName = "YOUR-ACCOUNT-NAME";
	private static final String accountKey = "YOUR-ACCOUNT-KEY";
	
	public static final String storageConnectionString = "BlobEndpoint=http://"+accountName+".blob.core.chinacloudapi.cn;"
			+ "QueueEndpoint=http://"+accountName+".queue.core.chinacloudapi.cn;"
			+ "TableEndpoint=http://"+accountName+".table.core.chinacloudapi.cn;"
			+ "AccountName=" + accountName + ";"
			+ "AccountKey=" + accountKey;

 
##运行范例代码

com.microsoft.azure.storage.blob.gettingstarted.BlobBasics

com.microsoft.azure.storage.blob.gettingstarted.QueueBasics

com.microsoft.azure.storage.blob.gettingstarted.TableBasics
