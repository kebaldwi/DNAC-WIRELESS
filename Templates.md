# Building Templates
In this section we will explain how to build a template in DNA Center.

## Intent Based Networking
Either one or multiple Templates may be used to deploy Intent in combination with the Design Settings and Policies deployed within the UI. One or Multiple templates may be used in Onboarding (PnP) or Day N methods. Day N methods are designed for making ongoing changes and may require 'no' statements depending on the configuration construct being modified. 

Additionally:
1.	Intent can be defined as the set of configuration constructs deployed via a template.
2.	Variables can be used to modify or choose between constructs deployed via decision (‘IF’) statements
3.	Repetition of any construct may be introduced through the use of Looping structures on any device.
4.	Variables may be used when the device is being onboarded or provisioned

## Phylosophies
There are a number of coding paradigms which various programmers use when building, maintaining and publishing programming code which are extremely useful when trying to integrate programmability for use in modern day infrastructure use cases. Lets deal with each concept in turn:

  - imperative in which the programmer instructs the machine how to change its state
      - procedural which groups instructions into procedures
      - object-oriented which groups instructions together with the part of the state they operate on
  - declarative in which the programmer merely declares properties of the desired result, but not how to compute it
      - functional in which the desired result is declared as the value of a series of function applications
      - logic in which the desired result is declared as the answer to a question about a system of facts and rules
      - mathematical in which the desired result is declared as the solution of an optimization problem
        
## Modular Programming    
Modular programming is a software design technique that emphasizes separating the functionality of a program into independent, interchangeable modules, such that each contains everything necessary to execute only one aspect of the desired functionality.

A module refers to high-level decomposition of the code of an entire program into pieces: structured programming to the low-level code use of structured control flow, and object-oriented programming to the data use of objects, a kind of data structure.

This calls out two very key points: 

  1. **Functionality**
     Code segmented into small chunks to reduce complexity 
  2. **Reusability**
     Modular code designed for reuse as parts of functions

## Parsing IOS Configurations
As you begin your builds of Templates it helps to analyze the various IOS configurations and group logical syntactic components and where we see reusability, for example in service statements, we can create groupings of commands and put those into either separate templates (modules) to be used in a composite template or separate them into a separate template you can reuse.

Remember the DNA Center **Network Profile** that you will build offers a couple of options, additional templates or in the Day N role, a composite template. Either is available for use.

Once you have grouped configuration snippets into separate logical constructs you can then see what additional platforms you might apply them too, as this will steer you in the direction of whether multiple modules (snippets) are required or whether you will need a complete duplication of certain functions.

Once we have identified all the various modules we will need, we can then start to analyze which of the codes the Design App can facilitate, and ensure the design has those settings and remove them from the modules.

## Templates
We have two templates offered in DNA Center. A **Regular Template** which is designed to stand alone for a specific function and a **Composite template** which will group standard templates and which can only be used in Day N Projects.

As we build out a Regular Template we can either as has previously been mentioned put all the IOS commands which makes the configuration within the template more complex to maintain, or we can separate out the various sections into separate templates and call them as additional templates in either the Onboarding or Day N flows.

Once you have created a new template and pasted the IOS configurations into the template editor you can then look for values which can be replaced by variables. 

### Variables
Variables are used to allow scripts or code for that matter to be reused. A variable within a script allows us to replace the data on demand thereby allowing the reuse of parts of or entire templates. Variables may be defined in a couple of ways but the data entered will either numerical or string. A numerical value is just that a number where as a string is either a line of text or perhaps just a name.

Analyse your configuration to make optimium use of variables which will allow reuse. Please refer to [Variables](./Variables.md).

### Velocity Scripting
To further simplify your IOS configuration analyze your IOS template for manipulations that might occur if it were a 24 port switch as opposed to a 48 port switch, and then build logical constructs to allow for one template to address multiple platforms.

While it is possible to take a CLI script for one device and create a template for one device at a time, that would leave us with a lot of templates and make it harder to make changes on an ongoing basis. Using the techniques of Velocity Scripting will allow us to deploy equipment with scripts which can be reused on a broader basis, allowing us to keep configurations similar for conformity reasons but also to reduce the number of places where changes would have to be made. For additional information please see [Velocity Scripting](./Velocity.md).

Within these logical constructs you have many tools, please review each section as needed:
* [If Statements](./Velocity.md#if-statements)
* [Macros](./Velocity.md#macros)
* [Loops](./Velocity.md#foreach-loops)
* [Multiline commands](./Velocity.md#multi-line-commands)

## Template Creation
Cisco DNA Center provides regular and composite configuration templates. CLI templates let you choose the elements in the configurations. Cisco DNA Center provides variables that you can replace with actual values and logic statements.

  * Create a Regular Template
  * Create a Composite Template
  * Edit Templates

### Create a Regular Template
1. From the Cisco DNA Center home page, choose Tools > Template Editor. By default, the Onboarding Configuration project is available for creating PnP templates. You can create your own custom projects. Templates created in custom projects are categorized as day-N templates.
![json](images/GoToTemplateEditor.png?raw=true "Import JSON")
2. In the tree pane, select the project under which you are creating templates, and click the gear icon > Add Templates. Alternately, click > Add Templates.
   - **Note:** The template that you create for day 0 can also be applied for day N.
![json](images/CreateTemplate.png?raw=true "Import JSON")
3. In the Add New Template window, click Regular Template.
![json](images/AddNewTemplate.png?raw=true "Import JSON")
4. In the Name text box, enter a unique name for the template.
5. In the Project Name drop-down list, select the project. 
   - The drop-down list is enabled if you are navigating from the > Add Templates path. 
   - The drop-down list is disabled if you select a project and click the gear icon > Add Templates in the tree pane.
![json](images/SelectTemplateProject.png?raw=true "Import JSON")
6. In the Description text box, enter a description for the template. **optional**
7. In the Tags text box, enter an intuitive name to tag the templates. **optional** 
   Tagging a configuration template helps you to:
   - Search a template using the tag name in the search field.
   - Use the tagged template as a reference to configure more devices.
   - **Note:** If you use tags to filter the templates, you must apply the same tags to the device to which you want to apply the templates. Otherwise, you get the following error during provisioning: Cannot select the device. Not compatible with template.
8. Click Edit to view the selected device types and choose the device types that you want to apply to the template.
   - To view the selected devices, choose Selected from the Show drop-down list. By default, all device types are displayed.
   - There are different granularity levels for choosing the device type from the hierarchical structure. The device type is used during deployment to ensure that templates deploy devices that match the specified device type criteria. This lets you create specialized templates for specific device models.
   - **Note:** Template Editor does not show device product IDs (PIDs); instead, it shows the device series and model description. You can use cisco.com to look up the device data sheet based on the PID, find the device series and model description, and choose the device type appropriately.
![json](images/SelectDeviceTemplate.png?raw=true "Import JSON")
9. After choosing the device types, click Back to Add New Template.
10. From the Software Type drop-down list, choose the software type: IOS, IOS-XE, IOS-XR, NX-OS, Cisco Controller, Wide Area Application Services, Adaptive Security Appliance, NFV- OS, and Others.
    - For more information on the Cisco Wireless Controller supported software versions and the minimum supported version, see Cisco DNA Center Supported Devices document.
    - For example, if you select IOS as the software type, the commands apply to all software types, including IOS-XE and IOS-XR. This value is used during provisioning to check whether the selected device conforms to the selection in the template.
![json](images/SelectOSTemplate.png?raw=true "Import JSON")
11. In the Software Version text box, enter the software version. During provisioning, Cisco DNA Center checks to see if the selected device has the software version listed in the template. If there is a mismatch, the provision skips the template. **optional**
12. Click Add. The template is created and shown in the tree view under the project you selected.
![json](images/AddTemplate.png?raw=true "Import JSON")
13. You can edit the template content by selecting the template that you created in the left menu. To edit the template content, see Edit Templates.
14. In the Template Editor window, enter content for the template. You can use the Velocity Template Language (VTL) to write the content in the template.
![json](images/EditTemplateWindow.png?raw=true "Import JSON")
15. To save the template content, from the Actions drop-down list, choose Save.
16. To commit the template, from the Actions drop-down list, choose Commit. You can see only the committed templates in the network profile section.
    - **Note:** You can associate only a committed template to a network profile.

For more documentation please see: [User Guide](https://www.cisco.com/c/en/us/td/docs/cloud-systems-management/network-automation-and-management/dna-center/1-3-3-0/user_guide/b_cisco_dna_center_ug_1_3_3_0/b_cisco_dna_center_ug_1_3_2_0_chapter_01000.html#create_regular_templates)

If you found this repository or any section helpful please fill in comments and [give feedback](https://app.smartsheet.com/b/form/f75ce15c2053435283a025b1872257fe) on how it could be improved.
