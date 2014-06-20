---
title: Release Notes for Pivotal HD Service v 1.2.1.0
---
#Pre-Created Clusters

* Each service creation request from the Cloud Foundry CLI or Pivotal CF Developer Console now results in the deployment of a new Pivotal HD 1.1 cluster. Previously, a single, multi-tenant Pivotal HD cluster was deployed for use within Pivotal CF. 

#Pivotal HD Service Plans

* The Pivotal CF Administrator can now configure the metadata and Pivotal HD components they wish to offer as a Pivotal CF Service Plan. Previously, the service plan was hard coded.

* Administrators can now define the vSphere network where Pivotal HD Service deploys Pivotal HD clusters, independent of the network used for the deployment of Pivotal CF. If these networks are different, the networks must be able to route traffic to each other.

* vSphere resources continue to be configurable per component.

#GemFire XD Beta

* This release enables beta testing of GemFire XD 1.0 as a Pivotal CF Service.

* Hive, HBase, and the Pivotal HD Client VM have been removed as components of a PHD deployment.


#Updates in Ops Manager

As of Version 1.2.1.0:

* Changes to the Service are now reflected properly when an Administrator updates fields in Ops Mgr and applies the changes. Note that active Service Instances are never modified even if the Service Plan has been updated. Only new Service Instances created after the update reflect changes.

# Service Instance Dashboard

As of Version 1.2.1.0:

* Service Instances now include a dashboard, which Pivotal CF users can access from the Pivotal CF Web Console. This dashboard helps Pivotal CF users understand what Pivotal HD components are running and where without having to bind an application.


#Binding to a Service Instance

* Binding to a service instance now provisions and returns user credentials and API endpoints for all components of the PHD cluster.

#Known Issues:

* JVM memory allocation is fixed. Increasing the memory allocation for the GemFire XD locator component no longer results in more memory being used by the corresponding GemFire XD process.

* Pivotal HD for Pivotal CF v1.2.0.0 cannot be directly upgraded to v1.2.1.0.  It must first be uninstalled in Ops Manager and deployments and releases manually deleted via bosh prior to upgrading to v1.2.1.0.  Detailed instructions on how to do this are documented under [Installation Steps](installation.html#install).

* jvm memory allocation is currently fixed. Increasing the memory allocation for the GemFire XD locator or Slave component will not result in more memory being used by the corresponding GemFire XD processes.
