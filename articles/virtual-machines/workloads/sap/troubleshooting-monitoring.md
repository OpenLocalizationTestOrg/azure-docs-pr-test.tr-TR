---
title: "aaaTroubleshooting ve izleme, SAP HANA azure'da (büyük örnekler) | Microsoft Docs"
description: "Sorun giderme ve Azure (büyük örnekler) üzerinde SAP HANA izleyin."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Nasıl tootroubleshoot ve İzleyici SAP HANA (büyük örnekler) Azure ile ilgili


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>SAP HANA (büyük örnekler) azure'da izleme

SAP HANA Azure (büyük örnekler) üzerinde diğer bir Iaas dağıtımından farklı — hello uygulamasıdır yapmak ve bunları nasıl bu kaynakları aşağıdaki hello ve hangi işletim sistemi hello toomonitor gerekir:

- CPU
- Bellek
- Ağ bant genişliği
- Disk alanı

Azure sanal makinelerle yukarıda adı hello kaynak sınıfları yeterli olup veya olup bunlar tükendiğinde toofigure gerektiği. İşte daha fazla ayrıntı her hello farklı sınıflar:

**CPU kaynak tüketimi:** SAP HANA karşı belirli iş yükü için tanımlanan hello orandır zorlanan toomake emin yeterli CPU kaynakları kullanılabilir toowork bellekte depolanır hello veriler aracılığıyla olmalıdır. Bununla birlikte, burada HANA toomissing dizinler veya benzer sorunlar nedeniyle sorgular yürütme CPU çok tüketen durumlar olabilir. Başka bir deyişle, CPU kaynak tüketimini hello belirli HANA Hizmetleri tarafından tüketilen CPU kaynaklarının yanı sıra hello HANA büyük örneği birim izlemeniz gerekir.

**Bellek tüketimi:** önemli toomonitor gelen HANA içinde yanı sıra HANA dışında hello birimi üzerinde değil. Merhaba verileri sipariş toostay SAP yönergelerini boyutlandırma gerekli hello içinde bellek tahsis HANA nasıl tüketme HANA içinde izleyin. Merhaba büyük örnek düzeyi toomake ek yüklü olmayan-HANA yazılım değil çok fazla bellek kullanmasına ve bu nedenle için bellek HANA ile rekabet emin üzerinde toomonitor bellek tüketimi da isteyebilirsiniz.

**Ağ bant genişliği:** hello Azure sanal ağ geçidi sınırlı bant genişliği hello Azure VNet taşıma verilerin, yardımcı olması için tüm tarafından alınan toomonitor hello verileri Azure VM'ler hello Azure toohello sınırları ne kadar yakın olduğunuz çıkışı bir VNet toofigure içinde hello ağ geçidi SKU'su seçtiğiniz. Merhaba HANA büyük örneği biriminde algılama toomonitor gelen ve giden ağ trafiğini de ve zaman içinde işlenir hello birimleri tookeep izini yapar.

**Disk alanı:** Disk alanı tüketimini genellikle zamanla artar. Bunun pek çok nedeni vardır, ancak tüm çoğu: veri birimi artırır, işlem günlüğü yedeklemeleri, izleme dosyaları depolamak ve depolama anlık görüntüleri gerçekleştirme yürütülmesini. Bu nedenle, önemli toomonitor disk alanı kullanımı ve hello HANA büyük örneği birimiyle ilişkili hello disk alanını yönetme.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>İzleme ve HANA taraftan sorun giderme

Sipariş tooeffectively sorunları ilgili tooSAP (büyük örnekler) azure'da HANA çözümlemek, bir sorunun hello kök nedeni aşağı yararlı toonarrow. SAP belgelerine toohelp büyük miktarda yayımlanan.

İlgili sık sorulan sorular ilgili tooSAP HANA performans SAP notları aşağıdaki hello bulunabilir:

- [SAP Not #2222200 – SSS: SAP HANA ağ](https://launchpad.support.sap.com/#/notes/2222200)
- [SAP Not #2100040 – SSS: SAP HANA CPU](https://launchpad.support.sap.com/#/notes/0002100040)
- [SAP Not #199997 – SSS: SAP HANA bellek](https://launchpad.support.sap.com/#/notes/2177064)
- [SAP Not #200000 – SSS: SAP HANA performansı iyileştirme](https://launchpad.support.sap.com/#/notes/2000000)
- [SAP Not #199930 – SSS: SAP HANA g/ç çözümleme](https://launchpad.support.sap.com/#/notes/1999930)
- [SAP Not #2177064 – SSS: SAP HANA hizmeti yeniden başlatın ve kilitleniyor](https://launchpad.support.sap.com/#/notes/2177064)

**SAP HANA uyarıları**

İlk adım olarak, hello geçerli SAP HANA uyarı günlüklerini denetleyin. SAP HANA Studio'da çok gidin**Yönetim Konsolu: Uyarı: göster: tüm uyarıları**. Bu sekme hello en az ve en fazla eşikleri dışında kalan belirli değerleri (boş fiziksel bellek, CPU kullanımı, vb.) için tüm SAP HANA uyarıları gösterir. Varsayılan olarak, denetimleri 15 dakikada bir otomatik olarak yenilenir.

![SAP HANA Studio'da tooAdministration konsol gidin: Uyarı: göster: tüm uyarılar](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Tooimproper eşik ayarı nedeniyle tetiklenen bir uyarı için bir çözüm tooreset toohello varsayılan veya daha uygun bir eşik değere değerdir.

![Sıfırlama toohello varsayılan değeri ya da daha uygun bir eşik değer](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Uyarıları aşağıdaki hello CPU kaynağı sorunlarını gösterebilir:

- Ana bilgisayar CPU kullanımı (uyarı 5)
- En son noktası işlemi (uyarı 28)
- Kayıt noktası süresi (uyarı 54)

SAP HANA veritabanından hello aşağıdakilerden birini üzerinde yüksek CPU tüketimi karşılaşabilirsiniz:

- Uyarı 5 (ana bilgisayar CPU kullanımı) için geçerli veya son CPU kullanımını tetiklenir
- Merhaba CPU kullanımı hello genel bakış ekranda görüntülenen

![CPU kullanımı hello genel bakış ekranda görüntülenen](./media/troubleshooting-monitoring/image3-cpu-usage.png)

Merhaba yük grafiği yüksek CPU tüketimi veya yüksek tüketim hello geçmiş gösterebilir:

![Hello yük grafik yüksek CPU tüketimi veya yüksek tüketim hello geçmiş gösterebilir.](./media/troubleshooting-monitoring/image4-load-graph.png)

Toohigh CPU kullanımı tetiklenen uyarı, ancak bunlarla sınırlı olmamak de dahil olmak üzere çeşitli nedenlerden kaynaklanabilir: belirli işlemleri, veri yükleme, asılı SQL deyimlerini ve hatalı sorgu performansı (örneğin, ile HANA üzerinde BW uzun süre çalışan işlerin yürütme küpleri).

Toohello başvuran [SAP HANA sorunlarını giderme: CPU ilgili neden olur ve çözümleri](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) ayrıntılı sorun giderme adımları için site.

**İşletim Sistemi**

SAP HANA Linux'ta toomake saydam büyük sayfalar devre dışı bırakıldığından emin için en önemli hello birini denetimlerinin bkz [SAP Not #2131662 – saydam büyük sayfalar (THP) SAP HANA sunucularda](https://launchpad.support.sap.com/#/notes/2131662).

- Saydam büyük sayfalar Linux komutu aşağıdaki hello etkin olup olmadığını denetleyebilirsiniz: **kat /sys/kernel/mm/transparent\_hugepage ve etkin**
- Varsa _her zaman_ içine aşağıdaki şekilde köşeli parantez içine hello saydam büyük sayfalar etkinleştirildiğini gösterir: [her zaman] madvise hiçbir zaman if _hiçbir zaman_ arasına köşeli aşağıdaki şekilde, onu o hello saydam anlamına gelir Büyük sayfalar devre dışı bırakılır: her zaman madvise [hiçbir zaman]

Linux komutu aşağıdaki hello hiçbir şey döndürmelidir: **rpm - qa | grep ulimit.** Görünürse _ulimit_ olan yüklü, bunu hemen kaldırın.

**Bellek**

Bu hello tutar gözlemleyebilirsiniz SAP HANA hello tarafından ayrılan belleğin veritabanı beklenenden daha yüksektir. Uyarıları aşağıdaki hello yüksek bellek kullanımı ile ilgili sorunları belirtin:

- Konak fiziksel bellek kullanımı (uyarı 1)
- Ad sunucusu (uyarı 12) bellek kullanımı
- Sütun deposu tabloları (uyarı 40) toplam bellek kullanımı
- Bellek kullanımı (uyarı 43) hizmetleri hakkında
- Sütun deposu tabloların (uyarı 45) ana depolama bellek kullanımı
- Çalışma zamanı döküm dosyalarını (uyarı 46)

Toohello başvuran [SAP HANA sorunlarını giderme: bellek sorunları](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) ayrıntılı sorun giderme adımları için site.

**Ağ**

Çok başvuran[SAP Not #2081065 – SAP HANA ağ sorunlarını giderme](https://launchpad.support.sap.com/#/notes/2081065) ve sorun giderme adımları bu SAP notta hello ağ gerçekleştirin.

1. İstemci ve sunucu arasındaki gidiş dönüş süresi çözümleniyor.
  A. Merhaba SQL betiği çalıştırma [ _HANA\_ağ\_istemcileri_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Düğümler arası iletişim analiz edin.
  A. SQL betiği çalıştırma [ _HANA\_ağ\_Hizmetleri_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Linux komutu çalıştırmak **ifconfig** (Merhaba çıkış paket kayıpları yaşanan gösterir).
4. Linux komutu çalıştırmak **tcpdump**.

Ayrıca, hello açık kaynak kullanın [IPERF](https://iperf.fr/) Aracı (veya benzeri) toomeasure gerçek uygulama ağ performansı.

Toohello başvuran [SAP HANA sorunlarını giderme: ağ performansı ve bağlantı sorunları](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) ayrıntılı sorun giderme adımları için site.

**Depolama**

Bir son kullanıcı açısından bir uygulama (veya bir bütün olarak hello sistemi) ağır şekilde çalışan, yanıt vermiyor veya g/ç performansı ile ilgili sorun varsa toohang bile görünebilir. Merhaba, **birimleri** sekmesini SAP HANA Studio'da hello bağlı birimler ve hangi birimlerin her hizmeti tarafından kullanılan görebilirsiniz.

![SAP HANA Studio'da Hello birimler sekmesinde birimleri ve hangi birimlerin her hizmeti tarafından kullanılan hello bağlı görebilirsiniz](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

Merhaba alt bölümünde ayrıntılarını görebilirsiniz hello ekranın bağlı birimlerin birimler, dosyalar ve g/ç istatistikleri gibi hello.

![Birimler, dosyalar ve g/ç istatistikleri gibi ayrıntılarını görebilirsiniz hello ekranın hello alt bölümünde bağlı birimlerin hello](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Toohello başvuran [SAP HANA sorunlarını giderme: g/ç ana ilgili nedenler ve çözümler](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) ve [SAP HANA sorunlarını giderme: Disk ana ilgili nedenler ve çözümler](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) ayrıntılı sorun giderme adımları için site.

**Tanılama araçları**

SAP HANA sistem durumu denetimi HANA aracılığıyla gerçekleştirmek\_yapılandırma\_Minichecks. Bu aracı zaten uyarıları SAP HANA Studio'da olarak oluşturuldu kritik olabilecek teknik sorunlar döndürür.

Çok başvuran[SAP Not #1969700 – SAP HANA için SQL deyimi koleksiyonu](https://launchpad.support.sap.com/#/notes/1969700) ve hello SQL Statements.zip dosya ekli toothat Not indirin. Bu .zip dosyasını hello yerel sabit sürücüde depolayın.

SAP HANA Studio'da hello **sistem bilgileri** sekmesinde, hello sağ **adı** sütun ve seçin **içeri aktarma SQL deyimlerini**.

![SAP HANA Studio'da hello sistem bilgisi sekmesindeki hello Ad sütununda sağ tıklatın ve içeri aktarma SQL deyimlerini seçin](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Select hello SQL Statements.zip dosyası yerel olarak depolanan ve hello karşılık gelen SQL deyimlerini sahip bir klasör için içeri aktarılacak. Bu noktada, bu SQL deyimleri ile birçok farklı tanılama denetimleri çalıştırılabilir hello.

Örneğin, tootest SAP HANA sistem çoğaltma bant genişliği gereksinimlerini sağ hello **bant genişliği** deyiminin altında **çoğaltma: bant genişliği** seçip **açık** SQL konsolunda.

Merhaba tam SQL deyimini değişti ve daha sonra çalıştırılabilir izin giriş parametreleri (değişikliği bölümüne) toobe açar.

![Merhaba tam SQL deyimini değişti ve daha sonra çalıştırılabilir izin giriş parametreleri (değişikliği bölümüne) toobe açar](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Başka bir örnek hello deyimleri altında üzerinde sağ **çoğaltma: genel bakış**. Seçin **yürütme** hello bağlam menüsünden:

![Başka bir çoğaltma altında hello deyimleri üzerinde sağ örnektir: genel bakış. Execute hello bağlam menüsünden seçin](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Bu sorun giderme konusunda yardımcı olacak bilgileri sonuçlanır:

![Bu sorun giderme konusunda yardımcı olacak bilgiler sonuçlanır](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Aynı HANA için hello\_yapılandırma\_Minichecks ve onay herhangi _X_ hello işaretleri _C_ (kritik) sütun.

Örnek çıktı:

**HANA\_yapılandırma\_MiniChecks\_Rev102.01 + 1** genel SAP HANA denetimleri için.

![HANA\_yapılandırma\_MiniChecks\_Rev102.01 + 1 genel SAP HANA denetimleri için](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Hizmetleri\_genel bakış** ne SAP HANA Hizmetleri şu anda çalışan bir genel bakış için.

![HANA\_Hizmetleri\_ne SAP HANA Hizmetleri şu anda çalışan bir genel bakış için genel bakış](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Hizmetleri\_istatistikleri** SAP HANA için hizmet bilgileri (CPU, bellek, vs.).

![HANA\_Hizmetleri\_istatistikleri SAP HANA için hizmet bilgileri ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_yapılandırma\_genel bakış\_Rev110 +** hello SAP HANA örneği hakkında genel bilgi için.

![HANA\_yapılandırma\_genel bakış\_Rev110 + hello SAP HANA örneği hakkında genel bilgi için](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_yapılandırma\_parametreleri\_Rev70 +** toocheck SAP HANA parametreleri.

![HANA\_yapılandırma\_parametreleri\_Rev70 + toocheck SAP HANA parametreleri](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

