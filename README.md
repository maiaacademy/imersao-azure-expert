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

2. Search for and select **Resource groups**. 

3. On the **Resource groups** blade, click **+ Add** and create a resource group with the following settings:

    |Setting|Value|
    |---|---|
    |Subscription| the name of the Azure subscription you will use in this lab |
    |Resource Group| **RG-FLN-VMS**|
    |Region| East US 2 |
    |Tags| environment: resource, project: azureexpert |
    | | |

4. Repeat and create the Resources groups name "RG-FLN-Networking" and "RG-FLN-Storage".

1. Click **Review + Create** and then click **Create**.

## Lab #02 - Virtual Networks (20 minutes)

1. In the Azure portal, search for and select **Virtual networks**, and, on the **Virtual networks** blade, click **+ Add**.

1. Create a virtual network with the following settings (leave others with their default values):

    | Setting | Value |
    | --- | --- |
    | Subscription | the name of the Azure subscription you will be using in this lab |
    | Resource Group | the name of a resource group **RG-FLN-Network** |
    | Name | **VNET-FLN-HUB** |
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
    | Resource group | the name of a new resource group **RG-FLN-VMS** |
    | Virtual machine name | **VMFLNWEB01** |
    | Region | select one of the regions that support availability zones and where you can provision Azure virtual machines | 
    | Availability options | **Availability sets** |
    | Availability set | **AS-WEB** |
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
    | Virtual Network | **VNET-FLN-HUB** |
    | Subnet | **FrontEnd** |
    | Public IP | **VMFLNWEB01-PI** |
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
    | Disk name | **VMFLNWEB01-DataDisk01** |
    | Source type | **None** |
    | Account type | **Premium SSD** |
    | Size | **50 GiB** |
    | | |

1. Connect Virtual machine and start disk.

1. Explore properties to Virtual machine.

## Project #01 - Migrate Virtual Machines (60 min)

1. In the Azure portal, open another browser tab, navigate to the [301-nested-vms-in-virtual-network Azure QuickStart template](https://github.com/Azure/azure-quickstart-templates/tree/master/301-nested-vms-in-virtual-network) and select **Deploy to Azure**. This will automatically redirect the browser to the **Hyper-V Host Virtual Machine with nested VMs** blade in the Azure portal.

1. On the **Hyper-V Host Virtual Machine with nested VMs** blade in the Azure portal, specify the following settings (leave others with their default values):

    | Setting | Value | 
    | --- | --- |
    | Subscription | the name of the Azure subscription you are using in this lab |
    | Resource group | **RG-FLN-NESTED** |
    | Host Public IP Address Name | **VMFLNNESTED-PI** |
    | Virtual Network Name | **VNET-FLN-NESTED** |
    | Host Network Interface1Name | **VMFLNNESTED-NIC01** |
    | Host Network Interface2Name | **VMFLNNESTED-NIC02** |
    | Host Virtual Machine Name | **VMFLNNESTED** |
    | Host Admin Username | **admaz** |
    | Host Admin Password | **Azur3Exp3rt*** |

1. On the **Hyper-V Host Virtual Machine with nested VMs** blade, select **Review + create** and then select **Create**.

    > **Note**: Wait for the deployment to complete. The deployment might take about 10 minutes.

#### Task 2: Configure nested virtualization in the Azure VM

1. In the Azure portal, search for and select **Virtual machines** and, on the **Virtual machines** blade.

1. On the blade, select **Networking**. 

1. On the **Networking** blade, select **VMFLNNESTED-NIC01** and then select **Add inbound port rule**.

    >**Note**: Make sure that you modify the settings of **VMFLNNESTED-NIC01**, which has the public IP address assigned to it.

1. On the **Add inbound security rule** blade, specify the following settings (leave others with their default values) and select **Add**:

    | Setting | Value | 
    | --- | --- |
    | Destination port range | **3389** |
    | Protocol | **Any** |
    | Name | **AllowRDPInBound** |

1. Connect Virtual machine

1. Within the Remote Desktop session to **az30312a-hv-vm**, in the Server Manager window, click **Local Server**, click the **On** link next to the **IE Enhanced Security Configuration** label, and, in the **IE Enhanced Security Configuration** dialog box, select both **Off** options.

1. Within the Remote Desktop session, start Internet Explorer, browse to [Windows Server Evaluations](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019), and download the Windows Server 2019 **VHD** file to the **F:\VHDs** folder (you will need to create it first). 

1. Within the Remote Desktop session, start **Hyper-V Manager**. 

1. In the **Hyper-V Manager** console,select **New** and, in the cascading menu, select **Virtual Machine**. This will start the **New Virtual Machine Wizard**. 

1. On the **Before You Begin** page of the **New Virtual Machine Wizard**, select **Next >**.

1. On the **Specify Name and Location** page of the **New Virtual Machine Wizard**, specify the following settings and select **Next >**:

    | Setting | Value | 
    | --- | --- |
    | Name | **SRV01** | 
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











