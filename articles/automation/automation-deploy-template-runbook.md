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
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Bir Azure Otomasyonu PowerShell runbook'taki bir Azure Resource Manager şablonu dağıtma

Yazma bir [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) kullanarak bir Azure kaynağı dağıtan bir [Azure kaynak yönetimi şablon](../azure-resource-manager/resource-manager-create-first-template.md).

Bunu yaparak, Azure kaynaklarını dağıtımını otomatik hale getirebilirsiniz. Resource Manager şablonlarınızı Azure depolama gibi Merkezi, güvenli bir konumda saklayabilirsiniz.

Bu konuda, depolanan bir Resource Manager şablonu kullanan bir PowerShell runbook oluşturuyoruz [Azure Storage](../storage/common/storage-introduction.md) toodeploy yeni bir Azure depolama hesabı.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Azure aboneliği. Henüz bir aboneliğiniz yoksa [MSDN abone avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ya da <a href="/pricing/free-account/" target="_blank">[ücretsiz hesap için kaydolabilirsiniz](https://azure.microsoft.com/free/).
* [Otomasyon hesabı](automation-sec-configure-azure-runas-account.md) toohold runbook hello ve tooAzure kaynakları kimlik doğrulaması.  Bu hesap, izin toostart sahip ve hello sanal makineyi durdurun.
* [Azure depolama hesabı](../storage/common/storage-create-storage-account.md) hangi toostore hello Resource Manager şablonunda
* Azure Powershell yerel makine üzerinde yüklü. Bkz [yükleyin ve Azure Powershell yapılandırma](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) hakkında bilgi için Azure PowerShell tooget.

## <a name="create-hello-resource-manager-template"></a>Merhaba Resource Manager şablonu oluşturma

Bu örnekte, yeni bir Azure depolama hesabı dağıtan bir Resource Manager şablonunu kullanın.

Bir metin düzenleyicisinde metin aşağıdaki hello kopyalayın:

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

Merhaba dosyası yerel olarak kaydedin `TemplateTest.json`.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Azure depolama alanında Hello Resource Manager şablonunu Kaydet

PowerShell toocreate bir Azure depolama dosya paylaşımı kullanın ve hello karşıya artık `TemplateTest.json` dosya.
Nasıl toocreate bir dosya paylaşımı ve hello Azure portalında bir dosyayı karşıya yükleme hakkında yönergeler için bkz: [Windows Azure File storage ile çalışmaya başlama](../storage/files/storage-dotnet-how-to-use-files.md).

Yerel makinenizde PowerShell'i başlatın ve aşağıdaki komutları toocreate bir dosya paylaşımı hello çalıştırın ve hello Resource Manager şablonu toothat dosya paylaşımı yükleyin.

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

## <a name="create-hello-powershell-runbook-script"></a>Merhaba PowerShell runbook komut dosyası oluşturma

Merhaba alır bir PowerShell Betiği oluşturuyoruz artık `TemplateTest.json` dosyası Azure depolama biriminden ve hello şablonu toocreate yeni bir Azure depolama hesabı dağıtır.

Bir metin düzenleyicisinde metin aşağıdaki hello yapıştırın:

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

Merhaba dosyası yerel olarak kaydedin `DeployTemplate.ps1`.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>İçeri aktarma ve Azure Automation hesabınızda hello runbook yayımlama

Şimdi biz PowerShell tooimport hello runbook'un Azure Otomasyon hesabınızda kullanın ve sonra hello runbook yayımlayın.
Hakkında bilgi için tooimport ve bir runbook yayımlama hello Azure portal, bkz: [oluşturma veya bir Azure Otomasyonu runbook'u içeri aktarma](automation-creating-importing-runbook.md).

tooimport `DeployTemplate.ps1` Otomasyon hesabınızda bir PowerShell runbook olarak hello aşağıdaki PowerShell komutlarını çalıştırın:

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

## <a name="start-hello-runbook"></a>Merhaba runbook başlatın

Biz hello runbook tarafından arama hello Başlat artık [başlangıç AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet'i.

Toostart hello Azure portal, bir runbook'ta nasıl görürüm hakkında bilgi için [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md).

Komutları hello PowerShell konsolunda aşağıdaki hello çalıştırın:

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

Merhaba runbook çalıştırıldığında ve çalıştırarak durumunu denetleyebilirsiniz `$job.Status`.

Merhaba runbook hello Resource Manager şablonunu alır ve toodeploy yeni bir Azure depolama hesabı kullanır.
Merhaba yeni depolama hesabı hello aşağıdaki komutu çalıştırarak oluşturulduğunu görebilirsiniz:
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>Özet

İşte bu kadar! Artık tüm Azure kaynaklarınızı Azure Otomasyonu ve Azure Storage ve Resource Manager şablonları toodeploy kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

* Resource Manager şablonları hakkında daha fazla toolearn bakın [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md)
* Azure Storage'ı kullanmaya tooget bkz [giriş tooAzure depolama](../storage/common/storage-introduction.md).
* toofind yararlı diğer Azure Otomasyon çalışma kitabı bkz [Azure Otomasyonu Runbook ve modül galerileri](automation-runbook-gallery.md).
* toofind diğer yararlı Resource Manager şablonları görmek [Azure hızlı başlangıç şablonları](https://azure.microsoft.com/resources/templates/)

