---
title: aaaHow toouse Java'dan Azure Blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a905d318abdaa7538ec3f6b53b5186b965b8b86e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Nasıl toouse Java'dan Blob storage
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Genel Bakış
Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir. Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir. BLOB Depolama başvurulan tooas nesne depolama de olabilir.

Bu makale nasıl Microsoft Azure Blob storage kullanarak tooperform genel senaryolar hello gösterir. Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure depolama SDK'sı][Azure Storage SDK for Java]. Merhaba kapsanan senaryolar dahil **karşıya**, **listeleme**, **indirme**, ve **silme** BLOB'lar. BLOB'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#Next-Steps) bölümü.

> [!NOTE]
> Bir SDK'sı, Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir. Daha fazla bilgi için bkz: Merhaba [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Java uygulaması oluşturma
Bu makalede, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.

toodo tooinstall ihtiyacınız olacak şekilde, Java Geliştirme Seti (JDK) hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun. Bunu yaptıktan sonra geliştirme sisteminizde hello en düşük gereksinimleri ve hello listelenen bağımlılıkları karşılayan tooverify gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki. Sisteminiz bu gereksinimleri karşılıyorsa, karşıdan yükleme ve bu depodan sisteminizdeki Java için hello Azure depolama kitaplıkları için hello yönergeleri izleyebilir. Bu görevleri tamamladıktan sonra mümkün toocreate hello örnekleri bu makalede kullanan bir Java uygulaması olacaktır.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Uygulama tooaccess Blob storage'ı yapılandırma
İçeri aktarma deyimlerini toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess BLOB'lar istediğiniz hello Java aşağıdaki hello ekleyin.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesi ayarlama
Bir Azure Storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri. Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello depolama hesabınızın adını kullanarak hello olarak sağlamak ve hello listelenen hello depolama hesabı için birincil erişim anahtarını hello gerekir [Azure portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri. Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hello hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve bir çağrı toohello ile erişilebilir  **RoleEnvironment.getConfigurationSettings** yöntemi. Merhaba aşağıdaki örnek alır hello bağlantı dizesinden bir **ayarı** adlı öğe *StorageConnectionString* hello hizmet yapılandırma dosyası.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.

## <a name="create-a-container"></a>Bir kapsayıcı oluşturma
A **CloudBlobClient** nesne kapsayıcılar ve bloblar için başvuru nesneleri alma olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **CloudBlobClient** nesnesi.

> [!NOTE]
> Başka bir yolu toocreate vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** hello içinde [Azure Storage istemci SDK'sı başvurusu].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Kullanım hello **CloudBlobClient** tooget toouse istediğiniz bir başvuru toohello kapsayıcı nesne. Merhaba ile yoksa hello kapsayıcı oluşturabilirsiniz **createIfNotExists** aksi hello var olan bir kapsayıcı döndürür yöntemi. (Daha önce yaptığınız gibi), depolama erişim anahtarınızı belirtmeniz gerekir böylece varsayılan olarak, hello yeni kapsayıcı özel, bu kapsayıcı toodownload bloblarından.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>İsteğe bağlı: genel erişim için bir kapsayıcı yapılandırın
Bir kapsayıcının izinleri varsayılan olarak özel erişim için yapılandırılmış, ancak hello Internet üzerinde bir kapsayıcının izinleri tooallow genel, salt okunur erişim tüm kullanıcılar için kolayca yapılandırabilirsiniz:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Bir kapsayıcıya bir blob yükleme
tooupload dosya tooa blob bir kapsayıcı başvurusu alın ve tooget bir blob başvurusu kullanın. Bir blob başvurusu edindiğinizde hello blob başvurusu üzerinde karşıya yükleme çağırarak tüm akış karşıya yükleyebilirsiniz. Mevcut veya varsa üzerine değildir, bu işlem hello blob oluşturun. Aşağıdaki kod örneği hello bu gösterir ve bu hello kapsayıcısı zaten oluşturduğunuzu varsayar.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Liste hello BLOB'ları bir kapsayıcıda
toolist hello BLOB'ları bir kapsayıcıda ilk alın bir kapsayıcı başvurusu blob tooupload yaptığınız gibi. Merhaba kapsayıcının kullanabilirsiniz **listBlobs** yöntemi ile bir **için** döngü. Merhaba aşağıdaki kodu hello her blob bir kapsayıcı toohello konsolunda URI'sini çıkarır.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Blobları adlarında yol bilgileriyle adlandırabilirsiniz unutmayın. Bu, geleneksel bir dosya sisteminde olduğu gibi düzenleme ve geçiş yapabileceğiniz sanal bir dizin yapısı oluşturur. Merhaba dizin yapısını yalnızca sanal - hello yalnızca Blob depolama alanına kullanılabilir kapsayıcılar ve bloblar kaynaklardır unutmayın. Ancak, hello istemci kitaplığı sunar bir **CloudBlobDirectory** nesne toorefer tooa sanal dizini ve bu şekilde düzenlenen BLOB'ları ile çalışmanın hello işlemini basitleştirir.

Örneğin, "" rootphoto1"," 2010/photo1"," 2010/photo2"adlı BLOB'ları ve" 2011/photo1"karşıya neden fotoğrafları" adlı bir kapsayıcı olabilir. Bu hello "2010" ve "2011" hello "fotoğrafları" kapsayıcı içindeki sanal dizinler oluşturur. Çağırdığınızda **listBlobs** hello "fotoğrafları" kapsayıcısı üzerinde döndürülen hello koleksiyonu içerir **CloudBlobDirectory** ve **CloudBlob** hello temsil eden nesneleri dizinleri ve blobları hello en üst düzeyde yer alan. Bu durumda, fotoğraf "rootphoto1" yanı sıra, dizinler "2010" ve "2011" döndürülür. Merhaba kullanabilirsiniz **instanceof** işleci toodistinguish bu nesneler.

İsteğe bağlı olarak, parametreleri toohello geçirebilirsiniz **listBlobs** hello yöntemiyle **Listblobs** parametresini tootrue ayarlayın. Bu bağımsız olarak dizin döndürülen her blob neden olur. Daha fazla bilgi için bkz: **CloudBlobContainer.listBlobs** hello içinde [Azure Storage istemci SDK'sı başvurusu].

## <a name="download-a-blob"></a>Blob indirme
toodownload BLOB'ları hello sipariş tooget bir blob başvurusu bir blob'a yüklemek için yaptığınız gibi aynı adımları izleyin. Örnek karşıya hello hello blob nesnesi üzerinde karşıya yükleme çağrılır. Aşağıdaki örneğine hello çağrı indirme tootransfer hello blob içeriği tooa stream nesnesi gibi bir **FileOutputStream** toopersist hello blob tooa yerel dosyasını kullanabilirsiniz.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Blob silme
toodelete bir blob alma bir blob başvurusu ve arama **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Bir blob kapsayıcısından silin
Son olarak, toodelete bir blob kapsayıcısını Al blob kapsayıcı başvurusu ve çağrı **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Sonraki adımlar
Blob storage'nın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* [Azure depolama için Java SDK'sı][Azure Storage SDK for Java]
* [Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]
* [Azure Storage REST API][Azure Storage REST API]
* [Azure depolama ekibi blogu][Azure Storage Team Blog]

Daha fazla bilgi için Ayrıca bkz. [Java geliştiriciler için Azure](/java/azure).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
