# Azure: Building Highly Available and Secure Environment

## Step 1: Azure Login and Resource Group

1.  Login to Azure using portal.azure.com
2.  Search **Resource Group** and create a resource
3.  Enter name of group: **RG-Support-1**
4.  Select a region: **East US**
    * Add tags if necessary for automation
5.  Click **Review + Create**, then **Create**

## Step 2: Set up VNet, Subnets, and NSG

1.  Search **Virtual Networks** and click **Create**
    * Select Subscription and Resource Group to **RG-Support-1**
    * Name VNet: **VNet1**
    * Under IP addresses, use default IP: `10.0.0.0/16`
    * Edit default subnet mask to **Subnet-Web** and change starting address to `10.0.1.0/24`
    * Create second subnet, name it as **Subnet-Mgmt** and edit starting address to `10.0.2.0/24`
    * Click **review + Create** then **Create**
2.  Search **Network Security Group**
    * Select resource group and name: **NSG-Web**
    * Click **Create**
    * Click “Go to Resource”
    * Click **Inbound Security Rules** (under Settings)
    * Select **Add** and create new rule
        1.  Add ports `80`, `443` under Destination port ranges
        2.  Allow **TCP** protocol only
        3.  Name: **Allow-Inbound-Web** then click **Add**
    * Click on **Subnets** on **NSG-Web** (under Settings)
    * Select **Associate** and select **Vnet1** with **Subnet-Web**

## Step 3: Create Availability Set and Deploy VMs

1.  Search **Availability Set** and click **Create**
    * Select resource group and name: **AS-Web**
    * Keep default fault domains and update domains
    * Click **review + create**, then **create**
2.  Search **Virtual Machines** and click **Create**
    * Select resource group
    * Name VM: **VM-Web1**
    * Set availability options as **Availability set**
    * Set Availability set as **AS-Web**
    * Use standard security
    * Use **Windows 11 Pro** image
    * Set username: `azureuser` and make a secure password
    * Select Networking tab
        * Set virtual network as **Vnet-Prod**
        * Set subnet as **Subnet-Web**
    * Click **Review + Create**, then **create**
3.  Repeat for **VM-Web2**

## Step 4: Install System Administration Tools

1.  Navigate to **VM-Web1**
2.  Under **Operations**, click **Run Command**
    * Select **RunPowerShellScript**
        1.  Paste this command: `Enable-WindowsOptionalFeature -Online -FeatureName IIS-WebServerRole,IIS-ManagementConsole -All`
    * Click **run**
3.  You can use tools like **Network Watcher** and use the **IP flow verify** tool to confirm traffic such as below (refer to the NSG we implemented)
