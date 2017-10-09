---
title: "bir Azure içeri/dışarı aktarma dışarı aktarma işinin - v1 için sürücü kullanımı aaaPreviewing | Microsoft Docs"
description: "Nasıl toopreview hello BLOB'ları listesi hello Azure içeri/dışarı aktarma hizmetinde dışa aktarma işi için seçtiğiniz öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="7d4c9-103">Dışarı aktarma işi için sürücü kullanımının önizlemesini yapma</span><span class="sxs-lookup"><span data-stu-id="7d4c9-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="7d4c9-104">Bir dışarı aktarma işinin oluşturmadan önce bir dizi BLOB toobe dışarı toochoose gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="7d4c9-105">Seçtiğiniz toorepresent hello BLOB'lar blob önekleri veya Hello Microsoft Azure içeri/dışarı aktarma hizmeti toouse blob yolların listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="7d4c9-106">Ardından, kaç tane sürücülere toodetermine ihtiyaç toosend gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="7d4c9-107">Merhaba içeri/dışarı aktarma aracı sağlar hello `PreviewExport` seçtiğiniz hello BLOB'lar için komut toopreview sürücü kullanımı, hello hello sürücüleri boyutuna göre toouse adımıdır.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="7d4c9-108">Komut satırı parametreleri</span><span class="sxs-lookup"><span data-stu-id="7d4c9-108">Command-line parameters</span></span>

<span data-ttu-id="7d4c9-109">Merhaba kullanırken şu parametreler hello kullanabilirsiniz `PreviewExport` hello içeri/dışarı aktarma aracı komutu.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="7d4c9-110">Komut satırı parametresi</span><span class="sxs-lookup"><span data-stu-id="7d4c9-110">Command-line parameter</span></span>|<span data-ttu-id="7d4c9-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d4c9-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="7d4c9-112">**/ LOGDIR:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="7d4c9-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="7d4c9-113">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-113">Optional.</span></span> <span data-ttu-id="7d4c9-114">Merhaba günlük dosyası dizini.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-114">hello log directory.</span></span> <span data-ttu-id="7d4c9-115">Ayrıntılı günlük dosyalarını toothis dizin yazılır.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="7d4c9-116">Günlük dizini belirtilirse, hello geçerli dizin hello günlük dizini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="7d4c9-117">**/sn:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="7d4c9-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="7d4c9-118">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-118">Required.</span></span> <span data-ttu-id="7d4c9-119">Merhaba depolama hesabının adını Hello hello için iş verin.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="7d4c9-120">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="7d4c9-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="7d4c9-121">Bir kapsayıcı SAS varsa ve yalnızca belirtilmemişse gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="7d4c9-122">Merhaba hesap anahtarı hello depolama hesabı hello için iş verin.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="7d4c9-123">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="7d4c9-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="7d4c9-124">Bir depolama hesabı anahtarı varsa ve yalnızca belirtilmemişse gerekli.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="7d4c9-125">Liste hello BLOB'lar toobe için Hello kapsayıcı SAS hello dışarı aktarma işinin dışarı.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="7d4c9-126">**/ ExportBlobListFile:**< ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="7d4c9-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="7d4c9-127">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-127">Required.</span></span> <span data-ttu-id="7d4c9-128">Yol toohello XML içeren blob yollar listesi dosya veya yol önekleri dışarı hello BLOB'lar toobe için blob.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="7d4c9-129">Hello kullanılan hello dosya biçimi `BlobListBlobPath` hello öğesinde [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello içeri/dışarı aktarma hizmeti REST API'si işlemi.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="7d4c9-130">**/ DriveSize:**< DriveSize\></span><span class="sxs-lookup"><span data-stu-id="7d4c9-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="7d4c9-131">Gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-131">Required.</span></span> <span data-ttu-id="7d4c9-132">Merhaba bir dışa aktarma işi için sürücüleri toouse boyutunu *ör*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="7d4c9-133">Komut satırı örneği</span><span class="sxs-lookup"><span data-stu-id="7d4c9-133">Command-line example</span></span>

<span data-ttu-id="7d4c9-134">Merhaba aşağıdaki örnekte gösterilmiştir hello `PreviewExport` komutu:</span><span class="sxs-lookup"><span data-stu-id="7d4c9-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="7d4c9-135">Merhaba ve dışa aktarma blob listesi dosyasının blob adları içeren önekleri, aşağıda gösterildiği gibi blob:</span><span class="sxs-lookup"><span data-stu-id="7d4c9-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="7d4c9-136">Hello Azure içeri/dışarı aktarma aracı dışarı aktarılan tüm BLOB'ları toobe listeler ve nasıl hello sürücülerin bunlara boyutu gerekli tüm ek yükü dikkate alarak, ardından sürücü hello sayısı tahminleri belirtilen toopack toohold hello BLOB'ları ve sürücü kullanımını gerekli hesaplar bilgi.</span><span class="sxs-lookup"><span data-stu-id="7d4c9-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="7d4c9-137">Atlanmış bilgilendirme günlükleriyle hello çıktısı örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7d4c9-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="7d4c9-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d4c9-138">Next steps</span></span>

* [<span data-ttu-id="7d4c9-139">Azure içeri/dışarı aktarma aracı başvurusu</span><span class="sxs-lookup"><span data-stu-id="7d4c9-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
