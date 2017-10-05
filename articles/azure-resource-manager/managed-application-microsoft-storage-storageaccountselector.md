---
title: "Azure yönetilen uygulama StorageAccountSelector UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Storage.StorageAccountSelector kullanıcı Arabirimi öğesi açıklar"
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a>Microsoft.Storage.StorageAccountSelector UI öğesi
Yeni veya var olan depolama hesabını seçmek için bir denetim. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- Belirtilmişse, `defaultValue.name` benzersizlik için otomatik olarak doğrulanır. Depolama hesabı adı benzersiz değilse, kullanıcının farklı bir ad belirtin veya mevcut bir depolama hesabını seçin.
- İçin varsayılan değer `defaultValue.type` olan **Premium_LRS**.
- Belirtilen olmayan herhangi bir türü `constraints.allowedTypes` gizlenir ve belirtilen olmayan herhangi bir türü `constraints.excludedTypes` gösterilir.
`constraints.allowedTypes`ve `constraints.excludedTypes` hem isteğe bağlıdır, ancak aynı anda kullanılamaz.
- Varsa `options.hideExisting` olan **doğru**, kullanıcının mevcut bir depolama hesabını seçemezsiniz. Varsayılan değer **false**.


## <a name="sample-output"></a>Örnek çıktı
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a>Sonraki adımlar
* Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
