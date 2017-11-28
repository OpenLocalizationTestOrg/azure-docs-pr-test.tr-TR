---
title: "Azure içeri/dışarı aktarma aracı alma işi komutları - v1 için aaaQuick başvurusu | Microsoft Docs"
description: "Sık kullanılan alma işi komutları için Azure içeri/dışarı aktarma aracı komut başvurusu. Merhaba içeri/dışarı aktarma aracı toov1 başvuruyor."
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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="db87c-104">İçeri aktarma işlerinde sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="db87c-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="db87c-105">Bu bölüm, sık kullanılan komutlar için bazı hızlı başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="db87c-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="db87c-106">Ayrıntılı kullanımı için bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="db87c-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="db87c-107">Hazırlama veri zaten olduğunda bir sabit sürücü toohello sabit diske kopyalanır</span><span class="sxs-lookup"><span data-stu-id="db87c-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="db87c-108">Veri kopyalanan tooit zaten, ancak henüz BitLocker ile şifrelenmiş değil komutu aşağıdaki hello bir sabit sürücü hazırlar:</span><span class="sxs-lookup"><span data-stu-id="db87c-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="db87c-109">Bir tek bir dizin tooa sabit sürücüye kopyalama</span><span class="sxs-lookup"><span data-stu-id="db87c-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="db87c-110">komutu aşağıdaki hello henüz BitLocker ile şifrelenmiş olmayan bir tek kaynak dizini tooa sabit sürücüye kopyalar:</span><span class="sxs-lookup"><span data-stu-id="db87c-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="db87c-111">İki dizinleri tooa sabit diske kopyalama</span><span class="sxs-lookup"><span data-stu-id="db87c-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="db87c-112">toocopy iki kaynak dizinleri tooa sürücüsü, aşağıdaki komutları kullanın hello:</span><span class="sxs-lookup"><span data-stu-id="db87c-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="db87c-113">Merhaba ilk komut belirtir hello günlük dizini, depolama hesabı anahtarı, hedef sürücü harfi `format/encrypt` gereksinimleri ve ortak Parametreler:</span><span class="sxs-lookup"><span data-stu-id="db87c-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="db87c-114">Merhaba ikinci komut hello günlük dosyası, yeni bir oturum kimliği ve hello kaynak ve hedef konumları belirtir:</span><span class="sxs-lookup"><span data-stu-id="db87c-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="db87c-115">İkinci bir kopyası oturumda büyük dosya tooa sabit sürücü kopyalayın</span><span class="sxs-lookup"><span data-stu-id="db87c-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="db87c-116">komutu aşağıdaki hello önceki bir kopya oturumunda hazırlanan tek büyük dosya tooa sabit sürücü kopyalar:</span><span class="sxs-lookup"><span data-stu-id="db87c-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="db87c-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db87c-117">Next steps</span></span>

* [<span data-ttu-id="db87c-118">Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için</span><span class="sxs-lookup"><span data-stu-id="db87c-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
