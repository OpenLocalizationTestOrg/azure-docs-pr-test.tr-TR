---
title: "aaaAzure yönetilen uygulama UserNameTextBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Compute.UserNameTextBox UI öğesi açıklar"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Varsa `constraints.required` çok ayarlanır**doğru**, hello metin kutusuna bir değer toovalidate başarıyla içermesi gerekir. Merhaba varsayılan değer **doğru**.
- `osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.
- `constraints.regex`JavaScript normal ifade deseni olur. Belirtilmişse, ardından hello metin kutusunun değerini hello düzeni toovalidate başarıyla eşleşmesi gerekir. Varsayılan değer **null**.
- `constraints.validationMessage`bir dize toodisplay Hello metin kutusunun değeri tarafından belirtilen hello doğrulama başarısız olduğunda `constraints.regex`. Aksi takdirde belirtilen ardından metin kutusunun yerleşik doğrulama iletileri kullanılan hello. Merhaba varsayılan değer **null**.
- Bu öğe için belirtilen başlangıç değeri temel alan yerleşik doğrulama sahip `osPlatform`. Merhaba yerleşik doğrulama bir özel normal ifade ile birlikte kullanılabilir.
İçin bir değer `constraints.regex` belirtilmişse hem yerleşik hello ve özel doğrulama tetiklenir.

## <a name="sample-output"></a>Örnek çıktı
```json
"tabrezm"
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
