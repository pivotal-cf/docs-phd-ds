---
title: Creating Pivotal HD Cluster Instances
---

#Creating Instances

After Pivotal HD Data Services is installed you can deploy instances of the Pivotal HD cluster that are defined in the Service Plan. The plan defines the maximum number of cluster instances you can create as well as the number of pre-created cluster instances that are available.

To create an instance of a Pivotal HD Service Plan: 

1. Log in to the **Developer Console**.  

2. Click **Add Service**.

	The Services Marketplace screen displays.

3. Select the Pivotal HD Service.

4. ?? 

For more information, see [Getting Started with the Developer Console](http://docs.gopivotal.com/pivotalcf/console/pcf_console.html).

#Binding 

The process of binding an application to a service automatically populates a set of environment variables. These variables define credentials, URLs for services and other configurations. When you use Pivotal CF to bind an application to a Pivotal HD service, these variables are populated automatically. When the application moves into a production phase, you can easily bind the application to an external instance of Pivotal HD by setting new values for these variables. Pivotal CF can also automatically create these bindings. See [Bind a Service](http://docs.gopivotal.com/pivotalcf/devguide/services/bind-service.html).

??insert list of env vars

1. Log in to the **Developer Console**. 

2. Select your Pivotal HD Cluster service.

3. Click **Bind**

