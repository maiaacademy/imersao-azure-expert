# Imersao Azure Expert 2.0

Hands-on Lab

## Day 1
## Exercise #01 - Azure Calculator (20 minutes)

1. In a browser, navigate to the [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/) webpage.

2. Add the inventory data.

   ![Screenshot of the inventory data](/AllFiles/Images/IMG01.png)

**Important Notes**
- Development environment licensing will be purchased by Marketplace
- Include Reserved instances and Azure Hybrid Benefit in the Production Environment 
- Include VPN Gateway, Load Balancers, Public IP Address and 500 GB Outbound Data Transfer.

3. Scroll to the bottom of the Azure Pricing Calculator webpage to view total Estimated monthly cost.

4. Change the currency to Brazilian Real (R$), then select Export to download a copy of the estimate for offline viewing in Microsoft Excel (.xlsx) format.

## Exercise #02 - TCO Calculator (15 minutes) 

1. In a browser, navigate to the [Total Cost of Ownership (TCO) Calculator](https://azure.microsoft.com/en-us/pricing/tco/calculator/) page.

2. To add details of your on-premises server infrastructure, click **+ Add server workload** in the **Define your workloads** pane.

    | Settings | Value |
    | -- | -- |
    | Name | **Servers: Windows VMs** |
    | Workload | **Windows/Linux server** |
    | Environment | **Virtual Machines** |
    | Operating system | **Windows** |  
    | VMs | **50** |
    | Virtualization | **Hyper-V** |
    | Core(s) | **8**|
    | RAM (GB) | **16** |
    | Optimize by | **CPU** |
    | Windows Server 2008/2008 R2 | **Off** |
    | | |

3. Select **+ Add server workload** to make a row for a new server workloads definition. 

    | Settings | Value |
    | -- | -- |
    | Name | **Servers: Linux VMs** |
    | Workload | **Windows/Linux server** |
    | Environment | **Virtual Machines** |
    | Operating system | **Linux** |  
    | VMs | **20** |
    | Virtualization | **VMware** |
    | Core(s) | **8**|
    | RAM (GB) | **16** |
    | Optimize by | **CPU** |
    | Windows Server 2008/2008 R2 | **Off** |
    | | |

4. In the **Storage** pane, click **Add storage**.

    | Settings | Value |
    | -- | -- |
    | Name | **Server Storage** |
    | Storage type | **Local Disk/SAN** |
    | Disk type | **HDD** |
    | Capacity | **30 TB** |  
    | Backup | **50 TB** |
    | Archive | **0 TB** |
    | | |

5. In the **Networking** pane, add bandwidth. 

    | Settings | Value |
    | -- | -- |
    | Outbound bandwidth | 5 TB|
    | | |

6. Click **Next**.

7. Explore the options and make any adjustments that you require. 

    | Settings | Value |
    | -- | -- |
    | Currency | **Brazilian Real (R$)** |
    | | |

8. Click **Next**.

9. Review the Azure cost saving recommendations and visualizations.

    | Settings | Value |
    | -- | -- |
    | Timeframe| **3 years** |
    | Region | **Brazil South** |
    | | |

10. To save or print a PDF copy of the report, click **Download**.

## Lab #01 - Resource Groups (15 minutes)

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Search for and select **Resource groups**. 

1. On the **Resource groups** blade, click **+ Add** and create a resource group with the following settings:

    |Setting|Value|
    |---|---|
    |Subscription| the name of the Azure subscription you will use in this lab |
    |Resource Group| **RGNAME-VMS**|
    |Region| East US 2 |
    |Tags| environment: resource, project: azureexpert |
    | | |

1. Repeat and create the Resources groups name "RGNAME-NETWORKING" and "RGNAME-STORAGE".

1. Click **Review + Create** and then click **Create**.

1. Explore properties to Resource groups.

## Lab #02 - Virtual Networks (20 minutes)

1. In the Azure portal, search for and select **Virtual networks**, and, on the **Virtual networks** blade, click **+ Add**.

1. Create a virtual network with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you will be using in this lab |
    | Resource Group | the name of a resource group **RGNAME-NETWORK** |
    | Name | **VNETNAME-HUB** |
    | Region | the name of any Azure region available in the subscription you will use in this lab |
    | IPv4 address space | **10.1.0.0/16** |
    | Subnet name | **Default** |
    | Subnet address range | **10.1.1.0/24** |
     | | |
      
1. Accept the defaults and click **Review and Create**. Let validation occur, and hit **Create** again to submit your deployment.

1. Once the deployment completes browse for **Virtual Networks** in the portal search bar. Within **Virtual networks** blade, click on the newly created virtual network.

1. On the virtual network blade, click **Subnets** and then click **+ Subnet**. 

1. Create a subnet with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Name | **FrontEnd** |
    | Address range (CIDR block) | **10.1.100.0/24** |
    | Network security group | **None** |
    | Route table | **None** |
    | | |

## Lab #03 - Virtual Machine (30 minutes)

1. In the Azure portal, search for and select **Virtual machines** and, on the **Virtual machines** blade, click **+ Add**.

1. On the **Basics** tab of the **Create a virtual machine** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Subscription | the name of the Azure subscription you will be using in this lab |
    | Resource group | the name of a new resource group **RGNAME-VMS** |
    | Virtual machine name | **VMNAME01** |
    | Region | select same region the Resouce group | 
    | Availability options | **Availability sets** |
    | Availability set | **AS-VM** |
    | Image | **Windows Server 2019 Datacenter - Gen1** |
    | Azure Spot instance | **No** |
    | Size | **Standard_B2s** |
    | Username | **admaz** |
    | Password | **Azur3Exp3rt*** |
    | Public inbound ports | **RDP (3389) and HTTP (80)** |
    | Would you like to use an existing Windows Server license? | **No** |
    | | |

1. Click **Next: Disks >** and, on the **Disks** tab of the **Create a virtual machine** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | OS disk type | **Standard SSD** |
    | Enable Ultra Disk compatibility | **No** |

1. Click **OK** and, back on the **Networking** tab of the **Create a virtual machine** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Virtual Network | **VNETNAME** |
    | Subnet | **FrontEnd** |
    | Public IP | **VMNAME01-PI** |
    | NIC network security group | **Basic** |
    | Accelerated networking | **Off** |
	| Inbound Ports | **RDP (3389)** and HTTP (80)|
    | Place this virtual machine behind an existing load balancing solution? | **No** |
    | | |

1. Click **Next: Management >** and, on the **Management** tab of the **Create a virtual machine** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Boot diagnostics | **Enable with custom storage account** |
    | Diagnostics storage account | create new |
    | Properties storage account | Name: saflndiag, Account kind: StorageV2, Performance: Standard, Replication: Locally-redundant-storage (LRS) |
    | Enable auto-shutdown | off    
    
1. Click **Next: Advanced >**, on the **Advanced** tab of the **Create a virtual machine** blade, review the available settings without modifying any of them, and click **Review + Create**.

1. On the **Review + Create** blade, click **Create**.

1. Connect Virtual machine.

1. On the virtual machine blade, click **Disks**, Under **Data disks** click **+ Create and attach a new disk**. 

1. Create a managed disk with the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Disk name | **VMNAME01-DataDisk01** |
    | Source type | **None** |
    | Account type | **Premium SSD** |
    | Size | **50 GiB** |
    | | |

1. Connect Virtual machine and start disk.

1. Install the Web-Server feature in the virtual machine by running the following command in the **Administrator Windows PowerShell** command prompt. You can copy and paste this command.

   ```powershell
   Install-WindowsFeature -name Web-Server -IncludeManagementTools
   ```
1. Back in the portal, navigate back to the Overview blade of myVM and, use the Click to clipboard button to copy the public IP address, open a new browser tab, paste the public IP address into the URL text box, and press the Enter key to browse to it.

1. Explore properties to Virtual machines.

## Lab #04 - Azure Storage Blobs (20 minutes)

1. In the Azure portal, search for and select **Storage accounts** and, on the **Storage accounts** blade, select **+ Add**.

1. On the **Basics** tab of the **Create storage account** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | the name of a new resource group **storageaccountname01** |
    | Storage account name | any globally unique name between 3 and 24 in length consisting of letters and digits |
    | Location | the name of an Azure region where you can create an Azure Storage account  |
    | Performance | **Standard** |
    | Account kind | **StorageV2 (general purpose v2)** |
    | Replication | **Locally redundant storage (LRS)** |

1. Select **Next: Networking >**, on the **Networking** tab of the **Create storage account** blade, review the available options, accept the default option **Public endpoint (all networks}** and select **Next: Data protection >**.

1. On the **Data protection** tab of the **Create storage account** blade, review the available options, accept the defaults, select **Next: Advanced >**.

1. On the **Advanced** tab of the **Create storage account** blade, review the available options, accept the defaults, select **Review + Create**, wait for the validation process to complete and select **Create**.

1. On the Storage account blade, in the Blob service section, click Containers.

1. Select **Create Blob Container**, and use the empty text box to set the container name to **container1**.

1. Select **container1**, in the **container1** pane, select **Upload**, and in the drop-down list, select **Upload Files**.

1. In the **Upload Files** window, select the ellipsis button next to the **Selected files** label, in the **Choose files to upload** window, select **files**, and select **Open**.

1. Back in the **Upload Files** window, select **Upload**

1. Within the Remote Desktop session to **Virtual machine**, in the Server Manager window, select **Local Server**, select the **On** link next to the **IE Enhanced Security Configuration** label, and, in the **IE Enhanced Security Configuration** dialog box, select both **Off** options.

1. Within the Remote Desktop session, start Browser and navigate to the download page of [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/)

1. Within the Remote Desktop session, download and install Azure Storage Explorer with the default settings. 

1. Navigate to the [Azure portal](https://portal.azure.com), and sign-in by providing credentials of the user account with the Owner role in the subscription you are using in this lab.

1. Navigate to the blade of the newly created storage account, select **Access keys** and review the settings of the target blade.

1. On the storage account blade, select **Shared access signature** and review the settings of the target blade.

1. On the resulting blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Allowed services | **Blob** |
    | Allowed resource types | **Service**, **Container** and **Object** |
    | Allowed permissions | **Read**, **List** |
    | Blob versioning permissions | disabled |
    | Start | 24 hours before the current time in your current time zone | 
    | End | 24 hours after the current time in your current time zone |
    | Allowed protocols | **HTTPS only** |
    | Signing key | **key1** |

1. Select **Generate SAS and connection string**.

1. Copy the value of **Blob service SAS URL** into Clipboard.

1. Within the Remote Desktop session, start Azure Storage Explorer. 

1. In the Azure Storage Explorer window, in the **Connect to Azure Storage** window, select **Use a shared access signature (SAS) URI** and select **Next**.

1. In the **Attach with SAS URI** window, in the **Display name** text box, type **storageaccountname01**, in the **URI** text box, paste the value you copied into Clipboard, and select **Next**. 

    >**Note**: This should automatically populate the value of **Blob endpoint** text box.

1. In the **Connection Summary** window, select **Connect**. 

1. Select **Storage account" and "Blob containers", Open and download uploaded files

1. Leave the Azure Storage Explorer window open.

## Lab #05 - Azure Files (15 minutes)

1. In the Azure portal, navigate back to the blade of the storage account you created in the first task of this lab and, in the **File service** section, click **File shares**.

1. Click **+ File share** and create a file share with the following settings:

    | Setting | Value |
    | --- | --- |
    | Name | **fs-azureexpert** |
    | Quota | **1024** |
    | Tiers | hot |

1. Click the newly created file share and click **Connect**.

1. On the **Connect** blade, ensure that the **Windows** tab is selected, and click **Copy to clipboard**.

1. In the Azure portal, search for and select **Virtual machines**, and, in the list of virtual machines.

1. In the Virtual Machine Connection window, start Windows PowerShell and, in the **Administrator: Windows PowerShell** window run the following to set map share. 

1. Verify that the script completed successfully. 

1. Connect share and upload files.

## Lab #06 - Azure VNET Peering (30 minutes)

1. In the Azure portal, search for and select **Virtual networks**, and, on the **Virtual networks** blade, click **+ Add**.

1. Create a virtual network with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you will be using in this lab |
    | Resource Group | the name of a resource group **RGNAME-SPOKE1** |
    | Name | **VNETNAME-SPOKE1** |
    | Region | west us 2 |
    | IPv4 address space | **10.10.0.0/16** |
    | Subnet name | **Default** |
    | Subnet address range | **10.10.1.0/24** |
     | | |
      
1. Accept the defaults and click **Review and Create**. Let validation occur, and hit **Create** again to submit your deployment.

1. Once the deployment completes browse for **Virtual Networks** in the portal search bar. Within **Virtual networks** blade, click on the newly created virtual network.

1. In the Azure portal, search for and select **Virtual machines**

1. On the **Virtual machines**, click **Add** and create a new Virtual machine, on the **VMNAMESPOKE1**.

1. In the Azure portal, search for and select **Virtual networks**.

1. In the list of virtual networks, click **VNETNAME-SPOKE1**.

1. On the **VNETNAME-SPOKE1** virtual network blade, in the **Settings** section, click **Peerings** and then click **+ Add**.

1. Specify the following settings (leave others with their default values) and click **Add**:

    | Setting | Value|
    | --- | --- |
    | This virtual network: Peering link name | **To-Hub** |
    | This virtual network: Traffic to remote virtual network | **Allow (default)** |
    | This virtual network: Traffic forwarded from remote virtual network | **Allow (default)** |
    | Virtual network gateway | **None** |
    | Remote virtual network: Peering link name | **To-Spoke1** |    
    | Virtual network deployment model | **Resource manager** |
    | I know my resource ID | unselected |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Virtual network | **VNETNAME-HUB** |
    | Traffic to remote virtual network | **Allow (default)** |
    | Traffic forwarded from remote virtual network | **None** |
    | Virtual network gateway | **Use this virtual network's gateway** |

1. On the **VNETNAME-HUB** virtual network blade, in the **Settings** section, click **Peerings** and then click **+ Add**.

1. Add a peering with the following settings (leave others with their default values):

    | Setting | Value|
    | --- | --- |
    | This virtual network: Peering link name | **To-Spoke1** |
    | This virtual network: Traffic to remote virtual network | **Allow (default)** |
    | This virtual network: Traffic forwarded from remote virtual network | ****Allow (default)**** |
    | Virtual network gateway | **None*** |
    | Remote virtual network: Peering link name | **To-Hub** |    
    | Virtual network deployment model | **Resource manager** |
    | I know my resource ID | unselected |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Virtual network | **VNETNAME-HUB** |
    | Traffic to remote virtual network | **Allow (default)** |
    | Traffic forwarded from remote virtual network | **Allow (default)** |
    | Virtual network gateway | **None** |

1. At the top of the Azure portal, enter the name of a **VMNAMESPOKE1** that is in the running state, in the search box. When the name of the VM appears in the search results, select it.

1. Under Settings on the left, select **Networking**, and navigate to the network interface resource by selecting its name. View network interfaces.

1. On the left, select **Effective routes**. The effective routes for a network interface are shown.
    
1. In the Azure portal, search for and select **Virtual machines** on the Virtual Network Hub.

1. On the **Virtual machine** blade, click **Connect**, in the drop-down menu, click **RDP**, on the **Connect with RDP** blade, click **Download RDP File** and follow the prompts to start the Remote Desktop session.

1. Within the Remote Desktop session to **Virtual machine**, right-click the **Start** button and, in the right-click menu, click **Windows PowerShell (Admin)**.

1. In the Windows PowerShell console window, run the following to test connectivity to **VNETNAME-SPOKE1**.

   ```pwsh
   Test-NetConnection -ComputerName IPADDRESS-VM-HUB -Port 3389 -InformationLevel 'Detailed'
   ```
    >**Note**: The test uses TCP 3389 since this is this port is allowed by default by operating system firewall. 

1. Examine the output of the command and verify that the connection was successful.

1. In the Windows PowerShell console window, run the following to test connectivity to **VMNAME-HUB** 

   ```pwsh
   Test-NetConnection -ComputerName IPADDRESS-VM-SPOKE -Port 3389 -InformationLevel 'Detailed'
   ```
1. Examine the output of the command and verify that the connection was successful.

## Lab #07 - Network Security groups (20 minutes)

1. In the Azure portal, navigate back to the resource group blade, and in the list of its resources, click **Virtual machine**.

1. On the **Virtual machine** blade, click **Connect**, in the drop-down menu, click **RDP**, on the **Connect with RDP** blade, click **Download RDP File** and follow the prompts to start the Remote Desktop session.

1. In the Azure portal, search for and select **Network security groups**, and, on the **Network security groups** blade, click **+ Add**.

1. Create a network security group with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource Group | **RGNAME-NETWORK** |
    | Name | **NSG-WEB** |
    | Region | the name of the Azure region where you deployed all other resources in this lab |

1. On the deployment blade, click **Go to resource** to open the **NSG-WEB** network security group blade. 

1. On the **NSG-WEB** network security group blade, in the **Settings** section, click **Inbound security rules**. 

1. Add an inbound rule with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Source | **Any** |
    | Source port ranges | * |
    | Destination | **Any** |
    | Destination port ranges | **80,443** |
    | Protocol | **TCP** |
    | Action | **Allow** |
    | Priority | **200** |
    | Name | **Allow-Port_80-443** |

1. On the **NSG-WEB** network security group blade, in the **Settings** section, click **Network interfaces** and then click **+ Associate**.

1. Associate the **NSG_WEB** network security group with the **Network interface**.

    >**Note**: It may take up to 5 minutes for the rules from the newly created Network Security Group to be applied to the Network Interface Card.

1. Go to the Azure portal to view your **Network security groups**. Search for and select Network security groups.

1. Select the name of your Network security group.

**Note:** If necessary desatch associated Network security groups.

1. In the menu bar of the network security group, under Settings, you can view the Inbound security rules, Outbound security rules, Network interfaces, and Subnets that the network security group is associated to.

1. Under **Support + troubleshooting**, you can view Effective security rules.

1. Navigate back to computer.

1. In the Virtual Machine Connection window, start Windows PowerShell and, in the **Administrator: Windows PowerShell** window run the following to set connection test. 

   ```powershell
   Test-NetConnection -ComputerName PUBLICIPADDRESS-VM -Port 80 -InformationLevel 'Detailed'
   ```
1. Examine the output of the command and verify that the connection was successful.

1. Within the computer, start Browser and navigate to **PUBLICIPADDPRESS-VM**.

1. Examine the navegate was successful.

## Project #01 - Hub-spoke Archicture (60 minutes)

Implement a Hub-spoke topology

   ![Screenshot of the Hub-spoke](/AllFiles/Images/IMG02.png)

**Important Notes**
- Gateway VPN on the hub network
- Virtual machines on the spoke network running Ubuntu server
- VNET Peering connection in the hub to allow gateway transit
- VNET Peering connection in each spoke to use remote gateways
- VNET Peering connections to allow forwarded 
traffic
- Custom Route tables to address prefix "0.0.0.0" and next hop type to virtual applicance
- Network rule Azure Firewall all traffic
- DNAT rules Azure Firewall to destination ports RDP (3389).

References: [Hub-spoke network topology](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke)

1. End of day 1.

## Day 2

## Lab #01 - Azure Load Balancer (30 minutes)

1. Sign in to the [Azure portal](http://portal.azure.com).

1. In the Azure portal, search for and select **Virtual machines** and, on the **Virtual machines** blade, click **+ Add**.

1. On the **Basics** tab of the **Create a virtual machine** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Subscription | the name of the Azure subscription you will be using in this lab |
    | Resource group | the name of a new resource group **RGNAME-VMSM** |
    | Virtual machine name | **VMWEB01** and **VMWEB02** |
    | Region | select one of the regions that support availability zones and where you can provision Azure virtual machines | 
    | Availability options | **Availability zone** |
    | Availability zone | **1** and **2** |
    | Image | **Windows Server 2019 Datacenter - Gen1** |
    | Azure Spot instance | **No** |
    | Size | **Standard B2s** |
    | Username | **admazz** |
    | Password | **Azur3Exp3rt*** |
    | Public inbound ports | **None** |
    | Would you like to use an existing Windows Server license? | **No** |

1. Complete deploy Virtual Machines

1. Check two Virtual machines create successful.

1. Connect Virtual machines.

1. Install the Web-Server feature and configure Static page in the virtual machines by running the following command in the **Administrator Windows PowerShell ISE** command prompt. You can copy and paste this command.

   ```powershell
   # Install Web server
   Install-WindowsFeature -name Web-Server -IncludeManagementTools
   # Remove default Web page
   Remove-item  C:\inetpub\wwwroot\iisstart.htm
   # Configure new Web page
   Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Azure Expert VM is running " + $env:computername)
   ```

**Note**
Test open Browser to IP Address the Virtual machines.

1. In the Azure portal, search and select **Load balancers** and, on the **Load balancers** blade, click **+ Add**.

1. Create a load balancer with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | the name of a new resource group **RGNAME-NETWORK** |
    | Name | **ALBNAME** |
    | Region| name of the Azure region into which you deployed all other resources in this lab |
    | Type | **Public** |
    | SKU | **Standard** |
    | Public IP address | **Create new** |
    | Public IP address name | **ALBNAME-PI** |
    | Availability zone | **Zone-redundant** |
    | Add a public IPv6 address | **No** |

    > **Note**: Wait for the Azure load balancer to be provisioned. This should take about 2 minutes. 

1. On the deployment blade, click **Go to resource**.

1. On the **ALBNAME** load balancer blade, click **Backend pools** and click **+ Add**.

1. Add a backend pool with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Name | **BP-WEB** |
    | Virtual network | **VNETNAME** |
    | IP version | **IPv4** |
    | Virtual machine | **VMWEB01** | 
    | Virtual machine IP address | associate IP address |
    | Virtual machine | **VMWEB02** |
    | Virtual machine IP address | associate IP address |

1. Wait for the backend pool to be created, click **Health probes**, and then click **+ Add**.

1. Add a health probe with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Name | **HP-WEB** |
    | Protocol | **TCP** |
    | Port | **80** |
    | Interval | **5** |
    | Unhealthy threshold | **2** |

1. Wait for the health probe to be created, click **Load balancing rules**, and then click **+ Add**.

1. Add a load balancing rule with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Name | **LBR-WEB** |
    | IP Version | **IPv4** |
    | Protocol | **TCP** |
    | Port | **80** |
    | Backend port | **80** |
    | Backend pool | **BPNAME** |
    | Health probe | **HPNAME** |
    | Session persistence | **None** |
    | Idle timeout (minutes) | **4** |
    | TCP reset | **Disabled** |
    | Floating IP (direct server return) | **Disabled** |
    | Use outbound rules to provide backend pool members access to the internet. | **Enabled** |

1. Wait for the load balancing rule to be created, click **Overview**, and note the value of the **Public IP address**.

1. Start browser window and navigate to the IP address you identified in the previous step.

1. Verify that the browser window displays the message **Static page and servername**.

1. In Virtual machines, select **VMWEB01 or VMWEB02** and click **Stop**. 

1. Open another browser window but this time by using InPrivate mode and verify whether the target vm changes (as indicated by the message).

## Lab #02 - Azure Virtual Machine Scale Sets (30 minutes)

1. Log in to the **Azure portal** at https://portal.azure.com.

1. Type **Scale set** in the search box. In the results, under **Marketplace**, select **Virtual machine scale sets**. Select **Create** on the **Virtual machine scale sets** page, which will open the **Create a virtual machine scale set** page.

1. In the **Basics** tab, under **Project details**, make sure the correct subscription is selected and then choose to **Create new** resource group. Type **RGNAME-VMS** for the name and then select **OK**.

1. Type **VMMSSWEB** as the name for your scale 
set.

1. In **Region**, select a region that is close to your area.

1. Leave the default value of **ScaleSet VMs** for **Orchestration mode**.
1. Select a marketplace image for **Image**.

1. Enter your desired username, and password.

1. Select **Next** to move the the other pages. 

1. Leave the defaults for the **Instance** and **Disks** pages.

1. On the **Networking** page, under **Load balancing**, select **Yes** to put the scale set instances behind a load balancer. 

1. In **Load balancing options**, select **Azure load balancer**.
1. In **Select a load balancer**, select **ALBNAME** that you created earlier.

1. For **Select a backend pool**, select **Create new**, type **BP-VMMSS*, then select **Create**.

1. When you are done, select **Review + create**. 

1. After it passes validation, select **Create** to deploy the scale set.

1. In a **Browser**, navigate to the Public IP Address the VMSS.

## Lab #03 - Azure App Service (30 minutes)

1. Sign in to the [**Azure portal**](http://portal.azure.com).

1. In the Azure portal, search for and select **App services**, and, on the **App Services** blade, click **+ Add**.

1. On the **Basics** tab of the **Web App** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- | ---|
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | the name of a new resource group **RGNAME** |
    | Web app name | any globally unique name |
    | Publish | **Code** |
    | Runtime stack | **PHP 7.3** |
    | Operating system | **Windows** |
    | Region | the name of an Azure region where you can provision Azure web apps |
    | App service plan | accept the default configuration |

1. Click **Next : Monitoring >**, on the **Monitoring** tab of the **Web App** blade, set the **Enable Application Insights** switch to **No**, click **Review + create**, and then click **Create**. 

    >**Note**: Typically, you would want to enable **Application Insights**, however, its functionality is not used in this lab.

    >**Note**: Wait until the web app is created before you proceed to the next task. This should take about a minute. 

1. On the deployment blade, click **Go to resource**.

1. On the blade of the newly deployed web app, click the **URL** link to display the default web page in a new browser tab.

1. Close the new browser tab and, back in the Azure portal, in the **Deployment** section of the web app blade, click **Deployment slots**. 

    >**Note**: The web app, at this point, has a single deployment slot labeled **PRODUCTION**. 

1. Click **+ Add slot**, and add a new slot with the following settings: 

    | Setting | Value |
    | --- | ---|
    | Name | **staging** |
    | Clone settings from | **Do not clone settings**|

1. Back on the **Deployment slots** blade of the web app, click the entry representing the newly created staging slot. 

    >**Note**: This will open the blade displaying the properties of the staging slot. 

1. Review the staging slot blade and note that its URL differs from the one assigned to the production slot.

1. On the staging deployment slot blade, in the **Deployment** section, click **Deployment Center**.

    >**Note:** Make sure you are on the staging slot blade (rather than the production slot).

1. In the **Continuous Deployment (CI/CD)** section, select **Local Git**, and then click **Continue**.

1. Select **App Service build service**, click **Continue**, and then click **Finish**. 

1. Copy the resulting **Git Clone Url** to Notepad.

    >**Note:** You will need the Git Clone Url value in the next task of this lab.

1. Click **Deployment Credentials** toolbar icon to display **Deployment Credentials** pane. 

1. Click **User credentials**.

1. Complete the required information, and then click **Save Credentials**. 

    | Setting | Value |
    | --- | ---|
    | User name | any unique name (must not contain `@` character) |
    | Password | any password that satisfies complexity requirements |
    
    >**Note:** The password must be at least eight characters long, with two of the following three elements: letters, numbers, and non-alphanumeric characters.

    >**Note:** You will need these credentials in the next task of this lab.

1. In the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. If prompted to select either **Bash** or **PowerShell**, select **PowerShell**. 

    >**Note**: If this is the first time you are starting **Cloud Shell** and you are presented with the **You have no storage mounted** message, select the subscription you are using in this lab, and click **Create storage**. 

1. From the Cloud Shell pane, run the following to clone the remote repository containing the code for the web app.

   ```pwsh
   git clone https://github.com/Azure-Samples/php-docs-hello-world
   ```
 
1. From the Cloud Shell pane, run the following to set the current location to the newly created clone of the local repository containing the sample web app code.

   ```
   Set-Location -Path $HOME/php-docs-hello-world/
   ```

1. From the Cloud Shell pane, run the following to add the remote git (make sure to replace the `[deployment_user_name]` and `[git_clone_url]` placeholders with the value of the **Deployment Credentials** user name and **Git Clone Url**, respectively, which you identified in previous task):

   ```
   git remote add [deployment_user_name] [git_clone_url]
   ```

    >**Note**: The value following `git remote add` does not have to match the **Deployment Credentials** user name, but has to be unique

1. From the Cloud Shell pane, run the following to push the sample web app code from the local repository to the Azure web app staging deployment slot (make sure to replace the `[deployment_user_name]` placeholder with the value of the **Deployment Credentials** user name, which you identified in previous task):
   ```
   git push [deployment_user_name] master
   ```

1. If prompted to authenticate, type the `[deployment_user_name]` and the corresponding password (which you set in the previous task).

1. Close the Cloud Shell pane.

1. On the staging slot blade, click **Overview** and then click the **URL** link to display the default web page in a new browser tab.

1. Verify that the browser page displays the **Hello World!** message and close the new tab.

In this task, you will swap the staging slot with the production slot

1. Navigate back to the blade displaying the production slot of the web app.

1. In the **Deployment** section, click **Deployment slots** and then, click **Swap** toolbar icon.

1. On the **Swap** blade, review the default settings and click **Swap**. 

1. Click **Overview** on the production slot blade of the web app and then click the **URL** link to display the web site home page in a new browser tab.

1. Verify the default web page has been replaced with the **Hello World!** page. 

## Lab #04 - Azure Container Instances (30 minutes)

## Lab #05 - Azure Kubernetes Service (30 minutes)

## Lab #06 - Azure Resource Manager (30 minutes)

## Project #02 - Multicontainer application to Kubernetes (60 minutes)

1. In a browser, navigate to the [Azure Kubernetes Service Workshop](https://docs.microsoft.com/en-us/learn/modules/aks-workshop/) webpage and start lab.

2. Application architecture.

   ![Screenshot of the application archicture](/AllFiles/Images/IMG03.png)

1. End of day 2.

## Day 3

## Lab #01 - Azure Backup (30 minutes)

## Lab #02 - Azure AD (20 minutes)

## Lab #03 - Azure RBAC and Azure Policy (20 minutes) 

## Lab #04 - Azure Monitor (30 minutes)

## Lab #05 - Azure SQL Database (30 minutes)

## OPTIONAL: Project #03 - Azure Site Recovery (60 minutes)

1. In a browser, navigate to the [Disaster Recovery with Azure Site Recovery](https://docs.microsoft.com/en-us/learn/modules/protect-infrastructure-with-site-recovery/) webpage and start lab.

2. Disaster Recovery architecture.

   ![Screenshot of the application archicture](/AllFiles/Images/IMG04.png)

1. End of day 3 and **Imersao Azure Azure Expert**.

1. Continue in the **Mentoria Arquito Cloud**.










