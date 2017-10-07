---
title: "ARP tabloları alınıyor: Klasik: Azure expressroute bağlantı sorunlarını giderme | Microsoft Docs"
description: "Bu sayfa, bir expressroute bağlantı hattı için tabloları alma hello ARP için yönergeler sağlar."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>ARP tabloları hello Klasik dağıtım modelinde alınıyor
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - Klasik](expressroute-troubleshooting-arp-classic.md)
> 
> 

Bu makalede, Azure ExpressRoute bağlantı hattınız için hello Adres Çözümleme Protokolü (ARP) tabloları alma hello adım adım anlatılmaktadır.

> [!IMPORTANT]
> Bu belge tanılamak ve basit sorunları giderin hedeflenen toohelp değil. Hedeflenen toobe Microsoft destek için yenileme değildir. Yönergeleri izleyerek hello kullanarak hello sorunu çözemiyorsanız, bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Adres Çözümleme Protokolü (ARP) ve ARP tabloları
ARP protokolüdür tanımlanan bir katman 2 [RFC 826](https://tools.ietf.org/html/rfc826). ARP kullanılan toomap bir Ethernet adresi (MAC adresi) tooan IP adresi olur.

Bir ARP tablosu hello IPv4 adresi ve belirli bir eşleme için MAC adresi eşlenmesini sağlar. Merhaba bir ExpressRoute bağlantı hattı eşlemesi için ARP tablosu (birincil ve ikincil) her arabirim için bilgisinden hello sağlar:

1. Bir şirket içi yönlendirici arabirimi IP adresi tooa MAC adresi eşleme
2. Bir ExpressRoute yönlendirici arabirimi IP adresi tooa MAC adresi eşleme
3. Merhaba yaş hello eşleme

ARP tabloları, Katman 2 yapılandırmasını doğrulama ve temel Katman 2 bağlantı sorunlarını giderme konusunda yardımcı olabilir.

ARP tablosu örneği aşağıdadır:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


bölümden hello nasıl tooview hello hello ExpressRoute sınır yönlendiricileri tarafından görülen ARP tabloları hakkında bilgi sağlar.

## <a name="prerequisites-for-using-arp-tables"></a>ARP tablolarını kullanma önkoşulları
Devam etmeden önce hello aşağıdaki sahip olduğundan emin olun:

* En az bir eşleme ile yapılandırılmış geçerli bir expressroute bağlantı hattı. Merhaba hattı hello bağlantı sağlayıcı tarafından tam olarak yapılandırılması gerekir. Siz (veya bağlantı sağlayıcınız) hello eşlemeleri (Azure özel, Azure genel ve Microsoft) en az biri bu bağlantı hattındaki yapılandırmanız gerekir.
* Merhaba eşlemeleri (Azure özel, Azure genel ve Microsoft) yapılandırmak için kullanılan IP adresi aralığı. Başlangıç IP adresi ataması hello örneklerde gözden [ExpressRoute yönlendirme gereksinimleri sayfa](expressroute-routing.md) tooget nasıl IP adreslerini olduğunun anlaşılması toointerfaces, aise ve hello ExpressRoute tarafında eşlenmiş. Merhaba gözden geçirerek hello eşleme yapılandırmasını hakkında bilgi edinebilirsiniz [ExpressRoute eşleme yapılandırma sayfası](expressroute-howto-routing-classic.md).
* Bu IP adresi ile kullanılan hello arabirimlerinin hello MAC adresleri hakkında bilgi ağ ekip veya bağlantı sağlayıcınızdan.
* Merhaba en son Windows PowerShell modülü Azure (1,50 veya sonraki bir sürümü).

## <a name="arp-tables-for-your-expressroute-circuit"></a>ARP tablolar expressroute bağlantı hattı için
Bu bölümde her tür PowerShell kullanarak eşliği için nasıl tooview hello ARP tabloları hakkında yönergeler sağlar. Devam etmeden önce veya bağlantı sağlayıcınız tooconfigure hello eşliği gerekiyor. Her bağlantı hattı (birincil ve ikincil) iki yolu vardır. Merhaba ARP tablosu her yolu için bağımsız olarak kontrol edebilirsiniz.

### <a name="arp-tables-for-azure-private-peering"></a>Azure özel eşleme için ARP tabloları
cmdlet aşağıdaki hello Azure özel eşleme için hello ARP tablolar sağlar:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Örnek çıktı hello yollarından biri, için aşağıda verilmiştir:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Azure ortak eşleme için ARP tablolar:
cmdlet aşağıdaki hello Azure ortak eşleme için hello ARP tablolar sağlar:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Örnek çıktı hello yollarından biri, için aşağıda verilmiştir:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Örnek çıktı hello yollarından biri, için aşağıda verilmiştir:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Microsoft eşlemesi için ARP tabloları
cmdlet aşağıdaki hello hello ARP Microsoft eşlemesi için tablolar sağlar:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Örnek çıktı hello yollarının biri aşağıda verilmiştir:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>Nasıl toouse bu bilgileri
Merhaba bir eşlemenin ARP tablosu kullanılan toovalidate Katman 2 bağlantı ve olabilir. Bu bölümde, ARP tabloları farklı senaryolarda nasıl göründüğünü genel bir bakış sağlar.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>Bir bağlantı hattı bir işlemsel (Beklenen) durumda olduğunda ARP tablosu
* Merhaba ARP tablosu hello şirket içi yan geçerli bir IP ve MAC adresi için bir giriş ve hello Microsoft yan için benzer bir giriş var.
* Merhaba son sekizli hello şirket içi IP adresinin her zaman tek bir sayıdır.
* Merhaba son hello Microsoft IP adresi sekizlisi her zaman bir çift sayı olup.
* Merhaba aynı MAC adresi hello üç eşlemenin tamamını (birincil/ikincil) için Microsoft tarafında görünür.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Şirket içi veya hello bağlantı sağlayıcı yan sorunları olduğunda olduğunda ARP tablosu
 Yalnızca bir giriş hello ARP tablosu görüntülenir. Merhaba MAC adresi ve Microsoft tarafında hello üzerinde kullanılan başlangıç IP adresi arasında hello eşlemeyi gösterir.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Böyle bir sorunla karşılaşırsanız, destek açın, bağlantı sağlayıcısı tooresolve ile istekte.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Merhaba Microsoft yan sorunları olduğunda ARP tablosu
* Microsoft yan hello üzerinde sorunları varsa bir eşleme için gösterilen bir ARP tablosu görmezsiniz.
* Bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Katman 2 bağlantı ile ilgili bir sorun olduğunu belirtin.

## <a name="next-steps"></a>Sonraki adımlar
* Expressroute bağlantı hattı için Katman 3 yapılandırmaları doğrulama:
  * BGP oturumlarını rota Özet toodetermine hello durumunu alın.
  * ExpressRoute hangi ön eklerin tanıtılıp rota tablosu toodetermine alın.
* Veri aktarımı bayt giriş ve çıkış gözden geçirerek doğrulayın.
* Bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunları yaşamaya devam ediyorsanız.

