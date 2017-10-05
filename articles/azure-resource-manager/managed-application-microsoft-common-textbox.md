---
title: "Azure yönetilen uygulama TextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.TextBox kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI öğesi
Biçimlendirilmemiş metin düzenlemek için kullanılan bir denetimi. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

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
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Varsa `constraints.required` ayarlanır **doğru**, metin kutusunun başarıyla doğrulamak için bir değer içermesi gerekir. Varsayılan değer **false**.
- `constraints.regex`JavaScript normal ifade deseni olur. Belirtilmişse, metin kutusunun değerini başarıyla doğrulamak için desen eşleşmesi gerekir. Varsayılan değer **null**.
- `constraints.validationMessage`metin kutusunun değerini doğrulanamadığında görüntülenecek bir dizedir. Belirtilmezse, metin kutusunun yerleşik doğrulama iletileri kullanılır. Varsayılan değer **null**.
- İçin bir değer belirtin mümkündür `constraints.regex` zaman `constraints.required` ayarlanır **false**. Bu senaryoda, bir değer başarıyla doğrulamak metin kutusu için gerekli değildir. Belirtilmişse, normal ifade deseni eşleşmesi gerekir.

## <a name="sample-output"></a>Örnek çıktı

```json
"foobar"
```

## <a name="next-steps"></a>Sonraki adımlar
* Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
