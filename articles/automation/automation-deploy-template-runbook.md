---
title: "Bir Azure Otomasyonu runbook'u içinde bir Azure Resource Manager şablonu dağıtma | Microsoft Docs"
description: "Bir runbook'tan Azure Storage'da depolanan bir Azure Resource Manager şablonu dağıtma"
services: automation
documentationcenter: dev-center-name
author: georgewallace
manager: carmonm
keywords: PowerShell runbook, json, azure Otomasyonu
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: gwallace
ms.openlocfilehash: 63c8f1b1190e19e1f1d2a7871bffee44ef5c7877
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/03/2018
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Azure Otomasyonu PowerShell runbook’unda Azure Resource Manager şablonu dağıtma

Yazma bir [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) kullanarak bir Azure kaynağı dağıtan bir [Azure kaynak yönetimi şablon](../azure-resource-manager/resource-manager-create-first-template.md).

Bunu yaparak, Azure kaynaklarını dağıtımını otomatik hale getirebilirsiniz. Resource Manager şablonlarınızı Azure depolama gibi Merkezi, güvenli bir konumda saklayabilirsiniz.

Bu konuda, depolanan bir Resource Manager şablonu kullanan bir PowerShell runbook oluşturuyoruz [Azure Storage](../storage/common/storage-introduction.md) yeni bir Azure depolama hesabı dağıtmak için.

## <a name="prerequisites"></a>Önkoşullar

Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:

* Azure aboneliği. Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* Runbook’u tutacak ve Azure kaynaklarında kimlik doğrulamasını yapacak bir [Automation hesabı](automation-sec-configure-azure-runas-account.md).  Bu hesabın sanal makineyi başlatma ve durdurma izni olmalıdır.
* [Azure depolama hesabı](../storage/common/storage-create-storage-account.md) Resource Manager şablonu depolanacağı
* Azure Powershell yerel makine üzerinde yüklü. Bkz: [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) Azure PowerShell alma hakkında bilgi için.

## <a name="create-the-resource-manager-template"></a>Resource Manager şablonu oluşturma

Bu örnekte, yeni bir Azure depolama hesabı dağıtan bir Resource Manager şablonunu kullanın.

Bir metin Düzenleyicisi'nde, aşağıdaki metni kopyalayın:

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

Dosyayı yerel olarak kaydedin `TemplateTest.json`.

## <a name="save-the-resource-manager-template-in-azure-storage"></a>Azure depolama alanında Resource Manager şablonunu Kaydet

Bir Azure depolama dosya paylaşımı oluşturmak ve karşıya yüklemek için PowerShell kullanırız artık `TemplateTest.json` dosya.
Bir dosyasının nasıl oluşturulacağı hakkında yönergeler paylaşma ve Azure portalında bir dosyayı karşıya yüklemek için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage/files/storage-dotnet-how-to-use-files.md).

Yerel makinenizde PowerShell'i başlatın ve bir dosya paylaşımı oluşturmak ve bu dosya paylaşımı Resource Manager şablonunu karşıya yüklemek için aşağıdaki komutları çalıştırın.

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

## <a name="create-the-powershell-runbook-script"></a>PowerShell runbook komut dosyası oluşturma

Biz alır bir PowerShell betiği oluşturmak artık `TemplateTest.json` dosyası Azure depolama biriminden ve yeni bir Azure depolama hesabı oluşturmak için şablon dağıtır.

Bir metin Düzenleyicisi'nde aşağıdaki metni yapıştırın:

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
$Context = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

Dosyayı yerel olarak kaydedin `DeployTemplate.ps1`.

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a>Alma ve runbook'un Azure Otomasyon hesabınızda yayımlama

Şimdi biz runbook'un Azure Otomasyon hesabınızda içeri aktarmak için PowerShell kullanın ve ardından runbook yayımlayın.
İçeri aktarma ve Azure portalında bir runbook yayımlama hakkında daha fazla bilgi için bkz: [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md).

İçeri aktarmak için `DeployTemplate.ps1` Otomasyon hesabınızda bir PowerShell runbook olarak, aşağıdaki PowerShell komutlarını çalıştırın:

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
Import-AzureRmAutomationRunbook @importParams

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a>Runbook'u Başlat

Biz arayarak runbook'u Başlat artık [başlangıç AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet'i.

Azure portalında bir runbook'u başlatma hakkında daha fazla bilgi için bkz: [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md).

PowerShell konsolunda aşağıdaki komutları çalıştırın:

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

Runbook çalıştığında, ve çalıştırarak durumunu denetleyebilirsiniz `$job.Status`.

Runbook Resource Manager şablonunu alır ve yeni bir Azure depolama hesabı dağıtmak için kullanır.
Yeni depolama hesabı aşağıdaki komutu çalıştırarak oluşturulduğunu görebilirsiniz:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Özet

İşte bu kadar! Şimdi, Azure kaynaklarınızı dağıtmak için Azure Otomasyonu ve Azure Storage ve Resource Manager şablonları kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* Resource Manager şablonları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md)
* Azure Storage ile çalışmaya başlamak için bkz: [Azure Storage'a giriş](../storage/common/storage-introduction.md).
* Diğer kullanışlı Azure Otomasyon çalışma kitabı bulmak için bkz: [Azure Otomasyonu Runbook ve modül galerileri](automation-runbook-gallery.md).
* Diğer kullanışlı Resource Manager şablonları bulmak için bkz: [Azure hızlı başlangıç şablonları](https://azure.microsoft.com/resources/templates/)

