---
title: "Azure VPN ağ geçitleri ile yüksek oranda kullanılabilir yapılandırmaları aaaOverview | Microsoft Docs"
description: "Bu makalede Azure VPN Gateways kullanan yüksek oranda kullanılabilir yapılandırma seçeneklerine genel bakış sunulmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı
Bu makalede Azure VPN gateways kullanan şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantınız için Yüksek Oranda Kullanılabilir yapılandırma seçeneklerine genel bakış sunulmaktadır.

## <a name = "activestandby"></a>Azure VPN ağ geçidi artıklık hakkında
Her Azure VPN gateway, etkin bir bekleme yapılandırmasında iki örnekten oluşur. Herhangi bir planlı Bakım veya toohello etkin örnek olur planlanmamış kesintisi için hello bekleme örneğine (yerine) otomatik olarak ayırın ve hello S2S VPN veya VNet-VNet bağlantıları sürdürün. başlangıç anahtarı üzerinden kısa bir kesintiye neden olur. Planlı bakım için hello bağlantı 10 too15 saniye içinde geri yüklenmelidir. Planlanmamış sorunları için hello bağlantı kurtarma hakkında 1 dakika too1 daha uzun olur ve bir yarı hello kötü durumda dakika. P2S VPN istemci bağlantıları toohello ağ geçidi için hello P2S bağlantılarının kesilecek ve hello kullanıcılar hello istemci makinelerden tooreconnect gerekir.

![Etkin Bekleme](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı Karışık Bağlantı
tooprovide daha iyi kullanılabilirlik için çapraz bağlantıları şirket içi, birkaç seçeneğiniz vardır:

* Birden fazla şirket içi VPN cihazı
* Etkin-etkin Azure VPN gateway
* Her ikisinin birleşimi

### <a name = "activeactiveonprem"></a>Birden çok şirket içi VPN cihazları
Hello Aşağıdaki diyagramda gösterildiği gibi şirket içi ağ tooconnect tooyour Azure VPN ağ geçidi'nden, birden çok VPN aygıtları kullanabilirsiniz:

![Birden Fazla Şirket İçi VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Bu yapılandırma hello gelen birden çok etkin tünelleri aynı Azure VPN ağ geçidi tooyour şirket içi cihazları hello sağlar. konumda. Bazı gereksinimler ve kısıtlamalar vardır:

1. Birden fazla S2S VPN bağlantıları, VPN aygıtları tooAzure toocreate gerekir. Birden çok VPN aygıtları hello bağlandığınızda tooAzure aynı şirket içi ağ, Azure VPN ağ geçidi toohello yerel ağ geçidinden toocreate bir yerel ağ geçidi her VPN cihazı için ve bir bağlantı gerekir.
2. Merhaba yerel ağ geçitleri tooyour VPN aygıtları karşılık gelen benzersiz genel IP adresleri hello "Gatewayıpaddress" özelliği olması gerekir.
3. Bu yapılandırma için BGP gereklidir. Bir VPN cihazı temsil eden her yerel ağ geçidi hello "BgpPeerIpAddress" özelliğinde belirtilen benzersiz bir BGP eş IP adresi olmalıdır.
4. Merhaba AddressPrefix özelliği her yerel ağ geçidi alanında çakışmaması gerekir. İçinde /32 hello "BgpPeerIpAddress" belirtmelisiniz hello AddressPrefix alan, örneğin, 10.200.200.254/32 CIDR biçiminde.
5. BGP kullanması gereken tooadvertise hello aynı önekleri hello öneklerini tooyour Azure VPN ağ geçidi aynı şirket içi ağ ve hello trafiği iletilir bu tüneller içinden eşzamanlı olarak.
6. Her bağlantı tünelleri temel ve standart SKU'ları, 10, Azure VPN ağ geçidi için en fazla hello karşı kabul edilir ve HighPerformance SKU için 30. 

Bu yapılandırmada, hello Azure VPN ağ geçidi hala etkin bekleme modunda; bu nedenle aynı yük devretme davranışı hello ve kısa kesinti hala gerçekleşecek açıklandığı gibi [yukarıda](#activestandby). Ancak, bu kurulum şirket içi ağınızda ve VPN cihazlarınızda arıza ya da kesintilere karşı koruma sağlar.

### <a name="active-active-azure-vpn-gateway"></a>Etkin-etkin Azure VPN gateway
Burada hello ağ geçidi VMs aşağıdaki gösterilen hello tooyour şirket içi VPN cihazı S2S VPN tünelleri kuracak her iki örneği diyagram bir aktif-aktif yapılandırmasında bir Azure VPN ağ geçidi artık oluşturabilirsiniz:

![Etkin-Etkin](./media/vpn-gateway-highlyavailable/active-active.png)

Bu yapılandırmada, her Azure ağ geçidi örneğini benzersiz bir ortak IP adresi vardır ve her yerel ağ geçidi ve bağlantıyla içinde belirtilen bir IPSec/IKE S2S VPN tüneli tooyour şirket içi VPN cihazı kurar. Her iki VPN tünelleri hello gerçekte bir parçası olduğunu unutmayın aynı bağlantı. Hala şirket içi VPN aygıtının tooaccept tooconfigure gerekir veya iki S2S VPN tünelleri toothose iki Azure VPN ağ geçidi genel IP adresleri kurmak.

Hello Azure ağ geçidi örnekleri etkin-etkin yapılandırmasında olduğundan, Azure sanal ağı tooyour hello trafiği ağ hem tüneller içinden eşzamanlı olarak yönlendirilir, şirket içi VPN cihazınızın bir tünel üzerinden favor olsa bile şirket içi Merhaba diğer. Aynı TCP veya UDP akışı her zaman dizinlere hello hello ancak aynı tünel veya yol, bir bakım olayı hello örnekleri birinde olur sürece unutmayın.

Planlanan Bakım veya planlanmamış olay tooone ağ geçidi örneği olduğunda, bu örnek tooyour gelen hello IPSec tüneli VPN cihazı kesilecek şirket içi. Merhaba VPN cihazlarınızda karşılık gelen yollar kaldırılamıyor veya böylece hello trafiği toohello bırakılacak otomatik olarak geri alınmış diğer etkin IPSec tüneli. Hello Azure tarafı, başlangıç anahtarı üzerinden etkilenen hello örneği toohello etkin örnekten otomatik olarak gerçekleşir.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Çift yedeklilik: hem Azure hem de şirket içi ağlara için etkin-etkin VPN ağ geçitleri
Merhaba en güvenilir ağ ve Azure üzerindeki toocombine hello etkin-etkin ağ geçitlerini hello çizimde gösterildiği gibi bir seçenektir.

![Çift Yedeklilik](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Burada oluşturmak ve bir aktif-aktif yapılandırma hello Azure VPN ağ geçidi kurulumu ve iki yerel ağ geçitleri oluşturmak ve iki bağlantıları için iki şirket içi VPN aygıtları yukarıda açıklandığı gibi. Merhaba, 4 IPSec tünelleri, Azure sanal ağı ve şirket içi ağınız arasında bir tam ağ bağlantısı sonucudur.

Tüm ağ geçitleri ve tünelleri hello Azure yan etkin olan, hello trafiği olacak her TCP veya UDP akış rağmen tüm 4 tüneller arasında aynı anda yayılan yeniden izleyin hello aynı tünel veya yolundan hello Azure yan. Merhaba trafik yayarak hello IPSec tüneller üzerinden biraz daha iyi verim görebilirsiniz karşın hello birincil amacı, bu yapılandırma yüksek kullanılabilirlik için geçerlidir. Ve hello yayılmak, toohello istatistiksel yapısı, bu zor tooprovide hello ölçüm nasıl farklı uygulama trafiğinde koşullar hello toplam verimlilik etkiler.

Bu topoloji iki yerel ağ geçitleri ve şirket içi VPN aygıtları iki bağlantı toosupport hello çifti gerektirir ve BGP olan gerekli tooallow hello iki bağlantıları toohello aynı şirket içi ağ. Bu gereksinimleri aynı hello hello olan [yukarıda](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Azure VPN Gateways aracılığıyla Yüksek Oranda Kullanılabilir Sanal Ağdan Sanal Ağa Bağlantı
Merhaba aynı aktif-aktif yapılandırma de tooAzure VNet-VNet bağlantıları uygulayabilirsiniz. Her iki sanal ağlar için etkin-etkin VPN ağ geçitleri oluşturun ve bunları aynı tam aşağıda hello gösterildiği gibi iki Vnet diyagram hello arasındaki 4 tüneller bağlantısını kafes birlikte tooform hello bağlayın:

![Sanal Ağdan Sanal Ağa](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Bu, her zaman daha iyi kullanılabilirlik sağlayan, herhangi bir planlı bakım olayı için hello iki sanal ağlar arasında tüneller çifti sağlar. Merhaba şirket içi bağlantılar için aynı topolojisi gerektiren iki bağlantı olsa bile, yukarıda gösterilen hello VNet-VNet topolojisi her ağ geçidi için yalnızca bir bağlantı gerekir. Ayrıca, BGP transit yönlendirme hello VNet-VNet bağlantısı gerekli olmadığı sürece isteğe bağlıdır.

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [yapılandırma etkin-etkin VPN ağ geçitleri için şirket içi ve VNet-VNet bağlantıları](vpn-gateway-activeactive-rm-powershell.md) adımları tooconfigure etkin-etkin şirket içi ve VNet-VNet bağlantıları için.

