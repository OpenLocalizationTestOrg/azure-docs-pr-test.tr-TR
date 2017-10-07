---
title: "Yük Dengeleyici genel kullanıma yönelik aaaInternet | Microsoft Docs"
description: "Internet'e yönelik Yük Dengeleyici ve özellikleri için genel bakış. Nasıl bir yük dengeleyici sanal makineler ve bulut hizmetlerini kullanarak Azure için çalışır."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a>Internet kullanıma yönelik Yük Dengeleyici genel bakış

Azure yük dengeleyici hello ortak IP adresi ve bağlantı noktası numarası gelen trafiği toohello özel IP adresi ve bağlantı noktası numarası hello sanal makinenin ve tersi hello yanıt trafiği hello sanal makineden eşler. Yük Dengeleme kuralları toodistribute belirli birden çok sanal makineler veya hizmetler arasındaki trafik türlerinin izin verir. Örneğin, birden çok web sunucuları veya web rolleri web isteği trafiği hello yükünü yayılabilir.

Web rolleri veya çalışan rolleri örneklerini içeren bir bulut hizmeti için genel bir uç nokta hello hizmet açıklaması (.csdef) dosyasında tanımlayabilirsiniz.

Merhaba *servicedefinition.csdef* dosyası hello uç nokta yapılandırması içerir ve bir web veya çalışan rolü dağıtımı için birden çok rol örneği varsa, hello yük dengeleyici ayarları için olacaktır. Merhaba yolu tooadd örnekleri tooyour bulut dağıtımı hello örnek sayısı hello hizmet yapılandırma dosyası (.csfg) üzerinde değiştiriyor.

Merhaba aşağıdaki şekilde hello ortak ve özel TCP bağlantı noktası 80 için üç sanal makineler arasında paylaşılan web trafiği için yük dengeli bir uç nokta gösterilmektedir. Bu üç sanal makine bir yük dengeli kümesi yok.

![Ortak yük dengeleyici örneği](./media/load-balancer-internet-overview/IC727496.png)

Şekil 1 - web trafiği için yük dengeli uç nokta

Internet istemcileri TCP bağlantı noktası 80 üzerinde toohello genel IP adresi hello bulut hizmetinin web sayfası istekleri gönderdiğinizde, hello Azure yük dengeleyici hello isteklerini hello yük dengeli kümesi içindeki hello üç sanal makineler arasında dağıtır. Yük Dengeleyici algoritmalar hakkında daha fazla bilgi için bkz: Merhaba [yük dengeleyici genel bakış sayfasında](load-balancer-overview.md#load-balancer-features).

Varsayılan olarak, Azure yük dengeleyici ağ trafiği birden çok sanal makine örnekleri arasında eşit olarak dağıtır. Oturum benzeşimi de yapılandırabilirsiniz daha fazla bilgi için bkz: [yük dengeleyici dağıtım modu](load-balancer-distribution-mode.md).

## <a name="next-steps"></a>Sonraki adımlar

Hakkında bilgi edinin [iç yük dengeleyici](load-balancer-internal-overview.md) toobetter anlamak daha iyi bir uyum bulut dağıtımınız için hangi yük dengeleyicidir.

Ayrıca [Internet'e yönelik Yük Dengeleyici oluşturmaya başlamak](load-balancer-get-started-internet-arm-ps.md) ve ne tür yapılandırma [dağıtım modu](load-balancer-distribution-mode.md) bir özel yük dengeleyici ağ trafiği davranışı için.

Uygulamanızı tookeep bağlantıları canlı bir yük dengeleyicinin arkasındaki sunucular için gerekiyorsa, daha fazla hakkında anlayabileceği [boşta bir yük dengeleyici için TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md). Azure yük dengeleyici kullanırken toolearn boştaki bağlantı davranışı konusunda yardımcı olur.
