---
title: "Azure içeri/dışarı aktarma iş durumu - v1 aaaReviewing | Microsoft Docs"
description: "Bilgi nasıl oluşturduğunuzda toouse hello veya günlük dosyaları hello alma işi verme toosee hello hello içeri/dışarı aktarma işinin durumunu çalıştırıldı."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="c2340-103">Azure içeri/dışarı aktarma iş durumu kopyalama günlük dosyalarıyla gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="c2340-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="c2340-104">Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti bir içe veya dışa aktarma işi ile ilişkili sürücüleri işlediğinde, kendisinden, içeri aktarma veya BLOB'ları dışarı aktarma kopyalama günlük dosyaları toohello depolama hesabı tooor yazar.</span><span class="sxs-lookup"><span data-stu-id="c2340-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="c2340-105">Merhaba günlük dosyası, dışarı veya içeri aktarılan her dosya hakkında ayrıntılı durumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="c2340-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="c2340-106">tamamlanmış iş hello durumunu sorguladığınızda hello URL tooeach kopyalama günlük dosyası döndürülür; bkz: [alma işi](/rest/api/storageservices/Get-Job3) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="c2340-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="c2340-107">Örnek URL'leri</span><span class="sxs-lookup"><span data-stu-id="c2340-107">Example URLs</span></span>

<span data-ttu-id="c2340-108">Merhaba, örnek URL'ler için iki sürücü içeri aktarma işlemiyle kopyalama günlük dosyalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c2340-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="c2340-109">Bkz: [içeri/dışarı aktarma hizmeti günlük dosyası biçimi](storage-import-export-file-format-log.md) hello biçimi günlükleri ve durum kodları hello tam listesi için.</span><span class="sxs-lookup"><span data-stu-id="c2340-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c2340-110">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2340-110">Next steps</span></span>
 
 * [<span data-ttu-id="c2340-111">Kurulum hello Azure içeri/dışarı aktarma aracı</span><span class="sxs-lookup"><span data-stu-id="c2340-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="c2340-112">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="c2340-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="c2340-113">Bir içeri aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="c2340-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="c2340-114">Bir dışarı aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="c2340-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="c2340-115">Sorun giderme hello Azure içeri/dışarı aktarma aracı</span><span class="sxs-lookup"><span data-stu-id="c2340-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
