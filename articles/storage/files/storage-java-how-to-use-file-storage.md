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
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="f0966-103">Java ile Azure File storage için geliştirme</span><span class="sxs-lookup"><span data-stu-id="f0966-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="f0966-104">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="f0966-104">About this tutorial</span></span>
<span data-ttu-id="f0966-105">Bu öğretici Java toodevelop uygulamalar veya Azure File storage toostore dosya verilerini kullanan Hizmetleri kullanma temelleri hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f0966-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="f0966-106">Bu öğreticide, basit bir konsol uygulaması oluşturur ve Göster nasıl tooperform temel eylemleri Java ve Azure File storage ile:</span><span class="sxs-lookup"><span data-stu-id="f0966-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="f0966-107">Oluşturma ve Azure dosya paylaşımları silme</span><span class="sxs-lookup"><span data-stu-id="f0966-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="f0966-108">Oluşturma ve dizinleri silme</span><span class="sxs-lookup"><span data-stu-id="f0966-108">Create and delete directories</span></span>
* <span data-ttu-id="f0966-109">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="f0966-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="f0966-110">Karşıya yükleyin, indirin ve dosya silme</span><span class="sxs-lookup"><span data-stu-id="f0966-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="f0966-111">SMB üzerinden Azure File storage erişilebileceği için hello standart Java g/ç sınıfları kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var.</span><span class="sxs-lookup"><span data-stu-id="f0966-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="f0966-112">Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama Java SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.</span><span class="sxs-lookup"><span data-stu-id="f0966-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="f0966-113">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0966-113">Create a Java application</span></span>
<span data-ttu-id="f0966-114">toobuild hello örnekleri, hello Java Geliştirme Seti (JDK) ve hello [Java için Azure depolama SDK] [] gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0966-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="f0966-115">Ayrıca bir Azure depolama hesabı oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="f0966-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="f0966-116">Uygulama toouse Azure File storage Kurulumu</span><span class="sxs-lookup"><span data-stu-id="f0966-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="f0966-117">toouse hello Azure depolama API'leri, deyimi toohello dosyasının üst kısmında tooaccess hello Depolama hizmetinden burada düşündüğünüz hello Java aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f0966-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="f0966-118">Bir Azure depolama bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f0966-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="f0966-119">Azure File storage toouse tooconnect tooyour Azure depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0966-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f0966-120">Merhaba ilk adımı tooconfigure kullanacağız bir bağlantı dizesi olacaktır tooconnect tooyour depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="f0966-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="f0966-121">Şimdi bir statik değişken toodo tanımlamak.</span><span class="sxs-lookup"><span data-stu-id="f0966-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="f0966-122">Your_storage_account_name ve your_storage_account_key depolama hesabınız için hello gerçek değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f0966-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="f0966-123">Tooan Azure depolama hesabı bağlanma</span><span class="sxs-lookup"><span data-stu-id="f0966-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="f0966-124">tooconnect tooyour depolama hesabı, gereksinim duyduğunuz toouse hello **CloudStorageAccount** nesnesinin bir bağlantı dizesi tooits **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f0966-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="f0966-125">**CloudStorageAccount.parse** tooput gerekir böylece InvalidKeyException bir try/catch içinde engelleyin.</span><span class="sxs-lookup"><span data-stu-id="f0966-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="f0966-126">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0966-126">Create an Azure File share</span></span>
<span data-ttu-id="f0966-127">Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="f0966-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="f0966-128">Depolama hesabınız hesap kapasitenizi verdiğinden kadar paylaşımları olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0966-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="f0966-129">tooobtain erişim tooa paylaşımı ve içeriklerini, toouse Azure dosya depolama istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0966-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="f0966-130">Hello Azure File storage İstemcisi'ni kullanarak bir başvuru tooa paylaşımı edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0966-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="f0966-131">tooactually hello paylaşımı oluşturmak, hello kullan **createIfNotExists** hello CloudFileShare nesnesinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f0966-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="f0966-132">Bu noktada, **paylaşmak** adlı bir başvuru tooa paylaşımı tutan **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="f0966-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="f0966-133">Bir Azure Dosya Paylaşımı Sil</span><span class="sxs-lookup"><span data-stu-id="f0966-133">Delete an Azure File share</span></span>
<span data-ttu-id="f0966-134">Bir paylaşım silme arama hello tarafından yapılır **deleteIfExists** CloudFileShare nesnesi üzerinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f0966-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="f0966-135">Yapan örnek kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f0966-135">Here's sample code that does that.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="f0966-136">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0966-136">Create a directory</span></span>
<span data-ttu-id="f0966-137">Ayrıca, bunların tümünün hello kök dizinine sahip olmak yerine alt dizinleri içindeki dosyaları koyarak depolama düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0966-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="f0966-138">Azure File storage hesabı olacak olarak kadar dizinler izin toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0966-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="f0966-139">Aşağıdaki Hello kodu adlı bir alt dizinin oluşturur **sampledir** hello kök dizininin altında.</span><span class="sxs-lookup"><span data-stu-id="f0966-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="f0966-140">Bir dizini silme</span><span class="sxs-lookup"><span data-stu-id="f0966-140">Delete a directory</span></span>
<span data-ttu-id="f0966-141">Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizininin silinmesi oldukça basit bir görev olduğundan.</span><span class="sxs-lookup"><span data-stu-id="f0966-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="f0966-142">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="f0966-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="f0966-143">Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **listFilesAndDirectories** CloudFileDirectory başvuru üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f0966-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="f0966-144">Merhaba yöntemi, üzerinde yineleyebilirsiniz ListFileItem nesnelerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f0966-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="f0966-145">Örnek olarak, hello aşağıdaki kod dosyaları ve dizinleri hello kök dizini içinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="f0966-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="f0966-146">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="f0966-146">Upload a file</span></span>
<span data-ttu-id="f0966-147">Bir Azure dosya paylaşımı hello çok az içerir, dosyalarının bulunduğu kök dizini.</span><span class="sxs-lookup"><span data-stu-id="f0966-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="f0966-148">Bu bölümde, nasıl tooupload hello üzerine yerel depolama biriminden bir dosya kök dizini bir paylaşımın öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f0966-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="f0966-149">bir dosyayı karşıya yüklemeyi hello ilk adımı tooobtain bulunduğu bir başvuru toohello dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f0966-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="f0966-150">Arama hello tarafından bunu **getRootDirectoryReference** hello Paylaşım nesnesinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f0966-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="f0966-151">Bir başvuru toohello kök dizin hello paylaşımının sahip olduğunuza göre koddan hello kullanarak oturum bir dosyayı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0966-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="f0966-152">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="f0966-152">Download a file</span></span>
<span data-ttu-id="f0966-153">Daha fazla Azure File storage karşı gerçekleştirecek işlemleri sık hello toodownload dosyaları biridir.</span><span class="sxs-lookup"><span data-stu-id="f0966-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="f0966-154">Merhaba, aşağıdaki örneğine hello kod SampleFile.txt indirir ve içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f0966-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="f0966-155">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="f0966-155">Delete a file</span></span>
<span data-ttu-id="f0966-156">Başka bir ortak Azure File storage dosya silme işlemdir.</span><span class="sxs-lookup"><span data-stu-id="f0966-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="f0966-157">Merhaba aşağıdaki kodu adlı bir dizin içinde depolanan SampleFile.txt adlı bir dosyayı siler **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="f0966-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f0966-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0966-158">Next steps</span></span>
<span data-ttu-id="f0966-159">Toolearn diğer Azure depolama API'leri hakkında daha fazla bilgi isterseniz, bu bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f0966-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="f0966-160">[Azure Java geliştiricilerinin](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="f0966-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="f0966-161">Azure depolama için Java SDK'sı</span><span class="sxs-lookup"><span data-stu-id="f0966-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="f0966-162">Azure depolama SDK'sı Android için</span><span class="sxs-lookup"><span data-stu-id="f0966-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="f0966-163">Azure Storage istemci SDK'sı başvurusu</span><span class="sxs-lookup"><span data-stu-id="f0966-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="f0966-164">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="f0966-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="f0966-165">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="f0966-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="f0966-166">[Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="f0966-166">[Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>