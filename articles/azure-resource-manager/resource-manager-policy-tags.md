---
title: "etiketleri için aaaAzure kaynak ilkeleri | Microsoft Docs"
description: "Etiketler kaynaklardaki yönetmek için kaynak ilkeleri örnekleri sağlar"
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Kaynak etiketleri için geçerlidir

Bu konu, kaynakları tooensure tutarlı etiketleri kullanımını uygulayabilirsiniz ortak ilke kuralları sağlar.

Bir etiketi İlkesi tooa kaynak grubuna veya aboneliğe mevcut kaynaklarla uygulama firmalarda geriye dönük hello İlkesi toothose kaynaklar için geçerli değildir. Bu kaynaklar üzerindeki tooenforce hello ilkeleri kaynakları var olan bir güncelleştirme toohello tetikler. Bu makalede, bir güncelleştirme tetiklemek için bir PowerShell örnek içerir.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Bir kaynak grubundaki tüm kaynakların bir etiketi/değer sahip olduğundan emin olun

Ortak gerekli bir kaynak grubundaki tüm kaynakların bir özel etiket ve değerine sahip değildir. Bu gereksinim gerekli tootrack maliyetleri departmanı tarafından görülür. hello aşağıdaki koşullar karşılanmalıdır:

* Merhaba, etiket ve değer eklenmiş toonew ve hello etiketi olmayan kaynakları güncelleştirilmiş gereklidir.
* Etiket Hello gerekli ve tüm mevcut kaynaklardan değeri kaldırılamaz.

Bu gereksinim, iki yerleşik ilkeleri tooa kaynak grubu uygulayarak gerçekleştirmek.

| Kimlik | Açıklama |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Merhaba kullanıcı tarafından belirtilmediğinde gerekli bir etiket ve varsayılan değerini geçerlidir. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Gerekli bir etiket ve değerini zorlar. |

### <a name="powershell"></a>PowerShell

PowerShell Betiği aşağıdaki hello hello iki yerleşik ilke tanımları tooa kaynak grubu atar. Merhaba betiği çalıştırmadan önce tüm gerekli etiketleri toohello kaynak grubu atayın. Her etiket hello kaynak grubu üzerinde hello grubundaki hello kaynaklar için gereklidir. tooassign tooall kaynak grupları, aboneliğinizdeki hello sağlamaz `-Name` hello kaynak grupları alınırken parametresi.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Merhaba ilkeleri atadıktan sonra eklediğiniz kaynakları tooenforce hello etiketi ilkeleri var olan bir güncelleştirme tooall tetikleyebilir. Merhaba aşağıdaki betiği hello kaynaklardaki varolan herhangi bir etiket korur:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Bir kaynak türü için etiketler gerektirir
Aşağıdaki örnek hello toonest mantıksal işleçler toorequire bir uygulamanın nasıl etiketi yalnızca bir belirtilen kaynak türü için (Bu durumda, depolama hesapları için) gösterir.

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Etiket gerektirir
Merhaba aşağıdaki İlkesi (herhangi bir değer uygulanabilir) "costCenter" anahtarı içeren bir etiket yok isteklerini reddeder:

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Sonraki adımlar
* (Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın. Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir. Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md). REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).
* Bir giriş tooresource ilkeleri için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

