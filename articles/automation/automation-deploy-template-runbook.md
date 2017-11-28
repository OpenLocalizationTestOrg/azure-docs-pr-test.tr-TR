---
title: "Bir Azure Otomasyonu runbook'u içinde bir Azure Resource Manager şablonu dağıtma | Microsoft Docs"
description: "Bir runbook'tan Azure Storage'da depolanan bir Azure Resource Manager şablonu dağıtma"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell runbook, json, azure Otomasyonu
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="07f5c-104">Bir Azure Otomasyonu PowerShell runbook'taki bir Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="07f5c-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="07f5c-105">Yazma bir [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) kullanarak bir Azure kaynağı dağıtan bir [Azure kaynak yönetimi şablon](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="07f5c-106">Bunu yaparak, Azure kaynaklarını dağıtımını otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f5c-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="07f5c-107">Resource Manager şablonlarınızı Azure depolama gibi Merkezi, güvenli bir konumda saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f5c-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="07f5c-108">Bu konuda, depolanan bir Resource Manager şablonu kullanan bir PowerShell runbook oluşturuyoruz [Azure Storage](../storage/common/storage-introduction.md) yeni bir Azure depolama hesabı dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="07f5c-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07f5c-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="07f5c-109">Prerequisites</span></span>

<span data-ttu-id="07f5c-110">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="07f5c-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="07f5c-111">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="07f5c-111">Azure subscription.</span></span> <span data-ttu-id="07f5c-112">Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="07f5c-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="07f5c-113">Runbook’u tutacak ve Azure kaynaklarında kimlik doğrulamasını yapacak bir [Automation hesabı](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="07f5c-114">Bu hesabın sanal makineyi başlatma ve durdurma izni olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="07f5c-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="07f5c-115">[Azure depolama hesabı](../storage/common/storage-create-storage-account.md) Resource Manager şablonu depolanacağı</span><span class="sxs-lookup"><span data-stu-id="07f5c-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="07f5c-116">Azure Powershell yerel makine üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="07f5c-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="07f5c-117">Bkz: [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) Azure PowerShell alma hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="07f5c-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="07f5c-118">Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="07f5c-118">Create the Resource Manager template</span></span>

<span data-ttu-id="07f5c-119">Bu örnekte, yeni bir Azure depolama hesabı dağıtan bir Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="07f5c-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="07f5c-120">Bir metin Düzenleyicisi'nde, aşağıdaki metni kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="07f5c-120">In a text editor, copy the following text:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

<span data-ttu-id="07f5c-121">Dosyayı yerel olarak kaydedin `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="07f5c-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="07f5c-122">Azure depolama alanında Resource Manager şablonunu Kaydet</span><span class="sxs-lookup"><span data-stu-id="07f5c-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="07f5c-123">Bir Azure depolama dosya paylaşımı oluşturmak ve karşıya yüklemek için PowerShell kullanırız artık `TemplateTest.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="07f5c-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="07f5c-124">Bir dosyasının nasıl oluşturulacağı hakkında yönergeler paylaşma ve Azure portalında bir dosyayı karşıya yüklemek için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="07f5c-125">Yerel makinenizde PowerShell'i başlatın ve bir dosya paylaşımı oluşturmak ve bu dosya paylaşımı Resource Manager şablonunu karşıya yüklemek için aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="07f5c-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="07f5c-126">PowerShell runbook komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="07f5c-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="07f5c-127">Biz alır bir PowerShell betiği oluşturmak artık `TemplateTest.json` dosyası Azure depolama biriminden ve yeni bir Azure depolama hesabı oluşturmak için şablon dağıtır.</span><span class="sxs-lookup"><span data-stu-id="07f5c-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="07f5c-128">Bir metin Düzenleyicisi'nde aşağıdaki metni yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="07f5c-128">In a text editor, paste the following text:</span></span>

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="07f5c-129">Dosyayı yerel olarak kaydedin `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="07f5c-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="07f5c-130">Alma ve runbook'un Azure Otomasyon hesabınızda yayımlama</span><span class="sxs-lookup"><span data-stu-id="07f5c-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="07f5c-131">Şimdi biz runbook'un Azure Otomasyon hesabınızda içeri aktarmak için PowerShell kullanın ve ardından runbook yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="07f5c-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="07f5c-132">İçeri aktarma ve Azure portalında bir runbook yayımlama hakkında daha fazla bilgi için bkz: [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="07f5c-133">İçeri aktarmak için `DeployTemplate.ps1` Otomasyon hesabınızda bir PowerShell runbook olarak, aşağıdaki PowerShell komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="07f5c-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="07f5c-134">Runbook'u Başlat</span><span class="sxs-lookup"><span data-stu-id="07f5c-134">Start the runbook</span></span>

<span data-ttu-id="07f5c-135">Biz arayarak runbook'u Başlat artık [başlangıç AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="07f5c-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="07f5c-136">Azure portalında bir runbook'u başlatma hakkında daha fazla bilgi için bkz: [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="07f5c-137">PowerShell konsolunda aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="07f5c-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="07f5c-138">Runbook çalıştığında, ve çalıştırarak durumunu denetleyebilirsiniz `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="07f5c-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="07f5c-139">Runbook Resource Manager şablonunu alır ve yeni bir Azure depolama hesabı dağıtmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="07f5c-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="07f5c-140">Yeni depolama hesabı aşağıdaki komutu çalıştırarak oluşturulduğunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="07f5c-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="07f5c-141">Özet</span><span class="sxs-lookup"><span data-stu-id="07f5c-141">Summary</span></span>

<span data-ttu-id="07f5c-142">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="07f5c-142">That's it!</span></span> <span data-ttu-id="07f5c-143">Şimdi, Azure kaynaklarınızı dağıtmak için Azure Otomasyonu ve Azure Storage ve Resource Manager şablonları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f5c-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07f5c-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07f5c-144">Next steps</span></span>

* <span data-ttu-id="07f5c-145">Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="07f5c-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="07f5c-146">Azure Storage ile çalışmaya başlamak için bkz: [Azure Storage'a giriş](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="07f5c-147">Diğer kullanışlı Azure Otomasyon çalışma kitabı bulmak için bkz: [Azure Otomasyonu Runbook ve modül galerileri](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="07f5c-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="07f5c-148">Diğer kullanışlı Resource Manager şablonları bulmak için bkz: [Azure hızlı başlangıç şablonları](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="07f5c-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

