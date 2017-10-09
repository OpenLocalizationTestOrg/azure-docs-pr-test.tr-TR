---
title: "aaaHow tooannotate veri kaynakları | Microsoft Docs"
description: "Nasıl tooarticle vurgulama nasıl tooannotate veri varlıklarını kolay adlar, etiketler, açıklamalar ve uzmanlar dahil olmak üzere Azure veri Kataloğu."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Nasıl tooannotate veri kaynakları
## <a name="introduction"></a>Giriş
**Microsoft Azure veri Kataloğu** bir kayıt ve sistemi kurumsal veri kaynakları için bulma görevi gören bir tam olarak yönetilen bir bulut hizmetidir. Diğer bir deyişle, veri Kataloğu tüm bulmak, anlamak ve veri kaynaklarını kullanan kişilerin ve kuruluşların tooget daha fazla değer, var olan verilerden hakkındadır. Bir veri kaynağına veri Kataloğu ile kaydedildikten sonra meta verilerini kopyalanır ve hello hizmeti tarafından dizine ancak hello Öykü yok sonlanmıyor. Daha fazla anlaşılabilir toomore kişiler toomake hello veri kaynağı ve veri Kataloğu kullanıcılara tooprovide hello veri kaynağından ayıklanan kendi – açıklamaları ve etiketleri gibi– açıklayıcı meta verilerin toosupplement hello meta veri sağlar.

## <a name="annotation-and-crowdsourcing"></a>Ek açıklama ve kitle kaynak
Herkesin bir fikir vardır. Ve bu iyi bir şeydir.
Veri Kataloğu, farklı kullanıcıların farklı perspektiflerini kurumsal veri kaynakları varsa ve her bu Perspektifleri değerli olabileceğini tanır. Senaryo aşağıdaki hello göz önünde bulundurun:

* Hello Sistem Yöneticisi, ana bilgisayar hello veri kaynağı hello sunucular veya hizmetler için hizmet düzeyi sözleşmesi hello bilir.
* Merhaba veritabanı yöneticisi, her veritabanı için zamanlama ve izin verilen ETL işleme windows hello hello yedekleme bilir.
* Merhaba sistem sahibine kullanıcıları toorequest erişim toohello veri kaynağı için hello işlem bilir.
* Merhaba veri steward nasıl hello varlıklar ve öznitelikler hello veri kaynağındaki toohello kurumsal veri modeli eşleme bilir.
* Merhaba analist hello verilerin hello kendisinin destekleyen hello iş süreçlerini bağlamında nasıl kullanıldığını bilir.

Her bu Perspektifleri değerlidir ve her bir toobe yakalanan ve tooprovide kayıtlı veri kaynaklarının eksiksiz bir görünümünü kullanılan izin veren bir kitle kaynak yaklaşımı toometadata veri kataloğu kullanır. Merhaba veri Kataloğu portalını kullanarak, her bir kullanıcı ekleyin ve diğer kullanıcılar tarafından sağlanan mümkün tooview ek açıklamaları devam ederken kendi ek açıklamalarını düzenleyin.

## <a name="different-types-of-annotations"></a>Farklı türde ek açıklamaların
Veri Kataloğu destekler hello şu açıklamalarının türlerini:

| Ek açıklama | Notlar |
| --- | --- |
| Kolay ad |Kolay adlar toomake hello veri varlıklarını daha kolay anlaşılan hello veri varlık düzeyinde sağlanabilir. Merhaba temel alınan nesnenin adı şifreli, kısaltılmış veya aksi halde anlamlı toousers olduğunda kolay adlar en yararlı olur. |
| Açıklama |Açıklamaları sağlanan hello veri varlığına ve öznitelik / sütun düzeyi. Merhaba veri varlığına hello kullanıcının Perspektif veya kullanımını açıklayan serbest biçimli kısa metin ek açıklamaları açıklamalardır. |
| Etiketler (kullanıcı etiketleri) |Etiketler sağlanan hello veri varlığına ve öznitelik / sütun düzeyi. Kullanıcı, kullanılan toocategorize veri varlıklarını veya öznitelikleri olabilir ve kullanıcı tanımlı etiketleri etiketleridir. |
| Etiketler (sözlüğü etiketleri) |Etiketler sağlanan hello veri varlığına ve öznitelik / sütun düzeyi. Kullanılan toocategorize veri varlıklarını veya ortak bir iş sınıflandırması kullanarak özniteliklerini olabilen merkezi olarak tanımlanması terimler sözlüğü etiketleridir. Daha fazla bilgi için bkz: [nasıl tooset yukarı hello iş sözlüğünü yönetilen etiketleme için](data-catalog-how-to-business-glossary.md) |
| Uzmanlar |Uzmanlar hello veri varlık düzeyinde sağlanabilir. Uzmanlar hello veri Uzman perspektiflerine sahip kullanıcıları veya grupları tanımlayın ve hello Bul kullanıcılar için iletişim noktaları kayıtlı veri kaynaklarını ve hello var olan ek açıklamaları tarafından bulamadığınız sorularınız varsa gibi hizmet verebilir. |
| Erişim isteği |İstek erişim bilgileri hello veri varlık düzeyinde sağlanabilir. Bu bilgiler, henüz izinleri tooaccess olmadığı, bir veri kaynağını Bul kullanıcılar için olur. Kullanıcıların hello kullanıcının veya grubun erişim verir, URL hello işleminin hello veya bu kullanıcıların toogain erişmeniz aracı veya hello işlemin kendisi metin olarak girebilirsiniz hello e-posta adresini girebilirsiniz. |
| Belgeler |Belge hello veri varlık düzeyinde sağlanabilir. Varlık belgeleri, bağlantılar ve resimler içerebilir ve etiketleri ve açıklamaları ile ilettiği olmayan herhangi bir bilgi sağlayan zengin metin bilgilerdir. |

## <a name="annotating-multiple-assets"></a>Birden çok varlıklarına açıklama
Birden fazla veri varlığına hello veri Kataloğu portalında seçerken, kullanıcılar tek bir işlemde tüm seçili varlıklar açıklama ekleyebilirsiniz. Ek açıklamalar seçili tooall varlıklar, kolay tooselect yapma uygulanır ve ilgili veri varlıkları için etiketleri ve uzmanlar kümesini ve tutarlı bir açıklama sağlayın.

> [!NOTE]
> Kayıt aracını kullanarak Hello veri Kataloğu veri kayıt veri varlıklarını kaynaktaki etiketleri ve uzmanlar de girilebilir.
>
>

Ne zaman birden çok tablo ve görünümler, yalnızca sütunlara tüm varlıklar ortak olan veri seçilen seçerek hello veri Kataloğu Portalı'nda görüntülenir. Bu, seçilen tüm varlıklar için kullanıcılar tooprovide etiketleri ve açıklamaları hello aynı ad ile tüm sütunlar için sağlar.

## <a name="annotations-and-discovery"></a>Ek açıklamalar ve bulma
Yalnızca hello toohello veri kataloğu arama dizini kayıt sırasında hello veri kaynağından ayıklanan meta verileri eklenir, kullanıcı tarafından sağlanan meta verileri de dizinlenir. Bunun anlamı yalnızca ek açıklamaları bunlar Bul kullanıcılar toounderstand hello veri kolaylaştırmak için yapmak, ek açıklamaları aynı zamanda kullanıcıların toodiscover açıklama hello veri varlıkları için anlamlı toothem olun hello koşullarını kullanarak arama kolaylaştırır.

## <a name="summary"></a>Özet
Veri Kataloğu ile veri kaynağı kaydetme verileri bulunabilirlik katalog hizmeti hello hello veri kaynağından yapısal ve açıklayıcı meta verileri kopyalayarak hale getirir. Bir veri kaynağı kaydedildikten sonra kullanıcılar ek açıklamaları toomake daha kolay toodiscover sağlayın ve gelen hello veri Kataloğu portalını anlayın.

## <a name="see-also"></a>Ayrıca bkz.
* [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md) hakkında adım adım ayrıntılar için öğretici tooannotate veri kaynakları.
