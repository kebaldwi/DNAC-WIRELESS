# PnP Preparation 
## Overview
This lab is the first one in a series of labs. You may use the steps in the DCLOUD environment, or equally, you might utilize them as part of a Proof of Concept setup at a customer's lab. These procedures may also help form part of a deployment or implementation. Use them to ensure that all the necessary steps are complete before onboarding any devices within DNA Center.

We will be utilizing the lab in this manner:

![json](./images/DCLOUD-EN-SB.png?raw=true "Import JSON")

## General Information
As you may recall, in the informational sections of this repository, we set for the various methods of discovery for a device and the preliminary things required for proper zero-touch provisioning. This lab will ensure a successful connection to DNA Center by helping to deploy the initial concepts.

# Lab Preparation
## Lab Section 1 - DNA Center and ISE Integration
In this lab our focus changes slightly as we start to automate for host onboarding. A large component of host onboarding is the authentication of hosts and assignment within the network. In this section and in preparation for the steps which follow we will integrate DNA Center with Identity Services Engine. This integration allows pxGrid communication between the two and allows for automation of configuration within ISE for Network Access Devices, SGT, SGACL, and Policys.

### Step 1 - ***Prepare ISE for DNA Center Integration***
1. Open a web browser on the Windows Workstation Jump host. Open a connection to Identity Services Engine (ISE) and select the hamburger menu icon to open the system menu.

![json](./images/ise-dashboard.png?raw=true "Import JSON")

2. From the system menu under Administration select PxGrid Settings

![json](./images/ise-menu.png?raw=true "Import JSON")

3. On the PxGrid Settings page select both of the available options and click Save to allow DNA Center to integrate.

![json](./images/ise-pxgrid-settings.png?raw=true "Import JSON")
![json](./images/ise-pxgrid-setup.png?raw=true "Import JSON")

### Step 2 - ***DNA Center and ISE Integration***
1. Open a web browser on the Windows Workstation Jump host. Open a connection to Dna Center and select the hamburger menu icon and navigate to the System > Settings menu item.

![json](./images/dnac-system-settings.png?raw=true "Import JSON")

2. Within the System Settings page navigate down the list on the left and select the Authentication and Policy Server section.

![json](./images/dnac-system-settings-aaa.png?raw=true "Import JSON")

3. On the page select from the dropdown ISE to configure ISE integration.

![json](./images/dnac-system-settings-aaa-ise.png?raw=true "Import JSON")

4. Enter the information as seen on the page and click save.

![json](./images/dnac-system-settings-aaa-ise-config.png?raw=true "Import JSON")

5. A popup will appear as the ISE node is using an untrusted SelfSigned Certificate. For lab purposes Accept the certificate, this may appear a couple of times as shown.

![json](./images/dnac-system-settings-aaa-ise-trust.png?raw=true "Import JSON")

6. You will see the the various stages of integration proceed and finally a success message as shown below.

![json](./images/dnac-system-settings-aaa-ise-done.png?raw=true "Import JSON")
![json](./images/dnac-system-settings-aaa-ise-complete.png?raw=true "Import JSON")

## Lab Section 2 - DNA Center Design Preparation
While we could deploy more extensive settings for deployment, we will limit the configuration to the minimum necessary to perform this step, utilizing ***Postman*** to deploy the settings discover devices and onboard them into DNA Center. 

Should you desire to deploy rapidly and build the lab faster then use the following approach:

### Step 1 - ***Import Postman Collection***
1. Download and import the collection within the ***Postman*** using the <a href="https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/kebaldwi/DNAC-TEMPLATES/blob/master/LABS/LAB8-Dynamic-Automation/postman/DCLOUD_DNACTemplatesLab_Workflow.postman_collection.json">⬇︎DCLOUD_DNACTemplateLab_Workflow.postman_collection.json⬇︎</a> file.
2. Extract the file to the desktop using **Winrar** to expand them
3. Open the **postman** application from the desktop. Once the application is open select *Collections* then click the *Import* link. 
![json](./images/Postman-Pre-Collection-Import.png?raw=true "Import JSON")
4. A window should appear on the file upload page. Click the upload button and select desktop from the windows explorer. Select the file named `DCLOUD_DNACTemplatesLab_Workflow.postman_collection.json` and click open. 
![json](./images/Postman-Collection-Select.png?raw=true "Import JSON")
5. Then click import and the collection should be loaded into the collections as shown.
![json](./images/Postman-Post-Collection-Import.png?raw=true "Import JSON")

### Step 2 - ***Import Postman Environment***
1. Download and import the environment within the ***Postman*** using the <a href="https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/kebaldwi/DNAC-TEMPLATES/blob/master/LABS/LAB8-Dynamic-Automation/postman/DCLOUD_DNACTemplateLabs.postman_environment.json">⬇︎DCLOUD_DNACTemplateLabs.postman_environment.json⬇︎</a> file.
2. Extract the file to the desktop using **Winrar** to expand them
3. If not open, open the **postman** application from the desktop. Once the application is open select *Environments* and then the *Import* link. 
![json](./images/Postman-Pre-Environment-Import.png?raw=true "Import JSON")
4. A window should appear on the file upload page. Click the upload button and select desktop from the windows explorer. Select the file named `DCLOUD_DNACTemplateLabs.postman_environment.json` and click open. 
![json](./images/Postman-Environment-Select.png?raw=true "Import JSON")
5. Then click import and the environment should be loaded into the environments as shown. 
![json](./images/Postman-Post-Environment-Import.png?raw=true "Import JSON")
6. Next we will choose the environment by clicking the checkmark on the right of Environment in postman as shown here. 
![json](./images/Postman-Environment-Selection.png?raw=true "Import JSON")

### Step 3 - ***Turn off SSL validation for LAB purposes within Postman***
1. Turn off SSL verification for lab purposes in the settings of Postman by click the **Gear** icon to select **settings** and **deselect** `SSL certificate verification` and then close the settings window. 
![json](./images/Postman-SSL-Deselect.png?raw=true "Import JSON")
2. With these steps completed we are prepared to start the walk through of the sections below.

### Step 4 - ***Run the Collection within Postman***
This collection is built with a flow and delay timers wait for the collection to finish entirely.
1. If not open, open the **postman** application from the desktop. Once the application is open select *Collections* and then the '...' link and select **run collection**. </br>
![json](./images/Postman-CollectionRunner.png?raw=true "Import JSON")
2. On the right ensure all API are selected and click run collection. 
![json](./images/Postman-CollectionRunner-Run.png?raw=true "Import JSON")
3. After the entire collection has run you will see all of them listed on the left as shown, and two buttons on the top right, one for results and the other to run again.
![json](./images/Postman-CollectionRunner-Results.png?raw=true "Import JSON")
4. Within DNA Center you should see 3 devices within the inventory and additionally you should observe a complete hierarchy as well as settings and telemetry configured. The Devices will be discovered in the Building level at this stage.
![json](./images/Postman-Discovery.png?raw=true "Import JSON")
![json](./images/Postman-Settings.png?raw=true "Import JSON")

## Lab Section 3 - DHCP & DNS Service Preparation
In this section we will prepare Domain Name System (DNS) and Dynamic Host Configuration Protocol (DHCP) on the Windows Server for the lab environment. The reasons for the configurations made here are detailed heavily in Lab 2 titled [Onboarding Templates](https://github.com/kebaldwi/DNAC-TEMPLATES/blob/master/LABS/LAB2-Onboarding-Template/)

### Step 1 - ***Configuring DHCP and DNS via Powershell***
1. Download the powershell script to the ***windows server*** using the <a href="https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/kebaldwi/DNAC-TEMPLATES/blob/master/LABS/LAB8-Dynamic-Automation/scripts/powershell.ps1">⬇︎powershell.ps1⬇︎</a> file.
2. Once downloaded, extract the file.
   ![json](./images/Powershell-Extract.png?raw=true "Import JSON")
   ![json](./images/Powershell-Extract-Location.png?raw=true "Import JSON")
3. Right click on the file and run with powershell.
   ![json](./images/Powershell-Run.png?raw=true "Import JSON")
4. You may see a security warning. If you do accept it by entering **Y**.
   ![json](./images/Powershell-Security.png?raw=true "Import JSON")
At this point all the DNS and DHCP configuration on the ***windows server*** will be generated.
   ![json](./images/DNS-DHCP.png?raw=true "Import JSON")

## Lab Section 4 - Image Repository
As we have discovered the devices, from the network, DNA Center has the capability to pull those images deployed from the network devices in bundle mode. If the device is in install mode then you would manually have to add the images. We can then mark them as **Golden** for *Plug and Play* and *image upgrade* purposes. 

For our purposes as we will be focusing on only the **9300-2** switch we will complete the following steps.

The image used in this lab for the 9300-2 is downloadable from here [⬇︎Bengaluru-17.06.01 MD⬇︎](https://software.cisco.com/download/home/286315874/type/282046477/release/Bengaluru-17.6.1) **(required)** 

1. Within DNA Center Navigate to *Design>Image Repository*  
   ![json](./images/DNAC-Design-ImageRepo-menu.png?raw=true "Import JSON")
2.  **Image Repository** should be populated with the image of the network device you wish to deploy. You can import the image using the **+ Import** link which will open a popup allowing you to choose a file from the local file system, or allow you to reference a URL for either HTTP or FTP transfer. 
   ![json](./images/DNAC-Design-ImageRepo-import.png?raw=true "Import JSON")
3. We will select the file from our local system.
   ![json](./images/DNAC-Design-ImageRepo-select.png?raw=true "Import JSON")
3. The file will then import into DNA Center.    
   ![json](./images/DNAC-Design-ImageRepo-imageimport.png?raw=true "Import JSON")
4. Once the file is imported and as the devices were previously discovered and assigned to the infrastructure we will navigate to the *Floor 1* in the hierarchy and mark the *17.06.01* as **Golden** as shown for PnP to use it.  
   ![json](./images/DNAC-Design-ImageRepo-golden.png?raw=true "Import JSON")

## Lab Section 5 - DNA Center Template Preparation
As Labs 1 through 9  within DNAC Template Labs deal with the wired network in depth and the automation tasks like PnP and DayN templating for switching, in this set of labs we will focus on only the wireless network. We will now import the various templates for use in this lab for the router and switches to prepare the environment for the Wireless Labs ahead.

### Step 1 - ***Import Lab Preparation Project***
The Lab Preparation Project and Templates will be used to prepare the environment.

Download and import the Onboarding Template within the ***Template Editor*** using the <a href="https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/kebaldwi/DNAC-TEMPLATES/blob/master/LABS/LAB8-Dynamic-Automation/templates/DCLOUD-PrepEnvironment-project.json">⬇︎DCLOUD-PrepEnvironment-Project.json⬇︎</a> file.

Please un-zip the file and import the *json* file which will automatically create a project and included templates within. Use the following steps to import the project.

1. Navigate to the **Template Editor** within DNA Center through the menu *Tools>Template Editor*.
   ![json](./images/DNAC-Template-menu.png?raw=true "Import JSON")
2. Within the **template editor**, left-click the ⨁ icon to the right of find template and click **Import Project(s)** within the menu.  
   ![json](./images/DNAC-Template-menu-import.png?raw=true "Import JSON")
3. Download the file above *DNAC_Template_Lab_DayN_project.json* to be imported into the DNA Center. Once downloaded, extract the file.
4. From the **Import Project(s)** window, click **Select a file from your computer** from the explorer window, select the extracted JSON file and click open. 
   ![json](./images/DNAC-Template-Prep-select.png?raw=true "Import JSON")
5. Click **Import**, and the project and all the templates within it will be imported.   
   ![json](./images/DNAC-Template-import.png?raw=true "Import JSON")
6. Once the project is imported, select it to view each of the template files within it.

## Lab Section 6 - Setup of Discovered Devices
At this point in the lab the setup steps for the lab environment are done, DNS and DHCP are set up, ISE is integrated and DNA Center is ready for deploying configurations. In this section we will deploy the templates to configure the discovered devices. Note we could have automated this process too but wanted to separate this out so you can make modifications as you might need to for testing purposes.

### Lab SubSection 6.1 - 9300 Target Preparation
In this subsection we will prepare the **Target** using the *c9300-2.dcloud.cisco.com*. To begin preparation of this **Target** device we can deploy a template to modify discovered device within the infrastructure to reset it automatically. In order to accomplish this we will need to complete the following stages.

#### Step 1 - ***Building Switching Network Profiles***
1. Navigate to the **Design** within DNA Center through the menu *Design>Network Profile*.
   ![json](./images/DNAC-NetworkProfile-menu.png?raw=true "Import JSON")
2. Select *Switching* under **Add Profile** .
   ![json](./images/DNAC-NetworkProfile-Switching-Add.png?raw=true "Import JSON")
3. Enter the following: 
      1. Enter the *Profile name* 
      2. Select **DayN Template** tab to add the template for this workflow.
      3. Click the **Table View** 
      4. Click *Add Template* to proceed to the next step. 
         ![json](./images/DNAC-NetworkProfile-Switching-DayN.png?raw=true "Import JSON")
4. Enter the following: 
      1. Leave the **Device Type** as *Switches and Hubs*
      2. Select the dropdown **Template** tand search for *C9300-TARGET-Prep*.
      3. Click the **Tags** 
      4. Enter *RELOAD* as a tag. *(If necessary click the small* ***x** by any other tag visible)*
      5. Click **Add** 
         ![json](./images/DNAC-Profile-Target-add.png?raw=true "Import JSON")
5. Click **View** to ensure the RELOAD tag is the only tag applied and click **Save**.
   ![json](./images/DNAC-Profile-Target-save.png?raw=true "Import JSON")

#### Step 2 - ***Assigning Switching Network Profile to a Site***
1. **Assign** the network profile to the hierarchy 
![json](./images/DNAC-NetworkProfile-Switching-DayN-Assign.png?raw=true "Import JSON")
2. Select the **sites** to apply the profile within the hierarchy and click **Save**
![json](./images/DNAC-NetworkProfile-Switching-DayN-Assign-Site.png?raw=true "Import JSON")

#### Step 3 - ***Provisioning Target 9300 Switch***
We will now provision the **Target** switch using the *C9300-TARGET-Prep* DayN Template. The template uses a *Tag* of **RELOAD** so we need to first set that and then provision the switch. To do this, do the following:

##### Tag Switch
   1. Within DNA Center Navigate to *Provision>Inventory*.      
      ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Put a **checkmark** next to the device *c9300-1.dcloud.cisco.com*.
   3. Click the **Tag Device** link 
   4. Search for and place a **checkmark** beside *RELOAD*
   5. Click **Apply**    
      ![json](./images/DNAC-Provision-Target-tag.png?raw=true "Import JSON")

##### Provision Switch
   1. Within DNA Center Navigate to *Provision>Inventory*.      
      ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Put a checkmark next to the device *c9300-1.dcloud.cisco.com* to be provisioned.
   3. Click **Actions>Provision>Provision Device** link and walk through the workflow    
      ![json](./images/DNAC-Provision-Target-flow.png?raw=true "Import JSON")
   4. The floor was already selected during the **API Discovery** so click **next**    
      ![json](./images/DNAC-Provision-Target-flow-1.png?raw=true "Import JSON")
   5. Select *c9300-1.dcloud.cisco.com* on the left and the two tick boxes at the top of the page, then click **next**. If the template had inputs, they would be entered.
      ![json](./images/DNAC-Provision-Target-flow-2.png?raw=true "Import JSON")
   6. Check the settings and if you agree accept these settings by clicking  **Deploy**.
      ![json](./images/DNAC-Provision-Target-flow-3.png?raw=true "Import JSON")
   7. Three options are displayed. Choose to deploy **Now** and **Apply**
      ![json](./images/DNAC-Provision-Target-flow-4.png?raw=true "Import JSON")
   8. The task will be submitted, and the deployment will run.
   9. After a small amount of time, you will see a success notification. What is essential to understand is that the configuration, while pushed to the device, will resync in DNA Center after the resync timer has elapsed.        
      ![json](./images/DNAC-Provision-Target-success.png?raw=true "Import JSON")

#### Step 4 - ***Deleting the Target 9300 Switch***
We will now delete the **Target** switch to allow for the switch to be discovered automatically during the **Plug and Play (PnP)** process. In order to accomplish this complete the following tasks:
   1. Within DNA Center Navigate to *Provision>Inventory*.      
      ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Put a **checkmark** next to the device *c9300-1.dcloud.cisco.com*.
   3. Click **Actions>Inventory>Delete Device** link 
      ![json](./images/DNAC-Provision-Target-delete-1.png?raw=true "Import JSON")
   4. On the *Popup* that appears click **Ok**
      ![json](./images/DNAC-Provision-Target-delete-2.png?raw=true "Import JSON")
   5. DNA Center will then delete the switch from the Database.  
      ![json](./images/DNAC-Provision-Target-delete-3.png?raw=true "Import JSON")

### Lab SubSection 6.2 - ISR Preparation
In this subsection we will apply a small template to the ISR 4331. This is to prove out that we can deploy templates to modify discovered devices within the infrastructure no matter what variant they are. You could also use this method to apply configuration to a router to mitigate vulnerabilities discovered as part of a tennable security scan. 

#### Step 1 - ***Building Routing Network Profiles***
1. Navigate to the **Design** within DNA Center through the menu *Design>Network Profile*.
   ![json](./images/DNAC-NetworkProfile-menu.png?raw=true "Import JSON")
2. Select *Routing* under **Add Profile** .
   ![json](./images/DNAC-NetworkProfile-Routing-Add.png?raw=true "Import JSON")
3. Enter the following: 
      1. Enter the *Profile name* 
      2. Select *Zero* for **Service Providers**
      3. Click the **Device Type** dropdown and select *Cisco 4331 Integrated Services Router* 
      4. Click *Next* to proceed to the next step. 
      ![json](./images/DNAC-NetworkProfile-Routing-1.png?raw=true "Import JSON")
4. We are not utilizing **Step 2** so click *Next* to proceed to the next step.
   ![json](./images/DNAC-NetworkProfile-Routing-2.png?raw=true "Import JSON")
5. We are not utilizing **Step 3** so click *Next* to proceed to the next step.
   ![json](./images/DNAC-NetworkProfile-Routing-3.png?raw=true "Import JSON")
6. On **Step 4** complete the following: 
      1. Select the *Day-N Template(s)* tab 
      2. Click the **Template** dropdown and select *ISR-Prep* 
      3. Click *Next* to proceed to the next step. 
         ![json](./images/DNAC-NetworkProfile-Routing-4.png?raw=true "Import JSON")
7. To complete the Network Profile in **Step 5** click *Save*.
   ![json](./images/DNAC-NetworkProfile-Routing-5.png?raw=true "Import JSON")

#### Step 2 - ***Assigning Routing Network Profile to a Site***
1. **Assign** the network profile to the hierarchy 
   ![json](./images/DNAC-NetworkProfile-Routing-Assign.png?raw=true "Import JSON")
2. Select the **sites** to apply the profile within the hierarchy and click **Save**
   ![json](./images/DNAC-NetworkProfile-Routing-Assign-Site.png?raw=true "Import JSON")

#### Step 3 - ***Provisioning Router***
   1. Within DNA Center Navigate to *Provision>Inventory*.      
      ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Put a checkmark next to the device *isr-4331.dcloud.cisco.com* to be provisioned.
   3. Click the **Actions>Provision>Provision Device** link and walk through the workflow    
      ![json](./images/DNAC-Provision-ISR-flow.png?raw=true "Import JSON")
   4. The floor was already selected during the **API Discovery** so click **next**    
      ![json](./images/DNAC-Provision-ISR-flow-1.png?raw=true "Import JSON")
   5. The ISR 4331 was pre selected in the profile so click **next**
      ![json](./images/DNAC-Provision-ISR-flow-2.png?raw=true "Import JSON")
   6. Do the following:
      1. Select the Day-N Templates Tab
      2. Select the IP of the ISR
      3. Select both **checkmark**
      4. Click **next**
      ![json](./images/DNAC-Provision-ISR-flow-3.png?raw=true "Import JSON")
   7. A summary is displayed. Click **Deploy**.
      ![json](./images/DNAC-Provision-ISR-flow-4.png?raw=true "Import JSON")
   8. Three options are displayed. Choose to deploy **Now** and **Apply**
      ![json](./images/DNAC-Provision-ISR-flow-5.png?raw=true "Import JSON")
   9. The task will be submitted, and the deployment will run.
   10. After a small amount of time, you will see a success notification. What is essential to understand is that the configuration, while pushed to the device, will resync in DNA Center after the resync timer has elapsed.        
      ![json](./images/DNAC-Provision-ISR-success.png?raw=true "Import JSON")

### Lab SubSection 6.3 - Distribution 9300 Preparation
In this subsection we will apply a small templates to the Cat 9300-2 which is used as a distribution switch. This is to prove out that we can deploy templates to modify discovered devices within the infrastructure no matter what variant they are. You could also use this method to apply configuration to a switch to mitigate vulnerabilities discovered as part of a tennable security scan. 

#### Step 1 - ***Building Switching Network Profiles***
1. Navigate to the **Design** within DNA Center through the menu *Design>Network Profile*.
   ![json](./images/DNAC-NetworkProfile-menu.png?raw=true "Import JSON")
2. Click the **Edit** beside the *DNAC-Templates-C9300* Profile Name.
   ![json](./images/DNAC-NetworkProfile-Switching-edit.png?raw=true "Import JSON")
3. Enter the following: 
      1. Enter the *Profile name* 
      2. Select **DayN Template** tab to add the template for this workflow.
      3. Click the **Table View** 
      4. Click *Add Template* to proceed to the next step. 
         ![json](./images/DNAC-NetworkProfile-Switching-DayN.png?raw=true "Import JSON")
4. Enter the following: 
      1. Leave the **Device Type** as *Switches and Hubs*
      2. Select the dropdown **Template** tand search for *DISTRO-C9300-2*.
      3. Click the **Tags** 
      4. Enter *INFRA* as a tag. *(If necessary click the small* ***x** by any other tag visible)*
      5. Click **Add** 
         ![json](./images/DNAC-NetworkProfile-Switching-DayN-Template.png?raw=true "Import JSON")
5. Click **View** to ensure the INFRA tag is **the only tag** applied and click **Save**.
   ![json](./images/DNAC-NetworkProfile-Switching-DayN-Template-Save.png?raw=true "Import JSON")

#### Step 2 - ***Assigning Switching Network Profile to a Site***
The network profile is already assigned to the site, so this step is not required but for review purposes only these were the steps we used to accomplish that originally. As this is already completed you can skip to **Step 3**

1. **Assign** the network profile to the hierarchy 
![json](./images/DNAC-NetworkProfile-Switching-DayN-Assign.png?raw=true "Import JSON")
2. Select the **sites** to apply the profile within the hierarchy and click **Save**
![json](./images/DNAC-NetworkProfile-Switching-DayN-Assign-Site.png?raw=true "Import JSON")

#### Step 3 - ***Provisioning Distribution 9300 Switch***
We will now provision the distribution switch using the *DISTRO-C9300-2* DayN Composite Template. The template uses a *Tag* of **INFRA** so we need to first set that and then provision the switch. To do this, do the following:

##### Tag Switch
   1. Within DNA Center Navigate to *Provision>Inventory*.      
   ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Put a **checkmark** next to the device *c9300-2.dcloud.cisco.com*.
   3. Click the **Tag Device** link 
   4. Search for and place a **checkmark** beside *INFRA*
   5. Click **Apply**    
   ![json](./images/DNAC-Provision-Distro-tag.png?raw=true "Import JSON")

##### Provision Switch
   1. Within DNA Center Navigate to *Provision>Inventory*.      
      ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Put a checkmark next to the device *c9300-2.dcloud.cisco.com* to be provisioned.
   3. Click the **Actions>Provision>Provision Device** link and walk through the workflow    
      ![json](./images/DNAC-Provision-Distro-flow.png?raw=true "Import JSON")
   4. The floor was already selected during the **API Discovery** so click **next**    
      ![json](./images/DNAC-Provision-Distro-flow-1.png?raw=true "Import JSON")
   5. Select *c9300-1.dcloud.cisco.com* on the left and the two tick boxes at the top of the page, then click **next**. If the template had inputs, they would be entered.
      ![json](./images/DNAC-Provision-Distro-flow-2.png?raw=true "Import JSON")
   6. Check the settings and if you agree accept these settings by clicking  **Deploy**.
      ![json](./images/DNAC-Provision-Distro-flow-3.png?raw=true "Import JSON")
   7. Three options are displayed. Choose to deploy **Now** and **Apply**
      ![json](./images/DNAC-Provision-Distro-flow-4.png?raw=true "Import JSON")
   8. The task will be submitted, and the deployment will run.
   9. After a small amount of time, you will see a success notification. What is essential to understand is that the configuration, while pushed to the device, will resync in DNA Center after the resync timer has elapsed.        
      ![json](./images/DNAC-Provision-Distro-flow-success.png?raw=true "Import JSON")

## Lab Section 7 - Testing
Please use the testing for the DNS Discovery method used above.

### Step 1 - ***DNS Resolution Tests***
To test the environment to ensure it's ready, we need to try a few things.

First, from a Windows host, use the *nslookup* command to resolve ***pnpserver.dcloud.cisco.com***. Connect to the Windows workstation, and within the search window, search for CMD. Open the application and type the following command:

```
nslookup pnpserver.dcloud.cisco.com
```

The following output or something similar shows the resolution of the alias to the A host record entry which identifies the VIP address for the DNA Center Cluster will display.

![json](./images/DNACenterDNStests.png?raw=true "Import JSON")

### Step 2 - ***DNS Resolution***
Second, we need to ensure the DNA Center responds on the VIP, so use the ping command within the CMD application window previously opened as follows:

```
ping pnpserver.dcloud.cisco.com
```

![json](./images/DNACenterDNStestPing.png?raw=true "Import JSON")

At this point, the environment should be set up to onboard devices within VLAN 5 using the network address ***192.168.5.0/24*** utilizing either ***option 43*** or ***DNS discovery ***.

### Step 3 - ***Preparation Confirmation***
Once all the steps have been completed, the *access points* will have rebooted in a default state, acquired an IP address, discovered DNA Center and will appear in the **Plug and Play** tab in the **Provisioning** application. Confirm this by 

   1. Within DNA Center Navigate to *Provision>Inventory*.      
      ![json](./images/DNAC-InventoryProvision-menu.png?raw=true "Import JSON")
   2. Select the *Plug and Play* tab and notice the switch under the *unclaimed* section.
      ![json](./images/DNAC-Provision-Target-delete-4.png?raw=true "Import JSON")

At this point we are ready to set up our **Wireless Environment**.

## Summary
The next step will be to build the PnP Onboarding settings and template on DNA Center, which we will cover in the next lab entitled [Onboarding Templates](../LAB2-Onboarding-Template/README.md#Day0) - The next lab explains in-depth and how to deploy Day 0 templates.

## Feedback
If you found this set of Labs helpful, please fill in comments and [give feedback](https://app.smartsheet.com/b/form/f75ce15c2053435283a025b1872257fe) on how we can improve.
