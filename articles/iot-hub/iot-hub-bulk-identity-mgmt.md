---
title: Azure IOT Hub cihaz kimlikleri aaaImport verme | Microsoft Docs
description: "Nasıl toouse hello Azure IOT hizmeti SDK tooperform hello kimlik kayıt defteri tooimport karşı işlemleri toplu ve cihaz kimliklerini dışa aktarın. İçeri aktarma işlemleri toocreate, güncelleştirme ve silme cihaz kimliklerini toplu etkinleştirin."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2ade1494-45ea-46a7-ade7-cf6e11ce62da
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b67777d381e03de05d9c007b5ce6bdaf15bbb8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="7372d-104">IOT Hub cihaz kimliklerinizi toplu yönetme</span><span class="sxs-lookup"><span data-stu-id="7372d-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="7372d-105">Her IOT hub kimlik kayıt defteri hello hizmetinde toocreate aygıt başına kaynakları kullanabilir sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7372d-105">Each IoT hub has an identity registry you can use toocreate per-device resources in hello service.</span></span> <span data-ttu-id="7372d-106">Merhaba kimlik kayıt defteri, toocontrol erişim toohello aygıt'e yönelik uç noktalar da sağlar.</span><span class="sxs-lookup"><span data-stu-id="7372d-106">hello identity registry also enables you toocontrol access toohello device-facing endpoints.</span></span> <span data-ttu-id="7372d-107">Bu makalede nasıl tooimport ve dışarı aktarma cihaz kimliklerini bir kimlik kayıt defterinden tooand toplu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7372d-107">This article describes how tooimport and export device identities in bulk tooand from an identity registry.</span></span>

<span data-ttu-id="7372d-108">İçeri ve dışarı aktarma işlemleri sürer Merhaba içeriğine yerinde *işleri* sağlamak tooexecute toplu hizmet işlemleri IOT hub'ı karşı.</span><span class="sxs-lookup"><span data-stu-id="7372d-108">Import and export operations take place in hello context of *Jobs* that enable you tooexecute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="7372d-109">Merhaba **RegistryManager** sınıfı içerir hello **ExportDevicesAsync** ve **ImportDevicesAsync** hello kullanan yöntemleri **iş** Çerçeve.</span><span class="sxs-lookup"><span data-stu-id="7372d-109">hello **RegistryManager** class includes hello **ExportDevicesAsync** and **ImportDevicesAsync** methods that use hello **Job** framework.</span></span> <span data-ttu-id="7372d-110">Bu yöntemler tooexport, alma, etkinleştirme ve bir IOT hub kimlik kayıt defteri hello tamamen eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="7372d-110">These methods enable you tooexport, import, and synchronize hello entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="7372d-111">İşlerini nelerdir?</span><span class="sxs-lookup"><span data-stu-id="7372d-111">What are jobs?</span></span>

<span data-ttu-id="7372d-112">Kimlik kayıt defteri işlemlerini kullanmak hello **iş** sistem zaman, işlemi hello:</span><span class="sxs-lookup"><span data-stu-id="7372d-112">Identity registry operations use hello **Job** system when hello operation:</span></span>

* <span data-ttu-id="7372d-113">Potansiyel olarak uzun yürütme zaman toostandard çalıştırma işlemleri karşılaştırıldığında.</span><span class="sxs-lookup"><span data-stu-id="7372d-113">Has a potentially long execution time compared toostandard run-time operations.</span></span>
* <span data-ttu-id="7372d-114">Çok miktarda veri toohello kullanıcı döndürür.</span><span class="sxs-lookup"><span data-stu-id="7372d-114">Returns a large amount of data toohello user.</span></span>

<span data-ttu-id="7372d-115">Merhaba işlemi bekliyor veya hello işlemi hello sonucunu engelleme tek bir API çağrısı yerine, zaman uyumsuz olarak oluşturur bir **iş** bu IOT hub'ın.</span><span class="sxs-lookup"><span data-stu-id="7372d-115">Instead of a single API call waiting or blocking on hello result of hello operation, hello operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="7372d-116">Merhaba işlemi sonra hemen döndürür bir **JobProperties** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7372d-116">hello operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="7372d-117">Aşağıdaki C# hello kod parçacığında gösterildiği nasıl toocreate bir dışarı aktarma işinin:</span><span class="sxs-lookup"><span data-stu-id="7372d-117">hello following C# code snippet shows how toocreate an export job:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="7372d-118">toouse hello **RegistryManager** sınıfı, C# kodunda, hello eklemek **Microsoft.Azure.Devices** NuGet paketi tooyour projesi.</span><span class="sxs-lookup"><span data-stu-id="7372d-118">toouse hello **RegistryManager** class in your C# code, add hello **Microsoft.Azure.Devices** NuGet package tooyour project.</span></span> <span data-ttu-id="7372d-119">Merhaba **RegistryManager** sınıftır hello **Microsoft.Azure.Devices** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="7372d-119">hello **RegistryManager** class is in hello **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="7372d-120">Merhaba kullanabilirsiniz **RegistryManager** sınıf tooquery hello hello durumunu **iş** döndürülen hello kullanarak **JobProperties** meta verileri.</span><span class="sxs-lookup"><span data-stu-id="7372d-120">You can use hello **RegistryManager** class tooquery hello state of hello **Job** using hello returned **JobProperties** metadata.</span></span>

<span data-ttu-id="7372d-121">Merhaba aşağıdaki C# kod parçacığını nasıl hello varsa her beş saniyede toosee iş toopoll yürütülmesi tamamlandı gösterir:</span><span class="sxs-lookup"><span data-stu-id="7372d-121">hello following C# code snippet shows how toopoll every five seconds toosee if hello job has finished executing:</span></span>

```csharp
// Wait until job is finished
while(true)
{
  exportJob = await registryManager.GetJobAsync(exportJob.JobId);
  if (exportJob.Status == JobStatus.Completed || 
      exportJob.Status == JobStatus.Failed ||
      exportJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="export-devices"></a><span data-ttu-id="7372d-122">Dışarı aktarma cihazları</span><span class="sxs-lookup"><span data-stu-id="7372d-122">Export devices</span></span>

<span data-ttu-id="7372d-123">Kullanım hello **ExportDevicesAsync** yöntemi tooexport hello tamamen bir IOT hub kimlik kayıt defteri tooan, [Azure Storage](../storage/index.md) blob kapsayıcısı kullanarak bir [paylaşılan erişim imzası](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="7372d-123">Use hello **ExportDevicesAsync** method tooexport hello entirety of an IoT hub identity registry tooan [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="7372d-124">Bu yöntem, sizin denetlediğiniz bir blob kapsayıcısında cihaz bilgilerinizi güvenilir yedeklerini toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="7372d-124">This method enables you toocreate reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="7372d-125">Merhaba **ExportDevicesAsync** yöntemi iki parametre gerektirir:</span><span class="sxs-lookup"><span data-stu-id="7372d-125">hello **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="7372d-126">A *dize* blob kapsayıcısının bir URI içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7372d-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="7372d-127">Bu URI yazma erişimi toohello kapsayıcı veren bir SAS belirteci içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7372d-127">This URI must contain a SAS token that grants write access toohello container.</span></span> <span data-ttu-id="7372d-128">Merhaba işi bir blok blobu bu kapsayıcı toostore serileştirilmiş hello verme aygıt verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7372d-128">hello job creates a block blob in this container toostore hello serialized export device data.</span></span> <span data-ttu-id="7372d-129">Merhaba SAS belirteci bu izinleri şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="7372d-129">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="7372d-130">A *boolean* belirten verme verilerinizden tooexclude kimlik doğrulaması anahtarları istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="7372d-130">A *boolean* that indicates if you want tooexclude authentication keys from your export data.</span></span> <span data-ttu-id="7372d-131">Varsa **yanlış**, kimlik doğrulama anahtarları dışa aktarma çıktısında dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="7372d-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="7372d-132">Aksi takdirde, olarak anahtarları dışarı **null**.</span><span class="sxs-lookup"><span data-stu-id="7372d-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="7372d-133">Merhaba aşağıdaki C# kod parçacığını nasıl tooinitiate hello cihaz kimlik doğrulaması anahtarları içeren bir dışarı aktarma işinin verileri dışarı aktarma ve tamamlamak için yoklama gösterir:</span><span class="sxs-lookup"><span data-stu-id="7372d-133">hello following C# code snippet shows how tooinitiate an export job that includes device authentication keys in hello export data and then poll for completion:</span></span>

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);

// Wait until job is finished
while(true)
{
    exportJob = await registryManager.GetJobAsync(exportJob.JobId);
    if (exportJob.Status == JobStatus.Completed || 
        exportJob.Status == JobStatus.Failed ||
        exportJob.Status == JobStatus.Cancelled)
    {
    // Job has finished executing
    break;
    }

    await Task.Delay(TimeSpan.FromSeconds(5));
}
```

<span data-ttu-id="7372d-134">Merhaba iş çıktısını sağlanan hello blob kapsayıcısında hello ada sahip bir blok blobu olarak depolar **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="7372d-134">hello job stores its output in hello provided blob container as a block blob with hello name **devices.txt**.</span></span> <span data-ttu-id="7372d-135">Merhaba çıktı verileri JSON seri hale getirilmiş aygıt verileri, satır başına bir aygıtla oluşur.</span><span class="sxs-lookup"><span data-stu-id="7372d-135">hello output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="7372d-136">Merhaba aşağıdaki örnek hello çıktı verilerini gösterir:</span><span class="sxs-lookup"><span data-stu-id="7372d-136">hello following example shows hello output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Bir cihaz çifti veri varsa, hello twin verileri de hello cihaz verileri ile birlikte verilir. Merhaba aşağıdaki örnekte bu biçimi gösterir. <span data-ttu-id="7372d-139">Tüm verileri hello son kadar hello "twinETag" satırından twin verilerdir.</span><span class="sxs-lookup"><span data-stu-id="7372d-139">All data from hello "twinETag" line until hello end are twin data.</span></span>

```json
{
   "id":"export-6d84f075-0",
   "eTag":"MQ==",
   "status":"enabled",
   "statusReason":"firstUpdate",
   "authentication":null,
   "twinETag":"AAAAAAAAAAI=",
   "tags":{
      "Location":"LivingRoom"
   },
   "properties":{
      "desired":{
         "Thermostat":{
            "Temperature":75.1,
            "Unit":"F"
         },
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
            "$lastUpdatedVersion":2,
            "Thermostat":{
               "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
               "$lastUpdatedVersion":2,
               "Temperature":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               },
               "Unit":{
                  "$lastUpdated":"2017-03-09T18:30:52.3167248Z",
                  "$lastUpdatedVersion":2
               }
            }
         },
         "$version":2
      },
      "reported":{
         "$metadata":{
            "$lastUpdated":"2017-03-09T18:30:51.1309437Z"
         },
         "$version":1
      }
   }
}
```

<span data-ttu-id="7372d-140">Kodda toothis veri erişim, hello kullanarak bu verileri kolayca seri durumdan çıkarabiliyorsa **ExportImportDevice** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7372d-140">If you need access toothis data in code, you can easily deserialize this data using hello **ExportImportDevice** class.</span></span> <span data-ttu-id="7372d-141">Merhaba aşağıdaki C# kod parçacığını nasıl edildi tooread aygıt bilgileri tooa blok blobu daha önce dışa gösterir:</span><span class="sxs-lookup"><span data-stu-id="7372d-141">hello following C# code snippet shows how tooread device information that was previously exported tooa block blob:</span></span>

```csharp
var exportedDevices = new List<ExportImportDevice>();

using (var streamReader = new StreamReader(await blob.OpenReadAsync(AccessCondition.GenerateIfExistsCondition(), null, null), Encoding.UTF8))
{
  while (streamReader.Peek() != -1)
  {
    string line = await streamReader.ReadLineAsync();
    var device = JsonConvert.DeserializeObject<ExportImportDevice>(line);
    exportedDevices.Add(device);
  }
}
```

> [!NOTE]
> <span data-ttu-id="7372d-142">Merhaba de kullanabilirsiniz **GetDevicesAsync** hello yöntemi **RegistryManager** sınıfı toofetch aygıtlarınızı listesi.</span><span class="sxs-lookup"><span data-stu-id="7372d-142">You can also use hello **GetDevicesAsync** method of hello **RegistryManager** class toofetch a list of your devices.</span></span> <span data-ttu-id="7372d-143">Ancak, bu yaklaşım döndürülen aygıt nesneleri hello sayısı 1000 sabit sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="7372d-143">However, this approach has a hard cap of 1000 on hello number of device objects that are returned.</span></span> <span data-ttu-id="7372d-144">Merhaba beklenen kullanım örneği hello için **GetDevicesAsync** yöntemi geliştirme senaryoları tooaid hata ayıklama ve üretim iş yükleri için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="7372d-144">hello expected use case for hello **GetDevicesAsync** method is for development scenarios tooaid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="7372d-145">Cihazları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="7372d-145">Import devices</span></span>

<span data-ttu-id="7372d-146">Merhaba **ImportDevicesAsync** hello yönteminde **RegistryManager** sınıfı tooperform toplu içeri aktarma ve eşitleme işlemlerinde bir IOT hub kimlik kayıt defteri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7372d-146">hello **ImportDevicesAsync** method in hello **RegistryManager** class enables you tooperform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="7372d-147">Hello gibi **ExportDevicesAsync** yöntemi, hello **ImportDevicesAsync** yöntemi kullanan hello **iş** framework.</span><span class="sxs-lookup"><span data-stu-id="7372d-147">Like hello **ExportDevicesAsync** method, hello **ImportDevicesAsync** method uses hello **Job** framework.</span></span>

<span data-ttu-id="7372d-148">Hello kullanarak ilgilenebilmek **ImportDevicesAsync** yöntemi toplama tooprovisioning yeni cihazları kimlik kayıt defterinizde, ayrıca güncelleştirme ve var olan cihazları silmek için.</span><span class="sxs-lookup"><span data-stu-id="7372d-148">Take care using hello **ImportDevicesAsync** method because in addition tooprovisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="7372d-149">İçeri aktarma işlemi geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="7372d-149">An import operation cannot be undone.</span></span> <span data-ttu-id="7372d-150">Her zaman hello kullanarak var olan verileri yedekleme **ExportDevicesAsync** toplu yapmadan önce yöntemi tooanother blob kapsayıcısı tooyour kimlik kayıt defteri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7372d-150">Always back up your existing data using hello **ExportDevicesAsync** method tooanother blob container before you make bulk changes tooyour identity registry.</span></span>

<span data-ttu-id="7372d-151">Merhaba **ImportDevicesAsync** yöntemi iki parametre alır:</span><span class="sxs-lookup"><span data-stu-id="7372d-151">hello **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="7372d-152">A *dize* bir URI'sini içeren bir [Azure Storage](../storage/index.md) kapsayıcı toouse olarak blob *giriş* toohello işi.</span><span class="sxs-lookup"><span data-stu-id="7372d-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container toouse as *input* toohello job.</span></span> <span data-ttu-id="7372d-153">Bu URI okuma erişimi toohello kapsayıcı veren bir SAS belirteci içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7372d-153">This URI must contain a SAS token that grants read access toohello container.</span></span> <span data-ttu-id="7372d-154">Bu kapsayıcı hello ada sahip bir blob içermelidir **devices.txt** , kimlik kayıt defterine serileştirilmiş hello aygıt veri tooimport içerir.</span><span class="sxs-lookup"><span data-stu-id="7372d-154">This container must contain a blob with hello name **devices.txt** that contains hello serialized device data tooimport into your identity registry.</span></span> <span data-ttu-id="7372d-155">Merhaba veri içeri aktarma aygıt bilgileri içermelidir hello aynı JSON biçiminde o hello **ExportImportDevice** iş kullanır oluştururken bir **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="7372d-155">hello import data must contain device information in hello same JSON format that hello **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="7372d-156">Merhaba SAS belirteci bu izinleri şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="7372d-156">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="7372d-157">A *dize* bir URI'sini içeren bir [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) kapsayıcı toouse olarak blob *çıkış* hello işten.</span><span class="sxs-lookup"><span data-stu-id="7372d-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container toouse as *output* from hello job.</span></span> <span data-ttu-id="7372d-158">Merhaba işi bir blok blobu bu kapsayıcı toostore hata bilgilerini tamamlandı hello alma oluşturur **iş**.</span><span class="sxs-lookup"><span data-stu-id="7372d-158">hello job creates a block blob in this container toostore any error information from hello completed import **Job**.</span></span> <span data-ttu-id="7372d-159">Merhaba SAS belirteci bu izinleri şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="7372d-159">hello SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="7372d-160">Merhaba iki parametreleri toohello noktası aynı blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7372d-160">hello two parameters can point toohello same blob container.</span></span> <span data-ttu-id="7372d-161">Hello ayrı parametreleri yalnızca verilerinizi üzerinde hello çıkış kapsayıcı ek izinler gerektirdiğinden daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="7372d-161">hello separate parameters simply enable more control over your data as hello output container requires additional permissions.</span></span>

<span data-ttu-id="7372d-162">Aşağıdaki C# hello kod parçacığında gösterildiği nasıl tooinitiate bir alma işi:</span><span class="sxs-lookup"><span data-stu-id="7372d-162">hello following C# code snippet shows how tooinitiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="7372d-163">Bu yöntem aynı zamanda hello cihaz çifti için kullanılan tooimport hello verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="7372d-163">This method can also be used tooimport hello data for hello device twin.</span></span> <span data-ttu-id="7372d-164">Merhaba veri girişi için Hello biçimi olan hello aynı hello gösterilen hello biçiminde **ExportDevicesAsync** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7372d-164">hello format for hello data input is hello same as hello format shown in hello **ExportDevicesAsync** section.</span></span> <span data-ttu-id="7372d-165">Bu şekilde, dışarı hello verileri yeniden alın.</span><span class="sxs-lookup"><span data-stu-id="7372d-165">In this way, you can reimport hello exported data.</span></span> <span data-ttu-id="7372d-166">Merhaba **$metadata** isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7372d-166">hello **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="7372d-167">Alma davranışı</span><span class="sxs-lookup"><span data-stu-id="7372d-167">Import behavior</span></span>

<span data-ttu-id="7372d-168">Merhaba kullanabilirsiniz **ImportDevicesAsync** yöntemi tooperform hello aşağıdaki toplu işlemleri kimlik kayıt defterinizde:</span><span class="sxs-lookup"><span data-stu-id="7372d-168">You can use hello **ImportDevicesAsync** method tooperform hello following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="7372d-169">Yeni cihazların toplu kayıt</span><span class="sxs-lookup"><span data-stu-id="7372d-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="7372d-170">Var olan cihazların toplu silme</span><span class="sxs-lookup"><span data-stu-id="7372d-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="7372d-171">Toplu durum değişikliklerini (etkinleştirmek veya aygıtları devre dışı)</span><span class="sxs-lookup"><span data-stu-id="7372d-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="7372d-172">Yeni cihaz kimlik doğrulama anahtarlarının toplu atama</span><span class="sxs-lookup"><span data-stu-id="7372d-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="7372d-173">Otomatik yeniden üretme cihaz kimlik doğrulama anahtarlarının toplu</span><span class="sxs-lookup"><span data-stu-id="7372d-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="7372d-174">Toplu güncelleştirme twin veri</span><span class="sxs-lookup"><span data-stu-id="7372d-174">Bulk update of twin data</span></span>

<span data-ttu-id="7372d-175">Tek bir işlemlerini önceki hello herhangi bir birleşimini gerçekleştirebilir **ImportDevicesAsync** çağırın.</span><span class="sxs-lookup"><span data-stu-id="7372d-175">You can perform any combination of hello preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="7372d-176">Örneğin, yeni cihazları kaydetmek ve silebilir veya var olan cihazların Merhaba adresindeki güncelleştirme aynı anda.</span><span class="sxs-lookup"><span data-stu-id="7372d-176">For example, you can register new devices and delete or update existing devices at hello same time.</span></span> <span data-ttu-id="7372d-177">Merhaba birlikte kullanıldığında **ExportDevicesAsync** yöntemi, bir IOT hub tooanother tüm aygıtlarınızın tamamen geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7372d-177">When used along with hello **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub tooanother.</span></span>

<span data-ttu-id="7372d-178">Merhaba içeri aktarma dosyası twin meta veri içeriyorsa, bu meta veriler hello varolan twin meta verileri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="7372d-178">If hello import file includes twin metadata, then this metadata overwrites hello existing twin metadata.</span></span> <span data-ttu-id="7372d-179">Merhaba içeri aktarma dosyası twin meta verileri içermiyorsa, yalnızca hello `lastUpdateTime` meta verileri, geçerli saati hello kullanılarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7372d-179">If hello import file does not include twin metadata, then only hello `lastUpdateTime` metadata is updated using hello current time.</span></span>

<span data-ttu-id="7372d-180">İsteğe bağlı kullanım hello **importMode** hello her aygıt toocontrol hello içeri aktarma işlemi cihaz başına için seri hale getirme veri içeri aktar özelliği.</span><span class="sxs-lookup"><span data-stu-id="7372d-180">Use hello optional **importMode** property in hello import serialization data for each device toocontrol hello import process per-device.</span></span> <span data-ttu-id="7372d-181">Merhaba **importMode** özelliğinin seçenekleri aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="7372d-181">hello **importMode** property has hello following options:</span></span>

| <span data-ttu-id="7372d-182">importMode</span><span class="sxs-lookup"><span data-stu-id="7372d-182">importMode</span></span> | <span data-ttu-id="7372d-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7372d-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7372d-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="7372d-184">**createOrUpdate**</span></span> |<span data-ttu-id="7372d-185">Bir aygıt ile belirtilen hello yoksa **kimliği**, yeni kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="7372d-185">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="7372d-186">Hello cihaz zaten varsa, varolan bilgi şekilde toohello olmadan giriş verisi sağlanan hello ile yazılır **ETag** değeri.</span><span class="sxs-lookup"><span data-stu-id="7372d-186">If hello device already exists, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br> <span data-ttu-id="7372d-187">Merhaba kullanıcı çifti veri hello cihaz verileri birlikte isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7372d-187">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="7372d-188">Hello twin'ın etag belirtilmişse hello cihazın etag'den bağımsız olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="7372d-188">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="7372d-189">Merhaba varolan twin'ın etag ile uyumsuzluğa ise, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-189">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="7372d-190">**oluşturmaya**</span><span class="sxs-lookup"><span data-stu-id="7372d-190">**create**</span></span> |<span data-ttu-id="7372d-191">Bir aygıt ile belirtilen hello yoksa **kimliği**, yeni kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="7372d-191">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="7372d-192">Merhaba cihaz zaten varsa, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-192">If hello device already exists, an error is written toohello log file.</span></span> <br> <span data-ttu-id="7372d-193">Merhaba kullanıcı çifti veri hello cihaz verileri birlikte isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7372d-193">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="7372d-194">Hello twin'ın etag belirtilmişse hello cihazın etag'den bağımsız olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="7372d-194">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="7372d-195">Merhaba varolan twin'ın etag ile uyumsuzluğa ise, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-195">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="7372d-196">**Güncelleştirme**</span><span class="sxs-lookup"><span data-stu-id="7372d-196">**update**</span></span> |<span data-ttu-id="7372d-197">Bir aygıt ile belirtilen hello zaten varsa **kimliği**, varolan bilgileri şekilde toohello olmadan giriş verisi sağlanan hello olarak üzerine **ETag** değeri.</span><span class="sxs-lookup"><span data-stu-id="7372d-197">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="7372d-198">Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-198">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="7372d-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="7372d-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="7372d-200">Bir aygıt ile belirtilen hello zaten varsa **kimliği**, varolan bilgileri yalnızca varsa giriş verisi sağlanan hello ile üzerine bir **ETag** eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="7372d-200">If a device already exists with hello specified **id**, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="7372d-201">Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-201">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="7372d-202">Varsa bir **ETag** uyuşmazlığı, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-202">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> |
| <span data-ttu-id="7372d-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="7372d-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="7372d-204">Bir aygıt ile belirtilen hello yoksa **kimliği**, yeni kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="7372d-204">If a device does not exist with hello specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="7372d-205">Hello cihaz zaten varsa, varolan bilgileri yalnızca varsa giriş verisi sağlanan hello ile üzerine bir **ETag** eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="7372d-205">If hello device already exists, existing information is overwritten with hello provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="7372d-206">Varsa bir **ETag** uyuşmazlığı, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-206">If there is an **ETag** mismatch, an error is written toohello log file.</span></span> <br> <span data-ttu-id="7372d-207">Merhaba kullanıcı çifti veri hello cihaz verileri birlikte isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7372d-207">hello user can optionally specify twin data along with hello device data.</span></span> <span data-ttu-id="7372d-208">Hello twin'ın etag belirtilmişse hello cihazın etag'den bağımsız olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="7372d-208">hello twin’s etag, if specified, is processed independently from hello device’s etag.</span></span> <span data-ttu-id="7372d-209">Merhaba varolan twin'ın etag ile uyumsuzluğa ise, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-209">If there is a mismatch with hello existing twin’s etag, an error is written toohello log file.</span></span> |
| <span data-ttu-id="7372d-210">**sil**</span><span class="sxs-lookup"><span data-stu-id="7372d-210">**delete**</span></span> |<span data-ttu-id="7372d-211">Bir aygıt ile belirtilen hello zaten varsa **kimliği**, bu hesaba toohello silinir **ETag** değeri.</span><span class="sxs-lookup"><span data-stu-id="7372d-211">If a device already exists with hello specified **id**, it is deleted without regard toohello **ETag** value.</span></span> <br/><span data-ttu-id="7372d-212">Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-212">If hello device does not exist, an error is written toohello log file.</span></span> |
| <span data-ttu-id="7372d-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="7372d-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="7372d-214">Bir aygıt ile belirtilen hello zaten varsa **kimliği**, yalnızca varsa silinmiş bir **ETag** eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="7372d-214">If a device already exists with hello specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="7372d-215">Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-215">If hello device does not exist, an error is written toohello log file.</span></span> <br/><span data-ttu-id="7372d-216">Bir ETag uyuşmazlığı ise, bir hata toohello günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7372d-216">If there is an ETag mismatch, an error is written toohello log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="7372d-217">Merhaba serileştirme verileri açıkça tanımlamaz varsa bir **importMode** bayrağı bir aygıt için çok varsayılan olarak**createOrUpdate** hello sırasında içeri aktarma işlemi.</span><span class="sxs-lookup"><span data-stu-id="7372d-217">If hello serialization data does not explicitly define an **importMode** flag for a device, it defaults too**createOrUpdate** during hello import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="7372d-218">Aygıtları örnek alma – cihaz sağlamayı toplu</span><span class="sxs-lookup"><span data-stu-id="7372d-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="7372d-219">Merhaba aşağıdaki C# kod örneği gösterilmektedir nasıl toogenerate birden çok aygıt kimlikleri:</span><span class="sxs-lookup"><span data-stu-id="7372d-219">hello following C# code sample illustrates how toogenerate multiple device identities that:</span></span>

* <span data-ttu-id="7372d-220">Kimlik doğrulama anahtarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7372d-220">Include authentication keys.</span></span>
* <span data-ttu-id="7372d-221">Bu cihaz bilgileri tooa blok blobu yazma.</span><span class="sxs-lookup"><span data-stu-id="7372d-221">Write that device information tooa block blob.</span></span>
* <span data-ttu-id="7372d-222">Merhaba aygıtları hello kimlik kayıt defterine alın.</span><span class="sxs-lookup"><span data-stu-id="7372d-222">Import hello devices into hello identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in hello Microsoft.Azure.Devices.Common namespace
  var deviceToAdd = new ExportImportDevice()
  {
    Id = Guid.NewGuid().ToString(),
    Status = DeviceStatus.Enabled,
    Authentication = new AuthenticationMechanism()
    {
      SymmetricKey = new SymmetricKey()
      {
        PrimaryKey = CryptoKeyGenerator.GenerateKey(32),
        SecondaryKey = CryptoKeyGenerator.GenerateKey(32)
      }
    },
    ImportMode = ImportMode.Create
  };

  // Add device toohello list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write hello list toohello blob
var sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice => sb.AppendLine(serializedDevice));
await blob.DeleteIfExistsAsync();

using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Call import using hello blob tooadd new devices
// Log information related toohello job is written toohello same container
// This normally takes 1 minute per 100 devices
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="7372d-223">İçeri aktarma aygıtları örnek – toplu silme</span><span class="sxs-lookup"><span data-stu-id="7372d-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="7372d-224">Merhaba aşağıdaki kod örneği, yukarıdaki örnek kod kullanılarak eklenen toodelete hello aygıtları nasıl hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="7372d-224">hello following code sample shows you how toodelete hello devices you added using hello previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode toobe Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back tooan ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write hello new import data back toohello block blob
await blob.DeleteIfExistsAsync();
using (CloudBlobStream stream = await blob.OpenWriteAsync())
{
  byte[] bytes = Encoding.UTF8.GetBytes(sb.ToString());
  for (var i = 0; i < bytes.Length; i += 500)
  {
    int length = Math.Min(bytes.Length - i, 500);
    await stream.WriteAsync(bytes, i, length);
  }
}

// Step 3: Call import using hello same blob toodelete all devices
importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);

// Wait until job is finished
while(true)
{
  importJob = await registryManager.GetJobAsync(importJob.JobId);
  if (importJob.Status == JobStatus.Completed || 
      importJob.Status == JobStatus.Failed ||
      importJob.Status == JobStatus.Cancelled)
  {
    // Job has finished executing
    break;
  }

  await Task.Delay(TimeSpan.FromSeconds(5));
}
```

## <a name="get-hello-container-sas-uri"></a><span data-ttu-id="7372d-225">Merhaba kapsayıcı SAS URI'sini Al</span><span class="sxs-lookup"><span data-stu-id="7372d-225">Get hello container SAS URI</span></span>

<span data-ttu-id="7372d-226">Merhaba aşağıdaki kod örneği, nasıl gösterir toogenerate bir [SAS URI'sini](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) okuma, yazma ve blob kapsayıcısı için izinleri Sil:</span><span class="sxs-lookup"><span data-stu-id="7372d-226">hello following code sample shows you how toogenerate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set hello expiry time and permissions for hello container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate hello shared access signature on hello container,
  // setting hello constraints directly on hello signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return hello URI string for hello container,
  // including hello SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="7372d-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7372d-227">Next steps</span></span>

<span data-ttu-id="7372d-228">Bu makalede, nasıl tooperform toplu işlemleri hello kimlik IOT hub'ı kayıt defterinde karşı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="7372d-228">In this article, you learned how tooperform bulk operations against hello identity registry in an IoT hub.</span></span> <span data-ttu-id="7372d-229">Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="7372d-229">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="7372d-230">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="7372d-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="7372d-231">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="7372d-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="7372d-232">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="7372d-232">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7372d-233">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="7372d-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="7372d-234">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7372d-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
