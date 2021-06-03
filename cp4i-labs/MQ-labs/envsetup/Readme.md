# Setup Messaging PoT - MQ on CP4I lab environment

[Return to main lab page](../index.md)

## Featuring: 
- Creating VDIs
- Downloading lab artifacts from github
- IBMers creating new namespace
 
 ---

# Table of Contents 
- [1. Setup environmment for CP4I PoT](#setup)
	+ [1.1 Connect to your VDI](#connect)
	+ [1.2 Connect to the Red Hat OpenShift cluster](#ocp)
	+ [1.3 Download artifacts for MQ on CP4I PoT](#download)
- [2. Create Project (namespace) for your lab assets](#namespace)
	+ [2.1 Create entitlement secret for your namespace](#entitlement_secret)

---

<a name="setup"></a>
# 1. Setup environment for CP4I PoT 

<a name="connect"></a>
## 1.1 Connect to your Virtual Desktop Image 

1. As a CP4I PoT attendee you should have received an email with instructions to connect to a Virtual Desktop Instance (VDI) which you will use to execute the labs in this PoT. The email provided the details for connecting to your VDI. 

	![alt text][pic0]
	
1. Copy the password by clicking the copy icon. Then click "Open your IBM Cloud Environment". 

	![alt text][pic1]
	
1. The VNC window appears. Click connect. 

	![alt text][pic2]
	
4. Enter the password included in the details then click *Send Password*.

	![alt text][pic3]
			
5. The Linux desktop appears. You are now logged in as *student*. You'll notice the toolbar on the left. This is used to control the VNC settings. You will use it mostly for copy/paste from outside the VNC desktop. You can hide the toolbar by clicking the arrow on the side of the toolbar.
	
	![alt text][pic4]

<a name="ocp"></a>
## 1.2 Connect to the Red Hat OpenShift cluster 

Your attendee email also included a URL to connect to the Red Hat OpenShift cluster where you will execute the labs. The name of the cluster will vary depending on which one has been reserved. The example below shows the Obi-Wan cluster. 

1. From your email, copy the URL for the OCP Console.

	![alt text][pic5]

1. Paste the URL onto the clipboard of the VDI. Then copy/paste the URL into a browser tab and hit enter. 

	![alt text][pic6]
	
1. You are taken to the *Overview* page on the OCP console.

	![alt text][pic7]	

You will be in your assigned namespace.

**NOTE** "IBM Only - If you are running the lab in your own ROKS cluster, you may create a new project (namespace). [Click here to create your namespace](#namespace)"  

<a name="download"></a>
## 1.3 Download artifacts for MQ on CP4I PoT 

You should be logged on your VDI as *student*. 

1. Open a Firefox browser tab and navigate to [Github MQonCP4i](https://github.com/ibm-cloudintegration/mqoncp4i).

	![alt text][pic8]
		
2. Click *Code* and select *Download zip*.
	
	![alt text][pic9]
	

3. Click *Save file* radio button then click *OK*.
	
	![alt text][pic10]
	
	
4. Open a terminal window by double-clicking the icon on the desktop.
	
	![alt text][pic11]
	
	
5. Enter the following command to see the zip file you just downloaded.

	```text
	cd Downloads
	```
	
6. Enter the following command to unzip the downloaded file:

	```sh
	unzip mqoncp4i-main.zip
	```

	![alt text][pic12]	
	
	
7. Move the unzipped directory to your home directory with the following command:
	
	```sh
	cd mqoncp4i-main
	```
	
	```sh
	mv MQonCP4I/ ~/
	```
	
	![alt text][pic13]	
		
	This will create the directory **/home/student/MQonCP4I**.

	![alt text][pic14]	
	
	
Great! You are now ready to start working with MQ in the labs. If running a PoT, attendees are now ready to start Lab 1 where they will create queue managers using their assigned IDs.


[Continue to Lab 1](mq_cp4i_pot_lab1.html)

[Return MQ CP4I Menu](mq_cp4i_pot_overview.html)

<a name="namespace"></a>
# 2. Create Project (namespace) for your lab assets 

1. Click *Projects* then click *Create project*.

	![alt text][pic15]
	
1. Your attendee email also included a student number 01 - 99. This will be your student ID referenced in the lab guides. Append this number to "mq" to create your project name. Project is the term for namespace in OpenShift. This is used to keep your assets separate from the other students.  

	Enter the name of your project **mqxx** in the name field and click *Create*. **mq00** is reserved for the instructor and has been used to document the lab. 

	![alt text][pic16]


<a name="entitlement_secret"></a>	
## 2.1 Create entitlement secret for your namespace 

1. In OCP console, click the drop-down next to your username and select "Copy Login Command".

	![alt text][pic15]
	
1. A new browser tab opens. Click the *Display Token* hyperlink.

	![alt text][pic16]
	
1. Copy the command under "Log in with this token".

	![alt text][pic17]
	
1. Open a terminal window and paste the command into the terminal and hit enter which logs you into the cluster. Enter the following command to change to your namespace. Make sure to substitute 00 with your student number.

	```sh
	oc project mq00
	```
	
	![alt text][pic18]
	
	**NOTE** "An entitlement key will be provided to you as part of the PoT. If you already have an entitlement key you may use it."	
		
1. Enter the following command to create the secret replacing "**your-entitlement-key-goes-here**" with your real entitlement key:
	
	```sh
	oc create secret docker-registry ibm-entitlement-key --docker-username=cp --docker-password=**your-entitlement-key-goes-here** --docker-server=cp.icr.io --namespace=mq00
	```
	
1. You can now login to Docker with the following command replacing "**your-entitlement-key-goes-here**" with your entitlement key.

	```sh
	docker login cp.icr.io --username cp --password **your-entitlement-key-goes-here**
	```
![alt text][pic19]	

[Return to lab guide to continue](#download)


[pic0]: images/image101.png
[pic1]: images/image102.png
[pic2]: images/image17o.png
[pic3]: images/image18o.png
[pic4]: images/image19o.png
[pic5]: images/image103.png
[pic6]: images/image104.png
[pic7]: images/image105.png
[pic8]: images/image108.png
[pic9]: images/image109.png
[pic10]: images/image110.png
[pic11]: images/image111.png
[pic12]: images/image112a.png
[pic13]: images/image113a.png
[pic14]: images/image114a.png
[pic15]: images/image106.png
[pic16]: images/image107.png
[pic17]: images/image115.png
[pic18]: images/image116.png
[pic19]: images/image117.png
[pic20]: images/image118.png
[pic21]: images/image119.png



