---
title: "Azure Portal kullanarak aaaTroubleshoot Azure Data Lake Analytics işlerini | Microsoft Docs"
description: "Nasıl toouse hello Azure Portal tootroubleshoot Data Lake Analytics işlerini öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="2f6da-103">Azure Portal kullanarak Azure Data Lake Analytics işlerini sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2f6da-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="2f6da-104">Nasıl toouse hello Azure Portal tootroubleshoot Data Lake Analytics işlerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2f6da-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="2f6da-105">Bu öğreticide, bir eksik kaynak dosyası sorunu Kurulum ve hello Azure Portal tootroubleshoot hello sorun kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f6da-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="2f6da-106">Data Lake Analytics işi gönderme</span><span class="sxs-lookup"><span data-stu-id="2f6da-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="2f6da-107">U-SQL işi aşağıdaki hello gönder:</span><span class="sxs-lookup"><span data-stu-id="2f6da-107">Submit hello following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="2f6da-108">Merhaba kaynak dosyası hello komut dosyasında tanımlı olan **/Samples/Data/SearchLog.tsv1**, burada olmalıdır **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="2f6da-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="2f6da-109">Merhaba işi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2f6da-109">Troubleshoot hello job</span></span>

<span data-ttu-id="2f6da-110">**toosee tüm işleri hello**</span><span class="sxs-lookup"><span data-stu-id="2f6da-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="2f6da-111">Hello ifadesini Azure portal'ı tıklatın **Microsoft Azure** hello sol üst köşedeki.</span><span class="sxs-lookup"><span data-stu-id="2f6da-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="2f6da-112">Data Lake Analytics hesap adınızı içeren Hello kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f6da-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="2f6da-113">Merhaba işi Özet hello üzerinde gösterilen **iş yönetimi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="2f6da-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Azure Data Lake Analytics iş yönetimi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="2f6da-115">Merhaba iş yönetimi hello iş durumunu bir bakışta sağlar.</span><span class="sxs-lookup"><span data-stu-id="2f6da-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="2f6da-116">Başarısız bir işi olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2f6da-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="2f6da-117">Merhaba tıklatın **iş yönetimi** toosee hello işleri kutucuğu.</span><span class="sxs-lookup"><span data-stu-id="2f6da-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="2f6da-118">Merhaba işleri kategorilere içinde **çalıştıran**, **sıraya alınan**, ve **sona erdi**.</span><span class="sxs-lookup"><span data-stu-id="2f6da-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="2f6da-119">Merhaba başarısız işinizde göreceksiniz **sona erdi** bölümü.</span><span class="sxs-lookup"><span data-stu-id="2f6da-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="2f6da-120">Birincisi hello listesinde olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2f6da-120">It shall be first one in hello list.</span></span> <span data-ttu-id="2f6da-121">İşlerini çok sahip olduğunuzda, tıklayabilirsiniz **filtre** toohelp, toolocate işler.</span><span class="sxs-lookup"><span data-stu-id="2f6da-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Azure Data Lake Analytics işleri filtreleyin](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="2f6da-123">Yeni bir dikey penceresinde hello listesi tooopen hello iş ayrıntıları Hello başarısız işi tıklayın:</span><span class="sxs-lookup"><span data-stu-id="2f6da-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Azure Data Lake Analytics işi başarısız oldu](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="2f6da-125">Bildirim hello **yeniden gönderin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2f6da-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="2f6da-126">Merhaba sorunu düzelttikten sonra hello işi yeniden gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f6da-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="2f6da-127">Vurgulanan bölümünden hello önceki ekran tooopen hello hata ayrıntıları'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2f6da-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="2f6da-128">Benzer bir şey göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="2f6da-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics işi ayrıntıları ile başarısız oldu.](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="2f6da-130">Merhaba kaynak klasörü bulunamadı söyler.</span><span class="sxs-lookup"><span data-stu-id="2f6da-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="2f6da-131">Tıklatın **yinelenen komut dosyası**.</span><span class="sxs-lookup"><span data-stu-id="2f6da-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="2f6da-132">Güncelleştirme hello **FROM** yolu toohello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2f6da-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="2f6da-133">"/ Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="2f6da-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="2f6da-134">**İşi Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f6da-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="2f6da-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="2f6da-135">See also</span></span>
* [<span data-ttu-id="2f6da-136">Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="2f6da-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="2f6da-137">Azure Data Lake Azure PowerShell kullanarak Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2f6da-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="2f6da-138">Azure Data Lake Analytics ve U-SQL Visual Studio kullanarak kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2f6da-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="2f6da-139">Azure Data Lake Analytics'i Azure Portal'ı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="2f6da-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
