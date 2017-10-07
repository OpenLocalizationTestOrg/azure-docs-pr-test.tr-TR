---
title: "Java ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop Java uygulamaları ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Java ile Azure File storage için geliştirme
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici Java toodevelop uygulamalar veya Azure File storage toostore dosya verilerini kullanan Hizmetleri kullanma temelleri hello gösterilmektedir. Bu öğreticide, basit bir konsol uygulaması oluşturur ve Göster nasıl tooperform temel eylemleri Java ve Azure File storage ile:

* Oluşturma ve Azure dosya paylaşımları silme
* Oluşturma ve dizinleri silme
* Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
* Karşıya yükleyin, indirin ve dosya silme

> [!Note]  
> SMB üzerinden Azure File storage erişilebileceği için hello standart Java g/ç sınıfları kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var. Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama Java SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.

## <a name="create-a-java-application"></a>Java uygulaması oluşturma
toobuild hello örnekleri, hello Java Geliştirme Seti (JDK) ve hello [Java için Azure depolama SDK] [] gerekir. Ayrıca bir Azure depolama hesabı oluşturduğunuz.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Uygulama toouse Azure File storage Kurulumu
toouse hello Azure depolama API'leri, deyimi toohello dosyasının üst kısmında tooaccess hello Depolama hizmetinden burada düşündüğünüz hello Java aşağıdaki hello ekleyin.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesini ayarlayın
Azure File storage toouse tooconnect tooyour Azure depolama hesabınızın olması gerekir. Merhaba ilk adımı tooconfigure kullanacağız bir bağlantı dizesi olacaktır tooconnect tooyour depolama hesabı. Şimdi bir statik değişken toodo tanımlamak.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Your_storage_account_name ve your_storage_account_key depolama hesabınız için hello gerçek değerlerle değiştirin.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Tooan Azure depolama hesabı bağlanma
tooconnect tooyour depolama hesabı, gereksinim duyduğunuz toouse hello **CloudStorageAccount** nesnesinin bir bağlantı dizesi tooits **ayrıştırma** yöntemi.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** tooput gerekir böylece InvalidKeyException bir try/catch içinde engelleyin.

## <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma
Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**. Depolama hesabınız hesap kapasitenizi verdiğinden kadar paylaşımları olabilir. tooobtain erişim tooa paylaşımı ve içeriklerini, toouse Azure dosya depolama istemcisi gerekir.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Hello Azure File storage İstemcisi'ni kullanarak bir başvuru tooa paylaşımı edinebilirsiniz.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually hello paylaşımı oluşturmak, hello kullan **createIfNotExists** hello CloudFileShare nesnesinin yöntemi.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

Bu noktada, **paylaşmak** adlı bir başvuru tooa paylaşımı tutan **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Bir Azure Dosya Paylaşımı Sil
Bir paylaşım silme arama hello tarafından yapılır **deleteIfExists** CloudFileShare nesnesi üzerinde yöntemi. Yapan örnek kod aşağıda verilmiştir.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>Dizin oluşturma
Ayrıca, bunların tümünün hello kök dizinine sahip olmak yerine alt dizinleri içindeki dosyaları koyarak depolama düzenleyebilirsiniz. Azure File storage hesabı olacak olarak kadar dizinler izin toocreate sağlar. Aşağıdaki Hello kodu adlı bir alt dizinin oluşturur **sampledir** hello kök dizininin altında.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>Bir dizini silme
Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizininin silinmesi oldukça basit bir görev olduğundan.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **listFilesAndDirectories** CloudFileDirectory başvuru üzerinde. Merhaba yöntemi, üzerinde yineleyebilirsiniz ListFileItem nesnelerin bir listesini döndürür. Örnek olarak, hello aşağıdaki kod dosyaları ve dizinleri hello kök dizini içinde listelenir.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Dosyayı karşıya yükleme
Bir Azure dosya paylaşımı hello çok az içerir, dosyalarının bulunduğu kök dizini. Bu bölümde, nasıl tooupload hello üzerine yerel depolama biriminden bir dosya kök dizini bir paylaşımın öğreneceksiniz.

bir dosyayı karşıya yüklemeyi hello ilk adımı tooobtain bulunduğu bir başvuru toohello dizin oluşturur. Arama hello tarafından bunu **getRootDirectoryReference** hello Paylaşım nesnesinin yöntemi.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Bir başvuru toohello kök dizin hello paylaşımının sahip olduğunuza göre koddan hello kullanarak oturum bir dosyayı karşıya yükleyebilirsiniz.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Dosya indirme
Daha fazla Azure File storage karşı gerçekleştirecek işlemleri sık hello toodownload dosyaları biridir. Merhaba, aşağıdaki örneğine hello kod SampleFile.txt indirir ve içeriğini görüntüler.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>Dosya silme
Başka bir ortak Azure File storage dosya silme işlemdir. Merhaba aşağıdaki kodu adlı bir dizin içinde depolanan SampleFile.txt adlı bir dosyayı siler **sampledir**.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>Sonraki adımlar
Toolearn diğer Azure depolama API'leri hakkında daha fazla bilgi isterseniz, bu bağlantıları izleyin.

* [Java Geliştirici Merkezi](http://azure.microsoft.com/develop/java/)
* [Azure depolama için Java SDK'sı](https://github.com/azure/azure-storage-java)
* [Azure depolama SDK'sı Android için](https://github.com/azure/azure-storage-android)
* [Azure Storage istemci SDK'sı başvurusu](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)
