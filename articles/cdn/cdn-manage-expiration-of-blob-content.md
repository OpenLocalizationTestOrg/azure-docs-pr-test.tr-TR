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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Azure CDN Azure Storage bloblarında, bitiş tarihini Yönet
> [!div class="op_single_selector"]
> * [Azure Web Apps/bulut Hizmetleri, ASP.NET ve IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure depolama blob hizmeti](cdn-manage-expiration-of-blob-content.md)
> 
> 

Merhaba [blob hizmeti](../storage/common/storage-introduction.md#blob-storage) içinde [Azure Storage](../storage/common/storage-introduction.md) birkaç Azure tabanlı kaynakları birini Azure CDN ile tümleşiktir.  Kendi yaşam süresi (TTL) geçen kadar herhangi bir genel olarak erişilebilir blob içerik Azure CDN'de önbelleğe alınabilir.  Merhaba TTL hello tarafından belirlenir [ *Cache-Control* üstbilgi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) Azure depolama biriminden hello HTTP yanıt.

> [!TIP]
> Blob üzerindeki hiçbir TTL tooset seçebilirsiniz.  Bu durumda, Azure CDN varsayılan TTL yedi gün otomatik olarak uygular.
> 
> Hello Azure CDN toospeed erişim tooblobs ve diğer dosyaları nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure CDN'ye genel bakış](cdn-overview.md).
> 
> Hello Azure Storage blobu hizmeti hakkında daha fazla bilgi için bkz: [Blob hizmeti kavramları](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

Bu öğretici, Azure storage'da bir blob üzerinde hello TTL ayarlayabilirsiniz birkaç yol gösterir.  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) hello hızlı ve en güçlü şekilde tooadminister Azure hizmetlerinizi biridir.  Kullanım hello `Get-AzureStorageBlob` cmdlet tooget başvuru toohello blob hello ayarlamaktır `.ICloudBlob.Properties.CacheControl` özelliği. 

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
> PowerShell çok kullanabilirsiniz[CDN profili ve uç noktaları yönetmek](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>.NET için Depolama İstemci Kitaplığı
tooset blob kullanıcının .NET, kullanım hello kullanarak TTL [.NET için Azure Storage istemci Kitaplığı](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) özelliği.

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
> Daha fazla sayıda .NET kod örnekleri hello kullanılabilir [.NET için Azure Blob Depolama örnek](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Diğer yöntemleri
* [Azure Komut Satırı Arabirimi](../cli-install-nodejs.md)
  
    Merhaba blob karşıya yüklenirken hello ayarlamak *cacheControl* hello kullanarak özelliği `-p` geçin.  Bu örnek hello TTL tooone saat (3600 saniye cinsinden) ayarlar.
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Açıkça kümesi hello *x-ms-blob-cache-control* özelliği bir [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put engelleme listesi](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), veya [Blob özelliklerini ayarla](https://msdn.microsoft.com/library/azure/ee691966.aspx) isteği.
* Üçüncü taraf Depolama Yönetimi Araçları
  
    Bazı üçüncü taraf Azure Depolama Yönetimi araçlarını tooset hello izin *CacheControl* BLOB'lar özelliği. 

## <a name="testing-hello-cache-control-header"></a>Sınama hello *Cache-Control* üstbilgisi
Merhaba, BLOB TTL kolayca doğrulayabilirsiniz.  Tarayıcınızın kullanarak [Geliştirici Araçları](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), blob hello dahil olan test *Cache-Control* yanıtı üstbilgisi.  Gibi bir araç de kullanabilirsiniz **wget**, [Postman](https://www.getpostman.com/), veya [Fiddler](http://www.telerik.com/fiddler) tooexamine hello yanıt üstbilgileri.

## <a name="next-steps"></a>Sonraki Adımlar
* [Merhaba hakkında okuyun *Cache-Control* üstbilgisi](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Bilgi nasıl Azure CDN bulut hizmeti içeriğinin toomanage süre sonu](cdn-manage-expiration-of-cloud-service-content.md)

