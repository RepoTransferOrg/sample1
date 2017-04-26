# How To Running OPS E2E Test Cases

 Please follow the steps to setup the testing environment.

 ## Prerequisites
 OPS E2E Testing using the [Protractor](http://www.protractortest.org/#/tutorial) as the test framework. Protracotr is a Node.js program. To run, you need to install [Node.js](https://nodejs.org/en/) and [Java Development kit(JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html) first.

 ## Download the Project
 [Project Address](https://mseng.visualstudio.com/VSChina/VSChina%20Team/_git/OpenPublishing.E2ETesting). You can clone the repo with *"git clone* {clone url}" command into your directory.

 ## Install opse2e Tool
 [Opse2e](https://mseng.visualstudio.com/VSChina/VSChina%20Team/_git/Templating.E2ETools) is a private nodejs package, please go to [VSO WebComponents management page](https://mseng.visualstudio.com/DefaultCollection/VSChina/Templating/_packaging?feed=WebComponents&package=8316a24e-039a-496d-a3d3-125e7cdf1a8d&version=0bdaa70c-ecc7-4e3b-b68f-5a188988ce26&_a=package) to get your npmrc credential. See the steps.
 1. Click ‘Connect to feed’ button and then 'Generate npm credentials', 
 2. Finally copy the credential text to a **.npmrc** file and saved to user home directory. (such as C:\Users\jinbwan\.npmrc)

 Opse2e is a cli-based tool, you could run the following command to exec e2e cases.  
 1. *npm run opse2e init*    
 It does something like ‘webdriver-manager update’, but download chrome driver to current node_modules directory. This command just need run once.

 2. *npm run opse2e protractor*  
 
 It’s kind of similar as previous ‘gulp e2e’. But the good thing is you don’t need start a standalone selenium server any longer.  

 It has a big improvement that it’ll host a temporary selenium server on a free port automatically every time you run this command.  

 More information about the command could be got via '--help' options.  

 ## Running the Test Cases
 You can running the test cases with optional parms. For example:  
 *npm run opse2e -- protractor --suite pullRequest --baseUrl https://ops.microsoft.com/ --branch develop*  
 Please see the more information about the command:

 |Command|Description|
 |----|----|
 |*--configFile \<configFile>*|[Protractor inherit] The path of protractor config js. Default to 'test/protractor.config.js'|
 |*--baseUrl \<baseUrl>*|[Protractor inherit] The base url of the target test site|
 |*--seleniumAddress \<seleniumAddress>*|[Protractor inherit] A running selenium address to use|
 |*--exclude \<exclude>*|[Protractor inherit] Comma-separated list of files to exclude|
 |*--suite \<suite>* |[Protractor inherit] Comma-separated list of suites to test|
 |*--maxInstances \<maxInstances>*|[OPSE2E] Restricted to launch max browser instance number in parallel|
 |*--branchName \<branchName>*|[OPSE2E] Add ?branch={branchName} to test url|
 |*--reporterBaseDir \<reporterBaseDir>*|[OPSE2E] Base directory to save test result. Default to 'result/e2e/screenshots'|
 |*--testData \<testData>*|[OPSE2E] Select the test data in different environment|
 |*--preserveBaseDir*|[OPSE2E] Preserve test result base directory or not. Default to cleanup it before e2e started|
 |*--noEscalation*|[OPSE2E] Escalate protractor exit code to parent process or not. Default to escalate it|
 |*--throwConsoleError*|[OPSE2E] Throw an error for browser error logs or not. By defualt, just show warning in the reporter|  
