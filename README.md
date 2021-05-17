# Translate CCP Demo for Amazon Connect

This is a sample project that demonstrates using Amazon Translate with Amazon Connect chat to perform real-time translation on chat messages, allowing a user to support dozens of languages. The web app supports multi-chat allow an Amazon COnnect Chat user to support multiple languages concurrently. Deployment is using the Amplify UI (No CLI access required) and is using serverless architecture. Deployment takes about 10 minutes. 

Demo

<img src="./artifacts/TranslateDemo.gif" width="50%">

Architecture

<img src="./artifacts/Arch.png" width="50%" >

## Pre-Reqs

- Existing Amazon Connect Instance ([Create an instance in 3 easy steps](https://docs.aws.amazon.com/connect/latest/adminguide/tutorial1-set-up-your-instance.html))
- Github account ([Create a free GitHub account](https://github.com/join))

### Install

Click the below button

[![amplifybutton](https://oneclick.amplifyapp.com/button.svg)](https://console.aws.amazon.com/amplify/home#/deploy?repo=https://github.com/TTEC-Dig-VF/Amazon-Connect-Chat-Translate-Demo)

- Connect to Github
- Click on 'Create new role' then `Next: Permissions` > `Next: Tags` > `Next: Review` finally `Create role`

Expand `Environment variables` and add the below 2

- `REACT_APP_CONNECT_REGION` = `AWS Region`  (Example `eu-west-2`)
- `REACT_APP_CONNECT_INSTANCE_URL` = `Amazon Connect URL` (Example `https://<<INSTANCE_NAME>>.awsapps.com` or `https://<<INSTANCE_NAME>>.my.connect.aws`)

<img src="./artifacts/Environment variables.png" width="50%">


Once the app is ready, about 8 mins, you then need to update the allow the WebApp to allow CCP to be loaded as an iFrame.

<img src="./artifacts/Web app deployed.png" width="50%">

* Navigate to the Amazon Connect console, and select on your Amazon Connect instance name
* Goto `Approved origins` then `+ Add origin`
* Enter the URL that Amplify generated for you, then click `Add`  (Example URL `https://main.d13aaabbbccc.amplifyapp.com`)

Testing

* Login to the amplify web app, create an account, then login to Connect
* Start a customer chat (Goto `https://<yourConnectInstanceURL>/connect/test-chat`)
* Connect through to your agent that's running the new WebApp
* As the customer type some text in French and you'll see the agent translate app show 'Translate - (fr) French' 
* As the agent type in English into the translate textbox and press enter. This will be converted to french and sent back to the customer as french

### Custom Terminologies

* Custom Terminologies is supported by the web app, and a file is created upon installation which can be updated by following the steps below:
  * Update the provided Custom Terminologies files
    * Go to https://console.aws.amazon.com/translate/home?#terminology
    * Click on the radio button next to `connectChatTranslate`
    * Download the CSV
    * Edit 
    * Update the `connectChatTranslate` custom terminologies with the updated CSV
  * For more information visit: https://docs.aws.amazon.com/transcribe/latest/dg/how-vocabulary.html


### Features

* The web app looks for a contact attribute of `x_lang` if set then the language will be set accordingly. (Supported languages for translation: https://docs.aws.amazon.com/translate/latest/dg/what-is.html)
* If no `x_lang` contact attribute is set, the FIRST message from the customer will be used to perform language detection using Amazon Comprehend. (Supported languages for detection: https://docs.aws.amazon.com/comprehend/latest/dg/supported-languages.html)
* Agent side is hardcoded to `'en'`

### Costs

All the services used are included within the [AWS Free tier](https://aws.amazon.com/free/) offer. However, should you exceed this you will be charged for the services consumed. Please see the [clean up](https://github.com/TTEC-Dig-VF/Amazon-Connect-Chat-Translate-Demo#clean-up) section to delete all deployed infrastructure.
### Todo

* More testing & code clean up
* Enable language selection for the customer side
* Enable language section for the agent side
* Translate message prior connect to an agent
* Store state locally to survive page refresh
* Prevent translation attempt for same language pairs


### Clean up

Within the amplify UI navigate to your app, on the top right select `Actions` and then `Delete app`.
