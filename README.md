# DNAC-WIRELESS 
## Overview
This Repository will give examples of how to manage Cisco Unified Wireless technologies via DNA Center and ways that you can modify and use them for your organizational needs. Additional information will be included to hopefully give a well rounded explanation of Automation methods for Wireless using DNA Center and flows and concepts for dealing with day to day wireless tasks.

The goal of this repository is a practical guide to allow engineers to rapidly begin using DNAC automation and begin conversion towards an automated network infrastructure revolving around Cisco's DNA Center. 

## Intent Based Networking
Intent will be built in combination with the Design Settings and Policies to be deployed via the UI. One or Multiple templates or Model-Based Configuration may be used in Onboarding (PnP) or as required at Day N. Additionally, Intent can be defined as the set of configuration constructs deployed via a template, setting, policy, or model based config.


## Tutorial Sections
Various sections will be covered within this github repository please use this menu for navigation. Within the various folders are examples, explanation readme files for reference.

* [PnP Workflow](./PnP-Workflow.md#pnp-workflow) - This section explains the overall Plug and Play Methodology

### Supplimental Content
* [Variables](./Variables.md#variables) - This section explains Variables in depth and how and where to use them
* [Velocity Scripting](./Velocity.md#velocity-scripting) - This section will dive into Velocity Scripting constructs and use cases
* [Building Templates](./Templates.md#building-templates) - This section will explain how to build a template on DNAC
* [Onboarding Templates](./Onboarding.md#onboarding-templates-and-flows) - This section will explain Onboarding Templates in DNAC and their use
* [DayN Templates](./DayN.md#day-n-templates-and-flows) - This section will explain how to use templates for ongoing changes to the network
* [Advanced Velocity](./AdvancedVelocity.md#advanced-velocity) - This section will dive into Advanced Velocity examples
* [Troubleshooting](./TroubleShoot.md#Troubleshooting) - This section will dive into Troubleshooting Velocity 

## [DNAC WIRELESS LABS](https://github.com/kebaldwi/DNAC-WIRELESS/tree/master/LABS#dnac-wireless-labs-)
This section is built out in LAB form to guide you through the typical steps required to enable the various automation tasks delivered by DNA Center specific to the wireless environment. This lab will give examples of how to automate the wireless equipment via DNA Center. The intention is to give examples that can be modified for your use and tested on equipment within the dCLOUD LAB environment. Additional information within the lab provides a well-rounded explanation of Automation methods. Lastly, the lab allows for customers to use DNA Center workflows to practice deploying Onboarding, Building a Cisco Unified Wireless Network, utilizing Application Policy automation across Cisco Wireless Platforms.

The goal of this lab is for it to be a practical guide to aid engineers to rapidly begin using DNA Center automation and help them work towards an adoption strategy. Additionally, this lab will give customers a permanent place to try out wireless automation and include configurations for various use cases. This environment will enable engineers to reduce the time and effort needed to instantiate the network.

As a result, customers will gain experience setting up Plug and Play ,onboarding and configuring Cisco wireless. Additionally, they will use templating and troubleshooting tools, which may help during faultfinding to determine what is failing in a deployment.

Please use this menu to navigate the various sections of this Github repository. Within the multiple folders are examples, explanation readme files for reference.

* [PnP Preparation](https://github.com/kebaldwi/DNAC-WIRELESS/blob/master/LABS/LAB1-PNP-PREP/) - This lab explains the overall Global Plug and Play set up steps
* [Controller PnP](https://github.com/kebaldwi/DNAC-WIRELESS/blob/master/LABS/LAB2-Pnp-Discovery/) - This lab explains in depth and how to use Plug and Play with a Cisco 9800 Controller
* [Controller HA](https://github.com/kebaldwi/DNAC-WIRELESS/blob/master/LABS/LAB3-Controller-HA/) - This lab will dive into Controller High Availability
* [WLANs](https://github.com/kebaldwi/DNAC-WIRELESS/blob/master/LABS/LAB4-WLANs/) - This lab will explore how to build Wireless LAN's
* [AP Provisioning](https://github.com/kebaldwi/DNAC-WIRELESS/blob/master/LABS/LAB5-AP-Provisioning/) - This lab will explore how to Onboard and Provison
* [Application Policys](https://github.com/kebaldwi/DNAC-WIRELESS/tree/master/LABS/LAB6-Application-Policy/) - This lab will explain Application Policys in DNAC and their use
* [Telemetry](https://github.com/kebaldwi/DNAC-WIRELESS/tree/master/LABS/LAB7-Telemetry-Enablement/) - This lab will explain how to deploy Telemetry for assurance
* [Advanced Automation](https://github.com/kebaldwi/DNAC-WIRELESS/tree/master/LABS/LAB8-Advanced-Automation/) - This lab will explore Advanced Automation examples 

## DCLOUD as a LAB
### Overview
To help aid customers toward success with DNA Center Automation, You may utilize the above labs as they have been designed to work within DCLOUD's [Cisco Enterprise Networks Hardware Sandbox](https://dcloud2-sjc.cisco.com/content/catalogue?search=Enterprise%20Networks%20Hardware%20Sandbox&screenCommand=openFilterScreen) Lab. This allows you to run these labs and gives not only an environment to try the various code, but to develop and export your own code for use in production. This give the customer an environment where they can safely POC/POV methods and steps without harming their own production environments. This also negaes the need for shipping equipment, lead times, and licensing issues needed to get moving rapidly. Please do adhere to the best practices for the DCLOUD environment when using it.

The environment allows for use with a web-based browser client for VPN-less connectivity, access as well as AnyConnect VPN client connectivity for those who prefer it. The labs are hosted out of our San Jose Facility and so you would choose sessions from US West. Choose the Cisco Enterprise Network Sandbox version you prefer. To access this or any other content, including demonstrations, labs, and training in Cloud please work with your Cisco Account team or Cisco Partner Account Team directly. Your Account teams will make sure the session is scheduled and shared for you to use. Once booked follow the guide within Github to complete the tasks adhering to the best practices of the dCLOUD environment.

### DCLOUD Labs
This lab environment has been tested on the following DCLOUD session: [Cisco Enterprise Networks Hardware Sandbox v2.1](https://dcloud2-rtp.cisco.com/content/demo/759521?returnPathTitleKey=favourites-view)

The DCLOUD session includes the following equipment:

Virtual Machines:

    DNA Center 2.2.3.4 or better
    Identity Services Engine (ISE) 3.0 Patch 4 or better (deployed)
    Identity Services Engine (ISE) 3.0 (Not deployed)
    Stealthwatch 7.4.0 or better
    FlowCollector 7.4.0 or better
    Cisco Prime Infrastructure 3.10  or better
    Script Server - Ubuntu 20.04  or better
    Wireless LAN Controller - C9800 running IOS-XE Bengaluru 17.5.1 code or better
    Windows 10 Jump Host 
    Windows Server 2019 - Can be configured to provide identity, DHCP, DNS, etc.
    Windows 10 Clients

Hardware Devices:

    ISR 4451 Router - 17.06.01a IOS-XE Code
    Catalyst 9300 Switch - 17.06.01 IOS-XE Code with Embedded Wireless Controller (EWC) and ThousandEyes Enterprise Agent
    9130AX Access Points
    Silex Controllers (3 Wired NIC's and 1 Wireless NIC)

The lab envionment that is available is depicted here:

![json](./LABS/LAB1-PNP-PREP/images/DCLOUD_Topology2.png?raw=true "Import JSON")

If you found this repository or any section helpful please fill in comments and [give feedback](https://app.smartsheet.com/b/form/f75ce15c2053435283a025b1872257fe) on how it could be improved.

