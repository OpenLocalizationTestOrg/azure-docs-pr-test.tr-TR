---
title: "Azure VPN ağ geçitleri ile yüksek oranda kullanılabilir yapılandırmaları genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 3708a2f7c445a161f02416cf8427b1707e1db8f0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı
Bu makalede Azure VPN gateways kullanan şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantınız için Yüksek Oranda Kullanılabilir yapılandırma seçeneklerine genel bakış sunulmaktadır.

## <a name = "activestandby"></a>Azure VPN ağ geçidi artıklık hakkında
Her Azure VPN gateway, etkin bir bekleme yapılandırmasında iki örnekten oluşur. Etkin örnekte gerçekleşen herhangi bir planlı bakım veya plansız kesintide, beklemedeki örnek otomatik olarak yükü devralıp S2S VPN veya Sanal Ağdan Sanal Ağa bağlantıları sürdürür. Bu geçiş kısa bir kesintiye neden olur. Planlı bakım için bağlantı 10 ila 15 saniye içinde geri yüklenmelidir. Planlanmamış sorunlar için bağlantı kurtarma süresi yaklaşık 1 dakika ile en kötü durumda 1 buçuk dakika arasında değişir. Ağ geçidiyle P2S VPN istemci bağlantıları için P2S bağlantıları kesilir ve kullanıcıların istemci makinelerden yeniden bağlantı kurması gerekir.

![Etkin Bekleme](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı Karışık Bağlantı
Şirket içi ve dışı karışık bağlantılarınızda daha iyi kullanılabilirlik sağlamak için birkaç seçenek mevcuttur:

* Birden fazla şirket içi VPN cihazı
* Etkin-etkin Azure VPN gateway
* Her ikisinin birleşimi

### <a name = "activeactiveonprem"></a>Birden çok şirket içi VPN cihazları
Şirket içi ağınızdan Azure VPN gateway’e bağlanmak için aşağıdaki diyagramda gösterildiği gibi birden fazla VPN cihazı kullanabilirsiniz:

![Birden Fazla Şirket İçi VPN](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Bu yapılandırma aynı Azure VPN ağ geçidinden aynı konumdaki şirket içi cihazlarınıza birden fazla etkin tünel sağlar. Bazı gereksinimler ve kısıtlamalar vardır:

1. VPN cihazlarınız ile Azure arasında birden fazla S2S VPN bağlantısı oluşturmanız gerekir. Aynı şirket içi ağdan Azure’a birden fazla VPN cihazı bağladığınızda her VPN cihazı için bir yerel ağ geçidi ve Azure VPN ağ geçidinizden yerel ağ geçidine bir bağlantı oluşturmanız gerekir.
2. VPN cihazlarınıza karşılık gelen yerel ağ geçitleri "GatewayIpAddress" özelliğinde benzersiz genel IP adreslerine sahip olmalıdır.
3. Bu yapılandırma için BGP gereklidir. Bir VPN cihazını temsil eden her yerel ağ geçidinin "BgpPeerIpAddress" özelliğinde belirtilen benzersiz bir BGP eşleme IP adresi olmalıdır.
4. Her yerel ağ geçidindeki AddressPrefix özellik alanı birbiriyle örtüşmemelidir. AddressPrefix alanında “BgpPeerIpAddress” özelliğini /32 CIDR biçiminde belirtmeniz gerekir; örneğin, 10.200.200.254/32.
5. Aynı şirket içi ağ ön eklerini Azure VPN ağ geçidinize tanıtmak için BGP kullanmanız gerekir; bu durumda trafik bu tünellerden eşzamanlı olarak iletilir.
6. Her bağlantı Azure VPN ağ geçidinizin en fazla tünel sayısına göre sayılır; Temel ve Standart SKU’lar için 10 ve Yüksek Performanslı SKU’lar için 30. 

Bu yapılandırmada Azure VPN ağ geçidi hala etkin bekleme modundadır; bu nedenle [yukarıda](#activestandby) açıklanan yük devretme davranışının ve kısa kesintinin aynısı gerçekleşir. Ancak, bu kurulum şirket içi ağınızda ve VPN cihazlarınızda arıza ya da kesintilere karşı koruma sağlar.

### <a name="active-active-azure-vpn-gateway"></a>Etkin-etkin Azure VPN gateway
Bundan sonra, aşağıdaki şekilde gösterildiği gibi, her iki ağ geçidi sanal makine örneğinin de şirket içi VPN cihazınızda S2S VPN tünelleri oluşturacağı etkin-etkin bir yapılandırmada Azure VPN ağ geçidi oluşturabilirsiniz:

![Etkin-Etkin](./media/vpn-gateway-highlyavailable/active-active.png)

Bu yapılandırmada her Azure ağ geçidi örneği benzersiz bir genel IP adresine sahiptir ve her biri yerel ağ geçidinizde ve bağlantınızda belirtilen şirket içi VPN cihazınızda bir IPsec/IKE S2S VPN tüneli oluşturur. Her iki VPN tüneli de aslında aynı bağlantının bir parçasıdır. Şirket içi VPN cihazınızı yine de bu iki Azure VPN ağ geçidi genel IP adresini kabul edecek veya bunlarla iki S2S VPN tüneli oluşturacak şekilde yapılandırmanız gerekir.

Azure ağ geçidi örnekleri etkin-etkin yapılandırmada olduğundan, şirket içi VPN cihazınız bir tüneli diğerinden daha fazla tercih etse bile Azure sanal ağınızdan şirket içi ağınıza giden trafik her iki tünelden eşzamanlı olarak yönlendirilir. Ancak, örneklerden birinde bir bakım olayı gerçekleşmedikçe aynı TCP veya UDP akışı her zaman aynı tünel veya yoldan geçer.

Bir ağ geçidi örneğinde planlı bir bakım veya planlanmamış bir olay gerçekleştiğinde bu örnekten şirket içi VPN cihazınıza giden IPSec tünelinin bağlantısı kesilir. Trafiğin diğer etkin IPsec tüneline geçirilmesi için VPN cihazlarınızda karşılık gelen yolların kaldırılması veya otomatik olarak geri alınması gerekir. Azure tarafında bu geçiş etkilenen örnekten etkin örneğe doğru otomatik olarak gerçekleşir.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Çift yedeklilik: hem Azure hem de şirket içi ağlara için etkin-etkin VPN ağ geçitleri
En güvenilir seçenek, aşağıdaki diyagramda gösterildiği gibi hem ağınızda hem de Azure’da etkin-etkin ağ geçitlerinin birleştirilmesidir.

![Çift Yedeklilik](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Burada etkin-etkin yapılandırmada Azure VPN ağ geçidi oluşturup yapılandırır ve yukarıda açıklandığı gibi iki şirket içi VPN cihazınız için iki yerel ağ geçidi ile iki bağlantı oluşturursunuz. Sonuçta Azure sanal ağınız ile şirket içi ağınız arasında 4 IPsec tünelinden oluşan tam bir ağ bağlantısı elde edilir.

Azure tarafında tüm ağ geçitleri ve tüneller etkindir; bu nedenle trafik 4 tünelin tamamı arasında eşzamanlı olarak yayılır, ancak her TCP veya UDP akışı yine Azure tarafındaki aynı tüneli veya yolu izler. Trafik yayarak IPSec tünelleri üzerinde biraz daha iyi verim görebilmenize karşın, bu yapılandırmanın birincil amacı yüksek kullanılabilirlik içindir. Ayrıca yaymanın istatistiksel niteliği nedeniyle farklı uygulama trafiği koşullarının toplam verimliliği nasıl etkilediğini ölçmek güçtür.

Bu topoloji, şirket içi VPN cihazları çiftini desteklemek iki yerel ağ geçidi ve iki bağlantı gerektirir ve aynı şirket içi ağ ile iki bağlantı için BGP gereklidir. Bu gereksinimler [yukarıdakiler](#activeactiveonprem) ile aynıdır. 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Azure VPN Gateways aracılığıyla Yüksek Oranda Kullanılabilir Sanal Ağdan Sanal Ağa Bağlantı
Aynı etkin-etkin yapılandırma Azure Sanal Ağdan Sanal Ağa bağlantıları için de geçerli olabilir. Her iki sanal ağ için etkin-etkin VPN ağ geçitleri oluşturabilir ve aşağıdaki diyagramda gösterildiği gibi bunları birbirine bağlayarak iki sanal ağ arasında 4 tünelden oluşan tam bir ağ bağlantısı kurabilirsiniz:

![Sanal Ağdan Sanal Ağa](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Bunun yapılması iki sanal ağ arasında planlı bakım olayları için her zaman bir tünel çifti olmasını sağlar ve daha da iyi kullanılabilirlik sunar. Şirket içi ve dışı karışık bağlantı için aynı topoloji iki bağlantı gerektirse de, yukarıda gösterilen Sanal Ağdan Sanal Ağa topolojisi her ağ geçidi için yalnızca bir bağlantıya gereksinim duyar. Ayrıca, Sanal Ağdan Sanal Ağa bağlantı üzerinden geçiş yönlendirmesi gerekli olmadıkça BGP isteğe bağlıdır.

## <a name="next-steps"></a>Sonraki adımlar
Etkin-etkin şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantıları yapılandırma adımları için bkz. [Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantılar için Etkin-Etkin VPN Gateways Yapılandırma](vpn-gateway-activeactive-rm-powershell.md).

