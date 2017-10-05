---
title: "Azure'da giden bağlantılar anlama | Microsoft Docs"
description: "Bu makalede, Azure ortak Internet Hizmetleri ile iletişim kurmak sanal makineleri nasıl sağladığını açıklar."
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
ms.openlocfilehash: 03cb14b5710b6dd17599a3c4eab21380c76c2b40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Azure’da giden bağlantıları anlama

Azure'da bir sanal makine (VM) dışında Azure ortak IP adres alanındaki uç noktalar ile iletişim kurabilir. Bir VM ortak IP adresi alanı içindeki bir hedefe giden bir akışı başlattığında, Azure VM'in özel IP adresi genel bir IP adresi eşler ve VM ulaşmak dönüş trafiğine izin verir.

Azure giden bağlantı ulaşmak için üç farklı yöntem sağlar. Her yöntemin kendine özgü özellikleri ve sınırlamaları vardır. Hangisinin ihtiyaçlarınıza uygun dikkatle seçmek için her bir yöntemi gözden geçirin.

| Senaryo | Yöntem | Not |
| --- | --- | --- |
| Tek başına VM (yük dengeleyici, örnek düzeyinde ortak IP adresi yok) |Varsayılan SNAT |Azure genel bir IP adresi için SNAT ilişkilendirir. |
| VM Yük Dengelemesi (VM üzerinde örnek düzeyinde ortak IP adres yok) |Yük Dengeleyici kullanarak SNAT |Azure yük dengeleyicinin genel bir IP adresi için SNAT kullanır. |
| VM örnek düzeyinde ortak IP adresiyle (ile veya yük dengeleyici olmadan) |SNAT kullanılmıyor |Azure VM'ye atanan genel IP kullanır |

Azure ortak IP adres alanındaki dışında uç noktalar ile iletişim kurmak için bir VM istemiyorsanız erişimi engellemek için ağ güvenlik grupları (NSG) kullanabilirsiniz. Nsg'leri kullanarak ele alınmıştır daha ayrıntılı olarak [önleme ortak bağlantısını](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Örnek düzeyinde ortak IP adresi olmayan tek başına VM

Bu senaryoda, VM Azure yük dengeleyici havuzu parçası olmayan ve kendisine atanmış bir örnek düzeyinde ortak IP (ILPIP) adresi yok. VM giden akış oluşturduğunda, Azure ortak kaynak IP adresine giden akış özel kaynak IP adresi çevirir. Bu giden akış için kullanılan ortak IP adresi yapılandırılabilir değildir ve aboneliğin ortak IP kaynak sınırınızı sayılmaz. Azure kaynak ağ adresi çevirisi (SNAT) bu işlemi gerçekleştirmek için kullanır. Ortak IP adresinin kısa ömürlü bağlantı noktaları, tek tek akışları VM tarafından kaynaklanan ayırt etmek için kullanılır. Akışları oluşturduğunuzda SNAT kısa ömürlü bağlantı noktaları dinamik olarak ayırır. Bu bağlamda snat Uygulamanız için kullanılan kısa ömürlü bağlantı noktaları SNAT bağlantı noktaları denir.

SNAT bağlantı noktalarını tükenmiş olabilir sınırlı bir kaynaktır. Nasıl tüketildiğinin anlamak önemlidir. Bir SNAT bağlantı noktası tek hedef IP adresine akış başına kullanılır. Aynı hedef IP adresi için birden çok akışlar için her bir akışa tek bir SNAT bağlantı noktasını kullanır. Bu akış aynı hedef IP adresine aynı ortak IP adresinden kaynaklanan zaman benzersiz olmasını sağlar. Birden çok akışları her farklı bir hedef IP adresine tüketen hedef başına tek bir SNAT bağlantı noktası. Hedef IP adresi akışları benzersiz hale getirir.

Kullanabileceğiniz [yük dengeleyici için günlük analizi](load-balancer-monitor-log.md) ve [snat Uygulamanız için izleme için uyarı olay günlüklerini bağlantı noktası Tükenme iletileri](load-balancer-monitor-log.md#alert-event-log). SNAT bağlantı noktası kaynakları tükendi SNAT bağlantı noktaları tarafından varolan akışları serbest bırakılana kadar giden trafik akışları yük devredersiniz. Yük Dengeleyici SNAT bağlantı noktalarını geri kazanma için 4 dakikalık boşta kalma zaman aşımı kullanır.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Hiçbir örnek düzeyinde ortak IP adresine sahip yük dengeli VM

Bu senaryoda, VM Azure yük dengeleyici havuzu bir parçasıdır.  VM, kendisine atanmış bir ortak IP adresi yok. Yük Dengeleyici kaynak ortak IP ön uç arka uç havuzu ile bağlamak için bir kural ile yapılandırılmalıdır.  Bu yapılandırma tamamlamazsanız bölümünde açıklandığı gibi davranıştır [hiçbir örnek düzeyinde ortak IP ile tek başına VM](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Yük dengeli VM giden akış oluşturduğunda, Azure ortak yük dengeleyici ön uç genel IP adresine giden akış özel kaynak IP adresi çevirir. Azure kaynak ağ adresi çevirisi (SNAT) bu işlemi gerçekleştirmek için kullanır. Yük dengeleyicinin genel IP adresi kısa ömürlü bağlantı noktaları, VM tarafından kaynaklanan tek tek akışları ayırt etmek için kullanılır. Giden trafik akışları oluşturduğunuzda SNAT kısa ömürlü bağlantı noktaları dinamik olarak ayırır. Bu bağlamda snat Uygulamanız için kullanılan kısa ömürlü bağlantı noktaları SNAT bağlantı noktaları denir.

SNAT bağlantı noktalarını tükenmiş olabilir sınırlı bir kaynaktır. Nasıl tüketildiğinin anlamak önemlidir. Bir SNAT bağlantı noktası tek hedef IP adresine akış başına kullanılır. Aynı hedef IP adresi için birden çok akışlar için her bir akışa tek bir SNAT bağlantı noktasını kullanır. Bu akış aynı hedef IP adresine aynı ortak IP adresinden kaynaklanan zaman benzersiz olmasını sağlar. Birden çok akışları her farklı bir hedef IP adresine tüketen hedef başına tek bir SNAT bağlantı noktası. Hedef IP adresi akışları benzersiz hale getirir.

Kullanabileceğiniz [yük dengeleyici için günlük analizi](load-balancer-monitor-log.md) ve [snat Uygulamanız için izleme için uyarı olay günlüklerini bağlantı noktası Tükenme iletileri](load-balancer-monitor-log.md#alert-event-log). SNAT bağlantı noktası kaynakları tükendi SNAT bağlantı noktaları tarafından varolan akışları serbest bırakılana kadar giden trafik akışları yük devredersiniz. Yük Dengeleyici SNAT bağlantı noktalarını geri kazanma için 4 dakikalık boşta kalma zaman aşımı kullanır.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Örnek düzeyinde ortak IP adresi (ile veya yük dengeleyici olmadan) olan VM

Bu senaryoda, VM bir örnek düzeyinde ortak IP (atanmış ILPIP) sahiptir. VM veya dengelendiği olup önemli değildir. Bir ILPIP kullanıldığında, kaynak ağ adresi çevirisi (SNAT) kullanılmaz. VM için tüm giden trafik akışları ILPIP kullanır. Uygulamanız çok sayıda giden trafik akışları başlatır ve SNAT Tükenme deneyimi, SNAT kısıtlamalarının önüne geçmek için bir ILPIP atama düşünmelisiniz.

## <a name="discovering-the-public-ip-used-by-a-given-vm"></a>Belirli bir VM tarafından kullanılan genel IP bulma

Giden bir bağlantıyı ortak kaynak IP adresi belirlemek için birçok yolu vardır. OpenDNS VM ortak IP adresini gösteren bir hizmet sunar. Nslookup komutunu kullanarak, ad myip.opendns.com için bir DNS sorgusu OpenDNS çözümleyici gönderebilirsiniz. Hizmet sorguyu göndermek için kullanılan kaynak IP adresini döndürür. Sanal makineden aşağıdaki sorguyu çalıştırın, yanıt o VM için kullanılan genel IP değildir.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Genel bağlantı önleme

Bazen bir çıkış akışı oluşturmak için izin verilmesi bir VM için istenmeyen veya hangi hedefleri giden trafik akışları ile ulaşılabilen yönetmek için bir zorunluluk olabilir. Bu durumda, kullandığınız [ağ güvenlik grupları (NSG)](../virtual-network/virtual-networks-nsg.md) VM ulaşabilir hedefleri yönetmek için. Yük dengeli bir VM için bir NSG uyguladığınızda, dikkat edilmesi gereken [varsayılan etiketleri](../virtual-network/virtual-networks-nsg.md#default-tags) ve [varsayılan kuralları](../virtual-network/virtual-networks-nsg.md#default-rules).

VM, sistem durumu araştırma isteklerine Azure yük Dengeleyiciden aldığından emin olmak gerekir. Bir NSG'yi sistem durumu araştırma AZURE_LOADBALANCER varsayılan etiket isteklerinden engelliyorsa VM durumu araştırması başarısız olur ve VM düşürüleceği. Yük Dengeleyici, bu VM için yeni akışları gönderme durdurur.

## <a name="limitations"></a>Sınırlamalar

Varsa [(Genel) birden çok IP adresi bir yük dengeleyici ile ilişkili](load-balancer-multivip-overview.md), herhangi bir aday giden trafik akışları için bu ortak IP adresleridir.

Azure havuz boyutuna göre kullanılabilir SNAT bağlantı noktası sayısını belirlemek için bir algoritma kullanıyor.  Bu şu anda yapılandırılabilir değildir.

Kullanılabilir SNAT bağlantı noktası sayısını doğrudan bağlantı sayısını tercüme etmez rememember önemlidir. Lütfen nasıl ve ne zaman SNAT bağlantı noktalarını ayrılır ve bu exhaustible kaynak yönetme özellikleri için yukarıya bakın.
