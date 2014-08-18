---
title: Overview
---

The Pivotal HD Service allows Pivotal CF users to create Pivotal HD clusters on-demand.  A cluster is allocated each time a Pivotal CF user creates an instance of the Pivotal HD Service using the Pivotal CF Command Line Interface or Developer Web Console.  Pivotal CF users can also create and bind user credentials for each component of the Pivotal HD cluster to any application they push to Pivotal Elastic Runtime.

 A Pivotal CF Administrator initially imports the Pivotal HD Service into Pivotal CF Ops Manager, where they define the details of the service plan they wish to offer.  The service plan is a blueprint that describes what each instance of a Pivotal HD cluster is comprised of.  The definition consists of which Pivotal HD components to include, the number of slave nodes to deploy, and how much CPU, Ram and Disk to use for each virtual machine required for the included Pivotal HD components.  The administrator also specifies the maximum number of instances of the service that can be created along with the number to pre-create for rapid allocation to Pivotal CF users.  The Pivotal HD Service creates and starts the virtual machines of these pre-created clusters in advance, eliminating the need for Pivotal CF users to wait when creating an instance of the service."

The Pivotal HD Service includes several components from the Pivotal HD 1.1 software stack, including HDFS, YARN and MapReduce2.  Additionally, the Pivotal HD Service includes HAWQ and PXF.  Lastly, the Pivotal HD Service includes GemFire XD, which is currently available for beta testing purposes. For more details about the individual software components and their versions, please see the [Pivotal HD Enterprise 1.1.1 Release Notes](http://pivotalhd.docs.pivotal.io/doc/1110/PHDEnterprise1.1.1ReleaseNotes.html).

Figure 1 shows the work flow for creating Pivotal HD clusters using Pivotal HD Service:

**Figure 1. Pivotal HD Service Work Flow**

![Data Service Work Flow](/images/data_service.png "Data Service Work Flow")