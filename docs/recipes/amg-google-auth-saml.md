# Configure Google Workspaces authentication on AMG using SAML v2.0

In this guide, we will walk through how you can setup Google Workspaces as an Identity provider for Amazon Managed Grafana (AMG) using SAML v2.0 protocol. In order to follow this guide you need to create a paid [Google Workspaces](https://workspace.google.com/) account in addition to having an [AMG workspace](https://docs.aws.amazon.com/grafana/latest/userguide/getting-started-with-AMG.html#AMG-getting-started-workspace) created.

### Create AMG Workspace

Login to the AMG console and click **Create workspace.** In the following screen, provide a workspace name as shown below. Click **Next**

![Create Workspace - Specify workspace details](../images/amg-saml-google-auth/1.png)

In the **Configure settings** page, select **Security Assertion Markup Language (SAML)** option so you can configure a SAML based Identity Provider for users to login.

![Create Workspace - Configure settings](../images/amg-saml-google-auth/2.png)

Select the data sources you want to choose and click **Next**
![Create Workspace - Permission settings](../images/amg-saml-google-auth/3.png)
Click on **Create workspace** button in the **Review and create** screen. 
![Create Workspace - Review settings](../images/amg-saml-google-auth/4.png)

This will create a new AMG workspace as shown below.
![Create Workspace - Create AMG workspace](../images/amg-saml-google-auth/5.png)
### Configure Google Workspaces to integrate with AMG

Login to Google Workspaces with Super Admin permissions and go to **Web and mobile apps** under **Apps** section. Now click on **Add App** and select **Add custom SAML app.** Now give the app a name as shown below. Click **CONTINUE.**

![Google Workspace - Add custom SAML app - App details](../images/amg-saml-google-auth/6.png)


On the next screen, click on **DOWNLOAD METADATA** button to download the SAML metadata file. Click **CONTINUE.**

![Google Workspace - Add custom SAML app - Download Metadata](../images/amg-saml-google-auth/7.png)

On the next screen, you will see the ACS URL, Entity ID and Start URL fields. You can get the values for these fields from the AMG console. 

Select **EMAIL** from the drop down in the **Name ID format** field and select **Basic Information > Primary email** in the **Name ID** field.

Click **CONTINUE.**
![Google Workspace - Add custom SAML app - Service provider details](../images/amg-saml-google-auth/8.png)

![AMG - SAML Configuration details](../images/amg-saml-google-auth/9.png)

In the **Attribute mapping** screen, make the mapping between **Google Directory attributes** and **App attributes** as shown in the screenshot below

![Google Workspace - Add custom SAML app - Attribute mapping](../images/amg-saml-google-auth/10.png)

For users logging in through Google authentication to have **Admin** privileges in **AMG,** set the **Department** field’s value as ***monitoring*.** You can choose any field and any value for this. Whatever you choose to use on the Google Workspaces side, make sure you make the mapping on AMG SAML settings to reflect that.

### Upload SAML Metadata into AMG

 Now on the AMG console, click **Upload or copy/paste** option and select **Choose file** button to upload the SAML metadata file downloaded from Google Workspaces earlier. 

In the **Assertion mapping** section, type in **Department** in the **Assertion attribute role** field and **monitoring** in the **Admin role values** field. This will allow users logging in with **Department** as **monitoring** to have **Admin** privileges in Grafana so they can perform administrator duties such as creating Dashboards, datasources and such.

Set values under **Additional settings - optional** section as shown in the screenshot below. Click on **Save SAML configuration.** 

![AMG SAML - Assertion mapping](../images/amg-saml-google-auth/11.png)

Now AMG is setup to authenticate users using Google Workspaces. When users login, they will be redirected to the Google login page as shown below

![Google Workspace - Google sign in](../images/amg-saml-google-auth/12.png)

After entering their credentials, they will be logged into Grafana as shown in the screenshot below.
![AMG - Grafana user settings page](../images/amg-saml-google-auth/13.png)

As you can see, the user was able to successfully login to Grafana using Google Workspaces authentication.
