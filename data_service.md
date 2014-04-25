---
title: Using a Pivotal HD Data Service
---

#Creating Pivotal HD Cluster Instances

After Pivotal HD Data Services is installed you can deploy instances of the Pivotal HD cluster that are defined in the Service Plan. The plan defines the maximum number of cluster instances you can create as well as the number of pre-created cluster instances that are available.

To create an instance of a Pivotal HD Service Plan: 

1. Log in to the Pivotal CF **Developer Console**.  

2. Click **Add Service**.

	The Services Marketplace screen displays.

3. Select the Pivotal HD Service.

4. ?? 

For more information, see [Getting Started with the Developer Console](http://docs.gopivotal.com/pivotalcf/console/pcf_console.html).

#Accessing Pivotal HD Cluster Instance Machines

If you need to access a virtual machine in your Pivotal HD cluster or if you need to access the virtual machine that runs Pivotal HD Data Services, you can use Pivotal CF Ops Manager to display the necessary credentials and URLs. Ops Manager also displays status of each virtual machine and enables you to download its log files. 

##To view the status of the virtual machines in a cluster:

1. Use a Web browser to open the Pivotal CF Ops Manager application. 

2. Click the Pivotal Elastic Runtime tile.  

3. Click the **Status** tab.

	A table of with a row for each virtual machines displays. Each row describes the status of the virtual machine. 

##To find the credentials and URLS:

1. Use a Web browser to open the Pivotal CF Ops Manager application. 

2. Click the Pivotal Elastic Runtime tile.  

3. Click the **Credentials** tab.

	A table of credentials for various virtual machines displays. Locate the row for the machine that you want to access.

##To access log files for virtual machines:

1. Use a Web browser to open the Pivotal CF Ops Manager application. 

2. Click the Pivotal Elastic Runtime tile.  

3. Click the **Status** tab.

	A table of credentials for various virtual machines displays. Locate the row for the machine that you want to access.

4. Click the download icon in the **Logs** column to download the logs.

	Ops Manager creates a zip file containing the logs.
	
5. Click the **Logs** tab.

	A table of downloaded log files displays. 

6. Click the link for the zip file containing the logs you are interested in.

	A zip file containing the logs downloads to your computer. 

#Binding an Application to a Pivotal HD Cluster Instances

The process of binding an application to a service automatically populates a set of environment variables. These variables define credentials, URLs for services and other configurations. When you use Pivotal CF to bind an application to a Pivotal HD service, these variables are populated automatically. When the application moves into a production phase, you can easily bind the application to an external instance of Pivotal HD by setting new values for these variables. Pivotal CF can also automatically create these bindings. See [Bind a Service](http://docs.gopivotal.com/pivotalcf/devguide/services/bind-service.html).

??insert list of env vars

1. Log in to the **Developer Console**. 

2. Select your Pivotal HD Cluster service.

3. Click **Bind**



