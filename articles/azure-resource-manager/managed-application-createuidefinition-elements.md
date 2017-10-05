---
title: "Azure yönetilen uygulama kullanıcı Arabirimi tanımı işlevlerin oluşturma | Microsoft Docs"
description: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımları oluşturulurken kullanılacak işlevleri açıklanmaktadır"
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
ms.openlocfilehash: 635e44a7ec6f9244f5fe75eb5ad947cdd8ae59a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition öğeleri
Bu makalede, şema ve tüm desteklenen bir CreateUiDefinition öğelerinin özelliklerini açıklar. Bu öğeleri kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md). Öğelerin çoğu için şemayı aşağıdaki gibidir:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit the [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Özellik | Gerekli | Açıklama |
| -------- | -------- | ----------- |
| ad | Evet | Belirli bir öğenin örneği başvurmak için kullanılan bir iç tanımlayıcı. Öğe adı en yaygın kullanımı yer `outputs`, burada belirtilen öğelerinin çıkış değerleri şablon parametrelerinin eşlenir. Ayrıca, bir öğeye çıkış değeri bağlamak için kullanabileceğiniz `defaultValue` başka bir öğenin. |
| type | Evet | Öğe için işlemek için kullanıcı Arabirimi denetim. Desteklenen türlerinin listesi için bkz: [öğeleri](#elements). |
| Etiket | Evet | Öğenin görüntüleme metni. Değer, birden çok dizeyi içeren bir nesne olabilir şekilde birden çok etiketleri, bazı öğe türleri içerir. |
| defaultValue | Hayır | Öğesinin varsayılan değeri. Bazı öğe türleri karmaşık varsayılan değerleri desteğini değer bir nesne olabilir. |
| Araç İpucu | Hayır | Öğenin araç ipucu görüntülenecek metin. Benzer şekilde `label`, bazı öğeler birden çok araç ipucu dizeleri destekler. Markdown söz dizimini kullanarak satır içi bağlantı katıştırılabilir.
| Kısıtlamaları | Hayır | Öğeyi doğrulama davranışını özelleştirmek için kullanılan bir veya daha fazla özellikleri. Kısıtlamalar için desteklenen özellikler öğesi türüne göre değişir. Bazı öğe türleri doğrulama davranışını özelleştirmesini desteklemiyor ve bu nedenle hiçbir kısıtlamaları özelliğine sahiptir. |
| Seçenekler | Hayır | Öğe davranışını özelleştiren ek özellikler. Benzer şekilde `constraints`, desteklenen özellikler öğesi türüne göre farklılık gösterir. |
| Görünür | Hayır | Öğenin görüntülenip görüntülenmeyeceğini belirtir. Varsa `true`, öğesi ve ilgili alt öğeleri görüntülenir. Varsayılan değer `true`. Kullanım [mantıksal işlevleri](managed-application-createuidefinition-functions.md#logical-functions) dinamik olarak bu özelliğin değerini denetlemek için.

## <a name="elements"></a>Öğeleri

Belge Şeması, bir kullanıcı Arabirimi örnek her öğe içeriyor için öğe (genellikle ilgili doğrulama ve desteklenen özelleştirme) ve örnek çıktı davranışını açıklamalar.

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
* Yönetilen uygulamaların giriş için bkz: [Azure yönetilen uygulama genel bakış](managed-application-overview.md).
* UI tanımları oluşturmak için bir giriş için bkz [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
