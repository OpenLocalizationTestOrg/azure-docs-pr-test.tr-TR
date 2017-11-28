---
title: "aaaEnabling depolama ölçümlerini hello Azure portalı | Microsoft Docs"
description: "Blob, kuyruk, tablo ve Dosya Hizmetleri tooenable depolama ölçümlerini nasıl hello"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0407adfc-2a41-4126-922d-b76e90b74563
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/14/2017
ms.author: robinsh
ms.openlocfilehash: 4e705ecbdd083c77f8ceff87214d7221495d2d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="9e8b3-103">Azure Storage ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9e8b3-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="9e8b3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9e8b3-104">Overview</span></span>
<span data-ttu-id="9e8b3-105">Depolama ölçümleri, yeni bir depolama hesabı oluşturduğunuzda, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="9e8b3-106">Merhaba izlemeyi yapılandırmadan [Azure portal](https://portal.azure.com) veya Windows PowerShell veya program aracılığıyla hello depolama istemci kitaplıklarından birini aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-106">You can configure monitoring via hello [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of hello storage client libraries.</span></span>

<span data-ttu-id="9e8b3-107">Merhaba ölçüm verileri için bekletme süresi yapılandırabilirsiniz: Bu dönem için ne kadar süreyle hello depolama hizmeti hello ölçümleri ve sizin hello için boşluk gerekli toostore ücretleri tutar belirler bunları.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-107">You can configure a retention period for hello metrics data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="9e8b3-108">Genellikle, daha kısa bir bekletme dönemi saatlik ölçümleri daha dakika ölçümünün hello önemli ek boşluk dakika ölçümlerini gerekli nedeniyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="9e8b3-109">Yeterli zaman tooanalyze hello veriniz varsa ve çevrimdışı analiz ve raporlama amacıyla tookeep istediğiniz ölçümleri karşıdan şekilde bir bekletme dönemi seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="9e8b3-110">Ayrıca ölçümleri veri depolama hesabınızdan indirme için Fatura edilecek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a><span data-ttu-id="9e8b3-111">Azure portal kullanarak tooenable ölçümleri nasıl hello</span><span class="sxs-lookup"><span data-stu-id="9e8b3-111">How tooenable metrics using hello Azure portal</span></span>
<span data-ttu-id="9e8b3-112">Bu adımları tooenable ölçümlerini hello izleyin [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="9e8b3-112">Follow these steps tooenable metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="9e8b3-113">Tooyour depolama hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-113">Navigate tooyour storage account.</span></span>
1. <span data-ttu-id="9e8b3-114">Seçin **tanılama** hello üzerinde **menü** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="9e8b3-114">Select **Diagnostics** on hello **Menu** blade</span></span>
1. <span data-ttu-id="9e8b3-115">Emin **durum** çok ayarlanır**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-115">Ensure that **Status** is set too**On**.</span></span>
1. <span data-ttu-id="9e8b3-116">Merhaba Hizmetleri için Select hello ölçümleri toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-116">Select hello metrics for hello services you wish toomonitor.</span></span>
1. <span data-ttu-id="9e8b3-117">Bir bekletme ilkesi tooindicate belirtin ne kadar süreyle tooretain ölçümleri ve günlük verileri.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-117">Specify a retention policy tooindicate how long tooretain metrics and log data.</span></span>
1. <span data-ttu-id="9e8b3-118">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-118">Select **Save**.</span></span>

<span data-ttu-id="9e8b3-119">Bu hello Not [Azure portal](https://portal.azure.com) şu anda tooconfigure minute ölçümleri; depolama hesabınızdaki etkinleştirmez PowerShell kullanarak dakika ölçümlerini etkinleştirmeniz gerekir veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-119">Note that hello [Azure portal](https://portal.azure.com) does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-metrics-using-powershell"></a><span data-ttu-id="9e8b3-120">Nasıl tooenable ölçümleri PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="9e8b3-120">How tooenable metrics using PowerShell</span></span>
<span data-ttu-id="9e8b3-121">PowerShell, LocalMachine tooconfigure Storage ölçümleri depolama hesabınızdaki hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello geçerli ayarları kullanarak ve cmdlet hello Set-AzureStorageServiceMetricsProperty toochange hello geçerli ayarları.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="9e8b3-122">Depolama Ölçümleri kontrol hello cmdlet'leri şu parametreler hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="9e8b3-123">MetricsType: olası saat ve dakika değerleri.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="9e8b3-124">ServiceType: Blob, kuyruk ve tablo olası değerler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="9e8b3-125">MetricsLevel: olası değerler, hizmeti ve ServiceAndApi yok.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="9e8b3-126">Örneğin, hello aşağıdaki komutu hello hello bekletme süresi ile varsayılan depolama hesabınızdaki Blob hizmeti için ölçümleri toofive güne ayarlayabilir dakika üzerinde geçer:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-126">For example, hello following command switches on minute metrics for hello Blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="9e8b3-127">Merhaba aşağıdaki komutu hello geçerli saatlik ölçümleri düzeyi ve saklama gün boyunca hello blob hizmeti varsayılan depolama hesabınızdaki alır:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="9e8b3-128">Nasıl toouse tooconfigure hello Azure PowerShell cmdlet'leri toowork Azure aboneliğinizle ve nasıl tooselect hello varsayılan depolama hesabı hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e8b3-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="9e8b3-129">Nasıl tooenable Storage ölçümleri programlamayla</span><span class="sxs-lookup"><span data-stu-id="9e8b3-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="9e8b3-130">C# kod parçacığında aşağıdaki hello nasıl tooenable ölçümleri ve günlük hello Blob hizmeti kullandığınız için .NET için depolama istemci kitaplığı hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="9e8b3-131">Depolama ölçümleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9e8b3-131">Viewing Storage metrics</span></span>
<span data-ttu-id="9e8b3-132">Depolama hesabınız Storage Analytics ölçümleri toomonitor yapılandırdıktan sonra depolama çözümlemeleri hello ölçümleri depolama hesabındaki iyi bilinen tablo kümesini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-132">After you configure Storage Analytics metrics toomonitor your storage account, Storage Analytics records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="9e8b3-133">Grafikler tooview saatlik ölçümleri hello yapılandırabilirsiniz [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="9e8b3-133">You can configure charts tooview hourly metrics in hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="9e8b3-134">Merhaba tooyour depolama hesabında gidin [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e8b3-134">Navigate tooyour storage account in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="9e8b3-135">Seçin **ölçümleri** hello içinde **menü** dikey penceresinde hello için hizmet, ölçümleri tooview istiyor.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-135">Select **Metrics** in hello **Menu** blade for hello service whose metrics you want tooview.</span></span>
1. <span data-ttu-id="9e8b3-136">Seçin **Düzenle** hello grafikte tooconfigure istiyor.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-136">Select **Edit** on hello chart you want tooconfigure.</span></span>
1. <span data-ttu-id="9e8b3-137">Merhaba, **grafiği Düzenle** dikey penceresinde, select hello **zaman aralığı**, **grafik türü**ve görüntülenmesini istediğiniz hello grafikte hello ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-137">In hello **Edit Chart** blade, select hello **Time Range**, **Chart type**, and hello metrics you want displayed in hello chart.</span></span>
1. <span data-ttu-id="9e8b3-138">**Tamam**’ı seçin</span><span class="sxs-lookup"><span data-stu-id="9e8b3-138">Select **OK**</span></span>

<span data-ttu-id="9e8b3-139">Toodownload hello ölçümleri istiyorsanız, uzun vadeli depolama veya tooanalyze için bunları yerel olarak yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need to:</span></span>

* <span data-ttu-id="9e8b3-140">Bu tabloları kullanan bir araç kullanın ve tooview izin vermek ve bunları yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-140">Use a tool that is aware of these tables and will allow you tooview and download them.</span></span>
* <span data-ttu-id="9e8b3-141">Özel bir uygulama veya betik tooread yazma ve hello tabloları depolayın.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-141">Write a custom application or script tooread and store hello tables.</span></span>

<span data-ttu-id="9e8b3-142">Çok sayıda üçüncü taraf araçları depolama gözatma bu tabloları farkında olduğundan ve tooview etkinleştirmek bunları doğrudan.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly.</span></span>
<span data-ttu-id="9e8b3-143">Lütfen bakın [Azure Storage istemci araçları](storage-explorers.md) kullanılabilen araçlar listesi.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="9e8b3-144">Merhaba 0.8.0 sürümü ile başlayarak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/), görüntüleyebilir ve hello analytics ölçümleri tabloları indirin.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-144">Starting with version 0.8.0 of hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download hello analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="9e8b3-145">Sipariş tooaccess hello analizleri, depolama hesabınızı tüm hello tabloları listelerseniz hello analytics tabloları görünmez tablolar bir program aracılığıyla, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-145">In order tooaccess hello analytics tables programmatically, do note that hello analytics tables do not appear if you list all hello tables in your storage account.</span></span> <span data-ttu-id="9e8b3-146">Doğrudan adıyla erişmesine veya hello kullan [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello .NET istemci kitaplığı tooquery hello tablo adları.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-146">You can either access them directly by name, or use hello [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in hello .NET client library tooquery hello table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="9e8b3-147">Saatlik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="9e8b3-147">Hourly metrics</span></span>
* <span data-ttu-id="9e8b3-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="9e8b3-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="9e8b3-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="9e8b3-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="9e8b3-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="9e8b3-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="9e8b3-151">Dakika ölçümleri</span><span class="sxs-lookup"><span data-stu-id="9e8b3-151">Minute metrics</span></span>
* <span data-ttu-id="9e8b3-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="9e8b3-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="9e8b3-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="9e8b3-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="9e8b3-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="9e8b3-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="9e8b3-155">Kapasite</span><span class="sxs-lookup"><span data-stu-id="9e8b3-155">Capacity</span></span>
* <span data-ttu-id="9e8b3-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="9e8b3-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="9e8b3-157">Bu tablolar hello şemaları tam ayrıntılarını bulabilirsiniz [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e8b3-157">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="9e8b3-158">altındaki Hello örnek satırları yalnızca bir sütun alt kümesi hello kullanılabilir Göster, ancak bu ölçümleri Storage ölçümleri kaydeder hello şekilde önemli özelliklerinden bazıları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-158">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="9e8b3-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="9e8b3-159">PartitionKey</span></span> | <span data-ttu-id="9e8b3-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="9e8b3-160">RowKey</span></span> | <span data-ttu-id="9e8b3-161">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="9e8b3-161">Timestamp</span></span> | <span data-ttu-id="9e8b3-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="9e8b3-162">TotalRequests</span></span> | <span data-ttu-id="9e8b3-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="9e8b3-163">TotalBillableRequests</span></span> | <span data-ttu-id="9e8b3-164">Totalıngress</span><span class="sxs-lookup"><span data-stu-id="9e8b3-164">TotalIngress</span></span> | <span data-ttu-id="9e8b3-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="9e8b3-165">TotalEgress</span></span> | <span data-ttu-id="9e8b3-166">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="9e8b3-166">Availability</span></span> | <span data-ttu-id="9e8b3-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="9e8b3-167">AverageE2ELatency</span></span> | <span data-ttu-id="9e8b3-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="9e8b3-168">AverageServerLatency</span></span> | <span data-ttu-id="9e8b3-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="9e8b3-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9e8b3-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-170">20140522T1100</span></span> |<span data-ttu-id="9e8b3-171">Kullanıcı; Tüm</span><span class="sxs-lookup"><span data-stu-id="9e8b3-171">user;All</span></span> |<span data-ttu-id="9e8b3-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9e8b3-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9e8b3-173">7</span><span class="sxs-lookup"><span data-stu-id="9e8b3-173">7</span></span> |<span data-ttu-id="9e8b3-174">7</span><span class="sxs-lookup"><span data-stu-id="9e8b3-174">7</span></span> |<span data-ttu-id="9e8b3-175">4003</span><span class="sxs-lookup"><span data-stu-id="9e8b3-175">4003</span></span> |<span data-ttu-id="9e8b3-176">46801</span><span class="sxs-lookup"><span data-stu-id="9e8b3-176">46801</span></span> |<span data-ttu-id="9e8b3-177">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-177">100</span></span> |<span data-ttu-id="9e8b3-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="9e8b3-178">104.4286</span></span> |<span data-ttu-id="9e8b3-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="9e8b3-179">6.857143</span></span> |<span data-ttu-id="9e8b3-180">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-180">100</span></span> |
| <span data-ttu-id="9e8b3-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-181">20140522T1100</span></span> |<span data-ttu-id="9e8b3-182">Kullanıcı; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="9e8b3-182">user;QueryEntities</span></span> |<span data-ttu-id="9e8b3-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="9e8b3-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="9e8b3-184">5</span><span class="sxs-lookup"><span data-stu-id="9e8b3-184">5</span></span> |<span data-ttu-id="9e8b3-185">5</span><span class="sxs-lookup"><span data-stu-id="9e8b3-185">5</span></span> |<span data-ttu-id="9e8b3-186">2694</span><span class="sxs-lookup"><span data-stu-id="9e8b3-186">2694</span></span> |<span data-ttu-id="9e8b3-187">45951</span><span class="sxs-lookup"><span data-stu-id="9e8b3-187">45951</span></span> |<span data-ttu-id="9e8b3-188">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-188">100</span></span> |<span data-ttu-id="9e8b3-189">143.8</span><span class="sxs-lookup"><span data-stu-id="9e8b3-189">143.8</span></span> |<span data-ttu-id="9e8b3-190">7.8</span><span class="sxs-lookup"><span data-stu-id="9e8b3-190">7.8</span></span> |<span data-ttu-id="9e8b3-191">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-191">100</span></span> |
| <span data-ttu-id="9e8b3-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-192">20140522T1100</span></span> |<span data-ttu-id="9e8b3-193">Kullanıcı; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="9e8b3-193">user;QueryEntity</span></span> |<span data-ttu-id="9e8b3-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9e8b3-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9e8b3-195">1</span><span class="sxs-lookup"><span data-stu-id="9e8b3-195">1</span></span> |<span data-ttu-id="9e8b3-196">1</span><span class="sxs-lookup"><span data-stu-id="9e8b3-196">1</span></span> |<span data-ttu-id="9e8b3-197">538</span><span class="sxs-lookup"><span data-stu-id="9e8b3-197">538</span></span> |<span data-ttu-id="9e8b3-198">633</span><span class="sxs-lookup"><span data-stu-id="9e8b3-198">633</span></span> |<span data-ttu-id="9e8b3-199">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-199">100</span></span> |<span data-ttu-id="9e8b3-200">3</span><span class="sxs-lookup"><span data-stu-id="9e8b3-200">3</span></span> |<span data-ttu-id="9e8b3-201">3</span><span class="sxs-lookup"><span data-stu-id="9e8b3-201">3</span></span> |<span data-ttu-id="9e8b3-202">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-202">100</span></span> |
| <span data-ttu-id="9e8b3-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-203">20140522T1100</span></span> |<span data-ttu-id="9e8b3-204">Kullanıcı; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="9e8b3-204">user;UpdateEntity</span></span> |<span data-ttu-id="9e8b3-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="9e8b3-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="9e8b3-206">1</span><span class="sxs-lookup"><span data-stu-id="9e8b3-206">1</span></span> |<span data-ttu-id="9e8b3-207">1</span><span class="sxs-lookup"><span data-stu-id="9e8b3-207">1</span></span> |<span data-ttu-id="9e8b3-208">771</span><span class="sxs-lookup"><span data-stu-id="9e8b3-208">771</span></span> |<span data-ttu-id="9e8b3-209">217</span><span class="sxs-lookup"><span data-stu-id="9e8b3-209">217</span></span> |<span data-ttu-id="9e8b3-210">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-210">100</span></span> |<span data-ttu-id="9e8b3-211">9</span><span class="sxs-lookup"><span data-stu-id="9e8b3-211">9</span></span> |<span data-ttu-id="9e8b3-212">6</span><span class="sxs-lookup"><span data-stu-id="9e8b3-212">6</span></span> |<span data-ttu-id="9e8b3-213">100</span><span class="sxs-lookup"><span data-stu-id="9e8b3-213">100</span></span> |

<span data-ttu-id="9e8b3-214">Bu örnek dakika ölçümleri verileri dakika çözünürlükte hello zaman hello bölüm anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-214">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="9e8b3-215">Hello satır anahtarını hello hello satır için depolanan bilgi türünü tanımlayan ve bu bilgileri, hello erişim türünü ve hello istek türü iki parça oluşur:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-215">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="9e8b3-216">Merhaba erişim kullanıcı veya sistem burada kullanıcı tooall kullanıcı istekleri toohello depolama hizmeti anlamına gelir ve sistem depolama analizi tarafından yapılan toorequests başvuruyor türüdür.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-216">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="9e8b3-217">Merhaba istek türü, tüm durumda bir Özet satırı olan veya QueryEntity veya UpdateEntity gibi belirli API hello tanımlayan olur.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-217">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="9e8b3-218">Merhaba örnek verileri yukarıda tüm hello gösterir (11: 00'da başlayarak) tek bir dakikadır QueryEntities istekleri bunu hello sayısını kaydeder artı hello QueryEntity istek sayısı artı UpdateEntity istek hello sayısı toplam gösterilen hello olduğu tooseven Yukarı Ekle Merhaba kullanıcı: tüm satır.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-218">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="9e8b3-219">Hesaplayarak hello ortalama uçtan uca gecikmesine 104.4286 hello kullanıcı: tüm satır benzer şekilde, türetilemeyeceğini ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-219">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="9e8b3-220">Ölçümleri uyarıları</span><span class="sxs-lookup"><span data-stu-id="9e8b3-220">Metrics alerts</span></span>
<span data-ttu-id="9e8b3-221">Hello uyarıları ayarlama düşünmelisiniz [Azure portal](https://portal.azure.com) şekilde depolama ölçümleri otomatik olarak depolama hizmetlerinizi hello davranışlarındaki önemli değişiklikler hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-221">You should consider setting up alerts in hello [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in hello behavior of your storage services.</span></span> <span data-ttu-id="9e8b3-222">Bu ölçüm verilerini bir sınırlandırılmış biçimde bir Depolama Gezgini aracı toodownload kullanırsanız, Microsoft Excel tooanalyze hello verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-222">If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="9e8b3-223">Bkz: [Azure Storage istemci araçları](storage-explorers.md) kullanılabilir Depolama Gezgini araçları listesi.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="9e8b3-224">Uyarıları hello yapılandırabilirsiniz **uyarı kuralları** dikey penceresinde, erişilebilir altında **izleme** hello depolama hesabı menü dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-224">You can configure alerts in hello **Alert rules** blade, accessible under **Monitoring** in hello Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e8b3-225">Bir depolama olayı ve saat veya dakika ölçüm verilerini karşılık gelen hello zaman kaydedilir arasında bir gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-225">There may be a delay between a storage event and when hello corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="9e8b3-226">Dakika ölçümleri Hello durumda birkaç dakika veri aynı anda yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-226">In hello case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="9e8b3-227">Bu tootransactions hello harekete hello için geçerli dakikada toplanan önceki dakika neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-227">This can lead tootransactions from earlier minutes being aggregated into hello transaction for hello current minute.</span></span> <span data-ttu-id="9e8b3-228">Bu gerçekleştiğinde, hizmet hello tüm kullanılabilir ölçüm verilerini olmayabilir hello uyarı beklenmedik bir şekilde tetikleme tooalerts yol açabilir uyarı aralığı yapılandırılması.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-228">When this happens, hello alert service may not have all available metrics data for hello configured alert interval, which may lead tooalerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="9e8b3-229">Ölçüm verileri programlı olarak erişme</span><span class="sxs-lookup"><span data-stu-id="9e8b3-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="9e8b3-230">Merhaba aşağıdaki kod hello dakika ölçümleri dakika cinsinden bir aralığı için erişir ve bir konsol penceresi hello sonuçları görüntüler örnek C# kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-230">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="9e8b3-231">Hello Azure Storage kitaplığı hello depolama erişilirken hello ölçümleri tablolarda basitleştirir CloudAnalyticsClient sınıfı içeren 4 sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-231">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
      string.Format("Time: {0}, ", entity.Time) +
      string.Format("AccessType: {0}, ", entity.AccessType) +
      string.Format("TransactionType: {0}, ", entity.TransactionType) +
      string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="9e8b3-232">Depolama ölçümleri etkinleştirdiğinizde, hangi, ücretlendirme?</span><span class="sxs-lookup"><span data-stu-id="9e8b3-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="9e8b3-233">İstekleri toocreate tablo varlıkları ölçümünün hello standart ücretler uygulanabilir tooall Azure depolama işlemleri sırasında ücretlendirilen yazma.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-233">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="9e8b3-234">Bir istemci toometrics verilerini okuma ve silme istekleri de standart oranlarda faturalanabilir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-234">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="9e8b3-235">Bir veri bekletme ilkesi yapılandırdıysanız, Azure Storage eski ölçüm verileri sildiğinde, sizden ücret istenmese.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="9e8b3-236">Ancak, analiz verileri silerseniz, hesabınızı hello silme işlemleri için ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-236">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="9e8b3-237">Merhaba ölçümleri tabloları tarafından kullanılan hello kapasitesi Faturalanabilir ayrıca: tooestimate hello ölçüm verilerini depolamak için kullanılan kapasite miktarı aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e8b3-237">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="9e8b3-238">Sonra her saat her hizmetin her API bir hizmet kullanırsa, hem hizmet hem de API düzey özeti etkinleştirdiyseniz, yaklaşık 148 KB veri saatte hello ölçümleri işlem tablolarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="9e8b3-239">Sonra her saat her hizmetin her API bir hizmet kullanırsa, yalnızca hizmet düzeyi Özet etkinleştirdiyseniz, yaklaşık olarak 12 KB veri saatte hello ölçümleri işlem tablolarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="9e8b3-240">Hello BLOB'lar için kapasite tablosu sahip iki satır (kullanıcı, günlükleri için seçti sağlanan) her gün eklenen: Bu bu tablonun her günün hello boyutunu tarafından tooapproximately 300 bayt arttığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e8b3-240">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e8b3-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e8b3-241">Next steps</span></span>
[<span data-ttu-id="9e8b3-242">Günlüğe kaydetme ve günlük verilerine erişme depolama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9e8b3-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
