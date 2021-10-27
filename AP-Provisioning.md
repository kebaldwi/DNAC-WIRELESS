# AP Provisioning 
Provision a Cisco AP—Day 1 AP Provisioning

**Before you begin**

Make sure that you have Cisco APs in your inventory. If not, use the Discovery feature to discover APs. For more information, see [Discover Your Network](https://www.cisco.com/c/en/us/td/docs/cloud-systems-management/network-automation-and-management/dna-center/2-2-2/user_guide/b_cisco_dna_center_ug_2_2_2/b_cisco_dna_center_ug_2_2_2_chapter_010.html#id_48423).

**Procedure**
-
Step 1 - In the Cisco DNA Center GUI, click the **Menu** icon (![json](./images/dnac-hamburger-icon.png?raw=true "Import JSON")) and choose **Provision > Devices > Inventory**.

The **Inventory** window appears, with the discovered devices listed.

Step 2 - To view devices available in a particular site, expand the **Global** site in the left pane, and select the site, building, or floor that you are interested in.

All devices available in the selected site are displayed in the **Inventory** window.

Step 3 - From the **Device Type** list, click the **APs** tab, and from the **Reachability** list, click the **Reachable** tab to see the APs that are discovered and reachable.

Step 4 - Check the check box next to the AP device name that you want to provision.

Step 5 - From the **Action** drop-down list, choose **Provision > Provision**.

The **Assign Site** window appears.

Step 6 - Click **Choose a floor** and assign an AP to the site.

Step 7 - In the **Choose a floor** window, select the floor to which you want to associate the AP, and click **Save**.

Step 8 - Click **Next**.

The **Configuration** window appears.

Step 9 - By default, the custom RF profile that you marked as default under **Design > Network Settings > Wireless > Wireless Radio Frequency Profile** is chosen in the **RF Profile** drop-down list.

You can change the default RF Profile value for an AP by selecting a value from the RF Profile drop-down list. The options are **High, Typical, and Low**.

The AP group is created based on the selected RF profile.

Step 10 - Click **Next**.

Step 11 - In the **Summary** window, review the device details, and click **Deploy** to provision the AP.

Step 12 - In the **Provision Devices** window, do the following to preview the CLI configuration:

* 	Click the **Generate Configuration Preview** radio button.
* 	In the **Task Name** field, enter a name for the CLI preview task and click **Apply**.
* 	In the **Task Submitted** pop-up, click the **Work Items** link.
    
    **Note**	If you missed the **Task Submitted** pop-up, click the **Menu** icon (![json](./images/dnac-hamburger-icon.png?raw=true "Import JSON")) and choose **Activity > Work Items**.
* 	In the **Work Items** window, click the CLI preview task for which you submitted the configuration preview request.
* 	View the CLI configuration details and click **Deploy**.
* 	To immediately deploy the device, click the **Now** radio button, and click **Apply**.
* 	To schedule the device deployment for a later date and time, click the **Later** radio button and define the date and time of the deployment.
* 	In the **Information** pop-up, do the following:
	* 	Click Yes if you want to delete the CLI preview task from the **Work Items** window.
	* 	Click No if you want to retain the task in the Work Items window

		**Note**  	The CLI task will be marked as completed in the **Work Items** window. You can view the CLI configuration for this task, but you cannot deploy it again.

Step 13 - You are prompted with a message that creation or modification of an AP group is in progress, and then a message that APs will reboot after provisioning.

Step 14 - Click **OK**.

The **Last Sync Status** column in the **Inventory** window shows SUCCESS for a successful deployment.