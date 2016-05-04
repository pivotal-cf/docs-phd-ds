---
title: Creating and Modifying Pivotal HD On-Demand Service Plans
owner: Pivotal HD
---

#Overview

A [Pivotal Cloud Foundry&reg;](https://network.pivotal.io/products/pivotal-cf) (PCF) Administrator can define the details of the Pivotal HD On-Demand Service Plans they wish to offer to their PCF users. An on-demand service plan is a blueprint that describes the components and configuration of each instance of a Pivotal HD cluster. The Pivotal HD Service includes default values for the service plan, which can be changed by the PCF Administrator.

* [Creating an On-Demand Service Plan](#creating)

* [Modifying an On-Demand Service Plan](#modifying)

<a id="creating"></a>
#Creating an On-Demand Service Plan

To create an On-Demand Service Plan:

<ol>
            <li>
                <p>Use a Web browser to log in to the <strong>Pivotal Ops Manager</strong> application. (This application is part of your Pivotal Cloud Foundry&reg; installation.)</p>
            </li>
            <li>Click the <strong>Pivotal HD for PCF</strong> tile. </li>
            <li>
                <p>Select <strong>On-demand Service Plans</strong>.</p>
                <p>The <strong>On-demand Service Plans</strong> screen opens and displays a list of configured On-Demand Service Plans. If no service plans have been configured, you will see only the default, Standard service plan. </p>
            </li>
            <li>Click <strong>Add</strong>.<p>A new Service Plan is added and a form expands below its name.</p><img
                    alt="on-demand-service-plans.png"
                    height="50%"
                    src="images/on-demand-service-plans.png" /></li>
            <li>
                <p>Configure the following display options for your Service Plan. This information displays in the Apps Manager and command line interface.</p>

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
                            <td> The name you want PCF users to see in the CF CLI and Apps Manager. </td>
                        </tr>
                        <tr>
                            <td> Service Plan Feature Bullet 1 </td><td
                                rowspan="4"> The details of the service plan you want PCF users to see. The values in these fields display to users in the Marketplace section of the Apps Manager  </td>
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
            <li>Enter the following values regarding the cost of Pivotal HD clusters. These fields are for display only. The values in these fields display to users in the Cloud Foundry CLI and in the Marketplace section of the Apps Manager.<table
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
                            <td> (Required) The cost, if any, in US dollars to create an instance of this Service Plan.  For example: entering 1000 will display <b>$1000</b>. </td>
                            <td>Integer</td>
                        </tr>
                        <tr>
                            <td>Unit of Measurement</td>
                            <td>(Required) Unit of measurement used for billing, for example: Monthly, or weekly. </td>
                            <td>String</td>
                        </tr>
                    </tbody>
                </table>
            </li>
            <li> Enter the following values to control the behavior of the Pivotal HD Service Broker with respect to deploying instances of this Service Plan:<table
                    frame="void"
                    rules="all">
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
                            <td>(Required) Limits the number of instances that PCF users can create.  Use this field to ensure that the Pivotal HD Service Broker does not oversubscribe the underlying IaaS resources. </td>
                            <td>Integer<ul>
                                    <li>Minimum: 1</li>
                                </ul></td>
                        </tr>
                        <tr>
                            <td> Number of Pre-Created Instances</td>
                            <td>(Required) The Pivotal HD Service Broker pre-creates a pool of Service Instances to allocate to PCF users on-demand.  This field defines how many Service Plan instances the Pivotal HD Service Broker pre-creates.<p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">When a Service Instance is allocated to a PCF user, the Service Broker back-fills the pool.</p><p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">If all Service Instances are allocated and the Service Broker has not finished deploying a new one to the pool, PCF users will temporarily be unable to create a new Service Instance.</p><p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">The more instances that are pre-created, the more concurrent requests the Service Broker can satisfy.</p><p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">The Service Broker never pre-creates more instances than the configured Maximum Number of Instances. </p></td>
                            <td>Integer<ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: Maximum Number of Instances Created (configuration value, see above)</li>
                                </ul></td>
                        </tr>
                    </tbody>
                </table></li>
            <li> Choose which Pivotal HD Components you wish to deploy as a part of each instance of the Service Plan.  <p>For more information about Pivotal HD and its components, see the <a
                        href="http://pivotalhd-210.docs.pivotal.io/doc/2010/index.html">Pivotal HD Documentation</a> .</p><table rules="all"
                    frame="void">
                    <caption>Pivotal HD Components</caption>
                    <col
                        width="25%" />
                    <col
                        width="75%" />
                    <thead>
                        <tr>
                            <th>Component</th>
                            <th>Description</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><b>HDFS</b></td>
                            <td>
                                <p> Controls whether to deploy a virtual machine that runs the HDFS NameNode process.  Also controls whether to include the HDFS DataNode process on each Pivotal HD Slave virtual machine. </p>
								<p>HDFS cannot be the only included component.  If HDFS is the only component selected, the Pivotal HD Service Broker will not register the Service Plan.</p>
                            </td>
                        </tr>
                        <tr>
                            <td><b>Yarn/MapReduce2</b></td>
                            <td>
                                <p> Controls whether to deploy a virtual machine that runs the YARN/MapReduce2 ResourceManager and Job History Server processes.  Also controls whether to include the YARN/MapReduce2 NodeManager process on each Pivotal HD Slave virtual machine.</p>
                                <p>YARN/MapReduce2 depends on HDFS. If it is included but HDFS is not included, you must specify the Isilon HDFS NameNode Host Address and Port for the Service Plan to function </p>
                            </td>
                        </tr>
                        <tr>
                            <td><b>HAWQ</b></td>
                            <td>
                                <p> Controls whether to deploy a virtual machine that runs the HAWQ Master and PXF processes.  Also controls whether to include the HAWQ Segment Server process on each Pivotal HD Slave virtual machine.</p>
                                <p>HAWQ depends on HDFS. If it is included but HDFS is not included, you must specify the Isilon HDFS NameNode, Host Address, and Port for the Service Plan to function. </p>
                            </td>
                        </tr>
                        <tr>
                            <td><b>GemFire XD</b></td>
                            <td>
                                <p> Controls whether to deploy a virtual machine that runs the GemFire XD Locator process.  Also controls whether to include the GemFire XD server process on each Pivotal HD slave virtual machine.</p>
                                <p>GemFire XD does not depend on HDFS.  You may exclude HDFS without specifying the Isilon HDFS NameNode Host Address and Port if GemFire XD is the only component you are including. </p>
                            </td>
                        </tr>
                    </tbody>
                </table><table
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
                            <td>Number of PHD Slaves</td>
                            <td>(Required)  Controls the number of virtual machines created that each run all applicable slave/clustered processes for the components included in the Service Plan.  <p>Example: If HDFS and Yarn/MapReduce2 are included, then the slave runs the HDFS DataNode and YARN/MapReduce2 NodeManager processes. </p></td>
                            <td>Integer<p>Minimum: 1</p></td>
                        </tr>
                        <tr>
                            <td>PHD Slave CPU</td>
                            <td>(Required) Amount of virtual CPU cores to allocate to each virtual machine. </td>
                            <td>Integer<ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64</li>
                                </ul></td>
                        </tr>
                        <tr>
                            <td>PHD Slave RAM in MB </td>
                            <td>(Required) Amount of memory to allocate to each virtual machine. </td>
                            <td>Integer<ul>
                                    <li>Minimum: 8192</li>
                                    <li>Maximum: 1048576 </li>
                                </ul></td>
                        </tr>
                        <tr>
                            <td>PHD Slave Persistent Disk in MB </td>
                            <td>(Required) Amount of disk space to allocate to each virtual machine. </td>
                            <td>
                                <ul>
                                    <li>Minimum: 12288</li>
                                    <li>Maximum: 999999  </li>
                                </ul>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </li>
            <li> (Optional) If you don’t plan to deploy the HDFS component, fill in the fields further down in this form to define the Isilon HDFS instance you want each Service Instance’s YARN/MapReduce 2 or HAWQ processes to use.  For more information about using Isilon on HDFS, see <a
                    href="overview.html#isilon"
                   >HDFS Isilon Integration</a>.<table rules="all"
                    frame="void">
                    <caption>Isilon Configuration</caption>
                    <col
                        width="25%" />
                    <col
                        width="25%" />
                    <col
                        width="25%" />
                    <col
                        width="25%" />
                    <thead>
                        <tr>
                            <th>Parameter</th>
                            <th>Description</th>
                            <th>Value</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td> Isilon HDFS NameNode Host Address </td>
                            <td> The IP Address or hostname where Isilon is running.  Example: <code>myIsilon.instance.com</code><p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">If the HDFS component is included, this field is ignored.</p><p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">If the HDFS component is not included and this field is blank, the Pivotal HD Service Broker will not register this Service Plan </p></td>
                            <td>String</td>
                        </tr>
                        <tr>
                            <td> Isilon HDFS NameNode Port </td>
                            <td> The port that Isilon is running the HDFS protocol on.  Typically this is 8020.<p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">If HDFS component is included, this field is ignored.</p><p
                                    dir="ltr"
                                    style="line-height:1;margin-top:0pt;margin-bottom:0pt;">If HDFS component is not included and this field is blank, the Pivotal HD Service Broker will not register this Service Plan. </p></td>
                            <td>Integer</td>
                        </tr>
                    </tbody>
                </table></li>
            <li> (Optional) Revise the values in the remaining fields if you want to change the default resources used by the Service Instance’s virtual machines that the Pivotal HD Service Broker will create depending on which components are included in the Service Plan.<table rules="all"
            frame="void">
            <caption>Virtual Machine Resources</caption>
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
                    <td>NameNode CPU</td>
                    <td>The NameNode runs on its own dedicated virtual machine.</td>
                    <td>Integer<ul>
                        <li>Minimum: 1</li>
                        <li>Maximum: 64 </li>
                    </ul></td>
                </tr>
                <tr>
                    <td>NameNode RAM in MB </td>
                    <td>Amount of memory to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 2048</li>
                                    <li>Maximum: 1048576 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td>NameNode Persistent Disk in MB</td>
                    <td>Amount of disk space to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                        <li>Minimum: 8192</li>
                        <li>Maximum: 999999 </li>
                    </ul></td>
                </tr>
                <tr>
                    <td>ResourceManager CPU </td>
                    <td>Number of virtual CPU cores to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                        <li>Minimum: 1</li>
                        <li>Maximum: 64 </li>

                    </ul></td>
                </tr>
                <tr>
                    <td>ResourceManager RAM in MB </td>
                    <td> Amount of memory to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                        <li>Minimum: 2048</li>
                        <li>Maximum: 1048576 </li>

                    </ul></td>
                </tr>
                <tr>
                    <td>ResourceManager Ephemeral Disk in MB </td>
                    <td> Amount of disk space to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 5120</li>
                                    <li>Maximum: 999999 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td>HAWQ Master CPU</td>
                    <td>Number of virtual CPU cores to allocate to each virtual machine.  </td>
                    <td>Integer<ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td> HAWQ Master RAM in MB </td>
                    <td> Amount of memory to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 2048</li>
                                    <li>Maximum: 1048576 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td>HAWQ Master Persistent Disk in MB </td>
                    <td> Amount of disk space to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 4096</li>
                                    <li>Maximum: 999999 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td>Gemfire XD Locator CPU</td>
                    <td> Number of virtual CPU cores to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 1</li>
                                    <li>Maximum: 64 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td>Gemfire XD Locator RAM in MB</td>
                    <td> Amount of memory to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 1024</li>
                                    <li>Maximum: 1048576 </li>
                                </ul></td>
                </tr>
                <tr>
                    <td>Gemfire XD Locator Persistent Disk in MB </td>
                    <td> Amount of disk space to allocate to each virtual machine. </td>
                    <td>Integer<ul>
                                    <li>Minimum: 3072</li>
                                    <li>Maximum: 999999 </li>
                                </ul></td>
                </tr>
            </tbody>
        </table></li>
            <li>Click the <strong>Save</strong> button.</li>


</ol>

<a id="modifying"></a>
#Modifying an On-Demand Service Plan

<p><strong>Note:</strong> Modifications to the default On-Demand service plan settings only apply to any new <em>new</em> service instances that users create. If you modify the service plan, any pre-created service instances are destroyed and new, pre-allocated instances are created with the new configurations. Existing service instances are not modified.</p>

<p>To modify an On-Demand Service Plan:

<ol>
<li>
<p>Use a Web browser to open the <strong>Pivotal Ops Manager</strong> application. (This application is part of your Pivotal Cloud Foundry&reg; installation.)</p>
</li>
<li>Click the <strong>Pivotal HD for PCF</strong> tile. </li>
<li>
 <p>Click <strong>On-demand Service Plans</strong>.</p>
 <p>The <strong>On-demand Service Plans</strong> screen displays.</p>
</li>
<li>Click the name of the On-Demand Service plan that you want to modify.<p>A form expands below its name where you can change the configuration values. </p>
<li>Change any of the fields that define the service plan.</li>
<li>Click the <strong>Save</strong> button.</li>
</ol>