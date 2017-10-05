---
title: "Azure yönetilen uygulama UserNameTextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Compute.UserNameTextBox kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Microsoft.Compute.UserNameTextBox UI öğesi
Bir metin kutusu denetiminin Windows ve Linux kullanıcı adları için yerleşik doğrulama. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Varsa `constraints.required` ayarlanır **doğru**, metin kutusunun başarıyla doğrulamak için bir değer içermesi gerekir. Varsayılan değer **doğru**.
- `osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.
- `constraints.regex`JavaScript normal ifade deseni olur. Belirtilmişse, metin kutusunun değerini başarıyla doğrulamak için desen eşleşmesi gerekir. Varsayılan değer **null**.
- `constraints.validationMessage`metin kutusunun değeri tarafından belirtilen doğrulama başarısız olduğunda görüntülemek için bir dizedir `constraints.regex`. Belirtilmezse, metin kutusunun yerleşik doğrulama iletileri kullanılır. Varsayılan değer **null**.
- Bu öğe için belirtilen değeri temel alan yerleşik doğrulama sahip `osPlatform`. Yerleşik doğrulama bir özel normal ifade ile birlikte kullanılabilir.
İçin bir değer `constraints.regex` belirtildiğinden, yerleşik ve özel doğrulama tetiklenen sonra.

## <a name="sample-output"></a>Örnek çıktı
```json
"tabrezm"
```

## <a name="next-steps"></a>Sonraki adımlar
* Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
