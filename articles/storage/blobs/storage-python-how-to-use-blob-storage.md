---
title: aaaHow toouse python'dan Azure Blob storage (nesne depolama) | Microsoft Docs
description: "Azure Blob storage (nesne depolama) ile Merhaba bulutta yapılandırılmamış veri depolayın."
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
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="4e3e3-103">Nasıl toouse python'dan Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="4e3e3-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4e3e3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4e3e3-104">Overview</span></span>
<span data-ttu-id="4e3e3-105">Azure Blob Depolama hello bulutta nesne/BLOB olarak yapılandırılmamış veri depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="4e3e3-106">Blob Storage belge, medya dosyası veya uygulama yükleyici gibi her tür metin veya ikili veri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="4e3e3-107">BLOB Depolama başvurulan tooas nesne depolama de olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="4e3e3-108">Bu makale size nasıl gösterir Blob storage kullanarak tooperform senaryoları.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="4e3e3-109">Merhaba örnekleri Python içinde yazılmış ve hello kullan [Python için Microsoft Azure depolama SDK].</span><span class="sxs-lookup"><span data-stu-id="4e3e3-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="4e3e3-110">karşıya yükleme, listeleme, indirme ve BLOB'ları silme kapsamdaki hello senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="4e3e3-111">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e3e3-111">Create a container</span></span>
<span data-ttu-id="4e3e3-112">Merhaba blob türüne göre toouse, istediğiniz oluşturma bir **BlockBlobService**, **AppendBlobService**, veya **PageBlobService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="4e3e3-113">Merhaba aşağıdaki kod kullanan bir **BlockBlobService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="4e3e3-114">Tooprogrammatically erişim Azure blok Blob Depolama istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın Hello aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="4e3e3-115">Merhaba aşağıdaki kod oluşturur bir **BlockBlobService** Merhaba, depolama hesabı adı ve hesap anahtarını kullanarak nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="4e3e3-116">'Myaccount' ve 'mykey' hesap adı ve anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="4e3e3-117">Aşağıdaki kod örneğine hello kullanabileceğiniz bir **BlockBlobService** yoksa nesne toocreate hello kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="4e3e3-118">(Daha önce yaptığınız gibi), depolama erişim anahtarınızı belirtmeniz gerekir böylece varsayılan olarak, hello yeni kapsayıcı özel, bu kapsayıcı toodownload bloblarından.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="4e3e3-119">Merhaba kapsayıcı kullanılabilir tooeveryone içinde toomake hello BLOB'lar istiyorsanız, hello kapsayıcı oluşturmak ve koddan hello kullanarak hello genel erişim düzeyini geçirin.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="4e3e3-120">Alternatif olarak, aşağıdaki kodu hello oluşturduktan sonra bir kapsayıcı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="4e3e3-121">Bu değişiklikten sonra hello Internet üzerinden herkes ortak bir kapsayıcıdaki blobları görebilir ancak yalnızca değiştirebilir veya silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="4e3e3-122">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="4e3e3-122">Upload a blob into a container</span></span>
<span data-ttu-id="4e3e3-123">toocreate blok blobu ve karşıya yükleme verileri kullanmak hello **oluşturma\_blob\_gelen\_yolu**, **oluşturma\_blob\_gelen\_akış**, **oluşturma\_blob\_gelen\_bayt** veya **oluşturma\_blob\_gelen\_metin** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="4e3e3-124">Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="4e3e3-125">**oluşturma\_blob\_gelen\_yolu** karşıya hello hello belirtilen yol, bir dosyanın içeriğini ve **oluşturma\_blob\_gelen\_akış** karşıya hello zaten açılmış bir dosya/akışı içeriği.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="4e3e3-126">**oluşturma\_blob\_gelen\_bayt** bayt dizisi yükler ve **oluşturma\_blob\_gelen\_metin** belirtilen hello yükler Belirtilen kodlama (Varsayılanları tooUTF-8) Hello kullanarak metin değeri.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="4e3e3-127">Merhaba aşağıdaki örnek yükler hello Merhaba içeriğine **sunset.png** hello dosyasına **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="4e3e3-128">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="4e3e3-128">List hello blobs in a container</span></span>
<span data-ttu-id="4e3e3-129">toolist hello BLOB'ları bir kapsayıcıda kullanmak hello **listesi\_BLOB'lar** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="4e3e3-130">Bu yöntem bir oluşturucuyu döndürür.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-130">This method returns a generator.</span></span> <span data-ttu-id="4e3e3-131">Merhaba aşağıdaki kodu çıkarır hello **adı** her BLOB bir kapsayıcı toohello konsolunda.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="4e3e3-132">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="4e3e3-132">Download blobs</span></span>
<span data-ttu-id="4e3e3-133">bir blob toodownload verileri kullan **almak\_blob\_için\_yolu**, **almak\_blob\_için\_akış**, **alma\_blob\_için\_bayt**, veya **almak\_blob\_için\_metin**.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="4e3e3-134">Bunlar hello verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştiren üst düzey yöntemleridir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="4e3e3-135">Merhaba aşağıdaki örneği kullanarak gösterir **almak\_blob\_için\_yolu** toodownload Merhaba içeriğine hello **myblob** toohello depolamakveblob**çıkış sunset.png** dosya.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="4e3e3-136">Blob silme</span><span class="sxs-lookup"><span data-stu-id="4e3e3-136">Delete a blob</span></span>
<span data-ttu-id="4e3e3-137">Son olarak, bir blob toodelete çağrısı **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="4e3e3-138">Yazma tooan blob ekleme</span><span class="sxs-lookup"><span data-stu-id="4e3e3-138">Writing tooan append blob</span></span>
<span data-ttu-id="4e3e3-139">Ek blob, günlük tutma gibi ekleme işlemleri için en iyi duruma getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="4e3e3-140">Bir blok blobu gibi bir ek blobu bloklardan oluşur, ancak yeni bir blok tooan ek blob eklediğinizde, bu her zaman eklenmiş toohello hello blob sonudur.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="4e3e3-141">Bir ek blobdaki mevcut bloğu güncelleştiremezsiniz veya silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="4e3e3-142">bir blok blobu olduğu gibi bir ek blobu Hello blok kimliği gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="4e3e3-143">Her bir ek blobu bloğunda tooa en fazla 4 MB yukarı farklı bir boyutta olabilir ve bir ek blobu en fazla 50.000 blok içerebilir.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="4e3e3-144">Merhaba en fazla bir ek blobu bu nedenle biraz 195 GB'tan (4 MB X 50.000 blok) boyutudur.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="4e3e3-145">Aşağıdaki Hello örnek yeni bir ek blob oluşturur ve basit günlük yazma işlemini benzeterek bazı veri tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="4e3e3-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e3e3-146">Next steps</span></span>
<span data-ttu-id="4e3e3-147">Blob storage'nın hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="4e3e3-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="4e3e3-148">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="4e3e3-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="4e3e3-149">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="4e3e3-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="4e3e3-150">[Azure Depolama Ekibi Blog’u]</span><span class="sxs-lookup"><span data-stu-id="4e3e3-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="4e3e3-151">[Python için Microsoft Azure depolama SDK]</span><span class="sxs-lookup"><span data-stu-id="4e3e3-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Depolama Ekibi Blog’u]: http://blogs.msdn.com/b/windowsazurestorage/
[Python için Microsoft Azure depolama SDK]: https://github.com/Azure/azure-storage-python
