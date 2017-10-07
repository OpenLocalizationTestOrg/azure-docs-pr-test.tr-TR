---
title: "Visual Studio için Data Lake araçları kullanarak aaaDevelop U-SQL komut dosyalarını | Microsoft Docs"
description: "Visual Studio için tooinstall Data Lake araçları nasıl ve ne öğrenin toodevelop ve test U-SQL komut dosyaları."
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
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="99365-103">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="99365-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="99365-104">Bilgi nasıl toouse Visual Studio toocreate Azure Data Lake Analytics hesapları tanımlayın işler [U-SQL](data-lake-analytics-u-sql-get-started.md)ve işleri toohello Data Lake Analytics hizmeti gönderin.</span><span class="sxs-lookup"><span data-stu-id="99365-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="99365-105">Data Lake Analytics hakkında daha fazla bilgi için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99365-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="99365-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="99365-106">Prerequisites</span></span>

* <span data-ttu-id="99365-107">**Visual Studio**: Express dışında tüm sürümler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="99365-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="99365-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="99365-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="99365-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="99365-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="99365-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="99365-110">Visual Studio 2013</span></span>
* <span data-ttu-id="99365-111">**.NET için Microsoft Azure SDK** 2.7.1 sürümü veya sonraki sürümleri.</span><span class="sxs-lookup"><span data-stu-id="99365-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="99365-112">Hello kullanarak yükleme [Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="99365-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="99365-113">**Data Lake Analytics** hesabı.</span><span class="sxs-lookup"><span data-stu-id="99365-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="99365-114">hesabı, bir toocreate bkz [Azure portal kullanarak Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99365-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="99365-115">Visual Studio için Azure Data Lake Araçları’nı yükleme</span><span class="sxs-lookup"><span data-stu-id="99365-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="99365-116">Azure Data Lake araçları Visual Studio için yükleyip [hello İndirme Merkezi gelen](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="99365-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="99365-117">Yükleme işleminden sonra şunları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="99365-117">After installation, note that:</span></span>
* <span data-ttu-id="99365-118">Merhaba **Sunucu Gezgini** > **Azure** düğümü içeren bir **Data Lake Analytics** düğümü.</span><span class="sxs-lookup"><span data-stu-id="99365-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="99365-119">Merhaba **Araçları** menü sahip bir **Data Lake** öğesi.</span><span class="sxs-lookup"><span data-stu-id="99365-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="99365-120">Tooan Azure Data Lake Analytics hesabı Bağlan</span><span class="sxs-lookup"><span data-stu-id="99365-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="99365-121">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="99365-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="99365-122">**Görünüm** > **Sunucu Gezgini**’ni seçerek Sunucu Gezgini’ni açın.</span><span class="sxs-lookup"><span data-stu-id="99365-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="99365-123">**Azure**’a sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99365-123">Right-click **Azure**.</span></span> <span data-ttu-id="99365-124">Ardından **tooMicrosoft Azure aboneliğine bağlanma** ve hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="99365-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="99365-125">Sunucu Gezgini'nde **Azure** > **Data Lake Analytics**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="99365-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="99365-126">Data Lake Analytics hesaplarınızın listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="99365-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="99365-127">İlk U-SQL betiğinizi yazma</span><span class="sxs-lookup"><span data-stu-id="99365-127">Write your first U-SQL script</span></span>

<span data-ttu-id="99365-128">metin aşağıdaki hello basit bir U-SQL komut dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="99365-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="99365-129">Küçük bir veri kümesini ve bir dosya olarak dataset toohello varsayılan Data Lake Store adlı yazma tanımlar `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="99365-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="99365-130">Data Lake Analytics işi gönderme</span><span class="sxs-lookup"><span data-stu-id="99365-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="99365-131">**Dosya** > **Yeni** > **Proje**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="99365-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="99365-132">Select hello **U-SQL projesi** yazın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="99365-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="99365-133">Visual Studio, **Script.usql** dosyasıyla bir çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99365-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="99365-134">Hello önceki betik hello yapıştırma **Script.usql** penceresi.</span><span class="sxs-lookup"><span data-stu-id="99365-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="99365-135">Merhaba hello sol üst köşesindeki **Script.usql** penceresinde hello Data Lake Analytics hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="99365-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![U-SQL Visual Studio projesini gönderme](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="99365-137">Merhaba hello sol üst köşesindeki **Script.usql** penceresinde, seçin **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="99365-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="99365-138">Merhaba doğrulayın **Analytics hesabı**ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="99365-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="99365-139">Merhaba gönderimi tamamlandıktan sonra gönderme işleminin sonuçları hello Data Lake araçları Visual Studio sonuçlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="99365-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![U-SQL Visual Studio projesini gönderme](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="99365-141">toosee hello en son iş durumunu ve yenileme Merhaba ekranında tıklatın **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="99365-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="99365-142">Merhaba iş başarılı olduğunda hello gösterir **iş grafiği**, **meta veri işlemleri**, **Durum geçmişi**, ve **tanılama**:</span><span class="sxs-lookup"><span data-stu-id="99365-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![U-SQL Visual Studio Data Lake Analytics iş performans grafiği](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="99365-144">**İş özeti** hello hello iş özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="99365-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="99365-145">**İş ayrıntılarını** hello komut dosyası, kaynakları ve köşeleri dahil olmak üzere hello iş hakkında daha ayrıntılı bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="99365-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="99365-146">**İş grafiğinin** hello işinin ilerleme durumunu hello visualizes.</span><span class="sxs-lookup"><span data-stu-id="99365-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="99365-147">**Meta veri işlemleri** hello U-SQL kataloğunu üzerinde gerçekleştirilen tüm hello eylemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="99365-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="99365-148">**Veri** tüm hello girişleri ve çıkışları gösterir.</span><span class="sxs-lookup"><span data-stu-id="99365-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="99365-149">**Tanılama**, iş yürütme ve performans iyileştirme için gelişmiş bir analiz sağlar.</span><span class="sxs-lookup"><span data-stu-id="99365-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="99365-150">toocheck iş durumu</span><span class="sxs-lookup"><span data-stu-id="99365-150">toocheck job state</span></span>

1. <span data-ttu-id="99365-151">Sunucu Gezgini'nde **Azure** > **Data Lake Analytics**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="99365-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="99365-152">Merhaba Data Lake Analytics hesap adını genişletin.</span><span class="sxs-lookup"><span data-stu-id="99365-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="99365-153">**İşler**’e çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99365-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="99365-154">Daha önce gönderilen hello işi seçin.</span><span class="sxs-lookup"><span data-stu-id="99365-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="99365-155">İş toosee hello çıktısı</span><span class="sxs-lookup"><span data-stu-id="99365-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="99365-156">Server Explorer'da gönderdiğiniz toohello işi bulun.</span><span class="sxs-lookup"><span data-stu-id="99365-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="99365-157">Merhaba tıklatın **veri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="99365-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="99365-158">Merhaba, **iş çıkışları** sekmesi, select hello `"/data.csv"` dosya.</span><span class="sxs-lookup"><span data-stu-id="99365-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99365-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99365-159">Next steps</span></span>

* [<span data-ttu-id="99365-160">Test etmek ve hata ayıklamak için kendi iş istasyonunuzda U-SQL betiklerini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="99365-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="99365-161">U-SQL işlerinde C# kodu hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="99365-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="99365-162">Hello Azure Data Lake araçları Visual Studio kodunu kullanın</span><span class="sxs-lookup"><span data-stu-id="99365-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
