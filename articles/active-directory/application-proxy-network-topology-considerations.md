---
title: "Azure Active Directory Uygulama proxy'si kullanırken aaaNetwork topolojisi hakkında önemli noktalar | Microsoft Docs"
description: "Azure AD uygulama proxy'si kullanırken ağ topolojisi konuları kapsar."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Azure Active Directory Uygulama proxy'si kullanırken ağ topolojisi hakkında önemli noktalar

Bu makalede, Azure Active Directory (Azure AD) uygulama proxy'si yayımlama ve uygulamalarınızı uzaktan erişim için kullanırken ağ topolojisi konuları açıklanmaktadır.

## <a name="traffic-flow"></a>Trafik akışı

Azure AD uygulama proxy'si aracılığıyla uygulama yayımlandığında, üç bağlantıları üzerinden trafiği hello kullanıcılar toohello uygulamalardan akar:

1. Azure üzerinde toohello Azure AD uygulama proxy'si Hizmeti uç noktası ortak Hello kullanıcı bağlanır
2. Merhaba uygulama proxy'si hizmeti toohello uygulama ara sunucusu Bağlayıcısı bağlanır
3. Merhaba uygulama ara sunucusu Bağlayıcısı toohello hedef uygulama bağlanır

![Kullanıcı tootarget uygulamadan gelen trafik akışını gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Kiracı konumu ve uygulama proxy'si hizmeti

Azure AD kiracısı için kaydolduğunuzda, kiracınızın hello bölge belirttiğiniz hello ülkeye göre belirlenir. Uygulama proxy'si etkinleştirdiğinizde hello uygulama proxy'si hizmeti örnek kiracınız için seçilen veya hello aynı oluşturulan Azure AD kiracısı veya hello en yakın bölgeyi tooit bölgeye.

Örneğin, Azure AD kiracınıza ait bölge hello Avrupa Birliği (AB) ise, tüm uygulama proxy'si bağlayıcılar hello AB Azure veri merkezlerinde de hizmet örneği kullanın. Kullanıcılara erişim yayımlanan uygulamaları, kendi trafiği hello uygulama proxy'si hizmet örnekleri bu konumda geçer.

## <a name="considerations-for-reducing-latency"></a>Gecikme dikkat edilmesi gereken noktalar

Tüm proxy çözümleri gecikme ağ bağlantınızı tanıtır. Hangi proxy ya da VPN çözümü uzaktan erişim çözümünüzü seçtiğiniz olsun, bu her zaman şirket ağınıza hello bağlantı tooinside etkinleştirme sunucular kümesi içerir.

Kuruluşlar, genellikle kendi çevre ağında sunucu uç noktalarını içerir. Merhaba bağlayıcılar Kurumsal ağınızda bulunması sırasında Azure AD uygulama proxy'si ile ancak, trafik hello bulutta hello proxy hizmeti aracılığıyla akar. Çevre ağı gereklidir.

Merhaba sonraki bölümlerde daha gecikme süresini azaltmak ek öneriler toohelp içerir. 

### <a name="connector-placement"></a>Bağlayıcı yerleştirme

Uygulama proxy'si, Kiracı konumunuza göre örnekleri hello konumunu seçer. Ancak, burada, vermiş tooinstall hello bağlayıcı güç toodefine hello gecikme süresi, ağ trafiğinizi özelliklerini hello toodecide alın.

Uygulama proxy'si hizmeti Hello ayarlarken, aşağıdaki soruları hello isteyin:

* Merhaba uygulama nerede?
* Bulunan hello uygulama erişen kullanıcıların çoğunun nerede?
* Merhaba uygulama proxy'si örneği nerede?
* Azure ExpressRoute veya benzer bir VPN gibi kurma, bir adanmış ağ bağlantısı tooAzure veri merkezleri zaten var mı?

hem Azure hem de uygulamalarınızı (Adım 2 ve 3'te hello trafik akışı diyagramı) toocommunicate Hello bağlayıcının, bu nedenle bu iki bağlantı hello bağlayıcı etkiler hello gecikme süresi yerleşimini hello. Merhaba bağlayıcı Hello yerleşimini değerlendirirken, aşağıdaki noktaları göz önünde hello tutun:

* Çoklu oturum açma için toouse Kerberos Kısıtlı temsilci (KCD) istiyorsanız hello Bağlayıcısı görüş tooa datacenter olması gerekir. Ayrıca, hello bağlayıcı sunucusunun toobe etki alanına katılmış olmalıdır.  
* Şüpheli olduğunda, hello bağlayıcı daha yakından toohello uygulamasını yükleyin.

### <a name="general-approach-toominimize-latency"></a>Genel yaklaşım toominimize gecikme süresi

Her ağ bağlantısı iyileştirerek hello gecikme hello uçtan uca trafiğini en aza indirebilirsiniz. Her bağlantı tarafından iyileştirilebilir:

* Merhaba iki hello atlama ucunun arasındaki Hello uzaklığı azaltır.
* Merhaba doğru ağ tootraverse seçme. Örneğin, hello yerine bir özel ağ çapraz geçiş yapan genel Internet toodedicated bağlantılar daha hızlı olabilir.

Azure ile şirket ağınız arasında ayrılmış bir VPN ya da ExpressRoute bağlantı varsa, toouse isteyebilirsiniz.

## <a name="focus-your-optimization-strategy"></a>En iyi duruma getirme stratejinizi odaklanın

Kullanıcıların hello uygulama proxy'si hizmeti arasında toocontrol hello bağlantı yapabileceğiniz az yoktur. Kullanıcılar, uygulamalarınızı ev ağı, bir kafeterya veya farklı bir ülkede erişebilir. Bunun yerine, uygulamalardan hello uygulama proxy'si hizmeti toohello uygulama proxy'si bağlayıcılar toohello hello bağlantıları iyileştirebilirsiniz. Ortamınızdaki desenler izleyen hello eklemeyi göz önünde bulundurun.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Desen 1: Put hello bağlayıcı Kapat toohello uygulaması

Merhaba müşteri ağında yer hello bağlayıcı Kapat toohello hedef uygulama. Hello bağlayıcı ve uygulama Kapat olduğundan 3. adım hello topografi diyagramda bu yapılandırma en aza indirir. 

Bağlayıcınızı görüş toohello etki alanı denetleyicisi gerekiyorsa, bu deseni avantajlıdır. Çoğu senaryo için iyi çalışır olduğundan müşterilerimizin çoğu bu deseni kullanır. Bu deseni da Desen 2 toooptimize trafiği hello hizmeti ile Merhaba bağlayıcı arasındaki ile birleştirilebilir.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Desen 2: Genel eşliği ile ExpressRoute yararlanın

ExpressRoute genel eşliği ile ayarlanan varsa, uygulama proxy'si ve hello Bağlayıcısı arasındaki trafik için hello daha hızlı ExpressRoute bağlantı kullanabilirsiniz. Merhaba, hala ağınızda Kapat toohello uygulama Bağlayıcıdır.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Desen 3: özel eşleme ile ExpressRoute yararlanın

Ayrılmış bir VPN veya şirket ağınız ve Azure arasında özel eşleme ile ExpressRoute ayarlanan varsa, başka bir seçeneğiniz vardır. Bu yapılandırmada, Azure sanal ağında hello genellikle hello şirket ağının bir uzantısı olarak kabul edilir. Bu nedenle hello bağlayıcı hello Azure veri merkezi yükleyin ve hala hello bağlayıcı uygulama bağlantının hello düşük gecikme gereksinimleri karşılamak.

Ayrılmış bir bağlantı üzerinden trafik akışı için gecikme tehlikeye değil. Merhaba bağlayıcı bir Azure veri merkezi Kapat tooyour Azure AD Kiracı konumu yüklendiği için geliştirilmiş uygulama proxy'si Hizmeti Bağlayıcısı gecikme süresi de alırsınız.

![Azure veri merkezi içinde yüklü bağlayıcı gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Diğer yaklaşımlar

Bu makalenin Hello odak bağlayıcı yerleştirme olsa da, hello uygulama tooget iyi gecikme özellikleri hello yerleşimini de değiştirebilirsiniz.

Giderek, kuruluşların kendi ağları barındırılan ortamlara taşıyor. Bu tooplace sağlar, ayrıca kendi Kurumsal ağın parçası olan ve hello etki alanı içinde devam barındırılan bir ortamda uygulamalarını. Bu durumda, hello önceki bölümlerde ele alınan hello desenleri uygulanan toohello yeni uygulama konumu olabilir. Bu seçenek düşünüyorsanız, bkz: [Azure AD etki alanı Hizmetleri](../active-directory-domain-services/active-directory-ds-overview.md).

Ayrıca, kullanma, bağlayıcılar düzenleme göz önünde bulundurun [bağlayıcı grupları](active-directory-application-proxy-connectors.md) farklı konumlarda ve ağları tootarget uygulamalar. 

## <a name="common-use-cases"></a>Genel kullanım örnekleri

Bu bölümde, birkaç yaygın senaryolar üzerinden yol. Bu hello Azure AD kiracısı varsayar (ve bu nedenle proxy hizmet uç noktası) hello Amerika Birleşik Devletleri (ABD) bulunur. Merhaba bunları ele alınan konuları kullanım Merhaba Dünya çevresinde tooother bölgeleri de geçerlidir.

Bu senaryolar için her bağlantının bir "durak" çağırın ve daha kolay tartışma için sayı:

- **1 atlama**: kullanıcı toohello uygulama proxy'si hizmeti
- **2 atlama**: uygulama proxy'si hizmeti toohello uygulama ara sunucusu Bağlayıcısı
- **3 atlama**: uygulama ara sunucusu Bağlayıcısı toohello hedef uygulama 

### <a name="use-case-1"></a>Kullanım örneği 1

**Senaryo:** hello uygulamadır hello kuruluş ağındaki BİZE, hello kullanıcılarla aynı bölgede. ExpressRoute ya da VPN hello Azure veri merkezi ve hello şirket ağı arasında mevcut.

**Öneri:** hello önceki bölümde açıklanan izleyin düzeni 1. Gerekirse, geliştirilmiş gecikme için ExpressRoute kullanmayı düşünün.

Basit bir desen budur. Atlama 3 hello bağlayıcı hello uygulama yakın koyarak iyileştirin. Merhaba bağlayıcı genellikle görüş toohello uygulama ve toohello datacenter tooperform KCD işlemleriyle yüklendiği için de doğal bir seçim budur.

![Kullanıcılar, proxy, bağlayıcı ve uygulama tüm hello BİZE olduğunu gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Kullanım örneği 2

**Senaryo:** hello uygulamadır hello kuruluş ağındaki BİZE, genel olarak dağılmış kullanıcılarla. ExpressRoute ya da VPN hello Azure veri merkezi ve hello şirket ağı arasında mevcut.

**Öneri:** hello önceki bölümde açıklanan izleyin düzeni 1. 

Yeniden hello ortak Düzen hello bağlayıcı hello uygulama yakın nereye toooptimize atlama 3, yöneliktir. Atlama 3 tüm içinde aynı hello ise genellikle pahalı olmayan bölge. Ancak, kullanıcıların Merhaba dünya genelinde hello uygulama proxy'si hello ABD örneğinde erişmesi gereken çünkü atlama 1 hello kullanıcı olduğu bağlı olarak, daha pahalı olabilir. Bu, herhangi bir proxy çözümü genel dağılmış kullanıcılar ilgili benzer özelliklere sahip dikkate değerdir.

![Kullanıcılar genel yayılır, ancak hello proxy, bağlayıcı ve uygulama hello BİZE olan gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Kullanım örneği 3

**Senaryo:** hello uygulamadır hello kuruluş ağındaki BİZE. Ortak eşleme ile ExpressRoute, Azure ve hello şirket ağı arasında mevcut.

**Öneri:** desenleri 1 ve 2 ' nin hello önceki bölümde açıklanan izleyin.

İlk olarak, olası toohello uygulama olarak kapatmak gibi hello bağlayıcı yerleştirin. Ardından, hello sistem atlama 2 ExpressRoute otomatik olarak kullanır. 

Ortak eşleme Hello ExpressRoute bağlantı kullanıyorsa, hello trafiği hello proxy hello bağlayıcı arasındaki bu bağlantı üzerinden akar. Atlama 2 gecikme optimize etti.

![ExpressRoute hello proxy ve bağlayıcı arasında gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Kullanım örneği 4

**Senaryo:** hello uygulamadır hello kuruluş ağındaki BİZE. Özel eşleme ile ExpressRoute, Azure ve hello şirket ağı arasında mevcut.

**Öneri:** hello önceki bölümde açıklanan izleyin düzeni 3 '.

Merhaba bağlayıcı hello ExpressRoute özel eşleme aracılığıyla şirket ağına bağlı toohello Azure veri merkezi yerleştirin. 

Merhaba bağlayıcı hello Azure veri merkezi yerleştirilebilir. Merhaba bağlayıcı hala görüş toohello uygulama ve hello datacenter hello özel ağ üzerinden olduğundan, atlama 3 en iyi duruma getirilmiş kalır. Ayrıca, atlama 2 daha iyi duruma getirilmiştir.

![Merhaba bağlayıcı Azure veri merkezinde ve ExpressRoute hello Bağlayıcısı ve uygulama arasında gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Kullanım örneği 5

**Senaryo:** hello uygulamadır hello AB hello uygulama proxy'si örneği ve kullanıcıların hello çoğu kuruluşun ağındaki BİZE.

**Öneri:** yer hello bağlayıcı hello uygulama yakın. Uygulama proxy'si örneği hello toobe olur erişen ABD kullanıcı için aynı bölgede atlama 1 değil çok pahalı. Atlama 3 getirilmiştir. ExpressRoute toooptimize atlama 2 kullanmayı düşünün. 

![Merhaba ABD, hello bağlayıcı ve hello AB uygulamada bulunan kullanıcılar ve proxy gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

Ayrıca, bu durumda bir değişken kullanarak göz önünde bulundurun. Hello kuruluşunuzdaki kullanıcıların çoğunun hello BİZE olan, büyük olasılıkla ağınız toohello BİZE de genişleten demektir. Merhaba bağlayıcı hello ABD yerleştirin ve hello AB ayrılmış hello iç kurumsal ağ satırı toohello uygulamasını kullanın. Bu şekilde atlama 2 ve 3 en iyi duruma getirilir.

![Merhaba ABD, hello AB uygulamada bulunan kullanıcılar, proxy ve bağlayıcı gösteren diyagram](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Sonraki adımlar

- [Uygulama Ara sunucusunu etkinleştirme](active-directory-application-proxy-enable.md)
- [Çoklu oturum açmayı etkinleştirme](active-directory-application-proxy-sso-using-kcd.md)
- [Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md)
- [Uygulama Ara sunucusu ile ilgili sorunları giderme](active-directory-application-proxy-troubleshoot.md)
