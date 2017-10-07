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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>İçeri aktarma işlerinde sık kullanılan komutlar için hızlı başvuru
Bu bölüm, sık kullanılan komutlar için bazı hızlı başvuru sağlar. Ayrıntılı kullanımı için bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a>Hazırlama veri zaten olduğunda bir sabit sürücü toohello sabit diske kopyalanır
 Veri kopyalanan tooit zaten, ancak henüz BitLocker ile şifrelenmiş değil komutu aşağıdaki hello bir sabit sürücü hazırlar:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Bir tek bir dizin tooa sabit sürücüye kopyalama  
 komutu aşağıdaki hello henüz BitLocker ile şifrelenmiş olmayan bir tek kaynak dizini tooa sabit sürücüye kopyalar:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a>İki dizinleri tooa sabit diske kopyalama  
 toocopy iki kaynak dizinleri tooa sürücüsü, aşağıdaki komutları kullanın hello:  
  
 Merhaba ilk komut belirtir hello günlük dizini, depolama hesabı anahtarı, hedef sürücü harfi `format/encrypt` gereksinimleri ve ortak Parametreler:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 Merhaba ikinci komut hello günlük dosyası, yeni bir oturum kimliği ve hello kaynak ve hedef konumları belirtir:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>İkinci bir kopyası oturumda büyük dosya tooa sabit sürücü kopyalayın  
 komutu aşağıdaki hello önceki bir kopya oturumunda hazırlanan tek büyük dosya tooa sabit sürücü kopyalar:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Sonraki adımlar

* [Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
