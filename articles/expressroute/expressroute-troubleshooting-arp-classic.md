---
title: "ARP tabloları alınıyor: Klasik: Azure expressroute bağlantı sorunlarını giderme | Microsoft Docs"
description: "Bu sayfayı ARP tablolar için ExpressRoute devresi almak için yönergeler sağlar."
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
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="37d52-103">ARP tabloları Klasik dağıtım modelinde alınıyor</span><span class="sxs-lookup"><span data-stu-id="37d52-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37d52-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37d52-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="37d52-105">PowerShell - Klasik</span><span class="sxs-lookup"><span data-stu-id="37d52-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="37d52-106">Bu makalede, Azure ExpressRoute bağlantı hattınız için Adres Çözümleme Protokolü (ARP) tabloları almak için adım adım anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="37d52-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37d52-107">Bu belge, tanılamak ve basit sorunları gidermenize yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="37d52-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="37d52-108">Microsoft destek için yenileme olması amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="37d52-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="37d52-109">Aşağıdaki yönergeleri kullanarak sorunu çözemiyorsanız, bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="37d52-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="37d52-110">Adres Çözümleme Protokolü (ARP) ve ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="37d52-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="37d52-111">ARP protokolüdür tanımlanan bir katman 2 [RFC 826](https://tools.ietf.org/html/rfc826).</span><span class="sxs-lookup"><span data-stu-id="37d52-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="37d52-112">ARP Ethernet adresi (MAC adresi) bir IP adresine eşlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="37d52-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="37d52-113">Bir ARP tablosu IPv4 adresi ve belirli bir eşleme için MAC adresi eşlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="37d52-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="37d52-114">Bir ExpressRoute bağlantı hattı eşlemesi için ARP tablosu (birincil ve ikincil) her arabirim için aşağıdaki bilgileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="37d52-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="37d52-115">Bir şirket içi yönlendirici arabirimi IP adresi için bir MAC adresi eşleme</span><span class="sxs-lookup"><span data-stu-id="37d52-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="37d52-116">Bir ExpressRoute yönlendirici arabirimi IP adresi için bir MAC adresi eşleme</span><span class="sxs-lookup"><span data-stu-id="37d52-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="37d52-117">Eşleme yaşı</span><span class="sxs-lookup"><span data-stu-id="37d52-117">The age of the mapping</span></span>

<span data-ttu-id="37d52-118">ARP tabloları, Katman 2 yapılandırmasını doğrulama ve temel Katman 2 bağlantı sorunlarını giderme konusunda yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="37d52-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="37d52-119">ARP tablosu örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="37d52-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="37d52-120">Aşağıdaki bölümde ExpressRoute sınır yönlendiricileri tarafından görülen ARP tabloları görüntüleme hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="37d52-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="37d52-121">ARP tablolarını kullanma önkoşulları</span><span class="sxs-lookup"><span data-stu-id="37d52-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="37d52-122">Devam etmeden önce aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="37d52-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="37d52-123">En az bir eşleme ile yapılandırılmış geçerli bir expressroute bağlantı hattı.</span><span class="sxs-lookup"><span data-stu-id="37d52-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="37d52-124">Bağlantı hattı bağlantı sağlayıcı tarafından tam olarak yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="37d52-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="37d52-125">Siz (veya bağlantı sağlayıcınız) eşlemeleri (Azure özel, Azure genel ve Microsoft) en az biri bu bağlantı hattındaki yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="37d52-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="37d52-126">(Azure özel, Azure genel ve Microsoft) eşlemeleri yapılandırmak için kullanılan IP adresi aralığı.</span><span class="sxs-lookup"><span data-stu-id="37d52-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="37d52-127">IP adresi ataması örneklerde gözden [ExpressRoute yönlendirme gereksinimleri sayfa](expressroute-routing.md) arabirimlerine, aise ve ExpressRoute tarafında IP adreslerinin nasıl eşlendiğini bir anlamak için.</span><span class="sxs-lookup"><span data-stu-id="37d52-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="37d52-128">Eşleme yapılandırmasını hakkındaki bilgileri gözden geçirerek alabilir [ExpressRoute eşleme yapılandırma sayfası](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="37d52-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="37d52-129">Bu IP adresi ile kullanılan arabirimlerin MAC adresleri hakkında bilgi ağ ekip veya bağlantı sağlayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="37d52-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="37d52-130">Azure (sürüm 1,50 veya sonrası) için en son Windows PowerShell modülü.</span><span class="sxs-lookup"><span data-stu-id="37d52-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="37d52-131">ARP tablolar expressroute bağlantı hattı için</span><span class="sxs-lookup"><span data-stu-id="37d52-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="37d52-132">Bu bölümde her tür PowerShell kullanarak eşliği için ARP tabloları görüntüleme hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="37d52-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="37d52-133">Devam etmeden önce eşlemesini yapılandırmak üzere siz veya bağlantı sağlayıcınız gerekir.</span><span class="sxs-lookup"><span data-stu-id="37d52-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="37d52-134">Her bağlantı hattı (birincil ve ikincil) iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="37d52-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="37d52-135">Her yol ARP tablosu bağımsız olarak kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37d52-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="37d52-136">Azure özel eşleme için ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="37d52-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="37d52-137">Aşağıdaki cmdlet'i ARP Azure özel eşleme için tablolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="37d52-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="37d52-138">Örnek çıktı yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="37d52-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="37d52-139">Azure ortak eşleme için ARP tablolar:</span><span class="sxs-lookup"><span data-stu-id="37d52-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="37d52-140">Aşağıdaki cmdlet'i ARP Azure ortak eşleme için tablolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="37d52-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="37d52-141">Örnek çıktı yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="37d52-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="37d52-142">Örnek çıktı yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="37d52-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="37d52-143">Microsoft eşlemesi için ARP tabloları</span><span class="sxs-lookup"><span data-stu-id="37d52-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="37d52-144">Aşağıdaki cmdlet'i ARP Microsoft eşlemesi için tablolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="37d52-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="37d52-145">Örnek çıktı yollarından biri, için aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="37d52-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="37d52-146">Bu bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="37d52-146">How to use this information</span></span>
<span data-ttu-id="37d52-147">Bir eşlemenin ARP tablosu, Katman 2 bağlantı ve doğrulamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="37d52-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="37d52-148">Bu bölümde, ARP tabloları farklı senaryolarda nasıl göründüğünü genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="37d52-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="37d52-149">Bir bağlantı hattı bir işlemsel (Beklenen) durumda olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="37d52-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="37d52-150">ARP tablosu, şirket içi yan geçerli bir IP ve MAC adresi için bir giriş ve Microsoft tarafı için benzer bir giriş vardır.</span><span class="sxs-lookup"><span data-stu-id="37d52-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="37d52-151">Şirket içi IP adresinin son sekizlisi her zaman tek bir sayıdır.</span><span class="sxs-lookup"><span data-stu-id="37d52-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="37d52-152">Microsoft IP adresinin son sekizlisi her zaman bir çift sayı olup.</span><span class="sxs-lookup"><span data-stu-id="37d52-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="37d52-153">Aynı MAC adresi (birincil/ikincil) üç eşlemenin tamamını Microsoft tarafında görünür.</span><span class="sxs-lookup"><span data-stu-id="37d52-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="37d52-154">Şirket içi veya bağlantı sağlayıcı yan sorunları olduğunda olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="37d52-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="37d52-155">Yalnızca bir giriş ARP tabloda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="37d52-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="37d52-156">MAC adresi ve Microsoft tarafında kullanılan IP adresi arasındaki eşlemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="37d52-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="37d52-157">Böyle bir sorunla karşılaşırsanız, bunu çözmek için bağlantı sağlayıcınız ile bir destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="37d52-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="37d52-158">Microsoft yan sorunları olduğunda ARP tablosu</span><span class="sxs-lookup"><span data-stu-id="37d52-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="37d52-159">Microsoft tarafında sorunları varsa bir eşleme için gösterilen bir ARP tablosu görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="37d52-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="37d52-160">Bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="37d52-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="37d52-161">Katman 2 bağlantı ile ilgili bir sorun olduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="37d52-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37d52-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37d52-162">Next steps</span></span>
* <span data-ttu-id="37d52-163">Expressroute bağlantı hattı için Katman 3 yapılandırmaları doğrulama:</span><span class="sxs-lookup"><span data-stu-id="37d52-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="37d52-164">Bir rota BGP oturumlarının durumunu belirlemek için Özet alın.</span><span class="sxs-lookup"><span data-stu-id="37d52-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="37d52-165">ExpressRoute hangi ön eklerin tanıtılıp belirlemek için bir yol tablosu alın.</span><span class="sxs-lookup"><span data-stu-id="37d52-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="37d52-166">Veri aktarımı bayt giriş ve çıkış gözden geçirerek doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="37d52-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="37d52-167">Bir destek isteği açın [Microsoft Azure Yardım + Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunları yaşamaya devam ediyorsanız.</span><span class="sxs-lookup"><span data-stu-id="37d52-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

