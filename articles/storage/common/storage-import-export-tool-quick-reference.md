---
title: "Azure içeri/dışarı aktarma aracı alma işi komutları için aaaQuick başvurusu | Microsoft Docs"
description: "Sık kullanılan alma işi komutları için Azure içeri/dışarı aktarma aracı komut başvurusu."
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
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>İçeri aktarma işlerinde sık kullanılan komutlar için hızlı başvuru

Bu makale, sık kullanılan komutlar için bazı hızlı başvuru sağlar. Ayrıntılı kullanımı için bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](../storage-import-export-tool-preparing-hard-drives-import.md).

## <a name="first-session"></a>İlk oturumun

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a>İkinci oturum

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a>Son oturum iptal

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a>Son kesintiye uğramış oturum sürdürme

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a>Sürücüleri toolatest oturumu ekleme

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a>Sonraki adımlar

* [Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
