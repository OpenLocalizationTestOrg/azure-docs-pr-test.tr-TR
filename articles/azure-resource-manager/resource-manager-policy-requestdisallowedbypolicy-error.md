---
title: "Azure kaynak İlkesi RequestDisallowedByPolicy hatasıyla | Microsoft Docs"
description: "RequestDisallowedByPolicy hatanın nedenini açıklar."
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
ms.openlocfilehash: 182a27e444c2f5db66d518a1a0c608d3e319d553
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Azure kaynak ilkesiyle RequestDisallowedByPolicy hata

RequestDisallowedByPolicy hatanın nedeni, bu makalede, ayrıca bu hata için çözüm sağlar.

## <a name="symptom"></a>Belirti

Dağıtım sırasında bir eylem yapmak çalıştığınızda alabileceğiniz bir **RequestDisallowedByPolicy** engellediğini hata gerçekleştirilebilir. Hatanın bir örnek verilmiştir:

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Sorun giderme

Dağıtımınızı engellenen İlkesi hakkındaki ayrıntıları almak için aşağıdaki yöntemlerden birini kullanın:

### <a name="method-1"></a>Yöntem 1

Bu ilke tanımlayıcısı olarak PowerShell'de sağlamak **kimliği** dağıtımınızı engellenen İlkesi hakkındaki ayrıntıları almak için parametre.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Yöntem 2 

Azure CLI 2. 0'ilke tanımı adını sağlayın: 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Çözüm

Güvenlik veya uyumluluk, BT departmanınızın genel IP adresleri, ağ güvenlik grupları, kullanıcı tanımlı yollar veya yönlendirme tabloları oluşturma yasaklar kaynak İlkesi zorlayabilir. "Belirtiler" bölümünde açıklanan hata iletisi örnek adlı ilke **regionPolicyDefinition**, ancak farklı olabilir.
Bu sorunu gidermek için kaynak ilkelerini gözden geçirmek için BT departmanınıza çalışır ve bu ilkeleri ile uyumlu istenen eylemi gerçekleştirmek nasıl belirleyin.


Daha fazla bilgi için aşağıdaki makalelere bakın:

- [Kaynak ilkesine genel bakış](resource-manager-policy.md)
- [Ortak dağıtım RequestDisallowedByPolicy hataları](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


