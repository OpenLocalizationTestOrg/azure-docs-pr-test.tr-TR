---
title: "aaaAsymmetric yönlendirme | Microsoft Docs"
description: "Bu makalede, bir müşteri, birden çok bağlantılar tooa hedef olan bir ağda asimetrik yönlendirme ile yüz hello sorunlar açıklanmaktadır."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Birden çok ağ yoluyla Asimetrik yönlendirme
Bu makalede, ağ kaynağı ile hedef arasında birden çok yol varsa iletme ve döndürme ağ trafiğinin nasıl farklı rotalar izleyebileceği açıklanmaktadır.

Buna ait önemli toounderstand iki kavramları toounderstand asimetrik yönlendirme. Birden çok ağ yolunu hello etkisini biridir. Merhaba başka bir güvenlik duvarı gibi cihazların durumunu kalmasını nasıl ' dir. Bu tür cihazlara durum bilgisi olan cihazlar denir. Bu iki faktör bileşimini hello durum bilgisi olan aygıt trafiği hello aygıtla kendisini kaynaklanan algılamadı için hangi ağ trafiği durum bilgisi olan bir cihaz tarafından bırakılan senaryolar oluşturur.

## <a name="multiple-network-paths"></a>Birden çok ağ yolu
Internet üzerinden kendi Internet servis sağlayıcısı hello Internet gelen tüm trafiği tooand geçen bir bağlantı toohello hello yalnızca aynı yol bir kurumsal ağ içinde olduğunda. Genellikle, şirketler birden çok bağlantı hatları yedekli yollar, tooimprove ağ açık kalma süresi satın alın. Bu durumda, bir bağlantı ve hello toohello Internet hello ağının dışından trafiğinin giden mümkündür Döndür trafiği farklı bir bağlantı aracılığıyla gider. Bu duruma yaygın olarak asimetrik yönlendirme adı verilir. Yönlendirme asimetrik, geriye doğru ağ trafiğini hello özgün akıştan farklı bir yol alır.

![Birden çok yola sahip ağ](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Öncelikle hello Internet üzerinde oluşur ancak asimetrik de Yönlendirme birden fazla yol tooother birleşimlerini geçerlidir. Bu, örneğin, tooan Internet yolu ve toohello Git özel bir yol geçerlidir aynı hedef ve toohello Git toomultiple özel yollar aynı hedef.

Merhaba şekilde, kaynak toodestination boyunca her yönlendirici hello en iyi yolu tooreach bir hedef hesaplar. Merhaba yönlendiricinin belirleme olası en iyi yolu, iki ana etmenlere dayanır:

* Dış ağlar arası yönlendirme, Sınır Ağ Geçidi Protokolü (BGP) olarak bilinen bir yönlendirme protokolüne bağlıdır. BGP reklamları Komşuları alır ve adımları toodetermine hello en iyi yolu hedeflenen toohello hedef bir dizi aracılığıyla çalıştırır. Bu, kendi yönlendirme tablosunda hello en iyi yolunu depolar.
* bir rota ile ilişkili bir alt ağ maskesi uzunluğunu Hello yönlendirme yollarının etkiler. Yönlendirici alırsa, aynı IP adresi için birden çok tanıtım hello ancak daha belirli bir yolu olarak kabul olduğundan farklı bir alt ağ maskeleriyle hello yönlendirici daha uzun bir alt ağ maskesi hello reklamla tercih eder..

## <a name="stateful-devices"></a>Durum bilgisi olan cihazlar
Yönlendirici yönlendirme amaçları için bir paketin hello IP üstbilgisi arayın. Bazı aygıtlar hello paketin içinde bile daha derin arayın. Bu cihazlar, genellikle Katman4 (İletim Denetimi Protokolü veya TCP ya da Kullanıcı Veri Birimi Protokolü veya UDP) ve hatta Katman7 (Uygulama Katmanı) üst bilgilerine bakar. Bu tür cihazlar, güvenlik cihazları ya da bant genişliği iyileştirme cihazlarıdır. 

Durum bilgisi olan cihazlar için tipik bir örnek güvenlik duvarıdır. Bir güvenlik duvarı sağlar veya paket toopass protokolü, TCP/UDP bağlantı noktası ve URL üstbilgileri gibi çeşitli alanlara göre arabirimlerinden aracılığıyla reddeder. Bu düzeyde bir paket incelemesi işleme yükünü hello aygıtta ağır koyar. tooimprove performans hello Güvenlik Duvarı'nı bir akış hello ilk paket olup olmadığını denetler. Merhaba paket tooproceed izin veriyorsa, kendi durumu tablosunda hello akış bilgisini tutar. Tüm sonraki paketlere ilgili toothis akışı hello ilk belirleme göre verilir. Var olan bir akış parçası olan bir paket hello güvenlik duvarında gelen. Merhaba güvenlik duvarı ilgili önceki durum bilgisi varsa, hello güvenlik duvarı hello paket bırakır.

## <a name="asymmetric-routing-with-expressroute"></a>ExpressRoute ile asimetrik yönlendirme
Azure ExpressRoute aracılığıyla tooMicrosoft bağlandığınızda, ağ değişikliklerinizi bu ister:

* Birden çok bağlantılar tooMicrosoft sahip. Bir bağlantı, varolan bir Internet bağlantısı ve ExpressRoute aracılığıyla hello diğer şeklindedir. Bazı trafiği tooMicrosoft hello Internet Git ancak ExpressRoute aracılığıyla veya tersi geri dönün.
* ExpressRoute üzerinden daha belirli IP adresleri alırsınız. Bu nedenle, ExpressRoute aracılığıyla sunulan hizmetler için ağ tooMicrosoft gelen trafik için yönlendiriciler ExpressRoute her zaman tercih.

Bu iki değişiklikten sahip bir ağda toounderstand hello etkisi şimdi bazı senaryoları göz önünde bulundurun. Örneğin, yalnızca bir bağlantı hattı toohello Internet sahip ve hello Internet üzerinden tüm Microsoft hizmetlerini kullanma. Merhaba, ağ tooMicrosoft ve geri ilişkilerinden geçen trafiğinden hello aynı Internet bağlantısı ve hello güvenlik duvarı üzerinden geçer. Merhaba ilk paket görür ve hello akış hello durumu tabloda bulunduğundan paketlere izin verilmesi dönüş gibi hello güvenlik duvarı kayıtları akış hello.

![ExpressRoute ile asimetrik yönlendirme](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

Ardından, ExpressRoute hizmetini açıyorsunuz ve Microsoft tarafından ExpressRoute üzerinden sunulan hizmetleri tüketiyorsunuz. Tüm diğer Microsoft hizmetlerinden hello Internet kullanılır. Bağlı tooExpressRoute olduğundan, sınırında ayrı bir Güvenlik Duvarı'nı dağıtın. Microsoft, belirli hizmetleri için ExpressRoute daha belirli önekleri tooyour ağ tanıtır. Yönlendirme altyapınızı ExpressRoute bu önekler için tercih edilen yol hello olarak seçer. Size, ortak IP adresleri tooMicrosoft ExpressRoute reklam değil, Microsoft ortak IP adreslerinizi hello Internet üzerinden iletişim kurar. ExpressRoute ağ tooMicrosoft iletme trafiğinden kullanır ve Microsoft ters trafiğinden hello Internet kullanır. Merhaba hello sınır güvenlik duvarında hello durumu tabloda bulamazsa bir akışı için bir yanıt paketi gördüğünde hello dönüş trafiği bırakır.

Aynı ağ adresi çevirisi (NAT) havuz hello Internet ve ExpressRoute için toouse hello seçerseniz, ağınızdaki özel IP adresleri hello istemcilerle benzer sorunlar görürsünüz. Bu hizmetler için IP adreslerini ExpressRoute aracılığıyla bildirilmeyeceğini olduğundan Windows Update gibi hizmetler için istekleri hello Internet gidin. Ancak, hello dönüş trafik ExpressRoute aracılığıyla gelir. Microsoft IP adresi ile alırsa, aynı alt ağ maskesi hello Internet gelen ve ExpressRoute hello hello Internet ExpressRoute tercih eder. Bir güvenlik duvarı veya ağ kenarı ve ExpressRoute karşılıklı başka bir durum bilgisi olan aygıt hello akışı hakkında önceki hiçbir bilgi varsa, toothat akış ait karşılama paketleri bırakır.

## <a name="asymmetric-routing-solutions"></a>Asimetrik yönlendirme çözümleri
Asimetrik yönlendirme iki ana seçeneğiniz toosolve hello sorunu var. Yönlendirme aracılığıyla biridir ve hello diğer kaynak tabanlı NAT (SNAT) kullanmaktır.

### <a name="routing"></a>Yönlendirme
Ortak IP adreslerinizi tanıtılan tooappropriate geniş alan ağı (WAN) bağlantıları olduğundan emin olun. Toouse hello Internet kimlik doğrulama trafiği ve ExpressRoute için posta trafiği için isterseniz, örneğin, Active Directory Federasyon Hizmetleri (AD FS) genel IP adreslerinizi ExpressRoute bildirilmeyecek. Benzer şekilde, mutlaka değil tooexpose şirket içi bir yönlendirici hello AD FS sunucu tooIP adreslerini ExpressRoute alır. ExpressRoute hello tercih edilen yol için kimlik doğrulama trafiğini tooMicrosoft yaparsınız ExpressRoute alınan yollar daha özeldir. Bu durum asimetrik yönlendirmeye yol açar.

Kimlik doğrulaması için toouse ExpressRoute istiyorsanız NAT olmadan ExpressRoute üzerinden AD FS genel IP adresleri reklam emin olun Bu şekilde, Microsoft'tan kaynaklanan ve tooan giden trafik ExpressRoute üzerinde AD FS sunucu gider şirket içi. Merhaba Internet hello tercih edilen yol olduğundan müşteri tooMicrosoft dönüş trafiğinden ExpressRoute kullanır.

### <a name="source-based-nat"></a>Kaynak tabanlı NAT
Asimetrik yönlendirme sorunlarını çözmenin bir başka yolu da SNAT kullanmaktır. Toouse hello Internet bu tür iletişim için düşündüğünüz çünkü Örneğin, bir şirket içi Basit Posta Aktarım Protokolü (SMTP) sunucusunun hello ortak IP adresi ExpressRoute tanıtılan değil. Microsoft ile kaynaklanan ve tooyour girer bir istek hello Internet SMTP sunucusu arasında çapraz geçiş şirket içi. Gelen istek tooan iç IP adresi, SNAT hello. Merhaba SMTP sunucusu ters trafik (kullanacağınız için NAT) toohello sınır güvenlik duvarı yerine ExpressRoute aracılığıyla gider. Merhaba dönüş trafiği geri hello Internet gider.

![Kaynak tabanlı NAT ağ yapılandırması](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Asimetrik yönlendirmenin algılanması
İzleme yolu hello en iyi şekilde toomake ağ trafiğinizi beklenen hello yolu yaptıran emin olur. Trafik, şirket içi SMTP sunucusu tooMicrosoft tootake hello Internet yolunun bekliyorsanız, hello izleme yolu hello SMTP sunucusu tooOffice 365 beklenmektedir. Merhaba sonuç trafik ağınıza hello Internet doğru ve ExpressRoute doğru değil gerçekten ayrılıyor doğrular.

