---
title: "aaaSet alma nesne ve özellikleri ve meta veriler Azure depolama alanında | Microsoft Docs"
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
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="f3b01-103">Özellikler ile meta verileri ayarlama ve alma</span><span class="sxs-lookup"><span data-stu-id="f3b01-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="f3b01-104">Ayrıca Azure Storage destek Sistem özellikleri ve kullanıcı tanımlı meta veriler, içerdikleri toohello veri nesneleri.</span><span class="sxs-lookup"><span data-stu-id="f3b01-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="f3b01-105">Bu makalede ele yönetme Sistem özellikleri ve kullanıcı tanımlı meta verileriyle hello [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="f3b01-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="f3b01-106">**Sistem Özellikleri**: Sistem özellikleri her depolama kaynağı yok.</span><span class="sxs-lookup"><span data-stu-id="f3b01-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="f3b01-107">Bunlardan bazıları okunabilir veya başkalarının salt okunur durumdayken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f3b01-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="f3b01-108">Merhaba perde arkasında bazı sistem özellikleri toocertain standart HTTP üstbilgilerini karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="f3b01-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="f3b01-109">Hello Azure storage istemci kitaplığı bunları tutar.</span><span class="sxs-lookup"><span data-stu-id="f3b01-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="f3b01-110">**Kullanıcı tanımlı meta veriler**: kullanıcı tanımlı meta veriler olan bir ad-değer çiftinin hello formundaki belirli bir kaynak üzerinde belirtin meta verileri.</span><span class="sxs-lookup"><span data-stu-id="f3b01-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="f3b01-111">Meta veri toostore ek değerler ile depolama kaynağı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3b01-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="f3b01-112">Bu ek meta veri değerleri kendi yalnızca amaçlıdır ve hello kaynak biçimini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="f3b01-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="f3b01-113">Depolama kaynak için özellik ve meta veri değerlerini alma iki adımlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="f3b01-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="f3b01-114">Bu değerleri okumadan önce açıkça bunları tarafından arama hello alması gerekir **FetchAttributes** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f3b01-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3b01-115">Depolama kaynağı için özellik ve meta veri değerleri hello birini çağırın sürece doldurulmamış **FetchAttributes** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="f3b01-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="f3b01-116">Alacağınız bir `400 Bad Request` tüm ad/değer çiftleri ASCII olmayan karakterler içeriyorsa.</span><span class="sxs-lookup"><span data-stu-id="f3b01-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="f3b01-117">Meta veri ad/değer çiftleridir geçerli HTTP üstbilgileri ve HTTP üstbilgileri yöneten tooall kısıtlamaları uyması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3b01-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="f3b01-118">Bu nedenle, URL kodlaması veya adları ve ASCII olmayan karakterler içeren bir değer için Base64 kodlaması kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="f3b01-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="f3b01-119">Özellikler alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="f3b01-119">Setting and retrieving properties</span></span>
<span data-ttu-id="f3b01-120">tooretrieve özellik değerleri, çağrı hello **FetchAttributes** yöntemi, blob veya kapsayıcı toopopulate hello özellikleri, ardından hello değerleri okuyun.</span><span class="sxs-lookup"><span data-stu-id="f3b01-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="f3b01-121">tooset özellikleri bir nesne üzerinde hello özellik değeri belirtin ve sonra arama hello **SetProperties** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f3b01-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="f3b01-122">Merhaba aşağıdaki kod örneğinde bir kapsayıcı oluşturur, ardından bazı özellik değerleri tooa konsol penceresine yazar.</span><span class="sxs-lookup"><span data-stu-id="f3b01-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="f3b01-123">Meta veri alma ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="f3b01-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="f3b01-124">Meta veriler blob veya kapsayıcı kaynak üzerinde bir veya daha fazla ad-değer çiftleri olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3b01-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="f3b01-125">tooset meta verileri, ad-değer çiftleri toohello ekleme **meta veri** hello kaynak koleksiyonu ardından hello çağıran **SetMetadata** yöntemi toosave hello değerleri toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="f3b01-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="f3b01-126">Meta verilerinizin Hello adını C# tanımlayıcıları için adlandırma kurallarını toohello uygun olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f3b01-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="f3b01-127">Merhaba aşağıdaki kod örneğinde meta verileri bir kapsayıcıda ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f3b01-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="f3b01-128">Bir değer hello koleksiyonunun kullanılarak ayarlanır **Ekle** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f3b01-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="f3b01-129">Merhaba başka bir değer örtük anahtar/değer sözdizimi kullanılarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="f3b01-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="f3b01-130">Her ikisi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f3b01-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="f3b01-131">tooretrieve meta verileri, çağrı hello **FetchAttributes** , blob veya kapsayıcı toopopulate hello yöntemi **meta veri** sonra Merhaba, hello aşağıdaki örnekte gösterildiği gibi değerler koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="f3b01-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="f3b01-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f3b01-132">Next steps</span></span>
* [<span data-ttu-id="f3b01-133">.NET başvurusu için Azure Storage istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="f3b01-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="f3b01-134">.NET NuGet paketi için Azure Storage istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="f3b01-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
