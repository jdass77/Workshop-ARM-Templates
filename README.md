# Using Azure Resource Manager Templates to supercharge your Azure Deployments

Whether you’re a Developer building applications or an IT Pro building virtual data centres in
Azure, at some point you're going to want to use modern Configuration Management practices to
build those services. Azure Resource Manager Templates are the powerful declarative Infrastructure
as Code system that is baked in to Azure. In this session we'll take a look at what Azure Resource
Manager templates are, how to create and edit them and what tricks, tips and tools are available
to you to help you become a Configuration Management master in Azure.

_This workshop was originally created for the Global Azure Bootcamp 2019, but it may be used for
other training sessions or events. It is provided free and under [MIT license](LICENSE)._

**Daniel Scott-Raynsford**

![MVP](/images/MVP_Logo_Horizontal_Preferred_Cyan300_CMYK_72ppi.png)

[Microsoft Cloud and Datacenter MVP](https://mvp.microsoft.com/en-us/PublicProfile/5002340?fullName=Daniel%20%20Scott-Raynsford) | [@dscottraynsford](https://twitter.com/dscottraynsford) | [Linked-In](https://www.linkedin.com/in/dscottraynsford/) | [Email](mailto:dscottraynsford@outlook.com) | [GitHub](https://www.github.com/PlagueHO)

## Content

- [Prerequisite Knowledge](#prerequisite-knowledge)
- [What You Will Need](#what-you-will-need)
- [What You Will Learn](#what-you-will-learn)
- [Prerequisite Knowledge](#prerequisite-knowledge)
- [Section 1 - Getting Setup](#section-1---getting-setup)
- [Part 1.1 - Setting up Cloud Shell](#part-1.1---setting-up-cloud-shell) - 5 min
- [Part 1.2 - Configure Visual Studio Code](#part-1.2---configure-visual-studio-code) - 5 min
- [Part 1.3 - Register Providers required for Lab](#part-1.3---register-providers-required-for-lab) - 5 min
- [Section 2 - Creating an ARM Template](#section-2---creating-an-arm-template)
- [Part 2.1 - Create Resources in the Portal](#part-2.1---create-resources-in-the-portal)
- [Part 2.2 - Export an ARM Template](#part-2.2---export-an-arm-template)
- [Section 5 - Cleanup After the Workshop](#section-5---cleanup-after-the-workshop)
- [Part 5.1 - Remove Resources and Resource Groups](#part-5.1---remove-resources-and-resource-groups) - 2 min

Estimated workshop time: 75 min
Estimated Azure credit usage: USD 1.00 (as long as you delete the infrastructure straight after completion of the workshop)

## What You Will Need

To complete this workshop you'll need the following:

- A **Microsoft Azure Account**:
  - If you are running this as part of the Global Azure Bootcamp, you will
    have access to a free Azure Pass.
  - You can sign up for a free trial [here](https://azure.microsoft.com/en-us/free/).
- A computer running **Windows**, **OSX** or **Linux** (desktop OS) with
  an **up-to-date version** of either Chrome, Firefox, Edge or Opera.
- **Visual Studio Code**: An extremely powerfull, free open-source editor
  for Windows, Mac and Linux.
  Click [here](https://code.visualstudio.com/) to download it.

## Prerequisite Knowledge

- Basic knowledge of web application hosting on Windows or Linux
- Basic knowledge of text editors (Visual Studio Code)
- Basic knowledge of using text based consoles (PowerShell, Cmd or Bash)

## What You Will Learn

You'll learn the basics in the following skills:

- Create and use the Azure Cloud Shell.
- How to set up Visual Studio Code to edit ARM templates.
- Run some simple PowerShell commands in Cloud Shell.
- What an Azure Resource Manager (ARM) template is and what it is used for.
- How to create basic ARM templates
- How to deploy ARM templates
- How to use Visual Studio Code to edit ARM templates.

## Section 1 - Getting Setup

In this section we'll set up _Azure Cloud Shell_ and _Visual Studio Code_,
so that we're all set to create and deploy ARM templates right from our
desktop.

### Part 1.1 - Setting up Cloud Shell

> Estimated Completion Time: 5 min

Azure Cloud Shell is an interactive, browser-accessible shell for managing
Azure resources. It provides the flexibility of choosing the shell experience
that best suits the way you work. Cloud Shell offers both PowerShell and Bash
console experience and you can flip between them at the touch of a switch.

_Sidenote: the PowerShell experience is actually PowerShell Core running on top
of Bash in a Linux container!_

**In this lab we'll be using the PowerShell experience using the Az PowerShell
modules, but if you're experienced using Bash and the AzCLI, then feel free
to flick across.**

1. Open Cloud Shell by clicking the Cloud Shell icon:
   ![Open Cloud Shell](images/opencloudshell.png "Open Cloud Shell")

> If you have **not** previously used Azure Cloud Shell:

_When you first create a Cloud Shell a storage account will get created
for you to store your settings, scripts and other files you might create.
This enables you to have access to your own environment no matter what
device you're using.
You can customize the storage account settings if you wish, but in this
lab we'll just be using the defaults._

![Create Cloud Shell Storage](images/cloudshellcreatestorage.png "Create Cloud Shell Storage")

1. Select the **subscription** to create the Storage Account in and click
   **Create storage**.

1. The Storage Account will be created and the Cloud Shell will be started:

   ![Cloud Shell Started](images/cloudshellstarted.png "Cloud Shell Started")

> Once your Azure Cloud Shell storage has been set up or if you had previous set up Azure Cloud Shell:

1. Select **PowerShell** from the shell drop down:

   ![Select PowerShell Cloud Shell](images/cloudshellselectpowershell.png "Select PowerShell Cloud Shell")

### Part 1.2 - Configure Visual Studio Code

> Estimated Completion Time: 5 min

In this part we will configure Visual Studio Code with the following
extensions:

- [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account):
  The Azure Account extension provides a single Azure sign-in and subscription filtering experience for all other Azure extensions. It makes Azure's Cloud Shell service available in VS Code's integrated terminal.
- [Azure Resource Manager Tools](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools):
  This extension provides language support for Azure Resource Manager deployment templates and template language expressions.

We will then be configuring Visual Studio Code to be able to connect
to our Azure Cloud Shell.

1. Start Visual Studio Code.
1. Click Extensions.

   ![Visual Studio Code Extensions](images/vscodeextensions.png "Visual Studio Code Extensions")

1. Search for the `Azure Account` extension and click **Install**.

   ![Visual Studio Code Azure Account Extension](images/vscodeextensionazureaccount.png "Visual Studio Code Azure Account Extension")

1. Search for the `Azure Resource Manager Tools` extension and click `Install`.

   ![Visual Studio Code Azure Resource Manager Tools Extension](images/vscodeextensionazureresourcemanagertools.png "Visual Studio Code Azure Resource Manager Tools Extension")

1. Press <kbd>F1</kbd> to bring up the Visual Studio command search.
1. Enter `Cloud Shell` in the command search.
1. Click the **Azure: Open PowerShell in Cloud Shell** command.

   ![Visual Studio Code Cloud Shell Command](images/vscodesearchcloudshellcommand.png "Visual Studio Code Cloud Shell Command")

1. A terminal will open in the Visual Studio Code window requiring you
   to log in to Azure.

   ![Visual Studio Code Cloud Shell Sign In](images/vscodecloudshellsignin.png "Visual Studio Code Cloud Shell Sign In")

1. Click Sign In.
1. A browser window will open where you will be asked to sign into your
   Azure account.
1. Sign into the Azure account you created the Cloud Shell in during
   _Step 1.1_.
1. Return to your Visual Studio Code window where you will now have a
   Cloud Shell console ready to accept commands:

   ![Visual Studio Code Cloud Shell Started](images/vscodecloudshellstarted.png "Visual Studio Code Cloud Shell Started")

This console is exactly the same as the Cloud Shell you get in the
[Azure Portal](https://portal.azure.com) or in [shell.azure.com](https://shell.azure.com).

### Part 1.3 - Register Providers required for Lab

> Estimated Completion Time: 5 min

Depending on your type of subscription (Free, Azure Pass etc.) you may have to register the required resource providers.
This is because by default many resource providers (types of resource providers) are not registered by default.

1. Launch a **Cloud Shell** in Visual Studio Code, in the
   [Azure Portal](https://portal.azure.com) or using:

   [![Launch Cloud Shell](https://shell.azure.com/images/launchcloudshell.png "Launch Cloud Shell")](https://shell.azure.com)

1. Depending on your type of subscription (Free, Azure Pass etc.) you may
   have to register the required resource providers. This is because by
   default many resource providers (types of resource providers) are not
   registered by default.

   This only needs to be done once for a subscription. To do this, run
   the following commands in Cloud Shell:

   ```powershell
      Register-AzResourceProvider -ProviderNamespace 'Microsoft.Network'
      Register-AzResourceProvider -ProviderNamespace 'Microsoft.Compute'
      Register-AzResourceProvider -ProviderNamespace 'Microsoft.Storage'
      Register-AzResourceProvider -ProviderNamespace 'Microsoft.Web'
      Register-AzResourceProvider -ProviderNamespace 'Microsoft.SQL'
   ```

   ![Register Providers](images/registerproviders.png "Register Providers")

Your Azure Account and Visual Studio Code is set up to be able to work
with Azure Resource Manager (ARM) Templates more effectively.

**These tools are very useful throughout Azure and should be part of
any Azure professionals toolbox.**

## Section 2 - Creating an ARM Template

In this section we'll create some resources using the [Azure Portal](https://portal.azure.com)
and then export them as a new ARM Template.

### Part 2.1 - Create Resources in the Portal

Create a simple Azure App Service and App Service plan within a
Resource Group to host a simple web application.

> Estimated Completion Time: 5 min

1. Open the [Azure Portal](https://portal.azure.com)
1. Click `Create a Resource`:

   ![Create a Resource](images/portalcreatearesource.png "Create a Resource")

1. Select `Web` under Azure Marketplace and click `Web App`:

   ![Create a Web App](images/portalcreatewebapp.png "Create a Web App")

1. Set an **App name** to one that will be **Globally Unique**. For example
   `dsrgab19-dev`.
1. Select `Create new` under **Resource Group** and enter the same name
   as the **App Name** but append '-rg'. For example `dsrgab19-dev-rg`.
1. Set **OS** to `Windows`.
1. Set **Publish** to `Docker Image`.

   ![Create a Web App Settings](images/portalcreatewebappsettings.png "Create a Web App Settings")

1. Click `Configure Container`.
1. Select `Single Container (Preview)`.
1. Select `Private Registry`.
1. Set **Server URL** to `https://mcr.microsoft.com`.
1. Set **Image and Optional Tag** to `mcr.microsoft.com/dotnet/core/samples:aspnetapp`.

   ![Create a Web App Container](images/portalcreatewebappcontainer.png "Create a Web App Container")

1. Click `Apply`.
1. Click `Create`.

Your _App Service_ hosting a Windows Server Container will be deployed.
It will take a few minutes for the service to be provisioned.
Once it has been provisioned you can check the _App Service_ is serving
by opening your _App Service_ and clicking the `URL`.

   ![Test Web App](images/portaltestwebapp.png "Test Web App")

We'll leave this up to you to determine the best way to locate your
_App Service_.

Note: If you get this error, just wait a minute and try again:

   ![Web App Starting Up](images/webappstartingup.png "Web App Starting Up")

You should see this page when the App Service has started up:

   ![Web App Started Up](images/webappstartedup.png "Web App Started Up")

### Part 2.2 - Export an ARM Template

> Estimated Completion Time: 5 min

## Section 5 - Cleanup After the Workshop

### Part 5.1 - Remove Resources and Resource Groups

> Estimated Completion Time: 25 min

This step is optional and only needs to be done if you're finished with
workshop resources and want to get rid of them to save some Azure credit.

![Congratulations](images/congratulations.png "Congratulations")

**Well done!**
You have taken your first steps into the amazingly powerful world of
Containers, Kubernetes and Azure Kubernetes Service. This technology is
increadibly powerful and can allow your applications to run virtually
anywhere and they will always run the same way.

Thank you!
