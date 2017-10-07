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
# <a name="enabling-azure-storage-metrics-and-viewing-metrics-data"></a>Azure Storage ölçümlerini etkinleştirme ve ölçüm verilerini görüntüleme
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Genel Bakış
Depolama ölçümleri, yeni bir depolama hesabı oluşturduğunuzda, varsayılan olarak etkindir. Merhaba izlemeyi yapılandırmadan [Azure portal](https://portal.azure.com) veya Windows PowerShell veya program aracılığıyla hello depolama istemci kitaplıklarından birini aracılığıyla.

Merhaba ölçüm verileri için bekletme süresi yapılandırabilirsiniz: Bu dönem için ne kadar süreyle hello depolama hizmeti hello ölçümleri ve sizin hello için boşluk gerekli toostore ücretleri tutar belirler bunları. Genellikle, daha kısa bir bekletme dönemi saatlik ölçümleri daha dakika ölçümünün hello önemli ek boşluk dakika ölçümlerini gerekli nedeniyle kullanmanız gerekir. Yeterli zaman tooanalyze hello veriniz varsa ve çevrimdışı analiz ve raporlama amacıyla tookeep istediğiniz ölçümleri karşıdan şekilde bir bekletme dönemi seçmeniz gerekir. Ayrıca ölçümleri veri depolama hesabınızdan indirme için Fatura edilecek olduğunu unutmayın.

## <a name="how-tooenable-metrics-using-hello-azure-portal"></a>Azure portal kullanarak tooenable ölçümleri nasıl hello
Bu adımları tooenable ölçümlerini hello izleyin [Azure portal](https://portal.azure.com):

1. Tooyour depolama hesabına gidin.
1. Seçin **tanılama** hello üzerinde **menü** dikey penceresi
1. Emin **durum** çok ayarlanır**üzerinde**.
1. Merhaba Hizmetleri için Select hello ölçümleri toomonitor istiyor.
1. Bir bekletme ilkesi tooindicate belirtin ne kadar süreyle tooretain ölçümleri ve günlük verileri.
1. **Kaydet**’i seçin.

Bu hello Not [Azure portal](https://portal.azure.com) şu anda tooconfigure minute ölçümleri; depolama hesabınızdaki etkinleştirmez PowerShell kullanarak dakika ölçümlerini etkinleştirmeniz gerekir veya program aracılığıyla.

## <a name="how-tooenable-metrics-using-powershell"></a>Nasıl tooenable ölçümleri PowerShell'i kullanma
PowerShell, LocalMachine tooconfigure Storage ölçümleri depolama hesabınızdaki hello Azure PowerShell cmdlet Get-AzureStorageServiceMetricsProperty tooretrieve hello geçerli ayarları kullanarak ve cmdlet hello Set-AzureStorageServiceMetricsProperty toochange hello geçerli ayarları.

Depolama Ölçümleri kontrol hello cmdlet'leri şu parametreler hello kullanın:

* MetricsType: olası saat ve dakika değerleri.
* ServiceType: Blob, kuyruk ve tablo olası değerler şunlardır.
* MetricsLevel: olası değerler, hizmeti ve ServiceAndApi yok.

Örneğin, hello aşağıdaki komutu hello hello bekletme süresi ile varsayılan depolama hesabınızdaki Blob hizmeti için ölçümleri toofive güne ayarlayabilir dakika üzerinde geçer:

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5`
```

Merhaba aşağıdaki komutu hello geçerli saatlik ölçümleri düzeyi ve saklama gün boyunca hello blob hizmeti varsayılan depolama hesabınızdaki alır:

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```

Nasıl toouse tooconfigure hello Azure PowerShell cmdlet'leri toowork Azure aboneliğinizle ve nasıl tooselect hello varsayılan depolama hesabı hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Nasıl tooenable Storage ölçümleri programlamayla
C# kod parçacığında aşağıdaki hello nasıl tooenable ölçümleri ve günlük hello Blob hizmeti kullandığınız için .NET için depolama istemci kitaplığı hello gösterir:

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

## <a name="viewing-storage-metrics"></a>Depolama ölçümleri görüntüleme
Depolama hesabınız Storage Analytics ölçümleri toomonitor yapılandırdıktan sonra depolama çözümlemeleri hello ölçümleri depolama hesabındaki iyi bilinen tablo kümesini kaydeder. Grafikler tooview saatlik ölçümleri hello yapılandırabilirsiniz [Azure portal](https://portal.azure.com):

1. Merhaba tooyour depolama hesabında gidin [Azure portal](https://portal.azure.com).
1. Seçin **ölçümleri** hello içinde **menü** dikey penceresinde hello için hizmet, ölçümleri tooview istiyor.
1. Seçin **Düzenle** hello grafikte tooconfigure istiyor.
1. Merhaba, **grafiği Düzenle** dikey penceresinde, select hello **zaman aralığı**, **grafik türü**ve görüntülenmesini istediğiniz hello grafikte hello ölçümleri.
1. **Tamam**’ı seçin

Toodownload hello ölçümleri istiyorsanız, uzun vadeli depolama veya tooanalyze için bunları yerel olarak yapmanız gerekir:

* Bu tabloları kullanan bir araç kullanın ve tooview izin vermek ve bunları yükleyebilirsiniz.
* Özel bir uygulama veya betik tooread yazma ve hello tabloları depolayın.

Çok sayıda üçüncü taraf araçları depolama gözatma bu tabloları farkında olduğundan ve tooview etkinleştirmek bunları doğrudan.
Lütfen bakın [Azure Storage istemci araçları](storage-explorers.md) kullanılabilen araçlar listesi.

> [!NOTE]
> Merhaba 0.8.0 sürümü ile başlayarak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/), görüntüleyebilir ve hello analytics ölçümleri tabloları indirin.
> 
> 

Sipariş tooaccess hello analizleri, depolama hesabınızı tüm hello tabloları listelerseniz hello analytics tabloları görünmez tablolar bir program aracılığıyla, unutmayın. Doğrudan adıyla erişmesine veya hello kullan [CloudAnalyticsClient API](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.analytics.cloudanalyticsclient.aspx) hello .NET istemci kitaplığı tooquery hello tablo adları.

### <a name="hourly-metrics"></a>Saatlik ölçümleri
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Dakika ölçümleri
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Kapasite
* $MetricsCapacityBlob

Bu tablolar hello şemaları tam ayrıntılarını bulabilirsiniz [Storage Analytics Ölçüm tablosu şeması](https://msdn.microsoft.com/library/azure/hh343264.aspx). altındaki Hello örnek satırları yalnızca bir sütun alt kümesi hello kullanılabilir Göster, ancak bu ölçümleri Storage ölçümleri kaydeder hello şekilde önemli özelliklerinden bazıları gösterilmektedir:

| PartitionKey | RowKey | zaman damgası | TotalRequests | TotalBillableRequests | Totalıngress | TotalEgress | Kullanılabilirlik | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |Kullanıcı; Tüm |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |Kullanıcı; QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |Kullanıcı; QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |Kullanıcı; UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

Bu örnek dakika ölçümleri verileri dakika çözünürlükte hello zaman hello bölüm anahtarı kullanır. Hello satır anahtarını hello hello satır için depolanan bilgi türünü tanımlayan ve bu bilgileri, hello erişim türünü ve hello istek türü iki parça oluşur:

* Merhaba erişim kullanıcı veya sistem burada kullanıcı tooall kullanıcı istekleri toohello depolama hizmeti anlamına gelir ve sistem depolama analizi tarafından yapılan toorequests başvuruyor türüdür.
* Merhaba istek türü, tüm durumda bir Özet satırı olan veya QueryEntity veya UpdateEntity gibi belirli API hello tanımlayan olur.

Merhaba örnek verileri yukarıda tüm hello gösterir (11: 00'da başlayarak) tek bir dakikadır QueryEntities istekleri bunu hello sayısını kaydeder artı hello QueryEntity istek sayısı artı UpdateEntity istek hello sayısı toplam gösterilen hello olduğu tooseven Yukarı Ekle Merhaba kullanıcı: tüm satır. Hesaplayarak hello ortalama uçtan uca gecikmesine 104.4286 hello kullanıcı: tüm satır benzer şekilde, türetilemeyeceğini ((143.8 * 5) + 3 + 9) / 7.

## <a name="metrics-alerts"></a>Ölçümleri uyarıları
Hello uyarıları ayarlama düşünmelisiniz [Azure portal](https://portal.azure.com) şekilde depolama ölçümleri otomatik olarak depolama hizmetlerinizi hello davranışlarındaki önemli değişiklikler hakkında bilgi edinebilirsiniz. Bu ölçüm verilerini bir sınırlandırılmış biçimde bir Depolama Gezgini aracı toodownload kullanırsanız, Microsoft Excel tooanalyze hello verilerini kullanabilirsiniz. Bkz: [Azure Storage istemci araçları](storage-explorers.md) kullanılabilir Depolama Gezgini araçları listesi. Uyarıları hello yapılandırabilirsiniz **uyarı kuralları** dikey penceresinde, erişilebilir altında **izleme** hello depolama hesabı menü dikey penceresinde.

> [!IMPORTANT]
> Bir depolama olayı ve saat veya dakika ölçüm verilerini karşılık gelen hello zaman kaydedilir arasında bir gecikme olabilir. Dakika ölçümleri Hello durumda birkaç dakika veri aynı anda yazılabilir. Bu tootransactions hello harekete hello için geçerli dakikada toplanan önceki dakika neden olabilir. Bu gerçekleştiğinde, hizmet hello tüm kullanılabilir ölçüm verilerini olmayabilir hello uyarı beklenmedik bir şekilde tetikleme tooalerts yol açabilir uyarı aralığı yapılandırılması.
>

## <a name="accessing-metrics-data-programmatically"></a>Ölçüm verileri programlı olarak erişme
Merhaba aşağıdaki kod hello dakika ölçümleri dakika cinsinden bir aralığı için erişir ve bir konsol penceresi hello sonuçları görüntüler örnek C# kodunu gösterir. Hello Azure Storage kitaplığı hello depolama erişilirken hello ölçümleri tablolarda basitleştirir CloudAnalyticsClient sınıfı içeren 4 sürümünü kullanır.

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

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Depolama ölçümleri etkinleştirdiğinizde, hangi, ücretlendirme?
İstekleri toocreate tablo varlıkları ölçümünün hello standart ücretler uygulanabilir tooall Azure depolama işlemleri sırasında ücretlendirilen yazma.

Bir istemci toometrics verilerini okuma ve silme istekleri de standart oranlarda faturalanabilir. Bir veri bekletme ilkesi yapılandırdıysanız, Azure Storage eski ölçüm verileri sildiğinde, sizden ücret istenmese. Ancak, analiz verileri silerseniz, hesabınızı hello silme işlemleri için ücret kesilir.

Merhaba ölçümleri tabloları tarafından kullanılan hello kapasitesi Faturalanabilir ayrıca: tooestimate hello ölçüm verilerini depolamak için kullanılan kapasite miktarı aşağıdaki hello kullanabilirsiniz:

* Sonra her saat her hizmetin her API bir hizmet kullanırsa, hem hizmet hem de API düzey özeti etkinleştirdiyseniz, yaklaşık 148 KB veri saatte hello ölçümleri işlem tablolarında depolanır.
* Sonra her saat her hizmetin her API bir hizmet kullanırsa, yalnızca hizmet düzeyi Özet etkinleştirdiyseniz, yaklaşık olarak 12 KB veri saatte hello ölçümleri işlem tablolarında depolanır.
* Hello BLOB'lar için kapasite tablosu sahip iki satır (kullanıcı, günlükleri için seçti sağlanan) her gün eklenen: Bu bu tablonun her günün hello boyutunu tarafından tooapproximately 300 bayt arttığını gösterir.

## <a name="next-steps"></a>Sonraki adımlar
[Günlüğe kaydetme ve günlük verilerine erişme depolama etkinleştirme](/rest/api/storageservices/Enabling-Storage-Logging-and-Accessing-Log-Data)
