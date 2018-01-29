---
title: "Azure yönetilen uygulama dosya yükleme UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Microsoft.Common.FileUpload kullanıcı Arabirimi öğesi açıklar"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 095880322ba801895a22efcf3476fa37d9e2ac3c
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Microsoft.Common.FileUpload UI öğesi
Karşıya yüklemek için bir veya daha fazla belirtmesine imkan tanıyan bir denetimi. Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](publish-service-catalog-app.md).

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
- `constraints.accept`Tarayıcının dosyası iletişim kutusunda gösterilen dosya türlerini belirtir. Bkz: [HTML5 belirtimi](http://www.w3.org/TR/html5/forms.html#attr-input-accept) için izin verilen değerler. Varsayılan değer **null**.
- Varsa `options.multiple` ayarlanır **doğru**, kullanıcının tarayıcısının dosyası iletişim kutusunda birden fazla dosya seçmesine izin verilen. Varsayılan değer **false**.
- Bu öğe değerine göre iki modda karşıya yükleme dosyalarını destekler `options.uploadMode`. Varsa **dosya** belirtildi, çıktıyı bir BLOB dosyanın içeriğini içerir. Varsa **url** belirtilmişse dosyanın geçici bir konuma yüklenir ve çıktı blob URL'sini içerir. Geçici BLOB'lar 24 saat sonra temizlenecek. Varsayılan değer **dosya**.
- Değeri `options.openMode` nasıl dosyayı okuma belirler. Dosya düz metin olması bekleniyor, belirtin **metin**; başka belirtin **ikili**. Varsayılan değer **metin**.
- Varsa `options.uploadMode` ayarlanır **dosya** ve `options.openMode` ayarlanır **ikili**, base64 ile kodlanmış çıktı.
- `options.encoding`Dosya okunurken kullanılacak kodlama belirtir. Varsayılan değer **UTF-8**ve kullanılan yalnızca `options.openMode` ayarlanır **metin**.

## <a name="sample-output"></a>Örnek çıktı
Options.Multiple false ise ve options.uploadMode dosyadır, çıktı JSON dizesi olarak dosyanın içeriğini içerir:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Options.Multiple true ise and'options.uploadMode dosyasıdır ve çıktı dosyaların içeriğini bir JSON dizisi olarak içerir:

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

Bir CreateUiDefinition test edilirken (Google Chrome gibi) bazı tarayıcılar tarayıcı konsoluna Microsoft.Common.FileUpload öğe tarafından oluşturulan URL'leri keser. Tam URL'leri kopyalamak için tek bağlantılar sağ gerekebilir.


## <a name="next-steps"></a>Sonraki adımlar
* Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](overview.md).
* UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](create-uidefinition-overview.md).
* Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](create-uidefinition-elements.md).
