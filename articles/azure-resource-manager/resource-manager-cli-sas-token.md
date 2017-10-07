---
title: "aaaDeploy SAS belirteci ve Azure CLI ile Azure şablonu | Microsoft Docs"
description: "Azure Resource Manager ve Azure CLI toodeploy kaynakları tooAzure korunan bir şablondan SAS belirteci ile kullanın."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 59c64616d6e1f5e456d88a72854d0ed99e1bdc0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-private-resource-manager-template-with-sas-token-and-azure-cli"></a>SAS belirteci ve Azure CLI ile özel Resource Manager şablonu dağıtma

Şablonunuzu bir depolama hesabında bulunduğunda, access toohello şablonu kısıtlamak ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın. Bu konuda açıklanmaktadır nasıl toouse Azure PowerShell'i Resource Manager şablonları tooprovide dağıtımı sırasında bir SAS belirteci ile. 

## <a name="add-private-template-toostorage-account"></a>Özel şablon toostorage hesabı Ekle

Şablonları tooa depolama hesabınızı ekleyin ve bir SAS belirteci ile dağıtım sırasında toothem bağlayın.

> [!IMPORTANT]
> Merhaba adımları izleyerek hello şablonu içeren hello blob erişilebilir tooonly hello hesap sahibi değil. Ancak, hello blob için bir SAS belirteci oluşturduğunuzda hello blob bu URI ile erişilebilir tooanyone olur. Başka bir kullanıcı hello URI kesişirse kullanıcı mümkün tooaccess hello şablonudur. Bir SAS belirteci kullanarak erişim tooyour şablonları sınırlama, iyi bir yoludur ancak parolalar gibi hassas verileri doğrudan hello şablonunda içermemelidir.
> 
> 

Merhaba aşağıdaki örnekte bir özel depolama hesabı kapsayıcısının ayarlar ve bir şablon yükler:
   
```azurecli
az group create --name "ManageGroup" --location "South Central US"
az storage account create \
    --resource-group ManageGroup \
    --location "South Central US" \
    --sku Standard_LRS \
    --kind Storage \
    --name {your-unique-name}
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
az storage container create \
    --name templates \
    --public-access Off \
    --connection-string $connection
az storage blob upload \
    --container-name templates \
    --file vmlinux.json \
    --name vmlinux.json \
    --connection-string $connection
```

### <a name="provide-sas-token-during-deployment"></a>Dağıtım sırasında SAS belirteci sağlayın
toodeploy özel bir şablon bir depolama hesabındaki bir SAS belirteci oluştur ve hello URI hello şablonunun dahil edin. Merhaba sona erme saati tooallow yeterli zaman toocomplete hello dağıtım ayarlayın.
   
```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name {your-unique-name} \
    --query connectionString)
token=$(az storage blob generate-sas \
    --container-name templates \
    --name vmlinux.json \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name vmlinux.json \
    --output tsv \
    --connection-string $connection)
az group deployment create --resource-group ExampleGroup --template-uri $url?$token
```

Bir SAS belirteci ile bağlı şablonları kullanma örneği için bkz: [Azure Resource Manager ile bağlı şablonları kullanma](resource-group-linked-templates.md).

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toodeploying şablonları için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy-cli.md).
* Bir şablon dağıtan bir tam örnek betik için bkz: [dağıtmak Resource Manager şablonu komut dosyası](resource-manager-samples-cli-deploy.md)
* Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).
