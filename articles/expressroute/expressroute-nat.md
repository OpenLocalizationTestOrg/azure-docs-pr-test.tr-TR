---
title: "ExpressRoute bağlantı hatları için aaaNAT gereksinimleri | Microsoft Docs"
description: "Bu sayfada, ExpressRoute bağlantı hatları için NAT’yi yapılandırma ve yönetmeye yönelik ayrıntılı gereksinimler sağlanmıştır."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 867bf936-c851-485f-84c8-d8d6e33fee9f
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 09a0e841235de3f6b85e32172d7f99f20b5baf54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-nat-requirements"></a>ExpressRoute NAT gereksinimleri
ExpressRoute kullanarak, tooconnect tooMicrosoft bulut hizmetlerine yukarı tooset gerekir ve NAT yönetin. Bazı bağlantı sağlayıcıları NAT ayarlama ve yönetimini yönetilen bir hizmet olarak sunar. Bu tür bir hizmet teklifi sunuyorsanız, bağlantı sağlayıcısı toosee ile denetleyin. Aksi durumda, aşağıda açıklanan toohello gereksinimlerine uymalıdır. 

Gözden geçirme hello [ExpressRoute bağlantı hatları ve Yönlendirme etki alanları](expressroute-circuit-peerings.md) çeşitli Yönlendirme etki alanlarına tooget hello genel bakış sayfasında. toomeet hello ortak IP adresi gereksinimleri Azure genel ve Microsoft eşlemesi için NAT'ı kurma ağınız ve Microsoft arasında ayarlamanızı öneririz. Bu bölümde yukarı tooset gereksinim hello NAT altyapısının ayrıntılı bir açıklama sağlar.

## <a name="nat-requirements-for-azure-public-peering"></a>Azure ortak eşleme için NAT gereksinimleri
Hello Azure ortak eşleme yolu ortak IP adresleri Azure'da barındırılan, tooconnect tooall hizmetleri sağlar. Hello listelenen hizmetleri bunlar [ExpessRoute hakkında SSS](expressroute-faqs.md) ve Microsoft Azure üzerinde ISV'ler tarafından barındırılan tüm hizmetleri. 

> [!IMPORTANT]
> Bağlantı tooMicrosoft Azure hizmetleri genel eşliği her zaman başlatıldığında ağınızdan hello Microsoft ağına doğru. Bu nedenle, oturumlar, ExpressRoute Microsoft Azure Hizmetleri tooyour ağdan başlatılamaz. Bulamazsa, gönderilen paketlerin toothese IP'leri tanıtılan kullanacağı ExpressRoute yerine Internet hello.
> 

Ortak eşleme hedefleyen trafiğe tooMicrosoft Azure ile Snat toovalid hello Microsoft ağına girmeden önce ortak IPv4 adresleri olmalıdır. Aşağıdaki şekilde Hello toomeet hello gereksinim yukarıda yukarı hello NAT nasıl ayarlanabileceğini gösteren yüksek düzey bir resim sunar.

![](./media/expressroute-nat/expressroute-nat-azure-public.png) 

### <a name="nat-ip-pool-and-route-advertisements"></a>NAT IP havuzu ve rota tanıtma
Trafiğin hello geçerli ortak IPv4 adresiyle Azure ortak eşleme yoluna girdiğinden emin olmalısınız. Microsoft, mümkün toovalidate hello hello bölgesel bir yönlendirme Internet kaydı (RIR) veya bir Internet yönlendirme kaydıyla (IRR) IPv4 NAT adres havuzu sahipliğini olması gerekir. Bir onay numarası eşlenen gibi hello üzerinde tabanlı gerçekleştirilir ve NAT hello için kullanılan IP adresleri hello Toohello başvuran [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) kayıt defterlerini yönlendirme hakkında bilgi için sayfa.

Bu eşleme aracılığıyla tanıtılan NAT IP öneki hello hello uzunluk sınırlaması yoktur. Merhaba NAT havuzunu izlemeniz ve, NAT oturumlarına gerek duyulmadığından emin olmanız gerekir.

> [!IMPORTANT]
> Merhaba NAT IP havuzu tooMicrosoft tanıtılan toohello Internet olmamalıdır tanıtılan. Bu bağlantı tooother Microsoft Hizmetleri çalışmamasına neden olur.
> 
> 

## <a name="nat-requirements-for-microsoft-peering"></a>Microsoft eşlemesi için NAT gereksinimleri
Merhaba Microsoft eşleme yolu hello Azure ortak eşleme yolu desteklenmeyen tooMicrosoft bulut Hizmetleri bağlanmanıza olanak sağlar. Exchange Online, SharePoint Online, Skype Kurumsal ve Dynamics 365 gibi Office 365 Hizmetleri Hello hizmetleri içerir. Microsoft hello Microsoft eşlemesi üzerinde çift yönlü bağlantı toosupport bekliyor. Giden trafiğe tooMicrosoft bulut Hizmetleri ile Snat toovalid hello Microsoft ağına girmeden önce ortak IPv4 adresleri olmalıdır. Microsoft bulut hizmetlerinden hedefleyen trafiğe tooyour ağ ile Snat olması gerekir, Internet kenar tooprevent [asimetrik yönlendirme](expressroute-asymmetric-routing.md). Aşağıdaki Hello şekilde hello NAT Microsoft eşlemesi için Kurulum nasıl olmalıdır üst düzey bir resim sağlanmıştır.

![](./media/expressroute-nat/expressroute-nat-microsoft.png) 

### <a name="traffic-originating-from-your-network-destined-toomicrosoft"></a>Ağ hedefleyen tooMicrosoft trafiği
* Trafiğin geçerli bir ortak IPv4 adresi ile Merhaba Microsoft eşleme yoluna girdiğinden emin olmalısınız. Microsoft, mümkün toovalidate hello sahibi hello IPv4 NAT adres havuzu hello bölgesel yönlendirme internet kaydı (RIR) veya bir internet yönlendirme kaydıyla (IRR) olması gerekir. Bir onay numarası eşlenen gibi hello üzerinde tabanlı gerçekleştirilir ve NAT hello için kullanılan IP adresleri hello Toohello başvuran [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) kayıt defterlerini yönlendirme hakkında bilgi için sayfa.
* Azure ortak eşleme Kurulumu hello için kullanılan IP adresleri ve diğer ExpressRoute bağlantı hatları hello BGP oturumu üzerinden tanıtılan tooMicrosoft olmaması gerekir. Bu eşleme aracılığıyla tanıtılan NAT IP öneki hello hello uzunluk sınırlaması yoktur.
  
  > [!IMPORTANT]
  > Merhaba NAT IP havuzu tooMicrosoft tanıtılan toohello Internet olmamalıdır tanıtılan. Bu bağlantı tooother Microsoft Hizmetleri çalışmamasına neden olur.
  > 
  > 

### <a name="traffic-originating-from-microsoft-destined-tooyour-network"></a>Microsoft hedefleyen tooyour ağdan kaynaklanan trafik
* Belirli senaryolar ağınız içinde barındırılan Microsoft tooinitiate bağlantı tooservice uç noktaları gerektirir. Tipik bir hello senaryosu örneği, Office 365'ten ağınızda barındırılan bağlantı tooADFS sunucularını olacaktır. Böyle durumlarda, uygun önekleri ağınızdan hello Microsoft eşlemesine sızdırmanız gerekir. 
* İçinde ağ tooprevent hello hizmet uç noktaları için Internet kenar SNAT Microsoft trafiğinin gerekir [asimetrik yönlendirme](expressroute-asymmetric-routing.md). ExpressRoute üzerinden alınan bir yol ile eşleşen hedef IP’si olan istekler **ve yanıtlar** her zaman ExpressRoute üzerinden gönderilir. Asimetrik yönlendirme var. hello ile Merhaba Internet üzerinden hello isteği alınırsa yanıt ExpressRoute üzerinden gönderildi. Merhaba Internet kenar SNATing hello gelen Microsoft trafiğinin yanıt trafiği arka toohello hello sorunu çözme Internet kenar zorlar.

![ExpressRoute ile asimetrik yönlendirme](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="next-steps"></a>Sonraki adımlar
* Toohello gereksinimleri başvuran [yönlendirme](expressroute-routing.md) ve [QoS](expressroute-qos.md).
* İş akışı bilgileri için bkz. [ExpressRoute bağlantı hattı sağlama iş akışları ve devre durumları](expressroute-workflows.md).
* ExpressRoute bağlantınızı yapılandırın.
  
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md)
  * [Yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md)
  * [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md)

