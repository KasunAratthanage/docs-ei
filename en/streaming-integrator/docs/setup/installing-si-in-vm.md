# Installing the Streaming Integrator in a Virtual Machine

Follow the steps given below to install and run WSO2 Streaming Integrator on a VM.

## System requirements

| Type   | Requirement                                                                                     |
|--------|-------------------------------------------------------------------------------------------------|
| CPU    | You require a minimum of one CPU with 2 cores. It is recommended to have a CPU with 4 cores.    |
| Memory | ~ 4 GB minimum is recommended</br> </br>  ~ 2 GB heap size                                      |
| Disk   | ~ 1 GB minimum (excluding space allocated for log files and databases.)                         |

## Installing the Streaming Integrator

Follow the steps below:

1. Go to the Streaming Integrator [product page](https://wso2.com/integration/streaming-integrator/) and click **Download** to get the **product installer**. The installer that is compatible with your operating system is downloaded.

    !!! Info
        Alternatively, go to **Other Installation Options** and click **Binary** to download the product distribution as a ZIP file.

2. If you used the installer, double-click to open the installation wizard that guides you through the installation. When you finish, the product is installed and ready for use.

### Accessing the HOME directory

Let's call the installation location of your product the **`<SI_HOME>`** directory.

If you used the **installer** to install the product, this is located in a place specific to your OS as shown below:

<table style="width:100%;">
   <colgroup>
      <col style="width: 9%" />
      <col style="width: 90%" />
   </colgroup>
   <thead>
      <tr class="header">
         <th>OS</th>
         <th>Home directory</th>
      </tr>
   </thead>
   <tbody>
      <tr class="odd">
         <td>Mac OS</td>
         <td><code>/Library/WSO2/EnterpriseIntegrator/7.0.2/streaming-integrator</code></td>
      </tr>
      <tr class="even">
         <td>Windows</td>
         <td><code>C:\Program Files\WSO2\Enterprise Integrator\7.0.2\streaming-integrator</code></td>
      </tr>
      <tr class="odd">
         <td>Ubuntu</td>
         <td><code>/usr/lib/wso2/wso2ei/7.0.2/streaming-integrator</code></td>
      </tr>
      <tr class="even">
         <td>CentOS</td>
         <td><code>/usr/lib64/wso2/wso2ei/7.0.2/streaming-integrator</code></td>
      </tr>
   </tbody>
</table>

### Uninstalling the product

If you used the **installer** to install the product, you can uninstall by following the steps given below:

<table>
<thead>
<tr class="header">
<th>OS</th>
<th>Instructions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Mac OS</td>
<td><div class="content-wrapper">
<p>Open a terminal and run the following command as the root user:</p>
    <code>sudo bash /Library/WSO2/EnterpriseIntegrator/7.0.2</code>
</div>
</div>
</div></td>
</tr>
<tr class="even">
<td>Windows</td>
<td>Go to <strong>Start Menu -&gt; Programs -&gt; WSO2 -&gt; Uninstall Enterprise Integrator 7.0.2</strong> or search <strong>Uninstall Enterprise Integrator 7.0.2</strong> and click the shortcut icon. This uninstalls the product from your computer.</td>
</tr>
<tr class="odd">
<td>Ubuntu</td>
<td><div class="content-wrapper">
<p>Open a terminal and run the following command:</p>
    <code>sudo apt purge wso2ei-7.0.2</code>
</div>
</div>
</div></td>
</tr>
<tr class="even">
<td>CentOS</td>
<td><div class="content-wrapper">
<p>Open a terminal and run the following command:</p>
    <code>sudo yum remove wso2ei-7.0.2</code>
</div>
</div>
</div></td>
</tr>
</tbody>
</table>

## Running the Streaming Integrator

Start the WSO2 Streaming Integrator by following the instructions given below.

### Using the installer

* On **MacOS/Linux/CentOS**, open a terminal and execute the command given below.
  ```bash
  sudo wso2si
  ```
  The operation log keeps running until the profile starts, which usually
       takes several seconds. Wait until the profile fully boots up and
       displays a message similar to " *WSO2 Carbon started in n seconds.* "

* On **Windows**, go to **Start Menu -> Programs -> WSO2 -> Enterprise Integrator**. This
opens a terminal and start the relevant profile.

If you have **installed the product using the installer** and you want to manually run the product startup script from the `<SI_HOME/bin>` directory, you need to issue the following command:

```bash
sudo sh launcher_streaming-integrator.sh
```
This script automatically assigns the JAVA_HOME of your VM to the root user of your Streaming Integrator instance.

### Using the binary distribution

1. Before you execute the product startup script, be sure to set the JAVA HOME in your machine. Use a [JDK that is compatible with WSO2 Enterprise Integrator](https://docs.wso2.com/display/compatibility/Tested+Operating+Systems+and+JDKs).

2. Open a terminal and navigate to the `<SI_HOME>/bin/` directory, where `<SI_HOME>` is the home directory of the distribution you downloaded.

3. Execute the relevant command.

    * On **MacOS/Linux/CentOS**
      ```bash
      sh server.sh
      ```


    * On **Windows**
      ```bash
      server.bat
      ```

By default, the HTTP listener port is 8290 and the default HTTPS
listener port is 8253.

## Stopping the Streaming Integrator

To stop the Streaming Integrator runtime, press Ctrl+C in the command
window.

## What's Next?

Once you have successfully downloaded and installed WSO2 Streaming Integrator, you can proceed to do any of the following:

- If you were previously using WSO2 Stream Processor and want to migrate to WSO2 Streaming Integrator, follow the instructions in [Migrating from WSO2 Stream Processor](migrating-from-stream-processor.md).

- To deploy WSO2 Streaming Integrator as a single-node deployment or a cluster (based on your requirements), see [Deploying Streaming Integrator](deployment-guide.md).

- To set up WSO2 Streaming Integrator and make it ready to run in a production environment, see the [Production Checklist](production-checklist.md).
    