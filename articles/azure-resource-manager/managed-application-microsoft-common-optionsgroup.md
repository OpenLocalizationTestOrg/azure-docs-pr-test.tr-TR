---
title: "aaaAzure yönetilen uygulama OptionsGroup UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.OptionsGroup UI öğesi açıklar"
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a>Microsoft.Common.OptionsGroup UI öğesi
Seçim denetim kullanılabilir seçeneklerden bir satır. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
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
- Belirtilmişse, hello varsayılan değer mevcut bir etiketi olmalıdır `constraints.allowedValues`. Belirtilmezse, ilk öğe olarak hello `constraints.allowedValues` varsayılan olarak seçilidir. Merhaba varsayılan değer **null**.
- `constraints.allowedValues`en az bir öğe içermesi gerekir.
- Bu öğe hello desteklemiyor `constraints.required` özellik; öğenin seçili toovalidate başarıyla olması gerekir.

## <a name="sample-output"></a>Örnek çıktı
```json
"Bar"
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
