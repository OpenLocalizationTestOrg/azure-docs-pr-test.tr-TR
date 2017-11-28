---
title: "Visual Studio için Azure Stream Analytics araçlarını kullanın | Microsoft Docs"
description: "Başlangıç öğreticisi için Visual Studio için Azure Stream Analytics araçları"
keywords: Visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="bf8bd-104">Visual Studio için Azure Stream Analytics araçlarını kullanın</span><span class="sxs-lookup"><span data-stu-id="bf8bd-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="bf8bd-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="bf8bd-105">Introduction</span></span>
<span data-ttu-id="bf8bd-106">Bu öğreticide, Visual Studio için Azure Stream Analytics araçları oluşturmak, yazar, yerel olarak test, yönetmek ve akış analizi işleri hata ayıklamak için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="bf8bd-107">Bu öğreticiyi tamamladıktan sonra aşağıdakileri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="bf8bd-108">Visual Studio için Stream Analytics araçları edinin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="bf8bd-109">Yapılandırın ve akış analizi işi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="bf8bd-110">İşinizi yerel örnek verilerle yerel olarak test edin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="bf8bd-111">Sorunları gidermek için izleme'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="bf8bd-112">Var olan işleri projelerine verin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf8bd-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bf8bd-113">Prerequisites</span></span>
<span data-ttu-id="bf8bd-114">Bu öğreticiyi tamamlamak için aşağıdaki önkoşulları karşılamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="bf8bd-115">İçindeki "Stream Analytics işi oluştur" koyun adımlarını tamamlayın [Stream Analytics öğretici kullanarak bir IOT çözümü derleme](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="bf8bd-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="bf8bd-116">Visual Studio 2015, Visual Studio 2013 güncelleştirme 4 veya Visual Studio 2012 kullanın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="bf8bd-117">Enterprise (Ultimate/Premium), Professional ve topluluk sürümleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="bf8bd-118">Express sürümü desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-118">Express edition is not supported.</span></span> <span data-ttu-id="bf8bd-119">Visual Studio 2017 desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="bf8bd-120">.NET sürüm 2.7.1 için Azure SDK'sını kullanın veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="bf8bd-121">[Web platformu yükleyicisini](http://www.microsoft.com/web/downloads/platform.aspx) kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="bf8bd-122">Yükleme [analiz araçları Visual Studio için akış](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="bf8bd-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="bf8bd-123">Stream Analytics projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf8bd-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="bf8bd-124">Visual Studio'da sırasıyla **dosya** menü ve select **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="bf8bd-125">Sol taraftaki şablonları listesinden seçin **Stream Analytics** ve ardından **Azure Stream Analytics uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="bf8bd-126">Proje girin **adı**, **konumu**, ve **çözüm adı** için diğer projeler yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Yeni Proje penceresinin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="bf8bd-128">A **Ücretli** proje üretilir **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Çözüm Gezgini'nde oluşturulan Ücretli proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="bf8bd-130">Doğru abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="bf8bd-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="bf8bd-131">Visual Studio'da sırasıyla **Görünüm** menü ve açık **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="bf8bd-132">Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="bf8bd-133">Giriş kaynağı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="bf8bd-133">Define the input sources</span></span>
1.  <span data-ttu-id="bf8bd-134">İçinde **Çözüm Gezgini**, genişletin **girişleri** düğümü ve yeniden adlandırma **Input.json** için **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="bf8bd-135">Çift **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="bf8bd-136">**Giriş diğer adı** artık **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="bf8bd-137">Giriş diğer adı sorgu komut dosyasındaki kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="bf8bd-138">İçinde **kaynak türü**seçin **veri akışı**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="bf8bd-139">İçinde **kaynak**seçin **olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="bf8bd-140">İçinde **Service Bus Namespace**seçin **TollData** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="bf8bd-141">İçinde **olay hub'ı adı**seçin **girişi**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="bf8bd-142">İçinde **olay hub'ı ilke adı**seçin **RootManageSharedAccessKey** (varsayılan değer).</span><span class="sxs-lookup"><span data-stu-id="bf8bd-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="bf8bd-143">İçinde **olayı seri hale getirme biçimi**seçin **Json**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="bf8bd-144">İçinde **kodlama**seçin **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="bf8bd-145">Ayarlarınız aşağıdaki ekran görüntüsüne görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-145">Your settings should look like the following screenshot:</span></span>

    ![Giriş penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="bf8bd-147">Sihirbazı tamamlamak için tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="bf8bd-148">Artık çıkış akışı oluşturmak için başka bir giriş kaynağı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="bf8bd-149">Sağ **girişleri** düğümü ve select **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Yeni öğe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="bf8bd-151">Penceresinde seçin **Azure Stream Analytics giriş**, değiştirip **adı** için **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="bf8bd-152">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-152">Click **Add**.</span></span>

    ![Yeni öğe penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="bf8bd-154">Çift **ExitStream.json** proje ve siz de aynı adımları vermedi için giriş akış izleyin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="bf8bd-155">Girilmelidir **çıkmak** için **olay hub'ı adı** aşağıdaki ekran görüntüsünde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![ExitStream penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="bf8bd-157">Şimdi iki giriş akışları tanımladınız:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-157">Now you have defined two input streams:</span></span>

    ![Giriş ve çıkış giriş akışları](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="bf8bd-159">Ardından, car kayıt verileri içeren blob dosyası için başvuru veri girişi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="bf8bd-160">Sağ **girişleri** düğümünü proje ve akış girişleri için yaptığınız gibi aynı adımları sonra izleyin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="bf8bd-161">İçinde **giriş diğer adı**, girin **kayıt**hem de **kaynak türü**seçin **başvuru verileri**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Kayıt penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="bf8bd-163">İçinde **depolama hesabı**seçin **tolldata** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="bf8bd-164">İçinde **kapsayıcı**seçin **tolldata**hem de **yol deseni**, girin **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="bf8bd-165">Bu dosya adı büyük/küçük harfe duyarlıdır ve küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="bf8bd-166">Sihirbazı tamamlamak için tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="bf8bd-167">Şimdi tüm girişleri tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="bf8bd-168">Çıktı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="bf8bd-168">Define the output</span></span>
1.  <span data-ttu-id="bf8bd-169">İçinde **Çözüm Gezgini**, genişletin **girişleri** düğümü ve çift **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="bf8bd-170">İçinde **çıkış diğer adları**, girin **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="bf8bd-171">İçinde **havuzu**seçin **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="bf8bd-172">İçinde **veritabanı**seçin **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="bf8bd-173">İçinde **kullanıcı adı**, girin **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="bf8bd-174">İçinde **parola**, girin **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="bf8bd-175">İçinde **tablo**, girin **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="bf8bd-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-176">Click **Save**.</span></span>

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="bf8bd-178">Stream Analytics sorgu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf8bd-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="bf8bd-179">Bu öğreticide, veri hat ilgili birkaç iş soruları yanıtlamak çalışır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="bf8bd-180">Ayrıca, Stream Analytics ilgili yanıt vermek için kullanılan akış analizi sorgu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="bf8bd-181">İlk Stream Analytics işiniz başlamadan önce basit bir senaryoyu ve sorgu söz dizimi inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="bf8bd-182">Stream Analytics sorgu dili giriş</span><span class="sxs-lookup"><span data-stu-id="bf8bd-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="bf8bd-183">Ücretli Stand girin taşıtlardan sayısını gerektiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="bf8bd-184">Bu örnek sürekli akışı olduğundan, bir süre tanımlamak zorunda.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="bf8bd-185">"Kaç taşıtlardan üç dakikada Ücretli Stand girin?" olarak soru değiştirme</span><span class="sxs-lookup"><span data-stu-id="bf8bd-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="bf8bd-186">Veri saymak için bu şekilde, genellikle dönen sayım olarak da adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="bf8bd-187">Bu soruya yanıt veren Stream Analytics sorgu arayın:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="bf8bd-188">Akış analizi gibi SQL ve sorgu zaman ilgili yönlerini belirlemek için birkaç uzantıları ekler bir sorgu dili kullanır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="bf8bd-189">Daha fazla bilgi için bkz: [zaman Yönetimi](https://msdn.microsoft.com/library/azure/mt582045.aspx) ve [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN'den sorguda kullanılan yapılar.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="bf8bd-190">İlk Stream Analytics sorgu yazılmış, test zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="bf8bd-191">TollApp klasörü şu yol içinde yer alan örnek veri dosyalarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="bf8bd-192">.. \TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="bf8bd-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="bf8bd-193">Bu klasör, aşağıdaki dosyaları içerir:</span><span class="sxs-lookup"><span data-stu-id="bf8bd-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="bf8bd-194">Entry.JSON</span><span class="sxs-lookup"><span data-stu-id="bf8bd-194">Entry.json</span></span>
*   <span data-ttu-id="bf8bd-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="bf8bd-195">Exit.json</span></span>
*   <span data-ttu-id="bf8bd-196">Registration.JSON</span><span class="sxs-lookup"><span data-stu-id="bf8bd-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="bf8bd-197">Ücretli Stand girme taşıtlardan sayısı</span><span class="sxs-lookup"><span data-stu-id="bf8bd-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="bf8bd-198">Projede çift **Script.asaql** komut dosyasında açmak için **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="bf8bd-199">Kopyalayın ve komut dosyası önceki bölümde düzenleyiciye yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="bf8bd-200">Sorgu Düzenleyicisi'ni IntelliSense, söz dizimi renklendirme ve hata işaret destekler.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Sorgu Düzenleyicisi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="bf8bd-202">Stream Analytics sorguları yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="bf8bd-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="bf8bd-203">Bir sözdizimi hatası olup olmadığını görmek için sorguyu derlemek için projesine sağ tıklatın ve **yapı**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="bf8bd-204">Bu örnek verileri sorgusu doğrulamak için yerel örnek verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="bf8bd-205">Girişi sağ tıklatın ve seçin **yerel girdisi eklemek**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-205">Right-click the input, and select **Add local input**.</span></span>

    ![Yerel giriş Ekle](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="bf8bd-207">Açılan pencerede, yerel yolundan örnek verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="bf8bd-208">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-208">Click **Save**.</span></span>

    ![Yerel giriş penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="bf8bd-210">Adlı bir dosya **local_EntryStream.json** girişleri klasörünüze otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![Girişleri klasöre eklenen dosya](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="bf8bd-212">İçinde **sorgu Düzenleyicisi'ni**, tıklatın **yerel olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="bf8bd-213">Veya F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-213">Or you can press the F5 key.</span></span>

    ![Yerel olarak çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Yerel çıkış çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="bf8bd-216">Çıktıda görüntülemek için herhangi bir tuşa basın **ASA yerel çalıştırma sonucu** Visual Studio'daki.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![ASA yerel çalıştırma sonucu penceresi](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="bf8bd-218">Tıklatın **sonuç Klasör Aç** çıktı dosyaları CSV ve JSON biçiminde her ikisini de denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Sonuç klasör çıktısını açın](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="bf8bd-220">Örnek giriş verisi</span><span class="sxs-lookup"><span data-stu-id="bf8bd-220">Sample the input data</span></span>
<span data-ttu-id="bf8bd-221">Ayrıca, yerel bir dosyaya örnek giriş verileri giriş kaynaklardan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="bf8bd-222">Giriş yapılandırma dosyasını sağ tıklatın ve seçin **örnek verileri**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Örnek Veri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="bf8bd-224">Şu an için yalnızca olay hub'ı veya IOT hub'ı örnek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="bf8bd-225">Diğer giriş kaynağı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="bf8bd-226">Açılan pencerede örnek verileri kaydetmek için kullanılan yerel yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="bf8bd-227">Tıklatın **örnek**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-227">Click **Sample**.</span></span>

    ![Örnek veri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="bf8bd-229">Devam eden görebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-229">You can see the progress in the **Output** window.</span></span> 

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="bf8bd-231">Azure Stream Analytics sorgu Gönder</span><span class="sxs-lookup"><span data-stu-id="bf8bd-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="bf8bd-232">İçinde **sorgu Düzenleyicisi'ni**, tıklatın **göndermek için Azure** komut dosyası Düzenleyicisi'nde.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Azure'a Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="bf8bd-234">Seçin **yeni bir Azure Stream Analytics işi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="bf8bd-235">Girin **iş adı**, doğru seçin **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="bf8bd-236">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-236">Click **Submit**.</span></span>

    ![İş pencere Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="bf8bd-238">Bir işi Başlat</span><span class="sxs-lookup"><span data-stu-id="bf8bd-238">Start a job</span></span>
<span data-ttu-id="bf8bd-239">İşinizi oluşturulur, iş görünümünde otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="bf8bd-240">İşlemi başlatmak için tıklatın **yeşil ok** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-240">To start the job, click the **green arrow** button.</span></span>

    ![Bir işi Başlat](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="bf8bd-242">Varsayılan ayar seçin ve tıklayın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-242">Select the default setting, and click **Start**.</span></span>
 
    ![İş penceresi başlangıç](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="bf8bd-244">İş **durum** değişikliklerini **çalıştıran**, ve **giriş olayları** ve **çıkış olaylarındaki** görünür.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![İş özeti çalışma durumu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="bf8bd-246">Visual Studio'da sonuçlarını denetleyin</span><span class="sxs-lookup"><span data-stu-id="bf8bd-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="bf8bd-247">Visual Studio'da açın **Sunucu Gezgini** ve sağ **TollDataRefJoin** tablo.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="bf8bd-248">Seçin **Show Table Data** işinizi çıkışını görmek için.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Sunucu Gezgini'nde tablo verileri göster seçimi](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="bf8bd-250">İş ölçümleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bf8bd-250">View the job metrics</span></span>
<span data-ttu-id="bf8bd-251">Bazı temel iş istatistiklerinde bulunabilir **iş ölçümleri**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![İş ölçümleri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="bf8bd-253">Sunucu Gezgininde iş listesi</span><span class="sxs-lookup"><span data-stu-id="bf8bd-253">List the job in Server Explorer</span></span>
<span data-ttu-id="bf8bd-254">İçinde **Sunucu Gezgini**, tıklatın **akış analizi işleri** ve ardından **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="bf8bd-255">İş altında görünür **akış analizi işleri**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-255">The job appears under **Stream Analytics jobs**.</span></span>

![Server Explorer'da listelenen stream Analytics işleri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="bf8bd-257">Proje görünümü Aç</span><span class="sxs-lookup"><span data-stu-id="bf8bd-257">Open the job view</span></span>
<span data-ttu-id="bf8bd-258">İş görünümünde açmak için iş düğümünü genişletin ve çift **iş görünümünde** düğümü.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![İş görünümünde düğümü](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="bf8bd-260">Var olan bir projeyi</span><span class="sxs-lookup"><span data-stu-id="bf8bd-260">Export an existing job to a project</span></span>
<span data-ttu-id="bf8bd-261">Var olan bir projeye verebilirsiniz iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="bf8bd-262">İçinde **Sunucu Gezgini**, proje düğümüne sağ tıklayın **akış analizi işleri** düğümü ve select **verme yeni Stream Analytics projeye**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Yeni Stream Analytics projesine aktarma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="bf8bd-264">Proje içinde oluşturulan **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-264">The project is generated in **Solution Explorer**.</span></span>

![Çözüm Gezgini'nde oluşturulan proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="bf8bd-266">Ayrıca iş görünümünü kullanın ve tıklayın **proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-266">You also can use the job view, and click **Generate Project**.</span></span>

![Proje oluştur](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="bf8bd-268">Bilinen sorunlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="bf8bd-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="bf8bd-269">Power BI çıkışı ve Azure tarih Lake Store çıktı için desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="bf8bd-270">Ekleyerek veya değiştirerek kullanıcı tanımlı işlevler JavaScript için düzenleyici desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="bf8bd-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf8bd-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf8bd-271">Next steps</span></span>
* [<span data-ttu-id="bf8bd-272">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="bf8bd-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bf8bd-273">Azure Stream Analytics'i kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="bf8bd-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bf8bd-274">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bf8bd-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bf8bd-275">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="bf8bd-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bf8bd-276">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="bf8bd-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
