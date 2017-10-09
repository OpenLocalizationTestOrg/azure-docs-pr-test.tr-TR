---
title: "Microsoft Azure Service Fabric hakkında aaaCommon sorular | Microsoft Docs"
description: "Service Fabric ve yanıtlarını hakkında sık sorulan sorular"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Sık sorulan soruları Service Fabric

Service Fabric neler yapabileceğinizi ve nasıl kullanılacağını hakkında çok sık sorulan sorular bulunmaktadır. Bu belgede bu ortak sorularını ve yanıtlarını çoğunu kapsar.

## <a name="cluster-setup-and-management"></a>Küme kurulumu ve Yönetimi

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>Birden çok Azure bölgeleri veya kendi veri merkezlerini yayılan bir küme oluşturabilir miyim?

Evet. 

ağ bağlantısı tooeach diğer sahip oldukları sürece hello çekirdek Service Fabric kümeleme teknolojisine herhangi bir yere hello world çalışan kullanılan toocombine makineler olabilir. Ancak, oluşturma ve böyle bir kümeyi çalıştırma karmaşık olabilir.

Bu senaryoda ilgileniyorsanız, kişi tooget hello yoluyla öneririz [Service Fabric Github sorunlar listesine](https://github.com/azure/service-fabric-issues) veya destek temsilcisine sipariş tooobtain ek Kılavuzu. Merhaba Service Fabric takım tooprovide açıklığa, yönerge ve önerileri bu senaryo için çalışıyor. 

Bazı şeyleri tooconsider: 

1. Hello Azure Service Fabric küme kaynağı bugün bölgesel, bu hello küme hello sanal makine ölçek ayarlar olduğu gibi üzerine kurulmuştur. Bu, bölgesel bir hatanın hello olayda hello özelliği toomanage hello küme hello Azure Resource Manager aracılığıyla ya da kaybedebilirsiniz Azure Portal hello olduğunu anlamına gelir. Merhaba küme çalışmaya devam eder ve onunla mümkün toointeract doğrudan olacağını olsa bile bu durum oluşabilir. Ayrıca, Azure bugün hello özelliği toohave bölgeler arasında kullanılabilir tek bir sanal ağ sağlamaz. Bu Azure bölgeli kümede ya da gerektirdiği anlamına gelir. [hello VM ölçek kümesi içindeki her bir VM için genel IP adresleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine) veya [Azure VPN ağ geçitleri](../vpn-gateway/vpn-gateway-about-vpngateways.md). Bu tür bir ortam kurma konumu önce dikkatli analiz ve planlama gerekli şekilde bu ağ seçeneğiniz maliyetleri, performans ve toosome derece uygulama tasarımı üzerinde farklı etkileri vardır.
2. Merhaba bakım, yönetim ve izleme bu makinelerin özellikle arasında dağıtılmış olduğunda karmaşık, hale gelebilir _türleri_ gibi farklı bulut sağlayıcıları arasında veya şirket içi kaynakları ile Azure arasında ortamlarının . Dikkatli olunması yükseltmeleri tooensure, izleme, yönetim ve tanılama hello küme ve hello uygulamalar için bu tür bir ortamda üretim iş yükleri çalıştırmadan önce anlaşılır. Çok sayıda Azure veya kendi veri merkezleri içinde bu sorunları çözmek deneyimi zaten varsa, daha sonra bu çıkışı oluşturma veya Service Fabric kümesi çalıştırdığınızda bu aynı çözümler uygulanabilir olasıdır. 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Service Fabric düğümlerin işletim sistemi güncelleştirmelerini otomatik olarak alıyorsunuz?

Bugün değil, ancak bu ayrıca Azure toodeliver oranla ortak bir istek.

Hello geçici, sahibiz [bir uygulama sağlanan](service-fabric-patch-orchestration-application.md) hello işletim sistemleri, Service Fabric düğümlerinizi altında düzeltme eki ve toodate kalır.

Merhaba sınama işletim sistemi güncelleştirmelerini ile bunlar genellikle geçici kullanılabilirlik kaybına sonuçları hello makinenin yeniden başlatılması gerekir ' dir. Service Fabric trafiği Hizmetleri tooother düğümleri için otomatik olarak yeniden kendisi tarafından bir sorun değildir. Ancak, işletim sistemi güncelleştirmelerini hello kümede düzenlenir değil, aynı anda birçok düğümleri Git aşağı hello olası yoktur. Bu tür eşzamanlı yeniden başlatmalar veya bir hizmet için tam kullanılabilirlik kaybına neden olabilir (durum bilgisi olan bir hizmeti için) belirli bir bölüm için en az.

Hello gelecekteki, biz kullanılabilirlik yeniden başlatmalar ve diğer beklenmeyen hataları rağmen korunduğundan emin olduktan tamamen otomatik ve güncelleştirme etki alanları arasında Eşgüdümlü toosupport bir işletim sistemi güncelleştirme ilkesi planlayın.

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>Büyük sanal makine ölçek kümeleri my BT kümede kullanabilir miyim? 

**Kısa yanıt** - Hayır 

**Uzun yanıt** - hello büyük sanal makine ölçek kümeleri tooscale izin verse de bir sanal makine ölçek fazla 1000 VM örnekleri, otomatik yerleştirme grupları (PGs) hello kullanarak bunu yapar. Yalnızca hata etki alanlarını (FDs) ve yükseltme etki alanları (UDs) yerleştirme Grup Service fabric kullandığı FDs ve UDs toomake yerleştirme kararları, hizmet çoğaltmaları/hizmet örnekleri içinde tutarlı değil. Merhaba FDs ve UDs karşılaştırılabilir olduğundan yalnızca yerleştirme grubunda BT tarafından kullanılamaz. PG1 VM1 FD topolojisini varsa, örneğin, = 0 ve PG2 VM9 FD topolojisini = 4, onu gelmez VM1 ve VM2 olan iki farklı donanım rafları, dolayısıyla BT hello FD değerleri bu servis talebi toomake yerleştirme kararları kullanamazsınız.

Diğer sorunlar var. büyük sanal makine ölçek kümeleri ile şu anda, düzey 4 hello eksikliği yük gibi karşı desteği Toofor başvuran [büyük ayrıntıları ölçekleme kümeleri](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Service Fabric kümesi hello minimum boyutu nedir? Neden küçük olamaz?

Merhaba minimum desteklenen üretim iş yükleri çalıştıran bir Service Fabric kümesi için beş düğümü boyutudur. Geliştirme ve test senaryoları için üç düğümlü kümeler destekliyoruz.

Bu alt limitlerin Hello Service Fabric kümesi hello adlandırma hizmeti ve hello Yük Devretme Yöneticisi dahil olmak üzere, durum bilgisi olan sistem hizmetleri kümesi çalıştığından mevcut. Ne Hizmetleri bırakıldı izlemek bu hizmetleri toohello kümesi dağıtılmış ve güçlü tutarlılık üzerinde şu anda barındırılan nerede bağlıdır. Bu güçlü tutarlılık hello özelliği tooacquire üzerinde sırayla bağlıdır bir *çekirdek* için verilen herhangi bir güncelleştirme bu toohello durumu, bir çekirdek hello çoğaltmaları (N/2 + 1) için belirli bir hizmeti katı çoğunu temsil ettiği Hizmetleri.

Bu arka plan ile bazı olası küme yapılandırmaları inceleyelim:

**Bir düğüm**: hello tek düğümlü herhangi bir nedenle hello kaybı hello tüm küme hello kaybı anlamına gelir beri bu seçenek yüksek oranda kullanılabilirlik sağlamaz.

**İki düğüm**: iki düğüm arasında dağıtılan bir hizmet için çekirdek (N = 2) 2'dir (2/2 + 1 = 2). Tek bir çoğaltma kaybolur imkansız toocreate bir çekirdek olur. Hizmet yükseltme gerçekleştirme geçici olarak bir çoğaltma sürüyor gerektirdiğinden, bu kullanışlı bir yapılandırma değildir.

**Üç düğümü**: (N = 3) üç düğümü ile Merhaba gereksinim toocreate bir çekirdek hala iki düğüm olması (3/2 + 1 = 2). Bu, tek bir düğümünü kaybeder ve hala çekirdeğini korumak anlamına gelir.

güvenli bir şekilde yükseltme yapmak ve tek tek düğüm hatalarını varlığını sürdürmesi için aynı anda durum mu olduğu sürece hello üç düğüm Küme yapılandırması geliştirme ve test için desteklenir. Üretim iş yükleri için beş düğüm için esnek toosuch aynı anda başarısız olması gerekir.

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>Gece/hafta sonları toosave maliyetleri my kümesine devre dışı bırakabilirsiniz?

Genellikle yapamazsınız. Service Fabric hello sanal makine taşınan tooa farklı ana bilgisayar ise hello verileri ile taşımaz, yani durumu yerel, kısa ömürlü disklerde depolar. Merhaba yeni bir düğüm tarafından diğer düğümlere toodate getirilene gibi normal işleminde, bir sorun değildir. Ancak, tüm düğümler durdurur ve daha sonra yeniden hello düğümlerinin en yeni konaklarda başlatın ve hello sistem oluşturulamıyor toorecover olun önemli olasılığı yoktur.

Dağıtmadan önce uygulamanızı test etmek için toocreate kümeleri isterseniz, bu kümeleri dinamik olarak parçası olarak oluşturmanızı öneririz, [sürekli tümleştirme/sürekli dağıtım ardışık düzen](service-fabric-set-up-continuous-integration.md).


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>My işletim sisteminden (örneğin Windows Server 2012 tooWindows Server 2016) nasıl yükseltme?

Gelişmiş bir deneyim üzerinde bugün çalışıyoruz sırada hello yükseltme için siz sorumlusunuz. Merhaba hello OS görüntüde yükseltmelisiniz hello sanal makinelerin aynı anda bir VM küme. 

## <a name="container-support"></a>Kapsayıcı desteği

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>Dağıtılan tooSF oluşturulamıyor tooresolve DNS olan my kapsayıcıları neden olan adresleri?

Bu sorun üzerinde 5.6.204.9494 kümelerinin üzerinde bildirilen sürüm 

**Azaltma** : izleyin [bu belgeyi](service-fabric-dnsservice.md) tooenable hello DNS service fabric hizmeti kümenizdeki.

**Düzeltme** : kullanılabilir olduğunda, 5.6.204.9494 yüksek olan desteklenen yükseltme tooa küme sürümü. Kümenizi tooautomatic yükseltmeler ayarlarsanız hello küme otomatik olarak sabit Bu sorun var. toohello sürümüne yükseltin.

  
## <a name="application-design"></a>Uygulama tasarımı

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>Güvenilir bir koleksiyonun bölümler hello en iyi şekilde tooquery veri nedir?

Güvenilir koleksiyonlarıdır genellikle [bölümlenmiş](service-fabric-concepts-partitioning.md) daha fazla performans ve verimlilik için tooenable ölçek genişletme. Belirli bir hizmeti için hello durumu 10'luk veya makinelerin 100s üzerinden yayılan, anlamına gelir. Bu tam veri kümesi üzerinde tooperform işlemleri, birkaç seçeneğiniz vardır:

- Başka bir hizmet toopull gerekli hello verilerdeki tüm bölümleri sorgular bir hizmet oluşturun.
- Başka bir hizmetin tüm bölümler veri aldığınız bir hizmet oluşturun.
- Düzenli aralıklarla veri hizmeti her tooan dış depolama alanından iletin. Bu yaklaşım, yalnızca, gerçekleştiriyorsunuz hello sorguları çekirdek iş mantığınızı parçası değilse uygundur.


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>My aktörler arasında hello en iyi şekilde tooquery veri nedir?

Bağımsız bir birim tasarlanmış toobe durumunun aktörler ve onun değildir İşlem çalışma zamanında aktör durumunun geniş sorgular tooperform önerilir. Merhaba tam kümesi aktör durumunun boyunca gerek tooquery varsa ya da dikkate almanız gerekenler:

- Sağlayacak şekilde Hello ağ toogather tüm verileri aktörler toohello hizmetinizi bölüm sayısı hello sayısından isteklerinin sayısı aktör hizmetlerinizi durum bilgisi olan güvenilir hizmetler ile değiştirin.
- Aktör tooperiodically itme daha kolay sorgulamak için kendi durumu tooan dış depo tasarlama. Yukarıdaki bu yaklaşım yalnızca gerçekleştirmekte hello sorguları kullanarak çalışma zamanı davranışını gerekli değilse uygulanabilir gibidir.

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>Ne kadar veri ı güvenilir bir koleksiyonda depolayabilir miyim?

Merhaba tutar depolayabileceğiniz yalnızca hello kümedeki sahip makine hello sayısı ve kullanılabilir bellek miktarı hello bu makinelere sınırlıdır şekilde güvenilir hizmetler genellikle bölümlenir.

Bir örnek olarak, güvenilir bir koleksiyon 100 bölümleri ve 3 çoğaltmalar, bir hizmet olarak 1 kb boyutunda ortalama nesneleri depolamak olduğunu varsayalım. Şimdi makine başına bellek 16 gb ile 10 makine kümesi olduğunu varsayalım. Basitlik ve toobe çok koruyucu için hello işletim sistemi ve Sistem Hizmetleri, hello Service Fabric çalışma zamanını ve hizmetlerinizi 6 hello küme için makine başına kullanılabilir 10 gb ya da 100 gb bırakarak gb, kullandığını varsayın.

Her bir nesne olmalıdır göz önünde bulundurarak, depolanan üç (bir birincil ve iki çoğaltma), yaklaşık 35 milyon nesneler için yeterli bellek koleksiyonunuzda tam kapasitede çalışırken olurdu. Ancak, bir hata etki alanı ve yaklaşık 1/3 kapasiteye temsil eder ve hello numara tooroughly 23 milyon azaltmak bir yükseltme etki eşzamanlı kaybı dayanıklı toohello olması önerilir.

Bu hesaplama ayrıca varsaydığını unutmayın:

- Hello dağıtım hello bölümleri arasında veri kabaca Tekdüzen veya yük ölçümleri toohello küme Resource Manager raporlama. Varsayılan olarak, Service Fabric Yük Dengelemesi yineleme sayısına göre. Bizim örneğimizde yukarıdaki hello kümedeki her düğümde, 10 birincil çoğaltma ve 20 ikincil çoğaltmaları koyabilirsiniz. İyi hello bölümleri arasında eşit olarak dağıtılmış yük için işe yarar. Yük bile değilse, böylece hello Resource Manager küçük çoğaltmaları birlikte paketi ve büyük çoğaltmaları tooconsume daha fazla bellek tek bir düğümde izin verebilirsiniz yük bildirilmesi gerekir.

- Söz konusu hello güvenilir hizmet hello yalnızca bir depolama hello küme durumda. Birden çok Hizmetleri tooa kümesi dağıtabilirsiniz beri toobe her toorun gerekir ve durumuna yönetebileceğiniz hello kaynakların oluşturduğunu gerekir.

- Bu hello küme büyüyen veya küçültme değil. Daha fazla makine eklerseniz, Service Fabric bir tek tek bir çoğaltma makineler yayılamaz bu yana makine hello sayısı hello hizmetinizi bölüm sayısı değerini geçiyor kadar yinelemeleri tooleverage hello ek kapasite yeniden dengelemeniz. Bunun aksine, makineler kaldırarak hello küme hello boyutunu azaltın, çoğaltmalarınızı daha sıkı bir şekilde paketlenmiş ve daha az genel kapasiteye sahip.

### <a name="how-much-data-can-i-store-in-an-actor"></a>Ne kadar veri t bir aktör depolayabilir miyim?

Güvenilir hizmetleriyle gibi hello aktör hizmetinde depoladığınız veri miktarı yalnızca hello toplam disk alanı ve kullanılabilir bellek kümenizdeki hello düğümleri arasında sınırlıdır. Ancak, kullanılan tooencapsulate durum ve ilişkili iş mantığı az miktarda olduklarında tek tek aktörler en etkili. Genel kural olarak, tek bir aktör kilobayt cinsinden ölçülen durumu olması gerekir.

## <a name="other-questions"></a>Diğer sorular

### <a name="how-does-service-fabric-relate-toocontainers"></a>Service Fabric toocontainers nasıl ilişkilidir?

Tutarlı bir şekilde tüm ortamlarda çalıştırın ve tek bir makinede yalıtılmış bir şekilde işleyebilir şekilde kapsayıcıları basit yol toopackage Hizmetleri ve bağımlılıklarını sunar. Service Fabric yolu toodeploy sunar ve gibi hizmetler yönetmek [bir kapsayıcıda paketlenmiş Hizmetleri](service-fabric-containers-overview.md).

### <a name="are-you-planning-tooopen-source-service-fabric"></a>Tooopen kaynak Service Fabric planlıyor musunuz?

Biz tooopen kaynak hello reliable services ve güvenilir aktörler çerçeveler Github'da düşündüğünüz ve topluluk katkılarına toothose projeleri kabul eder. Lütfen hello izleyin [Service Fabric blog](https://blogs.msdn.microsoft.com/azureservicefabric/) duyurdu gibi daha fazla ayrıntı için.

şu anda hiçbir planları tooopen kaynak hello Service Fabric çalışma Hello olan.

## <a name="next-steps"></a>Sonraki adımlar

- [Service Fabric kavramları ve en iyi uygulamalar hakkında bilgi edinin](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
