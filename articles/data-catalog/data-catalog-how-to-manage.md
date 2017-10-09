---
title: "Azure veri Kataloğu aaaManage veri varlıklarını | Microsoft Docs"
description: "Merhaba makale nasıl toocontrol görünürlük ve veri varlıklarının sahipliğini Azure veri Kataloğu'nda kayıtlı vurgular."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Azure veri Kataloğu'nda veri varlıklarını yönetme
## <a name="introduction"></a>Giriş
Böylece kolayca bulmak ve tooperform analiz gerekir ve kararları hello veri kaynaklarını anlamasına azure veri Kataloğu veri kaynağı bulma için tasarlanmıştır. Sizin ve diğer kullanıcıların bulmak ve kullanılabilir veri kaynaklarını çok çeşitli hello anlamak bulma yeteneklere hello büyük etkisi olun. Bu öğeleri aklınızda tüm kayıtlı veri kaynaklarının toobe görünür tooand bulunabilirlik tüm katalog kullanıcıları tarafından veri Kataloğu'nun hello varsayılan davranışı içindir.

Veri Kataloğu verme, erişim toohello verileri kendisi. Veri erişimi hello veri kaynağı hello sahibi tarafından denetlenir. Veri Kataloğu ile veri kaynaklarını bulmasına ve hello kataloğa kayıtlı bir ilgili toohello kaynak hello meta verileri görüntüleyebilirsiniz.

Burada veri kaynakları yalnızca görünür toospecific kullanıcılar veya belirli grupların toomembers olmalıdır durumlar olabilir. Bu senaryolarda, kullanıcılar hello katalog içindeki kayıtlı veri kaynaklarının sahipliğini almak ve hello oldukları hello kaynakların güvenilirliğini denetlemek.

> [!NOTE]
> Bu makalede açıklanan hello işlevi yalnızca hello, Azure veri Kataloğu standart sürümü kullanılabilir. Merhaba ücretsiz sürüm sahipliği ve veri varlık görünürlüğü kısıtlamak için özellikleri sağlamaz.
>
>

## <a name="manage-ownership-of-data-assets"></a>Veri varlıklarının sahipliğini yönetme
Varsayılan olarak, veri Kataloğu'nda kayıtlı veri varlıklarını sahipsiz. Herhangi bir kullanıcı izni tooaccess hello Kataloğu ile bulabilir ve bu varlıklarına açıklama. Kullanıcılar, sahipsiz veri varlıklarının sahipliğini ve hello oldukları hello varlıklarının görünürlüğünü sınırlayın.

Veri Kataloğu'ndaki bir veri varlığına ait olduğunda, yalnızca hello sahipleri tarafından yetkilendirilmiş kullanıcılar hello varlık bulmak ve meta verilerini görüntülemek ve yalnızca hello sahipleri hello varlık hello Kataloğu'ndan silebilirsiniz.

> [!NOTE]
> Veri Kataloğu sahipliği hello kataloğunda depolanmış hello meta etkiler. Sahipliği hello temel alınan veri kaynağında tüm izinleri confer değil.
>
>

### <a name="take-ownership"></a>Sahipliği alın
Kullanıcılar, hello seçerek veri varlıklarının sahipliğini alabilir **Sahipliği Al** hello veri Kataloğu portalında seçeneği. Özel izinler gerekli tootake sahipliğini sahipsiz veri varlığına ' dir. Herhangi bir kullanıcı bir sahipsiz veri varlığı sahipliğini alabilir.

### <a name="add-owners-and-co-owners"></a>Sahipleri ve ikincil sahipler ekleme
Bir veri varlığına zaten sahip değilse, diğer kullanıcıların yalnızca Sahiplik alınamıyor. Bunlar birlikte sahipleri olarak var olan bir sahibi tarafından eklenmiş olması gerekir. Tüm sahibi ikincil sahip ek kullanıcı veya güvenlik grupları ekleyebilir.

> [!NOTE]
> Bu en iyi yöntem toohave herhangi bir veri varlığına ait sahipleri olarak en az iki kişiler aranır.
>
>

### <a name="remove-owners"></a>Sahipleri Kaldır
Tüm varlık sahibi ikincil sahip eklemeniz yeterlidir gibi tüm varlık sahibi tüm ikincil sahip kaldırabilirsiniz.

Bir sahibi olarak kendisine veya kendisini kaldırır bir varlık sahibi artık hello varlık yönetebilirsiniz. Merhaba varlık sahibinin sahibi olarak kendisine veya kendisini kaldırır ve diğer ortak sahip yoktur, hello varlık durumu sahipsiz tooan döner.

## <a name="control-visibility"></a>Denetim görünürlüğü
Veri varlığına sahipleri hello oldukları hello veri varlıklarının görünürlüğünü kontrol edebilirsiniz. toorestrict görünürlüğü hello varsayılan olarak, tüm veri Kataloğu kullanıcıları bulmak ve görünüm veri varlığına hello burada hello varlık sahibi değiştirmek hello görünürlük ayarından **herkesin** çok**sahipler ve bu kullanıcılar** hello özelliklerinde hello varlık. Sahipleri, belirli kullanıcılar ve güvenlik grupları daha sonra ekleyebilirsiniz.

> [!NOTE]
> Mümkün olduğunda, varlık sahipliği ve görünürlük izinleri toosecurity grupları ve tooindividual kullanıcıları değil atanması gerekir.
>
>

## <a name="catalog-administrators"></a>Katalog yöneticileri
Veri Kataloğu yöneticileri örtük olarak hello katalogdaki tüm varlıkları ikincil sahip olur. Varlık sahipleri görünürlük yöneticileri kaldıramazsınız ve yöneticiler sahipliği ve tüm veri varlıklarını hello kataloğunda görünürlük yönetebilir.

## <a name="summary"></a>Özet
Merhaba veri Kataloğu kitle kaynak modeli toometadata ve veri varlık bulma tüm katalog kullanıcıları toocontribute sağlar ve keşfedin. Merhaba, veri Kataloğu standart sürümü, sahipliği ve Yönetimi toolimit hello görünürlük ve belirli veri varlıklarını kullanımı için tasarlanmıştır.
