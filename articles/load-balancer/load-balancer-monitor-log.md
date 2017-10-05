---
title: "Yük Dengeleyici için işlemleri, olayları ve sayaçları izleme | Microsoft Docs"
description: "Uyarı olayları etkinleştir ve Azure yük dengeleyici için sistem durumu günlüğü araştırma hakkında bilgi edinin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="c0f98-103">Azure Load Balancer için günlük analizi</span><span class="sxs-lookup"><span data-stu-id="c0f98-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="c0f98-104">Azure'da günlükleri farklı türlerde yönetmek ve yük dengeleyici sorunlarını gidermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="c0f98-105">Bu günlükler bazıları Portalı aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="c0f98-106">Tüm günlükleri Azure blob depolama alanından ayıklanan ve farklı araçlar, Excel ve Powerbı gibi görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="c0f98-107">Aşağıdaki listeden günlükleri farklı türleri hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="c0f98-108">**Denetim günlüklerini:** kullanabileceğiniz [Azure denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) (eskiden İşlem günlükleri olarak bilinir) Azure Abonelikleriniz ve durumlarını gönderilen tüm işlemleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="c0f98-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="c0f98-109">Denetim günlüklerini varsayılan olarak etkindir ve Azure Portalı'nda görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="c0f98-110">**Uyarı olayı günlükleri:** yük dengeleyici tarafından uyarıları rasied görüntülemek için bu günlük kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="c0f98-111">Yük Dengeleyici için durum her beş dakikada toplanır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="c0f98-112">Bu günlük yalnızca bir yük dengeleyici uyarı olayı tetiklenir yazılır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="c0f98-113">**Sistem durumu araştırma günlüklerini:** , arka uç havuzundaki istekleri sistem durumu araştırma hataları nedeniyle yük dengeleyiciden gösterilmeyen örnek sayısı gibi sistem durumu araştırma tarafından algılanan sorunları görüntülemek için bu günlük kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="c0f98-114">Sistem durumu araştırma durumundaki bir değişiklik olduğunda bu günlük yazılır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0f98-115">Günlük analizi yük dengeleyici yalnızca Internet'e yönelik için şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="c0f98-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="c0f98-116">Günlükleri yalnızca Resource Manager dağıtım modelinde dağıtılan kaynaklar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="c0f98-117">Klasik dağıtım modelinde kaynakların günlükleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c0f98-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="c0f98-118">Dağıtım modelleri hakkında daha fazla bilgi için bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c0f98-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="c0f98-119">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="c0f98-119">Enable logging</span></span>

<span data-ttu-id="c0f98-120">Denetim günlüğü, her Resource Manager kaynak için otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="c0f98-121">Olay ve bu günlükleri kullanılabilir veri toplama başlatmak için araştırma sistem günlüğü etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="c0f98-122">Günlük kaydını etkinleştirmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="c0f98-123">Oturum açma için [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0f98-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c0f98-124">Bir yük dengeleyici, henüz yoksa [bir yük dengeleyici oluşturma](load-balancer-get-started-internet-arm-ps.md) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="c0f98-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="c0f98-125">Portalı'nda tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="c0f98-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="c0f98-126">Seçin **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="c0f98-126">Select **Load Balancers**.</span></span>

    ![Portal - yük dengeleyici](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="c0f98-128">Mevcut bir Yük Dengeleyiciyi seçin >> **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="c0f98-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="c0f98-129">Yük Dengeleyici adı altında iletişim kutusunun sağ tarafta kaydırın **izleme**, tıklatın **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="c0f98-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![Portal - yük dengeleyici ayarları](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="c0f98-131">İçinde **tanılama** bölmesi altında **durum**seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="c0f98-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="c0f98-132">Tıklatın **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="c0f98-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="c0f98-133">Altında **GÜNLÜKLERİ**, mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0f98-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="c0f98-134">Olay verilerini kaç gün olay günlüklerinde depolanacak belirlemek için kaydırıcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="c0f98-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c0f98-135">Click **Save**.</span></span>

    ![Portal - tanılama günlükleri](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="c0f98-137">Denetim günlükleri ayrı bir depolama hesabı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="c0f98-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="c0f98-138">Kullanım olay ve sistem durumu depolama araştırma günlük kaydı hizmeti ücret uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="c0f98-139">Denetim günlüğü</span><span class="sxs-lookup"><span data-stu-id="c0f98-139">Audit log</span></span>

<span data-ttu-id="c0f98-140">Denetim günlüğü varsayılan olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c0f98-140">The audit log is generated by default.</span></span> <span data-ttu-id="c0f98-141">Günlükleri 90 gün boyunca Azure'nın olay günlüklerini deposunda saklanır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="c0f98-142">Bu günlükler hakkında daha fazla bilgi okuyarak [olayları görüntülemek ve Denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) makale.</span><span class="sxs-lookup"><span data-stu-id="c0f98-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="c0f98-143">Uyarı olay günlüğü</span><span class="sxs-lookup"><span data-stu-id="c0f98-143">Alert event log</span></span>

<span data-ttu-id="c0f98-144">Bu günlük yalnızca üzerinde etkinleştirdikten, oluşturulan bir yük dengeleyici temelinde.</span><span class="sxs-lookup"><span data-stu-id="c0f98-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="c0f98-145">Olayları JSON biçiminde günlüğe kaydedilen ve günlüğe kaydetme etkinleştirildiğinde, belirtilen depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="c0f98-146">Bir olayın bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="c0f98-147">JSON çıktısını gösterir *eventname* yük dengeleyici nedenini açıklayan özelliğini bir uyarı oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="c0f98-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="c0f98-148">Bu durumda, oluşturulan uyarı TCP bağlantı noktası Tükenme nedeniyle IP NAT kaynağı tarafından sınırları (SNAT) neden oldu.</span><span class="sxs-lookup"><span data-stu-id="c0f98-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="c0f98-149">Sistem durumu araştırma günlük</span><span class="sxs-lookup"><span data-stu-id="c0f98-149">Health probe log</span></span>

<span data-ttu-id="c0f98-150">Bu günlük yalnızca üzerinde etkinleştirdikten, oluşturulan bir yük dengeleyici temel olarak ayrıntılı yukarıdaki başına.</span><span class="sxs-lookup"><span data-stu-id="c0f98-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="c0f98-151">Veri günlük kaydı etkinleştirildiğinde, belirtilen depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="c0f98-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="c0f98-152">'Öngörüler günlükleri loadbalancerprobehealthstatus' adlı bir kapsayıcı oluşturulur ve aşağıdaki veriler günlüğe kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="c0f98-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="c0f98-153">JSON çıktısını özellikleri alanında araştırma sistem durumu için temel bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="c0f98-154">*DipDownCount* özelliği, ağ trafiğini başarısız araştırma yanıtları nedeniyle gösterilmeyen uç üzerinde örnekleri toplam sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="c0f98-155">Görüntüleme ve denetim günlüğü çözümleme</span><span class="sxs-lookup"><span data-stu-id="c0f98-155">View and analyze the audit log</span></span>

<span data-ttu-id="c0f98-156">Görüntüleme ve aşağıdaki yöntemlerden birini kullanarak denetim günlüğü verilerini çözümleme:</span><span class="sxs-lookup"><span data-stu-id="c0f98-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="c0f98-157">**Azure Araçları:** bilgi almanızı Azure PowerShell, Azure komut satırı arabirimi (CLI), Azure REST API veya Azure preview portal aracılığıyla denetim günlükleri.</span><span class="sxs-lookup"><span data-stu-id="c0f98-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="c0f98-158">Her yöntem için adım adım yönergeler ayrıntılı olarak [denetim işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c0f98-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="c0f98-159">**Power BI:** zaten yoksa bir [Power BI](https://powerbi.microsoft.com/pricing) hesabı deneyebilirsiniz, ücretsiz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="c0f98-160">Kullanarak [Azure denetim günlükleri paketi Power BI için içerik](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), önceden yapılandırılmış panolar verilerinizle analiz edebilirsiniz veya görünümler gereksinimlerinize uyacak şekilde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="c0f98-161">Görüntüleme ve durum araştırması ve olay günlüğü çözümleme</span><span class="sxs-lookup"><span data-stu-id="c0f98-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="c0f98-162">Depolama hesabınıza bağlanın ve olay ve sistem durumu araştırma günlükleri için JSON günlük girişlerini almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="c0f98-163">JSON dosyaları yükledikten sonra CSV ve Excel, Powerbı veya başka bir veri görselleştirme araç görünümünde dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0f98-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="c0f98-164">Visual Studio ve sabitleri ve değişkenleri C# değerlerini değiştirmenin temel kavramları biliyorsanız, kullanabileceğiniz [Dönüştürücü Araçları oturum](https://github.com/Azure-Samples/networking-dotnet-log-converter) github'dan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c0f98-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c0f98-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c0f98-165">Additional resources</span></span>

* <span data-ttu-id="c0f98-166">[Azure denetim günlükleri Power BI ile görselleştirme](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog postası.</span><span class="sxs-lookup"><span data-stu-id="c0f98-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="c0f98-167">[Görüntüleme ve Azure denetim günlükleri Power BI ve daha fazla çözümleme](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog postası.</span><span class="sxs-lookup"><span data-stu-id="c0f98-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0f98-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0f98-168">Next steps</span></span>

[<span data-ttu-id="c0f98-169">Yük dengeleyici araştırmalarını anlama</span><span class="sxs-lookup"><span data-stu-id="c0f98-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
