---
title: "Doğrulanıyor bağlantısı: Sorun giderme kılavuzu Azure ExpressRoute | Microsoft Docs"
description: "Bu sayfa, sorun giderme ve bir expressroute bağlantı hattı uçtan uca bağlantısını doğrulama yönergelerini sağlar."
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
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="857d9-103">ExpressRoute bağlantısı doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="857d9-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="857d9-104">Bir şirket içi ağ bağlantı sağlayıcı tarafından kolaylaştırılan özel bir bağlantı üzerinden Microsoft bulutunu genişletir, ExpressRoute aşağıdaki üç farklı ağ bölgeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="857d9-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="857d9-105">Müşteri ağ</span><span class="sxs-lookup"><span data-stu-id="857d9-105">Customer Network</span></span>
-   <span data-ttu-id="857d9-106">Sağlayıcı ağ</span><span class="sxs-lookup"><span data-stu-id="857d9-106">Provider Network</span></span>
-   <span data-ttu-id="857d9-107">Microsoft Veri merkezinde</span><span class="sxs-lookup"><span data-stu-id="857d9-107">Microsoft Datacenter</span></span>

<span data-ttu-id="857d9-108">Bu belgenin amacı, nereye tanımlamak için kullanıcı yardımcı olmaktır (veya bir olsa bile) bir bağlantı sorunu var ve böylece bu sorunu çözmek için uygun ekibinden yardım aramak için hangi bölgedeki.</span><span class="sxs-lookup"><span data-stu-id="857d9-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="857d9-109">Bir sorunu gidermek için Microsoft destek gerekirse ile destek bilet [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="857d9-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="857d9-110">Bu belge, tanılama ve basit sorunlarını giderme Yardımı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="857d9-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="857d9-111">Microsoft destek için yenileme olması amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="857d9-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="857d9-112">Bir destek bileti ile açmak [Microsoft Support] [ Support] sağlanan yönergeleri kullanarak sorunu çözmeyi erişemiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="857d9-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="857d9-113">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="857d9-113">Overview</span></span>
<span data-ttu-id="857d9-114">Aşağıdaki diyagramda bir müşteri ağı ExpressRoute kullanarak Microsoft ağına mantıksal bağlantısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="857d9-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="857d9-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="857d9-115">[![1]][1]</span></span>

<span data-ttu-id="857d9-116">Önceki diyagramda sayıları anahtar ağ noktalarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="857d9-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="857d9-117">Ağ noktaları genellikle ilişkili numaralarına göre bu makalede başvurulur.</span><span class="sxs-lookup"><span data-stu-id="857d9-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="857d9-118">ExpressRoute bağlantı modeli (bulut Exchange birlikte bulundurma, noktadan noktaya Ethernet bağlantısı veya Any herhangi bir (IPVPN)) bağlı olarak ağ noktalarını 3 ve 4 anahtarları (Katman 2 aygıtları) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="857d9-119">Gösterilen anahtar ağ noktaları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="857d9-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="857d9-120">Müşteri işlem aygıt (örneğin, bir sunucu veya bilgisayar)</span><span class="sxs-lookup"><span data-stu-id="857d9-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="857d9-121">CEs: Müşteri sınır yönlendiricileri</span><span class="sxs-lookup"><span data-stu-id="857d9-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="857d9-122">PEs (CE'e yönelik): sağlayıcısı sınır yönlendiricileri/müşteri sınır yönlendiricileri karşılıklı anahtarları.</span><span class="sxs-lookup"><span data-stu-id="857d9-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="857d9-123">İçin bu belgede PE CEs adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="857d9-124">PEs (MSEE'e yönelik): sağlayıcısı sınır yönlendiricileri/Msee'ler karşılıklı anahtarları.</span><span class="sxs-lookup"><span data-stu-id="857d9-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="857d9-125">İçin bu belgede PE Msee'ler adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="857d9-126">Msee'ler: Microsoft Enterprise Edge (MSEE) ExpressRoute yönlendiricileri</span><span class="sxs-lookup"><span data-stu-id="857d9-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="857d9-127">Sanal ağ (VNet) ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="857d9-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="857d9-128">Azure sanal cihazda işlem</span><span class="sxs-lookup"><span data-stu-id="857d9-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="857d9-129">Bulut Exchange birlikte bulundurma veya noktadan noktaya Ethernet bağlantısı bağlantı modeli kullanılıyorsa, müşteri sınır yönlendiricisi (2) BGP eşliği (5) Msee'ler ile oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="857d9-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="857d9-130">Ağ noktalarını 3 ve 4 hala var ancak katman 2 cihaz olarak biraz saydam.</span><span class="sxs-lookup"><span data-stu-id="857d9-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="857d9-131">Any herhangi bir (IPVPN) bağlantı modeli kullanılıyorsa, (MSEE'e yönelik) PEs (4) BGP eşliği (5) Msee'ler ile kurmak.</span><span class="sxs-lookup"><span data-stu-id="857d9-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="857d9-132">Yollar sonra geri müşteri ağ IPVPN hizmet sağlayıcısı ağ üzerinden yayılması.</span><span class="sxs-lookup"><span data-stu-id="857d9-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="857d9-133">ExpressRoute, yüksek kullanılabilirlik için yedek bir BGP oturumları Msee'ler (5) PE Msee'ler (4) arasındaki çift Microsoft gerektirir.</span><span class="sxs-lookup"><span data-stu-id="857d9-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="857d9-134">Ağ yolları yedek çifti de müşteri ağ arasında PE CEs teşvik.</span><span class="sxs-lookup"><span data-stu-id="857d9-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="857d9-135">Ancak, Any herhangi bir (IPVPN) bağlantı modelinde, tek bir CE aygıt (2) bir veya daha fazla PEs (3) için bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="857d9-136">Bir expressroute bağlantı hattı doğrulamak için aşağıdaki adımları (noktasıyla ilişkili sayıyla ağ) ele alınmaktadır:</span><span class="sxs-lookup"><span data-stu-id="857d9-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="857d9-137">Bağlantı hattı hazırlama ve durumu (5) doğrula</span><span class="sxs-lookup"><span data-stu-id="857d9-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="857d9-138">En az bir ExpressRoute doğrulamak eşliği, yapılandırılmış (5)</span><span class="sxs-lookup"><span data-stu-id="857d9-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="857d9-139">Microsoft ile hizmet arasında ARP doğrulama sağlayıcısı (4 ve 5 arasında bağlantı)</span><span class="sxs-lookup"><span data-stu-id="857d9-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="857d9-140">BGP ve (BGP 4 ila 5 5-bir VNet bağlıysa, 6 arasındaki) MSEE yollara doğrula</span><span class="sxs-lookup"><span data-stu-id="857d9-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="857d9-141">Onay trafiği istatistikleri (trafik 5'ten geçirme)</span><span class="sxs-lookup"><span data-stu-id="857d9-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="857d9-142">Daha fazla doğrulama ve denetimleri geri gelecekteki iade aylık eklenecek!</span><span class="sxs-lookup"><span data-stu-id="857d9-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="857d9-143">Bağlantı hattı hazırlama ve durumunu doğrula</span><span class="sxs-lookup"><span data-stu-id="857d9-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="857d9-144">Bağlantı modeli bağımsız olarak bir expressroute bağlantı hattı oluşturulması gerekir ve bu nedenle devre sağlama için bir hizmet anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="857d9-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="857d9-145">Bir expressroute bağlantı hattı sağlama PE Msee'ler (4) ve Msee'ler (5) arasında yedekli bir katman 2 bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="857d9-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="857d9-146">Makale oluşturma, değiştirme, sağlamak ve bir expressroute bağlantı hattı doğrulamanın nasıl yapılacağı hakkında daha fazla bilgi için bkz: [oluşturma ve bir expressroute bağlantı hattı değiştirme][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="857d9-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="857d9-147">Bir hizmet anahtarı, bir expressroute bağlantı hattı benzersiz olarak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="857d9-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="857d9-148">Bu belgede belirtilen powershell komutların çoğu için bu anahtar gereklidir.</span><span class="sxs-lookup"><span data-stu-id="857d9-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="857d9-149">Ayrıca, bir ExpressRoute sorun giderme, bağlantı hattı kolaylıkla tanımlamak için hizmet anahtarı sağlamak için bir expressroute bağlantı ortağı Microsoft'tan ya da Yardım gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="857d9-150">Azure Portalı aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="857d9-150">Verification via the Azure portal</span></span>
<span data-ttu-id="857d9-151">Azure portalında seçerek bir expressroute bağlantı hattı durumunu denetlenebilir ![2][2] sol kenar çubuğu menü ve expressroute bağlantı hattı seçme.</span><span class="sxs-lookup"><span data-stu-id="857d9-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="857d9-152">Bir expressroute bağlantı seçme "Tüm kaynaklar" altında listelenen bağlantı hattı ExpressRoute bağlantı hattı dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="857d9-153">İçinde ![3][3] dikey penceresinde aşağıdaki ekran görüntüsünde gösterildiği gibi essentials listelenen ExpressRoute bölümünü:</span><span class="sxs-lookup"><span data-stu-id="857d9-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="857d9-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="857d9-154">![4][4]</span></span>    

<span data-ttu-id="857d9-155">ExpressRoute essentials'ta *hattı durum* Microsoft tarafında devre durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="857d9-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="857d9-156">*Sağlayıcı durumu* bağlantı hattı olup olmadığını gösteren *hazırlandı/değil sağlanan* hizmet sağlayıcı tarafındaki.</span><span class="sxs-lookup"><span data-stu-id="857d9-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="857d9-157">İşlem, olacak şekilde bir expressroute bağlantı hattı için *hattı durumu* olmalıdır *etkin* ve *sağlayıcı durumu* olmalıdır *hazırlandı*.</span><span class="sxs-lookup"><span data-stu-id="857d9-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="857d9-158">Varsa *hattı durumu* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="857d9-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="857d9-159">Varsa *sağlayıcı durumu* olan sağlanan değil, hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="857d9-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="857d9-160">PowerShell aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="857d9-160">Verification via PowerShell</span></span>
<span data-ttu-id="857d9-161">Bir kaynak grubundaki tüm ExpressRoute bağlantı hatları listelemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="857d9-162">Azure portalı üzerinden, kaynak grubu adı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="857d9-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="857d9-163">Bu belgenin önceki alt bölümüne bakın ve kaynak grubu adı örnek ekran görüntüsü listelendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="857d9-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="857d9-164">Bir kaynak grubunda belirli bir expressroute bağlantı hattı seçmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="857d9-165">Örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="857d9-165">A sample response is:</span></span>

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

<span data-ttu-id="857d9-166">Bir expressroute bağlantı hattı işletimsel olup olmadığını onaylamak için belirli aşağıdaki alanları dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="857d9-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="857d9-167">Varsa *CircuitProvisioningState* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="857d9-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="857d9-168">Varsa *ServiceProviderProvisioningState* olan sağlanan değil, hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="857d9-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="857d9-169">PowerShell (Klasik) aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="857d9-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="857d9-170">Bir abonelik altında tüm ExpressRoute bağlantı hatları listelemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="857d9-171">Belirli bir expressroute bağlantı hattı seçmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="857d9-172">Örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="857d9-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="857d9-173">Bir expressroute bağlantı hattı işletimsel olup olmadığını onaylamak için belirli aşağıdaki alanları dikkat edin: ServiceProviderProvisioningState: sağlanan durum: etkin</span><span class="sxs-lookup"><span data-stu-id="857d9-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="857d9-174">Varsa *durum* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="857d9-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="857d9-175">Varsa *ServiceProviderProvisioningState* olan sağlanan değil, hizmet sağlayıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="857d9-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="857d9-176">Eşleme yapılandırmasını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="857d9-176">Validate Peering Configuration</span></span>
<span data-ttu-id="857d9-177">Hizmet sağlayıcısı expressroute bağlantı hattı Sağlama tamamlandıktan sonra bir yönlendirme yapılandırması MSEE PRs (4) Msee'ler (5) arasındaki expressroute bağlantı hattı üzerinden oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="857d9-178">Her expressroute bağlantı hattı etkin bir, iki veya üç yönlendirme bağlamları sahip olabilir: Azure özel eşleme (trafiğin Azure içindeki özel sanal ağların için), Azure ortak eşleme (trafiğin Azure genel IP adresleri için) ve Microsoft eşleme (trafiği Office 365 ve Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="857d9-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="857d9-179">Oluşturma ve yönlendirme yapılandırmasını değiştirme hakkında daha fazla bilgi için bkz: [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="857d9-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="857d9-180">Azure Portalı aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="857d9-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="857d9-181">Burada görüntülerle ExpressRoute eşlemeler Azure portalında bilinen bir hata varsa *değil* hizmet sağlayıcısı tarafından yapılandırılmışsa Portalı'nda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="857d9-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="857d9-182">Portal veya PowerShell üzerinden ExpressRoute eşlemeleri ekleme *servis sağlayıcı ayarları geçersiz kılar*.</span><span class="sxs-lookup"><span data-stu-id="857d9-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="857d9-183">Bu eylem, expressroute bağlantı hattı üzerinde yönlendirme keser ve ayarlarını geri yüklemek ve normal yönlendirme yeniden kurmak için hizmet sağlayıcı desteği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="857d9-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="857d9-184">Hizmet sağlayıcısı yalnızca Katman 2 hizmetleri sağlayan belirli ise yalnızca ExpressRoute eşlemeler değiştirin!</span><span class="sxs-lookup"><span data-stu-id="857d9-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="857d9-185">Katman 3 hizmet sağlayıcısı tarafından sağlanır ve eşlemeler portalda boş, PowerShell servis sağlayıcı yapılandırılmış ayarları görmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="857d9-186">Azure portalında seçerek bir expressroute bağlantı hattı durumunu denetlenebilir ![2][2] sol kenar çubuğu menü ve expressroute bağlantı hattı seçme.</span><span class="sxs-lookup"><span data-stu-id="857d9-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="857d9-187">Bir expressroute bağlantı seçme "Tüm kaynaklar" altında listelenen bağlantı hattı ExpressRoute bağlantı hattı dikey penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="857d9-188">İçinde ![3][3] dikey penceresinde aşağıdaki ekran görüntüsünde gösterildiği gibi essentials'in listelenmesi ExpressRoute bölümünü:</span><span class="sxs-lookup"><span data-stu-id="857d9-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="857d9-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="857d9-189">![5][5]</span></span>

<span data-ttu-id="857d9-190">Azure ortak ve Microsoft eşleme yönlendirme bağlamları etkin olmayan ancak önceki örnekte belirtilen Azure özel eşleme yönlendirme bağlamı olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="857d9-191">Başarılı bir şekilde etkinleştirilmiş bir eşleme bağlamı listelenen (BGP için gerekli) birincil ve ikincil noktadan noktaya alt ağlar da gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="857d9-192">/ 30 alt ağ arabiriminin IP adresini ve Msee'ler PE Msee için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="857d9-193">Bir eşleme etkin değilse, atanan birincil ve ikincil alt ağları PE Msee'ler yapılandırmasına eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="857d9-194">Aksi durumda, MSEE yönlendiricilerde yapılandırmasını değiştirmek için başvurmak [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="857d9-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="857d9-195">PowerShell aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="857d9-195">Verification via PowerShell</span></span>
<span data-ttu-id="857d9-196">Azure özel eşleme yapılandırma ayrıntılarını almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="857d9-197">Bir başarılı bir şekilde yapılandırılmış özel eşleme için bir örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="857d9-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="857d9-198">Başarılı bir şekilde etkinleştirilmiş bir eşleme bağlamı, listelenen birincil ve ikincil adres öneklerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="857d9-199">/ 30 alt ağ arabiriminin IP adresini ve Msee'ler PE Msee için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="857d9-200">Azure ortak eşleme yapılandırma ayrıntılarını almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="857d9-201">Microsoft eşlemesi yapılandırma ayrıntılarını almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="857d9-202">Bir eşleme yapılandırılmamışsa bir hata iletisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="857d9-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="857d9-203">Belirtilen eşleme (Azure Bu örnekte eşliği genel) içinde hattı yapılandırılmadığında bir örnek yanıt:</span><span class="sxs-lookup"><span data-stu-id="857d9-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="857d9-204">Bir eşleme etkin değilse, atanan birincil ve ikincil alt ağları Bağlantılı PE MSEE yapılandırmasına eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="857d9-205">Ayrıca denetleyin doğru *Vlanıd*, *AzureASN*, ve *PeerASN* üzerinde Msee'ler kullanılır ve bu değerleri eşleniyorsa bağlantılı PE MSEE üzerinde kullanılan olanlara.</span><span class="sxs-lookup"><span data-stu-id="857d9-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="857d9-206">MD5 karma seçilirse, paylaşılan anahtar MSEE ve PE MSEE çiftine aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="857d9-207">MSEE yönlendiricilerde yapılandırmasını değiştirmek için başvurmak [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="857d9-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="857d9-208">PowerShell (Klasik) aracılığıyla doğrulama</span><span class="sxs-lookup"><span data-stu-id="857d9-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="857d9-209">Azure özel eşleme yapılandırma ayrıntılarını almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="857d9-210">Özel bir başarılı bir şekilde yapılandırılmış eşleme için ek olarak, örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="857d9-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="857d9-211">A başarılı bir şekilde, etkinleştirilmiş eşleme bağlamı, listelenen birincil ve ikincil eş alt ağlar sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="857d9-212">/ 30 alt ağ arabiriminin IP adresini ve Msee'ler PE Msee için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="857d9-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="857d9-213">Azure ortak eşleme yapılandırma ayrıntılarını almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="857d9-214">Microsoft eşlemesi yapılandırma ayrıntılarını almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="857d9-215">Katman 3 eşlemeler hizmet sağlayıcısı tarafından ayarlanan, portal veya PowerShell üzerinden ExpressRoute eşlemeler ayarlama, servis sağlayıcı ayarları üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="857d9-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="857d9-216">Sağlayıcı yan eşleme ayarları sıfırlama hizmet sağlayıcısının desteği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="857d9-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="857d9-217">Hizmet sağlayıcısı yalnızca Katman 2 hizmetleri sağlayan belirli ise yalnızca ExpressRoute eşlemeler değiştirin!</span><span class="sxs-lookup"><span data-stu-id="857d9-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="857d9-218">Bir eşleme etkin değilse, atanan birincil ve ikincil eş alt ağları Bağlantılı PE MSEE yapılandırmasına eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="857d9-219">Ayrıca denetleyin doğru *Vlanıd*, *AzureAsn*, ve *PeerAsn* üzerinde Msee'ler kullanılır ve bu değerleri eşleniyorsa bağlantılı PE MSEE üzerinde kullanılan olanlara.</span><span class="sxs-lookup"><span data-stu-id="857d9-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="857d9-220">MSEE yönlendiricilerde yapılandırmasını değiştirmek için başvurmak [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="857d9-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="857d9-221">Microsoft hizmet sağlayıcısı arasında ARP doğrula</span><span class="sxs-lookup"><span data-stu-id="857d9-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="857d9-222">Bu bölüm, PowerShell (Klasik) komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="857d9-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="857d9-223">Azure Resource Manager PowerShell komutları kullanıyorsanız, aboneliğe yönetici/ortak yönetici erişimi olduğundan emin olun [Klasik Azure portalı][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="857d9-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="857d9-224">Azure Resource Manager kullanarak sorun giderme için komutları lütfen [Resource Manager dağıtım modeli alma ARP tablolarda] [ ARP] belge.</span><span class="sxs-lookup"><span data-stu-id="857d9-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="857d9-225">ARP almak için Azure portalı ve Azure Resource Manager PowerShell komutları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="857d9-226">Azure Resource Manager PowerShell komutları ile bir hatayla karşılaşılmazsa Klasik PowerShell komutlarını Klasik PowerShell komutları de Azure Resource Manager ExpressRoute bağlantı hatları ile çalışması olarak çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="857d9-227">Özel eşleme için birincil MSEE'nin yönlendiriciden ARP tablosu almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="857d9-228">Bir örnek yanıt başarılı senaryoda komutu için:</span><span class="sxs-lookup"><span data-stu-id="857d9-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="857d9-229">Benzer şekilde, MSEE ARP tablosundan kontrol edebilirsiniz *birincil*/*ikincil* yolu için *özel*/*ortak*/*Microsoft* eşlemeleri.</span><span class="sxs-lookup"><span data-stu-id="857d9-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="857d9-230">Aşağıdaki örnek, bir eşleme için komut yanıtı yok gösterir.</span><span class="sxs-lookup"><span data-stu-id="857d9-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="857d9-231">ARP tablosu MAC adreslerinin eşlenen arabirimlerin IP adreslerini yoksa, aşağıdaki bilgileri gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="857d9-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="857d9-232">Varsa/30 ilk IP adresini MSEE PR ve MSEE arasındaki bağlantıyı MSEE PR. arabirimde kullanılır atanan alt ağ</span><span class="sxs-lookup"><span data-stu-id="857d9-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="857d9-233">Azure, ikinci IP adresi Msee için her zaman kullanır.</span><span class="sxs-lookup"><span data-stu-id="857d9-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="857d9-234">Hizmet (S-Tag) VLAN etiketlerini ve müşteri (C-Tag) hem de MSEE PR ve MSEE çifti eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="857d9-235">BGP ve MSEE yollara doğrula</span><span class="sxs-lookup"><span data-stu-id="857d9-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="857d9-236">Bu bölüm, PowerShell (Klasik) komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="857d9-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="857d9-237">Azure Resource Manager PowerShell komutları kullanıyorsanız, aboneliğe yönetici/ortak yönetici erişimi olduğundan emin olun [Klasik Azure portalı][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="857d9-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="857d9-238">BGP bilgi almak için Azure portalı ve Azure Resource Manager PowerShell komutları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="857d9-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="857d9-239">Azure Resource Manager PowerShell komutları ile bir hatayla karşılaşılmazsa Klasik PowerShell komutlarını Klasik PowerShell komutları de Azure Resource Manager ExpressRoute bağlantı hatları ile çalışması olarak çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="857d9-240">Belirli bir yönlendirme bağlamının (BGP komşu) yönlendirme tablosu özetini almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="857d9-241">Bir örnek yanıt şöyledir:</span><span class="sxs-lookup"><span data-stu-id="857d9-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="857d9-242">Önceki örnekte gösterildiği gibi komut yönlendirme ne kadar süreyle bağlamı için kurulmuş belirlemek yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="857d9-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="857d9-243">Ayrıca, eşleme yönlendirici tarafından tanıtılan rota ön sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="857d9-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="857d9-244">Durumu etkin veya boş ise, atanan birincil ve ikincil eş alt ağları Bağlantılı PE MSEE yapılandırmasına eşleşip eşleşmediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="857d9-245">Ayrıca denetleyin doğru *Vlanıd*, *AzureAsn*, ve *PeerAsn* üzerinde Msee'ler kullanılır ve bu değerleri eşleniyorsa bağlantılı PE MSEE üzerinde kullanılan olanlara.</span><span class="sxs-lookup"><span data-stu-id="857d9-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="857d9-246">MD5 karma seçilirse, paylaşılan anahtar MSEE ve PE MSEE çiftine aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="857d9-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="857d9-247">MSEE yönlendiricilerde yapılandırmasını değiştirmek için başvurmak [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="857d9-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="857d9-248">Belirli bir eşlemesi içinde belirli hedefler erişilebilir değilse, belirli eşleme bağlamına ait Msee'ler rota tablosu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="857d9-249">Yönlendirme tablosunda (NATed IP olabilir) eşleşen bir önek varsa yola NSG/güvenlik duvarları/ACL'leri varsa ve trafiğe izin olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="857d9-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="857d9-250">Tam yönlendirme tablosu MSEE almak için *birincil* belirli yolu *özel* bağlamı yönlendirme, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="857d9-251">Komutu için bir örnek başarılı sonuç verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="857d9-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="857d9-252">Benzer şekilde, MSEE yönlendirme tablosundan kontrol edebilirsiniz *birincil*/*ikincil* yolu için *özel*/*ortak*/*Microsoft* eşleme bağlamı.</span><span class="sxs-lookup"><span data-stu-id="857d9-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="857d9-253">Aşağıdaki örnek, bir eşleme için komut yanıtı yok gösterir:</span><span class="sxs-lookup"><span data-stu-id="857d9-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="857d9-254">Onay trafiği istatistikleri</span><span class="sxs-lookup"><span data-stu-id="857d9-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="857d9-255">Birleşik birincil ve ikincil yol trafiğini istatistikleri--bayt ve bir kapatma--bir eşleme bağlamında almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="857d9-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="857d9-256">Komutun bir örnek çıktı verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="857d9-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="857d9-257">Örnek bir çıktı mevcut olmayan eşleme için komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="857d9-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="857d9-258">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="857d9-258">Next Steps</span></span>
<span data-ttu-id="857d9-259">Daha fazla bilgi veya Yardım için aşağıdaki bağlantıları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="857d9-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="857d9-260">[Microsoft Destek][Support]</span><span class="sxs-lookup"><span data-stu-id="857d9-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="857d9-261">[Oluşturma ve bir expressroute bağlantı hattı değiştirme][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="857d9-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="857d9-262">[Oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="857d9-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="857d9-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Mantıksal hızlı Rota bağlantısı"</span><span class="sxs-lookup"><span data-stu-id="857d9-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="857d9-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Tüm kaynaklar simgesi"</span><span class="sxs-lookup"><span data-stu-id="857d9-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="857d9-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Genel Bakış simgesi"</span><span class="sxs-lookup"><span data-stu-id="857d9-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="857d9-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials örnek ekran görüntüsü"</span><span class="sxs-lookup"><span data-stu-id="857d9-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="857d9-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials örnek ekran görüntüsü"</span><span class="sxs-lookup"><span data-stu-id="857d9-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






