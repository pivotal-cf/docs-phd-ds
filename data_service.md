---
title: Using a Pivotal HD Data Service
---

#Creating Pivotal HD Cluster Instances

After Pivotal HD Data Services is installed you can deploy instances of the Pivotal HD cluster that are defined in the Service Plan. The plan defines the maximum number of cluster instances you can create as well as the number of pre-created cluster instances that are available. 

You use either the Pivotal CF Developer Console or the Pivotal CF command line to create cluster instances.

##Developer Console

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

**Pivotal CF Developer Console**

![Pivotal CF Developer Console](/images/dev_console_large.png "Pivotal CF Developer Console")
	
For more information, see [Getting Started with the Developer Console](http://docs.gopivotal.com/pivotalcf/console/pcf_console.html).

##Pivotal CF Command Line

To create a Pivotal HD cluster instance:

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`cf target -s <space name>`
		
2. Run the following command:

	`cf create-service p-hd <Service Plan name> <instance name>`
	
	Where:
	
	 * *Service Plan name* is the name of the Service Plan you created previously. See [Creating a Service Plan](service_plans.html).
	 * *instance name* is the name of the instance you are creating. 
	 
	For example:
	
	<pre class="terminal">
	$ cf target -s staging
	API endpoint: https://api.rock.music.cf-app.com (API version: 2.2.0)
	User:         admin
	Org:          pivotalrocks
	Space:        staging
	$ cf create-service p-hd Standard phd1
	Creating service phd1 in org pivotalrocks / space staging as admin...
	OK
    </pre>

3.  

#Deleting Pivotal HD Cluster Instances

After creating a Pivotal HD cluster instance, you can delete the instance.


##Developer Console

1. Log in to the **Pivotal CF Developer Console**.  

2. Select your Org from the drop-down list on the left. 

3. Select the space where your Pivotal HD cluster instance is deployed from the left navigation menu. 

	A list of applications and services instances displays.

3. Locate the row under **Services** that contains the service instance you want to delete and click **Delete**. 

	A confirmation dialog box displays.

##Pivotal CF Command Line

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`cf target -s <space name>`
		
2. Run the following command:

	`cf delete-service <instance name>`
	
	Where *instance name* is the name of the instance you are creating. 
	 
	For example:
	
	<pre class="terminal">
	cf delete-service phd1

	Are you sure you want to delete the service phd1 ? y
	Deleting service phd1 in org pivotalrocks / space staging as admin...
	OK
	
    </pre>

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

##About Bindings and Environment Variables

When you bind an application, a set of environment variables are set that contain URLs, credentials, and other meta-data about the application. 

You can view these variables in two ways:

##Pivotal CF Developer Console

To view the binding variables from the Pivotal CF Developer Console:

1. Log in to the **Pivotal CF Developer Console**.  

2. Select your Org from the drop-down list on the left. 

3. Select the space where your Pivotal HD cluster instance is deployed from the left navigation menu. 

	A list of applications and services instances displays.

4. Now what??

##JSON Display

You can display the binding variables as a JSON document:

1. Open a Web browser and enter a URL constructed as follows:

	`<app name>.<Web Console URL>/env`
	
	For example, the following URL returns the environment variables for the `app-sinatra-services` application. 

	`app-sinatra-services.rock.music.cf-app.com/env`

	The browser displays the following JSON document (formatted for easier reading):

	<pre class="terminal">

	{
	  "p-hd": [
	    {
	      "name": "phd-inst1",
	      "label": "p-hd",
	      "tags": [],
	      "plan": "Standard",
	      "credentials": {
	        "hadoop_username": "u294d1cab32a2454",
	        "hdfs": {
	          "configuration": {
	            "fs.defaultFS": "hdfs://10.0.1.6:8020"
	          },
	          "directory": "/user/u294d1cab32a2454"
	        },
	        "yarn": {
	          "configuration": {
	            "yarn.resourcemanager.address": "10.0.1.7:8032",
	            "mapreduce.framework.name": "yarn",
	            "yarn.resourcemanager.scheduler.address": "10.0.1.7:8030",
	            "mapreduce.job.working.dir": "/user/u294d1cab32a2454/work",
	            "yarn.app.mapreduce.am.staging-dir": "/user/u294d1cab32a2454/staging"
	          }
	        },
	        "hawq": {
	          "uri": "jdbc:postgres://10.0.1.8:5432/default;username=u294d1cab32a2454;password=564a77eb-0aad-4a92-7c83-9b73183e2784"
	        },
	        "gemfirexd": {
	          "uri": "jdbc:gemfirexd://10.0.1.9:1527/user=u294d1cab32a2454;password=6e5e7546-bb92-4d3b-4165-5e5c68fe0e59"
	        }
	      }
	    }
	  ]
	}
</pre>

##Developer Console

1. Log in to the **Developer Console**. 

2. Select your Pivotal HD Cluster service.

3. Select space where the application you want to bind is deployed.

	A list of deployed applications and services displays. 

5. Locate the row containing the application and click the **>** link. 

	A page displays that show the bound services and instances for this application.

6. Click **Bind**

	A list of a available services displays.

7. Click the **Bind** button for the service you want to bind to this application. 

##Pivotal CF Command Line

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`cf target -s <space name>`

3. Run the following command:

	`cf bind-service <application> <service instance name>`

	For example:
	
	<pre class="terminal">
	
	cf bind-service app-sinatra-services phd2
	Binding service phd2 to app app-sinatra-services in org pivotalrocks / space staging as admin...
	OK
	TIP: Use 'cf push' to ensure your env variable changes take effect
</pre>

#Unbinding an Application from a Pivotal HD cluster instance

You can unbind a bound application from a Pivotal HD cluster instance. 

##Developer Console

1. Log in to the **Developer Console**. 

2. Select your Pivotal HD Cluster service.

3. Select space where the application you want to bind is deployed.

	A list of deployed applications and services displays. 

5. Locate the row containing the application and click the **>** link. 

	A page displays that show the bound services and instances for this application.

6. Locate the bound service instance you want to unbind and click **Unbind**.

	A confirmation dialog box displays. 

##Pivotal CF Command Line

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`cf target -s <space name>`

3. Run the following command:

	`cf bind-service <application> <service instance name>`

	For example:
	
	<pre class="terminal">
	
	cf bind-service app-sinatra-services phd2
	Binding service phd2 to app app-sinatra-services in org pivotalrocks / space staging as admin...
	OK
	TIP: Use 'cf push' to ensure your env variable changes take effect
</pre>


#Using BOSH Director to Examine a PHD Deployment 
   
   You can login to the BOSH Director and use the BOSH Command-Line Interface to run diagnostic commands that examine a Pivotal CF installation, including your Pivotal HD cluster instances.  The BOSH Director runs on the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.
   
   See [Troubleshooting with the BOSH CLI](http://docs.gopivotal.com/pivotalcf/customizing/trouble-advanced.html). 
      
1. Log in to the BOSH Director.

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
	
* `cf services`

	Displays a list of Cloud Foundry services, including any instances of Pivotal HD Data Services. For example:
	
	<pre class="terminal">
	$ cf services
	Getting services in org pivotalrocks / space staging as admin...
	OK

	name        service   plan       bound apps             
	phd-clus1   p-hd      Standard   app-sinatra-services	

	</pre>
	
* `cf service-brokers`

	Displays a list of Cloud Foundry service brokers. For example:
	
	<pre class="terminal">
	$ cf service-brokers
	Getting service brokers as admin...

	name         url   
	phd-broker   http://10.0.0.51:8080
   </pre>

* `cf delete-service-broker`

	Deletes a Cloud Foundry service broker.

* `bosh delete deployment`

	Deletes a BOSH deployment. 

* `bosh releases`

	Displays a list of available releases. 

	
#Using SSH into Virtual Machines in the Cluster	

To access the various machines in a Pivotal HD cluster by ssh:

1. Open the Ops Manager application in a Web browser.

2. now what ?? can't see it no phd in rock.music
