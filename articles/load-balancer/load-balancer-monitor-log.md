---
title: "aaaMonitor işlemleri, olaylar ve yük dengeleyici için sayaçları | Microsoft Docs"
description: "Nasıl tooenable olayları uyarı ve Azure yük dengeleyici için sistem durumu günlüğü araştırma öğrenin"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="58341-103">Azure Load Balancer için günlük analizi</span><span class="sxs-lookup"><span data-stu-id="58341-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="58341-104">Günlükleri farklı türlerde içinde Azure toomanage kullanın ve yük dengeleyici giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58341-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="58341-105">Bu günlükler bazıları hello Portalı aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="58341-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="58341-106">Tüm günlükleri Azure blob depolama alanından ayıklanan ve farklı araçlar, Excel ve Powerbı gibi görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="58341-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="58341-107">Merhaba listeden hello günlüklerinin farklı türleri hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58341-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="58341-108">**Denetim günlüklerini:** kullanabileceğiniz [Azure denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) (daha önce işlem günlükleri olarak bilinen) tooview gönderilen tooyour Azure aboneliği ve durumlarını olan tüm işlemleri.</span><span class="sxs-lookup"><span data-stu-id="58341-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="58341-109">Denetim günlüklerini varsayılan olarak etkindir ve hello Azure portal görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="58341-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="58341-110">**Uyarı olayı günlükleri:** hello yük dengeleyici tarafından bu günlük tooview uyarıları rasied kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58341-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="58341-111">Merhaba durum hello yük dengeleyici için beş dakikada toplanır.</span><span class="sxs-lookup"><span data-stu-id="58341-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="58341-112">Bu günlük yalnızca bir yük dengeleyici uyarı olayı tetiklenir yazılır.</span><span class="sxs-lookup"><span data-stu-id="58341-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="58341-113">**Sistem durumu araştırma günlüklerini:** istekleri sistem durumu araştırma hataları nedeniyle hello yük dengeleyiciden gösterilmeyen örneği, arka uç havuzundaki hello sayısı gibi sistem durumu araştırma tarafından algılanan bu günlük tooview sorunları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58341-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="58341-114">Bu günlük toowhen yazılır hello durumu araştırma bir değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="58341-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58341-115">Günlük analizi yük dengeleyici yalnızca Internet'e yönelik için şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="58341-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="58341-116">Günlükleri yalnızca hello Resource Manager dağıtım modelinde dağıtılan kaynaklar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="58341-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="58341-117">Merhaba Klasik dağıtım modelinde kaynakların günlükleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="58341-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="58341-118">Merhaba dağıtım modelleri hakkında daha fazla bilgi için bkz: [anlama Resource Manager dağıtımını ve klasik dağıtımı](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="58341-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="58341-119">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="58341-119">Enable logging</span></span>

<span data-ttu-id="58341-120">Denetim günlüğü, her Resource Manager kaynak için otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="58341-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="58341-121">Tooenable olay ve bu günlükleri kullanılabilir hello veri toplama durumu araştırma günlük toostart gerekir.</span><span class="sxs-lookup"><span data-stu-id="58341-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="58341-122">Aşağıdaki adımları tooenable günlük hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="58341-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="58341-123">Oturum açma toohello [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58341-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="58341-124">Bir yük dengeleyici, henüz yoksa [bir yük dengeleyici oluşturma](load-balancer-get-started-internet-arm-ps.md) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="58341-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="58341-125">Merhaba Portalı'nda tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="58341-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="58341-126">Seçin **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="58341-126">Select **Load Balancers**.</span></span>

    ![Portal - yük dengeleyici](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="58341-128">Mevcut bir Yük Dengeleyiciyi seçin >> **tüm ayarları**.</span><span class="sxs-lookup"><span data-stu-id="58341-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="58341-129">Merhaba sağ tarafında hello iletişim hello yük dengeleyici hello adı altında çok kaydırma**izleme**, tıklatın **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="58341-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![Portal - yük dengeleyici ayarları](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="58341-131">Merhaba, **tanılama** bölmesi altında **durum**seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="58341-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="58341-132">Tıklatın **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="58341-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="58341-133">Altında **GÜNLÜKLERİ**, mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58341-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="58341-134">Merhaba kaydırıcı toodetermine hello olay günlüklerinde olay veriyi depolanacak kaç gün kullanın.</span><span class="sxs-lookup"><span data-stu-id="58341-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="58341-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58341-135">Click **Save**.</span></span>

    ![Portal - tanılama günlükleri](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="58341-137">Denetim günlükleri ayrı bir depolama hesabı gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="58341-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="58341-138">Hello kullan depolama olay ve sistem durumu için yoklama günlüğü hizmeti ücret uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="58341-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="58341-139">Denetim günlüğü</span><span class="sxs-lookup"><span data-stu-id="58341-139">Audit log</span></span>

<span data-ttu-id="58341-140">Merhaba denetim günlüğü varsayılan olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58341-140">hello audit log is generated by default.</span></span> <span data-ttu-id="58341-141">Merhaba günlükleri 90 gün boyunca Azure'nın olay günlüklerini deposunda korunur.</span><span class="sxs-lookup"><span data-stu-id="58341-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="58341-142">Merhaba okuyarak Bu günlükler hakkında daha fazla bilgi [olayları görüntülemek ve Denetim günlükleri](../monitoring-and-diagnostics/insights-debugging-with-events.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="58341-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="58341-143">Uyarı olay günlüğü</span><span class="sxs-lookup"><span data-stu-id="58341-143">Alert event log</span></span>

<span data-ttu-id="58341-144">Bu günlük yalnızca üzerinde etkinleştirdikten, oluşturulan bir yük dengeleyici temelinde.</span><span class="sxs-lookup"><span data-stu-id="58341-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="58341-145">Merhaba olayları JSON biçiminde günlüğe kaydedilen ve hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="58341-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="58341-146">Merhaba, bir olay örneği aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="58341-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="58341-147">Merhaba JSON çıktısını gösterir hello *eventname* hello yük dengeleyici hello nedenini açıklayan özelliğini bir uyarı oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="58341-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="58341-148">Bu durumda, oluşturulan hello uyarı IP NAT sınırlar kaynağı tarafından neden tooTCP bağlantı noktası Tükenme (SNAT) oluştu.</span><span class="sxs-lookup"><span data-stu-id="58341-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="58341-149">Sistem durumu araştırma günlük</span><span class="sxs-lookup"><span data-stu-id="58341-149">Health probe log</span></span>

<span data-ttu-id="58341-150">Bu günlük yalnızca üzerinde etkinleştirdikten, oluşturulan bir yük dengeleyici temel olarak ayrıntılı yukarıdaki başına.</span><span class="sxs-lookup"><span data-stu-id="58341-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="58341-151">Merhaba veri hello günlük kaydı etkin olduğunda belirtilen hello depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="58341-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="58341-152">'Öngörüler günlükleri loadbalancerprobehealthstatus' adlı bir kapsayıcı oluşturulur ve veriler aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="58341-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="58341-153">Merhaba özellikleri alan hello temel bilgileri hello araştırma sistem durumu için Hello JSON çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="58341-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="58341-154">Merhaba *dipDownCount* özelliği Merhaba, ağ trafiğini toofailed araştırma yanıtları son gösterilmeyen uç hello toplam örneği sayısı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="58341-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="58341-155">Görüntüleme ve hello denetim günlüğü çözümleme</span><span class="sxs-lookup"><span data-stu-id="58341-155">View and analyze hello audit log</span></span>

<span data-ttu-id="58341-156">Görüntüleme ve yöntemleri aşağıdaki hello birini kullanarak denetim günlüğü verilerini çözümleme:</span><span class="sxs-lookup"><span data-stu-id="58341-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="58341-157">**Azure Araçları:** bilgi almanızı hello denetim günlüklerini Azure PowerShell, hello Azure komut satırı arabirimi (CLI), hello Azure REST API'si aracılığıyla veya Azure Önizleme portalını hello.</span><span class="sxs-lookup"><span data-stu-id="58341-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="58341-158">Her yöntem için adım adım yönergeler hello ayrıntılı [denetim işlemleri Resource Manager ile](../azure-resource-manager/resource-group-audit.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="58341-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="58341-159">**Power BI:** zaten yoksa bir [Power BI](https://powerbi.microsoft.com/pricing) hesabı deneyebilirsiniz, ücretsiz.</span><span class="sxs-lookup"><span data-stu-id="58341-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="58341-160">Hello kullanarak [Azure denetim günlükleri paketi Power BI için içerik](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), önceden yapılandırılmış panolar verilerinizle analiz edebilirsiniz veya gereksinimlerinizi görünümleri toosuit özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58341-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="58341-161">Görüntüleme ve hello durum araştırması ve olay günlüğü çözümleme</span><span class="sxs-lookup"><span data-stu-id="58341-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="58341-162">Tooconnect tooyour depolama alanına ihtiyacınız hesap ve olay ve sistem durumu araştırma günlükleri için hello JSON günlük girişlerini almak.</span><span class="sxs-lookup"><span data-stu-id="58341-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="58341-163">Merhaba JSON dosyaları yükledikten sonra bunları tooCSV ve Excel, Powerbı veya başka bir veri görselleştirme araç görünümünde dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58341-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="58341-164">Visual Studio ve sabitleri ve değişkenleri C# değerlerini değiştirmenin temel kavramları biliyorsanız hello kullanabilirsiniz [Dönüştürücü Araçları oturum](https://github.com/Azure-Samples/networking-dotnet-log-converter) github'dan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="58341-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58341-165">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="58341-165">Additional resources</span></span>

* <span data-ttu-id="58341-166">[Azure denetim günlükleri Power BI ile görselleştirme](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog postası.</span><span class="sxs-lookup"><span data-stu-id="58341-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="58341-167">[Görüntüleme ve Azure denetim günlükleri Power BI ve daha fazla çözümleme](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog postası.</span><span class="sxs-lookup"><span data-stu-id="58341-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58341-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58341-168">Next steps</span></span>

[<span data-ttu-id="58341-169">Yük dengeleyici araştırmalarını anlama</span><span class="sxs-lookup"><span data-stu-id="58341-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
