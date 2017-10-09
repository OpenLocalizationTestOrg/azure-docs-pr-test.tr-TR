---
title: "Visual Studio için Azure Stream Analytics araçları aaaUse | Microsoft Docs"
description: "Başlangıç Öğreticisi hello Visual Studio için Azure Stream Analytics araçları için"
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
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="37f3e-104">Visual Studio için Azure Stream Analytics araçlarını kullanın</span><span class="sxs-lookup"><span data-stu-id="37f3e-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="37f3e-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="37f3e-105">Introduction</span></span>
<span data-ttu-id="37f3e-106">Bu öğreticide, nasıl toouse Azure Stream Analytics araçları Visual Studio toocreate için yazar, yerel olarak test, yönetmek ve akış analizi işleri hata ayıklama öğrenin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="37f3e-107">Bu öğreticiyi tamamladıktan sonra aşağıdakileri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="37f3e-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="37f3e-108">Visual Studio için Stream Analytics araçları edinin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="37f3e-109">Yapılandırın ve akış analizi işi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="37f3e-110">İşinizi yerel örnek verilerle yerel olarak test edin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="37f3e-111">İzleme tootroubleshoot sorunlar kullanın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="37f3e-112">Varolan işleri tooprojects verin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37f3e-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="37f3e-113">Prerequisites</span></span>
<span data-ttu-id="37f3e-114">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="37f3e-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="37f3e-115">Hello "Stream Analytics işi oluştur" koyun hello adımlarını tamamlayın [Stream Analytics öğretici kullanarak bir IOT çözümü derleme](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="37f3e-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="37f3e-116">Visual Studio 2015, Visual Studio 2013 güncelleştirme 4 veya Visual Studio 2012 kullanın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="37f3e-117">Enterprise (Ultimate/Premium), Professional ve topluluk sürümleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="37f3e-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="37f3e-118">Express sürümü desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="37f3e-118">Express edition is not supported.</span></span> <span data-ttu-id="37f3e-119">Visual Studio 2017 desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="37f3e-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="37f3e-120">Kullanım hello .NET sürüm 2.7.1 için Azure SDK'sı veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="37f3e-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="37f3e-121">Hello kullanarak yükleme [Web Platformu yükleyicisi](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="37f3e-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="37f3e-122">Merhaba yüklemek [akış analiz araçları Visual Studio için](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="37f3e-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="37f3e-123">Stream Analytics projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="37f3e-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="37f3e-124">Visual Studio'da hello tıklatın **dosya** menü ve select **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="37f3e-125">Merhaba şablonları listesinden hello soldaki seçin **Stream Analytics** ve ardından **Azure Stream Analytics uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="37f3e-126">Merhaba proje girin **adı**, **konumu**, ve **çözüm adı** için diğer projeler yaptığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="37f3e-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Yeni Proje penceresinin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="37f3e-128">A **Ücretli** proje üretilir **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Çözüm Gezgini'nde oluşturulan Ücretli proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="37f3e-130">Merhaba doğru abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="37f3e-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="37f3e-131">Visual Studio'da hello tıklatın **Görünüm** menü ve açık **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="37f3e-132">Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="37f3e-133">Merhaba giriş kaynaklarıyla tanımlayın</span><span class="sxs-lookup"><span data-stu-id="37f3e-133">Define hello input sources</span></span>
1.  <span data-ttu-id="37f3e-134">İçinde **Çözüm Gezgini**, hello genişletin **girişleri** düğümü ve yeniden adlandırma **Input.json** çok**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="37f3e-135">Çift **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="37f3e-136">Merhaba **giriş diğer adı** artık **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="37f3e-137">Merhaba giriş diğer adı hello sorgu komut dosyasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="37f3e-138">İçinde **kaynak türü**seçin **veri akışı**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="37f3e-139">İçinde **kaynak**seçin **olay hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="37f3e-140">İçinde **Service Bus Namespace**seçin hello **TollData** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="37f3e-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="37f3e-141">İçinde **olay hub'ı adı**seçin **girişi**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="37f3e-142">İçinde **olay hub'ı ilke adı**seçin **RootManageSharedAccessKey** (Merhaba varsayılan değer).</span><span class="sxs-lookup"><span data-stu-id="37f3e-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="37f3e-143">İçinde **olayı seri hale getirme biçimi**seçin **Json**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="37f3e-144">İçinde **kodlama**seçin **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="37f3e-145">Ayarlarınızı hello ekran aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="37f3e-145">Your settings should look like hello following screenshot:</span></span>

    ![Giriş penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="37f3e-147">toofinish hello Sihirbazı'nı tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="37f3e-148">Artık başka bir giriş kaynağı toocreate hello çıkış akışı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f3e-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="37f3e-149">Sağ hello **girişleri** düğümü ve select **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Yeni öğe](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="37f3e-151">Merhaba penceresinde seçin **Azure Stream Analytics giriş**, hello değiştirip **adı** çok**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="37f3e-152">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-152">Click **Add**.</span></span>

    ![Yeni öğe penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="37f3e-154">Çift **ExitStream.json** hello proje ve hello Giriş akışı için yaptığınız gibi aynı adımları izleyin hello.</span><span class="sxs-lookup"><span data-stu-id="37f3e-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="37f3e-155">Emin tooenter olması **çıkmak** hello için **olay hub'ı adı** hello ekran aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="37f3e-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![ExitStream penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="37f3e-157">Şimdi iki giriş akışları tanımladınız:</span><span class="sxs-lookup"><span data-stu-id="37f3e-157">Now you have defined two input streams:</span></span>

    ![Giriş ve çıkış giriş akışları](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="37f3e-159">Ardından, car kayıt verilerini içeren hello blob dosyası için başvuru veri girişi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="37f3e-160">Sağ hello **girişleri** düğümünü hello proje ve hello akış girişleri için yaptığınız gibi aynı adımları izleyin hello.</span><span class="sxs-lookup"><span data-stu-id="37f3e-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="37f3e-161">İçinde **giriş diğer adı**, girin **kayıt**hem de **kaynak türü**seçin **başvuru verileri**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Kayıt penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="37f3e-163">İçinde **depolama hesabı**seçin hello **tolldata** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="37f3e-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="37f3e-164">İçinde **kapsayıcı**seçin **tolldata**hem de **yol deseni**, girin **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="37f3e-165">Bu dosya adı büyük/küçük harfe duyarlıdır ve küçük harf olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="37f3e-166">toofinish hello Sihirbazı'nı tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="37f3e-167">Şimdi tüm hello girişleri tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="37f3e-168">Merhaba çıkış tanımlayın</span><span class="sxs-lookup"><span data-stu-id="37f3e-168">Define hello output</span></span>
1.  <span data-ttu-id="37f3e-169">İçinde **Çözüm Gezgini**, hello genişletin **girişleri** düğümü ve çift **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="37f3e-170">İçinde **çıkış diğer adları**, girin **çıkış**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="37f3e-171">İçinde **havuzu**seçin **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="37f3e-172">İçinde **veritabanı**seçin **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="37f3e-173">İçinde **kullanıcı adı**, girin **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="37f3e-174">İçinde **parola**, girin **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="37f3e-175">İçinde **tablo**, girin **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="37f3e-176">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-176">Click **Save**.</span></span>

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="37f3e-178">Stream Analytics sorgu oluşturma</span><span class="sxs-lookup"><span data-stu-id="37f3e-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="37f3e-179">Bu öğretici tooanswer ilgili tootoll veri birkaç iş soruları çalışır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="37f3e-180">Ayrıca, Stream Analytics tooprovide ilgili yanıtlarında kullanılabilir Stream Analytics sorgu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="37f3e-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="37f3e-181">İlk Stream Analytics işiniz başlamadan önce basit bir senaryo ve hello sorgu sözdizimi inceleyelim.</span><span class="sxs-lookup"><span data-stu-id="37f3e-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="37f3e-182">Giriş toohello Stream Analytics sorgu dili</span><span class="sxs-lookup"><span data-stu-id="37f3e-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="37f3e-183">Ücretli Stand girin taşıtlardan toocount hello sayısı gerektiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="37f3e-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="37f3e-184">Bu örnek sürekli akışı olduğundan, bir süre toodefine sahip.</span><span class="sxs-lookup"><span data-stu-id="37f3e-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="37f3e-185">"Kaç taşıtlardan üç dakikada Ücretli Stand girin?" Merhaba soru toobe değiştirme</span><span class="sxs-lookup"><span data-stu-id="37f3e-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="37f3e-186">Yaygın olarak verilerdir bu şekilde toocount tooas hello dönen sayısı denir.</span><span class="sxs-lookup"><span data-stu-id="37f3e-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="37f3e-187">Bu soruya yanıt veren hello Stream Analytics sorgusu bakın:</span><span class="sxs-lookup"><span data-stu-id="37f3e-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="37f3e-188">Akış analizi gibi SQL ve birkaç uzantıları toospecify saati ile ilgili yönlerini hello sorgu ekleyen bir sorgu dili kullanır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="37f3e-189">Daha fazla bilgi için bkz: [zaman Yönetimi](https://msdn.microsoft.com/library/azure/mt582045.aspx) ve [Pencereleme](https://msdn.microsoft.com/library/azure/dn835019.aspx) MSDN'den hello sorguda kullanılan yapılar.</span><span class="sxs-lookup"><span data-stu-id="37f3e-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="37f3e-190">İlk Stream Analytics sorgu yazılmış, zaman tootest olduğundan bu.</span><span class="sxs-lookup"><span data-stu-id="37f3e-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="37f3e-191">Merhaba örnek veri dosyalarını TollApp klasörü yolu izleyerek hello içinde bulunan kullanın:</span><span class="sxs-lookup"><span data-stu-id="37f3e-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="37f3e-192">.. \TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="37f3e-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="37f3e-193">Bu klasör, aşağıdaki dosyaları hello içerir:</span><span class="sxs-lookup"><span data-stu-id="37f3e-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="37f3e-194">Entry.JSON</span><span class="sxs-lookup"><span data-stu-id="37f3e-194">Entry.json</span></span>
*   <span data-ttu-id="37f3e-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="37f3e-195">Exit.json</span></span>
*   <span data-ttu-id="37f3e-196">Registration.JSON</span><span class="sxs-lookup"><span data-stu-id="37f3e-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="37f3e-197">Ücretli Stand girme taşıtlardan Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="37f3e-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="37f3e-198">Hello projesinde çift **Script.asaql** tooopen hello komut dosyasında hello **sorgu Düzenleyicisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="37f3e-199">Kopyalama ve hello betik hello önceki bölümde hello düzenleyicisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="37f3e-200">IntelliSense, söz dizimi renklendirme ve hello hata işaret Hello sorgu Düzenleyicisi'ni destekler.</span><span class="sxs-lookup"><span data-stu-id="37f3e-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Sorgu Düzenleyicisi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="37f3e-202">Stream Analytics sorguları yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="37f3e-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="37f3e-203">bir sözdizimi hatası ise toocompile hello sorgu toosee hello projesine sağ tıklatın ve **yapı**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="37f3e-204">toovalidate bu sorguyu örnek verileri karşı yerel örnek verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f3e-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="37f3e-205">Merhaba girişi sağ tıklatın ve seçin **yerel girdisi eklemek**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Yerel giriş Ekle](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="37f3e-207">Merhaba açılır penceresinde hello örnek verileri yerel yolundan seçin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="37f3e-208">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-208">Click **Save**.</span></span>

    ![Yerel giriş penceresi ekleyin](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="37f3e-210">Adlı bir dosya **local_EntryStream.json** tooyour giriş klasörü otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="37f3e-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Dosya eklenen tooinputs klasörü](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="37f3e-212">Merhaba, **sorgu Düzenleyicisi'ni**, tıklatın **yerel olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="37f3e-213">Veya hello F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="37f3e-213">Or you can press hello F5 key.</span></span>

    ![Yerel olarak çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Yerel çıkış çalıştırma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="37f3e-216">Herhangi bir anahtar tooview hello çıktı hello basın **ASA yerel çalıştırma sonucu** Visual Studio'daki.</span><span class="sxs-lookup"><span data-stu-id="37f3e-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![ASA yerel çalıştırma sonucu penceresi](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="37f3e-218">Tıklatın **sonuç Klasör Aç** toocheck hello çıktı dosyaları hem de CSV ve JSON biçimi.</span><span class="sxs-lookup"><span data-stu-id="37f3e-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Sonuç klasör çıktısını açın](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="37f3e-220">Örnek hello giriş verileri</span><span class="sxs-lookup"><span data-stu-id="37f3e-220">Sample hello input data</span></span>
<span data-ttu-id="37f3e-221">Ayrıca, giriş kaynağı tooa yerel dosyadan örnek giriş verileri de erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f3e-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="37f3e-222">Merhaba giriş yapılandırma dosyasını sağ tıklatın ve seçin **örnek verileri**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Örnek Veri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="37f3e-224">Şu an için yalnızca olay hub'ı veya IOT hub'ı örnek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37f3e-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="37f3e-225">Diğer giriş kaynağı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="37f3e-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="37f3e-226">Merhaba açılır penceresinde hello kullanılan yerel yolu toosave hello örnek verileri girin.</span><span class="sxs-lookup"><span data-stu-id="37f3e-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="37f3e-227">Tıklatın **örnek**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-227">Click **Sample**.</span></span>

    ![Örnek veri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="37f3e-229">Merhaba hello ediyor görebilirsiniz **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="37f3e-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Çıktı penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="37f3e-231">Stream Analytics sorgu tooAzure Gönder</span><span class="sxs-lookup"><span data-stu-id="37f3e-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="37f3e-232">Merhaba, **sorgu Düzenleyicisi'ni**, tıklatın **tooAzure gönderme** hello komut dosyası Düzenleyicisi'nde.</span><span class="sxs-lookup"><span data-stu-id="37f3e-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![TooAzure Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="37f3e-234">Seçin **yeni bir Azure Stream Analytics işi oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="37f3e-235">Merhaba girin **iş adı**ve select hello doğru **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="37f3e-236">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-236">Click **Submit**.</span></span>

    ![İş pencere Gönder](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="37f3e-238">Bir işi Başlat</span><span class="sxs-lookup"><span data-stu-id="37f3e-238">Start a job</span></span>
<span data-ttu-id="37f3e-239">İşinizi oluşturulur, hello iş görünümünde otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="37f3e-240">toostart hello işi, hello tıklatın **yeşil ok** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="37f3e-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Bir işi Başlat](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="37f3e-242">Merhaba varsayılan ayarı seçin ve'ı tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-242">Select hello default setting, and click **Start**.</span></span>
 
    ![İş penceresi başlangıç](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="37f3e-244">Merhaba iş **durum** çok değiştirir**çalıştıran**, ve **giriş olayları** ve **çıkış olaylarındaki** görünür.</span><span class="sxs-lookup"><span data-stu-id="37f3e-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![İş özeti çalışma durumu](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="37f3e-246">Visual Studio'da hello sonuçları denetleyin</span><span class="sxs-lookup"><span data-stu-id="37f3e-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="37f3e-247">Visual Studio'da açın **Sunucu Gezgini** ve sağ hello **TollDataRefJoin** tablo.</span><span class="sxs-lookup"><span data-stu-id="37f3e-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="37f3e-248">Seçin **Show Table Data** işinizin toosee hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="37f3e-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Sunucu Gezgini'nde tablo verileri göster seçimi](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="37f3e-250">Merhaba iş metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="37f3e-250">View hello job metrics</span></span>
<span data-ttu-id="37f3e-251">Bazı temel iş istatistiklerinde bulunabilir **iş ölçümleri**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![İş ölçümleri penceresi](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="37f3e-253">Sunucu Gezgininde listesi hello işi</span><span class="sxs-lookup"><span data-stu-id="37f3e-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="37f3e-254">İçinde **Sunucu Gezgini**, tıklatın **akış analizi işleri** ve ardından **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="37f3e-255">Merhaba iş altında görünür **akış analizi işleri**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Server Explorer'da listelenen stream Analytics işleri](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="37f3e-257">Açık hello işi görüntüle</span><span class="sxs-lookup"><span data-stu-id="37f3e-257">Open hello job view</span></span>
<span data-ttu-id="37f3e-258">tooopen hello iş görünümünde, iş düğümünü genişletin ve hello çift **iş görünümünde** düğümü.</span><span class="sxs-lookup"><span data-stu-id="37f3e-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![İş görünümünde düğümü](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="37f3e-260">Mevcut bir iş tooa projesini dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="37f3e-260">Export an existing job tooa project</span></span>
<span data-ttu-id="37f3e-261">Mevcut bir iş tooa projesini verebilirsiniz iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="37f3e-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="37f3e-262">İçinde **Sunucu Gezgini**, sağ hello iş hello düğümünde **akış analizi işleri** düğümü ve select **tooNew Stream Analytics proje verme**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![Stream Analytics proje tooNew dışarı aktarma](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="37f3e-264">Merhaba proje üretilir **Çözüm Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-264">hello project is generated in **Solution Explorer**.</span></span>

![Çözüm Gezgini'nde oluşturulan proje](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="37f3e-266">Ayrıca hello iş görünümünde kullanın ve tıklatın **proje oluştur**.</span><span class="sxs-lookup"><span data-stu-id="37f3e-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Proje oluştur](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="37f3e-268">Bilinen sorunlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="37f3e-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="37f3e-269">Power BI çıkışı ve Azure tarih Lake Store çıktı için desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="37f3e-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="37f3e-270">Ekleyerek veya değiştirerek kullanıcı tanımlı işlevler JavaScript için düzenleyici desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="37f3e-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37f3e-271">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37f3e-271">Next steps</span></span>
* [<span data-ttu-id="37f3e-272">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="37f3e-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="37f3e-273">Azure Stream Analytics'i kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="37f3e-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="37f3e-274">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="37f3e-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="37f3e-275">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="37f3e-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="37f3e-276">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="37f3e-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
