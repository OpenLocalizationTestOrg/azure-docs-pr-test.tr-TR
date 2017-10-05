---
title: "Ayarlayın ve nesne özellikleri ve Azure depolama alanında meta veri alma | Microsoft Docs"
description: "Azure Storage nesnelerde özel meta verileri depolamak ve ayarlayın ve sistem alınamıyor."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="00cc9-103">Özellikler ile meta verileri ayarlama ve alma</span><span class="sxs-lookup"><span data-stu-id="00cc9-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="00cc9-104">Azure Storage destek Sistem özellikleri ve kullanıcı tanımlı meta veriler, içerdikleri verilere ek olarak nesneleri.</span><span class="sxs-lookup"><span data-stu-id="00cc9-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="00cc9-105">Bu makalede ele yönetme Sistem özellikleri ve kullanıcı tanımlı meta verileriyle [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="00cc9-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="00cc9-106">**Sistem Özellikleri**: Sistem özellikleri her depolama kaynağı yok.</span><span class="sxs-lookup"><span data-stu-id="00cc9-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="00cc9-107">Bunlardan bazıları okunabilir veya başkalarının salt okunur durumdayken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="00cc9-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="00cc9-108">Perde arkasında bazı sistem özellikleri belirli standart HTTP üstbilgilerine karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="00cc9-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="00cc9-109">Azure storage istemci kitaplığı bunları tutar.</span><span class="sxs-lookup"><span data-stu-id="00cc9-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="00cc9-110">**Kullanıcı tanımlı meta veriler**: kullanıcı tanımlı meta veriler olan bir ad-değer çifti biçiminde belirli bir kaynak üzerinde belirtin meta verileri.</span><span class="sxs-lookup"><span data-stu-id="00cc9-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="00cc9-111">Meta veri depolama kaynağı ek değerlerle depolamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00cc9-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="00cc9-112">Bu ek meta veri değerleri kendi yalnızca amaçlıdır ve kaynak biçimini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="00cc9-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="00cc9-113">Depolama kaynak için özellik ve meta veri değerlerini alma iki adımlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="00cc9-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="00cc9-114">Bu değerleri okumadan önce açıkça bunları çağırarak alması gerekir **FetchAttributes** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="00cc9-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00cc9-115">Özellik ve meta veri değerlerini depolama kaynağı için aşağıdakilerden birini gerektirmediği sürece doldurulmamış **FetchAttributes** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="00cc9-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="00cc9-116">Alacağınız bir `400 Bad Request` tüm ad/değer çiftleri ASCII olmayan karakterler içeriyorsa.</span><span class="sxs-lookup"><span data-stu-id="00cc9-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="00cc9-117">Meta veri ad/değer çiftleri geçerli HTTP üstbilgi olduğundan ve bu nedenle tüm kısıtlamaları HTTP üstbilgileri yöneten uyması gerekir.</span><span class="sxs-lookup"><span data-stu-id="00cc9-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="00cc9-118">Bu nedenle, URL kodlaması veya adları ve ASCII olmayan karakterler içeren bir değer için Base64 kodlaması kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="00cc9-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="00cc9-119">Özellikler alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="00cc9-119">Setting and retrieving properties</span></span>
<span data-ttu-id="00cc9-120">Özellik değerlerini almak için arama **FetchAttributes** yöntemi blob veya özelliklerini doldurmak için kapsayıcı ardından değerleri okuyun.</span><span class="sxs-lookup"><span data-stu-id="00cc9-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="00cc9-121">Bir nesne üzerinde özelliklerini ayarlamak için özellik belirtmek değer sonra çağırın **SetProperties** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="00cc9-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="00cc9-122">Aşağıdaki kod örneğinde bir kapsayıcı oluşturur, ardından özellik değerlerini bazıları konsol penceresine yazar.</span><span class="sxs-lookup"><span data-stu-id="00cc9-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="00cc9-123">Meta veri alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="00cc9-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="00cc9-124">Meta veriler blob veya kapsayıcı kaynak üzerinde bir veya daha fazla ad-değer çiftleri olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00cc9-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="00cc9-125">Meta veri ayarlamak için ad-değer çiftlerini eklemek **meta veri** kaynak koleksiyonu'ı çağırın **SetMetadata** değerleri hizmete kaydetmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="00cc9-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="00cc9-126">Meta verilerinizin adını C# tanımlayıcıları için adlandırma kuralları için uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="00cc9-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="00cc9-127">Aşağıdaki kod örneğinde bir kapsayıcıda meta verilerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="00cc9-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="00cc9-128">Bir değer koleksiyonunun kullanılarak ayarlanır **Ekle** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="00cc9-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="00cc9-129">Başka bir değer örtük anahtar/değer sözdizimi kullanılarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="00cc9-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="00cc9-130">Her ikisi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="00cc9-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="00cc9-131">Meta verilerini almak için çağrı **FetchAttributes** yöntemi blob veya doldurmak için kapsayıcı **meta veri** koleksiyonu, aşağıdaki örnekte gösterildiği gibi değerler ardından okuyun.</span><span class="sxs-lookup"><span data-stu-id="00cc9-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="00cc9-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00cc9-132">Next steps</span></span>
* [<span data-ttu-id="00cc9-133">.NET başvurusu için Azure Storage istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="00cc9-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="00cc9-134">.NET NuGet paketi için Azure Storage istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="00cc9-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
