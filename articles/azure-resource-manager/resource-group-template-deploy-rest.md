---
title: "REST API ve şablon aaaDeploy kaynaklarla | Microsoft Docs"
description: "Azure Resource Manager ve Resource Manager REST API'si toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Kaynakları Resource Manager şablonları ve Resource Manager REST API’si ile dağıtma
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

Bu makalede nasıl toouse hello Resource Manager REST API'si ile Resource Manager şablonları toodeploy kaynakları tooAzure açıklanmaktadır.  

> [!TIP]
> Dağıtım sırasında bir hata ayıklama daha fazla yardım için bkz:
> 
> * [Dağıtım işlemlerini görüntülemek](resource-manager-deployment-operations.md) toolearn yardımcı olacak bilgileri alma hakkında sorun giderme, hata
> * [Azure Resource Manager ile kaynakları tooAzure dağıtırken sık karşılaşılan sorunları giderme](resource-manager-common-deployment-errors.md) toolearn nasıl tooresolve ortak dağıtım hataları
> 
> 

Şablonunuz, yerel bir dosya veya bir URI kullanılabilir olan dış dosyası olabilir. Şablonunuzu bir depolama hesabında bulunduğunda, access toohello şablonu kısıtlamak ve dağıtım sırasında bir paylaşılan erişim imzası (SAS) belirteci sağlayın.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>REST API Hello ile dağıtma
1. Ayarlama [ortak parametrelerini ve üstbilgileri](https://docs.microsoft.com/rest/api/index), kimlik doğrulama belirteçleri de dahil olmak üzere.
2. Varolan bir kaynak grubu yoksa, bir kaynak grubu oluşturun. Abonelik kimliği, hello yeni kaynak grubunu ve çözümünüz için gereksinim duyduğunuz konumu hello adını sağlayın. Daha fazla bilgi için bkz: [bir kaynak grubu oluşturmak](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Merhaba çalıştırarak çalıştırmadan önce dağıtımınızı doğrulama [şablon dağıtımı doğrulamak](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) işlemi. Tam olarak (Merhaba sonraki adımda gösterilen) hello dağıtım yürütülürken gibi hello dağıtım sınarken parametreleri sağlar.
4. Bir dağıtım oluşturun. Abonelik Kimliğiniz, hello hello kaynak grubunun adını, hello hello dağıtım adını ve bağlantı tooyour şablonu sağlar. Merhaba şablon dosyası hakkında daha fazla bilgi için bkz: [parametre dosyası](#parameter-file). Merhaba REST API toocreate bir kaynak grubu hakkında daha fazla bilgi için bkz: [şablon dağıtımı oluşturmak](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Bildirim hello **modu** çok ayarlanır**artımlı**. toorun tam dağıtım Ayarla **modu** çok**tam**. Şablonunuzda olmayan kaynakları yanlışlıkla silebilirsiniz gibi hello tam modu kullanırken dikkatli olun.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Toolog yanıt içeriğini, istek içeriği veya her ikisini istiyorsanız ekleyin **debugSetting** hello isteği.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Bir paylaşılan erişim imzası (SAS) belirteci, depolama hesabı toouse ayarlayabilirsiniz. Daha fazla bilgi için bkz: [paylaşılan erişim imzası için temsilci seçme erişimle](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Merhaba şablon dağıtımı Hello durumunu alın. Daha fazla bilgi için bkz: [şablon dağıtımı hakkında bilgi alma](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Parametre dosyası

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Sonraki adımlar
* zaman uyumsuz REST işlemlerini işleme hakkında toolearn bkz [izlemek zaman uyumsuz Azure işlemleri](resource-manager-async-operations.md).
* Kaynaklara hello .NET istemci kitaplığı aracılığıyla dağıtmaya ilişkin bir örnek için bkz: [.NET kitaplıkları ve bir şablon kullanarak kaynakları dağıtmak](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Şablon toodefine parametrelerinde bkz [şablonları yazma](resource-group-authoring-templates.md#parameters).
* Çözüm toodifferent ortamlarınızın dağıtma ile ilgili yönergeler için bkz: [Microsoft Azure geliştirme ve test ortamlarında](solution-dev-test-environments.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

