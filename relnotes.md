---
title: Release Notes for Pivotal HD Service v 1.3.2.0
owner: Pivotal HD
---

**Note:** Pivotal HD for [Pivotal Cloud Foundry&reg;](https://network.pivotal.io/products/pivotal-cf) (PCF) 1.3.2.0 is not supported for production deployments.

#Changes since v1.2.1.0:
* Administrators can now define multiple, On-demand Service Plans using Pivotal Cloud Foundry&reg; Operations Manager.
* Administrators can now define [External Service Plans](external-service-plans.html), which broker access to pre-existing Pivotal HD software components.
* Administrators can now exclude HDFS from on-demand Service Plans, and instead utilize a [pre-existing instance of HDFS running on Isilon](isilon.html) OneFS v7.1 + the HDFS 2.2 Service Patch.
* On-demand Service Plans now deploy Service Instances consisting of Pivotal HD software v2.0.1 instead of v1.1.0.
* GemFire XD is now a fully supported component of on-demand Service Plans.
* Files written to HDFS by the GemFire XD component of on-demand Service Plans can now be accessed as external tables by the HAWQ component.
* On-demand Service Plans now utilize exactly the number of IP Addresses required instead of a fixed amount.  See the [Prerequisites](installation.html#prereq) for for information on IP Address requirements.
* On-demand Service Plans now enforce the maximum allowed size of a persistent disk in BOSH for each virtual machine it deploys.
* Default resource sizes for On-Demand Service Plans have been tuned.

#Known Issues
* v1.3.2.0 can only be upgraded from v1.2.1.0.
* v1.3.2.0 requires v1.3.4.0 of Operations Manager.
* When upgrading from v.1.2.1.0, Service Plans will reset to include all Pivotal HD components in Operations Manager.  Un-check any components you do not wish to include before applying your changes.
* The state of Pivotal HD Service instances is not visible in Operations Manager and must be viewed using the BOSH CLI.
