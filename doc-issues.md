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
