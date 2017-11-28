---
title: "aaaStore ve görünüm tanılama verilerini Azure storage'da | Microsoft Docs"
description: "Azure Tanılama verileri Azure depolama alanına almak ve görüntüleme"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="76512-103">Azure Storage deposu ve görünüm Tanılama verileri</span><span class="sxs-lookup"><span data-stu-id="76512-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="76512-104">Toohello Microsoft Azure storage öykünücüsü veya tooAzure depolama aktarım sürece Tanılama verileri kalıcı olarak depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="76512-104">Diagnostic data is not permanently stored unless you transfer it toohello Microsoft Azure storage emulator or tooAzure storage.</span></span> <span data-ttu-id="76512-105">Bir kez depolama biriminde, onu birkaç kullanılabilen araçlar biriyle görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="76512-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="76512-106">Bir depolama hesabı belirtin</span><span class="sxs-lookup"><span data-stu-id="76512-106">Specify a storage account</span></span>
<span data-ttu-id="76512-107">Merhaba ServiceConfiguration.cscfg dosyasında toouse istediğiniz hello depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="76512-107">You specify hello storage account that you want toouse in hello ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="76512-108">Merhaba hesap bilgileri, bir bağlantı dizesi bir yapılandırma ayarı olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="76512-108">hello account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="76512-109">Merhaba aşağıdaki örnek Visual Studio'da yeni bir bulut hizmeti projesi için oluşturulan hello varsayılan bağlantı dizesini gösterir:</span><span class="sxs-lookup"><span data-stu-id="76512-109">hello following example shows hello default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="76512-110">Bir Azure depolama hesabı için bu bağlantı dizesi tooprovide hesap bilgilerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76512-110">You can change this connection string tooprovide account information for an Azure storage account.</span></span>

<span data-ttu-id="76512-111">Toplanacak tanılama veri Hello türüne bağlı olarak, Azure tanılama hello Blob hizmeti veya hello tablo hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="76512-111">Depending on hello type of diagnostic data that is being collected, Azure Diagnostics uses either hello Blob service or hello Table service.</span></span> <span data-ttu-id="76512-112">Merhaba aşağıdaki tabloda kalıcı hello veri kaynaklarını ve bunların biçimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="76512-112">hello following table shows hello data sources that are persisted and their format.</span></span>

| <span data-ttu-id="76512-113">Veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="76512-113">Data source</span></span> | <span data-ttu-id="76512-114">Depolama biçimi</span><span class="sxs-lookup"><span data-stu-id="76512-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="76512-115">Azure günlükleri</span><span class="sxs-lookup"><span data-stu-id="76512-115">Azure logs</span></span> |<span data-ttu-id="76512-116">Tablo</span><span class="sxs-lookup"><span data-stu-id="76512-116">Table</span></span> |
| <span data-ttu-id="76512-117">IIS 7.0 günlükleri</span><span class="sxs-lookup"><span data-stu-id="76512-117">IIS 7.0 logs</span></span> |<span data-ttu-id="76512-118">Blob</span><span class="sxs-lookup"><span data-stu-id="76512-118">Blob</span></span> |
| <span data-ttu-id="76512-119">Azure tanılama altyapı günlükleri</span><span class="sxs-lookup"><span data-stu-id="76512-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="76512-120">Tablo</span><span class="sxs-lookup"><span data-stu-id="76512-120">Table</span></span> |
| <span data-ttu-id="76512-121">Başarısız istek izleme günlükleri</span><span class="sxs-lookup"><span data-stu-id="76512-121">Failed Request Trace logs</span></span> |<span data-ttu-id="76512-122">Blob</span><span class="sxs-lookup"><span data-stu-id="76512-122">Blob</span></span> |
| <span data-ttu-id="76512-123">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="76512-123">Windows Event logs</span></span> |<span data-ttu-id="76512-124">Tablo</span><span class="sxs-lookup"><span data-stu-id="76512-124">Table</span></span> |
| <span data-ttu-id="76512-125">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="76512-125">Performance counters</span></span> |<span data-ttu-id="76512-126">Tablo</span><span class="sxs-lookup"><span data-stu-id="76512-126">Table</span></span> |
| <span data-ttu-id="76512-127">Kilitlenme bilgi dökümleri</span><span class="sxs-lookup"><span data-stu-id="76512-127">Crash dumps</span></span> |<span data-ttu-id="76512-128">Blob</span><span class="sxs-lookup"><span data-stu-id="76512-128">Blob</span></span> |
| <span data-ttu-id="76512-129">Özel hata günlükleri</span><span class="sxs-lookup"><span data-stu-id="76512-129">Custom error logs</span></span> |<span data-ttu-id="76512-130">Blob</span><span class="sxs-lookup"><span data-stu-id="76512-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="76512-131">Tanılama veri aktarımı girişi</span><span class="sxs-lookup"><span data-stu-id="76512-131">Transfer diagnostic data</span></span>
<span data-ttu-id="76512-132">SDK 2.5 ve sonrası hello istek tootransfer Tanılama verileri hello yapılandırma dosyası aracılığıyla ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="76512-132">For SDK 2.5 and later, hello request tootransfer diagnostic data can occur through hello configuration file.</span></span> <span data-ttu-id="76512-133">Merhaba yapılandırmasında belirtilen zamanlanan aralıklarla tanılama veri aktarın.</span><span class="sxs-lookup"><span data-stu-id="76512-133">You can transfer diagnostic data at scheduled intervals as specified in hello configuration.</span></span>

<span data-ttu-id="76512-134">SDK 2.4 ve önceki tootransfer hello tanılama verilerini de hello yapılandırma dosyası aracılığıyla programlı olarak isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="76512-134">For SDK 2.4 and previous you can request tootransfer hello diagnostic data through hello configuration file as well as programmatically.</span></span> <span data-ttu-id="76512-135">Merhaba programlı yaklaşım da toodo isteğe bağlı aktarımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="76512-135">hello programmatic approach also allows you toodo on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76512-136">Tanılama veri tooan Azure depolama hesabı aktardığınızda, tanılama verilerini kullanan hello depolama alanı kaynakları için ücrete neden.</span><span class="sxs-lookup"><span data-stu-id="76512-136">When you transfer diagnostic data tooan Azure storage account, you incur costs for hello storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="76512-137">Tanılama verileri depola</span><span class="sxs-lookup"><span data-stu-id="76512-137">Store diagnostic data</span></span>
<span data-ttu-id="76512-138">Günlük verileri adlarından hello ile Blob veya tablo depolama alanına depolanır:</span><span class="sxs-lookup"><span data-stu-id="76512-138">Log data is stored in either Blob or Table storage with hello following names:</span></span>

<span data-ttu-id="76512-139">**Tabloları**</span><span class="sxs-lookup"><span data-stu-id="76512-139">**Tables**</span></span>

* <span data-ttu-id="76512-140">**WadLogsTable** - hello İzleme dinleyicisi kullanarak kod içinde yazılmış günlükleri.</span><span class="sxs-lookup"><span data-stu-id="76512-140">**WadLogsTable** - Logs written in code using hello trace listener.</span></span>
* <span data-ttu-id="76512-141">**WADDiagnosticInfrastructureLogsTable** -Tanılama izleme ve yapılandırma değişikliklerini.</span><span class="sxs-lookup"><span data-stu-id="76512-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="76512-142">**WADDirectoriesTable** – izleme bu hello tanı İzleyicisi dizinleri.</span><span class="sxs-lookup"><span data-stu-id="76512-142">**WADDirectoriesTable** – Directories that hello diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="76512-143">Bu, IIS günlüklerini içerir, IIS istek günlüklerini ve özel dizinleri başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="76512-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="76512-144">Merhaba hello blob günlük dosyasının konumunu hello kapsayıcı alanında belirtilen ve hello hello blob hello RelativePath alanında adıdır.</span><span class="sxs-lookup"><span data-stu-id="76512-144">hello location of hello blob log file is specified in hello Container field and hello name of hello blob is in hello RelativePath field.</span></span>  <span data-ttu-id="76512-145">hello Azure sanal makinesi üzerinde var gibi hello AbsolutePath alan hello konumunu ve hello dosya adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="76512-145">hello AbsolutePath field indicates hello location and name of hello file as it existed on hello Azure virtual machine.</span></span>
* <span data-ttu-id="76512-146">**WADPerformanceCountersTable** – performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="76512-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="76512-147">**WADWindowsEventLogsTable** – Windows olayı günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="76512-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="76512-148">**Bloblar**</span><span class="sxs-lookup"><span data-stu-id="76512-148">**Blobs**</span></span>

* <span data-ttu-id="76512-149">**wad denetimi kapsayıcısı** – (yalnızca SDK 2.4 ve önceki) hello Azure tanılama denetimleri hello XML yapılandırma dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="76512-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains hello XML configuration files that controls hello Azure diagnostics .</span></span>
* <span data-ttu-id="76512-150">**wad IIS failedreqlogfiles** – IIS isteği başarısız oldu günlüklerdeki bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="76512-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="76512-151">**wad IIS logfiles** – IIS günlüklerini hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="76512-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="76512-152">**"özel"** – özel bir kapsayıcı dayalı hello tanı İzleyicisi tarafından izlenen dizinleri yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="76512-152">**"custom"** – A custom container based on configuring directories that are monitored by hello diagnostic monitor.</span></span>  <span data-ttu-id="76512-153">Bu blob kapsayıcısının Hello adı WADDirectoriesTable belirtilir.</span><span class="sxs-lookup"><span data-stu-id="76512-153">hello name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-tooview-diagnostic-data"></a><span data-ttu-id="76512-154">Araçlar tooview Tanılama verileri</span><span class="sxs-lookup"><span data-stu-id="76512-154">Tools tooview diagnostic data</span></span>
<span data-ttu-id="76512-155">Aktarılan toostorage tamamlandıktan sonra birkaç kullanılabilir tooview hello veri araçlardır.</span><span class="sxs-lookup"><span data-stu-id="76512-155">Several tools are available tooview hello data after it is transferred toostorage.</span></span> <span data-ttu-id="76512-156">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76512-156">For example:</span></span>

* <span data-ttu-id="76512-157">Visual Studio - server Explorer'da hello Azure Araçları için Microsoft Visual Studio, yüklü değilse, Azure depolama hesaplarından Sunucu Gezgini tooview salt okunur blob ve tablo verilerinizi hello Azure Storage düğümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76512-157">Server Explorer in Visual Studio - If you have installed hello Azure Tools for Microsoft Visual Studio, you can use hello Azure Storage node in Server Explorer tooview read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="76512-158">Yerel depolama öykünücüsü hesabınızdan verileri görüntüleyebilir ve ayrıca depolama hesaplarından Azure için oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="76512-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="76512-159">Daha fazla bilgi için bkz: [gözatma ve Sunucu Gezgini ile depolama kaynaklarını yönetme](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="76512-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="76512-160">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, OSX ve Linux Azure Storage verilerle tooeasily çalışma sağlayan bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="76512-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="76512-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) tooview, sağlayan Azure tanılama Manager içerir indirmek ve Azure üzerinde çalışan hello uygulamalar tarafından toplanan hello Tanılama verileri yönetmek.</span><span class="sxs-lookup"><span data-stu-id="76512-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you tooview, download and manage hello diagnostics data collected by hello applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76512-162">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="76512-162">Next Steps</span></span>
[<span data-ttu-id="76512-163">Bulut Hizmetleri uygulaması Azure Tanılama ile Merhaba akışı izleme</span><span class="sxs-lookup"><span data-stu-id="76512-163">Trace hello flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

