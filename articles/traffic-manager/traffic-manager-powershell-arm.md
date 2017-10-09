---
title: aaaUsing PowerShell toomanage Azure Traffic Manager'da | Microsoft Docs
description: "Trafik Yöneticisi ile Azure kaynak yöneticisi için PowerShell kullanma"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="011f5-103">PowerShell toomanage trafik Yöneticisi'ni kullanma</span><span class="sxs-lookup"><span data-stu-id="011f5-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="011f5-104">Azure Resource Manager hello tercih edilen Yönetim Azure hizmetlerinde arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="011f5-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="011f5-105">Azure Traffic Manager profillerini, Azure Resource Manager tabanlı API'ler ve araçlar kullanılarak yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="011f5-106">Kaynak modeli</span><span class="sxs-lookup"><span data-stu-id="011f5-106">Resource model</span></span>

<span data-ttu-id="011f5-107">Azure Traffic Manager trafik Yöneticisi profili denir ayarlar koleksiyonu kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="011f5-108">Hizmet uç noktaları toowhich trafiği listesini yönlendirilir ve bu profili, DNS ayarlarını, trafik yönlendirme ayarlarını, uç nokta izleme ayarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="011f5-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="011f5-109">Her trafik Yöneticisi profili 'TrafficManagerProfiles' türünde bir kaynak temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="011f5-110">Merhaba REST API düzeyi hello URI her profili için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="011f5-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="011f5-111">Azure PowerShell ayarlama</span><span class="sxs-lookup"><span data-stu-id="011f5-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="011f5-112">Bu yönergeler Microsoft Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="011f5-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="011f5-113">Merhaba aşağıdaki makalede açıklanır nasıl tooinstall ve Azure PowerShell yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="011f5-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="011f5-114">Nasıl tooinstall Azure PowerShell'i ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="011f5-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="011f5-115">Bu makaledeki Hello örnekler, varolan bir kaynak grubu olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="011f5-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="011f5-116">Komutu aşağıdaki hello kullanarak bir kaynak grubu oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="011f5-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="011f5-117">Azure Resource Manager, tüm kaynak gruplarının bir konum olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="011f5-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="011f5-118">Bu konum hello varsayılan olarak bu kaynak grubunda oluşturduğunuz kaynaklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="011f5-119">Trafik Yöneticisi profili kaynaklar olduğundan genel, bölgesel değil, ancak kaynak grubu konumu hello seçimine Azure Traffic Manager üzerinde etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="011f5-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="011f5-120">Trafik Yöneticisi profili oluştur</span><span class="sxs-lookup"><span data-stu-id="011f5-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="011f5-121">toocreate bir Traffic Manager profilini kullanmak hello `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="011f5-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="011f5-122">Aşağıdaki tablonun hello hello parametreleri açıklanır:</span><span class="sxs-lookup"><span data-stu-id="011f5-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="011f5-123">Parametre</span><span class="sxs-lookup"><span data-stu-id="011f5-123">Parameter</span></span> | <span data-ttu-id="011f5-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="011f5-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="011f5-125">Ad</span><span class="sxs-lookup"><span data-stu-id="011f5-125">Name</span></span> |<span data-ttu-id="011f5-126">Merhaba trafik Yöneticisi profili kaynak Hello kaynak adı.</span><span class="sxs-lookup"><span data-stu-id="011f5-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="011f5-127">Aynı Hello profilleri kaynak grubu benzersiz adlara sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="011f5-128">Bu ad, DNS sorgularını kullanılan hello DNS adı ayrıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="011f5-129">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="011f5-129">ResourceGroupName</span></span> |<span data-ttu-id="011f5-130">Merhaba kaynak grubu içeren hello profil kaynak Hello adı.</span><span class="sxs-lookup"><span data-stu-id="011f5-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="011f5-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="011f5-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="011f5-132">Hello trafik yönlendirme yöntemini kullanılan toodetermine hangi uç noktaya bir DNS sorgusu yanıtta döndürülen belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="011f5-133">Olası değerler 'Performans', 'Weighted' veya 'Priority' tır.</span><span class="sxs-lookup"><span data-stu-id="011f5-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="011f5-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="011f5-134">RelativeDnsName</span></span> |<span data-ttu-id="011f5-135">Bu trafik Yöneticisi profili tarafından sağlanan hello DNS adının Hello ana bilgisayar adı bölümü belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="011f5-136">Bu değer, Azure Traffic Manager tooform hello tam etki alanı adıyla hello profilinin (FQDN) kullanılan hello DNS etki alanı adı ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="011f5-137">Örneğin, 'contoso' hello değerini ayarlama 'contoso.trafficmanager.net.' olur</span><span class="sxs-lookup"><span data-stu-id="011f5-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="011f5-138">TTL</span><span class="sxs-lookup"><span data-stu-id="011f5-138">TTL</span></span> |<span data-ttu-id="011f5-139">Merhaba DNS için-yaşam süresi (TTL), saniye cinsinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="011f5-140">Merhaba yerel DNS Çözümleyicileri ve DNS istemcilerini bu TTL bildirir Bu trafik Yöneticisi profili için ne kadar süreyle toocache DNS yanıtları.</span><span class="sxs-lookup"><span data-stu-id="011f5-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="011f5-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="011f5-141">MonitorProtocol</span></span> |<span data-ttu-id="011f5-142">Merhaba Protokolü toouse toomonitor uç nokta durumu belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="011f5-143">Olası değerler şunlardır: 'HTTP' ve 'HTTPS'.</span><span class="sxs-lookup"><span data-stu-id="011f5-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="011f5-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="011f5-144">MonitorPort</span></span> |<span data-ttu-id="011f5-145">Merhaba TCP bağlantı noktası toomonitor uç nokta durumu kullanılan belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="011f5-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="011f5-146">MonitorPath</span></span> |<span data-ttu-id="011f5-147">Merhaba yolu göreli toohello uç nokta etki alanı adı tooprobe uç noktası durumu için kullanılan belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="011f5-148">Merhaba cmdlet ile Azure trafik Yöneticisi profili oluşturur ve karşılık gelen bir profil nesne tooPowerShell döndürür.</span><span class="sxs-lookup"><span data-stu-id="011f5-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="011f5-149">Bu noktada, hello profili uç nokta içermiyor.</span><span class="sxs-lookup"><span data-stu-id="011f5-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="011f5-150">Uç noktaları tooa trafik Yöneticisi profili ekleme hakkında daha fazla bilgi için bkz: [trafik Yöneticisi uç noktaları ekleme](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="011f5-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="011f5-151">Trafik Yöneticisi profilini Al</span><span class="sxs-lookup"><span data-stu-id="011f5-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="011f5-152">tooretrieve var olan trafik Yöneticisi profili nesnesini kullanın hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="011f5-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="011f5-153">Bu cmdlet bir trafik Yöneticisi Profil nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="011f5-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="011f5-154">Trafik Yöneticisi profilini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="011f5-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="011f5-155">Traffic Manager profillerini değiştirme 3 adımlı işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="011f5-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="011f5-156">Alma hello profili kullanarak `Get-AzureRmTrafficManagerProfile` veya hello profili tarafından döndürülen kullanın `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="011f5-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="011f5-157">Hello profil değiştirin.</span><span class="sxs-lookup"><span data-stu-id="011f5-157">Modify hello profile.</span></span> <span data-ttu-id="011f5-158">Ekleme ve uç noktaları kaldırın veya uç nokta veya profil parametrelerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="011f5-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="011f5-159">Bu değişiklikler çevrimdışı işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="011f5-159">These changes are off-line operations.</span></span> <span data-ttu-id="011f5-160">Yalnızca hello profili temsil eden bellekte hello yerel nesnesi değiştiriyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="011f5-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="011f5-161">Hello kullanarak, değişiklikleri `Set-AzureRmTrafficManagerProfile` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="011f5-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="011f5-162">Hello profilinin RelativeDnsName tüm profil özellikleri değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="011f5-163">toochange RelativeDnsName Merhaba, profili ve yeni bir adla yeni bir profil silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="011f5-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="011f5-164">Aşağıdaki örnek hello nasıl toochange hello profilinin TTL gösterir:</span><span class="sxs-lookup"><span data-stu-id="011f5-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="011f5-165">Trafik Yöneticisi uç noktaları üç tür vardır:</span><span class="sxs-lookup"><span data-stu-id="011f5-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="011f5-166">**Azure uç noktaları** Azure üzerinde barındırılan hizmeti</span><span class="sxs-lookup"><span data-stu-id="011f5-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="011f5-167">**Dış uç noktalar** Azure dışında barındırılan hizmeti</span><span class="sxs-lookup"><span data-stu-id="011f5-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="011f5-168">**İç içe uç noktaları** iç içe geçmiş kullanılan tooconstruct hiyerarşileri trafik Yöneticisi profillerine şunlardır.</span><span class="sxs-lookup"><span data-stu-id="011f5-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="011f5-169">İç içe geçmiş uç noktaları karmaşık uygulamalar için Gelişmiş trafik yönlendirme yapılandırmaları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="011f5-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="011f5-170">Her üç durumda, iki yolla uç noktalar eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="011f5-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="011f5-171">Daha önce açıklanan 3 adımlı işlem kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="011f5-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="011f5-172">Bu yöntemin Hello avantajı, birkaç uç noktası değişiklikleri tek bir güncelleştirme yapılabilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="011f5-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="011f5-173">Merhaba yeni AzureRmTrafficManagerEndpoint cmdlet'ini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="011f5-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="011f5-174">Bu cmdlet, tek bir işlemde bir uç nokta tooan varolan trafik Yöneticisi profili ekler.</span><span class="sxs-lookup"><span data-stu-id="011f5-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="011f5-175">Azure uç noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="011f5-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="011f5-176">Azure uç noktaları Azure içinde barındırılan hizmetler başvuru.</span><span class="sxs-lookup"><span data-stu-id="011f5-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="011f5-177">Azure uç noktaları iki tür desteklenir:</span><span class="sxs-lookup"><span data-stu-id="011f5-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="011f5-178">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="011f5-178">Azure Web Apps</span></span>
2. <span data-ttu-id="011f5-179">(Olabilen ekli tooa yük dengeleyici veya bir sanal makine NIC) azure Publicıpaddress kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="011f5-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="011f5-180">Merhaba Publicıpaddress trafik Yöneticisi'nde kullanılan toobe atanmış bir DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="011f5-181">Her durumda:</span><span class="sxs-lookup"><span data-stu-id="011f5-181">In each case:</span></span>

* <span data-ttu-id="011f5-182">Merhaba hizmet hello 'uç noktası Targetresourceıd' parametresi kullanılarak belirtilen `Add-AzureRmTrafficManagerEndpointConfig` veya `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="011f5-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="011f5-183">Merhaba 'Target' ve 'EndpointLocation' hello uç noktası Targetresourceıd tarafından kapsanan.</span><span class="sxs-lookup"><span data-stu-id="011f5-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="011f5-184">Merhaba belirtme 'Weight' isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="011f5-185">Hello profil yapılandırılmış toouse hello 'Weighted' trafik yönlendirme yöntemini ise ağırlıkları yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="011f5-186">Aksi takdirde, bunlar yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="011f5-187">Belirtilen başlangıç değeri 1 ile 1000 arasında bir sayı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="011f5-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="011f5-188">Merhaba varsayılan değer, '1' dir.</span><span class="sxs-lookup"><span data-stu-id="011f5-188">hello default value is '1'.</span></span>
* <span data-ttu-id="011f5-189">Belirten hello 'Priority' isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="011f5-190">Hello profil yapılandırılmış toouse hello 'Priority' trafik yönlendirme yöntemini ise öncelikleri yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="011f5-191">Aksi takdirde, bunlar yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="011f5-192">Geçerli değerler 1 too1000 daha yüksek öncelik belirten alt ile değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="011f5-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="011f5-193">Bir uç nokta için belirtilmişse, tüm uç noktaları için belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="011f5-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="011f5-194">Atlanırsa, varsayılan değerleri '1'den başlayarak hello uç noktası listelenmez hello sırayla uygulanır.</span><span class="sxs-lookup"><span data-stu-id="011f5-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="011f5-195">Örnek 1: kullanarak Web uygulama uç noktaları ekleme`Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="011f5-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="011f5-196">Bu örnekte, size bir trafik Yöneticisi profili oluşturun ve hello kullanarak iki Web uygulaması uç nokta ekleyin `Add-AzureRmTrafficManagerEndpointConfig` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="011f5-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="011f5-197">Örnek 2: Publicıpaddress kullanarak uç nokta ekleme`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="011f5-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="011f5-198">Bu örnekte, bir ortak IP adresi kaynağı toohello trafik Yöneticisi profili eklenir.</span><span class="sxs-lookup"><span data-stu-id="011f5-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="011f5-199">Hello genel IP adresi yapılandırılmış bir DNS adına sahip olmalıdır ve her iki toohello NIC VM veya tooa yük dengeleyicinin bağlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="011f5-200">Dış uç noktalar ekleme</span><span class="sxs-lookup"><span data-stu-id="011f5-200">Adding External Endpoints</span></span>

<span data-ttu-id="011f5-201">Dış uç noktalar toodirect trafiği tooservices Azure dışında barındırılan Yöneticisi kullanır trafiği.</span><span class="sxs-lookup"><span data-stu-id="011f5-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="011f5-202">Dış uç noktalar ya da Azure uç noktaları ile eklenen kullanarak `Add-AzureRmTrafficManagerEndpointConfig` arkasından `Set-AzureRmTrafficManagerProfile`, veya `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="011f5-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="011f5-203">Dış uç noktalar belirtirken:</span><span class="sxs-lookup"><span data-stu-id="011f5-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="011f5-204">Merhaba 'Target' parametresini kullanarak Hello uç noktası etki alanı adı belirtilmelidir</span><span class="sxs-lookup"><span data-stu-id="011f5-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="011f5-205">Merhaba 'EndpointLocation' Hello 'Performans' trafik yönlendirme yöntemini kullandıysanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="011f5-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="011f5-206">Aksi takdirde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-206">Otherwise it is optional.</span></span> <span data-ttu-id="011f5-207">Merhaba değeri olmalıdır bir [geçerli Azure bölgesi adı](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="011f5-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="011f5-208">'Ağırlık' hello ve 'Priority' isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="011f5-209">Örnek 1: kullanarak dış uç noktalar ekleme `Add-AzureRmTrafficManagerEndpointConfig` ve`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="011f5-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="011f5-210">Bu örnekte, size bir trafik Yöneticisi profili oluşturun, iki dış uç noktalar ekleme ve hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="011f5-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="011f5-211">Örnek 2: kullanarak dış uç noktalar ekleme`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="011f5-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="011f5-212">Bu örnekte, bir dış uç noktası tooan varolan profili ekleyin.</span><span class="sxs-lookup"><span data-stu-id="011f5-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="011f5-213">Hello profil hello profili ve kaynak grubu adları kullanılarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="011f5-214">'İç içe' uç noktaları ekleme</span><span class="sxs-lookup"><span data-stu-id="011f5-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="011f5-215">Her trafik Yöneticisi profili, tek bir trafik yönlendirme yöntemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="011f5-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="011f5-216">Ancak, tek bir trafik Yöneticisi profili tarafından sağlanan hello yönlendirme çok daha karmaşık trafik yönlendirme gerektiren senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="011f5-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="011f5-217">Trafik Yöneticisi profilleri toocombine hello birden fazla trafik yönlendirme yöntemini yararları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="011f5-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="011f5-218">İç içe profil toooverride hello varsayılan trafik Yöneticisi davranışı toosupport daha büyük ve daha karmaşık uygulama dağıtımları izin verir.</span><span class="sxs-lookup"><span data-stu-id="011f5-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="011f5-219">Daha ayrıntılı örnekler için bkz: [iç içe trafik Yöneticisi profillerine](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="011f5-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="011f5-220">İç içe geçmiş uç noktalarını kullanarak belirli bir uç nokta türü, 'NestedEndpoints' hello üst profilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="011f5-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="011f5-221">İç içe geçmiş uç noktaları belirtirken:</span><span class="sxs-lookup"><span data-stu-id="011f5-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="011f5-222">Merhaba 'uç noktası Targetresourceıd' parametresini kullanarak Hello uç noktası belirtilmelidir</span><span class="sxs-lookup"><span data-stu-id="011f5-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="011f5-223">Merhaba 'EndpointLocation' Hello 'Performans' trafik yönlendirme yöntemini kullandıysanız gereklidir.</span><span class="sxs-lookup"><span data-stu-id="011f5-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="011f5-224">Aksi takdirde isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-224">Otherwise it is optional.</span></span> <span data-ttu-id="011f5-225">Merhaba değeri olmalıdır bir [geçerli Azure bölgesi adı](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="011f5-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="011f5-226">'Ağırlık' hello ve 'Priority' için olduğu gibi Azure uç noktaları isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="011f5-227">Merhaba 'MinChildEndpoints' parametresi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="011f5-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="011f5-228">Merhaba varsayılan değer, '1' dir.</span><span class="sxs-lookup"><span data-stu-id="011f5-228">hello default value is '1'.</span></span> <span data-ttu-id="011f5-229">Kullanılabilir uç nokta Hello sayısı bu eşiğin altına düşmesi durumunda hello üst profili hello alt profil 'düşürülmüş' ve diğer uç noktalardan hello üst profili trafiği toohello yönlendiren dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="011f5-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="011f5-230">Örnek 1: kullanarak iç içe geçmiş uç noktaları ekleme `Add-AzureRmTrafficManagerEndpointConfig` ve`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="011f5-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="011f5-231">Bu örnekte, biz yeni trafik Yöneticisi alt ve üst profilleri oluşturma, hello alt iç içe geçmiş endpoint toohello üst öğe olarak ekleyin ve hello değişiklikleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="011f5-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="011f5-232">Bu örnekte okumanızdır, biz herhangi diğer uç noktaları toohello alt veya üst profilleri eklemediniz.</span><span class="sxs-lookup"><span data-stu-id="011f5-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="011f5-233">Örnek 2: kullanarak iç içe geçmiş uç noktaları ekleme`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="011f5-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="011f5-234">Bu örnekte, biz var olan bir alt profilini bir iç içe geçmiş endpoint tooan varolan üst profili ekleyin.</span><span class="sxs-lookup"><span data-stu-id="011f5-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="011f5-235">Hello profil hello profili ve kaynak grubu adları kullanılarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="011f5-236">Trafik Yöneticisi uç noktasını güncelleyin</span><span class="sxs-lookup"><span data-stu-id="011f5-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="011f5-237">Mevcut bir trafik Yöneticisi uç noktası iki yolu tooupdate vardır:</span><span class="sxs-lookup"><span data-stu-id="011f5-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="011f5-238">Merhaba trafik Yöneticisi profili kullanarak Al `Get-AzureRmTrafficManagerProfile`güncelleştirme hello profilindeki hello uç nokta özellikleri ve değişiklikleri kullanarak hello `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="011f5-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="011f5-239">Bu yöntem tek bir işlemde birden fazla uç mümkün tooupdate olma hello avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="011f5-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="011f5-240">Merhaba kullanan trafik Yöneticisi uç noktasını alın `Get-AzureRmTrafficManagerEndpoint`güncelleştirme hello uç nokta özellikleri ve değişiklikleri kullanarak hello `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="011f5-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="011f5-241">Merhaba uç noktaları hello profil dizisinde içine dizin gerektirmediğinden bu yöntem basittir.</span><span class="sxs-lookup"><span data-stu-id="011f5-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="011f5-242">Örnek 1: kullanarak uç noktaları güncelleştirme `Get-AzureRmTrafficManagerProfile` ve`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="011f5-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="011f5-243">Bu örnekte, iki uç nokta bir profil içinde hello öncelik değiştirin.</span><span class="sxs-lookup"><span data-stu-id="011f5-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="011f5-244">Örnek 2: bir uç nokta kullanarak güncelleştirme `Get-AzureRmTrafficManagerEndpoint` ve`Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="011f5-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="011f5-245">Bu örnekte, var olan bir profili tek bir uç noktası hello ağırlığını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="011f5-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="011f5-246">Etkinleştirme ve uç noktaları ve profilleri devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="011f5-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="011f5-247">Trafik Yöneticisi etkin ve devre dışı, etkinleştirme ve tüm profillerini devre dışı bırakma izin vererek yanı sıra tekil uç noktalarını toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="011f5-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="011f5-248">Bu değişiklikler alma/güncelleştirme/ayarı hello uç noktası veya profili kaynaklar tarafından yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="011f5-249">toostreamline bu yaygın işlemler de adanmış cmdlet'leri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="011f5-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="011f5-250">Örnek 1: Etkinleştirme ve trafik Yöneticisi profili devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="011f5-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="011f5-251">tooenable bir Traffic Manager profilini kullanmak `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="011f5-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="011f5-252">Hello profili, bir profil nesnesi kullanılarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="011f5-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="011f5-253">Hello profil nesnesi hello ardışık düzeni aracılığıyla veya hello kullanarak geçirilebilir '-TrafficManagerProfile' parametresi.</span><span class="sxs-lookup"><span data-stu-id="011f5-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="011f5-254">Bu örnekte, biz hello profili tarafından hello profili ve kaynak grubu adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="011f5-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="011f5-255">Trafik Yöneticisi profili toodisable:</span><span class="sxs-lookup"><span data-stu-id="011f5-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="011f5-256">Merhaba devre dışı bırakma AzureRmTrafficManagerProfile cmdlet onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="011f5-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="011f5-257">Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.</span><span class="sxs-lookup"><span data-stu-id="011f5-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="011f5-258">Örnek 2: Etkinleştirme ve trafik Yöneticisi uç noktası devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="011f5-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="011f5-259">tooenable bir trafik Yöneticisi uç noktası kullan `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="011f5-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="011f5-260">İki yolu toospecify hello endpoint vardır</span><span class="sxs-lookup"><span data-stu-id="011f5-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="011f5-261">Merhaba ardışık düzeni geçirilen TrafficManagerEndpoint nesnesi veya hello kullanarak '-TrafficManagerEndpoint' parametresi</span><span class="sxs-lookup"><span data-stu-id="011f5-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="011f5-262">Merhaba uç nokta adı, uç nokta türü, profil adı ve kaynak grubu adı kullanma:</span><span class="sxs-lookup"><span data-stu-id="011f5-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="011f5-263">Benzer şekilde, toodisable trafik Yöneticisi uç noktası:</span><span class="sxs-lookup"><span data-stu-id="011f5-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="011f5-264">İle `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet için onay ister.</span><span class="sxs-lookup"><span data-stu-id="011f5-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="011f5-265">Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.</span><span class="sxs-lookup"><span data-stu-id="011f5-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="011f5-266">Trafik Yöneticisi uç noktasını sil</span><span class="sxs-lookup"><span data-stu-id="011f5-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="011f5-267">tooremove tekil uç noktalarını kullanmak hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="011f5-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="011f5-268">Bu cmdlet onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="011f5-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="011f5-269">Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.</span><span class="sxs-lookup"><span data-stu-id="011f5-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="011f5-270">Trafik Yöneticisi profilini Sil</span><span class="sxs-lookup"><span data-stu-id="011f5-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="011f5-271">toodelete bir Traffic Manager profilini kullanmak hello `Remove-AzureRmTrafficManagerProfile` hello profili ve kaynak grubu adlarını belirtme cmdlet:</span><span class="sxs-lookup"><span data-stu-id="011f5-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="011f5-272">Bu cmdlet onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="011f5-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="011f5-273">Bu istemi hello kullanılarak gizlenebilir. '-Force' parametresi.</span><span class="sxs-lookup"><span data-stu-id="011f5-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="011f5-274">hello profil toobe silinmiş bir profil nesnesi kullanılarak da belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="011f5-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="011f5-275">Bu sıra ayrıca yöneltilen:</span><span class="sxs-lookup"><span data-stu-id="011f5-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="011f5-276">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="011f5-276">Next steps</span></span>

[<span data-ttu-id="011f5-277">Trafik Yöneticisi izleme</span><span class="sxs-lookup"><span data-stu-id="011f5-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="011f5-278">Traffic Manager için performans konuları</span><span class="sxs-lookup"><span data-stu-id="011f5-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
