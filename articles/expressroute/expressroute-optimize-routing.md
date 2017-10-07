---
title: "ExpressRoute yönlendirmesini en iyi duruma getirme: Azure | Microsoft Docs"
description: "Bu sayfa nasıl birden fazla ExpressRoute olduğunda toooptimize yönlendirme, bağlantı hattına Ayrıntılar corp ağınız ve Microsoft arasında bağlantı sağlar."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>ExpressRoute Yönlendirmeyi En iyi Duruma Getirme
Birden çok ExpressRoute bağlantı hattına sahip birden fazla yol tooconnect tooMicrosoft vardır. Sonuç olarak, yetersiz yönlendirme olabilir - diğer bir deyişle, trafiğinizin daha uzun bir yol tooreach Microsoft, alabilir ve Microsoft tooyour ağ. Merhaba uzun hello ağ yolu, hello daha yüksek hello gecikme süresi. Gecikmenin uygulama performansı ve kullanıcı deneyimi üzerinde doğrudan etkisi vardır. Bu makalede, bu sorunu gösterir ve standart yönlendirme teknolojilerini kullanarak yönlendirme toooptimize nasıl hello açıklar.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Yetersiz müşteri tooMicrosoft yönlendirme
Bir kapatma hello yönlendirme sorun örneği tarafından bakalım. Merhaba ABD, biri, Los Angeles ve diğeri New York'ta içinde iki ofisiniz olduğunu düşünün. Ofisleriniz, kendi omurga ağınız veya hizmet sağlayıcınızın IP VPN’i olabilen bir Geniş Alan Ağı (WAN) üzerine bağlıdır. ABD Batı'daki biri diğeri ABD Doğu'daki hello WAN üzerinde de bağlanan, iki ExpressRoute bağlantı hatları var. Belli ki, iki yolları tooconnect toohello Microsoft ağına sahip. Şimdi, hem ABD Batı hem de ABD Doğu’da Azure dağıtımına (örneğin, Azure Uygulama Hizmeti) sahip olduğunuzu düşünün. Amacınız her office Access'in kullanıcılara en iyi deneyimler için Azure services yakındaki hello Hizmet yöneticiniz tanıtır tooconnect Los Angeles tooAzure ABD Batı'nda kullanıcılarınıza ve New York tooAzure ABD Doğu'nda kullanıcılarınıza olduğundan. Ne yazık ki, hello planı iyi hello Doğu Yakası kullanıcıları için kullanılabilir ancak hello Batı Yakası kullanıcıları üretir. Merhaba hello sorunun nedenini hello aşağıda verilmiştir. Her expressroute bağlantı hattı üzerinde şu hello öneki Azure ABD Doğu (23.100.0.0/16) hem Azure ABD Batı'daki (13.100.0.0/16) önekini hello tooyou tanıtır. Hangi önekin hangi bölgeden olduğunu bilmiyorsanız, mümkün tootreat olmayan, farklı. WAN ağınız hello öneklerini her ikisi de yakın tooUS Doğu ABD Batı'dan olan ve bu nedenle hem office kullanıcılar toohello expressroute bağlantı hattı ABD Doğu'rota düşünebilirsiniz. Merhaba sonunda, Los Angeles office hello birçok mutsuz kullanıcılar gerekir.

![ExpressRoute durum 1 sorunu - müşteri tooMicrosoft yönlendirme yetersiz](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Çözüm: BGP Toplulukları’nı kullanın
toooptimize her iki ofis kullanıcıları için yönlendirmeyi, hangi önekin Azure Batı ABD ve hangi Azure Doğu ABD olduğunu tooknow gerekir. Bu bilgileri [BGP Topluluğu değerlerini](expressroute-routing.md) kullanarak kodlarız. Benzersiz bir BGP topluluğu değeri tooeach Azure bölgesi, örneğin atanan Doğu ABD için "12076:51004", Batı ABD için "12076:51006". Artık hangi önekin hangi Azure bölgesinden olduğunu bildiğinize göre, tercih edilmesi gereken ExpressRoute bağlantı hattını yapılandırabilirsiniz. Merhaba BGP tooexchange yönlendirme bilgilerinin kullandığımız için BGP'nin yerel tercihini tooinfluence yönlendirme kullanabilirsiniz. Bizim örneğimizde, ABD Doğu'daki daha ABD Batı'daki daha yüksek bir yerel tercih değeri too13.100.0.0/16 ve benzer şekilde, ABD Doğu'daki ABD Batı'daki daha yüksek bir yerel tercih değeri too23.100.0.0/16 atayabilirsiniz. Bu yapılandırma her iki yolları tooMicrosoft kullanılabilir, New York'taki kullanıcılarınız ABD Doğu tooAzure ABD Doğu ExpressRoute hello kullanırken Los Angeles'taki kullanıcılarınızın hello BİZE Batı tooconnect tooAzure ABD Batı'daki expressroute bağlantı hattına olur, emin olun . Her iki tarafta da yönlendirme en iyi duruma getirilmiştir. 

![ExpressRoute Vaka 1 çözümü: BGP Toplulukları’nı kullanın](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Yerel tercihini kullanarak aynı tekniği Merhaba, müşteri tooAzure sanal ağ'dan uygulanan toorouting olabilir. Biz Azure tooyour ağdan tanıtılan BGP topluluk değeri toohello ön eklere yok. Sanal ağ dağıtımınız, Office'in Kapat toowhich olduğu bildiğiniz olduğundan, ancak yönlendiricileriniz uygun şekilde yapılandırabilirsiniz tooprefer bir ExpressRoute bağlantı hattı tooanother.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Yetersiz Microsoft toocustomer yönlendirme
İşte başka bir örnek burada Microsoft bağlantılarının ağınıza daha uzun bir yol tooreach alın. Bu durumda, [karma bir ortamda](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx) şirket içi Exchange sunucularını ve Exchange Online kullanın. Ofisleriniz bağlı tooa WAN ' dir. Şirket içi sunucularınızı hem de, ofisler tooMicrosoft hello iki ExpressRoute bağlantı hatları aracılığıyla hello öneklerini tanıtır. Exchange Online posta kutusu geçişi gibi durumlarda bağlantıları toohello şirket içi sunucular başlatır. Ne yazık ki, hello bağlantı tooyour Los Angeles office hello tüm kıtadan geçmeden geri toohello Batı Yakası geçiş önce yönlendirilmiş toohello ABD Doğu'daki expressroute bağlantı hattı olur. Merhaba hello sorununun benzer toohello nedeni ilk. Herhangi bir ipucu hello Microsoft ağı hangi müşteri önekinin Kapat tooUS Doğu ve hangisinin tooUS Batı kapatmak bildiremez. Toopick hello yanlış yolu tooyour Los Angeles ofisinde olur.

![2 - Microsoft toocustomer yönlendirme yetersiz ExpressRoute durumu](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Çözüm: AS YOLU eklenmesini kullanın
İki çözümleri toohello sorun vardır. Merhaba ilk Los Angeles ofisiniz hello ABD Batı'daki expressroute bağlantı hattı üzerinde 177.2.0.0/31 için şirket içi öneki yalnızca tanıtım ve New York ofisiniz 177.2.0.2/31 şirket hello ABD Doğu'daki expressroute bağlantı hattı için şirket içi öneki biridir. Sonuç olarak, Microsoft tooconnect tooeach ofisinize için yalnızca bir yolu yoktur. Belirsizlik olmaz ve yönlendirme en iyi duruma getirilir. Bu tasarımla, yük devretme stratejinizi toothink gerekir. Hello yolu tooMicrosoft ExpressRoute aracılığıyla hello olay bozuk, Exchange Online hala tooyour şirket içi sunucular bağlanabildiğinden emin toomake gerekir. 

Merhaba ikinci iki expressroute bağlantı hattında tooadvertise hem hello öneklerini, devam etmek ve ayrıca bize hangi önekin Kapat toowhich bir ofisinize olduğunu ipucu size çözümüdür. BGP AS yolu eklenmesini desteklemek için önek tooinfluence yönlendirme için hello AS Yolu'nu yapılandırabilirsiniz. Bu örnekte, böylece ABD Batı'daki hello expressroute bağlantı hattı için bu önek (ağımız hello yolu toothis öneki hello batıdan daha kısa olacağını düşüneceğinden) hedefleyen trafik için tercih eder ABD Doğu'daki 172.2.0.0/31 AS yolu hello uzatabilirsiniz. Benzer şekilde biz hello ABD Doğu'daki expressroute bağlantı hattını tercih ABD Batı'daki 172.2.0.2/31 için AS YOLU'nu hello uzatabilirsiniz. Her iki ofis için de yönlendirme en iyi duruma getirilmiştir. Bu tasarımla, bir ExpressRoute bağlantı hattı bozuk ise, Exchange Online başka bir ExpressRoute bağlantı hattı ve WAN’ınız aracılığıyla yine de size ulaşabilir. 

> [!IMPORTANT]
> Microsoft Peering'nde hello önekler için AS YOLU'nu hello numaraları alındı olarak size özel kaldırın. Tooappend gereken ortak AS numaraları akışındaki hello AS yolu tooinfluence Microsoft Peering için.
> 
> 

![ExpressRoute Vaka 2 çözümü: AS YOLU eklenmesini kullanın](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Burada verilen hello örnekleri Microsoft ve ortak eşlemeleri için olsa da, destekliyoruz hello hello özel eşleme için aynı yetenekleri. Ayrıca, hello AS yolu eklenmesini tek tek expressroute bağlantı hattı içinde tooinfluence hello seçimi hello birincil ve ikincil yol çalışır.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Sanal ağlar arasında yetersiz yönlendirme
ExpressRoute ile sanal ağ tooVirtual (olan olarak da bilinen "VNet") ağ etkinleştirebilirsiniz tooan expressroute bağlantı hattı bağlayarak iletişim. Toomultiple ExpressRoute bağlantı hatları bağlantı, yetersiz yönlendirme hello sanal ağlar arasında ortaya çıkar. Bir örnek düşünelim. Biri ABD Batı ve diğeri ABD Doğu’da olmak üzere iki ExpressRoute devreniz vardır. Her bölgede, iki sanal ağınız vardır. Web sunucusu, bir VNet içinde dağıtılır ve uygulama sunucuları diğer hello. Fazlalık için bağlantı iki Vnet'in de her bölgeye tooboth hello yerel expressroute bağlantı hattı hello ve uzak expressroute bağlantı hattı hello. Aşağıda görüldüğü gibi her sanal ağdan vardır iki yolları toohello diğer sanal ağ. expressroute bağlantı hattını yerel ve hangisinin uzak Hello sanal ağlar bilmediğiniz. Sonuç olarak eşit maliyet çoklu yol (ECMP) yönlendirme tooload Bakiye arası-VNet trafiği yapmak gibi bazı trafik akışına hello uzun yol sürer ve hello uzak expressroute bağlantı hattı yönlendirilmiş.

![ExpressRoute Vaka 3: Sanal ağlar arasında yetersiz yönlendirme](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Çözüm: yüksek ağırlık toolocal bağlantı atayın
Merhaba çözüm, basit bir işlemdir. Merhaba sanal ağlar ve hello devreler nerede bildiğiniz olduğundan, bize her VNet tercih etmelisiniz yolu anlayabilirsiniz. Özellikle bu örnek için daha yüksek ağırlık toohello yerel bağlantı toohello uzak bağlantı daha atayın (Merhaba yapılandırma örneği bkz [burada](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Bir VNet hello hello öneki aldığında diğer VNet birden çok bağlantı üzerinde onu hello bağlantı için bu önek hedefleyen hello en yüksek ağırlık toosend trafiği ile tercih eder.

![ExpressRoute servis talebi 3 çözüm - Ata yüksek ağırlık toolocal bağlantı](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> Ayrıca, birden çok ExpressRoute bağlantı hatları AS yolu eklenmesini, hello İkinci senaryoda yukarıda açıklanan teknikleri uygulamak yerine bir bağlantı hello ağırlığını yapılandırarak varsa VNet tooyour şirket içi ağdan yönlendirme etkileyebilir. Her öneki için her zaman hello bağlantı ağırlık hello AS yol uzunluğu önce karar verirken ele alacağız nasıl toosend trafiği.
>
>
