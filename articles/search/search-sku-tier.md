---
title: "aaaChoose bir SKU veya Azure arama için fiyatlandırma katmanı | Microsoft Docs"
description: "Azure arama sırasında bu SKU'ları sağlanabilir: ücretsiz, temel ve standart, standart olduğu çeşitli kaynak yapılandırmaları ve kapasite düzeyleri kullanılabilir."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Azure Search için SKU veya fiyatlandırma katmanı seçme
Azure Search'te bir [hizmet sağlandığına](search-create-service-portal.md) belirli fiyatlandırma katmanı veya SKU. Seçenekleriniz **serbest**, **temel**, veya **standart**, burada **standart** birden çok yapılandırmaları ve kapasiteleri kullanılabilir.

Bu makalede Hello amacı bir katmanı seçin toohelp budur. Bir katmanın kapasitesini toobe çok düşük kapatırsa, tooprovision hello daha yüksek katman en yeni bir hizmet gerekir ve dizinleri yeniden yükleyin. Aynı bir SKU tooanother hizmet hello hiçbir yerinde yükseltmesini yoktur.

> [!NOTE]
> Bir katman seçtikten sonra ve [bir arama hizmeti sağlamak](search-create-service-portal.md), çoğaltma artırabilir ve bölüm hello Hizmeti'nde sayar. Yönergeler için bkz [ölçeklendirme sorgu ve dizin oluşturma iş yükleri için kaynak düzeylerini](search-capacity-planning.md).
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>Nasıl karar tooapproach bir fiyatlandırma katmanı
Azure Search'te hello katman kapasitesi, Özellik kullanılabilirliği belirler. Genellikle, özellikleri her katmanını Önizleme özellikleri dahil olmak üzere, kullanılabilir. Merhaba S3 HD dizin oluşturucular desteği işlemdir.

> [!TIP]
> Her zaman sağlamanızı öneririz bir **serbest** hizmet (abonelik, süre sonu olmayan her bir) böylece kendi kullanıma hazır hafif projeleri için. Kullanım hello **serbest** ; ikinci Faturalanabilir hizmet hello oluşturma hizmeti sınama ve değerlendirme için **temel** veya **standart** katmanı üretim ya da daha büyük test iş yükleri için.
>
>

Kapasite ve hello hizmetini çalıştıran maliyetlerini el eldeki gidin. Bu makaledeki bilgileri, SKU hello doğru dengeyi sunar karar vermenize yardımcı olabilir, ancak bunu herhangi toobe yararlı hello aşağıdaki üzerinde en az kaba tahminleri gerekir:

* Sayısını ve boyutunu dizinlerini toocreate planlama
* Sayısını ve boyutunu belgeleri tooupload
* Bazı fikir sorgu biriminin bakımından sorguları başına ikinci (QPS)

Bir sabit sınır hello sayısı dizinleri ya da hizmet belgeler veya hello hizmeti tarafından kullanılan kaynakları (depolama veya çoğaltmaları) aracılığıyla maksimum sınırlarına ulaştığından sayısını ve boyutunu önemlidir. Merhaba hizmetiniz için gerçek sınırı hangisi ilk kullanılır: kaynakları veya nesneler.

Tahminler el de, aşağıdaki adımları hello hello işlemini basitleştirmek:

* **1. adım** toolearn kullanılabilir seçenekler hakkında aşağıda hello SKU açıklamaları gözden geçirin.
* **2. adım** hello soruları tooarrive ön karar en altında.
* **3. adım** kararınız depolama sabit sınırlara gözden geçirme ve fiyatlandırma sonlandır.

## <a name="sku-descriptions"></a>SKU açıklamaları
Aşağıdaki tablonun hello her katman açıklamalarını sağlar.

| Katman | Birincil senaryolar |
| --- | --- |
| **Boş** |Değerlendirme, araştırma ya da küçük iş yükleri için kullanılan ücret ödemeden, paylaşılan bir hizmet. Diğer aboneleriyle paylaşıldığından, sorgu işleme ve dizin oluşturma başka Kime hello hizmetinin kullandığı göre değişir. Kapasite Küçük (50 MB 10.000 ile 3 dizinlerini belgeleri veya her). |
| **Temel** |Ayrılmış donanım üzerinde küçük üretim iş yükleri. Yüksek oranda kullanılabilir. Kapasite too3 çoğaltmaları ve 1 bölüm (2 GB) ' dir. |
| **S1** |Standart 1 (12) bölümler ve çoğaltmalar (12), ayrılmış donanım üzerinde Orta üretim iş yükleri için kullanılan esnek birleşimlerini destekler. Bölümleri ve en çok 36 Faturalanabilir arama birimi sayısı tarafından desteklenen birleşimleri yinelemede ayırabilirsiniz. Bu düzeyde bölümleri 25 GB ve QPS saniyede yaklaşık 15 sorgular. |
| **S2** |Standart 2 S1 ancak büyük boyutlu bölümler ve çoğaltmalar Merhaba aynı 36 arama birimi kullanarak büyük üretim iş yükleri çalışır. Bu düzeyde bölümleri 100 GB ve QPS saniyede yaklaşık 60 sorgular. |
| **S3** |Standart 3 orantılı olarak büyük üretim iş yükleri daha yüksek son sistemlerde too12 bölümleri veya 12 çoğaltmaları yapılandırmalarını altında 36 arama birimi çalıştırır. Bu düzeyde bölümleri 200 GB ve QPS saniye başına birden fazla 60 sorgular. |
| **S3 HD** |Standart 3 yüksek yoğunluklu, çok sayıda küçük dizinler için tasarlanmıştır. 200 GB too3 bölümleri yukarı sahip olabilir. QPS, saniye başına birden fazla 60 sorgudur. |

> [!NOTE]
> Çoğaltma ve bölüm üst sınırlar, çıkışı, hangi hello maksimum nominal değerde gelir daha etkili bir alt limit uygular (36 birim başına en fazla), arama birimi olarak faturalandırılır. Örneğin, toouse hello en fazla 12 çoğaltmalar, en fazla 3 bölümleri olabilir (12 * 3 = 36 birimleri). Benzer şekilde, toouse en büyük bölümleri, çoğaltmaları too3 azaltın. Bkz: [ölçeklendirme sorgu ve iş yüklerini Azure Search'te dizin oluşturma için kaynak düzeylerini](search-capacity-planning.md) izin verilen birleşimleri grafikte için.
>
>

## <a name="review-limits-per-tier"></a>Katman başına sınırları gözden geçirin
Merhaba aşağıdaki grafikte bir alt hello sınırlamaları uygulanmaya kümesidir [Azure Search hizmet sınırları](search-limits-quotas-capacity.md). Merhaba faktörler büyük olasılıkla tooimpact SKU karar listeler. Aşağıdaki hello sorular gözden geçirirken toothis grafik başvurabilir.

| Kaynak | Ücretsiz | Temel | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Hizmet Düzeyi Sözleşmesi (SLA) |Hayır <sup>1</sup> |Evet |Evet |Evet |Evet |Evet |
| Dizin sınırları |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Belge sınırları |toplam 10.000 |hizmeti başına 1 milyon |Bölüm başına 15 milyon |Bölüm başına 60 milyon |Bölüm başına 120 milyon |Dizin başına 1 milyon |
| En fazla bölümleri |Yok |1 |12 |12 |12 |3 <sup>2</sup> |
| Bölüm boyutu |50 MB Toplam |Hizmeti başına 2 GB |Bölüm başına 25 GB |(Yukarı hizmeti başına 1.2 TB maksimum tooa) bölüm başına 100 GB |(Yukarı hizmeti başına tooa maksimum 2.4 TB) bölüm başına 200 GB |200 GB (yukarı hizmeti başına tooa en fazla 600 GB) |
| En fazla yineleme |Yok |3 |12 |12 |12 |12 |
| Saniye başına sorguları |Yok |Çoğaltma başına yaklaşık 3 |Çoğaltma başına yaklaşık 15 |Çoğaltma başına yaklaşık 60 |Çoğaltma başına yaklaşık >60 |Çoğaltma başına yaklaşık >60 |

<sup>1</sup> ücretsiz katmanı ve önizleme özellikleri hizmet düzeyi sözleşmelerine (SLA) ile gelen değil. Hizmetiniz için yeterli artıklık sağladığınızda tüm Faturalanabilir katmanları için SLA etkili olur. İki veya daha fazla çoğaltmaları için (okuma) sorgu SLA gereklidir. Üç veya daha fazla çoğaltmalar, sorgu ve dizin oluşturma (okuma-yazma) SLA için gereklidir. bölüm sayısı Hello bir SLA önem verilmez. 

<sup>2</sup> S3 ve S3 HD aynı yüksek kapasiteli altyapısı tarafından yedeklenmiş ancak her biri farklı şekillerde maksimum sınırına ulaştığında. S3 çok büyük dizinler daha az sayıda hedefler. Bu nedenle, kaynak bağlı kendi üst sınır: (her hizmet için 2.4 TB). S3 HD çok sayıda çok küçük dizinleri hedefler. 1.000 dizinleri S3 HD sınırlarına dizin kısıtlamalarını hello biçiminde ulaşır. 1. 000'den fazla dizinler gerektiren bir S3 HD müşterisiyseniz, hakkında bilgi için Microsoft Support başvurun tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Gereksinimlerine uymayan SKU'ları ortadan kaldırma
Aşağıdaki sorular hello hello doğru SKU seçim, iş yükü için en gelmesini yardımcı olabilir.

1. Elinizde **hizmet düzeyi sözleşmesi (SLA)** gereksinimleri? Herhangi bir Faturalanabilir katmanı kullanabilirsiniz (temel üzerinde yukarı), ancak hizmetiniz artıklık için yapılandırmanız gerekir. İki veya daha fazla çoğaltmaları için (okuma) sorgu SLA gereklidir. Üç veya daha fazla çoğaltmalar, sorgu ve dizin oluşturma (okuma-yazma) SLA için gereklidir. bölüm sayısı Hello bir SLA önem verilmez.
2. **Kaç tane dizinler** gerektiriyor mu? Bir SKU karar Finansman hello büyük değişkenlerinden biri hello her SKU tarafından desteklenen dizinleri sayısıdır. Dizin destek hello alt belirtmeyecektir farklı düzeylerde fiyatlandırma katmanlarına. Dizin sayısı gereksinimlerine SKU karar birincil bir etken olabilir.
3. **Kaç tane belgeleri** her dizine yüklenir? hello sayısını ve boyutunu belgelerin hello nihai hello dizin boyutunu belirler. Tahmin edebilirsiniz varsayılarak hello dizin tahmini boyutunu Merhaba, bu numarayı hello bölüm boyutu bu boyut dizini bölümleri gerekli toostore hello sayısına göre genişletilmiş SKU başına karşı karşılaştırabilirsiniz.
4. **Merhaba beklenen sorgu yük nedir**? Depolama gereksinimleri anladım sonra sorgu iş yükleri göz önünde bulundurun. S2 ve her iki S3 SKU'ları eşdeğer yakın verimlilik sağlar, ancak SLA gereksinimleri herhangi Önizleme SKU'ları kural.
5. Merhaba S2 ve S3 katman düşünüyorsanız, gerekip gerekmediğini belirleme [dizin oluşturucular](search-indexer-overview.md). Dizin oluşturucular henüz hello S3 HD katmanı için kullanılabilir değildir. Alternatif dizin güncelleştirmeleri için bir gönderme modeli toouse burada uygulama kodu toopush bir veri kümesi tooan dizini yazma yaklaşımdır.

Müşterilerin çoğu, kullanıcıların yanıtları toohello sorular yukarıda göre veya belirli bir SKU çıkarabilirsiniz. Hala ile hangi SKU toogo emin değilseniz, sorular tooMSDN veya StackOverflow forumlarına gönderin veya daha ayrıntılı yönergeler için Azure desteğine başvurun.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>Karar doğrulama: hello SKU yeterli depolama alanı ve QPS sunar?
Son adım olarak, hello yeniden ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/search/) ve hello [hizmet sınırları hizmeti başına ve dizin başına bölümlerde](search-limits-quotas-capacity.md) toodouble onay aboneliği ve hizmet sınırları karşı tahmin eder.

Sınırların dışında ya da hello fiyat veya depolama alanı gereksinimleri varsa, birden çok daha küçük hizmetleri arasında toorefactor hello iş yüklerini (örneğin) isteyebilirsiniz. Daha ayrıntılı bir düzeyde, dizinleri toobe küçük yeniden tasarlamanız veya toomake sorguları daha verimli kullanım filtreler.

> [!NOTE]
> Belgeleri yabancı veri içeriyorsa depolama gereksinimleri aşırı inflated olabilir. İdeal olarak, belgeler, yalnızca aranabilir verileri veya meta veriler içerir. İkili veriler yapılamayan ve ayrı olarak (belki de bir Azure tablo veya blob depolama alanında) hello dizin toohold bir URL başvuru toohello dış veri alanında ile depolanması gerekir. tek bir belgenin Hello en büyük boyutu 16 MB (veya daha az ise, toplu bir istek birden çok belgeyi karşıya yükleme). Bkz: [hizmet sınırları Azure Search'te](search-limits-quotas-capacity.md) daha fazla bilgi için.
>
>

## <a name="next-step"></a>Sonraki adım
Üzerinde sağ sığacak hello SKU olan öğrendikten sonra bu adımlarla devam edin:

* [Merhaba Portalı'nda arama hizmeti oluşturun](search-create-service-portal.md)
* [Bölümler ve çoğaltmalar tooscale Hello ayrılması hizmetinizi değiştirme](search-capacity-planning.md)
