---
title: "Java ile Azure File storage için geliştirme | Microsoft Docs"
description: "Java uygulamaları ve dosya verilerini depolamak için Azure File storage'ı kullanma hizmetleri geliştirmeyi öğrenin."
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
ms.openlocfilehash: 16924599e49990265e07f7a58613756d93c46942
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Java ile Azure File storage için geliştirme
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğreticide uygulama veya dosya verilerini depolamak için Azure File storage'ı kullanma hizmetleri geliştirmek için Java kullanarak temelleri gösterilmektedir. Bu öğreticide, basit bir konsol uygulaması oluşturur ve Java ve Azure File storage ile temel eylemleri gerçekleştirme göster:

* Oluşturma ve Azure dosya paylaşımları silme
* Oluşturma ve dizinleri silme
* Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
* Karşıya yükleyin, indirin ve dosya silme

> [!Note]  
> SMB üzerinden Azure File storage erişilebileceği için standart Java g/ç sınıfları kullanarak Azure dosya paylaşımına erişim basit uygulamaları yazmak mümkündür. Bu makalede Azure depolama Java kullanan SDK'ın, uygulamaların nasıl yazılacağını anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) Azure dosya depolama alanına anlaşmak için.

## <a name="create-a-java-application"></a>Java uygulaması oluşturma
Örnekleri oluşturmak için Java Geliştirme Seti (JDK) ve [Java için Azure depolama SDK] [] gerekir. Ayrıca bir Azure depolama hesabı oluşturduğunuz.

## <a name="setup-your-application-to-use-azure-file-storage"></a>Azure File storage kullanmak için uygulamanızı kurma
Azure depolama API'leri kullanmak için şu deyimi ve storage hizmetinden erişmek istiyorsanız burada Java dosyanın en üstüne ekleyin.

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesini ayarlayın
Azure File storage kullanmak için Azure depolama hesabınıza bağlanmanız gerekir. İlk adım, depolama hesabınıza bağlanmak için kullanacağız bir bağlantı dizesini yapılandırmak için olacaktır. Şimdi bunun için statik bir değişken tanımlayın.

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Your_storage_account_name ve your_storage_account_key depolama hesabınız için gerçek değerlerle değiştirin.
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a>Bir Azure depolama hesabına bağlanma
Depolama hesabınıza bağlanmak için kullanmanız gerekir **CloudStorageAccount** bir bağlantı dizesi geçirme nesne, kendi **ayrıştırma** yöntemi.

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

**CloudStorageAccount.parse** try/catch bloğunun içine yerleştirilecek gerekir böylece bir InvalidKeyException oluşturur.

## <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma
Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**. Depolama hesabınız hesap kapasitenizi verdiğinden kadar paylaşımları olabilir. Bir paylaşımı ve içeriklerini erişim sağlamak için Azure dosya depolama istemcisi kullanmanız gerekir.

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Azure File storage İstemcisi'ni kullanarak bir paylaşım için bir başvuru edinebilirsiniz.

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

Gerçekte paylaşımı oluşturmak için kullanın **createIfNotExists** CloudFileShare nesnesinin yöntemi.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

Bu noktada, **paylaşmak** adlı bir paylaşım için bir başvuru tutan **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Bir Azure Dosya Paylaşımı Sil
Bir paylaşım silme yapılır çağırarak **deleteIfExists** CloudFileShare nesnesi üzerinde yöntemi. Yapan örnek kod aşağıda verilmiştir.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>Dizin oluşturma
Depolama kök dizininde yerine bunların tümünün alt dizinleri içindeki dosyaları yerleştirerek de düzenleyebilirsiniz. Azure File storage hesabınıza izin verdiği kadar dizinleri oluşturmanıza olanak sağlar. Aşağıdaki kodu adlı bir alt dizinin oluşturacak **sampledir** kök dizininin altında.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
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
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme
Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **listFilesAndDirectories** CloudFileDirectory başvuru üzerinde. Yöntemi, üzerinde yineleyebilirsiniz ListFileItem nesnelerin bir listesini döndürür. Örnek olarak, aşağıdaki kod, dosyalar ve dizinler kök dizini içinde listelenir.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Dosyayı karşıya yükleme
Bir Azure dosya paylaşımı en azından içerir, dosyalarının bulunduğu kök dizini. Bu bölümde, bir paylaşım kök dizini üzerine yerel depolama biriminden bir dosya karşıya nasıl yükleneceğini öğreneceksiniz.

Bir dosyayı karşıya yüklemeyi ilk adımı bulunduğu dizin başvuru elde edilir. Çağırarak bunu **getRootDirectoryReference** Paylaşım nesnesinin yöntemi.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Bir başvuru paylaşımının kök dizinine sahip olduğunuza göre üzerine aşağıdaki kodu kullanarak bir dosyayı karşıya yükleyebilirsiniz.

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Dosya indirme
Azure File storage karşı gerçekleştirecek daha sık işlemleri dosyalarını indirmek için biridir. Aşağıdaki örnekte, kod SampleFile.txt indirir ve içeriğini görüntüler.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>Dosya silme
Başka bir ortak Azure File storage dosya silme işlemdir. Aşağıdaki kod adlı bir dizin içinde depolanan SampleFile.txt adlı bir dosyayı siler **sampledir**.

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>Sonraki adımlar
Diğer Azure depolama API'leri hakkında daha fazla bilgi edinmek istiyorsanız, bu bağlantıları izleyin.

* [Java Geliştirici Merkezi](http://azure.microsoft.com/develop/java/)
* [Azure depolama için Java SDK'sı](https://github.com/azure/azure-storage-java)
* [Azure depolama SDK'sı Android için](https://github.com/azure/azure-storage-android)
* [Azure Storage istemci SDK'sı başvurusu](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)
* [AzCopy Komut Satırı Yardımcı Programı ile veri aktarımı](storage-use-azcopy.md)