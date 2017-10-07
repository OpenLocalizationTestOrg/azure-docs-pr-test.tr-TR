---
title: "aaaMonitor uygulama ağ geçidi için erişim günlükleri, performans günlükleri, arka uç sistem durumu ve ölçümleri | Microsoft Docs"
description: "Bilgi nasıl tooenable ve uygulama ağ geçidi için erişim günlüklerini ve performans günlüklerini yönetme"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="7a3e6-103">Arka uç sistem durumu, tanılama günlüklerini ve uygulama ağ geçidi ölçümleri</span><span class="sxs-lookup"><span data-stu-id="7a3e6-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="7a3e6-104">Azure uygulama ağ geçidi kullanarak yolları aşağıdaki hello kaynaklarında izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="7a3e6-105">[Arka uç sistem durumu](#back-end-health): uygulama ağ geçidi arka uç havuzları ve PowerShell hello Azure portal aracılığıyla hello yetenek toomonitor hello hello hello sunucuları durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="7a3e6-106">Merhaba arka uç havuzları hello performans tanılama günlükleri aracılığıyla hello durumunu da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="7a3e6-107">[Günlükleri](#diagnostic-logs): günlükleri izin performans için erişim ve diğer veri toobe kaydedildi veya izleme amacıyla bir kaynaktan tüketilen.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="7a3e6-108">[Ölçümleri](#metrics): uygulama ağ geçidi şu anda bir ölçüm yok.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="7a3e6-109">Bu ölçüm, saniye başına baytların hello uygulama ağ geçidi hello verimini ölçer.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="7a3e6-110">Arka uç sistem durumu</span><span class="sxs-lookup"><span data-stu-id="7a3e6-110">Back-end health</span></span>

<span data-ttu-id="7a3e6-111">Uygulama ağ geçidi hello yetenek toomonitor hello hello arka uç havuzları hello portal, PowerShell ve hello komut satırı arabirimi (CLI) aracılığıyla tek tek üyeleri durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="7a3e6-112">Birleşik bir sistem durumu da bulabilirsiniz hello performans tanılama günlükleri aracılığıyla arka uç havuzları özeti.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="7a3e6-113">Merhaba arka uç sistem durumu raporu hello çıktı hello uygulama ağ geçidi durumu araştırma toohello arka uç örneklerinin yansıtır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="7a3e6-114">Yoklama başarılı olduğunda ve geri hello son trafik alabilir, sağlıklı kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="7a3e6-115">Aksi takdirde, kötü olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a3e6-116">Bir uygulama ağ geçidi alt ağı üzerinde bir ağ güvenlik grubu (NSG) varsa, bağlantı noktası aralıkları 65503 65534 hello uygulama ağ geçidi alt gelen trafik için açın.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="7a3e6-117">Bu bağlantı noktaları hello arka uç sistem API toowork için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="7a3e6-118">Merhaba Portalı aracılığıyla arka uç durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="7a3e6-118">View back-end health through hello portal</span></span>

<span data-ttu-id="7a3e6-119">Merhaba Portalı'nda, arka uç sistem durumu otomatik olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="7a3e6-120">Mevcut bir uygulama ağ geçidi içinde seçin **izleme** > **arka uç sistem durumu**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="7a3e6-121">(Bu bir NIC, IP veya FQDN olup olmadığı) hello arka uç havuzu içindeki her üyenin bu sayfada listelenir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="7a3e6-122">Arka uç havuzu adını, bağlantı noktası, arka uç HTTP ayarları adı ve sistem durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="7a3e6-123">Sistem durumu için geçerli değerler **sağlıklı**, **sağlıksız**, ve **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="7a3e6-124">Arka uç sistem durumunu görüyorsanız, **bilinmeyen**, bu erişim toohello arka uç engellenmez bir NSG kuralı, bir kullanıcı tanımlı yönlendirme (UDR) veya özel DNS hello sanal ağındaki emin olun.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![Arka uç sistem durumu][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="7a3e6-126">PowerShell aracılığıyla arka uç durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="7a3e6-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="7a3e6-127">PowerShell koddan hello gösterir kullanarak tooview arka uç sistem durumu nasıl hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="7a3e6-128">Azure CLI 2.0 aracılığıyla arka uç durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="7a3e6-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="7a3e6-129">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="7a3e6-129">Results</span></span>

<span data-ttu-id="7a3e6-130">Aşağıdaki kod parçacığında hello hello yanıt örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="7a3e6-131"><a name="diagnostic-logging"></a>Tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="7a3e6-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="7a3e6-132">Günlükleri farklı türlerde içinde Azure toomanage kullanın ve uygulama ağ geçitleri giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="7a3e6-133">Bu günlükler bazıları hello portalı üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="7a3e6-134">Tüm günlükler Azure Blob depolama alanından ayıklanan ve farklı Araçlar'da gibi görüntülenebilir [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md), Excel ve Power BI.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="7a3e6-135">Merhaba farklı türlerinden günlükleri listesi aşağıdaki hello hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="7a3e6-136">**Etkinlik günlüğü**: kullanabileceğiniz [Azure etkinlik günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) (önceki adıyla işletimsel ve Denetim günlükleri olarak bilinir) tooview olmayan tüm işlemleri tooyour Azure aboneliği ve durumlarını gönderildi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="7a3e6-137">Etkinlik günlüğü girişleri varsayılan olarak toplanır ve hello Azure portal görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="7a3e6-138">**Erişim günlüğüne**: Bu günlük tooview uygulama ağ geçidi erişim desenlerini kullanın ve önemli bilgiler, dahil olmak üzere hello arayanın IP, istenen URL, yanıt gecikme, dönüş kodu ve bayt giriş ve çıkış analiz edin. Bir erişim günlüğü, her 300 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="7a3e6-139">Bu günlük, uygulama ağ geçidi örneği başına bir kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="7a3e6-140">Merhaba uygulama ağ geçidi örneği hello InstanceId özelliği tarafından belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="7a3e6-141">**Performans günlüğü**: uygulama ağ geçidi örneklerinin nasıl gerçekleştirmekte bu günlük tooview kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="7a3e6-142">Bu günlük sunulan, toplam istekleri dahil olmak üzere her bir örnek, üretilen iş bayt performans bilgilerini yakalar, toplam istek sayısı sunulan, başarısız istek sayısını ve sağlıklı ve sağlıksız arka uç örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="7a3e6-143">Bir performans günlüğü, her 60 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="7a3e6-144">**Güvenlik Duvarı günlük**: hello web uygulaması güvenlik duvarı ile yapılandırılmış bir uygulama Ağ Geçidi algılama veya önleme modu üzerinden oturum bu günlük tooview hello isteklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="7a3e6-145">Günlükleri, yalnızca hello Azure Resource Manager dağıtım modelinde dağıtılan kaynaklar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7a3e6-146">Merhaba Klasik dağıtım modelinde kaynakların günlükleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="7a3e6-147">Merhaba daha iyi hello iki modellerinin anlamak için bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="7a3e6-148">Günlüklerinizi depolamak için üç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="7a3e6-149">**Depolama hesabı**: günlükleri uzun bir süre depolandığında ve gerektiğinde gözden depolama hesapları günlükleri için en iyi kullanımı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="7a3e6-150">**Olay hub'ları**: olay hub'ları olan diğer güvenlik bilgilerini ile tümleştirmek için harika bir seçenek ve Olay yönetimi (SEIM) araçları kaynaklarınızı tooget uyarılar.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="7a3e6-151">**Günlük analizi**: günlük analizi uygulamanızın veya genel gerçek zamanlı izleme veya eğilimleri bakarak için en iyi şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="7a3e6-152">PowerShell aracılığıyla günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="7a3e6-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="7a3e6-153">Etkinlik günlüğü her Resource Manager kaynak için otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="7a3e6-154">Erişim ve bu günlükleri kullanılabilir hello veri toplama performans günlüğü toostart etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="7a3e6-155">Günlük, aşağıdaki adımları kullanın hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="7a3e6-156">Merhaba günlük verilerinin depolandığı, depolama hesabınızın kaynak kimliği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="7a3e6-157">Bu değer hello şekildedir: /subscriptions/\<Subscriptionıd\>/resourceGroups/\<kaynak grubu adı\>/providers/Microsoft.Storage/storageAccounts/\<depolama hesabı adı\>.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="7a3e6-158">Aboneliğinizdeki herhangi bir depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="7a3e6-159">Hello Azure portal toofind bu bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-159">You can use hello Azure portal toofind this information.</span></span>

    ![Portal: depolama hesabı kaynak kimliği](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="7a3e6-161">Günlük kaydı etkin uygulama ağ geçidinizin kaynak kimliği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="7a3e6-162">Bu değer hello şekildedir: /subscriptions/\<Subscriptionıd\>/resourceGroups/\<kaynak grubu adı\>/providers/Microsoft.Network/applicationGateways/\<uygulama ağ geçidi ad\>.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="7a3e6-163">Merhaba portal toofind bu bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-163">You can use hello portal toofind this information.</span></span>

    ![Portal: uygulama ağ geçidi kaynak kimliği](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="7a3e6-165">Merhaba aşağıdaki PowerShell cmdlet'ini kullanarak tanılama günlük kaydını etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="7a3e6-166">Etkinlik günlükleri ayrı bir depolama hesabı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="7a3e6-167">Depolama Hello kullanılması erişimi ve performans günlüğünü servis ücretleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="7a3e6-168">Azure portal Hello günlüğü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7a3e6-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="7a3e6-169">İçinde Azure portal Merhaba, kaynağınızı bulun ve tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="7a3e6-170">Uygulama ağ geçidi için üç günlük vardır:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="7a3e6-171">Erişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-171">Access log</span></span>
   * <span data-ttu-id="7a3e6-172">Performans günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-172">Performance log</span></span>
   * <span data-ttu-id="7a3e6-173">Güvenlik Duvarı günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-173">Firewall log</span></span>

2. <span data-ttu-id="7a3e6-174">veri toplama toostart, tıklatın **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![Tanılama açma][1]

3. <span data-ttu-id="7a3e6-176">Merhaba **tanılama ayarları** dikey penceresinde hello ayarları hello için tanılama günlükleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="7a3e6-177">Bu örnekte, günlük analizi hello günlükleri depolar.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="7a3e6-178">Tıklatın **yapılandırma** altında **günlük analizi** tooconfigure çalışma alanınızı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="7a3e6-179">Olay hub'ları ve bir depolama hesabı toosave hello tanılama günlüklerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Merhaba yapılandırma işlemini başlatma][2]

4. <span data-ttu-id="7a3e6-181">Varolan bir Operations Management Suite (OMS) çalışma alanını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="7a3e6-182">Bu örnek, mevcut bir kullanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-182">This example uses an existing one.</span></span>

   ![OMS çalışma alanları için seçenekleri][3]

5. <span data-ttu-id="7a3e6-184">Hello ayarları onaylayın ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-184">Confirm hello settings and click **Save**.</span></span>

   ![Tanılama ayarları dikey seçimleri][4]

### <a name="activity-log"></a><span data-ttu-id="7a3e6-186">Etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-186">Activity log</span></span>

<span data-ttu-id="7a3e6-187">Azure hello etkinlik günlüğü varsayılan olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="7a3e6-188">Merhaba günlükleri 90 gün boyunca hello Azure olay günlüklerini deposunda korunur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="7a3e6-189">Merhaba okuyarak Bu günlükler hakkında daha fazla bilgi [olayları ve etkinlik günlüğü görüntüle](../monitoring-and-diagnostics/insights-debugging-with-events.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="7a3e6-190">Erişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-190">Access log</span></span>

<span data-ttu-id="7a3e6-191">Ayrıntılı adımları önceki hello biçimde açıklandığı gibi her bir uygulama ağ geçidi örnek üzerinde yalnızca etkinleştirdikten ise hello erişim günlüğü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="7a3e6-192">Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="7a3e6-193">Uygulama ağ geçidi'nin her erişim JSON biçiminde hello aşağıdaki örnekte gösterildiği gibi kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="7a3e6-194">Değer</span><span class="sxs-lookup"><span data-stu-id="7a3e6-194">Value</span></span>  |<span data-ttu-id="7a3e6-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a3e6-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7a3e6-196">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="7a3e6-196">instanceId</span></span>     | <span data-ttu-id="7a3e6-197">Uygulama ağ geçidi örneği, sunulacak hello isteği.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="7a3e6-198">ClientIP</span><span class="sxs-lookup"><span data-stu-id="7a3e6-198">clientIP</span></span>     | <span data-ttu-id="7a3e6-199">Kaynak IP hello istek için.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="7a3e6-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="7a3e6-200">clientPort</span></span>     | <span data-ttu-id="7a3e6-201">Merhaba istek için kaynak bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="7a3e6-202">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="7a3e6-202">httpMethod</span></span>     | <span data-ttu-id="7a3e6-203">Merhaba isteği tarafından kullanılan HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="7a3e6-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="7a3e6-204">requestUri</span></span>     | <span data-ttu-id="7a3e6-205">Merhaba URI'sini isteği aldı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="7a3e6-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="7a3e6-206">RequestQuery</span></span>     | <span data-ttu-id="7a3e6-207">**Sunucu yönlendirilen**: hello isteğin gönderildiği arka uç havuzu örnek.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="7a3e6-208">**X-AzureApplicationGateway-günlük-ID**: bağıntı hello istek için kullanılan kimliği.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="7a3e6-209">Merhaba arka uç sunucularda kullanılan tootroubleshoot trafiği sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="7a3e6-210">**Sunucu durumu**: uygulama ağ geçidi hello arka uçtan alınan HTTP yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="7a3e6-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="7a3e6-211">UserAgent</span></span>     | <span data-ttu-id="7a3e6-212">Kullanıcı Aracısı'ndan hello HTTP istek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="7a3e6-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="7a3e6-213">httpStatus</span></span>     | <span data-ttu-id="7a3e6-214">HTTP durum kodu toohello istemci uygulama ağ geçidi'nden döndürdü.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="7a3e6-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="7a3e6-215">httpVersion</span></span>     | <span data-ttu-id="7a3e6-216">Merhaba İstek HTTP sürümü.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="7a3e6-217">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="7a3e6-217">receivedBytes</span></span>     | <span data-ttu-id="7a3e6-218">Paket, alınan bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="7a3e6-219">SentBytes</span><span class="sxs-lookup"><span data-stu-id="7a3e6-219">sentBytes</span></span>| <span data-ttu-id="7a3e6-220">Paket, gönderilen bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="7a3e6-221">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="7a3e6-221">timeTaken</span></span>| <span data-ttu-id="7a3e6-222">Uzunluk, işlenen istek toobe ve gönderilen kendi yanıt toobe için geçen süre (milisaniye cinsinden).</span><span class="sxs-lookup"><span data-stu-id="7a3e6-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="7a3e6-223">Bu uygulama ağ geçidi hello ilk bayta kalan süreyi hello yanıt işlemi tamamlanmadan gönderdiğinizde bir HTTP isteği toohello zaman alır hello zamandan hello aralığı olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="7a3e6-224">Karşılama istek ve yanıt paketleri hello ağ üzerinden yolculuk hello süresi geçen süre alan genellikle hello toonote içerir önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="7a3e6-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="7a3e6-225">sslEnabled</span></span>| <span data-ttu-id="7a3e6-226">SSL iletişimi toohello arka uç havuzları kullanılıp.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="7a3e6-227">Açma ve kapatma değerler geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="7a3e6-228">Performans günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-228">Performance log</span></span>

<span data-ttu-id="7a3e6-229">Ayrıntılı adımları önceki hello biçimde açıklandığı gibi her bir uygulama ağ geçidi örnek üzerinde yalnızca etkinleştirdiyseniz, hello performans günlüğü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="7a3e6-230">Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="7a3e6-231">Merhaba performans günlüğü verilerini 1 dakikalık aralıklarla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="7a3e6-232">Veri aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-232">hello following data is logged:</span></span>


|<span data-ttu-id="7a3e6-233">Değer</span><span class="sxs-lookup"><span data-stu-id="7a3e6-233">Value</span></span>  |<span data-ttu-id="7a3e6-234">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a3e6-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7a3e6-235">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="7a3e6-235">instanceId</span></span>     |  <span data-ttu-id="7a3e6-236">Uygulama ağ geçidi örneği performans verileri oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="7a3e6-237">Birden çok örnekli uygulama ağ geçidi için örneği başına bir satır yok.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="7a3e6-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="7a3e6-238">healthyHostCount</span></span>     | <span data-ttu-id="7a3e6-239">Merhaba arka uç havuzundaki sağlıklı ana bilgisayar sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="7a3e6-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="7a3e6-240">unHealthyHostCount</span></span>     | <span data-ttu-id="7a3e6-241">Merhaba arka uç havuzundaki sağlıksız ana bilgisayar sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="7a3e6-242">RequestCount</span><span class="sxs-lookup"><span data-stu-id="7a3e6-242">requestCount</span></span>     | <span data-ttu-id="7a3e6-243">Hizmet isteği sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-243">Number of requests served.</span></span>        |
|<span data-ttu-id="7a3e6-244">Gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="7a3e6-244">latency</span></span> | <span data-ttu-id="7a3e6-245">Gecikme süresi (milisaniye cinsinden) hello örneği toohello gelen istekleri hello istekleri hizmet uç yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="7a3e6-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="7a3e6-246">failedRequestCount</span></span>| <span data-ttu-id="7a3e6-247">Başarısız istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-247">Number of failed requests.</span></span>|
|<span data-ttu-id="7a3e6-248">Üretilen iş</span><span class="sxs-lookup"><span data-stu-id="7a3e6-248">throughput</span></span>| <span data-ttu-id="7a3e6-249">Saniyedeki bayt cinsinden hello son günlük itibaren ortalama performansıdır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="7a3e6-250">Gecikme hello HTTP isteğin ilk baytını hello hello HTTP yanıtı son baytını hello gönderildiğinde alınan toohello zaman olduğunda hello zamandan hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="7a3e6-251">Buna ait hello toplamını hello uygulama ağ geçidi işleme artı hello maliyet ağ toohello end, arka uç alır tooprocess hello isteği hello hello saati.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="7a3e6-252">Güvenlik Duvarı günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-252">Firewall log</span></span>

<span data-ttu-id="7a3e6-253">önceki adımları hello içinde ayrıntılı olarak her uygulama ağ geçidi için yalnızca etkinleştirdiyseniz, hello Güvenlik Duvarı günlük oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="7a3e6-254">Bu günlük, aynı zamanda bu hello web uygulaması güvenlik duvarı bir uygulama ağ geçidi üzerinde yapılandırılmış gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="7a3e6-255">Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="7a3e6-256">Veri aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-256">hello following data is logged:</span></span>


|<span data-ttu-id="7a3e6-257">Değer</span><span class="sxs-lookup"><span data-stu-id="7a3e6-257">Value</span></span>  |<span data-ttu-id="7a3e6-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a3e6-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7a3e6-259">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="7a3e6-259">instanceId</span></span>     | <span data-ttu-id="7a3e6-260">Uygulama ağ geçidi örneği için hangi güvenlik duvarı veri oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="7a3e6-261">Birden çok örnekli uygulama ağ geçidi için örneği başına bir satır yok.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="7a3e6-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="7a3e6-262">clientIp</span></span>     |   <span data-ttu-id="7a3e6-263">Kaynak IP hello istek için.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="7a3e6-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="7a3e6-264">clientPort</span></span>     |  <span data-ttu-id="7a3e6-265">Merhaba istek için kaynak bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="7a3e6-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="7a3e6-266">requestUri</span></span>     | <span data-ttu-id="7a3e6-267">Merhaba, bir URL isteği aldı.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="7a3e6-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="7a3e6-268">ruleSetType</span></span>     | <span data-ttu-id="7a3e6-269">Kural türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-269">Rule set type.</span></span> <span data-ttu-id="7a3e6-270">Merhaba kullanılabilir OWASP değerdir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="7a3e6-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="7a3e6-271">ruleSetVersion</span></span>     | <span data-ttu-id="7a3e6-272">Kural kullanılan sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-272">Rule set version used.</span></span> <span data-ttu-id="7a3e6-273">Değerleri 2.2.9 ve 3.0 kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="7a3e6-274">RuleId</span><span class="sxs-lookup"><span data-stu-id="7a3e6-274">ruleId</span></span>     | <span data-ttu-id="7a3e6-275">Olay tetikleme hello kuralı kimliği.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="7a3e6-276">İleti</span><span class="sxs-lookup"><span data-stu-id="7a3e6-276">message</span></span>     | <span data-ttu-id="7a3e6-277">Olay tetikleme hello için kullanıcı dostu iletisi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="7a3e6-278">Daha fazla ayrıntı hello Ayrıntılar bölümünde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="7a3e6-279">Eylem</span><span class="sxs-lookup"><span data-stu-id="7a3e6-279">action</span></span>     |  <span data-ttu-id="7a3e6-280">Merhaba istek üzerinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-280">Action taken on hello request.</span></span> <span data-ttu-id="7a3e6-281">Engellenen ve izin verilen değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="7a3e6-282">Site</span><span class="sxs-lookup"><span data-stu-id="7a3e6-282">site</span></span>     | <span data-ttu-id="7a3e6-283">Site için hangi hello günlük oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-283">Site for which hello log was generated.</span></span> <span data-ttu-id="7a3e6-284">Şu anda, yalnızca genel kurallar genel olduğundan listelenir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="7a3e6-285">Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="7a3e6-285">details</span></span>     | <span data-ttu-id="7a3e6-286">Olay tetikleme hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="7a3e6-287">details.Message</span><span class="sxs-lookup"><span data-stu-id="7a3e6-287">details.message</span></span>     | <span data-ttu-id="7a3e6-288">Merhaba kuralı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="7a3e6-289">details.Data</span><span class="sxs-lookup"><span data-stu-id="7a3e6-289">details.data</span></span>     | <span data-ttu-id="7a3e6-290">Belirli veri, eşleşen hello kural isteğinde bulundu.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="7a3e6-291">details.File</span><span class="sxs-lookup"><span data-stu-id="7a3e6-291">details.file</span></span>     | <span data-ttu-id="7a3e6-292">Merhaba kuralı bulunan yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="7a3e6-293">details.Line</span><span class="sxs-lookup"><span data-stu-id="7a3e6-293">details.line</span></span>     | <span data-ttu-id="7a3e6-294">Merhaba olayı tetikleyen hello yapılandırma dosyasındaki satır numarası.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="7a3e6-295">Görüntüleme ve çözümleme hello etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a3e6-295">View and analyze hello activity log</span></span>

<span data-ttu-id="7a3e6-296">Görüntüleme ve yöntemleri aşağıdaki hello birini kullanarak Etkinlik günlüğü verilerini çözümleme:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="7a3e6-297">**Azure Araçları**: bilgi almanızı hello etkinlik günlüğü Azure PowerShell, hello Azure CLI, hello Azure REST API'si aracılığıyla ya da Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="7a3e6-298">Her yöntem için adım adım yönergeler hello ayrıntılı [etkinlik işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="7a3e6-299">**Power BI**: henüz yoksa bir [Power BI](https://powerbi.microsoft.com/pricing) hesabı deneyebilirsiniz, ücretsiz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="7a3e6-300">Hello kullanarak [Azure etkinlik günlükleri paketi Power BI için içerik](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), verilerinizi olduğu veya özelleştirin olarak kullanabileceğiniz, önceden yapılandırılmış panolarla çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="7a3e6-301">Görüntüleme ve hello erişim, performans ve güvenlik duvarı günlüklerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="7a3e6-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="7a3e6-302">Azure [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md) Blob storage hesabınızdan hello sayacı ve olay günlük dosyaları toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="7a3e6-303">Görselleştirme ve güçlü arama özellikleri tooanalyze günlüklerinizi içerir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="7a3e6-304">Ayrıca, tooyour depolama hesabı bağlanmak ve erişim ve performans günlüklerini hello JSON günlük girişlerini almak.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="7a3e6-305">Hello JSON dosyaları indirdikten sonra bunları tooCSV dönüştürmek ve bunları Excel, Power BI veya diğer herhangi bir veri görselleştirmesi aracı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="7a3e6-306">Visual Studio ve sabitleri ve değişkenleri C# değerlerini değiştirmenin temel kavramları biliyorsanız hello kullanabilirsiniz [Dönüştürücü Araçları oturum](https://github.com/Azure-Samples/networking-dotnet-log-converter) github'dan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="7a3e6-307">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="7a3e6-307">Metrics</span></span>

<span data-ttu-id="7a3e6-308">Ölçümleri hello Portalı'nda performans sayaçları görüntüleyebileceğiniz belirli Azure kaynakları için bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="7a3e6-309">Uygulama ağ geçidi için bir ölçüm kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="7a3e6-310">Bu ölçümüdür üretilen iş ve hello Portalı'nda bkz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="7a3e6-311">Tooan uygulama ağ geçidi bulun ve tıklatın **ölçümleri**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="7a3e6-312">tooview hello değerleri, hello select performansı **kullanılabilir ölçümler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="7a3e6-313">Görüntü aşağıdaki hello farklı zaman aralıkları toodisplay hello veri kullanabileceğiniz bir örnek hello filtrelerle görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![Filtrelerle ölçüm görünümü][5]

<span data-ttu-id="7a3e6-315">toosee ölçümleri, geçerli bir listesini görmek [desteklenen Azure İzleyicisi ile ölçümleri](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="7a3e6-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="7a3e6-316">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="7a3e6-316">Alert rules</span></span>

<span data-ttu-id="7a3e6-317">Bir kaynak için ölçümleri temel uyarı kuralları başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="7a3e6-318">Örneğin, bir uyarı bir Web kancası çağrısı veya hello uygulama ağ geçidi hello verimini belirli bir süre boyunca yukarıda, aşağıda veya bir eşik ise yönetici e-posta.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="7a3e6-319">Aşağıdaki örneğine hello size bir e-posta tooan yönetici eşik bir işleme ihlallerini sonra gönderir bir uyarı kuralı oluşturmada size yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="7a3e6-320">Tıklatın **ölçüm uyarı Ekle** tooopen hello **Ekle kuralı** dikey.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="7a3e6-321">Bu dikey hello ölçümleri dikey penceresinden de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-321">You can also reach this blade from hello metrics blade.</span></span>

   !["Ölçüm uyarı Ekle" düğmesi][6]

2. <span data-ttu-id="7a3e6-323">Merhaba üzerinde **Ekle kuralı** dikey penceresinde hello adı, koşul, dolgu bölümleri bildir tıklatın ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="7a3e6-324">Merhaba, **koşulu** Seçici, hello dört değerleri birini seçin: **büyük**, **büyük veya ona eşit**, **değerinden**, veya  **Küçük veya eşit**.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="7a3e6-325">Merhaba, **süresi** bir süre 5 dakika too6 Saat Seçici, seçin.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="7a3e6-326">Seçerseniz **sahipleri, Katkıda Bulunanlar ve okuyucular e-posta**, hello e-posta olabilir dinamik erişim toothat kaynağa sahip hello kullanıcıları temel alan.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="7a3e6-327">Aksi takdirde hello kullanıcıların virgülle ayrılmış bir listesini sağlayabilirsiniz **ek yönetici email(s)** kutusu.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![Kural dikey ekleme][7]

<span data-ttu-id="7a3e6-329">Merhaba eşik ihlal varsa, benzer toohello bir görüntü aşağıdaki hello içinde bir e-postalar ulaşır:</span><span class="sxs-lookup"><span data-stu-id="7a3e6-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![E-posta ihlal edilen eşiği][8]

<span data-ttu-id="7a3e6-331">Ölçüm uyarı oluşturduktan sonra uyarıların bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="7a3e6-332">Tüm hello uyarı kuralları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-332">It provides an overview of all hello alert rules.</span></span>

![Uyarılar ve kuralları listesi][9]

<span data-ttu-id="7a3e6-334">Uyarı bildirimleri hakkında daha fazla toolearn bkz [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7a3e6-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="7a3e6-335">Web kancası ve nasıl uyarıları ile kullanabilmek için hakkında daha fazla toounderstand ziyaret [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7a3e6-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a3e6-336">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a3e6-336">Next steps</span></span>

* <span data-ttu-id="7a3e6-337">Sayaç ve olay günlüklerini kullanarak Görselleştir [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="7a3e6-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="7a3e6-338">[Azure etkinlik günlüğü Power BI ile görselleştirme](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog postası.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="7a3e6-339">[Görüntüleme ve Azure etkinlik günlükleri Power BI ve daha fazla çözümleme](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog postası.</span><span class="sxs-lookup"><span data-stu-id="7a3e6-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
