# Tutorial: Hello Windows Azure #

Test Changeset 

In the next 5 minutes we will build, debug, and deploy a simple “Hello World” ASP.NET Application using Windows Azure. I want to show you a simple demo, so you can get a feel for the concepts and steps involved with building a Windows Azure application using the Windows Azure SDK and Visual Studio Tools. In later demos you will see how we can build more complex applications that utilize additional roles, the Windows Azure APIs, and Windows Azure Storage services as well as additional services of Azure Services. 

<a id="goals" />
### Goals ###
In this tutorial you will see three things:

1. First you will see how the Windows Azure SDK and Visual Studio Tools for Windows Azure provide development tools that enable a rich and familiar development experience for cloud applications
2. Second you will see how Windows Azure abstracts you from the underlying infrascture and uses simple models to define the roles and number of instances for your application.  
3. Finally, you will see how to deploy, start, and manage a Windows Azure application through the Management portal.

<a name="technologies" />
### Key Technologies ###

* .NET Framework 4.0
* Visual Studio 2010
* Windows Azure SDK and Windows Azure Tools for Microsoft Visual Studio 2010

<a name="setup" />
### Setup and Configuration ###

Make sure you have installed all the prerequisites for this demo including the Windows Azure SDK.   

>*In order to run through the complete tutorial, you must have network connectivity. Additionally, you must have a Windows Azure developer account. You can sign up for a free trial here: http://bit.ly/WindowsAzureFreeTrial.* 

<a name="segments" />
### Tutorial Segments ###

This demo is composed of the following segments:

1. Creating a Hello Windows Azure application.
2. Deploying to Windows Azure.

<a name="tutorial" />
## Tutorial ##

<a name="segment1" />
### Creating a Hello Windows Azure Application ###

Let's start by launching Visual Studio 2010. In Visual Studio select **File -> New Project** and in **Installed Templates** select the **Cloud** category inside the **Visual C#** node.

![Windows Azure Project template](https://github.com/microsoft-dpe/Tutorial-HelloWindowsAzure/raw/master/images/Image1.png)

You'll see there s a template called **Windows Azure Project**. This template launches a wizard that allows us to select the type of role to use within our project.

>*Make sure to open Visual Studio as an administrator. Right-click and choose Run As Administrator.*

Name your new project **HelloAzure** and rename the **WebRole1** to **HelloAzure_WebRole**. Visual Studio will now creat a new solution that contains two project. The first project name **HelloAzure_WebRole** is a standard ASP.NET Web Application project with a few additional resources added. The second project is a new Windows Azure Project that references our ASP.NET project. It also contains configuration files that define the model for our Windows Azure solution.

![HelloAzure solution](http://wadewegner.blob.core.windows.net/tutorialdemo/Image2.png)

Before we take a look at these configuration files let's build our HelloAzure web page.

Open the default web page and add an ASP.NET label control. Adjust the font size on the label to **XX-Large**.

![Adding an ASP.NET label](http://wadewegner.blob.core.windows.net/tutorialdemo/Image3.png)

Right-click the design surface and select **View Code** from the context menu to view the **Default.aspx.cs** code behind file. Add code the **Page_Load** event to set the text for the label.

![Update the code behind file](http://wadewegner.blob.core.windows.net/tutorialdemo/Image4.png)

Before you run the application take a look at the model that defines the Windows Azure application. Open the **ServiceConfiguration.Local.cscfg** file in the **HelloAzure** project. This configuration file defines the roles for your Windows Azure project. As you can see, it also defines the number of instances per role. Change the number of instances from 1 to 2.

![Increase role instance count to 2](http://wadewegner.blob.core.windows.net/tutorialdemo/Image5.png)

Start the application in debug model by selecting **Debug -> Start Debugging** or press the **F5** button. This will package the application and deploy to the local compute emulator. After the application starts you will see our simple ASP.NET web application and the text **Hello Windows Azure**.

![Running the Web application in the compute emulator](http://wadewegner.blob.core.windows.net/tutorialdemo/Image6.png)

Debugging the Web application causes the ASP.NET project to compile into a .NET assembly just as normal; however, since we are running the Windows Azure project, the ASP.NET application is also packaged up and deployed to the local compute emulator.

To see the details of the running application you can look at the compute emulator UI. Right-click the **Azure** icon in the task bar and select **Show Compute Emulator UI**. Expand the **HelloAzure** application in the compute emulator and expand the **Hello_WebRole**.

![Show the compute emulator UI](http://wadewegner.blob.core.windows.net/tutorialdemo/Image7.png)

![See the two running instances](http://wadewegner.blob.core.windows.net/tutorialdemo/Image8.png)

A good analogy is to think of the compute emulator as providing a Cassini-like environment for Windows Azure. This gives you a local simulated environment for developing and testing Windows Azure applications on your machine.

Switch back to Visual Studio and set a breakpoint on the label text.

![Set a breakpoint](http://wadewegner.blob.core.windows.net/tutorialdemo/Image9.png)

Now, refresh the page. Notice that you can drop into Visual Studio to debug your project and step through lines of code - just as you normally do with ASP.NET applications.

![Debug your running application](http://wadewegner.blob.core.windows.net/tutorialdemo/Image10.png)

Press **F5** to continue the execution of the application. You can stop the application by closing the browser.

<a name="segment2" />
### Deploying to Windows Azure ###

Now that you've seen how you can build and debug a simple web application with Windows Azure and Visual Studio it's time to deploy your HelloAzure application to the cloud.

In Visual Studio right-click on the **HelloAzure** project and select **Package** from the context menu.

![Package the solution](http://wadewegner.blob.core.windows.net/tutorialdemo/Image11.png)

Choose the **Cloud** service configuration file and click **Package**. This will compile and build the solution. It will also create a new service package (which is essentially a zip file) containing the assemblies and configuration files for the solution.

![Choose the Cloud service configuration](http://wadewegner.blob.core.windows.net/tutorialdemo/Image12.png)

Once the package process is complete Visual Studio will open the directory where the service package was created. Copy the path of this file.

![CSPKG and CSCFG files](http://wadewegner.blob.core.windows.net/tutorialdemo/Image13.png)

You will now deploy the Windows Azure package using the Windows Azure management portal. Open a brwoser and navigate to http://windows.azure.com/. Login using your Live ID.

> If you don't have a Windows Azure account ... TBD

![Log into the Windows Azure management portal](http://wadewegner.blob.core.windows.net/tutorialdemo/Image14.png)

Open in the management portal select the type of project you want to create. In this case you want to deploy an application to run in Windows Azure - click on the **New Hosted Service** button from the **Common Tasks** ribbon.

![Create a New Hosted Service](http://wadewegner.blob.core.windows.net/tutorialdemo/Image15.png)

You need to select the subscription from which to create the hosted service. Enter the hosted service name (i.e. **HelloAzure**) and enter the URL prefix (i.e. **helloazure**). The URL prefix has to be unique - if the prefix you choose is taken then choose another. For this tutorial choose **Anywhere US** for the deployment - in practice you can choose a specific geography for you application or specifc an affinity group.

![Specify the settings for the hosted service](http://wadewegner.blob.core.windows.net/tutorialdemo/Image16.png)

Leave the deployment options at the default to let our service deploy to the staging environment and start after the deployment. Give the deployment a name (i.e. **v1.0**) and select the package and the configuration files location. Use the **Browse Locally** button and browse for the **HelloAzure.cskpg** file generated by Visual Studio. You also need to specify the ServiceConfiguration file that defines the roles and number of instances per role. Use the **Browse Locally** button and browse for the **ServiceConfiguration.cscfg** file generated by Visual Studio. For this sample you do not need to add a certificate for your application so you can click **OK** to create and deploy the hosted service.

![Specify the CSPKG and CSCFG files and deploy](http://wadewegner.blob.core.windows.net/tutorialdemo/Image17.png)

Wait a few minutes for the package to upload. Once uploaded the web role will start to initialize. Windows Azure will spin up virtual machines for each of the role instances. Once the instances are started your application - the assemblies, ASPX pages, and so forth, that were uploaded in the CSPKG file - are deployed and running in IIS within each of the instances.

![Instances spinning up](http://wadewegner.blob.core.windows.net/tutorialdemo/Image18.png)

One the application is running in staging you can access it using the temporary Website URL generated. Select the node with the deployment name. By selecting the deployment in the items list you can see its properties in the right pane. Click on the **DNS name** link to navigate to your **HelloAzure** application.

![Run the application by clicking the staging DNS name](http://wadewegner.blob.core.windows.net/tutorialdemo/Image19.png)

You can see that your Hello Windows Azure application is now running in Windows Azure and publicly exposed on the web!

![Running in Windows Azure](http://wadewegner.blob.core.windows.net/tutorialdemo/Image20.png)

Let's move this application into the production slot. Go back to the managament portal. Click the **Swap VIP** button in the Deployments ribbon. You will be prompted to confirm that you want to switch to the production environment. Press the **OK** button when prompted. While the VIP swap occurs quickly it can take the portal a little bit to update.

![Perform a VIP Swap](http://wadewegner.blob.core.windows.net/tutorialdemo/Image21.png)

![Confirm the VIP Swap](http://wadewegner.blob.core.windows.net/tutorialdemo/Image22.png)

Once the VIP swap completes you can now browse to yur application running in production. Select the node with the deployment name and click the **DNS name** on the properties pane.

![Running in production](http://wadewegner.blob.core.windows.net/tutorialdemo/Image23.png)

You can now confirm that your Hello Azure application is running in production! Notice that the URL is the same sub-domain on cloudapp.net that was specified when creating the project in the management portal.

<a name="summary" />
## Summary ##

In this demo, you saw how we could easily build and debug web applications using the familiar ASP.NET programming model, Visual Studio, the Windows Azure SDK. You also saw how we could use the Windows Azure Management Portal to create projects, deploy applications, and manage the staging and production environments. Finally, in less than 5 minutes we created and ran a new application in the cloud.

What you did not see is the entire infrastructure Windows Azure provided. For example, we did not worry about physical machines, rack space, network switches or connectivity. We also did not have to remote into machines and physically copy files across machines. Windows Azure abstracted us from the underlying infrastructure and provided the automated deployment, isolation, redundancy, and load balancing for our application. This was intentionally a simple demo to help you understand the concepts. In later demos, you will see how we can build more complex applications that utilize additional roles, the Windows Azure APIs, and Windows Azure Storage services. 

