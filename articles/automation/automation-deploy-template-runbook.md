---
title: "bir Azure Otomasyonu runbook'u Azure Resource Manager şablonunda aaaDeploy | Microsoft Docs"
description: "Bir runbook'tan nasıl toodeploy bir Azure Resource Manager şablonu Azure depolama alanına depolanır"
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
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="c8b45-104">Bir Azure Otomasyonu PowerShell runbook'taki bir Azure Resource Manager şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8b45-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="c8b45-105">Yazma bir [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) kullanarak bir Azure kaynağı dağıtan bir [Azure kaynak yönetimi şablon](../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="c8b45-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="c8b45-106">Bunu yaparak, Azure kaynaklarını dağıtımını otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b45-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="c8b45-107">Resource Manager şablonlarınızı Azure depolama gibi Merkezi, güvenli bir konumda saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b45-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="c8b45-108">Bu konuda, depolanan bir Resource Manager şablonu kullanan bir PowerShell runbook oluşturuyoruz [Azure Storage](../storage/common/storage-introduction.md) toodeploy yeni bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="c8b45-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) toodeploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8b45-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c8b45-109">Prerequisites</span></span>

<span data-ttu-id="c8b45-110">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c8b45-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c8b45-111">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="c8b45-111">Azure subscription.</span></span> <span data-ttu-id="c8b45-112">Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c8b45-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="c8b45-113">[Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="c8b45-113">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="c8b45-114">Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.</span><span class="sxs-lookup"><span data-stu-id="c8b45-114">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="c8b45-115">[Azure depolama hesabı](../storage/common/storage-create-storage-account.md) hangi toostore hello Resource Manager şablonunda</span><span class="sxs-lookup"><span data-stu-id="c8b45-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which toostore hello Resource Manager template</span></span>
* <span data-ttu-id="c8b45-116">Azure Powershell yerel makine üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="c8b45-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="c8b45-117">Bkz [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) hakkında bilgi için Azure PowerShell tooget.</span><span class="sxs-lookup"><span data-stu-id="c8b45-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-resource-manager-template"></a><span data-ttu-id="c8b45-118">Merhaba Resource Manager şablonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8b45-118">Create hello Resource Manager template</span></span>

<span data-ttu-id="c8b45-119">Bu örnekte, yeni bir Azure depolama hesabı dağıtan bir Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8b45-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="c8b45-120">Bir metin düzenleyicisinde metin aşağıdaki hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="c8b45-120">In a text editor, copy hello following text:</span></span>

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

<span data-ttu-id="c8b45-121">Merhaba dosyası yerel olarak kaydedin `TemplateTest.json`.</span><span class="sxs-lookup"><span data-stu-id="c8b45-121">Save hello file locally as `TemplateTest.json`.</span></span>

## <a name="save-hello-resource-manager-template-in-azure-storage"></a><span data-ttu-id="c8b45-122">Azure depolama alanında Hello Resource Manager şablonunu Kaydet</span><span class="sxs-lookup"><span data-stu-id="c8b45-122">Save hello Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="c8b45-123">PowerShell toocreate bir Azure depolama dosya paylaşımı kullanın ve hello karşıya artık `TemplateTest.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="c8b45-123">Now we use PowerShell toocreate an Azure Storage file share and upload hello `TemplateTest.json` file.</span></span>
<span data-ttu-id="c8b45-124">Nasıl toocreate bir dosya paylaşımı ve hello Azure portalında bir dosyayı karşıya yükleme hakkında yönergeler için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="c8b45-124">For instructions on how toocreate a file share and upload a file in hello Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="c8b45-125">Yerel makinenizde PowerShell'i başlatın ve aşağıdaki komutları toocreate bir dosya paylaşımı hello çalıştırın ve hello Resource Manager şablonu toothat dosya paylaşımı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c8b45-125">Launch PowerShell on your local machine, and run hello following commands toocreate a file share and upload hello Resource Manager template toothat file share.</span></span>

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a><span data-ttu-id="c8b45-126">Merhaba PowerShell runbook komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8b45-126">Create hello PowerShell runbook script</span></span>

<span data-ttu-id="c8b45-127">Merhaba alır bir PowerShell Betiği oluşturuyoruz artık `TemplateTest.json` dosyası Azure depolama biriminden ve hello şablonu toocreate yeni bir Azure depolama hesabı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c8b45-127">Now we create a PowerShell script that gets hello `TemplateTest.json` file from Azure Storage and deploys hello template toocreate a new Azure Storage account.</span></span>

<span data-ttu-id="c8b45-128">Bir metin düzenleyicisinde metin aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8b45-128">In a text editor, paste hello following text:</span></span>

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



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="c8b45-129">Merhaba dosyası yerel olarak kaydedin `DeployTemplate.ps1`.</span><span class="sxs-lookup"><span data-stu-id="c8b45-129">Save hello file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a><span data-ttu-id="c8b45-130">İçeri aktarma ve Azure Automation hesabınızda hello runbook yayımlama</span><span class="sxs-lookup"><span data-stu-id="c8b45-130">Import and publish hello runbook into your Azure Automation account</span></span>

<span data-ttu-id="c8b45-131">Şimdi biz PowerShell tooimport hello runbook'un Azure Otomasyon hesabınızda kullanın ve sonra hello runbook yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="c8b45-131">Now we use PowerShell tooimport hello runbook into your Azure Automation account, and then publish hello runbook.</span></span>
<span data-ttu-id="c8b45-132">Hakkında bilgi için tooimport ve bir runbook yayımlama hello Azure portal, bkz: [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="c8b45-132">For information about how tooimport and publish a runbook in hello Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="c8b45-133">tooimport `DeployTemplate.ps1` Otomasyon hesabınızda bir PowerShell runbook olarak hello aşağıdaki PowerShell komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8b45-133">tooimport `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run hello following PowerShell commands:</span></span>

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a><span data-ttu-id="c8b45-134">Merhaba runbook başlatın</span><span class="sxs-lookup"><span data-stu-id="c8b45-134">Start hello runbook</span></span>

<span data-ttu-id="c8b45-135">Biz hello runbook tarafından arama hello Başlat artık [başlangıç AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c8b45-135">Now we start hello runbook by calling hello [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="c8b45-136">Toostart hello Azure portal, bir runbook'ta nasıl görürüm hakkında bilgi için [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="c8b45-136">For information about how toostart a runbook in hello Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="c8b45-137">Komutları hello PowerShell konsolunda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8b45-137">Run hello following commands in hello PowerShell console:</span></span>

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="c8b45-138">Merhaba runbook çalıştırıldığında ve çalıştırarak durumunu denetleyebilirsiniz `$job.Status`.</span><span class="sxs-lookup"><span data-stu-id="c8b45-138">hello runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="c8b45-139">Merhaba runbook hello Resource Manager şablonunu alır ve toodeploy yeni bir Azure depolama hesabı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8b45-139">hello runbook gets hello Resource Manager template and uses it toodeploy a new Azure Storage account.</span></span>
<span data-ttu-id="c8b45-140">Merhaba yeni depolama hesabı hello aşağıdaki komutu çalıştırarak oluşturulduğunu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c8b45-140">You can see that hello new storage account was created by running hello following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="c8b45-141">Özet</span><span class="sxs-lookup"><span data-stu-id="c8b45-141">Summary</span></span>

<span data-ttu-id="c8b45-142">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="c8b45-142">That's it!</span></span> <span data-ttu-id="c8b45-143">Artık tüm Azure kaynaklarınızı Azure Otomasyonu ve Azure Storage ve Resource Manager şablonları toodeploy kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b45-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates toodeploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8b45-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8b45-144">Next steps</span></span>

* <span data-ttu-id="c8b45-145">Resource Manager şablonları hakkında daha fazla toolearn bakın [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c8b45-145">toolearn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="c8b45-146">Azure Storage'ı kullanmaya tooget bkz [giriş tooAzure depolama](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8b45-146">tooget started with Azure Storage, see [Introduction tooAzure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="c8b45-147">toofind yararlı diğer Azure Otomasyon çalışma kitabı bkz [Azure Otomasyonu Runbook ve modül galerileri](automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="c8b45-147">toofind other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="c8b45-148">toofind diğer yararlı Resource Manager şablonları görmek [Azure hızlı başlangıç şablonları](https://azure.microsoft.com/resources/templates/)</span><span class="sxs-lookup"><span data-stu-id="c8b45-148">toofind other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

