---
title: "Azure veri Kataloğu'ndaki aaaHow toodiscover veri kaynaklarında | Microsoft Docs"
description: "Bu makalede nasıl toodiscover aramayı ve filtrelemeyi de dahil olmak üzere Azure veri Kataloğu ile veri varlıklarını kayıtlı vurgular ve isabet vurgulama özelliklerini hello Azure veri Kataloğu portalını hello kullanarak."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Azure veri Kataloğu'nda nasıl toodiscover veri kaynakları
## <a name="introduction"></a>Giriş
Azure veri Kataloğu kayıt ve bulma kurumsal veri kaynakları için bir sistem görevi gören bir tam olarak yönetilen bir bulut hizmetidir. Diğer bir deyişle, Bul, anlamak ve veri kaynaklarını kullanan kişilerin veri Kataloğu yardımcı olur ve daha fazla değer, var olan verilerden alma kuruluşlar yardımcı olur. Bir veri kaynağına veri Kataloğu ile kaydedildikten sonra böylece toodiscover hello verileri kolayca arayabilirsiniz meta verilerini hello hizmeti tarafından dizine alınır.

## <a name="searching-and-filtering"></a>Arama ve filtreleme
Veri Kataloğu bulma işlemi iki birincil mekanizmayı kullanır: arama ve filtreleme.

Arama hem sezgisel hem de güçlü tasarlanmış toobe olur. Varsayılan olarak, arama terimleri kullanıcı tarafından ek açıklamalar dahil olmak üzere hello kataloğunda herhangi bir özellikle eşleştirilir.

Filtreleme tasarlanmıştır toocomplement arama. Uzmanlar, veri kaynağı türü, nesne türü ve etiketler gibi belirli özellikleri seçebilirsiniz. Yalnızca eşleşen veri varlıklarını görüntülemek ve arama sonuçları toomatching varlıklar sınırlayın.

Arama ve filtreleme, bir birleşimini kullanarak, gereksinim duyduğunuz veri Kataloğu toodiscover hello veri kaynaklarıyla kayıtlı hello veri kaynaklarına hızlıca gidebilirsiniz.

## <a name="search-syntax"></a>Söz dizimi arama
Merhaba varsayılan serbest metin arama basit ve sezgisel olsa da, veri kataloğu arama söz dizimi hello arama sonuçları üzerinde daha fazla denetim için de kullanabilirsiniz. Teknikleri izleyerek veri kataloğu arama destekler hello:

| Teknik | Kullanım | Örnek |
| --- | --- | --- |
| Basit Arama |Bir veya daha fazla arama terimi kullanan basit arama. Sonuçlar herhangi bir özelliği bir veya daha fazla belirtilen hello koşulları ile eşleşen tüm varlıkları içerir. |`sales data` |
| Özellik kapsamı |Belirtilen özelliği yalnızca dönüş veri kaynaklarının nerede hello arama terimi hello ile eşleştirilir. |`name:finance` |
| Boole işleçleri |Genişletmek veya bir aramayı Boole işleçleri kullanarak daraltın. |`finance NOT corporate` |
| Parantez ile gruplandırma |Parantez toogroup bölümleri hello sorgu tooachieve mantıksal ayırma, özellikle Boole işleçleri ile birlikte kullanın. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Karşılaştırma işleçleri |Sayısal ve tarih veri türlerine sahip özellikler için eşitlik dışındaki karşılaştırmaları kullanın. |`modifiedTime > "11/05/2014"` |

Veri kataloğu arama hakkında daha fazla bilgi için bkz: Merhaba [Azure veri Kataloğu](https://msdn.microsoft.com/library/azure/mt267594.aspx) makalesi.

## <a name="hit-highlighting"></a>İsabet vurgulama
Arama sonuçları görüntülediğinizde, herhangi bir belirtilen hello eşleşen özelliklere görüntülenen arama terimleri (örneğin, hello veri varlık adı, açıklama ve etiketleri) olan vurgulanan toomake, verilen veri varlık tarafından verilen bir arama döndürülen neden daha kolay tooidentify.

> [!NOTE]
> isabet vurgulama, kullanım hello kapalı tooturn **vurgulayın** hello veri Kataloğu portalında geçin.
>
>

Arama sonuçları görüntülediğinizde, bir veri varlığına bile isabet etkin vurgulama içindedir neden bu her zaman belirgin olmayabilir. Tüm özellikleri varsayılan olarak aranır olduğundan, bir veri varlığına bir eşleşme nedeniyle bir sütun düzeyinde özellik döndürülmesi. Ve birden çok kullanıcı kendi etiketleri ve açıklamaları ile kayıtlı veri varlıklarına açıklama çünkü tüm meta veri hello arama sonuçları listesinde görüntülenebilir.

Merhaba varsayılan döşeme görünümü'nde hello arama sonuçlarında görüntülenen her bölme içerir bir **görünüm arama terimini** simgesi istiyorsanız, hızlı bir şekilde hello sayısı eşleşiyor ve konum ve toojump toothem görüntüleyebilmesi için.

 ![İsabet vurgulama ve hello Azure veri Kataloğu Portalı'nda arama sonuçları](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Özet
Veri Kataloğu kopyalarla yapısal ve açıklayıcı bir veri kaynağı kaydetme çünkü hello veri meta verilerini kaynak toohello katalog hizmeti, hello veri kaynağını daha kolay toodiscover haline gelir ve anlama. Bir veri kaynağı kaydınız sonra filtreleme kullanarak bulmak ve gelen hello veri Kataloğu portalını arayın.

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında adım adım ayrıntılar için toodiscover veri kaynaklarını görmek [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md).
