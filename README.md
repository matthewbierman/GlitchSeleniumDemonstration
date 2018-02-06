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
10. Next we are going to run some automated test against against our new site, start by cloning the project using Git
11. [Optional] Create a directory for the test project, using Git Bash I entered in:
    cd C:
    mkdir testproject
12. Open Git Bash and use the "cd" command to make the current directory your project directory "cd testproject"
13. Clone the test project using the following command "git clone https://github.com/matthewbierman/LetsFindLunchTestSample.git"
14. Open VS Code.
15. Navigate to your project folder, I used File->Open Folder and navigated to "C:\testproject\LetsFindLunchTestSample"
16. You may get a notice about missing packages, if you do you can restore them using the "Restore" button provided, other wise open the terminal (View->Integrated Terminal) and run the command "dotnet restore". This downloads the needed packages/references to the Selenium Webdriver and Selenium Chrome Webdriver libraries.
17. Open the file IndexTest.cs, this contains two unit test that use Selenium. Find the property "indexURL" (currently line 65) and update the url to your sample app.
18. To run our test in the terminal type in "dotnet xunit". A Chrome window should be displayed and you should see the test being run, both test should run succesfully.
  You may get an error "The specified framework 'Microsoft.NETCore.App', version '2.0.5' was not found." 
  This requires you update the value "RuntimeFrameworkVersion" in LetsFindLunchTest.csproj to your correct runtime version found in "C:\Program Files\dotnet\shared\Microsoft.NETCore.App"
19. Currently if we enter no address and click the button it tries the service and we get an error, lets add some javascript to test for this and then add a unit test to test the new feature.
20. Return to your Glitch app and open up the file "public/scripts/index.js". Replace line 45 

        fetchNewLunch(location);
        
    with:
    
        if(location === "")
        {
            alert("please enter a location");
        }
        else
        {
            fetchNewLunch(location);
        }  
21. The preview page should refresh automatically, now if we click the "Lunch!" button, we should get an alert that says "please enter a location".
22. Lets return to our unit test project in VS Code and add a unit test.
23. Open IndexTest.cs and add the following code at line 12:

        [Fact]
        public void AlertForEmptyLocation()
        {
            Driver.Navigate().GoToUrl(indexURL);

            var txtLocation = GetElement(By.Id("txtLocation"));

            Assert.True(txtLocation.Text == string.Empty);

            var btnFindLunch = GetElement(By.Id("btnFindLunch"));

            btnFindLunch.Click();

            IAlert alert = Driver.SwitchTo().Alert();

            Assert.True(alert.Text == "please enter a location");
        }
24. Be sure to save your changes (Ctrl-S) and run the unit test again, you should now have 3 successfull test.
