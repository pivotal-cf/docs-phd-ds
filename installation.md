---
title: Installing Pivotal HD Data Services
---

#Prerequisites

Installation of Pivotal HD Data Services requires the following:

* An installed instance of Pivotal Cloud Foundry
* Pivotal Elastic Runtime installed in the Cloud Foundry environment.
* Web Browser
* Network access and credentials for the Pivotal Cloud Foundry Ops Manager application. 
* Network access and credentials for the Pivotal Cloud Foundry Developer Console. 

#Installing Pivotal HD Data Services

<ol>
        <li>Download the Pivotal HD Data Services software from <a href="http://network.gopivotal.com/">The Pivotal Network</a>.
        </li>
        <li>Use a Web browser to open the <strong>Pivotal Ops Manager</strong> application. (This application is part of your Pivotal Cloud Foundry installation.) <p>The <strong>Pivotal CF Ops Manager Installation Dashboard</strong> displays:</p>
                <img
                    align="left"
                    alt="Ops Manager"
                    src="images/ops_manager_large.png" />
            </li>
        
        <li> Click the <strong>Import a Product</strong> button.
            
            <p> The <strong>Add Products</strong> screen displays.</p>
        </li>
        <li>Click the <strong>Choose File</strong> button and navigate to the file you downloaded.
            
            <p>The file uploads to your Pivotal CF deployment. </p>
        </li>
        <li> Click the <strong>Add</strong> button. <p>Pivotal Ops Manager adds a new tile for Pivotal HD to the Installation Dashboard. </p>
            </li>
        
        <li>Click the <strong>Pivotal HD for Pivotal CF</strong> tile.</li>
        <li>
            <p>If it is not already selected, click <strong>Network Settings</strong>.</p>
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
                <p>If necessary, you can configure hardware resources for the PHD Data Services Broker. Generally, you do not need to change these values. You can configure values for: </p>
                <ul>
                <li>CPU</li>
                <li>RAM</li>
                <li>Persistent Disk</li>
            </ul>
                <p>The compilation nodes are temporary VMs that Ops Manager uses when creating other VMs. You do not need to change these values.</p>
            </li>
            <li>Click <strong>Save</strong>.</li>
            <li>Click the <strong>Installation Dashboard</strong> link.<p>The <strong>Installation Dashboard</strong> screen displays. </p></li>
            <li>Click the <strong>Apply Changes</strong> button.<p>Ops Manager creates a virtual machine to run the service broker and begins the installation. A progress meter displays the progress of the installation.  When the installation is complete, you can create instances of the Pivotal HD cluster as defined in the Service Plan.</p>
                <p>To create cluster instances, see <a
                        href="data_service.html">Using Pivotal HD Data Services</a>.</p></li>
    </ol>



