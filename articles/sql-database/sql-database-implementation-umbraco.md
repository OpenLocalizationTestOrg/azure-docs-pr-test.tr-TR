---
title: "aaaAzure SQL veritabanı Azure örnek olay incelemesi - Umbraco | Microsoft Docs"
description: "Nasıl Umbraco SQL veritabanı tooquickly sağlamak ve ölçek Hizmetleri kiracılar binlerce hello bulutta kullandığını öğrenin"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco hello bulutta Azure SQL veritabanı tooquickly sağlamak ve kiracılar binlerce için ölçek Hizmetleri kullanır
![Umbraco logosu](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco herhangi bir şey küçük kampanya ya da broşür sitelerinden toocomplex uygulamaları Fortune 500 şirketleri ve genel medya Web siteleri için çalıştırılabilir bir popüler açık kaynaklı içerik yönetim sistemidir (CMS) ' dir. 

> "Hello sistem Umbraco çalıştıran 100. 000'den fazla geliştiricilere forumlarımıza ve canlı, birden fazla 350,000 siteleri kullanan Geliştirici oldukça büyük topluluğu sahibiz."
> 
> — Mahir Christensen, teknik sağlama, Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

toosimplify müşteri dağıtımı, Umbraco eklenen Umbraco-bir hizmet olarak (UaaS): şirket içi dağıtımlar için hello ihtiyacını ortadan kaldıran bir yazılım olarak-hizmet (SaaS) sunumu yerleşik ölçeklendirme sağlar ve yönetim ek yükü etkinleştirerek kaldırır Geliştiriciler toofocus ürün çözüm yerine yenilik yönetimi. Umbraco, Microsoft Azure tarafından sunulan esnek hizmet olarak platform (PaaS) modeli güvenmek tarafından tüm bu avantajlar hello mümkün tooprovide olur.

UaaS SaaS müşteriler toouse Umbraco CMS sağlar, daha önce kendi ulaşma dışında olan özellikleri. Bu müşterilerden üretim veritabanını içeren çalışan CMS ortamı ile sağlanır. Müşteriler, geliştirme ve hazırlık ortamları gereksinimlerine bağlı olarak ek veritabanlarını tootwo ekleyebilirsiniz. Otomatik bir işlem o müşteri bir veritabanına yeni bir ortam istendiğinde, otomatik olarak atar. Merhaba veritabanı zaten Umbraco kullanılabilir veritabanlarının (bkz: Şekil 1) bir Azure esnek havuzdan tarafından önceden sağlanmış olduğundan hello yeni veritabanı saniye cinsinden hazırdır.

![Umbraco sağlama yaşam döngüsü](./media/sql-database-implementation-umbraco/figure1.png)

Şekil 1 '. Hizmet (UaaS) olarak Umbraco için sağlama yaşam döngüsü

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Azure esnek havuzlar ve Otomasyon dağıtımları basitleştirin
Azure SQL veritabanı ve diğer Azure hizmetleriyle, Umbraco müşteriler ortamlarını otomatik olarak sağlayabilir ve Umbraco kolayca izleyebilir ve sezgisel bir iş akışının bir parçası veritabanları yönetebilirsiniz:

1. Sağlama
   
   Umbraco 200 kullanılabilir önceden sağlanan veritabanlarından esnek havuz kapasitesi tutar. Yeni bir müşteri için UaaS kaydolduğunda Umbraco hello kullanılabilirlik havuzundan bir veritabanı atayarak hello müşteri yakın gerçek zamanlı yeni bir CMS ortamıyla sağlar.
   
   Bir kullanılabilirlik havuzu kendi eşiğe ulaştığında yeni bir esnek havuz oluşturulur ve önceden sağlanan toobe gerektiği gibi toocustomers atanan yeni veritabanlarıdır.
   
   Uygulama, tamamen C# yönetim kitaplıklarını ve Azure Service Bus kuyruklarını kullanarak otomatik hale getirilmiştir.
2. Kullanma
   
   Müşteriler kendi veritabanıyla toothree ortamlarda (üretim, hazırlama ve/veya geliştirme), her kullanın. Müşteri Umbraco tooprovide tooover sağlamak zorunda kalmadan ölçeklendirme verimli sağlayan esnek havuzlarında veritabanlarıdır.
   
   ![Umbraco projeye genel bakış](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Umbraco Proje Ayrıntıları](./media/sql-database-implementation-umbraco/figure3.png)
   
   Şekil 2. Umbraco-bir hizmet olarak (UaaS) müşteri Web sitesi, projeye genel bakış ve ayrıntılarını gösterme
   
   Azure SQL veritabanı gerçek veritabanı işlemleri için gereken veritabanı işlem birimleri (Dtu'lar) toorepresent hello göreli güç kullanır. UaaS müşteriler için veritabanları genelde yaklaşık 10 Dtu'lar çalışır, ancak her hello esneklik tooscale isteğe bağlı olur. UaaS müşteriler gerekli kaynaklar, yoğun zamanlarında bile her zaman sahip olduğunuzdan emin olabilirsiniz anlamına gelir. Örneğin, bir son Pazar gece Spor olayı sırasında bir UaaS müşteri veritabanı yükselmeleri too100 Dtu'lar yukarı hello hello oyun süresince karşılaştı. Azure esnek havuzlar için Umbraco toosupport olası performans düşüşü olmadan, yüksek talep yapılan.
3. İzleme
   
   Umbraco izleyiciler hello özel e-posta uyarıları yanı sıra Azure portalı içinde panoları kullanarak etkinliği veritabanı.
4. Olağanüstü durum kurtarma
   
   Azure iki olağanüstü durum kurtarma (DR) seçenekleri sağlar: etkin coğrafi çoğaltma ve coğrafi geri yükleme. Merhaba şirket seçmelisiniz DR seçeneği bağımlı kendi [iş sürekliliği hedefleri](sql-database-business-continuity.md).
   
   Aktif coğrafi çoğaltma hello olayı kapalı kalma süresi içinde yanıt hello hızlı düzeyi sağlar. Aktif coğrafi çoğaltma kullanarak, farklı bölgelerdeki sunucular üzerinde toofour okunabilir ikinciller yukarı oluşturabilirsiniz ve yük devretme tooany hello ikincil kopya hello olay bir hatanın ardından başlatabilirsiniz.
   
   Umbraco, coğrafi çoğaltma gerektirmez, ancak bunu yararlanmak Azure coğrafi geri yükleme toohelp kesinti hello olayı içinde en az kapalı kalma süresi emin olun. coğrafi geri yükleme veritabanı yedeklemeleri coğrafi olarak yedekli Azure depolama alanında kullanır. Merhaba birincil bölgede bir kesinti olduğunda, bir yedek kopyadan kullanıcılar toorestore sağlar.
5. Devre dışı bırakma sağlama
   
   Bir proje Ortamı silindiğinde, ilişkili tüm veritabanları (geliştirme, hazırlama ya da Canlı) Azure Service Bus kuyruğu temizleme sırasında kaldırılır. Bu işlem otomatik geri yüklemeler hello kullanılmayan veritabanları tooUmbraco'nın esnek veritabanı kullanılabilirlik havuzu, en iyi koruyarak gelecekteki sağlama için kullanılabilir hale getirme.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Esnek havuzlar kolayca UaaS tooscale izin ver
Azure esnek havuzlar yararlanarak, Umbraco tooover veya eksik sağlamak zorunda kalmadan, müşterilerinin performansını iyileştirebilirsiniz. Umbraco, neredeyse 3000 veritabanı şu anda 19 esnek havuzlardaki vardır., hello özelliği tooeasily ile gerekli tooaccommodate kendi mevcut 325,000 müşteriler veya hazır toodeploy hello bulutta bir CMS olan yeni müşteriler ölçeklendirme.

Aslında, tooMorten Christensen, teknik neden Umbraco, adresindeki göre "UaaS şimdi günde yaklaşık 30 yeni müşteriler büyümesini yaşıyor. Müşterilerimizin mümkün tooprovision yeni projeler saniye cinsinden olma hello kolaylık ile mutlu, hemen güncelleştirmeleri tootheir Canlı siteleri 'tek tıklatmayla dağıtım' kullanarak bir geliştirme ortamı'ndan yayımlamak ve hatalar bulursanız gibi hızlı bir şekilde değişiklik . "

Bir müşteri ikinci ve/veya üçüncü ortamı artık gerektirmiyorsa, yalnızca o ortamları kaldırabilirsiniz. Diğer müşteriler için hello Umbraco esnek veritabanı kullanılabilirlik havuzu bir parçası olarak kullanılabilir kaynakları serbest bırakır.

![Umbraco dağıtım mimarisi](./media/sql-database-implementation-umbraco/figure4.png)

Şekil 3 '. Microsoft Azure üzerinde UaaS dağıtım mimarisi

## <a name="hello-path-from-datacenter-toocloud"></a>Veri Merkezi toocloud Hello yolundan
Merhaba Umbraco geliştiriciler başlangıçta hello karar toomove tooa SaaS modeli yapıldığında, bunlar hello hizmeti kullanıma uygun maliyetli ve ölçeklenebilir şekilde toobuild gerekir biliyorduk.

> "esnek havuzlar kapasite yukarı ve aşağı gerektiğinde arama yapmadan çünkü SaaS sunumu için mükemmel var. Sağlama kolaydır ve bizim Kurulum'a biz kullanımı en tutabilirsiniz."
> 
> — Mahir Christensen, teknik sağlama, Umbraco
> 
> 

"Biz toospend istedik bizim zamanında altyapısını yönetmeye değil, müşterilerimizin sorunlarını çözme. Biz toomake istedik bizim müşteriler tooget için kolay, hello en yüksek değeri, "Niels Hartvi'den Umbraco kurucusu söyler. "Hello sunucuları kendisini barındıran biz başlangıçta denendi, ancak kapasite planlaması bir onarımı kabus olacaktı." Tesadüfen Umbraco herhangi bir veritabanı yönetici UaaS kullanmak için bir anahtar değer teklifinde, alt çizgi uygulamadığınız değil.

Merhaba Umbraco geliştiriciler için önemli bir hedef tooprovide UaaS müşteriler tooprovision ortamları için bir yol kapasite sınırlamaları duymadan ve hızla oluştu. Ancak işlemede WINS'e adanmış bir barındırılan hizmet Umbraco veri merkezlerinde fazlalık kapasite toohandle gerekli miktarda olurdu sağlama. Düzenli olarak gereğinden az çok miktarda bilgi işlem altyapısı ekleme yapısındaki.

Ayrıca, bunları kendi var olan kodu mümkün olduğunca çok tooreuse belirleyebilmesini bir çözüm hello Umbraco geliştirme ekibi istedik. Umbraco geliştirici olarak Mikkel Madsen durumları, "biz biz zaten Microsoft SQL Server, Microsoft Azure SQL veritabanı, ASP.net ve Internet Information Services (IIS) gibi bilmiyorsanız, hello Microsoft geliştirme araçları ile mutluluk. Bir Iaas veya bir PaaS yatırım yapmadan önce bulut çözümü, biz toomake toomake büyük değişikliklerin tooour kod tabanını sahip olmayacaktır şekilde bu bizim Microsoft araçları ve platformları, desteklediğinden emin istedik. "

Tüm toomeet nitelikleri aşağıdaki hello ile bulut iş ortağı için Umbraco kendi ölçütleriyle Aranan:

* Yeterli kapasitesi ve güvenilirliği
* Destek mühendisleri olmaması, Umbraco toocompletely zorunlu şekilde Microsoft geliştirme araçları, geliştirme ortamlarını reinvent
* Merhaba coğrafi pazarda UaaS (işletmelerin gerek tooensure bunlar verilerine hızlı bir şekilde erişebilmesini ve verilerini bölgesel yasal düzenleme gereksinimlerine uyan bir konumda depolanır) rekabet tümünde varlığı

## <a name="why-umbraco-chose-azure-for-uaas"></a>Neden Azure Umbraco UaaS için seçtiğiniz
TooMorten "tüm bizim ölçütlerden, yönetilebilirlik ve ölçeklenebilirlik toofamiliarity ve düşük maliyet karşılanır çünkü bizim seçenekleri düşünüldükten sonra Azure seçtik. Christensen göre Biz hello ortamları Azure vm'lerinde ayarlayın ve her ortam esnek havuzlar tüm hello örnekleri kendi Azure SQL veritabanı örneğine sahip. Veritabanları geliştirme, hazırlama ve canlı ortamlar arasında ayırarak biz müşterilerimizin sağlam performans sunabilir yalıtım eşleşen tooscale — büyük kazanım. "

Mahir devam önce "biz tooprovision sunucuları web veritabanları için el ile vardı. Şimdi, biz toothink ilgili yok. Her şeyi otomatik olarak — toocleanup sağlama gelen. "

Mahir de Azure tarafından sağlanan özellikleri ölçeklendirme hello ile memnun olur. "esnek havuzlar kapasite yukarı ve aşağı gerektiğinde arama yapmadan çünkü SaaS sunumu için mükemmel var. Sağlama kolaydır ve bizim Kurulum'a biz kullanımı en tutabilirsiniz." Mahir durumları, "hizmet katmanı tabanlı Dtu'lar hello uyumluluğunu birlikte esnek havuzlar hello basitliği bize, hello güç tooprovision yeni kaynak havuzları isteğe bağlı'sağlar. Yakın zamanda, büyük müşterilerimizin birini too100 Dtu'lar Canlı ortamında si. Azure kullanarak, bizim esnek havuzlar toopredict DTU gereksinimleri gerekmeden gerçek zamanlı olarak gereken hello kaynaklarla hello Müşteri'nin veritabanlarını sağlamıştır. Basitçe, müşterilerimizin hello çevirme süresinin bekledikleri ve biz bizim performansı hizmet düzeyi sözleşmelerinin karşılayabilecek alın."

Mikkel Madsen onu toplar: "biz hello üstünde (veritabanları, her iki geliştirme önceden sağlama ve canlı) bir ortak SaaS senaryo (gerçek zamanlı ölçekte ekleme yeni müşteriler) tooour uygulama düzeni bağlayan hello güçlü Azure algoritması embraced temel alınan teknoloji. (Azure SQL veritabanı ile birlikte Azure Service Bus kuyruklarını kullanan)"

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Azure ile müşteri beklentilerini UaaS aşıyor
Azure, bulut iş ortağı olarak seçerek bu yana Umbraco mümkün tooprovide UaaS müşterilerin kendi kendini barındıran bir çözümden gerekli hello BT kaynak yatırım olmadan en iyi duruma getirilmiş içerik yönetimi performans olmuştur. Mahir diyor gibi "biz hello geliştiriciye kolaylık sağlamak ve Azure bize veriyor ölçeklenebilirlik memnuniyet ve müşterilerimizin hello özellikleri ve güvenilirliği ile thrilled. Genel olarak, bunu bize için harika bir win olmamıştı!"

## <a name="more-information"></a>Daha fazla bilgi
* toolearn Azure esnek havuzları hakkında daha fazla bilgi görmek [esnek havuzlar](sql-database-elastic-pool.md).
* Azure Service Bus hakkında daha fazla toolearn bkz [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* Web rolleri ve çalışan rolleri hakkında daha fazla toolearn bkz [çalışan rolleri](../fundamentals-introduction-to-azure.md#compute).    
* sanal ağlar hakkında daha fazla toolearn bkz [sanal ağ](https://azure.microsoft.com/documentation/services/virtual-network/).    
* Yedekleme ve kurtarma hakkında daha fazla toolearn bkz [iş sürekliliği](sql-database-business-continuity.md).    
* ppols, izleme hakkında daha fazla toolearn bkz [havuzları izleme](sql-database-elastic-pool-manage-portal.md).    
* bir hizmet olarak Umbraco hakkında daha fazla toolearn bkz [Umbraco](https://umbraco.com/cloud).

