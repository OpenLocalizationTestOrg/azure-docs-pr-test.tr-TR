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
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="6da1e-103">Java ile Azure File storage için geliştirme</span><span class="sxs-lookup"><span data-stu-id="6da1e-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="6da1e-104">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="6da1e-104">About this tutorial</span></span>
<span data-ttu-id="6da1e-105">Bu öğreticide uygulama veya dosya verilerini depolamak için Azure File storage'ı kullanma hizmetleri geliştirmek için Java kullanarak temelleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="6da1e-106">Bu öğreticide, basit bir konsol uygulaması oluşturur ve Java ve Azure File storage ile temel eylemleri gerçekleştirme göster:</span><span class="sxs-lookup"><span data-stu-id="6da1e-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="6da1e-107">Oluşturma ve Azure dosya paylaşımları silme</span><span class="sxs-lookup"><span data-stu-id="6da1e-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="6da1e-108">Oluşturma ve dizinleri silme</span><span class="sxs-lookup"><span data-stu-id="6da1e-108">Create and delete directories</span></span>
* <span data-ttu-id="6da1e-109">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="6da1e-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="6da1e-110">Karşıya yükleyin, indirin ve dosya silme</span><span class="sxs-lookup"><span data-stu-id="6da1e-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="6da1e-111">SMB üzerinden Azure File storage erişilebileceği için standart Java g/ç sınıfları kullanarak Azure dosya paylaşımına erişim basit uygulamaları yazmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="6da1e-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="6da1e-112">Bu makalede Azure depolama Java kullanan SDK'ın, uygulamaların nasıl yazılacağını anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) Azure dosya depolama alanına anlaşmak için.</span><span class="sxs-lookup"><span data-stu-id="6da1e-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="6da1e-113">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da1e-113">Create a Java application</span></span>
<span data-ttu-id="6da1e-114">Örnekleri oluşturmak için Java Geliştirme Seti (JDK) ve [Java için Azure depolama SDK] [] gerekir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="6da1e-115">Ayrıca bir Azure depolama hesabı oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="6da1e-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="6da1e-116">Azure File storage kullanmak için uygulamanızı kurma</span><span class="sxs-lookup"><span data-stu-id="6da1e-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="6da1e-117">Azure depolama API'leri kullanmak için şu deyimi ve storage hizmetinden erişmek istiyorsanız burada Java dosyanın en üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6da1e-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="6da1e-118">Bir Azure depolama bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6da1e-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="6da1e-119">Azure File storage kullanmak için Azure depolama hesabınıza bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="6da1e-120">İlk adım, depolama hesabınıza bağlanmak için kullanacağız bir bağlantı dizesini yapılandırmak için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6da1e-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="6da1e-121">Şimdi bunun için statik bir değişken tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6da1e-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="6da1e-122">Your_storage_account_name ve your_storage_account_key depolama hesabınız için gerçek değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6da1e-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="6da1e-123">Bir Azure depolama hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="6da1e-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="6da1e-124">Depolama hesabınıza bağlanmak için kullanmanız gerekir **CloudStorageAccount** bir bağlantı dizesi geçirme nesne, kendi **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6da1e-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="6da1e-125">**CloudStorageAccount.parse** try/catch bloğunun içine yerleştirilecek gerekir böylece bir InvalidKeyException oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6da1e-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="6da1e-126">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da1e-126">Create an Azure File share</span></span>
<span data-ttu-id="6da1e-127">Tüm dosyaları ve dizinleri Azure dosya depolama olarak adlandırılan bir kapsayıcıda yer bir **paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="6da1e-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="6da1e-128">Depolama hesabınız hesap kapasitenizi verdiğinden kadar paylaşımları olabilir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="6da1e-129">Bir paylaşımı ve içeriklerini erişim sağlamak için Azure dosya depolama istemcisi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="6da1e-130">Azure File storage İstemcisi'ni kullanarak bir paylaşım için bir başvuru edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6da1e-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="6da1e-131">Gerçekte paylaşımı oluşturmak için kullanın **createIfNotExists** CloudFileShare nesnesinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6da1e-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="6da1e-132">Bu noktada, **paylaşmak** adlı bir paylaşım için bir başvuru tutan **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="6da1e-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="6da1e-133">Bir Azure Dosya Paylaşımı Sil</span><span class="sxs-lookup"><span data-stu-id="6da1e-133">Delete an Azure File share</span></span>
<span data-ttu-id="6da1e-134">Bir paylaşım silme yapılır çağırarak **deleteIfExists** CloudFileShare nesnesi üzerinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6da1e-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="6da1e-135">Yapan örnek kod aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-135">Here's sample code that does that.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="6da1e-136">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="6da1e-136">Create a directory</span></span>
<span data-ttu-id="6da1e-137">Depolama kök dizininde yerine bunların tümünün alt dizinleri içindeki dosyaları yerleştirerek de düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6da1e-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="6da1e-138">Azure File storage hesabınıza izin verdiği kadar dizinleri oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6da1e-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="6da1e-139">Aşağıdaki kodu adlı bir alt dizinin oluşturacak **sampledir** kök dizininin altında.</span><span class="sxs-lookup"><span data-stu-id="6da1e-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="6da1e-140">Bir dizini silme</span><span class="sxs-lookup"><span data-stu-id="6da1e-140">Delete a directory</span></span>
<span data-ttu-id="6da1e-141">Hala dosyaları içeren bir dizin veya diğer dizinleri silemezsiniz unutulmamalıdır rağmen bir dizininin silinmesi oldukça basit bir görev olduğundan.</span><span class="sxs-lookup"><span data-stu-id="6da1e-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="6da1e-142">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="6da1e-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="6da1e-143">Dosya ve dizinlerin bir paylaşımı içinde listesini alma kolayca yapılır çağırarak **listFilesAndDirectories** CloudFileDirectory başvuru üzerinde.</span><span class="sxs-lookup"><span data-stu-id="6da1e-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="6da1e-144">Yöntemi, üzerinde yineleyebilirsiniz ListFileItem nesnelerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="6da1e-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="6da1e-145">Örnek olarak, aşağıdaki kod, dosyalar ve dizinler kök dizini içinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="6da1e-146">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="6da1e-146">Upload a file</span></span>
<span data-ttu-id="6da1e-147">Bir Azure dosya paylaşımı en azından içerir, dosyalarının bulunduğu kök dizini.</span><span class="sxs-lookup"><span data-stu-id="6da1e-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="6da1e-148">Bu bölümde, bir paylaşım kök dizini üzerine yerel depolama biriminden bir dosya karşıya nasıl yükleneceğini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6da1e-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="6da1e-149">Bir dosyayı karşıya yüklemeyi ilk adımı bulunduğu dizin başvuru elde edilir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="6da1e-150">Çağırarak bunu **getRootDirectoryReference** Paylaşım nesnesinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6da1e-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="6da1e-151">Bir başvuru paylaşımının kök dizinine sahip olduğunuza göre üzerine aşağıdaki kodu kullanarak bir dosyayı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6da1e-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="6da1e-152">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="6da1e-152">Download a file</span></span>
<span data-ttu-id="6da1e-153">Azure File storage karşı gerçekleştirecek daha sık işlemleri dosyalarını indirmek için biridir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="6da1e-154">Aşağıdaki örnekte, kod SampleFile.txt indirir ve içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6da1e-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="6da1e-155">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="6da1e-155">Delete a file</span></span>
<span data-ttu-id="6da1e-156">Başka bir ortak Azure File storage dosya silme işlemdir.</span><span class="sxs-lookup"><span data-stu-id="6da1e-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="6da1e-157">Aşağıdaki kod adlı bir dizin içinde depolanan SampleFile.txt adlı bir dosyayı siler **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="6da1e-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6da1e-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6da1e-158">Next steps</span></span>
<span data-ttu-id="6da1e-159">Diğer Azure depolama API'leri hakkında daha fazla bilgi edinmek istiyorsanız, bu bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6da1e-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="6da1e-160">Java Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="6da1e-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="6da1e-161">Azure depolama için Java SDK'sı</span><span class="sxs-lookup"><span data-stu-id="6da1e-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="6da1e-162">Azure depolama SDK'sı Android için</span><span class="sxs-lookup"><span data-stu-id="6da1e-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="6da1e-163">Azure Storage istemci SDK'sı başvurusu</span><span class="sxs-lookup"><span data-stu-id="6da1e-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="6da1e-164">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="6da1e-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="6da1e-165">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="6da1e-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="6da1e-166">AzCopy Komut Satırı Yardımcı Programı ile veri aktarımı</span><span class="sxs-lookup"><span data-stu-id="6da1e-166">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)