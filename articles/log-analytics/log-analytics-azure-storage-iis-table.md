---
title: "Azure günlük analizi olayları için IIS ve tablo depolama için aaaUse blob depolama | Microsoft Docs"
description: "Günlük analizi tanılama tootable depolama yazma Azure Hizmetleri için hello günlüklerini veya tooblob depolama yazılmış IIS günlüklerini okuyabilir."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="5efe3-103">Günlük analizi olan olaylar için IIS ve Azure tablo depolaması için Azure blob storage kullanma</span><span class="sxs-lookup"><span data-stu-id="5efe3-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="5efe3-104">Günlük analizi depolama veya IIS yazılı tooblob depolama oturum tanılama tootable yazma Hizmetleri aşağıdaki hello hello günlüklerini okuyabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5efe3-104">Log Analytics can read hello logs for hello following services that write diagnostics tootable storage or IIS logs written tooblob storage:</span></span>

* <span data-ttu-id="5efe3-105">Service Fabric kümeleri (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="5efe3-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="5efe3-106">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="5efe3-106">Virtual Machines</span></span>
* <span data-ttu-id="5efe3-107">Web/çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-107">Web/Worker Roles</span></span>

<span data-ttu-id="5efe3-108">Azure tanılama günlük analizi bu kaynakları için veri toplayabilmek için önce etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5efe3-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="5efe3-109">Tanılama etkinleştirildikten sonra hello Azure portalını kullanabilirsiniz veya PowerShell günlük analizi toocollect hello günlükleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5efe3-109">Once diagnostics are enabled, you can use hello Azure portal or PowerShell configure Log Analytics toocollect hello logs.</span></span>

<span data-ttu-id="5efe3-110">Azure tanılama toocollect Tanılama verileri çalışan rolü, web rolü veya Azure'da çalışan sanal makine sağlayan Azure uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="5efe3-110">Azure Diagnostics is an Azure extension that enables you toocollect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="5efe3-111">Merhaba veriler bir Azure depolama hesabında depolanır ve günlük analizi tarafından toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="5efe3-111">hello data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="5efe3-112">Günlük analizi toocollect için bu Azure tanılama günlükleri, aşağıdaki konumlardan hello hello günlükleri olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="5efe3-112">For Log Analytics toocollect these Azure Diagnostics logs, hello logs must be in hello following locations:</span></span>

| <span data-ttu-id="5efe3-113">Günlük türü</span><span class="sxs-lookup"><span data-stu-id="5efe3-113">Log Type</span></span> | <span data-ttu-id="5efe3-114">Kaynak Türü</span><span class="sxs-lookup"><span data-stu-id="5efe3-114">Resource Type</span></span> | <span data-ttu-id="5efe3-115">Konum</span><span class="sxs-lookup"><span data-stu-id="5efe3-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5efe3-116">IIS günlükleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-116">IIS logs</span></span> |<span data-ttu-id="5efe3-117">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="5efe3-117">Virtual Machines</span></span> <br> <span data-ttu-id="5efe3-118">Web rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-118">Web roles</span></span> <br> <span data-ttu-id="5efe3-119">Çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-119">Worker roles</span></span> |<span data-ttu-id="5efe3-120">wad IIS logfiles (Blob Depolama)</span><span class="sxs-lookup"><span data-stu-id="5efe3-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="5efe3-121">Syslog</span><span class="sxs-lookup"><span data-stu-id="5efe3-121">Syslog</span></span> |<span data-ttu-id="5efe3-122">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="5efe3-122">Virtual Machines</span></span> |<span data-ttu-id="5efe3-123">LinuxsyslogVer2v0 (Tablo depolama)</span><span class="sxs-lookup"><span data-stu-id="5efe3-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="5efe3-124">Service Fabric çalışma olayları</span><span class="sxs-lookup"><span data-stu-id="5efe3-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="5efe3-125">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="5efe3-125">Service Fabric nodes</span></span> |<span data-ttu-id="5efe3-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="5efe3-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="5efe3-127">Service Fabric güvenilir aktör olayları</span><span class="sxs-lookup"><span data-stu-id="5efe3-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="5efe3-128">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="5efe3-128">Service Fabric nodes</span></span> |<span data-ttu-id="5efe3-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="5efe3-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="5efe3-130">Service Fabric güvenilir hizmeti olayları</span><span class="sxs-lookup"><span data-stu-id="5efe3-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="5efe3-131">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="5efe3-131">Service Fabric nodes</span></span> |<span data-ttu-id="5efe3-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="5efe3-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="5efe3-133">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-133">Windows Event logs</span></span> |<span data-ttu-id="5efe3-134">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="5efe3-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="5efe3-135">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="5efe3-135">Virtual Machines</span></span> <br> <span data-ttu-id="5efe3-136">Web rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-136">Web roles</span></span> <br> <span data-ttu-id="5efe3-137">Çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-137">Worker roles</span></span> |<span data-ttu-id="5efe3-138">WADWindowsEventLogsTable (Tablo depolama)</span><span class="sxs-lookup"><span data-stu-id="5efe3-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="5efe3-139">Windows ETW günlükleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-139">Windows ETW logs</span></span> |<span data-ttu-id="5efe3-140">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="5efe3-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="5efe3-141">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="5efe3-141">Virtual Machines</span></span> <br> <span data-ttu-id="5efe3-142">Web rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-142">Web roles</span></span> <br> <span data-ttu-id="5efe3-143">Çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-143">Worker roles</span></span> |<span data-ttu-id="5efe3-144">WADETWEventTable (Tablo depolama)</span><span class="sxs-lookup"><span data-stu-id="5efe3-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="5efe3-145">Azure Web siteleri IIS günlükleri şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="5efe3-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="5efe3-146">Sanal makineler için hello yükleme hello seçeneğiniz [günlük analizi aracı](log-analytics-azure-vm-extension.md) sanal makine tooenable ek Öngörüler içine.</span><span class="sxs-lookup"><span data-stu-id="5efe3-146">For virtual machines, you have hello option of installing hello [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine tooenable additional insights.</span></span> <span data-ttu-id="5efe3-147">Ayrıca toobeing mümkün tooanalyze IIS günlüklerini ve olay günlüklerini, yapılandırma değişiklik izleme, SQL değerlendirmesi ve güncelleştirme değerlendirme dahil olmak üzere ek analiz gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5efe3-147">In addition toobeing able tooanalyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="5efe3-148">Bir sanal makinede Azure tanılamayı etkinleştirin koleksiyonu olay günlüğünü ve IIS günlüğü için</span><span class="sxs-lookup"><span data-stu-id="5efe3-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="5efe3-149">Koleksiyon hello Microsoft Azure portal kullanarak olay günlüğünü ve IIS günlüğü için aşağıdaki yordamı tooenable bir sanal makinede Azure tanılama kullanım hello.</span><span class="sxs-lookup"><span data-stu-id="5efe3-149">Use hello following procedure tooenable Azure diagnostics in a virtual machine for Event Log and IIS log collection using hello Microsoft Azure portal.</span></span>

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="5efe3-150">tooenable Azure Tanılama'hello Azure portal ile bir sanal makine</span><span class="sxs-lookup"><span data-stu-id="5efe3-150">tooenable Azure diagnostics in a virtual machine with hello Azure portal</span></span>
1. <span data-ttu-id="5efe3-151">Bir sanal makine oluşturduğunuzda hello VM aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-151">Install hello VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="5efe3-152">Merhaba sanal makine zaten varsa, VM aracısının yüklü olduğundan bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5efe3-152">If hello virtual machine already exists, verify that hello VM Agent is already installed.</span></span>

   * <span data-ttu-id="5efe3-153">İçinde Azure portal Merhaba, toohello sanal makine gidin, seçin **isteğe bağlı yapılandırma**, ardından **tanılama** ve **durum** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="5efe3-153">In hello Azure portal, navigate toohello virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** too**On**.</span></span>

     <span data-ttu-id="5efe3-154">Tamamlandıktan sonra hello VM yüklü ve çalışan hello Azure tanılama uzantısına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5efe3-154">Upon completion, hello VM has hello Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="5efe3-155">Tanılama verilerinin toplanması için bu uzantıyı sorumludur.</span><span class="sxs-lookup"><span data-stu-id="5efe3-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="5efe3-156">İzlemeyi etkinleştirmek ve olay günlüğü var olan bir VM yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5efe3-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="5efe3-157">Tanılama hello VM düzeyi adresindeki etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5efe3-157">You can enable diagnostics at hello VM level.</span></span> <span data-ttu-id="5efe3-158">tooenable tanılama ve olay günlüğünü yapılandırmak, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5efe3-158">tooenable diagnostics and then configure event logging, perform hello following steps:</span></span>

   1. <span data-ttu-id="5efe3-159">Merhaba VM seçin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-159">Select hello VM.</span></span>
   2. <span data-ttu-id="5efe3-160">Tıklatın **izleme**.</span><span class="sxs-lookup"><span data-stu-id="5efe3-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="5efe3-161">Tıklatın **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="5efe3-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="5efe3-162">Set hello **durum** çok**ON**.</span><span class="sxs-lookup"><span data-stu-id="5efe3-162">Set hello **Status** too**ON**.</span></span>
   5. <span data-ttu-id="5efe3-163">Toocollect istediğiniz her tanılama günlük seçin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-163">Select each diagnostics log that you want toocollect.</span></span>
   6. <span data-ttu-id="5efe3-164">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5efe3-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="5efe3-165">Web rolü IIS günlüğü ve olay toplama için Azure tanılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="5efe3-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="5efe3-166">Çok başvuran[nasıl tooEnable bir bulut hizmetinde tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) Azure tanılama etkinleştirme genel adımlar için.</span><span class="sxs-lookup"><span data-stu-id="5efe3-166">Refer too[How tooEnable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="5efe3-167">Merhaba yönergelerde bu bilgileri kullanın ve günlük analizi ile kullanılmak üzere özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-167">hello instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="5efe3-168">Azure Tanılama ile etkin:</span><span class="sxs-lookup"><span data-stu-id="5efe3-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="5efe3-169">IIS günlüklerini hello scheduledTransferPeriod aktarımı aralıklarla günlük verileri varsayılan olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="5efe3-169">IIS logs are stored by default, with log data transferred at hello scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="5efe3-170">Windows olay günlüklerini varsayılan olarak aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="5efe3-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="tooenable-diagnostics"></a><span data-ttu-id="5efe3-171">tooenable tanılama</span><span class="sxs-lookup"><span data-stu-id="5efe3-171">tooenable diagnostics</span></span>
<span data-ttu-id="5efe3-172">Windows olay günlüklerini tooenable veya toochange scheduledTransferPeriod Merhaba, gösterildiği gibi Azure hello XML yapılandırma dosyası (diagnostics.wadcfg) kullanarak tanılama Yapılandır [4. adım: Tanılama yapılandırma dosyanızı oluşturun ve hello yükleyin uzantısı](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="5efe3-172">tooenable Windows Event Logs, or toochange hello scheduledTransferPeriod, configure Azure Diagnostics using hello XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install hello extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="5efe3-173">Merhaba aşağıdaki örnek yapılandırma dosyası IIS günlüklerini ve tüm olayları hello uygulama ve sistem günlüklerini toplar:</span><span class="sxs-lookup"><span data-stu-id="5efe3-173">hello following example configuration file collects IIS Logs and all Events from hello Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="5efe3-174">ConfigurationSettings aşağıdaki örneğine hello gibi bir depolama hesabı belirttiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="5efe3-174">Ensure that your ConfigurationSettings specifies a storage account, as in hello following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="5efe3-175">Merhaba **AccountName** ve **AccountKey** değerleri hello erişim anahtarlarını Yönet altında hello depolama hesabı Panosu Azure portalında bulundu.</span><span class="sxs-lookup"><span data-stu-id="5efe3-175">hello **AccountName** and **AccountKey** values are found in hello Azure portal in hello storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="5efe3-176">Merhaba bağlantı dizesi için Hello Protokolü olmalıdır **https**.</span><span class="sxs-lookup"><span data-stu-id="5efe3-176">hello protocol for hello connection string must be **https**.</span></span>

<span data-ttu-id="5efe3-177">Merhaba güncelleştirilmiş tanılama yapılandırması uygulandıktan sonra tooyour bulut hizmeti ve yazılırken tanılama tooAzure depolama, ardından hazır tooconfigure günlük analizi olur.</span><span class="sxs-lookup"><span data-stu-id="5efe3-177">Once hello updated diagnostic configuration is applied tooyour cloud service and it is writing diagnostics tooAzure Storage, then you are ready tooconfigure Log Analytics.</span></span>

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a><span data-ttu-id="5efe3-178">Azure depolama biriminden Hello Azure portal toocollect günlüklerini kullanın</span><span class="sxs-lookup"><span data-stu-id="5efe3-178">Use hello Azure portal toocollect logs from Azure Storage</span></span>
<span data-ttu-id="5efe3-179">Hello Azure portal tooconfigure günlük analizi toocollect hello günlükleri, Azure Hizmetleri aşağıdaki hello için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5efe3-179">You can use hello Azure portal tooconfigure Log Analytics toocollect hello logs for hello following Azure services:</span></span>

* <span data-ttu-id="5efe3-180">Service Fabric kümeleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-180">Service Fabric clusters</span></span>
* <span data-ttu-id="5efe3-181">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="5efe3-181">Virtual Machines</span></span>
* <span data-ttu-id="5efe3-182">Web/çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="5efe3-182">Web/Worker Roles</span></span>

<span data-ttu-id="5efe3-183">Hello Azure portal, tooyour günlük analizi çalışma alanına gidin ve hello aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5efe3-183">In hello Azure portal, navigate tooyour Log Analytics workspace and perform hello following tasks:</span></span>

1. <span data-ttu-id="5efe3-184">Tıklatın *depolama hesapları günlükleri*</span><span class="sxs-lookup"><span data-stu-id="5efe3-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="5efe3-185">Merhaba tıklatın *Ekle* görevi</span><span class="sxs-lookup"><span data-stu-id="5efe3-185">Click hello *Add* task</span></span>
3. <span data-ttu-id="5efe3-186">Merhaba tanılama günlükleri içeren hello depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="5efe3-186">Select hello Storage account that contains hello diagnostics logs</span></span>
   * <span data-ttu-id="5efe3-187">Bu hesap, Klasik depolama hesabı veya bir Azure Resource Manager depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5efe3-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="5efe3-188">Merhaba toocollect günlükleri için istediğiniz veri türünü seçin</span><span class="sxs-lookup"><span data-stu-id="5efe3-188">Select hello Data Type you want toocollect logs for</span></span>
   * <span data-ttu-id="5efe3-189">Merhaba, IIS günlüklerini seçimlerdir; Olayları; Syslog (Linux); ETW günlükleri; Hizmeti yapı olayları</span><span class="sxs-lookup"><span data-stu-id="5efe3-189">hello choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="5efe3-190">veri türü ve değiştirilemez hello üzerinde temel kaynak Hello değeri otomatik olarak doldurulur</span><span class="sxs-lookup"><span data-stu-id="5efe3-190">hello value for Source is automatically populated based on hello data type and cannot be changed</span></span>
6. <span data-ttu-id="5efe3-191">Tamam toosave hello Yapılandırması'nı tıklatın</span><span class="sxs-lookup"><span data-stu-id="5efe3-191">Click OK toosave hello configuration</span></span>

<span data-ttu-id="5efe3-192">Günlük analizi toocollect istediğiniz ek depolama hesapları ve veri türleri için 2-6 adımlarını yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics toocollect.</span></span>

<span data-ttu-id="5efe3-193">Günlük analizi depolama hesabında hello mümkün toosee verilerden olduğunuz yaklaşık 30 dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="5efe3-193">In approximately 30 minutes, you are able toosee data from hello storage account in Log Analytics.</span></span> <span data-ttu-id="5efe3-194">Merhaba yapılandırma uygulandıktan sonra toostorage yazılan veriler yalnızca görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5efe3-194">You will only see data that is written toostorage after hello configuration is applied.</span></span> <span data-ttu-id="5efe3-195">Günlük analizi hello depolama hesabından hello önceden mevcut verileri okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="5efe3-195">Log Analytics does not read hello pre-existing data from hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="5efe3-196">Hello portal kaynağı var hello depolama hesabında bu hello doğrulanmadı veya yeni veriler yazılır.</span><span class="sxs-lookup"><span data-stu-id="5efe3-196">hello portal does not validate that hello Source exists in hello storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="5efe3-197">Bir sanal makinede Azure tanılamayı etkinleştirin koleksiyonu PowerShell kullanarak olay günlüğünü ve IIS günlüğü için</span><span class="sxs-lookup"><span data-stu-id="5efe3-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="5efe3-198">Kullanım hello adımları [yapılandırma günlük analizi tooindex Azure tanılama](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread tootable depolama yazılır Azure tanılama gelen.</span><span class="sxs-lookup"><span data-stu-id="5efe3-198">Use hello steps in [Configuring Log Analytics tooindex Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread from Azure diagnostics that are written tootable storage.</span></span>

<span data-ttu-id="5efe3-199">Azure PowerShell kullanarak depolama tooAzure yazılır hello olayları daha kesin olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5efe3-199">Using Azure PowerShell you can more precisely specify hello events that are written tooAzure Storage.</span></span>
<span data-ttu-id="5efe3-200">Daha fazla bilgi için bkz: [etkinleştirme tanılama Azure Virtual Machines'de](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5efe3-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="5efe3-201">Etkinleştirmek ve PowerShell Betiği aşağıdaki hello kullanarak Azure tanılama güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-201">You can enable and update Azure diagnostics using hello following PowerShell script.</span></span>
<span data-ttu-id="5efe3-202">Bu komut dosyasını bir özel günlük kaydı yapılandırmasıyla de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5efe3-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="5efe3-203">Merhaba betik tooset hello depolama hesabı, hizmet adı ve sanal makine adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5efe3-203">Modify hello script tooset hello storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="5efe3-204">Merhaba betik Klasik sanal makineleri için cmdlet'leri kullanır.</span><span class="sxs-lookup"><span data-stu-id="5efe3-204">hello script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="5efe3-205">Komut dosyası örneği aşağıdaki hello gözden geçirin, kopyalayın, gerektiği şekilde değiştirin, hello örnek bir PowerShell komut dosyası olarak kaydetmek ve hello betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5efe3-205">Review hello following script sample, copy it, modify it as needed, save hello sample as a PowerShell script file, and then run hello script.</span></span>

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="5efe3-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5efe3-206">Next steps</span></span>
* <span data-ttu-id="5efe3-207">[Günlük ve Azure Hizmetleri için ölçümleri toplamak](log-analytics-azure-storage.md) desteklenen Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="5efe3-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="5efe3-208">[Çözümlerle](log-analytics-add-solutions.md) hello veri tooprovide fikirler.</span><span class="sxs-lookup"><span data-stu-id="5efe3-208">[Enable Solutions](log-analytics-add-solutions.md) tooprovide insight into hello data.</span></span>
* <span data-ttu-id="5efe3-209">[Arama sorguları kullanmak](log-analytics-log-searches.md) tooanalyze hello veri.</span><span class="sxs-lookup"><span data-stu-id="5efe3-209">[Use search queries](log-analytics-log-searches.md) tooanalyze hello data.</span></span>
