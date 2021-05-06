![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Modern cloud apps
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
November 2020
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2020 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->
- [Modern cloud apps hands-on lab step-by-step](#modern-cloud-apps-hands-on-lab-step-by-step)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Requirements](#requirements)
  - [Help references](#help-references)
  - [Exercise 1: Proof of concept deployment](#exercise-1-proof-of-concept-deployment)
    - [Task 1: Deploy the e-commerce website, SQL Database, and storage](#task-1-deploy-the-e-commerce-website-sql-database-and-storage)
    - [Task 2: Setup SQL Database Geo-Replication](#task-2-setup-sql-database-geo-replication)
    - [Task 3: Deploying the Call Center admin website](#task-3-deploying-the-call-center-admin-website)
    - [Task 4: Deploying the payment gateway](#task-4-deploying-the-payment-gateway)
    - [Task 5: Deploying the Offers Web API](#task-5-deploying-the-offers-web-api)
    - [Task 6: Add API endpoint configuration settings](#task-6-add-api-endpoint-configuration-settings)
  - [Exercise 2: Identity and Security](#exercise-2-identity-and-security)
    - [Task 1: Enable Azure AD Premium Trial](#task-1-enable-azure-ad-premium-trial)
    - [Task 2: Create a new Contoso user](#task-2-create-a-new-contoso-user)
    - [Task 3: Configure access control for the call center administration Web Application](#task-3-configure-access-control-for-the-call-center-administration-web-application)
    - [Task 4: Apply custom branding for the Azure Active Directory logon page](#task-4-apply-custom-branding-for-the-azure-active-directory-logon-page)
    - [Task 5: Verify the branding has been successfully applied to the Azure Active Directory logon page](#task-5-verify-the-branding-has-been-successfully-applied-to-the-azure-active-directory-logon-page)
  - [Exercise 3: Enable Azure B2C for customer site](#exercise-3-enable-azure-b2c-for-customer-site)
    - [Task 1: Create a new directory](#task-1-create-a-new-directory)
    - [Task 2: Add a new application](#task-2-add-a-new-application)
    - [Task 3: Create Policies, Sign up and sign in](#task-3-create-policies-sign-up-and-sign-in)
    - [Task 4: Create a profile editing policy](#task-4-create-a-profile-editing-policy)
    - [Task 5: Create a password reset policy](#task-5-create-a-password-reset-policy)
    - [Task 6: Modify the Contoso.App.SportsLeague.Web](#task-6-modify-the-contosoappsportsleagueweb)
    - [Task 7: Send authentication requests to Azure AD](#task-7-send-authentication-requests-to-azure-ad)
    - [Task 8: Display user information](#task-8-display-user-information)
    - [Task 9: Run the sample app](#task-9-run-the-sample-app)
  - [Exercise 4: Enabling Telemetry with Application Insights](#exercise-4-enabling-telemetry-with-application-insights)
    - [Task 1: Configure the application for telemetry](#task-1-configure-the-application-for-telemetry)
    - [Task 2: View the Application Insights logs](#task-2-view-the-application-insights-logs)
  - [Exercise 5: Automating backend processes with Azure Functions and Logic Apps](#exercise-5-automating-backend-processes-with-azure-functions-and-logic-apps)
    - [Task 1: Create an Azure Function to Generate PDF Receipts](#task-1-create-an-azure-function-to-generate-pdf-receipts)
    - [Task 2: Configure and deploy the Function App](#task-2-configure-and-deploy-the-function-app)
    - [Task 3: Create an Azure Logic App to Process Orders](#task-3-create-an-azure-logic-app-to-process-orders)
    - [Task 4: Use Twilio to send SMS Order Notifications](#task-4-use-twilio-to-send-sms-order-notifications)
  - [Exercise 6: Automate deployments using GitHub actions](#exercise-6-automate-deployments-using-github-actions)
    - [Task 1: Create a GitHub repository](#task-1-create-a-github-repository)
    - [Task 2: Commit the existing lab files to source control](#task-2-commit-the-existing-lab-files-to-source-control)
    - [Task 3: Create a service principal in Active Directory](#task-3-create-a-service-principal-in-active-directory)
    - [Task 4: Create repository secrets](#task-4-create-repository-secrets)
    - [Task 5: Define the production deployment workflow](#task-5-define-the-production-deployment-workflow)
    - [Task 6: Trigger the Production Deployment Workflow](#task-6-trigger-the-production-deployment-workflow)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Delete resources](#task-1-delete-resources)

<!-- /TOC -->

# Modern cloud apps hands-on lab step-by-step

## Abstract and learning objectives

In this hands-on lab, you will be challenged to implement an end-to-end scenario using a supplied sample that is based on Azure App Services, Microsoft Azure Functions, Azure SQL Database, Azure Logic Apps, and related services. The scenario will include implementing compute, storage, workflows, and monitoring, using various components of Microsoft Azure.

Please note that as opposed to the whiteboard design session, the lab is not focused on maintaining PCI compliance and using more advanced security features such as App Service Environment, Network Security Groups, and Application Gateway. The hands-on lab can be implemented on your own, but it is highly recommended to pair up with other members working on the lab to model a real-world experience and to allow each member to share their expertise for the overall solution.

By the end of this hands-on lab, you will have learned how to use several key services within Azure to improve overall functionality of the original solution, and to increase the security and scalability of the new and improved design.

## Overview

The Cloud Workshop: Modern Cloud Apps lab is a hands-on exercise that will challenge you to implement an end-to-end scenario using a supplied sample that is based on Microsoft Azure App Services and related services. The scenario will include implementing compute, storage, security, and scale using various components of Microsoft Azure. The lab can be implemented on your own, but it is highly recommended to pair up with additional team members to more closely model a real-world experience, and to allow members to share their expertise for the overall solution.

## Solution architecture

![A diagram that depicts the various Azure PaaS services for the solution. Azure AD Org is used for authentication to the call center app. Azure AD B2C for authentication is used for authentication to the client app. SQL Database for the backend customer data. Azure App Services for the web and API apps. Order processing includes using Functions, Logic Apps, Queues and Storage. Azure App Insights is used for telemetry capture.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image2.png "Solution Architecture Diagram")

## Requirements

1. Microsoft Azure subscription
2. Local machine or a virtual machine configured with Visual Studio 2019 Community Edition
3. Twilio account and/or personal cell phone to setup a trial Twilio account
4. A GitHub account and local installation of a Git client

## Help references

| Description | Links |
|:---------|:-------------|
| SQL firewall | <https://azure.microsoft.com/en-us/documentation/articles/sql-database-configure-firewall-settings/> |
| Deploying a Web App | <https://azure.microsoft.com/en-us/documentation/articles/web-sites-deploy/> |
| Deploying an API app | <https://azure.microsoft.com/en-us/documentation/articles/app-service-dotnet-deploy-api-app/> |
| Accessing an API app from a JavaScript client | <https://azure.microsoft.com/en-us/documentation/articles/app-service-api-javascript-client/> |
| SQL Database Geo-Replication overview | <https://azure.microsoft.com/en-us/documentation/articles/sql-database-geo-replication-overview/> |
| What is Azure AD? | <https://azure.microsoft.com/en-us/documentation/articles/active-directory-whatis/> |
| Azure Web Apps authentication | <http://azure.microsoft.com/blog/2014/11/13/azure-websites-authentication-authorization/> |
| View your access and usage reports | <https://msdn.microsoft.com/en-us/library/azure/dn283934.aspx> |
| Custom branding an Azure AD Tenant | <https://msdn.microsoft.com/en-us/library/azure/Dn532270.aspx> |
| Service Principal Authentication | <https://docs.microsoft.com/en-us/azure/app-service-api/app-service-api-dotnet-service-principal-auth> |
| Consumer Site B2C | <https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-dotnet> |
| Getting Started with Active Directory B2C | <https://azure.microsoft.com/en-us/trial/get-started-active-directory-b2c/> |
| How to Delete an Azure Active Directory | <https://blog.nicholasrogoff.com/2017/01/20/how-to-delete-an-azure-active-directory-add-tenant/> |
| Run performance tests on your app | <http://blogs.msdn.com/b/visualstudioalm/archive/2015/09/15/announcing-public-preview-for-performance-load-testing-of-azure-webapp.aspx> |
| Application Insights Custom Events | <https://azure.microsoft.com/en-us/documentation/articles/app-insights-api-custom-events-metrics/> |
| Enabling Application Insights | <https://azure.microsoft.com/en-us/documentation/articles/app-insights-start-monitoring-app-health-usage/> |
| Detect failures | <https://azure.microsoft.com/en-us/documentation/articles/app-insights-asp-net-exceptions/> |
| Monitor performance problems | <https://azure.microsoft.com/en-us/documentation/articles/app-insights-web-monitor-performance/> |
| Creating a Logic App | <https://azure.microsoft.com/en-us/documentation/articles/app-service-logic-create-a-logic-app/> |
| Logic app connectors | <https://azure.microsoft.com/en-us/documentation/articles/app-service-logic-connectors-list/> |
| Logic Apps Docs | <https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-what-are-logic-apps> |
| Azure Functions -- create first function | <https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-first-azure-function> |
| Azure Functions docs | <https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-azure-functions> |
| Deploy to Azure with GitHub Actions | <https://docs.microsoft.com/en-us/azure/developer/github/github-actions> |

## Exercise 1: Proof of concept deployment

Duration: 60 minutes

Contoso has asked you for a proof of concept in Microsoft Azure by deploying the web, database, and API applications for the solution as well as validating that the core functionality of the solution works. Ensure all resources use the same resource group previously created for the App Service Environment.

### Task 1: Deploy the e-commerce website, SQL Database, and storage

In this exercise, you will provision a website via the Azure **Web App + SQL** template using the Microsoft Azure Portal. You will then edit the necessary configuration files in the starter project and deploy the e-commerce website.

<!-- omit in toc -->
#### Subtask 1: Configure SQL Database Firewall and Retrieve Connection String

1. Navigate to the Azure Management portal, [http://portal.azure.com](http://portal.azure.com/), using a new tab or instance and login with your lab-provided Azure credentials.

2. Navigate to the **contososports-01** resource group.

3. Select the **ContosoSportsDB** SQL Database.

    ![The contososports Resource Group blade with the "ContosoSportsDB" highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image22.png "Azure Portal")

4. On the **SQL Database** blade, select the **Show database connection strings** link.

    ![On the SQL Database blade, in the left pane, Overview is selected. In the right pane, under Essentials, the Connection strings (Show database connection strings) link is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image23.png "SQL Database blade")

5. On the **Database connection strings** blade, select and copy the **ADO.NET** connection string. Then, save it in **Notepad** for use later, being sure to replace the password placeholder with **demo@pass123**

    ![In the Database connection strings blade, the ADO.NET connection string is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image24.png "Database connection strings blade")

6. Go back to the **contososports-01** resource group blade, and select the **contososports[Suffix]** SQL Server.

    ![The contososports resource group with the contososports sql server highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/2019-11-15-17-47-46.png "Azure Portal")

7. On the **Overview** screen of the **SQL Server** blade, select the **Show firewall settings**.

    ![On the SQL Server Overview screen with the Show firewall settings link highlighted.](media/2019-03-31-14-37-31.png "SQL Server Overview")

8. On the **Firewall Settings** blade, specify a new rule named **My IP**, copy your **Client IP address**, and paste it into the **Start IP** and **End IP**. This will set the allowed IP Address range to just your IP address so you can connect to the database from this machine.

    ![Screenshot of the Rule name, Start IP. and End IP fields on the Firewall Settings blade.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image27.png "Firewall Settings blade")

9. Select **Save**.

    ![Screenshot of the Firewall settings Save button.](media/2019-04-10-16-00-29.png "Firewall settings Save button")

10. Update progress can be found by selecting the **Notifications** link located at the top of the page.

    ![Screenshot of the Success dialog box, which says that the server firewall rules have been successfully updated.](media/2019-04-19-13-39-41.png "Success dialog box")

11. Close all configuration blades.

<!-- omit in toc -->
#### Subtask 2: Retrieve Storage Account Access Keys

1. Go back to the **contososports-01** blade resource group, and select the **contoso[Suffix]** Storage account.

2. On the **Storage account** blade, scroll down, and, under the **SETTINGS** menu area, select the **Access keys** option.

    ![In the Storage account blade, under Settings, Access keys is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image35.png "Storage account blade")

3. On the **Access keys** blade, click on **Show keys** then select the copy button by the **Connection String** field in the **key1** section. Paste the value into **Notepad** for later usage. 

    ![In the Access keys blade default keys section, the copy button for the key1 connection string is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image36.png "Access keys blade, default keys section")

<!-- omit in toc -->
#### Subtask 3: Retrieve Service Bus Queue Connection String

1. Go back to the **contososports-01** blade resource group, and select the **contososervicebus[Suffix]** Service Bus Namespace.

    ![Service Bus Namespace resource is highlighted](media/2020-03-18-10-38-09.png "Service Bus Namespace")

2. Select the **Queues** link under Entities.

    ![Queues link under Entities](media/2020-03-18-10-38-57.png "Queues link")

3. On the **Queues** pane, select the **receiptgenerator** Service Bus Queue.

    ![receiptgenerator queue is highlighted](media/2020-03-18-10-40-40.png "receiptgenerator queue is highlighted")

4. On the **receiptgenerator** Service Bus Queue blade, select the **Shared access policies** link under Settings.

    ![Shared access policies link is shown](media/2020-03-18-10-42-03.png "Shared access policies link is shown")

5. Select the **Publisher** shared access policy.

    ![Publisher policy is highlighted](media/2020-03-18-10-43-12.png "Publisher policy is highlighted")

    >**Note**: The _Publisher_ and _Listener_ shared access policies for the Azure Service Bus Queue were deployed as part of the ARM Template that was used to setup the lab environment. As you can see, the **Publisher** policy that we're copying the connection string for, only has permissions to _Send_ messages to the queue.
    >
    > By default, no policies are created. Additionally, it is best practice to use least privilege security to create separate shared access policies for publishers sending messages and listeners receiving messages from the queue. 

6. On the **SAS Policy** pane, copy the **Primary Connection String**. Paste the value into **Notepad** for later usage. 

    ![Primary Connection String is highlighted](media/2020-03-18-10-54-39.png "Primary Connection String is highlighted")

<!-- omit in toc -->
#### Subtask 4: Create secrets in Azure Key Vault

You've retrieved multiple access keys and connection strings in this task. To properly secure them, and to keep these values out of application code, we need a secure place to store them. This place is the Azure Key Vault.

1. Go back to the **contososports-01** resource group blade, and select the **contosokv[Suffix]** Key Vault resource.

    ![The resource listing is displayed with the key vault item selected.](media/rg_selectkeyvault.png "Resource group listing")

2. Beneath **Settings**, select **Access Policies**.

3. In order to add, edit, or view secrets, you must be granted access through a new Access policy. Select the **+ Add Access Policy** link.
    
    ![A portion of the Access Policies screen is shown with the + Add Access Policy link selected.](media/add_access_policy_link.png "Key Vault Access Policies")

4. Expand the **Secret permissions** drop down, and check the **Select all** checkbox.

5. For **Select principal**, select your Azure user account, and select **Add**.

    ![The Add access policy form is displayed with the Secret Permissions and Select principal fields highlighted.](media/kv_add_access_policy_form.png "The Add Access Policy Form")

6. Press **Save** on the **Access policies** screen to save the changes.

7. Beneath **Settings**, select **Secrets** then **Generate/Import**.

8. Create the following secret values by filling out **Name** and **Value** (retaining the defaults for all other fields):

    | Name | Value |
    |------|-------|
    | AzureQueueConnectionString | {the primary connection string you recorded for the queue} |
    | ContosoSportsLeague | {the database connection string} |
    | contososportsstorage | {the primary connection string you recorded for the storage account} |

    ![The Create a secret form is displayed with the Name and Value fields highlighted.](media/kv_createasecret.png "The Create a secret form")

<!-- omit in toc -->
#### Subtask 5: Centralize secrets for multiple projects using an App Configuration store

The Contoso Sports solution contains multiple projects, each of which access the same Azure resources. In this subtask, we will be centralizing the configuration of the solution applications via the deployed Azure **App Configuration** resource.

1. Go back to the **contososports-01** resource group blade, and select the **contosoconfig[Suffix]** App Configuration resource.

    ![The resource listing is displayed with the App Configuration resource highlighted.](media/appconfig_resourcelist_selection.png "The resource listing")

2. Select **Configuration explorer** found beneath the **Operations** section of the left menu.

3. On the **Configuration explorer** screen, expand **+ Create** and select **Key Vault reference**.
   
   ![The + Create button is expanded with the Key Vault reference item highlighted.](media/ac_createkeyvaultreference_menu.png "Create Key Vault Reference")

4. On the **Create** form, be sure to select the appropriate **Subscription**, **Resource group**, and the **contosokv** Key Vault. Create the following Key Vault references:

    | Key | Secret | Secret version |
    |-----|--------|----------------|
    | ConnectionStrings:ReceiptQueue | Select **AzureQueueConnectionString** | Select **Latest version** |
    | ConnectionStrings:ReceiptStorage | Select **contososportsstorage** | Select **Latest version** |
    | ConnectionStrings:SportsDB | Select **ContosoSportsLeague** | Select **Latest version** |

    ![The Create new Key vault reference form is displayed populated with the ConnectionStrings:ReceiptQueue values.](media/ac_createkeyvaultref_form.png "The create new key vault reference form")

5. From the left menu, select **Access keys** located in the **Settings** section.

6. Select the **Read-only keys** tab. 

7. Copy the **Primary key Connection string** value, and paste it into notepad. This value is needed to connect the deployed applications to the App Configuration store. 
    
    ![A portion of the Access keys screen is displayed. The Read-only keys tab is highlighted and the copy button next to the Primary key Connection string textbox is selected.](media/ac_connectionstringcopy.png "The Access keys screen")

<!-- omit in toc -->
#### Subtask 6: Update the configuration in the starter project

1. Go back to the **contososports-01** resource group blade.

2. Select the **contosoapp[Suffix]** web app (**App Service** type).

    ![Resources listed for ContosoSports. Web app selected.](media/2019-04-19-13-46-40.png "Resources listed for ContosoSports")

3. Copy the web app URL to Notepad.

    - Select the **Overview** link.
    - Copy the URL to Notepad for later use. Use the **Copy to clipboard** link.

    ![In the Web App Overview settings, the URL has a box around the link.](media/2019-03-22-16-33-05.png "Contoso Web App Overview")

4. On the **App Service** blade, scroll down in the left pane. Under the **Settings** menu, select **Configuration**.

    ![In the App Service blade, under Settings, select Configuration link.](media/2019-04-19-16-38-54.png "Configuration link")

5. Locate **Connection Strings** section below **Application Settings**.

    ![The App Service Configuration screen is displayed with the Connection Strings section title and + New connection string button highlighted.](media/image41.png "Connection Strings section")

6. Add a new **Connection String** with the following values, and select **OK**:

   - Name: **AppConfig**

   - Value: **Enter the Connection String for the App Configuration Store**.

   - Type: Select **Custom**.

    ![The Add/Edit connection string form is displayed and is populated with the preceding values.](media/image43.png "The Add/Edit connection string form")

7. Select **Save** to commit the changes.

8. The e-commerce website application resource needs access to the Key Vault. The App Configuration will use pass-through authentication to the Key Vault. To authenticate the application, it will utilize a system managed identity. From the left menu, select **Identity**.

9. With the **System assigned** tab selected, toggle the **Status** field to **On**, then select **Save**. 

    ![On the Identity screen, the System assigned tab is selected and the Status field is in the On position.](media/appconfig_systemidentity.png "The Identity Screen")

10. Open the **contosokv[Suffix]** Key Vault resource, and from the left menu, select **Access policies**. 

11. Select the **+ Add Access Policy** link.

12. In the **Add access policy** form, expand **Secret permissions** and check the box next to **Get** and **List**.  

13. In the **Select principal** blade, search for **contosoapp** and choose the managed identity that was just created.

14. Select **Add**.
    
    ![The Add access policy form is displayed with the Get secret permission selected, and the contosoconfig principal selected.](media/kv_addaccesspolicy_forconfig.png "The Add Access Policy Form")

15. Select **Save** on the Access policies screen to commit the changes. 

<!-- omit in toc -->
#### Subtask 7: Configure and deploy the e-commerce Web App from Visual Studio

1. Navigate to the **Contoso.Apps.SportsLeague.Web** project located in the **Web** folder using the **Solution Explorer** of Visual Studio.

2. Right-click the **Contoso.Apps.SportsLeague.Web** project, and select **Manage NuGet Packages**.

3. Select the **Browse** tab, and search for **Microsoft.Azure.AppConfiguration.AspNetCore**.

4. Select **Microsoft.Azure.AppConfiguration.AspNetCore** from the search results, and in the next pane, select **Install** to install the latest stable version.

    ![The Nuget Package Manager windows is displayed with the Browse tab selected, Microsoft.Azure.AppConfiguration.AspNetCore entered into the search box and selected from the search results. In the next pane, the Install button is selected.](media/nuget_installappconfigpackage_web.png "Nuget Package Manager")

5. Repeat step 4-6, this time installing the latest **Azure.Identity**.

6. Now we are ready to configure this application to use the App Configuration in Azure. Under the **Contoso.Apps.SportsLeague.Web** project, open the **Program.cs** file.

7. Uncomment the following **using** statements at the top of the file:
    
    ```C#
    using Microsoft.Extensions.Configuration;
    using Azure.Identity;
    ```

8. In the **CreateHostBuilder** method, uncomment the following code - this tells the application to utilize the AppConfig connection string that you've already setup on the **contosoapp** application service to point to the centralized App Configuration resource.
    
    ```C#
    webBuilder.ConfigureAppConfiguration((hostingContext, config) =>
    {
        var settings = config.Build();

        config.AddAzureAppConfiguration(options =>
        {
            options.Connect(settings["ConnectionStrings:AppConfig"])
                    .ConfigureKeyVault(kv =>
                    {
                        kv.SetCredential(new DefaultAzureCredential());
                    });
        });
    })
    .UseStartup<Startup>();
    ```
9. Press **Ctrl + S** to save the file then right-click the **Contoso.Apps.SportsLeague.Web** project, and select **Publish**.

    ![In Solution Explorer, under Solution \'Contoso.Apps.SportsLeague\' (7 projects), Web is expanded, and under Web, Contoso.Apps.SportsLeague.Web is selected.](media/2019-04-19-14-03-04.png "Solution Explorer")

10. On the Publish dialog, select **Azure** as the **Target**, then select **Next**.
    
11. For **Specific target**, select **Azure App Service (Windows)**, then select **Next**.

12. For **App Service**, expand the lab resource group, and select the **contosoapp[DeploymentID]** from the list, then choose **Finish**.
    
    ![The App Service dialog is shown with the resource group expanded and the contosoapp application service selected in the list. The OK button is highlighted.](media/deploywebapp_serviceselection.png "App Service Selection")

13. Select **Publish** to publish the Web application.

    ![Publish profile is displayed with the Publish button highlighted.](media/2020-06-15-16-53-15.png "Publish profile")

14. In the Visual Studio **Output** view, you will see a status that indicates the Web App was published successfully.

    ![Screenshot of the Visual Studio Output view, with the Publish Succeeded message circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image50.png "Visual Studio Output view")

    >**Note**: Your URL will differ from the one shown in the Output screenshot because it must be globally unique.

15. A new browser should automatically open the new web applications. Validate the website by choosing the **Store** link on the menu. You should see product items. If products are returned, then the connection to the database is successful.

    ![Screenshot of the Store link.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image51.png "Store link")

    >**Troubleshooting**: If the web site fails to start up or show products, go back and double check all your connection string entries and passwords web application settings. If you get a message indicating the Service is unavailable. Give it a moment, and refresh your browser.

### Task 2: Setup SQL Database Geo-Replication

In this exercise, the attendee will provision a secondary SQL Database and configure Geo-Replication using the Microsoft Azure Portal.

<!-- omit in toc -->
#### Subtask 1: Add secondary database

1. In the Azure Portal, navigate back to the lab resource group.

2. From the list of resources, select the **ContosoSportsDB** SQL database resource.

    ![The resource listing is displayed with the ContosoSportsDB SQL database resource highlighted.](media/resourcelist_contososportsdb.png "Resource listing")

3. Under the **Data Management** menu area, select **Geo-Replication**.

    ![In the Settings section, Geo-Replication is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up1.png "Settings section")

4. Select the Azure Region to place the Secondary within.

    ![The Geo-Replication pane with list of locations. Primary location is set to West US.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image54.png "Geo-Replication blade")

    The Secondary Azure Region should be the Region Pair for the region the SQL Database is hosted in. Consult <https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions> to see which region pair the location you are using for this lab is in.


5. Select **Create new **.

    ![the Target server Configure required settings option is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up2.png "Target server option")
   
6. On the **New server** blade, specify the following configuration:

   - Server name: **contososql[Suffix]** *(ensure the green checkmark appears)*.

   - Server admin login: **demouser**

   - Password and Confirm Password: **demo@pass123**

   - Location: *Select the Secondary region*

    ![The fields in the New Server blade display with the previously defined settings.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image56.png "New Server blade")

7.  Once the values are accepted in the **New server** blade, select **OK**.


8. On the **Create secondary** blade, select **Review + Create** then click on **Create**.

    > **Note**: The Geo-Replication will take a few minutes to complete.

9. After the Geo-Replication has finished provisioning, return to the resource group for the lab.

10. Select the name of the secondary SQL Server resource that you just created.

    ![In the list of resources, the secondary SQL server resource is selected.](media/secondarydatabaseinresourcelist.png "Resource listing")

11. On the **SQL Server** blade, within the **Overview** pane, select **Show firewall settings** link.

    ![On the SQL Server blade, at the top, the Set server firewall tile is boxed in red.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image62.png "SQL Server blade, Overview section")

12. On the **Firewall Settings** blade, specify a new rule named **My IP**, copy your **Client IP address**, and paste it into the **Start IP** and **End IP**. This will set the allowed IP Address range to just your IP address so you can connect to the database from this machine.

    ![On the Firewall Settings blade, in the New rule section, a new rule has been created with the previously defined settings.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image27.png "New rule section ")

13. Select **Save**.

    ![Screenshot of the Firewall settings Save button.](media/2019-04-10-16-00-29.png "Firewall settings Save button")

14. Update progress can be found by choosing the **Notifications** link located at the top of the page.

    ![Screenshot of the Success dialog box, which says that the server firewall rules have been successfully updated.](media/2019-04-19-13-39-41.png "Success dialog box")

15. Close all configuration blades.

<!-- omit in toc -->
#### Subtask 2: Setup SQL Failover Group

With SQL Database Geo-Replication configured, the Azure SQL Failover Groups feature can be used to enable "auto failover" scenarios for the SQL Database. This enables a single connection string endpoint to be used by the application, and SQL Database will automatically handle failing over from Primary to Secondary database in the event of a SQL Database outage / down time.

1. In the Azure Portal, navigate back to the lab resource group.

2. From the list of resources, select the Primary SQL server resource.
    
    ![The list of lab resources is shown with the primary SQL server resource selected.](media/primary_sqlserverresource_inlist.png "Resource listing")

3. On the **SQL server** blade, select **Failover groups** under **Data Management**.

    ![Failover groups setting option.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up3.png "Failover groups setting option")

4. On the **Failover groups** pane, select the **Add group** button.

    ![Add group button.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/failovergroupsaddgroupbutton.png "Add group buton")

5. On the **Failover group** pane, enter a unique **contososportsfg[Suffix]**.

    ![Failover group name field.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/sqlfailovergroupname.png "Failover group name field")

6. Select **Secondary server**, then choose the **Secondary SQL Database** that was previously created.

    ![Secondary SQL Database is highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/sqlfailoversecondaryserver.png "Secondary SQL Database is highlighted")

7. Select **Database within the group**, then choose the **ContosoSportsDB** database, then **Select**.

    ![Steps to choose the ContosoSportsDB are highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/sqlfailoversecondarydatabase.png "Steps to choose the ContosoSportsDB are highlighted")

8. Select **Create** to create the SQL Failover Group.

9.  Once the Failover Group has been created, select it in the list.

    ![Failover Group is highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/sqlfailovergrouplist.png "Failover Group is highlighted")

10. Notice, on the **Failover group** pane, the map and display showing the _Primary_ and _Secondary_ SQL Database servers within the failover group. The _Primary_ database shows as **Automatic** failover for Read/Write of data, while the _Secondary_ database doesn't since it is currently Read only.

    ![Map display of Primary and Seconary databases.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/sqlfailovergroupmap.png "Map display of Primary and Seconary databases")

11. Scroll down, below the map, to where the **Read/write listener endpoint** and **Read-only listener endpoint** are displayed. These allow for applications to be configured to connect to the SQL Failover Group endpoints instead of the individual SQL Server endpoints.

    Copy both **Listener Endpoint** values for later reference.

    ![Read/Write and Read-only listener endpoints are displayed.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/sqlfailovergroupendpoints.png "Read/Write and Read-only listener endpoints are displayed")

12. Go back to the **contososports-01** resource group blade.

13. Select the **contosokv[Suffix]** Key vault resource.

14. Under the **Settings** menu, select **Secrets**.

15. Locate and select the **ContosoSportsLeague** secret.

16. On the **Versions** screen, select **+ New Version**.
    
17. Copy the original connection string to the **ContosoSportsDB**, but replace the server name with the **Azure SQL Failover Group Read/Write Listener Endpoint** that was copied previously, then select **Create**.

    > **Note**: The connection string will need to be in the following format:
    > ```
    > Server=tcp:{failover_group_endpoint};Initial Catalog=ContosoSportsDB;Persist Security Info=False;User ID=demouser;Password=demo@pass123;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
    > ```

    ![The ContosoSportsLeague secret Versions screen is shown with a current and older version present in the list. ](media/newvalueforsecret_keyvault.png "Secrets version list")

<!-- omit in toc -->
#### Subtask 3: Failover SQL Database Failover Group

>**Note**: This subtask is optional.

Since the Replication and Failover process can take anywhere from 10 to 30 minutes to complete, you have the choice to skip Subtask 3 and 4, and go directly to Task 3. However, if you have the time, it is recommended that you complete these steps.

1. In the Azure Portal, navigate back to the lab resource group.

2. From the list of resources, select the Primary SQL server resource.
    
    ![The list of lab resources is shown with the primary SQL server resource selected.](media/primary_sqlserverresource_inlist.png "Resource listing")

3. On the **SQL server** blade, select **Failover groups** under Data Management.

    ![Failover groups option is highlighted.](images/up3.png "Failover groups option is highlighted")

4. Select the **Failover group** in the list.

    ![Failover group is highlighted in the list.](images/2020-03-17-19-38-01.png "Failover group is highlighted in the list")

5. On the Failover group blade, select the **Forced Failover** button, then select **Yes** to confirm the forced failover of the SQL Database Failover Group.

    ![Forced failover confirmation is displayed.](images/2020-03-17-19-39-56.png "Forced failover confirmation is displayed")

The failover may take a few minutes to complete. You can continue with the next Subtask.

<!-- omit in toc -->
#### Subtask 4: Test e-commerce Web App after Failover

1. From the Azure portal, select **Resource Groups**, and select **contososports-01**.

2. Select the **Web App** created earlier.

3. On the **App Service** blade, select **Overview**.

    ![Screenshot of Overview menu option.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image71.png "App Service blade")

4. On the **Overview** pane, select the **URL** for the Web App to open it in a new browser tab.

    ![On the App Service blade, in the Essentials section, the URL (http;//contososportsweb4azurewebsites.net) link is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image72.png "App Service blade Essentials section")

5. After the e-commerce Web App loads in Internet Explorer, select **STORE** in the top navigation bar of the website.

    ![On the Contoso sports league website navigation bar, the Store button is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image73.png "Contoso sports league website navigation bar")

6. Verify the product list from the database displays.

    ![Screenshot of the Contoso store webpage. Under Team Apparel, a Contoso hat, tank top, and hoodie display.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image74.png "Contoso store webpage")

### Task 3: Deploying the Call Center admin website

In this exercise, you will provision a website via the Azure Web App template using the Microsoft Azure Portal. You will then edit the necessary configuration files in the Starter Project and deploy the call center admin website.

<!-- omit in toc -->
#### Subtask 1: Provision the call center admin Web App

1. Using a new tab or instance of your browser, navigate to the Azure Management portal <http://portal.azure.com>.

2. Select **+ Create a resource**, then search for and select **Web App**.

3. Specify name **contososportscallcenterapp[Suffix]** for the Web App, **Resource Group** you have used throughout the lab are selected. Also, specify **.NET Core 3.1 (LTS)** as the **Runtime stack**.

4. Select **Linux Plan**, and create a new Linux-based App Service Plan for the Web App.

5. Select a different **Region** for the web app than what was chosen for the lab. You can't mix Linux and Windows app services in the same region in the same resource group.
   
6. After the values are accepted, select **Review and create**, then **Create**.  It will take a few minutes to provision.
   
  ![On the Create Web App blade, the App name field is set to contososportscallcentercp.](media/2019-03-28-05-29-59.png "Create Web App blade")

<!-- omit in toc -->
#### Subtask 2: Update the configuration in the starter project

1. Navigate to the **App Service** blade for the Call Center Admin App just provisioned.

    ![The App Service blade displays.](media/2020-03-17-19-59-03.png "App Service blade")

2. On the **App Service** blade, select **Configuration** in the left pane.

    ![In the App Service blade, under Settings, select Configuration link.](media/2019-04-19-16-38-54.png "Configuration link")

3. Scroll down, and locate the **Connection strings** section.

4. Add a new **Connection String** with the following values, and select **OK**:

   - Name: **AppConfig**

   - Value: **Enter the Connection String for the App Configuration Store**.

   - Type: Select **Custom**.

    ![The Add/Edit connection string form is displayed and is populated with the preceding values.](media/image43.png "The Add/Edit Connection String Form")

5. Select the **OK** button.

6. Select the **Save** button.

    ![the Save button is circled on the App Service blade.](media/2019-03-28-05-36-38.png "App Service blade")

7. The call center web application resource needs access to the Key Vault. The App Configuration will use pass-through authentication to the Key Vault. To authenticate the application, it will utilize a system managed identity. From the left menu, select **Identity**.

8. With the **System assigned** tab selected, toggle the **Status** field to **On**, then select **Save**. 
    
    ![On the Identity screen, the System assigned tab is selected and the Status field is in the On position.](media/appconfig_systemidentity.png "The Identity Screen")

9. Open the **contosokv[Suffix]** Key Vault resource, and from the left menu, select **Access policies**. 

10. Select the **+ Add Access Policy** link.

11. In the **Add access policy** form, expand **Secret permissions** and check the box next to **Get** and **List**.  

12. In the **Select principal** blade, search for the name of the call center application you just created and choose the managed identity.

13. Select **Add**.
    
    ![The Add access policy form is displayed.](media/kv_addaccesspolicy_forconfig.png "The Add Access Policy form")

14. Select **Save** on the Access policies screen to commit the changes. 

<!-- omit in toc -->
#### Subtask 3: Configure and deploy the call center admin Web App from Visual Studio

1. Navigate to the **Contoso.Apps.SportsLeague.Admin** project located in the **Web** folder using the **Solution Explorer** in Visual Studio.

2. Right-click the **Contoso.Apps.SportsLeague.Admin** project, and select **Manage NuGet Packages**.

3. Select the **Browse** tab, and search for **Microsoft.Azure.AppConfiguration.AspNetCore**.

4. Select **Microsoft.Azure.AppConfiguration.AspNetCore** from the search results, and in the next pane, select **Install** to install the latest stable version.

    ![The Nuget Package Manager windows is displayed with the Browse tab selected, Microsoft.Azure.AppConfiguration.AspNetCore entered into the search box and selected from the search results. In the next pane, the Install button is selected.](media/nuget_installappconfigpackage_web.png "The NuGet Package manager")

5. Repeat step 4-6, this time installing the latest **Azure.Identity**.

6. Now we are ready to configure this application to use the App Configuration in Azure. Under the **Contoso.Apps.SportsLeague.Admin** project, open the **Program.cs** file.

7. Uncomment the following **using** statements at the top of the file:
    
    ```C#
    using Microsoft.Extensions.Configuration;
    using Azure.Identity;
    ```

8. In the **CreateHostBuilder** method, uncomment the following code - this tells the application to utilize the AppConfig connection string that you've already setup on the **contosoapp** application service to point to the centralized App Configuration resource.
    
    ```C#
    webBuilder.ConfigureAppConfiguration((hostingContext, config) =>
    {
        var settings = config.Build();

        config.AddAzureAppConfiguration(options =>
        {
            options.Connect(settings["ConnectionStrings:AppConfig"])
                    .ConfigureKeyVault(kv =>
                    {
                        kv.SetCredential(new DefaultAzureCredential());
                    });
        });
    })
    .UseStartup<Startup>();
    ```

9. Save the file by pressing **Ctrl + S** then right-click the **Contoso.Apps.SportsLeague.Admin** project and select **Publish**.

    ![In Solution Explorer, the right-click menu for Contoso.Apps.SportsLeague.Admin displays, and Publish is selected.](media/2019-04-19-14-30-03.png "Right-Click menu")

10. On the Publish dialog, select **Azure** for the **Target**, then select **Next**.

11. For **Specific target**, select **Azure App Service (Linux)**, then select **Next**. 

12. For **App Service**, expand the lab Resource group, and select the **Web App** that was created for the Call Center Admin Web App (with the name that was created previously).

    ![The App Service dialog is shown with the resource group expanded and the call center app service selected.](media/appsvcdeploy_selectcallcenterappdialog.png "Publish target app service selection")
    
13. Select **Finish**.

14. Select **Publish** to publish the Web application.

    ![Publish button is highlighted](media/2020-06-19-22-25-36.png "Publish button")

15. Once deployment is complete, navigate to the Web App. It should look like the following:

    ![The Contoso website displays the Contoso Sports League Admin webpage, which says that orders that display below are sorted by date, and you can select an order to see its details. However, at this time, there is no data available under Completed Orders.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image89.png "Contoso website")

    >**Note**: If you see a page that indicates the app service is running and asking about deploying code, refresh the browser window by selecting CTRL+F5.

### Task 4: Deploying the payment gateway

In this exercise, the attendee will provision an Azure API app template using the Microsoft Azure Portal. The attendee will then deploy the payment gateway API to the API app.

<!-- omit in toc -->
#### Subtask 1: Provision the payment gateway API app

1. Using a new tab or instance of your browser, navigate to the Azure Management Portal <http://portal.azure.com>.

2. Select **+ Create a resource**, type **API App** into the marketplace search box, and press **Enter**.  Select the **Create** button.

3. On the new **API App** create form, create the following values:

   - **App name:** contososportspaymentgateway[Suffix]
   - **Subscription:** Your Azure subscription.
   - **Resource Group:** Select the lab resource group.
   - **App Service Plan/Location:** Select the **ContosoSportsPlan**.
   - **Application Insights:** Enter the configuration, and select **Disabled**

    ![On the API App create form, the Configuration fields are displayed.](media/2019-04-20-14-55-42.png "Configuration fields are displayed")

4. After the values are accepted, select **Create**.  It will take a few minutes to provision.

<!-- omit in toc -->
#### Subtask 2: Deploy the Contoso.Apps.PaymentGateway project in Visual Studio

1. In Visual Studio, navigate to the **Contoso.Apps.PaymentGateway** project located in the **APIs** folder using the **Solution Explorer**.

2. Right-click the **Contoso.Apps.PaymentGateway** project, and select **Publish**.

    ![In Solution Explorer, Contoso.Apps.PaymentGateway is selected, and in its right-click menu, Publish is selected.](media/2019-04-19-14-52-22.png "Solution Explorer")

3. On the Publish dialog, select **Azure** as the **Target**, then select **Next**.

4. For **Specific target**, select **Azure App Service (Windows)**, then select **Next**.

5. For **App Service**, expand the resource group, and select the API app service that you created for the payment gateway from the list, then choose **Next**.

    ![The App Service form is shown with the payment gateway api selected.](media/deployment_selectpaymentapiappservice.png "Publish target App Service selection")

6. In the **API Management** form, check the **Skip this step** checkbox. Select **Finish**.
   
7. Select **Publish** to publish the API App.

    ![Publish button is highlighted](media/2020-06-19-22-33-57.png "Publish button is highlighted")

8. In the Visual Studio **Output** view, you will see a status indicating the Web App was published successfully.

    ![The Visual Studio output shows that the web app was published successfully.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image99.png "Visual Studio output")

9.  Copy and paste the gateway **URL** of the deployed **API App** into Notepad for later use.

10. Viewing the Web App in a browser will display the Swagger UI for the API.

   ![Payment Gateway is up and running and the Swagger UI is displayed.](media/2019-04-11-04-58-04.png "Swagger UI")

  > **Note**: When opening the Swagger UI using the Internet Explorer browser you will see a "Resolver error" error message. This is a result of the Swagger UI no longer supporting Internet Explorer. In another browser, the Swagger UI will work as expected.

### Task 5: Deploying the Offers Web API

In this exercise, the attendee will provision an Azure API app template using the Microsoft Azure Portal. The attendee will then deploy the Offers Web API.

<!-- omit in toc -->
#### Subtask 1: Provision the Offers Web API app

1. Using a new tab or instance of your browser, navigate to the Azure Management Portal (<http://portal.azure.com>).

2. Select **+ Create a resource**, type **API App** into the marketplace search box, and press **Enter**.  Select the **Create** button.

3. On the new **API App** form, specify name **contososportsoffers[Suffix]** for the **API App**, and ensure the previously used Resource Group and the **ContosoSportsPlan** App Service Plan are selected. You may also disable **Application Insights**.

    ![In the API App form, a unique name is typed in the App name field. App configuration fields displayed.](media/2019-04-11-05-03-33.png "API App blade")

4. Select the **Create** button.

5. When the API App has completed provisioning, return to the resource group, then select the new API App from the list of resources.

<!-- omit in toc -->
#### Subtask 2: Configure Cross-Origin Resource Sharing (CORS)

1. On the **App Service** blade for the Offers API, under the **API** menu section, scroll down and select **CORS**.

    ![In the App Service blade, under API, CORS is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image102.png "App Service blade")

2. In the **Allowed Origins** text box, specify `*` to allow all origins, and select **Save**.

    >**Note**: You should not normally do this in a production environment. In production, you should enter the specific domains as allowed origins you need to allow CORS access to the API. The wildcard (*) is used for this lab to make it easier just for this lab.

    ![CORS configuration blade displayed.  Entering * as the Allowed Origins value.](media/2019-03-28-08-20-57.png "CORS configuration blade")

<!-- omit in toc -->
#### Subtask 3: Update the configuration in the starter project

1. On the **App Service** blade for the Offers API, select **Configuration**.

    ![In the App Service blade, under Settings, select Configuration link.](media/2019-04-19-16-38-54.png "Configuration link")

2. Scroll down, and locate the **Connection strings** section.

3. Add a new **Connection String** with the following values, and select **OK**:

   - Name: **AppConfig**

   - Value: **Enter the Connection String for the App Configuration Store**.

   - Type: Select **Custom**.

    ![The Add/Edit connection string form is displayed and is populated with the preceding values.](media/image43.png "The Add/Edit connection string form")

4. Select the **OK** button.

5. Select the **Save** button.

    ![the Save button is circled on the App Service blade.](media/2019-03-28-05-36-38.png "App Service blade")

6. The offers api resource needs access to the Key Vault. The App Configuration will use pass-through authentication to the Key Vault. To authenticate the application, it will utilize a system managed identity. From the left menu, select **Identity**.

7. With the **System assigned** tab selected, toggle the **Status** field to **On**, then select **Save**. 

    ![On the Identity screen, the System assigned tab is selected and the Status field is in the On position.](media/appconfig_systemidentity.png "The Identity screen")

8. Open the **contosokv[Suffix]** Key Vault resource, and from the left menu, select **Access policies**. 

9. Select the **+ Add Access Policy** link.

10. In the **Add access policy** form, expand **Secret permissions** and check the box next to **Get** and **List**.  

11. In the **Select principal** blade, search for the name of the offers api application you just created and choose its managed identity.

12. Select **Add**.

    ![The Add access policy form is displayed.](media/kv_addaccesspolicy_forconfig.png "The Add access policy form")

13. Select **Save** on the Access policies screen to commit the changes.

<!-- omit in toc -->
#### Subtask 4: Deploy the Contoso.Apps.SportsLeague.Offers project in Visual Studio

1. Navigate to the **Contoso.Apps.SportsLeague.Offers** project located in the **APIs** folder using the **Solution Explorer** in Visual Studio.

2. Right-click the **Contoso.Apps.SportsLeague.Offers** project, and select **Manage NuGet Packages**.

3. Select the **Browse** tab, and search for **Microsoft.Azure.AppConfiguration.AspNetCore**.

4. Select **Microsoft.Azure.AppConfiguration.AspNetCore** from the search results, and in the next pane, select **Install** to install the latest stable version.

    ![The Nuget Package Manager windows is displayed with the Browse tab selected, Microsoft.Azure.AppConfiguration.AspNetCore entered into the search box and selected from the search results. In the next pane, the Install button is selected.](media/nuget_installappconfigpackage_web.png "The NuGet Package Manager")

5. Repeat step 4-6, this time installing the latest **Azure.Identity**.

6. Now we are ready to configure this application to use the App Configuration in Azure. Under the **Contoso.Apps.SportsLeague.Offers** project, open the **Program.cs** file.

7. Uncomment the following **using** statements at the top of the file:

    ```C#
    using Microsoft.Extensions.Configuration;
    using Azure.Identity;
    ```
8. In the **CreateHostBuilder** method, uncomment the following code - this tells the application to utilize the AppConfig connection string that you've already setup on the API application service to point to the centralized App Configuration resource.

    ```C#
    webBuilder.ConfigureAppConfiguration((hostingContext, config) =>
    {
        var settings = config.Build();

        config.AddAzureAppConfiguration(options =>
        {
            options.Connect(settings["ConnectionStrings:AppConfig"])
                    .ConfigureKeyVault(kv =>
                    {
                        kv.SetCredential(new DefaultAzureCredential());
                    });
        });
    })
    .UseStartup<Startup>();
    ```

9. Save the file by pressing **Ctrl +S** then right-click the **Contoso.Apps.SportsLeague.Offers** project, and select **Publish**.

    ![In Solution Explorer, from the Contoso.Apps.SportsLeague.Admin right-click menu, Publish is selected.](media/2019-04-19-15-03-45.png "Solution Explorer")

10. On the Publish dialog, select **Azure** for the **Target**. Select **Next**.

11. For **Specific target**, select **Azure App Service (Windows)**. Select **Next**.

12. For **App Service**, expand the resource group, and select the API app service that you created for the Offer API from the list, then choose **Next**.

    ![The App Service dialog is shown with the offers api selected.](media/deployment_selectoffersapiservice.png "Publish target app service selection")
    
13. For **API Management**, check the **Skip this step** checkbox and select **Finish**.
    
14. Select **Publish** to publish the API App.

    ![Publish button is highlighted](media/offerapi_vspublishbutton.png "Publish button is highlighted")

15. In the Visual Studio **Output** view, you will see a status indicating the Web App was published successfully.

    ![The Visual Studio output shows that the web app was published successfully.](media/offerapi_publishsuccessoutput.png "Visual Studio output")

16. Copy and paste the offer api **URL** of the deployed **API App** into Notepad for later use.

17. Viewing the Web App in a browser will display the Swagger UI for the API.

18. In the Visual Studio **Output** view, you will see a status the API app was published successfully.

19. Record the value of the deployed API app URL into Notepad for later use.

20. Viewing the Web App in a browser will display the Swagger UI for the API.

    ![The Offers API is up and running and the Swagger UI is displayed.](media/2019-04-11-05-20-40.png "Swagger UI")

    > **Note**: When opening the Swagger UI using the Internet Explorer browser you will see a "Resolver error" error message. This is a result of the Swagger UI no longer supporting Internet Explorer. In another browser, the Swagger UI will work as expected.

21. Within the Swagger UI for the Offers API, select the `/api/get` method on the API. Then select the **Try it out** button, and then **Execute** to test out the API call from within the Swagger UI in the web browser. Once it executes, scroll down to view the results of the API call execution.

    ![Swagger UI displaying API call response.](media/2020-03-17-20-56-31.png "Swagger UI")

### Task 6: Add API endpoint configuration settings

<!-- omit in toc -->
#### Subtask 1: Add the API endpoint configuration settings

1. In the Azure Portal, return to the lab resource group.

2. Select the **contosoconfig[Suffix]** App Configuration resource from the list.

    ![The resource listing is displayed with the App Configuration resource highlighted.](media/appconfig_resourcelist_selection.png "The resource listing")

3. On the left menu, in the **Operations** section, select **Configuration explorer**.

4. Expand the **+ Create** button, and select **Key-value**. This API endpoint does not contain any secret values, thus is not required to be stored as a Key Vault value.

    ![The + Create button is expanded with the Key-value item selected.](media/appconfig_createkeyvaluemenu.png "Create key value menu item")

5. Create the new key-value entry with the following values:

   - Name: `APIEndpoints:PaymentsAPI`

   - Value: Enter the **HTTPS** URL for the Payment gateway API App with `/api/nvp` appended to the end. This is the value that you recorded when deploying the API. Alternatively, this value can be retrieved by opening the API resource in the Azure Portal and copying the URL value on the Overview screen.

        >**Example**: `https://paymentsapi0.azurewebsites.net/api/nvp`

6. Create another Key-value setting with the following values:

   - App Setting Name: `APIEndpoints:OffersAPI`

   - Value: Enter the **HTTPS** URL for the Offers API App with `/api/get` appended to the end. This is the value that you recorded when deploying the API. Alternatively, this value can be retrieved by opening the API resource in the Azure Portal and copying the URL value on the Overview screen.

    >**Example**: `https://offersapi4.azurewebsites.net/api/get`

    >**Note**: Ensure both API URLs are using **SSL** (https://), or you will see a CORS errors.

    ![The list of Configuration settings is shown with the two new API endpoint settings highlighted.](media/appconfig_listofsettingswithAPIendpointshighlighted.png "Configuration Settings")

<!-- omit in toc -->
#### Subtask 2: Validate App Settings are correct

1. Return to the lab Resource Group and select the **contosoapp** App Service (the e-commerce website). On the **App Service** blade, select **Overview**.

    ![Overview is selected on the left side of the App Service blade.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image119.png "App Service blade")

2. In the **Overview** pane, select the **URL** for the Web App to open it in a new browser tab.

    ![On the right side of the App Service overview screen, the URL (http://contososportsweb2101.azurewebsites.net) link is highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image120.png "App Service blade")

3. On the homepage, you should see the latest offers populated from the Offers API.

    ![On the Contoso Sports League webpage, Today\'s offers display: Baseball socks, Road bike, and baseball mitt.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image121.png "Contoso Sports League webpage")

    >**Note**: The page may be cached, if Today's Offers are not displayed, you can try re-publishing the e-commerce app service from Visual Studio (Contoso.Apps.SportsLeague.Web).

4. Submit several test orders to ensure all pieces of the site are functional.  **Accept the default data during the payment processing.**

    ![On the Contoso Sports League webpage, the message Order Completed displays.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image122.png "Contoso Sports League webpage")

>**Leader Note**: If the attendee is still experiencing CORS errors, ensure the URLs to the Web App in Azure local host are exact.

## Exercise 2: Identity and Security

Duration: 75 Minutes

The Contoso call center admin application will only be accessible by users of the Contoso Active Directory environment. You have been asked to create a new Azure AD Tenant and secure the application so only users from the tenant can log on.

### Task 1: Enable Azure AD Premium Trial

>**Note**: This task is **optional**, and it is valid only if you are a global administrator on the Azure AD tenant associated with your subscription.

1. Navigate to the Azure Management portal, [http://portal.azure.com](http://portal.azure.com/), using a new tab or instance.

2. Expand the left-hand navigation menu, select **Azure Active Directory**.

    ![The Azure Active Directory menu option.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image123.png "Azure Portal")

3. On the **Azure Active Directory** blade, locate and select the **Licenses** option under **Manage** Menu.

    ![In the Azure Active Directory blade, Company branding is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up4.png "Azure Active Directory blade")

4. Under Quick Tasks, select the **Get a free trial...** link.

    ![On the left side of the Azure Active Directory blade, Company branding is selected. On the right side, the Get a free Premium trial link is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up5.png "Azure Active Directory blade")

    If you already have a Premium Azure Active Directory, skip to Task 2.

5. On the **Activate** blade, select the **Free Trial** link within the **Azure AD Premium P2**, then select **Activate**.

    ![The Free trial link is selected on the Activate blade in the Azure AD Premium P2 box, and the Activate button is highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image126.png "Activate blade")

6. Close the **Azure Active Directory** blades.

### Task 2: Create a new Contoso user

>**Note**: This task is **optional**, and it is valid only if you are a global administrator on the Azure AD tenant associated with your subscription.

1. Navigate to the Azure Management portal, [http://portal.azure.com](http://portal.azure.com/), using a new tab or instance.

2. Select **Azure Active Directory** in the navigation menu to the left.

    ![Screenshot of Azure Active Directory menu option.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image123.png "Azure Portal")

3. On the **Azure Active Directory** blade, select **Custom Domain names**.

    ![Custom Domain Names menu option screenshot.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image128.png "Custom Domain names")

4. Copy the **Domain Name** for your Azure AD Tenant. It will be in the format: *[your tenant\].onmicrosoft.com*.
    This will be used for creating the new user's Username.

    ![Under Name, the Domain Name is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image129.png "Domain name")

5. On the **Azure Active Directory** blade, select **Users**.

    ![Under Manage, All users is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image130.png "Azure Active Directory blade")

6. Select **+ New user** to add a new user.

    ![The + New User button is boxed in red on the Azure Active Directory blade.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image131.png "Azure Active Directory blade")

7. On the **User** blade, specify following values and click on **Create**.

    - **User name:** Chris
    - **Name:** Chris Green
    - Select **Let me create the password** 
    - **Initial password:** Azure1234567

    ![On the User blade, the two previously defined fields (Name and User name) are circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up7.png "User blade")


### Task 3: Configure access control for the call center administration Web Application

>**Note**: This task is **optional**, and it is valid only if you have the right to create applications in your Azure AD Tenant.

<!-- omit in toc -->
#### Subtask 1: Enable Azure AD Authentication

1. On the left navigation of the Azure Portal, select **App Services**.

    ![Screenshot of the App Services button.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image135.png "App Services button")

2. On the **App Services** blade, select the **Call Center Administration Web app**.

    ![In the App Services blade, under Name, contososportscallcentercp is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image136.png "App Services blade")

3. Select the **Authentication (classic)** tile.

    ![On the App Service blade, under Settings, Authentication / Authorization is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up8.png "App Service blade")

4. Change **App Service Authentication** to **On**, and change the dropdown to **Log in with Azure Active Directory**.

    ![The Authentication / Authorization section displays with App Service Authentication button set to On, and Log in with Azure Active Directory selected in the Action to take when request is not authenticated drop-down list box.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image138.png "Authentication / Authorization section")

5. Select the **Azure Active Directory**.

    ![In the Authentication Providers section, Azure Active Directory (Not Configured) is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image139.png "Authentication Providers section")

6. On the **Azure Active Directory Settings** blade, change **Management mode** to **Express**.

    ![At the bottom of the Azure Active Directory Settings blade, Management mode is set to Express.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image140.png "Azure Active Directory Settings blade")

7. Keep the remaining fields as their default, and select **OK**.

    ![Screenshot of the OK button.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image141.png "OK button")

8. Change the **Action to take when request is not authenticated** option to **Login with Azure Active Directory**.

    ![The Action to take when request is not authenticated field is set to Log in with Azure Authentication.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image142.png "Action to take field")

9. In the **Authentication (classic)** blade, select **Save**.

    ![The Save button is circled in the App Service blade.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up9.png "App Service blade")

<!-- omit in toc -->
#### Subtask 2: Verify the call center administration website uses the access control logon

1. Close your browser (or use an alternative), and launch a browser is **InPrivate or Incognito mode**. Navigate to the **Call Center Administration** website.

2. The browser will redirect to the non-branded Access Control logon URL. You can log on with your Microsoft account or the **Contoso test user** you created earlier.

>**Note:** For first Login you may be prompted to change the password, Provide a new password to continue with the lab.

   ![Microsoft login prompt.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image144.png "Microsoft login prompt")

3. After you log on and **accept the consent**, your browser will be redirected to the Contoso Sports League Admin webpage.

    ![The Contoso Sports League Admin webpage displays with one Completed Order.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image145.png "Contoso Sports League Admin webpage")

4. Verify in the upper-right corner you see the link **Logged In**. If it is not configured, you will see **Sign in**.

    ![Screenshot of the Logged In message.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image146.png "Logged in message") ![Screenshot of the Sign In link.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image147.png "Sign in link")

### Task 4: Apply custom branding for the Azure Active Directory logon page

>**Note**: this task is **optional**, and it is valid only if you are a global administrator on the Azure AD tenant associated with your subscription, and you completed the Enabling Azure AD Premium exercise.

1. Navigate to the Azure Management portal, [http://portal.azure.com](http://portal.azure.com/), using a new tab or instance.

2. In the navigation menu to the left, select **Azure Active Directory**.

    ![The Azure Active Directory menu option.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image123.png "Azure Active Directory")

3. On the **Azure Active Directory** blade, select **Company branding**.

    ![On the Azure Active Directory blade, Company branding is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image148.png "Azure Active Directory blade")

4. Select the **Configure...** information box.

    ![The Configure company branding link is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image149.png "Configure company branding link")

5. On the **Configure company branding** blade, select the `default_signin_illustration.jpg` image file from `C:\MCW` for the **Sign-in page image**.

    ![The Configure company branding blade displays the default sign in picture of the Contoso sports league text, and a person on a bicycle. Below that, the Select a file field and browse icon is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image150.png "Configure company branding blade")

6. Select the `logo-60-280.png` image file from the supplementary files for the **Banner image**.

    ![The Contoso sports league banner text displays.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image151.png "Contoso sports league banner")

7. Select **Save**.

    ![The Save button is circled on the Configure company branding blade.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image152.png "Configure company branding blade")

### Task 5: Verify the branding has been successfully applied to the Azure Active Directory logon page

1. Close any previously authenticated browser sessions to the call center administration website, reopen using InPrivate or Incognito mode, and navigate to the **call center administration** website.

2. The browser will redirect to the branded access control logon URL.

    ![The Call center administration Sign in webpage displays in an InPrivate / Incognito browser.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image153.png "Call center administration website")

3. After you log on, your browser will be redirected to the Contoso Sports League Admin webpage.

    ![The Contoso Sports League Admin webpage displays with one completed order.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image145.png "Contoso Sports League Admin webpage")

4. Verify in the upper-right corner you see the link **Logged in**.

    ![Screenshot of the Logged in message.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image146.png "Logged in message")

    >**Note**: If you run the app using localhost, ensure connection strings within all the appsettings.json files in the solution have the placeholders removed with actual values. Search on appsettings.json in the Visual Studio Solution Explorer to come up with the list.

## Exercise 3: Enable Azure B2C for customer site

Duration: 75 minutes

In this exercise, you will configure an Azure AD Business to Consumer (B2C) instance to enable authentication and policies for sign-in, sign-out and profile policies for the Contoso E-Commerce site.

### Task 1: Create a new directory

1. In Azure portal search for **Subscriptions** and click on it.

2. Click on the name of your subscription.

  ![.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up10.png "Everything blade")
  
3. In left blade, under settings, click on **Resource Providers**

   ![.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up11.png "Everything blade")
   
4. Now under Resource providers search for **Microsoft.AzureActiveDirectory** and select it from the search results then click on **Register**.

   ![.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/up12.png "Everything blade")

5. Log in to the Azure portal by using your existing Azure subscription or by starting a free trial. In the left-hand navigation menu, select **+Create a resource**. Then, search for and select **Azure Active Directory B2C** and select **Create** on the new blade that pops up.

    ![In the Everything blade, the active directory B2C text is in the Search field, and under Results, Azure Active Directory B2C displays.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image156.png "Everything blade")

6. In the new blade, select **Create a new Azure AD B2C Tenant**. Then, enter the name as **ContosoB2C** and a unique domain name and region. Select **Review + create**, then **Create**. After directory creation completes, select the link in the new information tile that reads **Click here to navigate to your new directory**.

    ![Image of the Create a directory with the required fields filled in.](media/2020-06-20-23-12-29.png "Create a directory")

    ![Image showing the Directory creation was successful.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image157.png "Directory creation was successful")

7. The new Azure AD Directory that was created will now be open in new browser tab. Keep this tab open for the next few steps.

8. Back in the browser tab where you created the Azure AD Directory from, open the new Azure AD B2C tenant by selecting **Resource Groups** in the navigation menu to the left and then, **contososports**. Then, in the new blade, select the **B2C tenant** you just created.

    ![In the contososports resource group, the new B2C tenant is highlighted.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/b2ctenant_in_rg.png "Azure AD B2C Settings window")

9. In the new blade, select the **Azure AD B2C Settings** tile for the new B2C tenant. You will be taken to the new subscription for this tenant.

    ![In the Azure AD B2C tenant window, on the left, All Settings is selected. In the bottom right section, the Azure AD B2C Settings tile is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image160.png "Azure AD B2C Settings window")

10. In the new tab that opened, under the **MANAGE** menu area of the open **Azure AD B2C** blade, select **App registrations**. Then, in the new pane, select **+New registration**.

    ![In the Azure AD B2C Settings window, on the left, All Settings is selected. In the middle, under Settings, under Manage, App registrations is selected. On the right, the New registration button is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/b2c-add-app-link.png "Azure AD B2C Settings window")

### Task 2: Add a new application

1. Specify the following configuration options for the new Application registration:

    - Name: **Contoso B2C Application**

    - Supported account types: **Accounts in any identity provider or organizational directory (for authenticating users with user flows)**.

    - Redirect URI: Set to **Web**, then set the URL to the following format: `https://[your web url].azurewebsites.net/signin-oidc-b2c` _(This should be the HTTPS URL to the Contoso E-Commerce Site.)_

        ![The New application fields are set to the previously defined values.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image161.png "New application")

2. Select **Register**.

3. Once App registration has completed, copy the **Application (client) ID** of your new application to Notepad to use later. Keep this tab open for the next task.

     ![B2C application name and ID values are shown.](media/2020-06-20-23-36-30.png "Azure AD B2C screen")

### Task 3: Create Policies, Sign up and sign in

1. Navigate back to the **Azure AD B2C** screen.

2. To enable sign-up on your application, you will need to create a sign-up policy. This policy describes the experiences consumers will go through during sign-up and the contents of tokens the application will receive on successful sign-ups. Select **User flows** link on the left menu and then **+New user flow** link at the top of the blade.

    ![On the Azure AD B2C screen, User Flows selected from the left menu and the +New user flow button is highlighted in the toolbar.](media/2020-06-20-23-39-59.png "Azure AD B2C - User Flows selected")

3. Select the **Sign up and sign in** tile, then under Version, select **Recommended**, then select the **Create** button.
  
    ![The Select a user flow type section is displayed with the Sign up and sign in tile highlighted.](media/2019-03-28-12-20-42.png "Sign up and sign in tile")

4. Enter **SignUp** in the **Name** field.

    ![The unique Azure AD B2C user flow name is displayed.](media/2019-04-11-08-40-58.png "User Flow Name")

5. Beneath **Identity providers**, check **Email Signup**. Optionally, you can also select social identity providers (if previously configured for the tenant).

    ![In the Add policy blade, Identity providers is selected. In the Select identity providers blade, Email signup is selected.](media/2019-03-28-12-25-35.png "Add policy and Select identity providers blades")

6. In the **Multifactor authentication** section, ensure **MFA enforcement** is set to **Off**, this will disable MFA for this exercise.

    ![The Multifactor authentication section of the form is displayed with MFA enforcement set to Conditional.](media/up13.png "MFA enforcement form")

7. In the **Conditional Access** section. Uncheck the **Enforce conditional access policies** checkbox.

    ![The Conditional Access section of the form is displayed with the enforce conditional access policies checkbox unchecked.](media/uncheck_conditionalaccess.png "Conditional Access form")

8. In the **User attributes and claims** section, select the **Show more...** link.


9. In the **User attributes and token claims** section, select the following **Collect attribute** checkboxes:

    - **Country/Region**
    - **Display Name**
    - **Postal Code**

10. Select the following **Return claim** checkboxes:

    - **Display Name**
    - **Identity Provider**
    - **Postal Code**
    - **User is new**
    - **User's Object ID**
  
11. Review your selections, then select **OK**.

    ![The user attributes and claims section is displayed showing the appropriate checkbox selections described in the previous two steps.](media/2019-03-28-12-44-04.png "User attributes and claims listing")

12. Select **Create**. Observe the policy just created appears as **B2C\_1\_SignUp** (the **B2C\_1\_** fragment is automatically added) in the **Sign-up policies** blade.

    >**Note**: The page may take a few minutes to load/refresh after you start creating the policy.

    ![Azure AD B2C - User flows list.  Shows the newly created flow.](media/2019-03-28-12-46-48.png "Azure AD B2C User Flow List")

13. Open the policy by selecting the link in the list e.g. **B2C\_1\_SignUp**.

14. Select **Run user flow** and open the dialog.

    ![In the Policies section, Sign-in policies is selected.](media/2019-03-28-12-52-27.png "Policies section")

15. Select **Run user flow** - Choose application and run user flow. 

    ![Choose application options are displayed. Contoso B2C Application option is selected. Run user flow button is displayed.](media/2019-03-28-12-55-51.png "Test the user flow")

16. A browser tab/window will open that looks like the following screenshot.

    ![Test the user flow.  Sample sign in presented in the browser.](media/2019-03-28-13-00-01.png "Test the user flow")

17. Select **Sign up now**.

    ![Sign up now fields are presented to the user.](media/2019-03-28-13-02-25.png "Sign up now")

### Task 4: Create a profile editing policy

To enable profile editing on your application, you will need to create a profile editing policy. This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.

1. Select **User flows** link on the left blade.

2. Select **+ New user flow** link at the top of the blade.

3. For the **Select a user flow type**, select the **Profile editing** card.

    ![The Create a user flow screen is displayed with the Profile editing card selected.](media/2019-03-28-16-19-55.png "Select Profile Editing")

4. For the **Version**, select **Recommended**, then select **Create**.

5. The Name determines the profile editing policy name used by your application. For example, enter **EditProfile**.

    ![In the Add policy blade, Identity providers (1 Selected) is selected. Identities providers - select Local Account SignIn.](media/2019-03-28-16-24-26.png "select Local Account SignIn")

6. In the **Identity providers** section, select **Email signin**.

   ![The Identity providers section of the form is displayed with Email signin selected.](media/profile_identityproviders.png "Identity providers")

7. In the **Multifactor authentication** section, ensure the MFA enforcement is set to **Conditional**.

8. For the **Conditional Access** section, uncheck the **Enforce conditional access policies** checkbox.

   ![The Conditional Access section of the form is displayed with the Enforce conditional access policies checkbox unchecked.](media/profile_conditionalaccess.png "Conditional Access")

9. In the **User attributes** section, select the **Show more...** link at the bottom of the checkbox lists.

10. For the **Collect attribute** section, you choose attributes the consumer can view and edit.

    For now, select the following:

    - **Country/Region**
    - **Display Name**
    - **Job Title**
    - **Postal Code**
    - **State/Province**
    - **Street Address**

11. For the **Return claims** section, you choose claims you want returned in the tokens sent back to your application after a successful profile editing experience.

    For now, select the following:

    - **Display Name**
    - **Postal Code**

    ![Sign up - User attributes selected blade.](media/2019-03-28-16-28-53.png "Sign up - User attributes selected blade")

12. Select **OK**.

13. Select **Create**. Observe the policy just created appears as \"**B2C\_1\_EditProfile**\" (the **B2C\_1\_** fragment is automatically added) in the **Profile editing policies** blade.

14. Open the policy by selecting **B2C\_1\_EditProfile**, then **Run user flow**.

15. Select **Contoso B2C application** in the **Application** drop-down.

16. Select **Run user flow**. A new browser tab opens, and you can run through the profile editing consumer experience in your application.

### Task 5: Create a password reset policy

To enable profile editing on your application, you will need to create a profile password reset. This policy describes the experiences that consumers will go through during password reset and the contents of tokens that the application will receive on successful completion.

1. Select **User flows** link on the left blade.

2. Select **+ New user flow** link at the top of the blade.

3. From the **Select a user flow type**, select the **Password reset** card.

    ![The Create a user flow form is displayed with the Password reset card highlighted.](media/2020-03-19-09-47-15.png "Select Password reset")

4. For **Version**, select **Recommended**. Select **Create**.

5. The Name determines the profile editing policy name used by your application. For example, enter **SSPR**.

6. Under Identity providers, select **Reset password using email address**.

7. In the **Multifactor authentication** section, ensure **MFA enforcement** is set to **Conditional**.

8. In the **Conditional Access** section, uncheck the **Enforce conditional access policies** checkbox.

9. In the **Application claims** section, select the **Show more** link at the bottom of the checklist box.

10. In the **Return claim** column, choose attributes about the user that are returned to the application in the token.

    For now, select the following:

    - **Email Addresses**
    - **Given Name**

11. Select **OK**.

12. Select **Create**. Observe the policy just created appears as \"**B2C\_1\_SSPR**\" (the **B2C\_1\_** fragment is automatically added) in the **Profile editing policies** blade.

13. Open the policy by selecting **B2C\_1\_SSPR**, then **Run user flow**.

14. Select **Contoso B2C application** in the **Select Application** drop-down.

15. Select **Run user flow**. A new browser tab opens, and you can run through the profile editing consumer experience in your application.

### Task 6: Modify the Contoso.App.SportsLeague.Web

1. Expand the **Contoso.Apps.SportsLeague.Web** project. Find the **Startup.cs** code file, locate the `public void ConfigureServices(` method declaration, then add the following line of code to the bottom of this method:

    ```csharp
    services.AddAuthentication(Microsoft.AspNetCore.Authentication.AzureADB2C.UI.AzureADB2CDefaults.AuthenticationScheme)
                .AddAzureADB2C(options => Configuration.Bind("AzureADB2C", options));
    ```

    ![The Startup.cs file with the "app.UseAuthorization();" line of code highlighted.](media/2019-04-19-15-08-40.png "Startup.cs")

2. Add the following `using` directives to the top of the **Startup.cs** code file:

    ```csharp
    using Microsoft.AspNetCore.Authentication;
    using Microsoft.AspNetCore.Authentication.AzureADB2C.UI;
    ```

3. Locate the `app.UseAuthorization();` line within the `public void Configure` method, and add the following line of code before it:

    ```csharp
    app.UseAuthentication();
    ```

    The result will look similar to the following:

    ![app.UseAuthentication code inserted.](media/2020-03-18-14-44-13.png "app.UseAuthentication code inserted")
    
4. **Save** the file.

5. Locate the Azure AD B2C name by navigating to your resource group. Copy the name to Notepad.

    ![List of all of the resources within the ContosoSports resource group. Pointing to the B2C tenant name.](media/2019-03-28-16-51-14.png "Locate B2C tenant name")

6. Next, using the Azure Management Portal, using your main subscription, open the Contoso Web App blade, and select **Configuration**.

7. Add the following settings in the **Application Settings** section:

   - AzureADB2C:Instance - `https://[your Azure AD B2C name].b2clogin.com/tfp/`
   - AzureADB2C:ClientId - **B2C Application ID you copied down earlier**.
   - AzureADB2C:CallbackPath - `/signin-oidc-b2c`
   - AzureADB2C:Domain - **[your Azure AD B2C name].onmicrosoft.com**
   - AzureADB2C:SignUpSignInPolicyId - `B2C_1_SignUp`
   - AzureADB2C:ResetPasswordPolicyId - `B2C_1_SSPR`
   - AzureADB2C:EditProfilePolicyId - `B2C_1_EditProfile`

8. Select **Save**.

### Task 7: Send authentication requests to Azure AD

Your app is now properly configured to communicate with Azure AD B2C by using ASP.NET Core Identity. OWIN has taken care of all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session. All that remains is to initiate each user's flow.

1. Right click on the **Controllers** folder, and select **Add** -\> **Controller**.

    ![In Solution Explorer, in the right-click menu for the Controllers folder, Add is selected, and from its menu, Controller is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image177.png "Solution Explorer")

2. Select **MVC Controller -- Empty** and then select **Add**. Replace default name of **HOmeController1.cs** with the name of **AccountController.cs** for the new Controller being added.

    ![On the left of the Add Scaffold window, Installed / Controller is selected. In the center of the window, MVC 5 Controller - Empty is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image178.png "Add Scaffold window")

3. Add the following using statement to the top of the controller:

    ```csharp
    using Microsoft.AspNetCore.Authentication;
    using Microsoft.AspNetCore.Authentication.AzureADB2C.UI;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Configuration;
    ```

4. Locate the default controller **Index** method.

    ![The Default controller method Index is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image179.png "Default controller method Index")

5. Replace the method with the following code:

    ```csharp
    // Controllers\AccountController.cs

    private string _editProfilePolicyId;

    public AccountController(IConfiguration configuration)
    {
        _editProfilePolicyId = configuration.GetValue<string>("AzureADB2C:EditProfilePolicyId");
    }

    public ActionResult SignIn()
    {
        if (!User.Identity.IsAuthenticated)
        {
            return Challenge(new AuthenticationProperties() { RedirectUri = "/" }, AzureADB2CDefaults.AuthenticationScheme);
        }
        return RedirectToAction("Index", "Home");
    }

    public ActionResult SignUp()
    {
        if (!User.Identity.IsAuthenticated)
        {
            return Challenge(new AuthenticationProperties() { RedirectUri = "/" }, AzureADB2CDefaults.AuthenticationScheme);
        }
        return RedirectToAction("Index", "Home");
    }

    public ActionResult Profile()
    {
        if (User.Identity.IsAuthenticated)
        {
                var properties = new AuthenticationProperties() { RedirectUri = "/" };
                properties.Items[AzureADB2CDefaults.PolicyKey] = _editProfilePolicyId;
                return Challenge(
                    properties,
                    AzureADB2CDefaults.AuthenticationScheme);
        }
        return RedirectToAction("Index", "Home");
    }

    public ActionResult SignOut()
    {
        if (!User.Identity.IsAuthenticated)
        {
            return RedirectToAction("Index", "Home");
        }
        string redirectUri = Url.Action("Index", "Home", null, Request.Scheme);
        var properties = new AuthenticationProperties
        {
            RedirectUri = redirectUri
        };
        return SignOut(properties, AzureADB2CDefaults.CookieScheme, AzureADB2CDefaults.OpenIdScheme);
    }
    ```

6. Save the file.

### Task 8: Display user information

When you authenticate users by using OpenID Connect, Azure AD returns an ID token to the app that contains **claims**. These are assertions about the user. You can use claims to personalize your app. You can access user claims in your controllers via the ClaimsPrincipal.Current security principal object.

1. Open the **Controllers\\HomeController.cs** file and add the following using statements at the end of the other using statements at the top of the file:

    ```csharp
    using Contoso.Apps.SportsLeague.Web.Models;
    using Microsoft.AspNetCore.Authorization;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Extensions.Configuration;
    ```

2. Still in the **Controllers\\HomeController.cs** file, add the following method to the **HomeController** class and save the file.

    ```csharp
    [Authorize]
    public ActionResult Claims()
    {
        var displayName = User.Identity.Name;
        ViewBag.DisplayName = displayName;
        ViewBag.Claims = User.Claims;
        return View();
    }
    ```

3. You can access any claim that your application receives in the same way. A list of all the claims the app receives is available for you on the **Claims** page. In Visual Studio on the Contoso.Apps.SportsLeague.Web object, right-click on folder **Views -\> Home,** select **Add -\> View**, choose **Razor View - Empty** and name it **Claims.cshtml**.

    ![In Solution Explorer, on the right-click menu for Views\\Home, Add is selected, and from its menu, View is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image180.png "Solution Explorer")

4. Open the **Claims.cshtml** file and replace the code with the following and **Save** the file.

    ```csharp
    @using System.Security.Claims
    @{
        ViewBag.Title = "Claims";
    }
    <h2>@ViewBag.Title</h2>

    <h4>Claims Present in the Claims Identity: @ViewBag.DisplayName</h4>

    <table class="table-hover claim-table">
        <tr>
            <th class="claim-type claim-data claim-head">Claim Type</th>
            <th class="claim-data claim-head">Claim Value</th>
        </tr>

        @foreach (Claim claim in ViewBag.Claims)
        {
            <tr>
                <td class="claim-type claim-data">@claim.Type</td>
                <td class="claim-data">@claim.Value</td>
            </tr>
        }
    </table>
    ```

5. Right-click on the **Views -\> Shared** folder, select **Add**, add a new **View**. Choose **Razor View - Empty** and **\_LoginPartial.cshtml** for the name.

    ![In Solution Explorer, on the right-click menu for Views\\Shared, Add is selected, and from its menu, View is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image180.png  "Solution Explorer")

6. Add the following code to the razor partial view to provide a sign-in and sign-out link as well as a link to edit the user's profile and **Save** the file.

    ```html
    @if (User.Identity.IsAuthenticated)
    {
        <text>
            <ul class="nav navbar-nav navbar-right">
                <li>
                    <a id="profile-link">@User.Identity.Name</a>
                    <div id="profile-options" class="nav navbar-nav navbar-right">
                        <ul class="profile-links">
                            <li class="profile-link">
                                @Html.ActionLink("Edit Profile", "Profile", "Account")
                            </li>
                        </ul>
                    </div>
                </li>
                <li>
                    @Html.ActionLink("Sign out", "SignOut", "Account")
                </li>
            </ul>
        </text>
    }
    else
    {
        <ul class="nav navbar-nav navbar-right">
            <li>@Html.ActionLink("Sign up", "SignUp", "Account", routeValues: null, htmlAttributes: new { id = "signUpLink" })</li>
            <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
        </ul>
    }
    ```

7. Open `Views\Shared\_Layout.cshtml` in Visual Studio. Locate the header-top div, and add the line that starts with `@Html.ActionLink` and the line that starts with `@Html.Partial` and **Save** the file.

    ```html
    <div class="header-top">
        <div class="container">
            <div class="row">
                <div class="header-top-left">
                <a href="#"><i class="fa fa-twitter"></i></a>
                <a href="#"><i class="fa fa-facebook"></i></a>
                <a href="#"><i class="fa fa-linkedin"></i></a>
                <a href="#"><i class="fa fa-instagram"></i></a>
                </div>
                <div class="header-top-right">
                    <a href="#" class="top-wrap"><span class="icon-phone">Call today: </span> (555) 555-8000</a>
                    @Html.ActionLink("Claims", "Claims", "Home")
                </div>
                @Html.Partial("_LoginPartial")
            </div>
        </div>
    </div>
    ```

### Task 9: Run the sample app

1. Right-click on the **Contoso.Apps.SportsLeague.Web** project, and select **Publish**. Follow the steps to deploy the updated application to the Microsoft Azure Web App.

    Launch a browser outside of Visual Studio for testing if the page loads in Visual Studio.

2. Test out Sign up.

3. Next, test Sign out.

4. When you select Claims and are not signed in, it will bring you to the sign-in page and then display the claim information. Sign in, and test Edit Profile.

    ![On the Contoso website, the following links are circled: Claims, Sign up, and Sign in.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image182.png "Contoso website")

    Claims information page:    
    ![On the Contoso website, the following links are circled: Russell, Sign out, and Edit Profile.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image183.png "Contoso website, Claims information page")

## Exercise 4: Enabling Telemetry with Application Insights

Duration: 30 Minutes

To configure the application for logging and diagnostics, you have been asked to configure Microsoft Azure Application Insights and add some custom telemetry.

### Task 1: Configure the application for telemetry

<!-- omit in toc -->
#### Subtask 1: Add Application Insights Telemetry to the e-commerce website project

1. Open the Solution **Contoso.Apps.SportsLeague** in Visual Studio.

2. Navigate to the **Contoso.Apps.SportsLeague.Web** project located in the **Web** folder using the **Solution Explorer** in Visual Studio.

3. Expand the **Contoso.Apps.SportsLeague.Web** project, then right-click on the **Dependencies** node, and select **Manage NuGet Packages...**.

4. Within the **NuGet Package Manager**, select the **Browse** tab, then search for and install the following NuGet package:

    - **Microsoft.ApplicationInsights.AspNetCore**

5. Open the file `\Helpers\TelemetryHelper.cs` located in the **Contoso.Apps.SportsLeague.Web** project.

6. Add the following using statements to the top of the file:

    ```csharp
    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    ```

7. Add the following code to the **TrackException** method to instantiate the telemetry client and track exceptions:

    ```csharp
    var client = new TelemetryClient(TelemetryConfiguration.CreateDefault());
    client.TrackException(new Microsoft.ApplicationInsights.DataContracts.ExceptionTelemetry(exc));
    ```

8. Add the following code to the **TrackEvent** method to instantiate the telemetry client and track event data:

    ```csharp
    var client = new TelemetryClient(TelemetryConfiguration.CreateDefault());
    client.TrackEvent(eventName, properties);
    ```

9. Save the `TelemetryHelper.cs` file.

<!-- omit in toc -->
#### Subtask 2: Enable client side telemetry

1. Open the Azure Management Portal (<http://portal.azure.com>), and navigate to the **contososports-01** Resource Group.

2. Select the **Application Insights** instance with the name that starts with **contososportsai** that is associated with the Contoso E-Commerce Site.

3. Capture the **Instrumentation Key**.

    - Select the **Overview** menu item.
    - Copy the **Instrumentation Key** to Notepad for later use.

    ![Contoso.Apps.SportsLeague Application Insights Overview. Instrumentation Key selected.](media/2019-03-29-10-36-23.png "Instrumentation Key selected")

4. In the tiles up top, select **Getting Started**.

    ![From the Configure menu, Getting started is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image196.png "Configure menu")

5. In the portal, navigate to **How-to Guides** -> **Application Insights** -> **Code-based monitoring** -> **JavaScript** -> **Client-side JavaScript**, then navigate to the **Snippet based setup** section under **Adding the JavaScript SDK** within the documentation page.

    ![Screenshot of the Monitor and Diagnose Client Side Application arrow.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image197.png "Monitor and Diagnose Client Side Application")

    > **Note**: You can find the documentation page at the following URL: <https://docs.microsoft.com/azure/azure-monitor/app/javascript#snippet-based-setup>.

6. Select and copy the full contents of the JavaScript under the **Snippet based setup** heading.

    ![Under Guidance in the Client application monitoring and diagnosis blade, JavaScript displays.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image198.png "Client application monitoring and diagnosis blade")

    Here's the JavaScript code to copy/paste for quick reference:

    ```javascript
    <script type="text/javascript">
        !function(T,l,y){var S=T.location,u="script",k="instrumentationKey",D="ingestionendpoint",C="disableExceptionTracking",E="ai.device.",I="toLowerCase",b="crossOrigin",w="POST",e="appInsightsSDK",t=y.name||"appInsights";(y.name||T[e])&&(T[e]=t);var n=T[t]||function(d){var g=!1,f=!1,m={initialize:!0,queue:[],sv:"4",version:2,config:d};function v(e,t){var n={},a="Browser";return n[E+"id"]=a[I](),n[E+"type"]=a,n["ai.operation.name"]=S&&S.pathname||"_unknown_",n["ai.internal.sdkVersion"]="javascript:snippet_"+(m.sv||m.version),{time:function(){var e=new Date;function t(e){var t=""+e;return 1===t.length&&(t="0"+t),t}return e.getUTCFullYear()+"-"+t(1+e.getUTCMonth())+"-"+t(e.getUTCDate())+"T"+t(e.getUTCHours())+":"+t(e.getUTCMinutes())+":"+t(e.getUTCSeconds())+"."+((e.getUTCMilliseconds()/1e3).toFixed(3)+"").slice(2,5)+"Z"}(),iKey:e,name:"Microsoft.ApplicationInsights."+e.replace(/-/g,"")+"."+t,sampleRate:100,tags:n,data:{baseData:{ver:2}}}}var h=d.url||y.src;if(h){function a(e){var t,n,a,i,r,o,s,c,p,l,u;g=!0,m.queue=[],f||(f=!0,t=h,s=function(){var e={},t=d.connectionString;if(t)for(var n=t.split(";"),a=0;a<n.length;a++){var i=n[a].split("=");2===i.length&&(e[i[0][I]()]=i[1])}if(!e[D]){var r=e.endpointsuffix,o=r?e.location:null;e[D]="https://"+(o?o+".":"")+"dc."+(r||"services.visualstudio.com")}return e}(),c=s[k]||d[k]||"",p=s[D],l=p?p+"/v2/track":config.endpointUrl,(u=[]).push((n="SDK LOAD Failure: Failed to load Application Insights SDK script (See stack for details)",a=t,i=l,(o=(r=v(c,"Exception")).data).baseType="ExceptionData",o.baseData.exceptions=[{typeName:"SDKLoadFailed",message:n.replace(/\./g,"-"),hasFullStack:!1,stack:n+"\nSnippet failed to load ["+a+"] -- Telemetry is disabled\nHelp Link: https://go.microsoft.com/fwlink/?linkid=2128109\nHost: "+(S&&S.pathname||"_unknown_")+"\nEndpoint: "+i,parsedStack:[]}],r)),u.push(function(e,t,n,a){var i=v(c,"Message"),r=i.data;r.baseType="MessageData";var o=r.baseData;return o.message='AI (Internal): 99 message:"'+("SDK LOAD Failure: Failed to load Application Insights SDK script (See stack for details) ("+n+")").replace(/\"/g,"")+'"',o.properties={endpoint:a},i}(0,0,t,l)),function(e,t){if(JSON){var n=T.fetch;if(n&&!y.useXhr)n(t,{method:w,body:JSON.stringify(e),mode:"cors"});else if(XMLHttpRequest){var a=new XMLHttpRequest;a.open(w,t),a.setRequestHeader("Content-type","application/json"),a.send(JSON.stringify(e))}}}(u,l))}function i(e,t){f||setTimeout(function(){!t&&m.core||a()},500)}var e=function(){var n=l.createElement(u);n.src=h;var e=y[b];return!e&&""!==e||"undefined"==n[b]||(n[b]=e),n.onload=i,n.onerror=a,n.onreadystatechange=function(e,t){"loaded"!==n.readyState&&"complete"!==n.readyState||i(0,t)},n}();y.ld<0?l.getElementsByTagName("head")[0].appendChild(e):setTimeout(function(){l.getElementsByTagName(u)[0].parentNode.appendChild(e)},y.ld||0)}try{m.cookie=l.cookie}catch(p){}function t(e){for(;e.length;)!function(t){m[t]=function(){var e=arguments;g||m.queue.push(function(){m[t].apply(m,e)})}}(e.pop())}var n="track",r="TrackPage",o="TrackEvent";t([n+"Event",n+"PageView",n+"Exception",n+"Trace",n+"DependencyData",n+"Metric",n+"PageViewPerformance","start"+r,"stop"+r,"start"+o,"stop"+o,"addTelemetryInitializer","setAuthenticatedUserContext","clearAuthenticatedUserContext","flush"]),m.SeverityLevel={Verbose:0,Information:1,Warning:2,Error:3,Critical:4};var s=(d.extensionConfig||{}).ApplicationInsightsAnalytics||{};if(!0!==d[C]&&!0!==s[C]){method="onerror",t(["_"+method]);var c=T[method];T[method]=function(e,t,n,a,i){var r=c&&c(e,t,n,a,i);return!0!==r&&m["_"+method]({message:e,url:t,lineNumber:n,columnNumber:a,error:i}),r},d.autoExceptionInstrumented=!0}return m}(y.cfg);(T[t]=n).queue&&0===n.queue.length&&n.trackPageView({})}(window,document,{
        src: "https://az416426.vo.msecnd.net/scripts/b/ai.2.min.js", // The SDK URL Source
        //name: "appInsights", // Global SDK Instance name defaults to "appInsights" when not supplied
        //ld: 0, // Defines the load delay (in ms) before attempting to load the sdk. -1 = block page load and add to head. (default) = 0ms load after timeout,
        //useXhr: 1, // Use XHR instead of fetch to report failures (if available),
        //crossOrigin: "anonymous", // When supplied this will add the provided value as the cross origin attribute on the script tag 
        cfg: { // Application Insights Configuration
            instrumentationKey: "YOUR_INSTRUMENTATION_KEY_GOES_HERE"
            /* ...Other Configuration Options... */
        }});
    </script>
    ```

    >**Note**: Make sure to replace the `YOUR_INSTRUMENTATION_KEY_GOES_HERE` placeholder with the Application Insights Instrumentation Key.

7. Navigate to the **Contoso.Apps.SportsLeague.Web** project located in the **Web** folder using the **Solution Explorer** in Visual Studio.

8. Open **Views \> Shared \> \_Layout.cshtml**.

    ![In Solution Explorer, under Views\\Shared, Layout.cshtml is selected.](media/2019-04-19-15-45-29.png "Solution Explorer")

9. Replace the code before the `</head>` tag. Insert your **Instrumentation Key** from Notepad into the JavaScript code ``instrumentationKey:`` value.

    ![In Layout.cshtml, code displays, and several lines are selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image200.png "Layout.cshtml tab")

10. Save the **\_Layout.cshtml** file.

<!-- omit in toc -->
#### Subtask 3: Deploy the e-commerce Web App from Visual Studio

1. Navigate to the **Contoso.Apps.SportsLeague.Web** project located in the **Web** folder using the **Solution Explorer** in Visual Studio.

2. Right-click on the **Contoso.Apps.SportsLeague.Web** project, and select **Publish**.

    ![From the Contoso.Apps.SportsLeague.Web right-click menu, Publish is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image202.png "Solution Explorer")

3. Select **Publish** again when the Publish dialog appears.

4. Launch a browser **outside of Visual Studio** for testing if the page is loaded in Visual Studio.

5. Select a few links on the published E-Commerce website, and submit several orders to generate some sample telemetry.

### Task 2: View the Application Insights logs

1. Using a new tab or instance of your browser, navigate to the Azure Management portal <http://portal.azure.com>.

2. On the left menu area, select **All services**.

3. On the **All Services** blade, filter for **Application Insights** and choose the appropriate result.

4. On the **Application Insights** blade, select the Application Insights configuration you created for the e-commerce website.

    ![The Application Insights configuration option Contoso.Apps.SportsLeague.Web is selected.](media/2020-06-21-11-06-31.png "Application Insights configuration option")

5. Select **Application Dashboard**.  View the performance timeline to see the overall number of requests and page load time.

    ![Application Insights - Contoso.Apps.SportsLeague.Web - At the top of the page, the Application Dashboard link is highlighted and has an arrow pointing to it. Failed requests and server response metrics are displayed.](media/2019-03-29-11-10-04.png "Click the Dashboard link")

    ![The Contoso web metrics are displayed. Usage, reliability, and responsiveness graphs are displayed.](media/2019-03-29-11-12-13.png "Application Insights Default Dashboard")

6. Navigate back to the Application Insights overview for the **Application Insights** instance, then select **Performance** to see individual endpoint render performance.
  
    ![Contoso.Apps.SportsLeague.Web Performance link selected.](media/2019-03-29-11-01-14.png "Performance link selected")

    ![Contoso.Apps.SportsLeague.Web Performance - Endpoint performance metrics are displayed for various types of HTTP requests.](media/2019-03-29-11-20-06.png "Endpoint performance")

7. Under **Usage** link area, select the **Events** menu option. Select the **View More Insights** button.

    ![A screenshot using the Events button under the Usage Preview section.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image218.png "The Usage Preview section")

8. Select **View More Insights**, then scroll down to see event list.

    ![In the Custom events section, event metrics are displayed for users and sessions. Different web pages are listed. e.g. OrderCompleted and SuccessfulPaymentAuth.](media/2020-06-21-11-09-04.png "Event Statistics")
    
## Exercise 5: Automating backend processes with Azure Functions and Logic Apps

Duration: 45 Minutes

Contoso wants to automate the process of generating receipts in PDF format and alerting users when their orders have been processed using Azure Logic App and Functions. To run custom snippets of C\# or node.js in logic apps, you can create custom functions through Azure Functions. [Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview) offers server-free computing in Microsoft Azure and are useful for performing these tasks:

- Advanced formatting or compute of fields in logic apps

- Perform calculations in a workflow

- Extend the logic app functionality with functions that are supported in C\# or node.js

### Task 1: Create an Azure Function to Generate PDF Receipts

1. Open the Azure Management Portal (<http://portal.azure.com>).
   
2. Select the **+ Create a resource** tile, then select **Compute \> Function App**. Select **Create** button at the bottom.

    ![The New resource screen is shown with Compute and Function app selected.](media/newcomputefunctionapp.png "Create function app in the Portal")
   
3. Provision and deploy the new function app, with the following settings:

    - **Resource Group**: Use the existing resource group, **contososports-01**.

    - **Function App name**: _Choose a unique name_.

    - **Publish**: Select **Code**.

    - **Runtime Stack**: Select **.NET Core**.
    
    - **Version**: Select **3.1**.

    - **Region**: _Choose the same region used for the e-commerce web apps in this lab_.

4. Select **Next: Hosting >**.

5. On the **Hosting** tab, select the following values, then select **Review + create**:

    - **Storage account**: Select the lab storage account, prefixed with **contoso**.
  
    - **Operating System**: Select **Windows**.

    - **Plan type**: Select **App service plan**.

    - **Windows Plan**: Select **ContosoSportsPlan**.
    
    - **Sku and size**: Select **Standard S1**. 

6. On the **Monitoring tab**

    - Enable Application Insights: **No**


7. Select **Review + create**, then **Create**.

8. Navigate to the **Function App** that was just created, and select **Configuration**.

    ![Display Contoso Function App, with the Configuration link highlighted.](media/2020-06-21-11-19-23.png "Contoso Function App Application Settings")

9. Add a new **Application Setting** with the following values, and select **OK**:

   - Name: **AppConfigConnectionString**

   - Value: **Enter the Connection String for the App Configuration Store**.
  
10.  Select the **OK** button.

11. Select the **Save** button.

12. The function application resource needs access to the Key Vault. The App Configuration will use pass-through authentication to the Key Vault. To authenticate the application, it will utilize a system managed identity. From the left menu, select **Identity**.

13. With the **System assigned** tab selected, toggle the **Status** field to **On**, then select **Save**. 
    
    ![On the Identity screen, the System assigned tab is selected and the Status field is in the On position.](media/appconfig_systemidentity.png "Identity screen")

14. Open the **contosokv[Suffix]** Key Vault resource, and from the left menu, select **Access policies**. 

15. Select the **+ Add Access Policy** link.

16. In the **Add access policy** form, expand **Secret permissions** and check the box next to **Get** and **List**.  

17. In the **Select principal** blade, search for the name of the function application you just created and choose the managed identity.

18. Select **Add**.
    
    ![The Add access policy form is displayed.](media/kv_addaccesspolicy_forconfig.png "The Add Access Policy Form")

19. Select **Save** on the Access policies screen to commit the changes. 

### Task 2: Configure and deploy the Function App

1. In Visual Studio, expand the **Web** folder and right-click on the **Contoso.Apps.FunctionApp** project, and select **Manage NuGet Packages**.

2. On the **Browse** tab, search for and select **Microsoft.Extensions.Configuration.AzureAppConfiguration**. In the right pane, select **Install**.

3. Repeat step 2, this time for the package **Azure.Identity**.

4. Within the **Contoso.Apps.FunctionApp** project, locate and open the **ContosoMakePdf.cs** source file.

5. Uncomment the following **using** statements:

    ```C#
    using Microsoft.Extensions.Configuration;
    using Azure.Identity;
    ```  
6. Inside the static class **ContosoMakePdf**, uncomment the following code that sets up a connection to the App Configuration store and the Key Vault credential pass-through:
   
    ```C#
    private static IConfiguration Configuration { set; get; }

    static ContosoMakePdf()
    {
        var builder = new ConfigurationBuilder();            
        builder.AddAzureAppConfiguration(options =>
        {
            options.Connect(Environment.GetEnvironmentVariable("AppConfigConnectionString"))               
                    .ConfigureKeyVault(kv =>
                    {
                        kv.SetCredential(new DefaultAzureCredential());
                    });
        });
        Configuration = builder.Build();
    }
    ```
7. In the **ProcessOrder** method, uncomment the following line of code and **Save** the file.

    ```C#
    Order.ReceiptUrl = await StorageMethods.UploadPdfToBlob(receipt, fileName, Configuration, log);
    ```
8. To publish the Function App, open the Visual Studio solution, Right-click on the **Contoso.Apps.FunctionApp** project, then select **Publish**.

9.  For **Target**, choose **Azure** and then select **Next**.
   
10. For **Specific target**, choose **Azure Function App (Windows)**, then select **Next**.

11. For **Functions instance**, expand the lab resource group and select the **Function App**, then select **Finish**.

    ![The App Service dialog is shown with the resource group expanded and the Function App selected.](media/deployment_appservice_functionselection.png "Publish target app service selection")
   
12. Select **Publish**.

    > **Note**: The publish should only take a minute or so. You can check the **Output** window for any errors that may occur.

    ![The build Output window is displayed. Publish succeeded message is shown.](media/2019-04-15-15-33-20.png "Output window.")

13. To test your newly published Function App, start by navigating back to your Contoso Function App in the Azure Portal. Select the newly created **ContosoMakePDF** function listed in the functions.

    ![The Azure Functions shows the ContosoMakePDF function listed.](media/2020-06-21-11-25-59.png "Azure Functions")

14. Select the **Code + Test** link, then select the **Test/Run** button.

    ![The Code + Test link and Test/Run button are highlighted](media/2020-06-21-11-27-28.png "Function Test link")

15. Select **POST** for the HTTP method.

16. Open the **sample.dat** file found in your lab files C:\MCW\Contoso Sports League\Contoso.CreatePDFReport directory.  Copy the contents into the **Request body** text box.

    ![A small screenshot of Windows Explorer is shown emphasizing the file path to the sample.dat file.](media/2019-04-15-15-47-39.png "Sample.dat File")

17. Select the **Run** button located at the bottom of the blade.

    ![The screenshot displays the Test blade with sample.dat contents. The Request body field shows the Order JSON. There is an arrow pointing to Run button.](media/2020-06-21-11-29-48.png "Display Test blade with sample.dat contents")

    > **Note**: There is also a **Run** button located at the top of the Azure Function blade. Selecting either of these buttons will run the function just the same.

    After a few seconds, you should see logs like in the below image. You should see return status code of 200.  The **Output** text box should show recent Contoso purchase data. You should see a message stating the file has been created and stored in the blob storage.

    ![There is a screenshot displaying the Function App test result log.  A status code of 200 OK is displayed on the right side pane.](media/2020-06-21-11-30-54.png "Function App test result log.")

18. Check your receipt PDF in the storage account blob.

    - Navigate to the ContosoSports storage account.
    - Select the **Blobs** link.

    ![The Settings options are displayed. There is an arrow pointing to the Blobs link.](media/2020-06-21-11-32-12.png "Containers link")

19. Choose the newly created **receipts** blob container.

    ![The storage account blobs are listed. The receipts blob container is highlighted.](media/2019-04-15-16-08-35.png "Click the Blobs link")

20. Open **ContosoSportsLeague-Store-Receipt-XX.pdf** link.

    ![There is a screenshot displaying a list of the newly created PDF receipts. An arrow pointing to the Download link is located on the right side of the screen.](media/2019-04-15-16-11-24.png "PDF Receipts")

21. Open the `...` link and choose download menu item.

    ![A sample Contoso Sports League PDF receipt is displayed.](media/2019-04-15-16-15-06.png "Sample PDF receipt")

### Task 3: Create an Azure Logic App to Process Orders

Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with Azure Logic Apps. Logic Apps provide a way to simplify and implement scalable integrations and workflows in the cloud. It provides a visual designer to model and automate your process as a series of steps known as a workflow. There are [many connectors](https://docs.microsoft.com/en-us/azure/connectors/apis-list) across the cloud and on-premises to quickly integrate across services and protocols.

The advantages of using Logic Apps include the following:

- Saving time by designing complex processes using easy to understand design tools

- Implementing patterns and workflows seamlessly, that would otherwise be difficult to implement in code

- Getting started quickly from templates

- Customizing your logic app with your own custom APIs, code, and actions

- Connect and synchronize disparate systems across on-premises and the cloud

- Build off BizTalk server, API Management, Azure Functions, and Azure Service Bus with first-class integration support


1. Next, we will create a Logic App that will trigger when an item is added to the **receiptgenerator** queue. In the Azure Management Portal, select the **+ Create a resource** button, search for and select **Logic App**, then select **Create**.

2. Fill out the name as **ContosoLogicApplication** along with your subscription, and use the existing resource group **contososports-01**. Choose the **same region** that you have been using for this lab. Select **Review + create**, then **Create** once validation has passed.

    ![In the Create logic app blade, ContosoLogicApplication is in the Name field. Under Resource group, the Use existing radio button is selected, and contososports is the name.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image237.png "Create logic app blade")

3. Open the newly created **ContosoLogicApplication** logic app resource after it is deployed.

4. In the Logic Apps Designer, under **Templates**, select **Blank Logic App**.

    ![In the Logic Apps Designer, the Blank Logic App tile is selected.](media/2019-03-29-12-56-10.png "Logic Apps Designer")

    >**Note**: The first time you access the Logic App resource, it will automatically enter the Logic App Designer. Otherwise, you can open the logic app designer by selecting the **Logic app designer** link from the left menu of the resource screen (beneath **Development Tools**).

5. Select the **All** tab, then select **Service Bus**.

    ![In the Services section, the Service Bus tile is selected.](media/2020-03-18-12-12-10.png "Services section")

6. Select **Service Bus - When a message is received in a queue (auto-complete)**.

    ![In the Search all triggers section, Service Bus - When a message is received in a queue (auto-complete).](media/2020-03-18-12-13-24.png "Search all triggers section")

7. Specify **ContosoQueue** as the connection name, select the Contoso storage account from the list.

    ![In When there are messages in a queue, the Connection Name is ContosoQueue, and under Service Bus Namespace, contosooiyxeonvhew7u is selected.](media/2020-03-18-12-15-23.png "When there are messages in a queue ")

8. Select the **RootManageSharedAccessKey** from the list of Service Bus Policies, then select **Create**.

    ![RootManageSharedAccessKey is selected.](media/2020-03-18-12-17-17.png "RootManageSharedAccessKey is selected")

9.  Select the **receiptgenerator** queue from the drop-down.

    ![Under When there are messages in a queue, the Queue name is set to receiptgenerator.](media/2020-03-18-12-19-06.png "Queue name")

    >**Note**: If you wish, you can set the **Interval** and **Frequency** to check for new items to a shorter interval than the default; such as every 30 seconds. This could help reduce delay for when the Logic App is triggered when new messages are sent to the Service Bus Queue while you progress through this lab.

10. Select the **+ New step** button, choose the **All** tab, then select **Azure Functions**.

    ![In the Choose an action section, under Services ,the Azure Functions tile is selected.](media/2020-03-18-12-21-44.png "Choose an action")

11. Select the **Azure Function App** you just created.

    ![Under Azure Functions, on the Actions tab, a single Action, the Azure function ContosoFunctionApp, is listed.](media/2020-03-18-12-22-46.png "Azure Functions")

12. Select the Azure function **ContosoMakePDF**.

    ![Under Azure Functions, on the Actions tab, a single Action, the Azure function ContosoMakePDF, is listed.](media/2020-03-18-12-23-39.png "Azure Functions")

13. Type this in the Request Body:

    ```json
    {"Order": pick Content from list (see picture below) }
    ```

    Make sure the syntax is json format. Sometimes the ":" will go to the right side of Content by mistake. Keep it on the left. It should look like this:

    ![Under ContosoMakePDF, the previous JSON code is typed in the Request Body, and to the right of this, in Insert parameters from previous steps, Content is selected.](media/2020-03-18-12-25-29.png "ContosoMakePDF")

14. Select **Save** to save the Logic App.

15. Run the logic app by selecting the **Run** button of the Logic app designer toolbar. It should process the orders you have submitted previously to test PDF generation. Using Azure Storage Explorer or Visual Studio Cloud Explorer you can navigate to the storage account and open the receipts container to see the created PDFs.

    ![In Azure Storage Explorer, on the left, the following tree view is expanded: Storage Accounts\\contososportsstorage01r\\Blob Containers. Under Blob Containers, receipts is selected. On the right, the ContosoSportsLeague-Store-Receipt-72.pdf is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image252.png "Azure Storage Explorer")

16. Double-click the PDF document to download and see the Purchase receipt.

17. Open the **ContosoLogicApplication** Logic Apps Designer. We will be adding another to the flow for updating the database. In the designer, select **+ New step**.

    ![In Designer, the New Step link is circled. Under New step, the Add an action tile is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image254.png "Designer")

18. Select the **All** tab, then choose **SQL Server**.

    ![In the Services section, under Services, SQL Server is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image255.png "Services section")

19. Select **Update row (V2)**.

    ![In the SQL Server section, on the Actions tab, SQL Server - Update row (V2) is selected.](media/2020-03-18-12-35-07.png "SQL Server section")

20. Enter the following values, then select **Create**:

    - Authentication Type: **SQL Server Authentication**

    - SQL server name: _Enter the DNS name of the SQL Database Failover Cluster Read/Write Listener Endpoint that was copied previously_.

    - SQL database name: `ContosoSportsDB`

    - Username: `demouser`

    - Password: `demo@pass123`

    ![The Update row section displays the previously defined settings.](media/2020-03-18-12-37-03.png "Update row")

21. Select the **Server name** and **Database name** previously specified, then from the drop-down select the name of the **Orders** table, and enter `OrderId` into the **Row id** field.

    ![In the Update row section, under Table name, Orders is selected.](media/2020-03-18-12-41-11.png "Update row section")

22. Press **Save**, then select the **Code View** button.

23. Add the following JSON within the `Update_row_(V2).inputs` object:

    ```json
    "body": {
        "OrderDate": "@{body('ContosoMakePDF')['OrderDate']}",
        "FirstName": "@{body('ContosoMakePDF')['FirstName']}",
        "LastName": "@{body('ContosoMakePDF')['LastName']}",
        "Address": "@{body('ContosoMakePDF')['Address']}",
        "City": "@{body('ContosoMakePDF')['City']}",
        "State": "@{body('ContosoMakePDF')['State']}",
        "PostalCode": "@{body('ContosoMakePDF')['PostalCode']}",
        "Country": "@{body('ContosoMakePDF')['Country']}",
        "Phone": "@{body('ContosoMakePDF')['Phone']}",
        "SMSOptIn": "@{body('ContosoMakePDF')['SMSOptIn']}",
        "SMSStatus": "@{body('ContosoMakePDF')['SMSStatus']}",
        "Email": "@{body('ContosoMakePDF')['Email']}",
        "ReceiptUrl": "@{body('ContosoMakePDF')['ReceiptUrl']}",
        "Total": "@{body('ContosoMakePDF')['Total']}",
        "PaymentTransactionId": "@{body('ContosoMakePDF')['PaymentTransactionId']}",
        "HasBeenShipped": "@{body('ContosoMakePDF')['HasBeenShipped']}"
    },
    ```

    After this has been added, the JSON will look as follows:

    ![JSON edits have been made.](media/2020-03-18-18-21-47.png "JSON edits have been made")

24. And modify the `path` variable for the `Update_row_(V2)` action to include the index key or OrderId as follows:

    ```json
    "path": "/v2/datasets/@{encodeURIComponent(encodeURIComponent('default'))},@{encodeURIComponent(encodeURIComponent('default'))}/tables/@{encodeURIComponent(encodeURIComponent('[dbo].[Orders]'))}/items/@{encodeURIComponent(encodeURIComponent(body('ContosoMakePDF')['OrderId']))}"
    ```

25. **Save** and return to the designer.

26. Your updated designer view should look like this:

    ![The Update row section displays the purchase fields.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image261.png "Update row section")

27. Select Run on the Logic App Designer, and then run the Contoso sports Web App and check out an Item.

28. Run the call center website app, and select the last Details link in the list.

    ![Screenshot of the Details link.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image264.png "Details link")

29. You should now see a Download receipt link because the database has been updated.

    ![In the Order Details window, the Download receipt link is circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image265.png "Order Details window")

30. Select the Download receipt link to see the receipt.

31. Return to the Logic app and you should see all green check marks for each step. If not, select the yellow status icon to find out details.

    ![In the Logic app, all steps have green checkmarks.](media/2020-03-18-19-05-39.png "Logic app")

### Task 4: Use Twilio to send SMS Order Notifications

<!-- omit in toc -->
#### Subtask 1: Configure your Twilio trial account

1. If you do not have a Twilio account, sign up for one for free at the following URL:

    [https://www.twilio.com/try-twilio](https://www.twilio.com/try-twilio)

   ![Screenshot of the Twilio account Sign up for free webpage.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image268.png "Twilio account Sign up webpage")

2. On the home dashboard, select **Get a Trial Number**.
   
   ![The Twilio dashboard is shown with the Get a Trial Number button highlighted.](media/twilio_gettrialnumberbutton.png "The Twilio Dashboard")

3. Record the **Phone Number**, select the **Choose this Number** button on the **Your first Twilio Phone Number** prompt, and select **Done**.

    ![On the Your first Twilio Phone Number prompt, the number is obscured.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image274.png "Your first Twilio Phone Number prompt")

4. Select **Home**, then **Settings**. Authenticate if needed and then record the **Account SID** and **Auth Token** for use when configuring the Twilio Connector.

    ![On the Console, on the left, the Home button and the Settings menu tab are selected. On the right, under API Credentials, Account SID and Auth Token are circled.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image275.png "Console")

<!-- omit in toc -->
#### Subtask 2: Create a new logic app

1. Open **SQL Server Management Studio** and connect to the SQL Database for the **ContosoSportsDB** database.

    >**Note**: You can find the database server name by:

    > - Navigate the Azure ContosoSportsDB in the portal.
    > - In the Overview, locate the **Show database connection strings** link.
    > - Copy the **Server** parameter value.
    e.g. Server=tcp:``contososqlserver2019th.database.windows.net,1433``

    ![In Object Explorer, ContosoSportsDBserver1234.database is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image276.png "Object Explorer")

2. Under the **ContosoSportsDB** database, expand **Programmability**, right-click on **Stored Procedures**, select **New**, followed by **Stored Procedure...**

    ![In Object Explorer, the following path is expanded: ContosoSportsDBserver1234.database\\Databases\\ContosoSportsDB\\Programmability\\Stored Procedures. From the right-click menu for the Stored Procedures, New / Stored Procedure is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image277.png "Object Explorer")

3. Replace the Stored Procedure Template code with the following:

    ```sql
    CREATE PROCEDURE [dbo].[GetUnprocessedOrders]
    AS
    declare @returnCode int 
    SELECT @returnCode = COUNT(*) FROM [dbo].[Orders] WHERE PaymentTransactionId is not null AND PaymentTransactionId <> '' AND Phone is not null AND Phone <> '' AND SMSOptIn = '1' AND SMSStatus is null
    return @returnCode

    GO
    ```

4. Select **Execute** in the toolbar, or press the F5 key.

    ![Screenshot of the Execute button.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image278.png "Execute button")

5. Delete the SQL script for the Stored Procedure from the code editor, and replace it with the following:

    ```sql
    CREATE PROCEDURE [dbo].[ProcessOrders]
    AS
    SELECT * FROM [dbo].[Orders] WHERE PaymentTransactionId is not null AND PaymentTransactionId <> '' AND Phone is not null AND Phone <> '' AND SMSOptIn = '1' AND SMSStatus is null;

    UPDATE [dbo].[Orders] SET SMSStatus = 'sent' WHERE PaymentTransactionId is not null AND PaymentTransactionId <> '' AND Phone is not null AND Phone <> '' AND SMSOptIn = '1' AND SMSStatus is null;
    ```

6. Select **Execute** in the toolbar, or press the F5 key.

    ![Screenshot of the Execute button.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image278.png "Execute button")

7. In the Azure Management Portal, select the **+ Create a resource** button, then search for and select **Logic App**. Then select **Create** on the overview screen.

8. On the **Logic app** form, assign a value for **Name**, and set the Resource Group to **contososports**, then select **Review + create**. Once validation has passed, select **Create**.

    ![In the Create logic app form, the Name field is set to contososportssms. Under Resource group, contososports is selected.](media/2020-03-19-11-31-05.png "Create logic app form")

9. Once deployed, open the new Logic App you just created. 

10. In the Logic Apps Designer, select the **Blank Logic App** Template.

    ![In the Logic Apps Designer, the Blank Logic App tile is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image282.png "Logic Apps Designer")

11. On the **Logic Apps Designer**, select the **All** tab, and choose **Schedule**. Then, select **Recurrence**.

    ![In the Logic Apps Designer, the Schedule tile is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image283.png "Logic Apps Designer")

12. Set the **FREQUENCY** to **MINUTE**, and **INTERVAL** to 1.

    ![Under Recurrence, the Frequency field is Minute, and the Interval field is 1.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image284.png "Recurrence section")

13. Select the **+ New Step** button.

14. Type **SQL Server** into the filter box, and select the **SQL Server -- Execute stored procedure (V2)** action.

    ![Under Choose an action, sql server is typed in the search field. On the Actions tab, SQL Server (Execute stored procedure V2) is selected.](media/2020-03-19-11-34-57.png "Choose an action section")

15. Select the **Server name**, **Database name**, and `'[dbo].[GetUnprocessedOrders]` **Procedure name** values.

    ![In the Execute stored procedure section, the Procedure name is \[dbo\].\[GetUnprocessedOrders\].](media/2020-03-19-11-37-08.png "Execute stored procedure section")

16. Select **New Step**, and search for and select the **Control** object.

    ![The Control object is highlighted on the logic app designer pick tool.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image289.png "Buttons")

17. Select **New Step**, and search for and select the **Control -> Condition** object.

    ![The Control Condition object is highlighted on the logic app designer pick tool.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image290b.png "Buttons")  

18. Select **Choose a value**, and then select **Return Code** from the Dynamic content tile.

    ![The Choose a value box and Return Code objects are highlighte in the Dynamic content tile in the Logic Designer.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image290c.png "Buttons")

19. Specify **ReturnCode**, set the RELATIONSHIP to **is greater than**, and set the VALUE to **0**.

    ![Under Condition, Object Name is ReturnCode, Relationship is greater than, and Value is 0.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image290.png "Condition section")

20. Select the **Add an action** link on the **If true** condition.

    ![Under If true, the Add an action button is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image291.png "If yes section")

21. Select **SQL Server**, and then select the **SQL Server -- Execute stored procedure (V2)** action.

    ![Under If Yes, SQL Server - Execute stored procedure is circled.](media/2020-03-19-11-39-54.png "If yes section")

22. Select the **ProcessOrders** stored procedure in the Procedure name dropdown.

    ![Under If Yes, Execute stored procedure 2 is selected, and the Procedure name is \[dbo\].\[ProcessOrders\].](media/2020-03-19-11-40-49.png "If yes section")

23. Select the **Add an action** link.

    ![The Add an action button is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image294.png "Add an action button")

24. Select the **All** tab, and search for **Twilio** in the filter box, and select the **Twilio -- Send Text Message (SMS)** item in the Actions box.

    ![In the Choose an operation tile, the Search box is set to Twilio, and below, Twilio - Send Text Message (SMS) is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image295.png "Choose an Operation Tile.")

25. Set the Connection Name to Twilio, specify your Twilio **Account SID** and **Authentication Token**, then select the **Create** button.

    ![In the Twilio - Send Text Message (SMS) section, fields are set to the previously defined settings.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image296.png "Twilio - Send Text Message (SMS)")

26. Using the drop-down, select your Twilio number for the **FROM PHONE NUMBER** field. Specify a place holder phone number in the **TO PHONE NUMBER**, and a **TEXT** message.

    ![Under Send Text Message (SMS), the From Phone Number and To Phone Number fields are circled, and in the Text field is the message, Hello, your order has shipped!](media/2020-03-19-11-43-06.png "Send Text Message (SMS)")

27. On the Logic App toolbar, select the **Code View** button.

    ![The code view button is selected on the Logic App toolbar.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image298.png "Logic App toolbar")

28. Find the **Send\_Text\_Message\_(SMS)** action, and modify the body property of the Twilio action:

    ![The Code view displays the text message, and the from and to phone numbers.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image299.png "Code view")

    Add the following code between Hello and the comma:

    ```json
    "@{item()['FirstName']}"
    ```

    ![The Code view now displays the added code in the text message.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image300.png "Code view")

29. Modify the **to** property to pull the phone number from the item.

    ```json
    "to": "@{item()['Phone']}"
    ```

    ![The to phone number code now displays the updated line of code.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image301.png "Code view")

30. Immediately before the **Send\_Text\_Message\_(SMS)** section, create a new line, and add the following code:

    ```json
        "forEach_email": {
        "type": "Foreach",
        "foreach": "@body('Execute_stored_procedure_(V2)_2')['ResultSets']['Table1']",
        "actions": {
    ```

31. Remove the **runAfter** block from the **Send\_Text\_Message\_(SMS)** action.

    ![The runAfter block of code displays.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image302.png "Code view")

32. Locate the closing bracket of the **Send\_Text\_Message\_(SMS)** action, create a new line after it (be **SURE** to place a leading comma after the closing bracket), and add the following code:

    ```json
        },
        "runAfter": {
            "Execute_stored_procedure_(V2)_2": [
                "Succeeded"
            ]
        }
    }
    ```

33. Select **Save** on the toolbar to enable the logic app.

    ![On the Logic Apps Designer toolbar, the Save button is selected.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image304.png "Logic Apps Designer toolbar")

34. After the code for the **Send\_Text\_Message\_(SMS)** has been modified to be contained within the **forEach\_email** action and you save it, it be like the following JSON with your Twilio phone number in the "from" field:

    ```json
    "forEach_email": {
        "type": "Foreach",
        "foreach": "@body('Execute_stored_procedure_(V2)_2')['ResultSets']['Table1']",
        "actions": {
            "Send_Text_Message_(SMS)": {
                "inputs": {
                    "body": {
                        "body": "Hello @{item()['FirstName']}, your order has shipped!",
                        "from": "+1XXXXXXXXXX",
                        "to": "@{item()['Phone']}"
                    },
                    "host": {
                        "connection": {
                            "name": "@parameters('$connections')['twilio']['connectionId']"
                        }
                    },
                    "method": "post",
                    "path": "/Messages.json"
                },
                "type": "ApiConnection"
            }
        },
        "runAfter": {
            "Execute_stored_procedure_(V2)_2": [
                "Succeeded"
            ]
        }
    }
    ```

35. Your workflow should look like the image below, and you should receive a text for each order you placed.

    ![The Workflow diagram begins with Recurrence, then flows to Execute stored procedure, then to Condition. The Condition fields are as follows: Object Name, ReturnCode; Relationship, is greater than; Value, 0. Below the Workflow diagram is an If Yes box, with a workflow that begins wtih Execute stored procedure 2, and flows to forEach email. There is also an If No, Do Nothing box.](images/Hands-onlabstep-by-step-Moderncloudappsimages/media/image305.png "Workflow diagram")

## Exercise 6: Automate deployments using GitHub actions

Duration: 30 minutes

The Contoso Sports League would like to move their existing source control to GitHub. In addition to this, they wish to implement automatic deployments of their projects into production. The desired workflow is that features are developed in their own branch and once complete, pull requests are issued to the master branch. The pull requests are then reviewed for quality assurance, and once approved, the pull request is then merged into the master branch of the repository. Upon this merge, the projects in the solution should be automatically released into the production Azure environment using the code from the master branch. In this exercise, you will learn how to deploy code to Azure from GitHub Actions in two different ways: via a Service Principal created in Active Directory, as well as via Application Service Publish Profiles.

### Task 1: Create a GitHub repository

1. Open a web browser, and navigate to <https://www.github.com>. Log in using your GitHub account credentials.

2. In the upper-right corner, expand the user drop down menu and select **Your repositories**.

    ![The user menu is expanded with the Your repositories item selected.](media/github_yourrepositoriesmenu.png "GitHub user menu")

3. Next to the search criteria, locate and select the **New** button.

    ![The GitHub Find a repository search criteria is shown with the New button selected.](media/github_newbutton.png "New repository button")

4. On the **Create a new repository** screen, name the repository **ContosoSports** and select the **Create repository** button.

    ![The Create a new repository screen is shown with the Repository name set to ContosoSports and the Create repository button is highlighted.](media/github_createrepositoryform.png "Create a new repository form")

5. On the **Quick setup** screen, copy the **HTTPS** GitHub URL for your new repository, paste this in notepad for future use.

    ![The Quick setup screen is displayed with the copy button next to the GitHub URL textbox selected.](media/github_copygithuburl.png "The quick setup screen")

### Task 2: Commit the existing lab files to source control

1. Open a command prompt and change directory to the folder that contains the lab files solution file (Contoso.Apps.SportsLeague.sln).

2. At the command prompt, issue the following command to initialize the git repository:

    ```shell
    git init
    ```

3. Set the remote origin to the GitHub Url from the previous task by executing the following command (replace the URL with your own):

   ```shell
   git remote add origin <your GitHub Url>
   ```

4. Commit the initial code, and push it to the master branch by issuing the following commands:

    ```shell
    git add -a
    git commit -m "initial commit"
    git push -u origin master
    ```

### Task 3: Create a service principal in Active Directory

One method to deploy code using GitHub actions is to create a Service Principal that has the necessary access to deploy the web applications in the solution. In this exercise, we will be releasing the Call Center Admin Portal application using this service principal. This service principal is created in Azure Active Directory, and is granted the Contributor role to the deployed lab resources, scoped by the resource group.

1. In the Azure portal, select the icon to open the Cloud Shell located on the top toolbar.

    ![A portion of the Azure Portal top toolbar is displayed with the Cloud Shell menu item highlighted.](media/azureportal_cloudshellmenuitem.png "The cloud shell taskbar item")

    > **Note**: You may be prompted to create a storage account to support cloud shell activities, this is required in order to utilize the cloud shell.

2. Obtain the Subscription ID and Resource Group name by opening the resource group where you have deployed all of the applications in this lab. The Subscription ID is available in the Overview pane.

3. In the Cloud Shell, execute the following to create the service principal scoped by the resource group we've been using in this lab (replace Subscription ID and resource group name):

    ```PowerShell
    az ad sp create-for-rbac --name 'mcw-modern-cloud-apps' --role contributor --scopes /subscriptions/<Subscription ID>/resourceGroups/<Resource Group Name> --sdk-auth
    ```

4. This will output a JSON data result, copy and paste this result and save it for a future step in this lab.

    ![The output of the previous command is displayed with the JSON result highlighted.](media/azurecloudshell_serviceprincipaljson.png "JSON output in the cloud shell")

### Task 4: Create repository secrets

You have the ability to add secrets to the repository in GitHub. Secrets contain sensitive information that should never be checked into source control. These secrets are kept encrypted by GitHub and are made available to GitHub actions through the **secrets** collection (which you will see in the next task). We will be creating many secrets, as we have five projects that we are configuring for auto-deployment.

<!-- omit in toc -->
#### Subtask 1: Create the service principal credentials secret

1. In GitHub, return to the **ContosoSports** repository screen and select the **Settings** tab.

2. From the left menu, select **Secrets**.

3. Select the **New secret** button.

   ![The Settings tab of the ContosoSports repository is shown with the Secrets menu item and the New secret button highlighted.](media/github_newsecretbutton.png "GitHub repository settings")

4. In the New secret form, enter the name **AZURE_CREDENTIALS**, and for the value, paste in the JSON data obtained when creating the Service Principal in the previous task. Select **Add secret**.

<!-- omit in toc -->
#### Subtask 2: Create the e-commerce web application publish profile secret

1. In the Azure Portal, open the e-commerce web application service, it is the one named contosoapp{randomcharacters}.

2. From the top toolbar of the App Service screen, select **Get publish profile** item. This will download a file. Open this file in a text editor.

    ![On the App service screen, the Get publish profile button is highlighted on the toolbar menu.](media/azureportal_appservice_getpublishprofile.png "Get Publish profile")

3. Return to the ContosoSports repository GitHub Secrets screen, and add a new secret named **AZURE_WEBAPP_PUBLISH_PROFILE**, for the value, paste the contents of the publish profile from the previous step, then select the **Add secret** button.

<!-- omit in toc -->
#### Subtask 3: Create publish profile secrets for the remaining projects

Repeat Subtask 2 for the remaining projects by obtaining the publish profiles from the Azure Portal. Create the secrets as follows:

| Secret Name | Value |
|-------------|--------------------------|
| AZURE_API_PAYMENT_PUBLISH_PROFILE | Contents of the publish profile for the Payments API |
| AZURE_API_OFFERS_PUBLISH_PROFILE | Contents of the publish profile for the Offers API |
| AZURE_FUNCTIONAPP_PUBLISH_PROFILE | Contents of the publish profile for the Receipt Function Application |

![The GitHub repository secrets screen is displayed with a table containing all the secrets added in this lab.](media/github_secretslisting.png "GitHub repository secrets")

### Task 5: Define the production deployment workflow

1. In the web browser, return to the ContosoSports repository on GitHub, and select the **Actions** tab.

    ![On the ContosoSports repository screen, the Actions tab is selected.](media/github_actionstab.png "Repository Actions")

2. Beneath the **Get started with GitHub Actions** heading, select the **set up a workflow yourself** link.

3. Above the editor, name the workflow **productiondeployment.yml**. Remove all code in the file editor.

    ![The Actions workflow editor is displayed with an empty code listing with the name productiondeployment.yml highlighted.](media/github_actions_namedandempty.png "The Actions workflow editor")

4. Copy and paste the following workflow to the text editor. The code is documented inline.

    ```yml
    name: Contoso Sports Production Deployment

    # This workflow is triggered on push to the master branch of the repository
    on:
    push:
        branches:
        - master

    # Environment variables are defined so that they can be used throughout the job definitions.
    # Be sure to replace the tokens in the AZURE_*_NAME variables with the names of the resources in Azure
    env:  
    AZURE_WEBAPP_NAME: '<E-Commerce Web Application Name - named similar to contosoapp{random characters}>'
    AZURE_WEBAPP_PROJECT_NAME: 'Contoso.Apps.SportsLeague.Web'  
    AZURE_WEBAPP_PUBLISH_PROFILE: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}

    AZURE_ADMINAPP_NAME: '<The name of the Call Center admin App Service in Azure>'
    AZURE_ADMINAPP_PROJECT_NAME: 'Contoso.Apps.SportsLeague.Admin'

    AZURE_API_PAYMENT_NAME: '<The name of the Payments API App Service in Azure>'
    AZURE_API_PAYMENT_PROJECT_NAME: 'Contoso.Apps.PaymentGateway'
    AZURE_API_PAYMENT_PUBLISH_PROFILE: ${{ secrets.AZURE_API_PAYMENT_PUBLISH_PROFILE }}

    AZURE_API_OFFERS_NAME: '<The name of the Offers API App Service in Azure>'
    AZURE_API_OFFERS_PROJECT_NAME: 'Contoso.Apps.SportsLeague.Offers'
    AZURE_API_OFFERS_PUBLISH_PROFILE: ${{ secrets.AZURE_API_OFFERS_PUBLISH_PROFILE }}

    AZURE_FUNCTIONAPP_NAME: '<The name of the Function App in Azure>'
    AZURE_FUNCTIONAPP_PROJECT_NAME: 'Contoso.Apps.FunctionApp'
    AZURE_FUNCTIONAPP_PUBLISH_PROFILE: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE }}

    DOTNET_VERSION: '3.1.102'

    # Jobs define the actions that take place when code is pushed to the master branch
    jobs:

    # Build and deploy the E-Commerce Web Application using the Publish Profile
    build-and-deploy-webapp:
        runs-on: ubuntu-latest
        steps:
        # Checkout the repo
        - uses: actions/checkout@master

        # Setup .NET Core SDK
        - name: Setup .NET Core
            uses: actions/setup-dotnet@v1
            with:
            dotnet-version: ${{ env.DOTNET_VERSION }}

        # Run dotnet build and publish on the project
        - name: dotnet build web portal and publish
            run: |
            dotnet build ${{ env.AZURE_WEBAPP_PROJECT_NAME }} --configuration Release
            dotnet publish ${{ env.AZURE_WEBAPP_PROJECT_NAME }} -c Release -o './webdeploy'

        # Deploy to Azure Application Service
        - name: 'Deploy public web portal'
            uses: azure/webapps-deploy@v2
            with:
            app-name: ${{ env.AZURE_WEBAPP_NAME }}
            publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
            package: './webdeploy'

    # Build and deploy the Call Center admin using the Service Principal credentials
    build-and-deploy-admin:
        runs-on: ubuntu-latest
        steps:
        # Checkout the repo
        - uses: actions/checkout@master

        # Setup .NET Core SDK
        - name: Setup .NET Core
            uses: actions/setup-dotnet@v1
            with:
            dotnet-version: ${{ env.DOTNET_VERSION }}

        # Run dotnet build and publish
        - name: dotnet build web portal and publish on the project
            run: |
            dotnet build ${{ env.AZURE_ADMINAPP_PROJECT_NAME }} --configuration Release
            dotnet publish ${{ env.AZURE_ADMINAPP_PROJECT_NAME }} -c Release -o './admindeploy'

        # Login to Azure
        - name: Login via Az module
            uses: azure/login@v1.1
            with:
            creds: ${{ secrets.AZURE_CREDENTIALS }}

        # Deploy to Azure Application Service
        - name: 'Deploy admin web portal'
            uses: azure/webapps-deploy@v2
            with:
            app-name: ${{ env.AZURE_ADMINAPP_NAME }}
            credentials: ${{ secrets.AZURE_CREDENTIALS }}
            package: './admindeploy'

        ##Azure logout
        - name: logout
            run: |
            az logout

    # Build and deploy the Payments API using the Publish Profile
    build-and-deploy-payment-api:
        runs-on: ubuntu-latest
        steps:
        # Checkout the repo
        - uses: actions/checkout@master

        # Setup .NET Core SDK
        - name: Setup .NET Core
            uses: actions/setup-dotnet@v1
            with:
            dotnet-version: ${{ env.DOTNET_VERSION }}

        # Run dotnet build and publish on the project
        - name: dotnet build web portal and publish
            run: |
            dotnet build ${{ env.AZURE_API_PAYMENT_PROJECT_NAME }} --configuration Release
            dotnet publish ${{ env.AZURE_API_PAYMENT_PROJECT_NAME }} -c Release -o './paymentapideploy'

        # Deploy to Azure App Service 
        - name: 'Deploy payments API'
            uses: azure/webapps-deploy@v2
            with:
            app-name: ${{ env.AZURE_API_PAYMENT_NAME }}
            publish-profile: ${{ env.AZURE_API_PAYMENT_PUBLISH_PROFILE }}
            package: './paymentapideploy'

    # Build and deploy the Offer API using the Publish Profile
    build-and-deploy-offer-api:
        runs-on: ubuntu-latest
        steps:
        # Checkout the repo
        - uses: actions/checkout@master

        # Setup .NET Core SDK
        - name: Setup .NET Core
            uses: actions/setup-dotnet@v1
            with:
            dotnet-version: ${{ env.DOTNET_VERSION }}

        # Run dotnet build and publish on the project
        - name: dotnet build web portal and publish
            run: |
            dotnet build ${{ env.AZURE_API_OFFERS_PROJECT_NAME }} --configuration Release
            dotnet publish ${{ env.AZURE_API_OFFERS_PROJECT_NAME }} -c Release -o './offerapideploy'

        # Deploy to Azure App Service
        - name: 'Deploy offers API'
            uses: azure/webapps-deploy@v2
            with:
            app-name: ${{ env.AZURE_API_OFFERS_NAME }}
            publish-profile: ${{ env.AZURE_API_OFFERS_PUBLISH_PROFILE }}
            package: './offerapideploy'

    # Build and deploy the PDF receipt generation function app using the publish profile
    build-and-deploy-pdffunctionapp:
        runs-on: ubuntu-latest
        steps:
        # Checkout the repo
        - uses: actions/checkout@master

        # Setup .NET Core SDK
        - name: Setup .NET Core
            uses: actions/setup-dotnet@v1
            with:
            dotnet-version: ${{ env.DOTNET_VERSION }}

        # Run dotnet build and publish on the project
        - name: dotnet build web portal and publish
            run: |
            dotnet build ${{ env.AZURE_FUNCTIONAPP_PROJECT_NAME  }} --configuration Release
            dotnet publish ${{ env.AZURE_FUNCTIONAPP_PROJECT_NAME  }} -c Release -o './pdfappdeploy'

        - name: 'Deploy to Azure Function App service'
            uses: Azure/functions-action@v1
            with:
            app-name: ${{ env.AZURE_FUNCTIONAPP_NAME }}
            package: './pdfappdeploy'
            publish-profile: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE }}
    ```

    >**Note**: Due to the nature of some browsers, you may need to adjust the whitespace of the yml document after it has been pasted into GitHub.

5. Select the **Start commit** button to commit the workflow to the repository.

6. Enter a commit title and comment, and select **Commit new file**.

    ![The Commit new file dialog is shown with the title and description populated.](media/github_commitworkflowform.png "Commit new file dialog")

7. Committing this file is a push to the master branch. This means that the workflow that we just created is triggered. Select the **Actions** tab to view the currently running/historical record of workflow executions.

    ![The workflow we just defined is triggered and is displayed on the Actions tab.](media/github_workflowsstatus.png "GitHub repository Actions tab")

8. You are able to drill into each workflow, and each job executed by the workflow. Furthermore, as you drill into the job, you are able to see the output of each step contained in the job by expanding the section in the console runner window.

    ![The workflow is currently running, the workflow run displays the current status each job.](media/github_runningworkflowsteps.png "Running workflow")

    ![A completed workflow job console is shown with one of the steps expanded so that the output of the step is displayed.](media/github_jobstepexpanded.png "Completed workflow")

### Task 6: Trigger the Production Deployment Workflow

In this task, we will be making a modification to the e-commerce web application in a branch and issuing a pull request to the master branch. We will manually merge the pull request into the master branch to trigger the production deployment workflow.

1. Open a command prompt, and change directory to where the Visual Studio solution file is found.

2. Execute the following commands to create a branch for this modification. Keep this command window open.

    ```shell
    git pull
    git branch textchange
    git checkout textchange
    ```

3. In Visual Studio, expand the e-commerce website project (Web/Contoso.Apps.SportsLeague.Web), and edit and save the **Views/Home/Index.cshtml** file.

    ![The code listing for Views/Home/Index.cshtml is shown with some modified text highlighted.](media/visualstudio_edithomeindex.png "Visual Studio file editor")

4. Return to the command window, and execute the following commands to commit the text change to the branch.

    ```shell
    git commit -am "Changed some text"
    git push --set-upstream origin textchange
    ```

5. In a web browser, return to the ContosoSports source code repository.

6. Above the file listing table, you should see a notification that **textchange had recent pushes**. Select the **Compare &amp; pull request** button.

    ![The textchange had recent pushes notification is shown with the Compare and pull request button highlighted.](media/github_compareandpullrequest.png "Recent push notification")

7. On the **Open a pull request** form, feel free to write a comment, and select the **Create pull request** button.

8. You should now see a message indicating that there are no conflicts with the base branch.

    ![A message indicating there are no conflicts is shown.](media/github_pullrequest_noconflicts.png "No conflicts on the branch")

9. Select the **Actions** tab of the repository to verify that the deployment workflow has not been triggered by the recent file commits on the textchange branch.

10. Return to the pull request that was just created, by selecting the **Pull requests** tab, and selecting the pull request in the list.

11. Select the **Merge pull request** button on the pull request, then select **Confirm merge**.

12. Return to the **Actions** tab, and you should see that the workflow has been triggered (merging pushes new code to the branch, thus the production workflow is triggered).

    ![The workflows list is displayed with an in progress workflow that has been triggered by the merge of the pull request.](media/github_mergeworkflowtriggered.png "Workflow in progress")

13. Once the deployment workflow has completed. Navigate to the E-commerce web application and ensure the changes you made are visible.

    ![A portion of the e-commerce website is shown with the textual change highlighted.](media/ecommerce_textchangevisible.png "Screenshot demonstrating the text change")

## After the hands-on lab

Duration: 10 minutes

### Task 1: Delete resources

1. Since the HOL is now complete, go ahead and delete all the Resource Groups that were created for this HOL. You will no longer need those resources and it will be beneficial to clean up your Azure Subscription.

2. In GitHub, open the ContosoSports repository and select **Settings**. Scroll to the bottom of the screen, and select the **Delete this repository** button in the **Danger Zone** section.

You should follow all steps provided *after* attending the hands-on lab.
