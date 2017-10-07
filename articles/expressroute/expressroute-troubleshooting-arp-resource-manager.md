---
title: "ARP tabloları alınıyor: Resource Manager: Azure expressroute bağlantı sorunlarını giderme | Microsoft Docs"
description: "Bu sayfa yönergelerini alma hello ARP tablolar expressroute bağlantı hattı için sağlar"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>ARP tabloları hello Resource Manager dağıtım modelinde alınıyor
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Klasik](expressroute-troubleshooting-arp-classic.md)
> 
> 

Bu makalede, expressroute bağlantı hattı için ARP tabloları hello adımları toolearn hello anlatılmaktadır. 

> [!IMPORTANT]
> Bu belge tanılamak ve basit sorunları giderin hedeflenen toohelp değil. Hedeflenen toobe Microsoft destek için yenileme değildir. İle bir destek bileti açmanız gerekir [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) aşağıda açıklanan hello kılavuzu kullanarak oluşturulamıyor toosolve hello sorun olması durumunda.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Adres Çözümleme Protokolü (ARP) ve ARP tabloları
Adres Çözümleme Protokolü (ARP) tanımlanan bir protokolüdür Katman 2 [RFC 826](https://tools.ietf.org/html/rfc826). ARP kullanılan toomap hello Ethernet adresi (MAC adresi) bir IP adresine sahip olur.

Merhaba ARP tablosu hello IPv4 adresi ve belirli bir eşleme için MAC adresi eşlenmesini sağlar. Merhaba bir ExpressRoute bağlantı hattı eşlemesi için ARP tablosu (birincil ve ikincil) her arabirim için bilgisinden hello sağlar

1. Şirket içi yönlendirici arabirimi IP adresi toohello MAC adresi eşleme
2. ExpressRoute yönlendirici arabirimi IP adresi toohello MAC adresi eşleme
3. Merhaba eşleme yaşı

Temel sorun gidermeyi Katman 2 bağlantı sorunları ve Katman 2 yapılandırmasını doğrula ARP tabloları yardımcı olabilir. 

Örnek ARP tablosu: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Merhaba aşağıdaki bilgileri nasıl görüntüleyebileceğiniz üzerinde bölümde hello ExpressRoute sınır yönlendiricileri tarafından görülen ARP tabloları hello. 

## <a name="prerequisites-for-learning-arp-tables"></a>ARP tabloları öğrenme için Önkoşullar
Daha fazla ilerleme önce hello aşağıdaki sahip olduğundan emin olun

* En az bir eşleme ile yapılandırılmış bir geçerli expressroute bağlantı hattı. Merhaba hattı hello bağlantı sağlayıcı tarafından tam olarak yapılandırılması gerekir. Siz (veya bağlantı sağlayıcınız) hello eşlemeleri (Azure özel, Azure genel ve Microsoft) en az biri bu bağlantı hattındaki yapılandırmış olmanız gerekir.
* Merhaba eşlemeleri (Azure özel, Azure genel ve Microsoft) yapılandırmak için kullanılan IP adresi aralığı. Başlangıç IP adresi ataması hello örneklerde gözden [ExpressRoute yönlendirme gereksinimleri sayfa](expressroute-routing.md) tooget nasıl IP adreslerini olduğunun anlaşılması toointerfaces, tarafında ve hello ExpressRoute yan eşlenmiş. Merhaba gözden geçirerek hello eşleme yapılandırması hakkında bilgi alabilirsiniz [ExpressRoute eşleme yapılandırma sayfası](expressroute-howto-routing-arm.md).
* Ağ ekibinizin bilgilerinden / hello MAC adresleri arabirimlerin bağlantı sağlayıcı bu IP adresi ile kullanılır.
* Merhaba son PowerShell modülü Azure (1,50 ya da daha yeni sürümü) olmalıdır.

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Merhaba ARP tablolar expressroute bağlantı hattı için alınıyor
Bu bölüm, PowerShell kullanarak eşlemesi başına ARP tabloları nasıl görüntüleyebileceğiniz yönergeleri hello sağlar. Daha fazla İleri aşamalara önce hello eşliği, siz veya bağlantı sağlayıcınız yapılandırmış olmanız gerekir. Her bağlantı hattı (birincil ve ikincil) iki yolu vardır. Merhaba ARP tablosu her yolu için bağımsız olarak kontrol edebilirsiniz.

### <a name="arp-tables-for-azure-private-peering"></a>Azure özel eşleme için ARP tabloları
Azure özel eşleme için cmdlet aşağıdaki hello hello ARP tablolar sağlar

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Örnek çıktı hello yollarının biri aşağıda verilmiştir

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Azure genel eşliği ARP tabloları
Azure ortak eşleme için cmdlet aşağıdaki hello hello ARP tablolar sağlar

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Örnek çıktı hello yollarının biri aşağıda verilmiştir

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Microsoft eşlemesi için ARP tabloları
Microsoft eşlemesi için cmdlet aşağıdaki hello hello ARP tablolar sağlar

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Örnek çıktı hello yollarının biri aşağıda verilmiştir

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Nasıl toouse bu bilgileri
Merhaba bir eşlemenin ARP tablosu kullanılabilir toodetermine Katman 2 bağlantı ve doğrulayın. Bu bölümde, ARP tabloları farklı senaryolarda nasıl görüneceğine genel bir bakış sağlar.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Bir bağlantı hattı işlemsel durum (beklenen durumu) olduğunda ARP tablosu
* Merhaba ARP tablosu hello şirket içi yan geçerli bir IP adresi ve MAC adresi için bir giriş ve hello Microsoft yan için benzer bir giriş bulunur. 
* Merhaba son sekizli hello şirket içi IP adresinin her zaman tek sayı olacaktır.
* Merhaba Microsoft IP adresi son sekizlisi Hello her zaman bir çift sayı olacaktır.
* Merhaba aynı MAC adresi hello tüm 3 eşlemeleri (birincil / ikincil) için Microsoft tarafında görünür. 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>ARP tablosu şirket içi / bağlantı sağlayıcısı yan sorunlar var
Merhaba şirket içi sorunları vardır veya ya da yalnızca bir giriş ARP tablosu veya hello şirket içi MAC adresi hello görünür görebilirsiniz bağlantı sağlayıcı tamamlanmamış gösterecektir varsa. Bu hello MAC adresi ve hello Microsoft tarafında kullanılan IP adresi arasında hello eşlemeyi gösterir. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

or
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Bir destek isteği tür sorunlar, bağlantı sağlayıcısı toodebug ile açın. Merhaba ARP tablosu yoksa hello arabirimlerin IP adreslerini tooMAC adresleri, aşağıdaki bilgileri gözden geçirme hello eşlenmiş:
> 
> 1. Merhaba ilk IP adresi hello /30 alt arasında hello bağlantı için atanmışsa MSEE PR hello ve MSEE MSEE PR. hello arabirimde kullanılır Azure hello ikinci IP adresi Msee için her zaman kullanır.
> 2. Merhaba müşteri (C-etiketi) ve hizmet (S-Tag) VLAN etiketlerini hem MSEE PR ve MSEE çifti eşleşip eşleşmediğini denetleyin.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Microsoft yan sorunları olduğunda ARP tablosu
* Microsoft yan hello üzerinde sorunları varsa bir eşleme için gösterilen bir ARP tablosu görmezsiniz. 
* Bir destek bileti ile açmak [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Katman 2 bağlantı ile ilgili bir sorun olduğunu belirtin. 

## <a name="next-steps"></a>Sonraki Adımlar
* Expressroute bağlantı hattı için Katman 3 yapılandırmaları doğrula
  * Rota Özet toodetermine hello BGP oturumlarının durumunu alma 
  * Rota tablosu toodetermine ExpressRoute hangi ön eklerin tanıtılıp Al
* Veri aktarımı bayt giriş / çıkış gözden geçirerek doğrula
* Bir destek bileti ile açmak [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunları yaşamaya devam ediyorsanız.

