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
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="ef1ba-103">ARP tabloları hello Klasik dağıtım modelinde alınıyor</span><span class="sxs-lookup"><span data-stu-id="ef1ba-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef1ba-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ef1ba-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="ef1ba-105">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="ef1ba-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="ef1ba-106">Bu makalede, Azure ExpressRoute bağlantı hattınız için hello Adres Çözümleme Protokolü (ARP) tabloları alma hello adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef1ba-107">Bu belge tanılamak ve basit sorunları giderin hedeflenen toohelp değil.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="ef1ba-108">Hedeflenen toobe Microsoft destek için yenileme değildir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="ef1ba-109">Yönergeleri izleyerek hello kullanarak hello sorunu çözemiyorsanız, bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="ef1ba-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="ef1ba-110">Adres Çözümleme Protokolü (ARP) ve ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="ef1ba-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="ef1ba-111">ARP protokolüdür tanımlanan bir katman 2 [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="ef1ba-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="ef1ba-112">ARP kullanılan toomap bir Ethernet adresi (MAC adresi) tooan IP adresi olur.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="ef1ba-113">Bir ARP tablosu hello IPv4 adresi ve belirli bir eşleme için MAC adresi eşlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="ef1ba-114">Merhaba bir ExpressRoute bağlantı hattı eşlemesi için ARP tablosu (birincil ve ikincil) her arabirim için bilgisinden hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="ef1ba-115">Bir şirket içi yönlendirici arabirimi IP adresi tooa MAC adresi eşleme</span><span class="sxs-lookup"><span data-stu-id="ef1ba-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="ef1ba-116">Bir ExpressRoute yönlendirici arabirimi IP adresi tooa MAC adresi eşleme</span><span class="sxs-lookup"><span data-stu-id="ef1ba-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="ef1ba-117">Merhaba yaş hello eşleme</span><span class="sxs-lookup"><span data-stu-id="ef1ba-117">hello age of hello mapping</span></span>

<span data-ttu-id="ef1ba-118">ARP tabloları, Katman 2 yapılandırmasını doğrulama ve temel Katman 2 bağlantı sorunlarını giderme konusunda yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="ef1ba-119">ARP tablosu örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="ef1ba-120">bölümden hello nasıl tooview hello hello ExpressRoute sınır yönlendiricileri tarafından görülen ARP tabloları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="ef1ba-121">ARP tablolarını kullanma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="ef1ba-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="ef1ba-122">Devam etmeden önce hello aşağıdaki sahip olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="ef1ba-123">En az bir eşleme ile yapılandırılmış geçerli bir expressroute bağlantı hattı.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="ef1ba-124">Merhaba hattı hello bağlantı sağlayıcı tarafından tam olarak yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="ef1ba-125">Siz (veya bağlantı sağlayıcınız) hello eşlemeleri (Azure özel, Azure genel ve Microsoft) en az biri bu bağlantı hattındaki yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="ef1ba-126">Merhaba eşlemeleri (Azure özel, Azure genel ve Microsoft) yapılandırmak için kullanılan IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="ef1ba-127">Başlangıç IP adresi ataması hello örneklerde gözden [ExpressRoute yönlendirme gereksinimleri sayfa](expressroute-routing.md) tooget nasıl IP adreslerini olduğunun anlaşılması toointerfaces, aise ve hello ExpressRoute tarafında eşlenmiş.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="ef1ba-128">Merhaba gözden geçirerek hello eşleme yapılandırmasını hakkında bilgi edinebilirsiniz [ExpressRoute eşleme yapılandırma sayfası](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="ef1ba-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="ef1ba-129">Bu IP adresi ile kullanılan hello arabirimlerinin hello MAC adresleri hakkında bilgi ağ ekip veya bağlantı sağlayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="ef1ba-130">Merhaba en son Windows PowerShell modülü Azure (1,50 veya sonraki bir sürümü).</span><span class="sxs-lookup"><span data-stu-id="ef1ba-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="ef1ba-131">ARP tablolar expressroute bağlantı hattı için</span><span class="sxs-lookup"><span data-stu-id="ef1ba-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="ef1ba-132">Bu bölümde her tür PowerShell kullanarak eşliği için nasıl tooview hello ARP tabloları hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="ef1ba-133">Devam etmeden önce veya bağlantı sağlayıcınız tooconfigure hello eşliği gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="ef1ba-134">Her bağlantı hattı (birincil ve ikincil) iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="ef1ba-135">Merhaba ARP tablosu her yolu için bağımsız olarak kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="ef1ba-136">Azure özel eşleme için ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="ef1ba-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="ef1ba-137">cmdlet aşağıdaki hello Azure özel eşleme için hello ARP tablolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="ef1ba-138">Örnek çıktı hello yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="ef1ba-139">Azure ortak eşleme için ARP tablolar:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="ef1ba-140">cmdlet aşağıdaki hello Azure ortak eşleme için hello ARP tablolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="ef1ba-141">Örnek çıktı hello yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="ef1ba-142">Örnek çıktı hello yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="ef1ba-143">Microsoft eşlemesi için ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="ef1ba-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="ef1ba-144">cmdlet aşağıdaki hello hello ARP Microsoft eşlemesi için tablolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="ef1ba-145">Örnek çıktı hello yollarının biri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="ef1ba-146">Nasıl toouse bu bilgileri</span><span class="sxs-lookup"><span data-stu-id="ef1ba-146">How toouse this information</span></span>
<span data-ttu-id="ef1ba-147">Merhaba bir eşlemenin ARP tablosu kullanılan toovalidate Katman 2 bağlantı ve olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="ef1ba-148">Bu bölümde, ARP tabloları farklı senaryolarda nasıl göründüğünü genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="ef1ba-149">Bir bağlantı hattı bir işlemsel (Beklenen) durumda olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="ef1ba-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="ef1ba-150">Merhaba ARP tablosu hello şirket içi yan geçerli bir IP ve MAC adresi için bir giriş ve hello Microsoft yan için benzer bir giriş var.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="ef1ba-151">Merhaba son sekizli hello şirket içi IP adresinin her zaman tek bir sayıdır.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="ef1ba-152">Merhaba son hello Microsoft IP adresi sekizlisi her zaman bir çift sayı olup.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="ef1ba-153">Merhaba aynı MAC adresi hello üç eşlemenin tamamını (birincil/ikincil) için Microsoft tarafında görünür.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="ef1ba-154">Şirket içi veya hello bağlantı sağlayıcı yan sorunları olduğunda olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="ef1ba-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="ef1ba-155">Yalnızca bir giriş hello ARP tablosu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="ef1ba-156">Merhaba MAC adresi ve Microsoft tarafında hello üzerinde kullanılan başlangıç IP adresi arasında hello eşlemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="ef1ba-157">Böyle bir sorunla karşılaşırsanız, destek açın, bağlantı sağlayıcısı tooresolve ile istekte.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="ef1ba-158">Merhaba Microsoft yan sorunları olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="ef1ba-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="ef1ba-159">Microsoft yan hello üzerinde sorunları varsa bir eşleme için gösterilen bir ARP tablosu görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="ef1ba-160">Bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="ef1ba-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="ef1ba-161">Katman 2 bağlantı ile ilgili bir sorun olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef1ba-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef1ba-162">Next steps</span></span>
* <span data-ttu-id="ef1ba-163">Expressroute bağlantı hattı için Katman 3 yapılandırmaları doğrulama:</span><span class="sxs-lookup"><span data-stu-id="ef1ba-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="ef1ba-164">BGP oturumlarını rota Özet toodetermine hello durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="ef1ba-165">ExpressRoute hangi ön eklerin tanıtılıp rota tablosu toodetermine alın.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="ef1ba-166">Veri aktarımı bayt giriş ve çıkış gözden geçirerek doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="ef1ba-167">Bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunları yaşamaya devam ediyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ef1ba-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

