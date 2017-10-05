---
title: "Azure içeri/dışarı aktarma aracı alma işi komutlar için hızlı başvuru | Microsoft Docs"
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
ms.openlocfilehash: e9377e0c5001cf5be220e19e06ff96c1e058e853
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="5dd17-103">İçeri aktarma işlerinde sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="5dd17-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="5dd17-104">Bu makale, sık kullanılan komutlar için bazı hızlı başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="5dd17-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="5dd17-105">Ayrıntılı kullanımı için bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="5dd17-105">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="5dd17-106">İlk oturumun</span><span class="sxs-lookup"><span data-stu-id="5dd17-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="5dd17-107">İkinci oturum</span><span class="sxs-lookup"><span data-stu-id="5dd17-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="5dd17-108">Son oturum iptal</span><span class="sxs-lookup"><span data-stu-id="5dd17-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="5dd17-109">Son kesintiye uğramış oturum sürdürme</span><span class="sxs-lookup"><span data-stu-id="5dd17-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-to-latest-session"></a><span data-ttu-id="5dd17-110">En son oturumuna sürücü ekleme</span><span class="sxs-lookup"><span data-stu-id="5dd17-110">Add drives to latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="5dd17-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5dd17-111">Next steps</span></span>

* [<span data-ttu-id="5dd17-112">Sabit sürücüleri içeri aktarma işine hazırlamak için örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="5dd17-112">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
