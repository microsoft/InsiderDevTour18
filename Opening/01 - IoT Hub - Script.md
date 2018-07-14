## IoT Hub Demo 

### Prerequisites
- Twitter account
- Install VS Code

### Setup
**Note: If you already have an Azure account, you can skip this step**

1. Using an existing MSA, or create a new one, sign in at https://azure.microsoft.com/en-us/free and follow the steps for a free Azure account
2. Edge, login with a twitter account
3. Open VS code then hit F1 and then "Extensions: Install Extensions"
4.  Search and install:

	- Azure IoT Workbench

	- Azure Functions

**Note: DO NOT INSTALL C# extension (as it will show debug errors later)**

5. Select setting icon "don't show again"  on extension recommendations

6. Restart Visual Studio Code

### Set up Button and Base Project to deploy to Azure

1. Open VS Code and hit  F1 and then

	- IoT Workbench: New

	- Select folder under c\demos\IoT_Final

	- Select teXXmo (even if you don't have the physical button)

	- Select the template with Azure Functions

	- "Skip for Now" the Storage Account selection

	- Select don' t warn again on the request to install function tools
	- open the project folder

2. Hit F1 and then "IoT Workbench: Cloud"
	- Select Azure Provision

3. Create a new IoT Hub, select "Free Trial" or another subscription, 
	- give it a resource name
	- select a location
	- select Free for the scale
	- give it a name. 

> **Note:** You may hit an issue in creating the resource such as "provision canceled.". We are working on root cause, but in the meantime you can create the resource group (RG) through the Azure portal, and select that as the existing RG through code instead. You may also find this error goes away after a couple of attempts.

4. Once the Hub is created, you will see "IoT Hub provision succeeded." in the Output window. Take note of the Connection string in the Output window (for example, "HostName=...."), you will need this later

5. Create an Azure function, give it a name, create a new storage account and follow the steps. Wait until the function is created.

**NOTE: if you need to restart or resume, just type again IoT Workbench: Cloud and follow the steps**

6. Setup button (if you don't have a button, skip step 6-7 and use [simulator](https://prodiotsimulator.blob.core.windows.net/site/index.html) )

	- Press and hold the button until the light starts blinking in yellow

	- Search for WIFI networks (for example, ESP_44:6E:4A) and connect

7. In VS code, hit F1 and then "IoT Workbench: Device"

8.  Choose Config Device Settings

	- Config WIFI of IoT button, enter SSID and password of a Wi-Fi Hotspot the button can connect to. If the Microsoft Corpnet doesn't work, you can create an hotspot with your mobile phone

	- Config connection of IoT Hub device, select IotDevice connection (if you followed the steps above, it will be already prepopulated)
	- Shutdown IoT Button (necessary to save changes and reboot the device)

9. Write function
	- Open run.csx. Under log.info, add


```C#
Var client = new HttpClient();

client.PostAsync("", null);

```

10. Create LogicApp on Azure
	- Login to portal.azure.com

	- Create a resource, search "logic App"

	- Once it's created, go to the logic app designer (it will open automatically), select "when http request is received", add new step, add action, search twitter, select post new tweet. 

	- Sign in using same twitter account above
	
	- Click on "when conneciton is made" to get the connection string you will place back in your run.csx function. (in postAsync call)


11. Going back to VS code,  F1 & "IoT Workbench: Cloud"

	- choose Azure Deploy

	- Follow steps

	- As backup, save username and password in a text file (c\demos) 
 
 

## DEMO SCRIPT
This will be the part you show to the audiance.  Do to the delay in deploying, your button will actaully call the origional function already deployed to azure.

### CREATE WORKBENCH

1. In VS Code, hit F1
	- choose IoTWorkbench New, 

	- select empty folder on desktop

	- select  iot button, Azure Functions, Skip for now
2.  create your fucntion
	
	- hit F1 and select IoTWorkbench Cloud

	- choose Provision, select existing iothub, select existing device

	- give a name of a function, select resource group and storage

3. Open the function, explain log

4. In Azure, create the logic app

	- in Edge open azure portal. 

	- Add action, search twitter, select post a tweet & save

	- Copy url from when http request is received

	- CONNECT LOGIC APP to function
	
```
var client = new HttpClient(); 

client.PostAsync("", null);

```
5. Start iot workbench cloud deploy (but don't click!!!) and switch to the final project. Explain already deployed

6. Start the logs on the workbench

	- Azure menu on the left, select function, start streaming. 7. Explain
	- PRESS BUTTON
		- Backup/MVP: Edge simulator. Press send

	- FINALE
		- Show output window
		- Show edge window

	
## RESET SCRIPT

1. In Edge go to Twitter.com. Login and delete previous tweet (it doesn't send multiple tweets that look the same)

2. Login to Azure Portal with Megan

3. Reset Logic App
	- Open designer, remove the Twitter block
	-  Leave open in the designer mode

3. Open VS Code instance at c\demos\IoT_Final.
	-  Show run.csx, clear output window at bottom, select azure in the left vertical menu and select the function

	- Open VS Code instance blank

	- Get device connection string from myButton in VSCode (Explorer, at the bottom expand 'azure iot hub devices', right click on myButton to find the device connection string

	- Open https://prodiotsimulator.blob.core.windows.net/site/index.html  and paste the device connection string (don't press)
	- Create empty folder on desktop
