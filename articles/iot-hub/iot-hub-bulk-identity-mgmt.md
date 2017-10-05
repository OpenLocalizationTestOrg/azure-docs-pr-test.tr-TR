---
title: "Dışarı aktarma Azure IOT Hub cihaz kimlikleri alma | Microsoft Docs"
description: "İçeri ve dışarı cihaz kimliklerini kimlik kayıt defteri karşı toplu işlemleri gerçekleştirmek için Azure IOT hizmeti SDK'sını kullanma İçeri aktarma işlemleri oluşturma, güncelleştirme ve cihaz kimliklerini toplu silme olanak sağlar."
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
ms.openlocfilehash: ad2c6d585eef5450f7f0912ffa4753fe80d86b37
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a><span data-ttu-id="4da0b-104">IOT Hub cihaz kimliklerinizi toplu yönetme</span><span class="sxs-lookup"><span data-stu-id="4da0b-104">Manage your IoT Hub device identities in bulk</span></span>

<span data-ttu-id="4da0b-105">Her IOT hub kimlik kayıt defteri hizmeti aygıt başına kaynakları oluşturmak için kullanabilirsiniz sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-105">Each IoT hub has an identity registry you can use to create per-device resources in the service.</span></span> <span data-ttu-id="4da0b-106">Kimlik kayıt defteri aygıt'e yönelik uç noktalar için erişim denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="4da0b-106">The identity registry also enables you to control access to the device-facing endpoints.</span></span> <span data-ttu-id="4da0b-107">Bu makalede, alabilir ve toplu cihaz kimliklerini bir kimlik kayıt defterinden verin açıklar.</span><span class="sxs-lookup"><span data-stu-id="4da0b-107">This article describes how to import and export device identities in bulk to and from an identity registry.</span></span>

<span data-ttu-id="4da0b-108">İçeri ve dışarı aktarma işlemleri sürer bağlamında yerinde *işleri* IOT hub'ı karşı toplu hizmet işlemlerini yürütmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4da0b-108">Import and export operations take place in the context of *Jobs* that enable you to execute bulk service operations against an IoT hub.</span></span>

<span data-ttu-id="4da0b-109">**RegistryManager** sınıfı içerir **ExportDevicesAsync** ve **ImportDevicesAsync** kullanan yöntemleri **iş** framework.</span><span class="sxs-lookup"><span data-stu-id="4da0b-109">The **RegistryManager** class includes the **ExportDevicesAsync** and **ImportDevicesAsync** methods that use the **Job** framework.</span></span> <span data-ttu-id="4da0b-110">Bu yöntemler, verme, almak ve bir IOT hub kimlik kayıt defteri tamamen eşitlemek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4da0b-110">These methods enable you to export, import, and synchronize the entirety of an IoT hub identity registry.</span></span>

## <a name="what-are-jobs"></a><span data-ttu-id="4da0b-111">İşlerini nelerdir?</span><span class="sxs-lookup"><span data-stu-id="4da0b-111">What are jobs?</span></span>

<span data-ttu-id="4da0b-112">Kimlik kayıt defteri işlemlerini kullanmak **iş** sistem olduğunda işlemi:</span><span class="sxs-lookup"><span data-stu-id="4da0b-112">Identity registry operations use the **Job** system when the operation:</span></span>

* <span data-ttu-id="4da0b-113">Potansiyel olarak uzun yürütme zaman standart çalışma zamanı işlemleri karşılaştırıldığında.</span><span class="sxs-lookup"><span data-stu-id="4da0b-113">Has a potentially long execution time compared to standard run-time operations.</span></span>
* <span data-ttu-id="4da0b-114">Büyük miktarda veri kullanıcıya döndürür.</span><span class="sxs-lookup"><span data-stu-id="4da0b-114">Returns a large amount of data to the user.</span></span>

<span data-ttu-id="4da0b-115">İşlemi bekliyor veya işlem sonucu üzerinde engelleme tek bir API çağrısı yerine, zaman uyumsuz olarak oluşturur bir **iş** bu IOT hub'ın.</span><span class="sxs-lookup"><span data-stu-id="4da0b-115">Instead of a single API call waiting or blocking on the result of the operation, the operation asynchronously creates a **Job** for that IoT hub.</span></span> <span data-ttu-id="4da0b-116">İşlemi sonra hemen döndürür bir **JobProperties** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4da0b-116">The operation then immediately returns a **JobProperties** object.</span></span>

<span data-ttu-id="4da0b-117">Aşağıdaki C# kod parçacığını bir dışarı aktarma işinin oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-117">The following C# code snippet shows how to create an export job:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> <span data-ttu-id="4da0b-118">Kullanılacak **RegistryManager** sınıfı, C# kodunda, ekleme **Microsoft.Azure.Devices** NuGet paketini projenize.</span><span class="sxs-lookup"><span data-stu-id="4da0b-118">To use the **RegistryManager** class in your C# code, add the **Microsoft.Azure.Devices** NuGet package to your project.</span></span> <span data-ttu-id="4da0b-119">**RegistryManager** sınıfı olan **Microsoft.Azure.Devices** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="4da0b-119">The **RegistryManager** class is in the **Microsoft.Azure.Devices** namespace.</span></span>

<span data-ttu-id="4da0b-120">Kullanabileceğiniz **RegistryManager** durumunu sorgulamak için sınıf **iş** döndürülen kullanarak **JobProperties** meta verileri.</span><span class="sxs-lookup"><span data-stu-id="4da0b-120">You can use the **RegistryManager** class to query the state of the **Job** using the returned **JobProperties** metadata.</span></span>

<span data-ttu-id="4da0b-121">Aşağıdaki C# kod parçacığını işin yürütülmesi tamamlandı görmek için beş saniyede yoklamak gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-121">The following C# code snippet shows how to poll every five seconds to see if the job has finished executing:</span></span>

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

## <a name="export-devices"></a><span data-ttu-id="4da0b-122">Dışarı aktarma cihazları</span><span class="sxs-lookup"><span data-stu-id="4da0b-122">Export devices</span></span>

<span data-ttu-id="4da0b-123">Kullanım **ExportDevicesAsync** yöntemi bir IOT hub kimlik kayıt defterine tamamen dışarı aktarmak için bir [Azure Storage](../storage/index.md) blob kapsayıcısı kullanarak bir [paylaşılan erişim imzası](../storage/common/storage-security-guide.md#data-plane-security).</span><span class="sxs-lookup"><span data-stu-id="4da0b-123">Use the **ExportDevicesAsync** method to export the entirety of an IoT hub identity registry to an [Azure Storage](../storage/index.md) blob container using a [Shared Access Signature](../storage/common/storage-security-guide.md#data-plane-security).</span></span>

<span data-ttu-id="4da0b-124">Bu yöntem, sizin denetlediğiniz bir blob kapsayıcısında cihaz bilgilerinizi güvenilir yedeklerini oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4da0b-124">This method enables you to create reliable backups of your device information in a blob container that you control.</span></span>

<span data-ttu-id="4da0b-125">**ExportDevicesAsync** yöntemi iki parametre gerektirir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-125">The **ExportDevicesAsync** method requires two parameters:</span></span>

* <span data-ttu-id="4da0b-126">A *dize* blob kapsayıcısının bir URI içeriyor.</span><span class="sxs-lookup"><span data-stu-id="4da0b-126">A *string* that contains a URI of a blob container.</span></span> <span data-ttu-id="4da0b-127">Bu URI, kapsayıcıya yazma erişimi veren bir SAS belirteci içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-127">This URI must contain a SAS token that grants write access to the container.</span></span> <span data-ttu-id="4da0b-128">İş bir blok blobu serileştirilmiş verme aygıt verilerini depolamak için bu kapsayıcıda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4da0b-128">The job creates a block blob in this container to store the serialized export device data.</span></span> <span data-ttu-id="4da0b-129">SAS belirteci bu izinleri şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-129">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* <span data-ttu-id="4da0b-130">A *boolean* kimlik doğrulaması anahtarları, dışa aktarma verilerinin dışında tutmak isteyip istemediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-130">A *boolean* that indicates if you want to exclude authentication keys from your export data.</span></span> <span data-ttu-id="4da0b-131">Varsa **yanlış**, kimlik doğrulama anahtarları dışa aktarma çıktısında dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-131">If **false**, authentication keys are included in export output.</span></span> <span data-ttu-id="4da0b-132">Aksi takdirde, olarak anahtarları dışarı **null**.</span><span class="sxs-lookup"><span data-stu-id="4da0b-132">Otherwise, keys are exported as **null**.</span></span>

<span data-ttu-id="4da0b-133">Aşağıdaki C# kod parçacığını verme verilerde cihaz kimlik doğrulaması anahtarları içeren bir dışarı aktarma işini başlatmak nasıl gösterir ve tamamlanması için yoklama:</span><span class="sxs-lookup"><span data-stu-id="4da0b-133">The following C# code snippet shows how to initiate an export job that includes device authentication keys in the export data and then poll for completion:</span></span>

```csharp
// Call an export job on the IoT Hub to retrieve all devices
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

<span data-ttu-id="4da0b-134">İş çıktısı ada sahip bir blok blobu olarak sağlanan blob kapsayıcısında depolar **devices.txt**.</span><span class="sxs-lookup"><span data-stu-id="4da0b-134">The job stores its output in the provided blob container as a block blob with the name **devices.txt**.</span></span> <span data-ttu-id="4da0b-135">Çıktı verileri JSON seri hale getirilmiş aygıt verileri, satır başına bir aygıtla oluşur.</span><span class="sxs-lookup"><span data-stu-id="4da0b-135">The output data consists of JSON serialized device data, with one device per line.</span></span>

<span data-ttu-id="4da0b-136">Aşağıdaki örnek, çıktı verilerini gösterir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-136">The following example shows the output data:</span></span>

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Bir cihaz çifti veri varsa, twin verileri de aygıt verilerini birlikte verilir. Aşağıdaki örnekte bu biçimi gösterir. <span data-ttu-id="4da0b-139">"TwinETag" satırın sonuna kadar tüm veriler twin verilerdir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-139">All data from the "twinETag" line until the end are twin data.</span></span>

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

<span data-ttu-id="4da0b-140">Kodda bu verilere erişmesi gerekiyorsa, kolayca kullanarak bu verileri seri durumdan çıkarabiliyorsa **ExportImportDevice** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="4da0b-140">If you need access to this data in code, you can easily deserialize this data using the **ExportImportDevice** class.</span></span> <span data-ttu-id="4da0b-141">Aşağıdaki C# kod parçacığında, daha önce bir blok blobuna aktarılmış aygıt bilgileri okumak gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-141">The following C# code snippet shows how to read device information that was previously exported to a block blob:</span></span>

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
> <span data-ttu-id="4da0b-142">Aynı zamanda **GetDevicesAsync** yöntemi **RegistryManager** , cihazların bir listesini almak için sınıf.</span><span class="sxs-lookup"><span data-stu-id="4da0b-142">You can also use the **GetDevicesAsync** method of the **RegistryManager** class to fetch a list of your devices.</span></span> <span data-ttu-id="4da0b-143">Ancak, bu yaklaşım döndürülen cihaz nesnelerinin sayısı 1000 sabit sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-143">However, this approach has a hard cap of 1000 on the number of device objects that are returned.</span></span> <span data-ttu-id="4da0b-144">Beklenen kullanım durumu için **GetDevicesAsync** yöntemi hata ayıklama yardımcı olmak geliştirme senaryoları için ve üretim iş yükleri için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="4da0b-144">The expected use case for the **GetDevicesAsync** method is for development scenarios to aid debugging and is not recommended for production workloads.</span></span>

## <a name="import-devices"></a><span data-ttu-id="4da0b-145">Cihazları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="4da0b-145">Import devices</span></span>

<span data-ttu-id="4da0b-146">**ImportDevicesAsync** yönteminde **RegistryManager** sınıfı bir IOT hub kimlik kayıt defterinde toplu içeri aktarma ve eşitleme işlemleri gerçekleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4da0b-146">The **ImportDevicesAsync** method in the **RegistryManager** class enables you to perform bulk import and synchronization operations in an IoT hub identity registry.</span></span> <span data-ttu-id="4da0b-147">Gibi **ExportDevicesAsync** yöntemi, **ImportDevicesAsync** yöntemi kullanan **iş** framework.</span><span class="sxs-lookup"><span data-stu-id="4da0b-147">Like the **ExportDevicesAsync** method, the **ImportDevicesAsync** method uses the **Job** framework.</span></span>

<span data-ttu-id="4da0b-148">Kullanarak ilgilenebilmek **ImportDevicesAsync** yöntemi kimlik kayıt defterinizde yeni cihazları sağlamaya ek olarak, ayrıca güncelleştirme ve var olan cihazları silmek için.</span><span class="sxs-lookup"><span data-stu-id="4da0b-148">Take care using the **ImportDevicesAsync** method because in addition to provisioning new devices in your identity registry, it can also update and delete existing devices.</span></span>

> [!WARNING]
> <span data-ttu-id="4da0b-149">İçeri aktarma işlemi geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="4da0b-149">An import operation cannot be undone.</span></span> <span data-ttu-id="4da0b-150">Her zaman kullanarak var olan verileri yedekleme **ExportDevicesAsync** yöntemi toplu yapmadan önce başka bir blob kapsayıcısını, kimlik kayıt defterine değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-150">Always back up your existing data using the **ExportDevicesAsync** method to another blob container before you make bulk changes to your identity registry.</span></span>

<span data-ttu-id="4da0b-151">**ImportDevicesAsync** yöntemi iki parametre alır:</span><span class="sxs-lookup"><span data-stu-id="4da0b-151">The **ImportDevicesAsync** method takes two parameters:</span></span>

* <span data-ttu-id="4da0b-152">A *dize* bir URI'sini içeren bir [Azure Storage](../storage/index.md) olarak kullanılacak blob kapsayıcısı *giriş* işi.</span><span class="sxs-lookup"><span data-stu-id="4da0b-152">A *string* that contains a URI of an [Azure Storage](../storage/index.md) blob container to use as *input* to the job.</span></span> <span data-ttu-id="4da0b-153">Bu URI, kapsayıcı için okuma erişimi veren bir SAS belirteci içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-153">This URI must contain a SAS token that grants read access to the container.</span></span> <span data-ttu-id="4da0b-154">Bu kapsayıcı ada sahip bir blob içermelidir **devices.txt** kimlik kayıt defterine alın serileştirilmiş cihaz verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-154">This container must contain a blob with the name **devices.txt** that contains the serialized device data to import into your identity registry.</span></span> <span data-ttu-id="4da0b-155">İçeri aktarma verileri aynı aygıt bilgileri içermelidir JSON biçiminde **ExportImportDevice** iş kullanır oluştururken bir **devices.txt** blob.</span><span class="sxs-lookup"><span data-stu-id="4da0b-155">The import data must contain device information in the same JSON format that the **ExportImportDevice** job uses when it creates a **devices.txt** blob.</span></span> <span data-ttu-id="4da0b-156">SAS belirteci bu izinleri şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-156">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* <span data-ttu-id="4da0b-157">A *dize* bir URI'sini içeren bir [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) olarak kullanılacak blob kapsayıcısı *çıkış* işten.</span><span class="sxs-lookup"><span data-stu-id="4da0b-157">A *string* that contains a URI of an [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) blob container to use as *output* from the job.</span></span> <span data-ttu-id="4da0b-158">Bu kapsayıcıdaki tüm Tamamlanan alma işlemi hata bilgileri depolamak için bir blok blobu işi oluşturur **iş**.</span><span class="sxs-lookup"><span data-stu-id="4da0b-158">The job creates a block blob in this container to store any error information from the completed import **Job**.</span></span> <span data-ttu-id="4da0b-159">SAS belirteci bu izinleri şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-159">The SAS token must include these permissions:</span></span>

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> <span data-ttu-id="4da0b-160">İki parametre blob kapsayıcıya işaret edebilir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-160">The two parameters can point to the same blob container.</span></span> <span data-ttu-id="4da0b-161">Ayrı parametreleri yalnızca verilerinizi üzerinde çıkış kapsayıcı ek izinler gerektirdiğinden daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="4da0b-161">The separate parameters simply enable more control over your data as the output container requires additional permissions.</span></span>

<span data-ttu-id="4da0b-162">Aşağıdaki C# kod parçacığında, bir içeri aktarma işlemini başlatmak gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-162">The following C# code snippet shows how to initiate an import job:</span></span>

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

<span data-ttu-id="4da0b-163">Bu yöntem, cihaz çiftinin veri almak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-163">This method can also be used to import the data for the device twin.</span></span> <span data-ttu-id="4da0b-164">Giriş veri biçimi gösterilen biçim aynıdır **ExportDevicesAsync** bölümü.</span><span class="sxs-lookup"><span data-stu-id="4da0b-164">The format for the data input is the same as the format shown in the **ExportDevicesAsync** section.</span></span> <span data-ttu-id="4da0b-165">Bu şekilde, dışarı aktarılan verileri yeniden alın.</span><span class="sxs-lookup"><span data-stu-id="4da0b-165">In this way, you can reimport the exported data.</span></span> <span data-ttu-id="4da0b-166">**$Metadata** isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-166">The **$metadata** is optional.</span></span>

## <a name="import-behavior"></a><span data-ttu-id="4da0b-167">Alma davranışı</span><span class="sxs-lookup"><span data-stu-id="4da0b-167">Import behavior</span></span>

<span data-ttu-id="4da0b-168">Kullanabileceğiniz **ImportDevicesAsync** yöntemi, kimlik kayıt defterinde aşağıdaki toplu işlemleri gerçekleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="4da0b-168">You can use the **ImportDevicesAsync** method to perform the following bulk operations in your identity registry:</span></span>

* <span data-ttu-id="4da0b-169">Yeni cihazların toplu kayıt</span><span class="sxs-lookup"><span data-stu-id="4da0b-169">Bulk registration of new devices</span></span>
* <span data-ttu-id="4da0b-170">Var olan cihazların toplu silme</span><span class="sxs-lookup"><span data-stu-id="4da0b-170">Bulk deletions of existing devices</span></span>
* <span data-ttu-id="4da0b-171">Toplu durum değişikliklerini (etkinleştirmek veya aygıtları devre dışı)</span><span class="sxs-lookup"><span data-stu-id="4da0b-171">Bulk status changes (enable or disable devices)</span></span>
* <span data-ttu-id="4da0b-172">Yeni cihaz kimlik doğrulama anahtarlarının toplu atama</span><span class="sxs-lookup"><span data-stu-id="4da0b-172">Bulk assignment of new device authentication keys</span></span>
* <span data-ttu-id="4da0b-173">Otomatik yeniden üretme cihaz kimlik doğrulama anahtarlarının toplu</span><span class="sxs-lookup"><span data-stu-id="4da0b-173">Bulk auto-regeneration of device authentication keys</span></span>
* <span data-ttu-id="4da0b-174">Toplu güncelleştirme twin veri</span><span class="sxs-lookup"><span data-stu-id="4da0b-174">Bulk update of twin data</span></span>

<span data-ttu-id="4da0b-175">Tek bir önceki işlemleri herhangi bir birleşimini gerçekleştirebilir **ImportDevicesAsync** çağırın.</span><span class="sxs-lookup"><span data-stu-id="4da0b-175">You can perform any combination of the preceding operations within a single **ImportDevicesAsync** call.</span></span> <span data-ttu-id="4da0b-176">Örneğin, yeni cihazları kaydetmek ve silebilir veya aynı anda var olan cihazları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4da0b-176">For example, you can register new devices and delete or update existing devices at the same time.</span></span> <span data-ttu-id="4da0b-177">İle birlikte kullanıldığında **ExportDevicesAsync** yöntemi, tamamen tüm aygıtlar bir IOT hub'ından diğerine geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4da0b-177">When used along with the **ExportDevicesAsync** method, you can completely migrate all your devices from one IoT hub to another.</span></span>

<span data-ttu-id="4da0b-178">İçeri aktarma dosyası twin meta veri içeriyorsa, bu meta veriler varolan twin meta verileri üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="4da0b-178">If the import file includes twin metadata, then this metadata overwrites the existing twin metadata.</span></span> <span data-ttu-id="4da0b-179">İçeri aktarma dosyası twin meta veriler, ardından yalnızca içermez varsa `lastUpdateTime` meta veriler, geçerli saati kullanılarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-179">If the import file does not include twin metadata, then only the `lastUpdateTime` metadata is updated using the current time.</span></span>

<span data-ttu-id="4da0b-180">İsteğe bağlı kullanmak **importMode** içeri aktarma işlemi cihaz başına denetlemek için her cihaz için seri hale getirme veri içeri aktar özelliği.</span><span class="sxs-lookup"><span data-stu-id="4da0b-180">Use the optional **importMode** property in the import serialization data for each device to control the import process per-device.</span></span> <span data-ttu-id="4da0b-181">**İmportMode** özelliği aşağıdaki seçenekler vardır:</span><span class="sxs-lookup"><span data-stu-id="4da0b-181">The **importMode** property has the following options:</span></span>

| <span data-ttu-id="4da0b-182">importMode</span><span class="sxs-lookup"><span data-stu-id="4da0b-182">importMode</span></span> | <span data-ttu-id="4da0b-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4da0b-183">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4da0b-184">**createOrUpdate**</span><span class="sxs-lookup"><span data-stu-id="4da0b-184">**createOrUpdate**</span></span> |<span data-ttu-id="4da0b-185">Bir aygıt ile belirtilen yoksa **kimliği**, yeni kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="4da0b-185">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4da0b-186">Cihaz zaten varsa, varolan bilgileri olmadan regard için sağlanan giriş verilerle üzerine yazılır **ETag** değeri.</span><span class="sxs-lookup"><span data-stu-id="4da0b-186">If the device already exists, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br> <span data-ttu-id="4da0b-187">Kullanıcı, cihaz verileri birlikte twin verileri isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4da0b-187">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="4da0b-188">Twin'ın etag belirtilmişse, cihazın etag'den bağımsız olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-188">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="4da0b-189">Varolan twin'ın etag ile uyumsuzluğa ise, bir hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-189">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="4da0b-190">**oluşturmaya**</span><span class="sxs-lookup"><span data-stu-id="4da0b-190">**create**</span></span> |<span data-ttu-id="4da0b-191">Bir aygıt ile belirtilen yoksa **kimliği**, yeni kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="4da0b-191">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4da0b-192">Cihaz zaten varsa, bir hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-192">If the device already exists, an error is written to the log file.</span></span> <br> <span data-ttu-id="4da0b-193">Kullanıcı, cihaz verileri birlikte twin verileri isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4da0b-193">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="4da0b-194">Twin'ın etag belirtilmişse, cihazın etag'den bağımsız olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-194">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="4da0b-195">Varolan twin'ın etag ile uyumsuzluğa ise, bir hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-195">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="4da0b-196">**Güncelleştirme**</span><span class="sxs-lookup"><span data-stu-id="4da0b-196">**update**</span></span> |<span data-ttu-id="4da0b-197">Bir aygıt belirtilen ile zaten varsa **kimliği**, varolan bilgileri olmadan regard için sağlanan giriş verisi olarak üzerine **ETag** değeri.</span><span class="sxs-lookup"><span data-stu-id="4da0b-197">If a device already exists with the specified **id**, existing information is overwritten with the provided input data without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="4da0b-198">Cihaz yok, hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-198">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="4da0b-199">**updateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4da0b-199">**updateIfMatchETag**</span></span> |<span data-ttu-id="4da0b-200">Bir aygıt belirtilen ile zaten varsa **kimliği**, varolan bilgileri yalnızca varsa sağlanan girdi verileriyle üzerine bir **ETag** eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="4da0b-200">If a device already exists with the specified **id**, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="4da0b-201">Cihaz yok, hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-201">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="4da0b-202">Varsa bir **ETag** uyuşmazlığı, hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-202">If there is an **ETag** mismatch, an error is written to the log file.</span></span> |
| <span data-ttu-id="4da0b-203">**createOrUpdateIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4da0b-203">**createOrUpdateIfMatchETag**</span></span> |<span data-ttu-id="4da0b-204">Bir aygıt ile belirtilen yoksa **kimliği**, yeni kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="4da0b-204">If a device does not exist with the specified **id**, it is newly registered.</span></span> <br/><span data-ttu-id="4da0b-205">Cihaz zaten varsa, yalnızca varsa mevcut bilgileri sağlanan girdi verileriyle yazılır bir **ETag** eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="4da0b-205">If the device already exists, existing information is overwritten with the provided input data only if there is an **ETag** match.</span></span> <br/><span data-ttu-id="4da0b-206">Varsa bir **ETag** uyuşmazlığı, hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-206">If there is an **ETag** mismatch, an error is written to the log file.</span></span> <br> <span data-ttu-id="4da0b-207">Kullanıcı, cihaz verileri birlikte twin verileri isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4da0b-207">The user can optionally specify twin data along with the device data.</span></span> <span data-ttu-id="4da0b-208">Twin'ın etag belirtilmişse, cihazın etag'den bağımsız olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-208">The twin’s etag, if specified, is processed independently from the device’s etag.</span></span> <span data-ttu-id="4da0b-209">Varolan twin'ın etag ile uyumsuzluğa ise, bir hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-209">If there is a mismatch with the existing twin’s etag, an error is written to the log file.</span></span> |
| <span data-ttu-id="4da0b-210">**sil**</span><span class="sxs-lookup"><span data-stu-id="4da0b-210">**delete**</span></span> |<span data-ttu-id="4da0b-211">Bir aygıt belirtilen ile zaten varsa **kimliği**, olmadan regard için silinmiş **ETag** değeri.</span><span class="sxs-lookup"><span data-stu-id="4da0b-211">If a device already exists with the specified **id**, it is deleted without regard to the **ETag** value.</span></span> <br/><span data-ttu-id="4da0b-212">Cihaz yok, hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-212">If the device does not exist, an error is written to the log file.</span></span> |
| <span data-ttu-id="4da0b-213">**deleteIfMatchETag**</span><span class="sxs-lookup"><span data-stu-id="4da0b-213">**deleteIfMatchETag**</span></span> |<span data-ttu-id="4da0b-214">Bir aygıt belirtilen ile zaten varsa **kimliği**, yalnızca varsa silinmiş bir **ETag** eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="4da0b-214">If a device already exists with the specified **id**, it is deleted only if there is an **ETag** match.</span></span> <span data-ttu-id="4da0b-215">Cihaz yok, hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-215">If the device does not exist, an error is written to the log file.</span></span> <br/><span data-ttu-id="4da0b-216">Bir ETag uyuşmazlığı ise, bir hata günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="4da0b-216">If there is an ETag mismatch, an error is written to the log file.</span></span> |

> [!NOTE]
> <span data-ttu-id="4da0b-217">Serileştirme verileri açıkça tanımlamaz varsa bir **importMode** bayrağı için varsayılan bir aygıt için **createOrUpdate** içeri aktarma işlemi sırasında.</span><span class="sxs-lookup"><span data-stu-id="4da0b-217">If the serialization data does not explicitly define an **importMode** flag for a device, it defaults to **createOrUpdate** during the import operation.</span></span>

## <a name="import-devices-example--bulk-device-provisioning"></a><span data-ttu-id="4da0b-218">Aygıtları örnek alma – cihaz sağlamayı toplu</span><span class="sxs-lookup"><span data-stu-id="4da0b-218">Import devices example – bulk device provisioning</span></span>

<span data-ttu-id="4da0b-219">Aşağıdaki C# kod örneği birden çok aygıt kimlikleri oluşturmak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-219">The following C# code sample illustrates how to generate multiple device identities that:</span></span>

* <span data-ttu-id="4da0b-220">Kimlik doğrulama anahtarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="4da0b-220">Include authentication keys.</span></span>
* <span data-ttu-id="4da0b-221">Bu cihaz bilgileri bir blok blobuna yazma.</span><span class="sxs-lookup"><span data-stu-id="4da0b-221">Write that device information to a block blob.</span></span>
* <span data-ttu-id="4da0b-222">Cihaz kimlik kayıt defterine alın.</span><span class="sxs-lookup"><span data-stu-id="4da0b-222">Import the devices into the identity registry.</span></span>

```csharp
// Provision 1,000 more devices
var serializedDevices = new List<string>();

for (var i = 0; i < 1000; i++)
{
  // Create a new ExportImportDevice
  // CryptoKeyGenerator is in the Microsoft.Azure.Devices.Common namespace
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

  // Add device to the list
  serializedDevices.Add(JsonConvert.SerializeObject(deviceToAdd));
}

// Write the list to the blob
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

// Call import using the blob to add new devices
// Log information related to the job is written to the same container
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

## <a name="import-devices-example--bulk-deletion"></a><span data-ttu-id="4da0b-223">İçeri aktarma aygıtları örnek – toplu silme</span><span class="sxs-lookup"><span data-stu-id="4da0b-223">Import devices example – bulk deletion</span></span>

<span data-ttu-id="4da0b-224">Aşağıdaki kod örneği, yukarıdaki örnek kod kullanarak eklediğiniz cihazları silmek nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="4da0b-224">The following code sample shows you how to delete the devices you added using the previous code sample:</span></span>

```csharp
// Step 1: Update each device's ImportMode to be Delete
sb = new StringBuilder();
serializedDevices.ForEach(serializedDevice =>
{
  // Deserialize back to an ExportImportDevice
  var device = JsonConvert.DeserializeObject<ExportImportDevice>(serializedDevice);

  // Update property
  device.ImportMode = ImportMode.Delete;

  // Re-serialize
  sb.AppendLine(JsonConvert.SerializeObject(device));
});

// Step 2: Write the new import data back to the block blob
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

// Step 3: Call import using the same blob to delete all devices
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

## <a name="get-the-container-sas-uri"></a><span data-ttu-id="4da0b-225">Kapsayıcı SAS URI'sini Al</span><span class="sxs-lookup"><span data-stu-id="4da0b-225">Get the container SAS URI</span></span>

<span data-ttu-id="4da0b-226">Aşağıdaki kod örneği, nasıl oluşturulacağını gösterir bir [SAS URI'sini](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) okuma, yazma ve blob kapsayıcısı için izinleri Sil:</span><span class="sxs-lookup"><span data-stu-id="4da0b-226">The following code sample shows you how to generate a [SAS URI](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) with read, write, and delete permissions for a blob container:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
  // Set the expiry time and permissions for the container.
  // In this case no start time is specified, so the
  // shared access signature becomes valid immediately.
  var sasConstraints = new SharedAccessBlobPolicy();
  sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
  sasConstraints.Permissions = 
    SharedAccessBlobPermissions.Write | 
    SharedAccessBlobPermissions.Read | 
    SharedAccessBlobPermissions.Delete;

  // Generate the shared access signature on the container,
  // setting the constraints directly on the signature.
  string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

  // Return the URI string for the container,
  // including the SAS token.
  return container.Uri + sasContainerToken;
}
```

## <a name="next-steps"></a><span data-ttu-id="4da0b-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4da0b-227">Next steps</span></span>

<span data-ttu-id="4da0b-228">Bu makalede, bir IOT hub kimlik kayıt defteri karşı toplu işlemler gerçekleştirme öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="4da0b-228">In this article, you learned how to perform bulk operations against the identity registry in an IoT hub.</span></span> <span data-ttu-id="4da0b-229">Azure IOT hub'ı yönetme hakkında daha fazla bilgi için bu bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4da0b-229">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="4da0b-230">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="4da0b-230">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="4da0b-231">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="4da0b-231">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="4da0b-232">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="4da0b-232">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4da0b-233">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="4da0b-233">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="4da0b-234">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4da0b-234">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
