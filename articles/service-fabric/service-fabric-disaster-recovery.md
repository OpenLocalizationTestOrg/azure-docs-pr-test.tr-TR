---
title: "aaaAzure Service Fabric olağanüstü durum kurtarma | Microsoft Docs"
description: "Azure Service Fabric hello özellikleri gerekli toodeal olağanüstü tüm türleri sunar. Bu makalede oluşabilir afetler hello türlerini ve nasıl onlarla toodeal."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Azure Service Fabric olağanüstü durum kurtarma
Yüksek kullanılabilirlik gerçekleştirirken önemli bir bölümü Hizmetleri hataları tüm farklı türlerde varlığını sürdürmesini olduğundan emin olmaktır. Bu, Planlanmayan hatalar için özellikle önemlidir ve denetiminizin dışında. Bu makalede afetler olabilir değilse modellenir ve doğru şekilde yönetilen bazı ortak hatası modları açıklanır. Bu da ele Azaltıcı Etkenler ve Eylemler tootake yine de bir olağanüstü durum oluştuysa. Merhaba hedef toolimit ya da planlanmış hataları veya aksi halde, ortaya hello kapalı kalma süresi veya veri kaybı riski ortadan kaldırmak.

## <a name="avoiding-disaster"></a>Olağanüstü durum önleme
Service Fabric'ın birincil ortamınıza ve hizmetlerinizi genel hata türlerini afetler olmayan şekilde model toohelp hedefidir. 

Genel olağanüstü durum/hatası senaryoları iki tür vardır:

1. Donanım veya yazılım hatası
2. İşletimsel hataları

### <a name="hardware-and-software-faults"></a>Donanım ve yazılım hataları
Donanım ve yazılım hataları öngörülemeyen sonuçlara yol açabilir. Merhaba en kolay yolu toosurvive hataları fazla kopyasını donanım veya yazılım hatası sınırlarında yayılmış hello hizmeti çalışıyor. Hizmetinizi belirli olan yalnızca bir makinede çalışıyorsa, örneğin, ardından Merhaba, bir makinenin bu hizmet için bir olağanüstü durum hatasıdır. Merhaba basit yol tooavoid bu olağanüstü durum hello hizmet birden çok makineye çalıştırdığını tooensure ' dir. Sınama ayrıca gerekli tooensure hello hatası bir makinenin hizmet çalıştıran hello kesintiye değil olur. Kapasite planlama değiştirme örneği başka bir yerde oluşturulabilir ve kapasite azalma Hizmetleri kalan hello aşırı değil sağlar. Merhaba aynı düzeni tooavoid hello başarısızlığını ne çalıştığınız bağımsız olarak çalışır. Örneğin. bir SAN hello hata hakkında ilgilenen, birden çok SAN çalıştırın. Bir sunucu rafı hello kayıpları hakkında ilgilenen, birden çok kabin çalıştırın. Veri merkezleri hello kayıpları hakkında endişeleniyoruz, hizmetiniz birden çok Azure bölgeleri veya veri merkezleri arasında çalıştırmanız gerekir. 

Bu dağıtılmış modu türünde çalıştırırken, konu toosome türlerini eşzamanlı hataları, ancak tek ve belirli bir türdeki bile birden çok hatadan hala olduğunuz (örn: tek bir VM veya ağ bağlantısı başarısız) otomatik olarak işlenir (ve bu nedenle artık bir "olağanüstü durum"). Service Fabric hello küme ve başarısız düğümlerin ve hizmetler geri getirme tanıtıcıları genişleterek birçok mekanizma sağlar. Service Fabric ayrıca hizmetlerinizi birçok örneklerini sipariş tooavoid planlanmayan hatalar bu tür gelen dönüş gerçek afetler çalıştırılmasını sağlar.

Neden bir dağıtım büyüklükte toospan hataları çalışan uygun olmadığı nedenleri olabilir. Örneğin, daha fazla donanım kaynakları istekli değilseniz daha sürebilir hatanın göreli toohello fırsat toopay. Dağıtılmış uygulamaları ile ilgilenirken, ek iletişim atlama veya durum çoğaltma coğrafi uzaklıklar nedenler kabul edilebilir gecikme süresi arasında maliyetleri olabilir. Burada bu çizgi çizilir her uygulama için farklıdır. Yazılım hataları için özellikle hello hataya hello hizmetinde tooscale çalıştığınız olabilir. Bu durumda Hello hata koşulu tüm hello örneklerde bağıntılı olduğundan daha fazla kopyaları hello olağanüstü durum engellemez.

### <a name="operational-faults"></a>İşletimsel hataları
Hizmetinizi birçok açarken ile Merhaba dünya genelinde yayılmış olsa bile, yine felaket niteliğinde olayları yaşayabilirsiniz. Örneğin, birisi yanlışlıkla hello dns adı hello hizmeti için yeniden yapılandırır veya depolayabileceği siler. Örnek olarak, bir durum bilgisi olan Service Fabric hizmeti var ve biri hizmet yanlışlıkla silinirse varsayalım. Diğer bir azaltma sürece, bu hizmet ve tüm önceki hello durumunun olduğu şimdi gitti. Bu işlem olağanüstü türleri ("hata") farklı Azaltıcı Etkenler ve adımları kurtarma normal planlanmayan hatalar daha gerektirir. 

Bu tür işletimsel hataları üzeresiniz Hello en iyi yolu tooavoid
1. işletimsel erişim toohello ortamı kısıtla
2. kesinlikle denetim tehlikeli işlemleri
3. Otomasyon zorunlu tuttukları, el ile veya bant dışı değişiklikleri önlemek ve bunları ederek ilerlemesini kabul ederek önce belirli değişiklikleri hello gerçek ortama karşı doğrulama
4. bozucu operations "yumuşak" olduğundan emin olun. Yazılım işlemleri hemen etkinleşmesini yok veya bazı zaman penceresi içinde geri alınabilir

Service Fabric sağlama gibi işletimsel hataları tooprevent, bazı mekanizmalar sağlar [rol tabanlı](service-fabric-cluster-security-roles.md) erişim denetimi küme işlemleri için. Ancak, bu işlem hatalarının çoğu kuruluş çabalarına ve diğer sistemler gerektirir. Service Fabric işlem hataları, özellikle yedekleme geri kalan için bazı mekanizmaya ve durum bilgisi olan hizmetler için geri yükleyin.

## <a name="managing-failures"></a>Hataları yönetme
Service Fabric Hello amacı neredeyse her zaman otomatik hatalar yönetimidir. Bununla birlikte, içinde hataları bazı türleri toohandle sipariş, Hizmetler ek kod olması gerekir. Hataları diğer türleri gereken _değil_ otomatik olarak ele güvenliği ve iş sürekliliği nedenleriyle. 

### <a name="handling-single-failures"></a>Tek hataları işleme
Tek makineler, her türlü nedenleri için başarısız olabilir. Bunlardan bazıları, güç kaynakları ve donanım hatalarına ağ gibi donanım nedenler şunlardır. Diğer yazılım hatalarıdır. Bunlar hello gerçek işletim sistemi ve hello hizmetin kendisini hatalarının içerir. Service Fabric hello makinenin nerede toonetwork sorunları nedeniyle diğer makinelerden yalıtılmış hale durumlarda dahil hataları, bu tip otomatik olarak algılar.

Tek bir kopya hello kod herhangi bir nedenle başarısız olursa hizmet hello türü ne olursa olsun, bu hizmet için kapalı kalma süresi sonuçları tek bir örnek çalışıyor. 

Sipariş toohandle herhangi bir tek hata yapabileceğiniz hello basit hizmetlerinizi birden fazla düğüm üzerinde varsayılan olarak çalıştığı tooensure şeydir. Durum bilgisi olmayan hizmetler için bu sağlayarak gerçekleştirilebilir bir `InstanceCount` 1'den büyük. Durum bilgisi olan hizmetler için hello minimum her zaman önerilir bir `TargetReplicaSetSize` ve `MinReplicaSetSize` en az 3. Daha fazla hizmet kodunuzun kopyalarını çalıştıran hizmetinizi herhangi bir tek hata otomatik olarak ele almasını sağlar. 

### <a name="handling-coordinated-failures"></a>Eşgüdümlü işleme hataları
Eşgüdümlü hataları bir kümede tooeither planlanmış veya planlanmamış altyapı hataları ve değişiklikleri veya planlanan yazılım değişiklikleri nedeniyle oluşabilir. Service Fabric Eşgüdümlü hataları hata etki alanları olarak deneyimi altyapı bölgeleri modeller. Eşgüdümlü yazılım değişiklikleri yaşar alanları yükseltme etki alanları Modellenen. Hata ve yükseltme etki alanları hakkında daha fazla bilgi yer [bu belgeyi](service-fabric-cluster-resource-manager-cluster-description.md) küme topolojisi ve tanım açıklar.

Varsayılan olarak Service Fabric hata ve yükseltme etki alanı hizmetlerinizi çalıştırdığı planlarken göz önünde bulundurur. Varsayılan olarak, planlanmış veya planlanmamış değişiklikleri görülüyorsa hizmetlerinizin kullanılabilir olmaya devam etmesi için birçok hata ve yükseltme etki alanları arasında hizmetlerinizi çalıştırılan tooensure Service Fabric çalışır. 

Örneğin, güç kaynağı başarısız makineler toofail raf aynı anda neden olduğunu düşünelim. Hata etki alanı hatası birçok makineler hello kaybı çalışan hello hizmeti birden çok kopyası ile belirli bir hizmeti için tek hatası başka bir örneği dönüştürür. Hata etki alanlarını yönetme kritik tooensuring yüksek hizmetlerinizin kullanılabilirliğini olmasının budur. Service Fabric Azure'da çalıştırırken, hata etki alanlarını otomatik olarak yönetilir. Diğer ortamlarda bunlar olmayabilir. Şirket içi kendi kümeleri oluşturuyorsanız emin toomap olması ve hata etki alanı düzeninizi doğru şekilde planlayın.

Yükseltme etki alanları yazılım nerede bulunacağını toobe yükseltilene hello aynı modelleme için yararlı zaman. Bu nedenle, yükseltme etki alanları da genellikle yazılım planlanmış yükseltme sırasında nerede alınır hello sınırlarını tanımlayın. Yükseltmeler Service Fabric ve hizmetlerinizi izleyin hello aynı modeli. Yükseltme, yükseltme etki alanları ve istenmeyen değişiklikleri hello küme ve hizmetinizi etkileyen engeller hello Service Fabric sistem durumu modeli alma hakkında daha fazla bilgi için bu belgelere bakın:

 - [Uygulama yükseltme](service-fabric-application-upgrade.md)
 - [Uygulama yükseltme Öğreticisi](service-fabric-application-upgrade-tutorial.md)
 - [Service Fabric sistem durumu modeli](service-fabric-health-introduction.md)

Sağlanan hello küme eşlemesi kullanarak kümenizi hello düzenini görselleştirebilirsiniz [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Service Fabric Explorer'da hata etki alanları arasında yayılan düğümler][sfx-cluster-map]
</center>

> [!NOTE]
> Çalışan hizmet kodu ve durum, çok sayıda örneklerini çalışırken hatanın alanları modelleme yerleştirme kuralları tooensure hizmetlerinizi hata ve yükseltme etki alanları arasında çalıştırın ve yalnızca yerleşik sistem durumu izleme olan **bazı** Merhaba, Service Fabric sipariş tookeep normal işletim sorunları olmayan ve olağanüstü oturum açma hatalarından sağlar özellikleri. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Eşzamanlı donanım veya yazılım hataları işleme
Yukarıdaki tek hataları hakkında açıklandı. Gördüğünüz gibi durum bilgisiz ve durum bilgisi olan hizmetler için kolay toohandle hata ve yükseltme etki alanları arasında çalışan hello kodunu (ve durumu) fazla kopyasını tutarak var. Birden çok eşzamanlı rastgele hatalara de oluşabilir. Büyük olasılıkla toolead tooan gerçek olağanüstü durum bunlar.


### <a name="random-failures-leading-tooservice-failures"></a>Tooservice hataları önde gelen rasgele hataları
Merhaba hizmet olduğunu düşünelim bir `InstanceCount` düğümlerinin, 5 ve birkaç Bu örneklerde çalıştıran tüm hello aynı başarısız zaman. Service Fabric değiştirme örnekleri otomatik olarak diğer düğümlerde oluşturarak yanıt verir. Örnek sayısı tooits istenen hello hizmeti geri olana kadar değişiklik oluşturma devam eder. Başka bir örnek olarak, bir durum bilgisiz hizmetiyle vardı diyelim ki bir `InstanceCount`-1, tüm geçerli hello küme düğümleri üzerinde çalıştığı anlamına gelir. Bu örneklerde bazıları toofail olduğunu varsayalım. Bu durumda, Service Fabric hello hizmeti istenilen durumda değil ve toocreate hello hello düğümlerin eksik olduğu örneklerinde çalışır fark eder. 

Durum bilgisi olan hizmetler için olup hello hizmet durumu veya kalıcı üzerinde hello durumunuza bağlıdır. Ayrıca, kaç tane çoğaltmaları hello hizmeti yaşadı ve kaç tanesinin başarısız bağlıdır. Bir olağanüstü durum bilgisi olan bir hizmet için oluştu ve yönetmeyi üç aşamanın izleyen belirleme:

1. Kaydedilmediğine çekirdek kaybı olmadığını belirleme
 - Durum bilgisi olan hizmet hello çoğaltmalarının çoğunu aşağı hello hiçbir zaman çekirdek kayıp olduğundan hello birincil dahil olmak üzere aynı anda.
2. Merhaba çekirdek kayıp kalıcı olup olmadığını belirleme
 - Başlangıç saati, çoğu geçici hatalarıdır. İşlemleri yeniden başlatılır, düğümlerin yeniden, sanal makineleri yeniden, ağ bölümleri onarma. Bazen hataları kalıcı olmakla birlikte. 
    - Hizmetleri olmadan kalıcı için durumunda, bir çekirdek veya daha fazla çoğaltmaları sonuçları başarısızlığını _hemen_ kalıcı çekirdek kaybına. Service Fabric durum bilgisi olan kalıcı olmayan hizmetinde çekirdek kayıp algıladığında, hemen (potansiyel) bildirme tarafından 3 toostep dataloss ilerler. Devam etmeden toodataloss, bunlar kurtarılan olsa bile bunlar boş olacağından Service Fabric hello çoğaltmaları toocome geri bekleniyor hiçbir noktasında olduğunu bildiği için anlamlıdır.
    - Kalıcı durum bilgisi olan hizmetler için bir çekirdek veya daha fazla çoğaltması başarısız hello çoğaltmaları geri toocome ve geri yükleme çekirdek için bekleyen Service Fabric toostart neden olur. Bu bir hizmet kesintisi için sonuçları _Yazar_ etkilenen toohello hello hizmetinin bölüm (veya "çoğaltma kümesi"). Ancak, okuma hala azaltılmış tutarlılığı garanti ile mümkün olabilir. devam etmeden (olası) bir dataloss olayıdır ve diğer riskleri taşır hello varsayılan süreyi geri çekirdek toobe için Service Fabric bekler sonsuzdur. Merhaba varsayılan geçersiz kılma `QuorumLossWaitDuration` değer mümkündür, ancak önerilmez. Bunun yerine şu anda tüm çabalara toorestore hello çoğaltmaları aşağı yapılmalıdır. Bu arka yukarı hello düğümlerini getiren ve hello yerel kalıcı durumunu depolandığı hello sürücüleri yeniden bağlayabilirsiniz sağlama gerektirir. İşlem hatası tarafından Hello çekirdek kaybına neden olursa, Service Fabric otomatik olarak toorecreate hello işlemleri çalışır ve içerdikleri hello çoğaltmaları yeniden başlatın. Bu başarısız olursa, Service Fabric sistem durumu hataları bildirir. Bunlar çözümlenebilir, ardından hello çoğaltmaları genellikle geri dönün. Bazı durumlarda, yine de hello çoğaltmaları geri duruma getirilemiyor. Örneğin, hello sürücüleri tüm başarısız olmuş veya şekilde hello makineler fiziksel olarak yok. Bu durumda biz şimdi kalıcı çekirdek kayıp olay sahip. hello geri çoğaltmaları toocome bir Küme Yöneticisi aşağı bekleniyor tootell Service Fabric toostop biri Hizmetleri etkilenir ve çağrı hello hangi bölümlerini belirlemek gerekir `Repair-ServiceFabricPartition -PartitionId` veya ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API.  Bu API hello bölüm toomove QuorumLoss dışında ve olası dataloss halinde hello kimliği belirtebilirsiniz.

> [!NOTE]
> Bu _hiçbir zaman_ güvenli toouse dışında bu API hedeflenen bir şekilde belirli bölümlere göre. 
>

3. Gerçek veri kaybı yapıldıysa belirlemek ve yedeklerden geri yükleme
  - Service Fabric hello çağırdığında `OnDataLossAsync` olduğu her zaman nedeniyle yöntemi _şüpheli_ dataloss. Service Fabric sağlar bu çağrıyı toohello teslim edilmesini _en iyi_ kalan çoğaltma. Bu hesaptaki çoğaltma hello çoğu ilerleme olur. Merhaba neden her zaman dediğimiz _şüpheli_ dataloss olduğundan bu hello kalan çoğaltma oluştu olduğunda hello birincil yaptığınız gibi tüm aynı duruma gerçekte sahip mümkün olduğunu. Ancak, bu durum toocompare olmadan bu için iyi bir yolu yoktur Service Fabric veya işleçleri tooknow için emin. Bu noktada, Service Fabric ayrıca hello diğer çoğaltmaları bilir geri gelmelerini değil. Biz hello çekirdek kayıp tooresolve kendisi için bekleniyor durduğunda yapılan hello kararının. Merhaba iyi davranış biçimini hello hizmeti için genellikle toofreeze ve belirli yönetim müdahalesi bekle olur. Hello tipik uyarlamasını ne kadar `OnDataLossAsync` yöntemi musunuz?
  - İlk olarak, bu oturum `OnDataLossAsync` tetiklendi ve tüm gerekli Yönetim Uyarıları kapatmak tetiklenecek.
   - Genellikle bu noktada, toopause ve daha fazla kararları ve el ile gerçekleştirilen eylemleri toobe gerçekleştirilecek tamamlanmasını bekleyin. Yedeklemeleri kullanılabilir olsa bile hazırlanmış toobe gerekebilir olmasıdır. Örneğin, iki farklı hizmet bilgileri koordine etmek, bu yedekleri hello bilgi iki hizmetlere önem verdiğiniz hello geri yükleme gerçekleştikten sonra tutarlı sipariş tooensure değiştiren toobe gerekebilir. 
  - Genellikle de başka bir telemetri veya yoktur hello hizmetinden Egzoz. Bu meta veriler diğer hizmetlerin veya günlükleri içeriyor. Hello yedekleme ya da çoğaltılan toothis belirli çoğaltmasında mevcut değildi alınan ve hello birincil işlenen tüm çağrıları varsa bu bilgiyi kullanılan gerekli toodetermine olabilir. Geri yükleme uygulanabilirdir önce bu toobe yeniden yürütülmüş veya eklenen toohello yedekleme gerekebilir.  
   - Kullanılabilen tüm yedeklemelerinin bulunan yinelemenin durumu toothat kalan hello karşılaştırmaları. Araçlar ve bunu yapmak için kullanılabilir işler vardır hello Service Fabric güvenilir koleksiyonları kullanarak, açıklanan [bu makalede](service-fabric-reliable-services-backup-restore.md). Merhaba toosee hello çoğaltma içinde hello durumu yeterli ya da hangi hello yedekleme eksik olabilir ise hedeftir.
  - Merhaba karşılaştırma bir kez gerçekleştirilir ve gerekli hello geri yükleme tamamlandı, hello servis kodu durumu değişiklikler yapılmışsa true olarak döndürülmelidir. Merhaba çoğaltma hello en iyi kullanılabilir kopyasını hello durumu oluştu ve herhangi bir değişiklik olduğunu belirlediyseniz, false döndürür. TRUE gösteren herhangi bir _diğer_ çoğaltmaları kalan şimdi olabilir ile tutarsız. Bunlar bırakılacak ve bu çoğaltmasından yeniden. False gösterir şekilde hello durumu değişiklik yapıldığını diğer çoğaltmaları ne sahip oldukları tutabilirsiniz. 

Hizmetleri herhangi bir zamanda üretime dağıtılmadan önce hizmet yazarlar olası dataloss ve hata senaryoları alıştırma oldukça önemlidir. tooprotect dataloss hello olasılığını karşı olduğu önemli tooperiodically [hello durumu yedekleme](service-fabric-reliable-services-backup-restore.md) herhangi bir durum bilgisi olan hizmetler tooa coğrafi olarak yedekli depolama. Merhaba özelliği toorestore olduğundan da emin olun. Birçok farklı hizmet yedeklerini farklı zamanlarda alındığından tooensure geri yükledikten sonra birbiriyle tutarlı bir görünüm hizmetlerinizi olması gerekir. Örneğin, burada bir hizmet bir sayı oluşturur ve bunu depolar, sonra da depolar tooanother hizmeti gönderir bir durum düşünün. Bir geri yüklendikten sonra hello ikinci hizmet hello numarasına sahip ancak hello ilk desteklemez, bu işlem, yedekleme eklemediniz çünkü fark edebilirsiniz.

Bu hello kalan çıkışı gelen yetersiz toocontinue dataloss senaryosunda çoğaltmaları olan ve telemetri veya Egzoz hizmetinin durumunu yeniden yapılandırma görürseniz, en iyi, olası kurtarma noktası hedefi (RPO) Yedeklemelerinizin hello sıklığını belirler . Service Fabric kalıcı çekirdek ve bir yedekten geri yükleme gerektiren dataloss dahil olmak üzere çeşitli hatası senaryoları test etmek için birçok araçlar sağlar. Bu senaryolar, Service Fabric'ın Test Edilebilirlik araçları, hello hata analizi hizmeti tarafından yönetilen bir parçası olarak dahil edilir. Bu araçlar ve desenleri hakkında daha fazla bilgi edinilebilir [burada](service-fabric-testability-overview.md). 

> [!NOTE]
> Sistem Hizmetleri ile Merhaba etkisi belirli toohello hizmet söz konusu olan çekirdek kayıp zarar görebilir. Örneği için yeni hizmet oluşturma ve yük devretme işlemlerini hello Yük Devretme Yöneticisi hizmeti çekirdek kaybında engeller ancak hello adlandırma hizmeti çekirdek kaybında ad çözümlemesi etkiler. Merhaba Service Fabric sistem hizmetleri aynı deseni, Durum Yönetimi Hizmetleri olarak hello izleyin, ancak bu toomove denemelidir önerilmez çekirdek kayıp dışında ve olası dataloss halinde bunları. Merhaba önerilir bunun yerine çok[destek arama](service-fabric-support.md) toodetermine bir çözüm hedeflenen tooyour özel durum.  Genellikle hello çoğaltmaları dönüş aşağı kadar tercih toosimply bekleme olur.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Merhaba Service Fabric kümesi kullanılabilirliği
Hiçbir tek hata noktaları bulundurmaktan ile Merhaba Service Fabric kümesi kendisini genel olarak bakıldığında, yüksek oranda dağıtılmış bir ortamdır. Öncelikle hello Service Fabric sistem hizmetleri aynı yönergeleri sağlanan önceki hello izledikleri için herhangi bir düğümü kullanılabilirlik ve güvenilirlik sorunlarını hello kümesi için neden: Bunlar her zaman üç veya daha fazla yinelemelerle varsayılan ve bunlar tarafından Çalıştır Durum bilgisiz Sistem Hizmetleri tüm düğümler üzerinde çalıştırın. Merhaba temel Service Fabric ağ ve hata algılama Katmanlar tam olarak dağıtılır. Çoğu Sistem Hizmetleri hello kümedeki meta verilerden yeniden veya biliyorsanız nasıl tooresynchronize durumlarına diğer yerlerden. Sistem Hizmetleri Çekirdek kayıp durumları açıklananlar gibi yukarıdaki alırsanız hello küme hello kullanılabilirliğini tehlikeye haline gelir. Bu durumlarda operations hello kümede bir yükseltmeye başlatmadan veya yeni hizmetlerin dağıtımı gibi çalışır, ancak hello kümenin kendisi hala çalışıyor belirli mümkün tooperform olmayabilir. Yazma toohello Sistem Hizmetleri toocontinue çalışmasını gerektirmedikçe zaten çalıştırma Hizmetleri bu koşulları çalışır durumda. Örneğin, çekirdek kaybında hello Yük Devretme Yöneticisi ise, tüm hizmetleri toorun devam edecek, ancak bu hello Yük Devretme Yöneticisi hello katılımı gerektirdiğinden başarısız hizmetlerin mümkün tooautomatically yeniden olmaz. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Bir veri merkezi veya Azure bölgesinin hataları
Nadir durumlarda, bir fiziksel veri merkezi nedeniyle geçici olarak kullanılamaz hale gelebilir güç veya ağ bağlantısının tooloss. Bu durumlarda, Service Fabric kümeleri ve o veri merkezi ya da Azure bölgesi Hizmetleri kullanılamaz olacaktır. Ancak, _verileriniz korunur_. Azure'da çalışan kümeler için güncelleştirmeleri kesintileri hello üzerinde görüntüleyebilirsiniz [Azure durum sayfasına][azure-status-dashboard]. Merhaba kısmen veya tamamen fiziksel veri merkezidir düşüktür olay yok, var. barındırılan tüm Service Fabric kümeleri veya hello Hizmetleri içerdikleri kaybolabilir. Bu, bu veri merkezi veya bölge dışında yedeklenmeyen herhangi bir durumu içerir.

Geri kalan iki farklı stratejileri yoktur hello tek datacenter veya bölgesinin kalıcı veya sürekli hatası. 

1. Bu tür birden çok bölgede ayrı Service Fabric kümeleri çalıştırın ve yük devretme ile geri bu ortamlar arasında bazı mekanizması kullanır. Bu tür bir çoklu küme etkin-etkin veya etkin-pasif modeli ek yönetimi ve işlemleri kodu gerektirir. Bu, ayrıca diğer veri merkezleri veya bir zaman bölgelerde kullanılabilir olacak şekilde, bir veri merkezi veya bölgede hello Hizmetleri yedeklemelerden eşgüdümünü başarısız gerektirir. 
2. Birden çok veri merkezleri veya bölgeler kapsayan tek bir Service Fabric kümesi çalıştırın. Merhaba minimum desteklenen için bu üç veri merkezleri veya bölgeler yapılandırmadır. bölgeler sayısı Hello önerilen veya veri merkezleri beştir. Bu, daha karmaşık bir küme topolojisi gerektirir. Ancak, hello Bu modelin avantajı bir veri merkezi veya bölge başarısızlığını normal bir hata olağanüstü durumdan dönüştürülür olur. Bu hatalar, tek bir bölge içinde kümeleri için iş hello mekanizmaları tarafından işlenebilir. Hata etki alanlarını, yükseltme etki alanları ve Service Fabric'ın yerleştirme kuralları normal hataları tolerans böylece iş yükleri dağıtılır emin olun. Bu tür bir küme Hizmetler'in çalıştırılmasında yardımcı olan ilkeleri hakkında daha fazla bilgi için okumaya devam [yerleşim ilkeleri](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)

### <a name="random-failures-leading-toocluster-failures"></a>Toocluster hataları önde gelen rasgele hataları
Service Fabric çekirdek düğüm hello kavramı vardır. Merhaba temel küme hello kullanılabilirliğini sürdürmek düğümleri bunlar. Bu düğümler tooensure hello küme kalır diğer düğümlerle kiraları oluşturma ve belirli türdeki ağ hataları sırasında tiebreakers hizmet veren yardımcı. Rastgele hatalara hello çekirdek düğüm çoğunluğu hello kümede kaldırmak ve geri getirilmez, hello küme otomatik olarak kapanır. Azure'da, çekirdek düğümler otomatik olarak yönetilir: hello kullanılabilir hata ve yükseltme etki alanları dağıtılan ve tek çekirdek değer düğümü hello kümeden kaldırılırsa, onun yerine başka bir oluşturulur. 

Tek başına Service Fabric kümeleri hem Azure hello "Birincil düğüm türü" Merhaba hello oluştururken çekirdeği çalıştıran biri ' dir. Birincil düğüm türü tanımlarken, Service Fabric otomatik olarak hello too9 çekirdek düğüm ve her bir hello Sistem Hizmetleri 9 çoğaltmaları yedeklemek oluşturarak sağlanan düğüm sayısını yararlanır. Rastgele hatalara bir dizi sistem hizmeti yinelemeler çoğunu aynı anda alırsa, biz yukarıda açıklandığı gibi hello Sistem Hizmetleri Çekirdek kayıp girer. Merhaba çekirdek düğüm çoğunluğu kaybolursa hello küme kısa süre içinde kapanır.

## <a name="next-steps"></a>Sonraki adımlar
- Bilgi nasıl toosimulate hello kullanarak çeşitli hatalar [Test Edilebilirlik framework](service-fabric-testability-overview.md)
- Olağanüstü durum kurtarma ve yüksek kullanılabilirlik kaynaklar okuyun. Microsoft bu konular üzerinde büyük bir miktarını kılavuzunun yayımladı. Bu belgelerin toospecific teknikleri diğer ürünleri kullanmak için başvurmak olsa da, birçok genel en iyi yöntemler de hello Service Fabric bağlamda uygulayabilirsiniz içerir:
  - [Kullanılabilirlik denetim listesi](../best-practices-availability-checklist.md)
  - [Bir olağanüstü durum kurtarma ayrıntıya gerçekleştirme](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma][dr-ha-guide]
- [Service Fabric destek seçenekleri](service-fabric-support.md) hakkında bilgi edinin

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
