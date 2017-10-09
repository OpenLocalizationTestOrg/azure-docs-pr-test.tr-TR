---
title: Azure VPN Gateways ile BGP'ye aaaOverview | Microsoft Docs
description: "Bu makale Azure VPN Gateways ile BGP’ye genel bakış sağlar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Azure VPN Gateways ile BGP’ye genel bakış
Bu makale Azure VPN Gateways içindeki BGP (Sınır Ağ Geçidi Protokolü) desteğine genel bakış sağlar.

BGP hello Internet tooexchange Yönlendirme ve ulaşılabilirlik bilgilerini iki veya daha fazla ağ arasında yaygın olarak kullanılan hello standart yönlendirme protokolüdür. Ne zaman hello Azure sanal ağlar bağlamında kullanıldığında, BGP hello Azure VPN ağ geçitleri ve BGP eşleri olarak adlandırılan, şirket içi VPN cihazlarınızı etkinleştirir veya Komşuları olarak tooexchange "yolları", her iki ağ geçidini hello kullanılabilirliği ve ulaşılabilirliği olanlar için size bildirir Merhaba ağ geçitlerinden veya yönlendiricilerden söz konusu aracılığıyla toogo ekler. BGP, bir BGP eş tooall bir BGP ağ geçidinin öğrendiği yolları yayarak birden fazla ağ arasında geçiş yönlendirme de etkinleştirebilir diğer BGP eşleri. 

## <a name="why-use-bgp"></a>BGP neden kullanılır?
BGP, Azure Yol Tabanlı VPN ağ geçitleri ile birlikte kullanabileceğiniz isteğe bağlı bir özelliktir. Merhaba özelliği etkinleştirmeden önce şirket içi VPN cihazlarınızı BGP desteklediğinden emin olmalısınız. Toouse Azure VPN ağ geçitleri ve şirket içi VPN cihazlarınızı BGP olmadan devam edebilirsiniz. Statik yollar (BGP olmadan) kullanarak eşdeğer hello olan *karşılaştırması* dinamik BGP ile ağlarınız ve Azure arasında yönlendirme kullanarak.

BGP’nin çeşitli avantajları ve yeni özellikleri vardır:

### <a name="support-automatic-and-flexible-prefix-updates"></a>Otomatik ve esnek ön ek güncelleştirmelerini destekler
BGP ile yalnızca hello IPSec S2S VPN tüneli üzerinden toodeclare minimum önek tooa belirli BGP eşi gerekir. Ana bilgisayar önek olarak küçük olabilir (/ 32) hello şirket içi VPN cihazınızın BGP eş IP adresini. Hangi ağ önekleri, Azure Virtual Network tooaccess tooadvertise tooAzure tooallow istediğiniz şirket içi kontrol edebilirsiniz.

Ayrıca, büyük özel bir IP adres alanı (örneğin, 10.0.0.0/8) gibi VNet adres ön bazıları içerebilir büyük ön ekler tanıtabilirsiniz. Hello öneklerini VNet ön herhangi biri ile aynı olamaz olsa unutmayın. Bu yollar aynı tooyour VNet ön reddedilir.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Bir VNet ile şirket içi site arasında BGP’yi temel alan otomatik yük devretme ile birden fazla tüneli destekler
Birden fazla Azure VNet ile şirket içi VPN cihazlarınızı arasında hello bağlantı kurabilir aynı konumu. Bu özellik, bir aktif-aktif yapılandırma hello iki ağ arasında birden fazla tünel (yol) sağlar. Merhaba tüneller birini bağlantısı kesilmişse hello karşılık gelen yollar BGP aracılığıyla geri çekilir ve hello trafiği toohello kalan tünellere otomatik olarak geçer.

Aşağıdaki diyagramda hello bu yüksek oranda kullanılabilir kurulumun basit bir örneği gösterilmektedir:

![Birden fazla etkin yol](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Şirket içi ağlarınız ile birden fazla Azure VNet arasında geçiş yönlendirme desteği
BGP birden çok ağ geçitleri toolearn sağlar ve doğrudan veya dolaylı olarak bağlı olmasına bakılmaksızın farklı ağlardaki ön ekleri yayar. Bu özellik şirket içi siteleriniz arasında veya birden fazla Azure Sanal Ağında Azure VPN ağ geçitleri ile geçiş yönlendirmesi sağlayabilir.

Merhaba Aşağıdaki diyagramda hello hello Microsoft Networks içindeki Azure VPN ağ geçitleri üzerinden iki şirket içi ağlar arasındaki trafiği geçebilen birden fazla yol ile çoklu atlamalı bir topolojinin örneği gösterilmektedir:

![Çoklu atlamalı geçiş](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>BGP SSS
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [Azure VPN ağ geçitlerinde BGP ile çalışmaya başlama](vpn-gateway-bgp-resource-manager-ps.md) şirketler arası ve VNet-VNet bağlantıları için adımları tooconfigure BGP için.

