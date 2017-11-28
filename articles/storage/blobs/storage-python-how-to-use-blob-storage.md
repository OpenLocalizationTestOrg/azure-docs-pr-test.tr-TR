---
title: Python'dan Azure Blob storage (nesne depolama) kullanma | Microsoft Docs
description: "Azure Blob Storage (nesne depolama) ile bulutta yapılandırılmamış veri depolayın."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 1cab8407be6fc8932b68e50d0c301e8ea37ea3ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="1ddac-103">Python'dan Azure Blob storage kullanma</span><span class="sxs-lookup"><span data-stu-id="1ddac-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="1ddac-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1ddac-104">Overview</span></span>
<span data-ttu-id="1ddac-105">Azure Blob Storage, bulutta nesne/blob olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="1ddac-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="1ddac-107">Blob Storage aynı zamanda nesne depolama olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="1ddac-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="1ddac-108">Bu makalede yaygın senaryolar Blob storage kullanarak gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="1ddac-109">Python ve kullanım örnekleri yazılır [Python için Microsoft Azure depolama SDK].</span><span class="sxs-lookup"><span data-stu-id="1ddac-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="1ddac-110">Kapsamdaki senaryolar karşıya yükleme, listeleme, indirme ve BLOB'ları silme içerir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="1ddac-111">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ddac-111">Create a container</span></span>
<span data-ttu-id="1ddac-112">Kullanmak istediğiniz blob türüne göre oluşturma bir **BlockBlobService**, **AppendBlobService**, veya **PageBlobService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1ddac-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="1ddac-113">Aşağıdaki kod bir **BlockBlobService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1ddac-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="1ddac-114">Program aracılığıyla Azure blok Blob depolama alanına erişmek istediğiniz tüm Python dosyanın en üstüne yakın aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1ddac-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="1ddac-115">Aşağıdaki kod oluşturur bir **BlockBlobService** depolama hesabı adı ve hesap anahtarını kullanarak nesne.</span><span class="sxs-lookup"><span data-stu-id="1ddac-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="1ddac-116">'Myaccount' ve 'mykey' hesap adı ve anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ddac-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="1ddac-117">Aşağıdaki kod örneğinde kullanabileceğiniz bir **BlockBlobService** yoksa kapsayıcıyı oluşturulacak nesne.</span><span class="sxs-lookup"><span data-stu-id="1ddac-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="1ddac-118">(Daha önce yaptığınız gibi) Bu kapsayıcıdan BLOB indirmek için depolama erişim anahtarınızı belirtmeniz gerekir böylece varsayılan olarak, yeni özel kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="1ddac-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="1ddac-119">Kapsayıcı içinde BLOB'ları herkes tarafından kullanılabilmesini sağlamak istiyorsanız, kapsayıcı oluşturun ve aşağıdaki kodu kullanarak genel erişim düzeyini geçirin.</span><span class="sxs-lookup"><span data-stu-id="1ddac-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="1ddac-120">Alternatif olarak, aşağıdaki kodu kullanarak oluşturduktan sonra bir kapsayıcı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ddac-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="1ddac-121">Bu değişiklikten sonra Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak yalnızca değiştirebilir veya silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ddac-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="1ddac-122">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="1ddac-122">Upload a blob into a container</span></span>
<span data-ttu-id="1ddac-123">Bir blok blobu oluşturmak ve verileri yüklemek için kullanın **oluşturma\_blob\_gelen\_yolu**, **oluşturmak\_blob\_gelen\_akış**, **oluşturmak\_blob\_gelen\_bayt** veya **oluşturma\_blob\_gelen\_metin** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="1ddac-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="1ddac-124">Bunlar veri boyutu 64 MB aştığında gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="1ddac-125">**oluşturma\_blob\_gelen\_yolu** belirtilen yolun, bir dosyanın içeriğini yükler ve **oluşturma\_blob\_gelen\_akış** zaten açılmış bir dosya/akışı içeriğini yükler.</span><span class="sxs-lookup"><span data-stu-id="1ddac-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="1ddac-126">**oluşturma\_blob\_gelen\_bayt** bayt dizisi yükler ve **oluşturma\_blob\_gelen\_metin** belirtilen (varsayılan UTF-8) kodlaması kullanarak belirli bir metin değeri yükler.</span><span class="sxs-lookup"><span data-stu-id="1ddac-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="1ddac-127">Aşağıdaki örnek içeriğini yükler **sunset.png** içine dosya **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="1ddac-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="1ddac-128">Blob’ları bir kapsayıcıda listeleme</span><span class="sxs-lookup"><span data-stu-id="1ddac-128">List the blobs in a container</span></span>
<span data-ttu-id="1ddac-129">BLOB'ları bir kapsayıcıda listelemek için kullanın **listesi\_BLOB'lar** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ddac-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="1ddac-130">Bu yöntem bir oluşturucuyu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1ddac-130">This method returns a generator.</span></span> <span data-ttu-id="1ddac-131">Aşağıdaki kod çıktıları **adı** her BLOB bir kapsayıcıda konsoluna.</span><span class="sxs-lookup"><span data-stu-id="1ddac-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="1ddac-132">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="1ddac-132">Download blobs</span></span>
<span data-ttu-id="1ddac-133">Bir blob üzerinden veri indirmek için kullanın **almak\_blob\_için\_yolu**, **almak\_blob\_için\_akış**, **almak\_blob\_için\_bayt**, veya **almak\_blob\_için\_metin**.</span><span class="sxs-lookup"><span data-stu-id="1ddac-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="1ddac-134">Bunlar veri boyutu 64 MB aştığında gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="1ddac-135">Aşağıdaki örnek, kullanma gösterir **almak\_blob\_için\_yolu** içeriğini indirmek için **myblob** blob ve onun için depolamak **çıkış sunset.png** dosya.</span><span class="sxs-lookup"><span data-stu-id="1ddac-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="1ddac-136">Blob silme</span><span class="sxs-lookup"><span data-stu-id="1ddac-136">Delete a blob</span></span>
<span data-ttu-id="1ddac-137">Son olarak, bir blobu silmek için çağrı **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="1ddac-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="1ddac-138">Ek blobu yazma</span><span class="sxs-lookup"><span data-stu-id="1ddac-138">Writing to an append blob</span></span>
<span data-ttu-id="1ddac-139">Ek blob, günlük tutma gibi ekleme işlemleri için en iyi duruma getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="1ddac-140">Blok blobuna benzer şekilde bir ek blobu bloklardan oluşur ancak bir ek bloba yeni bir blok eklediğinizde her zaman blobun sonuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="1ddac-141">Bir ek blobdaki mevcut bloğu güncelleştiremezsiniz veya silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ddac-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="1ddac-142">Bir blok blobu olduğu için ek blobun blok kimliği gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="1ddac-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="1ddac-143">Her biri en fazla 4 MB olmak üzere bir ek blobundaki her blok farklı boyutlarda olabilir ve bir ek blobu en fazla 50.000 blok içerebilir.</span><span class="sxs-lookup"><span data-stu-id="1ddac-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="1ddac-144">Bu nedenle bir ek blobunun en büyük boyutu 195 GB’den biraz fazladır (4 MB x 50.000 blok).</span><span class="sxs-lookup"><span data-stu-id="1ddac-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="1ddac-145">Aşağıdaki örnek yeni bir ek blob oluşturur ve basit bir günlük yazma işlemini benzeterek buna veri ekler.</span><span class="sxs-lookup"><span data-stu-id="1ddac-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="1ddac-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ddac-146">Next steps</span></span>
<span data-ttu-id="1ddac-147">Blob Storage’ın temellerini öğrendiğinize göre, daha fazla bilgi edinmek için bu bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1ddac-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="1ddac-148">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="1ddac-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="1ddac-149">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="1ddac-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="1ddac-150">[Azure Depolama Ekibi Blog’u]</span><span class="sxs-lookup"><span data-stu-id="1ddac-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="1ddac-151">[Python için Microsoft Azure depolama SDK]</span><span class="sxs-lookup"><span data-stu-id="1ddac-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Depolama Ekibi Blog’u]: http://blogs.msdn.com/b/windowsazurestorage/
[Python için Microsoft Azure depolama SDK]: https://github.com/Azure/azure-storage-python
