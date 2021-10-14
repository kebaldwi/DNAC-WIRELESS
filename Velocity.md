# Velocity Scripting 
This section will describe the various tools and techniques used to make a powerful script out of normal CLI command scripts which are used by organizations on IOS devices around the world. This section is an attempt to demystify the hows and to bring clarity on what is truely possible. While it is possible to take a CLI script for one device and create a template for one device at a time, that would leave us with a lot of templates and make it harder to make changes on an ongoing basis. Using the techniques below will allow us to deploy equipment with scripts which can be reused, allowing us to keep configurations similar for conformity reasons but also to reduce the number of places where changes would have to be made. 

To that end it is important to write modular scripts which make use of all the power of programming but allow us to do it within the DNAC platform as templates. 

Velocity language typically allows for If/elseif/else constructs, macros and more.

## Comment Statements
Comment statements are a useful tool for scripting and allow for descriptive text to be used to explain the design or functionality of code. In simple IOS configurations anything after a '!' is not implemented but this is not true in velocity. To that end anything with a '!' is rendered as actual code so if something is desired not to be processed within this templating language please use '##' sequence.

```
## Comments can be placed here
```

## Variable Usage
Variables when combined in Velocity for the most part you can use them by calling them in either Formal or Regular notation.

```
Formal Notation.        ${Switch} 
Regular Notation:       $Switch
```

There are occassions where those viarables will need to be used in descriptions or other areas where we would typically have a string. In some occassions concatenation renders well, but in others we will need to define those by enclosing them in quotation marks. 

Take this example of a macro with an interface description:

```
#macro(uplink_interface)
 description "${site_code} - ${closet}"
```

### Combining Bind Variables
You can also extrapolate variables from known values once the device has been onboarded into the inventory. If the device was populated with the pnp startup-vlan command value then then the native vlan would be set to follow that automatically on the target switch. You could bind a variable and then use that to determine many other values for the device automatically.

```
#set( $voice-offset = 4000 )
#set( $data_offset = 1 )
#set( $integer = 0 )
#set( $native_vlan_var = $native_bind )
#set( $native_vlan = $integer.parseInt($native_vlan_var) )
#set( $data_vlan = ${native_vlan}-${data_offset} )
#set( $voice_vlan = ${data_vlan}+${voice-offset} )
```

## IF Statements
IF statements are a useful tool for scripting and allow for a decision tree in which under certain circumstances various commands can be used alone or in combination. To create an IF statement examples have been provided below. That said it is important to understand that the IF statement may be used alone or in combination with the following;

```
#if
#end

#if
#else
#end

#if
#elseif
#else
#end
```

That said it is important to understand that these decisions allow for you to script for multiple circumstances or platforms allowing you to write code which can be reused and therefore modular.

If/elseif/else construct with a check to see if data in variable contains a string:

 ```
 #if( $hostname.contains("C9300-48") )
    !some commands
 #elseif( $hostname.contains("C9300-24") )
    !some more commands
 #else
    !even more commands
 #end
 ```
 
## Macro's
A Macro is a snippit of code which can be called over and over again within a template. Take the following example into consideration. Alone the Macro does not seem that powerful but when combined with the previous sections IF statement it suddenly allows for a more powerful script.

Macro format is as follows:

```
      #[{]macro[}] (vmname $arg1[= def1] ... $argn [= defn] ]) [ VTL code ] #[{]end[}]

      Usage:

            vmname          - Name used to call the VM (#vmname)
            $arg1 ... $argn - Arguments to the VM. There can be any number of arguments, but the number 
                              used at invocation must match the number specified in the definition, unless 
                              there is a default value provided for missing parameters.
            def1 ... defn   - Optional default values provided for macro arguments. If a default value is 
                              provided for an argument, a default value must also be provided to all subsequent arguments.
            VTL code        - Any valid VTL code, anything you can put into a template, can be put into a VM

```

An example Macro of interface configurations:

```
#macro(Interfaces)
int lo 0
  desc mgmt address
  ip address 10.0.0.${Switch} 255.255.255.255
!
int vlan 1
  desc mgmt vlan - with pnp
  ip address 10.1.1.${Switch} 255.255.255.0
!
#end
```

When combined with the IF statements below, the above Macro allows for various IP's to be set on the same interface on multiple switches as long as the hostname variable contains a specific string value.

```
#if( $hostname.contains("C9300-48") )
#set( $Switch = 30 )
#Interfaces
#elseif( $hostname.contains("C9300-24") )
#set( $Switch = 20 )
#Interfaces
#else
#set ( $Switch = 10 )
#Interfaces
#end
```

## For Loops
A For loop allows for multiple iterations of a sequence of commands perhaps including some of the constructs mentioned above to iterate through and on each occasion use a different value.

Command Construct:

```
#[{]foreach[}] ( $ref in arg ) statements [#[{]else[}] alternate statements] #[{]end[}]

Usage:
    $ref                 - The first variable reference is the item.
    arg                  - May be one of the following: a reference to a list 
                           (i.e. object array, collection, or map), an array list, or the range operator.
    statements           - What is output each time Velocity finds a valid item in the list denoted above as arg. 
                           This output is any valid VTL and is rendered each iteration of the loop.
    alternate statements - What is to display whenever Velocity did not enter the loop (
                           when arg is null, empty, or doesn't have any valid iterator).
```
Additionally you can use these methods within the loop:

```
    $foreach.count : 1-based loop index
    $foreach.index : 0-based loop index
    $foreach.first : true on the first iteration
    $foreach.last : true on the last iteration
    $foreach.hasNext : false on the last iteration
    $foreach.stop() : exists the loop, synonym for #break
```

An example of a For Loop

```
    Reference Example: 
    
    #foreach ( $Vlan in $Vlans ) 
       interface vlan $Vlan 
    #else 
       no interface vlan $Vlan
    #end
    
    Array List Example: 
    
    #set( $ID = 15 )
    #foreach ( $Vlan in ["10", $ID, "20"] ) 
       interface vlan $Vlan  
    #end
    
    Range Operator Example: 
    
    #foreach ( $Vlan in [1..3] ) 
       interface vlan $Vlan 
    #end
```

For Safety the maximum allowed number of loop iterations can be controlled engine-wide with velocity.properties. By default, there is no limit:

```
    #The maximum allowed number of loops.
    directive.foreach.max_loops = -1
```

## Multi Line Commands
These can be used for building entries for multiple lines which need to be used within a command like with banners.

```
!BANNER LOGIN
<MLTCMD>banner login ^
  Session On $hostname Is Monitored!!!
  *****************************LEGAL WARNING************************************
  * This device is part of a Demonstration computer network and is provided for*
  * official use by authorized users ONLY. Any information, documents, or      *
  * materials in the network are the property of this firm. Unauthorized use,  *
  * duplication, or disclosure of information or systems in this network is    *
  * strictly prohibited by Federal Law (18 USC 10130). Use of this network     *
  * constitutes consent to monitoring which may be released to firm management *
  * and/or law enforcement agencies and may result in disciplinary action,     *
  * civil action, and/or criminal prosecution.                                 *
  ****************************LEGAL WARNING*************************************
^</MLTCMD>
```

If you found this repository or any section helpful please fill in comments and [give feedback](https://app.smartsheet.com/b/form/f75ce15c2053435283a025b1872257fe) on how it could be improved.

Special mention to: https://explore.cisco.com/dnac-use-cases/apache-velocity as examples and extrapolations were made using this documentation.
