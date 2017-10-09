---
title: "aaaWhat olan trafik Yöneticisi | Microsoft Docs"
description: "Bu makalede, trafik Yöneticisi nedir ve uygulamanız için hello sağ trafik yönlendirme seçim olup anlamanıza yardımcı olur"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 8e63ed11cdcdc03ae9cd28f88f0d1f9dc2cd44ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-traffic-manager"></a>Traffic Manager'a Genel Bakış

Microsoft Azure trafik Yöneticisi toocontrol hello hizmet uç noktaları için kullanıcı trafiğinin dağıtımını farklı veri merkezlerinde sağlar. Trafik Yöneticisi tarafından desteklenen hizmet uç noktaları ve bulut hizmetlerini Azure VM'ler, Web uygulamaları içerir. Traffic Manager’ı harici, Azure dışı uç noktalar için de kullanabilirsiniz.

Trafik Yöneticisi bir trafik yönlendirme yöntemini ve hello uç noktaları hello durumunu göre hello etki alanı adı sistemi (DNS) toodirect istemci istekleri toohello en uygun uç nokta kullanır. Trafik Yöneticisi sağlayan bir dizi [trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md) ve [uç nokta izleme seçenekleri](traffic-manager-monitoring.md) toosuit farklı uygulama gereksinimlerini ve otomatik yük devretme modeller. Trafik, tüm bir Azure bölgesi hello başarısızlığını dahil esnek toofailure yöneticisidir.

## <a name="traffic-manager-benefits"></a>Trafik Yöneticisi avantajları

Trafik Yöneticisi yardımcı olabilir:

* **Kritik uygulamaların kullanılabilirliğini artırın**

    Trafik Yöneticisi uç noktalarınızı izleme ve bir uç nokta azaldığında otomatik yük devretme sağlayarak, uygulamalar için yüksek kullanılabilirlik sağlar.

* **Yüksek performanslı uygulamalar için yanıt hızını artırmak**

    Azure veri merkezlerinde Merhaba Dünya bulunan toorun bulut Hizmetleri veya Web siteleri sağlar. Trafik Yöneticisi ile Merhaba en düşük ağ gecikmesini hello istemcisi için trafiği toohello endpoint yönlendirerek uygulama yanıt hızını artırır.

* **Kapalı kalma süresi olmadan hizmet bakımı gerçekleştirme**

    Uygulamalarınızın kapalı kalma süresi olmadan planlı bakım işlemleri gerçekleştirebilir. Merhaba bakım işlemi devam ederken traffic Manager trafik tooalternative uç noktaları yönlendirir.

* **Şirket içi ve bulut tabanlı uygulamalar birleştirin**

    Trafik Yöneticisi dış destekler, karma ile kullanılan toobe etkinleştirme Azure olmayan uç noktaları Bulut ve "veri bloğu buluta," "geçirmek buluta," Merhaba dahil olmak üzere dağıtımları ve "Yük devretme-bulut" senaryoları şirket.

* **Büyük ve karmaşık dağıtımlar için trafiği dağıtmak**

    Kullanarak [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md), trafik yönlendirme yöntemleri birleşik toocreate karmaşık olabilir ve esnek kurallara toosupport hello daha büyük ve daha karmaşık dağıtımları gerekir.

## <a name="how-traffic-manager-works"></a>Traffic Manager nasıl çalışır?

Azure trafik Yöneticisi, uygulama uç noktalar arasında trafiği toocontrol hello dağıtımını sağlar. Bir uç nokta içinde veya Azure dışında barındırılan tüm Internet'e hizmetidir.

Trafik Yöneticisi iki temel fayda sağlar:

1. Birkaç tooone göre trafiğinin dağıtımını [trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md)
2. [Sürekli uç noktası durumunu izleme](traffic-manager-monitoring.md) ve uç noktaları başarısız olduğunda otomatik yük devretme

Bir istemci tooconnect tooa hizmeti çalıştığında, ilk hello DNS adı hello hizmet tooan IP adresi çözmeniz gerekir. Merhaba istemci ardından toothat IP adresi tooaccess hello hizmeti bağlanır.

**Merhaba en önemli nokta toounderstand trafik Yöneticisi hello DNS düzeyinde çalışmasıdır.**  Trafik Yöneticisi kullandığı DNS toodirect istemcileri toospecific hizmet uç noktaları hello trafik yönlendirme yönteminin hello kurallara göre. İstemcileri seçili toohello endpoint bağlama **doğrudan**. Trafik Yöneticisi, bir proxy veya ağ geçidi değil. Trafik Yöneticisi hello istemciyle hello hizmeti arasında geçen hello trafiğine görmez.

### <a name="traffic-manager-example"></a>Trafik Yöneticisi örneği

Contoso Corp yeni bir iş ortağı portalı geliştirmiştir. Merhaba bu portalı https://partners.contoso.com/login.aspx URL'sidir. Merhaba uygulaması Azure üç bölgelerde barındırılır. tooimprove kullanılabilirlik ve genel performansını en üst düzeye çıkarmak, trafik Yöneticisi toodistribute istemci trafiğini toohello yakın kullanılabilir uç nokta kullanın.

tooachieve bu yapılandırma, bunlar hello aşağıdaki adımları tamamlayın:

1. Kendi hizmet üç örneği dağıtın. Merhaba DNS adları bu dağıtımlar, 'contoso-us.cloudapp .net', 'contoso-eu.cloudapp .net' ve 'contoso-asia.cloudapp .net' dır.
2. 'Contoso.trafficmanager.net' adlı bir trafik Yöneticisi profili oluşturun ve hello üç uç noktalar arasında toouse hello 'Performans' trafik yönlendirme yöntemini yapılandırma.
* Kendi gösterim etki alanı adı, 'partners.contoso.com', toopoint too'contoso.trafficmanager.net yapılandırın ', bir DNS CNAME kaydı kullanılarak.

![Trafik Yöneticisi DNS yapılandırması][1]

> [!NOTE]
> Bir gösterim etki alanını Azure Traffic Manager ile kullanırken, CNAME toopoint gösterim etki alanı adı tooyour trafik yöneticisi etki alanı adı kullanmanız gerekir. DNS standartlarında bir etki alanının toocreate bir CNAME hello 'tepesindeki' konumunda'ı (veya kök) izin vermiyor. Bu nedenle, '('naked' etki alanı olarak da adlandırılır) contoso.com' için bir CNAME oluşturamazsınız. Yalnızca altında "contoso.com", "www.contoso.com" gibi bir etki alanı için bir CNAME oluşturabilirsiniz. Bu sınırlamaya geçici toowork, "contoso.com" tooan alternatif adı 'www.contoso.com' gibi basit bir HTTP yeniden yönlendirme toodirect istekleri kullanmanızı öneririz.

### <a name="how-clients-connect-using-traffic-manager"></a>Trafik Yöneticisi'ni kullanarak istemcilerin nasıl bağlanacağını

Bir istemci hello sayfa https://partners.contoso.com/login.aspx istediğinde hello önceki örnekten devam etmeden, hello istemci adımları tooresolve hello DNS adından hello gerçekleştirir ve bağlantı kurun:

![Trafik Yöneticisi'ni kullanarak bağlantı kurma][2]

1. Merhaba istemcisi bir DNS sorgusu yapılandırılmış tooits yinelemeli DNS hizmeti tooresolve hello adı 'partners.contoso.com' gönderir. 'Yerel DNS' hizmet olarak da adlandırılan bir yinelemeli DNS hizmeti DNS etki alanı doğrudan barındırmıyor. Bunun yerine, hello istemci hello iş off-loads hello arayarak çeşitli yetkili DNS hizmetleri hello gerekli Internet tooresolve arasında bir DNS adı.
2. tooresolve hello DNS adı hello yinelemeli DNS hizmeti hello "contoso.com" etki alanı için hello ad sunucularını bulur. Ardından bu ad sunucuları toorequest hello 'partners.contoso.com' DNS kaydı iletişim kurar. Merhaba contoso.com DNS sunucuları toocontoso.trafficmanager.net işaret hello CNAME kaydı döndürür.
3. Ardından, hello yinelemeli DNS hizmeti hello Azure trafik Yöneticisi hizmeti tarafından sağlanan hello 'trafficmanager.net' etki hello ad sunucularını bulur. Daha sonra DNS sunucuları hello 'contoso.trafficmanager.net' DNS kaydı toothose için bir istek gönderir.
4. Merhaba trafik Yöneticisi ad sunucuları hello isteği alır. Bunlar dayalı bir uç nokta seçin:

    - Her bitiş noktasıyla yapılandırılmış hello durumunu (devre dışı uç noktaları alınmadı)
    - Hello her bitiş hello trafik Yöneticisi sistem tarafından belirlenen geçerli durumunu denetler. Daha fazla bilgi için bkz: [trafik Yöneticisi uç noktası izleme](traffic-manager-monitoring.md).
    - trafik yönlendirme yöntemini seçmiş hello. Daha fazla bilgi için bkz: [Traffic Manager yönlendirme yöntemleri](traffic-manager-routing-methods.md).

5. Seçilen hello uç nokta başka bir DNS CNAME kaydı döndürülür. Bu durumda, contoso us.cloudapp.net döndürülen bize varsayalım.
6. Ardından, hello yinelemeli DNS hizmeti hello 'cloudapp.net' etki alanı için hello ad sunucularını bulur. Bu ad sunucuları toorequest hello 'contoso-us.cloudapp .net' kişiler DNS kaydı. Merhaba ABD tabanlı hizmet uç noktası Hello IP adresini içeren bir 'A' DNS kaydı döndürülür.
7. Merhaba yinelemeli DNS hizmeti hello sonuçları birleştirir ve tek bir DNS yanıtı toohello istemci döndürür.
8. Merhaba istemci hello DNS sonuçlarını alır ve verilen IP adresi toohello bağlanır. Merhaba istemci toohello Uygulama Hizmeti uç noktası değil trafik Yöneticisi ile doğrudan bağlanır. Bir HTTPS uç noktası olduğundan, hello istemci hello gerekli SSL/TLS anlaşması gerçekleştirir ve hello için bir HTTP GET isteği yapar ' / login.aspx' sayfa.

Merhaba yinelemeli DNS hizmeti aldığı hello DNS yanıtlarını önbelleğe kaydeder. Merhaba DNS Çözümleyicisi hello istemci cihazda ayrıca hello sonuç önbelleğe alır. Önbelleğe alma sonraki DNS sorguları toobe daha hızlı veri hello önbellekten yerine tarafından diğer ad sunucularını sorgulama yanıtlanmasını sağlar. Merhaba hello önbellek süresini hello 'time-to-live' (TTL) özelliği her bir DNS kaydı tarafından belirlenir. Kısa değerler daha hızlı önbellek süre sonu ve bu nedenle daha fazla gidiş dönüş toohello trafik Yöneticisi ad sunucuları sonuçlanır. Uzun değerleri, başarısız bir uç nokta çıktığınızda uzun toodirect trafik alabilir anlamına gelir. Trafik Yöneticisi verir tooconfigure hello TTL trafik Yöneticisi DNS yanıtları toobe 0 saniye olarak en düşük kullanılıyor ve 2.147.483.647 saniye olarak yüksek (Merhaba üst aralık uyumlu [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt)), toochoose hello değeri etkinleştirme Bu, uygulamanızın hello gereksinimlerini en iyi dengeler.

## <a name="pricing"></a>Fiyatlandırma

Fiyatlandırma bilgileri için bkz: [trafik Yöneticisi fiyatlandırma](https://azure.microsoft.com/pricing/details/traffic-manager/).

## <a name="faq"></a>SSS

Trafik Yöneticisi ile ilgili sık sorulan sorular için bkz: [trafik Yöneticisi ile ilgili SSS](traffic-manager-FAQs.md)

## <a name="next-steps"></a>Sonraki adımlar

Trafik Yöneticisi hakkında daha fazla bilgi [uç nokta izleme ve otomatik yük devretme](traffic-manager-monitoring.md).

Trafik Yöneticisi hakkında daha fazla bilgi [trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md).

Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure.

<!--Image references-->
[1]: ./media/traffic-manager-how-traffic-manager-works/dns-configuration.png
[2]: ./media/traffic-manager-how-traffic-manager-works/flow.png

