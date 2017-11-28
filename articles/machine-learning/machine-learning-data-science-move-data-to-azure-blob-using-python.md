---
title: Python kullanarak Azure Blob depolama biriminden aaaMove veri tooand | Microsoft Docs
description: "Python kullanarak Azure Blob depolama alanından veri tooand Taşı"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="ce194-103">Python kullanarak Azure Blob depolama alanından veri tooand Taşı</span><span class="sxs-lookup"><span data-stu-id="ce194-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="ce194-104">Bu konuda nasıl toolist, karşıya yükleme ve hello Python API kullanarak blob'lara karşıdan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ce194-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="ce194-105">Merhaba Python Azure SDK'SINDA sağlanan API ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ce194-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="ce194-106">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce194-106">Create a container</span></span>
* <span data-ttu-id="ce194-107">Bir kapsayıcıya bir blob yükleme</span><span class="sxs-lookup"><span data-stu-id="ce194-107">Upload a blob into a container</span></span>
* <span data-ttu-id="ce194-108">Blob’ları indirme</span><span class="sxs-lookup"><span data-stu-id="ce194-108">Download blobs</span></span>
* <span data-ttu-id="ce194-109">Liste hello BLOB'ları bir kapsayıcıda</span><span class="sxs-lookup"><span data-stu-id="ce194-109">List hello blobs in a container</span></span>
* <span data-ttu-id="ce194-110">Blob silme</span><span class="sxs-lookup"><span data-stu-id="ce194-110">Delete a blob</span></span>

<span data-ttu-id="ce194-111">Merhaba Python API kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse hello python'dan Blob Depolama hizmetinin](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ce194-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="ce194-112">Tarafından sağlanan hello kodlarıyla ayarlanan VM kullanıyorsanız [veri bilimi sanal makinelerle](machine-learning-data-science-virtual-machines.md), sonra da AzCopy hello VM üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="ce194-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ce194-113">Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce194-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ce194-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ce194-114">Prerequisites</span></span>
<span data-ttu-id="ce194-115">Bu belge, Azure aboneliği bir depolama hesabı ve o hesap için karşılık gelen depolama anahtar hello sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ce194-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="ce194-116">Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce194-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="ce194-117">bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce194-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ce194-118">Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ce194-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="ce194-119">Veri tooBlob karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="ce194-119">Upload Data tooBlob</span></span>
<span data-ttu-id="ce194-120">Aşağıdaki kod parçacığında tooprogrammatically erişim Azure Storage istediğiniz herhangi bir Python kodu hello üstündeki yakın hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ce194-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="ce194-121">Merhaba **BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce194-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ce194-122">koddan hello Merhaba, depolama hesabı adı ve hesap anahtarı kullanarak bir BlobService nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce194-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="ce194-123">Hesap adı ve hesap anahtarı gerçek hesabı ve anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ce194-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="ce194-124">Yöntemleri tooupload veri tooa blob aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ce194-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="ce194-125">PUT\_blok\_blob\_gelen\_(hello belirtilen yol bir dosyadan Merhaba içeriğine yükler) yolu</span><span class="sxs-lookup"><span data-stu-id="ce194-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="ce194-126">PUT\_block_blob\_gelen\_dosyası (zaten açılmış bir dosya/akışı hello içeriği yükler)</span><span class="sxs-lookup"><span data-stu-id="ce194-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="ce194-127">PUT\_blok\_blob\_gelen\_bayt (karşıya bir bayt dizisi)</span><span class="sxs-lookup"><span data-stu-id="ce194-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="ce194-128">PUT\_blok\_blob\_gelen\_metin (belirtilen hello yükler hello kullanarak metin değeri belirtilen kodlama)</span><span class="sxs-lookup"><span data-stu-id="ce194-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="ce194-129">Aşağıdaki örnek kod hello bir yerel dosya tooa kapsayıcı yükler:</span><span class="sxs-lookup"><span data-stu-id="ce194-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ce194-130">Merhaba aşağıdaki örnek kod (dizinleri hariç) tüm hello dosyaları yerel dizin tooblob depolama yükler:</span><span class="sxs-lookup"><span data-stu-id="ce194-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="ce194-131">Veri Blobundan indirin</span><span class="sxs-lookup"><span data-stu-id="ce194-131">Download Data from Blob</span></span>
<span data-ttu-id="ce194-132">Bir blob üzerinden yöntemleri toodownload veri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ce194-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="ce194-133">Alma\_blob\_için\_yolu</span><span class="sxs-lookup"><span data-stu-id="ce194-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="ce194-134">Alma\_blob\_için\_dosyası</span><span class="sxs-lookup"><span data-stu-id="ce194-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="ce194-135">Alma\_blob\_için\_bayt</span><span class="sxs-lookup"><span data-stu-id="ce194-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="ce194-136">Alma\_blob\_için\_metin</span><span class="sxs-lookup"><span data-stu-id="ce194-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="ce194-137">Merhaba verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştirmek bu yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="ce194-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="ce194-138">Merhaba aşağıdaki örnek kod bir blob kapsayıcı tooa yerel dosyasında hello içeriğini indirir:</span><span class="sxs-lookup"><span data-stu-id="ce194-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ce194-139">Merhaba aşağıdaki örnek kod tüm BLOB bir kapsayıcı yükler.</span><span class="sxs-lookup"><span data-stu-id="ce194-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="ce194-140">Liste kullanan\_tooget hello listesi kullanılabilir BLOB'ları hello kapsayıcıda BLOB'ların ve tooa yerel dizin indirir.</span><span class="sxs-lookup"><span data-stu-id="ce194-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
