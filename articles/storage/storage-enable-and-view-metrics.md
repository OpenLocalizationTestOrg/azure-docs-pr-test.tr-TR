---
title: "Azure portalında depolama ölçümlerini etkinleştirme | Microsoft Docs"
description: "Blob, kuyruk, tablo ve Dosya Hizmetleri için depolama ölçümlerini etkinleştirme"
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
ms.openlocfilehash: 2906f808482d0b990e3ddd31ef5368e9fdd9f646
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a><span data-ttu-id="68e9b-103">Azure Storage ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="68e9b-103">Enabling Azure Storage metrics and viewing metrics data</span></span>
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a><span data-ttu-id="68e9b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="68e9b-104">Overview</span></span>
<span data-ttu-id="68e9b-105">Depolama ölçümleri, yeni bir depolama hesabı oluşturduğunuzda, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-105">Storage Metrics is enabled by default when you create a new storage account.</span></span> <span data-ttu-id="68e9b-106">Aracılığıyla izlemeyi yapılandırmadan [Azure portal](https://portal.azure.com) veya Windows PowerShell veya depolama istemci kitaplıklarından birini aracılığıyla programlı olarak.</span><span class="sxs-lookup"><span data-stu-id="68e9b-106">You can configure monitoring via the [Azure portal](https://portal.azure.com) or Windows PowerShell, or programmatically via one of the storage client libraries.</span></span>

<span data-ttu-id="68e9b-107">Ölçüm verileri için bekletme süresi yapılandırabilirsiniz: Bu dönem için ne kadar depolama hizmeti ölçümleri ve bunları depolamak için alan için gerekli ücretleri tutar belirler.</span><span class="sxs-lookup"><span data-stu-id="68e9b-107">You can configure a retention period for the metrics data: this period determines for how long the storage service keeps the metrics and charges you for the space required to store them.</span></span> <span data-ttu-id="68e9b-108">Genellikle, daha kısa bir bekletme dönemi saatlik ölçümleri daha dakika ölçümünün dakika ölçümleri için gereken önemli ek boşluk nedeniyle kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-108">Typically, you should use a shorter retention period for minute metrics than hourly metrics because of the significant extra space required for minute metrics.</span></span> <span data-ttu-id="68e9b-109">Verileri çözümlemek ve çevrimdışı analiz veya Raporlama amaçları için tutmak istediğiniz ölçümleri karşıdan yüklemek için yeterli zamana sahip olacağı şekilde tutma süresi seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-109">You should choose a retention period such that you have sufficient time to analyze the data and download any metrics you wish to keep for off-line analysis or reporting purposes.</span></span> <span data-ttu-id="68e9b-110">Ayrıca ölçümleri veri depolama hesabınızdan indirme için Fatura edilecek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="68e9b-110">Remember that you will also be billed for downloading metrics data from your storage account.</span></span>

## <a name="how-to-enable-metrics-using-the-azure-portal"></a><span data-ttu-id="68e9b-111">Azure portalını kullanarak ölçümlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="68e9b-111">How to enable metrics using the Azure portal</span></span>
<span data-ttu-id="68e9b-112">Ölçümlerini etkinleştirmek için aşağıdaki adımları izleyin [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="68e9b-112">Follow these steps to enable metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="68e9b-113">Depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-113">Navigate to your storage account.</span></span>
1. <span data-ttu-id="68e9b-114">Seçin **tanılama** üzerinde **menü** dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="68e9b-114">Select **Diagnostics** on the **Menu** blade</span></span>
1. <span data-ttu-id="68e9b-115">Emin **durum** ayarlanır **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-115">Ensure that **Status** is set to **On**.</span></span>
1. <span data-ttu-id="68e9b-116">Ölçümleri, izlemek istediğiniz hizmetleri seçin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-116">Select the metrics for the services you wish to monitor.</span></span>
1. <span data-ttu-id="68e9b-117">Ölçümleri korumak ve verileri günlüğe kaydetmek için ne kadar süreyle belirtmek için bir bekletme ilkesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-117">Specify a retention policy to indicate how long to retain metrics and log data.</span></span>
1. <span data-ttu-id="68e9b-118">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-118">Select **Save**.</span></span>

<span data-ttu-id="68e9b-119">Unutmayın [Azure portal](https://portal.azure.com) minute ölçümleri depolama hesabınızdaki; yapılandırmanızı şu anda olarak etkinleştirmez PowerShell kullanarak dakika ölçümlerini etkinleştirmeniz gerekir veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="68e9b-119">Note that the [Azure portal](https://portal.azure.com) does not currently enable you to configure minute metrics in your storage account; you must enable minute metrics using PowerShell or programmatically.</span></span>

## <a name="how-to-enable-metrics-using-powershell"></a><span data-ttu-id="68e9b-120">PowerShell kullanarak ölçümlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="68e9b-120">How to enable metrics using PowerShell</span></span>
<span data-ttu-id="68e9b-121">Geçerli ayarları değiştirmek için geçerli ayarları almak için Get-AzureStorageServiceMetricsProperty Azure PowerShell cmdlet'ini ve Set-AzureStorageServiceMetricsProperty cmdlet'ini kullanarak depolama hesabınız depolama ölçümleri yapılandırmak için yerel makinenizde PowerShell'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-121">You can use PowerShell on your local machine to configure Storage Metrics in your storage account by using the Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty to retrieve the current settings, and the cmdlet Set-AzureStorageServiceMetricsProperty to change the current settings.</span></span>

<span data-ttu-id="68e9b-122">Depolama Ölçümleri kontrol cmdlet'leri aşağıdaki parametreleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="68e9b-122">The cmdlets that control Storage Metrics use the following parameters:</span></span>

* <span data-ttu-id="68e9b-123">MetricsType: olası saat ve dakika değerleri.</span><span class="sxs-lookup"><span data-stu-id="68e9b-123">MetricsType: possible values are Hour and Minute.</span></span>
* <span data-ttu-id="68e9b-124">ServiceType: Blob, kuyruk ve tablo olası değerler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-124">ServiceType: possible values are Blob, Queue, and Table.</span></span>
* <span data-ttu-id="68e9b-125">MetricsLevel: olası değerler, hizmeti ve ServiceAndApi yok.</span><span class="sxs-lookup"><span data-stu-id="68e9b-125">MetricsLevel: possible values are None, Service, and ServiceAndApi.</span></span>

<span data-ttu-id="68e9b-126">Örneğin, aşağıdaki komutu varsayılan depolama hesabınızdaki Blob hizmeti için dakika ölçümler üzerinde bekletme dönemi beş gün olarak ayarlanmış olan geçer:</span><span class="sxs-lookup"><span data-stu-id="68e9b-126">For example, the following command switches on minute metrics for the Blob service in your default storage account with the retention period set to five days:</span></span>

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

<span data-ttu-id="68e9b-127">Aşağıdaki komut, geçerli saatlik ölçümleri düzeyi ve saklama gün varsayılan depolama hesabınızdaki blob hizmeti için alır:</span><span class="sxs-lookup"><span data-stu-id="68e9b-127">The following command retrieves the current hourly metrics level and retention days for the blob service in your default storage account:</span></span>

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

<span data-ttu-id="68e9b-128">Azure aboneliğinizi ve kullanmak için varsayılan depolama hesabını seçmek nasıl çalışmak için Azure PowerShell cmdlet'lerini nasıl yapılandırılacağı hakkında bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="68e9b-128">For information about how to configure the Azure PowerShell cmdlets to work with your Azure subscription and how to select the default storage account to use, see: [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="how-to-enable-storage-metrics-programmatically"></a><span data-ttu-id="68e9b-129">Depolama ölçümleri programlı olarak etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="68e9b-129">How to enable Storage metrics programmatically</span></span>
<span data-ttu-id="68e9b-130">Aşağıdaki C# kod parçacığında, ölçümleri ve .NET için depolama istemci kitaplığı kullanılarak Blob hizmeti için günlüğe kaydetmeyi etkinleştirmek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="68e9b-130">The following C# snippet shows how to enable metrics and logging for the Blob service using the storage client library for .NET:</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days.
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a><span data-ttu-id="68e9b-131">Depolama ölçümleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="68e9b-131">Viewing Storage metrics</span></span>
<span data-ttu-id="68e9b-132">Depolama hesabınız izlemek için Storage Analytics ölçümleri yapılandırdıktan sonra Storage Analytics ölçümleri depolama hesabındaki iyi bilinen tablo kümesini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="68e9b-132">After you configure Storage Analytics metrics to monitor your storage account, Storage Analytics records the metrics in a set of well-known tables in your storage account.</span></span> <span data-ttu-id="68e9b-133">Saatlik ölçümlerini görüntülemek üzere grafik yapılandırabilirsiniz [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="68e9b-133">You can configure charts to view hourly metrics in the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="68e9b-134">Depolama hesabınıza gidin [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68e9b-134">Navigate to your storage account in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="68e9b-135">Seçin **ölçümleri** içinde **menü** dikey ölçümleri görüntülemek istediğiniz hizmeti.</span><span class="sxs-lookup"><span data-stu-id="68e9b-135">Select **Metrics** in the **Menu** blade for the service whose metrics you want to view.</span></span>
1. <span data-ttu-id="68e9b-136">Seçin **Düzenle** yapılandırmak istediğiniz grafik.</span><span class="sxs-lookup"><span data-stu-id="68e9b-136">Select **Edit** on the chart you want to configure.</span></span>
1. <span data-ttu-id="68e9b-137">İçinde **grafiği Düzenle** dikey penceresinde, select **zaman aralığı**, **grafik türü**ve görüntülenmesini istediğiniz grafikte ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="68e9b-137">In the **Edit Chart** blade, select the **Time Range**, **Chart type**, and the metrics you want displayed in the chart.</span></span>
1. <span data-ttu-id="68e9b-138">**Tamam**’ı seçin</span><span class="sxs-lookup"><span data-stu-id="68e9b-138">Select **OK**</span></span>

<span data-ttu-id="68e9b-139">Uzun vadeli depolama için ölçümler indirmek için veya yerel olarak analiz etmek istiyorsanız, yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="68e9b-139">If you want to download the metrics for long-term storage or to analyze them locally, you will need to:</span></span>

* <span data-ttu-id="68e9b-140">Bu tabloları farkındadır ve görüntülemek ve bunları indirmek sağlayacak bir araç kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e9b-140">Use a tool that is aware of these tables and will allow you to view and download them.</span></span>
* <span data-ttu-id="68e9b-141">Özel bir uygulama ya da okuma ve tabloları depolamak için komut dosyası yazma.</span><span class="sxs-lookup"><span data-stu-id="68e9b-141">Write a custom application or script to read and store the tables.</span></span>

<span data-ttu-id="68e9b-142">Çok sayıda üçüncü taraf araçları depolama gözatma bu tabloları farkında olduğundan ve doğrudan görüntülemenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="68e9b-142">Many third-party storage-browsing tools are aware of these tables and enable you to view them directly.</span></span>
<span data-ttu-id="68e9b-143">Lütfen bakın [Azure Storage istemci araçları](storage-explorers.md) kullanılabilen araçlar listesi.</span><span class="sxs-lookup"><span data-stu-id="68e9b-143">Please see [Azure Storage Client Tools](storage-explorers.md) for a list of available tools.</span></span>

> [!NOTE]
> <span data-ttu-id="68e9b-144">Sürümüyle 0.8.0 başlangıç [Microsoft Azure Storage Gezgini](http://storageexplorer.com/), görüntüleyebilir ve analytics ölçümleri tabloları indirin.</span><span class="sxs-lookup"><span data-stu-id="68e9b-144">Starting with version 0.8.0 of the [Microsoft Azure Storage Explorer](http://storageexplorer.com/), you can view and download the analytics metrics tables.</span></span>
> 
> 

<span data-ttu-id="68e9b-145">Analytics tabloları programlı olarak erişmek için depolama hesabınızdaki tüm tabloları listelerseniz analytics tabloları görünmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="68e9b-145">In order to access the analytics tables programmatically, do note that the analytics tables do not appear if you list all the tables in your storage account.</span></span> <span data-ttu-id="68e9b-146">Doğrudan adıyla erişmesine veya kullanmak [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) tablo adları sorgulamak için .NET İstemci Kitaplığı'nda.</span><span class="sxs-lookup"><span data-stu-id="68e9b-146">You can either access them directly by name, or use the [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) in the .NET client library to query the table names.</span></span>

### <a name="hourly-metrics"></a><span data-ttu-id="68e9b-147">Saatlik ölçümleri</span><span class="sxs-lookup"><span data-stu-id="68e9b-147">Hourly metrics</span></span>
* <span data-ttu-id="68e9b-148">$MetricsHourPrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="68e9b-148">$MetricsHourPrimaryTransactionsBlob</span></span>
* <span data-ttu-id="68e9b-149">$MetricsHourPrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="68e9b-149">$MetricsHourPrimaryTransactionsTable</span></span>
* <span data-ttu-id="68e9b-150">$MetricsHourPrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="68e9b-150">$MetricsHourPrimaryTransactionsQueue</span></span>

### <a name="minute-metrics"></a><span data-ttu-id="68e9b-151">Dakika ölçümleri</span><span class="sxs-lookup"><span data-stu-id="68e9b-151">Minute metrics</span></span>
* <span data-ttu-id="68e9b-152">$MetricsMinutePrimaryTransactionsBlob</span><span class="sxs-lookup"><span data-stu-id="68e9b-152">$MetricsMinutePrimaryTransactionsBlob</span></span>
* <span data-ttu-id="68e9b-153">$MetricsMinutePrimaryTransactionsTable</span><span class="sxs-lookup"><span data-stu-id="68e9b-153">$MetricsMinutePrimaryTransactionsTable</span></span>
* <span data-ttu-id="68e9b-154">$MetricsMinutePrimaryTransactionsQueue</span><span class="sxs-lookup"><span data-stu-id="68e9b-154">$MetricsMinutePrimaryTransactionsQueue</span></span>

### <a name="capacity"></a><span data-ttu-id="68e9b-155">Kapasite</span><span class="sxs-lookup"><span data-stu-id="68e9b-155">Capacity</span></span>
* <span data-ttu-id="68e9b-156">$MetricsCapacityBlob</span><span class="sxs-lookup"><span data-stu-id="68e9b-156">$MetricsCapacityBlob</span></span>

<span data-ttu-id="68e9b-157">Bu tablolar şemalardan tam Ayrıntılar bulabilirsiniz [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span><span class="sxs-lookup"><span data-stu-id="68e9b-157">You can find full details of the schemas for these tables at [Storage Analytics Metrics Table Schema](https://msdn.microsoft.com/library/azure/hh343264.aspx).</span></span> <span data-ttu-id="68e9b-158">Aşağıdaki örnek satır, yalnızca bir sütun alt kümesi kullanılabilir göster ancak bu ölçümleri Storage ölçümleri kaydeder şekilde önemli özelliklerinden bazıları gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="68e9b-158">The sample rows below show only a subset of the columns available, but illustrate some important features of the way Storage Metrics saves these metrics:</span></span>

| <span data-ttu-id="68e9b-159">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="68e9b-159">PartitionKey</span></span> | <span data-ttu-id="68e9b-160">RowKey</span><span class="sxs-lookup"><span data-stu-id="68e9b-160">RowKey</span></span> | <span data-ttu-id="68e9b-161">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="68e9b-161">Timestamp</span></span> | <span data-ttu-id="68e9b-162">TotalRequests</span><span class="sxs-lookup"><span data-stu-id="68e9b-162">TotalRequests</span></span> | <span data-ttu-id="68e9b-163">TotalBillableRequests</span><span class="sxs-lookup"><span data-stu-id="68e9b-163">TotalBillableRequests</span></span> | <span data-ttu-id="68e9b-164">Totalıngress</span><span class="sxs-lookup"><span data-stu-id="68e9b-164">TotalIngress</span></span> | <span data-ttu-id="68e9b-165">TotalEgress</span><span class="sxs-lookup"><span data-stu-id="68e9b-165">TotalEgress</span></span> | <span data-ttu-id="68e9b-166">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="68e9b-166">Availability</span></span> | <span data-ttu-id="68e9b-167">AverageE2ELatency</span><span class="sxs-lookup"><span data-stu-id="68e9b-167">AverageE2ELatency</span></span> | <span data-ttu-id="68e9b-168">AverageServerLatency</span><span class="sxs-lookup"><span data-stu-id="68e9b-168">AverageServerLatency</span></span> | <span data-ttu-id="68e9b-169">PercentSuccess</span><span class="sxs-lookup"><span data-stu-id="68e9b-169">PercentSuccess</span></span> |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="68e9b-170">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="68e9b-170">20140522T1100</span></span> |<span data-ttu-id="68e9b-171">Kullanıcı; Tüm</span><span class="sxs-lookup"><span data-stu-id="68e9b-171">user;All</span></span> |<span data-ttu-id="68e9b-172">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="68e9b-172">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="68e9b-173">7</span><span class="sxs-lookup"><span data-stu-id="68e9b-173">7</span></span> |<span data-ttu-id="68e9b-174">7</span><span class="sxs-lookup"><span data-stu-id="68e9b-174">7</span></span> |<span data-ttu-id="68e9b-175">4003</span><span class="sxs-lookup"><span data-stu-id="68e9b-175">4003</span></span> |<span data-ttu-id="68e9b-176">46801</span><span class="sxs-lookup"><span data-stu-id="68e9b-176">46801</span></span> |<span data-ttu-id="68e9b-177">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-177">100</span></span> |<span data-ttu-id="68e9b-178">104.4286</span><span class="sxs-lookup"><span data-stu-id="68e9b-178">104.4286</span></span> |<span data-ttu-id="68e9b-179">6.857143</span><span class="sxs-lookup"><span data-stu-id="68e9b-179">6.857143</span></span> |<span data-ttu-id="68e9b-180">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-180">100</span></span> |
| <span data-ttu-id="68e9b-181">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="68e9b-181">20140522T1100</span></span> |<span data-ttu-id="68e9b-182">Kullanıcı; QueryEntities</span><span class="sxs-lookup"><span data-stu-id="68e9b-182">user;QueryEntities</span></span> |<span data-ttu-id="68e9b-183">2014-05-22T11:01:16.7640250Z</span><span class="sxs-lookup"><span data-stu-id="68e9b-183">2014-05-22T11:01:16.7640250Z</span></span> |<span data-ttu-id="68e9b-184">5</span><span class="sxs-lookup"><span data-stu-id="68e9b-184">5</span></span> |<span data-ttu-id="68e9b-185">5</span><span class="sxs-lookup"><span data-stu-id="68e9b-185">5</span></span> |<span data-ttu-id="68e9b-186">2694</span><span class="sxs-lookup"><span data-stu-id="68e9b-186">2694</span></span> |<span data-ttu-id="68e9b-187">45951</span><span class="sxs-lookup"><span data-stu-id="68e9b-187">45951</span></span> |<span data-ttu-id="68e9b-188">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-188">100</span></span> |<span data-ttu-id="68e9b-189">143.8</span><span class="sxs-lookup"><span data-stu-id="68e9b-189">143.8</span></span> |<span data-ttu-id="68e9b-190">7.8</span><span class="sxs-lookup"><span data-stu-id="68e9b-190">7.8</span></span> |<span data-ttu-id="68e9b-191">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-191">100</span></span> |
| <span data-ttu-id="68e9b-192">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="68e9b-192">20140522T1100</span></span> |<span data-ttu-id="68e9b-193">Kullanıcı; QueryEntity</span><span class="sxs-lookup"><span data-stu-id="68e9b-193">user;QueryEntity</span></span> |<span data-ttu-id="68e9b-194">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="68e9b-194">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="68e9b-195">1</span><span class="sxs-lookup"><span data-stu-id="68e9b-195">1</span></span> |<span data-ttu-id="68e9b-196">1</span><span class="sxs-lookup"><span data-stu-id="68e9b-196">1</span></span> |<span data-ttu-id="68e9b-197">538</span><span class="sxs-lookup"><span data-stu-id="68e9b-197">538</span></span> |<span data-ttu-id="68e9b-198">633</span><span class="sxs-lookup"><span data-stu-id="68e9b-198">633</span></span> |<span data-ttu-id="68e9b-199">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-199">100</span></span> |<span data-ttu-id="68e9b-200">3</span><span class="sxs-lookup"><span data-stu-id="68e9b-200">3</span></span> |<span data-ttu-id="68e9b-201">3</span><span class="sxs-lookup"><span data-stu-id="68e9b-201">3</span></span> |<span data-ttu-id="68e9b-202">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-202">100</span></span> |
| <span data-ttu-id="68e9b-203">20140522T1100</span><span class="sxs-lookup"><span data-stu-id="68e9b-203">20140522T1100</span></span> |<span data-ttu-id="68e9b-204">Kullanıcı; UpdateEntity</span><span class="sxs-lookup"><span data-stu-id="68e9b-204">user;UpdateEntity</span></span> |<span data-ttu-id="68e9b-205">2014-05-22T11:01:16.7650250Z</span><span class="sxs-lookup"><span data-stu-id="68e9b-205">2014-05-22T11:01:16.7650250Z</span></span> |<span data-ttu-id="68e9b-206">1</span><span class="sxs-lookup"><span data-stu-id="68e9b-206">1</span></span> |<span data-ttu-id="68e9b-207">1</span><span class="sxs-lookup"><span data-stu-id="68e9b-207">1</span></span> |<span data-ttu-id="68e9b-208">771</span><span class="sxs-lookup"><span data-stu-id="68e9b-208">771</span></span> |<span data-ttu-id="68e9b-209">217</span><span class="sxs-lookup"><span data-stu-id="68e9b-209">217</span></span> |<span data-ttu-id="68e9b-210">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-210">100</span></span> |<span data-ttu-id="68e9b-211">9</span><span class="sxs-lookup"><span data-stu-id="68e9b-211">9</span></span> |<span data-ttu-id="68e9b-212">6</span><span class="sxs-lookup"><span data-stu-id="68e9b-212">6</span></span> |<span data-ttu-id="68e9b-213">100</span><span class="sxs-lookup"><span data-stu-id="68e9b-213">100</span></span> |

<span data-ttu-id="68e9b-214">Bu örnek dakika ölçümleri verilerde bölüm anahtarı süreyi dakika çözünürlükte kullanır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-214">In this example minute metrics data, the partition key uses the time at minute resolution.</span></span> <span data-ttu-id="68e9b-215">Satır anahtarını satır içinde depolanan bilgi türünü tanımlayan ve bu bilgileri, erişim türünü ve istek türü iki parça oluşur:</span><span class="sxs-lookup"><span data-stu-id="68e9b-215">The row key identifies the type of information that is stored in the row and this is composed of two pieces of information, the access type, and the request type:</span></span>

* <span data-ttu-id="68e9b-216">Access kullanıcı veya sistem, burada depolama birimi hizmeti tüm kullanıcı isteklerini kullanıcı başvurduğu ve depolama analizi tarafından yapılan istekleri sistem başvurduğu türüdür.</span><span class="sxs-lookup"><span data-stu-id="68e9b-216">The access type is either user or system, where user refers to all user requests to the storage service, and system refers to requests made by Storage Analytics.</span></span>
* <span data-ttu-id="68e9b-217">İstek bir Özet satırı tüm hangi durumda olduğu veya QueryEntity veya UpdateEntity gibi belirli API tanımlayan türüdür.</span><span class="sxs-lookup"><span data-stu-id="68e9b-217">The request type is either all in which case it is a summary line, or it identifies the specific API such as QueryEntity or UpdateEntity.</span></span>

<span data-ttu-id="68e9b-218">Yukarıdaki örnek verileri (11: 00'da başlayarak) tek bir dakika için tüm kayıtları gösterir, QueryEntities istek sayısı artı QueryEntity sayısı isteklerinin sayısı şekilde UpdateEntity kadar yedi, toplam olan eklemek ister kullanıcı: tüm satırda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="68e9b-218">The sample data above shows all the records for a single minute (starting at 11:00AM), so the number of QueryEntities requests plus the number of QueryEntity requests plus the number of UpdateEntity requests add up to seven, which is the total shown on the user:All row.</span></span> <span data-ttu-id="68e9b-219">Hesaplayarak kullanıcı: tüm satırda ortalama uçtan uca gecikme 104.4286 benzer şekilde, türetilemeyeceğini ((143.8 * 5) + 3 + 9) / 7.</span><span class="sxs-lookup"><span data-stu-id="68e9b-219">Similarly, you can derive the average end-to-end latency 104.4286 on the user:All row by calculating ((143.8 * 5) + 3 + 9)/7.</span></span>

## <a name="metrics-alerts"></a><span data-ttu-id="68e9b-220">Ölçümleri uyarıları</span><span class="sxs-lookup"><span data-stu-id="68e9b-220">Metrics alerts</span></span>
<span data-ttu-id="68e9b-221">Uyarıları Ayarlama göz önünde bulundurmanız gerekir [Azure portal](https://portal.azure.com) şekilde depolama ölçümleri otomatik olarak depolama hizmetlerinizi davranışlarındaki önemli değişiklikler hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-221">You should consider setting up alerts in the [Azure portal](https://portal.azure.com) so Storage Metrics can automatically notify you of important changes in the behavior of your storage services.</span></span> <span data-ttu-id="68e9b-222">Bu ölçüm verilerini sınırlandırılmış biçimde indirmek için bir Depolama Gezgini aracı kullanırsanız, Microsoft Excel verileri çözümlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e9b-222">If you use a storage explorer tool to download this metrics data in a delimited format, you can use Microsoft Excel to analyze the data.</span></span> <span data-ttu-id="68e9b-223">Bkz: [Azure Storage istemci araçları](storage-explorers.md) kullanılabilir Depolama Gezgini araçları listesi.</span><span class="sxs-lookup"><span data-stu-id="68e9b-223">See [Azure Storage Client Tools](storage-explorers.md) for a list of available storage explorer tools.</span></span> <span data-ttu-id="68e9b-224">Uyarılar yapılandırabilirsiniz **uyarı kuralları** dikey penceresinde, erişilebilir altında **izleme** depolama hesabı menü dikey.</span><span class="sxs-lookup"><span data-stu-id="68e9b-224">You can configure alerts in the **Alert rules** blade, accessible under **Monitoring** in the Storage account menu blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68e9b-225">Bir depolama olayı ve karşılık gelen saat veya dakika ölçüm verilerini ne zaman kaydedilir arasında bir gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-225">There may be a delay between a storage event and when the corresponding hourly or minute metrics data is recorded.</span></span> <span data-ttu-id="68e9b-226">Dakika ölçümleri söz konusu olduğunda, birkaç dakika veri aynı anda yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-226">In the case of minute metrics, several minutes of data may be written at once.</span></span> <span data-ttu-id="68e9b-227">Bu işlemler için geçerli dakikada hareket halinde toplanan önceki dakika neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-227">This can lead to transactions from earlier minutes being aggregated into the transaction for the current minute.</span></span> <span data-ttu-id="68e9b-228">Bu gerçekleştiğinde, uyarı hizmetini tüm kullanılabilir ölçüm verilerini beklenmedik bir şekilde tetikleme uyarıları açabilir yapılandırılmış uyarı aralığı olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-228">When this happens, the alert service may not have all available metrics data for the configured alert interval, which may lead to alerts firing unexpectedly.</span></span>
>

## <a name="accessing-metrics-data-programmatically"></a><span data-ttu-id="68e9b-229">Ölçüm verileri programlı olarak erişme</span><span class="sxs-lookup"><span data-stu-id="68e9b-229">Accessing metrics data programmatically</span></span>
<span data-ttu-id="68e9b-230">Aşağıdaki liste için bir aralığı dakika dakika ölçümleri erişir ve sonuçları bir konsol penceresi görüntüler örnek C# kodunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-230">The following listing shows sample C# code that accesses the minute metrics for a range of minutes and displays the results in a console Window.</span></span> <span data-ttu-id="68e9b-231">Azure Storage kitaplığı depolama ölçümleri tablolarda erişme basitleştirir CloudAnalyticsClient sınıfı içeren 4 sürümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-231">It uses the Azure Storage Library version 4 that includes the CloudAnalyticsClient class that simplifies accessing the metrics tables in storage.</span></span>

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a><span data-ttu-id="68e9b-232">Depolama ölçümleri etkinleştirdiğinizde, hangi, ücretlendirme?</span><span class="sxs-lookup"><span data-stu-id="68e9b-232">What charges do you incur when you enable storage metrics?</span></span>
<span data-ttu-id="68e9b-233">Tüm Azure depolama işlemleri için geçerli standart tarifelere ölçümleri için tablo varlıkları oluşturmak için istekler ücretlendirilen yazma.</span><span class="sxs-lookup"><span data-stu-id="68e9b-233">Write requests to create table entities for metrics are charged at the standard rates applicable to all Azure Storage operations.</span></span>

<span data-ttu-id="68e9b-234">Ölçüm verilerini bir istemci tarafından okuma ve silme istekleri de standart oranlarda faturalanabilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-234">Read and delete requests by a client to metrics data are also billable at standard rates.</span></span> <span data-ttu-id="68e9b-235">Bir veri bekletme ilkesi yapılandırdıysanız, Azure Storage eski ölçüm verileri sildiğinde, sizden ücret istenmese.</span><span class="sxs-lookup"><span data-stu-id="68e9b-235">If you have configured a data retention policy, you are not charged when Azure Storage deletes old metrics data.</span></span> <span data-ttu-id="68e9b-236">Ancak, analiz verileri silerseniz, hesabınızı silme işlemleri için ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-236">However, if you delete analytics data, your account is charged for the delete operations.</span></span>

<span data-ttu-id="68e9b-237">Ölçümleri tabloları tarafından kullanılan kapasitesi de Faturalanabilir: ölçüm verilerini depolamak için kullanılan kapasite miktarı tahmin etmek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="68e9b-237">The capacity used by the metrics tables is also billable: you can use the following to estimate the amount of capacity used for storing metrics data:</span></span>

* <span data-ttu-id="68e9b-238">Sonra her saat her hizmetin her API bir hizmet kullanırsa, hem hizmet hem de API düzey özeti etkinleştirdiyseniz, yaklaşık 148 KB veri saatte ölçümleri işlem tablolarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-238">If each hour a service utilizes every API in every service, then approximately 148KB of data is stored every hour in the metrics transaction tables if you have enabled both service and API level summary.</span></span>
* <span data-ttu-id="68e9b-239">Sonra her saat her hizmetin her API bir hizmet kullanırsa, yalnızca hizmet düzeyi Özet etkinleştirdiyseniz, yaklaşık olarak 12 KB veri saatte ölçümleri işlem tablolarda depolanır.</span><span class="sxs-lookup"><span data-stu-id="68e9b-239">If each hour a service utilizes every API in every service, then approximately 12KB of data is stored every hour in the metrics transaction tables if you have enabled just service level summary.</span></span>
* <span data-ttu-id="68e9b-240">BLOB'lar için kapasite tablosunda (kullanıcı, günlükleri için seçti sağlanan) her gün eklenen iki satır vardır: Bu her gün bu tablonun boyutunu tarafından yaklaşık 300 bayt kadar arttığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="68e9b-240">The capacity table for blobs has two rows added each day (provided user has opted in for logs): this implies that every day the size of this table increases by up to approximately 300 bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68e9b-241">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="68e9b-241">Next steps</span></span>
[<span data-ttu-id="68e9b-242">Günlüğe kaydetme ve günlük verilerine erişme depolama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="68e9b-242">Enabling Storage Logging and Accessing Log Data</span></span>](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
