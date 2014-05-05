---
title: Using a Pivotal HD Data Service
---

#Creating Pivotal HD Cluster Instances

After Pivotal HD Data Services is installed you can deploy instances of the Pivotal HD cluster that are defined in the Service Plan. The plan defines the maximum number of cluster instances you can create as well as the number of pre-created cluster instances that are available. You use the Pivotal CF Developer Console to create cluster instances.

**Pivotal CF Developer Console**

![Pivotal CF Developer Console](/images/dev_console_large.png "Pivotal CF Developer Console")

To create an instance of a Pivotal HD Service Plan: 

1. Log in to the **Pivotal CF Developer Console**.  

2. Select your Org from the drop-down list on the left. 

3. Select **Marketplace** from the left navigation menu. 

	The **Services Marketplace** displays.

3. Select **Pivotal HD**.

	The **Pivotal HD Service** page displays.

4. Click **Create a Service**.

	The **Add a new Service Instance** page displays.
	
5. Enter a name for this PHD service instance. 

6. Select a space from the **Add to Space** drop-down list.

7. (Optional) Select an application from the **Bind to App** drop-down list. The drop-down list displays available applications previously configured for this Org and Space. If you do not want to bind an application at this time, select **[do not bind]**.

The PHD service deploys. To see the status of this cluster, select its space from the navigation menu on the left and select the instance from the list that displays. 
	
For more information, see [Getting Started with the Developer Console](http://docs.gopivotal.com/pivotalcf/console/pcf_console.html).

#Accessing Pivotal HD Cluster Instance Machines

If you need to access a virtual machine in your Pivotal HD cluster or if you need to access the virtual machine that runs Pivotal HD Data Services, you can use Pivotal CF Ops Manager to display the necessary credentials and URLs. Ops Manager also displays status of each virtual machine and enables you to download its log files. 

##Viewing the status of the virtual machines in a cluster:

1. Use a Web browser to open the Pivotal CF Ops Manager application. 

2. Click the Pivotal Elastic Runtime tile.  

3. Click the **Status** tab.

	A table of with a row for each virtual machines displays. Each row describes the status of the virtual machine. 

##Locating credentials and URLS of virtual machines in a cluster:

1. Use a Web browser to open the Pivotal CF Ops Manager application. 

2. Click the Pivotal Elastic Runtime tile.  

3. Click the **Credentials** tab.

	A table of credentials for various virtual machines displays. Locate the row for the machine that you want to access.

##Accessing log files of virtual machines in a cluster:

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

#Binding an Application to a Pivotal HD Cluster Instance

The process of binding an application to a service automatically populates a set of environment variables. These variables define credentials, URLs for services and other configurations. When you use Pivotal CF to bind an application to a Pivotal HD service, these variables are populated automatically. When the application moves into a production phase, you can easily bind the application to an external instance of Pivotal HD by setting new values for these variables. Pivotal CF can also automatically create these bindings. See [Bind a Service](http://docs.gopivotal.com/pivotalcf/devguide/services/bind-service.html).


??insert list of env vars

1. Log in to the **Developer Console**. 

2. Select your Pivotal HD Cluster service.

3. Click **Bind**

#Using BOSH Client to Examine a PHD Deployment 
   
   You can use the BOSH command line tools to examine a PHD cluster instance.
   
1. Log in to your Cloud Foundry Controller machine ??Dieu to provide name??

2. Run one of the following commands: 

* `bosh deployments`

	Displays a list of deployments.	For example:
		
	<pre class="terminal">
	   $ bosh deployments
	   +---------------------------------+--------------------------------+-------------------------------+
	   | Name                            | Release(s)                     | Stemcell(s)                   |
	   +---------------------------------+--------------------------------+-------------------------------+
	   | cf-5f2b8491a89b0598c95c         | cf/169                         | bosh-vsphere-esxi-ubuntu/2366 |
	   |                                 | push-console-release/6         |                               |
	   |                                 | runtime-verification-errands/1 |                               |
	   +---------------------------------+--------------------------------+-------------------------------+
	   | phd-1                           | phd/282                        | bosh-vsphere-esxi-centos/1868 |
	   +---------------------------------+--------------------------------+-------------------------------+
	   | phd-2                           | phd/282                        | bosh-vsphere-esxi-centos/1868 |
	   +---------------------------------+--------------------------------+-------------------------------+
	   | phd-3                           | phd/282                        | bosh-vsphere-esxi-centos/1868 |
	   +---------------------------------+--------------------------------+-------------------------------+
	   | phd-broker-037b5a195ed32bdf4e61 | phd-broker/277                 | bosh-vsphere-esxi-centos/1868 |
	   +---------------------------------+--------------------------------+-------------------------------+
	   Deployments total: 5
   </pre>
	   
* `bosh vms`

	Displays a list of virtual machines in the environment for all deployments. To limit the list to a specific deployment, enter its name as the first argument. For example:
	
	<pre class="terminal">
		$ bosh vms phd-3
		Deployment `phd-3'

		Director task 151

		Task 151 done

		+-------------------+---------+-----------------+-----------+
		| Job/index         | State   | Resource Pool   | IPs       |
		+-------------------+---------+-----------------+-----------+
		| gfxd-locator/0    | running | gfxd-locator    | 10.0.1.29 |
		| namenode/0        | running | namenode        | 10.0.1.27 |
		| phd-slave/0       | running | worker          | 10.0.1.30 |
		| resourcemanager/0 | running | resourcemanager | 10.0.1.28 |
		+-------------------+---------+-----------------+-----------+

		VMs total: 4
	</pre>
	
	You can also add the `--detail` flag to include the names of the each virtual machines.	For example:
	
	<pre class="terminal">
	[root@rock ~]# bosh vms phd-3 --detail
	Deployment `phd-3'

	Director task 152

	Task 152 done

	+-------------------+---------+-----------------+-----------+-----------------------------------------+--------------------------------------+--------------+
	| Job/index         | State   | Resource Pool   | IPs       | CID                                     | Agent ID                             | Resurrection |
	+-------------------+---------+-----------------+-----------+-----------------------------------------+--------------------------------------+--------------+
	| gfxd-locator/0    | running | gfxd-locator    | 10.0.1.29 | vm-e7cacaec-8190-4841-81fb-ae7ca4784ea1 | 4718b1bf-1af7-4fc9-802c-36037f0a30cc | active       |
	| namenode/0        | running | namenode        | 10.0.1.27 | vm-8eac5c1a-de57-414d-a109-c1117eb58cad | 5c45c684-46ac-4f76-a285-e507beeb029b | active       |
	| phd-slave/0       | running | worker          | 10.0.1.30 | vm-889afcd8-02ac-42bf-b848-992716a34cec | 75a00ccd-cad8-45dd-9369-2274e1b4ec01 | active       |
	| resourcemanager/0 | running | resourcemanager | 10.0.1.28 | vm-a64bc3fa-fdd0-40c0-8311-fe854b72ff16 | 3551bb58-e2e1-4bc2-8a7c-c941391f3679 | active       |
	+-------------------+---------+-----------------+-----------+-----------------------------------------+--------------------------------------+--------------+

	VMs total: 4
    
	</pre>
	
#Using SSH into Virtual Machines in the Cluster	

