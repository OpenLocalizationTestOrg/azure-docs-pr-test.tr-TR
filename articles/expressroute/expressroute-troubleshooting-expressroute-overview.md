---
title: "Doğrulanıyor bağlantısı: Sorun giderme kılavuzu Azure ExpressRoute | Microsoft Docs"
description: "Bu sayfa, sorun giderme ve bir expressroute bağlantı hattı son tooend bağlantısını doğrulama yönergelerini sağlar."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="7b654-103">ExpressRoute bağlantısı doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="7b654-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="7b654-104">Bir şirket içi ağ bağlantı sağlayıcı tarafından kolaylaştırılan özel bir bağlantı üzerinden Microsoft bulut hello genişletir, ExpressRoute üç farklı ağ bölgeleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="7b654-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="7b654-105">Müşteri ağ</span><span class="sxs-lookup"><span data-stu-id="7b654-105">Customer Network</span></span>
-   <span data-ttu-id="7b654-106">Sağlayıcı ağ</span><span class="sxs-lookup"><span data-stu-id="7b654-106">Provider Network</span></span>
-   <span data-ttu-id="7b654-107">Microsoft Veri merkezinde</span><span class="sxs-lookup"><span data-stu-id="7b654-107">Microsoft Datacenter</span></span>

<span data-ttu-id="7b654-108">Bu belgenin amacı Hello olduğu toohelp kullanıcı tooidentify nerede (veya bir olsa bile) bir bağlantı sorunu var ve hangi bölge içinde böylece tooseek Yardım uygun takım tooresolve hello sorundan.</span><span class="sxs-lookup"><span data-stu-id="7b654-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="7b654-109">Microsoft destek gerekli tooresolve bir sorun varsa, bir destek bileti ile açmak [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="7b654-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b654-110">Bu, hedeflenen toohelp tanılama ve basit sorunlarını giderme belgedir.</span><span class="sxs-lookup"><span data-stu-id="7b654-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="7b654-111">Hedeflenen toobe Microsoft destek için yenileme değildir.</span><span class="sxs-lookup"><span data-stu-id="7b654-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="7b654-112">Bir destek bileti ile açmak [Microsoft Support] [ Support] sağlanan hello yönergeleri kullanarak oluşturulamıyor toosolve hello sorun olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="7b654-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="7b654-113">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7b654-113">Overview</span></span>
<span data-ttu-id="7b654-114">Merhaba Aşağıdaki diyagramda hello mantıksal bağlantısını ExpressRoute kullanarak bir müşteri ağ tooMicrosoft ağ gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7b654-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="7b654-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="7b654-115">[![1]][1]</span></span>

<span data-ttu-id="7b654-116">Diyagram önceki hello hello sayılar anahtar ağ noktalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b654-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="7b654-117">Merhaba ağ noktaları genellikle ilişkili numaralarına göre bu makalede başvurulur.</span><span class="sxs-lookup"><span data-stu-id="7b654-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="7b654-118">Bağlı olarak Hello ExpressRoute bağlantı modeli (bulut Exchange birlikte bulundurma, noktadan noktaya Ethernet bağlantısı veya Any herhangi bir (IPVPN)) hello ağ noktalarını 3 ve 4 anahtarları (Katman 2 aygıtları) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="7b654-119">gösterilen hello anahtar ağ noktaları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7b654-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="7b654-120">Müşteri işlem aygıt (örneğin, bir sunucu veya bilgisayar)</span><span class="sxs-lookup"><span data-stu-id="7b654-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="7b654-121">CEs: Müşteri sınır yönlendiricileri</span><span class="sxs-lookup"><span data-stu-id="7b654-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="7b654-122">PEs (CE'e yönelik): sağlayıcısı sınır yönlendiricileri/müşteri sınır yönlendiricileri karşılıklı anahtarları.</span><span class="sxs-lookup"><span data-stu-id="7b654-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="7b654-123">Bu belgedeki tooas PE CEs denir.</span><span class="sxs-lookup"><span data-stu-id="7b654-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="7b654-124">PEs (MSEE'e yönelik): sağlayıcısı sınır yönlendiricileri/Msee'ler karşılıklı anahtarları.</span><span class="sxs-lookup"><span data-stu-id="7b654-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="7b654-125">Bu belgedeki tooas PE Msee'ler denir.</span><span class="sxs-lookup"><span data-stu-id="7b654-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="7b654-126">Msee'ler: Microsoft Enterprise Edge (MSEE) ExpressRoute yönlendiricileri</span><span class="sxs-lookup"><span data-stu-id="7b654-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="7b654-127">Sanal ağ (VNet) ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="7b654-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="7b654-128">Cihaz hello Azure VNet üzerinde işlem</span><span class="sxs-lookup"><span data-stu-id="7b654-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="7b654-129">Merhaba bulut Exchange birlikte bulundurma veya noktadan noktaya Ethernet bağlantısı bağlantı modeli kullanılıyorsa, hello müşteri sınır yönlendiricisi (2) BGP eşliği (5) Msee'ler ile oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="7b654-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="7b654-130">Ağ noktalarını 3 ve 4 hala var ancak katman 2 cihaz olarak biraz saydam.</span><span class="sxs-lookup"><span data-stu-id="7b654-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="7b654-131">Merhaba herhangi herhangi bir (IPVPN) bağlantı modeli kullanılıyorsa, PEs (MSEE'e yönelik) hello (4) BGP eşliği (5) Msee'ler ile kurmak.</span><span class="sxs-lookup"><span data-stu-id="7b654-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="7b654-132">Yollar sonra geri toohello müşteri ağ hello IPVPN hizmet sağlayıcısı ağ üzerinden yayılır.</span><span class="sxs-lookup"><span data-stu-id="7b654-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="7b654-133">ExpressRoute, yüksek kullanılabilirlik için yedek bir BGP oturumları Msee'ler (5) PE Msee'ler (4) arasındaki çift Microsoft gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7b654-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="7b654-134">Ağ yolları yedek çifti de müşteri ağ arasında PE CEs teşvik.</span><span class="sxs-lookup"><span data-stu-id="7b654-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="7b654-135">Ancak, herhangi herhangi bir (IPVPN) bağlantı modelinde, tek bir CE aygıt (2) bağlı tooone ya da daha fazla PEs (3) olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="7b654-136">toovalidate bir expressroute bağlantı hattı, aşağıdaki adımları hello (noktasıyla ilişkili hello sayıyla hello ağ) ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="7b654-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="7b654-137">Bağlantı hattı hazırlama ve durumu (5) doğrula</span><span class="sxs-lookup"><span data-stu-id="7b654-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="7b654-138">En az bir ExpressRoute doğrulamak eşliği, yapılandırılmış (5)</span><span class="sxs-lookup"><span data-stu-id="7b654-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="7b654-139">Microsoft ve hello hizmet sağlayıcısı (bağlantı 4 ve 5 arasında) arasında ARP doğrula</span><span class="sxs-lookup"><span data-stu-id="7b654-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="7b654-140">BGP ve hello MSEE (BGP 4 too5 VNet bağlıysa, 5 too6 arasındaki) yollara doğrula</span><span class="sxs-lookup"><span data-stu-id="7b654-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="7b654-141">Onay hello trafiği istatistikleri (trafik 5'ten geçirme)</span><span class="sxs-lookup"><span data-stu-id="7b654-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="7b654-142">Daha fazla doğrulama ve denetimleri hello gelecekteki iade geri aylık eklenecek!</span><span class="sxs-lookup"><span data-stu-id="7b654-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="7b654-143">Bağlantı hattı hazırlama ve durumunu doğrula</span><span class="sxs-lookup"><span data-stu-id="7b654-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="7b654-144">Oluşturulan toobe ve bu nedenle hizmet Hello bağlantı modeli bağımsız olarak, bir expressroute bağlantı hattı sahip devre sağlama için oluşturulan anahtarı.</span><span class="sxs-lookup"><span data-stu-id="7b654-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="7b654-145">Bir expressroute bağlantı hattı sağlama PE Msee'ler (4) ve Msee'ler (5) arasında yedekli bir katman 2 bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="7b654-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="7b654-146">Hello makale nasıl toocreate, değiştirme, sağlamak ve bir expressroute bağlantı hattı doğrulayın daha fazla bilgi için bkz: [oluşturma ve bir expressroute bağlantı hattı değiştirme][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="7b654-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="7b654-147">Bir hizmet anahtarı, bir expressroute bağlantı hattı benzersiz olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7b654-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="7b654-148">Bu belgede belirtilen hello powershell komutların çoğu için bu anahtar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7b654-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="7b654-149">Ayrıca, Yardım ihtiyacınız olursa Microsoft'tan ya da bir expressroute bağlantı ortağı tootroubleshoot bir ExpressRoute sorun, hello hizmet sağlamak anahtar tooreadily hello hattı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7b654-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="7b654-150">Hello Azure portal aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="7b654-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="7b654-151">Hello Azure portal'da, bir expressroute bağlantı hattı hello durumunu seçerek denetlenebilir ![2][2] expressroute bağlantı hattı üzerinde hello sol kenar çubuğu menüsüne ve ardından seçerek hello.</span><span class="sxs-lookup"><span data-stu-id="7b654-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="7b654-152">Bir expressroute bağlantı seçme "Tüm kaynaklar" altında listelenen bağlantı hattı hello ExpressRoute bağlantı hattı dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="7b654-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="7b654-153">Merhaba, ![3][3] hello dikey penceresinde hello essentials hello aşağıdaki ekran görüntüsü gösterildiği gibi listelenen ExpressRoute bölümünü:</span><span class="sxs-lookup"><span data-stu-id="7b654-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="7b654-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="7b654-154">![4][4]</span></span>    

<span data-ttu-id="7b654-155">Merhaba ExpressRoute Essentials içindeki *hattı durumu* hello Microsoft yan hello devreye hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b654-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="7b654-156">*Sağlayıcı durumu* hello hattı olup olmadığını gösteren *hazırlandı/değil sağlanan* hello hizmet sağlayıcı tarafında.</span><span class="sxs-lookup"><span data-stu-id="7b654-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="7b654-157">Bir ExpressRoute bağlantı hattı toobe için işletimsel, hello *hattı durumu* olmalıdır *etkin* ve hello *sağlayıcı durumu* olmalıdır *hazırlandı*.</span><span class="sxs-lookup"><span data-stu-id="7b654-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="7b654-158">Merhaba, *hattı durumu* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="7b654-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="7b654-159">Merhaba, *sağlayıcı durumu* olan sağlanan değil, hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="7b654-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="7b654-160">PowerShell aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="7b654-160">Verification via PowerShell</span></span>
<span data-ttu-id="7b654-161">toolist tüm ExpressRoute bağlantı hatları bir kaynak grubunda Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="7b654-162">Kaynak grubu adı hello Azure portal elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b654-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="7b654-163">Merhaba, bu belgenin önceki alt bölümüne bakın ve bu hello kaynak grubu adı hello örnek ekran görüntüsü listelenen not edin.</span><span class="sxs-lookup"><span data-stu-id="7b654-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="7b654-164">belirli bir expressroute bağlantı hattı komutu aşağıdaki kullanım hello bir kaynak grubunda tooselect:</span><span class="sxs-lookup"><span data-stu-id="7b654-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="7b654-165">Örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7b654-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="7b654-166">tooconfirm bir expressroute bağlantı hattı çalıştığından, özellikle dikkat toohello alanları izleyen ödeme:</span><span class="sxs-lookup"><span data-stu-id="7b654-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="7b654-167">Merhaba, *CircuitProvisioningState* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="7b654-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="7b654-168">Merhaba, *ServiceProviderProvisioningState* olan sağlanan değil, hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="7b654-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="7b654-169">PowerShell (Klasik) aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="7b654-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="7b654-170">toolist tüm ExpressRoute bağlantı hatları bir abonelik altında Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="7b654-171">tooselect belirli bir expressroute bağlantı hattı hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="7b654-172">Örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7b654-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="7b654-173">tooconfirm bir expressroute bağlantı hattı çalıştığından, özellikle dikkat toohello alanları izleyen ödeme: ServiceProviderProvisioningState: sağlanan durum: etkin</span><span class="sxs-lookup"><span data-stu-id="7b654-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="7b654-174">Merhaba, *durum* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="7b654-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="7b654-175">Merhaba, *ServiceProviderProvisioningState* olan sağlanan değil, hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="7b654-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="7b654-176">Eşleme yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="7b654-176">Validate Peering Configuration</span></span>
<span data-ttu-id="7b654-177">Merhaba expressroute bağlantı hattı sağlama tamamlanmış hello Hello hizmet sağlayıcısı sahip olduktan sonra bir yönlendirme yapılandırması hello MSEE PRs (4) Msee'ler (5) arasındaki expressroute bağlantı hattı üzerinden oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="7b654-178">Her expressroute bağlantı hattı bir, iki veya üç yönlendirme bağlamları etkin olabilir: (trafiği tooprivate sanal ağlar Azure) Azure özel eşleme, (trafiği toopublic azure'daki IP adresleri) Azure ortak eşleme ve Microsoft (trafiği tooOffice 365 eşleme ve Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="7b654-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="7b654-179">Hakkında daha fazla bilgi için toocreate ve yönlendirme yapılandırmasını değiştirmek, hello makalesine bakın [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7b654-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="7b654-180">Hello Azure portal aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="7b654-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="7b654-181">Merhaba; burada görüntülerle ExpressRoute eşlemeler olan Azure portal bilinen bir hata varsa *değil* hello hizmet sağlayıcısı tarafından yapılandırılmışsa hello Portalı'nda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="7b654-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="7b654-182">ExpressRoute eşlemeler hello portal veya PowerShell aracılığıyla ekleme *hello servis sağlayıcı ayarları geçersiz kılar*.</span><span class="sxs-lookup"><span data-stu-id="7b654-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="7b654-183">Bu eylem hello hello expressroute bağlantı hattı üzerinde yönlendirmeyi keser ve hello hizmeti sağlayıcısı toorestore hello ayarlarının hello desteği gerektirir ve normal yönlendirme yeniden.</span><span class="sxs-lookup"><span data-stu-id="7b654-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="7b654-184">Yalnızca bu hello hizmet sağlayıcısı yalnızca Katman 2 hizmetleri sağlayan belirli ise hello ExpressRoute eşlemeler değiştirin!</span><span class="sxs-lookup"><span data-stu-id="7b654-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="7b654-185">Hizmet sağlayıcısı ve hello eşlemeler tarafından Hello hello Portalı'nda boş olması koşuluyla Katman 3 ise, PowerShell kullanılan toosee hello servis sağlayıcı yapılandırılmış ayarları olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="7b654-186">Hello Azure portal'da, bir expressroute bağlantı hattı durumunu seçerek denetlenebilir ![2][2] expressroute bağlantı hattı üzerinde hello sol kenar çubuğu menüsüne ve ardından seçerek hello.</span><span class="sxs-lookup"><span data-stu-id="7b654-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="7b654-187">Bir expressroute bağlantı seçme "Tüm kaynaklar" altında listelenen bağlantı hattı hello ExpressRoute bağlantı hattı dikey penceresi açılacaktır.</span><span class="sxs-lookup"><span data-stu-id="7b654-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="7b654-188">Merhaba, ![3][3] bölümüne hello dikey penceresinde hello ExpressRoute hello aşağıdaki ekran görüntüsü gösterildiği gibi essentials'in listelenmesi:</span><span class="sxs-lookup"><span data-stu-id="7b654-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="7b654-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="7b654-189">![5][5]</span></span>

<span data-ttu-id="7b654-190">Azure ortak ve Microsoft eşleme yönlendirme bağlamları etkin olmayan ancak örnek önceki hello belirtilen Azure özel eşleme yönlendirme bağlamı olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="7b654-191">Başarılı bir şekilde etkinleştirilmiş bir eşleme bağlamı listelenen hello (BGP için gerekli) birincil ve ikincil noktadan noktaya alt ağlar da gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b654-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="7b654-192">Merhaba /30 alt ağlar hello Msee'ler hello arabirimi IP adresini ve PE Msee için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b654-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="7b654-193">Bir eşleme etkin değilse, atanan hello birincil ve ikincil alt ağları eşleşip eşleşmediğini denetleyin PE Msee'ler hello yapılandırmasına.</span><span class="sxs-lookup"><span data-stu-id="7b654-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="7b654-194">Değilse, toochange hello yapılandırma, MSEE yönlendiricilerde çok başvurun[oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="7b654-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="7b654-195">PowerShell aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="7b654-195">Verification via PowerShell</span></span>
<span data-ttu-id="7b654-196">tooget hello Azure özel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="7b654-197">Bir başarılı bir şekilde yapılandırılmış özel eşleme için bir örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7b654-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="7b654-198">Başarılı bir şekilde etkinleştirilmiş bir eşleme bağlamı listelenen hello birincil ve ikincil adres öneklerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b654-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="7b654-199">Merhaba /30 alt ağlar hello Msee'ler hello arabirimi IP adresini ve PE Msee için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b654-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="7b654-200">tooget hello Azure genel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="7b654-201">tooget hello Microsoft eşleme yapılandırma ayrıntılarını, hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="7b654-202">Bir eşleme yapılandırılmamışsa bir hata iletisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7b654-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="7b654-203">Merhaba eşleme (Azure Bu örnekte eşliği genel) belirtildiği zaman bir örnek yanıt hello hattı içinde yapılandırılmamış:</span><span class="sxs-lookup"><span data-stu-id="7b654-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="7b654-204">Bir eşleme etkin değilse hello atanan birincil ve ikincil alt ağları eşleşme hello hello yapılandırmasına PE MSEE bağlı olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b654-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="7b654-205">Ayrıca onay hello varsa düzeltin *Vlanıd*, *AzureASN*, ve *PeerASN* üzerinde Msee'ler kullanılır ve bu değerleri toohello hello üzerinde kullanılan olanları eşleniyorsa PE MSEE bağlanır.</span><span class="sxs-lookup"><span data-stu-id="7b654-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="7b654-206">MD5 karma seçilirse, hello paylaşılan anahtar MSEE ve PE MSEE çiftine aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b654-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="7b654-207">Merhaba MSEE yönlendiricilerde toochange hello yapılandırma başvurmak çok [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7b654-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="7b654-208">PowerShell (Klasik) aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="7b654-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="7b654-209">tooget hello Azure özel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="7b654-210">Özel bir başarılı bir şekilde yapılandırılmış eşleme için ek olarak, örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7b654-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="7b654-211">A başarılı bir şekilde, etkinleştirilmiş eşleme bağlam listelenen hello birincil ve ikincil eş alt sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="7b654-212">Merhaba /30 alt ağlar hello Msee'ler hello arabirimi IP adresini ve PE Msee için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b654-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="7b654-213">tooget hello Azure genel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="7b654-214">tooget hello Microsoft eşleme yapılandırma ayrıntılarını, hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="7b654-215">Katman 3 eşlemeler hello hizmet sağlayıcısı tarafından ayarlanan, hello ExpressRoute eşlemeler hello portal veya PowerShell aracılığıyla ayarlama hello servis sağlayıcı ayarları üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="7b654-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="7b654-216">Merhaba sağlayıcı yan eşleme ayarları sıfırlama hello hizmet sağlayıcısının hello desteği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7b654-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="7b654-217">Yalnızca bu hello hizmet sağlayıcısı yalnızca Katman 2 hizmetleri sağlayan belirli ise hello ExpressRoute eşlemeler değiştirin!</span><span class="sxs-lookup"><span data-stu-id="7b654-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="7b654-218">Bir eşleme etkin değilse hello birincil ve ikincil eş atanan alt ağları eşleşme hello yapılandırmasına hello PE MSEE bağlı olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b654-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="7b654-219">Ayrıca onay hello varsa düzeltin *Vlanıd*, *AzureAsn*, ve *PeerAsn* üzerinde Msee'ler kullanılır ve bu değerleri toohello hello üzerinde kullanılan olanları eşleniyorsa PE MSEE bağlanır.</span><span class="sxs-lookup"><span data-stu-id="7b654-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="7b654-220">Merhaba MSEE yönlendiricilerde toochange hello yapılandırma başvurmak çok [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7b654-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="7b654-221">ARP arasında Microsoft ve hello hizmeti sağlayıcısını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="7b654-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="7b654-222">Bu bölüm, PowerShell (Klasik) komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b654-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="7b654-223">Azure Resource Manager PowerShell komutları kullanıyorsanız, yönetici/ortak yönetici erişimi toohello abonelik aracılığıyla sahip olduğundan emin olun [Klasik Azure portalı][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="7b654-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="7b654-224">Azure Resource Manager kullanarak sorun giderme için komutları toohello başvurun [hello Resource Manager dağıtım modeli alma ARP tablolarda] [ ARP] belge.</span><span class="sxs-lookup"><span data-stu-id="7b654-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="7b654-225">tooget ARP, hello Azure portalı ve Azure Resource Manager PowerShell komutları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7b654-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="7b654-226">Hello Azure Resource Manager PowerShell komutları ile bir hatayla karşılaşılmazsa Klasik PowerShell komutlarını Klasik PowerShell komutları de Azure Resource Manager ExpressRoute bağlantı hatları ile çalışması olarak çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b654-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="7b654-227">tooget hello hello özel eşliği olarak birincil MSEE'nin yönlendirici ARP tablosundan Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="7b654-228">Bir örnek yanıt hello başarılı senaryoda hello komutu için:</span><span class="sxs-lookup"><span data-stu-id="7b654-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="7b654-229">Benzer şekilde, hello hello hello MSEE ARP tablosundan kontrol edebilirsiniz *birincil*/*ikincil* yolu için *özel* /  *Ortak*/*Microsoft* eşlemeleri.</span><span class="sxs-lookup"><span data-stu-id="7b654-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="7b654-230">Merhaba aşağıdaki örnekte gösterildiği bir eşleme için hello komut yanıtı hello yok.</span><span class="sxs-lookup"><span data-stu-id="7b654-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="7b654-231">Merhaba ARP tablosu yoksa hello arabirimlerin IP adreslerini tooMAC adresleri, aşağıdaki bilgileri gözden geçirme hello eşlenmiş:</span><span class="sxs-lookup"><span data-stu-id="7b654-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="7b654-232">Merhaba ilk IP adresi hello /30 alt arasında hello bağlantı için atanmışsa MSEE PR hello ve MSEE MSEE PR. hello arabirimde kullanılır</span><span class="sxs-lookup"><span data-stu-id="7b654-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="7b654-233">Azure hello ikinci IP adresi Msee için her zaman kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b654-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="7b654-234">Merhaba müşteri (C-etiketi) ve hizmet (S-Tag) VLAN etiketlerini hem MSEE PR ve MSEE çifti eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b654-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="7b654-235">BGP ve hello MSEE yollara doğrula</span><span class="sxs-lookup"><span data-stu-id="7b654-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="7b654-236">Bu bölüm, PowerShell (Klasik) komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b654-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="7b654-237">Azure Resource Manager PowerShell komutları kullanıyorsanız, yönetici/ortak yönetici erişimi toohello abonelik aracılığıyla sahip olduğundan emin olun [Klasik Azure portalı][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="7b654-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="7b654-238">Azure portalı ve Azure Resource Manager PowerShell komutları kullanılabilir tooget BGP bilgileri, her iki hello.</span><span class="sxs-lookup"><span data-stu-id="7b654-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="7b654-239">Hello Azure Resource Manager PowerShell komutları ile bir hatayla karşılaşılmazsa Klasik PowerShell komutlarını Klasik PowerShell komutları de Azure Resource Manager ExpressRoute bağlantı hatları ile çalışması olarak çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b654-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="7b654-240">tooget yönlendirme tablosunu (BGP komşu) için belirli bir yönlendirme bağlam Özet Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b654-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="7b654-241">Bir örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7b654-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="7b654-242">Hello önceki örnekte gösterildiği gibi hello hello yönlendirme bağlamı ne kadar süreyle kurulduğunda için yararlı toodetermine komuttur.</span><span class="sxs-lookup"><span data-stu-id="7b654-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="7b654-243">Ayrıca, yol önekleri hello eşleme yönlendirici tarafından tanıtılan sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7b654-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="7b654-244">Merhaba durumu etkin veya boş ise, hello birincil ve ikincil eş atanan alt ağları eşleşme hello yapılandırmasına hello PE MSEE bağlı olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b654-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="7b654-245">Ayrıca onay hello varsa düzeltin *Vlanıd*, *AzureAsn*, ve *PeerAsn* üzerinde Msee'ler kullanılır ve bu değerleri toohello hello üzerinde kullanılan olanları eşleniyorsa PE MSEE bağlanır.</span><span class="sxs-lookup"><span data-stu-id="7b654-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="7b654-246">MD5 karma seçilirse, hello paylaşılan anahtar MSEE ve PE MSEE çiftine aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b654-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="7b654-247">Merhaba MSEE yönlendiricilerde toochange hello yapılandırma başvurmak çok[oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="7b654-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="7b654-248">Belirli bir eşlemesi içinde belirli hedefler erişilebilir değilse, toohello belirli eşleme bağlam ait hello Msee'ler hello rota tablosu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b654-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="7b654-249">(NATed IP olabilir) eşleşen bir önek hello yönlendirme tablosunda varsa, hello yolda NSG/güvenlik duvarları/ACL'leri varsa ve hello trafiğe olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7b654-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="7b654-250">tooget hello tam yönlendirme tablosundan MSEE hello üzerinde *birincil* hello belirli yolu *özel* yönlendirme bağlamı, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="7b654-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="7b654-251">Merhaba komutu için bir örnek başarılı sonuç verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7b654-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="7b654-252">Benzer şekilde, hello yönlendirme hello hello MSEE tablosundan kontrol edebilirsiniz *birincil*/*ikincil* yolu için *özel* / *Ortak*/*Microsoft* eşleme bağlamı.</span><span class="sxs-lookup"><span data-stu-id="7b654-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="7b654-253">Merhaba aşağıdaki örnekte gösterildiği bir eşleme için hello komut yanıtı hello yok:</span><span class="sxs-lookup"><span data-stu-id="7b654-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="7b654-254">Onay hello trafiği istatistikleri</span><span class="sxs-lookup"><span data-stu-id="7b654-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="7b654-255">tooget hello birincil ve ikincil yol trafiğini istatistikleri--bayt ve bir kapatma--bir eşleme bağlamında, komutu aşağıdaki kullanım hello birleştirilmiş:</span><span class="sxs-lookup"><span data-stu-id="7b654-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="7b654-256">Örnek bir çıktı hello komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7b654-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="7b654-257">Mevcut olmayan eşleme için hello komutunun örnek çıktı verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7b654-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="7b654-258">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="7b654-258">Next Steps</span></span>
<span data-ttu-id="7b654-259">Daha fazla bilgi veya Yardım için bağlantılar aşağıdaki hello denetleyin:</span><span class="sxs-lookup"><span data-stu-id="7b654-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="7b654-260">[Microsoft Destek][Support]</span><span class="sxs-lookup"><span data-stu-id="7b654-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="7b654-261">[Oluşturma ve bir expressroute bağlantı hattı değiştirme][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="7b654-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="7b654-262">[Oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="7b654-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Mantıksal hızlı Rota bağlantısı"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Tüm kaynaklar simgesi"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Genel Bakış simgesi"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials örnek ekran görüntüsü"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials örnek ekran görüntüsü"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






