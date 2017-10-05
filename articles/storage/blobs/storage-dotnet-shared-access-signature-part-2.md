---
title: "Oluşturma ve paylaşılan erişim imzası (SAS) ile Azure Blob storage kullanma | Microsoft Docs"
description: "Bu öğretici, Blob storage'ı kullanmak için paylaşılan erişim imzaları oluşturma ve istemci uygulamalarında kullanma gösterir."
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
ms.openlocfilehash: 0d7bede352667931527c8583cb172a46a37b5aa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="e85cd-103">Paylaşılan erişim imzası, bölüm 2: Oluşturma ve bir SAS Blob storage'ı kullanma</span><span class="sxs-lookup"><span data-stu-id="e85cd-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="e85cd-104">[Bölüm 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) keşfedilen Bu öğretici paylaşılan erişim imzası (SAS) ve bunları kullanmak için en iyi uygulamalar açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e85cd-104">[Part 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="e85cd-105">Bölüm 2 oluşturmak ve ardından paylaşılan erişim imzaları Blob storage'ı nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-105">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="e85cd-106">Örnekler C# dilinde yazılmıştır ve .NET için Azure Storage istemci kitaplığı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-106">The examples are written in C# and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="e85cd-107">Bu öğreticide örnekler:</span><span class="sxs-lookup"><span data-stu-id="e85cd-107">The examples in this tutorial:</span></span>

* <span data-ttu-id="e85cd-108">Üzerinde bir kapsayıcı paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="e85cd-109">Blob üzerindeki paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="e85cd-110">Bir kapsayıcının kaynakları imzalarını yönetmek için bir saklı erişim ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="e85cd-110">Create a stored access policy to manage signatures on a container's resources</span></span>
* <span data-ttu-id="e85cd-111">Bir istemci uygulamasında paylaşılan erişim imzaları test</span><span class="sxs-lookup"><span data-stu-id="e85cd-111">Test the shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="e85cd-112">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="e85cd-112">About this tutorial</span></span>
<span data-ttu-id="e85cd-113">Bu öğreticide, oluşturma ve kapsayıcılar ve bloblar için paylaşılan erişim imzaları kullanma gösteren iki konsol uygulamaları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e85cd-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="e85cd-114">**Uygulama 1**: yönetimi uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e85cd-114">**Application 1**: The management application.</span></span> <span data-ttu-id="e85cd-115">Bir kapsayıcı ve bir blob için bir paylaşılan erişim imzası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e85cd-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="e85cd-116">Depolama hesabı erişim tuşu kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-116">Includes the storage account access key in source code.</span></span>

<span data-ttu-id="e85cd-117">**Uygulama 2**: istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e85cd-117">**Application 2**: The client application.</span></span> <span data-ttu-id="e85cd-118">İlk uygulama ile oluşturulan paylaşılan erişim imzaları kullanarak erişse kapsayıcı ve blob kaynakları.</span><span class="sxs-lookup"><span data-stu-id="e85cd-118">Accesses container and blob resources using the shared access signatures created with the first application.</span></span> <span data-ttu-id="e85cd-119">Yalnızca paylaşılan erişim imzalarını erişim kapsayıcısına ve blob kaynaklarını--kullanır mevcut *değil* depolama hesabının erişim anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-119">Uses only the shared access signatures to access container and blob resources--it does *not* include the storage account access key.</span></span>

## <a name="part-1-create-a-console-application-to-generate-shared-access-signatures"></a><span data-ttu-id="e85cd-120">1. Kısım: paylaşılan erişim imzaları üretmek için bir konsol uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="e85cd-120">Part 1: Create a console application to generate shared access signatures</span></span>
<span data-ttu-id="e85cd-121">İlk olarak, yüklü .NET için Azure Storage istemci kitaplığı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e85cd-121">First, ensure that you have the Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="e85cd-122">Yükleyebileceğiniz [NuGet paketi](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet paketi") istemci kitaplığı için en güncel derlemelerini içeren.</span><span class="sxs-lookup"><span data-stu-id="e85cd-122">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library.</span></span> <span data-ttu-id="e85cd-123">Bu, en son düzeltmeler olmasını sağlamaya yönelik önerilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-123">This is the recommended method for ensuring that you have the most recent fixes.</span></span> <span data-ttu-id="e85cd-124">İstemci kitaplığının en son sürümünü bir parçası olarak indirebilirsiniz [.NET için Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e85cd-124">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="e85cd-125">Visual Studio'da yeni bir Windows konsol uygulaması oluşturun ve adlandırın **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="e85cd-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="e85cd-126">Başvurular ekleyin [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) ve [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) aşağıdaki yaklaşımlardan birini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="e85cd-126">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of the following approaches:</span></span>

* <span data-ttu-id="e85cd-127">Kullanım [NuGet Paket Yöneticisi](https://docs.nuget.org/consume/installing-nuget) Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e85cd-127">Use the [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="e85cd-128">Seçin **proje** > **NuGet paketlerini Yönet**, her paket için (Microsoft.WindowsAzure.ConfigurationManager ve WindowsAzure.Storage) çevrimiçi olarak arayın ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="e85cd-129">Alternatif olarak, bu derlemeler yüklemenizde Azure SDK'sının bulun ve bunları başvurular ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-129">Alternatively, locate these assemblies in your installation of the Azure SDK and add references to them:</span></span>
  * <span data-ttu-id="e85cd-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="e85cd-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="e85cd-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="e85cd-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="e85cd-132">Program.cs dosyasının üst kısmında, aşağıdaki ekleyin **kullanarak** yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="e85cd-132">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="e85cd-133">Bir yapılandırma ayarı depolama hesabınıza işaret eden bir bağlantı dizesini içeren app.config dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-133">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span></span> <span data-ttu-id="e85cd-134">App.config dosyasını buna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e85cd-134">Your app.config file should look similar to this one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="e85cd-135">Bir kapsayıcı için bir paylaşılan erişim imzası URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="e85cd-136">Başından itibaren üzerinde yeni bir kapsayıcı paylaşılan erişim imzası oluşturmak için bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-136">To begin with, we add a method to generate a shared access signature on a new container.</span></span> <span data-ttu-id="e85cd-137">Bu durumda, sona erme saati ve verir izinleri olduğunu gösteren bilgiler URI üzerinde taşıyan şekilde imza depolanmış erişim ilkesi ile ilişkili değil.</span><span class="sxs-lookup"><span data-stu-id="e85cd-137">In this case, the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions it grants.</span></span>

<span data-ttu-id="e85cd-138">İlk olarak, kodu ekleyin **Main()** yöntemi depolama hesabınıza erişim için kimlik doğrulaması yapmak ve yeni bir kapsayıcı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="e85cd-138">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls to the methods created below here...

    //Require user input before closing the console window.
    Console.ReadLine();
}
```

<span data-ttu-id="e85cd-139">Ardından, kapsayıcı paylaşılan erişim imzası oluşturur ve imza URI döndüren bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-139">Next, add a method that generates the shared access signature for the container and returns the signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set the expiry time and permissions for the container.
    //In this case no start time is specified, so the shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="e85cd-140">Sonuna şu satırları ekleyin **Main()** yöntemi çağırmadan önce **Console.ReadLine()**, çağırmak için **GetContainerSasUri()** ve imza URI yazmak için Konsol penceresinde:</span><span class="sxs-lookup"><span data-stu-id="e85cd-140">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for the container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="e85cd-141">Derleme ve yeni kapsayıcı paylaşılan erişim imzası URI çıktısını almak için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-141">Compile and run to output the shared access signature URI for the new container.</span></span> <span data-ttu-id="e85cd-142">URI aşağıdakine benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="e85cd-142">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="e85cd-143">Kod çalıştırdıktan sonra oluşturduğunuz için kapsayıcı paylaşılan erişim imzası sonraki 24 saat için geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="e85cd-143">Once you have run the code, the shared access signature you created for the container will be valid for the next 24 hours.</span></span> <span data-ttu-id="e85cd-144">İmza listesi BLOB kapsayıcısında ve yeni BLOB kapsayıcıya yazma için bir istemci izni verir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-144">The signature grants a client permission to list blobs in the container and to write new blobs to the container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="e85cd-145">Bir blob için bir paylaşılan erişim imzası URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="e85cd-146">Ardından, yeni blob kapsayıcı içinde oluşturmak ve paylaşılan erişim imzası oluşturmak için benzer bir kod yazın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-146">Next, we write similar code to create a new blob within the container and generate a shared access signature for it.</span></span> <span data-ttu-id="e85cd-147">URI'de başlangıç zamanı, bitiş saati ve izin bilgileri içerecek şekilde bu paylaşılan erişim imzası depolanmış erişim ilkesi ile ilişkili değil.</span><span class="sxs-lookup"><span data-stu-id="e85cd-147">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information in the URI.</span></span>

<span data-ttu-id="e85cd-148">Yeni bir blob oluşturur ve bazı metin, yazar sonra paylaşılan erişim imzası oluşturur ve URI imza döndüren yeni bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-148">Add a new method that creates a new blob and writes some text to it, then generates a shared access signature and returns the signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set the expiry time and permissions for the blob.
    //In this case, the start time is specified as a few minutes in the past, to mitigate clock skew.
    //The shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the blob, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="e85cd-149">Ekranın alt kısmındaki **Main()** yöntemini çağırmak için aşağıdaki satırları ekleyin **GetBlobSasUri()**, çağırmadan önce **Console.ReadLine()**ve paylaşılan erişim imzası yazma URI konsol penceresine:</span><span class="sxs-lookup"><span data-stu-id="e85cd-149">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="e85cd-150">Derleme ve yeni blob paylaşılan erişim imzası URI çıktısını almak için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-150">Compile and run to output the shared access signature URI for the new blob.</span></span> <span data-ttu-id="e85cd-151">URI aşağıdakine benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="e85cd-151">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-the-container"></a><span data-ttu-id="e85cd-152">Kapsayıcıda depolanmış erişim ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-152">Create a stored access policy on the container</span></span>
<span data-ttu-id="e85cd-153">Şimdi bir saklı erişim ilkesi kendisiyle ilişkilendirilmiş herhangi bir paylaşılan erişim imzaları kısıtlamalarını tanımlayacaksınız kapsayıcısı üzerinde oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="e85cd-153">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="e85cd-154">Önceki örneklerde, biz başlangıç saati (örtük veya açık olarak), sona erme saati ve izinleri paylaşılan erişim imzası URI kendisini belirtilen.</span><span class="sxs-lookup"><span data-stu-id="e85cd-154">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span></span> <span data-ttu-id="e85cd-155">Aşağıdaki örneklerde, biz Bu saklı erişim ilkesi, paylaşılan erişim imzası değil, belirtin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-155">In the following examples, we specify these on the stored access policy, not on the shared access signature.</span></span> <span data-ttu-id="e85cd-156">Bunun yapılması paylaşılan erişim imzası vermeden bu kısıtlamaların değiştirmek için bize sağlar.</span><span class="sxs-lookup"><span data-stu-id="e85cd-156">Doing so enables us to change these constraints without reissuing the shared access signature.</span></span>

<span data-ttu-id="e85cd-157">Bir veya daha fazla paylaşılan erişim imzası kısıtlamalar ve saklı erişim ilkesinde kalanı olması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e85cd-157">It's possible to have one or more of the constraints on the shared access signature, and the remainder on the stored access policy.</span></span> <span data-ttu-id="e85cd-158">Ancak, yalnızca başlangıç zamanı, bitiş saati ve izinleri tek bir yerde veya diğer belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e85cd-158">However, you can only specify the start time, expiry time, and permissions in one place or the other.</span></span> <span data-ttu-id="e85cd-159">Örneğin, paylaşılan erişim imzası üzerinde izinleri belirtmek ve ayrıca bunları depolanmış erişim ilkesine belirtin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-159">For example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span></span>

<span data-ttu-id="e85cd-160">Bir saklı erişim ilkesi için bir kapsayıcı eklediğinizde, kapsayıcının var olan izinleri almak, yeni Erişim İlkesi Ekle ve kapsayıcının izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-160">When you add a stored access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span></span>

<span data-ttu-id="e85cd-161">Bir kapsayıcıda yeni bir saklı erişim ilkesi oluşturur ve ilkenin adını döndüren yeni bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-161">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get the container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="e85cd-162">Ekranın alt kısmındaki **Main()** yöntemi çağırmadan önce **Console.ReadLine()**, aşağıdaki satırları ilk Temizle varolan tüm erişim ilkeleri ekleyin ve ardından çağrısı  **CreateSharedAccessPolicy()** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e85cd-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies, and then call the **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on the container, which may be optionally used to provide constraints for
//shared access signatures on the container and the blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="e85cd-163">Bir kapsayıcı erişim ilkeleri temizlediğinizde, gerekir ilk kapsayıcının var olan izinleri almak sonra izinleri temizleyin ve ardından yeniden izinlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-163">When you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-the-container-that-uses-an-access-policy"></a><span data-ttu-id="e85cd-164">Paylaşılan erişim imzası bir erişim ilkesi kullanan kapsayıcısı üzerinde URI oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-164">Generate a shared access signature URI on the container that uses an access policy</span></span>
<span data-ttu-id="e85cd-165">Ardından, daha önce ancak biz imza önceki örnekte oluşturduğumuz depolanmış erişim ilkesi ilişkilendirmek bu kez oluşturduğumuz kapsayıcısı için başka bir paylaşılan erişim imzası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e85cd-165">Next, we create another shared access signature for the container that we created earlier, but this time we associate the signature with the stored access policy we created in the previous example.</span></span>

<span data-ttu-id="e85cd-166">Kapsayıcı için başka bir paylaşılan erişim imzası oluşturmak için yeni bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-166">Add a new method to generate another shared access signature for the container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate the shared access signature on the container. In this case, all of the constraints for the
    //shared access signature are specified on the stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="e85cd-167">Ekranın alt kısmındaki **Main()** yöntemi çağırmadan önce **Console.ReadLine()**, çağırmak için aşağıdaki satırları ekleyin **GetContainerSasUriWithPolicy** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e85cd-167">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-the-blob-that-uses-an-access-policy"></a><span data-ttu-id="e85cd-168">URI üstünde bir erişim ilkesi kullanan Blob paylaşılan erişim imzası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e85cd-168">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span></span>
<span data-ttu-id="e85cd-169">Son olarak, başka bir blob oluşturun ve saklı erişim ilkesi ile ilişkili bir paylaşılan erişim imzası oluşturmak için benzer bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-169">Finally, we add a similar method to create another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="e85cd-170">Bir blob oluşturun ve paylaşılan erişim imzası oluşturmak için yeni bir yöntem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-170">Add a new method to create a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature. " +
    "A stored access policy defines the constraints for the signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate the shared access signature on the blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="e85cd-171">Ekranın alt kısmındaki **Main()** yöntemi çağırmadan önce **Console.ReadLine()**, çağırmak için aşağıdaki satırları ekleyin **GetBlobSasUriWithPolicy** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e85cd-171">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="e85cd-172">**Main()** yöntemi şimdi şöyle görünmelidir tamamının.</span><span class="sxs-lookup"><span data-stu-id="e85cd-172">The **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="e85cd-173">Paylaşılan erişim imzası URI'ler konsol penceresine yazma sonra kopyalayın ve bu öğreticinin ikinci bölümünde kullanmak için bir metin dosyası yapıştırmak için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e85cd-173">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for the container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on the container, which may be optionally used to provide constraints for
    //shared access signatures on the container and the blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="e85cd-174">GenerateSharedAccessSignatures konsol uygulamasını çalıştırdığınızda, aşağıdakine benzer bir çıktı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e85cd-174">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following.</span></span> <span data-ttu-id="e85cd-175">Bu öğreticinin Kısım 2'de kullanmak paylaşılan erişim imzaları değil.</span><span class="sxs-lookup"><span data-stu-id="e85cd-175">These are the shared access signatures you use in Part 2 of the tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-to-test-the-shared-access-signatures"></a><span data-ttu-id="e85cd-176">2. Kısım: paylaşılan erişim imzaları test etmek için bir konsol uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="e85cd-176">Part 2: Create a console application to test the shared access signatures</span></span>
<span data-ttu-id="e85cd-177">Önceki örneklerde oluşturulan paylaşılan erişim imzaları sınamak için biz ve blob kapsayıcısı üzerinde işlem gerçekleştirmeye imzalarını kullanır ikinci bir konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e85cd-177">To test the shared access signatures created in the previous examples, we create a second console application that uses the signatures to perform operations on the container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="e85cd-178">Öğreticinin ilk kısmı tamamlandı beri 24 saatten fazla geçmişse, üretilen imzalar artık geçerli olmayacak.</span><span class="sxs-lookup"><span data-stu-id="e85cd-178">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span></span> <span data-ttu-id="e85cd-179">Bu durumda, öğreticinin ikinci bölümünde kullanmak için yeni paylaşılan erişim imzaları üretmek için ilk konsol uygulamasındaki kod çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e85cd-179">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span></span>
>

<span data-ttu-id="e85cd-180">Visual Studio'da yeni bir Windows konsol uygulaması oluşturun ve adlandırın **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="e85cd-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="e85cd-181">Başvurular ekleyin [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) ve [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), daha önce yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="e85cd-181">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="e85cd-182">Program.cs dosyasının üst kısmında, aşağıdaki ekleyin **kullanarak** yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="e85cd-182">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="e85cd-183">Gövdesinde **Main()** yöntemi, değerlerine öğreticinin 1 bölümünde oluşturulan paylaşılan erişim imzaları değiştirerek aşağıdaki dize sabitleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-183">In the body of the **Main()** method, add the following string constants, changing their values to the shared access signatures you generated in part 1 of the tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-to-try-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="e85cd-184">Paylaşılan erişim imzası kullanarak kapsayıcı işlemleri denemek için bir yöntem ekleyin</span><span class="sxs-lookup"><span data-stu-id="e85cd-184">Add a method to try container operations using a shared access signature</span></span>
<span data-ttu-id="e85cd-185">Ardından, bazı kapsayıcı işlemleri için kapsayıcı paylaşılan erişim imzası kullanarak testleri bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-185">Next, we add a method that tests some container operations using a shared access signature for the container.</span></span> <span data-ttu-id="e85cd-186">Paylaşılan erişim imzası, tek başına imza tabanlı kapsayıcıya erişimi kimlik doğrulaması kapsayıcıya başvuru döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e85cd-186">The shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span></span>

<span data-ttu-id="e85cd-187">Aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-187">Add the following method to Program.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with the SAS provided.

    //Return a reference to the container using the SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list to store blob URIs returned by a listing operation on the container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob to the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions to the container. ";
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

    //List operation: List the blobs in the container.
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

    //Read operation: Get a reference to one of the blobs in the container and read it.
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

    //Delete operation: Delete a blob in the container.
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

<span data-ttu-id="e85cd-188">Güncelleştirme **Main()** çağrılacak yöntem **UseContainerSAS()** ikisini de kapsayıcısında oluşturduğunuz paylaşılan erişim imzaları:</span><span class="sxs-lookup"><span data-stu-id="e85cd-188">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures you created on the container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-to-try-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="e85cd-189">Paylaşılan erişim imzası kullanarak blob işlemleri denemek için bir yöntem ekleyin</span><span class="sxs-lookup"><span data-stu-id="e85cd-189">Add a method to try blob operations using a shared access signature</span></span>
<span data-ttu-id="e85cd-190">Son olarak, bir paylaşılan erişim imzası blob üzerindeki kullanarak bazı blobu işlemleri testleri bir yöntem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-190">Finally, we add a method that tests some blob operations using a shared access signature on the blob.</span></span> <span data-ttu-id="e85cd-191">Bu durumda, biz Oluşturucu kullanın **CloudBlockBlob(String)**, blob bir başvuru döndürmek için paylaşılan erişim imzası geçen.</span><span class="sxs-lookup"><span data-stu-id="e85cd-191">In this case, we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span></span> <span data-ttu-id="e85cd-192">Diğer kimlik doğrulaması gerekli değildir; tek başına imza dayanır.</span><span class="sxs-lookup"><span data-stu-id="e85cd-192">No other authentication is required; it's based on the signature alone.</span></span>

<span data-ttu-id="e85cd-193">Aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e85cd-193">Add the following method to Program.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using the SAS provided.

    //Return a reference to the blob using the SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob to the container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions to the blob. ";
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

    //Read operation: Read the contents of the blob.
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

    //Delete operation: Delete the blob.
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

<span data-ttu-id="e85cd-194">Güncelleştirme **Main()** çağrılacak yöntem **UseBlobSAS()** hem blob üzerindeki oluşturduğunuz paylaşılan erişim imzaları:</span><span class="sxs-lookup"><span data-stu-id="e85cd-194">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call the test methods with the shared access signatures created on the blob, with and without the access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="e85cd-195">Konsol uygulamasını çalıştırın ve hangi işlemleri hangi imzalar için izin verilen görmek için çıktıyı inceleyin.</span><span class="sxs-lookup"><span data-stu-id="e85cd-195">Run the console application and observe the output to see which operations are permitted for which signatures.</span></span> <span data-ttu-id="e85cd-196">Çıkış konsol penceresinde aşağıdakine benzer görünecektir:</span><span class="sxs-lookup"><span data-stu-id="e85cd-196">The output in the console window will look similar to the following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="e85cd-197">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e85cd-197">Next Steps</span></span>

* [<span data-ttu-id="e85cd-198">Paylaşılan erişim imzası, bölüm 1: SAS modelini anlama</span><span class="sxs-lookup"><span data-stu-id="e85cd-198">Shared Access Signatures, Part 1: Understanding the SAS Model</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="e85cd-199">Kapsayıcılar ve bloblar için anonim okuma erişimini yönetme</span><span class="sxs-lookup"><span data-stu-id="e85cd-199">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="e85cd-200">Paylaşılan erişim imzası (REST API) ile erişim için temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="e85cd-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="e85cd-201">Tablo ve kuyruk SAS Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="e85cd-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
