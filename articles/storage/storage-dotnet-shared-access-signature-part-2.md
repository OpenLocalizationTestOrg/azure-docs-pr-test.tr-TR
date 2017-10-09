---
title: "aaaCreate ve paylaşılan erişim imzası (SAS) ile Azure Blob storage kullanma | Microsoft Docs"
description: "Bu öğreticide toocreate Blob Depolama ile paylaşılan erişim imzası kullanmak için nasıl ve ne gösterilmiştir tooconsume istemci uygulamalarınızı bunları."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Paylaşılan erişim imzası, bölüm 2: Oluşturma ve bir SAS Blob storage'ı kullanma

[Bölüm 1](storage-dotnet-shared-access-signature-part-1.md) keşfedilen Bu öğretici paylaşılan erişim imzası (SAS) ve bunları kullanmak için en iyi uygulamalar açıklanmıştır. Bölüm 2 gösterilir nasıl toogenerate ve ardından paylaşılan erişim imzaları Blob storage ile. Merhaba örnekler C# dilinde yazılmıştır ve .NET için Azure Storage istemci kitaplığı hello kullanın. Bu öğreticide Hello örnekler:

* Üzerinde bir kapsayıcı paylaşılan erişim imzası oluşturma
* Blob üzerindeki paylaşılan erişim imzası oluşturma
* Depolanmış bir erişim ilkesi toomanage imzalar bir kapsayıcının kaynakları oluşturun.
* Bir istemci uygulamasında hello paylaşılan erişim imzaları test

## <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğreticide, oluşturma ve kapsayıcılar ve bloblar için paylaşılan erişim imzaları kullanma gösteren iki konsol uygulamaları oluşturun:

**Uygulama 1**: Merhaba yönetimi uygulaması. Bir kapsayıcı ve bir blob için bir paylaşılan erişim imzası oluşturur. Merhaba depolama hesabının erişim anahtarı kaynak kodunu içerir.

**Uygulama 2**: Merhaba istemci uygulaması. Merhaba ilk uygulaması ile oluşturulan hello paylaşılan erişim imzaları kullanarak erişse kapsayıcı ve blob kaynakları. Kullandığı yalnızca hello paylaşılan erişim imzaları tooaccess kapsayıcı ve blob kaynaklarını--mu *değil* hello depolama hesabının erişim anahtarı içerir.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>1. Kısım: bir konsol uygulaması toogenerate paylaşılan erişim imzaları oluşturma
İlk olarak, yüklü .NET için Azure Storage istemci kitaplığı hello olduğundan emin olun. Merhaba yükleyebilirsiniz [NuGet paketi](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet paketi") hello hello istemci kitaplığı için en güncel derlemelerini içeren. Merhaba yöntemi hello en son düzeltmelerin yüklü olmasını sağlamaya yönelik önerilen budur. Merhaba istemci kitaplığı hello hello en son sürümünü bir parçası olarak indirebilirsiniz [.NET için Azure SDK](https://azure.microsoft.com/downloads/).

Visual Studio'da yeni bir Windows konsol uygulaması oluşturun ve adlandırın **GenerateSharedAccessSignatures**. Başvuruları çok ekleyin[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) ve [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) hello aşağıdaki yaklaşımlardan birini kullanarak:

* Kullanım hello [NuGet Paket Yöneticisi](https://docs.nuget.org/consume/installing-nuget) Visual Studio. Seçin **proje** > **NuGet paketlerini Yönet**, her paket için (Microsoft.WindowsAzure.ConfigurationManager ve WindowsAzure.Storage) çevrimiçi olarak arayın ve yükleyin.
* Alternatif olarak, bu derlemeler hello Azure SDK'sı yüklemenizdeki bulun ve başvurular toothem ekleyin:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Merhaba Program.cs dosyasının Hello üstünde hello aşağıdakileri ekleyin **kullanarak** yönergeleri:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Bir yapılandırma ayarı noktaları tooyour depolama hesabını bir bağlantı dizesini içeren hello app.config dosyasını düzenleyin. App.config dosyasını benzer toothis bir görünmelidir:

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Bir kapsayıcı için bir paylaşılan erişim imzası URI oluşturma
toobegin ile yeni bir kapsayıcıda yöntemi toogenerate paylaşılan erişim imzası ekleriz. Bu durumda, hello imza depolanmış erişim ilkesi ile ilişkili değil, kendi bitiş saati ve hello izinleri gösteren URI hello bilgi hello üzerinde taşır şekilde verir.

İlk olarak, kod toohello ekleyin **Main()** yöntemi tooauthenticate erişim tooyour depolama hesabı ve yeni bir kapsayıcı oluşturun:

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

Ardından, hello paylaşılan erişim imzası hello kapsayıcısı için oluşturur ve hello imza URI döndüren bir yöntem ekleyin:

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Merhaba hello sonundaki satırlardan hello eklemek **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, toocall **GetContainerSasUri()** ve hello yazma İmza URI toohello konsol penceresi:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Derleme ve hello yeni kapsayıcı için toooutput hello paylaşılan erişim imzası URI çalıştırın. Merhaba URI benzer toohello şu olacaktır:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Merhaba kod çalıştırdıktan sonra hello paylaşılan erişim imzası hello kapsayıcısı için oluşturduğunuz sonraki 24 saat hello için geçerli olur. Merhaba imza izni toolist BLOB'lar hello kapsayıcı ve toowrite yeni BLOB'lar toohello kapsayıcı istemci verir.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Bir blob için bir paylaşılan erişim imzası URI oluşturma
Ardından, biz hello kapsayıcı içinde yeni bir blob benzer kodu toocreate yazma ve paylaşılan erişim imzası oluşturmak. Merhaba URI hello başlangıç zamanı, bitiş saati ve izin bilgileri içerecek şekilde bu paylaşılan erişim imzası depolanmış erişim ilkesi ile ilişkili değil.

Yeni bir blob oluşturur ve bazı metin tooit Yazar sonra paylaşılan erişim imzası oluşturur ve hello imza URI döndüren yeni bir yöntem ekleyin:

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Merhaba hello sonundaki **Main()** yöntemi, aşağıdaki satırları toocall hello eklemek **GetBlobSasUri()**, hello çağırmadan önce çok**Console.ReadLine()**ve paylaşılan hello yazma erişim imzası URI toohello konsol penceresi:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Derleme ve hello yeni blob için toooutput hello paylaşılan erişim imzası URI çalıştırın. Merhaba URI benzer toohello şu olacaktır:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Merhaba kapsayıcısında depolanmış erişim ilkesi oluşturma
Şimdi bir saklı erişim ilkesi kendisiyle ilişkilendirilmiş herhangi bir paylaşılan erişim imzaları hello kısıtlamalarını tanımlayacaksınız hello kapsayıcısı üzerinde oluşturalım.

Merhaba önceki örneklerde (örtük veya açık olarak) hello başlangıç saati belirtilmiş, paylaşılan erişim imzası URI kendisini hello sona erme saati ve hello hello izinleri. Örnek hello Biz bu depolanan hello erişim ilkesi, değil hello paylaşılan erişim imzası belirtin. Bize bunu sağlar yapmak toochange hello verilene olmadan bu kısıtlamaların paylaşılan erişim imzası.

Bir veya daha fazla hello paylaşılan erişim imzası hello kısıtlamalar ve depolanan hello erişim ilkesinde hello kalan olası toohave olur. Ancak, yalnızca hello başlangıç zamanı, bitiş saati ve izinleri bir yerde veya hello diğer belirtebilirsiniz. Örneğin, izinleri hello paylaşılan erişim imzası belirtmek ve ayrıca bunları depolanan hello erişim ilkesinde belirtin.

Saklı erişim ilkesi tooa kapsayıcısı eklediğinizde, hello kapsayıcının var olan izinleri almak, hello yeni Erişim İlkesi Ekle ve hello kapsayıcının izinlerini ayarlayın.

Bir kapsayıcıda yeni bir saklı erişim ilkesi oluşturur ve hello İlkesi hello adını döndüren yeni bir yöntem ekleyin:

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

Merhaba hello sonundaki **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, aşağıdaki hello satırları toofirst temizleyin varolan tüm erişim ilkeleri ekleyin ve hello çağrısı  **CreateSharedAccessPolicy()** yöntemi:

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

Bir kapsayıcı hello erişim ilkelerinin temizlediğinizde gerekir ilk hello kapsayıcının var olan izinleri sonra Temizle hello izinleri almak ve ardından yeniden hello izinlerini ayarlayın.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Paylaşılan erişim imzası bir erişim ilkesi kullanan hello kapsayıcısı üzerinde URI oluşturma
Ardından, daha önce oluşturduğumuz hello kapsayıcısı için başka bir paylaşılan erişim imzası oluşturuyoruz, ancak bu kez biz hello imza hello önceki örnekte oluşturduğumuz depolanan hello erişim ilkesi ile ilişkilendirin.

Yeni bir yöntem toogenerate hello kapsayıcısı için başka bir paylaşılan erişim imzası ekleyin:

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

Merhaba hello sonundaki **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, aşağıdaki satırları toocall hello hello eklemek **GetContainerSasUriWithPolicy** yöntemi :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Bir paylaşılan erişim imzası URI hello Blob kullandığı üzerinde bir erişim ilkesi oluştur
Son olarak, biz benzer bir yöntem toocreate başka bir blob ekleyin ve saklı erişim ilkesi ile ilişkili bir paylaşılan erişim imzası oluşturmak.

Yeni bir yöntem toocreate blob ekleyin ve bir paylaşılan erişim imzası oluştur:

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

Merhaba hello sonundaki **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, aşağıdaki satırları toocall hello hello eklemek **GetBlobSasUriWithPolicy** yöntemi:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Merhaba **Main()** yöntemi şimdi şöyle görünmelidir tamamının. Toowrite hello paylaşılan erişim imzası URI'ler toohello konsol penceresi, çalıştırın, sonra kopyalayın ve bunları bu öğreticinin ikinci bölümünde hello kullanmak için bir metin dosyasına yapıştırın.

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

Merhaba GenerateSharedAccessSignatures konsol uygulamasını çalıştırdığınızda, çıktı benzer toohello aşağıdaki görürsünüz. Merhaba öğreticinin Kısım 2'de kullanmak hello paylaşılan erişim imzaları bunlar.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>2. Kısım: bir konsol uygulaması tootest hello paylaşılan erişim imzaları oluşturma
paylaşılan erişim imzası hello önceki örneklerde oluşturulan tootest Merhaba, biz hello kapsayıcı ve blob hello imzaları tooperform işlemleri kullanır ikinci bir konsol uygulaması oluşturun.

> [!NOTE]
> Hello hello öğretici ilk kısmı tamamlandı beri 24 saatten fazla geçmişse, üretilen hello imzalar artık geçerli olacaktır. Bu durumda, hello kod hello ilk konsol uygulaması toogenerate içinde hello öğreticinin ikinci bölümünde hello kullanmak için yeni paylaşılan erişim imzaları çalıştırmanız gerekir.
>

Visual Studio'da yeni bir Windows konsol uygulaması oluşturun ve adlandırın **ConsumeSharedAccessSignatures**. Başvuruları çok ekleyin[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) ve [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), daha önce yaptığınız gibi.

Merhaba Program.cs dosyasının Hello üstünde hello aşağıdakileri ekleyin **kullanarak** yönergeleri:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Merhaba hello gövdesinde **Main()** yöntemi, dize sabitleri izleyerek, bölüm başlangıç Öğreticisi 1 oluşturulan kendi değerlerini toohello paylaşılan erişim imzaları değiştirme hello ekleyin.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Paylaşılan erişim imzası kullanarak bir yöntem tootry kapsayıcı işlem ekleme
Ardından, bazı kapsayıcı işlemleri için hello kapsayıcı paylaşılan erişim imzası kullanarak testleri bir yöntem ekleyin. Merhaba paylaşılan erişim imzası kullanılan tooreturn erişim toohello kapsayıcı tek başına hello imza tabanlı kimlik doğrulaması bir başvuru toohello kapsayıcı ' dir.

Yöntem tooProgram.cs aşağıdaki hello ekleyin:

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Güncelleştirme hello **Main()** yöntemi toocall **UseContainerSAS()** ikisi hello ile paylaşılan erişim imzası hello kapsayıcısında oluşturduğunuz:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Paylaşılan erişim imzası kullanarak bir yöntem tootry blobu işlemleri ekleme
Son olarak, hello blob'unda paylaşılan erişim imzası kullanarak bazı blobu işlemleri testleri bir yöntem ekleyin. Bu durumda, biz hello Oluşturucu kullanın **CloudBlockBlob(String)**, hello paylaşılan erişim imzası, tooreturn başvuru toohello blob geçen. Diğer kimlik doğrulaması gerekli değildir; İmza hello tek başına dayanır.

Yöntem tooProgram.cs aşağıdaki hello ekleyin:

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

Güncelleştirme hello **Main()** yöntemi toocall **UseBlobSAS()** hem hello hello blob üzerinde oluşturulan erişim imzaları paylaşılan:

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

Merhaba konsol uygulamasını çalıştırın ve hangi işlemleri hangi imzalar için izin verilen hello çıktı toosee gözlemleyin. Merhaba konsol penceresinde Hello çıkış benzer toohello aşağıdaki görünür:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Sonraki Adımlar

* [Paylaşılan erişim imzası, bölüm 1: hello SAS modelini anlama](storage-dotnet-shared-access-signature-part-1.md)
* [Anonim okuma erişimini toocontainers ve BLOB'ları yönetme](storage-manage-access-to-resources.md)
* [Paylaşılan erişim imzası (REST API) ile erişim için temsilci seçme](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Tablo ve kuyruk SAS Tanıtımı](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
