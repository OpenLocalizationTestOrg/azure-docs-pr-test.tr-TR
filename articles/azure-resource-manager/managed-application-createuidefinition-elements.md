---
title: "aaaAzure yönetilen uygulama oluşturma UI tanımı işlevleri | Microsoft Docs"
description: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımları oluşturulurken Hello işlevleri toouse açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition öğeleri
Bu makalede hello şema ve tüm desteklenen bir CreateUiDefinition öğelerinin özelliklerini açıklar. Bu öğeleri kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md). Merhaba şema öğelerin çoğu için aşağıdaki gibidir:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Özellik | Gerekli | Açıklama |
| -------- | -------- | ----------- |
| ad | Evet | Bir iç tanımlayıcı tooreference öğenin belirli bir örneği. Merhaba hello öğe adı en yaygın kullanımı yer `outputs`, öğeleridir hello şablon eşlenen toohello parametrelerinin hello hello çıkış değerleri belirtilen burada. Bunu ayrıca bir öğe toohello toobind hello çıkış değeri kullanabilirsiniz `defaultValue` başka bir öğenin. |
| type | Evet | UI denetim toorender hello öğesinin hello. Desteklenen türlerinin listesi için bkz: [öğeleri](#elements). |
| Etiket | Evet | Merhaba hello öğesinin metin görüntüler. Böylece Hello değeri birden çok dizeyi içeren bir nesne birden çok etiketleri, bazı öğe türleri içerir. |
| defaultValue | Hayır | Merhaba öğesinin Hello varsayılan değeri. Bazı öğe türleri karmaşık varsayılan değerleri desteğini Hello değer bir nesne olabilir. |
| Araç İpucu | Hayır | Merhaba araç ipucunda hello öğesinin metin toodisplay hello. Benzer çok`label`, bazı öğeler birden çok araç ipucu dizeleri destekler. Markdown söz dizimini kullanarak satır içi bağlantı katıştırılabilir.
| Kısıtlamaları | Hayır | Kullanılan toocustomize hello doğrulama davranışını hello öğesinin bir veya daha fazla özellikler. kısıtlamalar desteklenen hello özelliklerini öğesi türüne göre değişir. Bazı öğe türleri hello doğrulama davranışını özelleştirmesini desteklemiyor ve bu nedenle hiçbir kısıtlamaları özelliğine sahiptir. |
| Seçenekler | Hayır | Merhaba öğesi hello davranışını özelleştiren ek özellikler. Benzer çok`constraints`, desteklenen hello özellikleri öğesi türüne göre değişiklik gösterir. |
| Görünür | Hayır | Merhaba öğesi görüntülenip görüntülenmeyeceğini belirtir. Varsa `true`, hello öğesi ve ilgili alt öğelerini görüntülenir. Merhaba varsayılan değer `true`. Kullanım [mantıksal işlevleri](managed-application-createuidefinition-functions.md#logical-functions) toodynamically denetim bu özelliğin değeri.

## <a name="elements"></a>Öğeleri

Merhaba belgelerine her öğe bir UI örnek içeriyor için şema, açıklamalar hello öğesi (genellikle ilgili doğrulama ve desteklenen özelleştirme) ve örnek çıktı hello davranışı.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Sonraki adımlar
* Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
