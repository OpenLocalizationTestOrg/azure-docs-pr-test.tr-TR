---
title: "Azure yönetilen uygulamalar oluşturma UI tanımı anlama | Microsoft Docs"
description: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımları oluşturmayı açıklar"
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
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a>CreateUiDefinition ile çalışmaya başlama
Bu belge, Azure portal tarafından yönetilen bir uygulama oluşturmak için kullanılan kullanıcı arabirimi oluşturmak için kullanılan bir CreateUiDefinition çekirdek kavramlarını tanıtır.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

Bir CreateUiDefinition her zaman üç özellikleri içerir: 

* işleyici
* Sürüm
* Parametreleri

Yönetilen uygulamalar için işleyici her zaman olmalıdır `Microsoft.Compute.MultiVm`, ve en son desteklenen sürümünü `0.1.2-preview`.

Parameters özelliği şema sürümü ve belirtilen işleyici birleşimi bağlıdır. Yönetilen uygulamalar için desteklenen özelliklerdir `basics`, `steps`, ve `outputs`. Temel kavramları ve adımları özelliklerini içeren _öğeleri_ - gibi metin kutuları ve bırakmalar - Azure portalında görüntülenecek. Çıktılar özelliğini Azure Resource Manager dağıtım şablonu parametreleri için belirtilen öğelerinin çıkış değerlerini eşlemek için kullanılır.

Dahil olmak üzere `$schema` önerilir ancak isteğe bağlıdır. Belirtilmişse, değerin için `version` içinde eşleşmelidir `$schema` URI.

## <a name="basics"></a>Temel Bilgiler
Temel bilgileri her zaman Azure portalında bir CreateUiDefinition ayrıştırırken oluşturulan Sihirbazı'nın ilk adımı adımdır. Belirtilen öğeleri görüntüleme yanı sıra `basics`, portalı abonelik, kaynak grubu ve dağıtımı için konum seçmek kullanıcıları için öğeleri yerleştirir. Genellikle, bir küme veya yönetici kimlik bilgileri adı gibi dağıtım çapında parametreler için sorgu öğeleri bu adımı tamamlamalıdır.

Bir öğenin davranışı kullanıcının abonelik, kaynak grubu veya konum bağımlı olması durumunda, bu öğenin temel kullanılamaz. Örneğin, **Microsoft.Compute.SizeSelector** kullanıcının abonelik ve kullanılabilir boyutların listesi belirlemek için konum bağlıdır. Bu nedenle, **Microsoft.Compute.SizeSelector** adımlarda yalnızca kullanılabilir. Genellikle, yalnızca öğeleri **Microsoft.Common** ad alanı temelleri kullanılabilir. Ancak bazı öğeler diğer ad (gibi **Microsoft.Compute.Credentials**), kullanıcının içeriğine bağlı verme, hala izin verilir.

## <a name="steps"></a>Adımlar
Adımları özelliği her biri bir veya daha fazla öğe içeren temel bilgileri sonra görüntülemek için sıfır veya daha fazla ek adımlar içerebilir. Rol veya dağıtılan uygulama katmanı başına adımları eklemeyi düşünün. Örneğin, bir adım ana düğüm girdileri için ve çalışan düğümleri için bir adım bir kümede ekleyin.

## <a name="outputs"></a>Çıkışları
Azure Portalı'nı kullanan `outputs` öğelerinden eşlemek için özellik `basics` ve `steps` Azure Resource Manager dağıtım şablonu parametreleri. Bu sözlüğün anahtarlarını şablon parametrelerinin adları ve değerleri başvurulan öğelerin çıkış nesnelerden özellikleridir.

## <a name="functions"></a>İşlevler
Benzer şekilde [şablon işlevleri](resource-group-template-functions.md) Azure Kaynak Yöneticisi'nde (hem de söz dizimi ve işlevsellik) CreateUiDefinition öğeleri girişleri ve çıkışları ile çalışmak için işlevleri sağlayan yanı sıra koşulları gibi özellikleri.

## <a name="next-steps"></a>Sonraki adımlar
CreateUiDefinition kendisini basit bir şeması vardır. Tüm desteklenen öğeleri ve aşağıdaki belgeler wondrous ayrıntılı olarak açıklayan işlevleri gerçek derinliği geldiği:

- [Öğeleri](managed-application-createuidefinition-elements.md)
- [İşlevler](managed-application-createuidefinition-functions.md)

CreateUiDefinition için geçerli bir JSON şeması burada bulunur: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Sonraki sürümlerinde aynı konumda kullanılabilir. Değiştir `0.1.2-preview` URL'sinin ve `version` kullanmayı düşündüğünüz sürüm tanıtıcısını değerle. Şu anda desteklenen sürüm tanımlayıcılardır `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, ve `0.1.2-preview`.