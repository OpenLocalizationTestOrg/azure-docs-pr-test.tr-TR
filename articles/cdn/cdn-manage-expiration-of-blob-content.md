---
title: "Azure CDN Azure Storage bloblarında sona erme tarihi yönetme | Microsoft Docs"
description: "Azure CDN önbelleğe alma işleminde, BLOB'ları için yaşam süresi denetleme seçenekleri hakkında bilgi edinin."
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
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="e5a0a-103">Azure CDN Azure Storage bloblarında, bitiş tarihini Yönet</span><span class="sxs-lookup"><span data-stu-id="e5a0a-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5a0a-104">Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS</span><span class="sxs-lookup"><span data-stu-id="e5a0a-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="e5a0a-105">Azure depolama blob hizmeti</span><span class="sxs-lookup"><span data-stu-id="e5a0a-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="e5a0a-106">[Blob hizmeti](../storage/common/storage-introduction.md#blob-storage) içinde [Azure Storage](../storage/common/storage-introduction.md) birkaç Azure tabanlı kaynakları birini Azure CDN ile tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="e5a0a-107">Kendi yaşam süresi (TTL) geçen kadar herhangi bir genel olarak erişilebilir blob içerik Azure CDN'de önbelleğe alınabilir.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="e5a0a-108">TTL değeri tarafından belirlenir [ *Cache-Control* üstbilgi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) Azure depolama biriminden HTTP yanıt.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="e5a0a-109">Blob üzerindeki hiçbir TTL ayarlamak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="e5a0a-110">Bu durumda, Azure CDN varsayılan TTL yedi gün otomatik olarak uygular.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="e5a0a-111">BLOB'ları ve diğer dosyalara erişimi hızlandırmak için Azure CDN nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5a0a-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="e5a0a-112">Azure Storage blobu hizmeti hakkında daha fazla bilgi için bkz: [Blob hizmeti kavramları](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5a0a-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="e5a0a-113">Bu öğretici, Azure storage'da bir blob TTL ayarlayabilirsiniz birkaç yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="e5a0a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5a0a-114">Azure PowerShell</span></span>
<span data-ttu-id="e5a0a-115">[Azure PowerShell](/powershell/azure/overview) Azure hizmetlerinizi yönetmeyi hızlı ve en güçlü yollarından biri.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="e5a0a-116">Kullanım `Get-AzureStorageBlob` blob başvurusu almak için cmdlet ayarlamaktır `.ICloudBlob.Properties.CacheControl` özelliği.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="e5a0a-117">PowerShell için de kullanabilirsiniz [CDN profili ve uç noktaları yönetmek](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e5a0a-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="e5a0a-118">.NET için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="e5a0a-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="e5a0a-119">.NET kullanarak bir blob'un TTL ayarlamak için kullanın [.NET için Azure Storage istemci Kitaplığı](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ayarlamak için [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="e5a0a-120">Daha fazla sayıda .NET kod örnekleri kullanılabilir [.NET için Azure Blob Depolama örnek](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="e5a0a-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="e5a0a-121">Diğer yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e5a0a-121">Other methods</span></span>
* [<span data-ttu-id="e5a0a-122">Azure Komut Satırı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="e5a0a-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="e5a0a-123">Blob karşıya yüklenirken ayarlamak *cacheControl* özelliğini kullanarak `-p` geçin.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="e5a0a-124">Bu örnekte, TTL bir saat (3600 saniye) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="e5a0a-125">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="e5a0a-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="e5a0a-126">Açık olarak ayarlanıp *x-ms-blob-cache-control* özelliği bir [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put engelleme listesi](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), veya [Blob özelliklerini ayarla](https://msdn.microsoft.com/library/azure/ee691966.aspx) isteği.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="e5a0a-127">Üçüncü taraf Depolama Yönetimi Araçları</span><span class="sxs-lookup"><span data-stu-id="e5a0a-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="e5a0a-128">Bazı üçüncü taraf Azure Depolama Yönetimi araçlarını ayarlamanıza izin *CacheControl* BLOB'lar özelliği.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="e5a0a-129">Sınama *Cache-Control* üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="e5a0a-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="e5a0a-130">Bloblarınızın TTL kolayca doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="e5a0a-131">Tarayıcınızın kullanarak [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), blob de dahil olmak üzere test *Cache-Control* yanıtı üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="e5a0a-132">Gibi bir araç de kullanabilirsiniz **wget**, [Postman](https://www.getpostman.com/), veya [Fiddler](http://www.telerik.com/fiddler) yanıt üstbilgileri incelemek için.</span><span class="sxs-lookup"><span data-stu-id="e5a0a-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5a0a-133">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e5a0a-133">Next Steps</span></span>
* [<span data-ttu-id="e5a0a-134">Hakkında bilgi edinin *Cache-Control* üstbilgisi</span><span class="sxs-lookup"><span data-stu-id="e5a0a-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="e5a0a-135">Azure CDN içinde bulut hizmeti içeriğinin kullanım süresini yönetme öğrenin</span><span class="sxs-lookup"><span data-stu-id="e5a0a-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

