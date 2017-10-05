---
title: "Bir Azure içeri/dışarı aktarma dışarı aktarma işinin - v1 için sürücü kullanımı Önizleme | Microsoft Docs"
description: "Azure içeri/dışarı aktarma hizmetinde dışa aktarma işi için seçtiğiniz BLOB'ları listesi Önizleme öğrenin."
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
ms.openlocfilehash: 6ec74ae0b0931f3fed99a43f4f7e58f9d425b138
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="a561d-103">Dışarı aktarma işi için sürücü kullanımının önizlemesini yapma</span><span class="sxs-lookup"><span data-stu-id="a561d-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="a561d-104">Bir dışarı aktarma işinin oluşturmadan önce BLOB'ları dışarı kümesini seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a561d-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="a561d-105">Microsoft Azure içeri/dışarı aktarma hizmeti, blob yolların listesini kullanın veya seçtiğiniz BLOB'ları temsil etmek için önekleri blob olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a561d-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="a561d-106">Ardından, göndermesi gerekir. kaç tane sürücüleri belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a561d-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="a561d-107">İçeri/dışarı aktarma aracı sağlar `PreviewExport` bulacağınızı kullanmak için seçtiğiniz BLOB tabanlı için sürücüleri boyutuna sürücü kullanımı önizlemesini görmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="a561d-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="a561d-108">Komut satırı parametreleri</span><span class="sxs-lookup"><span data-stu-id="a561d-108">Command-line parameters</span></span>

<span data-ttu-id="a561d-109">Kullanırken aşağıdaki parametreleri kullanabilirsiniz `PreviewExport` içeri/dışarı aktarma aracı komutu.</span><span class="sxs-lookup"><span data-stu-id="a561d-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="a561d-110">Komut satırı parametresi</span><span class="sxs-lookup"><span data-stu-id="a561d-110">Command-line parameter</span></span>|<span data-ttu-id="a561d-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a561d-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="a561d-112">**/ LOGDIR:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="a561d-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="a561d-113">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="a561d-113">Optional.</span></span> <span data-ttu-id="a561d-114">Günlük dosyası dizini.</span><span class="sxs-lookup"><span data-stu-id="a561d-114">The log directory.</span></span> <span data-ttu-id="a561d-115">Bu dizin için ayrıntılı günlük dosyalarına yazılır.</span><span class="sxs-lookup"><span data-stu-id="a561d-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="a561d-116">Günlük dizini belirtilmezse, geçerli dizin günlük dizini olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a561d-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="a561d-117">**/sn:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="a561d-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="a561d-118">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="a561d-118">Required.</span></span> <span data-ttu-id="a561d-119">Dışa aktarma işi için depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="a561d-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="a561d-120">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="a561d-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="a561d-121">Bir kapsayıcı SAS varsa ve yalnızca belirtilmemişse gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a561d-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="a561d-122">Dışa aktarma işi için depolama hesabı için hesap anahtarı.</span><span class="sxs-lookup"><span data-stu-id="a561d-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="a561d-123">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="a561d-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="a561d-124">Bir depolama hesabı anahtarı varsa ve yalnızca belirtilmemişse gerekli.</span><span class="sxs-lookup"><span data-stu-id="a561d-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="a561d-125">BLOB'ları dışarı aktarma işinin dışarı aktarılmasına izin listesi için kapsayıcı SAS.</span><span class="sxs-lookup"><span data-stu-id="a561d-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="a561d-126">**/ ExportBlobListFile:**< ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="a561d-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="a561d-127">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="a561d-127">Required.</span></span> <span data-ttu-id="a561d-128">XML yolu içeren blob yollar listesi dosya veya yol önekleri verilecek BLOB'ları için blob.</span><span class="sxs-lookup"><span data-stu-id="a561d-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="a561d-129">Kullanılan dosya biçimi `BlobListBlobPath` öğesinde [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) içeri/dışarı aktarma hizmeti REST API'si işlemi.</span><span class="sxs-lookup"><span data-stu-id="a561d-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="a561d-130">**/ DriveSize:**< DriveSize\></span><span class="sxs-lookup"><span data-stu-id="a561d-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="a561d-131">Gerekli.</span><span class="sxs-lookup"><span data-stu-id="a561d-131">Required.</span></span> <span data-ttu-id="a561d-132">Bir dışarı aktarma işi için kullanılacak sürücüleri boyutunu *ör*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="a561d-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="a561d-133">Komut satırı örneği</span><span class="sxs-lookup"><span data-stu-id="a561d-133">Command-line example</span></span>

<span data-ttu-id="a561d-134">Aşağıdaki örnekte gösterilmiştir `PreviewExport` komutu:</span><span class="sxs-lookup"><span data-stu-id="a561d-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="a561d-135">Dışarı aktarma blob listeyi dosyası blob adları içeren ve önekleri, aşağıda gösterildiği gibi blob olabilir:</span><span class="sxs-lookup"><span data-stu-id="a561d-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="a561d-136">Azure içeri/dışarı aktarma aracı verilecek tüm BLOB'ları listeler ve gerekli tüm ek yükü dikkate alarak belirtilen boyutu, sürücü halinde paketlemek nasıl hesaplar, sonra BLOB'ları ve sürücü kullanım bilgilerini tutmak için gerekli sürücüleri sayısını tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="a561d-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="a561d-137">Atlanmış bilgilendirme günlükleriyle çıktısı örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a561d-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="a561d-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a561d-138">Next steps</span></span>

* [<span data-ttu-id="a561d-139">Azure içeri/dışarı aktarma aracı başvurusu</span><span class="sxs-lookup"><span data-stu-id="a561d-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
