---
title: AzCopy kullanarak Azure Blob depolama biriminden aaaMove veri tooand | Microsoft Docs
description: "AzCopy kullanarak Azure Blob depolama alanından veri tooand Taşı"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>AzCopy kullanarak Azure Blob depolama alanından veri tooand Taşı
AzCopy karşıya yükleme, indirme ve Microsoft Azure blob, dosya ve tablo depolama kopyalama veri tooand için tasarlanmış bir komut satırı yardımcı programıdır.

AzCopy ve ek bilgiler hello Azure platformu ile kullanma hakkında yükleme ile ilgili yönergeler için bkz: [hello AzCopy komut satırı yardımcı programı ile çalışmaya başlama](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Tarafından sağlanan hello kodlarıyla ayarlanan VM kullanıyorsanız [veri bilimi sanal makinelerle](machine-learning-data-science-virtual-machines.md), sonra da AzCopy hello VM üzerinde zaten yüklü.
> 
> [!NOTE]
> Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu belge, bir depolama hesabı bir Azure aboneliğiniz varsa ve bu hesap için karşılık gelen depolama anahtarı hello varsayar. Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.

* bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).
* Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>AzCopy komutlarını çalıştırın
toorun AzCopy komutlar bir komut penceresi açın ve hello AzCopy.exe yürütülebilir bulunduğu bilgisayarınızda toohello AzCopy yükleme dizinine gidin. 

AzCopy komutları Hello temel sözdizimi şöyledir:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Merhaba AzCopy yükleme konumu tooyour sistem yolu ekleyin ve ardından herhangi bir dizinden hello komutları çalıştırın. Varsayılan olarak, AzCopy da yüklü olduğundan*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* veya *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Dosyaları tooan Azure blob karşıya yükleme
tooupload bir dosya hello aşağıdaki komutu kullanın:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Bir Azure blob üzerinden dosyaları indirme
bir Azure blob, komutu aşağıdaki kullanım hello dosyasından toodownload:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Azure kapsayıcı arasında aktarım BLOB'ları
tootransfer BLOB'ları Azure kapsayıcılar arasındaki hello aşağıdaki komutu kullanın:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>AzCopy kullanma ipuçları
> [!TIP]
> 1. Zaman **karşıya** dosyaları */S* dosyaları yinelemeli olarak yükler. Bu parametre olmadan dizinlerindeki dosyaları karşıya değil.  
> 2. Zaman **indirme** dosyası */S* aramaları tüm dosyaların hello belirtilen dizindeki ve alt dizinlerinde kadar kapsayıcısını özyinelemeli olarak hello veya verilen hello içinde belirtilen desenle eşleşen tüm dosyaları hello Dizin ve alt dizinlerinde yüklenir.  
> 3. Belirtemeyeceğiniz bir **belirli blob dosya** hello kullanarak toodownload */Source* parametresi. toodownload belirli bir dosya belirtin hello blob dosya adı toodownload hello kullanarak */desen* parametresi. **/S** parametresi bir dosya adı deseni yinelemeli olarak kullanılan toohave AzCopy Ara olabilir. Merhaba düzeni parametre olmadan, AzCopy dizindeki tüm dosyaları indirir.
> 
> 

