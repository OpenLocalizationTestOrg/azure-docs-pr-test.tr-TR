---
title: "Azure Portal kullanarak Azure Data Lake Analytics işlerini sorunlarını giderme | Microsoft Docs"
description: "Data Lake Analytics işlerini gidermek için Azure Portalı'nı kullanmayı öğrenin. "
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
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="e14d2-103">Azure Portal kullanarak Azure Data Lake Analytics işlerini sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e14d2-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="e14d2-104">Data Lake Analytics işlerini gidermek için Azure Portalı'nı kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e14d2-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="e14d2-105">Bu öğreticide, bir eksik kaynak dosyası sorunu Kurulum ve sorun giderme için Azure Portalı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e14d2-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="e14d2-106">Data Lake Analytics işi gönderme</span><span class="sxs-lookup"><span data-stu-id="e14d2-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="e14d2-107">Aşağıdaki U-SQL işi gönder:</span><span class="sxs-lookup"><span data-stu-id="e14d2-107">Submit the following U-SQL job:</span></span>

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
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="e14d2-108">Komut dosyasında tanımlı kaynak dosyası **/Samples/Data/SearchLog.tsv1**, burada olmalıdır **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="e14d2-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="e14d2-109">İş sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e14d2-109">Troubleshoot the job</span></span>

<span data-ttu-id="e14d2-110">**Tüm işleri görmek için**</span><span class="sxs-lookup"><span data-stu-id="e14d2-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="e14d2-111">Azure portalından tıklatın **Microsoft Azure** sol üst köşedeki.</span><span class="sxs-lookup"><span data-stu-id="e14d2-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="e14d2-112">Data Lake Analytics hesap adınızı içeren kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e14d2-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="e14d2-113">İş özeti gösterilir **iş yönetimi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="e14d2-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Azure Data Lake Analytics iş yönetimi](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="e14d2-115">Proje yönetimi, iş durumunu bir bakışta sağlar.</span><span class="sxs-lookup"><span data-stu-id="e14d2-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="e14d2-116">Başarısız bir işi olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e14d2-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="e14d2-117">Tıklatın **iş yönetimi** işleri görmek için döşeme.</span><span class="sxs-lookup"><span data-stu-id="e14d2-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="e14d2-118">İşlerini kategorilere ayrılır **çalıştıran**, **sıraya alınan**, ve **sona erdi**.</span><span class="sxs-lookup"><span data-stu-id="e14d2-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="e14d2-119">Başarısız işinizde göreceksiniz **sona erdi** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e14d2-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="e14d2-120">Listedeki ilk bir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e14d2-120">It shall be first one in the list.</span></span> <span data-ttu-id="e14d2-121">İşlerini çok sahip olduğunuzda, tıklayabilirsiniz **filtre** işleri bulmanıza yardımcı olacak.</span><span class="sxs-lookup"><span data-stu-id="e14d2-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Azure Data Lake Analytics işleri filtreleyin](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="e14d2-123">Yeni bir dikey pencerede iş ayrıntılarını açmak için listeden başarısız işi tıklayın:</span><span class="sxs-lookup"><span data-stu-id="e14d2-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure Data Lake Analytics işi başarısız oldu](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="e14d2-125">Bildirim **yeniden gönderin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e14d2-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="e14d2-126">Sorunu düzelttikten sonra işi yeniden gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e14d2-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="e14d2-127">Hata ayrıntılarını açmak için önceki ekran görüntüsünde vurgulanan bölümünden'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e14d2-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="e14d2-128">Benzer bir şey göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="e14d2-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics işi ayrıntıları ile başarısız oldu.](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="e14d2-130">Kaynak klasörü bulunamadı söyler.</span><span class="sxs-lookup"><span data-stu-id="e14d2-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="e14d2-131">Tıklatın **yinelenen komut dosyası**.</span><span class="sxs-lookup"><span data-stu-id="e14d2-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="e14d2-132">Güncelleştirme **FROM** aşağıdaki yolu:</span><span class="sxs-lookup"><span data-stu-id="e14d2-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="e14d2-133">"/ Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="e14d2-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="e14d2-134">**İşi Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e14d2-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="e14d2-135">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e14d2-135">See also</span></span>
* [<span data-ttu-id="e14d2-136">Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="e14d2-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="e14d2-137">Azure Data Lake Azure PowerShell kullanarak Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e14d2-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="e14d2-138">Azure Data Lake Analytics ve U-SQL Visual Studio kullanarak kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e14d2-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="e14d2-139">Azure Data Lake Analytics'i Azure Portal'ı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="e14d2-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
