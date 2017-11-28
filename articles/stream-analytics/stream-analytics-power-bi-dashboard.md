---
title: Azure Stream Analytics aaaPower BI Panoda | Microsoft Docs
description: "Yüksek hacimli bir akış analizi işi verileri çözümlemek ve bir gerçek zamanlı akış Power BI Panosu toogather iş zekası kullanın."
keywords: "Analytics Pano, gerçek zamanlı Panosu"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a><span data-ttu-id="964d5-104">Analizler ve Power BI akış: veri akışı için gerçek zamanlı analiz Panosu</span><span class="sxs-lookup"><span data-stu-id="964d5-104">Stream Analytics and Power BI: A real-time analytics dashboard for streaming data</span></span>
<span data-ttu-id="964d5-105">Azure Stream Analytics, iş zekası araçları, baştaki hello birinin tootake avantajı sağlar [Microsoft Power BI](https://powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="964d5-105">Azure Stream Analytics enables you tootake advantage of one of hello leading business intelligence tools, [Microsoft Power BI](https://powerbi.com/).</span></span> <span data-ttu-id="964d5-106">Bu makalede, bilgi nasıl iş zekası araçları, Azure akış analizi işi için çıkış olarak Power BI kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="964d5-106">In this article, you learn how create business intelligence tools by using Power BI as an output for your Azure Stream Analytics jobs.</span></span> <span data-ttu-id="964d5-107">Da bilgi nasıl toocreate ve gerçek zamanlı bir Panoda kullanın.</span><span class="sxs-lookup"><span data-stu-id="964d5-107">You also learn how toocreate and use a real-time dashboard.</span></span>

<span data-ttu-id="964d5-108">Bu makalede Stream Analytics hello devam [gerçek zamanlı sahtekarlık algılama](stream-analytics-real-time-fraud-detection.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="964d5-108">This article continues from hello Stream Analytics [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="964d5-109">Bu öğreticide oluşturduğunuz hello iş akışı oluşturur ve böylece bir akış analizi işi tarafından algılanan sahte telefon aramaları görselleştirebilirsiniz çıktı Power BI ekler.</span><span class="sxs-lookup"><span data-stu-id="964d5-109">It builds on hello workflow created in that tutorial and adds a Power BI output so that you can visualize fraudulent phone calls that are detected by a Streaming Analytics job.</span></span> 

<span data-ttu-id="964d5-110">İzleyebilir [video](https://www.youtube.com/watch?v=SGUpT-a99MA) bu senaryo gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="964d5-110">You can watch [a video](https://www.youtube.com/watch?v=SGUpT-a99MA)  that illustrates this scenario.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="964d5-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="964d5-111">Prerequisites</span></span>

<span data-ttu-id="964d5-112">Başlamadan önce hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="964d5-112">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="964d5-113">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="964d5-113">An Azure account.</span></span>
* <span data-ttu-id="964d5-114">Power BI için bir hesap.</span><span class="sxs-lookup"><span data-stu-id="964d5-114">An account for Power BI.</span></span> <span data-ttu-id="964d5-115">Bir iş veya Okul hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964d5-115">You can use a work account or a school account.</span></span>
* <span data-ttu-id="964d5-116">Merhaba tamamlanmış bir sürümünü [gerçek zamanlı sahtekarlık algılama](stream-analytics-real-time-fraud-detection.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="964d5-116">A completed version of hello [real-time fraud detection](stream-analytics-real-time-fraud-detection.md) tutorial.</span></span> <span data-ttu-id="964d5-117">Başlangıç Öğreticisi kurgusal telefonla meta verileri oluşturan bir uygulamayı içerir.</span><span class="sxs-lookup"><span data-stu-id="964d5-117">hello tutorial includes an app that generates fictitious telephone-call metadata.</span></span> <span data-ttu-id="964d5-118">Merhaba öğreticide, bir olay hub'ı oluşturun ve telefon araması veri toohello olay hub'ı akış hello gönderin.</span><span class="sxs-lookup"><span data-stu-id="964d5-118">In hello tutorial, you create an event hub and send hello streaming phone call data toohello event hub.</span></span> <span data-ttu-id="964d5-119">Sahte çağrıları (aynı hello sayı hello gelen çağrıları aynı, farklı konumlarda'saat) algıladığı için bir sorgu yazın.</span><span class="sxs-lookup"><span data-stu-id="964d5-119">You write a query that detects fraudulent calls (calls from hello same number at hello same time in different locations).</span></span> 


## <a name="add-power-bi-output"></a><span data-ttu-id="964d5-120">Power BI çıkışı ekleme</span><span class="sxs-lookup"><span data-stu-id="964d5-120">Add Power BI output</span></span>
<span data-ttu-id="964d5-121">Merhaba gerçek zamanlı sahtekarlık algılama öğreticide hello çıktı tooAzure Blob depolama alanına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="964d5-121">In hello real-time fraud detection tutorial, hello output is sent tooAzure Blob storage.</span></span> <span data-ttu-id="964d5-122">Bu bölümde, bilgi tooPower BI gönderir bir çıktı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="964d5-122">In this section, you add an output that sends information tooPower BI.</span></span>

1. <span data-ttu-id="964d5-123">Hello Azure portal, daha önce oluşturduğunuz hello akış analizi işi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="964d5-123">In hello Azure portal, open hello Streaming Analytics job that you created earlier.</span></span> <span data-ttu-id="964d5-124">Merhaba önerilen ad kullandıysanız hello iş adlı `sa_frauddetection_job_demo`.</span><span class="sxs-lookup"><span data-stu-id="964d5-124">If you used hello suggested name, hello job is named `sa_frauddetection_job_demo`.</span></span>

2. <span data-ttu-id="964d5-125">Select hello **çıkışları** hello işi Panosu hello ortadaki kutusuna ve ardından **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="964d5-125">Select hello **Outputs** box in hello middle of hello job dashboard and then select **+ Add**.</span></span>

3. <span data-ttu-id="964d5-126">İçin **çıkış diğer adları**, girin `CallStream-PowerBI`.</span><span class="sxs-lookup"><span data-stu-id="964d5-126">For **Output Alias**, enter `CallStream-PowerBI`.</span></span> <span data-ttu-id="964d5-127">Farklı bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964d5-127">You can use a different name.</span></span> <span data-ttu-id="964d5-128">Bunu yaparsanız, hello adı daha sonra gerektiğinden, not edin.</span><span class="sxs-lookup"><span data-stu-id="964d5-128">If you do, make a note of it, because you need hello name later.</span></span> 

4. <span data-ttu-id="964d5-129">Altında **havuzu**seçin **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="964d5-129">Under **Sink**, select **Power BI**.</span></span>

   ![Power BI için bir çıktı oluşturmak](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. <span data-ttu-id="964d5-131">Tıklatın **yetkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="964d5-131">Click **Authorize**.</span></span>

    <span data-ttu-id="964d5-132">Burada bir iş veya Okul hesabı için Azure kimlik bilgilerinizi sağlayabilir penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="964d5-132">A window opens where you can provide your Azure credentials for a work or school account.</span></span> 

    ![Erişim tooPower BI kimlik bilgilerini girin](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. <span data-ttu-id="964d5-134">Kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="964d5-134">Enter your credentials.</span></span> <span data-ttu-id="964d5-135">Kimlik bilgilerinizi girdiğinizde Power BI alanınızı izni toohello akış analizi işi tooaccess de yaparken sonra unutmayın.</span><span class="sxs-lookup"><span data-stu-id="964d5-135">Be aware then when you enter your credentials, you're also giving permission toohello Streaming Analytics job tooaccess your Power BI area.</span></span>

7. <span data-ttu-id="964d5-136">Ne zaman, döndürülen toohello **yeni çıktı** dikey penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="964d5-136">When you're returned toohello **New output** blade, enter hello following information:</span></span>

    * <span data-ttu-id="964d5-137">**Çalışma grubu**: Power BI kiracınızın toocreate hello dataset istediğiniz bir çalışma alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="964d5-137">**Group Workspace**: Select a workspace in your Power BI tenant where you want toocreate hello dataset.</span></span>
    * <span data-ttu-id="964d5-138">**Veri kümesi adı**: girin `sa-dataset`.</span><span class="sxs-lookup"><span data-stu-id="964d5-138">**Dataset Name**:  Enter `sa-dataset`.</span></span> <span data-ttu-id="964d5-139">Farklı bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="964d5-139">You can use a different name.</span></span> <span data-ttu-id="964d5-140">Bunu yaparsanız, bunu daha sonra kullanmak üzere not.</span><span class="sxs-lookup"><span data-stu-id="964d5-140">If you do, make a note of it for later.</span></span>
    * <span data-ttu-id="964d5-141">**Tablo adı**: girin `fraudulent-calls`.</span><span class="sxs-lookup"><span data-stu-id="964d5-141">**Table Name**: Enter `fraudulent-calls`.</span></span> <span data-ttu-id="964d5-142">Şu anda, akış analizi işleri Power BI çıkışı bir veri kümesinde yalnızca bir tablo olabilir.</span><span class="sxs-lookup"><span data-stu-id="964d5-142">Currently, Power BI output from Stream Analytics jobs can have only one table in a dataset.</span></span>

    ![PBI çalışma](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > <span data-ttu-id="964d5-144">Power BI bir veri kümesi varsa ve sahip tablo hello hello aynı adları hello Stream Analytics işinde belirttiğiniz olanları var olanları hello üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="964d5-144">If Power BI has a dataset and table that have hello same names as hello ones that you specify in hello Stream Analytics job, hello existing ones are overwritten.</span></span>
    > <span data-ttu-id="964d5-145">Siz açıkça bu veri kümesi ve tablo Power BI hesabınızı oluşturmamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="964d5-145">We recommend that you do not explicitly create this dataset and table in your Power BI account.</span></span> <span data-ttu-id="964d5-146">Merhaba işini pompa çıkış Power BI'da oturum başlatır ve akış analizi işi başlattığınızda otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="964d5-146">They are automatically created when you start your Stream Analytics job and hello job starts pumping output into Power BI.</span></span> <span data-ttu-id="964d5-147">Sorgu iş herhangi bir sonuç döndürmezse hello veri kümesi ve tablo oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="964d5-147">If your job query doesn't return any results, hello dataset and table are not  created.</span></span>
    >

8. <span data-ttu-id="964d5-148">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="964d5-148">Click **Create**.</span></span>

<span data-ttu-id="964d5-149">Merhaba veri kümesi ayarları aşağıdaki hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="964d5-149">hello dataset is created with hello following settings:</span></span>

* <span data-ttu-id="964d5-150">**defaultRetentionPolicy: BasicFIFO**: FIFO, en çok 200.000 satırları içeren verilerdir.</span><span class="sxs-lookup"><span data-stu-id="964d5-150">**defaultRetentionPolicy: BasicFIFO**: Data is FIFO, with a maximum of 200,000 rows.</span></span>
* <span data-ttu-id="964d5-151">**defaultMode: pushStreaming**: hello dataset akış döşeme ve geleneksel rapor tabanlı görselleri (paketini destekler</span><span class="sxs-lookup"><span data-stu-id="964d5-151">**defaultMode: pushStreaming**: hello dataset supports both streaming tiles and traditional report-based visuals (a.k.a.</span></span> <span data-ttu-id="964d5-152">anında iletme).</span><span class="sxs-lookup"><span data-stu-id="964d5-152">push).</span></span>

<span data-ttu-id="964d5-153">Şu anda diğer bayraklarıyla veri kümesi oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="964d5-153">Currently, you can't create datasets with other flags.</span></span>

<span data-ttu-id="964d5-154">Power BI veri kümeleri hakkında daha fazla bilgi için bkz: Merhaba [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) başvuru.</span><span class="sxs-lookup"><span data-stu-id="964d5-154">For more information about Power BI datasets, see hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx) reference.</span></span>


## <a name="write-hello-query"></a><span data-ttu-id="964d5-155">Merhaba sorgu yazma</span><span class="sxs-lookup"><span data-stu-id="964d5-155">Write hello query</span></span>

1. <span data-ttu-id="964d5-156">Kapat hello **çıkışları** dikey penceresinde ve dönüş toohello iş dikey penceresi.</span><span class="sxs-lookup"><span data-stu-id="964d5-156">Close hello **Outputs** blade and return toohello job blade.</span></span>

2. <span data-ttu-id="964d5-157">Merhaba tıklatın **sorgu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="964d5-157">Click hello **Query** box.</span></span> 

3. <span data-ttu-id="964d5-158">Sorgu aşağıdaki hello girin.</span><span class="sxs-lookup"><span data-stu-id="964d5-158">Enter hello following query.</span></span> <span data-ttu-id="964d5-159">Bu sorgu hello sahtekarlık algılama öğreticide oluşturduğunuz benzer toohello kendi kendine birleşim sorgudur.</span><span class="sxs-lookup"><span data-stu-id="964d5-159">This query is similar toohello self-join query you created in hello fraud-detection tutorial.</span></span> <span data-ttu-id="964d5-160">Merhaba bu sorgu sonuçları toohello yeni oluşturduğunuz çıkış gönderir farktır (`CallStream-PowerBI`).</span><span class="sxs-lookup"><span data-stu-id="964d5-160">hello difference is that this query sends results toohello new output you created (`CallStream-PowerBI`).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="964d5-161">Hello giriş değil adlandırırsanız `CallStream` hello sahtekarlık algılama öğreticide için adınızı alternatif `CallStream` hello içinde **FROM** ve **katılma** hello sorgu yan tümcelerinde.</span><span class="sxs-lookup"><span data-stu-id="964d5-161">If you did not name hello input `CallStream` in hello fraud-detection tutorial, substitute your name for `CallStream` in hello **FROM** and **JOIN** clauses in hello query.</span></span>

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. <span data-ttu-id="964d5-162">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="964d5-162">Click **Save**.</span></span>


## <a name="test-hello-query"></a><span data-ttu-id="964d5-163">Test hello sorgusu</span><span class="sxs-lookup"><span data-stu-id="964d5-163">Test hello query</span></span>
<span data-ttu-id="964d5-164">Bu bölümde, isteğe bağlı ancak önerilir.</span><span class="sxs-lookup"><span data-stu-id="964d5-164">This section is optional, but recommended.</span></span> 

1. <span data-ttu-id="964d5-165">Merhaba TelcoStreaming uygulama şu anda çalışmıyorsa başlatın, aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="964d5-165">If hello TelcoStreaming app is not currently running, start it by following these steps:</span></span>

    * <span data-ttu-id="964d5-166">Bir komut penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="964d5-166">Open a command window.</span></span>
    * <span data-ttu-id="964d5-167">Merhaba telcogenerator.exe ve değiştirilmiş telcodatagen.exe.config dosyaları nerede toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="964d5-167">Go toohello folder where hello telcogenerator.exe and modified telcodatagen.exe.config files are.</span></span>
    * <span data-ttu-id="964d5-168">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="964d5-168">Run hello following command:</span></span>

            telcodatagen.exe 1000 .2 2

2. <span data-ttu-id="964d5-169">Merhaba, **sorgu** dikey penceresinde hello nokta sonraki toohello tıklatın `CallStream` girin ve ardından **örnek giriş verilerinden**.</span><span class="sxs-lookup"><span data-stu-id="964d5-169">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

3. <span data-ttu-id="964d5-170">Veri ve tıklatın üç dakika eşitleyeceğini istediğinizi belirtin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="964d5-170">Specify that you want three minutes' worth of data and click **OK**.</span></span> <span data-ttu-id="964d5-171">Merhaba veri örneklendirilen haberdar kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="964d5-171">Wait until you're notified that hello data has been sampled.</span></span>

4. <span data-ttu-id="964d5-172">Tıklatın **Test** ve sonuçları alınırken emin olun.</span><span class="sxs-lookup"><span data-stu-id="964d5-172">Click **Test** and make sure you're getting results.</span></span>


## <a name="run-hello-job"></a><span data-ttu-id="964d5-173">Merhaba işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="964d5-173">Run hello job</span></span>

1. <span data-ttu-id="964d5-174">Bu hello TelcoStreaming uygulama çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="964d5-174">Make sure that hello TelcoStreaming app is running.</span></span>

2. <span data-ttu-id="964d5-175">Kapat hello **sorgu** dikey.</span><span class="sxs-lookup"><span data-stu-id="964d5-175">Close hello **Query** blade.</span></span>

3. <span data-ttu-id="964d5-176">Merhaba iş dikey penceresinde tıklayın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="964d5-176">In hello job blade, click **Start**.</span></span>

    ![Merhaba Stream Analytics işi Başlat](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

<span data-ttu-id="964d5-178">Akış analizi işi hello gelen akış sahte çağrılarında arayan başlatır.</span><span class="sxs-lookup"><span data-stu-id="964d5-178">Your Streaming Analytics job starts looking for fraudulent calls in hello incoming stream.</span></span> <span data-ttu-id="964d5-179">Hello iş ayrıca hello veri kümesi ve tablo Power BI'da oluşturur ve hello sahte çağrıları toothem ilgili veri göndermeye başlar.</span><span class="sxs-lookup"><span data-stu-id="964d5-179">hello job also creates hello dataset and table in Power BI and starts sending data about hello fraudulent calls toothem.</span></span>


## <a name="create-hello-dashboard-in-power-bi"></a><span data-ttu-id="964d5-180">Power BI'da Hello pano oluşturun</span><span class="sxs-lookup"><span data-stu-id="964d5-180">Create hello dashboard in Power BI</span></span>

1. <span data-ttu-id="964d5-181">Çok Git[Powerbi.com](https://powerbi.com) ve iş veya Okul hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="964d5-181">Go too[Powerbi.com](https://powerbi.com) and sign in with your work or school account.</span></span> <span data-ttu-id="964d5-182">Merhaba Stream Analytics işi sorgu sonuçları çıkışı yapıyorsa, veri kümesi zaten oluşturulmuş bakın:</span><span class="sxs-lookup"><span data-stu-id="964d5-182">If hello Stream Analytics job query outputs results, you see that your dataset is already created:</span></span>

    ![Power bı'da akış veri kümesi](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. <span data-ttu-id="964d5-184">Çalışma alanınızda tıklatın  **+ &nbsp;oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="964d5-184">In your workspace, click **+&nbsp;Create**.</span></span>

    ![Power BI çalışma alanında Hello oluştur düğmesi](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. <span data-ttu-id="964d5-186">Yeni bir pano oluşturun ve adlandırın `Fraudulent Calls`.</span><span class="sxs-lookup"><span data-stu-id="964d5-186">Create a new dashboard and name it `Fraudulent Calls`.</span></span>

    ![Bir pano oluşturun ve Power BI çalışma alanında bir ad verin](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. <span data-ttu-id="964d5-188">Merhaba penceresinin Hello üstünde tıklatın **Ekle döşeme**seçin **özel akış veri**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="964d5-188">At hello top of hello window, click **Add tile**, select **CUSTOM STREAMING DATA**, and then click **Next**.</span></span>

    ![Özel veri kümesi akış](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. <span data-ttu-id="964d5-190">Altında **bilgisayarınızı DATSETS**, kümenizi seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="964d5-190">Under **YOUR DATSETS**, select your dataset and then click **Next**.</span></span>

    ![Akış Veri kümenizi](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. <span data-ttu-id="964d5-192">Altında **görselleştirme türü**seçin **kartı**ve ardından hello **alanları** listesinde **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="964d5-192">Under **Visualization Type**, select **Card**, and then in hello **Fields** list, select **fraudulentcalls**.</span></span>

    ![Yeni kutucuk için görselleştirme ayrıntıları](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. <span data-ttu-id="964d5-194">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="964d5-194">Click **Next**.</span></span>

8. <span data-ttu-id="964d5-195">Başlık ve alt başlık gibi kutucuğu ayrıntıları doldurun.</span><span class="sxs-lookup"><span data-stu-id="964d5-195">Fill in tile details like a title and subtitle.</span></span>

    ![Başlık ve yeni kutucuk için alt başlığı](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. <span data-ttu-id="964d5-197">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="964d5-197">Click **Apply**.</span></span>

    <span data-ttu-id="964d5-198">Şimdi bir sahtekarlık sayaç var!</span><span class="sxs-lookup"><span data-stu-id="964d5-198">Now you have a fraud counter!</span></span>

    ![Sahtekarlık sayacı](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. <span data-ttu-id="964d5-200">İzleme hello tooadd (4. adım ile başlayarak) bir kutucuk yeniden adımları.</span><span class="sxs-lookup"><span data-stu-id="964d5-200">Follow hello steps again tooadd a tile (starting with step 4).</span></span> <span data-ttu-id="964d5-201">Bu süre, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="964d5-201">This time, do hello following:</span></span>

    * <span data-ttu-id="964d5-202">Çok ulaştıklarında**görselleştirme türü**seçin **çizgi grafiği**.</span><span class="sxs-lookup"><span data-stu-id="964d5-202">When you get too**Visualization Type**, select **Line chart**.</span></span> 
    * <span data-ttu-id="964d5-203">Eksen ekleme ve seçin **windowend**.</span><span class="sxs-lookup"><span data-stu-id="964d5-203">Add an axis and select **windowend**.</span></span> 
    * <span data-ttu-id="964d5-204">Bir değer ekleyip seçin **fraudulentcalls**.</span><span class="sxs-lookup"><span data-stu-id="964d5-204">Add a value and select **fraudulentcalls**.</span></span>
    * <span data-ttu-id="964d5-205">İçin **zaman penceresi toodisplay**seçin son 10 dakika hello.</span><span class="sxs-lookup"><span data-stu-id="964d5-205">For **Time window toodisplay**, select hello last 10 minutes.</span></span>

    ![Bölme çizgi grafiği için oluşturma](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. <span data-ttu-id="964d5-207">Tıklatın **sonraki**, başlık ve alt başlık eklemek ve tıklayın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="964d5-207">Click **Next**, add a title and subtitle, and click **Apply**.</span></span>

    <span data-ttu-id="964d5-208">Merhaba Power BI panosuna şimdi, iki veri görünümlerini sahte çağrıları hakkında veri akış hello algılanan olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="964d5-208">hello Power BI dashboard now gives you two views of data about fraudulent calls as detected in hello streaming data.</span></span>

    ![Power BI panosuna sahte çağrıları için iki kutucuk gösteren tamamlandı](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a><span data-ttu-id="964d5-210">Power BI hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="964d5-210">Learn more about Power BI</span></span>

<span data-ttu-id="964d5-211">Bu öğretici gösterir nasıl toocreate görselleştirmeleri bir veri kümesi için yalnızca birkaç tür.</span><span class="sxs-lookup"><span data-stu-id="964d5-211">This tutorial demonstrates how toocreate only a few kinds of visualizations for a dataset.</span></span> <span data-ttu-id="964d5-212">Power BI, kuruluşunuzun diğer müşteri iş zekası araçları oluşturmanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="964d5-212">Power BI can help you create other customer business intelligence tools for your organization.</span></span> <span data-ttu-id="964d5-213">Daha fazla fikir için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="964d5-213">For more ideas, see hello following resources:</span></span>

* <span data-ttu-id="964d5-214">Merhaba Power BI panosuna başka bir örneği için izleme [Power BI ile çalışmaya başlama](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span><span class="sxs-lookup"><span data-stu-id="964d5-214">For another example of a Power BI dashboard, watch hello [Getting Started with Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) video.</span></span>
* <span data-ttu-id="964d5-215">Akış analizi yapılandırma hakkında daha fazla bilgi için proje çıktı tooPower BI ve Power BI gruplarını kullanarak hello gözden [Power BI](stream-analytics-define-outputs.md#power-bi) hello bölümünü [Stream Analytics çıkarır](stream-analytics-define-outputs.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="964d5-215">For more information about configuring Streaming Analytics job output tooPower BI and using Power BI groups, review hello [Power BI](stream-analytics-define-outputs.md#power-bi) section of hello [Stream Analytics outputs](stream-analytics-define-outputs.md) article.</span></span> 
* <span data-ttu-id="964d5-216">Power BI genellikle kullanma hakkında daha fazla bilgi için bkz: [Power BI panoları](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span><span class="sxs-lookup"><span data-stu-id="964d5-216">For information about using Power BI generally, see [Dashboards in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).</span></span>


## <a name="learn-about-limitations-and-best-practices"></a><span data-ttu-id="964d5-217">Sınırlamalar ve en iyi uygulamalar hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="964d5-217">Learn about limitations and best practices</span></span>
<span data-ttu-id="964d5-218">Şu anda Power BI kabaca saniye başına bir kez çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="964d5-218">Currently, Power BI can be called roughly once per second.</span></span> <span data-ttu-id="964d5-219">Akış görselleri 15 KB paketlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="964d5-219">Streaming visuals support packets of 15 KB.</span></span> <span data-ttu-id="964d5-220">Ötesinde, akış görselleri başarısız (ancak anında iletme toowork devam eder).</span><span class="sxs-lookup"><span data-stu-id="964d5-220">Beyond that, streaming visuals fail (but push continues toowork).</span></span> <span data-ttu-id="964d5-221">Bu sınırlamalar nedeniyle Power BI kendisini en doğal olarak Azure akış analizi önemli veri yükünü azaltma burada mu toocases uygundur.</span><span class="sxs-lookup"><span data-stu-id="964d5-221">Because of these limitations, Power BI lends itself most naturally toocases where Azure Stream Analytics does a significant data load reduction.</span></span> <span data-ttu-id="964d5-222">Atlayan pencere veya veri gönderimi bir anında iletme saniye başına en fazla olduğunu ve sorgunuzu hello işleme gereksinimleri içinde adlandırıldığını Hopping penceresi tooensure kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="964d5-222">We recommend using a Tumbling window or Hopping window tooensure that data push is at most one push per second, and that your query lands within hello throughput requirements.</span></span>

<span data-ttu-id="964d5-223">Saniye cinsinden pencerenizi eşitlik toocompute hello değeri toogive aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="964d5-223">You can use hello following equation toocompute hello value toogive your window in seconds:</span></span>

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

<span data-ttu-id="964d5-225">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="964d5-225">For example:</span></span>

* <span data-ttu-id="964d5-226">Verileri bir saniyelik aralıklarda gönderme 1.000 cihazları var.</span><span class="sxs-lookup"><span data-stu-id="964d5-226">You have 1,000 devices sending data at one-second intervals.</span></span>
* <span data-ttu-id="964d5-227">Merhaba Power BI Pro saat başına 1.000.000 satır destekleyen SKU kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="964d5-227">You are using hello Power BI Pro SKU that supports 1,000,000 rows per hour.</span></span>
* <span data-ttu-id="964d5-228">Toopublish hello aygıt tooPower BI başına ortalama veri miktarını istiyor.</span><span class="sxs-lookup"><span data-stu-id="964d5-228">You want toopublish hello amount of average data per device tooPower BI.</span></span>

<span data-ttu-id="964d5-229">Sonuç olarak, hello eşitlik olur:</span><span class="sxs-lookup"><span data-stu-id="964d5-229">As a result, hello equation becomes:</span></span>

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

<span data-ttu-id="964d5-231">Bu yapılandırma verildiğinde, hello özgün sorgu toohello aşağıdakileri değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="964d5-231">Given this configuration, you can change hello original query toohello following:</span></span>

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a><span data-ttu-id="964d5-232">Yetkilendirmeyi yenileyin</span><span class="sxs-lookup"><span data-stu-id="964d5-232">Renew authorization</span></span>
<span data-ttu-id="964d5-233">Merhaba parola işinizi oluşturulmuş veya son kimliği doğrulanmış oluşturulmasından sonra değiştirilmişse, Power BI hesabınızı tooreauthenticate gerekir.</span><span class="sxs-lookup"><span data-stu-id="964d5-233">If hello password has changed since your job was created or last authenticated, you need tooreauthenticate your Power BI account.</span></span> <span data-ttu-id="964d5-234">Azure Active Directory (Azure AD) kiracınızın Azure çok faktörlü kimlik doğrulaması yapılandırılmışsa, ayrıca toorenew Power BI yetkilendirme iki haftada gerekir.</span><span class="sxs-lookup"><span data-stu-id="964d5-234">If Azure Multi-Factor Authentication is configured on your Azure Active Directory (Azure AD) tenant, you also need toorenew Power BI authorization every two weeks.</span></span> <span data-ttu-id="964d5-235">Yenilemezseniz, iş çıktısı eksikliği gibi Belirtiler görebilir veya bir `Authenticate user error` hello işlem günlüğüne kaydeder.</span><span class="sxs-lookup"><span data-stu-id="964d5-235">If you don't renew, you could see symptoms such as a lack of job output or an `Authenticate user error` in hello operation logs.</span></span>

<span data-ttu-id="964d5-236">Benzer şekilde, hello belirtecin süresi dolduktan sonra bir iş başlatılır, bir hata oluşur ve hello işi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="964d5-236">Similarly, if a job starts after hello token has expired, an error occurs and hello job fails.</span></span> <span data-ttu-id="964d5-237">tooresolve bu sorunu çalıştıran hello işini durdurmak ve Power BI çıktı tooyour gidin.</span><span class="sxs-lookup"><span data-stu-id="964d5-237">tooresolve this issue, stop hello job that's running and go tooyour Power BI output.</span></span> <span data-ttu-id="964d5-238">tooavoid veri kaybı select hello **yetkilendirmeyi yenileyin** işinizi hello gelen yeniden başlatın ve bağlama **son durdurulma zamanı**.</span><span class="sxs-lookup"><span data-stu-id="964d5-238">tooavoid data loss, select hello **Renew authorization** link, and then restart your job from hello **Last Stopped Time**.</span></span>

<span data-ttu-id="964d5-239">Power BI ile Merhaba yetkilendirme yenilendikten sonra yeşil bir uyarı hello sorunu Çözümlendi hello yetkilendirme alanı tooreflect görünür.</span><span class="sxs-lookup"><span data-stu-id="964d5-239">After hello authorization has been refreshed with Power BI, a green alert appears in hello authorization area tooreflect that hello issue has been resolved.</span></span>

## <a name="get-help"></a><span data-ttu-id="964d5-240">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="964d5-240">Get help</span></span>
<span data-ttu-id="964d5-241">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="964d5-241">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="964d5-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="964d5-242">Next steps</span></span>
* [<span data-ttu-id="964d5-243">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="964d5-243">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="964d5-244">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="964d5-244">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="964d5-245">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="964d5-245">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="964d5-246">Azure Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="964d5-246">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="964d5-247">Azure Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="964d5-247">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
