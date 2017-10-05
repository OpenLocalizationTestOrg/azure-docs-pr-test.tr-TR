---
title: "Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme | Microsoft Docs"
description: "Visual Studio için Data Lake Araçları'nı nasıl yükleyeceğinizi ve U-SQL betiklerini nasıl geliştirip test edeceğinizi öğrenin."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7bbbb08ff635477a88403a3ae6bd3486d31838ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3fe5c-103">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="3fe5c-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="3fe5c-104">Azure Data Lake Analytics hesapları oluşturmak, [U-SQL](data-lake-analytics-u-sql-get-started.md) içinde işler tanımlamak ve Data Lake Analytics hizmetine iş göndermek için Visual Studio’nun nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-104">Learn how to use Visual Studio to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="3fe5c-105">Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fe5c-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3fe5c-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3fe5c-106">Prerequisites</span></span>

* <span data-ttu-id="3fe5c-107">**Visual Studio**: Express dışında tüm sürümler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="3fe5c-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3fe5c-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="3fe5c-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="3fe5c-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="3fe5c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="3fe5c-110">Visual Studio 2013</span></span>
* <span data-ttu-id="3fe5c-111">**.NET için Microsoft Azure SDK** 2.7.1 sürümü veya sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="3fe5c-112">[Web platformu yükleyicisini](http://www.microsoft.com/web/downloads/platform.aspx) kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-112">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="3fe5c-113">**Data Lake Analytics** hesabı.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="3fe5c-114">Hesap oluşturmak için bkz. [Azure portalı kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3fe5c-114">To create an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3fe5c-115">Visual Studio için Azure Data Lake Araçları’nı yükleme</span><span class="sxs-lookup"><span data-stu-id="3fe5c-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="3fe5c-116">[İndirme Merkezi'nden](http://aka.ms/adltoolsvs) Visual Studio için Azure Data Lake Araçları’nı indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-116">Download and install Azure Data Lake Tools for Visual Studio [from the Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="3fe5c-117">Yükleme işleminden sonra şunları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="3fe5c-117">After installation, note that:</span></span>
* <span data-ttu-id="3fe5c-118">**Sunucu Gezgini** > **Azure** düğümü, **Data Lake Analytics** düğümü içerir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-118">The **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="3fe5c-119">**Araçlar** menüsünde **Data Lake** öğesi vardır.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-119">The **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-to-an-azure-data-lake-analytics-account"></a><span data-ttu-id="3fe5c-120">Azure Data Lake Analytics hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="3fe5c-120">Connect to an Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="3fe5c-121">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="3fe5c-122">**Görünüm** > **Sunucu Gezgini**’ni seçerek Sunucu Gezgini’ni açın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="3fe5c-123">**Azure**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-123">Right-click **Azure**.</span></span> <span data-ttu-id="3fe5c-124">Ardından **Microsoft Azure Aboneliğine Bağlan**’ı seçin ve yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-124">Then select **Connect to Microsoft Azure Subscription** and follow the instructions.</span></span>
4. <span data-ttu-id="3fe5c-125">Sunucu Gezgini'nde **Azure** > **Data Lake Analytics**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="3fe5c-126">Data Lake Analytics hesaplarınızın listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="3fe5c-127">İlk U-SQL betiğinizi yazma</span><span class="sxs-lookup"><span data-stu-id="3fe5c-127">Write your first U-SQL script</span></span>

<span data-ttu-id="3fe5c-128">Aşağıda basit bir U-SQL betiği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-128">The following text is a simple U-SQL script.</span></span> <span data-ttu-id="3fe5c-129">Küçük bir veri kümesini tanımlar ve bu veri kümesini `/data.csv` adlı bir dosya olarak varsayılan Data Lake Store’a yazar.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-129">It defines a small dataset and writes that dataset to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="3fe5c-130">Data Lake Analytics işi gönderme</span><span class="sxs-lookup"><span data-stu-id="3fe5c-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="3fe5c-131">**Dosya** > **Yeni** > **Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="3fe5c-132">**U-SQL Projesi** türünü seçin ve **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-132">Select the **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="3fe5c-133">Visual Studio, **Script.usql** dosyasıyla bir çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="3fe5c-134">Önceki betiği **Script.usql** penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-134">Paste the previous script into the **Script.usql** window.</span></span>

4. <span data-ttu-id="3fe5c-135">**Script.usql** penceresinin sol üst köşesinde Data Lake Analytics hesabını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-135">In the upper-left corner of the **Script.usql** window, specify the Data Lake Analytics account.</span></span>

    ![U-SQL Visual Studio projesini gönderme](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="3fe5c-137">**Script.usql** penceresinin sol üst köşesinde **Gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-137">In the upper-left corner of the **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="3fe5c-138">**Analytics Hesabı**’nı doğrulayın ve ardından **Gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-138">Verify the **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="3fe5c-139">Gönderim tamamlandıktan sonra, gönderme işleminin sonuçları Visual Studio için Data Lake Araçları Sonuçları içinde sunulur.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-139">Submission results are available in the Data Lake Tools for Visual Studio Results after the submission is complete.</span></span>

    ![U-SQL Visual Studio projesini gönderme](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="3fe5c-141">En son iş durumunu görmek ve ekranı yenilemek için **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-141">To see the latest job status and refresh the screen, click **Refresh**.</span></span> <span data-ttu-id="3fe5c-142">İş başarılı olduğunda **İş Grafiği**, **Meta Veri İşlemleri**, **Durum Geçmişi** ve **Tanılama**’yı gösterir:</span><span class="sxs-lookup"><span data-stu-id="3fe5c-142">When the job succeeds, it shows the **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![U-SQL Visual Studio Data Lake Analytics iş performans grafiği](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="3fe5c-144">**İş Özeti**, işin özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-144">**Job Summary** shows the summary of the job.</span></span>   
   * <span data-ttu-id="3fe5c-145">**İş Ayrıntıları**, iş hakkında betik, kaynaklar ve köşeler gibi daha özel bilgiler gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-145">**Job Details** shows more specific information about the job, including the script, resources, and vertices.</span></span>
   * <span data-ttu-id="3fe5c-146">**İş Grafiği**, işin ilerleme durumunu görselleştirir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-146">**Job Graph** visualizes the progress of the job.</span></span>
   * <span data-ttu-id="3fe5c-147">**Meta Veri İşlemleri**, U-SQL kataloğunda yapılan tüm işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-147">**MetaData Operations** shows all the actions that were taken on the U-SQL catalog.</span></span>
   * <span data-ttu-id="3fe5c-148">**Veri** tüm girdileri ve çıktıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-148">**Data** shows all the inputs and outputs.</span></span>
   * <span data-ttu-id="3fe5c-149">**Tanılama**, iş yürütme ve performans iyileştirme için gelişmiş bir analiz sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="to-check-job-state"></a><span data-ttu-id="3fe5c-150">İş durumu denetlemek için</span><span class="sxs-lookup"><span data-stu-id="3fe5c-150">To check job state</span></span>

1. <span data-ttu-id="3fe5c-151">Sunucu Gezgini'nde **Azure** > **Data Lake Analytics**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="3fe5c-152">Data Lake Analytics hesap adını genişletin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-152">Expand the Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="3fe5c-153">**İşler**’e çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="3fe5c-154">Daha önce gönderdiğiniz işi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-154">Select the job that you previously submitted.</span></span>

### <a name="to-see-the-output-of-a-job"></a><span data-ttu-id="3fe5c-155">Bir işin çıktısını görmek için</span><span class="sxs-lookup"><span data-stu-id="3fe5c-155">To see the output of a job</span></span>

1. <span data-ttu-id="3fe5c-156">Sunucu Gezgini’nde gönderdiğiniz işe gidin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-156">In Server Explorer, browse to the job you submitted.</span></span>
2. <span data-ttu-id="3fe5c-157">**Veri** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-157">Click the **Data** tab.</span></span>
3. <span data-ttu-id="3fe5c-158">**İş Çıktıları** sekmesinde `"/data.csv"` dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe5c-158">In the **Job Outputs** tab, select the `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fe5c-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fe5c-159">Next steps</span></span>

* [<span data-ttu-id="3fe5c-160">Test etmek ve hata ayıklamak için kendi iş istasyonunuzda U-SQL betiklerini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="3fe5c-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="3fe5c-161">U-SQL işlerinde C# kodu hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="3fe5c-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="3fe5c-162">Visual Studio Code için Azure Data Lake Araçları’nı kullanma</span><span class="sxs-lookup"><span data-stu-id="3fe5c-162">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
