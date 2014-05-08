---
title: Using a Pivotal HD Data Service
---

After Pivotal HD Data Services is installed you can deploy instances of the Pivotal HD cluster that are defined in the Service Plan. The plan defines the maximum number of cluster instances you can create as well as the number of pre-created cluster instances that are available. You can bind applications deployed in the Cloud Foundry environment to these cluster instances. 

* [Creating Pivotal HD Cluster Instances](#create-cluster)
* [Deleting Pivotal HD Cluster Instances](#delete-cluster)
* [Binding Applications to Pivotal HD Cluster Instances](#binding)
* [Unbinding Applications from Pivotal HD Cluster Instances](#unbinding)


<a id="create-cluster"></a>
#Creating and Using Pivotal HD Cluster Instances

You use either the Pivotal CF Developer Console or the Pivotal CF command line to create cluster instances.

##Pivotal CF Developer Console

To create an instance of a Pivotal HD Service Plan using the Pivotal CF Developer Console: 

1. Log in to the **Pivotal CF Developer Console**.  

2. Select your Org from the drop-down list on the left. 

3. Select **Marketplace** from the left navigation menu. 

	The **Services Marketplace** displays.

4. Select **Pivotal HD**.

	The **Pivotal HD Service** page displays.

5. Click **Create a Service**.

	The **Add a new Service Instance** page displays.
	
6. Enter a name for this PHD service instance. 

7. Select a space from the **Add to Space** drop-down list.

8. (Optional) Select an application from the **Bind to App** drop-down list. The drop-down list displays available applications previously configured for this Org and Space. If you do not want to bind an application, select **[do not bind]**.

9. Click **Add**. 

The PHD service deploys. To see the status of this cluster, select its space from the navigation menu on the left and select the instance from the list that displays. 

**Pivotal CF Developer Console**

![Pivotal CF Developer Console](/images/dev_console_large.png "Pivotal CF Developer Console")
	
For more information, see [Getting Started with the Developer Console](http://docs.gopivotal.com/pivotalcf/console/pcf_console.html).

##Pivotal CF Command Line

To create a Pivotal HD cluster instance:

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`$ cf target -s <space name>`
		
2. Run the following command:

	`$ cf create-service p-hd <Service Plan name> <instance name>`
	
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

<a id="delete-cluster"></a>
#Deleting Pivotal HD Cluster Instances

After creating a Pivotal HD cluster instance, you can delete the instance.


##Pivotal CF Developer Console

1. Log in to the **Pivotal CF Developer Console**.  

2. Select your Org from the drop-down list on the left. 

3. Select the space where your Pivotal HD cluster instance is deployed from the left navigation menu. 

	A list of applications and services instances displays.

3. Locate the row under **Services** that contains the service instance you want to delete and click **Delete**. 

	A confirmation dialog box displays.

##Pivotal CF Command Line

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`$ cf target -s <space name>`
		
2. Run the following command:

	`$ cf delete-service <instance name>`
	
	Where *instance name* is the name of the instance you are creating. 
	 
	For example:
	
	<pre class="terminal">
	$ cf delete-service phd1

	Are you sure you want to delete the service phd1 ? y
	Deleting service phd1 in org pivotalrocks / space staging as admin...
	OK
	
    </pre>

<a id="binding"></a>
#Binding an Application to a Pivotal HD Cluster Instance

The process of binding an application to a service automatically populates a set of environment variables. These variables define credentials, URLs for services and other configurations. When you use Pivotal CF to bind an application to a Pivotal HD service, these variables are populated automatically. When the application moves into a production phase, you can easily bind the application to an external instance of Pivotal HD by setting new values for these variables.

For more information, see the following topic in the Pivotal CF documentation: [Bind a Service](http://docs.gopivotal.com/pivotalcf/devguide/services/bind-service.html).

##Viewing Binding Meta Data and Environment Variables

You can view the binding variables using either the Pivotal CF Developers Console or a Web browser to retrieve a the variables in JSON format.

###Pivotal CF Developer Console

To view the binding variables from the **Pivotal CF Developer Console**:

1. Log in to the **Pivotal CF Developer Console**.  

2. Select your Org from the drop-down list on the left. 

3. Select the space where your Pivotal HD cluster instance is deployed from the left navigation menu. 

	A list of applications and services instances displays.

4. Locate your Pivotal HD instance in the list of Bound Services and click **Credentials**.

	A dialog box displays the credentials for the components of the Pivotal HD instance.
	For example:
	
	![PHD Credentials Bindings](/images/cred_bindings.png "PHD Credentials Bindings")

	You may need to copy the contents of each field and paste them into a text editor to view them. 
	
###JSON Format

You can display the binding variables as a JSON document:

1. Open a Web browser and enter a URL constructed as follows:

	`<app name>.<Web Console URL>/env`
	
	For example, the following URL returns the environment variables for the `app-sinatra-services` application. 

	`app-sinatra-services.rock.music.cf-app.com/env`

	The browser displays the following JSON document (the output has been formatted for easier reading):

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

##Pivotal CF Developer Console

1. Log in to the **Developer Console**. 

2. Select your Pivotal HD Cluster service.

3. Select the space where the application you want to bind is deployed.

	A list of deployed applications and services displays. 

5. Locate the row containing the application and click the **>** link. 

	A page displays that show the bound services and instances for this application.

6. Click **Bind**

	A list of a available services displays.

7. Click the **Bind** button for the service you want to bind to this application. 

##Pivotal CF Command Line

1. Using ssh, log in to the virtual machine that Ops Manager deploys on the first install of the Ops Manager Director for VMware vSphere.

2. If necessary, select a space using the following command:

	`$ cf target -s <space name>`

3. Run the following command:

	`$ cf bind-service <application> <service instance name>`

	For example:
	
	<pre class="terminal">
	
	$ cf bind-service app-sinatra-services phd2
	Binding service phd2 to app app-sinatra-services in org pivotalrocks / space staging as admin...
	OK
	TIP: Use 'cf push' to ensure your env variable changes take effect
</pre>


<a id="unbinding"></a>
#Unbinding an Application from a Pivotal HD cluster instance

You can unbind a bound application from a Pivotal HD cluster instance using either the Pivotal CF Developer Console or the Pivotal CF command line. 

##Pivotal CF Developer Console

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

	`$ cf target -s <space name>`

3. Run the following command:

	`$ cf bind-service <application> <service instance name>`

	For example:
	
	<pre class="terminal">
	
	$ cf bind-service app-sinatra-services phd2
	Binding service phd2 to app app-sinatra-services in org pivotalrocks / space staging as admin...
	OK
	TIP: Use 'cf push' to ensure your env variable changes take effect
</pre>


