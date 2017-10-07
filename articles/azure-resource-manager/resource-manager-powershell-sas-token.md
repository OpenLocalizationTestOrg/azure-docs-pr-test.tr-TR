---
title: "aaaDeploy SAS belirteci ve PowerShell ile Azure şablonu | Microsoft Docs"
description: "Azure Resource Manager ve Azure PowerShell toodeploy kaynakları tooAzure korunan bir şablondan SAS belirteci ile kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: b95e096591d6213f8ef79235c8cd85705c4b79ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-powershell"></a>SAS belirteci ve Azure PowerShell ile özel Resource Manager şablonu dağıtma

Şablonunuzu bir depolama hesabında bulunduğunda, access toohello şablonu kısıtlamak ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın. Bu konuda açıklanmaktadır nasıl toouse Azure PowerShell'i Resource Manager şablonları tooprovide dağıtımı sırasında bir SAS belirteci ile. 

## <a name="add-private-template-toostorage-account"></a>Özel şablon toostorage hesabı Ekle

Şablonları tooa depolama hesabınızı ekleyin ve bir SAS belirteci ile dağıtım sırasında toothem bağlayın.

> [!IMPORTANT]
> Merhaba adımları izleyerek hello şablonu içeren hello blob erişilebilir tooonly hello hesap sahibi değil. Ancak, hello blob için bir SAS belirteci oluşturduğunuzda hello blob bu URI ile erişilebilir tooanyone olur. Başka bir kullanıcı hello URI kesişirse kullanıcı mümkün tooaccess hello şablonudur. Bir SAS belirteci kullanarak erişim tooyour şablonları sınırlama, iyi bir yoludur ancak parolalar gibi hassas verileri doğrudan hello şablonunda içermemelidir.
> 
> 

Merhaba aşağıdaki örnekte bir özel depolama hesabı kapsayıcısının ayarlar ve bir şablon yükler:
   
```powershell
# create a storage account for templates
New-AzureRmResourceGroup -Name ManageGroup -Location "South Central US"
New-AzureRmStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name} -Type Standard_LRS -Location "West US"
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# create a container and upload template
New-AzureStorageContainer -Name templates -Permission Off
Set-AzureStorageBlobContent -Container templates -File c:\MyTemplates\storage.json
```

## <a name="provide-sas-token-during-deployment"></a>Dağıtım sırasında SAS belirteci sağlayın
toodeploy özel bir şablon bir depolama hesabındaki bir SAS belirteci oluştur ve hello URI hello şablonunun dahil edin. Merhaba sona erme saati tooallow yeterli zaman toocomplete hello dağıtım ayarlayın.
   
```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name {your-unique-name}

# get hello URI with hello SAS token
$templateuri = New-AzureStorageBlobSASToken -Container templates -Blob storage.json -Permission r `
  -ExpiryTime (Get-Date).AddHours(2.0) -FullUri

# provide URI with SAS token during deployment
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri $templateuri
```

Bir SAS belirteci ile bağlı şablonları kullanma örneği için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).


## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toodeploying şablonları için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md).
* Bir şablon dağıtan bir tam örnek betik için bkz: [dağıtmak Resource Manager şablonu komut dosyası](resource-manager-samples-powershell-deploy.md)
* Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

