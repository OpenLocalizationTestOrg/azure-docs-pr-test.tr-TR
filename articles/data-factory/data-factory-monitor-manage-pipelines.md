---
title: "aaaMonitor ve ardışık düzen hello Azure portal ve PowerShell kullanarak yönetme | Microsoft Docs"
description: "Nasıl toouse Azure portalı ve Azure PowerShell toomonitor hello ve hello Azure data factory'leri ve oluşturduğunuz ardışık düzen yönetmek öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a><span data-ttu-id="8637f-103">İzleme ve hello Azure portal ve PowerShell kullanarak Azure Data Factory işlem hatlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8637f-103">Monitor and manage Azure Data Factory pipelines by using hello Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8637f-104">Azure portal/Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="8637f-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="8637f-105">Kullanılarak izleme ve yönetim uygulaması</span><span class="sxs-lookup"><span data-stu-id="8637f-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="8637f-106">Merhaba izleme ve yönetim uygulaması izleme ve veri işlem hatlarınızı yönetmek ve sorunları gidermek için daha iyi destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="8637f-106">hello monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="8637f-107">Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="8637f-107">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="8637f-108">Bu makalede nasıl toomonitor, yönetmek ve işlem hatlarınızı Azure portalı ve PowerShell kullanarak hata ayıklama açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8637f-108">This article describes how toomonitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="8637f-109">Merhaba makale ayrıca nasıl toocreate uyarılar ve bilgiler almak sağlar hataları hakkında bildirim.</span><span class="sxs-lookup"><span data-stu-id="8637f-109">hello article also provides information on how toocreate alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="8637f-110">Ardışık Düzen ve etkinlik durumlarını anlama</span><span class="sxs-lookup"><span data-stu-id="8637f-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="8637f-111">Hello Azure portal kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8637f-111">By using hello Azure portal, you can:</span></span>

* <span data-ttu-id="8637f-112">Veri fabrikanızın diyagramı olarak görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8637f-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="8637f-113">Bir ardışık düzendeki etkinlik görünümü.</span><span class="sxs-lookup"><span data-stu-id="8637f-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="8637f-114">Giriş ve çıkış veri kümeleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8637f-114">View input and output datasets.</span></span>

<span data-ttu-id="8637f-115">Bu bölümde ayrıca veri kümesi dilim durum tooanother durumundan nasıl geçiş açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8637f-115">This section also describes how a dataset slice transitions from one state tooanother state.</span></span>   

### <a name="navigate-tooyour-data-factory"></a><span data-ttu-id="8637f-116">Tooyour veri fabrikası gidin</span><span class="sxs-lookup"><span data-stu-id="8637f-116">Navigate tooyour data factory</span></span>
1. <span data-ttu-id="8637f-117">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8637f-117">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8637f-118">Tıklatın **veri fabrikaları** hello sol hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="8637f-118">Click **Data factories** on hello menu on hello left.</span></span> <span data-ttu-id="8637f-119">Göremiyorsanız, tıklatın **daha fazla hizmet >**ve ardından **veri fabrikaları** hello altında **INTELLİGENCE + ANALİZ** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="8637f-119">If you don't see it, click **More services >**, and then click **Data factories** under hello **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Tümüne Gözat > veri fabrikaları](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="8637f-121">Merhaba üzerinde **veri fabrikaları** dikey penceresinde, ilgilendiğiniz select hello veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="8637f-121">On hello **Data factories** blade, select hello data factory that you're interested in.</span></span>

    ![Veri Fabrikası seçin](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="8637f-123">Merhaba veri fabrikası için hello giriş sayfasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8637f-123">You should see hello home page for hello data factory.</span></span>

   ![Data factory dikey penceresi](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="8637f-125">Veri fabrikanızın diyagram görünümü</span><span class="sxs-lookup"><span data-stu-id="8637f-125">Diagram view of your data factory</span></span>
<span data-ttu-id="8637f-126">Merhaba **diyagramı** data factory görünümünü hello veri fabrikası ve varlıklarını yönetmenize ve bölmeden cam toomonitor sağlar.</span><span class="sxs-lookup"><span data-stu-id="8637f-126">hello **Diagram** view of a data factory provides a single pane of glass toomonitor and manage hello data factory and its assets.</span></span> <span data-ttu-id="8637f-127">toosee hello **diyagramı** 'ı tıklatın, görüntüleyin, veri fabrikası **diyagramı** hello giriş sayfasında hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="8637f-127">toosee hello **Diagram** view of your data factory, click **Diagram** on hello home page for hello data factory.</span></span>

![Diyagram görünümü](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="8637f-129">Yakınlaştırma, yakınlaştırma toofit, yakınlaştırma too100%, kilit hello düzeni hello diyagramı çıkışı, yakınlaştırma ve otomatik olarak ardışık düzen ve veri kümeleri yerleştir.</span><span class="sxs-lookup"><span data-stu-id="8637f-129">You can zoom in, zoom out, zoom toofit, zoom too100%, lock hello layout of hello diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="8637f-130">Merhaba veri çizgileri bilgileri de görebilirsiniz (diğer bir deyişle, seçilen öğelerin Yukarı Akış ve aşağı akış öğelerini göster).</span><span class="sxs-lookup"><span data-stu-id="8637f-130">You can also see hello data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="8637f-131">Bir işlem hattı içindeki etkinlikler</span><span class="sxs-lookup"><span data-stu-id="8637f-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="8637f-132">Merhaba ardışık düzen sağ tıklayın ve ardından **açık işlem hattı** toosee hello etkinlikler için girdi ve çıktı veri kümeleriyle birlikte potansiyel satış hello tüm etkinlikler.</span><span class="sxs-lookup"><span data-stu-id="8637f-132">Right-click hello pipeline, and then click **Open pipeline** toosee all activities in hello pipeline, along with input and output datasets for hello activities.</span></span> <span data-ttu-id="8637f-133">Bu özellik, işlem hattınızı birden fazla etkinlik içerir ve tek bir ardışık toounderstand hello işletimsel çizgileri istediğinizde yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="8637f-133">This feature is useful when your pipeline includes more than one activity and you want toounderstand hello operational lineage of a single pipeline.</span></span>

    ![İşlem hattı menüsünü açma](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="8637f-135">Aşağıdaki örneğine hello kopyalama etkinliği bir girdi ve çıktı hello düzenindeki bakın.</span><span class="sxs-lookup"><span data-stu-id="8637f-135">In hello following example, you see a copy activity in hello pipeline with an input and an output.</span></span> 

    ![Bir işlem hattı içindeki etkinlikler](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="8637f-137">Merhaba tıklatarak geri toohello hello data Factory giriş sayfasına gidebilirsiniz **veri fabrikası** hello içerik haritası hello sol üst köşesinde bağlantıyı.</span><span class="sxs-lookup"><span data-stu-id="8637f-137">You can navigate back toohello home page of hello data factory by clicking hello **Data factory** link in hello breadcrumb at hello top-left corner.</span></span>

    ![Geri toodata Fabrika gidin](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="8637f-139">Her etkinliği bir ardışık düzen içinde hello durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="8637f-139">View hello state of each activity inside a pipeline</span></span>
<span data-ttu-id="8637f-140">Merhaba durumunu hello etkinliği tarafından üretilen hello veri kümeleri görüntüleyerek hello geçerli bir etkinlik durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-140">You can view hello current state of an activity by viewing hello status of any of hello datasets that are produced by hello activity.</span></span>

<span data-ttu-id="8637f-141">Merhaba çift tıklatarak **OutputBlobTable** hello içinde **diyagramı**, farklı etkinlik çalışması içinde bir ardışık düzen tarafından üretilen tüm hello dilimler görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-141">By double-clicking hello **OutputBlobTable** in hello **Diagram**, you can see all hello slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="8637f-142">Merhaba kopyalama etkinliği Merhaba son sekiz saat başarıyla çalıştırdı ve hello içinde hello dilimlerinin görebilirsiniz **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="8637f-142">You can see that hello copy activity ran successfully for hello last eight hours and produced hello slices in hello **Ready** state.</span></span>  

![Merhaba ardışık durumu](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="8637f-144">Merhaba dataset dilimler hello veri fabrikasında durumları aşağıdaki hello biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="8637f-144">hello dataset slices in hello data factory can have one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="8637f-145">Durum</span><span class="sxs-lookup"><span data-stu-id="8637f-145">State</span></span></th><th align="left"><span data-ttu-id="8637f-146">Bölgesine</span><span class="sxs-lookup"><span data-stu-id="8637f-146">Substate</span></span></th><th align="left"><span data-ttu-id="8637f-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8637f-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="8637f-148">Bekleniyor</span><span class="sxs-lookup"><span data-stu-id="8637f-148">Waiting</span></span></td><td><span data-ttu-id="8637f-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="8637f-149">ScheduleTime</span></span></td><td><span data-ttu-id="8637f-150">Başlangıç saati hello dilim toorun için gelen kurmadı.</span><span class="sxs-lookup"><span data-stu-id="8637f-150">hello time hasn't come for hello slice toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="8637f-151">DatasetDependencies</span></span></td><td><span data-ttu-id="8637f-152">Merhaba Yukarı Akış bağımlılıkları hazır değil.</span><span class="sxs-lookup"><span data-stu-id="8637f-152">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="8637f-153">ComputeResources</span></span></td><td><span data-ttu-id="8637f-154">Merhaba işlem kaynakları kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="8637f-154">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="8637f-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="8637f-156">Tüm hello etkinlik örnekleri diğer dilimleri çalıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="8637f-156">All hello activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="8637f-157">ActivityResume</span></span></td><td><span data-ttu-id="8637f-158">Merhaba etkinlik duraklatıldı ve hello etkinlik sürdürülene kadar hello dilimler çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="8637f-158">hello activity is paused and can't run hello slices until hello activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-159">Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="8637f-159">Retry</span></span></td><td><span data-ttu-id="8637f-160">Etkinlik yürütme yeniden deneniyor.</span><span class="sxs-lookup"><span data-stu-id="8637f-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-161">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="8637f-161">Validation</span></span></td><td><span data-ttu-id="8637f-162">Doğrulama henüz başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="8637f-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="8637f-163">ValidationRetry</span></span></td><td><span data-ttu-id="8637f-164">Doğrulama denenen bekleme toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="8637f-164">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="8637f-165">Devam ediyor</span><span class="sxs-lookup"><span data-stu-id="8637f-165">InProgress</span></span></td><td><span data-ttu-id="8637f-166">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="8637f-166">Validating</span></span></td><td><span data-ttu-id="8637f-167">Doğrulama devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="8637f-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="8637f-168">Merhaba dilim işleniyor.</span><span class="sxs-lookup"><span data-stu-id="8637f-168">hello slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="8637f-169">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="8637f-169">Failed</span></span></td><td><span data-ttu-id="8637f-170">Süresi sona erdi</span><span class="sxs-lookup"><span data-stu-id="8637f-170">TimedOut</span></span></td><td><span data-ttu-id="8637f-171">Merhaba Etkinlik yürütme hello etkinliği tarafından izin daha uzun sürdü.</span><span class="sxs-lookup"><span data-stu-id="8637f-171">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-172">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="8637f-172">Canceled</span></span></td><td><span data-ttu-id="8637f-173">Merhaba dilim kullanıcı eylemi tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="8637f-173">hello slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-174">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="8637f-174">Validation</span></span></td><td><span data-ttu-id="8637f-175">Doğrulama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8637f-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="8637f-176">Merhaba dilim oluşturulan ve/veya doğrulanmış toobe başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="8637f-176">hello slice failed toobe generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="8637f-177">Hazır</span><span class="sxs-lookup"><span data-stu-id="8637f-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="8637f-178">Merhaba dilim kullanıma hazır olur.</span><span class="sxs-lookup"><span data-stu-id="8637f-178">hello slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-179">Atlandı</span><span class="sxs-lookup"><span data-stu-id="8637f-179">Skipped</span></span></td><td><span data-ttu-id="8637f-180">None</span><span class="sxs-lookup"><span data-stu-id="8637f-180">None</span></span></td><td><span data-ttu-id="8637f-181">Merhaba dilimin işlenmekte olan değil.</span><span class="sxs-lookup"><span data-stu-id="8637f-181">hello slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="8637f-182">None</span><span class="sxs-lookup"><span data-stu-id="8637f-182">None</span></span></td><td>-</td><td><span data-ttu-id="8637f-183">Bir dilim tooexist farklı bir durum ile kullanılan ancak sıfırlandı.</span><span class="sxs-lookup"><span data-stu-id="8637f-183">A slice used tooexist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="8637f-184">Merhaba dilim girişinde tıklayarak bir dilim hello ayrıntılarını görüntüleyebilirsiniz **en son güncelleştirilen dilimler** dikey.</span><span class="sxs-lookup"><span data-stu-id="8637f-184">You can view hello details about a slice by clicking a slice entry on hello **Recently Updated Slices** blade.</span></span>

![Dilim ayrıntıları](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="8637f-186">Hello dilim birden çok kez yürütülmüşse, birden çok satır hello bkz **etkinlik çalışır** listesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-186">If hello slice has been executed multiple times, you see multiple rows in hello **Activity runs** list.</span></span> <span data-ttu-id="8637f-187">Hello çalıştırmak hello girişi tıklayarak Çalıştır etkinliği hakkında ayrıntılı bilgi görüntüleyebileceğiniz **etkinlik çalışır** listesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-187">You can view details about an activity run by clicking hello run entry in hello **Activity runs** list.</span></span> <span data-ttu-id="8637f-188">Merhaba liste varsa bir hata iletisi ile birlikte tüm hello günlük dosyalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8637f-188">hello list shows all hello log files, along with an error message if there is one.</span></span> <span data-ttu-id="8637f-189">Bu özellik, veri fabrikası tooleave kalmadan yararlı tooview ve hata ayıklama günlüklerini kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8637f-189">This feature is useful tooview and debug logs without having tooleave your data factory.</span></span>

![Etkinlik çalışma ayrıntıları](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="8637f-191">Merhaba dilim hello değilse **hazır** durumu, hazır değil ve geçerli dilimin yürütülmesini hello hello engelleme hello Yukarı Akış dilimleri görebilirsiniz **hazır olmayan Yukarı Akış dilimleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-191">If hello slice isn't in hello **Ready** state, you can see hello upstream slices that aren't ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="8637f-192">Bu özellik, dilim olduğunda yararlıdır **bekleyen** durumu ve istediğiniz dilim hello toounderstand hello Yukarı Akış bağımlılıkları bekliyor.</span><span class="sxs-lookup"><span data-stu-id="8637f-192">This feature is useful when your slice is in **Waiting** state and you want toounderstand hello upstream dependencies that hello slice is waiting on.</span></span>

![Hazır olmayan yukarı akış dilimleri](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="8637f-194">Veri kümesi durumu diyagramı</span><span class="sxs-lookup"><span data-stu-id="8637f-194">Dataset state diagram</span></span>
<span data-ttu-id="8637f-195">Veri Fabrikası dağıtmak ve hello ardışık düzen geçerli bir etkin döneme sahip sonra hello dataset durum tooanother geçiş böler.</span><span class="sxs-lookup"><span data-stu-id="8637f-195">After you deploy a data factory and hello pipelines have a valid active period, hello dataset slices transition from one state tooanother.</span></span> <span data-ttu-id="8637f-196">Şu anda durumu diyagramı aşağıdaki hello hello dilim durumunu izler:</span><span class="sxs-lookup"><span data-stu-id="8637f-196">Currently, hello slice status follows hello following state diagram:</span></span>

![Durum Diyagramı](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="8637f-198">Merhaba veri fabrikasında veri kümesi durumu geçişi akışı hello aşağıdadır: bekleme içinde-ilerleme/Sürüyor (doğrulama) -> hazır/başarısız->.</span><span class="sxs-lookup"><span data-stu-id="8637f-198">hello dataset state transition flow in data factory is hello following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="8637f-199">Merhaba dilim başlatır bir **bekleyen** durumu, yürütülmeden önce karşılanıp önkoşulları toobe için bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="8637f-199">hello slice starts in a **Waiting** state, waiting for preconditions toobe met before it executes.</span></span> <span data-ttu-id="8637f-200">Ardından, hello Etkinliğin başlangıç yürütme ve hello dilim girer içine bir **sürüyor** durumu.</span><span class="sxs-lookup"><span data-stu-id="8637f-200">Then, hello activity starts executing, and hello slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="8637f-201">Merhaba Etkinlik yürütme başarılı veya başarısız.</span><span class="sxs-lookup"><span data-stu-id="8637f-201">hello activity execution might succeed or fail.</span></span> <span data-ttu-id="8637f-202">Merhaba dilim olarak işaretli **hazır** veya **başarısız**bağlı olarak hello hello yürütme sonucu.</span><span class="sxs-lookup"><span data-stu-id="8637f-202">hello slice is marked as **Ready** or **Failed**, based on hello result of hello execution.</span></span>

<span data-ttu-id="8637f-203">Merhaba dilim toogo hello gelen geri sıfırlayabilirsiniz **hazır** veya **başarısız** durumu toohello **bekleyen** durumu.</span><span class="sxs-lookup"><span data-stu-id="8637f-203">You can reset hello slice toogo back from hello **Ready** or **Failed** state toohello **Waiting** state.</span></span> <span data-ttu-id="8637f-204">Merhaba dilim durumu çok işaretleyebilirsiniz**atla**, yürütme ve hello dilim işlenmiyor hello etkinlik engeller.</span><span class="sxs-lookup"><span data-stu-id="8637f-204">You can also mark hello slice state too**Skip**, which prevents hello activity from executing and not processing hello slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="8637f-205">Ardışık Düzen Durdur</span><span class="sxs-lookup"><span data-stu-id="8637f-205">Pause and resume pipelines</span></span>
<span data-ttu-id="8637f-206">Azure PowerShell kullanarak işlem hatlarınızı yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="8637f-207">Örneğin, duraklatma ve ardışık düzen Azure PowerShell cmdlet'lerini çalıştırarak sürdürme.</span><span class="sxs-lookup"><span data-stu-id="8637f-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="8637f-208">Merhaba diyagram görünümü, duraklatma ve sürdürme ardışık düzen desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8637f-208">hello diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="8637f-209">Bir kullanıcı arabirimi toouse istiyorsanız hello izleme ve yönetme uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="8637f-209">If you want toouse an user interface, use hello monitoring and managing application.</span></span> <span data-ttu-id="8637f-210">Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-210">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="8637f-211">Duraklat/işlem hatları hello kullanarak askıya alabilirsiniz **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8637f-211">You can pause/suspend pipelines by using hello **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="8637f-212">Bu cmdlet, bir sorun düzeltilene kadar toorun hatlarınızı istemediğiniz yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8637f-212">This cmdlet is useful when you don’t want toorun your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="8637f-213">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8637f-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="8637f-214">Merhaba ardışık ile Merhaba sorun çözüldükten sonra hello aşağıdaki PowerShell komutunu çalıştırarak askıya hello ardışık düzen devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8637f-214">After hello issue has been fixed with hello pipeline, you can resume hello suspended pipeline by running hello following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="8637f-215">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8637f-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="8637f-216">Ardışık Düzen hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="8637f-216">Debug pipelines</span></span>
<span data-ttu-id="8637f-217">Azure Data Factory Zengin özellikleri sizin için toodebug sağlar ve ardışık düzen hello Azure portalı ve Azure PowerShell kullanarak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="8637f-217">Azure Data Factory provides rich capabilities for you toodebug and troubleshoot pipelines by using hello Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="8637f-218">[! Bu çok daha kolay kullanarak hataları izleme hello tootroubleshot ve yönetim uygulaması Not}.</span><span class="sxs-lookup"><span data-stu-id="8637f-218">[!NOTE} It is much easier tootroubleshot errors using hello Monitoring & Management App.</span></span> <span data-ttu-id="8637f-219">Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-219">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="8637f-220">Ardışık düzeninde hataları bulma</span><span class="sxs-lookup"><span data-stu-id="8637f-220">Find errors in a pipeline</span></span>
<span data-ttu-id="8637f-221">Ardışık düzeninde hello etkinlik başarısız olursa hello ardışık düzen tarafından üretilen hello dataset hello hatası nedeniyle bir hata durumunda olur.</span><span class="sxs-lookup"><span data-stu-id="8637f-221">If hello activity run fails in a pipeline, hello dataset that is produced by hello pipeline is in an error state because of hello failure.</span></span> <span data-ttu-id="8637f-222">Hata ayıklama ve yöntemleri aşağıdaki hello kullanarak Azure Data factory'de hatalarında sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="8637f-222">You can debug and troubleshoot errors in Azure Data Factory by using hello following methods.</span></span>

#### <a name="use-hello-azure-portal-toodebug-an-error"></a><span data-ttu-id="8637f-223">Hello Azure portal toodebug hata kullanın</span><span class="sxs-lookup"><span data-stu-id="8637f-223">Use hello Azure portal toodebug an error</span></span>
1. <span data-ttu-id="8637f-224">Merhaba üzerinde **tablo** dikey penceresinde hello sahip hello sorun dilimi tıklatın **durum** çok ayarlamak**başarısız**.</span><span class="sxs-lookup"><span data-stu-id="8637f-224">On hello **Table** blade, click hello problem slice that has hello **Status** set too**Failed**.</span></span>

   ![Sorun dilim ile tablo dikey penceresi](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="8637f-226">Merhaba üzerinde **veri dilimi** dikey penceresinde hello etkinlik başarısız Çalıştır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8637f-226">On hello **Data slice** blade, click hello activity run that failed.</span></span>

   ![Veri dilimi bir hata ile](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="8637f-228">Merhaba üzerinde **etkinlik çalışma ayrıntıları** dikey penceresinde hello Hdınsight işleme ile ilişkili olan hello dosyaları karşıdan yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-228">On hello **Activity run details** blade, you can download hello files that are associated with hello HDInsight processing.</span></span> <span data-ttu-id="8637f-229">Tıklatın **karşıdan** hello hata hakkındaki ayrıntılar içeren durumu/stderr toodownload hello hata günlüğü dosyası için.</span><span class="sxs-lookup"><span data-stu-id="8637f-229">Click **Download** for Status/stderr toodownload hello error log file that contains details about hello error.</span></span>

   ![Etkinlik ayrıntıları dikey penceresinde hatası ile çalıştırma](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a><span data-ttu-id="8637f-231">PowerShell toodebug hata kullanın</span><span class="sxs-lookup"><span data-stu-id="8637f-231">Use PowerShell toodebug an error</span></span>
1. <span data-ttu-id="8637f-232">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="8637f-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="8637f-233">Merhaba çalıştırmak **Get-AzureRmDataFactorySlice** toosee hello dilimleri ve bunların durumlarını komutu.</span><span class="sxs-lookup"><span data-stu-id="8637f-233">Run hello **Get-AzureRmDataFactorySlice** command toosee hello slices and their statuses.</span></span> <span data-ttu-id="8637f-234">Merhaba durumuna sahip bir dilim görmeniz gerekir **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="8637f-234">You should see a slice with hello status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="8637f-235">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8637f-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="8637f-236">Değiştir **StartDateTime** hattınızı başlangıç saati ile.</span><span class="sxs-lookup"><span data-stu-id="8637f-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="8637f-237">Şimdi, hello çalıştırın **Get-AzureRmDataFactoryRun** cmdlet tooget etkinliği hakkında ayrıntılı bilgi hello hello dilim için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8637f-237">Now, run hello **Get-AzureRmDataFactoryRun** cmdlet tooget details about hello activity run for hello slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="8637f-238">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8637f-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="8637f-239">Merhaba StartDateTime hello önceki adımda not ettiğiniz hello hata/sorun dilim için hello başlangıç zamanı değeridir.</span><span class="sxs-lookup"><span data-stu-id="8637f-239">hello value of StartDateTime is hello start time for hello error/problem slice that you noted from hello previous step.</span></span> <span data-ttu-id="8637f-240">Merhaba tarih-saat çift tırnak içine alınabilir.</span><span class="sxs-lookup"><span data-stu-id="8637f-240">hello date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="8637f-241">Benzer toohello aşağıda hello hata ilişkin ayrıntıları içeren bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8637f-241">You should see output with details about hello error that is similar toohello following:</span></span>

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. <span data-ttu-id="8637f-242">Merhaba çalıştırabilirsiniz **Kaydet AzureRmDataFactoryLog** hello hello çıkışı görmek ve hello kullanarak hello günlük dosyalarını indirmek kimliği değeri cmdlet'iyle **- DownloadLogsoption** hello cmdlet'i için.</span><span class="sxs-lookup"><span data-stu-id="8637f-242">You can run hello **Save-AzureRmDataFactoryLog** cmdlet with hello Id value that you see from hello output, and download hello log files by using hello **-DownloadLogsoption** for hello cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="8637f-243">Ardışık düzeninde hataları yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8637f-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8637f-244">Daha kolay tootroubleshoot hataları olan ve izleme ve yönetim uygulaması kullanarak yeniden çalıştır başarısız dilimler hello.</span><span class="sxs-lookup"><span data-stu-id="8637f-244">It's easier tootroubleshoot errors and rerun failed slices by using hello Monitoring & Management App.</span></span> <span data-ttu-id="8637f-245">Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="8637f-245">For details about using hello application, see [monitor and manage Data Factory pipelines by using hello Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-hello-azure-portal"></a><span data-ttu-id="8637f-246">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="8637f-246">Use hello Azure portal</span></span>
<span data-ttu-id="8637f-247">Sorun giderme ve hata ayıklama hataları ardışık düzeninde sonra toohello hata dilim gezinme ve hello tıklayarak hataları çalıştırabilirsiniz **çalıştırmak** hello komut çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating toohello error slice and clicking hello **Run** button on hello command bar.</span></span>

![Başarısız bir dilimi yeniden çalıştırın](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="8637f-249">(Örneğin, veri kullanılamıyorsa) durumda hello dilim doğrulama bir ilke hatası nedeniyle başarısız oldu, hello hatası düzeltin ve yeniden hello tıklayarak doğrulamayı **doğrulama** hello komut çubuğunda düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-249">In case hello slice has failed validation because of a policy failure (for example, if data isn't available), you can fix hello failure and validate again by clicking hello **Validate** button on hello command bar.</span></span>

![Hataları giderin ve doğrulama](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="8637f-251">Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="8637f-251">Use Azure PowerShell</span></span>
<span data-ttu-id="8637f-252">Hello kullanarak hataları çalıştırabilirsiniz **Set-AzureRmDataFactorySliceStatus** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8637f-252">You can rerun failures by using hello **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="8637f-253">Merhaba bkz [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) sözdizimi ve hello cmdlet'i hakkındaki diğer ayrıntılar için konu.</span><span class="sxs-lookup"><span data-stu-id="8637f-253">See hello [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about hello cmdlet.</span></span>

<span data-ttu-id="8637f-254">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="8637f-254">**Example:**</span></span>

<span data-ttu-id="8637f-255">Merhaba aşağıdaki örnek ayarlar hello tablo 'DAWikiAggregatedData' too'Waiting tüm dilimleri hello durumunu ' hello Azure data factory'de 'WikiADF'.</span><span class="sxs-lookup"><span data-stu-id="8637f-255">hello following example sets hello status of all slices for hello table 'DAWikiAggregatedData' too'Waiting' in hello Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="8637f-256">Merhaba 'Güncelleştirme türü' too'UpstreamInPipeline ayarlanmış ', yani her dilim Merhaba tablonun tüm hello bağımlı (Yukarı Akış) tablolar ve durumlarını too'Waiting ayarlanır'.</span><span class="sxs-lookup"><span data-stu-id="8637f-256">hello 'UpdateType' is set too'UpstreamInPipeline', which means that statuses of each slice for hello table and all hello dependent (upstream) tables are set too'Waiting'.</span></span> <span data-ttu-id="8637f-257">Bu parametre 'Bireysel' için başka bir olası değer hello.</span><span class="sxs-lookup"><span data-stu-id="8637f-257">hello other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="8637f-258">Uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8637f-258">Create alerts</span></span>
<span data-ttu-id="8637f-259">Azure günlükleri kullanıcı olayları bir Azure kaynak olduğunda (örneğin, veri fabrikası) oluşturulan, güncelleştirilmiş veya silinmiş.</span><span class="sxs-lookup"><span data-stu-id="8637f-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="8637f-260">Bu olaylara bağlı olarak uyarıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-260">You can create alerts on these events.</span></span> <span data-ttu-id="8637f-261">Veri Fabrikası toocapture çeşitli ölçümleri kullanın ve ölçümleri uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="8637f-261">You can use Data Factory toocapture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="8637f-262">Gerçek zamanlı izleme için olayları kullanın ve ölçümleri geçmiş amaçları için kullanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="8637f-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="8637f-263">Uyarı olayları</span><span class="sxs-lookup"><span data-stu-id="8637f-263">Alerts on events</span></span>
<span data-ttu-id="8637f-264">Azure olayları, Azure kaynaklarınızı neler olduğunu içine yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8637f-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="8637f-265">Azure Data Factory kullanırken, olaylar oluşturulur zaman:</span><span class="sxs-lookup"><span data-stu-id="8637f-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="8637f-266">Veri Fabrikası oluşturulduğunda, silinmiş veya güncelleştirildiğinde.</span><span class="sxs-lookup"><span data-stu-id="8637f-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="8637f-267">Veri işleme ("çalışır") olarak başlatıldı veya tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8637f-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="8637f-268">İsteğe bağlı Hdınsight kümesi oluşturulduğunda veya kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="8637f-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="8637f-269">Bu kullanıcı olaylarına uyarılar oluşturabilir ve bunları toosend e-posta bildirimleri toohello yönetici ve coadministrators hello aboneliğin yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8637f-269">You can create alerts on these user events and configure them toosend email notifications toohello administrator and coadministrators of hello subscription.</span></span> <span data-ttu-id="8637f-270">Ayrıca, tooreceive e-posta bildirimleri hello koşullar karşılandığında isteyen kullanıcıların ek e-posta adresini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-270">In addition, you can specify additional email addresses of users who need tooreceive email notifications when hello conditions are met.</span></span> <span data-ttu-id="8637f-271">Bu özellik, hataları üzerinde bildirim tooget ve toocontinuously İzleyici, veri fabrikası istemediğiniz istediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8637f-271">This feature is useful when you want tooget notified on failures and don’t want toocontinuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="8637f-272">Şu anda hello portal olayları uyarıları göstermez.</span><span class="sxs-lookup"><span data-stu-id="8637f-272">Currently, hello portal doesn't show alerts on events.</span></span> <span data-ttu-id="8637f-273">Kullanım hello [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md) toosee tüm uyarılar.</span><span class="sxs-lookup"><span data-stu-id="8637f-273">Use hello [Monitoring and Management app](data-factory-monitor-manage-app.md) toosee all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="8637f-274">Bir uyarı tanımı belirtin</span><span class="sxs-lookup"><span data-stu-id="8637f-274">Specify an alert definition</span></span>
<span data-ttu-id="8637f-275">bir uyarı tanımı toospecify, uyarı toobe istediğiniz hello işlemleri açıklayan bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8637f-275">toospecify an alert definition, you create a JSON file that describes hello operations that you want toobe alerted on.</span></span> <span data-ttu-id="8637f-276">Aşağıdaki örneğine hello hello uyarısı hello RunFinished işlemi için bir e-posta bildirimi gönderir.</span><span class="sxs-lookup"><span data-stu-id="8637f-276">In hello following example, hello alert sends an email notification for hello RunFinished operation.</span></span> <span data-ttu-id="8637f-277">toobe belirli, bir e-posta bildirimi gönderildi hello veri fabrikasında bir farklı çalıştır tamamlandı ve Çalıştır hello başarısız oldu (durum = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="8637f-277">toobe specific, an email notification is sent when a run in hello data factory has completed and hello run has failed (Status = FailedExecution).</span></span>

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

<span data-ttu-id="8637f-278">Kaldırabileceğiniz **subStatus** hello belirli bir arıza uyarı toobe istemiyorsanız, JSON tanımını gelen.</span><span class="sxs-lookup"><span data-stu-id="8637f-278">You can remove **subStatus** from hello JSON definition if you don’t want toobe alerted on a specific failure.</span></span>

<span data-ttu-id="8637f-279">Bu örnek, aboneliğinizdeki tüm veri fabrikaları için hello uyarı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8637f-279">This example sets up hello alert for all data factories in your subscription.</span></span> <span data-ttu-id="8637f-280">Merhaba uyarı toobe belirli veri fabrikası için ayarlamak istiyorsanız, veri fabrikası belirtebilirsiniz **resourceUri** hello içinde **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="8637f-280">If you want hello alert toobe set up for a particular data factory, you can specify data factory **resourceUri** in hello **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="8637f-281">Merhaba aşağıdaki tabloda kullanılabilir işlemleri ve durumları (ve alt durumlar) hello listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8637f-281">hello following table provides hello list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="8637f-282">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="8637f-282">Operation name</span></span> | <span data-ttu-id="8637f-283">Durum</span><span class="sxs-lookup"><span data-stu-id="8637f-283">Status</span></span> | <span data-ttu-id="8637f-284">Alt durum</span><span class="sxs-lookup"><span data-stu-id="8637f-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8637f-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="8637f-285">RunStarted</span></span> |<span data-ttu-id="8637f-286">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="8637f-286">Started</span></span> |<span data-ttu-id="8637f-287">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="8637f-287">Starting</span></span> |
| <span data-ttu-id="8637f-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="8637f-288">RunFinished</span></span> |<span data-ttu-id="8637f-289">Başarısız / başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="8637f-289">Failed / Succeeded</span></span> |<span data-ttu-id="8637f-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="8637f-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="8637f-291">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="8637f-291">Succeeded</span></span><br/><br/><span data-ttu-id="8637f-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="8637f-292">FailedExecution</span></span><br/><br/><span data-ttu-id="8637f-293">Süresi sona erdi</span><span class="sxs-lookup"><span data-stu-id="8637f-293">TimedOut</span></span><br/><br/><span data-ttu-id="8637f-294">< iptal edildi</span><span class="sxs-lookup"><span data-stu-id="8637f-294"><Canceled</span></span><br/><br/><span data-ttu-id="8637f-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="8637f-295">FailedValidation</span></span><br/><br/><span data-ttu-id="8637f-296">terk</span><span class="sxs-lookup"><span data-stu-id="8637f-296">Abandoned</span></span> |
| <span data-ttu-id="8637f-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="8637f-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="8637f-298">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="8637f-298">Started</span></span> | |
| <span data-ttu-id="8637f-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="8637f-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="8637f-300">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="8637f-300">Succeeded</span></span> | |
| <span data-ttu-id="8637f-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="8637f-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="8637f-302">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="8637f-302">Succeeded</span></span> | |

<span data-ttu-id="8637f-303">Bkz: [uyarı kuralı oluştur](https://msdn.microsoft.com/library/azure/dn510366.aspx) hello örnekte kullanılan hello JSON öğeleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="8637f-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about hello JSON elements that are used in hello example.</span></span>

#### <a name="deploy-hello-alert"></a><span data-ttu-id="8637f-304">Merhaba uyarı dağıtma</span><span class="sxs-lookup"><span data-stu-id="8637f-304">Deploy hello alert</span></span>
<span data-ttu-id="8637f-305">toodeploy hello uyarı, hello Azure PowerShell cmdlet'ini kullanın **New-AzureRmResourceGroupDeployment**hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="8637f-305">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="8637f-306">Merhaba kaynak grubuna dağıtım başarıyla tamamladıktan sonra aşağıdaki iletileri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="8637f-306">After hello resource group deployment has finished successfully, you see hello following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> <span data-ttu-id="8637f-307">Merhaba kullanabilirsiniz [uyarı kuralı oluştur](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate bir uyarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="8637f-307">You can use hello [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate an alert rule.</span></span> <span data-ttu-id="8637f-308">Merhaba JSON yükü benzer toohello JSON örnektir.</span><span class="sxs-lookup"><span data-stu-id="8637f-308">hello JSON payload is similar toohello JSON example.</span></span>  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a><span data-ttu-id="8637f-309">Azure kaynak grubu dağıtımı Hello listesini alma</span><span class="sxs-lookup"><span data-stu-id="8637f-309">Retrieve hello list of Azure resource group deployments</span></span>
<span data-ttu-id="8637f-310">tooretrieve hello listesi dağıtılan Azure kaynak grubu dağıtımı, hello cmdlet'ini kullanın **Get-AzureRmResourceGroupDeployment**hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="8637f-310">tooretrieve hello list of deployed Azure resource group deployments, use hello cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="8637f-311">Kullanıcı olaylarına sorun giderme</span><span class="sxs-lookup"><span data-stu-id="8637f-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="8637f-312">Merhaba tıkladıktan sonra oluşturulan tüm hello olayları görebilirsiniz **ölçümleri ve işlemleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="8637f-312">You can see all hello events that are generated after clicking hello **Metrics and operations** tile.</span></span>

    ![Ölçümleri ve işlemleri bölmesi](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="8637f-314">Merhaba tıklatın **olayları** toosee hello olaylar bölmesi.</span><span class="sxs-lookup"><span data-stu-id="8637f-314">Click hello **Events** tile toosee hello events.</span></span>

    ![Olaylar bölmesi](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="8637f-316">Merhaba üzerinde **olayları** dikey penceresinde, olaylar, filtrelenmiş olayları ve benzeri ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-316">On hello **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Olaylar dikey penceresi](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="8637f-318">Tıklatın bir **işlemi** bir hataya neden olur hello işlemleri listesinde.</span><span class="sxs-lookup"><span data-stu-id="8637f-318">Click an **Operation** in hello operations list that causes an error.</span></span>

    ![Bir işlem seçin](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="8637f-320">Tıklatın bir **hata** olay toosee hello hata ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="8637f-320">Click an **Error** event toosee details about hello error.</span></span>

    ![Olay hatası](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="8637f-322">Bkz: [Azure Insight cmdlet'leri](https://msdn.microsoft.com/library/mt282452.aspx) tooadd kullanabilirsiniz, PowerShell cmdlet'leri almak veya uyarıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8637f-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use tooadd, get, or remove alerts.</span></span> <span data-ttu-id="8637f-323">Merhaba kullanmanın bazı örnekler şunlardır **Get-AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8637f-323">Here are a few examples of using hello **Get-AlertRule** cmdlet:</span></span>

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

<span data-ttu-id="8637f-324">Get-help komutları toosee ayrıntılarını ve örnekler hello Get-AlertRule cmdlet'i için aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8637f-324">Run hello following get-help commands toosee details and examples for hello Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="8637f-325">Merhaba uyarı oluşturma olayları görüyorsanız hello portal dikey penceresinde, ancak e-posta bildirimleri almadığınız, belirtilen hello e-posta adresi dış gönderenlerden tooreceive e-postaları ayarlanmış olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="8637f-325">If you see hello alert generation events on hello portal blade but you don't receive email notifications, check whether hello email address that is specified is set tooreceive emails from external senders.</span></span> <span data-ttu-id="8637f-326">Hello uyarı e-postalar, e-posta ayarlarınız tarafından engellenmiş.</span><span class="sxs-lookup"><span data-stu-id="8637f-326">hello alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="8637f-327">Ölçümleri uyarılar</span><span class="sxs-lookup"><span data-stu-id="8637f-327">Alerts on metrics</span></span>
<span data-ttu-id="8637f-328">Veri fabrikasında çeşitli ölçümleri yakalamak ve ölçümleri uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="8637f-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="8637f-329">İzleme ve uyarılar, veri fabrikası hello dilimleri ölçümlerini aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8637f-329">You can monitor and create alerts on hello following metrics for hello slices in your data factory:</span></span>

* <span data-ttu-id="8637f-330">**Başarısız çalıştırır**</span><span class="sxs-lookup"><span data-stu-id="8637f-330">**Failed Runs**</span></span>
* <span data-ttu-id="8637f-331">**Başarılı çalıştırır**</span><span class="sxs-lookup"><span data-stu-id="8637f-331">**Successful Runs**</span></span>

<span data-ttu-id="8637f-332">Bu ölçümler yararlıdır ve genel başarılı ve başarısız genel bir bakış hello veri fabrikasında çalıştıran tooget yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8637f-332">These metrics are useful and help you tooget an overview of overall failed and successful runs in hello data factory.</span></span> <span data-ttu-id="8637f-333">Olduğundan her zaman dilimi Çalıştır ölçümleri gösterilen.</span><span class="sxs-lookup"><span data-stu-id="8637f-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="8637f-334">Başında hello başlangıç saati, bu ölçümleri toplanır ve tooyour depolama hesabı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8637f-334">At hello beginning of hello hour, these metrics are aggregated and pushed tooyour storage account.</span></span> <span data-ttu-id="8637f-335">bir depolama hesabı ayarlamanız tooenable ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="8637f-335">tooenable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="8637f-336">Ölçümleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8637f-336">Enable metrics</span></span>
<span data-ttu-id="8637f-337">tooenable ölçümleri tıklatın hello hello aşağıdakini **Data Factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="8637f-337">tooenable metrics, click hello following from hello **Data Factory** blade:</span></span>

<span data-ttu-id="8637f-338">**İzleme** > **ölçüm** > **tanılama ayarlarını** > **tanılama**</span><span class="sxs-lookup"><span data-stu-id="8637f-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Tanılama bağlantı](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="8637f-340">Merhaba üzerinde **tanılama** dikey penceresinde tıklatın **üzerinde**hello depolama hesabını seçin ve'ı tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8637f-340">On hello **Diagnostics** blade, click **On**, select hello storage account, and click **Save**.</span></span>

![Tanılama dikey penceresi](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="8637f-342">Hello ölçümleri toobe hello üzerinde görünür tooone saattir yukarı sürebilir **izleme** dikey çünkü ölçümleri toplama saatlik olur.</span><span class="sxs-lookup"><span data-stu-id="8637f-342">It might take up tooone hour for hello metrics toobe visible on hello **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="8637f-343">Ölçümler hakkında bir uyarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="8637f-343">Set up an alert on metrics</span></span>
<span data-ttu-id="8637f-344">Merhaba tıklatın **Data Factory ölçümleri** döşeme:</span><span class="sxs-lookup"><span data-stu-id="8637f-344">Click hello **Data Factory metrics** tile:</span></span>

![Veri Fabrikası ölçümleri kutucuğu](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="8637f-346">Merhaba üzerinde **ölçüm** dikey penceresinde tıklatın **+ uyarı Ekle** hello araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="8637f-346">On hello **Metric** blade, click **+ Add alert** on hello toolbar.</span></span>
<span data-ttu-id="8637f-347">![Data factory ölçüm dikey penceresi > Uyarı Ekle](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="8637f-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="8637f-348">Merhaba üzerinde **uyarı kuralı eklemek** sayfasında, aşağıdaki adımları hello ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8637f-348">On hello **Add an alert rule** page, do hello following steps, and click **OK**.</span></span>

* <span data-ttu-id="8637f-349">Merhaba uyarı için bir ad girin (örnek: "uyarı başarısız oldu").</span><span class="sxs-lookup"><span data-stu-id="8637f-349">Enter a name for hello alert (example: "failed alert").</span></span>
* <span data-ttu-id="8637f-350">Merhaba uyarı için bir açıklama girin (örnek: "bir hata oluştuğunda bir e-posta Gönder").</span><span class="sxs-lookup"><span data-stu-id="8637f-350">Enter a description for hello alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="8637f-351">Bir ("Çalıştığında başarısız oldu" vs. ölçümünü seçin "Başarılı çalışır").</span><span class="sxs-lookup"><span data-stu-id="8637f-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="8637f-352">Bir koşul ve bir eşik değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8637f-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="8637f-353">Merhaba süreyi belirtin.</span><span class="sxs-lookup"><span data-stu-id="8637f-353">Specify hello period of time.</span></span>
* <span data-ttu-id="8637f-354">Bir e-posta tooowners, Katkıda Bulunanlar ve okuyucular gönderilmesi gerekip gerekmediğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8637f-354">Specify whether an email should be sent tooowners, contributors, and readers.</span></span>

![Data factory ölçüm dikey penceresi > Uyarı kuralı Ekle](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="8637f-356">Sonra Hello uyarı kuralı başarıyla eklendi, hello dikey penceresi kapanır ve üzerinde hello hello yeni uyarı gördüğünüz **ölçüm** dikey.</span><span class="sxs-lookup"><span data-stu-id="8637f-356">After hello alert rule is added successfully, hello blade closes and you see hello new alert on hello **Metric** blade.</span></span>

![Data factory ölçüm dikey penceresi > eklenen yeni uyarı](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="8637f-358">Merhaba uyarılar hello sayısı görmeniz gerekir **uyarı kuralları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="8637f-358">You should also see hello number of alerts in hello **Alert rules** tile.</span></span> <span data-ttu-id="8637f-359">Merhaba tıklatın **uyarı kuralları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="8637f-359">Click hello **Alert rules** tile.</span></span>

![Data factory ölçüm dikey penceresi - uyarı kuralları](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="8637f-361">Merhaba üzerinde **uyarı kuralları** dikey penceresinde, var olan tüm uyarıları görebilir.</span><span class="sxs-lookup"><span data-stu-id="8637f-361">On hello **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="8637f-362">bir uyarı, tooadd tıklatın **uyarı Ekle** hello araç.</span><span class="sxs-lookup"><span data-stu-id="8637f-362">tooadd an alert, click **Add alert** on hello toolbar.</span></span>

![Uyarı kuralları dikey penceresi](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="8637f-364">Uyarı bildirimleri</span><span class="sxs-lookup"><span data-stu-id="8637f-364">Alert notifications</span></span>
<span data-ttu-id="8637f-365">Merhaba uyarı kuralı hello koşulu ile eşleşen sonra hello uyarı etkinleştirildikten bildiren bir e-posta almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8637f-365">After hello alert rule matches hello condition, you should get an email that says hello alert is activated.</span></span> <span data-ttu-id="8637f-366">Merhaba sorun çözüldüğünde ve hello Uyarı koşulu artık eşleşmiyor sonra hello uyarı çözümlendiğinde bildiren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="8637f-366">After hello issue is resolved and hello alert condition doesn’t match anymore, you get an email that says hello alert is resolved.</span></span>

<span data-ttu-id="8637f-367">Bu davranış için bir uyarı kuralı niteleyen her hatasında bir bildirim burada gönderilen olaylar farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8637f-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="8637f-368">PowerShell kullanarak uyarıları dağıtma</span><span class="sxs-lookup"><span data-stu-id="8637f-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="8637f-369">Ölçümleri aynı hello için uyarıları dağıtabilirsiniz olaylar için bunu yolu.</span><span class="sxs-lookup"><span data-stu-id="8637f-369">You can deploy alerts for metrics hello same way that you do for events.</span></span>

<span data-ttu-id="8637f-370">**Uyarı tanımı**</span><span class="sxs-lookup"><span data-stu-id="8637f-370">**Alert definition**</span></span>

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

<span data-ttu-id="8637f-371">Değiştir *Subscriptionıd*, *resourceGroupName*, ve *dataFactoryName* uygun değerlerle hello örnekteki.</span><span class="sxs-lookup"><span data-stu-id="8637f-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in hello sample with appropriate values.</span></span>

<span data-ttu-id="8637f-372">*metricName* şu anda iki değer destekler:</span><span class="sxs-lookup"><span data-stu-id="8637f-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="8637f-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="8637f-373">FailedRuns</span></span>
* <span data-ttu-id="8637f-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="8637f-374">SuccessfulRuns</span></span>

<span data-ttu-id="8637f-375">**Merhaba uyarı dağıtma**</span><span class="sxs-lookup"><span data-stu-id="8637f-375">**Deploy hello alert**</span></span>

<span data-ttu-id="8637f-376">toodeploy hello uyarı, hello Azure PowerShell cmdlet'ini kullanın **New-AzureRmResourceGroupDeployment**hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="8637f-376">toodeploy hello alert, use hello Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in hello following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="8637f-377">Başarılı dağıtım sonrasında iletiden görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8637f-377">You should see following message after a successful deployment:</span></span>

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

<span data-ttu-id="8637f-378">Merhaba de kullanabilirsiniz **Ekle AlertRule** cmdlet toodeploy bir uyarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="8637f-378">You can also use hello **Add-AlertRule** cmdlet toodeploy an alert rule.</span></span> <span data-ttu-id="8637f-379">Merhaba bkz [Ekle AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) ayrıntı ve örnekler için konu.</span><span class="sxs-lookup"><span data-stu-id="8637f-379">See hello [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a><span data-ttu-id="8637f-380">Bir veri fabrikası tooa farklı bir kaynak grubuna veya aboneliğe taşıma</span><span class="sxs-lookup"><span data-stu-id="8637f-380">Move a data factory tooa different resource group or subscription</span></span>
<span data-ttu-id="8637f-381">Veri Fabrikası tooa farklı bir kaynak grubunda veya farklı bir abonelik hello kullanarak taşıyabilirsiniz **taşıma** hello giriş sayfasında veri fabrikanızın düğmesini çubuğu komutu.</span><span class="sxs-lookup"><span data-stu-id="8637f-381">You can move a data factory tooa different resource group or a different subscription by using hello **Move** command bar button on hello home page of your data factory.</span></span>

![Veri Fabrikası taşıma](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="8637f-383">Bu gibi durumlarda, ilgili kaynakları (örneğin, hello data factory ile ilişkili olan uyarılar), ayrıca hello veri fabrikası birlikte taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8637f-383">You can also move any related resources (such as alerts that are associated with hello data factory), along with hello data factory.</span></span>

![Taşıma kaynaklar iletişim kutusu](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
