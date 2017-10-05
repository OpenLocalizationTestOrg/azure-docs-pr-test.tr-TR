---
title: "Uygulama ağ geçidi için erişim günlükleri, performans günlükleri, arka uç sistem durumu ve ölçümleri izleme | Microsoft Docs"
description: "Etkinleştirme ve uygulama ağ geçidi için erişim günlüklerini ve performans günlüklerini yönetme hakkında bilgi edinin"
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="66152-103">Arka uç sistem durumu, tanılama günlüklerini ve uygulama ağ geçidi ölçümleri</span><span class="sxs-lookup"><span data-stu-id="66152-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="66152-104">Azure uygulama ağ geçidi kullanarak, aşağıdaki yollarla kaynakları izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="66152-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="66152-105">[Arka uç sistem durumu](#back-end-health): uygulama Ağ Geçidi sunucularının arka uç havuzlarındaki PowerShell ve Azure Portalı aracılığıyla durum izleme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="66152-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="66152-106">Performans Tanılama günlükleri aracılığıyla arka uç havuzları durumunu da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="66152-107">[Günlükleri](#diagnostic-logs): günlükleri izin performans, erişim ve diğer veri kaydedilmeyecek veya izleme amacıyla bir kaynaktan tüketilen.</span><span class="sxs-lookup"><span data-stu-id="66152-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="66152-108">[Ölçümleri](#metrics): uygulama ağ geçidi şu anda bir ölçüm yok.</span><span class="sxs-lookup"><span data-stu-id="66152-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="66152-109">Bu ölçüm, saniye başına bayt uygulama ağ geçidi verimini ölçer.</span><span class="sxs-lookup"><span data-stu-id="66152-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="66152-110">Arka uç sistem durumu</span><span class="sxs-lookup"><span data-stu-id="66152-110">Back-end health</span></span>

<span data-ttu-id="66152-111">Uygulama ağ geçidi arka uç havuzları portal, PowerShell ve komut satırı arabirimi (CLI) aracılığıyla tek tek üyeleri sistem durumu izleme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="66152-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="66152-112">Birleşik bir sistem durumu da bulabilirsiniz performans tanılama günlükleri aracılığıyla arka uç havuzları özeti.</span><span class="sxs-lookup"><span data-stu-id="66152-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="66152-113">Arka uç sistem durumu raporu arka uç örneklerine uygulama ağ geçidi durumu araştırması çıktısını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="66152-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="66152-114">Yoklama zaman başarısız olur ve arka uç trafik alabilir, sağlıklı kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="66152-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="66152-115">Aksi takdirde, kötü olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="66152-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66152-116">Bir uygulama ağ geçidi alt ağı üzerinde bir ağ güvenlik grubu (NSG) ise, uygulama ağ geçidi alt ağı gelen trafik için bağlantı noktası aralıkları 65503 65534 açın.</span><span class="sxs-lookup"><span data-stu-id="66152-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="66152-117">Bu bağlantı noktaları, arka uç sistem çalışmak için API için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="66152-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="66152-118">Portal üzerinden arka uç durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="66152-118">View back-end health through the portal</span></span>

<span data-ttu-id="66152-119">Portalda, arka uç sistem durumu otomatik olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="66152-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="66152-120">Mevcut bir uygulama ağ geçidi içinde seçin **izleme** > **arka uç sistem durumu**.</span><span class="sxs-lookup"><span data-stu-id="66152-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="66152-121">(Bu bir NIC, IP veya FQDN olup olmadığı) arka uç havuzundaki her üyenin bu sayfada listelenir.</span><span class="sxs-lookup"><span data-stu-id="66152-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="66152-122">Arka uç havuzu adını, bağlantı noktası, arka uç HTTP ayarları adı ve sistem durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="66152-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="66152-123">Sistem durumu için geçerli değerler **sağlıklı**, **sağlıksız**, ve **bilinmeyen**.</span><span class="sxs-lookup"><span data-stu-id="66152-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="66152-124">Arka uç sistem durumunu görüyorsanız, **bilinmeyen**, arka uç erişimi bir NSG kuralı, bir kullanıcı tanımlı yönlendirme (UDR) veya özel DNS sanal ağda tarafından engellenmediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="66152-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![Arka uç sistem durumu][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="66152-126">PowerShell aracılığıyla arka uç durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="66152-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="66152-127">Aşağıdaki PowerShell kod kullanarak arka uç durumunu görüntülemek nasıl gösterir `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="66152-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="66152-128">Azure CLI 2.0 aracılığıyla arka uç durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="66152-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="66152-129">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="66152-129">Results</span></span>

<span data-ttu-id="66152-130">Aşağıdaki kod parçacığında yanıt örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="66152-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="66152-131"><a name="diagnostic-logging"></a>Tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="66152-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="66152-132">Azure'da günlükleri farklı türlerde yönetmek ve uygulama ağ geçitleri sorunlarını gidermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="66152-133">Bu günlükler bazıları portalı üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="66152-134">Tüm günlükler Azure Blob depolama alanından ayıklanan ve farklı Araçlar'da gibi görüntülenebilir [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md), Excel ve Power BI.</span><span class="sxs-lookup"><span data-stu-id="66152-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="66152-135">Aşağıdaki listeden günlükleri farklı türleri hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="66152-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="66152-136">**Etkinlik günlüğü**: kullanabileceğiniz [Azure etkinlik günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) (önceki adıyla işletimsel ve Denetim günlükleri olarak bilinir), Azure aboneliğinizin ve durumlarını gönderilen tüm işlemleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="66152-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="66152-137">Etkinlik günlüğü girişleri varsayılan olarak toplanır ve Azure Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="66152-138">**Erişim günlüğüne**: uygulama ağ geçidi erişim düzenlerini görüntülemek ve arayanın IP, istenen URL, yanıt gecikme, dönüş kodu ve bayt ve kapatma gibi önemli bilgileri analiz etmek için bu günlük kullanabilirsiniz. Bir erişim günlüğü, her 300 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="66152-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="66152-139">Bu günlük, uygulama ağ geçidi örneği başına bir kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="66152-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="66152-140">Uygulama ağ geçidi örneğinin InstanceId'si özelliği tarafından belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="66152-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="66152-141">**Performans günlüğü**: uygulama ağ geçidi örneklerinin nasıl performans gösterdiğini görüntülemek için bu günlük kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="66152-142">Bu günlük sunulan, toplam istekleri dahil olmak üzere her bir örnek, üretilen iş bayt performans bilgilerini yakalar, toplam istek sayısı sunulan, başarısız istek sayısını ve sağlıklı ve sağlıksız arka uç örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="66152-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="66152-143">Bir performans günlüğü, her 60 saniyede toplanır.</span><span class="sxs-lookup"><span data-stu-id="66152-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="66152-144">**Güvenlik Duvarı günlük**: web uygulaması güvenlik duvarı ile yapılandırılmış bir uygulama Ağ Geçidi algılama veya önleme modu üzerinden oturum istekleri görüntülemek için bu günlük kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="66152-145">Günlükleri, yalnızca Azure Resource Manager dağıtım modelinde dağıtılan kaynaklar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="66152-146">Klasik dağıtım modelinde kaynakların günlükleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="66152-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="66152-147">Daha iyi iki modellerinin anlamak için bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="66152-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="66152-148">Günlüklerinizi depolamak için üç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="66152-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="66152-149">**Depolama hesabı**: günlükleri uzun bir süre depolandığında ve gerektiğinde gözden depolama hesapları günlükleri için en iyi kullanımı.</span><span class="sxs-lookup"><span data-stu-id="66152-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="66152-150">**Olay hub'ları**: olay hub'ları olan diğer güvenlik bilgilerini ile tümleştirmek için harika bir seçenek ve Olay yönetimi (SEIM) araçları kaynaklarınız üzerinde uyarıları almak için.</span><span class="sxs-lookup"><span data-stu-id="66152-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="66152-151">**Günlük analizi**: günlük analizi uygulamanızın veya genel gerçek zamanlı izleme veya eğilimleri bakarak için en iyi şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="66152-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="66152-152">PowerShell aracılığıyla günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="66152-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="66152-153">Etkinlik günlüğü her Resource Manager kaynak için otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="66152-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="66152-154">Erişim ve bu günlükleri kullanılabilir veri toplama başlatmak için oturum performans etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="66152-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="66152-155">Günlük kaydını etkinleştirmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="66152-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="66152-156">Depolama hesabınızın kaynak kimliği, günlük verilerinin depolandığı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="66152-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="66152-157">Bu değer biçimindedir: /subscriptions/\<Subscriptionıd\>/resourceGroups/\<kaynak grubu adı\>/providers/Microsoft.Storage/storageAccounts/\<depolama hesabı adı\>.</span><span class="sxs-lookup"><span data-stu-id="66152-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="66152-158">Aboneliğinizdeki herhangi bir depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="66152-159">Bu bilgileri bulmak için Azure portalını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-159">You can use the Azure portal to find this information.</span></span>

    ![Portal: depolama hesabı kaynak kimliği](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="66152-161">Günlük kaydı etkin uygulama ağ geçidinizin kaynak kimliği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="66152-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="66152-162">Bu değer biçimindedir: /subscriptions/\<Subscriptionıd\>/resourceGroups/\<kaynak grubu adı\>/providers/Microsoft.Network/applicationGateways/\<uygulama ağ geçidi adı \>.</span><span class="sxs-lookup"><span data-stu-id="66152-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="66152-163">Bu bilgileri bulmak için portalı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-163">You can use the portal to find this information.</span></span>

    ![Portal: uygulama ağ geçidi kaynak kimliği](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="66152-165">Aşağıdaki PowerShell cmdlet'ini kullanarak tanılama günlük kaydını etkinleştir:</span><span class="sxs-lookup"><span data-stu-id="66152-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="66152-166">Etkinlik günlükleri ayrı bir depolama hesabı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="66152-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="66152-167">Depolama kullanımı erişimi ve performans günlüğünü servis ücretleri doğurur.</span><span class="sxs-lookup"><span data-stu-id="66152-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="66152-168">Azure portalı üzerinden günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="66152-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="66152-169">Azure portalında kaynağınızı bulun ve tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="66152-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="66152-170">Uygulama ağ geçidi için üç günlük vardır:</span><span class="sxs-lookup"><span data-stu-id="66152-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="66152-171">Erişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-171">Access log</span></span>
   * <span data-ttu-id="66152-172">Performans günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-172">Performance log</span></span>
   * <span data-ttu-id="66152-173">Güvenlik Duvarı günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-173">Firewall log</span></span>

2. <span data-ttu-id="66152-174">Veri toplama başlatmak için tıklatın **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="66152-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![Tanılama açma][1]

3. <span data-ttu-id="66152-176">**Tanılama ayarları** dikey tanılama günlükleri için ayarları sağlar.</span><span class="sxs-lookup"><span data-stu-id="66152-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="66152-177">Bu örnekte, günlük analizi günlükleri depolar.</span><span class="sxs-lookup"><span data-stu-id="66152-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="66152-178">Tıklatın **yapılandırma** altında **günlük analizi** çalışma alanınızı yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="66152-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="66152-179">Tanılama günlüklerini kaydetmek için olay hub'ları ve bir depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![Yapılandırma işlemi başlatılıyor][2]

4. <span data-ttu-id="66152-181">Varolan bir Operations Management Suite (OMS) çalışma alanını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66152-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="66152-182">Bu örnek, mevcut bir kullanır.</span><span class="sxs-lookup"><span data-stu-id="66152-182">This example uses an existing one.</span></span>

   ![OMS çalışma alanları için seçenekleri][3]

5. <span data-ttu-id="66152-184">Ayarları onaylayın ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="66152-184">Confirm the settings and click **Save**.</span></span>

   ![Tanılama ayarları dikey seçimleri][4]

### <a name="activity-log"></a><span data-ttu-id="66152-186">Etkinlik günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-186">Activity log</span></span>

<span data-ttu-id="66152-187">Azure etkinlik günlüğü varsayılan olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66152-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="66152-188">Günlükleri 90 gün boyunca Azure olay günlüklerini deposunda saklanır.</span><span class="sxs-lookup"><span data-stu-id="66152-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="66152-189">Bu günlükler hakkında daha fazla bilgi okuyarak [olayları ve etkinlik günlüğü görüntüle](../monitoring-and-diagnostics/insights-debugging-with-events.md) makale.</span><span class="sxs-lookup"><span data-stu-id="66152-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="66152-190">Erişim günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-190">Access log</span></span>

<span data-ttu-id="66152-191">Önceki adımlarda ayrıntılı olarak her bir uygulama ağ geçidi örnek üzerinde yalnızca etkinleştirdikten ise erişim günlüğü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="66152-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="66152-192">Veri günlük kaydı etkinleştirildiğinde, belirttiğiniz depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="66152-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="66152-193">Uygulama ağ geçidi'nin her erişim, aşağıdaki örnekte gösterildiği gibi JSON biçiminde günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="66152-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="66152-194">Değer</span><span class="sxs-lookup"><span data-stu-id="66152-194">Value</span></span>  |<span data-ttu-id="66152-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66152-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="66152-196">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="66152-196">instanceId</span></span>     | <span data-ttu-id="66152-197">İsteği sunan uygulama ağ geçidi örneği.</span><span class="sxs-lookup"><span data-stu-id="66152-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="66152-198">ClientIP</span><span class="sxs-lookup"><span data-stu-id="66152-198">clientIP</span></span>     | <span data-ttu-id="66152-199">İstek için kaynak IP.</span><span class="sxs-lookup"><span data-stu-id="66152-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="66152-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="66152-200">clientPort</span></span>     | <span data-ttu-id="66152-201">İstek için kaynak bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="66152-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="66152-202">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="66152-202">httpMethod</span></span>     | <span data-ttu-id="66152-203">İstek tarafından kullanılan HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="66152-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="66152-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="66152-204">requestUri</span></span>     | <span data-ttu-id="66152-205">Alınan istek URI'si.</span><span class="sxs-lookup"><span data-stu-id="66152-205">URI of the received request.</span></span>        |
|<span data-ttu-id="66152-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="66152-206">RequestQuery</span></span>     | <span data-ttu-id="66152-207">**Sunucu yönlendirilen**: bir istek gönderildi arka uç havuzu örnek.</span><span class="sxs-lookup"><span data-stu-id="66152-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="66152-208">**X-AzureApplicationGateway-günlük-ID**: bağıntı istek için kullanılan kimliği.</span><span class="sxs-lookup"><span data-stu-id="66152-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="66152-209">Arka uç sunucularına trafiği sorunlarını gidermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="66152-210">**Sunucu durumu**: uygulama ağ geçidi arka uçtan alınan HTTP yanıt kodu.</span><span class="sxs-lookup"><span data-stu-id="66152-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="66152-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="66152-211">UserAgent</span></span>     | <span data-ttu-id="66152-212">Kullanıcı Aracısı'ndan HTTP isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="66152-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="66152-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="66152-213">httpStatus</span></span>     | <span data-ttu-id="66152-214">Uygulama ağ geçidi'nden istemciye döndürülen HTTP durum kodu.</span><span class="sxs-lookup"><span data-stu-id="66152-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="66152-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="66152-215">httpVersion</span></span>     | <span data-ttu-id="66152-216">İstek HTTP sürümü.</span><span class="sxs-lookup"><span data-stu-id="66152-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="66152-217">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="66152-217">receivedBytes</span></span>     | <span data-ttu-id="66152-218">Paket, alınan bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="66152-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="66152-219">SentBytes</span><span class="sxs-lookup"><span data-stu-id="66152-219">sentBytes</span></span>| <span data-ttu-id="66152-220">Paket, gönderilen bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="66152-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="66152-221">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="66152-221">timeTaken</span></span>| <span data-ttu-id="66152-222">Bir isteğin işlenmesi için ve gönderilecek yanıt için geçen süre (milisaniye cinsinden) uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="66152-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="66152-223">Bu, uygulama ağ geçidi bir HTTP isteğinin yanıtı gönderdiğinizde, işlem tamamlanmadan zaman için ilk baytını alır zaman aralığından olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="66152-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="66152-224">Time-Taken alanı genellikle isteği ve yanıt paketlerin ağ üzerinden yolculuk zaman içerir dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="66152-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="66152-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="66152-225">sslEnabled</span></span>| <span data-ttu-id="66152-226">Arka uç havuzları iletişimin SSL kullanılıp.</span><span class="sxs-lookup"><span data-stu-id="66152-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="66152-227">Açma ve kapatma değerler geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="66152-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="66152-228">Performans günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-228">Performance log</span></span>

<span data-ttu-id="66152-229">Önceki adımlarda ayrıntılı olarak her bir uygulama ağ geçidi örnek üzerinde yalnızca etkinleştirdiyseniz, performans günlüğü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="66152-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="66152-230">Veri günlük kaydı etkinleştirildiğinde, belirttiğiniz depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="66152-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="66152-231">Performans günlüğü verilerini 1 dakikalık aralıklarla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="66152-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="66152-232">Aşağıdaki veriler günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="66152-232">The following data is logged:</span></span>


|<span data-ttu-id="66152-233">Değer</span><span class="sxs-lookup"><span data-stu-id="66152-233">Value</span></span>  |<span data-ttu-id="66152-234">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66152-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="66152-235">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="66152-235">instanceId</span></span>     |  <span data-ttu-id="66152-236">Uygulama ağ geçidi örneği performans verileri oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="66152-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="66152-237">Birden çok örnekli uygulama ağ geçidi için örneği başına bir satır yok.</span><span class="sxs-lookup"><span data-stu-id="66152-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="66152-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="66152-238">healthyHostCount</span></span>     | <span data-ttu-id="66152-239">Arka uç havuzundaki sağlıklı ana bilgisayar sayısı.</span><span class="sxs-lookup"><span data-stu-id="66152-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="66152-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="66152-240">unHealthyHostCount</span></span>     | <span data-ttu-id="66152-241">Arka uç havuzundaki sağlıksız ana bilgisayar sayısı.</span><span class="sxs-lookup"><span data-stu-id="66152-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="66152-242">RequestCount</span><span class="sxs-lookup"><span data-stu-id="66152-242">requestCount</span></span>     | <span data-ttu-id="66152-243">Hizmet isteği sayısı.</span><span class="sxs-lookup"><span data-stu-id="66152-243">Number of requests served.</span></span>        |
|<span data-ttu-id="66152-244">Gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="66152-244">latency</span></span> | <span data-ttu-id="66152-245">İsteklere hizmet arka uç örneğinden isteklerinin gecikme süresi (milisaniye cinsinden).</span><span class="sxs-lookup"><span data-stu-id="66152-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="66152-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="66152-246">failedRequestCount</span></span>| <span data-ttu-id="66152-247">Başarısız istek sayısı.</span><span class="sxs-lookup"><span data-stu-id="66152-247">Number of failed requests.</span></span>|
|<span data-ttu-id="66152-248">Üretilen iş</span><span class="sxs-lookup"><span data-stu-id="66152-248">throughput</span></span>| <span data-ttu-id="66152-249">Saniyedeki bayt cinsinden son günlük itibaren ortalama performansıdır.</span><span class="sxs-lookup"><span data-stu-id="66152-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="66152-250">Gecikme süresi, HTTP isteğin ilk baytını HTTP yanıtın son baytını gönderildiğinde zaman alındığında zamandan hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="66152-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="66152-251">Uygulama ağ geçidi işleme süresi ve arka uç ve arka uç, isteği işlemek için gereken süre ağ maliyetine toplamıdır.</span><span class="sxs-lookup"><span data-stu-id="66152-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="66152-252">Güvenlik Duvarı günlüğü</span><span class="sxs-lookup"><span data-stu-id="66152-252">Firewall log</span></span>

<span data-ttu-id="66152-253">Önceki adımlarda ayrıntılı olarak her uygulama ağ geçidi için yalnızca etkinleştirdiyseniz, Güvenlik Duvarı günlük oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="66152-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="66152-254">Bu günlük Ayrıca web uygulaması Güvenlik Duvarı'nı bir uygulama ağ geçidi üzerinde yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66152-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="66152-255">Veri günlük kaydı etkinleştirildiğinde, belirttiğiniz depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="66152-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="66152-256">Aşağıdaki veriler günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="66152-256">The following data is logged:</span></span>


|<span data-ttu-id="66152-257">Değer</span><span class="sxs-lookup"><span data-stu-id="66152-257">Value</span></span>  |<span data-ttu-id="66152-258">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66152-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="66152-259">örnek kimliği</span><span class="sxs-lookup"><span data-stu-id="66152-259">instanceId</span></span>     | <span data-ttu-id="66152-260">Uygulama ağ geçidi örneği için hangi güvenlik duvarı veri oluşturuluyor.</span><span class="sxs-lookup"><span data-stu-id="66152-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="66152-261">Birden çok örnekli uygulama ağ geçidi için örneği başına bir satır yok.</span><span class="sxs-lookup"><span data-stu-id="66152-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="66152-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="66152-262">clientIp</span></span>     |   <span data-ttu-id="66152-263">İstek için kaynak IP.</span><span class="sxs-lookup"><span data-stu-id="66152-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="66152-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="66152-264">clientPort</span></span>     |  <span data-ttu-id="66152-265">İstek için kaynak bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="66152-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="66152-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="66152-266">requestUri</span></span>     | <span data-ttu-id="66152-267">Alınan istek URL'si.</span><span class="sxs-lookup"><span data-stu-id="66152-267">URL of the received request.</span></span>       |
|<span data-ttu-id="66152-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="66152-268">ruleSetType</span></span>     | <span data-ttu-id="66152-269">Kural türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66152-269">Rule set type.</span></span> <span data-ttu-id="66152-270">Kullanılabilir OWASP değerdir.</span><span class="sxs-lookup"><span data-stu-id="66152-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="66152-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="66152-271">ruleSetVersion</span></span>     | <span data-ttu-id="66152-272">Kural kullanılan sürümünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="66152-272">Rule set version used.</span></span> <span data-ttu-id="66152-273">Değerleri 2.2.9 ve 3.0 kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="66152-274">RuleId</span><span class="sxs-lookup"><span data-stu-id="66152-274">ruleId</span></span>     | <span data-ttu-id="66152-275">Tetikleyici olay kimliği kuralı.</span><span class="sxs-lookup"><span data-stu-id="66152-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="66152-276">İleti</span><span class="sxs-lookup"><span data-stu-id="66152-276">message</span></span>     | <span data-ttu-id="66152-277">Tetikleyici olay kullanıcı dostu iletisi.</span><span class="sxs-lookup"><span data-stu-id="66152-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="66152-278">Ayrıntılar bölümünde daha ayrıntılı bilgi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="66152-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="66152-279">Eylem</span><span class="sxs-lookup"><span data-stu-id="66152-279">action</span></span>     |  <span data-ttu-id="66152-280">İstek üzerinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="66152-280">Action taken on the request.</span></span> <span data-ttu-id="66152-281">Engellenen ve izin verilen değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="66152-282">Site</span><span class="sxs-lookup"><span data-stu-id="66152-282">site</span></span>     | <span data-ttu-id="66152-283">Günlük oluşturulduğu site.</span><span class="sxs-lookup"><span data-stu-id="66152-283">Site for which the log was generated.</span></span> <span data-ttu-id="66152-284">Şu anda, yalnızca genel kurallar genel olduğundan listelenir.</span><span class="sxs-lookup"><span data-stu-id="66152-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="66152-285">Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="66152-285">details</span></span>     | <span data-ttu-id="66152-286">Olay Ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="66152-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="66152-287">details.Message</span><span class="sxs-lookup"><span data-stu-id="66152-287">details.message</span></span>     | <span data-ttu-id="66152-288">Kural açıklaması.</span><span class="sxs-lookup"><span data-stu-id="66152-288">Description of the rule.</span></span>        |
|<span data-ttu-id="66152-289">details.Data</span><span class="sxs-lookup"><span data-stu-id="66152-289">details.data</span></span>     | <span data-ttu-id="66152-290">Belirli veri kural eşleşen isteğinde bulundu.</span><span class="sxs-lookup"><span data-stu-id="66152-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="66152-291">details.File</span><span class="sxs-lookup"><span data-stu-id="66152-291">details.file</span></span>     | <span data-ttu-id="66152-292">Kural bulunan yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="66152-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="66152-293">details.Line</span><span class="sxs-lookup"><span data-stu-id="66152-293">details.line</span></span>     | <span data-ttu-id="66152-294">Satır numarası yapılandırma dosyasında olay tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="66152-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="66152-295">Görüntüleme ve etkinlik günlüğü çözümleme</span><span class="sxs-lookup"><span data-stu-id="66152-295">View and analyze the activity log</span></span>

<span data-ttu-id="66152-296">Görüntüleme ve aşağıdaki yöntemlerden birini kullanarak Etkinlik günlüğü verilerini çözümleme:</span><span class="sxs-lookup"><span data-stu-id="66152-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="66152-297">**Azure Araçları**: bilgi almanızı Azure PowerShell, Azure CLI, Azure REST API veya Azure Portalı aracılığıyla etkinlik günlüğü.</span><span class="sxs-lookup"><span data-stu-id="66152-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="66152-298">Her yöntem için adım adım yönergeler ayrıntılı olarak [etkinlik işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="66152-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="66152-299">**Power BI**: henüz yoksa bir [Power BI](https://powerbi.microsoft.com/pricing) hesabı deneyebilirsiniz, ücretsiz.</span><span class="sxs-lookup"><span data-stu-id="66152-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="66152-300">Kullanarak [Azure etkinlik günlükleri paketi Power BI için içerik](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), verilerinizi olduğu veya özelleştirin olarak kullanabileceğiniz, önceden yapılandırılmış panolarla çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="66152-301">Görüntüleme ve erişim, performans ve güvenlik duvarı günlüklerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="66152-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="66152-302">Azure [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md) Blob storage hesabınızdan sayacı ve olay günlük dosyaları toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="66152-303">Görselleştirme ve günlükleriniz analiz etmek için güçlü arama özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="66152-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="66152-304">Ayrıca, depolama hesabınıza bağlanın ve erişim ve performans günlüklerini JSON günlük girişlerini almak.</span><span class="sxs-lookup"><span data-stu-id="66152-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="66152-305">JSON dosyaları indirdikten sonra bunları CSV'ye Dönüştür ve Excel, Power BI veya diğer herhangi bir veri görselleştirmesi aracı görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="66152-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="66152-306">Visual Studio ve sabitleri ve değişkenleri C# değerlerini değiştirmenin temel kavramları biliyorsanız, kullanabileceğiniz [Dönüştürücü Araçları oturum](https://github.com/Azure-Samples/networking-dotnet-log-converter) github'dan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="66152-307">Ölçümler</span><span class="sxs-lookup"><span data-stu-id="66152-307">Metrics</span></span>

<span data-ttu-id="66152-308">Ölçümleri portalda performans sayaçları görüntüleyebileceğiniz belirli Azure kaynakları için bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="66152-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="66152-309">Uygulama ağ geçidi için bir ölçüm kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="66152-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="66152-310">Bu ölçümüdür üretilen iş ve Portalı'nda bkz.</span><span class="sxs-lookup"><span data-stu-id="66152-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="66152-311">Bir uygulama ağ geçidi bulun ve tıklatın **ölçümleri**.</span><span class="sxs-lookup"><span data-stu-id="66152-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="66152-312">Değerleri görüntülemek için seçin performansı **kullanılabilir ölçümler** bölümü.</span><span class="sxs-lookup"><span data-stu-id="66152-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="66152-313">Aşağıdaki görüntüde, farklı zaman aralıkları verileri görüntülemek için kullanabileceğiniz filtreleri içeren bir örnek görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![Filtrelerle ölçüm görünümü][5]

<span data-ttu-id="66152-315">Geçerli ölçümleri listesini görmek için bkz: [desteklenen Azure İzleyicisi ile ölçümleri](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="66152-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="66152-316">Uyarı kuralları</span><span class="sxs-lookup"><span data-stu-id="66152-316">Alert rules</span></span>

<span data-ttu-id="66152-317">Bir kaynak için ölçümleri temel uyarı kuralları başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66152-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="66152-318">Örneğin, bir uyarı bir Web kancası çağrısı veya uygulama ağ geçidi verimini belirli bir süre boyunca yukarıda, aşağıda veya bir eşik ise yönetici e-posta.</span><span class="sxs-lookup"><span data-stu-id="66152-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="66152-319">Aşağıdaki örnek eşiği bir işleme ihlallerini sonra yönetici e-posta gönderen bir uyarı kuralı oluşturmada size yol gösterir:</span><span class="sxs-lookup"><span data-stu-id="66152-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="66152-320">Tıklatın **ölçüm uyarı Ekle** açmak için **Ekle kuralı** dikey.</span><span class="sxs-lookup"><span data-stu-id="66152-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="66152-321">Bu dikey ölçümleri dikey penceresinden de ulaşabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-321">You can also reach this blade from the metrics blade.</span></span>

   !["Ölçüm uyarı Ekle" düğmesi][6]

2. <span data-ttu-id="66152-323">Üzerinde **Ekle kuralı** dikey penceresinde, adı, koşul, dolgu bölümleri bildir tıklatın ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="66152-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="66152-324">İçinde **koşulu** Seçici, dört değerden birini seçin: **büyük**, **büyük veya ona eşit**, **değerinden**, veya **Küçük veya eşit**.</span><span class="sxs-lookup"><span data-stu-id="66152-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="66152-325">İçinde **süresi** Seçicisi, bir süre 5 dakika ile 6 saat seçin.</span><span class="sxs-lookup"><span data-stu-id="66152-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="66152-326">Seçerseniz **sahipleri, Katkıda Bulunanlar ve okuyucular e-posta**, bu kaynağa erişim izni olan kullanıcıların göre e-posta dinamik olabilir.</span><span class="sxs-lookup"><span data-stu-id="66152-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="66152-327">Aksi takdirde kullanıcıların virgülle ayrılmış bir listesini sağlayabilirsiniz **ek yönetici email(s)** kutusu.</span><span class="sxs-lookup"><span data-stu-id="66152-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![Kural dikey ekleme][7]

<span data-ttu-id="66152-329">Eşik ihlal varsa, aşağıdaki resimde gösterilene benzer bir e-posta ulaşır:</span><span class="sxs-lookup"><span data-stu-id="66152-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![E-posta ihlal edilen eşiği][8]

<span data-ttu-id="66152-331">Ölçüm uyarı oluşturduktan sonra uyarıların bir listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="66152-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="66152-332">Tüm uyarı kuralları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="66152-332">It provides an overview of all the alert rules.</span></span>

![Uyarılar ve kuralları listesi][9]

<span data-ttu-id="66152-334">Uyarı bildirimleri hakkında daha fazla bilgi için bkz: [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="66152-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="66152-335">Web kancası ve nasıl uyarılarla kullanabilmek için daha iyi anlamak için ziyaret [bir Web kancası Azure ölçüm uyarıyı yapılandırmak](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="66152-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66152-336">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66152-336">Next steps</span></span>

* <span data-ttu-id="66152-337">Sayaç ve olay günlüklerini kullanarak Görselleştir [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="66152-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="66152-338">[Azure etkinlik günlüğü Power BI ile görselleştirme](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog postası.</span><span class="sxs-lookup"><span data-stu-id="66152-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="66152-339">[Görüntüleme ve Azure etkinlik günlükleri Power BI ve daha fazla çözümleme](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog postası.</span><span class="sxs-lookup"><span data-stu-id="66152-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
