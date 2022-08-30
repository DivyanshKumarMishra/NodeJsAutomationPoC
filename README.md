# NodeJsAutomationPoC

## Step 1: Environment Setup
  1. Clone the [repository](https://github.com/browserstack/node-appium-app-browserstack)
  2. Go to the repository run the commands `npm install` and `npm i wd`

## Step 2: Upload the app
  We can use one of the following options to upload an Android app (.apk or .aab file) or iOS app (.ipa file) to BrowserStack servers. The generated `app_url` is a unique ID used to identify the uploaded app build. Take note of this app_url as it will be used in steps ahead.
   ### 1. Sample app   
   The app upload API request returns an "app_url" value in its response. 
   It uniquely identifies your uploaded app on BrowserStack.
      
   ```{"app_url":"bs://<app-id>"}```
        
   In your test script, use this "app_url" value to specify the application under test using the "app" capability. 
   During test execution, your app will automatically be installed and launched on the device being tested.      
   ```
   {
      "app", "bs://<app-id>"	
   }   
   ```
   ###  2. Upload via file manager
   ###  3. Upload via REST API  
      curl -u "divyanshmishra_FlHT9A:UkGPGHMe7y2AmzAS1vV2" 
      -X POST "https://api-cloud.browserstack.com/app-automate/upload" 
      -F "file=@/path/to/app/file/Application-debug.apk"
 Here we're gonna discuss just the sample app method.
 
 ## Step 3: Configure test script
   Edit the `BrowserStackSample.js` file in your cloned repository to update key configurations required to run your first sample build. This includes setting up important desired capabilities, a series of key-value pairs, that allow you to configure the behaviour of your Appium tests on BrowserStack.
   ```
    let wd = require('wd');
    let assert = require('assert');
    let asserters = wd.asserters;
    let Q = wd.Q;
    desiredCaps = {
    
      // Set your BrowserStack access credentials
      
      'browserstack.user' : 'divyanshmishra_FlHT9A',
      'browserstack.key' : 'UkGPGHMe7y2AmzAS1vV2',
      
      // Set app_url of the application under test
        
      'app' : 'bs://c700ce60cf13ae8ed97705a55b8e022f13c5827c',
      
      // Specify device and os_version for testing
      
      'device' : 'Google Pixel 3',
      'os_version' : '9.0',
      
      // Set other BrowserStack capabilities
      
      'project' : 'First NodeJS project',
      'build' : 'browserstack-build-1',
      'name': 'first_test'
    };
    
    // Initialize the remote Webdriver using BrowserStack remote URL
    // and desired capabilities defined above
    
    driver = wd.promiseRemote("http://hub-cloud.browserstack.com/wd/hub");
    
    // Test case for the BrowserStack sample iOS app. 
    // If you have uploaded your app, update the test case here.
    
    driver.init(desiredCaps)
    
      //Write your custom code here
      
      .fin(function() { 
      
        // Invoke driver.quit() after the test is done to indicate that the test is completed.
        
        return driver.quit(); 
      })
      .done();
  ```
## Step 4: Execute your test script
   In the terminal run the command
   ``` node ./android/BrowserStackSample.js```
   
## Step 5: Visit the Dashboard for test results



          
          
             
