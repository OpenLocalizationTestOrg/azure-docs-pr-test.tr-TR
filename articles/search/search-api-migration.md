---
title: "Azure Search Hizmeti REST API sürümü 2016-09-01 aaaUpgrading toohello | Microsoft Docs"
description: "Azure Search Hizmeti REST API sürümü 2016-09-01 toohello yükseltme"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Azure Search Hizmeti REST API sürümü 2016-09-01 toohello yükseltme
Sürüm 2015-02-28 veya 2015-02-28-Önizleme hello birini kullanıyorsanız, [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/azure/dn798935.aspx), bu makalede, uygulama toouse hello sonraki genel olarak kullanılabilir API sürümü, 2016-09-01 yükseltmenize yardımcı olur.

Sürüm 2016-09-01 hello REST API, önceki sürümlerinden bazı değişiklikler içerir. Kodunuzu değiştirmeden önce kullandığınız bağlı olarak hangi sürümün yalnızca en az çaba istemeniz gerekir böylece bunlar çoğunlukla geriye dönük uyumludur. Bkz: [adımları tooupgrade](#UpgradeSteps) yönelik yönergeler toochange, kod toouse hello yeni API sürümü.

> [!NOTE]
> Azure Search Hizmeti örneğinizi hello en son dahil olmak üzere birkaç REST API sürümlerini destekler. En son Merhaba, ancak, kod toouse hello en yeni sürüme geçirmek öneririz artık olduğunda toouse bir sürüm devam edebilirsiniz.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Sürüm 2016-09-01 yenilikler
Sürüm 2016-09-01 hello ikinci genel olarak kullanılabilir hello Azure Search Hizmeti REST API'si sürümüdür. Bu API sürümündeki yeni özellikler içerir:

* [Özel çözümleyiciler](https://aka.ms/customanalyzers), hangi izin dizine ve aranabilir belirteçlere metin dönüştürme işleminin hello üzerinde tootake denetim.
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) ve [Azure Table Storage](search-howto-indexing-azure-tables.md) tooeasily izin dizin oluşturucular içeri aktarma verileri Azure depolama alanından Azure Search bir zamanlama veya isteğe bağlı.
* [Alan eşlemeleri](search-indexer-field-mappings.md), hangi izin toocustomize nasıl dizin oluşturucular verileri Azure Search alın.
* Etag'ler bir eşzamanlılık güvenli şekilde tooupdate hello tanımları dizinler, dizin oluşturucular ve veri kaynaklarını izin verir. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Adımları tooupgrade
2015-02-28 sürümünden yükseltme yapıyorsanız, büyük olasılıkla toochange hello sürüm numarası dışındaki tüm değişiklikleri tooyour kod toomake olmayacaktır. Merhaba yalnızca durumlar toochange kod gerekebilir ne zaman şunlardır:

* Tanınmayan özellikleri bir API yanıt döndürüldüğünde kod başarısız olur. Varsayılan olarak, uygulamanızın anlamadığı özellikleri yok saymanız gerekir.
* Kodunuzu API istekleri devam ederse ve tooresend çalışır bunları toohello yeni API sürümü. Uygulamanızı hello arama API döndürülen devamlılık belirteçleri devam ederse, örneğin, bu durum oluşabilir (daha fazla bilgi için Ara `@search.nextPageParameters` hello içinde [arama API Başvurusu](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Ardından bu durumlardan birini tooyou uygularsanız, toochange uygun şekilde kodunuzu gerekebilir. Hello kullanarak toostart istemediğiniz sürece Aksi halde, hiçbir değişiklik gerekli olmalıdır [yeni özellikler](#WhatsNew) 2016-09-01 sürümü.

Sürüm 2015-02-28-Önizlemesi'nden yükseltiyorsanız, yukarıdaki hello için de geçerlidir, ancak bazı Önizleme özellikleri 2016-09-01 sürümünde mevcut olmayan farkında olmanız da gerekir:

* CSV dosyaları ve JSON dizileri içeren BLOB'lar için Azure Blob Storage dizin oluşturucu desteği.
* Eş anlamlıları
* "Bu gibi daha fazla" sorguları

Kodunuzu bu özellikleri kullanıyorsa, mümkün tooupgrade too2016-09-bunları kullanımınızı kaldırma olmadan 01 olmaz.

> [!IMPORTANT]
> Lütfen unutmayın, Önizleme API'leri sınama ve değerlendirme için tasarlanmıştır ve üretim ortamlarında kullanılmamalıdır.
> 
> 

## <a name="conclusion"></a>Sonuç
Hello Azure Search Hizmeti REST API kullanma hakkında daha fazla ayrıntı ihtiyacınız varsa, en son güncelleştirilen hello bkz [API Başvurusu](https://msdn.microsoft.com/library/azure/dn798935.aspx) konusuna bakın.

Azure Search'te bildiriminiz bizim. Sorunlarla karşılaşırsanız, ücretsiz tooask bize hello hakkında Yardım için eşitleyerek [Azure arama MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) veya [StackOverflow](http://stackoverflow.com/). Azure hakkında soru soran StackOverflow, yapma emin tootag ile arama `azure-search`.

Azure Search kullandığınız için teşekkür ederiz!

