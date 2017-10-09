---
title: "aaaAzure, cool, sık erişimli ve arşivleme için BLOB Depolama | Microsoft Docs"
description: "Azure Blob depolama hesapları için yoğun erişimli, seyrek erişimli ve arşiv depolaması"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: eb33ed4f-1b17-4fd6-82e2-8d5372800eef
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/05/2017
ms.author: mihauss
ms.openlocfilehash: 42fb699bf16147ba8a4d9f75a62debadea5af65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-blob-storage-hot-cool-and-archive-preview-storage-tiers"></a>Azure Blob Depolama: Yoğun erişimli, seyrek erişimli ve arşiv (önizleme) depolama katmanları

## <a name="overview"></a>Genel Bakış

Verilerinizi, nasıl kullandığınıza bağlı olarak en uygun maliyetli şekilde depolayabilmeniz için Azure Depolama, Blob nesne depolama için üç depolama katmanı sunuyor. Hello Azure **sık erişimli depolama katmanı** sık erişilen verileri depolamak için optimize edilmiştir. Hello Azure **seyrek erişimli depolama katmanı** seyrek erişilen ve en az bir ay için depolanan verileri depolamak için optimize edilmiştir. Merhaba [arşiv depolama katmanı (Önizleme)](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) seyrek erişilen ve en az altı ay boyunca esnek gecikme gereksinimlerine (Merhaba sırası saat) ile depolanan verileri depolamak için optimize edilmiştir. Merhaba *arşiv* depolama katmanı, yalnızca hello blob düzeyinde ve hello tüm depolama hesabı üzerinde kullanılabilir. Merhaba seyrek erişimli depolama katmanındaki veriler, biraz daha düşük bir kullanılabilirliği kabul edebilir, ancak hala yüksek dayanıklılık ve erişimli veriler kadar benzer zamanı erişimi ve işleme özelliklerini gerektirir. Seyrek erişimli ve arşiv verileri için, biraz daha düşük kullanılabilirlik SLA'sı ve yüksek erişim maliyetleri, çok daha düşük depolama maliyetleri için kabul edilebilir tercihlerdir.

Bugün, hello bulutta depolanan veriler büyük bir hızla artmaktadır. toomanage artan depolama ihtiyaçlarınızın maliyetlerini, verilerinizi erişim sıklığı gibi özniteliklerini temel alarak ve saklama dönemi planlanan yararlı tooorganize. Merhaba bulutta depolanan veriler nasıl onu oluşturulur, işlendiği ve yaşam süresi boyunca erişilen bakımından farklı olabilir. Bazı veriler ve yaşam süresi boyunca aktif şekilde erişilebilir ve değiştirilebilir. Bazı veriler büyük ölçüde hello veri yaş bırakarak erişimle, yaşam sürelerinin başlarında sık erken erişilir. Bazı veriler hello bulutta boşta kalır ve nadiren, herhangi bir zamanda, bir kez erişilen durumunda depolanan.

Bu veri senaryolarının her biri, belirli erişim düzeni için optimize edilmiş olan farklı hale getirilmiş bir depolama katmanından faydalanır. Sık erişimli, seyrek erişimli ve arşiv depolama katmanlarının kullanılmaya başlanmasıyla, Azure Blob Depolama farklı fiyatlandırma modelleriyle bu ayrılmış depolama katmanları ihtiyacına hitap ediyor.

## <a name="blob-storage-accounts"></a>Blob Storage hesapları

**Blob Storage hesapları**, yapılandırılmamış verilerinizi bloblar (nesneler) olarak Azure Storage’da depolamanıza yönelik özel depolama hesaplarıdır. Blob Depolama hesaplarıyla, artık hot seçebilirsiniz ve seyrek erişimli depolama katmanları hesap düzeyinde veya çalışırken, seyrek erişimli ve katmanları düzeyinde erişim düzenlerini esas alarak hello blob, arşiv. Seyrek erişilen soğuk verilerinizi hello en düşük depolama maliyeti, sık erişimli ve daha sık erişilen sık erişimli verilerinizi daha hello düşük erişim maliyetiyle depolamak daha maliyeti daha düşük depolama sık erişilen seyrek erişimli verilerinizi daha az depolar. BLOB storage hesapları benzer tooyour varolan genel amaçlı depolama hesapları ve tüm hello harika dayanıklılık, kullanılabilirlik, ölçeklenebilirlik ve blok blobları için yüzde 100 API tutarlığı dahil Günümüzde, kullandığınız performans özelliklerini paylaşır ve ekleme BLOB'ları.

> [!NOTE]
> Blob Storage hesapları yalnızca blok ve ilave bloblarını destekler, sayfa bloblarını desteklemez.

BLOB storage hesapları kullanıma hello **erişim katmanı** toospecify hello depolama katmanı olarak sağlayan öznitelik **etkin** veya **Cool** hello hello veriye bağlı olarak hesabı. Merhaba, verilerinizin kullanım düzeninde bir değişiklik varsa, aynı zamanda herhangi bir zamanda bu depolama katmanları arasında geçiş yapabilirsiniz. Merhaba arşiv Katmanı (Önizleme) yalnızca hello blob düzeyinde uygulanabilir.

> [!NOTE]
> Değişen hello depolama katmanı ek ücretlere neden olabilir. Merhaba bkz [fiyatlandırma ve faturalama](#pricing-and-billing) daha fazla ayrıntı için bölüm.

### <a name="hot-access-tier"></a>Sık erişim katmanı

Merhaba sık erişimli depolama katmanı için örnek kullanım senaryoları şunları içerir:

* Etkin kullanımda veya beklenen toobe (gelen okuma ve için yazılmış) sık erişilen verileri.
* İşlem ya da sonuçta geçiş toohello seyrek erişimli depolama katmanı için hazırlanan veriler.

### <a name="cool-access-tier"></a>Seyrek erişim katmanı

Merhaba seyrek erişimli depolama katmanı için örnek kullanım senaryoları şunları içerir:

* Kısa süreli yedekleme ve olağanüstü durum kurtarma veri kümeleri.
* Eski medya içeriği değil artık sık görüntülenmeyen ancak erişildiğinde hemen beklenen toobe kullanılabilir değildir.
* Daha fazla veri sonra işlemek üzere toplandığını sırada toobe gereken büyük veri kümeleri maliyet etkili bir şekilde depolanır. (*Örneğin*, bilimsel verilerin uzun süreli depolanması, üretim tesisinden alınan ham telemetri verileri)

### <a name="archive-access-tier-preview"></a>Arşiv erişim katmanı (önizleme)

[Arşiv depolama](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering) hello düşük depolama maliyeti ve daha yüksek veri alma karşılaştırıldığında maliyetleri toohot ve seyrek erişimli depolama sahiptir.

Bir blob arşiv deposunda olduğunda okunamaz, kopyalanamaz, üzerine yazılamaz ve değiştirilemez. Arşiv depolamasındaki blobların anlık görüntüsünü de alamazsınız. Ancak, varolan işlemleri toodelete kullanın, liste, blob özellikleri/meta verilerini almak veya, BLOB hello katmanını değiştirebilirsiniz. Arşiv depolama tooread verilerin ilk hello katmanı hello blob toohot veya cool değiştirmeniz gerekir. Bu işlem rehydration bilinir ve too15 saatleri toocomplete 50 GB'den küçük BLOB'lar için yukarı alabilir. Daha büyük bloblar için gereken ek süre hello blob üretilen iş sınırı ile değişir.

Rehydration sırasında Hello katmanı değiştiyse hello "Arşiv durumu" blob özelliği tooconfirm kontrol edebilirsiniz. Merhaba durumunu "rehydrate-bekleyen-için-sık erişimli" veya "rehydrate-bekleyen--seyrek" Merhaba hedef katmanına bağlı olarak okur. Tamamlama, hello "durum Arşiv" blob özelliği kaldırılır ve hello "erişim katmanı" blob özelliği hello seyrek veya sık erişimli katmanı yansıtır.  

Merhaba arşiv depolama katmanı için örnek kullanım senaryoları şunları içerir:

* Uzun süreli yedekleme, arşivleme ve olağanüstü durum kurtarma veri kümeleri.
* Son kullanılabilir biçime işlendikten sonra bile özgün (ham) veriler korunmalıdır. (*Örneğin*, kodlama diğer biçimlere dönüştürüldükten sonra ham medya dosyaları)
* Uyumluluk ve uzun süredir saklanan toobe gerekir ve ender erişilen arşiv verileri. (*Örneğin* güvenlik kamerası kayıtları, sağlık kuruluşları için eski röntgen/MRI çekimleri, finans hizmetleri için sesli kayıtlar ve müşteri görüşmesi dökümleri)

### <a name="recommendations"></a>Öneriler

Depolama hesapları hakkıında daha fazla bilgi için bkz. [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

Blok veya ilave blobu depolaması yalnızca gerektiren uygulamalar için Blob storage hesapları kullanılmasını öneririz, katmanlı depolama fiyatlandırma modelini hello tootake avantajlarından Ayrıştırılan. Ancak, bu şekilde toogo, genel amaçlı depolama hesapları olacaktır kullanarak burada hello gibi belirli koşullar altında mümkün olmayabilir anlama:

* Dosyaları ve bloblarınızın depolanan istiyorsanız aynı depolama hesabındaki hello veya toouse tabloları, kuyrukları, gerekir. Hiçbir teknik bir avantajı toostoring bu hello sahip, hello aynı paylaşılan anahtara dışında aynı hesabı yoktur.

* Yine toouse hello Klasik dağıtım modeli gerekir. BLOB storage hesapları yalnızca hello Azure Resource Manager dağıtım modeli kullanılabilir.

* Toouse sayfa bloblarını gerekir. Blob Storage hesapları sayfa bloblarını desteklemez. Sayfa bloblarını kullanmaya özel olarak ihtiyacınız yoksa, genelde blok bloblarını kullanılmasını öneriyoruz.

* Merhaba bir sürümünü kullanmanız [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) 2014-02-14 tarihinden önceki veya bir istemci kitaplığı sürümü ile alt 4.x ve uygulamanızı güncelleştirememeniz.

> [!NOTE]
> Blob depolama hesapları şu anda çoğu Azure bölgesinde desteklenmektedir.
 

## <a name="blob-level-tiering-feature-preview"></a>Blob düzeyinde katmanlama özelliği (önizleme)

BLOB düzeyi katmanlama şimdi sağlar, adlı tek bir işlem kullanılarak hello nesne düzeyinde verilerinizin toochange hello katmanı [ayarlamak Blob katmanı](/rest/api/storageservices/set-blob-tier). Kolayca hesapları arasında toomove veri gerek kalmadan hello erişim katmanı hello etkin, etkin olmayan arasında bir BLOB veya arşiv katmanları kullanım desenlerini değiştikçe değiştirebilirsiniz. Tüm katman değişiklikleri, bir blob arşivden yeniden doldurulma sırasında olmadığı sürece hemen gerçekleşir. BLOB'ları katmanları içinde birlikte bulunabilir tüm üç depolama alanında aynı hesap hello. Açıkça atanan bir katmanı yok blob hello katmanı hello hesap erişim katmanı ayarından devralır.

toouse Önizleme, bu özelliklerin hello hello yönergeleri izleyin [Azure Arşiv ve Blob düzeyi katmanlama blog duyuru](https://azure.microsoft.com/blog/announcing-the-public-preview-of-azure-archive-blob-storage-and-blob-level-tiering).

Merhaba izleyin blob düzeyi katmanlama için Önizleme sırasında uygulamak bazı kısıtlamalar listeler:

* ABD Doğu 2'de başarılı önizleme kayıt destek arşiv depolama sonrası oluşturulan yalnızca yeni blob depolama hesapları.

* Ortak bölgelerde başarılı önizleme kayıt destek blob düzeyi katmanlama sonrası oluşturulan yalnızca yeni blob depolama hesapları.

* Blob düzeyinde katmanlama ve arşiv depolaması yalnızca [LRS] (../ common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#locally-redundant-storage) depolaması içinde desteklenir. [GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#geo-redundant-storage) ve [RA-GRS](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#read-access-geo-redundant-storage) hello gelecekte desteklenecektir.

* Anlık görüntüler bir blob hello katmanını değiştiremeyebilir.

* Arşiv depolamasındaki bir blobu kopyalayamaz ve anlık görüntüsünü alamazsınız.

## <a name="comparison-of-hello-storage-tiers"></a>Merhaba depolama katmanları karşılaştırması

Aşağıdaki tablonun hello hello sık erişimli ve seyrek erişimli depolama katmanları karşılaştırması gösterir. Merhaba arşiv blob düzeyi katman Önizleme'de, bunun için hiçbir SLA olduğundan vardır.

| | **Sık erişimli depolama katmanı** | **Seyrek erişimli depolama katmanı** |
| ---- | ----- | ----- |
| **Kullanılabilirlik** | %99,9 | %99 |
| **Kullanılabilirlik** <br> **(RA-GRS okumaları)**| %99,99 | %99,9 |
| **Kullanım ücretleri** | Yüksek depolama maliyeti, düşük erişim ve işlem maliyetleri | Düşük depolama maliyeti, yüksek erişim ve işlem maliyetleri |
| **En düşük nesne boyutu** | Yok | Yok |
| **En az depolama süresi** | Yok | Yok |
| **Gecikme süresi** <br> **(Toofirst bayta kalan süre)** | milisaniye | milisaniye |
| **Ölçeklenebilirlik ve Performans Hedefleri** | Genel amaçlı depolama hesaplarıyla aynı | Genel amaçlı depolama hesaplarıyla aynı |

> [!NOTE]
> BLOB Depolama hesapları destek hello genel amaçlı depolama hesaplarıyla aynı performans ve ölçeklenebilirlik hedeflerini. Daha fazla bilgi için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).


## <a name="pricing-and-billing"></a>Fiyatlandırma ve Faturalama
BLOB storage hesapları, blob storage hello depolama katmanını temel alan için bir fiyatlandırma modelini kullanır. Blob storage hesabı kullanırken hello aşağıdaki fatura değerlendirmeleri geçerlidir:

* **Depolama maliyetleri**: Ayrıca toohello depolanan veri miktarına, veri depolama maliyetini hello hello depolama katmanına bağlı olarak değişir. Merhaba gigabayt başına maliyet, hello sık erişimli depolama katmanına hello seyrek erişimli depolama katmanı düşüktür.

* **Veri erişim maliyetleri**: hello seyrek erişimli depolama katmanındaki veriler için bir gigabayt başına veri erişim ücret okuma ve yazma işlemleri için ücretlendirilirsiniz.

* **İşlem maliyetleri**: Her iki katma için işlem başına ücret alınır. Ancak, hello işlem başına maliyet hello seyrek erişimli depolama katmanı hello sık erişimli depolama katmanına göre olandan yüksektir.

* **Coğrafi çoğaltma veri aktarımı maliyetleri**: Bu yalnızca tooaccounts coğrafi, GRS ve RA-GRS dahil olmak üzere çoğaltma yapılandırılmış uygulanır. Coğrafi çoğaltma veri aktarımı gigabayt başına ücret doğurur.

* **Giden veri aktarımı maliyetleri**: Giden veri aktarımları (bir Azure bölgesinin dışına aktarılan veriler), genel amaçlı depolama hesapları ile tutarlı şekilde gigabayt başına esaslı olarak bant genişliği kullanımı için fatura doğurur.

* **Değişen hello depolama katmanı**: cool toohot hello depolama katmanının değiştirilmesi ücret eşit tooreading her geçiş için hello depolama hesabında varolan tüm hello veri doğurur. Merhaba üzerinde etkin toocool hello depolama katmanının değiştirilmesi, diğer yandan maliyetini ücretsizdir.

> [!NOTE]
> Hello fiyatlandırma modeli için Blob storage hesapları hakkında daha fazla bilgi için bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) sayfası. Merhaba giden veri aktarımı ücretlerine hakkında daha fazla bilgi için bkz: [veri aktarımları fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/data-transfers/) sayfası.

## <a name="quickstart"></a>Hızlı Başlangıç

Bu bölümde hello hello Azure portal kullanarak senaryolar gösterilmektedir:

* Nasıl toocreate Blob storage hesabı.
* Nasıl toomanage Blob storage hesabı.

Bu ayar toohello tüm depolama hesabı geçerli olmadığından örnekleri aşağıdaki hello hello erişim katmanı tooarchive ayarlayamazsınız. Arşiv katmanını yalnızca belirli bir blob için ayarlayabilirsiniz.

### <a name="create-a-blob-storage-account-using-hello-azure-portal"></a>Hello Azure portalı kullanarak Blob Depolama hesabı oluşturma

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba Hub menüsünde seçin **yeni** > **veri + depolama** > **depolama hesabı**.

3. Depolama hesabınız için bir ad girin.
   
    Bu ad genel olarak benzersiz olmalıdır; Merhaba depolama hesabında kullanılan tooaccess hello nesneleri hello URL'SİNİN bir parçası olarak kullanılır.  

4. Seçin **Resource Manager** hello dağıtım modeli olarak.
   
    Katmanlı depolama yalnızca Resource Manager depolama hesaplarıyla birlikte kullanılabilir; Merhaba dağıtım modeli yeni kaynaklar için önerilen budur. Daha fazla bilgi için hello denetleyin [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).  

5. Merhaba hesap türü açılır listesinden seçin **Blob Storage**.
   
    Depolama hesabı hello türünü seçin, budur. Katmanlı depolama genel amaçlı depolamada kullanılamaz; yalnızca hello Blob Depolama türündeki hesapta kullanılabilir.     
   
    Bunu seçtiğinizde hello performans katmanı tooStandard ayarlandığını unutmayın. Katmanlı depolama hello Premium performans katmanı ile kullanılamaz.

6. Merhaba hello depolama hesabı için çoğaltma seçeneğini seçin: **LRS**, **GRS**, veya **RA-GRS**. Merhaba varsayılandır **RA-GRS**.
   
    LRS = yerel olarak yedekli depolama; GRS = coğrafi olarak yedekli depolama (2 bölge); RA-GRS okuma erişimli coğrafi olarak yedekli depolama olduğu (okuma bulunduğu 2 bölge erişim toohello ikinci).
   
    Azure Depolama çoğaltma seçenekleri ile ilgili ayrıntılar için bkz. [Azure Depolama çoğaltma](../common/storage-redundancy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

7. Gereksinimlerinize uygun depolama katmanını seçin hello: kümesi hello **erişim katmanı** tooeither **Cool** veya **etkin**. Merhaba varsayılandır **etkin**. 

8. Toocreate hello yeni depolama hesabı istediğiniz hello aboneliği seçin.

9. Yeni bir kaynak grubu belirtin veya varolan bir kaynak grubunu seçin. Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../../azure-resource-manager/resource-group-overview.md).

10. Depolama hesabınız için Hello bölgeyi seçin.

11. Tıklatın **oluşturma** toocreate hello depolama hesabı.

### <a name="change-hello-storage-tier-of-a-blob-storage-account-using-hello-azure-portal"></a>Hello Azure portalı kullanarak Blob Depolama hesabı Hello depolama katmanını değiştirme

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. toonavigate tooyour depolama hesabı, tüm kaynakları belirleyin ve ardından depolama hesabınızı seçin.

3. Merhaba ayarlar dikey penceresinde tıklayın **yapılandırma** tooview ve/veya değişiklik hello hesabı yapılandırması.

4. Gereksinimlerinize uygun depolama katmanını seçin hello: kümesi hello **erişim katmanı** tooeither **Cool** veya **etkin**...

5. Merhaba dikey penceresinde hello üstündeki Kaydet'i tıklatın.

> [!NOTE]
> Değişen hello depolama katmanı ek ücretlere neden olabilir. Merhaba bkz [fiyatlandırma ve faturalama](#pricing-and-billing) daha fazla ayrıntı için bölüm.


## <a name="evaluating-and-migrating-tooblob-storage-accounts"></a>Değerlendirme ve tooBlob depolama hesapları geçirme
Merhaba bu bölümün amacı olan toohelp kullanıcılar toomake düzgün toousing Blob storage hesapları geçiş. İki kullanıcı senaryosu vardır:

* Varolan genel amaçlı depolama hesabınız ve tooevaluate değişiklik tooa hello uygun depolama katmanını Blob storage hesabıyla istiyor.
* Toouse Blob storage hesabı karar verdiniz veya zaten bir tane ve, hello seyrek veya sık erişimli depolama katmanı kullanıp kullanmayacağınızı tooevaluate istiyor.

Her iki durumda da hello ilk iş sırası depolama ve bir Blob Depolama hesabında depolanan verileriniz erişim tooestimate hello maliyetidir ve bu maliyetin mevcut maliyetlerinizle karşılaştırılmasıdır karşılaştırın.

## <a name="evaluating-blob-storage-account-tiers"></a>Blob depolama hesabı katmanlarını değerlendirme

Depolama ve bir Blob Depolama hesabında depolanan verilere erişim tooestimate hello maliyet sipariş, beklediğiniz kullanım modelini yaklaşık olmak veya var olan kullanım modelinizi tooevaluate gerekir. Genel olarak, tooknow istiyor:

* Depolama tüketiminiz – Ne kadar veri depolanıyor ve bu aylık olarak nasıl değişiyor?

* Ne kadar veri okuması ve yazılı toohello hesabı (yeni veriler dahil) olan depolama erişim modelleriniz -? Veri erişimi için kaç tane işlem kullanılıyor ve bunlar ne tür işlemler?

## <a name="monitoring-existing-storage-accounts"></a>Var olan depolama hesaplarını izleme

Mevcut depolama hesapları ve bu verileri toplamak toomonitor günlüğe kaydetme işlemlerini gerçekleştiren ve ölçüm verilerini sağlayan bir depolama hesabı için Azure Storage Analytics kullanımı yapabilirsiniz. Storage Analytics toplu işlem istatistiklerini ilişkin kapasite verilerini istekleri toohello hem genel amaçlı depolama hesapları, hem de Blob Depolama hesapları Blob Depolama hizmetine dahil ölçümleri depolayabilirsiniz. Bu veriler hello iyi bilinen tablolara depolanır aynı depolama hesabı.

Daha fazla bilgi için bkz. [Storage Analytics Ölçümleri hakkında](https://msdn.microsoft.com/library/azure/hh343258.aspx) ve [Storage Analytics Ölçüm Tablosu Şeması](https://msdn.microsoft.com/library/azure/hh343264.aspx)

> [!NOTE]
> BLOB storage hesapları yalnızca depolama ve hello ölçüm verilerini bu hesap için erişim için hello tablo Hizmeti uç noktası kullanıma sunar.

toomonitor hello depolama tüketimini hello Blob Depolama hizmetinin, tooenable hello kapasite ölçümlerini gerekir.
Bu ile etkinleştirildiğinde, kapasite verileri günlük bir depolama hesabının Blob hizmeti için kaydedilen ve toohello yazılan bir tablo girişi kaydedilen *$MetricsCapacityBlob* hello içinde aynı tablo depolama hesabı.

toomonitor hello veri erişim düzeni için Blob Depolama hizmetinin Merhaba, tooenable hello saatlik işlem ölçümlerini bir API düzeyinde gerekir. Bu etkin, API başına işlemler saatte bir toplanır ve toohello yazılan bir tablo girişi kaydedilen *$MetricsHourPrimaryTransactionsBlob* hello içinde aynı tablo depolama hesabı. Merhaba *$MetricsHourSecondaryTransactionsBlob* tablo kayıtlarını hello işlemleri toohello ikincil uç RA-GRS depolama hesapları kullanırken.

> [!NOTE]
> Blok genelindeki sayfa blob’larını ve sanal makine disklerini engelleme ve ekleme blob verileriyle birlikte depoladığınız genel amaçlı bir depolama hesabınız varsa bu tahmin işlemi geçerli değildir. Bu kapasite ayrım bir yolu yoktur ve yalnızca hello için blob türüne göre ölçümleri engelleme ve ekleme olabilir blobları işlem tooa Blob storage hesabı geçişi kaynaklanır.

tooget yaklaşık veri tüketim ve erişim modelinizi olarak, bekletme dönemi için düzenli kullanımınızı temsil hello ölçümünün seçin ve tahmin etmeniz öneririz. Bir seçenek tooretain hello ölçüm verilerini hello hello ay sonunda analiz için haftada 7 gün ve toplama hello veri içindir. Başka bir seçenek tooretain hello ölçüm verilerini hello son 30 gün ve toplamak ve hello hello 30 günlük süre sonunda hello verilerini çözümleme.

Ölçüm verilerini etkinleştirme, toplama ve görüntüleme hakkında bilgi için bkz. [Azure Depolama ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

> [!NOTE]
> Analiz verilerinin depolanması, erişimi ve indirilmesi de normal kullanıcı verileri gibi ücretlendirilir.

### <a name="utilizing-usage-metrics-tooestimate-costs"></a>Kullanım ölçümleri tooestimate maliyetleri kullanma

### <a name="storage-costs"></a>Depolama maliyetleri

Merhaba hello kapasite ölçüm tablosunda en son giriş *$MetricsCapacityBlob* hello satır anahtarı ile *'verileri'* gösterir hello kullanıcı verilerinin depolama kapasitesi. Merhaba hello kapasite ölçüm tablosunda en son giriş *$MetricsCapacityBlob* hello satır anahtarı ile *'analytics'* gösterir hello hello analiz günlüklerinin depolama kapasitesi.

Bu toplam kapasite (etkinse) hem kullanıcı verileri ve çözümlemeler günlükleri tarafından tüketilen sonra olabilir tooestimate hello maliyetini, veri hello depolama hesabına depolama kullanılır. aynı yöntem ayrıca blok depolama maliyetlerini tahmin etmek için kullanılabilir ve ilave blobları genel amaçlı depolama hesaplarındaki hello.

### <a name="transaction-costs"></a>İşlem maliyetleri

Merhaba toplamını *'TotalBillableRequests'*, tüm girişleri hello işlemde bir API için ölçüm tablosunda hello işlemleri API'nin toplam sayısını gösterir. *Örneğin*, hello toplam sayısı *'GetBlob'* işlemleri belirli bir süre içindeki hesaplanabilir hello tüm girişlere yönelik toplam Faturalandırılabilir isteklerin toplamına hello satır anahtarını içeren *' kullanıcı; GetBlob'*.

Sipariş tooestimate ilişkin işlem maliyetlerini içinde Blob storage hesapları, farklı fiyatlandırılır beri hello işlemleri üç gruba aşağı toobreak gerekir.

* *'PutBlob'*, *'PutBlock'*, *'PutBlockList'*, *'AppendBlock'*, *'ListBlobs'*, *'ListContainers'*, *'CreateContainer'*, *'SnapshotBlob'* ve *'CopyBlob'* gibi yazma işlemleri.
* *'DeleteBlob'* ve *'DeleteContainer'* gibi silme işlemleri.
* Diğer tüm işlemler.

Sipariş tooestimate işlem maliyetleri de genel amaçlı depolama hesapları için tüm işlemleri toplamanız hello işlemden/API'den tooaggregate gerekir.

### <a name="data-access-and-geo-replication-data-transfer-costs"></a>Veri erişimi ve coğrafi çoğaltma veri aktarımı maliyetleri

Storage analytics sağlamaz hello miktarda veri okuma ve tooa depolama hesabına yazılan, kabaca hello işlem ölçümleri tablosuna bakılarak tahmin edilebilir. Merhaba toplamını *'Totalıngress'* tablosu tüm girişleri hello işlem ölçümlerini bir API için API'nin hello toplam bayt giriş verileri miktarını belirtir. Benzer şekilde hello toplamını *'TotalEgress'* hello toplam bayt çıkış verileri miktarını belirtir.

Blob storage hesapları için sipariş tooestimate hello veri erişim maliyetleri de, hello işlemleri iki gruba aşağı toobreak gerekir. 

* Merhaba hello depolama hesabından alınan veri miktarı tahmini hello toplamına bakılarak *'TotalEgress'* öncelikle hello için *'GetBlob'* ve *'CopyBlob'* işlemler.

* Merhaba toohello depolama hesabına yazılan veri miktarı tahmini hello toplamına bakılarak *'Totalıngress'* öncelikle hello için *'PutBlob'*, *'Copyblob'*, *'CopyBlob'* ve *'AppendBlock'* işlemleri.

coğrafi çoğaltma veri aktarımı için Blob Depolama hesapları da hello bir GRS veya RA-GRS depolama hesabı kullanılırken yazılan veri miktarı için hello tahmini kullanılarak hesaplanabilir Hello maliyeti.

> [!NOTE]
> Merhaba seyrek veya sık erişimli depolama katmanı kullanma hello maliyetlerini hesaplama hakkında daha ayrıntılı bir örnek için hello başlıklı SSS bakalım *'sık ve seyrek erişimli erişim katmanları nelerdir ve hangi bir toouse nasıl belirlemeliyim?'* Merhaba, [Azure depolama fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/storage/).
 
## <a name="migrating-existing-data"></a>Mevcut verileri geçirme

Bir Blob Storage hesabı yalnızca blok ve ilave bloblarının depolanmasına yöneliktir. Toostore tabloları, kuyrukları, dosyaları ve diskleri yanı sıra BLOB'ları, varolan genel amaçlı depolama hesapları, dönüştürülmüş tooBlob depolama hesapları olamaz. toouse depolama katmanları Merhaba, varolan verilerinizi yeni oluşturulan hello hesaplara taşımanız ve toocreate yeni Blob storage hesapları gerekir.

Yöntemleri toomigrate mevcut verileri şirket içi depolama aygıtlarından, üçüncü taraf bulut depolama sağlayıcılardan ya da varolan genel amaçlı depolama hesaplarınızdan Azure Blob storage hesapları aşağıdaki hello kullanabilirsiniz:

### <a name="azcopy"></a>AzCopy

AzCopy yüksek performanslı veri tooand Azure depolama biriminden kopyalanması için tasarlanmış bir Windows komut satırı yardımcı programıdır. Blob Depolama hesabınızda, şirket içi depolama aygıtlarından AzCopy toocopy verileri mevcut genel amaçlı depolama hesaplarınızdan Blob Depolama hesabınızda veya tooupload verileri kullanabilirsiniz.

Daha fazla ayrıntı için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="data-movement-library"></a>Veri hareketi kitaplığı

.NET için Azure Storage veri hareketi kitaplığı Azcopy'yi çalıştıran hello çekirdek veri hareketi altyapısını temel temel alır. Merhaba kitaplığı yüksek performans, güvenilir, tasarlanmıştır ve kolay veri aktarım işlemleri benzer tooAzCopy. Bu, AzCopy tarafından uygulamanızda yerel olarak çalışan ve AzCopy dış örneklerini izleme ile toodeal gerek kalmadan sağlanan hello özellikleri tüm faydalarını tootake sağlar.

Daha fazla ayrıntı için bkz. [.Net için Azure Storage Veri Hareketi Kitaplığı](https://github.com/Azure/azure-storage-net-data-movement)

### <a name="rest-api-or-client-library"></a>REST API’si veya istemci kitaplığı

Özel uygulama toomigrate oluşturmak için verilerinizi bir Blob storage hesabına hello Azure istemci kitaplıklarından birini kullanarak veya Azure storage Hizmetleri REST API hello. Azure Storage NET, Java, C++, Node.JS, PHP, Ruby ve Python gibi birden fazla dilde ve platformda zengin istemci kitaplıkları sağlar. Merhaba istemci kitaplıkları yeniden deneme mantığı, günlüğe kaydetme ve paralel karşıya yüklemeler gibi gelişmiş özellikler sunar. Merhaba HTTP/HTTPS istekleri yapan herhangi bir dil tarafından çağrılabilen REST API karşı doğrudan geliştirebilirsiniz.

Daha fazla bilgi için,bkz. [Azure Blob Storage’ı kullanmaya başlayın](storage-dotnet-how-to-use-blobs.md).

> [!NOTE]
> İstemci tarafı şifreleme kullanılarak şifrelenir BLOB'lar hello blobla depolanan şifrelemeyle ilgili meta verilerini depolar. Tüm kopyalama mekanizmalarının emin olması, blob meta verileri, hello ve özellikle şifrelemeyle ilgili meta verileri Merhaba, korunur kesinlikle önemlidir. Merhaba blobları bu meta veriler olmadan kopyalarsanız, hello blob içeriği tekrar alınabilir değil. Şifrelemeyle ilgili meta veriler hakkında daha fazla bilgi için bkz. [Azure Depolama İstemci Tarafı Şifrelemesi](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).
 
## <a name="faq"></a>SSS

1. **Mevcut depolama hesapları hâlâ kullanılabilir mi?**
   
    Evet, var olan depolama hesapları hala kullanılabilir ve fiyatlandırma veya işlev açısından bir farklılık göstermez.  Bunlar hello özelliği toochoose depolama katmanı gerekmez ve katmanlama hello gelecekteki sahip değil.

2. **Neden ve ne zaman Blob depolama hesapları kullanmaya başlamalıyım?**
   
    BLOB storage hesapları blobları depolamak için tasarlanmıştır ve bize toointroduce yeni blob merkezli özellikleri sağlar. İleride, Blob Depolama bu hesap türüne göre hiyerarşik depolama gibi özellikler gelecekte BLOB'lar, depolama ve katmanlama şekilde önerilen hello görülecektir hesaplarıdır. Ancak, iş gereksinimlerinize göre toomigrate istediğiniz zaman tooyou değildir.

3. **My varolan bir depolama hesabı tooa Blob storage hesabı dönüştürebilir miyim?**
   
    Hayır. Blob depolama hesabı farklı türde bir depolama hesabıdır ve yeni bir tane oluşturmanız ve daha önce açıklandığı şekilde verilerinizi taşımanız gereklidir.

4. **Nesneleri hello iki depolama katmanında depolayabilir miyim aynı hesabı?**
   
    Merhaba *'Erişim katmanı'* özniteliği hesap düzeyinde ayarlamak hello depolama katmanı hello değeri gösterir ve bu hesaptaki tooall nesnelere uygulanır. Ancak, hello blob düzeyinde katmanlama (Önizleme) özelliği, tooset hello erişim katmanı üzerinde belirli BLOB'lar izin verir ve bu hello hesabındaki hello erişim katmanı ayarı geçersiz kılar. 

5. **Merhaba Blob Depolama hesabımdaki depolama katmanını değiştirebilir miyim?**
   
    Evet. Hello depolama katmanı tarafından hello ayarını değiştirebilirsiniz *'Erişim katmanı'* hello depolama hesabındaki özniteliği. Değişen hello depolama katmanı hello hesabında depolanan tooall nesneler geçerlidir. Sık kullanılan toocool değişen hello depolama katmanından doğurmazken, cool toohot değiştirme tabi sırada bir hello hesaptaki tüm hello verilerin okunması için GB başına maliyet doğurur.

6. **Blob Depolama hesabımdaki depolama katmanını hello ne sıklıkta değiştirebilir miyim?**
   
    Merhaba depolama katmanı ne sıklıkta değiştirilebilir bir sınırlama koymuyoruz ancak, cool toohot hello depolama katmanının değiştirilmesi önemli bir ücrete tabi unutmayın. Merhaba depolama katmanını sık değiştirmenizi önermiyoruz.

7. **Merhaba seyrek erişimli depolama katmanındaki bloblar Hello farklı olanları hello sık erişimli depolama katmanındaki hello daha davranır?**
   
    Merhaba sık erişimli depolama katmanındaki bloblar sahip hello aynı gecikme süresine genel amaçlı depolama hesaplarındaki. Hello seyrek erişimli depolama katmanındaki bloblar genel amaçlı depolama hesaplarındaki bir benzer gecikme süresine (milisaniye olarak) sahiptir.
   
    Hello seyrek erişimli depolama katmanındaki bloblar bir biraz daha düşük kullanılabilirlik hizmet düzeyine (SLA) hello sık erişimli depolama katmanında depolanan hello bloblara sahiptir. Daha fazla bilgi için bkz. [Depolama için SLA](https://azure.microsoft.com/support/legal/sla/storage).

8. **Sayfa bloblarını ve sanal makine disklerini Blob depolama hesaplarında depolayabilir miyim?**
   
    Blob Storage hesapları yalnızca blok ve ilave bloblarını destekler, sayfa bloblarını desteklemez. Azure virtual machine diskleri sayfa blobları tarafından yedeklenir ve sonuç olarak kullanılan toostore sanal makine disklerini Blob storage hesapları olamaz. Ancak bir Blob storage hesabı blok blobları olarak olası toostore hello sanal makine disklerinin yedeklerini olur.

9. **My mevcut uygulamaları toouse Blob storage hesapları toochange gerekiyor mu?**
   
    Blob Storage hesapları, blok ve ilave blobları için genel amaçlı depolama hesaplarıyla % 100 API tutarlıdır. Uygulamanız blok blobları kullanarak veya ilave bloblarını ve hello hello 2014-02-14 sürümünü kullanmakta olduğunuz sürece [Storage Services REST API](https://msdn.microsoft.com/library/azure/dd894041.aspx) veya daha büyük uygulamanızı çalışması gerekir. Hello Protokolü eski bir sürümünü kullanıyorsanız, sonra uygulama toouse hello yeni sürümünüzü toowork olarak şekilde sorunsuz bir şekilde her iki tür depolama hesabı ile güncelleştirmeniz gerekir. Genel olarak, her zaman hangi depolama hesabı türü ne olursa olsun, kullandığınız hello en son sürümünü kullanmanızı öneririz.

10. **Kullanıcı deneyiminde bir değişiklik olur mu?**
    
    BLOB storage hesapları blok depolamak için çok benzer tooa genel amaçlı depolama hesapları ve ilave blobları ve Azure Storage, yüksek dayanıklılık ve kullanılabilirlik, ölçeklenebilirlik, performans ve güvenlik dahil olmak üzere tüm hello temel özellikleri destekler. Merhaba özellikler ve kısıtlamalar belirli tooBlob depolama hesapları ve yukarıdaki her şeyi, depolama katmanları dışındaki başka kalır aynı hello.

## <a name="next-steps"></a>Sonraki adımlar

### <a name="evaluate-blob-storage-accounts"></a>Blob Storage hesaplarını değerlendirme

[Bölgeye göre Blob depolama hesaplarının kullanılabilirliğini denetleme](https://azure.microsoft.com/regions/#services)

[Azure Depolama ölçümlerini etkinleştirerek geçerli depolama hesaplarınızın kullanımını değerlendirme](../common/storage-enable-and-view-metrics.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Bölgeye göre Blob depolama fiyatlandırmasını denetleme](https://azure.microsoft.com/pricing/details/storage/)

[Veri aktarımı fiyatlandırmasını denetleme](https://azure.microsoft.com/pricing/details/data-transfers/)

### <a name="start-using-blob-storage-accounts"></a>Blob Storage hesaplarını kullanmaya başlama

[Azure Blob depolamayı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md)

[Azure depolama biriminden veri tooand taşıma](../common/storage-moving-data.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Depolama hesaplarınıza göz atma ve bu hesapları keşfetme](http://storageexplorer.com/)