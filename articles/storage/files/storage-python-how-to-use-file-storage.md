---
title: "Python ile Azure File storage için aaaDevelop | Microsoft Docs"
description: "Nasıl toodevelop Python uygulamalar ve Azure File storage toostore kullanan hizmetler dosya verileri öğrenin."
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
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="a4df3-103">Python ile Azure File storage için geliştirme</span><span class="sxs-lookup"><span data-stu-id="a4df3-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="a4df3-104">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="a4df3-104">About this tutorial</span></span>
<span data-ttu-id="a4df3-105">Bu öğretici Python toodevelop uygulamalar veya Azure File storage toostore dosya verilerini kullanan Hizmetleri kullanma temelleri hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a4df3-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="a4df3-106">Bu öğreticide, basit bir konsol uygulaması oluşturur ve Göster nasıl tooperform temel eylemleri Python ve Azure File storage ile:</span><span class="sxs-lookup"><span data-stu-id="a4df3-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="a4df3-107">Azure dosya paylaşımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4df3-107">Create Azure File shares</span></span>
* <span data-ttu-id="a4df3-108">Dizinler oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4df3-108">Create directories</span></span>
* <span data-ttu-id="a4df3-109">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="a4df3-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="a4df3-110">Karşıya yükleyin, indirin ve dosya silme</span><span class="sxs-lookup"><span data-stu-id="a4df3-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="a4df3-111">SMB üzerinden Azure File storage erişilebileceği için hello standart Python g/ç sınıfları ve işlevleri kullanarak hello Azure dosya paylaşımına erişim olası toowrite basit uygulamalar var.</span><span class="sxs-lookup"><span data-stu-id="a4df3-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="a4df3-112">Bu makalede nasıl kullanan toowrite uygulamaları hello kullanan Azure depolama Python SDK hello anlatmaktadır [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure dosya depolama.</span><span class="sxs-lookup"><span data-stu-id="a4df3-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="a4df3-113">Uygulama toouse Azure File storage ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a4df3-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="a4df3-114">Tooprogrammatically erişim Azure Storage istediğiniz herhangi bir Python kaynak dosyasının hello üstüne yakın Hello aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4df3-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="a4df3-115">Bir bağlantı tooAzure dosya depolama ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a4df3-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="a4df3-116">Merhaba `FileService` nesne paylaşımları, dizinleri ve dosyaları ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4df3-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="a4df3-117">Merhaba aşağıdaki kod oluşturur bir `FileService` Merhaba, depolama hesabı adı ve hesap anahtarını kullanarak nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a4df3-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="a4df3-118">Değiştir `<myaccount>` ve `<mykey>` , hesap adı ve anahtarınız ile.</span><span class="sxs-lookup"><span data-stu-id="a4df3-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="a4df3-119">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4df3-119">Create an Azure File share</span></span>
<span data-ttu-id="a4df3-120">Aşağıdaki kod örneğine hello kullanabileceğiniz bir `FileService` yoksa nesne toocreate hello paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="a4df3-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="a4df3-121">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4df3-121">Create a directory</span></span>
<span data-ttu-id="a4df3-122">Ayrıca, bunların tümünün hello kök dizinine sahip olmak yerine alt dizinleri içindeki dosyaları koyarak depolama düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4df3-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="a4df3-123">Azure File storage hesabı olacak olarak birden çok dizini izin toocreate sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4df3-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="a4df3-124">Aşağıdaki Hello kodu adlı bir alt dizinin oluşturur **sampledir** hello kök dizininin altında.</span><span class="sxs-lookup"><span data-stu-id="a4df3-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="a4df3-125">Dosya ve dizinlerin bir Azure dosya paylaşımında listeleme</span><span class="sxs-lookup"><span data-stu-id="a4df3-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="a4df3-126">toolist hello dosyaları ve dizinleri bir paylaşımda kullanmak hello **listesi\_dizinleri\_ve\_dosyaları** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a4df3-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="a4df3-127">Bu yöntem bir oluşturucuyu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a4df3-127">This method returns a generator.</span></span> <span data-ttu-id="a4df3-128">Merhaba aşağıdaki kodu çıkarır hello **adı** her bir dosya ve dizin paylaşımı toohello konsolunda.</span><span class="sxs-lookup"><span data-stu-id="a4df3-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="a4df3-129">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="a4df3-129">Upload a file</span></span> 
<span data-ttu-id="a4df3-130">Azure dosya paylaşımı hello çok az içerir, bir kök dizin dosyalarının bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="a4df3-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="a4df3-131">Bu bölümde, nasıl tooupload hello üzerine yerel depolama biriminden bir dosya kök dizini bir paylaşımın öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a4df3-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="a4df3-132">bir dosya toocreate ve karşıya yükleme verileri kullanmak hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` veya `create_file_from_text` yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="a4df3-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="a4df3-133">Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="a4df3-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a4df3-134">`create_file_from_path`Karşıya hello hello belirtilen yoldan dosya içeriğini ve `create_file_from_stream` karşıya hello zaten açılmış bir dosya/akışı içeriği.</span><span class="sxs-lookup"><span data-stu-id="a4df3-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="a4df3-135">`create_file_from_bytes`bayt dizisi yükler ve `create_file_from_text` karşıya hello belirtilen hello kullanarak metin değeri belirtilen kodlama (Varsayılanları tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="a4df3-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="a4df3-136">Merhaba aşağıdaki örnek yükler hello Merhaba içeriğine **sunset.png** hello dosyasına **myfile** dosya.</span><span class="sxs-lookup"><span data-stu-id="a4df3-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="a4df3-137">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="a4df3-137">Download a file</span></span>
<span data-ttu-id="a4df3-138">bir dosya toodownload verileri kullan `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, veya `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="a4df3-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="a4df3-139">Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="a4df3-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a4df3-140">Merhaba aşağıdaki örneği kullanarak gösterir `get_file_to_path` toodownload Merhaba içeriğine hello **myfile** toohello depolamak ve dosya **çıkış sunset.png** dosya.</span><span class="sxs-lookup"><span data-stu-id="a4df3-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="a4df3-141">Dosya silme</span><span class="sxs-lookup"><span data-stu-id="a4df3-141">Delete a file</span></span>
<span data-ttu-id="a4df3-142">Son olarak, bir dosya toodelete çağrı `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="a4df3-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="a4df3-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4df3-143">Next steps</span></span>
<span data-ttu-id="a4df3-144">Artık, öğrendiğinize göre nasıl toomanipulate Python, Azure File storage daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="a4df3-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="a4df3-145">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="a4df3-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="a4df3-146">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="a4df3-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="a4df3-147">Microsoft Azure depolama için Python SDK'sı</span><span class="sxs-lookup"><span data-stu-id="a4df3-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)