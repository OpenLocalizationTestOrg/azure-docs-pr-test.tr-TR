---
title: "Python ile Azure File storage için geliştirme | Microsoft Docs"
description: "Python uygulamaları ve dosya verilerini depolamak için Azure File storage'ı kullanma hizmetleri geliştirmeyi öğrenin."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3dd14e8d3ea7d1e50f41633a7920a6d36becf789
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="348e6-103">Python ile Azure File storage için geliştirme</span><span class="sxs-lookup"><span data-stu-id="348e6-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="348e6-104">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="348e6-104">About this tutorial</span></span>
<span data-ttu-id="348e6-105">Bu öğretici, temel uygulamaları veya dosya verilerini depolamak için Azure dosya depolama kullanan hizmetler geliştirmek için Python kullanımını gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="348e6-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="348e6-106">Bu öğreticide, basit bir konsol uygulaması oluşturur ve Python ve Azure File storage ile temel eylemleri gerçekleştirme göster:</span><span class="sxs-lookup"><span data-stu-id="348e6-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="348e6-107">Azure dosya paylaşımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="348e6-107">Create Azure File shares</span></span>
* <span data-ttu-id="348e6-108">Dizinler oluşturma</span><span class="sxs-lookup"><span data-stu-id="348e6-108">Create directories</span></span>
* <span data-ttu-id="348e6-109">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="348e6-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="348e6-110">Karşıya yükleyin, indirin ve dosya silme</span><span class="sxs-lookup"><span data-stu-id="348e6-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="348e6-111">SMB üzerinden Azure File storage erişilebileceği için standart Python g/ç sınıfları ve işlevleri kullanarak Azure dosya paylaşımına erişim basit uygulamaları yazmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="348e6-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="348e6-112">Bu makalede Azure depolama Python kullanan SDK'ın, uygulamaların nasıl yazılacağını anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) Azure dosya depolama alanına anlaşmak için.</span><span class="sxs-lookup"><span data-stu-id="348e6-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="348e6-113">Uygulamanızı Azure File storage kullanacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="348e6-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="348e6-114">Azure Storage programlı olarak erişmek istediğiniz tüm Python kaynak dosyanın en üstüne yakın aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="348e6-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="348e6-115">Azure File storage için bir bağlantı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="348e6-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="348e6-116">`FileService` Nesne paylaşımları, dizinleri ve dosyaları ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="348e6-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="348e6-117">Aşağıdaki kod oluşturur bir `FileService` depolama hesabı adı ve hesap anahtarını kullanarak nesne.</span><span class="sxs-lookup"><span data-stu-id="348e6-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="348e6-118">Değiştir `<myaccount>` ve `<mykey>` , hesap adı ve anahtarınız ile.</span><span class="sxs-lookup"><span data-stu-id="348e6-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="348e6-119">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="348e6-119">Create an Azure File share</span></span>
<span data-ttu-id="348e6-120">Aşağıdaki kod örneğinde kullanabileceğiniz bir `FileService` yoksa paylaşımı oluşturmak için nesne.</span><span class="sxs-lookup"><span data-stu-id="348e6-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="348e6-121">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="348e6-121">Create a directory</span></span>
<span data-ttu-id="348e6-122">Depolama kök dizininde yerine bunların tümünün alt dizinleri içindeki dosyaları yerleştirerek de düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="348e6-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="348e6-123">Azure File storage hesabınıza izin verdiği sayıda dizinleri oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="348e6-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="348e6-124">Aşağıdaki kodu adlı bir alt dizinin oluşturacak **sampledir** kök dizininin altında.</span><span class="sxs-lookup"><span data-stu-id="348e6-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="348e6-125">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="348e6-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="348e6-126">Dosyaların ve dizinlerin bir paylaşımda listelemek için kullanın **listesi\_dizinleri\_ve\_dosyaları** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="348e6-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="348e6-127">Bu yöntem bir oluşturucuyu döndürür.</span><span class="sxs-lookup"><span data-stu-id="348e6-127">This method returns a generator.</span></span> <span data-ttu-id="348e6-128">Aşağıdaki kod çıktıları **adı** her bir dosya ve dizin konsoluna bir paylaşımda.</span><span class="sxs-lookup"><span data-stu-id="348e6-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="348e6-129">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="348e6-129">Upload a file</span></span> 
<span data-ttu-id="348e6-130">Azure dosya paylaşımı en azından içerir, bir kök dizin dosyalarının bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="348e6-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="348e6-131">Bu bölümde, bir paylaşım kök dizini üzerine yerel depolama biriminden bir dosya karşıya nasıl yükleneceğini öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="348e6-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="348e6-132">Bir dosya oluşturun ve verileri yüklemek için kullanmak `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` veya `create_file_from_text` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="348e6-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="348e6-133">Bunlar veri boyutu 64 MB aştığında gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="348e6-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="348e6-134">`create_file_from_path`Belirtilen yol bir dosyanın içeriğini yükler ve `create_file_from_stream` zaten açılmış bir dosya/akışı içeriğini yükler.</span><span class="sxs-lookup"><span data-stu-id="348e6-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="348e6-135">`create_file_from_bytes`bayt dizisi yükler ve `create_file_from_text` belirtilen (varsayılan UTF-8) kodlaması kullanarak belirli bir metin değeri yükler.</span><span class="sxs-lookup"><span data-stu-id="348e6-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="348e6-136">Aşağıdaki örnek içeriğini yükler **sunset.png** içine dosya **myfile** dosya.</span><span class="sxs-lookup"><span data-stu-id="348e6-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="348e6-137">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="348e6-137">Download a file</span></span>
<span data-ttu-id="348e6-138">Bir dosyadan veri indirmek için kullanacağınız `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, veya `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="348e6-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="348e6-139">Bunlar veri boyutu 64 MB aştığında gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="348e6-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="348e6-140">Aşağıdaki örnek, kullanma gösterir `get_file_to_path` içeriğini indirmek için **myfile** dosya ve onun için depolamak **çıkış sunset.png** dosya.</span><span class="sxs-lookup"><span data-stu-id="348e6-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="348e6-141">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="348e6-141">Delete a file</span></span>
<span data-ttu-id="348e6-142">Son olarak, bir dosyayı silmek için çağrı `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="348e6-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="348e6-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="348e6-143">Next steps</span></span>
<span data-ttu-id="348e6-144">Python ile Azure File storage işlemek nasıl öğrendiğinize göre daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="348e6-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="348e6-145">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="348e6-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="348e6-146">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="348e6-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="348e6-147">Microsoft Azure depolama için Python SDK'sı</span><span class="sxs-lookup"><span data-stu-id="348e6-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)