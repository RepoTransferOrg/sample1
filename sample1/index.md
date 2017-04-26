# OPS build E2E Test cases and descriptions

## Automaiton Regression build test cases

**Reference repos**

|GitHub repository|Description|
|-----------------|-----------------|
|[DOCSRepo](https://github.com/OPS-E2E-PPE/E2E_DocsBranch)|The Docs theme test repo for PPE environment|
|[MSDNRepo](https://github.com/OPS-E2E-PPE/E2E_MSDNBranch)|The MSDN theme test repo for PPE environment|
|[TECHNETRepo](https://github.com/OPS-E2E-PPE/E2E_TechnetBranch)|The TechNet theme test repo for PPE environment|
|[VSCOMRepo](https://github.com/OPS-E2E-PPE/E2E_VSCOMBranch)|The VSCom theme test repo for PPE environment|

**Test cases behaviors,description and check points**

Following are the regression automation test cases. You can see the report [here](#report).

1. [Build/Publish] Create a new branch. Area should cover MSDN,VS,DOCS
    
    - **Description**: This should be BVT. Build triggered automatically, build report, output content should be converted in the testing. Users get notification email after publishing completes.
    - **Check Points**:
        * New created branch's content are all published (check the published content/resource/toc (simplify to c/r/t below) number. 
        * New published content page can be visited

2. [Build/Publish] User push some changes on existing branch

    - **Description**:  Incremental build should be covered in this testing. Users get notification email after publishing completes.
    - **Check Points**: 
        * New commit build successfully. 
        * Changes showed on the content page

3. [Build/Publish] User can trigger manual publishing via OPS portal

    - **Description**: With option of force publishing(without). Users get notification email after publishing completes.
    - **Check Points**:
        * Build results should be successful.
        * If it's incremental, then no content should be published.If it's force publish, the c/r/t number should be same with its first publish.

4. [Build/Publish] User can trigger manual publishing via OPS portal

    - **Description**: With option of force publishing(with). Users get notification email after publishing completes.
    - **Check Points**:
        * Build results should be successful.
        * If it's incremental, then no content should be published.If it's force publish, the c/r/t number should be same with its first publish.

5. [Build/Publish] User can delete a protected branch from VSO/GitHub

    - **Description**: Once user deletes a protected branch, the corresponding branch page can still be visited. (such as master and live branch).
    - **Check Points**:
        * Once user deletes the protected branch, the delete action result should fail with friendly error message.
        * Protected branch pages can still be visited although it's no longer existed in VSO/GitHub.
        * The protected branch should be shown in branch selector dropdown box( verify on page)

6. [Build/Publish] User create pull request to merge changes to master/live branch

    - **Description**: This should be BVT. Build triggered automatically, build report, output content, comments, notifications should be converted in the testing.
    - **Check Points**: 
        * PR state in GitHub when the job is initialized.
        * Set PR comment in GitHub when the job completes.
        * Set PR state in GitHub when the job completes.
        * Email notification is sent - Optional.

7. [Build/Publish] User updates an existing pull request

    - **Description**: When a PR is updated by new commits in source branch, a new PR validation build will be triggered. Should cover source branch is in same repo or is in forked repo.
    - **Check Points**: 
        * PR state in GitHub when the job is initialized.
        * Set PR comment in GitHub when the job completes.
        * Set PR state in GitHub when the job completes.
        * Email notification is sent - Optional.

8. [Build/Publish] User did changes in configuration：1.Op.config.json 2. Docfx.json

    -  **Description**: Configuration change will cause.
        * build behavior change.
        * Show/hide validation.
        * Show/Hide component on output page.Detail is in the docs.  
    - **Check Points**:
        * Too complex and need to sync offline.(will update later).

9. [Build/Publish] Build report

    - **Description**: Should check build files count, resource count, warning/error count, output url, etc.
    - **Check Points**:
        * Build/PR will both receive email.
        * PR will always see the build status on the PR page.
        * PR will see the comments once the PR comment is enable.

10. [Build/Publish] I can build PDF when someone pushes changes into the branch or manually triggered from portal

    - **Description**: You can control which branches to publish or generate PDFs from. By default, build is done in all the branches. This property setting is only read from the configuration file in the live branch.
    - **Check Points**: 
        * Download the packges and check if all the pdf has generated.

11. [Local build] Local build

    - **Description**: User runs .openpublishing.build.ps1 in local cloned repository and the script generates build outputs.
    - **Check Points**:
        * Pages has been generated under root/_sites folder
        * The build result is OK

12. [Provision]New Docset (new repo)

    - **Description**: Verify LICENSE,LICENSE-CODE and READM.md file for Docs
    - **Check Points**:
        * Build results should be successful in master branch;Build results should be no built in live branch (sometimes,          it will, but the result is warning. The live will trigger build because GitHub api call is asynchronous) 
        * The en-us repo will be created in the OPS portal https://opportal-sandbox.azurewebsites.net/#/repos/  
          The docset will be created in the ops portal.
        * Repo check (master and live) 
            1. Folder: Docset Folder
            2. File: ".gitignore",".openpublishing.build.ps1",".openpublishing.publish.config.json" exist in the top of the repo.
        * Docset check (master and live)
            1. File: "docfx.json","Index.md","TOC.md" exist in Docset Folde.
        * Check content about above #3 and #4 files.
        * New published content page can be visited in master.No published content in live.       

13. [Provision]De-provision en-us repo

    - **Description**: Remove web hook and disconnect this repo from OPS. The physical files in this repo will not be deleted,                      including the OPS config files, you can delete them later by yourself.
    - **Check Points**:
        * No this en-us repo in OPS.
        * No this docset in OPS 
        * No new commit build in this repo (master and live).The physical files in this repo will not be deleted, including the OPS config files.
        * Published topics are unavailable online in master.
        * Webhook of en-us repository will be removed on GitHub.

14. [Provision]De-provision en-us docset

    - **Description**: Delete this docset from all its repos, delete all published content. Source files will not be                                touched.Note:we will not delete published topics when we deprovision localized docsets
    - **Check Points**:
        * No this en-us repo in OPS (because we don’t allow empty repos in our system) 
        * No this docset in OPS.
        * No new commit build in this repo.
        * Published topics are unavailable online in master.

12. [Provision] User add locale in existing repo and do provision for this locale.

    - **Description**: New repo will be created and provisioned.
    - **Check Points**: 
        * Topic reference a topic not in loc repo. Should be fallback to default locale.
        * New repo will be created in the ops portal(master branch and live branch).
        * Build results should be successful in master branch.
        * For docs, the template repository config in .op.config will use corresponding locale instead of en-us.
        * En-us repository will be added in .op.config as fallback repository.
        * Locale in .op.config will be updated to provisioned locale.

12. [Provision] User de-provision the repo

    - **Description**:
        * The published topics are still available online until you de-provision en-us repo too, or delete the files manually      from localized repo before de-provisioning.
        * If your repo is on Open Localization (OL), please remove its locale from OL translation config before de-provisioning    in OPS.
    - **Check Points**:
        * No localized repo in OPS portal.
        * The content on this repo will not be touched,.openpublishing.publish.config.json and openpublishing.build.ps1 will be    not changed(no new commit in this repo) (master and live).
        * Published topics are still available online in master(check content page.
        * Webhook of localized repository will be removed on GitHub.

13. [Provision] User changes docset config

    - **Description**: If user changes base path, themes, should check published url/page.
    - **Check Points**:


14. |[Cross-repository] Dependency build

    - **Description**: If repoA has dependency on repoB, and the dependency relationship is set. Then if repoB is changed, repoA should also be built.
    - **Check Points**: 

15. [Cross-repository] Token/code snippets locale fallback behavior

    - **Description**: 
    - **Check Points**:
        * If token/code snippets doesn't exist in localized repository but only in fallback repository.
        * The build can still pass The content should be rendered OK except the token/code snippets is same with fallback          repository.

16. [Cross-repository] include source files from another repo

    - Similar with the above one

## Manual Regression Test Cases for Deployment

 > [!NOTE]
 > The regression test cases need to running after PPE and Production deploayment every sprint.

**Reference repo**:

|Organization Name|Repository Name|Docset Name|
|---------|---------|---------|
|OPS-E2E-Prod|[Azure-docs-cli-python](https://github.com/OPS-E2E-Prod/azure-docs-cli-python)|e2eprod-azure-cli-docs|
|OPS-E2E-Prod|[Azure-docs-pr](https://github.com/OPS-E2E-Prod/azure-docs-pr)|e2eprod-azure-documents|
|OPS-E2E-Prod|[Azure-docs-pr.cs-cz](https://github.com/OPS-E2E-Prod/azure-docs-pr.cs-cz)|e2eprod-azure-documents|
|OPS-E2E-Prod|[Azure-docs-rest-apis](https://github.com/OPS-E2E-Prod/azure-docs-rest-apis)|e2eprod-AzureRestApi|
|OPS-E2E-Prod|[Azure-docs-sdk-dotnet](https://github.com/OPS-E2E-Prod/azure-docs-sdk-dotnet)|e2eprod-azuredotnet|
|OPS-E2E-Prod|[Docs](https://github.com/OPS-E2E-Prod/docs)|e2eprod-core-docs|
|OPS-E2E-PPE|[Azure-docs-cli-python](https://github.com/OPS-E2E-PPE/azure-docs-cli-python)|e2eppe-azure-cli-docs|
|OPS-E2E-PPE|[Azure-docs-pr](https://github.com/OPS-E2E-PPE/azure-docs-pr)|e2eppe-azure-documents|
|OPS-E2E-PPE|[Azure-docs-pr.cs-cz](https://github.com/OPS-E2E-PPE/azure-docs-pr.cs-cz)|e2eppe-azure-documents|
|OPS-E2E-PPE|[Azure-docs-rest-apis](https://github.com/OPS-E2E-PPE/azure-docs-rest-apis)|e2eppe-AzureRestApi|
|OPS-E2E-PPE|[Azure-docs-sdk-dotnet](https://github.com/OPS-E2E-PPE/azure-docs-sdk-dotnet)|e2eppe-azuredotnet|
|OPS-E2E-PPE|[Docs](https://github.com/OPS-E2E-PPE/docs)|e2eppe-core-docs|

**Test cases behaviors,description and check points**

1. Force Publish - Live branch. Check warning count no change.
2. Incremental Publish - Live branch. Warning count no change.
    * Make sure the warning count is same
3. Force publish master first and then create new branch(PR) and send PR to master with expected warning. Change existing file &    add new file.
    * Verify warning count no change. Check comments.
    * No merge needed.



## <a id="report"> </a>Automation cases running report
OPS E2E automation test cases report address：https://vsctestportal.azurewebsites.net/Ops

Now we have two jobs to running the cases:

* E2E test run on production: Triggered every 30 minutes
* E2E test run on PPE: Triggered every 2 hour
