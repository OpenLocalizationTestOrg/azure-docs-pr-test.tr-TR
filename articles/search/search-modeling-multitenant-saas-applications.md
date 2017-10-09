---
title: "aaaModeling çoklu müşteri mimarisi Azure Search'te | Microsoft Docs"
description: "Azure Search kullanırken çok kiracılı SaaS uygulamaları için ortak tasarım desenleri öğrenin."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Tasarım desenleri çok kiracılı SaaS uygulamaları ve Azure Search için
Çok kiracılı uygulama hello sağlayan biridir aynı Hizmetleri ve özellikleri tooany kimin göremez ya da başka bir kiracı hello veri paylaşır Kiracı sayısı. Bu belge, Azure Search ile oluşturulan çok müşterili uygulamalar için Kiracı yalıtımı stratejileri açıklanır.

## <a name="azure-search-concepts"></a>Azure arama kavramları
Bir hizmet olarak arama çözümü olarak Azure arama, herhangi bir altyapı yönetme veya uzmanı arama olmadan olmadan tooapplications geliştiriciler tooadd zengin arama deneyimleri sağlar. Veri toohello hizmet karşıya ve hello bulutta depolanır. Basit istekleri toohello Azure Search API kullanarak hello veri sonra değiştirilen aranır ve. Merhaba hizmeti genel bir bakış bulunabilir [bu makalede](http://aka.ms/whatisazsearch). Tasarım modeli ele almadan önce önemli toounderstand bazı kavramları olduğu Azure Search.

### <a name="search-services-indexes-fields-and-documents"></a>Arama Hizmetleri, dizinleri, alanları ve belgeleri
Azure arama kullanılırken bir tooa abone *search hizmeti*. Karşıya yüklenen tooAzure arama veri olduğu gibi depolanan bir *dizin* hello arama hizmeti içinde. Tek bir hizmet kapsamındaki dizin sayısı olabilir. bir hizmet kapsamındaki Hello dizinleri bir veritabanı içinde likened tootables olabileceği toouse hello tanıdık kavramlarını veritabanları, likened tooa veritabanı hello arama hizmeti olabilir.

Her dizininin özelleştirilebilir bir dizi tanımlanmış kendi şeması, bir arama hizmeti içinde *alanları*. Veri tek hello formunda tooan Azure Search dizini eklenen *belgeleri*. Her belge karşıya yüklenen tooa belirli dizini olmalıdır ve bu dizinin şema sığması gerekir. Azure Search kullanarak verileri ararken hello tam metin arama sorguları karşı belirli bir dizin verilir.  toocompare bu kavramları toothose veritabanı alanları, bir tablodaki likened toocolumns olabilir ve belgeleri likened toorows olabilir.

### <a name="scalability"></a>Ölçeklenebilirlik
Tüm Azure Search Hizmeti hello standart içinde [fiyatlandırma katmanı](https://azure.microsoft.com/pricing/details/search/) iki boyut ölçeklendirebilirsiniz: depolama ve kullanılabilirlik.

* *Bölümler* bir arama hizmeti tooincrease hello depolama eklenebilir.
* *Çoğaltmaları* tooa hizmet tooincrease hello bir arama hizmeti işleyebilir isteklerin verimini eklenebilir.

Bölümleri ve çoğaltmaları ekleyerek veya kaldırarak hello arama hizmeti toogrow veri ve trafik hello uygulama talepleri hello tutarda hello kapasitesini izin verir. İçinde bir arama hizmeti tooachieve için okuma sipariş [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), iki çoğaltma gerektirir. İçinde bir okuma-yazma için bir hizmet tooachieve sipariş [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), üç çoğaltmaları gerektirir.

### <a name="service-and-index-limits-in-azure-search"></a>Azure Search dizini ve hizmet sınırları
Birkaç farklı [fiyatlandırma katmanlarına](https://azure.microsoft.com/pricing/details/search/) Azure Search'te her hello katmanların farklı sahip [sınırlarını ve kotaları](search-limits-quotas-capacity.md). Bu sınırlar hizmet düzeyi hello bazıları, bazı hello dizin düzeyinde değil ve hello bölüm düzeyinde bazılarıdır.

|  | Temel | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Hizmeti başına en fazla yineleme |3 |12 |12 |12 |12 |
| Hizmet başına en fazla bölüm |1 |12 |12 |12 |1 |
| En fazla arama birimi (çoğaltmaları * bölümler) hizmeti başına |3 |36 |36 |36 |36 (en fazla 3 bölümler) |
| Hizmeti başına en fazla belgeleri |1 milyon |180 milyondan fazla |720 milyon |1.4 milyar |600 milyon |
| Hizmeti başına en fazla depolama |2 GB |300 GB |1,2 TB |2,4 TB |600 GB |
| Bölüm başına en fazla belgeleri |1 milyon |15 milyon |60 milyon |120 milyon |200 milyon |
| Bölüm başına en fazla depolama |2 GB |25 GB |100 GB |200 GB |200 GB |
| Hizmeti başına en fazla dizinler |5 |50 |200 |200 |3000 (en fazla 1000 dizinleri/bölüm) |

#### <a name="s3-high-density"></a>S3 Yüksek yoğunluklu '
Azure Search'ün S3 fiyatlandırma katmanında, özellikle çok müşterili senaryoları için tasarlanmıştır Merhaba yüksek yoğunluk (HD) modu için bir seçenek yoktur. Çoğu durumda gerekli toosupport çok sayıda küçük kiracılar Basitlik ve maliyet verimliliği tek hizmet tooachieve hello yararları altında olur.

S3 HD hello özelliği tooscale bölümleri hello özelliği toohost için tek bir hizmeti daha fazla dizinlerde kullanan dizinleri çıkışı ticaret tarafından çok sayıda küçük dizinleri toobe tek arama hizmeti hello Yönetimi altında paketlenmiş hello sağlar.

Concretely, S3 hizmet too1.4 milyar belgeleri birlikte barındırabilir 1 ve 200 dizinler arasında olabilir. S3 HD hello diğer yandan tek tek dizinler tooonly too1 milyon belgeleri gidin, ancak bölüm başına 200 milyon toplam belge sayısı olan (yukarı too3000 hizmeti başına) bölüm başına too1000 dizinleri yukarı işleyebilir olanak tanır (too600 yukarı hizmeti başına milyon).

## <a name="considerations-for-multitenant-applications"></a>Çok müşterili uygulamalar için ilgili önemli noktalar
Çok müşterili uygulamalar etkili bir şekilde kaynakları hello kiracılar arasında gizlilik hello arasında belirli bir düzeyde koruyarak çeşitli kiracılar dağıtmanız gerekir. Bu tür bir uygulama için hello mimarisi tasarlarken bazı noktalar vardır:

* *Kiracı yalıtımı:* uygulama geliştiricileri tootake uygun önlemleri tooensure hiçbir kiracılar yetkisiz veya istenmeyen diğer kiracıların erişim toohello veri olması gerekir. Veri gizliliği Hello açısından, paylaşılan kaynakların ve gürültülü komşu korumadan etkin Yönetimi Kiracı yalıtımı stratejileri gerektirir.
* *Bulut kaynak maliyeti:* başka herhangi bir uygulama ile yazılım çözümleri maliyet rekabetçi bir çok kiracılı uygulama bileşeni olarak kalması gereken gibi.
* *Operations Kolaylığı:* hello uygulamanın işlemleri üzerindeki etkisi çok müşterili mimarisi geliştirirken hello ve karmaşıklığını önemli bir konu olduğu. Azure arama sahip bir [% 99,9 SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Genel ayak izini:* çok müşterili uygulamalar Merhaba Dünya çapında dağıtılan tooeffectively hizmet vermemesini kiracılar gerekebilir.
* *Ölçeklenebilirlik:* uygulama geliştiricileri nasıl bunlar mutabık kılmak uygulama karmaşıklığını yeterince düşük düzeyde koruma ve Kiracı sayısı ile Merhaba uygulama tooscale tasarlama arasındaki tooconsider gerekir ve hello kiracılarınızın verilerin boyutu ve iş yükü.

Azure Search'te kullanılan tooisolate kiracılar verileri ve iş yükü olabilecek birkaç sınırlarını sunar.

## <a name="modeling-multitenancy-with-azure-search"></a>Azure Search ile çoklu müşteri Mimarisi Modelleme
Hello durumda çok müşterili bir senaryonun hello uygulama geliştiricisi bir veya daha fazla arama hizmetleri kullanır ve Hizmetleri, dizinler veya her ikisi arasında kiracıları bölün. Çok kiracılı bir senaryo modelleme varken, Azure arama birkaç ortak desenler kullanır:

1. *Kiracı başına dizin:* her bir kiracı kendi dizini içindeki diğer kiracılar ile paylaşılan bir arama hizmeti yok.
2. *Kiracı başına hizmet:* en yüksek düzeyde veri ve iş yükü ayrımı sunumu her bir kiracı kendi adanmış bir Azure Search Hizmeti sahip.
3. *Her ikisi de karışımını:* küçük kiracılar paylaşılan hizmetler içinde tek tek dizinler atanmış durumdayken daha büyük ve daha fazlasını etkin kiracılar ayrılmış Hizmetleri atanır.

## <a name="1-index-per-tenant"></a>1. Kiracı başına dizin
![Merhaba Kiracı başına dizin modelinin portrayal](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

Bir kiracı başına dizin modelinde, her bir kiracı kendi dizin sahip olduğu birden çok kiracıya tek bir Azure Search Hizmeti kaplar.

Kiracılar, tüm istekleri arayın ve Azure Search'te dizin düzeyinde bir belge işlemleri verilen olduğundan veri yalıtımı elde edin. Merhaba uygulama katmanında toodirect hello hizmet düzeyinde kaynakları da tüm kiracılar arasında yönetirken çeşitli kiracılar trafiği toohello uygun dizinleri hello hello gerek tanıma yoktur.

Bir anahtar hello Kiracı başına dizin modelinin hello özelliği hello Uygulama geliştirici toooversubscribe hello kapasitesini hello uygulamanın kiracılar arasında bir arama hizmeti için özniteliğidir. Merhaba kiracılar varsa, bir iş yükünün düzensiz dağıtım, kiracılar can en iyi birleşimi hello dağıtılmasını search hizmet tooaccommodate yüksek oranda etkin, yoğun bir kaynak Kiracı sayısı aynı anda bir uzun kuyruğu hizmet verirken dizinler daha az aktif kiracılar. Merhaba dengelemeyi her Kiracı aynı anda yüksek oranda etkin olduğu hello modeli toohandle durumlar hello bağlanamaması ' dir.

Hello Kiracı başına dizin modeli, burada tüm Azure Search Hizmeti satın önceden bir değişken maliyet modeli için hello temeli sağlar ve daha sonra kiracılar ile doldurulur. Bu deneme ve ücretsiz hesaplar için belirlenmiş kullanılmayan kapasiteyi toobe sağlar.

Genel bir yer olan uygulamalar için hello Kiracı başına dizin modeli hello en etkili olmayabilir. Bir uygulamanın kiracılar Merhaba Dünya çapında dağıtılmışsa, ayrı bir hizmet maliyetleri her biri arasında çoğaltabilirsiniz her bölge için gerekli olabilir.

Azure arama için hello tek tek dizinler ve dizinleri toogrow toplam sayısı hello hello ölçek sağlar. Uygun fiyatlandırma, katmanı seçildiğinde, bölümler ve çoğaltmalar toohello tüm arama hizmeti tek bir dizin zaman hello hizmet içinde depolama veya trafiği açısından çok büyük büyür eklenebilir.

Dizinleri toplam sayısı Hello tek bir hizmet için çok fazla büyürse, başka bir hizmet yeni kiracılar hello sağlanan toobe tooaccommodate sahiptir. Dizinleri yeni hizmetler eklendikçe arama hizmetleri arasında taşındı toobe varsa, el ile bir dizin toohello diğer kopyalanan toobe hello veri hello dizinden sahip Azure Search taşınan bir dizin toobe için izin vermediğinden.

## <a name="2-service-per-tenant"></a>2. Kiracı başına hizmeti
![Portrayal hello Kiracı başına hizmet modeli](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

Kiracı başına hizmet mimarisinde, her bir kiracı kendi Arama hizmeti vardır.

Bu modelde, hello uygulama yalıtımı, kiracılar için en fazla düzeyi hello uygular. Her hizmet, depolama ve işleme ayrı API anahtarları yanı sıra arama isteği işlemek için ayrılmış.

Kaynakları çeşitli kiracılar iş yüklerinde paylaşılmayan gibi her bir kiracı büyük ayak izini sahip veya Kiracı tootenant'den az değişkenlik hello iş yükü yüklü olduğu uygulamalar için hello Kiracı başına hizmet modeli bir etkili bir seçimdir.

Kiracı modeli başına bir hizmet, ayrıca bir tahmin edilebilir, sabit maliyet modelin hello avantajını sunar. Bir kiracı toofill edene kadar bir tüm arama hizmeti yok önceden yatırım olduğunu, ancak bir kiracı başına dizin modelinden hello maliyet-başına-Kiracı yüksektir.

Merhaba Kiracı başına hizmet modeli, genel bir yer olan uygulamalar için verimli bir seçimdir. Coğrafi olarak dağılmış kiracılarla kolay toohave her bir kiracının hizmet vermiyor hello uygun bölge.

tek tek kiracılar kendi hizmet outgrow olduğunda bu deseni ölçeklendirme içinde hello zorluklar ortaya çıkar. Azure arama yükseltme hello tüm verileri el ile kopyalanan toobe tooa yeni bir hizmet olması gereken şekilde fiyatlandırma katmanı, bir arama hizmeti şu anda desteklemiyor.

## <a name="3-mixing-both-models"></a>3. Her iki modeli karıştırma
Çoklu müşteri Mimarisi Modelleme için başka bir desen dizin başına Kiracı ve Kiracı başına hizmeti stratejileri karıştırma.

Merhaba daha az etkin, daha küçük kiracılar uzun sonu, paylaşılan bir hizmet olarak dizinler kaplar sırada hello iki desenleri birleştirilmesinden ayrılmış Hizmetleri bir uygulamanın en büyük kiracılar kaplar. Bu model hello en büyük kiracılar hello hizmetinden tutarlı bir şekilde yüksek performanslı herhangi gürültülü komşu küçük kiracılardan hello tooprotect sağlamanın sahip olmasını sağlar.

Ancak, bu stratejinin uygulanması hangi kiracılar paylaşılan bir hizmet bir dizinde karşı adanmış bir hizmet gerektirecektir tahmin etmeye içinde öngörü kullanır. Merhaba gerek toomanage bu RRAS'nin modellerinin ile hem uygulama karmaşıklığını artırır.

## <a name="achieving-even-finer-granularity"></a>Sağlanması bile daha hassas ayrıntı düzeyi
Tasarım desenleri toomodel çok müşterili senaryolarda Azure Search yukarıda Hello her Kiracı uygulamasının tüm örneğini olduğu Tekdüzen bir kapsam varsayalım. Ancak, uygulamaları bazen çok sayıda küçük kapsamı işleyebilir.

Hizmet başına Kiracı ve Kiracı başına dizin modelleri yeterince küçük kapsamları emin değilseniz, olası toomodel dizin tooachieve bile daha hassas bir ayrıntı düzeyi derecesini var.

tek bir dizin için farklı istemci uç noktaları farklı şekilde davranır toohave bir alan olası her istemci için belirli bir değere atayan eklenen tooan dizin olabilir. Bir istemci Azure Search tooquery çağıran veya bir dizin değiştirmek, her Merhaba istemci uygulaması hello koddan Azure Search'ün kullanarak bu alan için uygun değer hello belirtir [filtre](https://msdn.microsoft.com/library/azure/dn798921.aspx) sorgu zaman yeteneği.

Bu yöntem, kullanılan tooachieve işlevselliğini ayrı kullanıcı hesaplarını, ayrı izin düzeyleri ve hatta tamamen ayrı uygulamalar olabilir.

> [!NOTE]
> Merhaba yaklaşımı kullanarak tooconfigure birden çok kiracılar etkiler hello alaka arama sonuçları tek dizin tooserve açıklanmaktadır. Tüm kiracılar veri terim sıklığı gibi temel istatistikleri hello ilgi puanları dahil edilmiş şekilde arama ilgi puanları Kiracı düzeyi kapsamı olmayan bir dizin düzeyinde kapsamda hesaplanır.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Azure arama seçimdir bir ilgi çekici pek çok uygulama [hello hizmetin sağlam özellikleri hakkında daha fazla](http://aka.ms/whatisazsearch). Ne zaman değerlendirme hello çeşitli tasarım desenleri çok müşterili uygulamalar için hello göz önünde bulundurun [çeşitli fiyatlandırma katmanlarına](https://azure.microsoft.com/pricing/details/search/) ve ilgili hello [hizmet sınırları](search-limits-quotas-capacity.md) toobest Azure Search toofit uyarlama uygulama iş yükleri ve mimarileri ölçekteki.

Azure Search ve çok müşterili senaryoları hakkında herhangi bir sorunuz yönlendirilebilir tooazuresearch_contact@microsoft.com.

