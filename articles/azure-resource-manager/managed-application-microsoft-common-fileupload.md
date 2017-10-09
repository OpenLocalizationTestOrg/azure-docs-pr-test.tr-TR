---
title: "aaaAzure yönetilen uygulama dosya yükleme UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.FileUpload UI öğesi açıklar"
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Microsoft.Common.FileUpload UI öğesi
Bir veya daha fazla kullanıcı toospecify sağlayan bir denetimi tooupload dosyaları. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).

## <a name="ui-sample"></a>Kullanıcı Arabirimi örneği
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Şema
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Açıklamalar
- `constraints.accept`Merhaba hello tarayıcının dosyası iletişim kutusunda gösterilen dosya türlerini belirtir. Merhaba bkz [HTML5 belirtimi](http://www.w3.org/TR/html5/forms.html#attr-input-accept) için izin verilen değerler. Merhaba varsayılan değer **null**.
- Varsa `options.multiple` çok ayarlanır**doğru**, hello tarayıcının dosya iletişim kutusu bir dosyada birden çok tooselect hello kullanıcı izin verilir. Merhaba varsayılan değer **false**.
- Bu öğe hello değerine göre iki modda karşıya yükleme dosyalarını destekler `options.uploadMode`. Varsa **dosya** belirtilirse, hello çıktı hello bir BLOB hello dosyanın içeriğini içerir. Varsa **url** belirtilmişse hello dosyasıdır karşıya yüklenen tooa geçici konuma ve hello çıktı hello blob hello URL'sini içerir. Geçici BLOB'lar 24 saat sonra temizlenecek. Merhaba varsayılan değer **dosya**.
- Merhaba değerini `options.openMode` nasıl hello dosyayı okuma belirler. Merhaba beklenen toobe düz metin dosyasıysa belirtin **metin**; başka belirtin **ikili**. Merhaba varsayılan değer **metin**.
- Varsa `options.uploadMode` çok ayarlanır**dosya** ve `options.openMode` çok ayarlanır**ikili**, hello çıkış base64 ile kodlanmış.
- `options.encoding`Merhaba kodlama toouse hello dosyası okunurken belirtir. Merhaba varsayılan değer **UTF-8**ve kullanılan yalnızca `options.openMode` çok ayarlanır**metin**.

## <a name="sample-output"></a>Örnek çıktı
Options.Multiple false ise ve options.uploadMode dosyadır, çıktı hello dosyasının Merhaba içeriğine JSON dizesi olarak içerir:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Options.Multiple true ise and'options.uploadMode dosyasıdır ve çıktı hello dosyaları Merhaba içeriğine bir JSON dizisi olarak içerir:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Options.Multiple false ise ve options.uploadMode URL'dir çıktıyı JSON dizesi olarak bir URL içerir:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Options.Multiple geçerlidir ve url options.uploadMode ise, çıktı bir JSON dizisi olarak URL'lerin bir listesini içerir:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Bir CreateUiDefinition test edilirken (Google Chrome gibi) bazı tarayıcılar hello tarayıcı konsoluna hello Microsoft.Common.FileUpload öğe tarafından oluşturulan URL'leri keser. Tooright tıklatma tek bağlantılar toocopy hello tam URL'leri gerekebilir.


## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).
