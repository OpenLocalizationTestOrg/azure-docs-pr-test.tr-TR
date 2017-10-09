---
title: "Azure arama için planlama aaaCapacity | Microsoft Docs"
description: "Azure Search, her bir kaynağın Faturalanabilir arama birimlerinde nerede fiyatlandırılır bölüm ve çoğaltma bilgisayar kaynakları ayarlayın."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Sorgu ve iş yüklerini Azure Search'te dizin oluşturma için ölçek kaynak düzeyleri
Çalıştırdıktan sonra [bir fiyatlandırma katmanı seçin](search-sku-tier.md) ve [bir arama hizmeti sağlamak](search-create-service-portal.md), hello sonraki adımdır toooptionally artış hello sayısı çoğaltmaları ya da hizmetiniz tarafından kullanılan bölümlerini. Her katman fatura birimleri sabit sayıda sunar. Bu makalede açıklanır nasıl tooallocate bu birimleri tooachieve sorgu yürütme, dizin oluşturma ve depolama için gereksinimlerinizi dengeleyen bir en iyi yapılandırma.

Kaynak yapılandırması, bir hizmetin hello ayarladığınızda kullanılabilir [temel katmana](http://aka.ms/azuresearchbasic) veya hello [standart katmanları](search-limits-quotas-capacity.md). Bu katmanlar adresinde Faturalanabilir Hizmetleri için kapasite artışlarla satın *arama birimine* (SUs) burada her bölüm ve çoğaltma sayar bir SU. 

Daha az SUs sonuçları orantılı olarak daha düşük bir faturaya eklenecektir kullanma. Merhaba Hizmeti'nin ayarlandığından sürece faturalama için etkindir. Merhaba tek yolu tooavoid faturalama hello hizmetin silinmesi ve gerektiğinde daha sonra yeniden oluşturulması olan bir hizmet geçici olarak kullanmıyorsanız.

> [!Note]
> Bir hizmetin silinmesi her şeyin üzerinde siler. Geri arama verilerini kalıcı ve Azure yedekleme için arama içinde hiçbir olanak yoktur. Mevcut bir dizine yeni bir hizmet üzerinde tooredeploy, hello kullanılan program toocreate çalıştırın ve ilk olarak yükleyin. 

## <a name="terminology-partitions-and-replicas"></a>Terminolojisi: bölümler ve çoğaltmalar
Bölümler ve çoğaltmalar bir arama hizmeti yedekleyen hello birincil kaynaklardır.

| Kaynak | Tanım |
|----------|------------|
|*Bölümler* | Dizin depolama ve g/ç okuma/yazma işlemleri (örneğin, yeniden oluşturma ve dizin yenilerken) sağlar.|
|*Çoğaltmaları* | Merhaba arama hizmeti örneklerini öncelikle tooload Bakiye sorgu işlemleri kullanılır. Her çoğaltma her zaman bir dizinin bir kopya barındırır. 12 çoğaltmalar varsa, hello hizmette yüklenen her dizin 12 kopyalarını gerekir.|

> [!NOTE]
> Toodirectly yönetmek veya hangi dizinleri yineleme üzerinde çalışma yönetmek yolu yoktur. Her çoğaltma her dizini bir kopyasını hello hizmet mimarisinin bir parçasıdır.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Nasıl tooallocate bölümler ve çoğaltmalar
Azure Search'te bir hizmet başlangıçta en düşük düzeyde bir bölüm ve bir çoğaltma oluşan kaynakları tahsis edilir. Bunu destekleyen katmanları için daha fazla depolama ve g/ç gerekir veya daha büyük sorgu birimleri ya da daha iyi performans için daha fazla çoğaltmalarını eklerseniz bölümleri artırarak artımlı olarak hesaplama kaynaklarını ayarlayabilirsiniz. Tek bir hizmeti yeterli kaynakları toohandle tüm iş yüklerini (dizin oluşturma ve sorgular) olması gerekir. Birden çok hizmet arasında iş yükleri ayırabilir olamaz.

tooincrease ya da değişiklik hello ayırma çoğaltmalarda ve bölümleri hello Azure portalını kullanmanızı öneririz. Merhaba portal maksimum sınırları kalın izin verilen birleşimleri sınırları uygular:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve hello arama hizmeti seçin.
2. İçinde **ayarları**açın hello **ölçek** dikey ve kullanım hello kaydırıcılar tooincrease veya bölümler ve çoğaltmalar Merhaba sayısını azaltın.

Komut dosyası veya kod tabanlı bir sağlama yaklaşım gerekiyorsa hello [Yönetimi REST API](https://msdn.microsoft.com/library/azure/dn832687.aspx) bir alternatif toohello portalıdır.

Genellikle, özellikle hello hizmet işlemleri sorgu iş yükleri doğru eğilimi nedeniyle arama uygulamaları bölümler,'den daha fazla çoğaltmaları gerekir. Merhaba bölüm [yüksek kullanılabilirlik](#HA) nedenini açıklar.

> [!NOTE]
> Bir hizmet sağlandıktan sonra yükseltilen tooa olamaz daha yüksek SKU. Toocreate hello yeni katman bir arama hizmeti ihtiyacınız ve dizinleri yeniden yükleyin. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) hizmet sağlama konusunda yardım için.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Yüksek kullanılabilirlik
Kolaydır ve görece yukarı tooscale hızlı, genellikle bir bölüm ve bir başlayın veya iki çoğaltmaları ve ardından sorgu birimler olarak ölçek büyütme yapı öneririz. Hello temel veya S1 katmanları en çok sayıda Hizmetleri için bir bölüm, (bölüm başına 15 milyondan fazla belge), yeterli depolama ve g/ç sağlar.

Sorgu iş yükleri öncelikle çoğaltmalar üzerinde çalıştırın. Daha fazla verimlilik veya yüksek kullanılabilirlik gerekiyorsa, ek çoğaltmaları büyük olasılıkla gerektirir.

Yüksek kullanılabilirlik için genel öneriler şunlardır:

* Salt okunur iş yüklerinin (sorgular) yüksek kullanılabilirlik için iki çoğaltma
* Okuma/yazma iş yüklerinin (sorgular ve tek tek belgeler eklendikçe, güncelleştirilmiş veya dizin) yüksek kullanılabilirlik için üç veya daha fazla çoğaltmaları

Azure arama için hizmet düzeyi sözleşmelerine (SLA), sorgu işlemleri ve ekleme, güncelleştirme veya silme belgeleri oluşur dizin güncelleştirmeleri hedefler.

### <a name="index-availability-during-a-rebuild"></a>Bir yeniden oluşturma sırasında dizin kullanılabilirliği

Azure arama için yüksek kullanılabilirlik bir dizini yeniden oluşturma içermeyen tooqueries ve dizin güncelleştirmeleri ilgilidir. Bir alan silin, veri türünü değiştirin veya alanı yeniden adlandırma, toorebuild hello dizini gerekir. toorebuild hello dizin hello silmelisiniz dizin, başlangıç dizini yeniden oluşturun ve hello verileri yeniden yükleyin.

> [!NOTE]
> Merhaba dizinini yeniden oluşturmayı olmadan yeni alanları tooan Azure Search dizini ekleyebilirsiniz. Merhaba hello yeni alanın değerini zaten hello dizindeki tüm belgeler için null olur.

toomaintain dizin kullanılabilirlik bir yeniden oluşturma sırasında aynı üzerinde farklı bir hizmet olarak adlandırın ve ardından kodunuzu yeniden yönlendirme veya yük devretme mantığı sağlayın hello ile aynı hizmetine veya hello bir kopyasını dizin hello üzerinde hello dizini farklı bir adla bir kopyasını olmalıdır.

## <a name="disaster-recovery"></a>Olağanüstü durum kurtarma
Şu anda, olağanüstü durum kurtarma için yerleşik hiçbir mekanizması yoktur. Ekleme bölümleri veya çoğaltmaları olağanüstü durum kurtarma hedefleri karşılamak için yanlış stratejisi hello olacaktır. Merhaba en yaygın tooadd artıklık hello hizmeti düzeyinde başka bir bölgede ikinci bir arama hizmeti ayarlayarak yaklaşımdır. Kullanılabilirlik gibi bir dizini yeniden oluşturma sırasında ile Merhaba yeniden yönlendirme veya yük devretme mantığı kodunuzdan gelmelidir.

## <a name="increase-query-performance-with-replicas"></a>Yinelemelerle sorgu performansı artırma
Sorgu gecikmesi ek çoğaltmaları gerekli olan bir göstergesidir. Genellikle, sorgu performansı iyileştirme bir ilk adım, bu kaynağın daha fazla tooadd içindir. Çoğaltmaları ekledikçe hello dizin ek kopyalarını çevrimiçi toosupport büyük sorgu iş yükleri duruma getirilir ve tooload Bakiye hello hello birden çok çoğaltma istekleri.

Sabit tahminleri / saniye (QPS) sorgularını sağladığımız olamaz: sorgu performansı hello hello karmaşıklığına bağlıdır sorgu ve rakip iş yükleri. Ortalama, temel veya S1 SKU'ları bir yineleme yaklaşık 15 QPS servis edebilirsiniz, ancak daha yüksek veya düşük sorgu karmaşıklığına bağlı olarak, üretilen iş görüntülenir (modellenmiş sorguları daha karmaşık) ve ağ gecikme süresi. Ayrıca, çoğaltmaları ekleme kesinlikle ölçek ve performans, ekleyeceksiniz olsa da, sonuç hello toorecognize kesinlikle doğrusal değil önemlidir: üç çoğaltmaları ekleme garanti etmez Üçlü işleme.

toolearn QPS iş yükleri için tahmin etmek için yaklaşımlar dahil olmak üzere QPS hakkında bkz [Search hizmetinizi yönetme](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Bölümleri olan dizin oluşturma performansı artırma
Gerçek zamanlı veri yenileme gerektiren arama uygulamalar orantılı olarak daha fazla bölüm çoğaltmaları daha gerekir. Bölümler ekleme okuma/yazma işlemleri çok sayıda işlem kaynakları arasında yayar. Bu aynı zamanda, daha fazla disk alanı ek dizinler ve belgeleri depolamak için sağlar.

Daha büyük dizinler uzun tooquery alın. Bu nedenle, bölümler artımlı her artış çoğaltmaları küçük ancak orantılı bir artış gerektirdiğini görebilirsiniz. Merhaba karmaşıklığına sorgular ve sorgu toplu sorgu yürütme ne kadar hızlı açık içine öğeli.

## <a name="basic-tier-partition-and-replica-combinations"></a>Temel katman: bölüm ve çoğaltma birleşimler
Temel bir hizmet tam olarak bir bölüm olması ve toothree çoğaltmaları sınırına üç SUs yukarı. Merhaba yalnızca ayarlanabilir çoğaltmaları kaynaktır. En az iki çoğaltma sorguları yüksek kullanılabilirlik gerekir.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Standart katmanları: bölüm ve çoğaltma birleşimler
Bu tabloda, çoğaltmaları ve bölümler, tüm standart katmanları için konu toohello 36 SU sınırı hello SUs gerekli toosupport birleşimleri gösterilmektedir.

|   | **1 bölümü** | **2 bölüm** | **3 bölümleri** | **4 bölümleri** | **6 bölümleri** | **12 bölümleri** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 çoğaltma** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **2 çoğaltma** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **3 çoğaltmaları** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **4 çoğaltmaları** |4 SU |8 SU |12 SU |16 SU |24 SU |Yok |
| **5 çoğaltmaları** |5 SU |10 SU |15 SU |20 SU |30 SU |Yok |
| **6 çoğaltmaları** |6 SU |12 SU |18 SU |24 SU |36 SU |Yok |
| **12 çoğaltmaları** |12 SU |24 SU |36 SU |Yok |Yok |Yok |

SUs, fiyatlandırma ve kapasite hello Azure Web sitesi üzerinde ayrıntılı olarak açıklanmıştır. Daha fazla bilgi için bkz: [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> çoğaltmalarda ve bölümleri Hello sayıyı böler eşit olarak 12 (özellikle, 1, 2, 3, 4, 6, 12). Böylece tüm bölümler eşit bölümlerinde yayılabilen Azure Search her dizin 12 parça önceden böler olmasıdır. Örneğin, üç bölüm hizmetiniz varsa ve dizin oluşturma, her bölüm hello dizinin dört parça içerir. Dizin bir Azure Search parça ne uygulama ayrıntılarını konu toochange gelecekte serbest bırakır. Merhaba numarası 12 Bugün olsa da, 12 hello gelecekteki tooalways numarasını beklediğiniz döndürmemelidir.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Çoğaltma ve bölüm kaynakları için faturalama formülü
kaç tane SUs belirli birleşimleri için kullanılan hesaplama hello formülüdür çoğaltmalarda ve bölümler, hello ürün veya (R X P SU =). Örneğin, üç bölüm tarafından çarpılan üç çoğaltmaları fatura dokuz SUs.

SU başına maliyet, standart için temel daha düşük birim başına fatura oranı içeren hello katmanı tarafından belirlenir. Her katman üzerinde bulunabilir derecelendirir [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/search/).
