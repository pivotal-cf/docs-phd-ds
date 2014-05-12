---
title: Installing Pivotal HD Service
---

#Prerequisites

Installing Pivotal HD Service requires the following:

* An installed instance of Pivotal CF
* Pivotal Elastic Runtime installed in the Pivotal CF environment
* Web Browser
* Network access and credentials for the Pivotal Cloud Foundry Ops Manager application

#Installation Steps

<ol>
        <li>Download the Pivotal HD Service's software binary from <a href="http://network.gopivotal.com/">The Pivotal Network</a>.
        </li>
        <li>Use a Web browser to open the <strong>Pivotal Ops Manager</strong> application. (This application is part of your Pivotal CF installation.) <p>The <strong>Pivotal CF Ops Manager Installation Dashboard</strong> displays:</p>
               <p> <img
                    alt="Ops Manager"
                    src="images/ops_manager_large.png" /></p>
            </li>
        
        <li> Click the <strong>Import a Product</strong> button.
            
            <p> The <strong>Add Products</strong> screen displays.</p>
        </li>
        <li>Click the <strong>Choose File</strong> button and navigate to the file you downloaded.
            
            <p>The file uploads to your Pivotal CF deployment. </p>
        </li>
        <li> Click the <strong>Add</strong> button. <p>Pivotal Ops Manager adds a new tile for Pivotal HD Service to the Installation Dashboard. </p>
            </li>
        
        <li>Click the <strong>Pivotal HD for Pivotal CF</strong> tile.</li>
        <li>
            <p>If it is not already selected, click <strong>Network Settings</strong>.</p>
			<p>For additional information and examples about setting up vSphere networking, see <a href="#vsphere">About vSphere Networking</a>.
        </li>
        <li>
            <p>Configure the following network settings for the virtual machines in your Pivotal HD cluster instances:</p>
            <table 
                frame="void" rules="all">
                <caption>Network Settings</caption>
                <col
                    width="33%" />
                <col
                    width="33%" />
                <col
                    width="33%" />
                <thead>
                    <tr>
                        <th>Parameter</th>
                        <th>Description</th>
                        <th>Values</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Network Name</td>
                        <td>The name of the network you want all Pivotal HD virtual machines to reside on. If the network is different than the network you configured in the Ops Manager vSphere settings, you must ensure connectivity between the two networks so that the service can monitor the Pivotal HD virtual machines properly.</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>IP Address Subnet</td>
                        <td>A valid subnet in which to deploy virtual machines. <p>Choose IP addresses that do not overlap with those you assigned to Ops Manager to ensure that  Pivotal HD virtual machines and Pivotal CF virtual machines are assigned unique IP addresses.</p></td>
                        <td>
                            <p>Enter the subnet using CIDR notation. For example:</p>
                            <p>
                                <code>10.10.10.10/16</code>. </p>
                        </td>
                    </tr>
                    <tr>
                        <td>Excluded IP Address Range</td>
                        <td>List any IP addresses you wish to reserve. These addresses will not be used by  by the Pivotal HD Service  to create virtual machines. </td>
                        <td>
                            <p>Separate multiple ranges with commas. For example:</p>
                            <p><code> 10.10.10.2-10.10.10.10, 10.10.10.200-10.10.10.254</code></p>
                        </td>
                    </tr>
                    <tr>
                        <td>DNS Servers</td>
                        <td>One or more IP Addresses of the Domain Name Servers. .</td>
                        <td></td>
                    </tr>
                    <tr>
                        <td>Default Gateway IP Address</td>
                        <td>IP address of the default gateway.</td>
                        <td>Separate the IP addresses with a comma.</td>
                    </tr>
                </tbody>
            </table>
        </li>
        <li>
            <p>Click <strong>Save</strong>.</p>
        </li>
        
        <li> Select <strong>On-demand Service Plans</strong> if you want to change the configuration of the on-demand Service Plan. The default Service Plan defines a Pivotal HD cluster that includes HDFS, YARN/MapReduce, HAWQ, and GemFire XD. You can use the default Service Plan as-is, or you can modify the Service Plan for your requirements. See <a
                    href="service_plans.html">Creating Service Plans</a>.</li>
            
            <li>Click <strong>Resource Sizes</strong>.
                <p>If necessary, you can change the configured hardware resource sizes for the Pivotal HD Service Broker You can configure values for: </p>
                <ul>
                <li>CPU</li>
                <li>RAM</li>
                <li>Persistent Disk</li>
            </ul>
                <p>The compilation nodes are temporary VMs that Ops Manager uses when creating other VMs. You do not need to change these values.</p>
            </li>
            <li>Click <strong>Save</strong>.</li>
            <li>Click the <strong>Installation Dashboard</strong> link.<p>The <strong>Installation Dashboard</strong> screen displays. </p></li>
            <li>Click the <strong>Apply Changes</strong> button.<p>Ops Manager creates a virtual machine to run the service broker and begins the installation. A progress meter displays the progress of the installation. 
				<p>When the installation is complete, the Pivotal HD Service Broker deploys the configured number of pre-created instances of Pivotal HD.  Information about these deployments are accessible from the BOSH Command Line Interface and not from the Operations Manager user interface.  Once the Pivotal HD clusters are deployed, the Pivotal HD Service broker automatically registers the service in the Elastic Runtime marketplace.  Once the Service is registered, Pivotal CF users can create instances and gain access to their own Pivotal HD cluster on-demand.</p>
				
		  </p>
                <p>To create cluster instances, see <a
                        href="data_service.html">Using Pivotal HD Service</a>.</p></li>
    </ol>

<a id="vsphere"></a>
#About vSphere Networking Configurations

This section describes vSphere configurations that you define on the **Network Settings** page. 

When configuring the Pivotal HD Service, you define which vSphere network you want the Pivotal Service Broker to use when deploying the virtual machines that comprise each Pivotal HD cluster.  This network can either be the same or different as the one you have configured Pivotal CF Operations Manager to use when deploying Pivotal CF.

Consider the following vSphere network diagram:

![vSphere Networking](/images/vsphere_networking.png)

If Operations Manager has been configured to deploy Pivotal CF and any imported Services to network A in the picture above, you can configure the Pivotal HD Service to also deploy Pivotal HD clusters to network A.  If you choose to use the same network as Pivotal CF, it is likely you will use IP addresses from a single IP subnet across all deployments.  Should you choose to use IP addresses from the same subnet, you must ensure that Operations Manager and the Pivotal HD Service do not attempt to use the same IP addresses in their deployments.

To achieve this, you must exclude the IP range you want the Pivotal HD deployments to use in the Ops Manager vSphere network settings and you must exclude the IP range you want Ops Manager deployments to use in the Pivotal HD Service's network settings.

Here is an example of how you might do that if you were deploying everything to the IP subnet 10.0.0.0/16.  In this example, we are reserving the first 512 IP Addresses for Operations Manager and the next 512 IP addresses for the Pivotal HD Service.

**VSphere Network Settings Tab:**

* Network Name: `vSphereNetwork_A`
* IP Address Subnet: `10.0.0.0/16`
* Excluded IP Address Range: `10.0.2.1-10.0.3.254` (IP addresses s you want the Pivotal HD Service to use in Pivotal HD deployments)
* DNS Servers: `8.8.8.8`
* Default Gateway IP Address: `10.0.0.1`

**Pivotal HD Service Network Settings Tab:**

* Network Name: `vSphereNetwork_A`
* IP Address Subnet: `10.0.0.0/16`
* Excluded IP Address Range: `10.0.0.1-10.0.2.0`  (IPs you want Operations Mgr to use in PCF deployments)
* DNS Servers: `8.8.8.8`
* Default Gateway IP Address: `10.0.0.1`

Alternatively, if you configure Ops Manager to deploy Pivotal CF to Network A and the Pivotal HD Service to deploy PHD clusters to Network C.  The only requirement in this case is that the two networks be able to route traffic to each other.

