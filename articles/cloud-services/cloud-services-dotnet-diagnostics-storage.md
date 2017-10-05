---
title: "Azure depolama alanında tanılama veri deposu ve Görünüm | Microsoft Docs"
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
ms.openlocfilehash: 374cc179e13c00e439415e3df16e0c6d5ccba5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="ce894-103">Azure Storage deposu ve görünüm Tanılama verileri</span><span class="sxs-lookup"><span data-stu-id="ce894-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="ce894-104">Microsoft Azure storage öykünücüsü veya Azure depolama transfer sürece Tanılama verileri kalıcı olarak depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="ce894-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="ce894-105">Bir kez depolama biriminde, onu birkaç kullanılabilen araçlar biriyle görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="ce894-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="ce894-106">Bir depolama hesabı belirtin</span><span class="sxs-lookup"><span data-stu-id="ce894-106">Specify a storage account</span></span>
<span data-ttu-id="ce894-107">ServiceConfiguration.cscfg dosyasında kullanmak istediğiniz depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ce894-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="ce894-108">Hesap bilgileri, bir bağlantı dizesi bir yapılandırma ayarı olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="ce894-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="ce894-109">Aşağıdaki örnek, Visual Studio'da yeni bir bulut hizmeti projesi için oluşturulan varsayılan bağlantı dizesini gösterir:</span><span class="sxs-lookup"><span data-stu-id="ce894-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="ce894-110">Bir Azure depolama hesabı için hesap bilgilerini sağlamak için bu bağlantı dizesi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce894-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="ce894-111">Toplanacak tanılama veri türüne bağlı olarak, Azure tanılama Blob hizmeti veya tablo hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="ce894-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="ce894-112">Aşağıdaki tabloda, kalıcı veri kaynaklarını ve bunların biçimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ce894-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="ce894-113">Veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="ce894-113">Data source</span></span> | <span data-ttu-id="ce894-114">Depolama biçimi</span><span class="sxs-lookup"><span data-stu-id="ce894-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="ce894-115">Azure günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce894-115">Azure logs</span></span> |<span data-ttu-id="ce894-116">Tablo</span><span class="sxs-lookup"><span data-stu-id="ce894-116">Table</span></span> |
| <span data-ttu-id="ce894-117">IIS 7.0 günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce894-117">IIS 7.0 logs</span></span> |<span data-ttu-id="ce894-118">Blob</span><span class="sxs-lookup"><span data-stu-id="ce894-118">Blob</span></span> |
| <span data-ttu-id="ce894-119">Azure tanılama altyapı günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce894-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="ce894-120">Tablo</span><span class="sxs-lookup"><span data-stu-id="ce894-120">Table</span></span> |
| <span data-ttu-id="ce894-121">Başarısız istek izleme günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce894-121">Failed Request Trace logs</span></span> |<span data-ttu-id="ce894-122">Blob</span><span class="sxs-lookup"><span data-stu-id="ce894-122">Blob</span></span> |
| <span data-ttu-id="ce894-123">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce894-123">Windows Event logs</span></span> |<span data-ttu-id="ce894-124">Tablo</span><span class="sxs-lookup"><span data-stu-id="ce894-124">Table</span></span> |
| <span data-ttu-id="ce894-125">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="ce894-125">Performance counters</span></span> |<span data-ttu-id="ce894-126">Tablo</span><span class="sxs-lookup"><span data-stu-id="ce894-126">Table</span></span> |
| <span data-ttu-id="ce894-127">Kilitlenme bilgi dökümleri</span><span class="sxs-lookup"><span data-stu-id="ce894-127">Crash dumps</span></span> |<span data-ttu-id="ce894-128">Blob</span><span class="sxs-lookup"><span data-stu-id="ce894-128">Blob</span></span> |
| <span data-ttu-id="ce894-129">Özel hata günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce894-129">Custom error logs</span></span> |<span data-ttu-id="ce894-130">Blob</span><span class="sxs-lookup"><span data-stu-id="ce894-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="ce894-131">Tanılama veri aktarımı girişi</span><span class="sxs-lookup"><span data-stu-id="ce894-131">Transfer diagnostic data</span></span>
<span data-ttu-id="ce894-132">Tanılama veri aktarım isteği, SDK 2.5 ve daha sonra yapılandırma dosyası aracılığıyla ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="ce894-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="ce894-133">Yapılandırmada belirtilen zamanlanan aralıklarla tanılama veri aktarın.</span><span class="sxs-lookup"><span data-stu-id="ce894-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="ce894-134">SDK 2.4 ve önceki Tanılama verileri de yapılandırma dosyası aracılığıyla programlı olarak aktarmak isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="ce894-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="ce894-135">Programsal yaklaşım isteğe bağlı aktarımları yapmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce894-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce894-136">Bir Azure depolama hesabına tanılama veri aktarırken tanılama verilerini kullanan depolama alanı kaynakları için ücrete neden.</span><span class="sxs-lookup"><span data-stu-id="ce894-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="ce894-137">Tanılama verileri depola</span><span class="sxs-lookup"><span data-stu-id="ce894-137">Store diagnostic data</span></span>
<span data-ttu-id="ce894-138">Günlük verileri Blob veya tablo depolama aşağıdaki adlarla depolanır:</span><span class="sxs-lookup"><span data-stu-id="ce894-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="ce894-139">**Tabloları**</span><span class="sxs-lookup"><span data-stu-id="ce894-139">**Tables**</span></span>

* <span data-ttu-id="ce894-140">**WadLogsTable** - İzleme dinleyicisi kullanarak kod içinde yazılmış günlükleri.</span><span class="sxs-lookup"><span data-stu-id="ce894-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="ce894-141">**WADDiagnosticInfrastructureLogsTable** -Tanılama izleme ve yapılandırma değişikliklerini.</span><span class="sxs-lookup"><span data-stu-id="ce894-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="ce894-142">**WADDirectoriesTable** – tanı İzleyicisi İzleme dizinleri.</span><span class="sxs-lookup"><span data-stu-id="ce894-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="ce894-143">Bu, IIS günlüklerini içerir, IIS istek günlüklerini ve özel dizinleri başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="ce894-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="ce894-144">Blob günlük dosyasının konumunu kapsayıcı alanında belirtilen ve blob adını RelativePath alanıdır.</span><span class="sxs-lookup"><span data-stu-id="ce894-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="ce894-145">Azure sanal makinede var gibi AbsolutePath alan dosyasının adını ve konumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ce894-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="ce894-146">**WADPerformanceCountersTable** – performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="ce894-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="ce894-147">**WADWindowsEventLogsTable** – Windows olayı günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ce894-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="ce894-148">**Bloblar**</span><span class="sxs-lookup"><span data-stu-id="ce894-148">**Blobs**</span></span>

* <span data-ttu-id="ce894-149">**wad denetimi kapsayıcısı** – (yalnızca SDK 2.4 ve önceki) Azure tanılama denetimleri XML yapılandırma dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ce894-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="ce894-150">**wad IIS failedreqlogfiles** – IIS isteği başarısız oldu günlüklerdeki bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="ce894-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="ce894-151">**wad IIS logfiles** – IIS günlüklerini hakkında bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="ce894-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="ce894-152">**"özel"** – özel bir kapsayıcı dayalı tanı İzleyicisi tarafından izlenen dizinleri yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ce894-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="ce894-153">Bu blob kapsayıcısının adı WADDirectoriesTable belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ce894-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="ce894-154">Tanılama verileri görüntülemek için Araçlar</span><span class="sxs-lookup"><span data-stu-id="ce894-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="ce894-155">Depolama birimine aktarıldıktan sonra verileri görüntülemek birkaç araç bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ce894-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="ce894-156">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce894-156">For example:</span></span>

* <span data-ttu-id="ce894-157">Microsoft Visual Studio için Azure araçlarını yüklediyseniz, Visual Studio - sunucu Gezgini'nde, Azure Depolama düğümü sunucu Gezgini'nde salt okunur blob ve tablo verileri Azure depolama hesaplarından görüntülemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce894-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="ce894-158">Yerel depolama öykünücüsü hesabınızdan verileri görüntüleyebilir ve ayrıca depolama hesaplarından Azure için oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="ce894-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="ce894-159">Daha fazla bilgi için bkz: [gözatma ve Sunucu Gezgini ile depolama kaynaklarını yönetme](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="ce894-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="ce894-160">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) , Windows, OSX ve Linux Azure Storage ile kolayca çalışmanızı sağlayan bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ce894-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="ce894-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) , görüntülemek, indirin ve Azure üzerinde çalışan uygulamalar tarafından toplanan tanılama verilerini yönetmenize olanak sağlayan Azure tanılama Manager içerir.</span><span class="sxs-lookup"><span data-stu-id="ce894-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce894-162">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ce894-162">Next Steps</span></span>
[<span data-ttu-id="ce894-163">Bulut Hizmetleri uygulaması Azure Tanılama ile akışında izleme</span><span class="sxs-lookup"><span data-stu-id="ce894-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](cloud-services-dotnet-diagnostics-trace-flow.md)

