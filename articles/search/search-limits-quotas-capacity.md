---
title: "Azure Search'te aaaService sınırları | Microsoft Docs"
description: "Kapasite planlama için kullanılan hizmet sınırları ve istekleri ve yanıtları Azure arama için en fazla sınırlandırır."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Azure Search hizmet sınırları
Maksimum depolama, iş yükleri ve dizinler, belgeler, miktarda sınırlar ve bağımlı nesneler olup olmadığına göre [Azure Search sağlamak](search-create-service-portal.md) adresindeki bir **serbest**, **temel**, veya **Standart** fiyatlandırma katmanı.

* **Ücretsiz** Azure aboneliğinizle birlikte gelen bir çok kiracılı paylaşılan bir hizmettir. Bu özel kaynakları için kaydolmadan önce hello hizmetiyle tooexperiment sağlayan bir ek-ücretsiz varolan aboneleri için seçenektir.
* **Temel** daha küçük ölçekli üretim iş yükleri için özel bilgi işlem kaynakları sağlar.
* **Standart** her düzeydeki daha fazla depolama ve işleme kapasitesi ile ayrılmış makinelerde çalışır. Standart gelen dört düzeyler: S1, S2, S3 ve S3 yüksek yoğunluklu (S3 HD).

> [!NOTE]
> Bir hizmeti belirli bir katman sağlanır. Toojump katmanları tooget fazla kapasite gerekiyorsa, yeni bir hizmet (hiçbir yerinde yükseltme yoktur) hazırlamanız gerekir. Daha fazla bilgi için bkz: [bir SKU katmanı seçin veya](search-sku-tier.md). bir hizmet kapasitesiyle ayarlama hakkında daha fazla toolearn zaten sağladığınız bkz [ölçeklendirme sorgu ve dizin oluşturma iş yükleri için kaynak düzeylerini](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Abonelik sınırları
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Hizmet sınırları
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Dizin sınırları
Dizinleri sınırları ve dizin oluşturucular sınırları arasında bire bir ilişkisi yok. Bir sınırı 200 dizinleri verildiğinde, hello üst sınır dizin oluşturucular için de hello için 200: aynı hizmet.

| Kaynak | Ücretsiz | Temel | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Dizini: dizin başına en fazla alan |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Dizin: dizin başına profilleri Puanlama maksimum |100 |100 |100 |100 |100 |100 |
| Dizini: Profil başına en fazla işlevleri |8 |8 |8 |8 |8 |8 |
| Dizin oluşturucular: çağrı başına en fazla dizin yükleme |10.000 belgeleri |Maksimum belge yalnızca sınırlıdır |Maksimum belge yalnızca sınırlıdır |Maksimum belge yalnızca sınırlıdır |Maksimum belge yalnızca sınırlıdır |YOK <sup>2</sup> |
| Dizin oluşturucular: en fazla çalışma süresini | 1-3 dakika <sup>3</sup> |24 saat |24 saat |24 saat |24 saat |YOK <sup>2</sup> |
| BLOB dizin oluşturucu: en fazla blob boyutu, MB |16 |16 |128 |256 |256 |YOK <sup>2</sup> |
| BLOB dizin oluşturucu: blob üzerinden ayıkladığınız içeriği en fazla karakter |32,000 |64,000 |4 milyon |4 milyon |4 milyon |YOK <sup>2</sup> |

<sup>1</sup> temel katman yalnızca SKU dizin başına 100 alanlarının alt sınırı ile Merhaba.

<sup>2</sup> S3 HD dizin oluşturucular şu anda desteklemiyor. Bu özellik için Acil bir gereksiniminiz varsa Azure desteğine başvurun.

<sup>3</sup> hello ücretsiz katmanı için maksimum yürütme süresini dizin oluşturucu olan 3 dakika blob kaynaklarının ve diğer tüm veri kaynakları 1 dakikadır.

## <a name="document-size-limits"></a>Belge boyutu sınırları
| Kaynak | Ücretsiz | Temel | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Dizin API başına belgenin boyutu |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |

Bir dizin API çağrılırken toohello en fazla belge boyutu ifade eder. Belge, gerçekte bir hello dizin API istek gövdesi hello boyutu sınırı boyutudur. Aynı anda birden çok belge toohello dizin API toplu geçirebilirsiniz beri hello boyut sınırı gerçekte kaç belgeleri hello toplu işlemde bağlıdır. Bir toplu işin için tek bir belgenin, JSON 16 MB hello en fazla belge boyutudur.

Aşağı tookeep belge boyutu hello isteğinden tooexclude sorgulanabilir olmayan veri unutmayın. Görüntüleri ve diğer ikili veriler doğrudan sorgulanabilir değildir ve hello dizininde depolanan döndürmemelidir. Arama sonuçları, sorgulanabilir olmayan verileri toointegrate URL başvuru toohello kaynağına depolar yapılamayan bir alan tanımlayın.

## <a name="workload-limits-queries-per-second"></a>İş yükü sınırları (sorguları saniye başına)
| Kaynak | Ücretsiz | Temel | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |Yok |Çoğaltma başına yaklaşık 3 |Çoğaltma başına yaklaşık 15 |Çoğaltma başına yaklaşık 60 |Çoğaltma başına yaklaşık >60 |Çoğaltma başına yaklaşık >60 |

Sorgular (QPS) saniyede benzetimli ve gerçek müşteri iş yükleri tahmini tooderive değerleri kullanarak buluşsal yöntemler üzerinde göre yaklaşık olur. Tam QPS verimlilik, hello sorgu veri ve hello doğasına bağlı olarak değişir.

Yukarıda verilen kaba tahminleri gerçek hızı, özellikle de serbest paylaşılan nerede işleme kullanılabilir bant genişliğini ve sistem kaynakları için rekabet dayanır hizmeti hello zor toodetermine olsa da. QPS çözümünüz için her zaman kaç diğer iş yüklerini hello çalıştıran bağlı olarak farklılık gösterir şekilde hello ücretsiz katmanında birden çok abone tarafından işlem ve depolama kaynaklarını paylaşılan aynı anda.

Merhaba parametrelerinin daha fazla denetime sahip olduğundan hello standart düzeyinde, daha fazla QPS yakından tahmin edebilirsiniz. Merhaba en iyi yöntemler bölümüne bakın [arama çözümünüzü yönetme](search-manage.md) nasıl hakkında yönergeler için iş yükleri için toocalculate QPS.

## <a name="api-request-limits"></a>API istek sınırları
* İstek başına 16 MB maksimum <sup>1</sup>
* 8 KB URL uzunluğu üst sınırı
* Dizinin toplu iş başına en fazla 1000 belge karşıya yükler, birleştirir veya siler
* $Orderby tümcesinde en çok 32 alanları
* En fazla arama terimi 32.766 bayt sayısı (2 bayt eksi 32 KB) UTF-8 ile kodlanmış metnin boyutudur

<sup>1</sup> olarak Azure arama, istek gövdesini hello olan konu tooan hello içeriği tek tek alanların veya teorik sınırları sınırlı olduğu değil koleksiyonları pratik bir sınırı etkileyici 16 MB sayısı üst sınırı (bkz [destekleniyor veri türleri](https://msdn.microsoft.com/library/azure/dn798938.aspx) alan birleşim ve kısıtlamaları hakkında daha fazla bilgi için).

## <a name="api-response-limits"></a>API yanıtını sınırları
* Döndürülen arama sonuçlarını sayfa başına en fazla 1000 belge
* Önermek API istek döndürülen en fazla 100 önerileri

## <a name="api-key-limits"></a>API anahtarı sınırları
Api anahtarlarından hizmetini kimlik doğrulaması için kullanılır. İki tür vardır. Yönetici anahtarları hello istek başlığında belirtilen ve tam okuma-yazma erişimi toohello hizmeti verin. Sorgu anahtarları hello URL ve genellikle dağıtılmış tooclient uygulamalar belirtilen salt okunur.

* En fazla hizmeti başına 2 yönetici anahtarları
* En fazla hizmeti başına 50 sorgu anahtarları
