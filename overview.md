---
title: Overview
---

Pivotal HD Data Services allows Pivotal Cloud Foundry users to define the parameters of a Pivotal HD cluster and quickly create one or more instances of the cluster in the Cloud Foundry environment. Using Cloud Foundry tools, developers can easily bind applications to the Pivotal HD cluster for data access. When an application moves into production, you can bind the application to use a production instance of Pivotal HD that is external to Cloud Foundry. 

An administrator initially defines a *Service Plan* for the cluster. The Service Plan specifies which Hadoop components to deploy, the number of nodes to deploy, the hardware configuration of the nodes, the number of slaves, and other information. The administrator also specifies the maximum number of clusters that can be created and the number of *pre-created* clusters to keep ready for quick deployment. Pivotal HD Data Services creates and starts the nodes of these these pre-created cluster instances in advance, eliminating the need to wait while the cluster's virtual machines are created and started. 

Pivotal HD Data Services includes all of the Pivotal HD version 1.1 software. A separate installation of Pivotal HD is not required to use Pivotal HD Data Services. 

Figure 1 shows the work flow for creating Pivotal HD clusters using Pivotal HD Data Services:

**Figure 1. Pivotal HD Data Services Work Flow**

![Data Service Work Flow](/images/data_service.png "Data Service Work Flow")