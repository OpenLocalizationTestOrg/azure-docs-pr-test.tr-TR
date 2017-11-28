---
title: "aaaEnabling depolama ölçümlerini hello Azure portalı | Microsoft Docs"
description: "Blob, kuyruk, tablo ve Dosya Hizmetleri tooenable depolama ölçümlerini nasıl hello"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="53bb6-103">Depolama ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="53bb6-103">Enabling Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="53bb6-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="53bb6-104">Overview</span></span>
<span data-ttu-id="53bb6-105">Depolama ölçümleri, yeni bir depolama hesabı oluşturduğunuzda, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="53bb6-106">Her iki hello kullanarak izlemeyi yapılandırmadan [Klasik Azure portalı](https://manage.windowsazure.com), Windows PowerShell veya bir depolama API aracılığıyla programlı olarak.</span><span class="sxs-lookup"><span data-stu-id="53bb6-106">You can configure monitoring using either hello [Azure Classic Portal](https://manage.windowsazure.com), Windows PowerShell, or programmatically through a storage API.</span></span>

<span data-ttu-id="53bb6-107">Depolama ölçümleri etkinleştirdiğinizde hello veri saklama süresi seçmeniz gerekir: Bu dönem için ne kadar süreyle hello depolama hizmeti hello ölçümleri ve sizin hello için boşluk gerekli toostore ücretleri tutar belirler bunları.</span><span class="sxs-lookup"><span data-stu-id="53bb6-107">When you enable Storage Metrics, you must choose a retention period for hello data: this period determines for how long hello storage service keeps hello metrics and charges you for hello space required toostore them.</span></span> <span data-ttu-id="53bb6-108">Genellikle, daha kısa bir bekletme dönemi saatlik ölçümleri daha dakika ölçümünün hello önemli ek boşluk dakika ölçümlerini gerekli nedeniyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of hello significant extra space required for minute metrics.</span></span> <span data-ttu-id="53bb6-109">Yeterli zaman tooanalyze hello veriniz varsa ve çevrimdışı analiz ve raporlama amacıyla tookeep istediğiniz ölçümleri karşıdan şekilde bir bekletme dönemi seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-109">You should choose a retention period such that you have sufficient time tooanalyze hello data and download any metrics you wish tookeep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="53bb6-110">Ayrıca ölçümleri veri depolama hesabınızdan indirme için Fatura edilecek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="53bb6-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a><span data-ttu-id="53bb6-111">Klasik Azure portalı kullanarak tooenable Storage ölçümleri nasıl hello</span><span class="sxs-lookup"><span data-stu-id="53bb6-111">How tooenable Storage metrics using hello Azure Classic Portal</span></span>
<span data-ttu-id="53bb6-112">Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), bir depolama hesabı toocontrol depolama ölçümleri hello yapılandırma sayfasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="53bb6-112">In hello [Azure Classic Portal](https://manage.windowsazure.com), you use hello Configure page for a storage account toocontrol Storage Metrics.</span></span> <span data-ttu-id="53bb6-113">İzleme için bir düzeyi ve bir bekletme dönemi BLOB'lar, tablolar ve Kuyruklar her gün ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53bb6-113">For monitoring, you can set a level and a retention period in days for each of blobs, tables, and queues.</span></span> <span data-ttu-id="53bb6-114">Her durumda, hello düzeyi hello aşağıdakilerden biridir:</span><span class="sxs-lookup"><span data-stu-id="53bb6-114">In each case, hello level is one of hello following:</span></span>

* <span data-ttu-id="53bb6-115">Kapalı — Hiçbir ölçümleri toplanır.</span><span class="sxs-lookup"><span data-stu-id="53bb6-115">Off — No metrics are collected.</span></span>
* <span data-ttu-id="53bb6-116">En küçük — Temel giriş/çıkış, kullanılabilirlik, gecikme ve hello Blob, tablo ve kuyruk Hizmetleri için toplanır başarı yüzdeleri gibi ölçümleri birtakım depolama ölçümleri toplar.</span><span class="sxs-lookup"><span data-stu-id="53bb6-116">Minimal — Storage Metrics collects a basic set of metrics such as ingress/egress, availability, latency, and success percentages, which are aggregated for hello Blob, Table, and Queue services.</span></span>
* <span data-ttu-id="53bb6-117">Ayrıntılı — içeren ölçümlerini tam kümesi depolama ölçümleri toplar her depolama API işlemi için aynı ölçümleri Merhaba, ayrıca toohello hizmet düzeyi ölçümlerini.</span><span class="sxs-lookup"><span data-stu-id="53bb6-117">Verbose — Storage Metrics collects a full set of metrics that includes hello same metrics for each storage API operation, in addition toohello service-level metrics.</span></span> <span data-ttu-id="53bb6-118">Ayrıntılı ölçümler uygulama işlemleri sırasında oluşabilecek sorunları daha yakından analizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="53bb6-118">Verbose metrics enable closer analysis of issues that occur during application operations.</span></span>

<span data-ttu-id="53bb6-119">Klasik Azure portalı hello Not şu anda, depolama hesabınızdaki tooconfigure minute ölçümleri etkinleştirmez; PowerShell kullanarak dakika ölçümlerini etkinleştirmeniz gerekir veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="53bb6-119">Note that hello Azure Classic Portal does not currently enable you tooconfigure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-tooenable-storage-metrics-using-powershell"></a><span data-ttu-id="53bb6-120">Nasıl tooenable Storage ölçümleri PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="53bb6-120">How tooenable Storage metrics using PowerShell</span></span>
<span data-ttu-id="53bb6-121">PowerShell, LocalMachine tooconfigure Storage ölçümleri depolama hesabınızdaki hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello geçerli ayarları kullanarak ve cmdlet hello Set-AzureStorageServiceMetricsProperty toochange hello geçerli ayarları.</span><span class="sxs-lookup"><span data-stu-id="53bb6-121">You can use PowerShell on your local machine tooconfigure Storage Metrics in your storage account by using hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello current settings, and hello cmdlet Set-AzureStorageServiceMetricsProperty toochange hello current settings.</span></span>

<span data-ttu-id="53bb6-122">Depolama Ölçümleri kontrol hello cmdlet'leri şu parametreler hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="53bb6-122">hello cmdlets that control Storage Metrics use hello following parameters:</span></span>

* <span data-ttu-id="53bb6-123">MetricsType olası saat ve dakika değerleri.</span><span class="sxs-lookup"><span data-stu-id="53bb6-123">MetricsType possible values are Hour and Minute.</span></span>
* <span data-ttu-id="53bb6-124">ServiceType olası değerler şunlardır: Blob, kuyruk ve tablo.</span><span class="sxs-lookup"><span data-stu-id="53bb6-124">ServiceType possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="53bb6-125">MetricsLevel olası değerler şunlardır: None (Merhaba Klasik Azure portalı eşdeğer tooOff) hizmeti (Merhaba Klasik Azure Portalı'nda eşdeğer tooMinimal) ve ServiceAndApi (Merhaba Klasik Azure Portalı'nda eşdeğer tooVerbose).</span><span class="sxs-lookup"><span data-stu-id="53bb6-125">MetricsLevel possible values are None (equivalent tooOff in hello Azure Classic Portal), Service (equivalent tooMinimal in hello Azure Classic Portal), and ServiceAndApi (equivalent tooVerbose in hello Azure Classic Portal).</span></span>

<span data-ttu-id="53bb6-126">Örneğin, hello aşağıdaki komutu hello hello bekletme süresi ile varsayılan depolama hesabınızdaki blob hizmeti için ölçümleri toofive güne ayarlayabilir dakika üzerinde geçer:</span><span class="sxs-lookup"><span data-stu-id="53bb6-126">For example, hello following command switches on minute metrics for hello blob service in your default storage account with hello retention period set toofive days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
<span data-ttu-id="53bb6-127">Merhaba aşağıdaki komutu hello geçerli saatlik ölçümleri düzeyi ve saklama gün boyunca hello blob hizmeti varsayılan depolama hesabınızdaki alır:</span><span class="sxs-lookup"><span data-stu-id="53bb6-127">hello following command retrieves hello current hourly metrics level and retention days for hello blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
<span data-ttu-id="53bb6-128">Nasıl toouse tooconfigure hello Azure PowerShell cmdlet'leri toowork Azure aboneliğinizle ve nasıl tooselect hello varsayılan depolama hesabı hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="53bb6-128">For information about how tooconfigure hello Azure PowerShell cmdlets toowork with your Azure subscription and how tooselect hello default storage account toouse, see: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-tooenable-storage-metrics-programmatically"></a><span data-ttu-id="53bb6-129">Nasıl tooenable Storage ölçümleri programlamayla</span><span class="sxs-lookup"><span data-stu-id="53bb6-129">How tooenable Storage metrics programmatically</span></span>
<span data-ttu-id="53bb6-130">C# kod parçacığında aşağıdaki hello nasıl tooenable ölçümleri ve günlük hello Blob hizmeti kullandığınız için .NET için depolama istemci kitaplığı hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="53bb6-130">hello following C# snippet shows how tooenable metrics and logging for hello Blob service using hello storage client library for .NET:</span></span>

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

## <a name="viewing-storage-metrics"></a><span data-ttu-id="53bb6-131">Depolama ölçümleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="53bb6-131">Viewing Storage metrics</span></span>
<span data-ttu-id="53bb6-132">Depolama hesabınız depolama ölçümleri toomonitor yapılandırıldığında, depolama hesabındaki iyi bilinen tablolara kümesi hello ölçümleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="53bb6-132">When you have configured Storage Metrics toomonitor your storage account, it records hello metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="53bb6-133">Grafikte çıktıklarında depolama hesabınızda Klasik Azure portalı tooview hello saatlik ölçümleri hello için hello İzleyici sayfasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53bb6-133">You can use hello Monitor page for your storage account in hello Azure Classic Portal tooview hello hourly metrics as they become available on a chart.</span></span> <span data-ttu-id="53bb6-134">Merhaba Klasik Azure portalı bu sayfasında, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="53bb6-134">On this page in hello Azure Classic Portal, you can:</span></span>

* <span data-ttu-id="53bb6-135">Hangi ölçümleri tooplot hello grafik seçin (kullanılabilir ölçümler hello seçimine bağımlı olup, hello hizmet hello Yapılandır sayfasında ayrıntılı veya en az izlenmesinde seçiminize göre).</span><span class="sxs-lookup"><span data-stu-id="53bb6-135">Select which metrics tooplot on hello chart (hello choice of available metrics will depend on whether you chose verbose or minimal monitoring for hello service on hello Configure page).</span></span>
* <span data-ttu-id="53bb6-136">Merhaba grafikte görüntülenen hello ölçümleri Hello zaman aralığını seçin.</span><span class="sxs-lookup"><span data-stu-id="53bb6-136">Select hello time range for hello metrics displayed on hello chart.</span></span>
* <span data-ttu-id="53bb6-137">Toouse bir mutlak veya göreli ölçeği tooplot hello ölçümleri'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="53bb6-137">Choose toouse an absolute or relative scale tooplot hello metrics.</span></span>
* <span data-ttu-id="53bb6-138">E-posta uyarıları toonotify yapılandırmanız, belirli bir ölçüyü belirli bir değere ulaştığında.</span><span class="sxs-lookup"><span data-stu-id="53bb6-138">Configure email alerts toonotify you when a specific metric reaches a certain value.</span></span>

<span data-ttu-id="53bb6-139">Uzun vadeli depolama veya tooanalyze toodownload hello ölçümleri istiyorsanız yerel olarak toouse bir aracı gerekir veya kaldıracak tooread hello tabloları bazı kodlar yazmak onları.</span><span class="sxs-lookup"><span data-stu-id="53bb6-139">If you want toodownload hello metrics for long-term storage or tooanalyze them locally, you will need toouse a tool or write some code tooread hello tables.</span></span> <span data-ttu-id="53bb6-140">Merhaba dakika ölçümleri analiz indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-140">You must download hello minute metrics for analysis.</span></span> <span data-ttu-id="53bb6-141">Merhaba tabloları depolama hesabınızdaki tüm hello tablolarını listelemek, ancak doğrudan ada göre erişme görünmez.</span><span class="sxs-lookup"><span data-stu-id="53bb6-141">hello tables do not appear if you list all hello tables in your storage account, but you can access them directly by name.</span></span> <span data-ttu-id="53bb6-142">Çok sayıda üçüncü taraf araçları depolama gözatma bu tabloları farkında olduğundan ve tooview etkinleştirmek bunları doğrudan (Merhaba blog gönderisi bkz [Microsoft Azure depolama gezginleri](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) kullanılabilen araçların listesi için).</span><span class="sxs-lookup"><span data-stu-id="53bb6-142">Many third-party storage-browsing tools are aware of these tables and enable you tooview them directly (see hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available tools).</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="53bb6-143">Saatlik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="53bb6-143">Hourly metrics</span></span>
* <span data-ttu-id="53bb6-144">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="53bb6-144">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="53bb6-145">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="53bb6-145">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="53bb6-146">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="53bb6-146">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="53bb6-147">Dakika ölçümleri</span><span class="sxs-lookup"><span data-stu-id="53bb6-147">Minute metrics</span></span>
* <span data-ttu-id="53bb6-148">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="53bb6-148">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="53bb6-149">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="53bb6-149">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="53bb6-150">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="53bb6-150">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="53bb6-151">Kapasite</span><span class="sxs-lookup"><span data-stu-id="53bb6-151">Capacity</span></span>
* <span data-ttu-id="53bb6-152">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="53bb6-152">$MetricsCapacityBlob</span></span>

<span data-ttu-id="53bb6-153">Bu tablolar hello şemaları tam ayrıntılarını bulabilirsiniz [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="53bb6-153">You can find full details of hello schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="53bb6-154">altındaki Hello örnek satırları yalnızca bir sütun alt kümesi hello kullanılabilir Göster, ancak bu ölçümleri Storage ölçümleri kaydeder hello şekilde önemli özelliklerinden bazıları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="53bb6-154">hello sample rows below show only a subset of hello columns available, but illustrate some important features of hello way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="53bb6-155">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="53bb6-155">PartitionKey</span></span> | <span data-ttu-id="53bb6-156">RowKey</span><span class="sxs-lookup"><span data-stu-id="53bb6-156">RowKey</span></span> | <span data-ttu-id="53bb6-157">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="53bb6-157">Timestamp</span></span> | <span data-ttu-id="53bb6-158">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="53bb6-158">TotalRequests</span></span> | <span data-ttu-id="53bb6-159">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="53bb6-159">TotalBillableRequests</span></span> | <span data-ttu-id="53bb6-160">Totalıngress</span><span class="sxs-lookup"><span data-stu-id="53bb6-160">TotalIngress</span></span> | <span data-ttu-id="53bb6-161">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="53bb6-161">TotalEgress</span></span> | <span data-ttu-id="53bb6-162">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="53bb6-162">Availability</span></span> | <span data-ttu-id="53bb6-163">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="53bb6-163">AverageE2ELatency</span></span> | <span data-ttu-id="53bb6-164">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="53bb6-164">AverageServerLatency</span></span> | <span data-ttu-id="53bb6-165">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="53bb6-165">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="53bb6-166">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="53bb6-166">20140522T1100</span></span> |<span data-ttu-id="53bb6-167">Kullanıcı; Tüm</span><span class="sxs-lookup"><span data-stu-id="53bb6-167">user;All</span></span> |<span data-ttu-id="53bb6-168">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="53bb6-168">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="53bb6-169">7</span><span class="sxs-lookup"><span data-stu-id="53bb6-169">7</span></span> |<span data-ttu-id="53bb6-170">7</span><span class="sxs-lookup"><span data-stu-id="53bb6-170">7</span></span> |<span data-ttu-id="53bb6-171">4003</span><span class="sxs-lookup"><span data-stu-id="53bb6-171">4003</span></span> |<span data-ttu-id="53bb6-172">46801</span><span class="sxs-lookup"><span data-stu-id="53bb6-172">46801</span></span> |<span data-ttu-id="53bb6-173">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-173">100</span></span> |<span data-ttu-id="53bb6-174">104.4286</span><span class="sxs-lookup"><span data-stu-id="53bb6-174">104.4286</span></span> |<span data-ttu-id="53bb6-175">6.857143</span><span class="sxs-lookup"><span data-stu-id="53bb6-175">6.857143</span></span> |<span data-ttu-id="53bb6-176">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-176">100</span></span> |
| <span data-ttu-id="53bb6-177">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="53bb6-177">20140522T1100</span></span> |<span data-ttu-id="53bb6-178">Kullanıcı; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="53bb6-178">user;QueryEntities</span></span> |<span data-ttu-id="53bb6-179">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="53bb6-179">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="53bb6-180">5</span><span class="sxs-lookup"><span data-stu-id="53bb6-180">5</span></span> |<span data-ttu-id="53bb6-181">5</span><span class="sxs-lookup"><span data-stu-id="53bb6-181">5</span></span> |<span data-ttu-id="53bb6-182">2694</span><span class="sxs-lookup"><span data-stu-id="53bb6-182">2694</span></span> |<span data-ttu-id="53bb6-183">45951</span><span class="sxs-lookup"><span data-stu-id="53bb6-183">45951</span></span> |<span data-ttu-id="53bb6-184">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-184">100</span></span> |<span data-ttu-id="53bb6-185">143.8</span><span class="sxs-lookup"><span data-stu-id="53bb6-185">143.8</span></span> |<span data-ttu-id="53bb6-186">7.8</span><span class="sxs-lookup"><span data-stu-id="53bb6-186">7.8</span></span> |<span data-ttu-id="53bb6-187">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-187">100</span></span> |
| <span data-ttu-id="53bb6-188">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="53bb6-188">20140522T1100</span></span> |<span data-ttu-id="53bb6-189">Kullanıcı; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="53bb6-189">user;QueryEntity</span></span> |<span data-ttu-id="53bb6-190">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="53bb6-190">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="53bb6-191">1</span><span class="sxs-lookup"><span data-stu-id="53bb6-191">1</span></span> |<span data-ttu-id="53bb6-192">1</span><span class="sxs-lookup"><span data-stu-id="53bb6-192">1</span></span> |<span data-ttu-id="53bb6-193">538</span><span class="sxs-lookup"><span data-stu-id="53bb6-193">538</span></span> |<span data-ttu-id="53bb6-194">633</span><span class="sxs-lookup"><span data-stu-id="53bb6-194">633</span></span> |<span data-ttu-id="53bb6-195">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-195">100</span></span> |<span data-ttu-id="53bb6-196">3</span><span class="sxs-lookup"><span data-stu-id="53bb6-196">3</span></span> |<span data-ttu-id="53bb6-197">3</span><span class="sxs-lookup"><span data-stu-id="53bb6-197">3</span></span> |<span data-ttu-id="53bb6-198">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-198">100</span></span> |
| <span data-ttu-id="53bb6-199">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="53bb6-199">20140522T1100</span></span> |<span data-ttu-id="53bb6-200">Kullanıcı; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="53bb6-200">user;UpdateEntity</span></span> |<span data-ttu-id="53bb6-201">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="53bb6-201">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="53bb6-202">1</span><span class="sxs-lookup"><span data-stu-id="53bb6-202">1</span></span> |<span data-ttu-id="53bb6-203">1</span><span class="sxs-lookup"><span data-stu-id="53bb6-203">1</span></span> |<span data-ttu-id="53bb6-204">771</span><span class="sxs-lookup"><span data-stu-id="53bb6-204">771</span></span> |<span data-ttu-id="53bb6-205">217</span><span class="sxs-lookup"><span data-stu-id="53bb6-205">217</span></span> |<span data-ttu-id="53bb6-206">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-206">100</span></span> |<span data-ttu-id="53bb6-207">9</span><span class="sxs-lookup"><span data-stu-id="53bb6-207">9</span></span> |<span data-ttu-id="53bb6-208">6</span><span class="sxs-lookup"><span data-stu-id="53bb6-208">6</span></span> |<span data-ttu-id="53bb6-209">100</span><span class="sxs-lookup"><span data-stu-id="53bb6-209">100</span></span> |

<span data-ttu-id="53bb6-210">Bu örnek dakika ölçümleri verileri dakika çözünürlükte hello zaman hello bölüm anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="53bb6-210">In this example minute metrics data, hello partition key uses hello time at minute resolution.</span></span> <span data-ttu-id="53bb6-211">Hello satır anahtarını hello hello satır için depolanan bilgi türünü tanımlayan ve bu bilgileri, hello erişim türünü ve hello istek türü iki parça oluşur:</span><span class="sxs-lookup"><span data-stu-id="53bb6-211">hello row key identifies hello type of information that is stored in hello row and this is composed of two pieces of information, hello access type, and hello request type:</span></span>

* <span data-ttu-id="53bb6-212">Merhaba erişim kullanıcı veya sistem burada kullanıcı tooall kullanıcı istekleri toohello depolama hizmeti anlamına gelir ve sistem depolama analizi tarafından yapılan toorequests başvuruyor türüdür.</span><span class="sxs-lookup"><span data-stu-id="53bb6-212">hello access type is either user or system, where user refers tooall user requests toohello storage service, and system refers toorequests made by Storage Analytics.</span></span>
* <span data-ttu-id="53bb6-213">Merhaba istek türü, tüm durumda bir Özet satırı olan veya QueryEntity veya UpdateEntity gibi belirli API hello tanımlayan olur.</span><span class="sxs-lookup"><span data-stu-id="53bb6-213">hello request type is either all in which case it is a summary line, or it identifies hello specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="53bb6-214">Merhaba örnek verileri yukarıda tüm hello gösterir (11: 00'da başlayarak) tek bir dakikadır QueryEntities istekleri bunu hello sayısını kaydeder artı hello QueryEntity istek sayısı artı UpdateEntity istek hello sayısı toplam gösterilen hello olduğu tooseven Yukarı Ekle Merhaba kullanıcı: tüm satır.</span><span class="sxs-lookup"><span data-stu-id="53bb6-214">hello sample data above shows all hello records for a single minute (starting at 11:00AM), so hello number of QueryEntities requests plus hello number of QueryEntity requests plus hello number of UpdateEntity requests add up tooseven, which is hello total shown on hello user:All row.</span></span> <span data-ttu-id="53bb6-215">Hesaplayarak hello ortalama uçtan uca gecikmesine 104.4286 hello kullanıcı: tüm satır benzer şekilde, türetilemeyeceğini ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="53bb6-215">Similarly, you can derive hello average end-to-end latency 104.4286 on hello user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

<span data-ttu-id="53bb6-216">Depolama ölçümleri otomatik olarak depolama hizmetlerinizi hello davranışını önemli değişiklikler size bildirebilir böylece hello Klasik Azure portalı hello İzleyici sayfasında uyarıları ayarlama düşünmelisiniz. Bu ölçüm verilerini bir sınırlandırılmış biçimde bir Depolama Gezgini aracı toodownload kullanırsanız, Microsoft Excel tooanalyze hello verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53bb6-216">You should consider setting up alerts in hello Azure Classic Portal on hello Monitor page so that Storage Metrics can automatically notify you of any important changes in hello behavior of your storage services.If you use a storage explorer tool toodownload this metrics data in a delimited format, you can use Microsoft Excel tooanalyze hello data.</span></span> <span data-ttu-id="53bb6-217">Merhaba blog gönderisi bkz [Microsoft Azure depolama gezginleri](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) kullanılabilir Depolama Gezgini araçları listesi.</span><span class="sxs-lookup"><span data-stu-id="53bb6-217">See hello blog post [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) for a list of available storage explorer tools.</span></span>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="53bb6-218">Ölçüm verileri programlı olarak erişme</span><span class="sxs-lookup"><span data-stu-id="53bb6-218">Accessing metrics data programmatically</span></span>
<span data-ttu-id="53bb6-219">Merhaba aşağıdaki kod hello dakika ölçümleri dakika cinsinden bir aralığı için erişir ve bir konsol penceresi hello sonuçları görüntüler örnek C# kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-219">hello following listing shows sample C# code that accesses hello minute metrics for a range of minutes and displays hello results in a console Window.</span></span> <span data-ttu-id="53bb6-220">Hello Azure Storage kitaplığı hello depolama erişilirken hello ölçümleri tablolarda basitleştirir CloudAnalyticsClient sınıfı içeren 4 sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="53bb6-220">It uses hello Azure Storage Library version 4 that includes hello CloudAnalyticsClient class that simplifies accessing hello metrics tables in storage.</span></span>

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="53bb6-221">Depolama ölçümleri etkinleştirdiğinizde, hangi, ücretlendirme?</span><span class="sxs-lookup"><span data-stu-id="53bb6-221">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="53bb6-222">İstekleri toocreate tablo varlıkları ölçümünün hello standart ücretler uygulanabilir tooall Azure depolama işlemleri sırasında ücretlendirilen yazma.</span><span class="sxs-lookup"><span data-stu-id="53bb6-222">Write requests toocreate table entities for metrics are charged at hello standard rates applicable tooall Azure Storage operations.</span></span>

<span data-ttu-id="53bb6-223">Bir istemci toometrics verilerini okuma ve silme istekleri de standart oranlarda faturalanabilir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-223">Read and delete requests by a client toometrics data are also billable at standard rates.</span></span> <span data-ttu-id="53bb6-224">Bir veri bekletme ilkesi yapılandırdıysanız, Azure Storage eski ölçüm verileri sildiğinde, sizden ücret istenmese.</span><span class="sxs-lookup"><span data-stu-id="53bb6-224">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="53bb6-225">Ancak, analiz verileri silerseniz, hesabınızı hello silme işlemleri için ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-225">However, if you delete analytics data, your account is charged for hello delete operations.</span></span>

<span data-ttu-id="53bb6-226">Merhaba ölçümleri tabloları tarafından kullanılan hello kapasitesi Faturalanabilir ayrıca: tooestimate hello ölçüm verilerini depolamak için kullanılan kapasite miktarı aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="53bb6-226">hello capacity used by hello metrics tables is also billable: you can use hello following tooestimate hello amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="53bb6-227">Sonra her saat her hizmetin her API bir hizmet kullanırsa, hem hizmet hem de API düzey özeti etkinleştirdiyseniz, yaklaşık 148 KB veri saatte hello ölçümleri işlem tablolarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="53bb6-227">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in hello metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="53bb6-228">Sonra her saat her hizmetin her API bir hizmet kullanırsa, yalnızca hizmet düzeyi Özet etkinleştirdiyseniz, yaklaşık olarak 12 KB veri saatte hello ölçümleri işlem tablolarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="53bb6-228">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in hello metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="53bb6-229">Hello BLOB'lar için kapasite tablosu sahip iki satır (kullanıcı, günlükleri için seçti sağlanan) her gün eklenen: Bu bu tablonun her günün hello boyutunu tarafından tooapproximately 300 bayt arttığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="53bb6-229">hello capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day hello size of this table increases by up tooapproximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53bb6-230">Sonraki adımlar:</span><span class="sxs-lookup"><span data-stu-id="53bb6-230">Next steps:</span></span>
[<span data-ttu-id="53bb6-231">Günlüğe kaydetme ve günlük verilerine erişme depolama çözümlemeleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="53bb6-231">Enabling Storage Analytics Logging and Accessing Log Data</span></span>](https://msdn.microsoft.com/library/dn782840.aspx)
