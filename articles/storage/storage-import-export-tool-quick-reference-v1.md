---
title: "Hızlı başvuru için Azure içeri/dışarı aktarma aracı alma işi komutları - v1 | Microsoft Docs"
description: "Sık kullanılan alma işi komutları için Azure içeri/dışarı aktarma aracı komut başvurusu. İçeri/Dışarı Aktarma Aracı'nın v1 başvuruyor."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="7ca50-104">İçeri aktarma işlerinde sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="7ca50-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="7ca50-105">Bu bölüm, sık kullanılan komutlar için bazı hızlı başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ca50-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="7ca50-106">Ayrıntılı kullanımı için bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="7ca50-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="7ca50-107">Veri diskleri kopyalandığında diskleri hazırlayın</span><span class="sxs-lookup"><span data-stu-id="7ca50-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="7ca50-108">Verileri sabit sürücüye edilmiş edilmiş henüz tamamlanmamış kopyalandığında bir diskler hazırlamak için bir örnek komut İşte BitLocker ile şifrelenmiş:</span><span class="sxs-lookup"><span data-stu-id="7ca50-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="7ca50-109">Bir sabit sürücüye tek bir dizin kopyalama</span><span class="sxs-lookup"><span data-stu-id="7ca50-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="7ca50-110">Bir sabit sürücüye edilmiş edilmiş henüz tamamlanmamış tek bir kaynak dizin kopyalamak için bir örnek komut İşte BitLocker ile şifrelenmiş:</span><span class="sxs-lookup"><span data-stu-id="7ca50-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="7ca50-111">Bir sabit sürücüye wwo dizinleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="7ca50-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="7ca50-112">İki kaynak dizini bir sürücüye kopyalamak için iki komutları gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ca50-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="7ca50-113">İlk komut, günlük dizini, depolama hesabı anahtarı, hedef sürücü harfini belirtir ve `format/encrypt` ortak parametreler ek gereksinimler:</span><span class="sxs-lookup"><span data-stu-id="7ca50-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="7ca50-114">İkinci komut, günlük dosyası, yeni bir oturum kimliği ve kaynak ve hedef konumların belirtir:</span><span class="sxs-lookup"><span data-stu-id="7ca50-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="7ca50-115">Büyük bir dosya için bir sabit sürücü ikinci bir kopyası oturumda kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7ca50-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="7ca50-116">Önceki bir kopya oturumunda hazırlanmış bir sürücüye tek büyük bir dosya kopyalayan bir örnek komut şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7ca50-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="7ca50-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7ca50-117">Next steps</span></span>

* [<span data-ttu-id="7ca50-118">Sabit sürücüleri içeri aktarma işine hazırlamak için örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="7ca50-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
