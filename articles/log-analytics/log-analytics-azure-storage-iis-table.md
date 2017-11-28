---
title: "Azure günlük analizi olayları için IIS ve tablo depolama için BLOB storage kullanma | Microsoft Docs"
description: "Günlük analizi tablo depolama için tanılama yazma Azure Hizmetleri için günlükleri veya blob depolamaya yazılabilir IIS günlüklerini okuyabilir."
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
ms.openlocfilehash: 459ef90ca1d76bada6565bfefd7b4bd1086197d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="bde7b-103">Günlük analizi olan olaylar için IIS ve Azure tablo depolaması için Azure blob storage kullanma</span><span class="sxs-lookup"><span data-stu-id="bde7b-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="bde7b-104">Günlük analizi tablo depolama için tanılama yazma aşağıdaki hizmetler için günlükleri veya blob depolamaya yazılabilir IIS günlüklerini okuyabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bde7b-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="bde7b-105">Service Fabric kümeleri (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="bde7b-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="bde7b-106">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="bde7b-106">Virtual Machines</span></span>
* <span data-ttu-id="bde7b-107">Web/çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-107">Web/Worker Roles</span></span>

<span data-ttu-id="bde7b-108">Azure tanılama günlük analizi bu kaynakları için veri toplayabilmek için önce etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="bde7b-109">Tanılama etkinleştirildikten sonra Azure portalını kullanabilir veya PowerShell günlükleri toplamak için günlük analizi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bde7b-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="bde7b-110">Azure tanılama çalışan rolü, web rolü ya da sanal makine Azure'da çalışan Tanılama verileri toplayacak şekilde sağlayan Azure uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="bde7b-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="bde7b-111">Veriler bir Azure depolama hesabında depolanır ve günlük analizi tarafından toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="bde7b-112">Günlük analizi'nın bu Azure tanılama günlükleri toplamak günlükleri şu konumlarda olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="bde7b-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="bde7b-113">Günlük türü</span><span class="sxs-lookup"><span data-stu-id="bde7b-113">Log Type</span></span> | <span data-ttu-id="bde7b-114">Kaynak Türü</span><span class="sxs-lookup"><span data-stu-id="bde7b-114">Resource Type</span></span> | <span data-ttu-id="bde7b-115">Konum</span><span class="sxs-lookup"><span data-stu-id="bde7b-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bde7b-116">IIS günlükleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-116">IIS logs</span></span> |<span data-ttu-id="bde7b-117">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="bde7b-117">Virtual Machines</span></span> <br> <span data-ttu-id="bde7b-118">Web rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-118">Web roles</span></span> <br> <span data-ttu-id="bde7b-119">Çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-119">Worker roles</span></span> |<span data-ttu-id="bde7b-120">wad IIS logfiles (Blob Depolama)</span><span class="sxs-lookup"><span data-stu-id="bde7b-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="bde7b-121">Syslog</span><span class="sxs-lookup"><span data-stu-id="bde7b-121">Syslog</span></span> |<span data-ttu-id="bde7b-122">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="bde7b-122">Virtual Machines</span></span> |<span data-ttu-id="bde7b-123">LinuxsyslogVer2v0 (Tablo depolama)</span><span class="sxs-lookup"><span data-stu-id="bde7b-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="bde7b-124">Service Fabric çalışma olayları</span><span class="sxs-lookup"><span data-stu-id="bde7b-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="bde7b-125">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="bde7b-125">Service Fabric nodes</span></span> |<span data-ttu-id="bde7b-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="bde7b-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="bde7b-127">Service Fabric güvenilir aktör olayları</span><span class="sxs-lookup"><span data-stu-id="bde7b-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="bde7b-128">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="bde7b-128">Service Fabric nodes</span></span> |<span data-ttu-id="bde7b-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="bde7b-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="bde7b-130">Service Fabric güvenilir hizmeti olayları</span><span class="sxs-lookup"><span data-stu-id="bde7b-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="bde7b-131">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="bde7b-131">Service Fabric nodes</span></span> |<span data-ttu-id="bde7b-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="bde7b-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="bde7b-133">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-133">Windows Event logs</span></span> |<span data-ttu-id="bde7b-134">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="bde7b-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="bde7b-135">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="bde7b-135">Virtual Machines</span></span> <br> <span data-ttu-id="bde7b-136">Web rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-136">Web roles</span></span> <br> <span data-ttu-id="bde7b-137">Çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-137">Worker roles</span></span> |<span data-ttu-id="bde7b-138">WADWindowsEventLogsTable (Tablo depolama)</span><span class="sxs-lookup"><span data-stu-id="bde7b-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="bde7b-139">Windows ETW günlükleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-139">Windows ETW logs</span></span> |<span data-ttu-id="bde7b-140">Service Fabric düğümler</span><span class="sxs-lookup"><span data-stu-id="bde7b-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="bde7b-141">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="bde7b-141">Virtual Machines</span></span> <br> <span data-ttu-id="bde7b-142">Web rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-142">Web roles</span></span> <br> <span data-ttu-id="bde7b-143">Çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-143">Worker roles</span></span> |<span data-ttu-id="bde7b-144">WADETWEventTable (Tablo depolama)</span><span class="sxs-lookup"><span data-stu-id="bde7b-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="bde7b-145">Azure Web siteleri IIS günlükleri şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="bde7b-146">Sanal makineler için yükleme seçeneğiniz [günlük analizi aracı](log-analytics-azure-vm-extension.md) ek Öngörüler etkinleştirmek için sanal makinenize içine.</span><span class="sxs-lookup"><span data-stu-id="bde7b-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="bde7b-147">IIS günlüklerini ve olay günlüklerini analiz edebilirsiniz olmaya ek olarak, izleme yapılandırma değişikliği, SQL değerlendirmesi ve güncelleştirme değerlendirme dahil olmak üzere ek analiz gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="bde7b-148">Bir sanal makinede Azure tanılamayı etkinleştirin koleksiyonu olay günlüğünü ve IIS günlüğü için</span><span class="sxs-lookup"><span data-stu-id="bde7b-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="bde7b-149">Bir sanal makinede Microsoft Azure Portalı'nı kullanarak olay günlüğünü ve IIS günlük toplama için Azure Tanılama'yı etkinleştirmek için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bde7b-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="bde7b-150">Bir sanal makinede Azure portal ile Azure tanılama etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="bde7b-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="bde7b-151">Bir sanal makine oluşturduğunuzda VM aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="bde7b-152">Sanal makine zaten varsa, VM Aracısı zaten yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bde7b-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="bde7b-153">Azure portalında sanal makineye gidin **isteğe bağlı yapılandırma**, ardından **tanılama** ve **durum** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="bde7b-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="bde7b-154">Tamamlandığında, VM yüklü ve çalışan Azure tanılama uzantısına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="bde7b-155">Tanılama verilerinin toplanması için bu uzantıyı sorumludur.</span><span class="sxs-lookup"><span data-stu-id="bde7b-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="bde7b-156">İzlemeyi etkinleştirmek ve olay günlüğü var olan bir VM yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bde7b-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="bde7b-157">Tanılama VM düzeyinde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="bde7b-158">Tanılamayı etkinleştirin ve olay günlüğünü yapılandırmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bde7b-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="bde7b-159">VM seçin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-159">Select the VM.</span></span>
   2. <span data-ttu-id="bde7b-160">Tıklatın **izleme**.</span><span class="sxs-lookup"><span data-stu-id="bde7b-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="bde7b-161">Tıklatın **tanılama**.</span><span class="sxs-lookup"><span data-stu-id="bde7b-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="bde7b-162">Ayarlama **durum** için **ON**.</span><span class="sxs-lookup"><span data-stu-id="bde7b-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="bde7b-163">Toplamak istediğiniz her Tanılama Günlüğü'nü seçin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="bde7b-164">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bde7b-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="bde7b-165">Web rolü IIS günlüğü ve olay toplama için Azure tanılama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bde7b-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="bde7b-166">Başvurmak [nasıl için tanılamayı etkinleştir bir bulut hizmetinde](../cloud-services/cloud-services-dotnet-diagnostics.md) Azure tanılama etkinleştirme genel adımlar için.</span><span class="sxs-lookup"><span data-stu-id="bde7b-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="bde7b-167">Aşağıdaki yönergelerde bu bilgileri kullanın ve günlük analizi ile kullanılmak üzere özelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="bde7b-168">Azure Tanılama ile etkin:</span><span class="sxs-lookup"><span data-stu-id="bde7b-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="bde7b-169">IIS günlüklerini scheduledTransferPeriod aktarımı aralıklarla günlük verileri varsayılan olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="bde7b-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="bde7b-170">Windows olay günlüklerini varsayılan olarak aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="bde7b-171">Tanılama etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="bde7b-171">To enable diagnostics</span></span>
<span data-ttu-id="bde7b-172">Windows olay günlüklerini etkinleştirmek ya da scheduledTransferPeriod değiştirmek için XML yapılandırma dosyası (diagnostics.wadcfg) kullanarak Azure tanılama gösterildiği gibi yapılandırmak [4. adım: Tanılama yapılandırma dosyanızı oluşturun ve uzantısını yükle](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="bde7b-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="bde7b-173">Aşağıdaki örnek yapılandırma dosyası, uygulama ve sistem günlüklerini IIS günlüklerini ve tüm olayları toplar:</span><span class="sxs-lookup"><span data-stu-id="bde7b-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
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

<span data-ttu-id="bde7b-174">ConfigurationSettings aşağıdaki örnekteki gibi bir depolama hesabı belirttiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="bde7b-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="bde7b-175">**AccountName** ve **AccountKey** değerleri depolama hesabı panosundaki erişim anahtarlarını Yönet altında Azure portalında bulundu.</span><span class="sxs-lookup"><span data-stu-id="bde7b-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="bde7b-176">Bağlantı dizesi için Protokolü olmalıdır **https**.</span><span class="sxs-lookup"><span data-stu-id="bde7b-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="bde7b-177">Güncelleştirilmiş tanılama yapılandırması bulut hizmetinize uygulanır ve Azure depolama için tanılama yazıyor sonra daha sonra günlük analizi yapılandırmaya hazırsınız demektir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="bde7b-178">Azure depolama biriminden günlükleri toplamak için Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="bde7b-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="bde7b-179">Aşağıdaki Azure Hizmetleri için günlükleri toplamak için günlük analizi yapılandırmak için Azure portalını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bde7b-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="bde7b-180">Service Fabric kümeleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-180">Service Fabric clusters</span></span>
* <span data-ttu-id="bde7b-181">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="bde7b-181">Virtual Machines</span></span>
* <span data-ttu-id="bde7b-182">Web/çalışan rolleri</span><span class="sxs-lookup"><span data-stu-id="bde7b-182">Web/Worker Roles</span></span>

<span data-ttu-id="bde7b-183">Azure portalında günlük analizi çalışma alanına gidin ve aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bde7b-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="bde7b-184">Tıklatın *depolama hesapları günlükleri*</span><span class="sxs-lookup"><span data-stu-id="bde7b-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="bde7b-185">Tıklatın *Ekle* görevi</span><span class="sxs-lookup"><span data-stu-id="bde7b-185">Click the *Add* task</span></span>
3. <span data-ttu-id="bde7b-186">Tanılama günlükleri içeren depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="bde7b-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="bde7b-187">Bu hesap, Klasik depolama hesabı veya bir Azure Resource Manager depolama hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bde7b-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="bde7b-188">Günlüklerini toplamak istediğiniz veri türünü seçin</span><span class="sxs-lookup"><span data-stu-id="bde7b-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="bde7b-189">IIS günlüklerini seçimlerdir; Olayları; Syslog (Linux); ETW günlükleri; Hizmeti yapı olayları</span><span class="sxs-lookup"><span data-stu-id="bde7b-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="bde7b-190">Kaynak için değer veri türüne göre otomatik olarak doldurulur ve değiştirilemez</span><span class="sxs-lookup"><span data-stu-id="bde7b-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="bde7b-191">Yapılandırmayı kaydetmek için Tamam'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="bde7b-191">Click OK to save the configuration</span></span>

<span data-ttu-id="bde7b-192">Ek depolama hesapları ve toplamak için günlük analizi istediğiniz veri türleri için 2-6 adımlarını yineleyin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="bde7b-193">Yaklaşık 30 dakika içinde günlük analizi depolama hesabında verileri görmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="bde7b-194">Yalnızca yapılandırma uygulandıktan sonra depolama alanına yazılır veri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="bde7b-195">Günlük analizi depolama hesabından önceden mevcut verileri okuyamadı.</span><span class="sxs-lookup"><span data-stu-id="bde7b-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="bde7b-196">Portal kaynağı depolama hesabında yok veya yeni veriler yazılır doğrulamaz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="bde7b-197">Bir sanal makinede Azure tanılamayı etkinleştirin koleksiyonu PowerShell kullanarak olay günlüğünü ve IIS günlüğü için</span><span class="sxs-lookup"><span data-stu-id="bde7b-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="bde7b-198">İçindeki adımları kullanın [Azure tanılama dizini oluşturmak için günlük analizi yapılandırma](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) tablo depolama alanına yazılır Azure tanılama okuma için PowerShell kullanma.</span><span class="sxs-lookup"><span data-stu-id="bde7b-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="bde7b-199">Azure PowerShell kullanarak Azure depolama alanına yazılır olayları daha kesin olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="bde7b-200">Daha fazla bilgi için bkz: [etkinleştirme tanılama Azure Virtual Machines'de](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="bde7b-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="bde7b-201">Etkinleştirme ve aşağıdaki PowerShell Betiği kullanılarak Azure tanılama güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="bde7b-202">Bu komut dosyasını bir özel günlük kaydı yapılandırmasıyla de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bde7b-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="bde7b-203">Depolama hesabı, hizmet adı ve sanal makine adı ayarlamak için komut dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bde7b-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="bde7b-204">Komut dosyası Klasik sanal makineleri için cmdlet'leri kullanır.</span><span class="sxs-lookup"><span data-stu-id="bde7b-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="bde7b-205">Aşağıdaki betik örneğinde gözden geçirin, kopyalayın, gerektiği şekilde değiştirin, örnek bir PowerShell komut dosyası olarak kaydetmek ve sonra komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bde7b-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

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
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="bde7b-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bde7b-206">Next steps</span></span>
* <span data-ttu-id="bde7b-207">[Günlük ve Azure Hizmetleri için ölçümleri toplamak](log-analytics-azure-storage.md) desteklenen Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="bde7b-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="bde7b-208">[Çözümlerle](log-analytics-add-solutions.md) verileri bir anlayış sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="bde7b-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="bde7b-209">[Arama sorguları kullanmak](log-analytics-log-searches.md) verileri çözümlemek için.</span><span class="sxs-lookup"><span data-stu-id="bde7b-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
