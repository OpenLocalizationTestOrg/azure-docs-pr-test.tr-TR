---
title: "aaaAzure kaynak sağlayıcıları ve kaynak türleri | Microsoft Docs"
description: "Resource Manager, şemalar ve kullanılabilir API sürümleri desteği hello kaynak sağlayıcıları ve hello kaynakları barındırabilir hello bölgeler açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Kaynak sağlayıcıları ve türleri

Kaynakları dağıtırken sık tooretrieve hello kaynak sağlayıcıları ve türler hakkında bilgi gerekir. Bu makalede, öğrenin:

* Tüm kaynak sağlayıcıları Azure içinde görüntüleme
* Bir kaynak sağlayıcısının kayıt durumunu denetle
* Kayıt kaynak sağlayıcısı
* Bir kaynak sağlayıcısı için Görünüm kaynak türü
* Bir kaynak türü için geçerli konumlar görünümü
* Bir kaynak türü için geçerli API sürümleri görüntüle

Bu adımları hello portal, PowerShell veya Azure CLI aracılığıyla gerçekleştirebilirsiniz.

## <a name="powershell"></a>PowerShell

toosee Azure ve hello kayıt durumu, aboneliğiniz için tüm kaynak sağlayıcıları kullanın:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Hangi için benzer sonuçlar getirir:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Bir kaynak sağlayıcısı kaydediliyor abonelik toowork hello kaynak sağlayıcısı ile yapılandırır. Merhaba kaydı için her zaman hello abonelik kapsamıdır. Varsayılan olarak, birçok kaynak sağlayıcısı otomatik olarak kaydedilir. Ancak, gerekebilir toomanually bazı kaynak sağlayıcılarını kaydedin. bir kaynak sağlayıcısı tooregister, izni tooperform hello olmalıdır `/register/action` hello kaynak sağlayıcısı için işlem. Bu işlem, hello katkıda bulunan ve sahibi rolleri dahil edilmiştir.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Hangi için benzer sonuçlar getirir:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

Aboneliğinizdeki kaynak türleri bu kaynak Sağlayıcısı'ndan hala varsa, bir kaynak Sağlayıcısı kaydı silinemiyor.

belirli kaynak sağlayıcı, kullanım için toosee bilgileri:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Hangi için benzer sonuçlar getirir:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

toosee hello kaynak türleri için bir kaynak sağlayıcısı kullanın:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Hangi döndürür:

```powershell
batchAccounts
operations
locations
locations/quotas
```

Merhaba API sürümü hello kaynak sağlayıcısı tarafından yayımlanan REST API işlemleri tooa sürümüne karşılık gelir. Bir kaynak sağlayıcısı yeni özellikleri etkinleştirir gibi hello REST API yeni bir sürümünü yayımlar. 

tooget hello kullanılabilir API sürümleri için bir kaynak türünü kullanın:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Hangi döndürür:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Kaynak Yöneticisi tüm bölgelerde desteklenir, ancak hello kaynakları dağıttığınız tüm bölgelerde desteklenmiyor olabilir. Ayrıca, hello kaynak destekleyen bazı bölgelerde kullanmasını önlemek aboneliğinizi sınırlamaları olabilir. 

bir kaynak türü için tooget desteklenen hello konumlarını kullanın.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Hangi döndürür:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Azure CLI
toosee Azure ve hello kayıt durumu, aboneliğiniz için tüm kaynak sağlayıcıları kullanın:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Hangi için benzer sonuçlar getirir:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Bir kaynak sağlayıcısı kaydediliyor abonelik toowork hello kaynak sağlayıcısı ile yapılandırır. Merhaba kaydı için her zaman hello abonelik kapsamıdır. Varsayılan olarak, birçok kaynak sağlayıcısı otomatik olarak kaydedilir. Ancak, gerekebilir toomanually bazı kaynak sağlayıcılarını kaydedin. bir kaynak sağlayıcısı tooregister, izni tooperform hello olmalıdır `/register/action` hello kaynak sağlayıcısı için işlem. Bu işlem, hello katkıda bulunan ve sahibi rolleri dahil edilmiştir.

```azurecli
az provider register --namespace Microsoft.Batch
```

Devam eden, bu kayıt bir ileti döndürür.

Aboneliğinizdeki kaynak türleri bu kaynak Sağlayıcısı'ndan hala varsa, bir kaynak Sağlayıcısı kaydı silinemiyor.

belirli kaynak sağlayıcı, kullanım için toosee bilgileri:

```azurecli
az provider show --namespace Microsoft.Batch
```

Hangi için benzer sonuçlar getirir:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

toosee hello kaynak türleri için bir kaynak sağlayıcısı kullanın:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Hangi döndürür:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

Merhaba API sürümü hello kaynak sağlayıcısı tarafından yayımlanan REST API işlemleri tooa sürümüne karşılık gelir. Bir kaynak sağlayıcısı yeni özellikleri etkinleştirir gibi hello REST API yeni bir sürümünü yayımlar. 

tooget hello kullanılabilir API sürümleri için bir kaynak türünü kullanın:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Hangi döndürür:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Kaynak Yöneticisi tüm bölgelerde desteklenir, ancak hello kaynakları dağıttığınız tüm bölgelerde desteklenmiyor olabilir. Ayrıca, hello kaynak destekleyen bazı bölgelerde kullanmasını önlemek aboneliğinizi sınırlamaları olabilir. 

bir kaynak türü için tooget desteklenen hello konumlarını kullanın.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Hangi döndürür:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Portal

Azure ve hello kayıt durumu, aboneliğiniz için tüm kaynak sağlayıcıları toosee seçin **abonelikleri**.

![Abonelik seç](./media/resource-manager-supported-services/select-subscriptions.png)

Merhaba abonelik tooview seçin.

![Abonelik belirtin](./media/resource-manager-supported-services/subscription.png)

Seçin **kaynak sağlayıcıları** ve kullanılabilir kaynak sağlayıcıları hello listesini görüntüleyin.

![kaynak sağlayıcıları göster](./media/resource-manager-supported-services/show-resource-providers.png)

Bir kaynak sağlayıcısı kaydediliyor abonelik toowork hello kaynak sağlayıcısı ile yapılandırır. Merhaba kaydı için her zaman hello abonelik kapsamıdır. Varsayılan olarak, birçok kaynak sağlayıcısı otomatik olarak kaydedilir. Ancak, gerekebilir toomanually bazı kaynak sağlayıcılarını kaydedin. bir kaynak sağlayıcısı tooregister, izni tooperform hello olmalıdır `/register/action` hello kaynak sağlayıcısı için işlem. Bu işlem, hello katkıda bulunan ve sahibi rolleri dahil edilmiştir. tooregister bir kaynak sağlayıcısı seçin **kaydetmek**.

![Kayıt kaynak sağlayıcısı](./media/resource-manager-supported-services/register-provider.png)

Aboneliğinizdeki kaynak türleri bu kaynak Sağlayıcısı'ndan hala varsa, bir kaynak Sağlayıcısı kaydı silinemiyor.

belirli kaynak sağlayıcısı toosee bilgilerini seçme **daha fazla hizmet**.

![Daha fazla hizmet seçin](./media/resource-manager-supported-services/more-services.png)

Arama **kaynak Gezgini** ve hello kullanılabilir seçeneklerden birini belirleyin.

![Kaynak Gezgini seçin](./media/resource-manager-supported-services/select-resource-explorer.png)

Seçin **sağlayıcıları**.

![Sağlayıcı seçin](./media/resource-manager-supported-services/select-providers.png)

Select hello kaynak sağlayıcısı ve kaynak tooview istediğinizi yazın.

![Kaynak türü seçin](./media/resource-manager-supported-services/select-resource-type.png)

Kaynak Yöneticisi tüm bölgelerde desteklenir, ancak hello kaynakları dağıttığınız tüm bölgelerde desteklenmiyor olabilir. Ayrıca, hello kaynak destekleyen bazı bölgelerde kullanmasını önlemek aboneliğinizi sınırlamaları olabilir. Merhaba kaynak Gezgini hello kaynak türü için geçerli konumlarını görüntüler.

![Konumları göster](./media/resource-manager-supported-services/show-locations.png)

Merhaba API sürümü hello kaynak sağlayıcısı tarafından yayımlanan REST API işlemleri tooa sürümüne karşılık gelir. Bir kaynak sağlayıcısı yeni özellikleri etkinleştirir gibi hello REST API yeni bir sürümünü yayımlar. Merhaba kaynak Gezgini hello kaynak türü için geçerli API sürümü görüntüler.

![API sürümleri göster](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Sonraki adımlar
* Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* Kaynakları dağıtma hakkında toolearn bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).
* bir kaynak sağlayıcısı için tooview hello bkz [Azure REST API](/rest/api/).

