---
title: Release Notes for Pivotal HD Data Services v 1.2.0.0
---
#Pre-Created Clusters

* Each service creation request from the Cloud Foundry CLI or Pivotal CF Developer Console now results in the deployment of a new Pivotal HD 1.1 cluster. Previously, a single, multi-tenant Pivotal HD cluster was deployed for use within Pivotal CF. 

#Pivotal HD Service Plans

* The Pivotal CF Administrator can now configure the metadata and Pivotal HD components they wish to offer as a Pivotal CF Service Plan. Previously, the service plan was hard coded.

* Administrators can now define the vSphere network where Pivotal HD Data Services deploys Pivotal HD clusters, independent of the network used for the deployment of Pivotal CF. If these networks are different, the networks must be able to route traffic to each other.

* vSphere resources continue to be configurable per component.

#GemFire XD Beta

* This release enables beta testing of GemFire XD 1.0 as a Pivotal CF Service.

* Hive, HBase, and the Pivotal HD Client VM have been removed as components of a PHD deployment

#Binding to a Service Instance

* Binding to a service instance now provisions and returns user credentials and API endpoints for all components of the PHD cluster.

#Known Issues:

* JVM memory allocation is fixed. Increasing the memory allocation for the GemFire XD locator component no longer results in more memory being used by the corresponding GemFire XD process.
