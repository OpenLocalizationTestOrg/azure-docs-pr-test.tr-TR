---
title: "Azure SQL veritabanı ölçümleri & tanılama günlükleri | Microsoft Docs"
description: "Kaynak kullanımı, bağlantı ve sorgu yürütme istatistikleri depolamak için Azure SQL veritabanı kaynak yapılandırma hakkında bilgi edinin."
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
ms.openlocfilehash: bf41aa530c68ea0e94a09d1dab63237c6f42bce7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="4052a-103">Azure SQL Database ölçümleri ve tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="4052a-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="4052a-104">Azure SQL Database ölçümleri ve daha kolay izleme için tanılama günlükleri yayma.</span><span class="sxs-lookup"><span data-stu-id="4052a-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="4052a-105">Kaynak kullanımı, çalışanlar ve oturumlar ve bu Azure kaynakları birine bağlantısını depolamak için Azure SQL veritabanı yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4052a-105">You can configure Azure SQL Database to store resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="4052a-106">**Azure Depolama**: Küçük maliyetlerle çok sayıda telemetri arşivleme için</span><span class="sxs-lookup"><span data-stu-id="4052a-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="4052a-107">**Azure Event Hub**: Azure SQL veritabanı telemetri özel izleme çözümü veya etkin işlem hatları ile tümleştirmek için</span><span class="sxs-lookup"><span data-stu-id="4052a-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="4052a-108">**Azure günlük analizi**: için raporlama, uyarı ve yetenekleri Azaltıcı çözüm izleme kutusunu dışında</span><span class="sxs-lookup"><span data-stu-id="4052a-108">**Azure Log Analytics**: For out of the box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![architecture](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="4052a-110">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4052a-110">Enable logging</span></span>

<span data-ttu-id="4052a-111">Ölçümleri ve Tanılama Günlüğü varsayılan olarak etkinleştirilmedi.</span><span class="sxs-lookup"><span data-stu-id="4052a-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="4052a-112">Etkinleştirme ve ölçüm ve aşağıdaki yöntemlerden birini kullanarak oturum tanılama yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4052a-112">You can enable and manage metrics and diagnostics logging using one of the following methods:</span></span>
- <span data-ttu-id="4052a-113">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="4052a-113">Azure portal</span></span>
- <span data-ttu-id="4052a-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4052a-114">PowerShell</span></span>
- <span data-ttu-id="4052a-115">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4052a-115">Azure CLI</span></span>
- <span data-ttu-id="4052a-116">REST API</span><span class="sxs-lookup"><span data-stu-id="4052a-116">REST API</span></span> 
- <span data-ttu-id="4052a-117">Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="4052a-117">Resource Manager template</span></span>

<span data-ttu-id="4052a-118">Ölçümleri ve tanılama günlükleri etkinleştirdiğinizde, burada seçilen verileri toplanır Azure kaynak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4052a-118">When you enable metrics and diagnostics logging, you need to specify the Azure resource where selected data is collected.</span></span> <span data-ttu-id="4052a-119">Seçenekleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="4052a-119">Options available:</span></span>
- <span data-ttu-id="4052a-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4052a-120">Log analytics</span></span>
- <span data-ttu-id="4052a-121">Olay Hub'ı</span><span class="sxs-lookup"><span data-stu-id="4052a-121">Event Hub</span></span>
- <span data-ttu-id="4052a-122">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4052a-122">Azure Storage</span></span> 

<span data-ttu-id="4052a-123">Yeni bir Azure kaynak sağlama veya var olan bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="4052a-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="4052a-124">Depolama kaynağı seçtikten sonra hangi verileri toplamak için belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4052a-124">After selecting the storage resource, you need to specify which data to collect.</span></span> <span data-ttu-id="4052a-125">Kullanılabilir seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4052a-125">Options available include:</span></span>

- <span data-ttu-id="4052a-126">**[1 dakikalık ölçümleri](sql-database-metrics-diag-logging.md#1-minute-metrics)**  -içeren DTU yüzdesi, DTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, başarılı/başarısız/engellenen Güvenlik Duvarı bağlantılarını, oturumlar yüzdesi, çalışanların yüzdesi Depolama, depolama yüzdesi, XTP depolama yüzdesi</span><span class="sxs-lookup"><span data-stu-id="4052a-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="4052a-127">Olay hub'ı veya bir AzureStorage hesabı belirtirseniz, seçilen zaman aralığı silinmiş daha eski bu verileri belirtmek için bir bekletme ilkesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy to specify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="4052a-128">Günlük analizi belirtirseniz, bekletme ilkesi seçilen fiyatlandırma katmanını bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4052a-128">If you specify Log Analytics, the retention policy depends on the selected pricing tier.</span></span> <span data-ttu-id="4052a-129">Daha fazla bilgi edinin [günlük analizi fiyatlandırma](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="4052a-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="4052a-130">Her ikisi de okumanızı öneririz [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md) ve [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) günlük ancak ölçümleri etkinleştirmek yalnızca nasıl anlamak için makaleleri ve çeşitli Azure Hizmetleri tarafından desteklenen kategorileri oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4052a-130">We recommend that you read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4052a-131">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="4052a-131">Azure portal</span></span>

<span data-ttu-id="4052a-132">Ölçümleri ve tanılama günlüklerini toplama Azure portalında etkinleştirmek için Azure SQL veritabanı veya esnek havuz sayfasına gidin ve ardından **tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="4052a-132">To enable metrics and diagnostic logs collection in the Azure portal, navigate to your Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![Azure portalında etkinleştir](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="4052a-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4052a-134">PowerShell</span></span>

<span data-ttu-id="4052a-135">Ölçümleri ve PowerShell kullanarak tanılama günlük kaydını etkinleştirmek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-135">To enable metrics and diagnostics logging using PowerShell, use the following commands:</span></span>

- <span data-ttu-id="4052a-136">Tanılama günlüklerinin bir depolama hesabındaki depolama etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-136">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="4052a-137">Depolama hesabı kimliği günlükleri göndermek istediğiniz depolama hesabını kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="4052a-137">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="4052a-138">Bir olay Hub'ına tanılama günlüklerini akışını etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-138">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="4052a-139">Hizmet veri yolu kuralı kimliği, bu biçiminde bir dizedir:</span><span class="sxs-lookup"><span data-stu-id="4052a-139">The Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="4052a-140">Günlük analizi çalışma alanı için tanılama günlüklerini gönderilmesine izin vermek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-140">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="4052a-141">Aşağıdaki komutu kullanarak, günlük analizi çalışma alanı kaynak kimliğini elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4052a-141">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="4052a-142">Birden çok çıktı seçenekleri etkinleştirmek için bu parametreler birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-142">You can combine these parameters to enable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="4052a-143">CLI</span><span class="sxs-lookup"><span data-stu-id="4052a-143">CLI</span></span>

<span data-ttu-id="4052a-144">Ölçümleri ve Azure CLI kullanarak tanılama günlük kaydını etkinleştirmek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-144">To enable metrics and diagnostics logging using the Azure CLI, use the following commands:</span></span>

- <span data-ttu-id="4052a-145">Tanılama günlüklerinin bir depolama hesabındaki depolama etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-145">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="4052a-146">Depolama hesabı kimliği günlükleri göndermek istediğiniz depolama hesabını kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="4052a-146">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

- <span data-ttu-id="4052a-147">Bir olay Hub'ına tanılama günlüklerini akışını etkinleştirmek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-147">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="4052a-148">Hizmet veri yolu kuralı kimliği, bu biçiminde bir dizedir:</span><span class="sxs-lookup"><span data-stu-id="4052a-148">The Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="4052a-149">Günlük analizi çalışma alanı için tanılama günlüklerini gönderilmesine izin vermek için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4052a-149">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

<span data-ttu-id="4052a-150">Birden çok çıktı seçenekleri etkinleştirmek için bu parametreler birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-150">You can combine these parameters to enable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="4052a-151">REST API</span><span class="sxs-lookup"><span data-stu-id="4052a-151">REST API</span></span>

<span data-ttu-id="4052a-152">Konusunu okuyun [Azure İzleyici REST API'sini kullanarak tanılama ayarlarını değiştirme](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="4052a-152">Read about how to [change Diagnostic settings using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="4052a-153">Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="4052a-153">Resource Manager template</span></span>

<span data-ttu-id="4052a-154">Konusunu okuyun [Resource Manager şablonu kullanarak kaynak oluşturmada tanılama ayarlarını etkinleştirin](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="4052a-154">Read about how to [enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="4052a-155">Günlük analizi akışa</span><span class="sxs-lookup"><span data-stu-id="4052a-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="4052a-156">Azure SQL Database ölçümleri ve tanılama günlükleri, günlük analizi portalında veya Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyici REST API'si aracılığıyla tanılama ayarında günlük analizi etkinleştirerek yerleşik "Göndermek için günlük analizi" seçeneğini kullanarak içine gönderilebilen.</span><span class="sxs-lookup"><span data-stu-id="4052a-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using the built-in “Send to Log Analytics” option in the portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="4052a-157">Yüklemeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="4052a-157">Installation overview</span></span>

<span data-ttu-id="4052a-158">Azure SQL veritabanı Donanma izleme günlük analizi ile basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="4052a-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="4052a-159">Üç adım gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="4052a-159">Three steps are required:</span></span>

1.  <span data-ttu-id="4052a-160">Günlük analizi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4052a-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="4052a-161">Ölçümleri ve tanılama günlüklerini oluşturulan günlük analizi kaydetmek için veritabanlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4052a-161">Configure databases to record metrics and diagnostic logs into the created Log Analytics</span></span>
3.  <span data-ttu-id="4052a-162">Yükleme **Azure SQL analizi** günlük analizi Galerisi'nde çözüm</span><span class="sxs-lookup"><span data-stu-id="4052a-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="4052a-163">Günlük analizi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4052a-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="4052a-164">Tıklatın **yeni** sol menüde.</span><span class="sxs-lookup"><span data-stu-id="4052a-164">Click **New** in the left-hand menu.</span></span>
2. <span data-ttu-id="4052a-165">Tıklatın **izleme + Yönetimi**</span><span class="sxs-lookup"><span data-stu-id="4052a-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="4052a-166">Tıklatın **günlük analizi**</span><span class="sxs-lookup"><span data-stu-id="4052a-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="4052a-167">Gerekli ek bilgiler içeren günlük analizi formu doldurun: çalışma alanı adı, abonelik, kaynak grubu, konum ve fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="4052a-167">Fill in the Log Analytics form with the additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![günlük analizi](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-to-record-metrics-and-diagnostic-logs"></a><span data-ttu-id="4052a-169">Kayıt ölçümleri ve tanılama günlüklerini veritabanlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="4052a-169">Configure databases to record metrics and diagnostic logs</span></span>

<span data-ttu-id="4052a-170">Azure portalı üzerinden nerede veritabanları kendi ölçümleri kaydı yapılandırmak için en kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="4052a-170">The easiest way to configure where databases record their metrics is through the Azure portal.</span></span> <span data-ttu-id="4052a-171">Azure portalında Azure SQL veritabanı kaynağınızın gidin ve tıklayın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="4052a-171">In the Azure portal, navigate to your Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-the-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="4052a-172">Azure SQL analiz çözümü Galerisi'nden yükleyin</span><span class="sxs-lookup"><span data-stu-id="4052a-172">Install the Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="4052a-173">Günlük analizi kaynağı oluşturulur ve verilerinizi içine akan sonra Azure SQL analiz çözümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4052a-173">Once the Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="4052a-174">Bu aracılığıyla yapılabilir **Çözümleri Galerisi** , OMS giriş sayfası ve yan menüde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-174">This can be done through the **Solutions Gallery** that you can find on the OMS homepage and in the side menu.</span></span> <span data-ttu-id="4052a-175">Galeride bulun ve tıklatın **Azure SQL analizi** çözümü ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4052a-175">In the gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![İzleme çözümü](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="4052a-177">OMS sayfanız üzerinde yeni bir kutucuk olarak adlandırılan **Azure SQL analizi** görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4052a-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="4052a-178">Bu kutucuğu seçerek Azure SQL analizi panosu açılır.</span><span class="sxs-lookup"><span data-stu-id="4052a-178">Selecting this tile opens the Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="4052a-179">Azure SQL analiz çözümü kullanma</span><span class="sxs-lookup"><span data-stu-id="4052a-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="4052a-180">Azure SQL analizi Azure SQL veritabanı kaynak hiyerarşisi aracılığıyla gitmeye izin veren hiyerarşik bir Pano ' dir.</span><span class="sxs-lookup"><span data-stu-id="4052a-180">Azure SQL Analytics is a hierarchical dashboard that allows you to navigate through the hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="4052a-181">Bu özellik, üst düzey izleme yapmanıza olanak sağlar, ancak yalnızca sağ kümesine kaynakların izleme kapsamını belirlemek de sağlar.</span><span class="sxs-lookup"><span data-stu-id="4052a-181">This capability enables you to do high-level monitoring but it also enables you to scope your monitoring to just the right set of resources.</span></span>
<span data-ttu-id="4052a-182">Pano seçili kaynağın farklı kaynaklarınıza listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="4052a-182">Dashboard contains the lists of different resources under the selected resource.</span></span> <span data-ttu-id="4052a-183">Örneğin, seçili abonelik için tüm sunucular, esnek havuzlar ve seçilen aboneliğe ait veritabanları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-183">For example, for a selected subscription you can see the all servers, elastic pools and databases that belong to the selected subscription.</span></span> <span data-ttu-id="4052a-184">Ayrıca, esnek havuzlar ve veritabanları için bu kaynağın kaynak kullanım ölçümleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-184">Additionally, for Elastic Pools and databases, you can see the resource usage metrics of that resource.</span></span> <span data-ttu-id="4052a-185">Bu grafik DTU, CPU, g/ç, günlük, oturumlar, çalışanlar, bağlantıları ve GB depolama içerir.</span><span class="sxs-lookup"><span data-stu-id="4052a-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="4052a-186">Azure Event hub'ı akışa</span><span class="sxs-lookup"><span data-stu-id="4052a-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="4052a-187">Azure SQL Database ölçümleri ve tanılama günlükleri, olay hub'ı portalında veya Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyici REST API'si aracılığıyla tanılama ayarında Service Bus kural kimliği etkinleştirerek yerleşik "Bir olay hub'ına akış" seçeneğini kullanarak içine gönderilebilen.</span><span class="sxs-lookup"><span data-stu-id="4052a-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using the built-in “Stream to an event hub” option in the portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-to-do-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="4052a-188">Yapılacaklar ölçümleri ve Event Hub'ındaki tanılama günlükleri ile?</span><span class="sxs-lookup"><span data-stu-id="4052a-188">What to do with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="4052a-189">Seçili verileri olay Hub'ına akışı verdikten sonra etkinleştirme için bir adım daha yaklaşarak artık izleme senaryoları Gelişmiş demektir.</span><span class="sxs-lookup"><span data-stu-id="4052a-189">Once the selected data is streamed into Event Hub, you are one step closer to enabling advanced monitoring scenarios.</span></span> <span data-ttu-id="4052a-190">Event Hubs bir olay komut zincirinin "ön kapısı" olarak görev yapar ve veriler bir Event Hub'ına toplandıktan sonra herhangi bir gerçek zamanlı analiz sağlayıcısı veya toplu işlem/depolama bağdaştırıcısı kullanılarak dönüştürülebilir ve depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="4052a-190">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="4052a-191">Event Hubs olay akışı üretimlerini bu olayların tüketilmesinden ayırır, böylece olay tüketicileri olaylara kendi zamanlamalarında erişebilir.</span><span class="sxs-lookup"><span data-stu-id="4052a-191">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span> <span data-ttu-id="4052a-192">Olay hub'ı hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="4052a-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="4052a-193">[Azure Event Hubs nedir](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="4052a-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="4052a-194">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="4052a-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="4052a-195">Akış özelliği kullanabilir birkaç yollar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4052a-195">Here are just a few ways you might use the streaming capability:</span></span>

-   <span data-ttu-id="4052a-196">Hizmet durumunu görüntülemek için Powerbı - olay hub'ı kullanarak, akış analizi ve Powerbı, "sıcak yolu" veri akış tarafından kolayca ölçümleri ve tanılama verilerinizi yakın gerçek zamanlı Öngörüler Azure hizmetlerinizi dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4052a-196">View service health by streaming “hot path” data to PowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="4052a-197">Bir Event Hubs, akış analizi ve bir çıkış olarak kullanmak üzere Powerbı ile verileri işlemek ayarlama hakkında genel bakış için bkz: [akış analizi ve Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="4052a-197">For an overview of how to set up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="4052a-198">Akış günlükleri akışlara üçüncü taraf günlüğe kaydetme ve telemetri – kullanarak Event Hubs, akış ölçümlerinizi alabilir ve tanılama farklı üçüncü taraf izleme ve günlük analizi çözümleri günlükleri.</span><span class="sxs-lookup"><span data-stu-id="4052a-198">Stream logs to third-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in to different third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="4052a-199">Bir özel telemetri ve günlüğe kaydetme platformu yapı – zaten bir özel olarak geliştirilmiş telemetri platform varsa veya olan yalnızca biri, yüksek düzeyde ölçeklenebilir yapı hakkında olay hub'ları yapısını yayımlama-abone düşünüyorum esnek tanılama günlüklerini alma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="4052a-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest diagnostic logs.</span></span> <span data-ttu-id="4052a-200">Bkz: [bir küresel ölçekteki telemetri platform olay hub'ları kullanarak Dan Rosanova'nın kılavuzuna](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="4052a-200">See [Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="4052a-201">Azure depolama alanına akış</span><span class="sxs-lookup"><span data-stu-id="4052a-201">Stream into Azure Storage</span></span>

<span data-ttu-id="4052a-202">Azure SQL veritabanı ölçümleri ve tanılama günlükleri, Azure portalında veya Azure Storage Azure PowerShell cmdlet'leri, Azure CLI veya Azure İzleyicisi aracılığıyla tanılama ayarı etkinleştirerek yerleşik "Depolama hesabı arşivi" seçeneğini kullanarak Azure depolama alanına depolanabilir REST API.</span><span class="sxs-lookup"><span data-stu-id="4052a-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using the built-in "Archive to a storage account” option in the Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="4052a-203">Şema ölçümleri ve depolama hesabındaki tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="4052a-203">Schema of metrics and diagnostic logs in the storage account</span></span>

<span data-ttu-id="4052a-204">Ölçümleri ve tanılama günlüklerini toplama ayarladıktan sonra bir depolama kapsayıcısı ilk veri satırı kullanılamadığında, seçtiğiniz depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4052a-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in the storage account you selected when the first rows of data are available.</span></span> <span data-ttu-id="4052a-205">Bu BLOB'ları yapıdır:</span><span class="sxs-lookup"><span data-stu-id="4052a-205">The structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="4052a-206">Veya daha basit bir şekilde:</span><span class="sxs-lookup"><span data-stu-id="4052a-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="4052a-207">Örneğin, bir blob adı 1 dakikalık ölçümünün olabilir:</span><span class="sxs-lookup"><span data-stu-id="4052a-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="4052a-208">Esnek havuz verileri kaydetmek istediğiniz durumunda, blob adı biraz farklıdır:</span><span class="sxs-lookup"><span data-stu-id="4052a-208">In case you want to record the data from the Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="4052a-209">İndirme ölçümleri ve Azure depolama günlükleri</span><span class="sxs-lookup"><span data-stu-id="4052a-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="4052a-210">Bkz: [Azure depolama biriminden ölçümleri ve tanılama günlüklerini indirin](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="4052a-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="4052a-211">1 dakikalık ölçümleri</span><span class="sxs-lookup"><span data-stu-id="4052a-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="4052a-212">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="4052a-212">**Resource**</span></span>|<span data-ttu-id="4052a-213">**Ölçümler**</span><span class="sxs-lookup"><span data-stu-id="4052a-213">**Metrics**</span></span>|
|<span data-ttu-id="4052a-214">Database</span><span class="sxs-lookup"><span data-stu-id="4052a-214">Database</span></span>|<span data-ttu-id="4052a-215">DTU yüzdesi DTU kullanıldığında, DTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, başarılı/başarısız/engellenen Güvenlik Duvarı bağlantılarını, oturumlar yüzdesi, çalışanları yüzdesi, depolama, depolama yüzdesi, XTP depolama yüzdesi kilitlenmeleri</span><span class="sxs-lookup"><span data-stu-id="4052a-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="4052a-216">Esnek havuz</span><span class="sxs-lookup"><span data-stu-id="4052a-216">Elastic pool</span></span>|<span data-ttu-id="4052a-217">eDTU yüzde eDTU kullanıldığında, eDTU sınırı, CPU yüzdesi, fiziksel veri okuma yüzdesi, günlük yazma yüzdesi, oturumlar yüzdesi, çalışanları yüzdesi, depolama, depolama yüzdesi, depolama sınırı, XTP depolama yüzdesi</span><span class="sxs-lookup"><span data-stu-id="4052a-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4052a-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4052a-218">Next steps</span></span>

- <span data-ttu-id="4052a-219">Hem de okuma [Microsoft Azure ölçümlerini genel bakış](../monitoring-and-diagnostics/monitoring-overview-metrics.md) ve [genel bakış, Azure tanılama günlükleri](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) günlüğe kaydetme, ancak ölçümleri ve günlük kategorileri etkinleştirmek yalnızca nasıl anlamak için makaleleri çeşitli Azure Hizmetleri tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="4052a-219">Read both the [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles to gain an understanding of not only how to enable logging, but the metrics and log categories supported by the various Azure services.</span></span>
- <span data-ttu-id="4052a-220">Olay hub'ları hakkında bilgi edinmek için bu makaleler okuyun:</span><span class="sxs-lookup"><span data-stu-id="4052a-220">Read these articles to learn about event hubs:</span></span>
   - <span data-ttu-id="4052a-221">[Azure Event Hubs nedir](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="4052a-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="4052a-222">Event Hubs kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="4052a-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="4052a-223">Bkz: [Azure depolama biriminden ölçümleri ve tanılama günlüklerini indirin](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span><span class="sxs-lookup"><span data-stu-id="4052a-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
