#Quickly Deploying CKAN using VM Depot#

The latest release of CKAN VM Depot provides additional Chinese support, and incorporates common plug-ins and best practice configuration parameters, which to a great extent streamlines the otherwise complicated CKAN deployment. This guide explains how to quickly deploy CKAN using VM Depot.

###Prerequisites##
You need an available Microsoft Azure public cloud account.


### Importing a CKAN Image to Your Local Account with the Azure Console ##

Access the Azure Console at https://manage.windowsazure.cn and choose **Virtual Machines** -> **Images** -> **Browse VM Depot**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/1.PNG)

Locate the CKAN image, a one-touch deployment image released on VM Depot, under **UBUNTU**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/2.PNG)

You have options to copy the image to an existing storage account or create a new one:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/3.PNG)

The copying process takes a few minutes:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/4.PNG)

The local CKAN image turns to the **Pending registration** state after the copying is completed. Click **Register**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/6.PNG)

Enter a name for the registration:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/7.PNG)

The image turns **Available**. Now, you get the CKAN image ready:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/8.PNG)

### Creating a VM using the Local CKAN Image ##
Choose **Virtual Machines** -> **Create a Virtual Machine** from the Azure Console.
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/9.PNG)

Select **From Gallery**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/10.PNG)

Locate the CKAN image you just registered under **MY IMAGES**, and click **Next**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/11.PNG)

Enter the VM name, user name (**azureuser** by default), and authentication mode. Click **Next**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/12.PNG)

Create a cloud service, with the DNS address as **mytestckan.chinacloudapp.cn** in this example. 
Note that you need to enable at least three TCP ports (22, 80, and 443). Click **Next**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/13.PNG)

Click **Next** after confirming that the VM Agent has been installed:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/14.PNG)

Wait until the VM turns Running. Now, you have completed CKAN image deployment:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/15.PNG)

Type [http://mytestckan.chinacloudapp.cn](http://mytestckan.chinacloudapp.cn) in your browser’s address bar, and you can access the CKAN:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/16.PNG)

### Configurations After Installation (Mandatory) ##
For a deployed CKAN image to work, you need to change parameter **ckan.site_url** as follows:

Windows users could install the SSH client, such as PuTTY, for connecting to the created CKAN VM; Linux and Mac users could directly run an SSH command:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/18.PNG)
In this example, we log on to mytestckan.chinacloudapp.cn through password authentication.

Run the following command by replacing *YOUR-CKAN-DOMAIN-NAME* with your real domain name (mytestckan.chinacloudapp.cn in this example). 
Note that the domain name does not carry the prefix 'http://':

$sudo sed -i 's/ckanimage.chinacloudapp.cn/*YOUR-CKAN-DOMAIN-NAME*/' /etc/ckan/default/production.ini

Check whether the command works:

$cat /etc/ckan/default/production.ini | grep ckan.site_url

![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/19.PNG)
Note: You might have applied for a different domain name for your CKAN. Please replace site_url with the actual domain name accessible by end users.

Restart the apache and nginx services:

$sudo service apache2 restart && sudo service nginx restart

![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/20.PNG)

Now, you have completed configuring the CKAN and are ready to use it.


### Creating Your First Dataset ##
Log on to the CKAN portal as **admin** (default password as **admin**) and change your password immediately after logged on:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/16.PNG)

Choose **Dataset** -> **Add a Dataset**.
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/17.PNG)

Enter a name for the dataset, and then click **Next**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/21.PNG)

Click **Upload**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/22.PNG)

Select a local Excel document:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/23.PNG)

Set the format to **xls**, and click **Next**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/24.PNG)

Here you have options to specify additional information for the dataset. Click **Finish**:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/25.PNG)

Then, CKAN automatically imports the Excel spreadsheet and generates an OData API accessible by applications.
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/26.PNG)

Choose **Browse** -> **Preview** to view the imported data:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/27.PNG)
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/28.PNG)

You will see the created dataset on the CKAN homepage after the importing is completed:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/29.PNG)


### Customizing Your CKAN ##
You may hope to change the default configurations of the image, for example, website title and description. 
To do so, log on as **admin**, click **Administrator settings** button in the upper right corner of the homepage, 
and click the **Configure** tab. Here you can change, for example, the style and description of the website:
![](https://raw.githubusercontent.com/msopentechcn/docs/master/images/30.PNG)