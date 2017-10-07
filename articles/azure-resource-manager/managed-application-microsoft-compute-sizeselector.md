---
title: "aaaAzure yönetilen uygulama SizeSelector UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Compute.SizeSelector UI öğesi açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Microsoft.Compute.SizeSelector UI öğesi
Bir veya daha fazla sanal makine örnekleri için bir boyut seçmek için bir denetim. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- `recommendedSizes`en az bir boyut içermelidir. Merhaba, ilk boyutu hello varsayılan olarak kullanılır önerilir.
- Önerilen boyut hello seçili konumda kullanılabilir durumda değilse, hello boyutu otomatik olarak atlandı. Bunun yerine, hello sonraki önerilen boyut kullanılır.
- Hello belirtilmemiş herhangi bir boyutta `constraints.allowedSizes` gizlenir ve belirtilen olmayan herhangi bir boyutta `constraints.excludedSizes` gösterilir.
`constraints.allowedSizes`ve `constraints.excludedSizes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz. Merhaba kullanılabilir boyutların listesi çağırarak belirlenebilir [listesinden bir abonelik için kullanılabilir sanal makine boyutlarını](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).
- `osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**. Toodetermine hello donanım maliyetlerini hello sanal makinelerin kullandı.
- `imageReference`üçüncü taraf görüntüleri için sağlanan ancak birinci taraf görüntüleri için atlandı. Toodetermine hello yazılım maliyetleri hello sanal makinelerin kullandı.
- `count`kullanılan tooset hello uygun çarpanı hello öğesi var. Statik bir değer gibi destekleyen **2**, veya gibi başka bir öğeden dinamik bir değer `[steps('step1').vmCount]`. Merhaba varsayılan değer **1**.

## <a name="sample-output"></a>Örnek çıktı
```json
"Standard_D1"
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
