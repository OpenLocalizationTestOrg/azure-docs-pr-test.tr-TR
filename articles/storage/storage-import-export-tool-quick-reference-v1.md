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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>İçeri aktarma işlerinde sık kullanılan komutlar için hızlı başvuru
Bu bölüm, sık kullanılan komutlar için bazı hızlı başvuru sağlar. Ayrıntılı kullanımı için bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a>Veri diskleri kopyalandığında diskleri hazırlayın
 Verileri sabit sürücüye edilmiş edilmiş henüz tamamlanmamış kopyalandığında bir diskler hazırlamak için bir örnek komut İşte BitLocker ile şifrelenmiş:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a>Bir sabit sürücüye tek bir dizin kopyalama  
 Bir sabit sürücüye edilmiş edilmiş henüz tamamlanmamış tek bir kaynak dizin kopyalamak için bir örnek komut İşte BitLocker ile şifrelenmiş:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a>Bir sabit sürücüye wwo dizinleri kopyalama  
 İki kaynak dizini bir sürücüye kopyalamak için iki komutları gerekir.  
  
 İlk komut, günlük dizini, depolama hesabı anahtarı, hedef sürücü harfini belirtir ve `format/encrypt` ortak parametreler ek gereksinimler:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 İkinci komut, günlük dosyası, yeni bir oturum kimliği ve kaynak ve hedef konumların belirtir:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a>Büyük bir dosya için bir sabit sürücü ikinci bir kopyası oturumda kopyalayın.  
 Önceki bir kopya oturumunda hazırlanmış bir sürücüye tek büyük bir dosya kopyalayan bir örnek komut şöyledir:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Sonraki adımlar

* [Sabit sürücüleri içeri aktarma işine hazırlamak için örnek iş akışı](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
