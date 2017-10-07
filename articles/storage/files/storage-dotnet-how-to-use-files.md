---
title: ".NET ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop .NET uygulamalarını ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>.NET ile Azure Dosya depolama için geliştirme 
> [!NOTE]
> Bu makalede gösterilmektedir nasıl toomanage Azure File storage ile .NET kodu. Azure File storage hakkında daha fazla toolearn hello bakın [giriş tooAzure dosya depolama](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici .NET toodevelop uygulamaları ya da Azure File storage toostore dosya verilerini kullanan Hizmetleri kullanma temelleri hello gösterilmektedir. Bu öğreticide, basit bir konsol uygulaması oluşturur ve Göster nasıl .NET ve Azure File storage ile tooperform temel eylemleri:

* Merhaba bir dosyanın içeriğini alma
* Merhaba dosya paylaşımı için Hello kota (en fazla boyut) ayarlama.
* Merhaba paylaşımında tanımlı bir paylaşılan erişim ilkesi kullanan bir dosya için paylaşılan erişim imzası (SAS anahtarı) oluşturun.
* Hello tooanother dosyası kopyalamak aynı depolama hesabı.
* Bir dosya tooa blob hello kopyalama aynı depolama hesabı.
* Sorun giderme için Azure Storage Ölçümleri’ni kullanacağız.

> [!Note]  
> SMB üzerinden Azure File storage erişilebileceği için dosya g/ç için hello standart System.IO sınıflarını kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var. Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama .NET SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Merhaba konsol uygulaması oluşturun ve hello derleme alma
Visual Studio'da yeni bir Windows konsol uygulaması oluşturun. Aşağıdaki adımları hello nasıl toocreate bir konsol uygulaması Visual Studio 2017, ancak başlangıç adımları benzerdir diğer Visual Studio sürümlerinde gösterir.

1. **Dosya** > **Yeni** > **Proje**’yi seçin
2. **Yüklü** > **Şablonlar** > **Visual C#** > **Windows Klasik Masaüstü** öğesini seçin
3. **Konsol Uygulaması (.NET Framework)** öğesini seçin
4. Hello uygulamanız için bir ad girin **Name:** alanı
5. **Tamam**’ı seçin

Bu öğreticideki tüm kod örnekleri toohello eklenebilir `Main()` konsol uygulamanızın yöntemi `Program.cs` dosya.

Herhangi bir Azure bulut hizmeti veya web uygulaması dahil olmak üzere, .NET uygulaması ve Masaüstü ve mobil uygulamaları türünde hello Azure Storage istemci kitaplığı kullanabilirsiniz. Bu kılavuzda, sadeleştirmek için konsol uygulaması kullanmaktayız.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>NuGet tooinstall gerekli hello paketlerini kullanma
Bu öğretici, proje toocomplete tooreference gereken iki paket vardır:

* [.NET için Microsoft Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/): Bu paket depolama hesabınızdaki toodata kaynaklara programlı erişim sağlar.
* [.NET için Microsoft Azure Configuration Manager Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): Bu paket, uygulamanızın nerede çalıştığına bakmaksızın yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar.

Her iki paket NuGet tooobtain kullanabilirsiniz. Şu adımları uygulayın:

1. **Çözüm Gezgini**'nde projenize sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.
2. Çevrimiçi olarak "WindowsAzure.Storage" ifadesini arayın ve'ı tıklatın **yükleme** tooinstall hello depolama istemci kitaplığı ve bağımlılıklarını.
3. Çevrimiçi "WindowsAzure.ConfigurationManager" için arama ve tıklayın **yükleme** tooinstall hello Azure Yapılandırma Yöneticisi.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Depolama hesabı kimlik bilgileri toohello app.config dosyasını kaydedin
Sonraki adımda, kimlik bilgilerinizi projenizin app.config dosyasına kaydedin. Aşağıdaki örnek, değiştirme benzer toohello göründüğü şekilde hello app.config dosyasını düzenlemeniz `myaccount` , depolama hesabı adı ile ve `mykey` değerini depolama hesabınızın anahtarıyla.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> Azure File storage Hello hello Azure storage öykünücüsü en son sürümünü desteklemiyor. Bağlantı dizenizi Azure File storage ile Merhaba bulut toowork içinde Azure Storage hesabını hedeflemelidir.

## <a name="add-using-directives"></a>Using yönergeleri ekleme
Açık hello `Program.cs` dosya Çözüm Gezgini'nden ve hello aşağıdakileri ekleyin yönergeleri toohello dosyasının üst kısmında hello kullanarak.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Erişim hello dosya paylaşımı program aracılığıyla
Ardından, kod toohello aşağıdaki hello eklemek `Main()` yöntemi (sonra hello kodu yukarıda gösterilen) tooretrieve hello bağlantı dizesi. Bu kod, daha önce oluşturduğumuz başvuru toohello dosya alır ve içeriği toohello konsol penceresine çıkarır.

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

Merhaba konsol uygulaması toosee hello çıkışı çalıştırın.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Bir dosya paylaşımı için Hello maksimum boyutunu ayarlama
Sürümünden başlayarak hello Azure Storage istemci kitaplığı 5.x, ayarlayabileceğiniz kümesi hello kota (veya en büyük boyutu) bir dosya paylaşımı için gigabayt cinsinden. Ayrıca, ne kadar veri şu anda hello paylaşımında depolanan toosee kontrol edebilirsiniz.

Ayarı hello tarafından paylaşımı için kota bir, hello paylaşımında depolanan hello dosyaların toplam boyutu hello sınırlayabilirsiniz. Hello hello paylaşımdaki dosyaların toplam boyutu aşarsa hello kota hello paylaşımında ayarlayın, sonra istemcileri oluşturulamıyor tooincrease hello mevcut dosyaların boyutunu olabilir veya bu dosyaları boş olmadığı sürece, yeni dosyalar oluşturma.

Aşağıdaki örnek Hello nasıl toocheck hello bir paylaşım için geçerli kullanım ve nasıl tooset hello hello paylaşımı için kota gösterir.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Dosya veya dosya paylaşımı için paylaşılan erişim imzası oluşturma
Sürümünden başlayarak 5.x Merhaba Azure Storage istemci kitaplığı, paylaşılan erişim imzası (SAS) tek bir dosyayı veya dosya paylaşımı için oluşturabilirsiniz. Ayrıca, bir dosya paylaşımı toomanage paylaşılan erişim imzaları bir paylaşılan erişim ilkesi oluşturabilirsiniz. Tehlikeye girdiği durumlarda hello SAS iptal etme yolu sağladığı gibi bir paylaşılan erişim ilkesi oluşturmanız önerilir.

Aşağıdaki örneğine hello bir paylaşılan erişim ilkesi oluşturulur ve Itanium tabanlı sistemler için ilke tooprovide hello kısıtlamaları SAS için hello bir dosyada paylaşıma kullanır.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

Paylaşılan erişim imzaları oluşturma ve kullanma hakkında daha fazla bilgi edinmek için bkz. [Paylaşılan Erişim İmzaları (SAS) kullanma](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) ve [Azure Blobları ile SAS oluşturma ve kullanma](../blobs/storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Dosyaları kopyalama
Sürümünden başlayarak 5.x Merhaba Azure Storage istemci kitaplığı, tooanother dosyası, dosya tooa blob veya bir blobu tooa dosyayı kopyalayabilirsiniz. Merhaba sonraki bölümlerde, biz nasıl tooperform bu kopyalama göstermek işlemleri programlı olarak.

AzCopy toocopy bir dosya tooanother veya toocopy blob tooa dosya ya da tam tersini de kullanabilirsiniz. Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

> [!NOTE]
> Bir blob tooa dosyası veya dosya tooa blob kopyalıyorsanız aynı hello içinde kopyalama yapıyor olsanız bir paylaşılan erişim imzası (SAS) tooauthenticate hello kaynak nesnesi kullanmalısınız depolama hesabı.
> 
> 

**Bir dosya tooanother dosyasından kopyalama** hello aşağıdaki örnek tooanother dosyası hello kopyalar aynı. Bu kopyalama işlemi arasında kopyaladığından dosyalarında Merhaba aynı depolama hesabı, paylaşılan anahtar kimlik doğrulaması tooperform hello kopya kullanabilirsiniz.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**Bir dosya tooa blob kopyalama** hello aşağıdaki örnekte bir dosya oluşturur ve hello içinde tooa blob kopyalar aynı depolama hesabı. hangi hello hizmet hello kopyalama işlemi sırasında tooauthenticate erişim toohello kaynak dosyasını kullanır hello kaynak dosya için bir SAS Merhaba örneği oluşturur.

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

Hello bir blob tooa dosyaya kopyalayabilirsiniz aynı şekilde. Merhaba kaynak nesnesi bir blob ise, SAS tooauthenticate erişim toothat blob hello kopyalama işlemi sırasında oluşturun.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Ölçümleri kullanarak Azure Dosya depolama sorunlarını giderme
Artık Azure Depolama Analizi, Azure Dosya depolama için ölçümleri destekliyor. Ölçüm verilerini kullanarak istekleri ve tanılama sorunlarını izleyebilirsiniz.


Merhaba dan Azure File storage için ölçümleri etkinleştirebilirsiniz [Azure Portal](https://portal.azure.com). Program aracılığıyla arama hello hello REST API aracılığıyla dosya hizmeti özelliklerini ayarla işlemi ya da hello depolama istemci Kitaplığı'nda analoglarından biri tarafından ölçümleri etkinleştirebilirsiniz.


Aşağıdaki kod örneğine hello nasıl toouse hello depolama istemci kitaplığı Azure File storage için .NET tooenable ölçümleri için gösterir.

İlk olarak, hello aşağıdakileri ekleyin `using` yönergeleri tooyour `Program.cs` dosyası, ayrıca, eklediğiniz yukarıdaki toothose:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Kullanan Azure BLOB'ları, Azure Table ve Azure kuyrukları sırasında paylaşılan hello Not `ServiceProperties` hello türü `Microsoft.WindowsAzure.Storage.Shared.Protocol` ad alanı, Azure File storage kendi türünü kullandığını, hello `FileServiceProperties` hello türü `Microsoft.WindowsAzure.Storage.File.Protocol` ad alanı. Her iki ad alanı kodunuzdan, Bununla birlikte, kod toocompile aşağıdaki Merhaba başvurulmalıdır.

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

Ayrıca, çok başvuruda bulunabilir[Azure File storage sorun giderme makalesi](storage-troubleshoot-windows-file-connection-problems.md) uçtan uca sorun giderme kılavuzu için.

## <a name="next-steps"></a>Sonraki adımlar
Azure File Storage hakkında daha fazla bilgi edinmek için şu bağlantılara göz atın.

### <a name="conceptual-articles-and-videos"></a>Kavramsal makaleler ve videolar
* [Azure Dosya depolama: Windows ve Linux için uyumlu bulut SMB dosya sistemi](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Nasıl toouse Linux Azure File storage](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>File Storage için araç desteği
* [Nasıl toouse Microsoft Azure Storage ile AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Azure Storage ile Hello Azure CLI kullanma](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [Azure Dosya depolama sorunlarını giderme](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Başvuru
* [.NET başvurusu için Depolama İstemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Dosya Hizmeti REST API başvurusu](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Blog yazıları
* [Azure Dosya Depolama genel kullanıma sunulmuştur](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure Dosya depolama incelemesi](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure Dosya Hizmeti’ne Giriş](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Kalıcı bağlantılar tooMicrosoft Azure dosya depolama](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
