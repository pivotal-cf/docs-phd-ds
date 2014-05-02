---
title: Overview
---

Pivotal HD Data Services allows Pivotal Cloud Foundry users to define a Pivotal HD cluster and to quickly create instances of the cluster in the Cloud Foundry environment for use in development and testing. Using Cloud Foundry tools, you can bind applications to the cluster for data access. When an application moves into production, it is easy to bind the application to use a production instance of Pivotal HD that is external to Cloud Foundry. 

Ad administrator initially defines a Service Plan for the cluster. The Service Plan specifies which Hadoop components to deploy, the number of nodes to deploy, the hardware configuration of the nodes, and the number of slaves, etc. Pivotal HD Data Services uses the Service Plan to create a Pivotal HD cluster. The administrator also specifies the maximum number of clusters that can be created and the number of pre-created clusters.

Pre-created cluster instances are made available as "hot standbys". Pivotal HD Data Services creates and starts the nodes of these clusters in advance, making the clusters ready for immediate deployment. Developers can easily bind applications to the new cluster using Pivotal Cloud Foundry tools.

Pivotal HD Data Services includes all of the Pivotal HD version 1.1 software. A separate installation of Pivotal HD is not required to use Pivotal HD Data Services. 

?? Applications that require "elastic" resources can also use Pivotal HD Data Services to quickly spin-up a cluster and then destroy it when it is no longer needed so that its resources can be redeployed or shutdown to save power. 

Figure 1 shows the work flow for installing Pivotal HD Data Services and creating clusters:

**Figure 1. Pivotal HD Data Services Work Flow**

![Data Service Work Flow](/images/data_service.png "Data Service Work Flow")