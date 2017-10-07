---
title: "aaaAzure yönetilen uygulama CredentialsCombo UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Compute.CredentialsCombo UI öğesi açıklar"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Microsoft.Compute.CredentialsCombo UI öğesi
Windows ve Linux parolalar ve SSH ortak anahtarları için yerleşik doğrulama denetimleriyle grubudur. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Şema
Varsa `osPlatform` olan **Windows**, hello aşağıdaki şema kullanılır:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Varsa `osPlatform` olan **Linux**, hello aşağıdaki şema kullanılır:
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- `osPlatform`belirtilmeli ve birini kullanabilir **Windows** veya **Linux**.
- Varsa `constraints.required` çok ayarlanır**doğru**, parola hello veya SSH ortak anahtarı metin kutuları içermelidir değerleri toovalidate başarıyla. Merhaba varsayılan değer **doğru**.
- Varsa `options.hideConfirmation` çok ayarlanır**doğru**, hello kullanıcının parolasını onayladığınız için hello ikinci metin kutusu gizli sonra. Merhaba varsayılan değer **false**.
- Varsa `options.hidePassword` çok ayarlanır**doğru**, hello seçeneği toouse parola kimlik doğrulaması gizli sonra. Kullanılabilmesi için yalnızca `osPlatform` olan **Linux**. Varsayılan değer **false**.
- Merhaba ek kısıtlamalar izin hello kullanarak parolaları uygulanabilir `customPasswordRegex` özelliği. Merhaba dizesinde `customValidationMessage` parola özel doğrulama başarısız olduğunda görüntülenir. Merhaba her iki özellik için varsayılan değer olan **null**.

## <a name="sample-output"></a>Örnek çıktı
Varsa `osPlatform` olan **Windows**, veya hello kullanıcı sağlanan parola yerine bir SSH ortak anahtarı ardından hello aşağıdaki çıkış bekleniyor:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Merhaba kullanıcı SSH ortak anahtarı sağladıysanız, ardından hello aşağıdaki çıkış bekleniyor:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
