---
title: "aaaAzure arama performans ve en iyi duruma getirme konuları | Microsoft Docs"
description: "Azure Search performansı ayarlamak ve en iyi ölçeği yapılandırın"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Azure arama performans ve en iyi duruma getirme konuları
Harika arama deneyimi birçok cep için anahtar toosuccess ve web uygulamaları ' dir. Gayrimenkul hello Müşteri Deneyimi tooused araba Pazar tooonline katalogları, hızlı arama ve ilgili sonuçları etkiler. Bu belge nasıl, ölçeklenebilirlik, çoklu dil desteği veya özel bir derecelendirme gereksinimlerini tooget hello ile Gelişmiş senaryolar için özellikle Azure Search dışında en gelişmiş için en iyi uygulamalar Bul hedeflenen toohelp değil.  Ayrıca, bu belgede iç Ayrıntılar özetlemektedir ve gerçek müşteri uygulamalarında etkili yaklaşımlar kapsar.

## <a name="performance-and-scale-tuning-for-search-services"></a>Performans ve ölçek arama hizmetleri için ayarlama
Bunlar sağlar ve Bing ve Google hello yüksek performans gibi tüm kullanılan toosearch altyapılar duyuyoruz.  Sonuç olarak, müşteriler arama etkin web veya mobil uygulama kullandığınızda, benzer performans özellikleri istedikleri.  İçin arama performansı en iyi duruma getirme, hello en iyi yaklaşımlardan birini toofocus bir sorgu toocomplete ve return sonuçları hello süresini olduğu gecikme üzerinde değildir.  İçin arama gecikme süresini en iyi duruma getirme zaman için önemlidir:

1. Bir hedef gecikme (veya en fazla süreyi) tipik arama isteği toocomplete zamanınızı seçin.
2. Oluşturun ve bu gecikme oranları gerçekçi dataset toomeasure ile arama hizmetinizi karşı gerçek bir iş yükü test.
3. Sorgular (QPS) saniyede az sayıda başlayın ve hedef gecikme gecikme hello düşene hello sorgu tanımlanan kadar hello testinde yürütülen tooincrease hello numarası devam edin.  Uygulamanızın kullanımını büyüdükçe için ölçek planlama önemli Kıyaslama toohelp budur.
4. Mümkün olduğunda, HTTP bağlantılarını yeniden kullanabilirsiniz.  Hello Azure Search .NET SDK'sı kullanıyorsanız, bu örneğini yeniden gelir veya [Searchındexclient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) örneği ve kullanıyorsanız REST API Merhaba, tek bir HttpClient yeniden kullanmamalısınız.

Bunlar oluşturulurken test iş yükleri, Azure Search tookeep aklınızda bazı özellikleri vardır:

1. Toopush aynı anda çok sayıda arama sorguları, hello kaynakları Azure Search hizmetinizin kullanılabilir hale mümkündür.  Bu durumda, HTTP 503 yanıt kodları görürsünüz.  Daha fazla arama istekleri eklemek bu nedenle, en iyi toostart arama istekleri toosee hello gecikme oranları farklılıkları çeşitli aralıklarına sahip olur.
2. İçerik tooAzure arama etkiler karşıya yükleme hello genel performansı ve gecikme hello Azure Search hizmeti.  Kullanıcıların aramaları gerçekleştirirken toosend veri bekliyorsanız, bu iş yükünün içine önemli tootake olduğu testlerinizi hesabında.
3. Her arama sorgusu sırasında hello aynı gerçekleştirecek performans düzeyleri.  Örneğin, bir belge arama veya arama öneri genellikle çok sayıda modelleri ve filtreleri içeren bir sorgu daha hızlı gerçekleştirir.  En iyi tootake hello içine toosee beklediğiniz çeşitli sorguları testlerinizi oluştururken hesap olur.  
4. Merhaba sürekli yürütüyorsa aynı arama istekleri arama istekleri çeşitlemesi önemlidir, çünkü, verileri önbelleğe alma başlangıç toomake performans daha farklı bir sorgu ayarlayabilir daha iyi görünecektir.

> [!NOTE]
> [Visual Studio Yük testi](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) , kıyaslama sınamaları olarak Azure arama sorguları yürütmek için ihtiyacınız olacak tooexecute HTTP isteklerini sağlar ve istekleri paralelleştirme sağlar gerçekten iyi bir yolu tooperform değil.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Azure Search yüksek sorgu hızları için ölçekleme ve istekleri kısıtlanan
Çok fazla daraltılmış isteklerini almak ya da hedef gecikme ücretlerinizi artırılmış sorgu yük aşan toodecrease gecikme oranları iki yoldan biriyle arayabilirsiniz:

1. **Artış çoğaltmaları:** Azure Search tooload Bakiye hello istekler birden çok kopya izin vererek, verilerin bir kopyasını gibi bir çoğaltmadır.  Tüm Yük Dengeleme ve çoğaltmalar arasında verileri çoğaltmasını Azure arama tarafından yönetilir ve herhangi bir zamanda hizmetiniz için ayrılan çoğaltma hello sayısı değiştirebilirsiniz.  Standard arama hizmeti too12 yinelemede ve temel arama hizmeti 3 yinelemede tahsis edebilirsiniz. Çoğaltmaları olabilir hello araçtan ayarlanmış [Azure portal](search-create-service-portal.md) veya [PowerShell](search-manage-powershell.md).
2. **Artış arama katmanı:** Azure arama geldiğinde bir [katmanları sayısı](https://azure.microsoft.com/pricing/details/search/) ve bu katmanların her çeşitli performans düzeylerini sunar.  Bazı durumlarda bile çıkışı çoğaltmaları kullanımının zaman bulunduğunuzu o hello katmanının yeterince düşük gecikme süresi hızları sağlayamaz çok fazla sayıda sorgular olabilir.  Bu durumda, bir hello yüksek arama katmanı senaryoları ile çok sayıda belgeleri ve son derece yüksek sorgu iş yükleri için uygundur hello Azure arama S3 katmanı gibi yararlanarak tooconsider isteyebilirsiniz.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Azure Search yavaş tek tek sorgular için ölçeklendirme
Başka bir nedeni neden gecikme oranları yavaş olabilir, çok uzun toocomplete alma tek bir sorgudan olmasıdır.  Bu durumda, çoğaltmaları ekleme gecikme hızlarını artırır değil.  Bu durumda kullanılabilen iki seçenek vardır:

1. **Bölümler artırmak** bir bölüm verilerinizi ek kaynaklar arasında bölmek için bir mekanizmadır.  İkinci bir bölüm eklediğinizde, bu nedenle, verilerinizi ikiye böl.  Üçüncü bir bölüm dizininizi üç vb. ayırır.  Bu da bazı durumlarda, yavaş sorguları daha hızlı hesaplama toohello paralelleştirme gerçekleştireceğini hello etkisi yoktur.  İş de son derece düşük seçiciliği sorgular olan sorguları ile bu paralelleştirme burada anlatıldığı bazı örnekler verilmiştir.  Bu çok sayıda belge eşleşen sorguları oluşur veya olduğunu gerektiğinde tooprovide büyük belgeleri sayısını sayar.  Olduğundan hesaplama çok gerekli tooscore hello uygunluğunu hello belgeleri veya toocount hello numaralarını belgeler, ek bölümler tooprovide ek hesaplama yardımcı olur.  
   
   En çok Standard arama hizmeti olarak 12 bölüme ve 1 bölümünde hello temel arama hizmeti olabilir.  Bölümler olabilir hello araçtan ayarlanmış [Azure portal](search-create-service-portal.md) veya [PowerShell](search-manage-powershell.md).
2. **Sınır yüksek nicelik alanlar:** modellenebilir veya önemli sayıda benzersiz değere sahip ve sonuç olarak, çok fazla kaynak toocompute sonuçları devreye girer filtrelenebilir alan yüksek kardinalite alan oluşur.   Örneğin, belge toodocument hello değerlerinden çoğunu benzersiz olduğundan bir ürün kimliği veya açıklama alanı modellenebilir/filtrelenebilir olarak ayarlamak için yüksek kardinalite hale getireceği. Mümkün olduğunda, yüksek kardinalite alanları hello sayısını sınırla.
3. **Artış arama katmanı:** Azure Search katmanı yavaş sorguların başka bir şekilde tooimprove performansını olabilir tooa daha yüksek taşıma.  Her daha yüksek katman daha hızlı CPU'lar ve sorgu performansına pozitif bir etkisi olan daha fazla bellek de sağlar.

## <a name="scaling-for-availability"></a>Kullanılabilirlik için ölçeklendirme
Çoğaltmaları değil yalnızca sorgu gecikmesi azaltmaya yardımcı olmak ancak yüksek kullanılabilirlik için de izin verebilirsiniz.  Tek bir çoğaltma ile yazılım güncelleştirmelerinden sonra ya da gerçekleşecek diğer bakım olayları tooserver yeniden başlatmalar ödenecek dönemsel kapalı kalma süresi beklemelisiniz.  Uygulamanız aramaları (sorgular), yüksek kullanılabilirlik gerektiriyorsa sonuç olarak, bu önemli tooconsider yazma (dizin oluşturma olayları) yanı sıra ' dir.  Azure arama, tüm SLA seçenekleri Ücretli Arama teklifleri öznitelikleri aşağıdaki hello ile Merhaba sunar:

* salt okunur iş yüklerinin (sorgular) yüksek kullanılabilirlik için 2 çoğaltma
* okuma-yazma iş yüklerinin (sorgu ve dizin oluşturma) yüksek kullanılabilirlik için 3 veya daha fazla yineleme

Bunun hakkında daha fazla ayrıntı için lütfen başlangıç adresini ziyaret edin [Azure Search hizmet düzeyi sözleşmesi](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Çoğaltmaları birden çok çoğaltma sahip verilerinizin kopyalarını Azure Search toodo makine yeniden başlatmalar sağlar ve Bakım verirken bir anda bir çoğaltma karşı yürütülen toocontinue toobe sorgular olduğundan diğer çoğaltmaları hello.  Bu nedenle, bu kapalı kalma süresi artık daha az verisinin bir kopyası hello karşı yürütülen toobe hello sorguları nasıl etkileyebilir tooconsider gerekir.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Coğrafi olarak dağıtılan iş yükleri ölçekleme ve coğrafi artıklık sağlamak
Coğrafi olarak dağıtılan iş yükleri için Azure Search hizmetinizin barındırıldığı hello veri merkezi gölgeden uzak bulunan kullanıcılara yüksek gecikme hızları olduğunu bulabilirsiniz.  Bu nedenle, genellikle daha yakın bir yerde konumlandırıldığında toothese kullanıcılar bölgelerde birden çok arama hizmetleri önemli toohave olur.  Azure Search'te Azure Search dizinlerini coğrafi çoğaltma otomatik olarak yöntemi şu anda bölgeler arasında sağlamaz, ancak bu işlem basit tooimplement yapmasına ve çağrıları yönetmesine kullanılabilecek bazı teknikler vardır. Bunlar hello özetlenen sonraki birkaç bölümler.

Hello arama hizmetleri coğrafi olarak dağıtılan bir dizi amacı olan toohave iki veya daha fazla dizinler kullanılabilir olduğu bir kullanıcı olacak iki veya daha fazla bölgelerde Bu örnekte görüldüğü gibi hello düşük gecikme sağlar toohello Azure Search Hizmeti yönlendirilmiş:

   ![Bölgeye göre hizmetleri arası sekmesinde][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Veriler arasında birden fazla Azure arama hizmetleri eşitlenmiş şekilde kalmasının
Ya da kullanarak oluşan dağıtılmış arama hizmetlerinizi eşitlenmiş tutmak için iki seçenek vardır hello [Azure Search dizin oluşturucusunu](search-indexer-overview.md) veya itme API hello (tooas hello ya da [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Azure Search'te dizin oluşturucular
Hello Azure Search dizin oluşturucusunu kullanıyorsanız, zaten veri değişiklikleri merkezi bir veri deposu Azure SQL DB ya da Azure Cosmos DB gibi alma. Yeni bir arama hizmeti oluşturduğunuzda, yalnızca bu hizmet için yeni bir Azure Search dizin oluşturucusunu bu noktaları toothis oluşturabilir aynı veri deposu. Bu şekilde hello veri deposuna yeni değişiklikleri gelen her daha sonra alınır çeşitli dizin oluşturucular tarafından başlangıç dizini.  

Bu mimari aşağıdaki gibi görünür, örnek aşağıda verilmiştir.

   ![Tek veri kaynağıyla dağıtılmış dizin oluşturucu ve hizmet birleşimler][2]

### <a name="push-api"></a>Anında iletme API
Kullanıyorsanız, Azure Search itme API çok hello[güncelleştirme Azure Search dizininizi içeriği](https://docs.microsoft.com/rest/api/searchservice/update-index), bir güncelleştirme gerekli olduğunda değişiklikler tooall arama hizmetleri ileterek, çeşitli arama hizmetleri eşitlenmiş tutabilirsiniz.  Bunu yaparken, bir güncelleştirme tooone arama hizmeti başarısız olduğu ve bir veya daha fazla güncelleştirme başarılı önemli toomake emin toohandle durumda.

## <a name="leveraging-azure-traffic-manager"></a>Yararlanmayı Azure trafik Yöneticisi
[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) sonra birden fazla Azure arama hizmetleri tarafından desteklenen tooroute istekleri toomultiple coğrafi konumda bulunan Web sitelerine izin verir.  Merhaba trafik Yöneticisi bir avantajı, Azure Search tooensure kullanılabilir olduğunu araştırma ve böylelikle kullanıcıların tooalternate arama hizmetleri kapalı kalma süresi hello olayda rota ' dir.  Arama istekleri aracılığıyla Azure Web siteleri yönlendirme, ayrıca, Azure Traffic Manager hello Web sitesi yukarı olduğu tooload Bakiye durumlarda ancak Azure Search sağlar.  Trafik Yöneticisi yararlanır hangi hello mimarisi bir örneği burada verilmiştir.

   ![Çapraz-sekmesinde, bölgeye göre Hizmetleri Merkezi Traffic Manager ile][3]

## <a name="monitoring-performance"></a>Performans izleme
Azure Search hizmetinizin hello özelliği tooanalyze ve İzleyicisi Merhaba performans sunar [arama trafiği Analytics (STA)](search-traffic-analytics.md). STA, isteğe bağlı olarak hello tek tek arama işlemlerinin yanı sıra sonra analiz için işlenen ya da görselleştirilen toplanan ölçümler tooan Azure depolama hesabı Power BI'da oturum açabilirsiniz.  STA ölçümleri'ni kullanarak performans istatistikleri sorgular veya sorgusu yanıt sürelerini ortalama sayısı gibi gözden geçirebilirsiniz.  Ayrıca, hello işlem günlüğü toodrill belirli arama işlemlerinin ayrıntıları sağlar.

STA değerli bir araç toounderstand gecikme hızları, Azure Search açısından ' dir.  Oturum hello sorgu performans ölçümleri hello zamana dayalı bu yana bir sorgu tam olarak (gönderilen çıkışı istenen toowhen olduğu başlangıç saatinden itibaren) Azure Search'te işlenen toobe alır, mümkün toouse olduğunuz gecikmesi sorunları hello Azure Search Hizmeti varsa bu toodetermine yan veya dışında hizmet, ağ gecikme süresi uğradıysa gibi hello.  

## <a name="next-steps"></a>Sonraki adımlar
toolearn daha her biri için fiyatlandırma katmanlarına ve Hizmetleri sınırları hello hakkında bkz [hizmet sınırları Azure Search'te](search-limits-quotas-capacity.md).

Ziyaret [kapasite planlaması](search-capacity-planning.md) toolearn bölüm ve çoğaltma birleşimlerini hakkında daha fazla bilgi.

Performansı ve nasıl tooimplement hello en iyi duruma getirme, bazı gösterim bu makalede ele alınan toosee hakkında daha fazla ayrıntıya gitme için video aşağıdaki hello izleyin:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
