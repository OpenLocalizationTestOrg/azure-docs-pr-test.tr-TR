---
title: "azure'da aaaUnderstanding giden bağlantılar | Microsoft Docs"
description: "Bu makalede, Azure VM'ler toocommunicate ortak Internet Hizmetleri ile nasıl sağladığını açıklar."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Azure’da giden bağlantıları anlama

Azure'da bir sanal makine (VM) dışında Azure ortak IP adres alanındaki uç noktalar ile iletişim kurabilir. Bir VM ortak IP adresi alanı içindeki bir giden akış tooa hedef başlattığında, Azure hello VM'in özel IP adresi tooa ortak IP adresi eşler ve dönüş trafiği tooreach hello VM sağlar.

Azure tooachieve giden bağlantı üç farklı yöntem sağlar. Her yöntemin kendine özgü özellikleri ve sınırlamaları vardır. Her yöntem dikkatlice inceleyin hangisinin gereksinimlerinizi karşılayan toochoose.

| Senaryo | Yöntem | Not |
| --- | --- | --- |
| Tek başına VM (yük dengeleyici, örnek düzeyinde ortak IP adresi yok) |Varsayılan SNAT |Azure genel bir IP adresi için SNAT ilişkilendirir. |
| VM Yük Dengelemesi (VM üzerinde örnek düzeyinde ortak IP adres yok) |Merhaba yük dengeleyici kullanarak SNAT |Azure hello yük dengeleyici, genel bir IP adresi için SNAT kullanır. |
| VM örnek düzeyinde ortak IP adresiyle (ile veya yük dengeleyici olmadan) |SNAT kullanılmıyor |Azure VM toohello atanan hello genel IP kullanır |

Azure ortak IP adres alanındaki dışında uç noktaları VM toocommunicate istemiyorsanız, ağ güvenlik grupları (NSG) tooblock erişim kullanabilirsiniz. Nsg'leri kullanarak ele alınmıştır daha ayrıntılı olarak [önleme ortak bağlantısını](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Örnek düzeyinde ortak IP adresi olmayan tek başına VM

Bu senaryoda, hello VM Azure yük dengeleyici havuzu parçası olmayan ve tooit atanmış örnek düzeyinde ortak IP (ILPIP) adresi yok. Merhaba VM giden akış oluşturduğunda, Azure hello özel kaynak IP adresi hello giden akış tooa ortak kaynak IP adresi çevirir. Merhaba bu giden akış için kullanılan ortak IP adresi yapılandırılabilir değildir ve hello aboneliğin ortak IP kaynak sınırınızı sayılmaz. Azure kaynak ağ adresi çevirisi (SNAT) tooperform bu işlev kullanır. Kullanılan toodistinguish tek tek akışları hello VM tarafından kaynaklanan hello ortak IP adresinin kısa ömürlü bağlantı noktalarıdır. Akışları oluşturduğunuzda SNAT kısa ömürlü bağlantı noktaları dinamik olarak ayırır. Bu bağlamda snat Uygulamanız için kullanılan hello kısa ömürlü bağlantı noktaları başvurulan tooas SNAT bağlantı noktalarıdır.

SNAT bağlantı noktalarını tükenmiş olabilir sınırlı bir kaynaktır. Önemli toounderstand nasıl tüketildiğinin olur. Bir SNAT bağlantı noktası her akış tooa tek hedef IP adresi kullanılır. Birden çok akış toohello için aynı hedef IP adresi, her bir akışa tek bir SNAT bağlantı noktasını kullanır. Bu başlangıç akışları benzersiz olduğunda hello aynı kaynaklanan olmasını sağlar ortak IP adresi toohello aynı hedef IP adresi. Birden çok akışları her tooa farklı bir hedef IP adresi hedef başına tek bir SNAT bağlantı noktası kullanma. Merhaba hedef IP adresi hello akışları benzersiz hale getirir.

Kullanabileceğiniz [yük dengeleyici için günlük analizi](load-balancer-monitor-log.md) ve [SNAT bağlantı noktası Tükenme iletileri için uyarı olayı günlükleri toomonitor](load-balancer-monitor-log.md#alert-event-log). SNAT bağlantı noktası kaynakları tükendi SNAT bağlantı noktaları tarafından varolan akışları serbest bırakılana kadar giden trafik akışları yük devredersiniz. Yük Dengeleyici SNAT bağlantı noktalarını geri kazanma için 4 dakikalık boşta kalma zaman aşımı kullanır.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Hiçbir örnek düzeyinde ortak IP adresine sahip yük dengeli VM

Bu senaryoda, hello VM Azure yük dengeleyici havuzu bir parçasıdır.  Merhaba VM tooit atanan genel bir IP adresi yok. Merhaba yük dengeleyici kaynak, bir kural toolink hello ortak IP ön hello arka uç havuzu ile yapılandırılmalıdır.  Bu yapılandırma tamamlamazsanız hello için hello bölümünde açıklandığı gibi davranıştır [hiçbir örnek düzeyinde ortak IP ile tek başına VM](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Merhaba VM yük dengeli bir giden akış oluşturduğunda, Azure hello giden akış toohello genel IP adresi hello ortak yük dengeleyici ön uç hello özel kaynak IP adresi çevirir. Azure kaynak ağ adresi çevirisi (SNAT) tooperform bu işlev kullanır. Kullanılan toodistinguish tek tek akışları hello VM tarafından kaynaklanan hello yük dengeleyicinin genel IP adresinin kısa ömürlü bağlantı noktalarıdır. Giden trafik akışları oluşturduğunuzda SNAT kısa ömürlü bağlantı noktaları dinamik olarak ayırır. Bu bağlamda snat Uygulamanız için kullanılan hello kısa ömürlü bağlantı noktaları başvurulan tooas SNAT bağlantı noktalarıdır.

SNAT bağlantı noktalarını tükenmiş olabilir sınırlı bir kaynaktır. Önemli toounderstand nasıl tüketildiğinin olur. Bir SNAT bağlantı noktası her akış tooa tek hedef IP adresi kullanılır. Birden çok akış toohello için aynı hedef IP adresi, her bir akışa tek bir SNAT bağlantı noktasını kullanır. Bu başlangıç akışları benzersiz olduğunda hello aynı kaynaklanan olmasını sağlar ortak IP adresi toohello aynı hedef IP adresi. Birden çok akışları her tooa farklı bir hedef IP adresi hedef başına tek bir SNAT bağlantı noktası kullanma. Merhaba hedef IP adresi hello akışları benzersiz hale getirir.

Kullanabileceğiniz [yük dengeleyici için günlük analizi](load-balancer-monitor-log.md) ve [SNAT bağlantı noktası Tükenme iletileri için uyarı olayı günlükleri toomonitor](load-balancer-monitor-log.md#alert-event-log). SNAT bağlantı noktası kaynakları tükendi SNAT bağlantı noktaları tarafından varolan akışları serbest bırakılana kadar giden trafik akışları yük devredersiniz. Yük Dengeleyici SNAT bağlantı noktalarını geri kazanma için 4 dakikalık boşta kalma zaman aşımı kullanır.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Örnek düzeyinde ortak IP adresi (ile veya yük dengeleyici olmadan) olan VM

Bu senaryoda, bir örnek düzeyinde ortak IP (tooit atanan ILPIP) hello VM sahiptir. Merhaba VM veya dengelendiği olup önemli değildir. Bir ILPIP kullanıldığında, kaynak ağ adresi çevirisi (SNAT) kullanılmaz. Merhaba VM hello ILPIP tüm giden trafik akışları için kullanır. Uygulamanız çok sayıda giden trafik akışları başlatır ve SNAT Tükenme deneyimi, bir ILPIP tooavoid SNAT kısıtlamaları atama düşünmelisiniz.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Belirli bir VM tarafından kullanılan hello genel IP bulma

Toodetermine hello ortak kaynak IP adresi giden bir bağlantıyı birçok yolu vardır. OpenDNS göstermek bir hizmet sunar hello VM genel IP adresi. Merhaba nslookup komutunu kullanarak, hello adı myip.opendns.com toohello OpenDNS Çözümleyicisi için bir DNS sorgusu gönderebilir. Merhaba hizmeti kullanılan toosend hello sorgu hello kaynak IP adresi döndürür. Sorgu, VM'den aşağıdaki hello yürüttüğünüzde hello yanıt genel IP o VM için kullanılan hello ' dir.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Genel bağlantı önleme

Bazen, bir VM toobe toocreate giden akış izin verileceğini veya hangi hedefleri giden trafik akışları ile ulaşılabilen gereksinim toomanage olabilir istenmeyen aranır. Bu durumda, kullandığınız [ağ güvenlik grupları (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage hello hedefleri VM ulaşmak o hello. Bir NSG'yi uyguladığınızda tooa yük dengeli VM, toopay dikkat toohello gerek [varsayılan etiketleri](../virtual-network/virtual-networks-nsg.md#default-tags) ve [varsayılan kuralları](../virtual-network/virtual-networks-nsg.md#default-rules).

Bu hello VM Azure yük Dengeleyiciden sistem durumu araştırma isteklerine alabilir emin olmalısınız. Bir NSG blokları sistem durumu araştırma isteklerine olduğunda hello AZURE_LOADBALANCER varsayılan etiket, VM durumu araştırması başarısız olur ve hello VM düşürüleceği. Yük Dengeleyici yeni akışları toothat VM göndermeyi durdurur.

## <a name="limitations"></a>Sınırlamalar

Varsa [(Genel) birden çok IP adresi bir yük dengeleyici ile ilişkili](load-balancer-multivip-overview.md), herhangi bir aday giden trafik akışları için bu ortak IP adresleridir.

Azure hello hello havuzu boyutuna göre bir algoritma toodetermine hello SNAT kullanılabilir bağlantı noktası sayısını kullanır.  Bu şu anda yapılandırılabilir değildir.

Kullanılabilir SNAT bağlantı noktası sayısını hello toorememember doğrudan toonumber bağlantılarının tercüme etmez önemlidir. Lütfen yukarıdaki özellikleri için ne zaman ve nasıl SNAT bağlantı noktalarını ayrılır ve nasıl bakın toomanage bu exhaustible kaynak.
