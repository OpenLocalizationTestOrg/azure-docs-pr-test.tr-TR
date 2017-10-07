---
title: "Azure yük dengeleyici VIP'ler aaaMultiple | Microsoft Docs"
description: "Azure yük dengeleyici üzerinde birden çok Vip genel bakış"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Azure Load Balancer için birden çok VIP

Azure yük dengeleyici tooload Hizmetleri birden çok bağlantı noktası, birden çok IP adresi veya her ikisi de sağlar. Sanal makineleri bir dizi arasında ortak ve iç yük dengeleyici tanımları tooload Bakiye akışları kullanabilirsiniz.

Bu makalede, bu özelliği, önemli kavramlar ve kısıtlamaları hello temelleri açıklanır. Bir IP adresi yalnızca tooexpose Hizmetleri düşünüyorsanız için Basitleştirilmiş yönergelerini bulabilirsiniz [ortak](load-balancer-get-started-internet-portal.md) veya [iç](load-balancer-get-started-ilb-arm-portal.md) yük dengeleyici yapılandırmalarının. Birden çok Vip ekleme artımlı tooa tek VIP yapılandırmadır. Bu makalede Hello kavramları kullanarak herhangi bir zamanda Basitleştirilmiş bir yapılandırma genişletebilirsiniz.

Bir Azure yük dengeleyici tanımladığınızda, bir ön uç ve arka uç yapılandırması kuralları ile bağlanır. Merhaba hello kuralı tarafından başvurulan durumu araştırması olduğu kullanılan toodetermine nasıl yeni akışları hello arka uç havuzundaki tooa düğümü gönderilir. Merhaba ön uç sanal IP (bir IP adresi (ortak veya dahili), Aktarım Protokolü (UDP veya TCP) ve bir bağlantı noktası numarası oluşan 3-tanımlama grubu olan bir VIP tarafından), tanımlanır. Bir DIP tooa VM hello arka uç havuzundaki bir Azure sanal NIC üzerinde bir IP adresine bağlı olur.

Aşağıdaki tablonun hello bazı örnek ön uç yapılandırmaları içerir:

| VIP | IP adresi | Protokolü | port |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

Merhaba tablo dört farklı ön uçlar gösterir. Ön Uçlar #1, #2 ve #3 birden çok kural ile tek bir VIP değerlerdir. Merhaba aynı IP adresi kullanılır ancak başlangıç bağlantı noktası veya protokolü her ön uç için farklıdır. Ön Uçlar #1 ve #4 burada hello aynı ön uç protokolü ve bağlantı noktası birden çok Vip tekrar birden çok Vip bir örnektir.

Azure yük dengeleyici hello Yük Dengeleme kuralları tanımlama esneklik sağlar. Bir kuralın nasıl bir adresi ve bağlantı noktası hello ön uçta olduğu eşlenen toohello hedef adresi ve bağlantı hello arka uç noktasına bildirir. Arka uç bağlantı noktaları kuralları yeniden hello kural hello türüne bağlıdır. Her kural türünün, ana bilgisayar yapılandırması ve araştırma tasarım etkileyebilir belirli gereksinimleri vardır. İki kural türü vardır:

1. Merhaba varsayılan kuralı arka uç bağlantı noktasıyla yeniden
2. arka uç bağlantı noktaları nerede tekrar hello kayan IP kuralı

Azure yük dengeleyici sağlar, her ikisi de kural türleri üzerinde toomix hello aynı yük dengeleyici yapılandırması. Merhaba kural hello kısıtlamalar tarafından uymanız sürece hello yük dengeleyici bunları aynı anda belirli bir VM veya herhangi bir birleşimini kullanabilirsiniz. Seçtiğiniz hangi kural türü bu yapılandırmayı destekleyen, uygulama ve hello karmaşıklığını hello gereksinimlerine bağlıdır. Hangi kural türlerinin senaryonuz için en iyi olduğunu değerlendirmelidir.

Biz bu senaryolar daha fazla hello varsayılan davranışı ile başlatarak keşfedin.

## <a name="rule-type-1-no-backend-port-reuse"></a>Kural türü #1: hiçbir arka uç bağlantı noktasını yeniden kullanma

![MultiVIP çizim](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

Bu senaryoda, hello ön uç VIP'ler yapılandırılmış olan aşağıdaki gibi:

| VIP | IP adresi | Protokolü | port |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Merhaba DIP hello hello hedefi olan gelen akış. Merhaba arka uç havuzundaki her VM benzersiz bir bağlantı noktası bir DIP üzerinde istenen hello hizmeti kullanıma sunar. Bu hizmet, bir kural tanımı aracılığıyla hello ön uç ile ilişkilidir.

Şu iki kural tanımlayın:

| Kural | Ön uç eşleme | toobackend havuzu |
| --- | --- | --- |
| 1 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![arka uç](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![arka uç](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![arka uç](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![arka uç](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

Azure yük dengeleyici tam eşlemesindeki Hello şimdi aşağıdaki gibidir:

| Kural | VIP IP adresi | Protokolü | port | Hedef | port |
| --- | --- | --- | --- | --- | --- |
| ![Kural](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |DIP IP adresi |80 |
| ![Kural](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |DIP IP adresi |81 |

Her kural benzersiz bir hedef IP adresi ve hedef bağlantı noktası birleşimi ile akışını üretmek gerekir. Değişen hello hedef bağlantı noktası hello akış tarafından birden çok kural farklı bağlantı noktalarını aynı DIP akışları toohello sunabilir.

Sistem durumu araştırmalarının her zaman yönlendirilmiş toohello VM DIP olur. Sağlamanız gerekir, araştırma hello VM hello durumunu yansıtır.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Kural türü #2: kayan IP kullanarak arka uç bağlantı noktasını yeniden kullanma

Azure yük dengeleyici kullanılan hello kural türü ne olursa olsun birden çok VIP'ler arasında tooreuse hello ön uç bağlantı noktası hello esneklik sağlar. Ayrıca, bazı uygulama senaryoları tercih veya hello aynı toobe hello arka uç havuzundaki tek bir VM üzerindeki birden çok uygulama örneği tarafından kullanılan bağlantı noktası gerektirir. Bağlantı noktası yeniden ortak örnekleri için yüksek kullanılabilirliği kümeleme içerir, ağ sanal Gereçleri ve birden çok TLS uç noktaları yeniden şifreleme olmadan gösterme.

Tooreuse hello arka uç bağlantı noktası birden çok kural istiyorsanız hello kural tanımı kayan IP etkinleştirmeniz gerekir.

Kayan IP, doğrudan sunucu Döndür (DSR olarak) bilinen bir bölümüdür. DSR iki bölümden oluşur: Eşleme Şeması bir akış topolojisi ve bir IP adresi. Bir platform düzeyde Azure yük dengeleyici DSR akış topolojisinde kayan IP etkin olup olmadığı bağımsız olarak her zaman çalışır. Bu hello giden akış parçası her zaman doğru bir şekilde yeniden tooflow doğrudan arka toohello kaynak anlamına gelir.

Merhaba varsayılan kural türüyle Azure geleneksel Yük Dengeleme kullanım kolaylığı için IP adresi eşleme şeması kullanıma sunar. Başlangıç IP adresi eşleme şeması tooallow aşağıda anlatıldığı gibi ek esneklik için etkinleştirme kayan IP değiştirir.

Aşağıdaki diyagramda hello bu yapılandırma gösterilmektedir:

![MultiVIP çizim](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

Bu senaryo için her VM hello arka uç havuzundaki üç ağ arabirimi bulunur:

* DIP: sanal hello VM (Azure'un NIC kaynak IP yapılandırması) ile ilişkili NIC
* Vıp1: bir geri döngü arabirimde Konuk vıp1 IP adresiyle yapılandırılmış işletim sistemi
* Vıp2: bir geri döngü arabirimde Konuk vıp2 IP adresiyle yapılandırılmış işletim sistemi

> [!IMPORTANT]
> Merhaba mantıksal arabirimlerinin Hello yapılandırmasını hello konuk işletim sistemi içinde gerçekleştirilir. Bu yapılandırma değil gerçekleştirilen veya Azure tarafından yönetiliyor. Bu yapılandırma olmazsa, hello kuralları çalışmayacaktır. Sistem durumu araştırma tanımları hello hello VM DIP kullanmak yerine mantıksal VIP hello. Bu nedenle, hizmetiniz hello mantıksal VIP hello sunulan hello hizmetinin durumunu yansıtacak bir DIP bağlantı noktasında araştırma yanıtları sağlamanız gerekir.

Merhaba varsayalım hello önceki senaryoda olduğu gibi aynı ön uç yapılandırma:

| VIP | IP adresi | Protokolü | port |
| --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Şu iki kural tanımlayın:

| Kural | Ön uç eşleme | toobackend havuzu |
| --- | --- | --- |
| 1 |![Kural](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![arka uç](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (içinde VM1 ve VM2) |
| 2 |![Kural](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![arka uç](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (içinde VM1 ve VM2) |

Aşağıdaki tablonun hello hello tam eşleme hello yük dengeleyicisi gösterir:

| Kural | VIP IP adresi | Protokolü | port | Hedef | port |
| --- | --- | --- | --- | --- | --- |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |VIP (65.52.0.1) ile aynı |VIP (80) aynı |
| ![VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |VIP (65.52.0.2) ile aynı |VIP (80) aynı |

Merhaba hedef Merhaba gelen akış hello VIP hello VM hello geri döngü arabirimindeki adresidir. Her kural benzersiz bir hedef IP adresi ve hedef bağlantı noktası birleşimi ile akışını üretmek gerekir. Değişen hello hedef IP adresi hello akış tarafından bağlantı noktası yeniden üzerinde mümkündür aynı VM hello. Sunulan toohello yük dengeleyici toohello VIP'ın IP adresi ve bağlantı noktası hello ilgili geri döngü arabiriminin bağlayarak hizmetidir.

Bu örnek hello hedef bağlantı noktası değiştirmez dikkat edin. Bu bir kayan IP senaryo olsa da, bir kural toorewrite hello arka uç hedef bağlantı noktası ve toomake tanımlama Azure yük dengeleyici de destekler, hello ön uç hedef bağlantı noktasından farklı.

Merhaba kayan IP kural türü hello birden fazla yük dengeleyici yapılandırması desenlerini temelini oluşturur. Şu anda kullanılabilir olan bir örnektir hello [SQL AlwaysOn ile birden çok dinleyici](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) yapılandırma. Zamanla, biz bu senaryoların birkaçı belge.

## <a name="limitations"></a>Sınırlamalar

* Birden çok VIP yapılandırmaları yalnızca Iaas VM'ler ile desteklenir.
* Hello kayan IP kuralıyla uygulamanız için giden trafik akışları hello DIP kullanmanız gerekir. Uygulamanızı hello geri döngü hello konuk işletim sistemi arabiriminde yapılandırılan toohello VIP adresi bağlar, ardından SNAT kullanılabilir toorewrite hello giden akış değildir ve hello akış başarısız olur.
* Genel IP adresleri faturalama üzerinde bir etkisi yoktur. Daha fazla bilgi için bkz: [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Abonelik sınırları uygulayın. Daha fazla bilgi için bkz: [hizmet sınırları](../azure-subscription-service-limits.md#networking-limits) Ayrıntılar için.
