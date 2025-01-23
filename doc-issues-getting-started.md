## Getting Started Big picture
Unclear to me why we are creating locations or sites. What are we working towards? 
Seeing "To create a new Device, you will need an existing Location or need to create a new Location instance."
https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/creating-devices/#creating-a-location
Made me think, oh, that makes sense, but why didn't we do locations first then? Or what else do I need to know is required to make things get started?

Tutorial idea: Use the demo instance data as reference. Right now the Getting Started Feature Guide assumes empty data set, though that makes sense given a fresh install would have no data:
https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/creating-location-types-and-locations/#creating-location-types-and-locations


## Getting Started Step by Step

### Creating a Device Role

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/creating-devices/#creating-a-device-role
Click on Devices in the left sidebar menu
should be
Click on Organization in the left sidebar menu 
(per the screenshot)


### Location Types and Locations

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/creating-devices/#creating-a-location-type
```
...
Find LocationTypes
should be
Find Location Types
...
Select a Parent LocationType if needed
should be
Select a Parent Location Type if needed
...
Populate the LocationType's Name
should be
Populate the Location Type's Name
...
Select the desired ContentTypes for this LocationType (in this case dcim.device).
should be
Select the desired Content Types for this Location Type (in this case dcim.device).
```


https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/creating-devices/#creating-a-location

```
Select a LocationType
should be
Select a Location Type
```


https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/creating-location-types-and-locations/#creating-location-types-and-locations

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/images/getting-started-nautobot-ui/1-create-location-type.png
- image shows "city" when that is not the text being used in the example. 

"The screenshots below show the creation of each Location."
 - There is only one screenshot below

```
North America:

Leave the Parent blank; North America will be a top-tier Location
Select Continent from the Location Type drop-down menu selector
Populate the Name to be North America
Click on the Create and Add Another button
```

- When I click on Create, it says "status" is a required field even for continent,  no step for status in the list above for North America:
https://demo.nautobot.com/dcim/locations/add/
- When I add Country after adding another, status is already set to Active from my previous selection. 


### Platforms
https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/platforms/#specifying-the-devices-platform
While on the Add a new device/Editing device page, scroll down to the 'Management' section
In the Platform field drop-down selector, select the appropriate Platform

The instructions assume you configure platform under "Management" - when in reality it was under "Software / Platform"
Screenshot for this also needs to be updated for new structure:
https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/images/getting-started-nautobot-ui/44-add-platform.png

### Tenants

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/tenants/#assigning-a-tenant-to-an-object
"Assigning a Tenant to an Object
It is simple to assign a Tenant to an existing object. This next example will add a Tenant to an existing Device."

Out of place tone saying something is simple and "this next example" as opposed to previous steps did not have that type of introduction

### Interfaces

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/interfaces/#interface-add-example
Interface Add Example¶
Let’s take an example:
We want to define a Device Type of MX240-edge
This Device Type will have 20x 10G (xe-[0-1]/0/[0-9]) Interfaces and one LAG (ae0) Interface
The xe-0/0/9 and xe-1/0/9 Interfaces will be members of the ae0 Interface

Inconsistent tone to other Getting Started, also not numbered like other examples, used bullets. Need some transition to make clear the following sub-section is expanding on these goals, maybe aligning Sub headings into the bullet points like
- Creating a Device Type: We want to define a Device Type of MX240-edge
etc.


https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/interfaces/#creating-a-device-type 
To create a Device Type:

Click on Devices on the left sidebar.
Locate Device Types option in the drop-down menu
Click on the + button to add a new Device Type
A Device Type requires a Manufacturer object to be created prior to creating the Device Type
Device Type requires Manufacturer, Model, and Height values at creation
In this example, name the Device Type APDU9941
On the home page for the specific Device Type, click on +Add Components and select Interfaces


Needs guidance on sample data to put in Manufacturer and Height values. Skipped the step of "Create"  before the final step in this sequence. 

Saw this note and not sure if still relevant since very old version:
```
Note

As of this writing (Nautobot 1.0.3), Interfaces cannot be assigned in to a LAG in the Device Type template; component Interfaces must be designated in the specific instantiation of a Device created from the Device Type.
```

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/interfaces/#creating-a-new-device-using-the-device-type

`Device type select APC APDU9941 (this will show up as a fusion of the Manufacturer (APC) for the Device Type and the Device Type (APDU9941) Names)`

the screenshot shows device type with just APDU9941, but when I selected it from the drop down it had both `APC` and `APDU9941` together already in the `Device type` field. I could still select APC on manufacturer, but was different than the instructions.

Instructions did not tell me to set it as active status, which is required. 

### VLANS and VLAN Groups

https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/vlans-and-vlan-groups/#creating-the-vlans
```
Now we'll create two instances of VLANs, each with ID = 100 and Name = vlan 100 and an Active Status. The differentiator will be that one instance will be assigned to the Vancouver 1 Site and the other to the Ottawa 1 Site.

On the Add a new VLAN form:

Populate ID with 100
Populate Name with vlan 100
Select Status as Active
Select ANG01 from the Location selector drop-down
Click on the Create and Add Another button
On the Add a new VLAN form:

Populate ID with 100
Populate Name with vlan 100
Select Status as Active
Select BRE01 from the Location selector drop-down
Click on the Create button when complete with the second instance
```


The instructions say to create two instances of ID vlan 100, but when I create one vlan 100 and do create another, it already has the ANG01 populated in the form for VLAN 100. The instructions are written with a screenshot indicating that you can only have one location per form drop down, and that it is not prepopulated from the previous submission on location. 

```
Once you've created the three VLANs and then hit the Create button, you will be taken to the VLANs main page
```

After the final create, I am taken to the VLAN detail page of the last one created, ` vlan 100 (100)` for BRE01 in this case. I will need to navigate to the VLANs main page. 



```
Assigning VLANs to an Interface¶
To assign a VLAN to an Interface:

Click on IPAM on the left sidebar menu
Select Devices to go to the Devices main page
Click on the name of the Device you wish to add a VLAN to (ang01-edge-01) in this example
Click on the Edit button for the xe-0/0/0 Interface to go to the Editing interface xe-0/0/0 page
On the Editing interface xe-0/0/0 page, set 802.1Q Mode to Access (or whatever mode you need) and then click on the VLAN drop-down selector. Notice that there are two choices:
One choice is the vlan 100 instance specifically assigned to the ANG01 Location
The other choice is vlan 200, which was not assigned to a Location, and thus has a global scope
```

There is no `Devices` under `IPAM` probably should just be Click on Devices on sidebar



https://docs.nautobot.com/projects/core/en/latest/user-guide/feature-guides/getting-started/ipam/#assigning-ip-addresses

```
To assign an IP Address to a specific Device and Interface:

Click on Devices in the left side navigation menu
Click on Devices to go to the main page for Devices
Find the Device whose Interface you wish to associate to an IP Address and click on it
Go to the Interfaces tab and look for the row with the Interface you are interested in
Click on the edit button for the Interface (a pencil icon)
```

Other guides give specific instances from the demo app to use and this one doesn't, though you can imply from the screenshots what to do. Diatraxis tone inconsistent. 


### The Search Bar

example two steps
```
Example two shows a Device-specific search:

Search for edge
This takes you to a search results page
In the drop-down selector to the right, select Devices
Search results for Devices with edge in the name
Tenants for each Device (if applicable)
Device Type for each Device
Location for each Device
```

The steps starting at Teneants don't make sense, I am not sure what action I am taking. 

```
END OF Getting Started in the Web UI GUIDE
```

Unusual and not in any other guide