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
# <a name="manage-your-iot-hub-device-identities-in-bulk"></a>IOT Hub cihaz kimliklerinizi toplu yönetme

Her IOT hub kimlik kayıt defteri hello hizmetinde toocreate aygıt başına kaynakları kullanabilir sahiptir. Merhaba kimlik kayıt defteri, toocontrol erişim toohello aygıt'e yönelik uç noktalar da sağlar. Bu makalede nasıl tooimport ve dışarı aktarma cihaz kimliklerini bir kimlik kayıt defterinden tooand toplu açıklanmaktadır.

İçeri ve dışarı aktarma işlemleri sürer Merhaba içeriğine yerinde *işleri* sağlamak tooexecute toplu hizmet işlemleri IOT hub'ı karşı.

Merhaba **RegistryManager** sınıfı içerir hello **ExportDevicesAsync** ve **ImportDevicesAsync** hello kullanan yöntemleri **iş** Çerçeve. Bu yöntemler tooexport, alma, etkinleştirme ve bir IOT hub kimlik kayıt defteri hello tamamen eşitleyin.

## <a name="what-are-jobs"></a>İşlerini nelerdir?

Kimlik kayıt defteri işlemlerini kullanmak hello **iş** sistem zaman, işlemi hello:

* Potansiyel olarak uzun yürütme zaman toostandard çalıştırma işlemleri karşılaştırıldığında.
* Çok miktarda veri toohello kullanıcı döndürür.

Merhaba işlemi bekliyor veya hello işlemi hello sonucunu engelleme tek bir API çağrısı yerine, zaman uyumsuz olarak oluşturur bir **iş** bu IOT hub'ın. Merhaba işlemi sonra hemen döndürür bir **JobProperties** nesnesi.

Aşağıdaki C# hello kod parçacığında gösterildiği nasıl toocreate bir dışarı aktarma işinin:

```csharp
// Call an export job on hello IoT Hub tooretrieve all devices
JobProperties exportJob = await registryManager.ExportDevicesAsync(containerSasUri, false);
```

> [!NOTE]
> toouse hello **RegistryManager** sınıfı, C# kodunda, hello eklemek **Microsoft.Azure.Devices** NuGet paketi tooyour projesi. Merhaba **RegistryManager** sınıftır hello **Microsoft.Azure.Devices** ad alanı.

Merhaba kullanabilirsiniz **RegistryManager** sınıf tooquery hello hello durumunu **iş** döndürülen hello kullanarak **JobProperties** meta verileri.

Merhaba aşağıdaki C# kod parçacığını nasıl hello varsa her beş saniyede toosee iş toopoll yürütülmesi tamamlandı gösterir:

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

## <a name="export-devices"></a>Dışarı aktarma cihazları

Kullanım hello **ExportDevicesAsync** yöntemi tooexport hello tamamen bir IOT hub kimlik kayıt defteri tooan, [Azure Storage](../storage/index.md) blob kapsayıcısı kullanarak bir [paylaşılan erişim imzası](../storage/common/storage-security-guide.md#data-plane-security).

Bu yöntem, sizin denetlediğiniz bir blob kapsayıcısında cihaz bilgilerinizi güvenilir yedeklerini toocreate sağlar.

Merhaba **ExportDevicesAsync** yöntemi iki parametre gerektirir:

* A *dize* blob kapsayıcısının bir URI içeriyor. Bu URI yazma erişimi toohello kapsayıcı veren bir SAS belirteci içermesi gerekir. Merhaba işi bir blok blobu bu kapsayıcı toostore serileştirilmiş hello verme aygıt verilerini oluşturur. Merhaba SAS belirteci bu izinleri şunları içermelidir:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

* A *boolean* belirten verme verilerinizden tooexclude kimlik doğrulaması anahtarları istiyorsanız. Varsa **yanlış**, kimlik doğrulama anahtarları dışa aktarma çıktısında dahil edilir. Aksi takdirde, olarak anahtarları dışarı **null**.

Merhaba aşağıdaki C# kod parçacığını nasıl tooinitiate hello cihaz kimlik doğrulaması anahtarları içeren bir dışarı aktarma işinin verileri dışarı aktarma ve tamamlamak için yoklama gösterir:

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

Merhaba iş çıktısını sağlanan hello blob kapsayıcısında hello ada sahip bir blok blobu olarak depolar **devices.txt**. Merhaba çıktı verileri JSON seri hale getirilmiş aygıt verileri, satır başına bir aygıtla oluşur.

Merhaba aşağıdaki örnek hello çıktı verilerini gösterir:

```json
{"id":"Device1","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device2","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device3","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device4","eTag":"MA==","status":"disabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
{"id":"Device5","eTag":"MA==","status":"enabled","authentication":{"symmetricKey":{"primaryKey":"abc=","secondaryKey":"def="}}}
```

Bir cihaz çifti veri varsa, hello twin verileri de hello cihaz verileri ile birlikte verilir. Merhaba aşağıdaki örnekte bu biçimi gösterir. Tüm verileri hello son kadar hello "twinETag" satırından twin verilerdir.

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

Kodda toothis veri erişim, hello kullanarak bu verileri kolayca seri durumdan çıkarabiliyorsa **ExportImportDevice** sınıfı. Merhaba aşağıdaki C# kod parçacığını nasıl edildi tooread aygıt bilgileri tooa blok blobu daha önce dışa gösterir:

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
> Merhaba de kullanabilirsiniz **GetDevicesAsync** hello yöntemi **RegistryManager** sınıfı toofetch aygıtlarınızı listesi. Ancak, bu yaklaşım döndürülen aygıt nesneleri hello sayısı 1000 sabit sınır vardır. Merhaba beklenen kullanım örneği hello için **GetDevicesAsync** yöntemi geliştirme senaryoları tooaid hata ayıklama ve üretim iş yükleri için önerilmez.

## <a name="import-devices"></a>Cihazları içeri aktarma

Merhaba **ImportDevicesAsync** hello yönteminde **RegistryManager** sınıfı tooperform toplu içeri aktarma ve eşitleme işlemlerinde bir IOT hub kimlik kayıt defteri sağlar. Hello gibi **ExportDevicesAsync** yöntemi, hello **ImportDevicesAsync** yöntemi kullanan hello **iş** framework.

Hello kullanarak ilgilenebilmek **ImportDevicesAsync** yöntemi toplama tooprovisioning yeni cihazları kimlik kayıt defterinizde, ayrıca güncelleştirme ve var olan cihazları silmek için.

> [!WARNING]
> İçeri aktarma işlemi geri alınamaz. Her zaman hello kullanarak var olan verileri yedekleme **ExportDevicesAsync** toplu yapmadan önce yöntemi tooanother blob kapsayıcısı tooyour kimlik kayıt defteri değiştirir.

Merhaba **ImportDevicesAsync** yöntemi iki parametre alır:

* A *dize* bir URI'sini içeren bir [Azure Storage](../storage/index.md) kapsayıcı toouse olarak blob *giriş* toohello işi. Bu URI okuma erişimi toohello kapsayıcı veren bir SAS belirteci içermesi gerekir. Bu kapsayıcı hello ada sahip bir blob içermelidir **devices.txt** , kimlik kayıt defterine serileştirilmiş hello aygıt veri tooimport içerir. Merhaba veri içeri aktarma aygıt bilgileri içermelidir hello aynı JSON biçiminde o hello **ExportImportDevice** iş kullanır oluştururken bir **devices.txt** blob. Merhaba SAS belirteci bu izinleri şunları içermelidir:

   ```csharp
   SharedAccessBlobPermissions.Read
   ```
* A *dize* bir URI'sini içeren bir [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) kapsayıcı toouse olarak blob *çıkış* hello işten. Merhaba işi bir blok blobu bu kapsayıcı toostore hata bilgilerini tamamlandı hello alma oluşturur **iş**. Merhaba SAS belirteci bu izinleri şunları içermelidir:

   ```csharp
   SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Delete
   ```

> [!NOTE]
> Merhaba iki parametreleri toohello noktası aynı blob kapsayıcısı. Hello ayrı parametreleri yalnızca verilerinizi üzerinde hello çıkış kapsayıcı ek izinler gerektirdiğinden daha fazla denetim sağlar.

Aşağıdaki C# hello kod parçacığında gösterildiği nasıl tooinitiate bir alma işi:

```csharp
JobProperties importJob = await registryManager.ImportDevicesAsync(containerSasUri, containerSasUri);
```

Bu yöntem aynı zamanda hello cihaz çifti için kullanılan tooimport hello verileri olabilir. Merhaba veri girişi için Hello biçimi olan hello aynı hello gösterilen hello biçiminde **ExportDevicesAsync** bölümü. Bu şekilde, dışarı hello verileri yeniden alın. Merhaba **$metadata** isteğe bağlıdır.

## <a name="import-behavior"></a>Alma davranışı

Merhaba kullanabilirsiniz **ImportDevicesAsync** yöntemi tooperform hello aşağıdaki toplu işlemleri kimlik kayıt defterinizde:

* Yeni cihazların toplu kayıt
* Var olan cihazların toplu silme
* Toplu durum değişikliklerini (etkinleştirmek veya aygıtları devre dışı)
* Yeni cihaz kimlik doğrulama anahtarlarının toplu atama
* Otomatik yeniden üretme cihaz kimlik doğrulama anahtarlarının toplu
* Toplu güncelleştirme twin veri

Tek bir işlemlerini önceki hello herhangi bir birleşimini gerçekleştirebilir **ImportDevicesAsync** çağırın. Örneğin, yeni cihazları kaydetmek ve silebilir veya var olan cihazların Merhaba adresindeki güncelleştirme aynı anda. Merhaba birlikte kullanıldığında **ExportDevicesAsync** yöntemi, bir IOT hub tooanother tüm aygıtlarınızın tamamen geçirebilirsiniz.

Merhaba içeri aktarma dosyası twin meta veri içeriyorsa, bu meta veriler hello varolan twin meta verileri geçersiz kılar. Merhaba içeri aktarma dosyası twin meta verileri içermiyorsa, yalnızca hello `lastUpdateTime` meta verileri, geçerli saati hello kullanılarak güncelleştirilir.

İsteğe bağlı kullanım hello **importMode** hello her aygıt toocontrol hello içeri aktarma işlemi cihaz başına için seri hale getirme veri içeri aktar özelliği. Merhaba **importMode** özelliğinin seçenekleri aşağıdaki hello:

| importMode | Açıklama |
| --- | --- |
| **createOrUpdate** |Bir aygıt ile belirtilen hello yoksa **kimliği**, yeni kayıtlı. <br/>Hello cihaz zaten varsa, varolan bilgi şekilde toohello olmadan giriş verisi sağlanan hello ile yazılır **ETag** değeri. <br> Merhaba kullanıcı çifti veri hello cihaz verileri birlikte isteğe bağlı olarak belirtebilirsiniz. Hello twin'ın etag belirtilmişse hello cihazın etag'den bağımsız olarak işlenir. Merhaba varolan twin'ın etag ile uyumsuzluğa ise, bir hata toohello günlük dosyasına yazılır. |
| **oluşturmaya** |Bir aygıt ile belirtilen hello yoksa **kimliği**, yeni kayıtlı. <br/>Merhaba cihaz zaten varsa, bir hata toohello günlük dosyasına yazılır. <br> Merhaba kullanıcı çifti veri hello cihaz verileri birlikte isteğe bağlı olarak belirtebilirsiniz. Hello twin'ın etag belirtilmişse hello cihazın etag'den bağımsız olarak işlenir. Merhaba varolan twin'ın etag ile uyumsuzluğa ise, bir hata toohello günlük dosyasına yazılır. |
| **Güncelleştirme** |Bir aygıt ile belirtilen hello zaten varsa **kimliği**, varolan bilgileri şekilde toohello olmadan giriş verisi sağlanan hello olarak üzerine **ETag** değeri. <br/>Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır. |
| **updateIfMatchETag** |Bir aygıt ile belirtilen hello zaten varsa **kimliği**, varolan bilgileri yalnızca varsa giriş verisi sağlanan hello ile üzerine bir **ETag** eşleşmesi. <br/>Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır. <br/>Varsa bir **ETag** uyuşmazlığı, bir hata toohello günlük dosyasına yazılır. |
| **createOrUpdateIfMatchETag** |Bir aygıt ile belirtilen hello yoksa **kimliği**, yeni kayıtlı. <br/>Hello cihaz zaten varsa, varolan bilgileri yalnızca varsa giriş verisi sağlanan hello ile üzerine bir **ETag** eşleşmesi. <br/>Varsa bir **ETag** uyuşmazlığı, bir hata toohello günlük dosyasına yazılır. <br> Merhaba kullanıcı çifti veri hello cihaz verileri birlikte isteğe bağlı olarak belirtebilirsiniz. Hello twin'ın etag belirtilmişse hello cihazın etag'den bağımsız olarak işlenir. Merhaba varolan twin'ın etag ile uyumsuzluğa ise, bir hata toohello günlük dosyasına yazılır. |
| **sil** |Bir aygıt ile belirtilen hello zaten varsa **kimliği**, bu hesaba toohello silinir **ETag** değeri. <br/>Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır. |
| **deleteIfMatchETag** |Bir aygıt ile belirtilen hello zaten varsa **kimliği**, yalnızca varsa silinmiş bir **ETag** eşleşmesi. Merhaba aygıt mevcut değilse, bir hata toohello günlük dosyasına yazılır. <br/>Bir ETag uyuşmazlığı ise, bir hata toohello günlük dosyasına yazılır. |

> [!NOTE]
> Merhaba serileştirme verileri açıkça tanımlamaz varsa bir **importMode** bayrağı bir aygıt için çok varsayılan olarak**createOrUpdate** hello sırasında içeri aktarma işlemi.

## <a name="import-devices-example--bulk-device-provisioning"></a>Aygıtları örnek alma – cihaz sağlamayı toplu

Merhaba aşağıdaki C# kod örneği gösterilmektedir nasıl toogenerate birden çok aygıt kimlikleri:

* Kimlik doğrulama anahtarlarını içerir.
* Bu cihaz bilgileri tooa blok blobu yazma.
* Merhaba aygıtları hello kimlik kayıt defterine alın.

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

## <a name="import-devices-example--bulk-deletion"></a>İçeri aktarma aygıtları örnek – toplu silme

Merhaba aşağıdaki kod örneği, yukarıdaki örnek kod kullanılarak eklenen toodelete hello aygıtları nasıl hello gösterir:

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

## <a name="get-hello-container-sas-uri"></a>Merhaba kapsayıcı SAS URI'sini Al

Merhaba aşağıdaki kod örneği, nasıl gösterir toogenerate bir [SAS URI'sini](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md) okuma, yazma ve blob kapsayıcısı için izinleri Sil:

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

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, nasıl tooperform toplu işlemleri hello kimlik IOT hub'ı kayıt defterinde karşı öğrendiniz. Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:

* [IOT hub'ı ölçümleri][lnk-metrics]
* [İzleme işlemleri][lnk-monitor]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]

[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
