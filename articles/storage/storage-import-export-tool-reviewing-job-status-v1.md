---
title: "Azure içeri/dışarı aktarma iş durumu - v1 gözden geçirme | Microsoft Docs"
description: "İçeri/dışarı aktarma işinin durumunu görmek için içe veya dışa aktarma işlemi çalıştırıldığında oluşturulan günlük dosyalarını kullanmayı öğrenin."
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
ms.openlocfilehash: 621e41df127fded6ec6fe1f71e86cb8630965a70
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="61b06-103">Azure içeri/dışarı aktarma iş durumu kopyalama günlük dosyalarıyla gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="61b06-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="61b06-104">Microsoft Azure içeri/dışarı aktarma hizmeti bir içe veya dışa aktarma işi ile ilişkili sürücüleri işlediğinde, depolama hesabı için günlük dosyalarını veya içinden, içeri aktarma veya BLOB'ları dışarı aktarma kopyalama yazar.</span><span class="sxs-lookup"><span data-stu-id="61b06-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="61b06-105">Günlük dosyası, dışarı veya içeri aktarılan her dosya hakkında ayrıntılı durumunu içerir.</span><span class="sxs-lookup"><span data-stu-id="61b06-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="61b06-106">Tamamlanmış iş durumunu sorguladığınızda her kopya günlük dosyası için bir URL döndürülür; bkz: [alma işi](/rest/api/storageservices/Get-Job3) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="61b06-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="61b06-107">Örnek URL'leri</span><span class="sxs-lookup"><span data-stu-id="61b06-107">Example URLs</span></span>

<span data-ttu-id="61b06-108">Örnek URL'ler için iki sürücü içeri aktarma işlemiyle kopyalama günlük dosyalarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="61b06-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="61b06-109">Bkz: [içeri/dışarı aktarma hizmeti günlük dosyası biçimi](storage-import-export-file-format-log.md) günlükleri ve durum kodları tam listesi biçimi için.</span><span class="sxs-lookup"><span data-stu-id="61b06-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="61b06-110">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61b06-110">Next steps</span></span>
 
 * [<span data-ttu-id="61b06-111">Azure içeri/dışarı aktarma aracı ayarlama</span><span class="sxs-lookup"><span data-stu-id="61b06-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="61b06-112">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="61b06-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="61b06-113">Bir içeri aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="61b06-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="61b06-114">Bir dışarı aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="61b06-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="61b06-115">Azure İçeri/Dışarı Aktarma Aracı ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="61b06-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
