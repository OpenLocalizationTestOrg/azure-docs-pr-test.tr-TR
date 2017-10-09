---
title: "aaaAzure yönetilen uygulama TextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.TextBox UI öğesi açıklar"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI öğesi
Kullanılan tooedit olabilir bir denetim biçimlendirilmemiş metin. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Varsa `constraints.required` çok ayarlanır**doğru**, hello metin kutusuna bir değer toovalidate başarıyla içermesi gerekir. Merhaba varsayılan değer **false**.
- `constraints.regex`JavaScript normal ifade deseni olur. Belirtilmişse, ardından hello metin kutusunun değerini hello düzeni toovalidate başarıyla eşleşmesi gerekir. Varsayılan değer **null**.
- `constraints.validationMessage`bir dize toodisplay Hello metin kutusunun değerini doğrulama başarısız olduğunda. Aksi takdirde belirtilen ardından metin kutusunun yerleşik doğrulama iletileri kullanılan hello. Merhaba varsayılan değer **null**.
- Olası toospecify için bir değer `constraints.regex` zaman `constraints.required` çok ayarlanır**false**. Bu senaryoda, bir değer başarıyla hello metin kutusu toovalidate için gerekli değildir. Belirtilmişse, bu hello normal ifade deseni eşleşmelidir.

## <a name="sample-output"></a>Örnek çıktı

```json
"foobar"
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
