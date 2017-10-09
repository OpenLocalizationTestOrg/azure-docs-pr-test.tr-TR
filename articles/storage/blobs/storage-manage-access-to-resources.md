---
title: "aaaEnable ortak okuma erişiminin kapsayıcılar ve bloblar Azure Blob depolamada için | Microsoft Docs"
description: "Bilgi nasıl toomake kapsayıcılar ve bloblar anonim erişim için kullanılabilir ve nasıl tooaccess bunları programlı olarak."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: dd8ffdb39a66aa06f65ad3cdd4315d47c117f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a>Anonim okuma erişimini toocontainers ve BLOB'ları yönetme
Anonim, ortak okuma erişimi tooa kapsayıcı ve bloblarını Azure Blob depolamada etkinleştirebilirsiniz. Bunu yaparak, hesap anahtarınızı paylaşımı ve paylaşılan erişim imzası (SAS) gerek olmadan toothese kaynaklarına salt okunur erişim verebilirsiniz.

Ortak okuma erişimi BLOB'lar tooalways anonim okuma erişimi için kullanılabilir belirli istediğiniz senaryolar için uygundur. Daha ayrıntılı denetim için bir paylaşılan erişim imzası oluşturabilirsiniz. Paylaşılan erişim imzaları tooprovide sınırlı erişimi belirli bir süre için farklı izinleri kullanarak etkinleştirin. Paylaşılan oluşturma hakkında daha fazla bilgi için erişim imzalar, bkz: [kullanarak paylaşılan erişim imzaları (SAS) Azure storage'da](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a>Anonim kullanıcılar izinleri toocontainers ve blobları verin
Varsayılan olarak, bir kapsayıcı ve içindeki tüm BLOB'ları yalnızca hello hello depolama hesabının sahibi tarafından erişilebilir. toogive anonim kullanıcıların Okuma izinleri tooa kapsayıcı ve bloblarını, hello kapsayıcı izinleri tooallow genel erişim ayarlayabilirsiniz. Anonim kullanıcılar genel olarak erişilebilir bir kapsayıcıdaki blobları hello isteği doğrulanmadan okuyabilir.

Bir kapsayıcı aşağıdaki izinleri hello ile yapılandırabilirsiniz:

* **Hiçbir public okuma erişimi:** hello kapsayıcı ve bloblarını yalnızca hello depolama hesabı sahibi tarafından erişilebilir. Bu, tüm yeni kapsayıcıları için hello varsayılan değerdir.
* **Genel erişim için BLOB'ları yalnızca okuma:** hello kapsayıcıdaki Blobları anonim istek tarafından okunabilir ancak kapsayıcı verileri kullanılabilir değil. Anonim istemcileri hello BLOB'lar hello kapsayıcıdaki numaralandırılamıyor.
* **Tam herkese okuma erişimi:** tüm kapsayıcı ve blob verilerini anonim istek tarafından okunabilir. İstemcileri hello kapsayıcıdaki blobları anonim istek göre sıralayabilirsiniz, ancak depolama hesabı Merhaba kapsayıcılara numaralandırılamıyor.

Aşağıdaki tooset kapsayıcı izinleri hello kullanabilirsiniz:

* [Azure portal](https://portal.azure.com)
* [Azure PowerShell](../common/storage-powershell-guide-full.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#how-to-manage-azure-blobs)
* [Azure CLI 2.0](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-and-manage-blobs)
* Program aracılığıyla, bir hello depolama istemcisi kitaplıklarını veya hello REST API kullanarak

### <a name="set-container-permissions-in-hello-azure-portal"></a>Hello Azure portal'ın kapsayıcı izinleri ayarlama
Merhaba tooset kapsayıcı izinleri [Azure portal](https://portal.azure.com), şu adımları izleyin:

1. Açık, **depolama hesabı** dikey penceresinde hello portal. Depolama hesabınızı seçerek bulabileceğiniz **depolama hesapları** hello ana portal menü dikey penceresinde.
1. Altında **BLOB hizmeti** hello menü dikey penceresinde, seçin **kapsayıcıları**.
1. Merhaba kapsayıcı satır veya select hello üç nokta tooopen hello kapsayıcının sağ **bağlam menüsü**.
1. Seçin **erişim ilkesi** hello bağlam menüsünde.
1. Seçin bir **erişim türüne** hello açılan menüsünde.

    ![Kapsayıcı meta verileri iletişim Düzenle](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a>.NET ile kapsayıcı izinleri ayarlama
.NET için C# ve hello depolama istemci kitaplığı kullanarak bir kapsayıcı tooset izinlerini tarafından arama hello ilk hello kapsayıcının var olan izinleri almak **GetPermissions** yöntemi. Ardından kümesi hello **PublicAccess** özelliği hello için **BlobContainerPermissions** hello tarafından döndürülen nesne **GetPermissions** yöntemi. Son olarak, hello çağrısı **izinleri ayarla** hello yöntemiyle izinleri güncelleştirildi.

Aşağıdaki örnek hello toofull herkese okuma erişimi hello kapsayıcının izinleri ayarlar. BLOB'ları yalnızca hello ayarlamak için tooset izinleri toopublic okuma erişiminin **PublicAccess** özelliği çok**BlobContainerPublicAccessType.Blob**. Anonim kullanıcılar için tüm izinleri tooremove ayarlama özelliği çok hello**BlobContainerPublicAccessType.Off**.

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a>Kapsayıcılar ve bloblar anonim erişim
Kapsayıcılar ve bloblar anonim olarak erişen istemci kimlik bilgileri gerektirmeyecek oluşturucular kullanabilir. Örnek hello birkaç farklı şekilde tooreference Blob hizmeti kaynakları anonim olarak göster.

### <a name="create-an-anonymous-client-object"></a>Anonim istemci nesnesi oluşturun
Merhaba hesabı için hello Blob Hizmeti uç noktası sağlayarak anonim erişim için yeni bir hizmet istemci nesnesi oluşturabilirsiniz. Ancak, bu hesaptaki anonim erişim için kullanılabilir bir kapsayıcı hello adını bilmeniz gerekir.

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a>Anonim olarak bir kapsayıcı başvurusu
Anonim olarak kullanılabilir hello URL tooa kapsayıcı varsa tooreference hello kapsayıcı doğrudan kullanabilirsiniz.

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a>Anonim olarak bir blob başvurusu
Anonim erişim için kullanılabilir hello URL tooa blob varsa, bu URL'yi kullanarak doğrudan hello blob başvurusu yapabilir:

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a>Özellikler kullanılabilir tooanonymous kullanıcılar
Aşağıdaki tablonun hello bir kapsayıcının ACL tooallow genel erişim ayarladığınızda, anonim kullanıcılar tarafından hangi işlemleri çağrılabilir gösterir.

| REST işlemi | Tam ortak okuma erişimi izni | Yalnızca BLOB'lar için herkese okuma erişimi izniyle |
| --- | --- | --- |
| Liste kapsayıcıları |Yalnızca sahibi |Yalnızca sahibi |
| Kapsayıcı oluşturma |Yalnızca sahibi |Yalnızca sahibi |
| Kapsayıcı özellikleri Al |Tümü |Yalnızca sahibi |
| Kapsayıcı meta verileri alma |Tümü |Yalnızca sahibi |
| Kapsayıcı meta verileri ayarlama |Yalnızca sahibi |Yalnızca sahibi |
| Kapsayıcı ACL Al |Yalnızca sahibi |Yalnızca sahibi |
| Kapsayıcı ACL ayarlayın |Yalnızca sahibi |Yalnızca sahibi |
| Kapsayıcısını silmek |Yalnızca sahibi |Yalnızca sahibi |
| Liste BLOB'ları |Tümü |Yalnızca sahibi |
| BLOB yerleştirme |Yalnızca sahibi |Yalnızca sahibi |
| BLOB alma |Tümü |Tümü |
| BLOB özelliklerini alma |Tümü |Tümü |
| Blob özelliklerini ayarlama |Yalnızca sahibi |Yalnızca sahibi |
| BLOB meta verileri alma |Tümü |Tümü |
| BLOB meta verileri ayarlama |Yalnızca sahibi |Yalnızca sahibi |
| Blok yerleştirme |Yalnızca sahibi |Yalnızca sahibi |
| Engelleme listesi (yalnızca kaydedilmiş engeller) Al |Tümü |Tümü |
| Engelleme listesi (yalnızca kaydedilmemiş blokları veya tüm blokları) Al |Yalnızca sahibi |Yalnızca sahibi |
| Engelleme listesi yerleştirme |Yalnızca sahibi |Yalnızca sahibi |
| BLOB Sil |Yalnızca sahibi |Yalnızca sahibi |
| BLOB kopyalama |Yalnızca sahibi |Yalnızca sahibi |
| Anlık görüntü Blob |Yalnızca sahibi |Yalnızca sahibi |
| Kira blob'u |Yalnızca sahibi |Yalnızca sahibi |
| Sayfa yerleştirin |Yalnızca sahibi |Yalnızca sahibi |
| Sayfa aralıklarını alma |Tümü |Tümü |
| BLOB ekleme |Yalnızca sahibi |Yalnızca sahibi |

## <a name="next-steps"></a>Sonraki adımlar

* [Hello Azure Storage Hizmetleri için kimlik doğrulaması](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [Paylaşılan erişim imzaları (SAS) kullanma](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Paylaşılan Erişim İmzası ile Erişim için Temsilci Seçme](https://msdn.microsoft.com/library/azure/ee395415.aspx)
