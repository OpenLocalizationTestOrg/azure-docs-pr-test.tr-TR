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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="c04ce-103">ARP tabloları hello Resource Manager dağıtım modelinde alınıyor</span><span class="sxs-lookup"><span data-stu-id="c04ce-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c04ce-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c04ce-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="c04ce-105">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="c04ce-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="c04ce-106">Bu makalede, expressroute bağlantı hattı için ARP tabloları hello adımları toolearn hello anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c04ce-107">Bu belge tanılamak ve basit sorunları giderin hedeflenen toohelp değil.</span><span class="sxs-lookup"><span data-stu-id="c04ce-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="c04ce-108">Hedeflenen toobe Microsoft destek için yenileme değildir.</span><span class="sxs-lookup"><span data-stu-id="c04ce-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="c04ce-109">İle bir destek bileti açmanız gerekir [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) aşağıda açıklanan hello kılavuzu kullanarak oluşturulamıyor toosolve hello sorun olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="c04ce-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="c04ce-110">Adres Çözümleme Protokolü (ARP) ve ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="c04ce-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="c04ce-111">Adres Çözümleme Protokolü (ARP) tanımlanan bir protokolüdür Katman 2 [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="c04ce-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="c04ce-112">ARP kullanılan toomap hello Ethernet adresi (MAC adresi) bir IP adresine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c04ce-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="c04ce-113">Merhaba ARP tablosu hello IPv4 adresi ve belirli bir eşleme için MAC adresi eşlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c04ce-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="c04ce-114">Merhaba bir ExpressRoute bağlantı hattı eşlemesi için ARP tablosu (birincil ve ikincil) her arabirim için bilgisinden hello sağlar</span><span class="sxs-lookup"><span data-stu-id="c04ce-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="c04ce-115">Şirket içi yönlendirici arabirimi IP adresi toohello MAC adresi eşleme</span><span class="sxs-lookup"><span data-stu-id="c04ce-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="c04ce-116">ExpressRoute yönlendirici arabirimi IP adresi toohello MAC adresi eşleme</span><span class="sxs-lookup"><span data-stu-id="c04ce-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="c04ce-117">Merhaba eşleme yaşı</span><span class="sxs-lookup"><span data-stu-id="c04ce-117">Age of hello mapping</span></span>

<span data-ttu-id="c04ce-118">Temel sorun gidermeyi Katman 2 bağlantı sorunları ve Katman 2 yapılandırmasını doğrula ARP tabloları yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c04ce-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="c04ce-119">Örnek ARP tablosu:</span><span class="sxs-lookup"><span data-stu-id="c04ce-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="c04ce-120">Merhaba aşağıdaki bilgileri nasıl görüntüleyebileceğiniz üzerinde bölümde hello ExpressRoute sınır yönlendiricileri tarafından görülen ARP tabloları hello.</span><span class="sxs-lookup"><span data-stu-id="c04ce-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="c04ce-121">ARP tabloları öğrenme için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c04ce-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="c04ce-122">Daha fazla ilerleme önce hello aşağıdaki sahip olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="c04ce-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="c04ce-123">En az bir eşleme ile yapılandırılmış bir geçerli expressroute bağlantı hattı.</span><span class="sxs-lookup"><span data-stu-id="c04ce-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="c04ce-124">Merhaba hattı hello bağlantı sağlayıcı tarafından tam olarak yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c04ce-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="c04ce-125">Siz (veya bağlantı sağlayıcınız) hello eşlemeleri (Azure özel, Azure genel ve Microsoft) en az biri bu bağlantı hattındaki yapılandırmış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c04ce-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="c04ce-126">Merhaba eşlemeleri (Azure özel, Azure genel ve Microsoft) yapılandırmak için kullanılan IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="c04ce-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="c04ce-127">Başlangıç IP adresi ataması hello örneklerde gözden [ExpressRoute yönlendirme gereksinimleri sayfa](expressroute-routing.md) tooget nasıl IP adreslerini olduğunun anlaşılması toointerfaces, tarafında ve hello ExpressRoute yan eşlenmiş.</span><span class="sxs-lookup"><span data-stu-id="c04ce-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="c04ce-128">Merhaba gözden geçirerek hello eşleme yapılandırması hakkında bilgi alabilirsiniz [ExpressRoute eşleme yapılandırma sayfası](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c04ce-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="c04ce-129">Ağ ekibinizin bilgilerinden / hello MAC adresleri arabirimlerin bağlantı sağlayıcı bu IP adresi ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="c04ce-130">Merhaba son PowerShell modülü Azure (1,50 ya da daha yeni sürümü) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="c04ce-131">Merhaba ARP tablolar expressroute bağlantı hattı için alınıyor</span><span class="sxs-lookup"><span data-stu-id="c04ce-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="c04ce-132">Bu bölüm, PowerShell kullanarak eşlemesi başına ARP tabloları nasıl görüntüleyebileceğiniz yönergeleri hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="c04ce-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="c04ce-133">Daha fazla İleri aşamalara önce hello eşliği, siz veya bağlantı sağlayıcınız yapılandırmış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c04ce-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="c04ce-134">Her bağlantı hattı (birincil ve ikincil) iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="c04ce-135">Merhaba ARP tablosu her yolu için bağımsız olarak kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c04ce-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="c04ce-136">Azure özel eşleme için ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="c04ce-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="c04ce-137">Azure özel eşleme için cmdlet aşağıdaki hello hello ARP tablolar sağlar</span><span class="sxs-lookup"><span data-stu-id="c04ce-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="c04ce-138">Örnek çıktı hello yollarının biri aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="c04ce-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="c04ce-139">Azure genel eşliği ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="c04ce-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="c04ce-140">Azure ortak eşleme için cmdlet aşağıdaki hello hello ARP tablolar sağlar</span><span class="sxs-lookup"><span data-stu-id="c04ce-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="c04ce-141">Örnek çıktı hello yollarının biri aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="c04ce-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="c04ce-142">Microsoft eşlemesi için ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="c04ce-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="c04ce-143">Microsoft eşlemesi için cmdlet aşağıdaki hello hello ARP tablolar sağlar</span><span class="sxs-lookup"><span data-stu-id="c04ce-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="c04ce-144">Örnek çıktı hello yollarının biri aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="c04ce-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="c04ce-145">Nasıl toouse bu bilgileri</span><span class="sxs-lookup"><span data-stu-id="c04ce-145">How toouse this information</span></span>
<span data-ttu-id="c04ce-146">Merhaba bir eşlemenin ARP tablosu kullanılabilir toodetermine Katman 2 bağlantı ve doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c04ce-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="c04ce-147">Bu bölümde, ARP tabloları farklı senaryolarda nasıl görüneceğine genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="c04ce-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="c04ce-148">Bir bağlantı hattı işlemsel durum (beklenen durumu) olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="c04ce-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="c04ce-149">Merhaba ARP tablosu hello şirket içi yan geçerli bir IP adresi ve MAC adresi için bir giriş ve hello Microsoft yan için benzer bir giriş bulunur.</span><span class="sxs-lookup"><span data-stu-id="c04ce-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="c04ce-150">Merhaba son sekizli hello şirket içi IP adresinin her zaman tek sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="c04ce-151">Merhaba Microsoft IP adresi son sekizlisi Hello her zaman bir çift sayı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="c04ce-152">Merhaba aynı MAC adresi hello tüm 3 eşlemeleri (birincil / ikincil) için Microsoft tarafında görünür.</span><span class="sxs-lookup"><span data-stu-id="c04ce-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="c04ce-153">ARP tablosu şirket içi / bağlantı sağlayıcısı yan sorunlar var</span><span class="sxs-lookup"><span data-stu-id="c04ce-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="c04ce-154">Merhaba şirket içi sorunları vardır veya ya da yalnızca bir giriş ARP tablosu veya hello şirket içi MAC adresi hello görünür görebilirsiniz bağlantı sağlayıcı tamamlanmamış gösterecektir varsa.</span><span class="sxs-lookup"><span data-stu-id="c04ce-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="c04ce-155">Bu hello MAC adresi ve hello Microsoft tarafında kullanılan IP adresi arasında hello eşlemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="c04ce-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="c04ce-156">or</span><span class="sxs-lookup"><span data-stu-id="c04ce-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="c04ce-157">Bir destek isteği tür sorunlar, bağlantı sağlayıcısı toodebug ile açın.</span><span class="sxs-lookup"><span data-stu-id="c04ce-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="c04ce-158">Merhaba ARP tablosu yoksa hello arabirimlerin IP adreslerini tooMAC adresleri, aşağıdaki bilgileri gözden geçirme hello eşlenmiş:</span><span class="sxs-lookup"><span data-stu-id="c04ce-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="c04ce-159">Merhaba ilk IP adresi hello /30 alt arasında hello bağlantı için atanmışsa MSEE PR hello ve MSEE MSEE PR. hello arabirimde kullanılır</span><span class="sxs-lookup"><span data-stu-id="c04ce-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="c04ce-160">Azure hello ikinci IP adresi Msee için her zaman kullanır.</span><span class="sxs-lookup"><span data-stu-id="c04ce-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="c04ce-161">Merhaba müşteri (C-etiketi) ve hizmet (S-Tag) VLAN etiketlerini hem MSEE PR ve MSEE çifti eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c04ce-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="c04ce-162">Microsoft yan sorunları olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="c04ce-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="c04ce-163">Microsoft yan hello üzerinde sorunları varsa bir eşleme için gösterilen bir ARP tablosu görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c04ce-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="c04ce-164">Bir destek bileti ile açmak [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="c04ce-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="c04ce-165">Katman 2 bağlantı ile ilgili bir sorun olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="c04ce-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c04ce-166">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c04ce-166">Next Steps</span></span>
* <span data-ttu-id="c04ce-167">Expressroute bağlantı hattı için Katman 3 yapılandırmaları doğrula</span><span class="sxs-lookup"><span data-stu-id="c04ce-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="c04ce-168">Rota Özet toodetermine hello BGP oturumlarının durumunu alma</span><span class="sxs-lookup"><span data-stu-id="c04ce-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="c04ce-169">Rota tablosu toodetermine ExpressRoute hangi ön eklerin tanıtılıp Al</span><span class="sxs-lookup"><span data-stu-id="c04ce-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="c04ce-170">Veri aktarımı bayt giriş / çıkış gözden geçirerek doğrula</span><span class="sxs-lookup"><span data-stu-id="c04ce-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="c04ce-171">Bir destek bileti ile açmak [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunları yaşamaya devam ediyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c04ce-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

