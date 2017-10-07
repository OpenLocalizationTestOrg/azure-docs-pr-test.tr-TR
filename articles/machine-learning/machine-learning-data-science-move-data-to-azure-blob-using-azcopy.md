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
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="b448f-103">AzCopy kullanarak Azure Blob depolama alanından veri tooand Taşı</span><span class="sxs-lookup"><span data-stu-id="b448f-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="b448f-104">AzCopy karşıya yükleme, indirme ve Microsoft Azure blob, dosya ve tablo depolama kopyalama veri tooand için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="b448f-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="b448f-105">AzCopy ve ek bilgiler hello Azure platformu ile kullanma hakkında yükleme ile ilgili yönergeler için bkz: [hello AzCopy komut satırı yardımcı programı ile çalışmaya başlama](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b448f-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="b448f-106">Tarafından sağlanan hello kodlarıyla ayarlanan VM kullanıyorsanız [veri bilimi sanal makinelerle](machine-learning-data-science-virtual-machines.md), sonra da AzCopy hello VM üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="b448f-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="b448f-107">Bir tam giriş tooAzure blob depolama çok başvuran[Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve çok[Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="b448f-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b448f-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b448f-108">Prerequisites</span></span>
<span data-ttu-id="b448f-109">Bu belge, bir depolama hesabı bir Azure aboneliğiniz varsa ve bu hesap için karşılık gelen depolama anahtarı hello varsayar.</span><span class="sxs-lookup"><span data-stu-id="b448f-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="b448f-110">Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b448f-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="b448f-111">bir Azure aboneliği yukarı tooset bkz [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b448f-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b448f-112">Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b448f-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="b448f-113">AzCopy komutlarını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b448f-113">Run AzCopy commands</span></span>
<span data-ttu-id="b448f-114">toorun AzCopy komutlar bir komut penceresi açın ve hello AzCopy.exe yürütülebilir bulunduğu bilgisayarınızda toohello AzCopy yükleme dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="b448f-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="b448f-115">AzCopy komutları Hello temel sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b448f-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="b448f-116">Merhaba AzCopy yükleme konumu tooyour sistem yolu ekleyin ve ardından herhangi bir dizinden hello komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b448f-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="b448f-117">Varsayılan olarak, AzCopy da yüklü olduğundan*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* veya *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="b448f-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="b448f-118">Dosyaları tooan Azure blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="b448f-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="b448f-119">tooupload bir dosya hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b448f-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="b448f-120">Bir Azure blob üzerinden dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="b448f-120">Download files from an Azure blob</span></span>
<span data-ttu-id="b448f-121">bir Azure blob, komutu aşağıdaki kullanım hello dosyasından toodownload:</span><span class="sxs-lookup"><span data-stu-id="b448f-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="b448f-122">Azure kapsayıcı arasında aktarım BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="b448f-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="b448f-123">tootransfer BLOB'ları Azure kapsayıcılar arasındaki hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b448f-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="b448f-124">AzCopy kullanma ipuçları</span><span class="sxs-lookup"><span data-stu-id="b448f-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="b448f-125">Zaman **karşıya** dosyaları */S* dosyaları yinelemeli olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="b448f-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="b448f-126">Bu parametre olmadan dizinlerindeki dosyaları karşıya değil.</span><span class="sxs-lookup"><span data-stu-id="b448f-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="b448f-127">Zaman **indirme** dosyası */S* aramaları tüm dosyaların hello belirtilen dizindeki ve alt dizinlerinde kadar kapsayıcısını özyinelemeli olarak hello veya verilen hello içinde belirtilen desenle eşleşen tüm dosyaları hello Dizin ve alt dizinlerinde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b448f-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="b448f-128">Belirtemeyeceğiniz bir **belirli blob dosya** hello kullanarak toodownload */Source* parametresi.</span><span class="sxs-lookup"><span data-stu-id="b448f-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="b448f-129">toodownload belirli bir dosya belirtin hello blob dosya adı toodownload hello kullanarak */desen* parametresi.</span><span class="sxs-lookup"><span data-stu-id="b448f-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="b448f-130">**/S** parametresi bir dosya adı deseni yinelemeli olarak kullanılan toohave AzCopy Ara olabilir.</span><span class="sxs-lookup"><span data-stu-id="b448f-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="b448f-131">Merhaba düzeni parametre olmadan, AzCopy dizindeki tüm dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="b448f-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

