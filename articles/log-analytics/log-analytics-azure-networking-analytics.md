---
title: "Günlük analizi ağ Analytics çözümde aaaAzure | Microsoft Docs"
description: "Hello Azure ağ analizi çözümde günlük analizi tooreview Azure ağ güvenlik grubu ve Azure uygulama ağ geçidi günlükleri kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="fccc2-103">Günlük analizi çözümlerinde izleme azure ağ iletişimi</span><span class="sxs-lookup"><span data-stu-id="fccc2-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="fccc2-104">Günlük analizi çözümleri, ağları izleme için aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="fccc2-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="fccc2-105">Ağ Performans İzleyicisi'ne (NPM)</span><span class="sxs-lookup"><span data-stu-id="fccc2-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="fccc2-106">Ağ İzleyicisi Merhaba sistem durumu</span><span class="sxs-lookup"><span data-stu-id="fccc2-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="fccc2-107">Azure uygulama ağ geçidi analytics tooreview</span><span class="sxs-lookup"><span data-stu-id="fccc2-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="fccc2-108">Azure uygulama ağ geçidi günlükleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="fccc2-109">Azure uygulama ağ geçidi ölçümleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="fccc2-110">Azure ağ güvenlik grubu analytics tooreview</span><span class="sxs-lookup"><span data-stu-id="fccc2-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="fccc2-111">Azure ağ güvenlik grubu günlükleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="fccc2-112">Ağ Performans İzleyicisi'ni (NPM)</span><span class="sxs-lookup"><span data-stu-id="fccc2-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="fccc2-113">Merhaba [Ağ Performansı İzleyicisi](log-analytics-network-performance-monitor.md) yönetimi çözümüdür izleme hello sistem durumu, kullanılabilirliği ve ulaşılabilirliği ağların izler çözümü, bir ağ.</span><span class="sxs-lookup"><span data-stu-id="fccc2-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="fccc2-114">Arasında kullanılan toomonitor bağlantısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fccc2-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="fccc2-115">Genel Bulut ve şirket içi</span><span class="sxs-lookup"><span data-stu-id="fccc2-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="fccc2-116">veri merkezleri ve kullanıcı konumları (şubelere)</span><span class="sxs-lookup"><span data-stu-id="fccc2-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="fccc2-117">çok katmanlı bir uygulama çeşitli katmanlarını barındırma alt ağlar.</span><span class="sxs-lookup"><span data-stu-id="fccc2-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="fccc2-118">Daha fazla bilgi için bkz: [Ağ Performansı İzleyicisi](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="fccc2-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="fccc2-119">Azure uygulama ağ geçidi ve ağ güvenlik grubu analizi</span><span class="sxs-lookup"><span data-stu-id="fccc2-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="fccc2-120">toouse hello çözümleri:</span><span class="sxs-lookup"><span data-stu-id="fccc2-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="fccc2-121">Merhaba yönetim çözümü tooLog Analytics, Ekle ve</span><span class="sxs-lookup"><span data-stu-id="fccc2-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="fccc2-122">Tanılama toodirect hello tanılama tooa günlük analizi çalışma alanı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fccc2-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="fccc2-123">Gerekli toowrite hello günlükleri tooAzure Blob Depolama olmadığı.</span><span class="sxs-lookup"><span data-stu-id="fccc2-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="fccc2-124">Tanılama ve hello karşılık gelen çözümü birini veya her ikisini de uygulama ağ geçidi ve ağ güvenlik grupları için etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fccc2-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="fccc2-125">Belirli bir kaynak türü için tanılama günlük kaydını etkinleştirmeyin, ancak hello çözümü yüklemek, hello Pano Kanatlar bu kaynak için boş ve bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="fccc2-126">Ocak 2017 ' Analytics değiştirilen uygulama ağ geçitleri ve ağ güvenlik grupları tooLog günlükleri gönderme şekilde hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="fccc2-127">Hello görürseniz **Azure ağ analizi (kullanım dışı)** çözüm, çok başvurmak[hello eski ağ Analytics çözüm'den geçiş](#migrating-from-the-old-networking-analytics-solution) adımları toofollow gerekir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="fccc2-128">Veri toplama ayrıntıları ağ Azure gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="fccc2-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="fccc2-129">Hello Azure uygulama ağ geçidi analytics ve hello ağ güvenlik grubu analytics Yönetimi çözümlerini doğrudan Azure uygulama ağ geçitleri ve ağ güvenlik grupları tanılama günlüklerini toplayın.</span><span class="sxs-lookup"><span data-stu-id="fccc2-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="fccc2-130">Gerekli toowrite hello günlükleri tooAzure Blob Depolama değil ve aracı için veri toplama gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="fccc2-131">Merhaba aşağıdaki tabloda veri toplama yöntemleri ve Azure uygulama ağ geçidi analizi ve hello ağ güvenlik grubu analiz için verileri nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="fccc2-132">Platform</span><span class="sxs-lookup"><span data-stu-id="fccc2-132">Platform</span></span> | <span data-ttu-id="fccc2-133">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="fccc2-133">Direct agent</span></span> | <span data-ttu-id="fccc2-134">Systems Center Operations Manager Aracısı</span><span class="sxs-lookup"><span data-stu-id="fccc2-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="fccc2-135">Azure</span><span class="sxs-lookup"><span data-stu-id="fccc2-135">Azure</span></span> | <span data-ttu-id="fccc2-136">Operations Manager gerekli?</span><span class="sxs-lookup"><span data-stu-id="fccc2-136">Operations Manager required?</span></span> | <span data-ttu-id="fccc2-137">Operations Manager Aracısı verilerinin yönetim grubu gönderilen</span><span class="sxs-lookup"><span data-stu-id="fccc2-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="fccc2-138">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="fccc2-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="fccc2-139">Azure</span><span class="sxs-lookup"><span data-stu-id="fccc2-139">Azure</span></span> |  |  |<span data-ttu-id="fccc2-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="fccc2-140">&#8226;</span></span> |  |  |<span data-ttu-id="fccc2-141">oturum açıldığında</span><span class="sxs-lookup"><span data-stu-id="fccc2-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="fccc2-142">Azure uygulama ağ geçidi analytics çözümüne günlük analizi</span><span class="sxs-lookup"><span data-stu-id="fccc2-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure uygulama ağ geçidi Analytics simgesi](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="fccc2-144">Uygulama ağ geçitleri için günlükleri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="fccc2-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="fccc2-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="fccc2-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="fccc2-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="fccc2-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="fccc2-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="fccc2-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="fccc2-148">Ölçümleri aşağıdaki hello uygulama ağ geçitleri için desteklenir:</span><span class="sxs-lookup"><span data-stu-id="fccc2-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="fccc2-149">5 dakikalık işleme</span><span class="sxs-lookup"><span data-stu-id="fccc2-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="fccc2-150">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="fccc2-150">Install and configure hello solution</span></span>
<span data-ttu-id="fccc2-151">Aşağıdaki yönergeler tooinstall hello kullanın ve hello Azure uygulama ağ geçidi analiz çözümü yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="fccc2-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="fccc2-152">Hello Azure uygulama ağ geçidi analytics çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="fccc2-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="fccc2-153">Hello için tanılama günlüğünü etkinleştirme [uygulama ağ geçitleri](../application-gateway/application-gateway-diagnostics.md) toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="fccc2-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="fccc2-154">Azure uygulama ağ geçidi tanılama hello portalında etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fccc2-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="fccc2-155">Toohello uygulama ağ geçidi kaynak toomonitor Hello Azure portalına gidin</span><span class="sxs-lookup"><span data-stu-id="fccc2-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="fccc2-156">Seçin *tanılama günlükleri* sayfası aşağıdaki tooopen hello</span><span class="sxs-lookup"><span data-stu-id="fccc2-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure uygulama ağ geçidi kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="fccc2-158">Tıklatın *tanılamayı açın* sayfası aşağıdaki tooopen hello</span><span class="sxs-lookup"><span data-stu-id="fccc2-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure uygulama ağ geçidi kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="fccc2-160">Tanılama üzerinde tooturn tıklatın *üzerinde* altında *durumu*</span><span class="sxs-lookup"><span data-stu-id="fccc2-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="fccc2-161">Merhaba onay kutusunu tıklatın *tooLog Analytics Gönder*</span><span class="sxs-lookup"><span data-stu-id="fccc2-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="fccc2-162">Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fccc2-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="fccc2-163">Altında Hello onay kutusuna tıklayın **günlük** her hello günlük türleri toocollect</span><span class="sxs-lookup"><span data-stu-id="fccc2-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="fccc2-164">Tıklatın *kaydetmek* tooenable hello günlüğe tanılama tooLog analizi</span><span class="sxs-lookup"><span data-stu-id="fccc2-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="fccc2-165">PowerShell kullanarak Azure Ağ Tanılama'yı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fccc2-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="fccc2-166">PowerShell Betiği aşağıdaki hello nasıl bir örnek sağlar tooenable uygulama ağ geçitleri için günlüğü tanılama.</span><span class="sxs-lookup"><span data-stu-id="fccc2-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="fccc2-167">Azure uygulama ağ geçidi analytics kullanın</span><span class="sxs-lookup"><span data-stu-id="fccc2-167">Use Azure Application Gateway analytics</span></span>
![Azure uygulama ağ geçidi analytics döşeme görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="fccc2-169">Merhaba tıklattıktan sonra **Azure uygulama ağ geçidi analytics** döşeme hello genel bakış, günlüklerinizi özetlerini görüntüleyin ve kategorileri aşağıdaki hello toodetails içinde ayrıntıya gidin:</span><span class="sxs-lookup"><span data-stu-id="fccc2-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="fccc2-170">Uygulama ağ geçidi erişimi günlükleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="fccc2-171">Uygulama ağ geçidi erişim günlükleri için istemci ve sunucu hataları</span><span class="sxs-lookup"><span data-stu-id="fccc2-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="fccc2-172">Her uygulama ağ geçidi için saat başına istek sayısı</span><span class="sxs-lookup"><span data-stu-id="fccc2-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="fccc2-173">Saat başına istekleri her uygulama ağ geçidi için başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="fccc2-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="fccc2-174">Uygulama ağ geçitleri için kullanıcı aracısı tarafından hataları</span><span class="sxs-lookup"><span data-stu-id="fccc2-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="fccc2-175">Uygulama ağ geçidi performansı</span><span class="sxs-lookup"><span data-stu-id="fccc2-175">Application Gateway performance</span></span>
  * <span data-ttu-id="fccc2-176">Uygulama ağ geçidi ana bilgisayar durumu</span><span class="sxs-lookup"><span data-stu-id="fccc2-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="fccc2-177">Uygulama ağ geçidi için en yüksek ve 95 yüzdebirlik başarısız istekleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Azure uygulama ağ geçidi analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure uygulama ağ geçidi analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="fccc2-180">Merhaba üzerinde **Azure uygulama ağ geçidi analytics** panoyu hello Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview ayrıntılı hello günlük arama sayfası hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="fccc2-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="fccc2-181">Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fccc2-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="fccc2-182">Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fccc2-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="fccc2-183">Günlük analizi analytics çözümde Azure ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="fccc2-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Azure ağ güvenlik grubu Analytics simgesi](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="fccc2-185">Ağ güvenlik grupları için günlükleri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="fccc2-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="fccc2-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="fccc2-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="fccc2-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="fccc2-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="fccc2-188">Yükleme ve yapılandırma hello çözümü</span><span class="sxs-lookup"><span data-stu-id="fccc2-188">Install and configure hello solution</span></span>
<span data-ttu-id="fccc2-189">Aşağıdaki yönergeler tooinstall hello kullanın ve hello Azure ağ analiz çözümü yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="fccc2-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="fccc2-190">Hello Azure ağ güvenlik grubu analytics çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="fccc2-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="fccc2-191">Hello için tanılama günlüğünü etkinleştirme [ağ güvenlik grubu](../virtual-network/virtual-network-nsg-manage-log.md) toomonitor istediğiniz kaynakları.</span><span class="sxs-lookup"><span data-stu-id="fccc2-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="fccc2-192">Azure ağ güvenlik grubu tanılama hello portalında etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fccc2-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="fccc2-193">Toohello ağ güvenlik grubu kaynak toomonitor Hello Azure portalına gidin</span><span class="sxs-lookup"><span data-stu-id="fccc2-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="fccc2-194">Seçin *tanılama günlükleri* sayfası aşağıdaki tooopen hello</span><span class="sxs-lookup"><span data-stu-id="fccc2-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure ağ güvenlik grubu kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="fccc2-196">Tıklatın *tanılamayı açın* sayfası aşağıdaki tooopen hello</span><span class="sxs-lookup"><span data-stu-id="fccc2-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure ağ güvenlik grubu kaynak görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="fccc2-198">Tanılama üzerinde tooturn tıklatın *üzerinde* altında *durumu*</span><span class="sxs-lookup"><span data-stu-id="fccc2-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="fccc2-199">Merhaba onay kutusunu tıklatın *tooLog Analytics Gönder*</span><span class="sxs-lookup"><span data-stu-id="fccc2-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="fccc2-200">Varolan bir günlük analizi çalışma alanını seçin veya bir çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fccc2-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="fccc2-201">Altında Hello onay kutusuna tıklayın **günlük** her hello günlük türleri toocollect</span><span class="sxs-lookup"><span data-stu-id="fccc2-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="fccc2-202">Tıklatın *kaydetmek* tooenable hello günlüğe tanılama tooLog analizi</span><span class="sxs-lookup"><span data-stu-id="fccc2-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="fccc2-203">PowerShell kullanarak Azure Ağ Tanılama'yı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="fccc2-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="fccc2-204">PowerShell Betiği aşağıdaki hello nasıl bir örnek sağlar tooenable ağ güvenlik grupları için günlük kaydı tanılama</span><span class="sxs-lookup"><span data-stu-id="fccc2-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="fccc2-205">Azure ağ güvenlik grubu kullanın analizi</span><span class="sxs-lookup"><span data-stu-id="fccc2-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="fccc2-206">Merhaba tıklattıktan sonra **Azure ağ güvenlik grubu analytics** döşeme hello genel bakış, günlüklerinizi özetlerini görüntüleyin ve kategorileri aşağıdaki hello toodetails içinde ayrıntıya gidin:</span><span class="sxs-lookup"><span data-stu-id="fccc2-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="fccc2-207">Ağ güvenlik grubu akışları engellendi</span><span class="sxs-lookup"><span data-stu-id="fccc2-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="fccc2-208">Ağ güvenlik grubu kural engellenen akışlarıyla</span><span class="sxs-lookup"><span data-stu-id="fccc2-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="fccc2-209">Engellenen akışlarıyla MAC adresleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="fccc2-210">Ağ güvenlik grubu akışları izin</span><span class="sxs-lookup"><span data-stu-id="fccc2-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="fccc2-211">İzin verilen akışları ile ağ güvenlik grubu kuralları</span><span class="sxs-lookup"><span data-stu-id="fccc2-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="fccc2-212">İzin verilen akışlarıyla MAC adresleri</span><span class="sxs-lookup"><span data-stu-id="fccc2-212">MAC addresses with allowed flows</span></span>

![Azure ağ güvenlik grubu analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure ağ güvenlik grubu analytics Pano görüntüsü](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="fccc2-215">Merhaba üzerinde **Azure ağ güvenlik grubu analytics** panoyu hello Kanatlar birinde hello özet bilgileri gözden geçirin ve ardından bir tooview ayrıntılı hello günlük arama sayfası hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="fccc2-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="fccc2-216">Merhaba günlük arama sayfaları hiçbirinde, sonuçları zaman, ayrıntılı sonuçları ve günlük arama geçmişi görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fccc2-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="fccc2-217">Modelleri toonarrow hello sonuçlarına göre de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fccc2-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="fccc2-218">Merhaba eski ağ Analytics çözüm'den geçiş</span><span class="sxs-lookup"><span data-stu-id="fccc2-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="fccc2-219">Ocak 2017 ' Analytics değiştirilen Azure uygulama ağ geçitleri ve Azure ağ güvenlik grupları tooLog günlükleri gönderme şekilde hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="fccc2-220">Bu değişiklikler hello aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="fccc2-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="fccc2-221">TooLog Analytics hello olmadan gereken doğrudan toouse bir depolama hesabı günlüklerine yazılır</span><span class="sxs-lookup"><span data-stu-id="fccc2-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="fccc2-222">Günlük analizi kullanılabilir olmasını durduracak toothem günlükleri olduğunda hello zamandan daha az gecikme oluşturulan</span><span class="sxs-lookup"><span data-stu-id="fccc2-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="fccc2-223">Daha az yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="fccc2-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="fccc2-224">Azure tanılama tüm türleri için ortak bir biçimi</span><span class="sxs-lookup"><span data-stu-id="fccc2-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="fccc2-225">toouse hello çözümleri güncelleştirildi:</span><span class="sxs-lookup"><span data-stu-id="fccc2-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="fccc2-226">Azure uygulama Gateway bileşenlerinden tooLog Analytics doğrudan gönderilen tanılama toobe yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fccc2-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="fccc2-227">Doğrudan Azure ağ güvenlik gruplarındaki tooLog Analytics gönderilen tanılama toobe yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fccc2-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="fccc2-228">Merhaba etkinleştirmek *Azure uygulama ağ geçidi Analytics* ve hello *Azure ağ güvenlik grubu Analytics* hello işlemi kullanarak çözüm açıklanan [eklemek günlük analizi çözümleri Merhaba Çözümleri Galerisi](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="fccc2-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="fccc2-229">Tüm kayıtlı sorgu, panolar veya uyarıları toouse hello yeni veri türü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="fccc2-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="fccc2-230">TooAzureDiagnostics türüdür.</span><span class="sxs-lookup"><span data-stu-id="fccc2-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="fccc2-231">Merhaba ResourceType toofilter tooAzure ağ günlüklerini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="fccc2-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="fccc2-232">Onun yerine:</span><span class="sxs-lookup"><span data-stu-id="fccc2-232">Instead of:</span></span> | <span data-ttu-id="fccc2-233">Kullanım:</span><span class="sxs-lookup"><span data-stu-id="fccc2-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="fccc2-234">Sonekine sahip herhangi bir alan için \_s, \_d veya \_g hello adı hello ilk karakter toolower harf durumunu değiştir</span><span class="sxs-lookup"><span data-stu-id="fccc2-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="fccc2-235">Sonekine sahip herhangi bir alan için \_adında, hello veri o iç içe geçmiş hello alan adlarını temel alarak tek tek alanlara bölünür.</span><span class="sxs-lookup"><span data-stu-id="fccc2-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="fccc2-236">Merhaba kaldırmak *Azure ağ analizi (kullanım dışı)* çözümü.</span><span class="sxs-lookup"><span data-stu-id="fccc2-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="fccc2-237">PowerShell kullanıyorsanız, kullanın`Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="fccc2-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="fccc2-238">Merhaba değişiklik hello yeni çözümde görünür değil önce veri toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="fccc2-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="fccc2-239">Bu verileri kullanarak hello için eski türü ve alan adları tooquery devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fccc2-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fccc2-240">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fccc2-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="fccc2-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fccc2-241">Next steps</span></span>
* <span data-ttu-id="fccc2-242">Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı Azure Tanılama verileri.</span><span class="sxs-lookup"><span data-stu-id="fccc2-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
