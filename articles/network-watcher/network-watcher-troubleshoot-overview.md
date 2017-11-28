---
title: "Azure Ağ İzleyicisi sorun giderme aaaIntroduction tooresource | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi kaynak sorun giderme özelliklerine genel bakış sağlar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="c00ca-103">Giriş tooresource Azure Ağ İzleyicisi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c00ca-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="c00ca-104">Sanal ağ geçitleri, şirket içi kaynakları ile Azure içindeki diğer sanal ağlar arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c00ca-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="c00ca-105">Bu ağ geçitleri ve kendi bağlantılarını izleme kritik tooensuring iletişim bozuk değil.</span><span class="sxs-lookup"><span data-stu-id="c00ca-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="c00ca-106">Ağ İzleyicisi Merhaba yetenek tootroubleshoot sağlayan sanal ağ geçitleri ve ağ bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="c00ca-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="c00ca-107">Bu hello portal, PowerShell'i, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="c00ca-108">Çağrıldığında, Ağ İzleyicisi Merhaba durumunu hello sanal ağ geçidi veya bağlantı ve dönüş hello uygun sonuçları tanılar.</span><span class="sxs-lookup"><span data-stu-id="c00ca-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="c00ca-109">Merhaba tanılama tamamlandıktan sonra bu istek uzun süren bir işlemdir, hello sonuçlar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="c00ca-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="c00ca-111">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="c00ca-111">Results</span></span>

<span data-ttu-id="c00ca-112">döndürülen hello ön sonuçları hello kaynak hello durumunu genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="c00ca-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="c00ca-113">Daha ayrıntılı bilgi için kaynaklar hello bölümü aşağıdaki gösterildiği gibi sağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="c00ca-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="c00ca-114">Merhaba aşağıdaki hello ile döndürülen hello değerleri API sorun giderme listesidir:</span><span class="sxs-lookup"><span data-stu-id="c00ca-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="c00ca-115">**startTime** -bu değer hello sorun giderme, çalışmaya API çağrısı hello saattir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="c00ca-116">**endTime** -bu değer hello sorun giderme ne zaman sona hello saattir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="c00ca-117">**kod** -tek tanılama hatası varsa bu sağlıksız, değerdir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="c00ca-118">**Sonuçları** -sonuçları hello bağlantısı veya hello sanal ağ geçidinde döndürülen sonuçları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="c00ca-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="c00ca-119">**Kimliği** -bu değeri hello hataya türüdür.</span><span class="sxs-lookup"><span data-stu-id="c00ca-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="c00ca-120">**Özet** -bu değer hello hataya bir özetidir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="c00ca-121">**ayrıntılı** -bu değer hello hatası için ayrıntılı bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="c00ca-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="c00ca-122">**recommendedActions** -bu özellik önerilen eylemleri tootake koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="c00ca-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="c00ca-123">**actionText** -bu değer hangi eylemini tootake açıklayan hello metni içerir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="c00ca-124">**actionUri** -bu değer hello URI toodocumentation hakkında yönergeler sağlar. tooact.</span><span class="sxs-lookup"><span data-stu-id="c00ca-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="c00ca-125">**actionUriText** -bu değer hello eylem metni kısa açıklamasıdır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="c00ca-126">kullanılabilir olan tabloları göster hello farklı hata türleri (ID listesi önceki hello sonuçlarından altında) aşağıdaki hello ve hello hata günlükleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c00ca-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="c00ca-127">Ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="c00ca-127">Gateway</span></span>

| <span data-ttu-id="c00ca-128">Hata türü</span><span class="sxs-lookup"><span data-stu-id="c00ca-128">Fault Type</span></span> | <span data-ttu-id="c00ca-129">Neden</span><span class="sxs-lookup"><span data-stu-id="c00ca-129">Reason</span></span> | <span data-ttu-id="c00ca-130">Günlük</span><span class="sxs-lookup"><span data-stu-id="c00ca-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="c00ca-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="c00ca-131">NoFault</span></span> | <span data-ttu-id="c00ca-132">Herhangi bir hata algılandığında.</span><span class="sxs-lookup"><span data-stu-id="c00ca-132">When no error is detected.</span></span> |<span data-ttu-id="c00ca-133">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-133">Yes</span></span>|
| <span data-ttu-id="c00ca-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="c00ca-134">GatewayNotFound</span></span> | <span data-ttu-id="c00ca-135">Ağ geçidi veya ağ geçidi sağlanmamış bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="c00ca-136">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-136">No</span></span>|
| <span data-ttu-id="c00ca-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="c00ca-137">PlannedMaintenance</span></span> |  <span data-ttu-id="c00ca-138">Ağ geçidi örneği bakım yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="c00ca-139">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-139">No</span></span>|
| <span data-ttu-id="c00ca-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="c00ca-140">UserDrivenUpdate</span></span> | <span data-ttu-id="c00ca-141">Ne zaman bir kullanıcı güncelleştirme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-141">When a user update is in progress.</span></span> <span data-ttu-id="c00ca-142">Bu, yeniden boyutlandırma işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-142">This could be a resize operation.</span></span> | <span data-ttu-id="c00ca-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-143">No</span></span> |
| <span data-ttu-id="c00ca-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="c00ca-144">VipUnResponsive</span></span> | <span data-ttu-id="c00ca-145">Merhaba birincil hello ağ geçidi örneğini ulaşamıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="c00ca-146">Merhaba durumu araştırması başarısız olduğunda meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="c00ca-147">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-147">No</span></span> |
| <span data-ttu-id="c00ca-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="c00ca-148">PlatformInActive</span></span> | <span data-ttu-id="c00ca-149">Merhaba platform ile ilgili bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="c00ca-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="c00ca-150">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-150">No</span></span>|
| <span data-ttu-id="c00ca-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="c00ca-151">ServiceNotRunning</span></span> | <span data-ttu-id="c00ca-152">Merhaba temel alınan hizmet çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-152">hello underlying service is not running.</span></span> | <span data-ttu-id="c00ca-153">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-153">No</span></span>|
| <span data-ttu-id="c00ca-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="c00ca-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="c00ca-155">Hiçbir bağlantı hello ağ geçidinde bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="c00ca-156">Bu yalnızca bir uyarıdır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-156">This is only a warning.</span></span>| <span data-ttu-id="c00ca-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-157">No</span></span>|
| <span data-ttu-id="c00ca-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="c00ca-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="c00ca-159">Bağlantıları bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="c00ca-159">Connections are not connected.</span></span> <span data-ttu-id="c00ca-160">Bu yalnızca bir uyarıdır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-160">This is only a warning.</span></span>| <span data-ttu-id="c00ca-161">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-161">Yes</span></span>|
| <span data-ttu-id="c00ca-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="c00ca-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="c00ca-163">Merhaba geçerli ağ geçidi CPU kullanımı % > 95 ' dir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="c00ca-164">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="c00ca-165">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="c00ca-165">Connection</span></span>

| <span data-ttu-id="c00ca-166">Hata türü</span><span class="sxs-lookup"><span data-stu-id="c00ca-166">Fault Type</span></span> | <span data-ttu-id="c00ca-167">Neden</span><span class="sxs-lookup"><span data-stu-id="c00ca-167">Reason</span></span> | <span data-ttu-id="c00ca-168">Günlük</span><span class="sxs-lookup"><span data-stu-id="c00ca-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="c00ca-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="c00ca-169">NoFault</span></span> | <span data-ttu-id="c00ca-170">Herhangi bir hata algılandığında.</span><span class="sxs-lookup"><span data-stu-id="c00ca-170">When no error is detected.</span></span> |<span data-ttu-id="c00ca-171">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-171">Yes</span></span>|
| <span data-ttu-id="c00ca-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="c00ca-172">GatewayNotFound</span></span> | <span data-ttu-id="c00ca-173">Ağ geçidi veya ağ geçidi sağlanmamış bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="c00ca-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-174">No</span></span>|
| <span data-ttu-id="c00ca-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="c00ca-175">PlannedMaintenance</span></span> | <span data-ttu-id="c00ca-176">Ağ geçidi örneği bakım yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="c00ca-177">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-177">No</span></span>|
| <span data-ttu-id="c00ca-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="c00ca-178">UserDrivenUpdate</span></span> | <span data-ttu-id="c00ca-179">Ne zaman bir kullanıcı güncelleştirme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-179">When a user update is in progress.</span></span> <span data-ttu-id="c00ca-180">Bu, yeniden boyutlandırma işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-180">This could be a resize operation.</span></span>  | <span data-ttu-id="c00ca-181">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-181">No</span></span> |
| <span data-ttu-id="c00ca-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="c00ca-182">VipUnResponsive</span></span> | <span data-ttu-id="c00ca-183">Merhaba birincil hello ağ geçidi örneğini ulaşamıyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="c00ca-184">Merhaba durumu araştırması başarısız olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="c00ca-185">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-185">No</span></span> |
| <span data-ttu-id="c00ca-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="c00ca-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="c00ca-187">Bağlantı yapılandırması eksik.</span><span class="sxs-lookup"><span data-stu-id="c00ca-187">Connection configuration is missing.</span></span> | <span data-ttu-id="c00ca-188">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-188">No</span></span> |
| <span data-ttu-id="c00ca-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="c00ca-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="c00ca-190">Merhaba bağlantı "bağlantısız" olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="c00ca-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="c00ca-191">Hayır</span><span class="sxs-lookup"><span data-stu-id="c00ca-191">No</span></span>|
| <span data-ttu-id="c00ca-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="c00ca-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="c00ca-193">Merhaba temel alınan hizmet bağlantı yapılandırılmış hello yok.</span><span class="sxs-lookup"><span data-stu-id="c00ca-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="c00ca-194">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-194">Yes</span></span> |
| <span data-ttu-id="c00ca-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="c00ca-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="c00ca-196">arka plandaki hizmet hello yedek olarak işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="c00ca-197">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-197">Yes</span></span>|
| <span data-ttu-id="c00ca-198">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c00ca-198">Authentication</span></span> | <span data-ttu-id="c00ca-199">Önceden paylaşılmış anahtar uyuşmuyor.</span><span class="sxs-lookup"><span data-stu-id="c00ca-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="c00ca-200">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-200">Yes</span></span>|
| <span data-ttu-id="c00ca-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="c00ca-201">PeerReachability</span></span> | <span data-ttu-id="c00ca-202">Merhaba eş ağ geçidi ulaşılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="c00ca-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="c00ca-203">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-203">Yes</span></span>|
| <span data-ttu-id="c00ca-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="c00ca-204">IkePolicyMismatch</span></span> | <span data-ttu-id="c00ca-205">Merhaba eş ağ geçidi, Azure tarafından desteklenmez IKE ilkeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="c00ca-206">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-206">Yes</span></span>|
| <span data-ttu-id="c00ca-207">WfpParse hata</span><span class="sxs-lookup"><span data-stu-id="c00ca-207">WfpParse Error</span></span> | <span data-ttu-id="c00ca-208">Ayrıştırma hello WFP günlük bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="c00ca-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="c00ca-209">Evet</span><span class="sxs-lookup"><span data-stu-id="c00ca-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="c00ca-210">Desteklenen ağ geçidi türleri</span><span class="sxs-lookup"><span data-stu-id="c00ca-210">Supported Gateway types</span></span>

<span data-ttu-id="c00ca-211">Merhaba aşağıdaki listede hello destek hangi ağ geçitleri ve bağlantıları desteklenen gösterir Ağ İzleyicisi sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="c00ca-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="c00ca-212">**Ağ geçidi türleri**</span><span class="sxs-lookup"><span data-stu-id="c00ca-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="c00ca-213">VPN</span><span class="sxs-lookup"><span data-stu-id="c00ca-213">VPN</span></span>      | <span data-ttu-id="c00ca-214">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-214">Supported</span></span>        |
|<span data-ttu-id="c00ca-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c00ca-215">ExpressRoute</span></span> | <span data-ttu-id="c00ca-216">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-216">Not Supported</span></span> |
|<span data-ttu-id="c00ca-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="c00ca-217">Hypernet</span></span> | <span data-ttu-id="c00ca-218">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-218">Not Supported</span></span>|
|<span data-ttu-id="c00ca-219">**VPN türleri**</span><span class="sxs-lookup"><span data-stu-id="c00ca-219">**VPN types**</span></span> | |
|<span data-ttu-id="c00ca-220">Rota tabanlı</span><span class="sxs-lookup"><span data-stu-id="c00ca-220">Route Based</span></span> | <span data-ttu-id="c00ca-221">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-221">Supported</span></span>|
|<span data-ttu-id="c00ca-222">İlke tabanlı</span><span class="sxs-lookup"><span data-stu-id="c00ca-222">Policy Based</span></span> | <span data-ttu-id="c00ca-223">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-223">Not Supported</span></span>|
|<span data-ttu-id="c00ca-224">**Bağlantı türleri**</span><span class="sxs-lookup"><span data-stu-id="c00ca-224">**Connection types**</span></span>||
|<span data-ttu-id="c00ca-225">IPSec</span><span class="sxs-lookup"><span data-stu-id="c00ca-225">IPSec</span></span>| <span data-ttu-id="c00ca-226">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-226">Supported</span></span>|
|<span data-ttu-id="c00ca-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="c00ca-227">VNet2Vnet</span></span>| <span data-ttu-id="c00ca-228">Destekleniyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-228">Supported</span></span>|
|<span data-ttu-id="c00ca-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c00ca-229">ExpressRoute</span></span>| <span data-ttu-id="c00ca-230">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-230">Not Supported</span></span>|
|<span data-ttu-id="c00ca-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="c00ca-231">Hypernet</span></span>| <span data-ttu-id="c00ca-232">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-232">Not Supported</span></span>|
|<span data-ttu-id="c00ca-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="c00ca-233">VPNClient</span></span>| <span data-ttu-id="c00ca-234">Desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="c00ca-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="c00ca-235">Günlük dosyaları</span><span class="sxs-lookup"><span data-stu-id="c00ca-235">Log files</span></span>

<span data-ttu-id="c00ca-236">Kaynak sorun giderme tamamlandıktan sonra hello kaynak sorun giderme günlük dosyalarının bir depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="c00ca-237">Merhaba aşağıdaki görüntüde hello örnek hatayla sonuçlandı bir çağrı içeriğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![zip dosyası][1]

> [!NOTE]
> <span data-ttu-id="c00ca-239">Bazı durumlarda, yalnızca bir alt kümesini hello günlük dosyalarını toostorage yazılır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="c00ca-240">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c00ca-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c00ca-241">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="c00ca-242">Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="c00ca-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="c00ca-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="c00ca-243">ConnectionStats.txt</span></span>

<span data-ttu-id="c00ca-244">Merhaba **ConnectionStats.txt** dosyası hello bağlantı, giriş ve çıkış baytlarını, bağlantı durumu ve bağlantının oluşturulduğu hello zaman hello dahil olmak üzere, genel istatistikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="c00ca-245">API sorun giderme hello çağrısı toohello sağlıklı döndürürse, hello tek şey hello zip dosyasında döndürdü bir **ConnectionStats.txt** dosya.</span><span class="sxs-lookup"><span data-stu-id="c00ca-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="c00ca-246">Bu dosyanın içeriğini Hello aşağıdaki örneğine benzer toohello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c00ca-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="c00ca-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="c00ca-247">CPUStats.txt</span></span>

<span data-ttu-id="c00ca-248">Merhaba **CPUStats.txt** dosyasını içeren CPU kullanımı ve bellek sınama hello aynı anda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="c00ca-249">Bu dosyanın içeriğini Hello benzer toohello örneği aşağıdaki verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c00ca-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="c00ca-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="c00ca-250">IKEErrors.txt</span></span>

<span data-ttu-id="c00ca-251">Merhaba **IKEErrors.txt** dosyasını içeren IKE hataları izleme sırasında bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="c00ca-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="c00ca-252">Merhaba aşağıdaki örnek bir IKEErrors.txt dosyasının hello içeriğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="c00ca-253">Hatalarınızı hello sorunu bağlı olarak farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="c00ca-254">İptal etti wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="c00ca-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="c00ca-255">Merhaba **Scrubbed wfpdiag.txt** günlük dosyası hello wfp günlük içerir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="c00ca-256">Bu günlük paket bırakma ve IKE/AuthIP hataları günlüğe kaydedilmesini içerir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="c00ca-257">Merhaba aşağıdaki örnek hello hello Scrubbed wfpdiag.txt dosyasının içeriğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="c00ca-258">Bu örnekte, bir bağlantısı paylaşılan anahtarı hello satırından hello 3 hello alt görüldüğü gibi doğru değildi.</span><span class="sxs-lookup"><span data-stu-id="c00ca-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="c00ca-259">Aşağıdaki örneğine hello yalnızca hello tüm günlük parçacığıyla aynıdır Hello günlük hello sorunu bağlı olarak uzun olabilir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="c00ca-260">wfpdiag.txt.Sum</span><span class="sxs-lookup"><span data-stu-id="c00ca-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="c00ca-261">Merhaba **wfpdiag.txt.sum** hello arabellek ve işlenen olayların gösteren bir günlük dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c00ca-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="c00ca-262">Merhaba aşağıdaki wfpdiag.txt.sum dosyasının Merhaba içeriğine örnektir.</span><span class="sxs-lookup"><span data-stu-id="c00ca-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="c00ca-263">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c00ca-263">Next steps</span></span>

<span data-ttu-id="c00ca-264">Nasıl toodiagnose VPN ağ geçitleri ve bağlantıları üzerinden ziyaret ederek portal hello öğrenin [ağ geçidi sorun giderme - Azure portalında](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c00ca-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
