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
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Python kullanarak Azure Blob depolama alanından veri tooand Taşı
Bu konuda nasıl toolist, karşıya yükleme ve hello Python API kullanarak blob'lara karşıdan açıklanmaktadır. Merhaba Python Azure SDK'SINDA sağlanan API ile şunları yapabilirsiniz:

* Bir kapsayıcı oluşturma
* Bir kapsayıcıya bir blob yükleme
* Blob’ları indirme
* Liste hello BLOB'ları bir kapsayıcıda
* Blob silme

Merhaba Python API kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse hello python'dan Blob Depolama hizmetinin](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Tarafından sağlanan hello kodlarıyla ayarlanan VM kullanıyorsanız [veri bilimi sanal makinelerle](machine-learning-data-science-virtual-machines.md), sonra da AzCopy hello VM üzerinde zaten yüklü.
> 
> [!NOTE]
> Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu belge, Azure aboneliği bir depolama hesabı ve o hesap için karşılık gelen depolama anahtar hello sahip olduğunuzu varsayar. Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.

* bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).
* Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Veri tooBlob karşıya yükle
Aşağıdaki kod parçacığında tooprogrammatically erişim Azure Storage istediğiniz herhangi bir Python kodu hello üstündeki yakın hello ekleyin:

    from azure.storage.blob import BlobService

Merhaba **BlobService** nesne kapsayıcıları ve blob'larla çalışmanıza olanak sağlar. koddan hello Merhaba, depolama hesabı adı ve hesap anahtarı kullanarak bir BlobService nesnesi oluşturur. Hesap adı ve hesap anahtarı gerçek hesabı ve anahtarı ile değiştirin.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Yöntemleri tooupload veri tooa blob aşağıdaki hello kullan:

1. PUT\_blok\_blob\_gelen\_(hello belirtilen yol bir dosyadan Merhaba içeriğine yükler) yolu
2. PUT\_block_blob\_gelen\_dosyası (zaten açılmış bir dosya/akışı hello içeriği yükler)
3. PUT\_blok\_blob\_gelen\_bayt (karşıya bir bayt dizisi)
4. PUT\_blok\_blob\_gelen\_metin (belirtilen hello yükler hello kullanarak metin değeri belirtilen kodlama)

Aşağıdaki örnek kod hello bir yerel dosya tooa kapsayıcı yükler:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Merhaba aşağıdaki örnek kod (dizinleri hariç) tüm hello dosyaları yerel dizin tooblob depolama yükler:

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


## <a name="download-data-from-blob"></a>Veri Blobundan indirin
Bir blob üzerinden yöntemleri toodownload veri aşağıdaki hello kullan:

1. Alma\_blob\_için\_yolu
2. Alma\_blob\_için\_dosyası
3. Alma\_blob\_için\_bayt
4. Alma\_blob\_için\_metin

Merhaba verilerin hello boyutu 64 MB aştığında hello gerekli Öbekleme gerçekleştirmek bu yöntemleri.

Merhaba aşağıdaki örnek kod bir blob kapsayıcı tooa yerel dosyasında hello içeriğini indirir:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Merhaba aşağıdaki örnek kod tüm BLOB bir kapsayıcı yükler. Liste kullanan\_tooget hello listesi kullanılabilir BLOB'ları hello kapsayıcıda BLOB'ların ve tooa yerel dizin indirir.

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
