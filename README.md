# Creating a website with Glitch and testing it with Selenium

If you want to follow along you will need the latest version of Chrome, A GitHub account, VSCode, and Git Bash (or other Git client). The github account will be used to login/create an account on Glitch

What is Glitch? Glitch is free to use online node.js developement environment. It was created by FogCreek, a company that makes developer tools, created Trello and co-created Stack Overflow. Until recently Glitch was listed as Beta.

What is Selenium? Selinium is an open source UI testing library you can use to do acceptance or integration testing.

Steps:

1. Login to Glitch - Go to Glitch.com and login/create and account. I suggest using your GitHub account.
2. Select "Start a new project" then "Create a Node App" (I actually don't think it matters which one you choose because of the next step)
3. Click on your project name, then "Advanced Options", then "Import From GitHub" (You will probably have to do an additional step of authorizing an import by clickin "Grant Access" first). When prompted give "matthewbierman/LetsFindLunchSample" as your import location.
4. Now we can test our site, click on the "Show Live" button and a new tab will open up showing the index page of your site.
5. Enter a location (ZIP works fine) into the textbox, and click the "Lunch!" button and, if all is going to plan, receive your error.
6. Go back to previous (development) tab and lets look at the console log by clicking on the "Logs" button, you should see a log message of "Error:Google API Key is not defined"
7. Glitch stores keys and other information you do not want made public in a .env file, click on the .env file and enter in GOOGLEAPIKEY={key}. I will provide an active key during the demonstration.
8. After you update the environment, you should notice in the log window that the application will automatically be restarted, return to the Index page and you may notice that the page has been automatically reloaded.
9. Try to enter in another address or zipcode and click the "Lunch!" button, it should now add a place to the list whenever you click the button.


