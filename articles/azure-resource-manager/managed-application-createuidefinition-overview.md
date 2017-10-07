---
title: "Azure yönetilen uygulamaları için kullanıcı Arabirimi tanımı oluşturma aaaUnderstand | Microsoft Docs"
description: "Açıklar nasıl toocreate UI tanımları Azure yönetilen uygulamalar"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>CreateUiDefinition ile çalışmaya başlama
Bu belge hello çekirdek hello Azure portal toogenerate hello kullanıcı arabirimi tarafından yönetilen bir uygulama oluşturmak için kullanılan bir CreateUiDefinition kavramlarını tanıtır.

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
* parametreler

Yönetilen uygulamalar için işleyici her zaman olmalıdır `Microsoft.Compute.MultiVm`, ve en son desteklenen hello sürümü `0.1.2-preview`.

Merhaba parameters özelliği Hello şeması hello birleşimi hello belirtilen işleyici ve sürüm üzerinde bağlıdır. Yönetilen uygulamalar için desteklenen hello özelliklerdir `basics`, `steps`, ve `outputs`. Hello temel kavramları ve adımları özelliklerini içeren hello _öğeleri_ - metin kutuları ve bırakmalar gibi - toobe hello Azure portal görüntülenir. kullanılan toomap hello çıkış değerini özelliktir hello çıkışları belirtilen öğeleri toohello hello Azure Resource Manager dağıtım şablonu parametrelerinin hello.

Dahil olmak üzere `$schema` önerilir ancak isteğe bağlıdır. Belirtilmişse, değeri hello `version` hello hello içinde sürümüyle eşleşmelidir `$schema` URI.

## <a name="basics"></a>Temel Bilgiler
Merhaba temel bilgileri her zaman hello Azure portalında bir CreateUiDefinition ayrıştırırken oluşturulan hello Sihirbazı'nın ilk adımı hello adımdır. Toodisplaying hello öğeleri ayrıca belirtilen `basics`, hello portalı kullanıcıları toochoose hello abonelik, kaynak grubunu ve konumu hello dağıtılmak için öğeleri yerleştirir. Genellikle, bir küme veya yönetici kimlik bilgileri hello adı gibi dağıtım çapında parametreleri için sorgu öğeleri bu adımda gitmeniz gerekir.

Bir öğenin davranışı hello kullanıcının abonelik, kaynak grubu veya konum bağımlı olması durumunda, bu öğenin temel bilgileri kullanılamaz. Örneğin, **Microsoft.Compute.SizeSelector** hello kullanıcının abonelik ve konumda toodetermine hello kullanılabilir boyutların listesi üzerinde bağlıdır. Bu nedenle, **Microsoft.Compute.SizeSelector** adımlarda yalnızca kullanılabilir. Genellikle, yalnızca öğeleri hello **Microsoft.Common** ad alanı temelleri kullanılabilir. Ancak bazı öğeler diğer ad (gibi **Microsoft.Compute.Credentials**), kullanıcının Merhaba içeriğine bağlı verme, hala izin verilir.

## <a name="steps"></a>Adımlar
Merhaba adımları özellik sıfır veya daha fazla ek adımlar toodisplay her biri bir veya daha fazla öğe içeren temel bilgileri sonra içerebilir. Rol veya dağıtılan hello uygulama katmanı başına adımları eklemeyi düşünün. Örneğin, bir adım hello ana düğüm girdileri için ve adım hello çalışan düğümleri için bir kümede ekleyin.

## <a name="outputs"></a>Çıkışları
Hello Azure portal kullanır hello `outputs` özelliği toomap öğelerinden `basics` ve `steps` hello Azure Resource Manager dağıtım şablonu toohello parametreleri. Bu sözlüğün anahtarlarını Hello hello şablon parametrelerinin hello adlarının ve başvurulan hello öğelerden hello çıkış nesnelerin özelliklerini hello değerlerdir.

## <a name="functions"></a>İşlevler
Benzer çok[şablon işlevleri](resource-group-template-functions.md) Azure Kaynak Yöneticisi'nde (hem de söz dizimi ve işlevsellik) CreateUiDefinition öğeleri girişleri ve çıkışları ile çalışmak için işlevleri sağlayan yanı sıra koşulları gibi özellikleri.

## <a name="next-steps"></a>Sonraki adımlar
CreateUiDefinition kendisini basit bir şeması vardır. Hello gerçek derinliğini, tüm desteklenen hello öğeleri ve İşlevler, belgeleri aşağıdaki hangi hello wondrous ayrıntılı olarak açıklayın gelir:

- [Öğeleri](managed-application-createuidefinition-elements.md)
- [İşlevler](managed-application-createuidefinition-functions.md)

CreateUiDefinition için geçerli bir JSON şeması burada bulunur: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Sonraki sürümlerinde kullanılabilir hello aynı konumu. Hello yerine `0.1.2-preview` hello URL ve hello bölümünü `version` değeri toouse düşündüğünüz hello sürüm tanımlayıcısına sahip. şu anda desteklenen hello sürüm tanımlayıcılardır `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, ve `0.1.2-preview`.
