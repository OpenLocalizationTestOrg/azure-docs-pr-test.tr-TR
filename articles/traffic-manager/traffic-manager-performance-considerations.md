---
title: "aaaPerformance konuları için Azure Traffic Manager | Microsoft Docs"
description: "Performans Traffic Manager üzerindeki anlamak ve nasıl trafik Yöneticisi'ni kullanırken Web sitenizin tootest performans"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Traffic Manager için performans konuları

Bu sayfayı trafik Yöneticisi'ni kullanarak performans konuları açıklanmaktadır. Senaryo aşağıdaki hello göz önünde bulundurun:

Siteniz hello WestUS örneklerini ve EastAsia bölgeler var. Merhaba örnekleri birini hello trafik Yöneticisi araştırma için hello sistem durumu denetimi başarısız oluyor. Uygulama, yönlendirilmiş toohello sağlıklı bölge trafiğidir. Bu yük devretme bekleniyordu ancak performans şimdi tooa uzak bölge seyahat hello trafik hello gecikmesine bağlı bir sorun olabilir.

## <a name="performance-considerations-for-traffic-manager"></a>Traffic Manager için performans konuları

Trafik Yöneticisi, Web sitenizde sahip olabileceği hello yalnızca performans hello ilk DNS araması etkisidir. Traffic Manager profilinizin hello adı için bir DNS istek ana hello trafficmanager.net bölge hello Microsoft DNS kök sunucusu tarafından işlenir. Trafik Yöneticisi doldurur ve düzenli olarak güncelleştirir, hello trafik Yöneticisi ilkesini ve hello yoklama sonuçları göre hello Microsoft'un DNS kök sunucuları. Bu nedenle bile hello ilk DNS araması sırasında DNS sorgularını tooTraffic Yöneticisi gönderilir.

Trafik Yöneticisi oluşur çeşitli bileşenleri: DNS sunucuları, bir API hizmeti, hello depolama katmanı ve izleme hizmeti bir uç nokta adı. Trafik Yöneticisi hizmet bileşenini başarısız olursa, trafik Yöneticisi profili ile ilişkilendirilmiş hello DNS adı üzerinde hiçbir etkisi yoktur. Merhaba Microsoft DNS sunucuları Hello kayıtlarında değişmeden kalır. Ancak, uç nokta izleme ve DNS güncelleştirme durum değil. Bu nedenle, birincil sitenizi azaldığında trafik Yöneticisi şu mümkün tooupdate DNS toopoint tooyour yük devretme sitesinde değil.

DNS ad çözümlemesi hızlıdır ve sonuçları önbelleğe alınır. ad çözümlemesi için DNS sunucuları hello istemcinin kullandığı hello hello ilk DNS araması Hello hızına bağlıdır. Genellikle, istemci DNS araması ~ 50 ms içinde tamamlayabilirsiniz. Merhaba hello arama sonuçlarını hello DNS için-yaşam süresi (TTL) hello süresince önbelleğe alınır. Merhaba varsayılan TTL trafik Yöneticisi için 300 saniyedir.

Trafiğin, trafik Yöneticisi ile geçmez. Merhaba DNS arama işlemi tamamlandıktan sonra hello istemci web sitenizi örneği için bir IP adresi vardır. Merhaba istemci doğrudan toothat adresi bağlanır ve trafik Yöneticisi ile iletmez. Merhaba seçtiğiniz trafik Yöneticisi ilkesini hello DNS performans üzerindeki etkisi yoktur. Ancak, bir performans yönlendirme yöntemi hello uygulama deneyimi olumsuz yönde etkileyebilir. Örneğin, Kuzey Amerika tooan örneği Asya'da barındırılan trafiğinden ilkeniz yönlendirir, hello ağ gecikmesi Bu oturumlar için bir performans sorunu olabilir.

## <a name="measuring-traffic-manager-performance"></a>Trafik Yöneticisi performansı ölçme

Toounderstand hello performans ve trafik Yöneticisi profili davranışını kullanabileceğiniz birçok Web siteleri vardır. Bu sitelere çoğunu ücretsiz ancak sınırlamaları olabilir. Bazı siteler Gelişmiş izleme ve raporlama için ücret sunar.

DNS gecikmeleri Hello araçları bu sitelerde ölçmek ve istemci konumları Merhaba Dünya için IP adreslerini görüntüleme hello çözülür. Bu araçların çoğu hello DNS sonuçları önbelleğe almaz. Bu nedenle, hello araçları hello tam DNS araması test her çalıştırıldığında gösterir. Kendi istemciden test ettiğinizde, yalnızca hello tam DNS arama performansı kez hello TTL süresi sırasında karşılaşırsınız.

## <a name="sample-tools-toomeasure-dns-performance"></a>Örnek araçları toomeasure DNS performansı

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS birçok performans araçları sunar. Merhaba DNS karşılaştırma aracı tooresolve DNS adınızı süreyi ve nasıl, tooother DNS hizmet sağlayıcıları karşılaştırır gösterebilir.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Merhaba basit araçları WebSitePulse biridir. Merhaba URL toosee DNS çözümleme süresi, ilk bayta kalan, son bayta kalan ve diğer performans istatistiklerini girin. Üç farklı bir test konumlardan seçebilirsiniz. Bu örnekte, hello ilk yürütme DNS araması 0.204 sn aldığını gösterir bakın.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Aynı trafik Yöneticisi uç noktası hello DNS araması sonuçları önbelleğe alınır, hello hello ikinci test için hello çünkü 0.002 sn alır.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA'ın uygulama Sentetik İzleyicisi](https://asm.ca.com/en/checkit.php)

    Önceden hello Watchmouse onay Web sitesi aracı olarak bilinen, bu site Göster, hello DNS çözümlemesi süresi birden çok coğrafi bölgelerden aynı anda. Merhaba URL toosee DNS çözümleme süresi, bağlantı süresi ve hız birkaç coğrafi konumlardan girin. Merhaba Dünya farklı konumlar için hangi barındırılan hizmet döndürülen bu test toosee kullanın.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Bu araç, bir web sayfasının her öğe için performans istatistikleri sağlar. başlangıç sayfasını analiz sekmesi hello DNS araması yapılmasını harcanan süre yüzdesini gösterir.

* [My DNS nedir?](http://www.whatsmydns.net/)

    Bu site 20 farklı konumlardan DNS araması yapar ve bir haritada hello sonuçları görüntüler.

* [Web arabirimi sorgulaması](http://www.digwebinterface.com)

    Bu site, daha ayrıntılı CNAME ve A kayıtları dahil olmak üzere DNS bilgi gösterir. Renklendir'i hello 'output' ve 'İstatistiği' seçenekleri altında denetleyin ve 'All' altında Nameservers seçin emin olun.

## <a name="next-steps"></a>Sonraki Adımlar

[Traffic Manager trafik yönlendirme yöntemleri hakkında](traffic-manager-routing-methods.md)

[Trafik Yöneticisi ayarlarınızı sınama](traffic-manager-testing-settings.md)

[Traffic Manager üzerindeki işlemler (REST API Başvurusu)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure Traffic Manager cmdlet'leri](http://go.microsoft.com/fwlink/p/?LinkId=400769)

