---
title: "aaaTroubleshooting hello Azure içeri/dışarı aktarma aracı | Microsoft Docs"
description: "Toohandle hello Azure içeri/dışarı aktarma aracı kullanarak ne zaman ve nasıl görülen hello ortak sorunlardan bazıları hakkında bilgi edinin bunları."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 254439c15797862dded5d80028b8780ad163b2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="60a06-103">Sorun giderme hello Azure içeri/dışarı aktarma aracı</span><span class="sxs-lookup"><span data-stu-id="60a06-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="60a06-104">sorunla çalıştırıyorsa hello Microsoft Azure içeri/dışarı aktarma aracı hata iletilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="60a06-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="60a06-105">Bu konuda, kullanıcıların içine çalışabilir bazı yaygın sorunlar listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="60a06-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="60a06-106">Kopya oturumu başarısız oluyor, ne yapmalıyım?</span><span class="sxs-lookup"><span data-stu-id="60a06-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="60a06-107">Kopya oturumu başarısız olduğunda, iki seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="60a06-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="60a06-108">Merhaba hata kısa dönem ve şimdi tekrar çevrimiçi için hello ağ paylaşımı çevrimdışıysa örneğin yeniden denenebilir ise, hello kopya oturumu devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60a06-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="60a06-109">Merhaba hata yeniden denenebilir, örneğin hello yanlış kaynak dosyası dizini hello komut satırı parametrelerinde belirtilen değilse tooabort hello kopya oturumu gerekir.</span><span class="sxs-lookup"><span data-stu-id="60a06-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="60a06-110">Bkz: [bir içeri aktarma işi için sabit sürücüler hazırlama](../storage-import-export-tool-preparing-hard-drives-import-v1.md) sürdürme ve kopyalama oturumları iptal etme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="60a06-110">See [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="60a06-111">I sürdürün veya bir kopya oturum iptal olamaz.</span><span class="sxs-lookup"><span data-stu-id="60a06-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="60a06-112">Merhaba kopyalama oturumdur hello bir sürücü için ilk kopyalama oturumu sonra hello hata iletisi belirtin: "Merhaba ilk kopya oturumu durduruldu veya sürdürülemez."</span><span class="sxs-lookup"><span data-stu-id="60a06-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="60a06-113">Bu durumda, hello eski günlük dosyasını silin ve hello komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="60a06-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="60a06-114">Birinci bir sürücü için bir kopya oturumu değil hello varsa, her zaman iptal edildi veya sürdürülebilir.</span><span class="sxs-lookup"><span data-stu-id="60a06-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="60a06-115">Merhaba günlük dosyası kayıp, hello iş oluşturabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="60a06-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="60a06-116">bir sürücü için Hello günlük dosyası veri toothis sürücüsü kopyalama hello tüm bilgileri içerir ve gerekli tooadd daha fazla dosyaları toohello sürücüsü ve kullanılan toocreate bir alma işi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="60a06-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="60a06-117">Merhaba günlük dosyası kaybolursa, tüm hello kopyalama oturumları hello sürücü için tooredo gerekir.</span><span class="sxs-lookup"><span data-stu-id="60a06-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="60a06-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60a06-118">Next steps</span></span>
 
* [<span data-ttu-id="60a06-119">Hello azure içeri/dışarı aktarma aracı ayarlama</span><span class="sxs-lookup"><span data-stu-id="60a06-119">Setting up hello azure import/export tool</span></span>](../storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="60a06-120">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="60a06-120">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="60a06-121">Kopyalama günlük dosyalarıyla iş durumunu gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="60a06-121">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="60a06-122">Bir içeri aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="60a06-122">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="60a06-123">Bir dışarı aktarma işini onarma</span><span class="sxs-lookup"><span data-stu-id="60a06-123">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
