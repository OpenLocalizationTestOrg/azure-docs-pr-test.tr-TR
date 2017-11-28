---
title: "Azure CDN Azure Storage bloblarında aaaManage sona erme tarihi | Microsoft Docs"
description: "Azure CDN önbelleğe alma işleminde, BLOB'ları için yaşam süresi denetleme hello seçenekleri hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="c8cb8-103">Azure CDN Azure Storage bloblarında, bitiş tarihini Yönet</span><span class="sxs-lookup"><span data-stu-id="c8cb8-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8cb8-104">Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS</span><span class="sxs-lookup"><span data-stu-id="c8cb8-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="c8cb8-105">Azure depolama blob hizmeti</span><span class="sxs-lookup"><span data-stu-id="c8cb8-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="c8cb8-106">Merhaba [blob hizmeti](../storage/common/storage-introduction.md#blob-storage) içinde [Azure Storage](../storage/common/storage-introduction.md) birkaç Azure tabanlı kaynakları birini Azure CDN ile tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="c8cb8-107">Kendi yaşam süresi (TTL) geçen kadar herhangi bir genel olarak erişilebilir blob içerik Azure CDN'de önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="c8cb8-108">Merhaba TTL hello tarafından belirlenir [ *Cache-Control* üstbilgi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) Azure depolama biriminden hello HTTP yanıt.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="c8cb8-109">Blob üzerindeki hiçbir TTL tooset seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="c8cb8-110">Bu durumda, Azure CDN varsayılan TTL yedi gün otomatik olarak uygular.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="c8cb8-111">Hello Azure CDN toospeed erişim tooblobs ve diğer dosyaları nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8cb8-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="c8cb8-112">Hello Azure Storage blobu hizmeti hakkında daha fazla bilgi için bkz: [Blob hizmeti kavramları](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8cb8-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="c8cb8-113">Bu öğretici, Azure storage'da bir blob üzerinde hello TTL ayarlayabilirsiniz birkaç yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="c8cb8-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8cb8-114">Azure PowerShell</span></span>
<span data-ttu-id="c8cb8-115">[Azure PowerShell](/powershell/azure/overview) hello hızlı ve en güçlü şekilde tooadminister Azure hizmetlerinizi biridir.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="c8cb8-116">Kullanım hello `Get-AzureStorageBlob` cmdlet tooget başvuru toohello blob hello ayarlamaktır `.ICloudBlob.Properties.CacheControl` özelliği.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="c8cb8-117">PowerShell çok kullanabilirsiniz[CDN profili ve uç noktaları yönetmek](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c8cb8-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="c8cb8-118">.NET için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="c8cb8-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="c8cb8-119">tooset blob kullanıcının .NET, kullanım hello kullanarak TTL [.NET için Azure Storage istemci Kitaplığı](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="c8cb8-120">Daha fazla sayıda .NET kod örnekleri hello kullanılabilir [.NET için Azure Blob Depolama örnek](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="c8cb8-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="c8cb8-121">Diğer yöntemleri</span><span class="sxs-lookup"><span data-stu-id="c8cb8-121">Other methods</span></span>
* [<span data-ttu-id="c8cb8-122">Azure Komut Satırı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="c8cb8-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="c8cb8-123">Merhaba blob karşıya yüklenirken hello ayarlamak *cacheControl* hello kullanarak özelliği `-p` geçin.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="c8cb8-124">Bu örnek hello TTL tooone saat (3600 saniye cinsinden) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="c8cb8-125">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="c8cb8-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="c8cb8-126">Açıkça kümesi hello *x-ms-blob-cache-control* özelliği bir [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put engelleme listesi](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), veya [Blob özelliklerini ayarla](https://msdn.microsoft.com/library/azure/ee691966.aspx) isteği.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="c8cb8-127">Üçüncü taraf Depolama Yönetimi Araçları</span><span class="sxs-lookup"><span data-stu-id="c8cb8-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="c8cb8-128">Bazı üçüncü taraf Azure Depolama Yönetimi araçlarını tooset hello izin *CacheControl* BLOB'lar özelliği.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="c8cb8-129">Sınama hello *Cache-Control* üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="c8cb8-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="c8cb8-130">Merhaba, BLOB TTL kolayca doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="c8cb8-131">Tarayıcınızın kullanarak [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), blob hello dahil olan test *Cache-Control* yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="c8cb8-132">Gibi bir araç de kullanabilirsiniz **wget**, [Postman](https://www.getpostman.com/), veya [Fiddler](http://www.telerik.com/fiddler) tooexamine hello yanıt üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="c8cb8-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8cb8-133">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c8cb8-133">Next Steps</span></span>
* [<span data-ttu-id="c8cb8-134">Merhaba hakkında okuyun *Cache-Control* üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="c8cb8-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="c8cb8-135">Bilgi nasıl Azure CDN bulut hizmeti içeriğinin toomanage süre sonu</span><span class="sxs-lookup"><span data-stu-id="c8cb8-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

