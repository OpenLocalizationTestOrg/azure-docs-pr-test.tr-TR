---
title: "Eclipse için Azure Araç Seti yenilikleri"
description: "Eclipse için Azure Araç Seti en son özellikler hakkında bilgi edinin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 71c4f2d2298ea54f18e9ed64b246966b470a4ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Eclipse için Azure Araç Seti yenilikleri
## <a name="azure-toolkit-for-eclipse-releases"></a>Eclipse yayımları için Azure Araç Seti
Bu makale çeşitli yayınları ve Azure araç setini Eclipse için en son güncelleştirmeleri hakkında bilgi içerir.

> [!NOTE]
> Intellij IDE için bir Azure Araç Seti yoktur. Daha fazla bilgi için bkz: [Intellij için Azure Araç Seti].
> 
> 

### <a name="april-14-2017"></a>14 Nisan 2017
Azure araç setini Eclipse - Nisan 2017 yayın için aşağıdaki geliştirmeleri içerir:

* **Azure deneyimi oturum geliştirilmiş**: Eclipse için Azure Araç Seti artık Azure hesabınızda oturum açılırken iki yöntemi destekler: *etkileşimli* ve *otomatik*. Daha fazla bilgi için bkz: [içinde Azure oturum yönergeler Eclipse için Azure Araç Seti için].
* **Docker kapsayıcıları kullanma yayımlama**: Docker Eclipse için Azure Araç Seti kullanarak kapsayıcı olarak, web uygulamalarınızı şimdi yayımlayabilirsiniz. Daha fazla bilgi için bkz: [Docker Eclipse için Azure Araç Seti kullanarak bir kapsayıcı olarak bir Web uygulaması yayımlama].
* **Depolama hesap yönetimi**: Azure araç setini Eclipse için artık desteklemektedir depolama hesaplarınızı Azure Explorer görünümünden yönetme. Daha fazla bilgi için bkz: [depolama Eclipse için Azure Explorer'ı kullanarak hesapları yönetme].
* **Sanal Makine Yönetimi**: Eclipse için Azure Araç Seti artık destekler Azure Explorer görünümünden sanal makinelerinizi yönetme. Daha fazla bilgi için bkz: [yönetme Azure Gezgini Eclipse için kullanarak sanal makineleri].
* **Uzaktan hata ayıklama desteği kaldırılmasını**. Azure araç setini Eclipse için Azure App Service'te Java web uygulamaları uzaktan hata ayıklama kaldırıldığı; Bu araç seti kullanırken müşteriler yaşıyordu bazı sorunları gidermek gerekliydi.

### <a name="august-26-2016"></a>26 Ağustos 2016
Azure araç setini Eclipse - Ağustos 2016 sürüm için aşağıdaki geliştirmeleri içerir:

* **Özel JDK dağıtımları**. Eclipse için Azure Araç Seti artık belirtme ve rasgele bir JDK sürümü, Azure WebApp kapsayıcıya dağıtma destekler:
  * Azure tarafından sağlanan JDKs yanı sıra, Azure üzerinde Azul sistemler tarafından kullanılabilir hale Zulu dili OpenJDK sürümlerinin geniş seçimden seçebilirsiniz.
  * Depolama hesabınıza bir ZIP dosyası yüklerseniz, ayrıca kendi JDK dağıtım belirtebilirsiniz.
* **Azure Explorer görünümü geliştirmeler**:
  * Azure'nın yeni Resource Manager modelini kullanarak sanal makine yönetimi desteği: listesinde, oluşturabilir ve IDE ayrılmadan resource manager tabanlı sanal makineleri silin.
  * "Klasik" depolama hesapları yönetmek için var olan işlevselliği tamamlar Azure Resource Manager kullanarak depolama hesabı blob yönetimi için destek.
* **SQL Server için Microsoft JDBC sürücüsü 6.0**. Bu güncelleştirme, Microsoft SQL olan sunucu için (v6.0), en son JDBC sürücüsü içerir, Java projenize kolayca ekleyebilirsiniz kitaplık olarak dahil artık eski sürümü böylece değiştirme.

### <a name="june-29-2016"></a>29 Haziran 2016
Azure araç setini Eclipse - Haziran 2016 sürüm için aşağıdaki geliştirmeleri içerir:

* **Java 8 gereksinim**. Eclipse için Azure Araç Seti artık Java 8, gerektirir ancak bu gereksinim yalnızca için araç seti - uygulamalarınız Java'nın Azure tarafından desteklenen tüm sürümleri kullanmaya devam edebilirsiniz.
* **En son Java JDKs desteği**. Java JDKs en son sürümlerini şimdi Eclipse için Azure Araç Seti tarafından desteklenir.
* **Azure SDK'sı v2.9.1 desteği**. Azure SDK'nin en son sürümünü Eclipse için Azure Araç Seti için minimum önkoşul sunulmuştur.
* **Örnekleri tümleşik**. Eclipse için Azure Araç Seti artık başlama geliştiricilerin yardımcı olmak için birkaç örnek uygulama özellikleri.
* **Hdınsight aracı tümleştirme**. Azure Hdınsight araçları şimdi Eclipse için Azure araç seti ile paketlenmiştir. Daha fazla bilgi için bkz: [Eclipse için Hdınsight araçları eklentisi].
* **Uzaktan hata ayıklama Java Web uygulamaları**. Eclipse için Azure Araç Seti artık Azure App Service'te Java web uygulamaları uzaktan hata ayıklama destekler.
* **Eclipse Luna sürümü için destek.** Yeni minimum gerekli Eclipse IDE Luna sürümüdür.

### <a name="april-12-2016"></a>12 Nisan, 2016
Azure araç setini Eclipse - Nisan 2016 sürüm için aşağıdaki geliştirmeleri içerir:

* **Azure SDK'sı v2.9.0 desteği**. Azure SDK'nin en son sürümünü Eclipse için Azure Araç Seti için minimum önkoşul sunulmuştur.
* **Çeşitli kullanılabilirlik, yanıtlama ve performans iyileştirmeleri ilgili Azure Web uygulaması desteklemek için**. Bir dizi araç seti Azure sonucu ile nasıl iletişim kurduğu, performans iyileştirmelerini daha iyi yanıt arabiriminde.
* **Var olan bir Web uygulaması kapsayıcıyı Eclipse içinde azure'da silme yeteneği**. Eclipse için Azure Araç Seti artık Eclipse ayrılmadan var olan bir Azure Web kapsayıcı silmenize olanak sağlar.

### <a name="march-7-2016"></a>7 Mart 2016
Azure araç setini Eclipse - Mart 2016 sürüm için aşağıdaki geliştirmeleri içerir:

* **Hızlı Dağıtım basit Java uygulamaları için destek**. Eclipse için Azure Araç Seti artık Azure Web uygulaması kapsayıcıları, basit Java uygulamalara hızlı dağıtımı destekler, böylece artık Java uygulamalarını dağıtma dakika yerine saniye sürer.
* **Azure Explorer görünümü kullanarak Web uygulaması yönetimi için destek**. Araç Seti Azure Gezgini görünümünde, listeleme, başlatma ve durdurma Azure Web Apps artık destekler.
* **Güncelleştirilmiş Tomcat, Jetty, Zulu dili OpenJDK dağıtımları**. Eclipse için Azure Araç Seti Tomcat, Jetty ve Zulu dili OpenJDK güncelleştirilmiş sürümleri Azure bulut hizmetlerine Java dağıtımlar için destek sağlar.

### <a name="january-4-2016"></a>4 Ocak 2016
Azure araç setini Eclipse - Ocak 2016 sürüm için aşağıdaki geliştirmeleri içerir:

* **Zulu dili OpenJDK güncelleştirmeler için destek**. Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **Güncelleştirilmiş Tomcat ve Jetty dağıtımları**. Hangi Microsoft Azure üzerinde Azure araç seti ile Eclipse için kullanılabilir Jetty, Tomcat dağıtımları güncelleştirildi.
* **Özellik eşliği Eclipse Intellij araç takımları Azure arasındaki**. Eclipse için Azure Araç Seti ve [Intellij için Azure Araç Seti] artık özellikleri aynı kümesini destekler.

### <a name="september-1-2015"></a>1 Eylül 2015
Azure araç setini Eclipse - Eylül 2015 sürüm için aşağıdaki geliştirmeleri içerir:

* **Zulu dili OpenJDK güncelleştirmeler için destek**. Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **Güncelleştirilmiş Tomcat ve Jetty dağıtımları**. Hangi Microsoft Azure üzerinde Azure araç seti ile Eclipse için kullanılabilir Jetty, Tomcat dağıtımları güncelleştirildi. (Bu dağıtımları, geliştiricilerin hızlı geliştirme oluşturmak ve test projeleri Eclipse için Azure araç sağlar.
* **Otomatik olarak güncelleştirilen Tomcat ve Jetty başvurular için destek**. Azure üzerinde kullanılabilir olan belirli sürümlerini Tomcat ve Jetty yanı sıra, geliştiriciler artık olarak adlandırılan bir dağıtım başvurabilirsiniz "en son (otomatik güncelleştirilmiş)", hangi otomatik olarak rolü örneklerinizi her ana sürüm Tomcat veya Jetty son dağıtımına sonraki güncelleştirilecek geri dönüştürüldüğünde. (Geri dönüştürme otomatik olarak gerçekleşir, ancak geliştiriciler Azure Portalı aracılığıyla bir geri dönüşüm el ile tetikleyebilir.) Bu yeni özellik, geliştiricilerin güncelleştirilen sunucu yazılımlarını alabilmesi için kendi uygulama dağıtmanız gerekmez anlamına gelir. (
* Bu işlevsellik şu anda yalnızca geliştirme ve test amacıyla ya da görev kritik olmayan uygulamalar için tasarlanmıştır ve üretim için önerilmez.)
* **Azure Gezgin Görünümü BLOB, kuyruklar ve tablolar Azure depolama alanında**. Bu, geliştiricilerin kendi depolama yapıları ile ortak görevler bir dizi doğrudan Eclipse IDE içinden gerçekleştirmesini olanak tanır. Örneğin: silme, karşıya yükleme veya BLOB'ları yükleniyor.

### <a name="august-1-2015"></a>1 Ağustos 2015
Azure araç setini Eclipse - Ağustos 2015 sürüm için aşağıdaki geliştirmeleri içerir:

* **Uygulama Insights araçları anahtar yönetimi**. Bu güncelleştirme, alma, oluşturma ve Application Insights araçları anahtarlarınızı doğrudan Eclipse IDE içinden yönetmenize olanak sağlar.
* **SQL Server için Microsoft JDBC sürücüsü 4.1**. Bu güncelleştirme, Microsoft SQL Server için en son JDBC sürücüsü için destek içerir.
* **Azure SDK sürüm 2.7**. Bu en son Azure SDK'sının Windows yüklendiğinde Araç Seti için yeni önkoşul güncelleştirmesidir. (Unutmayın. Bu Windows olmayan işletim sistemlerinde gerekli değildir.)
* **Zulu dili OpenJDK v7 güncelleştirme desteği**. Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].

### <a name="may-1-2015"></a>1 Mayıs 2015
Azure araç setini Eclipse - Mayıs 2015 sürüm için aşağıdaki geliştirmeleri içerir:

* **Sunucu seçimi UI geliştirilmiş**. Bu sürüm Windows olmayan işletim sistemlerinde araç kullanımını basitleştirir.
* **Maven projeleri için desteği**. Bu sürümde Araç Seti Azure'a dağıtabilirsiniz uygulamaları olarak Maven projelerini destekler ve Application Insights yapılandırın.
* **Azure SDK 2.6 sürümü**. Bu en son Azure SDK'sının Windows yüklendiğinde Araç Seti için yeni önkoşul güncelleştirmesidir. (Unutmayın. Bu Windows olmayan işletim sistemlerinde gerekli değildir.)
* **Yeniden yayımlama yerine dağıtım yükseltmeyi**. Önceki sürümü zaten Canlı olduğunda bir dağıtım projesi yeniden yayımlanması, araç seti önceki dağıtım kapatılıyor ve geçmişte yaptığınız gibi baştan yeniden yayımlanması yerine Azure'nın dağıtım yükseltme işlevi artık kullanır. Bu, mümkün olduğunda bile güncelleştirme sırasında yüksek kullanılabilirlik elde etmeye yardımcı kesintisiz çalıştırmak, bulut hizmetini etkinleştirir ve yeniden yayımlama işlemini hızlandırır.
* **Desteklemek için en son Zulu dili OpenJDK v8 - 40 güncelleştirme**. Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].

### <a name="march-9-2015"></a>9 Mart 2015
Azure araç setini Eclipse - Mart 2015 sürüm için aşağıdaki geliştirmeleri içerir:

* **Mac, Ubuntu ve ek Linux özellikleri için destek**. Geliştiriciler oluşturmak, yapılandırmak ve Azure bulut hizmetlerine (PaaS) Windows dışındaki işletim sistemlerinde çalışan Eclipse Java projeleri yayımlamak için araç seti yükleyebilmek için bu sürüm Azure araç setini Eclipse için Mac OS ve birkaç UNIX platform desteği ekler.

> [!NOTE]
> Bu özellik Önizleme aşamasındadır ve üretim ortamlarında kullanım için önerilmez. Hizmet düzeyi sözleşmesi (SLA) müşteri desteği yoktur, ancak tüm geri bildirim takdir ve teşvik.
> 
> 

* **Yeni Application Insights eklentisiyle**. Geliştiriciler artık Azure üzerinde Application Insights kullanarak otomatik sunucu telemetri yapılandırmadı.
* **Ant tabanlı komut satırı dağıtım Otomasyon**. Bu özellik yayımlama Eclipse dışında Ant kullanarak dağıtımlarını daha yeni sürümleri için otomatik hale getirmek geliştiricilere sağlar. İlk kez Eclipse dağıtıldıktan sonra sonraki dağıtımları tam olarak dağıtımlar yalnızca komut satırı aracılığıyla otomatikleştirmek için komut dosyasını kullanabilirsiniz, önceden oluşturulan bir komut dosyası için bir proje otomatik olarak yapılandırılır.
* **Daha basit ve hızlı dağıtımı için Azure üzerinde tomcat ve Jetty kullanılabilirlik**. Geliştiriciler, bunun yerine bir Java sunucu hesaplarını (veya araç takımı aracılığıyla), bu nedenle karşıya gerek kalmadan yoktur doğrudan hızlı, başlama senaryoları için Java sunucu karşıya yüklemeye gerek Azure'da kullanılabilen çeşitli Tomcat ve Jetty sürümleri artık başvurabilirsiniz.
* **Azure bulut hizmetlerine Java web uygulamaları yayımlamak için kısayol yöntemi**. Basit geliştirme ve test senaryoları için öğrenme eğrisini düşürebilir, geliştiriciler artık Java uygulamalarını daha doğrudan Azure yayımlayabilirsiniz. Oluşturma ve Azure dağıtım projesi yapılandırma sürecinde Git gerek kalmadan yerine uygulamaları Tomcat v8 ve Zulu dili JVM (OpenJDK) varsayılan örneği ile dağıtılır.

### <a name="january-30-2015"></a>30 Ocak 2015
Azure araç setini Eclipse - Ocak 2015 sürüm için aşağıdaki geliştirmeleri içerir:

* **IBM® WebSphere® uygulama sunucusu özgürlük çekirdek desteği**. Bu sürüm IBM WebSphere uygulama sunucusu özgürlük çekirdek Araç Seti Azure'a dağıtmak için desteklenen uygulama sunucuları listesine ekler. Desteklenen uygulama sunucuları geçerli listesini bu son eklemeyi genişletir &quot;Giden Kutusu&quot; araç takımı tarafından hangi zaten dahil çeşitli Tomcat, Jetty, JBoss ve GlassFish sürümleri.
* **Application Insights SDK ekleme**. Bu yeni yayımlanan istemci API kitaplığı (v0.9.0) artık Java için Azure kitaplıkları için paketi bir parçasıdır.
* **Java için Azure kitaplıkları için paket güncelleştirilmiş**. Bu güncelleştirme, Java v0.7.0 ve depolama istemci API v2.0.0, yanı sıra için yeni yayımlanan Application Insights SDK'sı v0.9.0 Azure kitaplıkları içerir.

### <a name="november-12-2014"></a>12 Kasım 2014
Azure araç setini Eclipse - Kasım 2014 sürümü için aşağıdaki geliştirmeleri içerir:

* **Azure SDK'sı 2.5 desteği**. Bu en son Azure SDK'sı için araç seti için yeni önkoşul güncelleştirmesidir.
* **Güncelleştirilmiş sürümünü Zulu dili OpenJDK v1.8, v1.7 ve v1.6 paketleri için destek**. Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **Bulut Hizmetleri için yeni standart D boyutları için destek**, performansı artırmak ve ek bellek kaynaklarının sunar. Daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure].

### <a name="october-17-2014"></a>17 Ekim 2014
Azure araç setini Eclipse - Ekim 2014 sürümü için aşağıdaki geliştirmeleri içerir:

* **Yayımla bulut senaryosu için performans iyileştirmeleri**. Birden çok abonelikleri ve storage hesaplarını kullanıcınız varsa, abonelik bilgilerini yüklenmesi daha hızlıdır.
* **Zulu dili OpenJDK v1.8 paketinin güncelleştirilmiş sürümü için destek**. Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **3 taraf JDKs eski sürümleri onaysız kılınmadan desteği**. Kullanım dışı JDK paketleri artık yeni dağıtım projeleri için açılır menüde görünecektir. Mevcut projeleri başvuru kullanım dışı JDK paketleri olma süresi olan, ancak önerilir en son yararlanmayı böyle projelerini yükseltme için bunun mümkün devam eder.
* **Güncelleştirilmiş sürümü paket Azure kitaplıkları için Java İstemcisi API Kitaplığı**. Daha fazla bilgi için bkz: [Microsoft Azure istemci API].
* **Hata düzeltmeleri.** Bu sürüm, kullanıcı raporları ve test temel alan çeşitli hata düzeltmeleri içerir.

### <a name="august-5-2014"></a>5 Ağustos 2014
Azure araç setini Eclipse - Ağustos 2014 sürümü için aşağıdaki geliştirmeleri içerir

* **Azure SDK 2.4 desteği.** Eclipse Araç Seti eski sürümleri, bu yeni yayımlanmış SDK ile birlikte çalışmaz.
* **Güncelleştirilmiş Zulu dili OpenJDK v1.6 sürümlerini 1.7 ve v1.8 paketleri.** Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **Java İstemcisi API kitaplığı güncelleştirilmiş sürüm Azure kitaplıkları için paketi.** Daha fazla bilgi için bkz: [Microsoft Azure istemci API].
* **Son desteği yayımlama ayarları dosyası biçimi.** Yayımlama ayarları dosyası biçimi 2.0 sürümü için destek eklendi.
* **Mimari değişiklikler bulut özelliğini Yayımla arkasında.** Araç Seti artık yeni yayımlanmış Microsoft Azure istemci API Java için bulut ile yayımlama desteğini kullanıyor.
* **Hata düzeltmeleri.** Bu sürüm kullanıcı tarafından istenen hata düzeltmeleri içerir.

### <a name="june-12-2014"></a>12 Haziran 2014
Azure araç setini Eclipse - Haziran 2014 sürümü için aşağıdaki geliştirmeleri sağlayan küçük bir bakım güncelleştirmesidir:

* **Zulu dili OpenJDK paket v1.8 desteği.** Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **Zulu dili OpenJDK v1.6 ve 1,7 paketlerinin güncelleştirilmiş sürümleri.** Daha fazla bilgi için bkz: [Azul sistemleri web sayfası için Zulu dili OpenJDK].
* **Java İstemcisi API kitaplığı güncelleştirilmiş sürüm Azure kitaplıkları için paketi.** Daha fazla bilgi için bkz: [Microsoft Azure istemci API].
* **Hata düzeltmeleri.** Bu sürüm kullanıcı tarafından istenen hata düzeltmeleri içerir.

### <a name="april-4-2014"></a>4 Nisan 2014
Eclipse - Nisan 2014 sürümü için Azure eklentisi yayımladı. Bu, bir önkoşul ve eklenti yüklediğinizde otomatik olarak yüklenecek Azure SDK 2.3 sürümü ile birlikte gelen bir güncelleştirmedir. Şubat 2014 Önizleme olduğundan bu güncelleştirme yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **Azure SDK 2.3 sürümü için destek.** Eclipse - Nisan 2014 sürümü için Azure eklentisi Azure SDK 2.3 gerektirir. Azure SDK 2.3 zaten yoksa yeni eklenti kullanırken, kendi yüklemesine izin vermek için istenir. Azure SDK 2.3 eklentisi önceki sürümleriyle kullanmayın.
* **Uygulamaların tam paket dağıtımı olmadan yükseltme.** Böylece güncelleştirin ve yeniden oluşturun ve tüm paketi yeniden dağıtmak zorunda kalmadan en son uygulama BITS dağıtmak için rol örnekleri geri dönüşüm projenizi parçası olan Java uygulamaları dağıtırken eklentisi artık otomatik olarak bunları seçilen depolama hesabınızda yükler.
* **Tomcat 8 artık bir uygulama tarafından tanınmıyorsa sunucusudur.** İçinde makinenizde Tomcat 8 yükleme dizini seçerseniz **Server** sekmesinde **Azure dağıtım projesi** iletişim kutusunda, eklenti şimdi otomatik olarak algılar ve Tomcat 8, Tomcat eski sürümleri zaten listede benzer otomatik bir şekilde dağıtmak için.
* **Azul Zulu dili OpenJDK paket güncelleştirmesi: v1.7 güncelleştirmesi 51 ve v1.6 güncelleştirme 47.** Bu sürümde, Azul sistemin Zulu dili açık JDK v7 paket güncelleştirmesi 51 kullanılabilir etkilidir. Ayrıca, güncelleştirme 47'den itibaren kullanılabilir olmasını durduracak Zulu dili açık JDK v6 paketleri başlar. Bu güncelleştirmeler 45 yanı sıra önceden kullanılabilir Zulu dili açık JDK v7 paket güncelleştirme, 40 güncelleştirme ve 25 güncelleştirin.
* **A8 ve A9 Microsoft Azure sanal makine boyutu için destek.** Bir bulut hizmeti artık, yüksek bellek A8 ve A9 sanal makine boyutlarını da dağıtabilirsiniz. Bu VM boyutları hakkında daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure].
* **Otomatik yeniden yönlendirme HTTP'den HTTPS'ye SSL etkin rolleri için.** Kullanıcı isteği HTTP belirtiyorsa bulut hizmetinizin yalnızca HTTPS rolleri içeriyorsa, otomatik olarak HTTPS için yönlendirir. HTTP isteklerini işlemek için ayrı bir rol oluşturmak için gerek yoktur.
* **Yerel öykünmesi için kullanılan Emulator express.** Express Azure öykünücüsü, şimdi uygulamalarınızı yerel olarak hata ayıklama sırasında öykünücüsü olarak kullanılır.
* **Azure Microsoft Azure rebranded.** UI ekranlarını artık Azure rebranded ve artık Azure adlı yansıtır.

### <a name="february-6-2014"></a>6 Şubat 2014
Eclipse için - Şubat 2014 Azure eklentisi Önizleme yayımladı. Bu güncelleştirme, Ekim 2013 Önizleme bu yana yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **SSL boşaltma desteği.** Güvenli Yuva Katmanı (SSL) yük boşaltma kolayca SSL Java uygulama sunucunuzu yapılandırmak gerek kalmadan, azure'da Java dağıtımınızdaki Köprü Metni Aktarım Protokolü güvenli (HTTPS) desteğini etkinleştirmek sağlayan bir özellik olarak eklenmiştir. Bu oturum benzeşimi, özellikle geçerlidir ve/veya kimliği doğrulanmış iletişim senaryoları. Örneğin, araç takımı tarafından önceden desteklenen erişim denetimi Hizmeti'nden (ACS) filtresi kullanarak. Daha fazla bilgi için bkz: [SSL boşaltma] ve [kullanım SSL boşaltma nasıl].
* **GlassFish 4 artık bir uygulama tarafından tanınmıyorsa sunucusudur.** İçinde makinenizde GlassFish 4 yükleme dizini seçerseniz **Server** sekmesinde **Azure dağıtım projesi** iletişim kutusunda, eklenti şimdi otomatik olarak algılar ve GlassFish OSE 4, zaten listede GlassFish OSE 3 sürümüne benzer otomatik bir şekilde dağıtmak için.
* **Azul Zulu dili OpenJDK paket güncelleştirmesi 45.** Bu sürümde etkili Azul sistemin Zulu dili (açık JDK v7 paketi) güncelleştirme 45 şimdi kullanılabilir; Bu daha önce kullanılabilir yanı sıra 40 ve güncelleştirme 25 güncelleştirmesidir.
* **Özel 'auto' için uç nokta bağlantı noktalarını destekler.** Otomatik giriş uç noktaları ve bir bağlantı noktası Bu uç noktasına otomatik olarak ata Azure izin vermek için iç uç noktaları için özel bir bağlantı noktası ayarlayabilirsiniz. Daha önce yalnızca belirli bağlantı noktası numarası atayabilirsiniz.
* **Sertifika adı (CN) otomatik olarak imzalanan sertifika oluşturma UI Özelleştirme desteği.** Aynı sabit kodlanmış adı daha önce tüm yeni sertifikalar için kullanılır; Şimdi, farklı amaçlar için kullanılan Azure portalında birden çok sertifika ayırt yardımcı olmak için kendi sertifika adı belirtebilirsiniz.
* **Azure araç çubuğu:** Azure araç aşağıdaki değişiklikleri güncelleştirilmiş vardır: 
  * ![][ic710876]Bu simge için eklenmiştir **yeni Azure dağıtım projesi**.
  * ![][ic710877]Bu simge otomatik olarak imzalanan sertifika oluşturma iletişim kutusu için bir kısayol olarak eklendi.
* **A5 Azure sanal makine boyutu için destek.** Bu gibi durumlarda, bir bulut hizmeti artık yüksek bellek A5 sanal makine boyutu dağıtabilirsiniz. Bu VM boyutu hakkında daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure].
* **Microsoft Windows Server 2012 R2 desteği.** Şimdi bulut işletim sistemi olarak Windows Server 2012 R2 seçebilirsiniz.

### <a name="october-22-2013"></a>22 Ekim 2013
Azure eklentisi Eclipse - Ekim 2013 Preview sürümünü yayımladı. Eylül 2013 Önizleme olduğundan bu güncelleştirme yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **Azure SDK 2.2 sürümü için destek.** Eclipse için-Azure eklentisi Ekim 2013 önizlemesini Azure SDK'sı 2.2 destekler. Eklentisi Azure SDK 2.1 ile çalışmaya devam eder ve en az Azure SDK 2.1 yüklenmiş zaten yoksa Azure SDK 2.2 otomatik olarak yüklenir.
* **Azul Zulu dili OpenJDK paket güncelleştirmesi 40.** Eylül 2013 için bildirilen gibi Önizleme, kendi JDK yüklemeye gerek kalmadan doğrudan Azure üzerinde sağlanan üçüncü taraf JDK kullanarak eklentisi şimdi etkinleştirir. Ekim 2013 sürümde Azul sistemin Zulu dili (açık JDK v7 paketi) güncelleştirme 40 artık kullanılabilir; Bu özgün olarak yayımlanmış yanı sıra 25 güncelleştirmesidir.
* **Bulut dağıtım bağlantısı etkinlik günlüğünde.** Azure etkinlik dağıtımınızın durumunu olduğunda günlüğü içinde **yayımlanan**, tıklayabilirsiniz **yayımlanan** beri şimdi dağıtımınızı bağlantısını; dağıtımınız sonra tarayıcınızda açılır. (Durumunu **yayımlanan** daha önce etiketli **çalıştıran**.)
* **Hedef işletim sistemi seçimi adresinde zaman yayımlayın.** **Azure Yayımla** iletişim içeren yeni bir alan **hedef işletim sistemi**, hedef işletim sisteminizin ayarlamanız için daha bulunabilirlik bir yol sağlar.
* **Önceki dağıtımın otomatik olarak üzerine yazın.** **Azure Yayımla** iletişim içeren yeni bir onay kutusu **önceki dağıtım üzerine**. Bu seçenek işaretlenirse, ne zaman yeni dağıtımınızı yayımlanır önceki dağıtımı; otomatik olarak üzerine yazar değil deneyimi &quot;409 çakışma&quot; aynı konuma ilk önceki dağıtım yayımdan kaldırma olmadan yayımlarken sorunları.
* **Jetty 9 artık bir uygulama tarafından tanınmıyorsa sunucusudur.** İçinde makinenizde Jetty 9 yükleme dizini seçerseniz **Server** sekmesinde **Azure dağıtım projesi** iletişim kutusunda, eklenti şimdi otomatik olarak algılar ve Jetty 9, zaten listede eski sürümleri Jetty, benzer otomatik bir şekilde dağıtmak için.
* **Proje kısayol menüsünden bir rolü ekleyin.** **Azure** proje bağlam menüsü artık yeni bir menü öğesi içerir **Rol Ekle**, daha hızlı bir sağlayan ve yeni bir rol Azure projenize eklemek daha fazla bulunabilir yol.
* **Java kitaplığı için Azure kitaplıkları için paketi için bir güncelleştirme.** Bu sürümüne 0.4.6 bağlı [Microsoft Azure istemci API].

### <a name="september-25-2013"></a>25 Eylül 2013
Azure eklentisi Eclipse - Eylül 2013 Preview sürümünü yayımladı. Ağustos 2013 Önizleme olduğundan bu güncelleştirme yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **Azure üzerinde kullanılabilir Azul Zulu dili OpenJDK paketi dağıtma yeteneği.** Yeni bir seçenek Azure dağıtımı ile kullanmak üzere JDK belirtirken eklendi. Bu seçeneği kullanarak, kendi karşıya yüklemek zorunda kalmadan bir üçüncü taraf JDK pakete doğrudan Azure bulut dağıtabilirsiniz. Azul sistemleri gibi bu seçeneği kullanarak dağıtılabilen OpenJDK dayalı çağrılan Zulu dili paketini ilk sağlamaktadır.
* **Java kitaplığı için Azure kitaplıkları için paketi için bir güncelleştirme.** Bu sürümüne 0.4.5 bağlı [Microsoft Azure istemci API].

### <a name="august-1-2013"></a>1 Ağustos 2013
Azure eklentisi Eclipse - Ağustos 2013 Preview sürümünü yayımladı. Bu, bir önkoşul ve eklenti yüklediğinizde otomatik olarak yüklenecek Azure SDK 2.1 sürümünü eşlik eden bir güncelleştirmedir. Bu güncelleştirme, Temmuz 2013 Önizleme bu yana yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **Yerel uygulama sunucusu ve yerel JDK dağıtım paketinin bir parçası olarak eklenecek seçenekleri kaldırma.** JDK indiriliyor ve uygulama sunucusu dağıtımı sırasında bulut depolama biriminden daha küçük dağıtım paket boyutu, daha hızlı dağıtım süreleri ve daha kolay bakım öğeleri sonuçlarında indirme itibaren pakette, bu bileşenlerin katıştırma için tercih. Sonuç olarak, JDK eklenecek seçenekleri ve uygulama sunucusu dağıtım paketinden kaldırılır. Dağıtım paketinin parçası JDK otomatik karşıya yükleme için otomatik olarak dönüştürülecek gibi yerel JDK ve yerel uygulama sunucusu eklemek için yapılandırılmış olan mevcut projeleri ve uygulama sunucusu bulut depolama.
* **Azure SDK 2.1 sürümü için destek.** Azure eklentisi Eclipse - Ağustos 2013 Önizleme Azure SDK 2.1 gerektirir. Ağustos 2013 Önizleme Azure SDK'sını önceki sürümleriyle kullanmayın ve Azure SDK 2.1 Eclipse için Azure eklentisi önceki sürümleriyle kullanmayın.
* **Eclipse Kepler sürümü için destek.** Bu konuyla ilgili, yeni gerekli en düşük Indigo Eclipse IDE sürümüdür. Eclipse için Azure eklentisi üzerinde Helios artık resmi olarak test edilir.

### <a name="july-3-2013"></a>3 Temmuz 2013
Azure eklentisi Eclipse - Temmuz 2013 Preview sürümünü yayımladı. Mayıs 2013'ün önizleme olduğundan bu güncelleştirme yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **Yeni bir depolama hesabı oluşturma yeteneği.** A **yeni** düğmesi eklenmiştir **depolama hesabı Ekle** iletişim. Bu, Azure Yönetim Portalı'na oturum açmaya gerek kalmadan Eclipse eklentisi depolama hesabında oluşturmanıza olanak sağlar. (Zaten bu özelliği kullanmak için bir Azure aboneliğiniz olmalıdır.) Yeni bir depolama hesabı oluşturma hakkında daha fazla bilgi için bkz: [yeni bir depolama hesabı oluşturmak için].
* **Yeni &quot;(otomatik)&quot; JDK ve sunucunun otomatik dağıtım ve önbelleğe alma için kullanılan depolama hesabı için seçeneği.** Kullanırken **otomatik olarak karşıya yükleme** JDK için seçeneği ve uygulama sunucusu, artık belirtebilirsiniz **(otomatik)** JDK karşıya yüklenirken kullanmak URL ve depolama hesabı ve uygulama sunucusu veya Azure önbelleğe almayı kullanırken. Ardından, bu özellikler otomatik olarak aynı depolama hesabı seçin, tek olarak kullanacak **Azure Yayımla** iletişim. [Bir Hello World uygulamasının Azure için Eclipse'te oluşturma] öğretici, yeni kullanmak üzere güncelleştirilmiştir **(otomatik)** seçeneği.
* **Azure hizmet uç noktalarınızı ayarlayabilme.** Azure platformu uygulamanız için dağıtılan ve genel Azure platformu tarafından yönetilen olup olmadığını, Çin ya da özel bir 21Vianet tarafından Azure işletilen belirlemek hizmet uç noktaları belirtin. Daha fazla bilgi için bkz: [Azure hizmet uç noktaları].
* **Büyük dağıtımlar yerel depolama kaynağı belirtebilirsiniz.** Dağıtımınız varsayılan approot klasöründe yer çok büyük, durumunda, artık yerel depolama kaynağı, JDK dağıtım hedefi olarak belirtebilirsiniz ve uygulama sunucusu. Daha fazla bilgi için bkz: [dağıtma büyük dağıtımlar].
* **A6 ve A7 Azure sanal makine boyutları için destek.** Bir bulut hizmeti artık, yüksek bellek A6 ve A7 sanal makine boyutlarını da dağıtabilirsiniz. Bu boyutları hakkında daha fazla bilgi için bkz: [sanal makine ve bulut hizmeti boyutları Azure].
* **Java kitaplığı için Azure kitaplıkları için paketi için bir güncelleştirme.** Bu sürümüne 0.4.4 bağlı [Microsoft Azure istemci API].

### <a name="may-1-2013"></a>1 Mayıs 2013
Eclipse için-Azure eklentisi 2013 Preview sürümünü yayımladı. Bu, bir önkoşul ve eklenti yüklediğinizde otomatik olarak yüklenecek Azure SDK 2.0 sürümü ile birlikte gelen önemli bir güncelleştirmedir. Şubat 2013 Önizleme olduğundan bu sürümde yeni özellikleri, hata düzeltmeleri ve bazı geri bildirim temelli kullanılabilirlik geliştirmeleri içerir:

* **JDK ve uygulama sunucusu ve Azure depolama biriminden dağıtım otomatik olarak karşıya yükleme.** Otomatik olarak seçilen JDK ve uygulama sunucusu, gerekli olduğunda, belirtilen Azure depolama hesabı için karşıya yükleme ve buradan kullanıcı karşıya yüklemeyi daha sonra el ile sahip veya bir dağıtım paketinde katıştırmak yerine bu bileşenlerini dağıtır yeni bir seçeneği. Bu sık istenen özellik başlayanlar için özellikle JDK ve sunucu bileşenleri dağıtma kolaylığını önemli ölçüde artırabilir. Bu seçenekleri kullanan bir kılavuz için bkz: [Bir Hello World uygulamasının Azure için Eclipse'te oluşturma].
* **Depolama hesabı izleme ve başvuru depolama hesapları daha fazla kolayca (aracılığıyla bir açılır liste denetimi) yeteneği Merkezi.** Bu JDK ve sunucu bileşeni dağıtımı ve önbelleğe alma gibi depolama kullanan birden çok özellikleri için geçerlidir. Daha fazla bilgi için bkz: [Azure depolama hesabı listesi].
* **Bulut Sihirbazı'na Yayımla Basitleştirilmiş uzaktan erişim kurulumu.** Tüm yapmanız gereken uzaktan erişimi etkinleştirmek veya devre dışı uzaktan erişim tutmak için boş bırakın, bir kullanıcı adı ve parola türü budur.
* **Java kitaplığı için Azure kitaplıkları için paketi için bir güncelleştirme.** Bu sürümüne 0.4.2 bağlı [Microsoft Azure istemci API].
* **Windows Server 2012 Yapışkan oturumları desteği.** Daha önce her ikisi de işletim sistemi hedefleri destek oturum benzeşimi bulut artık Yapışkan oturumlar yalnızca Windows Server 2008 R2'de, çalışmıştır.
* **Paket yükleme performans geliştirmeleri.** Zaman bile JDK ve uygulama sunucusu dağıtım paketinde katıştırılmış, dağıtım işlemi karşıya yükleme bölümünü yaklaşık iki kez önceki sürümlere kıyasla hızlı olabilir.

### <a name="february-8-2013"></a>8 Şubat 2013
Azure eklentisi Eclipse - Şubat 2013 Preview sürümünü yayımladı. Kasım 2012 Önizleme olduğundan, hata düzeltmeleri, geri bildirim temelli kullanılabilirlik geliştirmeleri ve bazı yeni özellikler içeren küçük bir güncelleştirme değil:

* JDKs, uygulama sunucuları dağıtmak için destek ve isteğe bağlı bileşenlerle genel veya özel Azure blob yerine bunları dağıtım paketinde buluta dağıtırken de dahil olmak üzere depolama yüklemeleri.
* Hangi kullanıcı tanımlı bir role bileşenlerinin işlenme, ek sırasını değiştirme yeteneğini **Yukarı Taşı** ve **Aşağı Taşı** içinde düğmeleri **bileşenleri** bölümünü **Azure rol özellikleri**.
* Bir güncelleştirme **Java için Azure kitaplıkları için paketi** 0.4.0 sürümüne Kitaplığı [Microsoft Azure istemci API].

### <a name="november-5-2012"></a>5 Kasım 2012
Eclipse için - Kasım 2012 Azure eklentisi Önizleme yayımladı. Bu çok sayıda yeni özellik, yanı sıra ek hata düzeltmeleri ve geri bildirim temelli kullanılabilirlik geliştirmeleri Eylül 2012 Önizleme beri içeren önemli bir güncelleştirme.

* Microsoft Windows Server 2012 bulut işletim sistemi olarak desteği.
* Azure birlikte bulunan önbelleğe alma desteği memcached istemciler için destek.
* Azure AMQP tabanlı Mesajlaşma faydalanarak için Apache Qpid JMS istemci kitaplıkları ekleme.
* Geliştirilmiş bir **yeni proje** sihirbazında, yeni bir sayfa sonunda kullanıcıların hızlı bir şekilde kendi proje birkaç ortak anahtar özelliklerini etkinleştirmek olanak sağlar: Yapışkan oturumları, önbelleğe alma ve uzaktan hata ayıklama.
* Sunucu örnekleri arasındaki bağlantı noktası bağlama çakışmaları önlemek için işlem öykünücüsü'nde çalıştırırken 1 rol örneklerinin Otomatik azaltma.

### <a name="september-28-2012"></a>28 Eylül 2012
Eclipse için - Eylül 2012'de Azure eklentisi Önizleme yayımladı. Bu hizmet güncelleştirmesi Ağustos 2012 Önizleme olduğundan, var olan özellikleri bazı geri bildirim temelli kullanılabilirlik geliştirmeleri yanı sıra ek hata düzeltmeleri içerir:

* Microsoft Windows 8 ve Microsoft Windows Server önceden eklentisi bu işletim sisteminde düzgün çalışmasını engelleyen sorunlarını çözme 2012 geliştirme işletim sistemi olarak desteği.
* Uç nokta bağlantı noktası aralıklarının belirtilmesi için geliştirilmiş destek.
* Boşluk içeren dosya yolları ilgili hata düzeltmeleri.
* Rol bağlam menüsü geliştirmeler daha hızlı erişim için role özgü yapılandırma ayarları.
* Küçük düzeltmeler de **buluta yayımlama** Sihirbazı ve ek hata düzeltmeleri sayısı.

### <a name="august-28-2012"></a>28 Ağustos 2012
Eclipse için - Ağustos 2012 Azure eklentisi Önizleme yayımladı. Temmuz 2012 Önizleme olduğundan, var olan özellikleri için birkaç geri bildirim temelli kullanılabilirlik geliştirmeleri yanı sıra bu hizmet güncelleştirmesi ek hata düzeltmeleri içerir:

* Azure erişim denetimi Hizmetleri filtre iletişim kutusu içinde:
  * **İmzalama sertifikasının katıştırmak için seçeneği** bulut dağıtımı basitleştirmek için uygulamanızın WAR dosyası.
  * **Kendinden imzalı bir sertifika oluşturmak için seçeneği** UI ACS içinde filtre. Azure erişim denetimi Hizmetleri filtre hakkında ek bilgi için bkz: [kimlik doğrulaması Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile nasıl].
* Azure dağıtım projesi sihirbazında (rolün sunucu yapılandırması özellik sayfası için de geçerlidir):
  * **Otomatik bulma JDK konumunun** bilgisayarınızda (hangi isterseniz kılabilirsiniz).
  * **Sunucu türü otomatik olarak algılanmasını** uygulama sunucusu yükleme dizini belirlediğinizde.

### <a name="july-15-2012"></a>15 Temmuz 2012
Eclipse için - Temmuz 2012 Azure eklentisi bulundu ve/veya sonra Haziran 2012 sürüm kullanıcılar tarafından bildirilen yüksek bir öncelik hataların sayısını adresleri, Önizleme yayımladı. Bu yalnızca bir hizmet güncelleştirmesi, yeni özellik yer alır.

### <a name="june-7-2012"></a>7 Haziran 2012
Azure eklentisi Eclipse - Haziran 2012 CTP'yi yayımladı. Yeni özellikleri şunlardır:

* **Yeni Azure dağıtım projesi Sihirbazı:** , JDK seçmenize olanak tanır Java uygulama sunucusu ve Java uygulamaları doğrudan geliştirilmiş Sihirbaz kullanıcı Arabirimi. Aralarından seçim yapabileceğiniz Giden kutusu sunucu yapılandırmaları listesinde Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6 ve 7 JBoss (tek başına) içerir. Ayrıca, sunucu yapılandırmaları listesi özelleştirebilirsiniz. Bu UI geliştirme alternatiftir sürükleyerek ve sıkıştırılmış dosyaları bırakarak ve başlatma komut dosyaları üzerinden kopyalama için önceden olduğu ana yaklaşım. Bu yöntem hala düzgün çalışır, ancak büyük olasılıkla daha Gelişmiş senaryolar için kullanılır.
* **Sunucu yapılandırması rol özellik sayfası:** JDKs, Java uygulama sunucularını ve projesi oluşturduktan sonra dağıtımınız ile ilişkili uygulamaları kolayca geçiş yapmanızı sağlar. Daha fazla bilgi için bkz: [sunucu yapılandırma özellikleri].
* **&quot;Buluta yayımlama&quot; Sihirbazı:** projenizi Azure için karşıya yükleme paketi, vb. Azure yönetim portalına oturum açma daha önce el ile ağır-kimlik bilgileri getiriliyor, kaldırma otomatikleştirme doğrudan Eclipse, dağıtım için kolay bir yol sağlar. Doğrudan projenizi Azure'a dağıtmak nasıl bir örnek için bkz: [Bir Hello World uygulamasının Azure için Eclipse'te oluşturma].
* **Azure araç çubuğu:** bir Azure araç aşağıdaki özellikleri çağırma düğmelerini içeren Eclipse'te yayımlamıştır:
  * ![][ic710879]**Azure öykünücüsünde çalıştırın**: projenizi öykünücüsünde çalışır.
  * ![][ic710880]**Azure öykünücüsünü sıfırlayın**: öykünücü sıfırlar.
  * ![][ic710881]**Azure için bulut paketi yapı**: paketiniz dağıtım için derler.
  * ![][ic710876]**Yeni Azure dağıtım projesi**: yeni bir Azure dağıtım projesi oluşturur.
  * ![][ic710882]**Azure bulut Yayımla**: projenizi Azure'da yayımlar.
  * ![][ic710883]**Yayımdan**: dağıtımınızı siler.
  * Bu Azure araç çubuğu düğmeleri çoğunu kullanılan [Bir Hello World uygulamasının Azure için Eclipse'te oluşturma].
* **Java için Azure kitaplıkları:** artık kullanılabilir Java Kitaplığı'nda Eclipse için Azure kitaplıkları için tek bir paket parçası olarak eklentisi yükleme eşlik eden ve tüm gerekli bağımlılıkları da içeren. Kitaplığına bir başvuru Java projenize eklemeniz yeterlidir ve ayrı olarak indirmek olması gerekmez. Daha fazla bilgi için bkz: [Azure araç setini Eclipse için yükleme].
* **Eklenti yükleme sırasında kullanılabilir SQL Server için Microsoft JDBC sürücüsü 4.0:** yeni eklenti yüklemesi sırasında SQL Server için Microsoft JDBC sürücüsü en yeni sürümünü yüklenebilir.
* **Azure erişim denetimi hizmeti filtresi eklentisini yükleme sırasında kullanılabilir:** araç setini Eclipse kitaplıkta olarak eklenen yeni bu bileşen, Google, Live.com ve Yahoo! gibi çeşitli kimlik sağlayıcısı kullanarak Azure erişim denetimi Hizmeti'nden (ACS) kimlik doğrulamasını sorunsuz bir şekilde yararlanmak Java web uygulamanızı sağlar. Kimlik doğrulaması mantığı kendiniz yazmak, yalnızca birkaç seçeneklerini yapılandırmak ve ACS kullanarak oturum açmasını etkinleştirme ağır lifting yapmak filtre izin gerekmez. Yalnızca, kullanıcılar kendi kimliğine göre kaynakları Request nesnesi içinde filtre uygulamanıza döndürülen erişmenizi sağlayan kod yazmaya odaklanabilirsiniz. ACS filtresini kullanarak, bir öğretici için bkz: [kimlik doğrulaması Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile nasıl].
* **Azure SDK 1.7 önkoşul otomatik algılanmasını:** yeni bir Azure dağıtım projesi oluşturduğunuzda, zaten yüklü değilse Azure SDK 1.7 otomatik olarak yüklenir.
* **Uç noktalar örneği:** verir doğrudan bağlantı noktası bitiş noktası erişimi yük ile iletişim için dengeli rol örnekleri. Örnek uç noktalarının, kullanıcı Arabirimi aracılığıyla kullanılabilen uç noktaları aracılığıyla eklenebilir [uç noktalarının özellikleri] sayfası. Bu uzaktan hata ayıklamayı etkinleştirme yardımcı olur ve belirli JMX tanılama işlem çoklu senaryolarla bulutta çalışan örneklerini-örnek dağıtımları. 
* **Kullanıcı Arabirimi bileşenlerini:** , proje bağımlılıklarını projeye bireysel Azure rolleri ve Java uygulama projeleri gibi dış diğer kaynaklar arasında ayarlamak İleri düzey kullanıcılar için kolaylaştırır; kendi dağıtım mantığı açıklamak kolaylaştırır. Daha fazla bilgi için bkz: [bileşenlerin özellikleri].
* **Projeleri önceki sürümlerinin otomatik yükseltme:** eklenti önceki bir sürümüyle oluşturulmuş Azure projesi sahip bir çalışma alanını açtığınızda, önceki sürümlerinde projeleri, yeni sürümle uyumlu olmadığı için eski projeleri Eclipse'te kapatıldı olarak gösterilir. Bu eski projelerden biri açmaya çalışırsanız, bir Yükseltme Sihirbazı başlar. İle yükseltme, yeni bir proje onaylıyorsanız **_Upgraded** adına eklenen, oluşturulacak ve yeni sürümle çalışmak için otomatik olarak güncelleştirilir. Yeni Proje gerektiği gibi yeniden adlandırabilirsiniz. Parçası olarak yükseltme, özgün projenizi değiştirilmeyecek (ve kapalı kalır).

### <a name="december-10-2011"></a>10 Aralık 2011
Azure eklentisi Eclipse - aralık 2011 CTP'yi yayımladı. Yeni özellikleri şunlardır:

* **Oturum benzeşimi (&quot;Yapışkan oturumları&quot;) desteği:** kümelenmiş Java uygulamalarını yalnızca tek bir onay kutusu ile durum bilgisi olan, etkinleştirme yardımcı olur. Daha fazla bilgi için bkz: [oturum benzeşimi].
* **Başlangıç kod örnekleri önceden yapılan:** , yalnızca kopyalayıp projenizin örnekleri dizininden, başlangıç komut dosyanıza yapıştırın en popüler Java sunucuları için (Tomcat, Jetty, JBoss, GlassFish).
* **Öykünücü başlatma çıkış gerçek zamanlı:** şimdi tüm adımları yürütülmesini bir adanmış konsol penceresinde, başlangıç komut dosyasından Azure tarafından yürütülen gibi ilerleme ve hataları komut dosyanıza gösteren izleyebilir.
* **Otomatik, hafif java.exe izleme:** , zorlayacak bir rol geri dönüşüm java.exe çalıştıran, dağıtımınızı otomatik olarak dahil basit, önceden yapılmış bir komut dosyası kullanarak durduğunda.
* **Uzak Java uygulaması yapılandırma kullanıcı Arabirimi hata ayıklama:** kolayca adım adım ve gerçek zamanlı Java kodunda hata ayıklama öykünücü veya Azure bulut çalışan Java uygulamanıza erişmek kullanılan Eclipse'nın uzaktan hata ayıklayıcı etkinleştirmenize olanak sağlar. Daha fazla bilgi için bkz: [Azure uygulamalarında hata ayıklama Eclipse].
* **Yerel depolama kaynak yapılandırma kullanıcı Arabirimi:** böylece artık yerel kaynakları XML doğrudan işleyerek yapılandırmak zorunda. Bu özellik, doğrudan başlangıç betikten başvurabilir bir ortam değişkeni aracılığıyla dağıtıldıktan sonra yerel kaynak etkili dosya yoluna erişmek sağlar. Daha fazla bilgi için bkz: [yerel depolama özellikleri].
* **Ortam değişkeni yapılandırma kullanıcı Arabirimi:** böylece el ile yapılandırmasını XML düzenleme aracılığıyla ortam değişkenlerini ayarlama zorunda. Daha fazla bilgi için bkz: [ortam değişkenlerinin özellikleri].
* **SQL Azure JDBC sürücüsü:** eklentisi SQL Azure karşı daha kolay programlama etkinleştirme sorunsuz bir şekilde tümleştirilmiş bir Eclipse kitaplığı olarak yüklenen. 
* **Rol yapılandırmasını UI hızlı bağlam menüsü erişimi**: yalnızca Rol klasöre sağ tıklayın ve **özellikleri**.
* **Özel Azure projesi ve rol klasör simgeleri:** daha iyi görünürlük ve çalışma ve proje içinde daha kolay gezinme için.

## <a name="see-also"></a>Ayrıca Bkz.
Java IDE’leri için Azure Araç Setleri hakkında daha fazla bilgi için aşağıdaki bağlantılara bakın:

* [Eclipse için Azure Araç Seti]
  * *Azure araç setini Eclipse (Bu makalede) için Yenilikler*
  * [Azure araç setini Eclipse için yükleme]
  * [Eclipse Azure'da Hello World Web uygulaması oluşturun]
  * [Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]
* [Intellij için Azure Araç Seti]
  * [IntelliJ için Azure Araç Seti Yenilikleri]
  * [IntelliJ için Azure Araç Setini Yükleme]
  * [IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]
  * [Intellij Azure'da Hello World Web uygulaması oluşturun]

Azure’u Java ile kullanma hakkında daha fazla bilgi edinmek için bkz. [Azure Java Geliştirici Merkezi].

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World Web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Azure araç setini Eclipse için yükleme]: ./azure-toolkit-for-eclipse-installation.md
[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md
[Eclipse için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[IntelliJ için Azure Araç Setinde Oturum Açma Yönergeleri]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[IntelliJ için Azure Araç Seti Yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[içinde Azure oturum yönergeler Eclipse için Azure Araç Seti için]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Docker Eclipse için Azure Araç Seti kullanarak bir kapsayıcı olarak bir Web uygulaması yayımlama]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[depolama Eclipse için Azure Explorer'ı kullanarak hesapları yönetme]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[yönetme Azure Gezgini Eclipse için kullanarak sanal makineleri]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Geliştirici Merkezi]: http://go.microsoft.com/fwlink/?LinkID=699547

[Azul sistemleri web sayfası için Zulu dili OpenJDK]: http://go.microsoft.com/fwlink/?LinkId=402457
[Azure hizmet uç noktaları]: http://go.microsoft.com/fwlink/?LinkID=699526
[Azure depolama hesabı listesi]: http://go.microsoft.com/fwlink/?LinkID=699528
[bileşenlerin özellikleri]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[Bir Hello World uygulamasının Azure için Eclipse'te oluşturma]: http://go.microsoft.com/fwlink/?LinkID=699533
[Azure uygulamalarında hata ayıklama Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[dağıtma büyük dağıtımlar]: http://go.microsoft.com/fwlink/?LinkID=699536
[uç noktalarının özellikleri]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[ortam değişkenlerinin özellikleri]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[Eclipse için Hdınsight araçları eklentisi]: ./hdinsight/hdinsight-apache-spark-eclipse-tool-plugin.md
[kimlik doğrulaması Web kullanıcıları Azure erişim denetimi hizmeti kullanılarak Eclipse ile nasıl]: http://go.microsoft.com/fwlink/?LinkID=264703
[kullanım SSL boşaltma nasıl]: http://go.microsoft.com/fwlink/?LinkID=699545
[Eclipse için Azure Araç Setini Yükleme]: http://go.microsoft.com/fwlink/?LinkId=699546
[yerel depolama özellikleri]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[Microsoft Azure istemci API]: http://go.microsoft.com/fwlink/?LinkId=280397
[sunucu yapılandırma özellikleri]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[oturum benzeşimi]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL boşaltma]: http://go.microsoft.com/fwlink/?LinkID=699549
[yeni bir depolama hesabı oluşturmak için]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[sanal makine ve bulut hizmeti boyutları Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: ./media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: ./media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: ./media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: ./media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: ./media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: ./media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
