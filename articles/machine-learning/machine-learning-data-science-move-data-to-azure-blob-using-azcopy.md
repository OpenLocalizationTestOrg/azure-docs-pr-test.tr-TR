---
title: "AzCopy kullanarak Azure Blob Storage gelen ve veri taşıma | Microsoft Docs"
description: "AzCopy kullanarak Azure Blob Depolamadan/Depolamaya Veri Taşıma"
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
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="7e3aa-103">AzCopy kullanarak Azure Blob Storage gelen ve veri taşıma</span><span class="sxs-lookup"><span data-stu-id="7e3aa-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="7e3aa-104">AzCopy karşıya yükleme, indirme ve veri kopyalamayı için ve Microsoft Azure blob, dosya ve tablo depolama için tasarlanmış bir komut satırı yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="7e3aa-105">Azure platformu kullanarak üzerinde AzCopy ve ek bilgiler yükleme ile ilgili yönergeler için bkz: [AzCopy komut satırı yardımcı programı ile çalışmaya başlama](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="7e3aa-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="7e3aa-106">Tarafından sağlanan kodlarıyla ayarlanan VM kullanıyorsanız [veri bilimi sanal makinelerle](machine-learning-data-science-virtual-machines.md), sonra da AzCopy VM üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="7e3aa-107">Azure blob depolama tam bir giriş için bkz [Azure Blob Temelleri](../storage/blobs/storage-dotnet-how-to-use-blobs.md) ve [Azure Blob hizmeti](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e3aa-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7e3aa-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7e3aa-108">Prerequisites</span></span>
<span data-ttu-id="7e3aa-109">Bu belge, Azure aboneliği, bir depolama hesabı ve o hesap için karşılık gelen depolama anahtarı sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="7e3aa-110">Karşıya yükleme/veri yüklemeden önce Azure depolama hesabı adı ve hesap anahtarınızın bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="7e3aa-111">Bir Azure aboneliği ayarlamak için bkz: [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e3aa-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7e3aa-112">Bir depolama hesabı oluşturma hakkında yönergeler ve hesabı ve anahtarı bilgilerini almak için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="7e3aa-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="7e3aa-113">AzCopy komutlarını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7e3aa-113">Run AzCopy commands</span></span>
<span data-ttu-id="7e3aa-114">AzCopy komutları çalıştırmak için bir komut penceresi açın ve yürütülebilir AzCopy.exe bulunduğu bilgisayarınızda AzCopy yükleme dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="7e3aa-115">AzCopy komutları temel sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7e3aa-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="7e3aa-116">AzCopy yükleme konumu, sistem yoluna ekleyin ve ardından herhangi bir dizinden komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="7e3aa-117">AzCopy varsayılan olarak, yüklü *% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* veya *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="7e3aa-118">Dosyaları bir Azure blobuna yükle</span><span class="sxs-lookup"><span data-stu-id="7e3aa-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="7e3aa-119">Bir dosyayı karşıya yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e3aa-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="7e3aa-120">Bir Azure blob üzerinden dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="7e3aa-120">Download files from an Azure blob</span></span>
<span data-ttu-id="7e3aa-121">Bir Azure blob üzerinden bir dosyayı indirmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e3aa-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="7e3aa-122">Azure kapsayıcı arasında aktarım BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="7e3aa-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="7e3aa-123">BLOB'ları Azure kapsayıcıları arasında aktarmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e3aa-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="7e3aa-124">AzCopy kullanma ipuçları</span><span class="sxs-lookup"><span data-stu-id="7e3aa-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="7e3aa-125">Zaman **karşıya** dosyaları */S* dosyaları yinelemeli olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="7e3aa-126">Bu parametre olmadan dizinlerindeki dosyaları karşıya değil.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="7e3aa-127">Zaman **indirme** dosyası */S* tüm dosyaları belirtilen dizinde ve alt dizinlerinde veya belirtilen dizinde ve alt dizinlerinde belirtilen desenle eşleşen, indirilen tüm dosyaları kadar kapsayıcısını özyinelemeli olarak arar.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="7e3aa-128">Belirtemeyeceğiniz bir **belirli blob dosya** kullanarak indirmek için */Source* parametresi.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="7e3aa-129">Belirli bir dosyayı indirmek için kullanarak indirmek için blob dosya adını belirtin. */desen* parametresi.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="7e3aa-130">**/S** parametresi için bir dosya adı deseni yinelemeli Ara AzCopy sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="7e3aa-131">Desen parametre olmadan, AzCopy dizindeki tüm dosyaları indirir.</span><span class="sxs-lookup"><span data-stu-id="7e3aa-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

