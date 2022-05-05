READme File Starts here:
This website is designed to showcase stock information, and allows users to learn more about the individuals running the company: Lauryn, Sara, and Sydne and their credentials. They provide investment services: personalized portfolio management, stock market investment consultation, and general brokerage services. 

The way to download our code and set up the app:
You’ll need to set up Node.js & Git development environment 
Which requires:
Having a GitHub Account
GitHub Desktop software installed on your device locally
Text Editor (we suggest using VS Code as it’s user-friendly)
Clone your repository
Install packages 
npm install
npm install nodemon -g
Our web application requires some services, most prominently are user authentication and data storage. To do that:
Create a Google Cloud Project
On Google Cloud Platform go to API credentials
Click on + icon 
Create Credentials", and choose "Create OAuth Client Id".
Click to "Configure Consent Screen"
Then leave it blank and return to edit it after deploying in latter step
Now create the "OAuth Client Id"
Choose a "Web application" type
Choose a name 
Set "Authorized Redirect URIs" (while the website is still in development, you’ll change this in latter steps)
Once the client is created, note the GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET, and set them as environment variables
Firebase Project
Create a new firebase project through Google Firebase Console
Select the Google Cloud project created in previous step from the dropdown list
Enable Google Analytics
Configure Google Analytics by:
Creating a google analytics account 
Automatically create a new property on the account
Firestore Database Setup
Use firebase guide to create a Firestore database for the Firebase project you just created. 
Products Collection
After the database has been created, you create a new collection called "products" with a number of documents. Create each document using an auto-generated "Document Id" and features. We created the following:
name → (string)
description → (string)
price → (number)
url → (string)
Google Cloud Service Account Credentials
To trace data from the firestore database set up, the app will need access to a Google API credentials file. 
Find the service account used for the firestore database set up and create new JSON credentials file , then download to the repo with the name "google-credentials.json". 
AlphaVantage API
Secure a premium AlphaVantage API Key from the professor (i.e. ALPHAVANTAGE_API_KEY).
Configuration
In the root of this repository’s directory, create a new file named ".env", with your own id’s to specify your credentials retained from the previous set up stage.
# this is the ".env" file…
ALPHAVANTAGE_API_KEY="________"
GOOGLE_CLIENT_ID="______.apps.googleusercontent.com"
GOOGLE_CLIENT_SECRET="______"
Usage
Run your local web server, then visit (then visit http://localhost:3000/ in the browser):
 (inserted code) npm run start-dev
Deploying
Sign up and install Heroku CLI
Check that you can log in and see your listed applications
Use the Heroku dashboard to create a new application server, your unique name of your application
Verify the creation of the App
Verify the created app is associated with the local repo with a remote address called "heroku":
Callback URL Set Up
Use your unique application name to register another callback url using  the Google API Credentials OAuth Console.
New call back should look like this:
https://UNIQUEAPPANME.herokuapp.com/auth/google/callback" (where UNIQUEAPPNAME is the unique name of your application, e.g. "my-unique-app").
Server Configuration
Using your Heroku dashboard, click "Reveal Config Vars" to configure the server’s environment
# setting environment variables:
heroku config:set ALPHAVANTAGE_API_KEY="_______"
heroku config:set GOOGLE_CLIENT_ID="______.apps.googleusercontent.com"
heroku config:set GOOGLE_CLIENT_SECRET="______"
# this is used for customizing the callback url, matching the callback url you registered via google console:
heroku config:set GOOGLE_CALLBACK_URL="https://YOUR_APP.herokuapp.com/auth/google/callback"
# choose your own secret string value instead of xyz999:
heroku config:set SESSION_SECRET="xyz99999"
Buildpacks
Utilize the buildpack plug in to configure remote credentials
heroku buildpacks:set heroku/nodejs
heroku buildpacks:add https://github.com/s2t2/heroku-google-application-credentials-buildpack
# stores contents of local credentials file (e.g. "google-credentials.json")
# ... into an environment variable on the server
# ... for use in conjunction with the buildpack, which then creates a file from those values
heroku config:set GOOGLE_CREDENTIALS="$(< google-credentials.json)"
Deploying
After completing configuration, deploy the source code on your text editor to the Heroku Server by pushing to GitHub
git push heroku main
License
Creative Commons Attribution 4.0 International License
Copyright (c) 2022 (insert your name)
This allows you to 
Share — copy and redistribute the material in any medium or format
Adapt — remix, transform, and build upon the material for any purpose, even commercially.
This does not provide a warranty, meaning privacy or publicity laws may limit how you may utilize your application and its data. 


