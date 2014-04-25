---
title: Pivotal HD Data Services Overview
---

These pages describe how to install, configure and use Pivotal HD Data Services.

The document contains the following topics:

* [Overview](index.html#overview)
* [Installing Pivotal HD Data Services](installation.html)
* [Creating Service Plans](service_plans.html)
* [Using the Pivotal HD Data Service](data_service.html)

#Overview
Pivotal HD Data Services allows Pivotal Cloud Foundry users to define a Pivotal HD cluster and quickly create instances of the cluster in the Cloud Foundry environment for use in development and testing. When an application moves into production, it is easy to reconfigure the application to use a production instance of Pivotal HD. 

Ad administrator initially defines the configuration of the cluster (the number of nodes, hardware configuration of the nodes, number of slaves, etc.). The administrator also defines the number of instances to pre-create. Pre-created cluster instances are made available as "hot standbys". These nodes of these clusters are created and started in advance and are ready for immediate deployment. Developers can easily bind applications to the cluster using Pivotal Cloud Foundry tools. 

?? Applications that require "elastic" resources can also use Pivotal HD Data Services to quickly spin-up a cluster and then destroy it when it is no longer needed so that its resources can be redeployed or shutdown to save power. The clusters can also be used in a multi-tenant environment with support for billing.





