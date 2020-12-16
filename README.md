# Imersao Azure Expert 2.0

Hands-on Lab

## Exercise #01 - Azure Calculator (15 minutes)

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

1. Repeat and create the Resources groups name "RGNAME-Networking" and "RGNAME-Storage".

1. Click **Review + Create** and then click **Create**.

1. Explore properties to Resource groups.

## Lab #02 - Virtual Networks (20 minutes)

1. In the Azure portal, search for and select **Virtual networks**, and, on the **Virtual networks** blade, click **+ Add**.

1. Create a virtual network with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you will be using in this lab |
    | Resource Group | the name of a resource group **RG-FLN-Network** |
    | Name | **VNETNAME** |
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
    | Virtual machine name | **VMNAME** |
    | Region | select one of the regions that support availability zones and where you can provision Azure virtual machines | 
    | Availability options | **Availability sets** |
    | Availability set | **AS-VM** |
    | Image | **Windows Server 2019 Datacenter - Gen1** |
    | Azure Spot instance | **No** |
    | Size | **Standard_B2s** |
    | Username | **admaz** |
    | Password | **Azur3Exp3rt*** |
    | Public inbound ports | **RDP (3389)** |
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
    | Public IP | **VMNAME1-PI** |
    | NIC network security group | **Basic** |
    | Accelerated networking | **Off** |
	| Inbound Ports | **RDP (3389)** |
    | Place this virtual machine behind an existing load balancing solution? | **No** |
    | | |

1. Click **Next: Management >** and, on the **Management** tab of the **Create a virtual machine** blade, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Boot diagnostics | **Enable with custom storage account** |
    | Diagnostics storage account | create new |
    | Properties stora account | Name: saflndiag, Account kind: StorageV2, Performance: Standard, Replication: Locally-redundant-storage (LRS) |
    | Enable auto-shutdown | off
      
    >**Note**: Record the name of diagnostics storage account. You will use it in the next task. 
    
1. Click **Next: Advanced >**, on the **Advanced** tab of the **Create a virtual machine** blade, review the available settings without modifying any of them, and click **Review + Create**.

1. On the **Review + Create** blade, click **Create**.

1. Connect Virtual machine.

1. On the virtual machine blade, click **Disks**, Under **Data disks** click **+ Create and attach a new disk**. 

1. Create a managed disk with the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Disk name | **VMNAME-DataDisk01** |
    | Source type | **None** |
    | Account type | **Premium SSD** |
    | Size | **50 GiB** |
    | | |

1. Connect Virtual machine and start disk.

1. Explore properties to Virtual machines.

## Lab #04 - Migrate Virtual Machines (60 min)

1. In the Azure portal, open another browser tab, navigate to the [301-nested-vms-in-virtual-network Azure QuickStart template](https://github.com/Azure/azure-quickstart-templates/tree/master/301-nested-vms-in-virtual-network) and select **Deploy to Azure**. This will automatically redirect the browser to the **Hyper-V Host Virtual Machine with nested VMs** blade in the Azure portal.

1. On the **Hyper-V Host Virtual Machine with nested VMs** blade in the Azure portal, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | **RGNAME-NESTED** |
    | Host Public IP Address Name | **HOSTNAME-PI** |
    | Virtual Network Name | **VNETNAME-NESTED** |
    | Host Network Interface1Name | **HOSTNAME-NIC01** |
    | Host Network Interface2Name | **HOSTNAME-NIC02** |
    | Host Virtual Machine Name | **HOSTNAME** |
    | Host Admin Username | **admaz** |
    | Host Admin Password | **Azur3Exp3rt*** |

1. On the **Hyper-V Host Virtual Machine with nested VMs** blade, select **Review + create** and then select **Create**.

    > **Note**: Wait for the deployment to complete. The deployment might take about 10 minutes.

#### Task 2: Configure nested virtualization in the Azure VM

1. In the Azure portal, search for and select **Virtual machines** and, on the **Virtual machines** blade.

1. On the blade, select **Networking**. 

1. On the **Networking** blade, select **HOSTNAME-NIC01** and then select **Add inbound port rule**.

    >**Note**: Make sure that you modify the settings of **HOSTNAME-NIC01**, which has the public IP address assigned to it.

1. On the **Add inbound security rule** blade, specify the following settings (leave others with their default values) and select **Add**:

    | Setting | Value | 
    | --- | --- |
    | Destination port range | **3389** |
    | Protocol | **Any** |
    | Name | **Allow-Port_3389** |

1. Connect Virtual machine

1. Within the Remote Desktop session, in the Server Manager window, click **Local Server**, click the **On** link next to the **IE Enhanced Security Configuration** label, and, in the **IE Enhanced Security Configuration** dialog box, select both **Off** options.

1. Within the Remote Desktop session, start Internet Explorer, browse to [Windows Server Evaluations](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019), and download the Windows Server 2019 **VHD** file to the **F:\VHDs** folder (you will need to create it first). 

1. Within the Remote Desktop session, start **Hyper-V Manager**. 

1. In the **Hyper-V Manager** console,select **New** and, in the cascading menu, select **Virtual Machine**. This will start the **New Virtual Machine Wizard**. 

1. On the **Before You Begin** page of the **New Virtual Machine Wizard**, select **Next >**.

1. On the **Specify Name and Location** page of the **New Virtual Machine Wizard**, specify the following settings and select **Next >**:

    | Setting | Value | 
    | --- | --- |
    | Name | **SRVNAME** | 
    | Store the virtual machine in a different location | selected | 
    | Location | **F:\VMs** |

    >**Note**: Make sure to create the **F:\VMs** folder.

1. On the **Specify Generation** page of the **New Virtual Machine Wizard**, ensure that the **Generation 1** option is selected and select **Next >**:

1. On the **Assign Memory** page of the **New Virtual Machine Wizard**, set **Startup memory** to **4096** and select **Next >**.

1. On the **Configure Networking** page of the **New Virtual Machine Wizard**, in the **Connection** drop-down list select **NestedSwitch** and select **Next >**.

1. On the **Connect Virtual Hard Disk** page of the **New Virtual Machine Wizard**, select the option **Use an existing virtual hard disk**, set location to the VHD file you downloaded to the **F:\VHDs** folder, and select **Next >**.

1. On the **Summary** page of the **New Virtual Machine Wizard**, select **Finish**.

1. In the **Hyper-V Manager** console, select the newly created virtual machine and select **Start**. 

1. In the **Hyper-V Manager** console, verify that the virtual machine is running and select **Connect**. 

1. In the Virtual Machine Connection window, on the **Hi there** page, select **Next**. 

1. In the Virtual Machine Connection window, on the **License terms** page, select **Accept**. 

1. In the Virtual Machine Connection window, on the **Customize settings** page, set the password of the built-in Administrator account to **Azur3Exp3rt*** and select **Finish**. 

1. In the Virtual Machine Connection window, sign in by using the newly set password.

1. In the Virtual Machine Connection window, start Windows PowerShell and, in the **Administrator: Windows PowerShell** window run the following to set the computer name. 

   ```powershell
   Rename-Computer -NewName 'SRV01' -Restart
   ```
Migrate Hyper-V VMs to Azure

In the Azure portal, search for *Azure Migrate*.

1.  In **Services**, select **Azure Migrate**.

1. In **Overview**, select **Assess and migrate servers**. In **Servers**, select **Create project**.
. In **Create project**, select the Azure subscription and resource group. Create a resource group if you don't have one.

1. In **Project Details**, specify the project name and the geography in which you want to create the project.

1. Select **Create**.

1. On the **Servers** page > **Windows and Linux servers**, click **Assess and migrate servers**.

1. In **Azure Migrate: Server Assessment, click **Assess**.

1. In **Assess servers** > **Assessment type**, select **Azure VM**.

1. In **Discovery source**:
Specify a name for the assessment. 

1. Click **View all** to review the assessment properties.

1. In **Assessment properties** > **Target Properties**:
    - In **Target location**, specify the Azure region to which you want to migrate.
    - In **Storage type**,
        - Use performance-based data in the assessment, select **Automatic** for 
    - In **Reserved Instances**, specify whether you want to use reserve instances for the VM when you migrate it.

1. In **VM Size**:
 
    - In **Sizing criterion**, select if you want to base the assessment on machine configuration data/metadata, or on performance-based data.
 
    - In **VM Series**, specify the Azure VM series you want to consider.
  
    - In **Comfort factor**, indicate the buffer you want to use during assessment. This accounts for issues like seasonal usage, short performance history, and likely increases in future usage.  
   
9. In **Pricing**:
    - In **Offer**, specify the Azure offer. Server Assessment estimates the cost for that offer.
    - In **Currency**, select the billing currency for your account.
    - In **Discount (%)**, add any subscription-specific discounts you receive on top of the Azure offer. The default setting is 0%.
    - In **VM Uptime**, specify the duration (days per month/hour per day) that VMs will run.
 
    - In **EA Subscription**, specify whether to take an Enterprise Agreement (EA) subscription discount into account for cost estimation. 
    - In **Azure Hybrid Benefit**, specify whether you already have a Windows Server license.

10. Click **Save** if you make changes.

11. In **Assess Servers**, click **Next**.
12. In **Select machines to assess**, select **Create New**, and specify a group name. 
13. Select the appliance, and select the VMs you want to add to the group. Then click **Next**.
14. In **Review + create assessment, review the assessment details, and click **Create Assessment** to create the group and run the assessment.

An assessment describes:

- **Azure readiness**: Whether VMs are suitable for migration to Azure.
- **Monthly cost estimation**: The estimated monthly compute and storage costs for running the VMs in Azure.
- **Monthly storage cost estimation**: Estimated costs for disk storage after migration.

To view an assessment:

1. In **Servers** > **Azure Migrate: Server Assessment**, click the number next to **Assessments**.
2. In **Assessments**, select an assessment to open it.

3. Review the assessment summary. You can also edit the assessment properties, or recalculate the assessment.

For migrating Hyper-V VMs, Azure Migrate:Server Migration installs software providers (Microsoft Azure Site Recovery provider and Microsoft Azure Recovery Service agent) on Hyper-V Hosts or cluster nodes. 

1. In the Azure Migrate project > **Servers**, in **Azure Migrate: Server Migration**, click **Discover**.
2. In **Discover machines** > **Are your machines virtualized?**, select **Yes, with Hyper-V**.
3. In **Target region**, select the Azure region to which you want to migrate the machines.
6. Select **Confirm that the target region for migration is region-name**.
7. Click **Create resources**. This creates an Azure Site Recovery vault in the background.
    
8. In **Prepare Hyper-V host servers**, download the Hyper-V Replication provider, and the registration key file.

4. Copy the provider setup file and registration key file to each Hyper-V host (or cluster node) running VMs you want to replicate.
5. Run the provider setup file on each host, as described in the next procedure.
6. After installing the provider on hosts, in **Discover machines**, click **Finalize registration**.

It can take up to 15 minutes after finalizing registration until discovered VMs appear in Azure Migrate Server Migration. As VMs are discovered, the **Discovered servers** count rises.

With discovery completed, you can begin replication of Hyper-V VMs to Azure.

1. In the Azure Migrate project > **Servers**, **Azure Migrate: Server Migration**, click **Replicate**.
2. In **Replicate**, > **Source settings** > **Are your machines virtualized?**, select **Yes, with Hyper-V**. Then click **Next: Virtual machines**.
3. In **Virtual machines**, select the machines you want to replicate.

4. In **Virtual machines**, search for VMs as needed, and check each VM you want to migrate. Then, click **Next: Target settings**.

5. In **Target settings**, select the target region to which you'll migrate, the subscription, and the resource group in which the Azure VMs will reside after migration.

7. In **Replication Storage Account**, select the Azure Storage account in which replicated data will be stored in Azure.

8. **Virtual Network**, select the Azure VNet/subnet to which the Azure VMs will be joined after migration.

9. In **Availability options**, select:
    -  Availability Set to place the migrated machine in an Availability Set.

10. In **Azure Hybrid Benefit**:
      - Select **Yes** 

11. In **Compute**, review the VM name, size, OS disk type, and availability configuration (if selected in the previous step). VMs must conform with [Azure requirements]

    - **VM size**: If you're using assessment recommendations, the VM size dropdown will contain the recommended size.  
    - **OS disk**: Specify the OS (boot) disk for the VM. The OS disk is the disk that has the operating system bootloader and installer. 
    - **Availability Set**: If the VM should be in an Azure availability set after migration, specify the set. The set must be in the target resource group you specify for the migration.

12. In **Disks**, specify the VM disks that needs to be replicated to Azure. Then click **Next**.

13. In **Review and start replication**, review the settings, and click **Replicate** to start the initial replication for the servers.

> You can update replication settings any time before replication starts, in **Manage** > **Replicating machines**. Settings can't be changed after replication starts.

- When you click **Replicate** a Start Replication job begins. 
- When the Start Replication job finishes successfully, the machines begin their initial replication to Azure.
- After initial replication finishes, delta replication begins. Incremental changes to on-premises disks are periodically replicated to  Azure.

When delta replication begins, you can run a test migration for the VMs, before running a full migration to Azure. We highly recommend that you do this at least once for each machine, before you migrate it.

1. In **Migration goals** > **Servers** > **Azure Migrate: Server Migration**, click **Test migrated servers**.

2. Right-click the VM to test, and click **Test migrate**.

3. In **Test Migration**, select the Azure virtual network in which the Azure VM will be located after the migration. 
4. The **Test migration** job starts. Monitor the job in the portal notifications.
5. After the migration finishes, view the migrated Azure VM in **Virtual Machines** in the Azure portal. The machine name has a suffix **-Test**.
6. After the test is done, right-click the Azure VM in **Replicating machines**, and click **Clean up test migration**.

After you've verified that the test migration works as expected, you can migrate the on-premises machines.

1. In the Azure Migrate project > **Servers** > **Azure Migrate: Server Migration**, click **Replicating servers**.

2. In **Replicating machines**, right-click the VM > **Migrate**.

3. In **Migrate** > **Shut down virtual machines and perform a planned migration with no data loss**, select **Yes** > **OK**.

4. A migration job starts for the VM. Track the job in Azure notifications.

5. After the job finishes, you can view and manage the VM from the **Virtual Machines** page.

## Lab #05 - Azure Storage Blobs (15 minutes)

## Lab #06 - Azure Files (15 minutes)

## Lab #07 - Azure Point-to-site VPN (30 minutes)

## Lab #08 - Azure VNET Peering (15 minutes)

## Lab #09 - Network Security groups (15 minutes)

## Project #01 Hub-spoke Networking 

















