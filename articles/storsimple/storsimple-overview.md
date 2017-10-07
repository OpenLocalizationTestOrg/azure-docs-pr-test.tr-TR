---
title: "aaaStorSimple 8000 serisi çözümüne genel bakış | Microsoft Docs"
description: "StorSimple katmanlama, hello aygıt, sanal cihaz, hizmetleri ve depolama yönetimi açıklar ve StorSimple içinde kullanılan anahtar terimleri tanıtır."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>StorSimple 8000 serisi: karma bulut depolama çözümü
## <a name="overview"></a>Genel Bakış
Azure StorSimple, Depolama görevlerini şirket içi cihazlar ve Microsoft Azure bulut depolama arasında yöneten bir tümleşik depolama çözümü tooMicrosoft Hoş Geldiniz. StorSimple hello sorunlar ve Kurumsal Depolama ve veri koruma ile ilişkili giderleri birçoğunu ortadan kaldıran bir verimli, uygun maliyetli ve kolayca yönetilebilir depolama alanı ağı (SAN) çözümüdür. Merhaba özel StorSimple 8000 serisi aygıt kullanır, bulut hizmetleriyle tümleştirilen ve sorunsuz bir bulut depolama da dahil olmak üzere tüm Kurumsal Depolama görünümü için bir dizi yönetim araçları sağlar. (Merhaba hello Microsoft Azure Web sitesinde yayınlanan StorSimple dağıtım bilgileri tooStorSimple 8000 serisi cihazlar yalnızca uygulanır. Bir StorSimple 5000/7000 Serisi cihaz kullanıyorsanız, çok Git[StorSimple Yardım](http://onlinehelp.storsimple.com/).)

StorSimple kullanan [depolama katmanlama](#automatic-storage-tiering) toomanage depolanan verileri arasında çeşitli depolama medyası. Şirket içi depolanan katı hal sürücüleri (SSD) üzerinde Hello geçerli çalışma kümesi olduğundan, daha az sık kullanılan veri sabit disk sürücülerinin (HDD'ler) üzerinde depolanır ve Arşiv verileri toohello bulut gönderilir. Ayrıca, yinelenenleri kaldırma StorSimple kullanır ve sıkıştırma tooreduce hello veri hello depolama miktarını kullanır. Daha fazla bilgi için çok Git[yinelenenleri kaldırma ve sıkıştırma](#deduplication-and-compression). Diğer anahtar terimleri ve kavramları hello StorSimple 8000 serisi belgelerde kullanılan tanımları çok Git[StorSimple terminolojisi](#storsimple-terminology) hello bu makalenin sonunda.

Ayrıca toostorage yönetim, toocreate isteğe bağlı ve zamanlanmış yedeklemeler ve yerel olarak veya hello bulut sonra mağaza StorSimple veri koruması özelliklerini etkinleştirir. Yedeklemeler, bunlar oluşturulabilir ve hızlı bir şekilde geri, yani hello formunda artımlı anlık görüntü alınır. Çünkü bunlar ikincil depolama sistemleri (örneğin, bant yedekleme) değiştirin ve gerekirse toorestore, veri tooyour datacenter veya tooalternate sitelerin izin bulut anlık görüntüleri olağanüstü durum kurtarma senaryolarında kritik düzeyde önemli olabilir.

![video simgesi](./media/storsimple-overview/video_icon.png) Hızlı Giriş tooMicrosoft Azure StorSimple Hello videoyu izleyin.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>StorSimple neden kullanılır?
Merhaba aşağıdaki tabloda, Microsoft Azure StorSimple sağlayan hello anahtar avantajlarından bazıları açıklanmaktadır.

| Özellik | Avantaj |
| --- | --- |
| Saydam tümleştirme |Merhaba iSCSI protokolü tooinvisibly bağlantı veri depolama özellikleri kullanır. Bu hello merkezinde hello bulutta depolanan bu verileri sağlar veya tek bir konumda depolanan toobe uzak sunucularda görüntülenir. |
| Azaltılmış depolama maliyetleri |Yeterli yerel ayırır veya Bulut depolama toomeet geçerli talepleri ve bulut depolama yalnızca gerekli olduğunda genişletir. Bu daha fazla depolama alanı gereksinimleri ve gider hello yedek sürümlerini ortadan kaldırarak azaltır aynı verileri (kaldırmayı) ve sıkıştırma kullanarak. |
| Basitleştirilmiş Depolama Yönetimi |Sistem Yönetim Araçları tooconfigure sağlar ve depolanan verileri şirket içi, uzak bir sunucudaki ve hello bulutta yönetme. Ayrıca, yedekleme yönetmek ve bir Microsoft Yönetim Konsolu (MMC) ek bileşeninden işlevleri geri yükleyebilirsiniz.|
| Geliştirilmiş olağanüstü durum kurtarma ve uyumluluk |Genişletilmiş kurtarma süresi gerektirmez. Bunun yerine, gerektiğinde verileri yükler. Başka bir deyişle, normal işlemleri en az kesintiyi ile devam edebilirsiniz. Ayrıca, ilkeleri toospecify yedekleme zamanlamaları ve veri saklama yapılandırabilirsiniz. |
| Veri mobility |Veri tooMicrosoft Azure bulut Hizmetleri kurtarma ve geçiş amaçları için diğer sitelere erişilebilen karşıya yüklendi. Ayrıca, Microsoft Azure'da çalışan sanal makineler (VM'ler) üzerinde StorSimple tooconfigure StorSimple bulut cihazları kullanabilirsiniz. Merhaba VM'ler, daha sonra sanal cihazlar tooaccess depolanan veri test veya kurtarma amacıyla kullanabilirsiniz. |
| İş sürekliliği |StorSimple 5000-7000 Serisi kullanıcılar toomigrate veri tooa StorSimple 8000 serisi cihazlarını sağlar. |
| Hello Azure kamu Portal kullanılabilirliği |StorSimple hello Azure kamu Portal kullanılabilir. Daha fazla bilgi için bkz: [hello kamu Portal kullanarak şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Veri koruma ve kullanılabilirlik |Merhaba StorSimple 8000 serisi bölge olarak yedekli depolama (ZRS), ek tooLocally yedekli depolama (LRS) içinde ve coğrafi olarak yedekli depolama (GRS) destekler. Çok başvuran[bu makalede Azure Storage artıklık seçenekleri](https://azure.microsoft.com/documentation/articles/storage-redundancy/) ZRS Ayrıntılar için. |
| Kritik uygulamalar için destek |Bulut hangi sırayla Kritik uygulamalar tarafından gerekli veri katmanlı toohello emin olunmasını sağlar yerel olarak sabitlenmiş şekilde uygun birimleri tanımlamak StorSimple sağlar. Yerel olarak sabitlenmiş birimlerin konu toocloud gecikmeleri veya bağlantı sorunları olup olmadığı. Yerel olarak sabitlenmiş birimleri hakkında daha fazla bilgi için bkz: [hello StorSimple cihaz Yöneticisi hizmeti toomanage birimler kullanmak](storsimple-8000-manage-volumes-u2.md). |
| Düşük gecikme süreli ve yüksek performans |Merhaba yüksek performans, düşük gecikme süresi Azure premium storage özelliklerini yararlanmak bulut uygulamaları oluşturabilirsiniz. StorSimple premium bulut uygulamaları hakkında daha fazla bilgi için bkz: [dağıtma ve azure'da bir StorSimple bulut uygulaması yönetmek](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>StorSimple bileşenleri
Merhaba Microsoft Azure StorSimple çözümünüzle hello aşağıdaki bileşenleri içerir:

* **Microsoft Azure StorSimple cihaz** – SSD ve HDD, yedek denetleyicileri ve otomatik yük devretme yetenekleri ile birlikte içeren bir şirket içi karma depolama dizisi. Merhaba denetleyicileri katmanlama, şu anda kullanılan (veya sık kullanılan) veri yerel depolamada (Merhaba aygıt ya da şirket içi sunucuları), daha az sık kullanılan veri toohello bulut taşırken yerleştirme depolama yönetin.
* **StorSimple bulut uygulaması** – olarak da bilinen StorSimple sanal gereç Merhaba, hello mimarisi çoğaltır hello StorSimple cihazı yazılımı sürümü ve hello fiziksel karma depolama aygıtı çoğu özelliklerini budur. bir Azure sanal makinesinde tek bir düğümde Hello StorSimple bulut uygulaması çalıştırır. Azure premium Storage yararlanmak, premium sanal aygıt ve sonrasında güncelleştirme 2'de kullanılabilir.
* **StorSimple cihaz Yöneticisi hizmeti** – hello bir StorSimple cihazı veya StorSimple bulut uygulaması bir tek web arabiriminden yönetmenizi sağlayan Azure portalı uzantısı bir. Hello StorSimple cihaz Yöneticisi hizmeti toocreate kullanın ve hizmetleri yönetmek, görüntülemek ve cihazları yönetmek, uyarıları görüntülemek, birimler, yönetebilir ve görüntülemek ve yedekleme ilkeleri ve hello yedekleme kataloğu yönetin.
* **StorSimple için Windows PowerShell** – toomanage kullanabileceğiniz bir komut satırı arabirimi hello StorSimple cihazı. StorSimple için Windows PowerShell tooregister olanak tanıyan özellikler StorSimple Cihazınızı olduğundan, aygıtınızda hello ağ arabirim yapılandırın, belirli türden güncelleştirmeler yüklemeniz, Cihazınızı hello destek oturum erişerek sorun giderme ve hello değiştirme cihaz durumu. StorSimple için Windows PowerShell bağlanan toohello seri konsolu veya Windows PowerShell uzaktan iletişimini kullanarak erişebilirsiniz.
* **Azure PowerShell StorSimple cmdlet'lerini** – tooautomate hizmet düzeyi ve geçiş görevleri hello komut satırından izin Windows PowerShell cmdlet'leri koleksiyonu. StorSimple için hello Azure PowerShell cmdlet'leri hakkında daha fazla bilgi için toohello Git [cmdlet başvurusu](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **StorSimple Snapshot Manager** – birim grupları ve hello Windows birim gölge kopyası hizmeti toogenerate uygulamayla tutarlı yedeklemeler kullanan bir MMC ek bileşenini. Ayrıca, StorSimple Snapshot Manager toocreate yedekleme zamanlamaları ve kopya kullanın veya birimleri geri yükleyebilirsiniz.
* **SharePoint için StorSimple bağdaştırıcısı** – saydam görüntülenebilir ve yönetilebilir hello SharePoint Orta gelen StorSimple depolama yaparken tooSharePoint sunucu grupları,'de Microsoft Azure StorSimple depolama ve veri koruma'yı genişleten bir aracı Yönetim Portalı.

Merhaba diyagrama hello Microsoft Azure StorSimple mimarisinin üst düzey bir görünümünü ve bileşenleri sağlar.

![StorSimple mimarisi](./media/storsimple-overview/overview-big-picture.png)

Merhaba aşağıdaki bölümlerde daha ayrıntılı bu bileşenlerin her birini açıklayan ve nasıl hello çözüm verileri düzenler, depolama ayırır ve Depolama Yönetimi ve veri koruması kolaylaştıran açıklanmaktadır. Merhaba son bölümde bazı önemli terimler hello ve kavramları ilgili tooStorSimple bileşenleri ve bunların yönetimi için tanımları sağlar.

## <a name="storsimple-device"></a>StorSimple cihazı
Merhaba Microsoft Azure StorSimple cihaz birincil depolama ve depolanması iSCSI erişim toodata sağlayan bir şirket içi karma depolama dizisidir. Bulut depolama ile iletişim yönetir ve tooensure hello güvenlik ve Microsoft Azure StorSimple çözümünüzle hello üzerinde depolanan tüm verileri gizliliğini yardımcı olur.

Merhaba StorSimple cihazı SSD ve sabit disk sürücülerinin HDD yanı sıra, kümeleme ve otomatik yük devretme için destek içerir. Paylaşılan bir işlemci, paylaşılan depolama alanı ve iki yansıtılmış denetleyicisi içerir. Her denetleyici hello aşağıdakileri sağlar:

* Bağlantı tooa ana bilgisayarı
* Toosix ağ bağlantı noktalarını tooconnect toohello yerel ağ (LAN)
* Donanım izleme
* Güç kesildi olmasa bile, bilgileri saklar, geçici olmayan rasgele erişim belleği (NVRAM)
* Küme durumunu algılayan hello güncelleştirmeleri en az böylece yük devretme kümesindeki sunucularda toomanage yazılım güncelleştirmelerini güncelleştirme veya hizmet kullanılabilirliği üzerinde hiçbir etkisi
* Küme hizmeti, hangi işlevleri gibi yüksek düzeyde kullanılabilirlik sağladığınızdan ve HDD veya SSD hata verirse veya oluşabilecek olumsuz etkileri en aza bir arka uç küme çevrimdışına

Yalnızca bir denetleyici zamanda herhangi bir noktada etkindir. Merhaba etkin denetleyicisi başarısız olursa, hello ikinci denetleyicisi otomatik olarak etkinleşir.

Daha fazla bilgi için çok Git[StorSimple donanım bileşenleri ve durum](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>StorSimple Cloud Appliance
StorSimple toocreate hello mimarisi ve hello fiziksel karma depolama aygıtı özelliklerini çoğaltan bir bulut uygulaması kullanabilirsiniz. bir Azure sanal makinesinde tek bir düğümde Hello StorSimple bulut uygulaması (olarak da bilinen StorSimple sanal gereç hello) çalışır. (Bulut uygulaması, yalnızca bir Azure sanal makinesi üzerinde oluşturulabilir. Bir StorSimple cihazı veya bir şirket içi sunucuda oluşturamazsınız.)

Merhaba bulut uygulaması özellikler aşağıdaki hello sahiptir:

* Fiziksel bir Gereci gibi davranır ve bir iSCSI arabirimi toovirtual hello bulut makinelerinizde sunabilir.
* Bulut cihazları sınırsız sayıda hello bulutta oluşturmak ve bunları açma ve kapatma gerektiği şekilde açın.
* Olağanüstü durum kurtarma, geliştirme ve test senaryoları şirket içi ortamlarını benzetmek yardımcı olabilir ve öğe düzeyinde alma yedeklerden ile yardımcı olabilir.

Merhaba StorSimple bulut uygulaması iki modellerinde kullanılabilir: Merhaba 8010 cihaz (önceden 1100 hello model olarak biliniyordu) ve hello 8020 cihaz. Merhaba 8010 cihaz 30 TB maksimum kapasitesine sahiptir. Azure premium Storage yararlanır, hello 8020 cihaz 64 TB maksimum kapasitesine sahiptir. (Standart depolama Hdd'lerde veri depoladığı yerel katmanlarda, Azure premium depolama verileri Ssd'de depolar.) Bir Azure premium depolama hesabı toouse premium depolama olması gerektiğini unutmayın. Premium depolama hakkında daha fazla bilgi için çok Git[Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../storage/common/storage-premium-storage.md).

Merhaba StorSimple bulut uygulaması hakkında daha fazla bilgi için çok Git[dağıtma ve azure'da bir StorSimple bulut uygulaması yönetmek](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>StorSimple cihaz Yöneticisi hizmeti
Microsoft Azure StorSimple toocentrally sağlayan bir web tabanlı kullanıcı arabirimi (Merhaba StorSimple cihaz Yöneticisi hizmeti) sağlayan veri merkezi yönetmek ve bulut depolama. Merhaba StorSimple cihaz Yöneticisi hizmeti tooperform hello görevleri aşağıdaki kullanabilirsiniz:

* StorSimple cihazlar için sistem ayarlarını yapılandırın.
* Yapılandırmak ve StorSimple cihazlar için güvenlik ayarlarını yönetin.
* Bulut kimlik bilgileri ve özelliklerini yapılandırın.
* Yapılandırın ve bir sunucu üzerindeki birimleri yönetin.
* Birim grupları yapılandırın.
* Yedekleme ve veri geri yükleme.
* Performans İzleyici.
* Sistem ayarlarını gözden geçirin ve olası sorunları tanımlar.

Sistem ilk kurulum ve güncelleştirmelerin yüklenmesi gibi kesinti gerektiren olanlar dışında tüm yönetim görevlerini hello StorSimple cihaz Yöneticisi hizmeti tooperform kullanabilirsiniz.

Daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell
StorSimple için Windows PowerShell komut satırı toocreate kullanın ve hello Microsoft Azure StorSimple hizmeti yönetebilir ve ayarlama ve StorSimple cihazları izleme, arabirim sağlar. Bu bir Windows PowerShell tabanlı komut satırı StorSimple Cihazınızı yönetmek için ayrılmış cmdlet'ler içeren arabirimidir. StorSimple için Windows PowerShell izin özelliklere sahiptir:

* Bir cihaz kaydetme.
* Merhaba ağ arabirimi bir aygıtta yapılandırın.
* Belirli türde bir güncelleştirmeleri yükleyin.
* Cihazınızı hello destek oturum erişerek sorunlarını giderin.
* Merhaba aygıt durumunu değiştirin.

StorSimple için Windows PowerShell bir seri konsoldan erişmek için (bir ana bilgisayarda bilgisayar doğrudan toohello aygıt bağlı) veya Windows PowerShell uzaktan iletişimini kullanarak uzaktan. İlk cihaz kaydı gibi StorSimple görevleri için bazı Windows PowerShell yalnızca hello seri konsolunuzdaki yapılması unutmayın.

Daha fazla bilgi için çok Git[StorSimple tooadminister için Windows PowerShell'i kullanın Cihazınızı](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>Azure PowerShell StorSimple cmdlet'leri
Hello Azure PowerShell StorSimple cmdlet'leri, hizmet düzeyi tooautomate ve geçiş görevleri hello komut satırından izin Windows PowerShell cmdlet'leri koleksiyonudur. StorSimple için hello Azure PowerShell cmdlet'leri hakkında daha fazla bilgi için toohello Git [cmdlet başvurusu](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>StorSimple Snapshot Manager
StorSimple Snapshot Manager bir Microsoft Yönetim Konsolu (MMC) ek bileşenidir toocreate tutarlı, zaman içinde nokta yedek kopyalarını yerel kullanabilirsiniz ve bulut veri. Merhaba ek bileşenini Windows Server tabanlı bir ana bilgisayarda çalışır. StorSimple Snapshot Manager kullanabilirsiniz:

* Yapılandırma, yedekleme ve birimleri silin.
* Birimi yedeklenmiş verileri grupları tooensure uygulama tutarlı olduğundan.
* Böylece verileri belirlenmiş bir zamanlamayla yedeklenebilir ve (yerel olarak veya hello bulutta) atanmış bir konumda depolanan yedekleme ilkelerini yönetin.
* Birimleri ve dosyaları tek tek geri yükleyin.

Yedeklemeleri hello son anlık görüntü alındıktan sonra yalnızca hello değişiklikleri kaydetmek ve tam yedeklemeler daha çok daha az depolama alanı gerektiren anlık görüntü olarak yakalanır. Yedekleme zamanlamaları oluşturabilir veya gerektiğinde hemen yedek alabilir. Ayrıca, kaç anlık görüntü kaydedilecek denetleyen StorSimple Snapshot Manager tooestablish bekletme ilkeleri kullanabilirsiniz. Yedekleme, StorSimple Snapshot Manager sağlar toorestore verileri daha sonra gerekirse yerel hello Kataloğu'ndan veya Bulut anlık görüntüleri seçin. 

Gerektiğinde bir olağanüstü durum gerçekleşirse veya başka bir nedenle toorestore verilere ihtiyacınız varsa, StorSimple Snapshot Manager, artımlı olarak geri yükler. Verileri geri yükleme, bir dosyayı geri yüklemek, donanım değiştirin ya da işlemleri tooanother siteyi taşımak hello tüm sistemi Kapat gerektirmez.

Daha fazla bilgi için çok Git[StorSimple anlık görüntü Yöneticisi nedir?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>SharePoint için StorSimple Bağdaştırıcısı
Microsoft Azure StorSimple hello StorSimple bağdaştırıcısı SharePoint için StorSimple depolama ve veri koruması özelliklerini tooSharePoint sunucu grupları şeffaf bir şekilde genişletir isteğe bağlı bir bileşen içerir. Merhaba bağdaştırıcısı hello Microsoft Azure StorSimple sistemi tarafından yedeklenen toomove BLOB'lar tooa sunucunuz izin vererek Uzak Blob Depolama (KKY) sağlayıcısı ve hello SQL Server KKY özelliği ile çalışır. Microsoft Azure StorSimple sonra hello BLOB verilerini yerel olarak veya hello bulutta kullanıma dayalı depolar.

SharePoint için StorSimple bağdaştırıcısı Hello hello SharePoint Merkezi Yönetim Portalı içinde yönetilir. Sonuç olarak, SharePoint Yönetim Merkezi kalır ve toobe hello SharePoint grubundaki tüm depolama görünür.

Daha fazla bilgi için çok Git[SharePoint için StorSimple bağdaştırıcısı](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Depolama yönetimi teknolojileri
Ayrıca toohello StorSimple cihaz, sanal cihaz ve diğer bileşenleri ayrılmış, Microsoft Azure StorSimple yazılım teknolojileri tooprovide hızlı erişim toodata ve tooreduce depolama tüketimini aşağıdaki hello kullanır:

* [Otomatik depolama katmanlama](#automatic-storage-tiering) 
* [Ölçülü kaynak sağlama](#thin-provisioning) 
* [Yinelenenleri kaldırma ve sıkıştırma](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Otomatik depolama katmanlama
Microsoft Azure StorSimple otomatik olarak geçerli kullanımı, geçerlilik süresi ve ilişki tooother veriler temel alınarak mantıksal katmanları verileri düzenler. Çoğu etkin etkin durumdayken daha az yerel olarak depolanır ve etkin olmayan verileri otomatik olarak verileri toohello bulut geçirildi. Aşağıdaki diyagramda hello bu depolama yaklaşımı gösterilmektedir.

![StorSimple depolama katmanları](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

tooenable hızlı erişim, StorSimple hello StorSimple cihazı Ssd'de çok etkin verileri (etkin) depolar. Bazen kullanılan verilerini depolayan (normal veri) HDD hello aygıt ya da hello veri merkezindeki sunucular üzerinde. Etkin olmayan verileri, yedekleme verilerini taşır ve veriler korunur için arşivleme veya uyumluluk amacıyla toohello bulut. 

> [!NOTE]
> Güncelleştirme 2 veya sonraki sürümlerde, yerel olarak sabitlenmiş bir birim belirtebilirsiniz, bu durumda hello veri hello yerel cihazda kalır ve değil toohello bulut katmanlı. 


StorSimple ayarlar ve verileri yeniden düzenler ve kullanım düzenlerini olarak depolama atamalarını değiştirin. Örneğin, bazı bilgiler zaman içinde daha az etkin hale gelebilir. Aşamalı olarak daha az etkin hale geldiğinde, SSD tooHDDs ve ardından toohello bulut geçirilir. Bu aynı verileri tekrar etkin hale gelirse, geçirilen geri toohello depolama aygıtı değil.

Merhaba depolama katmanlama işlemi aşağıdaki gibidir:

1. Bir Sistem Yöneticisi bir Microsoft Azure bulut depolama hesabı ayarlar.
2. Hello Yöneticisi hello seri konsolu ve hello StorSimple Aygıt Yöneticisi'ni (hello Azure portalında çalışan) hizmeti tooconfigure hello cihaz ve dosya sunucusu, birimler ve veri koruma ilkeleri oluşturma kullanır. Şirket içi makineler (örneğin, dosya sunucuları) hello Internet küçük bilgisayar sistemi arabirimi (iSCSI) tooaccess hello StorSimple cihazı kullanın.
3. Başlangıçta, StorSimple hello hızlı SSD katmanında hello cihazın verileri depolar.
4. Hello SSD katmanı yaklaşımlar kapasitesini, olarak StorSimple deduplicates hello en eski veri blokları sıkıştırır ve toohello HDD Katmanı taşır.
5. Hello HDD katmanı yaklaşımlar kapasite, StorSimple hello en eski veri bloklarını şifreler ve bunları güvenli bir şekilde toohello Microsoft Azure depolama hesabı HTTPS üzerinden gönderir.
6. Microsoft Azure bir olağanüstü durum gerçekleşirse hello verilerin kurtarılabilmesini sağlamak, veri merkezinde ve uzak bir veri merkezinde hello verilerin birden çok çoğaltmalarının oluşturur.
7. Merhaba dosya sunucusu hello bulutta depolanan veriler istediğinde, StorSimple sorunsuz bir şekilde döndürür ve hello StorSimple cihazı hello SSD katmanı üzerinde bir kopyasını depolar.

#### <a name="how-storsimple-manages-cloud-data"></a>StorSimple bulut verilerini nasıl yönetir

StorSimple müşteri verileri tüm hello anlık görüntüler ve hello birincil verilerini (ana bilgisayar tarafından yazılan) üzerinden deduplicates. Yinelenenleri kaldırma depolama verimliliği için harika olsa da, "Merhaba bulutta karmaşık nedir" Merhaba sorunu çözmez kolaylaştırır. Merhaba katmanlı birincil veri ve hello anlık görüntü verilerini birbirleri ile çakışıyor. Merhaba buluttaki verilerin tek bir öbek katmanlı birincil veri olarak kullanılabilir ve ayrıca birkaç anlık görüntüleri tarafından başvuruda. Bu anlık görüntü silinene kadar tüm hello zaman içinde nokta verilerin bir kopyasını hello bulutunu kilitli her bulut anlık görüntüsü sağlar.

Başvuruları toothat veri olduğunda veriler yalnızca hello buluttan silinir. Örneğin, biz hello StorSimple cihazı ve bazı birincil veri silmek bulut verilerin bir anlık görüntüsünü tüm hello izlerseniz, biz hello göreceğiniz _birincil veri_ hemen bırakın. Merhaba _bulut verilerini_ içeren hello katmanlı veri ve hello yedeklemeler, kalır hello aynı. Hala hello bulut verilerini başvuran bir anlık görüntü olduğundan bu değildir. Sonra Hello bulut anlık görüntüsü silinir (ve başvurulan diğer tüm anlık görüntü hello aynı verileri), tüketim düşme bulut. Biz bulut verilerini kaldırmadan önce anlık görüntü yok hala bu verilere başvuruda denetleyin. Bu işlem çağrılırken _çöp toplama_ ve hello aygıtta çalıştıran bir arka plan hizmeti. Bulut verilerin kaldırılması hemen değil Hello atık toplama hizmeti başvuruları için hello silme önce toothat verileri denetler. Çöp toplama Hello hızına hello toplam sayısına anlık görüntüler ve hello toplam veri bağlıdır. Genellikle, hello bulut verilerini değerinden bir hafta içinde temizlenir.


### <a name="thin-provisioning"></a>Ölçülü kaynak sağlama
Ölçülü kaynak sağlama kullanılabilir depolama alanı tooexceed fiziksel kaynaklar görünür bir sanallaştırma teknolojisidir. Önceden yeterli depolama alanı ayırma yerine, StorSimple tam olarak yeterli alanı toomeet geçerli gereksinimleri ince sağlama tooallocate kullanır. StorSimple artırmak veya Bulut depolama toomeet değişen taleplerini azaltmak için bu yaklaşım bulut depolama esnek yapısını hello kolaylaştırır.

> [!NOTE]
> Yerel olarak sabitlenmiş birimlerin ölçülü kaynak sağlanan değil. Merhaba birim oluşturulduğunda tooa yalnızca yerel birim ayrılan depolama alanını tamamının sağlanır.


### <a name="deduplication-and-compression"></a>Yinelenenleri kaldırma ve sıkıştırma
Microsoft Azure StorSimple kullandığı yinelenenleri kaldırma ve veri sıkıştırma toofurther depolama gereksinimlerini azaltmak.

Yinelenenleri kaldırma azaltır hello genel hello depolanan veri kümesi içinde artıklık ortadan kaldırarak depolanan veri miktarı. Bilgi değiştikçe değişmeden hello veri StorSimple yoksayar ve yakalamaları değişiklikler yalnızca hello. Ayrıca, StorSimple tanımlama ve gereksiz bilgileri kaldırma depolanan verilerin hello miktarını azaltır. 

> [!NOTE]
> Yerel olarak sabitlenmiş birimlerdeki veriler yinelenenleri kaldırılmış veya sıkıştırılmış değil. Ancak, yerel olarak sabitlenmiş birimlerin yedekleri, yinelenenleri kaldırılmış sıkıştırılmış ve.


## <a name="storsimple-workload-summary"></a>StorSimple iş yükü özeti
Desteklenen hello StorSimple iş yükleri bir özeti aşağıda tabloda verilmiştir.

| Senaryo | İş yükü | Destekleniyor | Kısıtlamaları | Sürüm |
| --- | --- | --- | --- | --- |
| İş Birliği |Dosya Paylaşımı |Evet | |Tüm sürümler |
| İş Birliği |Dağıtılmış dosya paylaşımı |Evet | |Tüm sürümler |
| İş Birliği |SharePoint |Evet* |Yalnızca yerel olarak sabitlenmiş birimleri ile desteklenen |Güncelleştirme 2 ve üstü |
| Arşivleme |Basit dosya arşivleme |Evet | |Tüm sürümler |
| Sanallaştırma |Sanal makineler |Evet* |Yalnızca yerel olarak sabitlenmiş birimleri ile desteklenen |Güncelleştirme 2 ve üstü |
| Database |SQL |Evet* |Yalnızca yerel olarak sabitlenmiş birimleri ile desteklenen |Güncelleştirme 2 ve üstü |
| Kameralı |Kameralı |Evet* |StorSimple cihaz ayrılmış yalnızca toothis iş yükü olduğunda desteklenir |Güncelleştirme 2 ve üstü |
| Backup |Birincil hedef yedekleme |Evet* |StorSimple cihaz ayrılmış yalnızca toothis iş yükü olduğunda desteklenir |Güncelleştirme 3 ve üzeri |
| Backup |İkincil hedef yedekleme |Evet* |StorSimple cihaz ayrılmış yalnızca toothis iş yükü olduğunda desteklenir |Güncelleştirme 3 ve üzeri |

*Evet &#42; -Çözüm yönergeleri ve kısıtlamaları uygulanmalıdır.*

iş yükleri aşağıdaki hello StorSimple 8000 serisi cihazlar tarafından desteklenmez. StorSimple üzerinde dağıttıysanız, bu iş yükleri desteklenmeyen bir yapılandırmada neden olur.

* Tıbbi görüntüleme
* Exchange
* VDI
* Oracle
* SAP
* Büyük veriler
* İçerik dağıtımı
* SCSI önyükleme

Merhaba desteklenen StorSimple altyapı bileşenlerin bir listesi aşağıda verilmiştir.

| Senaryo | İş yükü | Destekleniyor | Kısıtlamaları | Sürüm |
| --- | --- | --- | --- | --- |
| Genel |Express Route |Evet | |Tüm sürümler |
| Genel |DataCore FC |Evet* |DataCore SANsymphony ile desteklenen |Tüm sürümler |
| Genel |DFSR |Evet* |Yalnızca yerel olarak sabitlenmiş birimleri ile desteklenen |Tüm sürümler |
| Genel |Dizinleme |Evet* |Katmanlı birimler için yalnızca meta veri dizinini desteklenir (verileri değil).<br>Yerel olarak sabitlenmiş birimler için dizin oluşturma tamamlandı desteklenir. |Tüm sürümler |
| Genel |Virüsten koruma |Evet* |Katmanlı birimler için yalnızca tarama açık ve Kapat desteklenir.<br> Yerel olarak sabitlenmiş birimler için tam tarama desteklenir. |Tüm sürümler |

*Evet &#42; -Çözüm yönergeleri ve kısıtlamaları uygulanmalıdır.*

StorSimple toobuild çözümleri ile kullanılan diğer yazılımların listesi verilmiştir.

| İş yükü türü | StorSimple ile kullanılan yazılım | Desteklenen sürümler|Bağlantı toosolution Kılavuzu| 
| --- | --- | --- | --- |
| Yedekleme hedefi |Veeam |Veeam v 9 ve sonraki sürümler |[Yedekleme hedefi olarak StorSimple Veaam ile](storsimple-configure-backup-target-veeam.md)|
| Yedekleme hedefi |Veritas Backup Exec |Yedekleme Exec 16 ve üzeri |[Yedekleme hedefi olarak StorSimple yedekleme Exec ile](storsimple-configure-backup-target-using-backup-exec.md)|
| Yedekleme hedefi |VERITAS NetBackup |NetBackup 7.7.x ve sonraki sürümler  |[Yedekleme hedefi olarak StorSimple NetBackup ile](storsimple-configure-backuptarget-netbackup.md)|
| Genel dosya paylaşımı <br></br> İş Birliği |Talon  |[StorSimple Talon ile](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>StorSimple terminolojisi
Microsoft Azure StorSimple çözümünüzün dağıtmadan önce hello aşağıdakileri gözden geçirmenizi öneririz terimleri ve tanımları.

### <a name="key-terms-and-definitions"></a>Anahtar terimleri ve tanımları
| Terim (kısaltma veya kısaltması) | Açıklama |
| --- | --- |
| erişim denetimi kaydı (ACR) |Hangi ana bilgisayarların tooit bağlanabilir belirler, Microsoft Azure StorSimple cihaz üzerindeki bir birimi ile ilişkili bir kaydı. Merhaba belirleme hello iSCSI temel tam adını (IQN) tooyour StorSimple cihazı bağlanan (Merhaba ACR bulunan) hello ana bilgisayar. |
| AES 256 |Merhaba buluttan tooand hareket ederken verileri şifrelemek için bir 256 bit Gelişmiş Şifreleme Standardı (AES) algoritması. |
| ayırma birimi boyutu (Avustralya) |Merhaba küçük olabilir disk alanı miktarını, Windows dosya sistemleri bir dosya toohold ayrılmış. Bir dosya boyutu bir hello küme boyutunu değil, ek boşluk kullanılan toohold hello dosya olmalıdır (toohello yukarı sonraki birden çok hello küme boyutu) kayıp alanı ve hello sabit disk parçalanması. <br>Hello hello yinelenenleri kaldırma algoritmalarıyla iyi çalıştığı için Azure StorSimple birimler için Avustralya 64 KB önerilir. |
| Otomatik depolama katmanlama |Otomatik olarak SSD tooHDDs ve tooa katmanında hello Bulut ve tüm depolama biriminden bir merkezi kullanıcı arabirimi yönetimini etkinleştirme daha az aktif veri taşıma. |
| Yedekleme kataloğu |Yedeklemeler, genellikle kullanılan hello uygulama türüne göre ilgili koleksiyonu. Bu koleksiyon hello StorSimple cihaz Yöneticisi hizmeti kullanıcı Arabirimi, hello yedekleme kataloğu dikey penceresinde görüntülenir. |
| Yedekleme kataloğu dosyası |Şu anda hello yedekleme veritabanında StorSimple anlık görüntü Yöneticisi'nin depolanan mevcut anlık görüntü listesini içeren bir dosya. |
| Yedekleme İlkesi |Birimler, yedekleme türü ve önceden tanımlanmış bir zamanlamaya göre toocreate yedeklemeler sayesinde bir zaman çizelgesi seçimi. |
| ikili büyük nesneler (BLOB) |Bir veritabanı yönetim sisteminin tek bir varlık olarak saklanan ikili verileri koleksiyonu. Bazen ikili yürütülebilir kod BLOB olarak depolanan BLOB'ları genellikle görüntüler, ses ve diğer multimedya nesneler, ancak. |
| Karşılıklı Kimlik Doğrulama Protokolü (CHAP) |Bir parola veya gizli paylaşımı hello eş üzerinde dayalı bir bağlantı tooauthenticate hello eşinin kullanılan protokol. Tek yönlü veya karşılıklı CHAP olabilir. Tek yönlü CHAP ile Merhaba hedef Başlatıcı kimliğini doğrular. Karşılıklı CHAP hello hedef hello Başlatıcı kimlik doğrulaması ve o hello Başlatıcı hello hedef kimlik doğrulaması gerektirir. |
| kopya |Bir birim yinelenen bir kopyası. |
| Bulut Katmanı (CaaT) olarak |Depolama katmanı hello depolama mimarisi içinde olarak tüm depolama bir kurumsal depolama ağı toobe parçası görüntülenmemesini tümleşik bulut. |
| Bulut hizmeti sağlayıcısı (CSP) |Bulut Hizmetleri Sağlayıcısı. |
| Bulut anlık görüntüsü |Merhaba bulutta depolanan birim verilerini zaman içinde nokta kopyası. Bir bulut anlık görüntüsü eşdeğerdir farklı, şirket dışı depolama sisteminizde çoğaltılan tooa anlık görüntü. Bulut anlık görüntüleri olağanüstü durum kurtarma senaryolarında özellikle kullanışlıdır. |
| Bulut depolama şifreleme anahtarı |Bir parola veya cihaz toohello bulut tarafından gönderilen StorSimple cihaz tooaccess hello şifrelenmiş verilerinizi tarafından kullanılan bir anahtar. |
| Küme durumunu algılayan güncelleştirme |Merhaba güncelleştirmeleri en az böylece yük devretme kümesindeki sunucularda yazılım güncelleştirmelerini yönetme veya servis kullanılabilirliğini etkilemez. |
| DataPath |Arası bağlı veri işleme işlemleri işlevsel birimlerini koleksiyonu. |
| Devre dışı bırakma |Bulut hizmeti sonları hello StorSimple cihazı hello arasındaki bağlantı hello kalıcı bir eylem ilişkilendirilmiş. Merhaba cihaz bulut anlık görüntüleri sonra bu işlemi kalmasını ve kopyalanması veya olağanüstü durum kurtarma için kullanılan. |
| Disk yansıtma |Mantıksal disk birimi ayrı sabit çoğaltmasını gerçek zamanlı tooensure sürekli kullanılabilirlik sürücüleri. |
| dinamik disk yansıtma |Dinamik diskler mantıksal disk birimi çoğaltma. |
| dinamik diskler |Kullanan Mantıksal Disk Yöneticisi (LDM) toostore hello ve verileri birden çok fiziksel disklerde yönetmek bir disk birimi biçimi. Dinamik diskler büyütülmüş tooprovide daha fazla boş alan olabilir. |
| Genişletilmiş disk demet (EBOD) kasası |Ek depolama alanı için ek sabit diskleri içeren Microsoft Azure StorSimple Cihazınızı, ikincil bir kutu. |
| FAT sağlama |Bir geleneksel depolama hangi depolama alanına ayrılmış alanı göre sağlama gereksinimlerini beklenen (ve genellikle hello geçerli gerekiyor). Ayrıca bkz. *ölçülü kaynak sağlama*. |
| sabit disk sürücüsü (HDD) |Döndürme plaka toostore veri kullanan bir sürücüye. |
| karma bulut depolama |Bulut depolama da dahil olmak üzere, yerel ve şirket dışı kaynak kullanan bir depolama mimarisi. |
| Internet küçük bilgisayar sistemi arabirimi (iSCSI) |Veri depolama donanımı veya tesis bağlama için bir Internet Protokolü IP tabanlı depolama ağ standardı. |
| iSCSI başlatıcısı |Windows tooconnect tooan dış iSCSI tabanlı depolama ağı çalıştıran bir konak bilgisayar sağlayan bir yazılım bileşeni. |
| iSCSI tam adını (IQN) |Bir iSCSI hedefi veya Başlatıcı tanımlayan benzersiz bir ad. |
| iSCSI hedefi |Merkezi iSCSI disk alt sistemleri depolama alanı ağlarında sağlayan bir yazılım bileşeni. |
| Arşivleme Canlı |Arşiv verileri (Site dışındaki bantta, örneğin depolandıktan değil) tüm hello zaman erişilebilir olduğu depolama yaklaşımı. Microsoft Azure StorSimple Canlı arşivleme kullanır. |
| yerel olarak sabitlenmiş birim |Merhaba cihazda bulunan ve hiçbir zaman bir birim toohello bulut katmanlı. |
| Yerel anlık görüntü |Zaman içinde nokta verilerin bir kopyasını hello Microsoft Azure StorSimple cihazında depolanmış birim. |
| Microsoft Azure StorSimple |Bir veri merkezi depolama Gereci ve sağlayan yazılım oluşan güçlü bir çözüm BT kuruluşları tooleverage bulut depolama dizinindeymiş gibi veri merkezi depolama biriminde. StorSimple, maliyetleri azaltırken veri koruma ve veri yönetimini basitleştirir. Merhaba çözüm hello bulut ile sorunsuz tümleştirme yoluyla birincil depolama, Arşiv, yedekleme ve olağanüstü durum kurtarma (DR) birleştirir. SAN depolama ve bulut veri yönetimi bir kurumsal sınıf platformunda birleştirerek, StorSimple cihazları hızı, Basitlik ve güvenilirliği tüm depolama ile ilgili gereksinimler için etkinleştirin. |
| Güç ve soğutma Modülü (PCM) |StorSimple Cihazınızı hello güç kaynakları ve soğutma fanı, hello oluşan donanım bileşenleri, bu nedenle adı güç ve soğutma modülü hello. Merhaba EBOD muhafazası iki 580W PCMs sahipken hello birincil muhafaza hello aygıtın iki 764W PCMs sahiptir. |
| Birincil kasası |Ana muhafaza StorSimple cihazınızın hello uygulama platformu denetleyicileri içeriyor. |
| Kurtarma süresi hedefi (RTO) |Merhaba maksimum iş sürecini veya sistem önce expended süre miktarını tam olarak bir olağanüstü durum sonra geri yüklendi. |
| Seri Bağlı SCSI (SAS) |Sabit disk sürücüsü (HDD) türü. |
| Hizmet verileri şifreleme anahtarı |Bir anahtar StorSimple cihaz Yöneticisi hizmeti hello ile kaydeden kullanılabilir tooany yeni StorSimple cihazı yapılan. Merhaba StorSimple cihaz Yöneticisi hizmeti ile Merhaba aygıt arasında aktarılan hello yapılandırma verilerini bir ortak anahtar kullanılarak şifrelenmiş ve sonra özel bir anahtar kullanarak yalnızca hello aygıtta şifresi çözülebilir. Hizmet verileri şifreleme anahtarı hello hizmet tooobtain şifre çözme için bu özel anahtar sağlar. |
| Hizmet kayıt anahtarı |Yardımcı olan bir anahtar kaydetmeniz hello StorSimple cihazı hello StorSimple cihaz Yöneticisi hizmeti ile böylece daha fazla yönetim işlemleri için Azure portalı hello görünür. |
| Küçük bilgisayar sistemi arabirimi (SCSI) |Fiziksel bilgisayarları birbirine bağlamak ve bunlar arasında veri geçirme için standartları kümesidir. |
| katı hal sürücüsü (SSD) |Hiçbir taşıma bölümleri içeren bir diski; Örneğin, bir flash sürücüye. |
| Depolama hesabı |Erişim kimlik bilgileri kümesi tooyour depolama hesabı için verilen bulut hizmeti sağlayıcı bağlantılı. |
| SharePoint için StorSimple Bağdaştırıcısı |Saydam StorSimple depolama ve veri koruması tooSharePoint sunucu grupları genişleten bir Microsoft Azure StorSimple bileşeni. |
| StorSimple cihaz Yöneticisi hizmeti |Azure StorSimple şirket içi ve sanal aygıtların bir uzantısı olarak hello toomanage sağlayan Azure portalı. |
| StorSimple Snapshot Manager |Bir Microsoft Yönetim Konsolu (MMC) ek Microsoft Azure StorSimple yedekleme ve geri yükleme işlemleri yönetmek için bileşeni. |
| yedek alın |Bir birim etkileşimli bir yedeğini hello kullanıcı tootake sağlayan bir özelliği. El ile yedekleme biriminin karşılıklı tootaking tanımlanmış bir ilke aracılığıyla otomatik bir yedekleme almaya alternatif bir yöntemdir. |
| Ölçülü kaynak sağlama |Hangi hello ile depolama sistemlerinde kullanılabilir depolama alanı kullanılan hello verimliliği en iyi duruma getirme yöntemi. Ölçülü kaynak sağlama olarak hello depolama hello en düşük alan her kullanıcı tarafından belirli bir zamanda gerekli göre birden çok kullanıcı arasında tahsis edilir. Ayrıca bkz. *fat sağlama*. |
| Katmanlama |Geçerli kullanımı, geçerlilik süresi ve ilişki tooother veriler temel alınarak mantıksal gruplandırmaları verileri düzenleme. StorSimple otomatik olarak katmanları verileri düzenler. |
| Birim |Sürücüleri Hello formunda sunulan mantıksal depolama alanları. StorSimple birimlerini hello ana bilgisayarı, iSCSI ve StorSimple cihazını hello kullanarak bulunan dahil olmak üzere tarafından bağlı toohello birimlerin karşılık gelir. |
| Birim kapsayıcısı |Birimler ve toothem uygulanan hello ayarları gruplandırması. StorSimple Cihazınızı tüm birimlerin birim kapsayıcıları gruplandırılır. Veri şifreleme ayarlarını toocloud ilişkili şifreleme anahtarları ve hello bulut içeren işlemleri için kullanılan bant genişliği ile gönderilen, depolama hesapları birim kapsayıcı ayarlarını içerir. |
| birim grubu |StorSimple anlık görüntü Yöneticisi'nde, bir birim grubu yapılandırılmış birimleri toofacilitate yedekleme işleme koleksiyonudur. |
| Birim Gölge Kopyası Hizmeti (VSS) |VSS kullanabilen uygulamaların toocoordinate hello artımlı anlık görüntü oluşturmaya ile iletişim kurarak uygulama tutarlılığı kolaylaştıran bir Windows Server işletim sistemi hizmetidir. VSS anlık görüntülerinin alınma hello uygulamaları geçici olarak devre dışı olmasını sağlar. |
| StorSimple için Windows PowerShell |Bir Windows PowerShell tabanlı komut satırı arabirimi ve StorSimple Cihazınızı yönetmek toooperate kullanılır. Bazı Windows PowerShell temel özelliklerini hello korurken, bu arabirim StorSimple cihazı yönetme doğrultusunda sağlamıştır ek adanmış cmdlet'lere sahiptir. |

## <a name="next-steps"></a>Sonraki adımlar
Hakkında bilgi edinin [StorSimple güvenlik](storsimple-8000-security.md).

