---
title: "aaaAzure yönetilen uygulama açılır UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.DropDown UI öğesi açıklar"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a>Microsoft.Common.DropDown UI öğesi
Seçim denetim bir açılır liste. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Merhaba etiketi `constraints.allowedValues` öğenin hello görüntüleme metni ve değeri seçildiğinde hello öğesinin hello çıktı değeri.
- Belirtilmişse, hello varsayılan değer mevcut bir etiketi olmalıdır `constraints.allowedValues`. Belirtilmezse, ilk öğe olarak hello `constraints.allowedValues` seçilir. Merhaba varsayılan değer **null**.
- `constraints.allowedValues`en az bir öğe içermesi gerekir.
- Bu öğe hello desteklemiyor `constraints.required` özelliği. tooemulate Bu davranış bir etiket ve değerine sahip bir öğe eklemek `""` (çok dize boş)`constraints.allowedValues`.

## <a name="sample-output"></a>Örnek çıktı
```json
"Bar"
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
