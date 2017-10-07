---
title: "aaaDesign olağanüstü durum kurtarma çözümleri - Azure SQL veritabanı | Microsoft Docs"
description: "Bilgi nasıl toodesign bulut çözümünüzü hello sağ yük düzeni seçerek olağanüstü durum kurtarma."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>SQL Database esnek havuzları kullanan uygulamalar için olağanüstü durum kurtarma stratejileri
Merhaba yıllar içinde biz bulut Hizmetleri kusursuz değildir ve geri dönülemez olaylar gerçekleşir öğrendiniz. Bu olaylar gerçekleştiğinde SQL veritabanı, uygulamanızın iş sürekliliği hello çeşitli özellikleri tooprovide sağlar. [Esnek havuzlar](sql-database-elastic-pool.md) ve tek veritabanlarını desteklemek hello olağanüstü durum kurtarma özellikleri aynı türde. Esnek havuz için bu makalede birkaç DR stratejilerini açıklar. Bu SQL veritabanını iş sürekliliği özelliklerden yararlanın.

Bu makalede kurallı SaaS ISV uygulama düzeni aşağıdaki hello kullanır:

<i>Modern bulut tabanlı web uygulamasının her son kullanıcı için bir SQL veritabanı sağlar. Merhaba ISV birçok müşteri vardır ve bu nedenle Kiracı veritabanları olarak bilinen birçok veritabanı kullanır. Merhaba Kiracı veritabanları genellikle öngörülemeyen etkinlik desenlerini sahip olduğundan hello ISV bir esnek havuz toomake hello veritabanı maliyeti çok tahmin edilebilir uzun süreler boyunca kullanır. Merhaba kullanıcı etkinliği ani zaman hello esnek havuz da hello performans yönetimini basitleştirir. Ayrıca toohello Kiracı veritabanları Merhaba uygulaması birkaç veritabanlarını da kullanan toomanage kullanıcı profilleri, güvenlik, kullanım desenlerini vb. topla. Merhaba tek tek kiracılar kullanılabilirliğini bütün olarak hello uygulamanın kullanılabilirliğini etkilemez. Ancak, hello kullanılabilirliğini ve performansını yönetim veritabanları hello uygulamanın işlevi için kritik öneme sahiptir ve hello yönetim veritabanları çevrimdışı hello tüm uygulama olduğunda çevrimdışı olur.</i>  

Bu makalede maliyet hassas başlangıç uygulamaları tooones sıkı kullanılabilirlik gereksinimleri olan senaryolarından aralığını kapsayan DR stratejiler açıklanmaktadır.

## <a name="scenario-1-cost-sensitive-startup"></a>Senaryo 1. Hassas başlangıç maliyeti
<i>Bir başlangıç iş 'M ve son derece hassas maliyet bildirimi.  Toosimplify dağıtımını ve yönetimini Merhaba uygulaması istediğiniz ve tek tek müşteriler için sınırlı bir SLA olabilir. Ancak bir bütün hiçbir zaman çevrimdışı olduğu gibi tooensure Merhaba uygulaması istiyorum.</i>

toosatisfy hello Basitlik gereksinim hello Azure bölgesi tercih ettiğiniz bir esnek havuzda içine tüm Kiracı veritabanları dağıtmak ve yönetim veritabanları coğrafi olarak çoğaltılmış tek veritabanları olarak dağıtın. İçin Hello olağanüstü durum kurtarma kiracıların coğrafi hiçbir ek ücret gelen geri yükleme, kullanın. tooensure hello kullanılabilirliğini yönetim veritabanları, coğrafi replicate bunları hello otomatik yük devretme grubu (içinde-önizleme) (1. adım) kullanılarak tooanother bölge. Merhaba devam eden hello olağanüstü durum kurtarma yapılandırması bu senaryoda eşit toohello toplam sahip olma maliyeti hello ikincil veritabanlarıyla maliyetidir. Bu yapılandırma hello sonraki diyagramda gösterilmiştir.

![Şekil 1](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

Merhaba birincil bölgede bir kesinti oluşursa, Kurtarma adımları toobring uygulamanızı çevrimiçi hello sonraki diyagram tarafından gösterilen hello.

* Merhaba yük devretme grubu otomatik yük devretme hello yönetim veritabanı toohello DR bölgesinin başlatır. Merhaba uygulaması otomatik olarak yeniden bağlanan toohello yeni birincil ve tüm yeni hesaplar ve Kiracı veritabanları hello DR bölgede oluşturulur. Merhaba mevcut müşteriler geçici olarak devre dışı verilerini bakın.
* Merhaba ile Merhaba esnek havuz oluşturma aynı yapılandırmaya hello özgün havuz (2).
* Coğrafi geri yükleme toocreate kopyalarını hello Kiracı veritabanı (3) kullanın. Merhaba tek tek geri yüklemeler hello son kullanıcı bağlantılar tarafından tetikleme göz önünde bulundurun veya başka bir uygulamaya özgü Öncelik düzenini kullanın.


Bu noktada, uygulamanızın hello DR bölgede tekrar çevrimiçi değil, ancak bazı müşteriler kendi verilere erişirken gecikme olur.

![Şekil 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Merhaba kesinti geçici varsa, tüm hello veritabanı geri yüklemeler hello DR bölgede tam önce o hello birincil bölge Azure tarafından kurtarılan mümkündür. Bu durumda, taşıma hello uygulama arka toohello birincil bölge yönetirler. Merhaba işlem hello sonraki diyagramda gösterildiği hello tedbirleri alır.

* Tüm bekleyen coğrafi geri yükleme istekleri iptal edin.   
* Merhaba yönetim veritabanları toohello birincil bölge üzerinde (5) başarısız. Merhaba bölgenin kurtarma işleminden sonra hello eski ana otomatik olarak ikincil hale getirildi. Şimdi bunların rolleri yeniden geçin. 
* Merhaba uygulamanın bağlantı dizesi toopoint geri toohello birincil bölge değiştirin. Şimdi tüm yeni hesaplarını ve Kiracı veritabanları hello birincil bölgede oluşturulur. Bazı var olan müşteriler geçici olarak devre dışı verilerini bakın.   
* Tüm veritabanları hello DR bölgede (6) değiştirilemez hello DR havuzu yalnızca tooread tooensure ayarlayın. 
* Her bir veritabanı hello hello kurtarma bu yana değişti DR havuzu içinde yeniden adlandırın veya hello karşılık gelen veritabanlarını hello birincil havuzunda (7) silin. 
* Kopya hello hello DR toohello birincil havuzu (8) veritabanlarından güncelleştirildi. 
* Merhaba DR havuzu (9) Sil

Bu noktada, uygulamanız tüm Kiracı veritabanları ile kullanılabilir hello birincil havuzunda hello birincil bölgede çevrimiçidir.

![Şekil 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

başlangıç anahtarı **yararlı** bu strateji düşük devam eden veri katmanı artıklığı maliyetidir. Yedeklemeleri hello hiçbir ek ücret ödemeden hiçbir uygulama yeniden yazma ile SQL veritabanı hizmeti tarafından otomatik olarak alınır.  Merhaba maliyet hello esnek veritabanları yalnızca geri yüklendiğinde oluşur. Merhaba **dengelemeyi** hello tam kurtarma tüm Kiracı veritabanlarının önemli zaman gerçekleştirir. Merhaba süre hello DR başlatmak geri yüklemeler toplam sayısı hello bağlıdır bölge ve hello toplam boyutunu veritabanlarını Kiracı. Bazı kiracılar geri yüklemeler diğerlerine göre daha öncelikli olsa bile, rekabet halinde olduğunuz hello hizmet istemlerde ve toominimize kısıtlar tüm hello ile aynı bölgede başlatılan diğer geri yüklemeler hello hello hello mevcut müşterilerin veritabanlarında genel etkisi. Ayrıca, Hello yeni esnek havuz hello DR bölgede oluşturulana kadar hello Kiracı veritabanlarının hello kurtarma başlatamıyor.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Senaryo 2. Katmanlı hizmetiyle olgun uygulama
<i>Katmanlı hizmet teklifleri ve deneme müşteriler ve müşterilerin ödeme için farklı SLA ile olgun bir SaaS uygulaması ben. Merhaba deneme müşteriler için mümkün olduğunca maliyet tooreduce hello sahibim. Deneme müşteriler kapalı kalma süresi alabilir ancak kendi olasılığını tooreduce istiyorum. Müşteriler ödeme hello için kapalı kalma süresi uçuş sorununa neden olur. Toomake ödeyen müşteri her zaman mümkün tooaccess olmasını istediğiniz şekilde verilerini.</i> 

Bu senaryo, ayrı hello deneme kiracılardan toosupport ayrı esnek havuzları halinde koyarak kiracılar Ücretli. Merhaba deneme müşterilerin Kiracı ve alt SLA daha uzun bir kurtarma süresi ile başına alt eDTU sahip. Merhaba ödeyen Kiracı ve daha yüksek bir SLA başına daha yüksek eDTU ile bir havuzdaki müşterilerdir. tooguarantee hello düşük kurtarma süresini, coğrafi olarak çoğaltılmış hello ödeyen müşterilerin Kiracı veritabanları. Bu yapılandırma hello sonraki diyagramda gösterilmiştir. 

![Şekil 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Tek bir coğrafi olarak çoğaltılmış veritabanı için (1) kullandığınız şekilde hello ilk senaryoda olduğu gibi hello yönetim veritabanları oldukça etkindir. Bu yeni kullanıcı aboneliklerini, profil güncelleştirmeleri ve diğer yönetim işlemleri için hello tahmin edilebilir performans sağlar. Merhaba hello ana hello yönetim veritabanlarının bulunduğu bölge hello birincil bölge ve hello ikinciller hello yönetim veritabanlarının bulunduğu hello bölge hello DR bölgesi.

Merhaba ödeyen müşteri Kiracı veritabanı etkin veritabanları "Merhaba birincil bölge içinde sağlanan havuzu Ücretli" Merhaba sahip. İkincil bir havuzu hello hello DR bölgede aynı ad ile sağlayın. Her bir kiracı toohello coğrafi olarak çoğaltılmış ikincil havuzu (2) değil. Bu, yük devretme kullanarak tüm Kiracı veritabanlarını Hızlı Kurtarma sağlar. 

Uygulamanızı çevrimiçi hello birincil bölgede hello kurtarma adımları toobring bir kesinti oluşursa hello sonraki şemada gösterilmiştir:

![Şekil 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Hemen hello yönetim veritabanları toohello DR bölge (3) başarısız.
* Merhaba uygulamanın bağlantı dizesi toopoint toohello DR bölge değiştirin. Şimdi tüm yeni hesaplarını ve Kiracı veritabanları hello DR bölgede oluşturulur. Merhaba varolan deneme müşteriler geçici olarak devre dışı verilerini bakın.
* Yük devretme kiracının veritabanları toohello hello DR bölge tooimmediately havuzunda Ücretli hello kullanılabilirliklerini (4) geri yükleyin. Merhaba yük devretme hızlı meta veri düzeyi değişikliği olduğundan, burada hello bireysel yük devretme isteğe bağlı hello son kullanıcı bağlantılar tarafından tetiklenen bir iyileştirme göz önünde bulundurun. 
* Yalnızca gerekli hello kapasite tooprocess hello değişikliği bunlar sırasında ikincil kopya, olan günlükleri hello ikincil veritabanlarıyla hemen artırmak için hello havuz kapasitesi ikincil havuz eDTU boyutu hello birincil alt varsa şimdi tooaccommodate hello tam iş yükünü tüm kiracılar (5). 
* İle aynı ad ve aynı hello hello Hello yeni esnek havuz oluşturma hello DR bölgede hello deneme müşterilerin veritabanları (6) için yapılandırma. 
* Merhaba deneme müşterilerin havuzu oluşturulduktan sonra coğrafi geri yükleme toorestore hello tek tek deneme Kiracı veritabanları hello yeni havuza (7) kullanın. Merhaba tek tek geri yüklemeler hello son kullanıcı bağlantılar tarafından tetikleme göz önünde bulundurun veya başka bir uygulamaya özgü Öncelik düzenini kullanın.

Bu noktada, uygulamanızın hello DR bölgede tekrar çevrimiçi değil. Tüm ödeyen müşteri erişimi tootheir verileri hello deneme müşteriler kendi verilere erişirken gecikme olur.

Ne zaman hello birincil bölge kurtarılan Azure tarafından *sonra* Merhaba uygulaması bu bölgede Merhaba uygulaması çalıştıran devam edebilirsiniz hello DR bölgede geri veya toofail geri toohello birincil bölge karar verebilirsiniz. Merhaba birincil bölge kurtarıldığında *önce* hello yük devretme işlemi tamamlandığında, sonradan başarısız olan hemen göz önünde bulundurun. Merhaba geri dönme hello sonraki diyagramda gösterildiği hello adımları gerçekleştirir: 

![Şekil 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Tüm bekleyen coğrafi geri yükleme istekleri iptal edin.   
* Merhaba yönetim veritabanları (8) başarısız. Merhaba bölgenin kurtarma işleminden sonra hello eski birincil otomatik hale hello ikincil. Bu duruma şimdi yeniden birincil hello.  
* Kiracı veritabanı (9) Ücretli hello başarısız. Benzer şekilde, hello bölgenin kurtarma işleminden sonra hello eski ana otomatik olarak hello ikinciller haline gelir. Şimdi hello ana yeniden olduklarında. 
* Set hello hello DR bölge yalnızca tooread (10) değiştirilmiştir deneme veritabanları geri.
* Her veritabanı hello kurtarma beri değiştirilen hello deneme müşteriler DR havuzunda yeniden adlandırın veya hello karşılık gelen veritabanı hello deneme müşteriler birincil havuzunda (11) silin. 
* Kopya hello hello DR toohello birincil havuzu (12) veritabanlarından güncelleştirildi. 
* Merhaba DR havuzu (13) Sil 

> [!NOTE]
> Merhaba yük devretme işlemi zaman uyumsuzdur. toominimize hello kurtarma süresini en az 20 veritabanları toplu olarak hello Kiracı veritabanı yük devretme komutu yürütün önemlidir. 
> 
> 

başlangıç anahtarı **yararlı** bu strateji onu hello yüksek SLA müşteriler ödeme Merhaba sağlamasıdır. Ayrıca, hello deneme DR havuzu oluşturulduktan hemen hello yeni denemeler engeli garanti eder. Merhaba **dengelemeyi** müşteriler Ücretli bu kurulumu hello toplam maliyeti hello Kiracı veritabanı tarafından hello ikincil DR havuzu için hello maliyetini artırır. Ayrıca, farklı bir boyut Hello ikincil havuzu varsa, hello hello DR bölgede havuzu yükseltme tamamlanana kadar hello ödeyen müşteriler yük devretme sonrasında düşük performans yaşar. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Senaryo 3. Katmanlı hizmetiyle coğrafi olarak dağıtılmış uygulama
<i>Katmanlı hizmet teklifleri ile olgun bir SaaS uygulaması var. Toooffer müşteriler Ücretli çok agresif bir SLA toomy istediğiniz ve hatta kısa kesinti müşteri memnuniyetsizliği neden olabileceğinden kesintiler durumunda etkisi hello riskini en aza bildirimi. Müşteriler ödeme o hello her zaman verilerine erişmeye önemlidir. Merhaba denemeler ücretsizdir ve bir SLA hello deneme süresi boyunca önerilmez.</i> 

toosupport bu senaryo, üç ayrı esnek havuzu kullanın. Sağlama iki eşit boyutu havuzlarıyla iki farklı bölgelerde toocontain hello veritabanında başına yüksek Edtu müşterilerin Kiracı veritabanı Ücretli. Merhaba deneme kiracıları içeren hello üçüncü havuzu hello iki bölgede birinde sağlanması ve veritabanı başına alt Edtu olabilir.

tooguarantee hello düşük kurtarma süresini kesintiler sırasında her iki hello bölgelerinin hello birincil veritabanlarının % 50 ile coğrafi olarak çoğaltılmış hello ödeyen müşterilerin Kiracı veritabanları. Benzer şekilde, her bölge hello ikincil veritabanlarıyla % 50'si vardır. Bu şekilde, bir bölge çevrimdışıysa, müşterilerin veritabanları Ücretli hello % 50'yalnızca etkilenen ve üzerinden toofail sahip. Merhaba diğer veritabanlarına değişmeden kalır. Bu yapılandırma hello Aşağıdaki diyagramda gösterilmiştir:

![Şekil 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Bu nedenle Hello önceki senaryolarda hello yönetim veritabanları oldukça etkin olarak bunları olarak tek coğrafi olarak çoğaltılmış veritabanları (1) yapılandırın. Bu hello yeni kullanıcı aboneliklerini, profil güncelleştirmeleri ve diğer yönetim işlemleri hello tahmin edilebilir performans sağlar. Bölge A hello birincil hello yönetim veritabanları için bölgedir ve hello bölge B hello yönetim veritabanlarını kurtarmak için kullanılır.

coğrafi olarak çoğaltılmış Hello ödeyen müşterilerin Kiracı veritabanları aynı zamanda, ancak ana ve ikincil bir bölge ve bölge B (2) arasında bölme. Bu şekilde toohello hello Kiracı birincil veritabanı hello kesintisi etkilenen başarısız diğer bölgeye ve kullanılabilir hale gelir. diğer yarısı hello Kiracı veritabanları olan değil etkilenebilir hiç hello. 

A. bölgede bir kesinti oluşursa hello sonraki diyagram hello kurtarma adımları tootake gösterir.

![Şekil 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Hemen hello yönetim veritabanları tooregion B (3) başarısız.
* Merhaba uygulamanın bağlantı dizesi toopoint toohello yönetim veritabanlarında bölge B. değiştirme hello yönetim veritabanları toomake hello yeni hesaplar ve Kiracı veritabanları B bölgede oluşturulur ve hello varolan Kiracı veritabanları var. bulunduğunda emin değiştirme olarak iyi. Merhaba varolan deneme müşteriler geçici olarak devre dışı verilerini bakın.
* Ücretli hello kiracının veritabanları toopool 2 bölge B tooimmediately Restore üzerinden kullanılabilirliklerini (4) başarısız. Merhaba yük devretme hızlı meta veri düzeyi değişikliği olduğundan, burada hello bireysel yük devretme isteğe bağlı hello son kullanıcı bağlantılar tarafından tetiklenen bir iyileştirme düşünebilirsiniz. 
* Bu yana 2 havuzuna yalnızca birincil veritabanlarını içeren artık hello havuzu artar toplam iş yükündeki hello ve hemen eDTU boyutuna (5) artırabilir. 
* İle aynı ad ve aynı hello hello Hello yeni esnek havuz oluşturma hello bölgede B hello deneme müşterilerin veritabanları (6) için yapılandırma. 
* Merhaba havuzu (7) hello havuza kullanım coğrafi geri yükleme toorestore hello tek tek deneme Kiracı veritabanı oluşturulduktan sonra. Merhaba tek tek geri yüklemeler hello son kullanıcı bağlantılar tarafından tetikleme göz önünde bulundurun veya başka bir uygulamaya özgü Öncelik düzenini kullanın.

> [!NOTE]
> Merhaba yük devretme işlemi zaman uyumsuzdur. toominimize hello kurtarma süresini en az 20 veritabanları toplu olarak hello Kiracı veritabanı yük devretme komutu yürütün önemlidir. 
> 

Bu noktada uygulamanız B. bölgede tekrar çevrimiçi değil Tüm ödeyen müşteri erişimi tootheir verileri hello deneme müşteriler kendi verilere erişirken gecikme olur.

Bölge A kurtarıldığında deneme müşteriler veya geri dönme toousing hello deneme müşteriler havuzu A. bölgede toouse bölge B istiyorsanız toodecide gerekir Tek bir ölçüt hello % deneme Kiracı veritabanlarının hello kurtarma beri değiştirilmiş olabilir. Bu karar bağımsız olarak toore Bakiye Ücretli hello kiracılar iki havuzları arasında gerekir. Merhaba deneme Kiracı veritabanlarını geri tooregion A. başarısız olduğunda hello sonraki diyagram hello işlemini gösterir.  

![Şekil 6](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Tüm bekleyen coğrafi geri yükleme istekleri tootrial DR havuzu iptal edin.   
* Merhaba yönetim veritabanı (8) başarısız. Merhaba bölgenin kurtarma işleminden sonra hello eski birincil hello ikincil otomatik hale geldi. Bu duruma şimdi yeniden birincil hello.  
* 1 ve başlatma geri toopool yük devretme tootheir ikinciller (9) hangi Ücretli Kiracı veritabanları başarısız seçin. Merhaba bölgenin kurtarma işleminden sonra 1 havuzdaki tüm veritabanları otomatik olarak ikincil hale geldi. Şimdi bunların % 50 ana yeniden haline gelir. 
* Havuz 2 toohello özgün eDTU (10) Hello boyutunu azaltın.
* Tüm kümesi B yalnızca tooread (11) hello bölgede deneme veritabanlarını geri.
* Her veritabanı havuzundaki hello kurtarma bu yana değişen hello deneme DR için yeniden adlandırın veya hello karşılık gelen veritabanı hello deneme birincil havuzunda (12) silin. 
* Kopya hello hello DR toohello birincil havuzu (13) veritabanlarından güncelleştirildi. 
* Merhaba DR havuzu (14) Sil 

başlangıç anahtarı **avantajları** bu stratejisi şunlardır:

* Bu, kesinti hello Kiracı veritabanları % 50'den fazla etkisi olamaz sağlar çünkü müşterilerin ödeme Merhaba hello en agresif SLA destekler. 
* Merhaba izi DR havuzu hello Kurtarma sırasında oluşturulan hemen hello yeni denemeler engeli güvence altına alır. 
* Merhaba havuz kapasitesi 1 havuzundaki ikincil veritabanlarıyla % 50 olarak daha verimli kullanılmasına izin verir ve 2 havuzuna garanti edilir toobe hello birincil veritabanları daha az etkin.

Merhaba ana **dengelemeler** şunlardır:

* Merhaba yönetim veritabanları hello birincil karşı yürütülen gibi hello CRUD işlemleri hello yönetim veritabanlarında hello bağlı olan son kullanıcıların tooregion A hello bağlı olan son kullanıcıların tooregion B için için daha düşük gecikme süresine sahiptir.
* Daha karmaşık bir tasarım hello yönetim veritabanının gerektirir. Örneğin, her bir kiracı kaydı yük devretme ve yeniden çalışma sırasında değiştirilmiş toobe gereken bir konum etiketi yok.  
* Hello B bölgede havuzu yükseltme tamamlanana kadar müşteriler ödeme hello normalden daha düşük performans düşebilir. 

## <a name="summary"></a>Özet
Bu makalede bir SaaS ISV çok kiracılı uygulama tarafından kullanılan hello veritabanı katmanı için hello olağanüstü durum kurtarma stratejileri odaklanır. Merhaba seçtiğiniz stratejisi hello iş modeli, hello SLA gibi hello uygulamanızın hello gereksinimlerine bağlıdır toooffer tooyour müşterilerin, bütçe kısıtlaması vs. Bilinçli karar böylece her stratejisi anahatları hello avantajları ve dengelemeyi açıklanmıştır. Ayrıca, büyük olasılıkla belirli uygulamanızı Azure diğer bileşenleri içerir. Böylece, iş sürekliliği Kılavuzu gözden geçirebilir ve bunlarla hello veritabanı katmanı hello kurtarılması düzenlemek. Azure, veritabanı uygulamalarında kurtarılması yönetme hakkında daha fazla toolearn başvurmak çok[tasarlama bulut çözümleri olağanüstü durum kurtarma için](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Sonraki adımlar
* Azure SQL veritabanı otomatik yedeklemeler hakkında toolearn bkz [SQL veritabanı yedeklemeleri otomatik](sql-database-automated-backups.md).
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).
* Kurtarma için otomatik yedeklemeler kullanma hakkında toolearn bkz [bir veritabanını hello hizmeti tarafından başlatılan yedeklerden geri](sql-database-recovery-using-backups.md).
* toolearn daha hızlı kurtarma seçenekleri hakkında bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).
* arşivleme için otomatik yedeklemeler kullanma hakkında toolearn bkz [veritabanı kopyalama](sql-database-copy.md).

