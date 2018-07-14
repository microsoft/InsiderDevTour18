# SETUP

## Purpose of this bot / talking points
This bot has been made for an insurance company to help users to better understand some medicines and how to also easily locate a pharmacy or hospital near you. It uses several of our AI services such as LUIS, to understand the questions of a user or cognitive services computer vision to recognize a picture of a medicine (not active in the demo but available in the code). It uses cards to simplify interactions as well as Bing services to locate the pharmacy and give you directions. The idea of this demo is to show the kind of elaborated bot you can create to boost the productivity of users by mixing several of Microsoft services. It also shows how easy it is to test it in the Azure Portal and how to quickly reach several channels such as Skype, Teams and others. 

## Phase 1 - Clone and run locally
- Start by **cloning** this repo (do not download it as .ZIP) on your hard drive: https://github.com/dupuyjs/Medication-Helper via the command 'git clone https://github.com/dupuyjs/Medication-Helper'
- Run **'npm install'** in the directory (you may have Python errors, ignore them)
- You need to **register and train a LUIS Application**, go to https://www.luis.ai/applications. After logging in with your provided account, click **Import New App** and follow the directions. 
- From the **Upload File** dialog, select the **luis.json** file under the **Medication-Helper/data** directory. When directed to the dashboard, **click on Train**. It may take a few minutes to finish. 
- Once done, you can test your LUIS model by typing out an utterance on the Test pannel. Try **'find a pharmacy in Paris'**, for instance. 
- Finally, **click on Publish App**, assign a key, and click Publish. You will be given an **Endpoint url**. Copy this URL somewhere as you will need it later like:

COGNITIVE_LUIS_URL = "https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/YourApplicationId?subscription-key=YourSubscriptionKey"

- **Generate a Bing Key**. Go to: https://www.bingmapsportal.com/Application and Sign-in using a MS Account to generate a key.  You will need to use a personal MSA for this as the Office dev tenant account does not work with the free Bing trial.
- Go to **My account -> My Keys** and create a new key. **Copy this key** as you will need it later like:

BING_MAPS_API_KEY = "YourSubscriptionBingKey"

- Using **VS Code**, create a file named **.env** (yes, just '.env') in the root directory (where app.ts live) and put those 2 keys inside:

COGNITIVE_LUIS_URL = "https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/YourApplicationId?subscription-key=YourSubscriptionKey"
BING_MAPS_API_KEY = "YourSubscriptionBingKey"

- **Download BotFramework Emulator** v3.5.36 (available for Mac, Windows, and Linux) via the GitHub releases page: https://github.com/Microsoft/BotFramework-Emulator/releases (the last v3 release, not a v4 alpha). Direct PC link version: https://github.com/Microsoft/BotFramework-Emulator/releases/download/v3.5.36/botframework-emulator-Setup-3.5.36.exe
- Run **'npm run start'** in the Medication-Helper directory.
- Start BotFramework Emulator and Select http://localhost:8080/api/messages to start interacting with your bot.

You've reached the end of the 1st setup phase. Now you've confirmed it works, you have to deploy it to Azure. 

## Phase 2 - Deploy to Azure

1. Go to http://portal.azure.com with your provided account for your city
2. Associate a **Free Azure Subscription** on it: https://azure.microsoft.com/en-us/free (but you'll need to provide a real credit card to validate the free activation)
3. Create a **new App Services - Web app** 
4. Give it a name like **InsiderBotWebApp**, create a new resource group, choose **Windows** as the OS, **disable Application Insights** and click **Create**
5. Go to this new resource created in the portal and to **Deployment -> Deployment options**
6. Choose **Source -> Local Git Repository** and click **Ok**
7. Go to **Deployment credentials** and **create a new username/password** if needed
8. Go to **Overview** and copy the **Git clone url**
9. Open a **Powershell command** inside the folder where you've cloned the Bot repository
10. Enter this command: **git remote add azure [YourGitCloneURL]**
11. Enter: **git push azure**
12. You will be prompted to **enter your credentials** you've created in 7
13. Go to **Settings -> Application settings** and under the **Application settings section**, create 2 keys: COGNITIVE_LUIS_URL and BING_MAPS_API_KEY with the values you've created before and click save

Additional links that may help you during this 2nd setup phase:

- https://docs.microsoft.com/en-us/azure/app-service/app-service-deploy-local-git
- https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-deploy-azure?view=azure-bot-service-3.0

We now have to register this bot hosted in this Azure Web App. 

## Phase 3 - Register the Bot

1. Create a **new Bot Channels Registration** from the Azure Portal
2. Name the bot **InsiderBot**
3. **Disable Application Insights**
4. Click on **Auto create App ID and password**
5. Click **Create New** in the Create Microsoft App ID blade
6. In the Create new Microsoft App ID blade, click **Create App ID in the App Registration Portal**. You'll be redirected to: https://apps.dev.microsoft.com/
7. Copy the **App ID** and click on Generate an app password to continue. **Copy the generated password**. You won't have a second chance to copy it so pay a lot of attention there.
8. **Paste both values** in the Azure Portal 'Create new Microsoft App ID' blade and click OK
9. In the Bot Channels Registration blade, click **Create**
10. Go back to the **Web App** in the **Settings -> Application settings -> Application settings** section, create 2 keys: MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD filled with the 2 values copied just before and click Save
11. In the **Web App Overview panel**, copy the URL that should be https://InsiderBotWebApp.azurewebsites.net
12. Go to the **Bot Channels Registration settings** and enter this URL inside the **Messaging endpoint**: https://InsiderBotWebApp.azurewebsites.net/api/messages
13. Go to **Bot Management -> Test in Web Chat** and enter 'pharmacy' to enable the first bot interaction

Additional link that may help you during this 3rd setup phase:
- https://docs.microsoft.com/en-us/azure/bot-service/bot-service-quickstart-registration?view=azure-bot-service-3.0

# DEMO

- In the **Azure Portal**, navigate to the **InsiderBot resource**
- Click to **'Test in Web Chat'** and say **'I'm looking for a medical location'** to activate the bot
- Select **'pharmacy'**
- Enter: **'39 quai du president roosevelt, issy, france'** as the address (MS France building)
- It should display a map. Say: **'Yes'**
- Several pharmacy should be found, you can click **'get directions'** to open bing maps in another tab. 

Note: you can try with a local address in your current country but please test before that the bot manages to find all the associated details. 
This bot can do many other things for you like describing medicines, translating the description or recognizing an image of a medicine box but we haven't set the various keys to activate those features. Just explain to the audience that you can do many other useful actions with such bots.

- Go to **Bot Management -> Channels** and click on **Teams**
- **Agree** to the terms and click Done
- **Click on 'Microsoft Teams'**, it will launch the app and create directly a new channel for the bot for you
- Say **'I'd like to go to the hospital'**
- Enter your address, you could even try to change it like 'Microsoft France, Paris' or 'Microsoft Italy'

>**Note:** We have had reports that some people were receiving an error messsage of "Sending new messages to this bot has been disabled by your administrator". Try the following: 1) Ensure you have enabled "Allow sideloading of external apps" in your Office tenant's admin portal (see  [here](https://docs.microsoft.com/en-us/microsoftteams/admin-settings)); 2) Re-add the Teams channel to your Bot as described above (and [here](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-3.0)). 
