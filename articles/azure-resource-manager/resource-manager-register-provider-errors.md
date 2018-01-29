---
title: "Azure kaynak sağlayıcısı kayıt hataları | Microsoft Docs"
description: "Azure kaynak sağlayıcısı kayıt hatalarını çözümlemeyi açıklar."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: d6a99917e732a3439a31cafa5608348694014054
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-resource-provider-registration"></a>Kaynak Sağlayıcısı kaydı için hataları çözümleyin

Bu makalede, aboneliğinizde daha önce kullanmadığınız bir kaynak sağlayıcısı kullanırken karşılaşabileceğiniz hatalar açıklanır.

## <a name="symptom"></a>Belirti

Kaynak dağıtırken şu hata kodu ve ileti alabilirsiniz:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Veya bildiren benzer bir ileti alabilirsiniz:

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

## <a name="cause"></a>Nedeni

Üç nedenden biri için bu hataları alırsınız:

1. Kaynak sağlayıcısı, aboneliğiniz için kayıtlı değil
1. API sürümü kaynak türü için desteklenmiyor
1. Kaynak türü için desteklenmeyen konumu

## <a name="solution"></a>Çözüm

Hata iletisi desteklenen konumlar ve API sürümleri için öneriler vermesi gerekir. Şablonunuzu önerilen değerlerden birine değiştirebilirsiniz. Azure portal ya da kullandığınız komut satırı arabirimi tarafından otomatik olarak kayıtlı ancak tüm çoğu sağlayıcıları. Belirli kaynak sağlayıcısı önce kullanmadıysanız, bu sağlayıcıyı kaydetmeniz gerekebilir. PowerShell veya Azure CLI aracılığıyla kaynak sağlayıcıları hakkında daha fazla bulabilir.

### <a name="solution-1"></a>Çözüm 1

İçin PowerShell kullanın **Get-AzureRmResourceProvider** , kayıt durumunu görmek için.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

Bir sağlayıcı kaydetmek için kullanın **Register-AzureRmResourceProvider** ve kaydetmek istediğiniz kaynak sağlayıcısının adını sağlayın.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

Belirli bir kaynak türü için desteklenen konumlardan almak için kullanın:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Belirli bir kaynak türü için desteklenen API sürümleri almak için kullanın:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

### <a name="solution-2"></a>Çözüm 2

**Azure CLI**

Sağlayıcı kayıtlı olup olmadığını görmek için `az provider list` komutu.

```azurecli-interactive
az provider list
```

Bir kaynak sağlayıcısı kaydetmek için kullanın `az provider register` komut ve belirtin *ad alanı* kaydetmek için.

```azurecli-interactive
az provider register --namespace Microsoft.Cdn
```

Desteklenen konumlar ve bir kaynak türü için API sürümlerini görmek için kullanın:

```azurecli-interactive
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

### <a name="solution-3"></a>Çözüm 3

Kayıt durumunu görmek ve bir kaynak sağlayıcısı ad alanı Portalı aracılığıyla kaydedin.

1. Aboneliğiniz için seçin **kaynak sağlayıcıları**.

   ![kaynak sağlayıcıları seç](./media/resource-manager-register-provider-errors/select-resource-provider.png)

1. Kaynak sağlayıcıları listesi bakın ve gerekiyorsa, seçin **kaydetmek** kayıt kaynak sağlayıcısı dağıtmaya çalıştığınız türü için bağlantı.

   ![kaynak sağlayıcıları Listele](./media/resource-manager-register-provider-errors/list-resource-providers.png)
