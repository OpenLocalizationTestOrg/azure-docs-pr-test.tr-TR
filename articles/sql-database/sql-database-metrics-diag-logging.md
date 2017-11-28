---
title: "aaaAzure SQL veritabanı ölçümleri & tanılama günlükleri | Microsoft Docs"
description: "Azure SQL veritabanı kaynak toostore kaynak kullanımı, bağlantı ve sorgu yürütme istatistikleri yapılandırma hakkında bilgi edinin."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="1d5df-103">Azure SQL Database ölçümleri ve tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="1d5df-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="1d5df-104">Azure SQL Database ölçümleri ve daha kolay izleme için tanılama günlükleri yayma.</span><span class="sxs-lookup"><span data-stu-id="1d5df-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="1d5df-105">Azure SQL veritabanı toostore kaynak kullanımı, çalışanlar ve oturumlar ve bu Azure kaynakları birine bağlantısını yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d5df-105">You can configure Azure SQL Database toostore resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="1d5df-106">**Azure Depolama**: Küçük maliyetlerle çok sayıda telemetri arşivleme için</span><span class="sxs-lookup"><span data-stu-id="1d5df-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="1d5df-107">**Azure Event Hub**: Azure SQL veritabanı telemetri özel izleme çözümü veya etkin işlem hatları ile tümleştirmek için</span><span class="sxs-lookup"><span data-stu-id="1d5df-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="1d5df-108">**Azure günlük analizi**: için izleme çözümü bildirimi, uyarı ve yetenekleri Azaltıcı hello kutusu dışında</span><span class="sxs-lookup"><span data-stu-id="1d5df-108">**Azure Log Analytics**: For out of hello box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="1d5df-110">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="1d5df-110">Enable logging</span></span>

<span data-ttu-id="1d5df-111">Ölçümleri ve Tanılama Günlüğü varsayılan olarak etkinleştirilmedi.</span><span class="sxs-lookup"><span data-stu-id="1d5df-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="1d5df-112">Etkinleştirme ve ölçümleri ve tanılama günlükleri yöntemler aşağıdaki hello birini kullanarak yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d5df-112">You can enable and manage metrics and diagnostics logging using one of hello following methods:</span></span>
- <span data-ttu-id="1d5df-113">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="1d5df-113">Azure portal</span></span>
- <span data-ttu-id="1d5df-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d5df-114">PowerShell</span></span>
- <span data-ttu-id="1d5df-115">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1d5df-115">Azure CLI</span></span>
- <span data-ttu-id="1d5df-116">REST API</span><span class="sxs-lookup"><span data-stu-id="1d5df-116">REST API</span></span> 
- <span data-ttu-id="1d5df-117">Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="1d5df-117">Resource Manager template</span></span>

<span data-ttu-id="1d5df-118">Ölçümleri ve tanılama günlükleri etkinleştirdiğinizde, burada seçilen verileri toplanır Azure kaynak toospecify hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-118">When you enable metrics and diagnostics logging, you need toospecify hello Azure resource where selected data is collected.</span></span> <span data-ttu-id="1d5df-119">Seçenekleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="1d5df-119">Options available:</span></span>
- <span data-ttu-id="1d5df-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="1d5df-120">Log analytics</span></span>
- <span data-ttu-id="1d5df-121">Olay Hub'ı</span><span class="sxs-lookup"><span data-stu-id="1d5df-121">Event Hub</span></span>
- <span data-ttu-id="1d5df-122">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1d5df-122">Azure Storage</span></span> 

<span data-ttu-id="1d5df-123">Yeni bir Azure kaynak sağlama veya var olan bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="1d5df-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="1d5df-124">Merhaba depolama kaynağı seçtikten sonra hangi veri toocollect toospecify gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-124">After selecting hello storage resource, you need toospecify which data toocollect.</span></span> <span data-ttu-id="1d5df-125">Kullanılabilir seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1d5df-125">Options available include:</span></span>

- <span data-ttu-id="1d5df-126">**[1 dakikalık ölçümleri](sql-database-metrics-diag-logging.md#1-minute-metrics)**  -içeren DTU yüzdesi, DTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, başarılı/başarısız/engellenen Güvenlik Duvarı bağlantılarını, oturumlar yüzdesi, çalışanların yüzdesi Depolama, depolama yüzdesi, XTP depolama yüzdesi</span><span class="sxs-lookup"><span data-stu-id="1d5df-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="1d5df-127">Olay hub'ı veya bir AzureStorage hesabı belirtirseniz, seçilen bir zaman dilimi silinir daha eski olan verilerin bir bekletme ilkesi toospecify belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy toospecify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="1d5df-128">Günlük analizi belirtirseniz, hello bekletme ilkesi hello seçilen fiyatlandırma katmanı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1d5df-128">If you specify Log Analytics, hello retention policy depends on hello selected pricing tier.</span></span> <span data-ttu-id="1d5df-129">Daha fazla bilgi edinin [günlük analizi fiyatlandırma](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="1d5df-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="1d5df-130">Her iki hello okumanızı öneririz [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md) ve [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain bir anlayış nasıl değil yalnızca makaleler hello ancak tooenable günlüğe kaydetme Ölçümleri ve günlük kategorileri çeşitli Azure hizmetlerine hello tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-130">We recommend that you read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="1d5df-131">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="1d5df-131">Azure portal</span></span>

<span data-ttu-id="1d5df-132">tooenable ölçümleri ve hello Azure portal, tanılama günlüklerini toplama tooyour Azure SQL veritabanı veya esnek havuz sayfasına gidin ve ardından **tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="1d5df-132">tooenable metrics and diagnostic logs collection in hello Azure portal, navigate tooyour Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![Hello Azure portal'ı etkinleştir](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="1d5df-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d5df-134">PowerShell</span></span>

<span data-ttu-id="1d5df-135">tooenable ölçümleri ve günlük kaydı tanılama PowerShell kullanarak hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-135">tooenable metrics and diagnostics logging using PowerShell, use hello following commands:</span></span>

- <span data-ttu-id="1d5df-136">bir depolama hesabında tanılama günlüklerinin tooenable depolama bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-136">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="1d5df-137">Merhaba depolama hesabı toowhich toosend hello istediğiniz günlükleri için hello depolama hesabı kimliği hello kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-137">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="1d5df-138">Tanılama günlüklerini tooan olay hub'ı tooenable akış bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-138">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="1d5df-139">Merhaba Service Bus kural kimliği bu biçiminde bir dize şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1d5df-139">hello Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="1d5df-140">Tanılama günlüklerini tooa günlük analizi çalışma alanının tooenable gönderme bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-140">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="1d5df-141">Merhaba kaynak kimliği komutu aşağıdaki hello kullanarak günlük analizi çalışma alanınızın elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1d5df-141">You can obtain hello resource id of your Log Analytics workspace using hello following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="1d5df-142">Bu parametreleri tooenable birden çok çıktı seçenekleri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-142">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="1d5df-143">CLI</span><span class="sxs-lookup"><span data-stu-id="1d5df-143">CLI</span></span>

<span data-ttu-id="1d5df-144">tooenable ölçümleri ve günlük Tanılama'yı kullanarak Azure CLI, aşağıdaki komutları kullanın hello hello:</span><span class="sxs-lookup"><span data-stu-id="1d5df-144">tooenable metrics and diagnostics logging using hello Azure CLI, use hello following commands:</span></span>

- <span data-ttu-id="1d5df-145">bir depolama hesabında tanılama günlüklerinin tooenable depolama bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-145">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="1d5df-146">Merhaba depolama hesabı toowhich toosend hello istediğiniz günlükleri için hello depolama hesabı kimliği hello kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-146">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="1d5df-147">Tanılama günlüklerini tooan olay hub'ı tooenable akış bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-147">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="1d5df-148">Merhaba Service Bus kural kimliği bu biçiminde bir dize şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1d5df-148">hello Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="1d5df-149">Tanılama günlüklerini tooa günlük analizi çalışma alanının tooenable gönderme bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1d5df-149">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

<span data-ttu-id="1d5df-150">Bu parametreleri tooenable birden çok çıktı seçenekleri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-150">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="1d5df-151">REST API</span><span class="sxs-lookup"><span data-stu-id="1d5df-151">REST API</span></span>

<span data-ttu-id="1d5df-152">Hakkında çok okuma[hello Azure İzleyici REST API'sini kullanarak tanılama ayarlarını değiştirme](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d5df-152">Read about how too[change Diagnostic settings using hello Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="1d5df-153">Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="1d5df-153">Resource Manager template</span></span>

<span data-ttu-id="1d5df-154">Hakkında çok okuma[Resource Manager şablonu kullanarak kaynak oluşturmada tanılama ayarlarını etkinleştirin](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="1d5df-154">Read about how too[enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="1d5df-155">Günlük analizi akışa</span><span class="sxs-lookup"><span data-stu-id="1d5df-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="1d5df-156">Azure SQL Database ölçümleri ve tanılama günlüklerini hello portalında veya Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyici REST aracılığıyla tanılama ayarında günlük analizi etkinleştirerek hello yerleşik "tooLog Analytics Gönder" seçeneğini kullanarak günlük analizi içine gönderilebilen API.</span><span class="sxs-lookup"><span data-stu-id="1d5df-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using hello built-in “Send tooLog Analytics” option in hello portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="1d5df-157">Yüklemeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="1d5df-157">Installation overview</span></span>

<span data-ttu-id="1d5df-158">Azure SQL veritabanı Donanma izleme günlük analizi ile basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="1d5df-159">Üç adım gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="1d5df-159">Three steps are required:</span></span>

1.  <span data-ttu-id="1d5df-160">Günlük analizi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d5df-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="1d5df-161">Günlük analizi oluşturulan hello veritabanları toorecord ölçümleri ve tanılama günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1d5df-161">Configure databases toorecord metrics and diagnostic logs into hello created Log Analytics</span></span>
3.  <span data-ttu-id="1d5df-162">Yükleme **Azure SQL analizi** günlük analizi Galerisi'nde çözüm</span><span class="sxs-lookup"><span data-stu-id="1d5df-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="1d5df-163">Günlük analizi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1d5df-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="1d5df-164">Tıklatın **yeni** hello sol menüde.</span><span class="sxs-lookup"><span data-stu-id="1d5df-164">Click **New** in hello left-hand menu.</span></span>
2. <span data-ttu-id="1d5df-165">Tıklatın **izleme + Yönetimi**</span><span class="sxs-lookup"><span data-stu-id="1d5df-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="1d5df-166">Tıklatın **günlük analizi**</span><span class="sxs-lookup"><span data-stu-id="1d5df-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="1d5df-167">Gerekli hello ek bilgilerle Hello günlük analizi formu doldurun: çalışma alanı adı, abonelik, kaynak grubu, konum ve fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="1d5df-167">Fill in hello Log Analytics form with hello additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![günlük analizi](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a><span data-ttu-id="1d5df-169">Veritabanlarını toorecord ölçümleri ve tanılama günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1d5df-169">Configure databases toorecord metrics and diagnostic logs</span></span>

<span data-ttu-id="1d5df-170">Burada veritabanları kendi ölçümleri kayıt hello en kolay yolu tooconfigure hello Azure portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-170">hello easiest way tooconfigure where databases record their metrics is through hello Azure portal.</span></span> <span data-ttu-id="1d5df-171">Azure portal Merhaba, tooyour Azure SQL veritabanı kaynak gidin ve'ı tıklatın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="1d5df-171">In hello Azure portal, navigate tooyour Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="1d5df-172">Galeriden Hello Azure SQL analiz çözümü yükleyin</span><span class="sxs-lookup"><span data-stu-id="1d5df-172">Install hello Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="1d5df-173">Merhaba günlük analizi kaynak oluşturup verilerinizi içine akan sonra Azure SQL analiz çözümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1d5df-173">Once hello Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="1d5df-174">Bu hello yapılabilir **Çözümleri Galerisi** , hello OMS giriş sayfası ve hello yan menüde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-174">This can be done through hello **Solutions Gallery** that you can find on hello OMS homepage and in hello side menu.</span></span> <span data-ttu-id="1d5df-175">Merhaba Galerisi'nde bulun ve tıklatın **Azure SQL analizi** çözümü ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1d5df-175">In hello gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![İzleme çözümü](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="1d5df-177">OMS sayfanız üzerinde yeni bir kutucuk olarak adlandırılan **Azure SQL analizi** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="1d5df-178">Bu döşeme seçilerek hello Azure SQL analizi panosu açılır.</span><span class="sxs-lookup"><span data-stu-id="1d5df-178">Selecting this tile opens hello Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="1d5df-179">Azure SQL analiz çözümü kullanma</span><span class="sxs-lookup"><span data-stu-id="1d5df-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="1d5df-180">Azure SQL analizi hello hiyerarşisi Azure SQL veritabanı kaynakları aracılığıyla toonavigate sağlayan hiyerarşik bir Pano ' dir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-180">Azure SQL Analytics is a hierarchical dashboard that allows you toonavigate through hello hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="1d5df-181">Bu yeteneği sağlar, toodo, ancak aynı zamanda izleme üst düzey tooscope etkinleştirir izleme toojust hello sağ kaynakları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1d5df-181">This capability enables you toodo high-level monitoring but it also enables you tooscope your monitoring toojust hello right set of resources.</span></span>
<span data-ttu-id="1d5df-182">Pano farklı kaynaklar seçili hello kaynak altında hello listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-182">Dashboard contains hello lists of different resources under hello selected resource.</span></span> <span data-ttu-id="1d5df-183">Örneğin, seçili abonelik için hello gördüğünüz tüm sunucular, esnek havuzlar ve toohello ait veritabanları seçili abonelik.</span><span class="sxs-lookup"><span data-stu-id="1d5df-183">For example, for a selected subscription you can see hello all servers, elastic pools and databases that belong toohello selected subscription.</span></span> <span data-ttu-id="1d5df-184">Ayrıca, esnek havuzlar ve veritabanları için bu kaynağın hello kaynak kullanım ölçümleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-184">Additionally, for Elastic Pools and databases, you can see hello resource usage metrics of that resource.</span></span> <span data-ttu-id="1d5df-185">Bu grafik DTU, CPU, g/ç, günlük, oturumlar, çalışanlar, bağlantıları ve GB depolama içerir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="1d5df-186">Azure Event hub'ı akışa</span><span class="sxs-lookup"><span data-stu-id="1d5df-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="1d5df-187">Azure SQL Database ölçümleri ve tanılama günlükleri, olay hub'ı hello portalında veya Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyici REST aracılığıyla tanılama ayarında Service Bus kural kimliği etkinleştirerek hello yerleşik "akış tooan olay hub'ı" seçeneğini kullanarak içine gönderilebilen API.</span><span class="sxs-lookup"><span data-stu-id="1d5df-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using hello built-in “Stream tooan event hub” option in hello portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="1d5df-188">Hangi toodo ölçümleri ve Event Hub'ındaki tanılama günlükleri ile?</span><span class="sxs-lookup"><span data-stu-id="1d5df-188">What toodo with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="1d5df-189">Olay Hub'ına seçili hello veri akışı verdikten sonra Gelişmiş izleme senaryolarında bir adım daha yakından tooenabling demektir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-189">Once hello selected data is streamed into Event Hub, you are one step closer tooenabling advanced monitoring scenarios.</span></span> <span data-ttu-id="1d5df-190">Olay hub'ları hello bir olay komut zincirinin "ön kapı" olarak görev yapan ve veriler bir Event Hub'ına toplandıktan sonra dönüştürülebilir ve tüm gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak saklanır.</span><span class="sxs-lookup"><span data-stu-id="1d5df-190">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="1d5df-191">Olay hub'ları, böylece olay tüketicileri hello olayları kendi zamanlamalarında erişebilir hello üretim hello üretimini ilgili olayların olay akışının ayırır.</span><span class="sxs-lookup"><span data-stu-id="1d5df-191">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span> <span data-ttu-id="1d5df-192">Olay hub'ı hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="1d5df-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="1d5df-193">[Azure Event Hubs nedir](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="1d5df-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="1d5df-194">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="1d5df-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="1d5df-195">Yetenek akış hello kullanabilir birkaç yollar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1d5df-195">Here are just a few ways you might use hello streaming capability:</span></span>

-   <span data-ttu-id="1d5df-196">Görüntüleme hizmet durumu "etkin yolunuzda" veri tooPowerBI - olay hub'ı kullanarak, akış analizi ve Powerbı, akış tarafından kolayca ölçümleri ve tanılama verilerinizi yakın gerçek zamanlı Öngörüler Azure hizmetlerinizi dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-196">View service health by streaming “hot path” data tooPowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="1d5df-197">Nasıl tooset bir olay hub'ları, Yukarı Akış Analizi ile verileri işlemek ve Powerbı çıkış olarak kullanan bir genel bakış için bkz: [akış analizi ve Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="1d5df-197">For an overview of how tooset up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="1d5df-198">Akış günlükleri toothird taraf günlüğe kaydetme ve telemetri akışları – kullanarak Event Hubs, akış ölçümleri ve tanılama günlüklerini toodifferent üçüncü taraf izleme ve günlük analiz çözümleri elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d5df-198">Stream logs toothird-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in toodifferent third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="1d5df-199">Bir özel telemetri ve günlüğe kaydetme platformu – özel olarak geliştirilmiş telemetri platform zaten varsa veya olan tanılama günlüklerini alma yalnızca biri, yüksek düzeyde ölçeklenebilir hello yayımlama-abone olma yapı hakkında olay hub'ları yapısını tooflexibly sağlar düşünüyorum oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d5df-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="1d5df-200">Bkz: [küresel ölçekteki telemetri Platform Dan Rosanova'nın Kılavuzu toousing olay hub'ları](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="1d5df-200">See [Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="1d5df-201">Azure depolama alanına akış</span><span class="sxs-lookup"><span data-stu-id="1d5df-201">Stream into Azure Storage</span></span>

<span data-ttu-id="1d5df-202">Azure SQL veritabanı ölçümleri ve tanılama günlüklerini Azure hello Azure portalında veya Azure Storage Azure PowerShell cmdlet'leri, Azure CLI ya da Azure tanılama ayarı etkinleştirerek hello yerleşik "tooa depolama hesabı Arşiv" seçeneğini kullanarak depolama alanına depolanabilir İzleyici REST API.</span><span class="sxs-lookup"><span data-stu-id="1d5df-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using hello built-in "Archive tooa storage account” option in hello Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="1d5df-203">Ölçümleri ve tanılama günlüklerini hello depolama hesabındaki şeması</span><span class="sxs-lookup"><span data-stu-id="1d5df-203">Schema of metrics and diagnostic logs in hello storage account</span></span>

<span data-ttu-id="1d5df-204">Ölçümleri ve tanılama günlüklerini toplama ayarladıktan sonra bir depolama kapsayıcısı hello ilk veri satırı kullanılamadığında seçtiğiniz hello depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1d5df-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in hello storage account you selected when hello first rows of data are available.</span></span> <span data-ttu-id="1d5df-205">Bu BLOB Hello yapıdır:</span><span class="sxs-lookup"><span data-stu-id="1d5df-205">hello structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="1d5df-206">Veya daha basit bir şekilde:</span><span class="sxs-lookup"><span data-stu-id="1d5df-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="1d5df-207">Örneğin, bir blob adı 1 dakikalık ölçümünün olabilir:</span><span class="sxs-lookup"><span data-stu-id="1d5df-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="1d5df-208">Merhaba esnek havuz toorecord hello verileri istemeniz durumunda, blob adı biraz farklıdır:</span><span class="sxs-lookup"><span data-stu-id="1d5df-208">In case you want toorecord hello data from hello Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="1d5df-209">İndirme ölçümleri ve Azure depolama günlükleri</span><span class="sxs-lookup"><span data-stu-id="1d5df-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="1d5df-210">Bkz: [Azure depolama biriminden ölçümleri ve tanılama günlüklerini indirin](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="1d5df-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="1d5df-211">1 dakikalık ölçümleri</span><span class="sxs-lookup"><span data-stu-id="1d5df-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="1d5df-212">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="1d5df-212">**Resource**</span></span>|<span data-ttu-id="1d5df-213">**Ölçümler**</span><span class="sxs-lookup"><span data-stu-id="1d5df-213">**Metrics**</span></span>|
|<span data-ttu-id="1d5df-214">Database</span><span class="sxs-lookup"><span data-stu-id="1d5df-214">Database</span></span>|<span data-ttu-id="1d5df-215">DTU yüzdesi DTU kullanıldığında, DTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, başarılı/başarısız/engellenen Güvenlik Duvarı bağlantılarını, oturumlar yüzdesi, çalışanları yüzdesi, depolama, depolama yüzdesi, XTP depolama yüzdesi kilitlenmeleri</span><span class="sxs-lookup"><span data-stu-id="1d5df-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="1d5df-216">Esnek havuz</span><span class="sxs-lookup"><span data-stu-id="1d5df-216">Elastic pool</span></span>|<span data-ttu-id="1d5df-217">eDTU yüzde eDTU kullanıldığında, eDTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, oturumlar yüzdesi, çalışanları yüzdesi, depolama, depolama yüzdesi, depolama sınırı, XTP depolama yüzdesi</span><span class="sxs-lookup"><span data-stu-id="1d5df-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1d5df-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d5df-218">Next steps</span></span>

- <span data-ttu-id="1d5df-219">Her iki hello okuma [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md) ve [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) makaleler toogain değil yalnızca nasıl tooenable günlüğü, ancak hello ölçümleri ve günlük kategorileri bir anlama çeşitli Azure hizmetlerine Hello tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1d5df-219">Read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>
- <span data-ttu-id="1d5df-220">Bu makaleler toolearn event hubs hakkında okuyun:</span><span class="sxs-lookup"><span data-stu-id="1d5df-220">Read these articles toolearn about event hubs:</span></span>
   - <span data-ttu-id="1d5df-221">[Azure Event Hubs nedir](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="1d5df-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="1d5df-222">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="1d5df-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="1d5df-223">Bkz: [Azure depolama biriminden ölçümleri ve tanılama günlüklerini indirin](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="1d5df-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
