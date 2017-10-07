---
title: "adlandırma kuralları için aaaAzure kaynak ilkeleri | Microsoft Docs"
description: "Kaynak adlandırma kuralları için Azure Resource Manager ilkelerini açıklar."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Kaynak adları ve metin için geçerlidir
Bu konu çeşitli gösterir [kaynak ilkeleri](resource-manager-policy.md) tooestablish adlandırma ve metin kuralları uygulayabilirsiniz. Bu ilkeler kaynak adları ve etiket değerleri için tutarlılık emin olun. 

## <a name="set-naming-convention-with-wildcard"></a>Joker karakter ile adlandırma kuralı ayarlayın
Merhaba aşağıdaki örnek gösterir hello tarafından desteklenen joker hello kullanımını **gibi** koşulu. Merhaba koşul hello varsa ad hello belirtilen desenle eşleşen belirtir (namePrefix\*nameSuffix) hello isteği reddedecek:

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Desen ile adlandırma kuralı ayarlayın

kaynak adları kullanım hello bir desen eşleşmesini toospecify koşul eşleşir. Merhaba aşağıdaki örnek gerektirir adları toostart ile `contoso` ve altı ek harf içermelidir:

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Etiket değeri için tarih deseni ayarlayın

toorequire tarih düzeni iki basamak, tire, üç harf, tire ve dört basamak kullanımı:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Sonraki adımlar
* (Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın. Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir. Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md). REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md). 
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

