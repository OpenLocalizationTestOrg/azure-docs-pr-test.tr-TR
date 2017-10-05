---
title: "Azure yönetilen uygulama PasswordBox UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.PasswordBox kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a>Microsoft.Common.PasswordBox UI öğesi
Bir parolayı onaylayın ve sağlamak için kullanılan bir denetimi. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Bu öğe desteklemiyor `defaultValue` özelliği.
- Uygulama ayrıntıları için `constraints`, bkz: [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).
- Varsa `options.hideConfirmation` ayarlanır **doğru**, kullanıcının parolasını onayladığınız için ikinci metin kutusu gizlenir. Varsayılan değer **false**.

## <a name="sample-output"></a>Örnek çıktı
```json
"p4ssw0rd"
```

## <a name="next-steps"></a>Sonraki adımlar
* Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
