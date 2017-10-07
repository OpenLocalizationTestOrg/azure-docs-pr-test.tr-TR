---
title: "aaaAzure SQL veritabanı Azure örnek olay incelemesi - Daxko/CSI | Microsoft Docs"
description: "Müşteri Hizmetleri ve performans Daxko/CSI SQL veritabanı tooaccelerate tooenhance ve geliştirme döngüsü kullanma hakkında bilgi edinin"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI kullanılan Azure tooaccelerate tooenhance ve geliştirme döngüsü, müşteri hizmetleri ve performans
![Daxko/CSI logosu](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Daxko/CSI yazılım karşılaştığı bir sınama: Müşteri tabanı uygunluk ve dinlenme merkezlerinin hızlı bir şekilde, teşekkürler toohello kapsamlı Kurumsal yazılım çözümünün başarısını büyüyen olsa da, BT altyapısı gereken bu büyüyen için hello tutma Müşteri tabanı hello şirketin test BT personeli. Hello şirket gittikçe büyüyen veritabanlarını yönetmek için özellikle yükselen işlemlerinin yükünü kısıtlanmış. Da kötüsü, bu işlem yükünü hello şirketin yazılım yeni mobility özellikleri gibi yeni girişimleri için geliştirme kaynakları içine kesme.

TooDavid Molina göre Daxko/CSI adresindeki ürün geliştirme Director, Azure sağlanan CSI yazılım toosimplify veritabanı yönetimi, gerekli hello hizmet olarak platform (PaaS) modeliyle ölçeklenebilirliği artırmak ve kaynakları toofocus üzerinde boşaltın ops yerine yazılım. "Azure SQL Database bize için harika bir seçenek oluştu. SQL Server, yük devretme kümesi ve tüm hello bakımı hakkında tooworry olmamasından diğer Altyapı gereksinimlerini bize için ideal."

Bu yana tooAzure geçirme, CSI yazılım yalnızca iki toomanage bir işlem personeli 600 müşteri veritabanları gerekiyor. Merhaba şirket toomove müşteri veritabanları boyutuna göre ve gereken Azure SQL Database esnek havuzlar kullanır.

Molina devam eder, "müşterilerimize hemen değiştirmek hello Keçeli. Esnek havuzları önce bazen zaman aşımları ve diğer sorunlar veri bloğu dönemlerde sahip oldukları. Azure esnek havuzları ile bunlar gerektiği gibi veri bloğu ve hello yazılım sorun olmadan kullanın."

Ayrıca Azure esnek havuzlar tooimproving performans müşteriler için yeni hizmetler ve özellikler, işlemler ve yönetim postalarla yerine geliştirme toofocus CSI yazılım kaynakları serbest. BT kaynaklarla CSI sunumu, SpectrumNG, toohelp, kurumsal yazılımlarının artırmak yazılım Yardım devreye Spor salonu üyeleri, personel verimliliğini artırmak ve personeli ve üyeleri etkileşimli görevler ve gerçek zamanlı bildirimler için mobil erişim verin.

Azure ayrıca CSI hızlandırmak ve Otomasyon seçenekleri sağlayarak hello geliştirme ve kalite güvence (QA) döngüsü artırmak yazılım Yardım. Merhaba şirketin Azure uygulamasıyla düğmesinin hello tıklatmayla bileşenleri yapı yöneticileri paketleyebilirsiniz. Molina açıklandığı gibi "Merhaba yayın döngüsü kapsamında, QA yakından bizim üretim yığını taklit eden Azure mümkün toodeploy tooa test ortamında sunulmuştur. Tooour geliştirme ortamı toovet değişiklikleri hemen biz derlemeleri dağıtabilirsiniz. Biz önce test etmek için eşlik olmadığına büyük kazanım için bize, olmasıdır."

## <a name="offloading-toohello-cloud"></a>Yük boşaltma toohello bulut
Toohello bulut taşımadan önce CSI yazılımı başarıyla Houston yerel bir veri merkezinde çok müşterili kendi altyapısında yukarı yerleşik. Merhaba şirket genişletilmiş gibi satın alma, sağlama ve tüm hello donanım Bakımı artan büyüyen sorunlar karşılaştığı ve yazılım, müşterilerinin toosupport gerekli. BT ekip planlamanıza toohandle işlemleri yeni kaynaklar sağlama ve yeni hizmetler toocustomers çalışırken tooa yavaşlama neden başka bir performans sorunu hale geldi.

Böylece işlemlerini yerine kendi kod odaklanmak, ek yükü ortadan kaldırmak için bulut seçenekleri içine CSI yazılım arama. Merhaba şirket hello üst bulut sağlayıcıları çoğunu yalnızca büyük bir BT personeli toomanage hello Iaas yığın hala gerektiren hizmet olarak altyapı (Iaas) çözümleri sunma buldu. Merhaba bitimine CSI yazılım hello Azure PaaS çözüm için kendi gereksinimlerini karşılayacak en iyi hello olduğunu belirledi. Molina açıklar, "biz yazılım tekliflerimiz bizim BT ek yükünü azaltırken odaklanabilirsiniz Azure hello donanım ve sistem yazılımı hello yolu dışında alır."

## <a name="making-hello-transition-tooazure"></a>Merhaba geçiş tooAzure yapma
Azure PaaS çözümünün seçtikten sonra arka uç altyapısı ve veritabanları toohello bulut geçirme CSI yazılım başlamıştır. Önceki tooAzure SpectrumNG müşteriler tooinstall hello arka ucunda bir Windows Communication Foundation (WCF) hizmetiyle iletişim bir istemci uygulaması gerekli. TooMolina, göre "bazı müşteriler kendi veri merkezlerinde her şeyi barındırılan rağmen hello ürün toobe multitenant oluşturduğumuz. Biz her şeyi Houston, bir veri merkezinde hello veri deposu olarak SQL Server kullanarak barındırılan.

"Bizim ürün sunumu da tasarlanmış toobe beyaz etiketli toomatch hello Müşteri'nin web varlığı ve bir SOAP API toosupport hello çevrimiçi sayfalar ve tüm üçüncü taraf tümleştirme olan (ASP.net ile yazılmış), üye kullanıma yönelik web portalı dahil."

Merhaba geçiş toohello bulut değil almak uzun hello mimarisi için. TooMolina göre "Merhaba çaba hello çoğunluğu biz config dosya bilgileri, bir merkezi bağlantı dizesi değişiklik okuyun ve otomatikleştirme hello paketleme, karşıya yükleme ve dağıtım bizim sürümlerin hello biçimini değiştirip ile ele."

toodevelop hello yapı Otomasyonu, Azure PowerShell CSI yazılım mühendisleri kullanılan ve REST API'leri toocreate paketleri ve yayın her gece için hazırlık ortamı tooa karşıya.
Merhaba genel geçiş tooan Azure bulut tabanlı dağıtım hızlı ve sorunsuz bir şekilde hello CSI yazılım BT Ekibi geçti. Molina açıklar, "tüm, biz beta ortamı hello bulutta hello projede almaya üç toofour hafta içinde vardı. Şaşırtıcı win bize için oluştu."

Geçiş CSI yazılım yapılandırma ve test ortamı hello sonra başlayan müşteriler. Zaten CSI yazılım barındırma kullanan müşteriler için hello geçiş neredeyse sorunsuz. Müşteriler, bir şirket içi dağıtımından geçirme hello geçiş toohello bulut bazı ek zaman aldı, ancak hala öncelikle olan müşteriler ve CSI yazılım için sorun teşkil edecek boş.

Yeni müşteri için CSI yazılım 's BT personeli kullanma işlemi tooon-Panosu bunları tooAzure hello:

1. Azure PowerShell betikleri hello müşteri için yeni bir veritabanı oluşturan kullanılan toospin; yine de uygun istiyor musunuz? tüm müşteriler premium katmanı tooensure üzerinde hello geçiş için ilk yeterli işleme başlar.
2. Mümkün olduğunda, CSI yazılım hello Azure SQL Geçiş Sihirbazı'nı toomove mevcut veri tooan Azure SQL veritabanı örneğini kullanır.
3. Son olarak, Microsoft SQL Server Integration Services (SSIS) kullanılan tooreconcile olan tüm veri temizleme olarak uyumsuzlukları hello veri ya da tooperform gerekli.

Bugün, yaklaşık yüzde 99 CSI yazılım müşteriler dört bölgesel veri merkezleri arasında (Kuzey Orta Güney Merkezi, Doğu ve Batı) Azure içinde barındırılır. Her müşterinin coğrafi bölgede veri merkezleri sağlayarak, gecikme tooa minimum tutulur.

## <a name="azure-elastic-pools-free-up-it-resources"></a>BT kaynaklarını ücretsiz Azure esnek havuzlar
Azure çeşitli özellikler CSI yazılım yardımcı shift altyapı ve işlemleri odaklanmış toobeing özellik ve geliştirme odaklanmış engeller. Belki de hello büyük avantajı esnek havuzlarını olmuştur.

CSI yazılım hakkında 550 veritabanları müşteriler için şu anda sağlar. Esnek havuzlar önce zor toomanage içindeki diğer birçok veritabanı olan bir katmanı yapısı. OPS yöneticileri hello veri bloğu ihtiyaçlara göre önemli BT-kaynak yükü gerekli müşteriler tooassign performans katmanı vardı. Esnek havuzları ile yöneticileri kiracılar premium ya da uygun şekilde standart havuzu atamak ve ardından boyutuna göre müşteriler taşıyabilir ve gerekir. Müşteriler hello esnek havuzlar hello etkilerini hemen Keçeli; Esnek havuzları önce müşteriler zaman aşımları ve diğer sorunlar aşırı kullanım dönemlerinde gerekliydi ancak esnek havuzları ile müşterilerin etkinlik WINS'e gerektiğinde yaşayabilirsiniz ve toouse SpectrumNG sorun olmadan devam edebilirsiniz.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure active coğrafi çoğaltma raporlama hızlandırır.
Birkaç CSI yazılım müşterileri de Azure active coğrafi çoğaltma avantajlarından sürüyor. Hello etkin coğrafi çoğaltma ile toofour okunabilir ikincil veritabanlarıyla yapılandırılabilir aynı veya farklı bir veri merkezi bölgeleri. CSI yazılım iki yolla etkin coğrafi çoğaltma kullanır: hello ikincil veritabanlarıyla ilk olarak, bir veri merkezi kesintisi veya hello bağlanamama tooconnect toohello birincil veritabanı; hello durumda kullanılabilir ve ikincisi, hello ikincil veritabanlarıyla okunabilir ve kullanılan toooffload raporlama işleri gibi salt okunur iş yükleri olabilir. Bazı CSI yazılım müşteriler iş akışları raporlama Bu avantajı tooaccelerate kullanın.

## <a name="csi-software-application-logic-and-architecture"></a>CSI yazılım uygulama mantığını ve mimarisi
SpectrumNG web rollerini kullanır. Merhaba uygulaması çok kiracılı olduğundan, bir WCF Hizmeti kullanılan toohandle hello ilk bağlantı isteğini müşterilerden değildir. Molina durumlar olarak "Merhaba isteğini tanıtır sonra sağlayan bize yapı tootheir veritabanları toodo giden bir bağlantı dizesi ne olursa olsun ihtiyacımız her bir müşteri toodo."

Web katmanı Hello kendi hizmet için Azure otomatik ölçeklendirme, avantajı CSI yazılım gün ve saate göre alır. Kullanılabilir otomatik olarak artan tooaccommodate daha yüksek kullanım iş saatlerinde her bölgesel datacenter toohello saat dilimini göre kaynaklardır. Kaynaklar ayrıca tooscale müşteri gereksinimlerine daha düşük olduğunda hafta sonları üzerinde ayarlanır.

![Daxko/CSI mimarisi](./media/sql-database-implementation-daxko/figure1.png)

Şekil 1 '. Bulut Hizmetleri çalışan rolü yapılandırılmış verileri Azure SQL veritabanı ve tablo depolama yarı yapılandırılmış verilerden çizer. Bir bulut aracılığıyla veri web rolü Hizmetleri ile SpectrumNG kullanıcıların etkileşim.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Web uygulamaları ve web planı katmanı için mobil uygulamaları kullanma
Azure SQL veritabanı CSI yazılım tooenable kaynakları serbest kullanarak Azure web uygulamalarında barındırılan özel bir API eksiksiz bir mobil platform dahil olmak üzere yeni girişimleri temel. Spor salonu üyeleri Hello platformu sağlar ve personel toouse mobil aygıtları toocheck zamanlamaları, sınıfları kitap ve iletileri alacak.

Merhaba platform kullanan hizmet odaklı mimari (SOA) tootake tek bir bileşen — bir satış noktası (POS) sistemi veya bir satış sistemi gibi — hello yaklaştığında tooanother web plan üzerinde taşıyın ve sonra hizmet toosupport şey üzerinde bırakarak bu bileşen Döndür Merhaba özgün web planı. Bu özelliği CSI yazılım inanılmaz esneklik ve maliyetleri düşük tutun yardımcı olur.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure CSI yazılım geliştiriciler odaklanmak uygulama ve hizmetlere izin verir
Azure SQL veritabanı değilse hello hızlı ve güvenilir hizmet keyfini çıkarın, yalnızca bir boon tooSpectrumNG müşteriler, aynı zamanda CSI Software'in için büyük kazanım olan BT personeli ve geliştiricilerin. Ops tooAzure hello bulutta aktararak CSI yazılım kaynakları ve altyapı için kendi ek yük azaltılmış, büyük ölçüde geliştirme döngüsü hızlandırılmış ve artık toomicromanage veritabanları toooptimize performans, kiracılar için gerekir.

## <a name="more-information"></a>Daha fazla bilgi
* toolearn Azure esnek havuzları hakkında daha fazla bilgi görmek [esnek havuzlar](sql-database-elastic-pool.md).
* Veritabanı Araçları ve esnek ölçeklemeyi, hakkında daha fazla toolearn bkz [esnek veritabanı araçlarını ve esnek ölçeklendirme](sql-database-elastic-scale-get-started.md).
* bir SQL Server veritabanını geçirme hakkında daha fazla toolearn bkz bkz [bir SQL Server veritabanı tooAzure geçirmek](sql-database-cloud-migrate.md).
* Aktif coğrafi çoğaltma hakkında daha fazla toolearn bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).
* Web rolleri ve çalışan rolleri hakkında daha fazla toolearn bkz [çalışan rolleri](../fundamentals-introduction-to-azure.md#compute).    
* Azure Service Bus hakkında daha fazla toolearn bkz [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn otomatik ölçekli hakkında daha fazla bilgi görmek [bulut Hizmetleri ölçeklendirme](../cloud-services/cloud-services-how-to-scale.md).

