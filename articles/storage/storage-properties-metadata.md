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
# <a name="set-and-retrieve-properties-and-metadata"></a>Özellikler ile meta verileri ayarlama ve alma

Ayrıca Azure Storage destek Sistem özellikleri ve kullanıcı tanımlı meta veriler, içerdikleri toohello veri nesneleri. Bu makalede ele yönetme Sistem özellikleri ve kullanıcı tanımlı meta verileriyle hello [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Sistem Özellikleri**: Sistem özellikleri her depolama kaynağı yok. Bunlardan bazıları okunabilir veya başkalarının salt okunur durumdayken ayarlayın. Merhaba perde arkasında bazı sistem özellikleri toocertain standart HTTP üstbilgilerini karşılık gelir. Hello Azure storage istemci kitaplığı bunları tutar.

* **Kullanıcı tanımlı meta veriler**: kullanıcı tanımlı meta veriler olan bir ad-değer çiftinin hello formundaki belirli bir kaynak üzerinde belirtin meta verileri. Meta veri toostore ek değerler ile depolama kaynağı kullanabilirsiniz. Bu ek meta veri değerleri kendi yalnızca amaçlıdır ve hello kaynak biçimini etkilemez.

Depolama kaynak için özellik ve meta veri değerlerini alma iki adımlı bir işlemdir. Bu değerleri okumadan önce açıkça bunları tarafından arama hello alması gerekir **FetchAttributes** yöntemi.

> [!IMPORTANT]
> Depolama kaynağı için özellik ve meta veri değerleri hello birini çağırın sürece doldurulmamış **FetchAttributes** yöntemleri.
>
> Alacağınız bir `400 Bad Request` tüm ad/değer çiftleri ASCII olmayan karakterler içeriyorsa. Meta veri ad/değer çiftleridir geçerli HTTP üstbilgileri ve HTTP üstbilgileri yöneten tooall kısıtlamaları uyması gerekir. Bu nedenle, URL kodlaması veya adları ve ASCII olmayan karakterler içeren bir değer için Base64 kodlaması kullanmanız önerilir.
>

## <a name="setting-and-retrieving-properties"></a>Özellikler alma ve ayarlama
tooretrieve özellik değerleri, çağrı hello **FetchAttributes** yöntemi, blob veya kapsayıcı toopopulate hello özellikleri, ardından hello değerleri okuyun.

tooset özellikleri bir nesne üzerinde hello özellik değeri belirtin ve sonra arama hello **SetProperties** yöntemi.

Merhaba aşağıdaki kod örneğinde bir kapsayıcı oluşturur, ardından bazı özellik değerleri tooa konsol penceresine yazar.

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

## <a name="setting-and-retrieving-metadata"></a>Meta veri alma ve ayarlama
Meta veriler blob veya kapsayıcı kaynak üzerinde bir veya daha fazla ad-değer çiftleri olarak belirtebilirsiniz. tooset meta verileri, ad-değer çiftleri toohello ekleme **meta veri** hello kaynak koleksiyonu ardından hello çağıran **SetMetadata** yöntemi toosave hello değerleri toohello hizmet.

> [!NOTE]
> Meta verilerinizin Hello adını C# tanımlayıcıları için adlandırma kurallarını toohello uygun olmalıdır.
>
>

Merhaba aşağıdaki kod örneğinde meta verileri bir kapsayıcıda ayarlar. Bir değer hello koleksiyonunun kullanılarak ayarlanır **Ekle** yöntemi. Merhaba başka bir değer örtük anahtar/değer sözdizimi kullanılarak yapılır. Her ikisi de geçerlidir.

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

tooretrieve meta verileri, çağrı hello **FetchAttributes** , blob veya kapsayıcı toopopulate hello yöntemi **meta veri** sonra Merhaba, hello aşağıdaki örnekte gösterildiği gibi değerler koleksiyonu.

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

## <a name="next-steps"></a>Sonraki adımlar
* [.NET başvurusu için Azure Storage istemci kitaplığı](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [.NET NuGet paketi için Azure Storage istemci kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/)
