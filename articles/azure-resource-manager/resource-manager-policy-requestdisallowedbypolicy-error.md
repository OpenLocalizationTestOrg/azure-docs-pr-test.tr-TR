---
title: "Azure kaynak İlkesi aaaRequestDisallowedByPolicy hatasıyla | Microsoft Docs"
description: "Merhaba RequestDisallowedByPolicy hata Hello nedenini açıklar."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Azure kaynak ilkesiyle RequestDisallowedByPolicy hata

Merhaba hello RequestDisallowedByPolicy hatanın nedenini bu makalede, ayrıca bu hata için çözüm sağlar.

## <a name="symptom"></a>Belirti

Toodo dağıtımı sırasında bir eylem çalıştığınızda alabileceğiniz bir **RequestDisallowedByPolicy** hello engellediğini hata gerçekleştirilebilir. Merhaba, hello hata örneği aşağıdadır:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Sorun giderme

Dağıtımınız, engellenen hello İlkesi tooretrieve ayrıntılarını hello yöntemlerden birini aşağıdaki hello kullanın:

### <a name="method-1"></a>Yöntem 1

Bu ilke tanımlayıcısı hello olarak PowerShell'de sağlamak **kimliği** parametresi tooretrieve dağıtımınızı engellenen hello ilkesi ayrıntılarını.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Yöntem 2 

Azure CLI 2. 0'hello ilke tanımı hello adını sağlayın: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Çözüm

Güvenlik veya uyumluluk, BT departmanınızın genel IP adresleri, ağ güvenlik grupları, kullanıcı tanımlı yollar veya yönlendirme tabloları oluşturma yasaklar kaynak İlkesi zorlayabilir. Merhaba "Belirtiler" bölümünde açıklanan hello hata iletisinin Hello örnek hello İlkesi adlı **regionPolicyDefinition**, ancak farklı olabilir.
tooresolve Bu sorun, BT departmanı tooreview hello kaynak ilkeleriyle çalışmak ve nasıl tooperform hello İstenen eyleme bu ilkeleri ile uyumlu belirleyin.


Daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [Kaynak ilkesine genel bakış](resource-manager-policy.md)
- [Ortak dağıtım RequestDisallowedByPolicy hataları](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


