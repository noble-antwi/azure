# MANAGE AZURE RESOURCES BY USING AZURE RESOURCE MANAGER TEMPLATES

## Introduction
In this project, we aim to automate and simplify resource deployments in Azure using Azure Resource Manager (ARM) templates. By leveraging ARM templates, we can define the infrastructure and configuration of Azure resources in a declarative manner, enabling consistent and repeatable deployments while reducing administrative overhead and minimizing human errors.

## Project Overview
The project will cover the following key aspects:

1. Creating an Azure Resource Manager template.
2. Editing and redeploying an Azure Resource Manager template.
3. Configuring Azure Cloud Shell and deploying a template with Azure PowerShell.
4. Deploying a template with the Azure CLI.

## Crafting an Azure Resource Manager Template
![]()
![Initial Page](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/00_Disk_Creation_Page.png>)

Initiating my journey, I delved into the Azure portal, configuring a managed disk with precise specifications. With an eye on future deployments, I exported the template, laying the groundwork for automated resource provisioning.


### Creating a Managed Disk
resource Group: Created a new Resu=ource Group by name Working_with_Templates
Availability zone :	No infrastructure redundancy required
Disk Name: temp_disk
Size 32: GiB
Disk tier: S4
Provisioned IOPS: 500
Provisioned throughput: 60

Under Encryption Tab, we selected Platfomr-managed key for Key managment and all other options were left in the default state.

I then clicked on Review and Create to Create the  Disk

![Review Creation Page](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/001_Review_Create_Disk.png>)

![Disk Creation](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/002_DiskCreationComplete.png>)

After the resource has been created, Under the Automation Blade, I clicked on Export Template which provides a template based on which more Disks can be created at a faster pace..
The template was downlaoded which came as a zip folder containting two JSON files namely parameters.json and template.json

## Tailoring and Re-deploying an Azure Resource Manager Template
After the above precedure, I would like to redeploy another Disk making use of the template downloaded earlier hence i searched for Deploy a Custom Template in the Azure Portal

I clicked on Build your own template in the editor  option instead of making use of Quickstart template.
![Template](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/003_TemplateFIle.png>)
![json file](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/004_DownloadedJSONFiles.png>)



On the Edit template blade, click Load file and upload the template.json file you downloaded to the local disk.
Within the editor pane, I cahnged the "defaultValue" from  "temp_disk" to "temp_disk2" and changed the  "name": "[parameters('disks_temp_disk_name')]", from [parameters('disks_temp_disk_name')]  to [parameters('temp_disk2')]

After changing the values, i clicked on save to now select the paramenters.json file as can be seen here.

Select Edit parameters, click Load file and upload the parameters.json.Had the oppotunity to upload the file and then pick the parameters file to edit. I mde changes to match the template name.

In the Settings section, click Deployments.
Note: All deployments details are documented in the resource group. It is a good practice to review the first few template-based deployments to ensure success prior to using the templates for large-scale operations.


![Custom Deployment](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/005CustomDeploymentInterface.png>)

![upload Json template](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/006_Uploadoftemplatejsonfile.png>)

![Changing Parameters](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/008_ParameterChange.png>)

![Changing Parameters 2](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/009_ParameterValueChanged.png>)

![Deployment Complete](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/010_CustomDeploymnetSetupComplete.png>)

![Disk Createe Successfully](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/011_DiskCreatedSuccessfully.png>)

![Confirmed Disk Created](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/012_TwoDIsksCreate.png>)
![Checking Deployment](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/013_DeploymmentSuccess.png>)

## Harnessing Azure Cloud Shell and PowerShell

Guided by a commitment to harness cutting-edge tools, I embraced Azure Cloud Shell and PowerShell, configuring storage settings and seamlessly deploying templates. With each command executed, I marveled at the transformative potential of automation in resource management.
![Through CloudShell](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/014_TheTwoFilesAvailableinCloudShell.png>)

Command used in creating the Disk is 
```
PS /home/noble> New-AzResourceGroupDeployment -ResourceGroupName Working_With_Templates -TemplateFile template.json -TemplateParameterFile parameters.json
```

![Template FIle in Shell](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/015_TemplateFIleInSellShowign.png>)

I confirmed the Disk was created by running the command 
``` Get-AzDisk ```

![Created Successfully](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/016-template_createdOnCloudShell.png>)

## Deploying Templates with the Azure CLI
![Change to Bash](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/017_Powershelltobacsh.png>)
In the final leg of my journey, I navigated the Azure Cloud Shell, adeptly switching to Bash and leveraging the Azure CLI to deploy templates swiftly. With each deployment confirmed, I savored the realization of my vision for streamlined resource provisioning.
![Listing Contents](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/018_ListingContens.png>)
In the cloud shell, i changed from Powershell to Bash with the command ```ls``` lisitng the contents
Select the Editor (curly brackets) icon and navigate to the template JSON file.
after which changes were made to the file in order to create a new Disk,

The bash deployment command is 
```
az deployment group create --resource-group Working_With_Templates --template-file template.json --parameters parameters.json 
```



![Making Changes to Template File in CLI](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/019_MakingCanagestoTheFile.png>)

![Change](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/019_MakingCanagestoTheFile.png>)

![Run Deployment](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/020_DeploymentinBashComplete.png>)

For confirmation of disk creation, i run the command 

```
az disk list --output table 
```
![Listing All Disks](<../media/Lab 03 Manage Azure resources by using Azure Resource Manager Templates/021_diskCreatedwithBashCompleteUponCheck.png>)


## Conclusion
My journey culminated in a profound appreciation for the power of automation in Azure resource management. Through meticulous crafting of ARM templates and adept utilization of tools like Azure Cloud Shell and PowerShell, I achieved newfound efficiency, enabling my team to focus on innovation and growth. This project not only transformed our approach to resource deployments but also fueled my passion for continuous improvement and mastery in Azure technologies.









## Edit an Azure Resource Manager template and then redeploy the template












## Deploy a template with the CLI

