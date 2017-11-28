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
ms.openlocfilehash: 32004d7d29a190a7ed7234513428c3c156b833b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="fec61-103">Paylaşılan erişim imzası, bölüm 2: Oluşturma ve bir SAS Blob storage'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="fec61-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="fec61-104">[Bölüm 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) keşfedilen Bu öğretici paylaşılan erişim imzası (SAS) ve bunları kullanmak için en iyi uygulamalar açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fec61-104">[Part 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="fec61-105">Bölüm 2 gösterilir nasıl toogenerate ve ardından paylaşılan erişim imzaları Blob storage ile.</span><span class="sxs-lookup"><span data-stu-id="fec61-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="fec61-106">Merhaba örnekler C# dilinde yazılmıştır ve .NET için Azure Storage istemci kitaplığı hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="fec61-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="fec61-107">Bu öğreticide Hello örnekler:</span><span class="sxs-lookup"><span data-stu-id="fec61-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="fec61-108">Üzerinde bir kapsayıcı paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="fec61-109">Blob üzerindeki paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="fec61-110">Depolanmış bir erişim ilkesi toomanage imzalar bir kapsayıcının kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fec61-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="fec61-111">Bir istemci uygulamasında hello paylaşılan erişim imzaları test</span><span class="sxs-lookup"><span data-stu-id="fec61-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="fec61-112">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="fec61-112">About this tutorial</span></span>
<span data-ttu-id="fec61-113">Bu öğreticide, oluşturma ve kapsayıcılar ve bloblar için paylaşılan erişim imzaları kullanma gösteren iki konsol uygulamaları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fec61-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="fec61-114">**Uygulama 1**: Merhaba yönetimi uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fec61-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="fec61-115">Bir kapsayıcı ve bir blob için bir paylaşılan erişim imzası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fec61-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="fec61-116">Merhaba depolama hesabının erişim anahtarı kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="fec61-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="fec61-117">**Uygulama 2**: Merhaba istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="fec61-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="fec61-118">Merhaba ilk uygulaması ile oluşturulan hello paylaşılan erişim imzaları kullanarak erişse kapsayıcı ve blob kaynakları.</span><span class="sxs-lookup"><span data-stu-id="fec61-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="fec61-119">Kullandığı yalnızca hello paylaşılan erişim imzaları tooaccess kapsayıcı ve blob kaynaklarını--mu *değil* hello depolama hesabının erişim anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="fec61-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="fec61-120">1. Kısım: bir konsol uygulaması toogenerate paylaşılan erişim imzaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="fec61-121">İlk olarak, yüklü .NET için Azure Storage istemci kitaplığı hello olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fec61-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="fec61-122">Merhaba yükleyebilirsiniz [NuGet paketi](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet paketi") hello hello istemci kitaplığı için en güncel derlemelerini içeren.</span><span class="sxs-lookup"><span data-stu-id="fec61-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="fec61-123">Merhaba yöntemi hello en son düzeltmelerin yüklü olmasını sağlamaya yönelik önerilen budur.</span><span class="sxs-lookup"><span data-stu-id="fec61-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="fec61-124">Merhaba istemci kitaplığı hello hello en son sürümünü bir parçası olarak indirebilirsiniz [.NET için Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fec61-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="fec61-125">Visual Studio'da yeni bir Windows konsol uygulaması oluşturun ve adlandırın **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="fec61-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="fec61-126">Başvuruları çok ekleyin[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) ve [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) hello aşağıdaki yaklaşımlardan birini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="fec61-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="fec61-127">Kullanım hello [NuGet Paket Yöneticisi](https://docs.nuget.org/consume/installing-nuget) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fec61-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="fec61-128">Seçin **proje** > **NuGet paketlerini Yönet**, her paket için (Microsoft.WindowsAzure.ConfigurationManager ve WindowsAzure.Storage) çevrimiçi olarak arayın ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fec61-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="fec61-129">Alternatif olarak, bu derlemeler hello Azure SDK'sı yüklemenizdeki bulun ve başvurular toothem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="fec61-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="fec61-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="fec61-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="fec61-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="fec61-132">Merhaba Program.cs dosyasının Hello üstünde hello aşağıdakileri ekleyin **kullanarak** yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="fec61-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="fec61-133">Bir yapılandırma ayarı noktaları tooyour depolama hesabını bir bağlantı dizesini içeren hello app.config dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="fec61-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="fec61-134">App.config dosyasını benzer toothis bir görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fec61-134">Your app.config file should look similar toothis one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="fec61-135">Bir kapsayıcı için bir paylaşılan erişim imzası URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="fec61-136">toobegin ile yeni bir kapsayıcıda yöntemi toogenerate paylaşılan erişim imzası ekleriz.</span><span class="sxs-lookup"><span data-stu-id="fec61-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="fec61-137">Bu durumda, hello imza depolanmış erişim ilkesi ile ilişkili değil, kendi bitiş saati ve hello izinleri gösteren URI hello bilgi hello üzerinde taşır şekilde verir.</span><span class="sxs-lookup"><span data-stu-id="fec61-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="fec61-138">İlk olarak, kod toohello ekleyin **Main()** yöntemi tooauthenticate erişim tooyour depolama hesabı ve yeni bir kapsayıcı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="fec61-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

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

<span data-ttu-id="fec61-139">Ardından, hello paylaşılan erişim imzası hello kapsayıcısı için oluşturur ve hello imza URI döndüren bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

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

<span data-ttu-id="fec61-140">Merhaba hello sonundaki satırlardan hello eklemek **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, toocall **GetContainerSasUri()** ve hello yazma İmza URI toohello konsol penceresi:</span><span class="sxs-lookup"><span data-stu-id="fec61-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="fec61-141">Derleme ve hello yeni kapsayıcı için toooutput hello paylaşılan erişim imzası URI çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fec61-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="fec61-142">Merhaba URI benzer toohello şu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="fec61-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="fec61-143">Merhaba kod çalıştırdıktan sonra hello paylaşılan erişim imzası hello kapsayıcısı için oluşturduğunuz sonraki 24 saat hello için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="fec61-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="fec61-144">Merhaba imza izni toolist BLOB'lar hello kapsayıcı ve toowrite yeni BLOB'lar toohello kapsayıcı istemci verir.</span><span class="sxs-lookup"><span data-stu-id="fec61-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="fec61-145">Bir blob için bir paylaşılan erişim imzası URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="fec61-146">Ardından, biz hello kapsayıcı içinde yeni bir blob benzer kodu toocreate yazma ve paylaşılan erişim imzası oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="fec61-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="fec61-147">Merhaba URI hello başlangıç zamanı, bitiş saati ve izin bilgileri içerecek şekilde bu paylaşılan erişim imzası depolanmış erişim ilkesi ile ilişkili değil.</span><span class="sxs-lookup"><span data-stu-id="fec61-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="fec61-148">Yeni bir blob oluşturur ve bazı metin tooit Yazar sonra paylaşılan erişim imzası oluşturur ve hello imza URI döndüren yeni bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

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

<span data-ttu-id="fec61-149">Merhaba hello sonundaki **Main()** yöntemi, aşağıdaki satırları toocall hello eklemek **GetBlobSasUri()**, hello çağırmadan önce çok**Console.ReadLine()**ve paylaşılan hello yazma erişim imzası URI toohello konsol penceresi:</span><span class="sxs-lookup"><span data-stu-id="fec61-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="fec61-150">Derleme ve hello yeni blob için toooutput hello paylaşılan erişim imzası URI çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fec61-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="fec61-151">Merhaba URI benzer toohello şu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="fec61-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="fec61-152">Merhaba kapsayıcısında depolanmış erişim ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="fec61-153">Şimdi bir saklı erişim ilkesi kendisiyle ilişkilendirilmiş herhangi bir paylaşılan erişim imzaları hello kısıtlamalarını tanımlayacaksınız hello kapsayıcısı üzerinde oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="fec61-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="fec61-154">Merhaba önceki örneklerde (örtük veya açık olarak) hello başlangıç saati belirtilmiş, paylaşılan erişim imzası URI kendisini hello sona erme saati ve hello hello izinleri.</span><span class="sxs-lookup"><span data-stu-id="fec61-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="fec61-155">Örnek hello Biz bu depolanan hello erişim ilkesi, değil hello paylaşılan erişim imzası belirtin.</span><span class="sxs-lookup"><span data-stu-id="fec61-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="fec61-156">Bize bunu sağlar yapmak toochange hello verilene olmadan bu kısıtlamaların paylaşılan erişim imzası.</span><span class="sxs-lookup"><span data-stu-id="fec61-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="fec61-157">Bir veya daha fazla hello paylaşılan erişim imzası hello kısıtlamalar ve depolanan hello erişim ilkesinde hello kalan olası toohave olur.</span><span class="sxs-lookup"><span data-stu-id="fec61-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="fec61-158">Ancak, yalnızca hello başlangıç zamanı, bitiş saati ve izinleri bir yerde veya hello diğer belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fec61-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="fec61-159">Örneğin, izinleri hello paylaşılan erişim imzası belirtmek ve ayrıca bunları depolanan hello erişim ilkesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="fec61-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="fec61-160">Saklı erişim ilkesi tooa kapsayıcısı eklediğinizde, hello kapsayıcının var olan izinleri almak, hello yeni Erişim İlkesi Ekle ve hello kapsayıcının izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fec61-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="fec61-161">Bir kapsayıcıda yeni bir saklı erişim ilkesi oluşturur ve hello İlkesi hello adını döndüren yeni bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

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

<span data-ttu-id="fec61-162">Merhaba hello sonundaki **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, aşağıdaki hello satırları toofirst temizleyin varolan tüm erişim ilkeleri ekleyin ve hello çağrısı  **CreateSharedAccessPolicy()** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="fec61-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

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

<span data-ttu-id="fec61-163">Bir kapsayıcı hello erişim ilkelerinin temizlediğinizde gerekir ilk hello kapsayıcının var olan izinleri sonra Temizle hello izinleri almak ve ardından yeniden hello izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fec61-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="fec61-164">Paylaşılan erişim imzası bir erişim ilkesi kullanan hello kapsayıcısı üzerinde URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="fec61-165">Ardından, daha önce oluşturduğumuz hello kapsayıcısı için başka bir paylaşılan erişim imzası oluşturuyoruz, ancak bu kez biz hello imza hello önceki örnekte oluşturduğumuz depolanan hello erişim ilkesi ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="fec61-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="fec61-166">Yeni bir yöntem toogenerate hello kapsayıcısı için başka bir paylaşılan erişim imzası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

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

<span data-ttu-id="fec61-167">Merhaba hello sonundaki **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, aşağıdaki satırları toocall hello hello eklemek **GetContainerSasUriWithPolicy** yöntemi :</span><span class="sxs-lookup"><span data-stu-id="fec61-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="fec61-168">Bir paylaşılan erişim imzası URI hello Blob kullandığı üzerinde bir erişim ilkesi oluştur</span><span class="sxs-lookup"><span data-stu-id="fec61-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="fec61-169">Son olarak, biz benzer bir yöntem toocreate başka bir blob ekleyin ve saklı erişim ilkesi ile ilişkili bir paylaşılan erişim imzası oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="fec61-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="fec61-170">Yeni bir yöntem toocreate blob ekleyin ve bir paylaşılan erişim imzası oluştur:</span><span class="sxs-lookup"><span data-stu-id="fec61-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

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

<span data-ttu-id="fec61-171">Merhaba hello sonundaki **Main()** hello çağırmadan önce çok yöntemi**Console.ReadLine()**, aşağıdaki satırları toocall hello hello eklemek **GetBlobSasUriWithPolicy** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="fec61-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="fec61-172">Merhaba **Main()** yöntemi şimdi şöyle görünmelidir tamamının.</span><span class="sxs-lookup"><span data-stu-id="fec61-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="fec61-173">Toowrite hello paylaşılan erişim imzası URI'ler toohello konsol penceresi, çalıştırın, sonra kopyalayın ve bunları bu öğreticinin ikinci bölümünde hello kullanmak için bir metin dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="fec61-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

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

<span data-ttu-id="fec61-174">Merhaba GenerateSharedAccessSignatures konsol uygulamasını çalıştırdığınızda, çıktı benzer toohello aşağıdaki görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fec61-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="fec61-175">Merhaba öğreticinin Kısım 2'de kullanmak hello paylaşılan erişim imzaları bunlar.</span><span class="sxs-lookup"><span data-stu-id="fec61-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="fec61-176">2. Kısım: bir konsol uygulaması tootest hello paylaşılan erişim imzaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="fec61-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="fec61-177">paylaşılan erişim imzası hello önceki örneklerde oluşturulan tootest Merhaba, biz hello kapsayıcı ve blob hello imzaları tooperform işlemleri kullanır ikinci bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fec61-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="fec61-178">Hello hello öğretici ilk kısmı tamamlandı beri 24 saatten fazla geçmişse, üretilen hello imzalar artık geçerli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fec61-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="fec61-179">Bu durumda, hello kod hello ilk konsol uygulaması toogenerate içinde hello öğreticinin ikinci bölümünde hello kullanmak için yeni paylaşılan erişim imzaları çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fec61-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="fec61-180">Visual Studio'da yeni bir Windows konsol uygulaması oluşturun ve adlandırın **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="fec61-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="fec61-181">Başvuruları çok ekleyin[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) ve [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), daha önce yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="fec61-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="fec61-182">Merhaba Program.cs dosyasının Hello üstünde hello aşağıdakileri ekleyin **kullanarak** yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="fec61-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="fec61-183">Merhaba hello gövdesinde **Main()** yöntemi, dize sabitleri izleyerek, bölüm başlangıç Öğreticisi 1 oluşturulan kendi değerlerini toohello paylaşılan erişim imzaları değiştirme hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fec61-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="fec61-184">Paylaşılan erişim imzası kullanarak bir yöntem tootry kapsayıcı işlem ekleme</span><span class="sxs-lookup"><span data-stu-id="fec61-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="fec61-185">Ardından, bazı kapsayıcı işlemleri için hello kapsayıcı paylaşılan erişim imzası kullanarak testleri bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fec61-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="fec61-186">Merhaba paylaşılan erişim imzası kullanılan tooreturn erişim toohello kapsayıcı tek başına hello imza tabanlı kimlik doğrulaması bir başvuru toohello kapsayıcı ' dir.</span><span class="sxs-lookup"><span data-stu-id="fec61-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="fec61-187">Yöntem tooProgram.cs aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-187">Add hello following method tooProgram.cs:</span></span>

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

<span data-ttu-id="fec61-188">Güncelleştirme hello **Main()** yöntemi toocall **UseContainerSAS()** ikisi hello ile paylaşılan erişim imzası hello kapsayıcısında oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="fec61-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="fec61-189">Paylaşılan erişim imzası kullanarak bir yöntem tootry blobu işlemleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fec61-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="fec61-190">Son olarak, hello blob'unda paylaşılan erişim imzası kullanarak bazı blobu işlemleri testleri bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fec61-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="fec61-191">Bu durumda, biz hello Oluşturucu kullanın **CloudBlockBlob(String)**, hello paylaşılan erişim imzası, tooreturn başvuru toohello blob geçen.</span><span class="sxs-lookup"><span data-stu-id="fec61-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="fec61-192">Diğer kimlik doğrulaması gerekli değildir; İmza hello tek başına dayanır.</span><span class="sxs-lookup"><span data-stu-id="fec61-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="fec61-193">Yöntem tooProgram.cs aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fec61-193">Add hello following method tooProgram.cs:</span></span>

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

<span data-ttu-id="fec61-194">Güncelleştirme hello **Main()** yöntemi toocall **UseBlobSAS()** hem hello hello blob üzerinde oluşturulan erişim imzaları paylaşılan:</span><span class="sxs-lookup"><span data-stu-id="fec61-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

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

<span data-ttu-id="fec61-195">Merhaba konsol uygulamasını çalıştırın ve hangi işlemleri hangi imzalar için izin verilen hello çıktı toosee gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="fec61-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="fec61-196">Merhaba konsol penceresinde Hello çıkış benzer toohello aşağıdaki görünür:</span><span class="sxs-lookup"><span data-stu-id="fec61-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="fec61-197">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fec61-197">Next Steps</span></span>

* [<span data-ttu-id="fec61-198">Paylaşılan erişim imzası, bölüm 1: hello SAS modelini anlama</span><span class="sxs-lookup"><span data-stu-id="fec61-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="fec61-199">Anonim okuma erişimini toocontainers ve BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="fec61-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="fec61-200">Paylaşılan erişim imzası (REST API) ile erişim için temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="fec61-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="fec61-201">Tablo ve kuyruk SAS Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="fec61-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
