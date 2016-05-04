---
title: HDFS Isilon Integration
owner: Pivotal HD
---

This section explains how Pivotal HD components deployed by the Pivotal HD Service interoperate with the  EMC Isilon Scale-Out NAS running the HDFS protocol.

* [Overview of Isilon Integration](#overview)
* [Prerequisites for Isilon Integration](#prereq)
* [HAWQ and HDFS Directories](#hawq_hdfs)

<a id="overview"></a>
#Overview of Isilon Integration
EMC Isilon is a Scale-Out NAS platform that can be configured for native support of the HDFS protocol.  Hosts running a MapReduce job or a HAWQ query will access the Isilon NAS in order to fetch the data required for their computation.

When the Pivotal HD Service is configured to use Isilon HDFS, it deploys Service Instances where the appropriate configuration files specify the Isilon host as the location of the HDFS NameNode.

Hadoop clients connect to HDFS through a fully-qualified domain name (FQDN) and port number. For EMC Isilon this FQDN is the SmartConnect address that is used to load balance connections across all nodes of an Isilon cluster. See the Isilon documentation on the [EMC Support Web site](http://www.emc.com/support/emc-isilon-customer-support.htm) for for more information about SmartConnect.

 Figure 2. illustrates this concept:

**Figure 2. HDFS on Isilon**
![HDFS on Isilon](/images/isilon_hdfs2.png "HDFS on Isilon")

<a id="prereq"></a>
#Prerequisites for Isilon Integration
The following capabilities must be configured or validated on Isilon prior to deploying a Pivotal HD Service plan configured to use Isilon’s HDFS protocol.

* Ensure Isilon OneFS software compatibility: Version 7.1 with the HDFS version 2.2 patch for OneFS is installed
* Ensure that HDFS is enabled using the HDFS license key
* Ensure there is network connectivity and sufficient bandwidth between the vSphere hosts where the PHD Service Instances will run and the Isilon instance.
* Verify or setup all required Hadoop users and ensure that they have the appropriate read/write privileges.  You can setup users by using the following commands on Isilon OneFS:

<pre >
mkdir /ifs/hdfs_data
chmod 777 /ifs/hdfs_data
isi auth groups create hadoop --gid 500
isi auth groups create hdfs --gid 501
isi auth groups create yarn --gid 502
isi auth groups create gpadmin --gid 503
isi auth groups create mapred --gid 504
isi auth groups create gfxd --gid 505
isi auth users create hadoop --enabled true --password <your-preferred-password> --uid 500 --primary-group hadoop
isi auth users create hdfs --enabled true --password <your-preferred-password> --uid 501 --primary-group hdfs
isi auth users create yarn --enabled true --password <your-preferred-password> --uid 502 --primary-group yarn
isi auth users create gpadmin --enabled true --password <your-preferred-password> --uid 503 --primary-group gpadmin
isi auth users create mapred --enabled true --password <your-preferred-password> --uid 504 --primary-group mapred
isi auth users create gfxd --enabled true --password <your-preferred-password> --uid 505 --primary-group gfxd
chown -R hadoop:hadoop /ifs/hdfs_data
</pre>

Note that HAWQ always connects to HDFS as the user `gpadmin` regardless of which user is accessing HAWQ.  Likewise, GemFire XD always connect to HDFS as the user `gfxd`.

Change The Isilon OneFS default block size setting for HDFS using the following command:

`isi hdfs settings modify --default-block-size 128M`

<a id="hawq_hdfs"></a>
# HAWQ and HDFS Directories

HAWQ is configured by default to use a specific directory on HDFS for the data it stores when a user writes to a standard table.  HAWQ is engineered under the assumption that only one instance of HAWQ writes to that directory. In order to ensure that instances of HAWQ do not conflict with each another, the Pivotal HD Service Broker configures a unique directory name for each HAWQ instance it creates. Using the `gpadmin` HDFS username, the Pivotal HD Service creates the corresponding HDFS directory on Isilon using the appropriate HDFS commands when it deploys a service instance that includes HAWQ.

The Pivotal HD Service creates directory names for each HAWQ instance using the following pattern:

`/user/gpadmin/phd-1`

`/user/gpadmin/phd-2`

`...`