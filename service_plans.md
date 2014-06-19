---
title: Creating Pivotal HD On-Demand Service Plans
---

#Overview

A Pivotal CF Administrator can define the details of the Pivotal HD service plan they wish to offer to their Pivotal CF users.  An on-demand service plan is a blueprint that describes the components and configuration of each instance of a Pivotal HD cluster.  The Pivotal HD Service includes default values for the service plan, which can be changed by the Pivotal CF Administrator.

* [Creating an On-Demand Service Plan](#creating)

* [Modifying an On-Demand Service Plan](#modifying)

<a id="creating"></a>
#Creating On-Demand Service Plans

To create an On-Demand Service Plan:

<ol>
            <li>
                <p>Use a Web browser to open the <strong>Pivotal Ops Manager</strong> application. (This application is part of your Pivotal Cloud Foundry installation.)</p>
            </li>
            <li>Click the <strong>Pivotal HD for Pivotal CF</strong> tile. </li>
            <li>
                <p>Click <strong>On-demand Service Plans</strong>.</p>
                <p>The <strong>On-demand Service Plans</strong> screen displays.</p>
            </li>
            <li>
                <p>Configure the following display options for your Pivotal HD cluster plans. This information displays in the Pivotal CF Console and Command-line Interface.</p>
						
                <table
                    frame="void" rules="all"
                    width="783">
                    <caption>Informational Display</caption>
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
                        </tr>
                    </thead>
                    <tbody>
                        
                        <tr>
                            <td>Service Plan Name</td>
                            <td>Name of the Service Plan. You use this name when creating Pivotal HD service instances.</td>
                        </tr>
                        <tr>
                            <td> Service Plan Feature Bullet 1 </td><td
                                rowspan="4">These fields are used by the Pivotal CF Administrator to describe the details of the service plan to Pivotal CF users.  The values in these fields display to users in the Marketplace section of the Pivotal CF Developer Console. </td>
                        </tr>
                        <tr>
                            <td>Service Plan Feature Bullet 2 </td>
                        </tr>
                        <tr>
                            <td>Service Plan Feature Bullet 3 </td>
                        </tr>
                      
                        
                        
                    </tbody>
                </table>
            </li>
            <li>Enter the following values regarding the cost of Pivotal HD clusters. These fields are for display only. The values in these fields display to users in the Cloud Foundry CLI and in the Marketplace section of the Pivotal CF Developer Console.<table
                    frame="void"
                    rules="all">
                    <caption>Cost Information</caption>
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
                            <td> Amount </td>
                            <td>Cost in US dollars to create a Pivotal HD cluster instance from this Service Plan </td>
                            <td>US dollars</td>
                        </tr>
                        <tr>
                            <td>Unit of Measurement</td>
                            <td>Unit of measurement used for billing, for example: Monthly, or weekly. </td>
                            <td>Text</td>
                        </tr>
                    </tbody>
                </table>
            </li>
            <li>The Pivotal CF Administrator should ensure that the Pivotal HD Service does not oversubscribe the underlying vSphere resources.  Enter the following values for the cluster defined in your service plan: <table
                    frame="void" rules="all">
                    <caption>Cluster Instances</caption>
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
                            <td>Maximum Number of Instances </td>
                            <td>Maximum number of Pivotal HD instances that users can create from this Service Plan.</td>
							<td><ul>
							                                    <li>Minimum: 1</li>
							                                </ul><p>This field must not be left blank.</p></td>
                        </tr>
                        <tr>
                            <td> Number of Pre-Created Instances</td>
                            <td>Pivotal HD Service creates a reserved pool of Service Plan Instances to allocate to Pivotal CF Users. When an Service Plan Instance is allocated in Pivotal CF Elastic Runtime, the service back-fills the pool. <p>The Service never pre-creates more instances than the configured Maximum Number of Instances. </p></td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: Maximum Number of Instances Created (configuration value, see above)</li>
                                </ul><p>This field must not be left blank.</p>
                            </td>
                        </tr>
                    </tbody>
                </table></li>
            <li>Fill in the remaining fields to define the configuration of the Pivotal HD clusters that will be created by this Service Plan. <p>For more information about Pivotal HD and its components, see the <a
                        href="http://pivotalhd.docs.gopivotal.com/index.html">Pivotal HD Documentation</a> .</p><table
                    frame="void"
                    rules="all"
                    width="846">
                    <caption>Pivotal HD Cluster Configuration</caption>
                    <col
                        width="34%" />
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
                            <td>Service Plan Components:</td>
                            <td>Select the HD components you want included in this Service Plan. HDFS is always included by default in a Service Plan.<p>To create a Service Plan that only offers a Hadoop service, select only the <strong>YARN/MapReduce2</strong> option.</p></td>
                            <td>
                                <ul>
                                    <li>Yarn/MapReduce2 </li>
                                    <li>HAWQ</li>
                                    <li>GemFire XD</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>Number of PHD Slaves</td>
                            <td
                                rowspan="3">Each instance of a PHD Slave virtual machine runs all applicable slave processes for the PHD components that are included in the Service Plan. If only Yarn/MapReduce2 is selected above, then the slave runs only that NodeManager process. <p></p>If HAWQ is also selected, the HAWQ Segment Server process is included. <p></p>Note that the HDFS DataNode process always runs on these slaves. </td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li><strong>Default: </strong>1</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>PHD Slave CPU</td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64</li>
                                    <li><strong>Default: </strong>2</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>PHD Slave RAM in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 8192</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>8192</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>PHD Slave Persistent Disk in MB </td>
                            <td></td>
                            <td>
                                <ul>
                                    <li>Minimum: 12288</li>
                                    <li>Maximum: 65011712 </li>
                                    <li><strong>Default: </strong>12288</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>NameNode CPU</td>
                            <td
                                rowspan="3">The NameNode runs on its own dedicated virtual machine.</td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64 </li>
                                    <li><strong>Default: </strong>1</li>
                                </ul>
                                <p> This field must contain a power of 2.</p>
                            </td>
                        </tr>
                        <tr>
                            <td>NameNode RAM in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 2048</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>2048</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>NameNode Persistent Disk in MB</td>
                            <td>
                                <ul>
                                    <li>Minimum: 8192</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>8192</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>ResourceManager CPU </td>
                            <td
                                rowspan="3">The ResourceManager runs on its own dedicated virtual machine. </td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64 </li>
                                    <li><strong>Default: </strong>1</li>
                                </ul>
                                <p>This field must contain a power of 2</p>
                            </td>
                        </tr>
                        <tr>
                            <td>ResourceManager RAM in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 2048</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>2048</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>ResourceManager Ephemeral Disk in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 5120</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>5120</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>HAWQ Master CPU</td>
                            <td
                                rowspan="3">The HAWQ Master runs on its own dedicated virtual machine. If you do not specify HAWQ as part of this cluster, these fields are ignored. </td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64 </li>
                                    <li><strong>Default: </strong>1</li>
                                </ul>
                                <p>This field must contain a power of 2</p>
                            </td>
                        </tr>
                        <tr>
                            <td> HAWQ Master RAM in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 2048</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>1</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>HAWQ Master  <span
                                    style="color: rgb(104, 104, 104); font-family: source_sans_prolight; font-size: 13px; font-style: normal; font-variant: normal; font-weight: normal; letter-spacing: normal; line-height: normal; orphans: auto; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: auto; word-spacing: 0px; -webkit-text-stroke-width: 0px; display: inline !important; float: none; background-color: rgb(248, 248, 248);">Persistent</span>  Disk in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 4096</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>4096</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>Gemfire XD Locator CPU</td>
                            <td
                                rowspan="3">The Gemfire XD Locator runs on its own dedicated virtual machine. If you do not specify GemFire XD as part of this cluster, these fields are ignored. </td>
                            <td>
                                <ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64 </li>
                                    <li><strong>Default: </strong>1</li>
                                </ul>
                                <p>This field must contain a power of 2</p>
                            </td>
                        </tr>
                        <tr>
                            <td>Gemfire XD Locator RAM in MB</td>
                            <td>
                                <ul>
                                    <li>Minimum: 1024</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>1024</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td>Gemfire XD Locator Persistent Disk in MB </td>
                            <td>
                                <ul>
                                    <li>Minimum: 3072</li>
                                    <li>Maximum: 1048576 </li>
                                    <li><strong>Default: </strong>3072</li>
                                </ul>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </li>
            <li>Click the <strong>Save</strong> button.</li>
			<li>(Optional) Click 
            
</ol>
<a id="modifying"></a>
#Modifying an On-Demand Service Plan

<p><strong>Note:</strong>Modifications to the default On-Demand service plan settings only apply to any new <em>new</em> service instances that users create. If you modify the service plan, any pre-created service instances are destroyed and new, pre-allocated instances are created with the new configurations. Existing service instances are not modified.</p>

<p>To modify an On-Demand Service Plan:

<ol>
<li>
<p>Use a Web browser to open the <strong>Pivotal Ops Manager</strong> application. (This application is part of your Pivotal Cloud Foundry installation.)</p>
</li>
<li>Click the <strong>Pivotal HD for Pivotal CF</strong> tile. </li>
<li>
 <p>Click <strong>On-demand Service Plans</strong>.</p>
 <p>The <strong>On-demand Service Plans</strong> screen displays.</p>
</li>
<li>Change any of the fields that define the service plan.</li>
<li>Click the <strong>Save</strong> button.</li>
</ol>