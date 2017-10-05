---
title: "İzleme ve ardışık düzen Azure portal ve PowerShell kullanarak yönetme | Microsoft Docs"
description: "Azure data factory'leri ve oluşturduğunuz ardışık düzen yönetmek ve izlemek için Azure portalı ve Azure PowerShell kullanmayı öğrenin."
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
ms.openlocfilehash: 61bb5379cd94dd00814e14420947e7783999ff0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-azure-portal-and-powershell"></a><span data-ttu-id="3aea5-103">İzleme ve Azure portalı ve PowerShell kullanarak Azure Data Factory işlem hatlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="3aea5-103">Monitor and manage Azure Data Factory pipelines by using the Azure portal and PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3aea5-104">Azure portal/Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="3aea5-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="3aea5-105">Kullanılarak izleme ve yönetim uygulaması</span><span class="sxs-lookup"><span data-stu-id="3aea5-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> <span data-ttu-id="3aea5-106">İzleme ve yönetim uygulama izleme ve veri işlem hatlarınızı yönetmek ve sorunları gidermek için daha iyi destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-106">The monitoring & management application provides a better support for monitoring and managing your data pipelines, and troubleshooting any issues.</span></span> <span data-ttu-id="3aea5-107">Uygulamayı kullanma hakkında daha fazla bilgi için bkz: [izlemek ve Data Factory işlem hatlarını izleme ve yönetim uygulaması kullanarak yönetmek](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="3aea5-107">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 


<span data-ttu-id="3aea5-108">Bu makalede, izleme, yönetme ve işlem hatlarınızı Azure portalı ve PowerShell kullanarak hata ayıklama açıklar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-108">This article describes how to monitor, manage, and debug your pipelines by using Azure portal and PowerShell.</span></span> <span data-ttu-id="3aea5-109">Makaleyi uyarıları oluşturma ve hatalar hakkında bilgi edinin bilgiler de sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-109">The article also provides information on how to create alerts and get notified about failures.</span></span>

## <a name="understand-pipelines-and-activity-states"></a><span data-ttu-id="3aea5-110">Ardışık Düzen ve etkinlik durumlarını anlama</span><span class="sxs-lookup"><span data-stu-id="3aea5-110">Understand pipelines and activity states</span></span>
<span data-ttu-id="3aea5-111">Azure Portalı'nı kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3aea5-111">By using the Azure portal, you can:</span></span>

* <span data-ttu-id="3aea5-112">Veri fabrikanızın diyagramı olarak görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-112">View your data factory as a diagram.</span></span>
* <span data-ttu-id="3aea5-113">Bir ardışık düzendeki etkinlik görünümü.</span><span class="sxs-lookup"><span data-stu-id="3aea5-113">View activities in a pipeline.</span></span>
* <span data-ttu-id="3aea5-114">Giriş ve çıkış veri kümeleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-114">View input and output datasets.</span></span>

<span data-ttu-id="3aea5-115">Bu bölümde, nasıl bir veri kümesi dilim başka bir duruma bir durumdan diğerine geçer de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-115">This section also describes how a dataset slice transitions from one state to another state.</span></span>   

### <a name="navigate-to-your-data-factory"></a><span data-ttu-id="3aea5-116">Veri fabrikanızın gidin</span><span class="sxs-lookup"><span data-stu-id="3aea5-116">Navigate to your data factory</span></span>
1. <span data-ttu-id="3aea5-117">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3aea5-118">Tıklatın **veri fabrikaları** soldaki menüde.</span><span class="sxs-lookup"><span data-stu-id="3aea5-118">Click **Data factories** on the menu on the left.</span></span> <span data-ttu-id="3aea5-119">Göremiyorsanız, tıklatın **daha fazla hizmet >**ve ardından **veri fabrikaları** altında **INTELLİGENCE + ANALİZ** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-119">If you don't see it, click **More services >**, and then click **Data factories** under the **INTELLIGENCE + ANALYTICS** category.</span></span>

   ![Tümüne Gözat > veri fabrikaları](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. <span data-ttu-id="3aea5-121">Üzerinde **veri fabrikaları** dikey penceresinde, ilgilendiğiniz data factory seçin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-121">On the **Data factories** blade, select the data factory that you're interested in.</span></span>

    ![Veri Fabrikası seçin](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   <span data-ttu-id="3aea5-123">Data factory giriş sayfasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-123">You should see the home page for the data factory.</span></span>

   ![Data factory dikey penceresi](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a><span data-ttu-id="3aea5-125">Veri fabrikanızın diyagram görünümü</span><span class="sxs-lookup"><span data-stu-id="3aea5-125">Diagram view of your data factory</span></span>
<span data-ttu-id="3aea5-126">**Diyagramı** data factory görünümünü bölmeden data factory ve varlıklarını yönetmek ve izlemek için cam sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-126">The **Diagram** view of a data factory provides a single pane of glass to monitor and manage the data factory and its assets.</span></span> <span data-ttu-id="3aea5-127">Görmek için **diyagramı** 'ı tıklatın, görüntüleyin, veri fabrikası **diyagramı** data factory giriş sayfasında.</span><span class="sxs-lookup"><span data-stu-id="3aea5-127">To see the **Diagram** view of your data factory, click **Diagram** on the home page for the data factory.</span></span>

![Diyagram görünümü](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

<span data-ttu-id="3aea5-129">Yakınlaştırma, yakınlaştırabilir, sığacak, % 100 Yaklaştır, diyagramın düzenini kilitlemek ve ardışık düzen ve veri kümeleri otomatik Konumlandır yakınlaştırma.</span><span class="sxs-lookup"><span data-stu-id="3aea5-129">You can zoom in, zoom out, zoom to fit, zoom to 100%, lock the layout of the diagram, and automatically position pipelines and datasets.</span></span> <span data-ttu-id="3aea5-130">Veri çizgileri bilgileri de görebilirsiniz (diğer bir deyişle, seçilen öğelerin Yukarı Akış ve aşağı akış öğelerini göster).</span><span class="sxs-lookup"><span data-stu-id="3aea5-130">You can also see the data lineage information (that is, show upstream and downstream items of selected items).</span></span>

### <a name="activities-inside-a-pipeline"></a><span data-ttu-id="3aea5-131">Bir işlem hattı içindeki etkinlikler</span><span class="sxs-lookup"><span data-stu-id="3aea5-131">Activities inside a pipeline</span></span>
1. <span data-ttu-id="3aea5-132">Ardışık Düzen sağ tıklayın ve ardından **açık işlem hattı** ardışık etkinlikler için girdi ve çıktı veri kümeleri ile birlikte tüm etkinliklerin görmek için.</span><span class="sxs-lookup"><span data-stu-id="3aea5-132">Right-click the pipeline, and then click **Open pipeline** to see all activities in the pipeline, along with input and output datasets for the activities.</span></span> <span data-ttu-id="3aea5-133">Bu özellik, hattınızı birden fazla etkinlik içerir ve tek bir ardışık işletimsel çizgileri anlamak istediğinizde yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="3aea5-133">This feature is useful when your pipeline includes more than one activity and you want to understand the operational lineage of a single pipeline.</span></span>

    ![İşlem hattı menüsünü açma](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. <span data-ttu-id="3aea5-135">Aşağıdaki örnekte, bir kopyalama etkinliği bir girdi ve çıktı düzenindeki bakın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-135">In the following example, you see a copy activity in the pipeline with an input and an output.</span></span> 

    ![Bir işlem hattı içindeki etkinlikler](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. <span data-ttu-id="3aea5-137">Giriş sayfasına geri data Factory tıklayarak gidebilirsiniz **veri fabrikası** sol üst köşesinde içerik haritası bağlantıyı.</span><span class="sxs-lookup"><span data-stu-id="3aea5-137">You can navigate back to the home page of the data factory by clicking the **Data factory** link in the breadcrumb at the top-left corner.</span></span>

    ![Veri Fabrikası için geri gidin](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-the-state-of-each-activity-inside-a-pipeline"></a><span data-ttu-id="3aea5-139">Bir işlem hattı içindeki her etkinlik durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="3aea5-139">View the state of each activity inside a pipeline</span></span>
<span data-ttu-id="3aea5-140">Herhangi bir etkinlik tarafından üretilen veri kümeleri durumunu görüntüleyerek bir etkinlik geçerli durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-140">You can view the current state of an activity by viewing the status of any of the datasets that are produced by the activity.</span></span>

<span data-ttu-id="3aea5-141">Çift tıklatarak **OutputBlobTable** içinde **diyagramı**, farklı etkinlik çalışması içinde bir ardışık düzen tarafından üretilen tüm dilimleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-141">By double-clicking the **OutputBlobTable** in the **Diagram**, you can see all the slices that are produced by different activity runs inside a pipeline.</span></span> <span data-ttu-id="3aea5-142">Kopya etkinliği için başarıyla son sekiz saat çalıştırılmış ve dilimlerinin görebilirsiniz **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-142">You can see that the copy activity ran successfully for the last eight hours and produced the slices in the **Ready** state.</span></span>  

![Ardışık Düzen durumu](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

<span data-ttu-id="3aea5-144">Data factory veri kümesi dilimleri aşağıdaki durumlardan biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="3aea5-144">The dataset slices in the data factory can have one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="3aea5-145">Durum</span><span class="sxs-lookup"><span data-stu-id="3aea5-145">State</span></span></th><th align="left"><span data-ttu-id="3aea5-146">Bölgesine</span><span class="sxs-lookup"><span data-stu-id="3aea5-146">Substate</span></span></th><th align="left"><span data-ttu-id="3aea5-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3aea5-147">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="3aea5-148">Bekleniyor</span><span class="sxs-lookup"><span data-stu-id="3aea5-148">Waiting</span></span></td><td><span data-ttu-id="3aea5-149">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="3aea5-149">ScheduleTime</span></span></td><td><span data-ttu-id="3aea5-150">Saat dilimi çalıştırmak gelen kurmadı.</span><span class="sxs-lookup"><span data-stu-id="3aea5-150">The time hasn't come for the slice to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-151">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="3aea5-151">DatasetDependencies</span></span></td><td><span data-ttu-id="3aea5-152">Yukarı Akış bağımlılıkları hazır değil.</span><span class="sxs-lookup"><span data-stu-id="3aea5-152">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-153">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="3aea5-153">ComputeResources</span></span></td><td><span data-ttu-id="3aea5-154">İşlem kaynakları kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="3aea5-154">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-155">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="3aea5-155">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="3aea5-156">Diğer tüm etkinlik örnekleri diğer dilimleri çalıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="3aea5-156">All the activity instances are busy running other slices.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-157">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="3aea5-157">ActivityResume</span></span></td><td><span data-ttu-id="3aea5-158">Etkinlik duraklatıldı ve etkinlik sürdürülene kadar dilimler çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-158">The activity is paused and can't run the slices until the activity is resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-159">Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="3aea5-159">Retry</span></span></td><td><span data-ttu-id="3aea5-160">Etkinlik yürütme yeniden deneniyor.</span><span class="sxs-lookup"><span data-stu-id="3aea5-160">Activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-161">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="3aea5-161">Validation</span></span></td><td><span data-ttu-id="3aea5-162">Doğrulama henüz başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="3aea5-162">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-163">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="3aea5-163">ValidationRetry</span></span></td><td><span data-ttu-id="3aea5-164">Doğrulama işleminin yeniden gerçekleştirilmesi bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="3aea5-164">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="3aea5-165">Devam ediyor</span><span class="sxs-lookup"><span data-stu-id="3aea5-165">InProgress</span></span></td><td><span data-ttu-id="3aea5-166">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="3aea5-166">Validating</span></span></td><td><span data-ttu-id="3aea5-167">Doğrulama devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="3aea5-167">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="3aea5-168">Dilim işleniyor.</span><span class="sxs-lookup"><span data-stu-id="3aea5-168">The slice is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="3aea5-169">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="3aea5-169">Failed</span></span></td><td><span data-ttu-id="3aea5-170">Süresi sona erdi</span><span class="sxs-lookup"><span data-stu-id="3aea5-170">TimedOut</span></span></td><td><span data-ttu-id="3aea5-171">Etkinlik yürütme etkinlik tarafından izin daha uzun sürdü.</span><span class="sxs-lookup"><span data-stu-id="3aea5-171">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-172">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="3aea5-172">Canceled</span></span></td><td><span data-ttu-id="3aea5-173">Dilim kullanıcı eylemi tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-173">The slice was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-174">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="3aea5-174">Validation</span></span></td><td><span data-ttu-id="3aea5-175">Doğrulama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-175">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="3aea5-176">Dilim oluşturulan doğrulandı ve/veya başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-176">The slice failed to be generated and/or validated.</span></span></td>
</tr>
<td><span data-ttu-id="3aea5-177">Hazır</span><span class="sxs-lookup"><span data-stu-id="3aea5-177">Ready</span></span></td><td>-</td><td><span data-ttu-id="3aea5-178">Dilim kullanıma hazır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-178">The slice is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-179">Atlandı</span><span class="sxs-lookup"><span data-stu-id="3aea5-179">Skipped</span></span></td><td><span data-ttu-id="3aea5-180">None</span><span class="sxs-lookup"><span data-stu-id="3aea5-180">None</span></span></td><td><span data-ttu-id="3aea5-181">Dilimin işlenmekte olan değil.</span><span class="sxs-lookup"><span data-stu-id="3aea5-181">The slice isn't being processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3aea5-182">None</span><span class="sxs-lookup"><span data-stu-id="3aea5-182">None</span></span></td><td>-</td><td><span data-ttu-id="3aea5-183">Bir dilim farklı bir durum ile var olmuş ancak sıfırlandı.</span><span class="sxs-lookup"><span data-stu-id="3aea5-183">A slice used to exist with a different status, but it has been reset.</span></span></td>
</tr>
</table>



<span data-ttu-id="3aea5-184">Bir dilim girişi tıklayarak bir dilim ilgili ayrıntıları görüntüleyebilirsiniz **en son güncelleştirilen dilimler** dikey.</span><span class="sxs-lookup"><span data-stu-id="3aea5-184">You can view the details about a slice by clicking a slice entry on the **Recently Updated Slices** blade.</span></span>

![Dilim ayrıntıları](./media/data-factory-monitor-manage-pipelines/slice-details.png)

<span data-ttu-id="3aea5-186">Dilim birden çok kez yürütülmüşse, birden çok satır bkz **etkinlik çalışır** listesi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-186">If the slice has been executed multiple times, you see multiple rows in the **Activity runs** list.</span></span> <span data-ttu-id="3aea5-187">Çalışma girişi tıklayarak Çalıştır etkinliği hakkında ayrıntılı bilgi görüntüleyebileceğiniz **etkinlik çalışır** listesi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-187">You can view details about an activity run by clicking the run entry in the **Activity runs** list.</span></span> <span data-ttu-id="3aea5-188">Liste varsa bir hata iletisi ile birlikte tüm günlük dosyalarını, gösterir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-188">The list shows all the log files, along with an error message if there is one.</span></span> <span data-ttu-id="3aea5-189">Bu özellik görüntülemek ve günlükleri, veri fabrikası ayrılmak zorunda kalmadan hata ayıklama yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="3aea5-189">This feature is useful to view and debug logs without having to leave your data factory.</span></span>

![Etkinlik çalışma ayrıntıları](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

<span data-ttu-id="3aea5-191">Dilim eklenti yoksa **hazır** durumu, hazır değil ve geçerli dilimin yürütülmesini engelleyen Yukarı Akış dilimleri görebilirsiniz **hazır olmayan Yukarı Akış dilimleri** listesi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-191">If the slice isn't in the **Ready** state, you can see the upstream slices that aren't ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span> <span data-ttu-id="3aea5-192">Bu özellik, dilim olduğunda yararlıdır **bekleyen** durumu ve dilim bekleyen Yukarı Akış bağımlılıkları anlamak istediğinizde.</span><span class="sxs-lookup"><span data-stu-id="3aea5-192">This feature is useful when your slice is in **Waiting** state and you want to understand the upstream dependencies that the slice is waiting on.</span></span>

![Hazır olmayan yukarı akış dilimleri](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a><span data-ttu-id="3aea5-194">Veri kümesi durumu diyagramı</span><span class="sxs-lookup"><span data-stu-id="3aea5-194">Dataset state diagram</span></span>
<span data-ttu-id="3aea5-195">Veri Fabrikası dağıtmak ve ardışık düzen geçerli bir etkin döneme sahip sonra dataset geçiş bir durumdan diğerine dilimler.</span><span class="sxs-lookup"><span data-stu-id="3aea5-195">After you deploy a data factory and the pipelines have a valid active period, the dataset slices transition from one state to another.</span></span> <span data-ttu-id="3aea5-196">Şu anda, dilim durumu aşağıdaki durumu diyagramı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="3aea5-196">Currently, the slice status follows the following state diagram:</span></span>

![Durum Diyagramı](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

<span data-ttu-id="3aea5-198">Veri fabrikasında veri kümesi durumu geçişi akışı aşağıdaki gibidir: bekleme içinde-ilerleme/Sürüyor (doğrulama) -> hazır/başarısız->.</span><span class="sxs-lookup"><span data-stu-id="3aea5-198">The dataset state transition flow in data factory is the following: Waiting -> In-Progress/In-Progress (Validating) -> Ready/Failed.</span></span>

<span data-ttu-id="3aea5-199">Dilim başlayacağını bir **bekleyen** yürütülmeden önce karşılanması gereken önkoşulları bekleme durumu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-199">The slice starts in a **Waiting** state, waiting for preconditions to be met before it executes.</span></span> <span data-ttu-id="3aea5-200">Ardından, yürütme etkinliği başlar ve dilim girmeyeceğini bir **sürüyor** durumu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-200">Then, the activity starts executing, and the slice goes into an **In-Progress** state.</span></span> <span data-ttu-id="3aea5-201">Etkinlik yürütme başarılı veya başarısız.</span><span class="sxs-lookup"><span data-stu-id="3aea5-201">The activity execution might succeed or fail.</span></span> <span data-ttu-id="3aea5-202">Dilim olarak işaretlenmiş **hazır** veya **başarısız**bağlı olarak yürütmenin sonucu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-202">The slice is marked as **Ready** or **Failed**, based on the result of the execution.</span></span>

<span data-ttu-id="3aea5-203">Gelen geri dönmek için dilim sıfırlayabilirsiniz **hazır** veya **başarısız** durumunu **bekleyen** durumu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-203">You can reset the slice to go back from the **Ready** or **Failed** state to the **Waiting** state.</span></span> <span data-ttu-id="3aea5-204">Dilim durumuna da işaretleyebilirsiniz **atla**, yürütme ve dilim işlenmiyor etkinlik engeller.</span><span class="sxs-lookup"><span data-stu-id="3aea5-204">You can also mark the slice state to **Skip**, which prevents the activity from executing and not processing the slice.</span></span>

## <a name="pause-and-resume-pipelines"></a><span data-ttu-id="3aea5-205">Ardışık Düzen Durdur</span><span class="sxs-lookup"><span data-stu-id="3aea5-205">Pause and resume pipelines</span></span>
<span data-ttu-id="3aea5-206">Azure PowerShell kullanarak işlem hatlarınızı yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-206">You can manage your pipelines by using Azure PowerShell.</span></span> <span data-ttu-id="3aea5-207">Örneğin, duraklatma ve ardışık düzen Azure PowerShell cmdlet'lerini çalıştırarak sürdürme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-207">For example, you can pause and resume pipelines by running Azure PowerShell cmdlets.</span></span> 

> [!NOTE] 
> <span data-ttu-id="3aea5-208">Diyagram görünümü, duraklatma ve sürdürme ardışık düzen desteklemez.</span><span class="sxs-lookup"><span data-stu-id="3aea5-208">The diagram view does not support pausing and resuming pipelines.</span></span> <span data-ttu-id="3aea5-209">Bir kullanıcı arabirimi kullanmak istiyorsanız, izleme ve yönetme uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-209">If you want to use an user interface, use the monitoring and managing application.</span></span> <span data-ttu-id="3aea5-210">Uygulamayı kullanma hakkında daha fazla bilgi için bkz: [izlemek ve Data Factory işlem hatlarını izleme ve yönetim uygulaması kullanarak yönetmek](data-factory-monitor-manage-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-210">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

<span data-ttu-id="3aea5-211">Duraklat/işlem hatları kullanarak askıya alabilirsiniz **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3aea5-211">You can pause/suspend pipelines by using the **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet.</span></span> <span data-ttu-id="3aea5-212">Bu cmdlet, bir sorun düzeltilene kadar hatlarınızı çalıştırmak istemediğiniz yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-212">This cmdlet is useful when you don’t want to run your pipelines until an issue is fixed.</span></span> 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="3aea5-213">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3aea5-213">For example:</span></span>

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

<span data-ttu-id="3aea5-214">Ardışık düzene sorun çözüldükten sonra aşağıdaki PowerShell komutunu çalıştırarak askıya alınmış ardışık düzen devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3aea5-214">After the issue has been fixed with the pipeline, you can resume the suspended pipeline by running the following PowerShell command:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
<span data-ttu-id="3aea5-215">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3aea5-215">For example:</span></span>

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a><span data-ttu-id="3aea5-216">Ardışık Düzen hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="3aea5-216">Debug pipelines</span></span>
<span data-ttu-id="3aea5-217">Azure Data Factory hata ayıklama ve ardışık düzen Azure portalı ve Azure PowerShell kullanarak sorun giderme için zengin özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-217">Azure Data Factory provides rich capabilities for you to debug and troubleshoot pipelines by using the Azure portal and Azure PowerShell.</span></span>

> <span data-ttu-id="3aea5-218">[! Not} izleme ve yönetim uygulaması kullanarak troubleshot hataları daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-218">[!NOTE} It is much easier to troubleshot errors using the Monitoring & Management App.</span></span> <span data-ttu-id="3aea5-219">Uygulamayı kullanma hakkında daha fazla bilgi için bkz: [izlemek ve Data Factory işlem hatlarını izleme ve yönetim uygulaması kullanarak yönetmek](data-factory-monitor-manage-app.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3aea5-219">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md) article.</span></span> 

### <a name="find-errors-in-a-pipeline"></a><span data-ttu-id="3aea5-220">Ardışık düzeninde hataları bulma</span><span class="sxs-lookup"><span data-stu-id="3aea5-220">Find errors in a pipeline</span></span>
<span data-ttu-id="3aea5-221">Ardışık düzeninde etkinlik çalıştırma başarısız olursa, ardışık düzen tarafından üretilen veri kümesi bir hata nedeniyle başarısız durumda.</span><span class="sxs-lookup"><span data-stu-id="3aea5-221">If the activity run fails in a pipeline, the dataset that is produced by the pipeline is in an error state because of the failure.</span></span> <span data-ttu-id="3aea5-222">Hata ayıklama ve aşağıdaki yöntemleri kullanarak Azure Data factory'de hatalarında sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-222">You can debug and troubleshoot errors in Azure Data Factory by using the following methods.</span></span>

#### <a name="use-the-azure-portal-to-debug-an-error"></a><span data-ttu-id="3aea5-223">Bir hata ayıklama için Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="3aea5-223">Use the Azure portal to debug an error</span></span>
1. <span data-ttu-id="3aea5-224">Üzerinde **tablo** dikey penceresinde sahip sorun dilimi tıklatın **durum** kümesine **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="3aea5-224">On the **Table** blade, click the problem slice that has the **Status** set to **Failed**.</span></span>

   ![Sorun dilim ile tablo dikey penceresi](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. <span data-ttu-id="3aea5-226">Üzerinde **veri dilimi** dikey penceresinde, etkinlik başarısız Çalıştır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-226">On the **Data slice** blade, click the activity run that failed.</span></span>

   ![Veri dilimi bir hata ile](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. <span data-ttu-id="3aea5-228">Üzerinde **etkinlik çalışma ayrıntıları** dikey penceresinde, Hdınsight işleme ile ilişkili olan dosyaları karşıdan yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-228">On the **Activity run details** blade, you can download the files that are associated with the HDInsight processing.</span></span> <span data-ttu-id="3aea5-229">Tıklatın **karşıdan** hata hakkında ayrıntılar içeren hata günlüğü dosyası karşıdan yüklemek durum/stderr için.</span><span class="sxs-lookup"><span data-stu-id="3aea5-229">Click **Download** for Status/stderr to download the error log file that contains details about the error.</span></span>

   ![Etkinlik ayrıntıları dikey penceresinde hatası ile çalıştırma](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-to-debug-an-error"></a><span data-ttu-id="3aea5-231">Bir hata ayıklama için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="3aea5-231">Use PowerShell to debug an error</span></span>
1. <span data-ttu-id="3aea5-232">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-232">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="3aea5-233">Çalıştırma **Get-AzureRmDataFactorySlice** dilimler ve bunların durumlarını görmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-233">Run the **Get-AzureRmDataFactorySlice** command to see the slices and their statuses.</span></span> <span data-ttu-id="3aea5-234">Durumundaki bir dilim görmeniz gerekir **başarısız**.</span><span class="sxs-lookup"><span data-stu-id="3aea5-234">You should see a slice with the status of **Failed**.</span></span>        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   <span data-ttu-id="3aea5-235">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3aea5-235">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   <span data-ttu-id="3aea5-236">Değiştir **StartDateTime** hattınızı başlangıç saati ile.</span><span class="sxs-lookup"><span data-stu-id="3aea5-236">Replace **StartDateTime** with start time of your pipeline.</span></span> 
3. <span data-ttu-id="3aea5-237">Şimdi Çalıştır **Get-AzureRmDataFactoryRun** etkinliği hakkında ayrıntılı bilgi almak için cmdlet'i çalıştırmak için dilim.</span><span class="sxs-lookup"><span data-stu-id="3aea5-237">Now, run the **Get-AzureRmDataFactoryRun** cmdlet to get details about the activity run for the slice.</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    <span data-ttu-id="3aea5-238">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3aea5-238">For example:</span></span>

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    <span data-ttu-id="3aea5-239">StartDateTime, önceki adımda not ettiğiniz hata/sorun dilim için başlangıç zamanı değeridir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-239">The value of StartDateTime is the start time for the error/problem slice that you noted from the previous step.</span></span> <span data-ttu-id="3aea5-240">Tarih-saat çift tırnak içine alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-240">The date-time should be enclosed in double quotes.</span></span>
4. <span data-ttu-id="3aea5-241">Çıktı aşağıdakine benzer hata ayrıntılarıyla birlikte görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3aea5-241">You should see output with details about the error that is similar to the following:</span></span>

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
5. <span data-ttu-id="3aea5-242">Çalıştırabilirsiniz **Kaydet AzureRmDataFactoryLog** çıkışı görmek ve günlük dosyalarını kullanarak indirmek kimliği değeri cmdlet'iyle **- DownloadLogsoption** cmdlet'i için.</span><span class="sxs-lookup"><span data-stu-id="3aea5-242">You can run the **Save-AzureRmDataFactoryLog** cmdlet with the Id value that you see from the output, and download the log files by using the **-DownloadLogsoption** for the cmdlet.</span></span>

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a><span data-ttu-id="3aea5-243">Ardışık düzeninde hataları yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3aea5-243">Rerun failures in a pipeline</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3aea5-244">Hataları gidermek ve başarısız dilimler izleme ve yönetim uygulaması kullanarak yeniden kolaydır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-244">It's easier to troubleshoot errors and rerun failed slices by using the Monitoring & Management App.</span></span> <span data-ttu-id="3aea5-245">Uygulamayı kullanma hakkında daha fazla bilgi için bkz: [izlemek ve Data Factory işlem hatlarını izleme ve yönetim uygulaması kullanarak yönetmek](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="3aea5-245">For details about using the application, see [monitor and manage Data Factory pipelines by using the Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span> 

### <a name="use-the-azure-portal"></a><span data-ttu-id="3aea5-246">Azure portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="3aea5-246">Use the Azure portal</span></span>
<span data-ttu-id="3aea5-247">Sorun giderme ve hata ayıklama hataları ardışık düzeninde sonra hata dilim gezinme ve tıklayarak hataları çalıştırabilirsiniz **çalıştırmak** komut çubuğundan düğme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-247">After you troubleshoot and debug failures in a pipeline, you can rerun failures by navigating to the error slice and clicking the **Run** button on the command bar.</span></span>

![Başarısız bir dilimi yeniden çalıştırın](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

<span data-ttu-id="3aea5-249">(Örneğin, veri kullanılamıyorsa) durumda dilim doğrulama bir ilke hatası nedeniyle başarısız oldu, hata düzeltme ve tıklayarak doğrulamak **doğrulama** komut çubuğundan düğme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-249">In case the slice has failed validation because of a policy failure (for example, if data isn't available), you can fix the failure and validate again by clicking the **Validate** button on the command bar.</span></span>

![Hataları giderin ve doğrulama](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a><span data-ttu-id="3aea5-251">Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="3aea5-251">Use Azure PowerShell</span></span>
<span data-ttu-id="3aea5-252">Kullanarak hataları çalıştırabilirsiniz **Set-AzureRmDataFactorySliceStatus** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="3aea5-252">You can rerun failures by using the **Set-AzureRmDataFactorySliceStatus** cmdlet.</span></span> <span data-ttu-id="3aea5-253">Bkz: [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) sözdizimi ve cmdlet ile ilgili diğer ayrıntıları için konu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-253">See the [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) topic for syntax and other details about the cmdlet.</span></span>

<span data-ttu-id="3aea5-254">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3aea5-254">**Example:**</span></span>

<span data-ttu-id="3aea5-255">Aşağıdaki örnek tablosunun tüm dilimleri durumunu 'DAWikiAggregatedData' 'Azure veri fabrikası 'WikiADF' bekleyen' ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-255">The following example sets the status of all slices for the table 'DAWikiAggregatedData' to 'Waiting' in the Azure data factory 'WikiADF'.</span></span>

<span data-ttu-id="3aea5-256">'Güncelleştirme 'türü 'tablosu için her dilimi ve tüm bağımlı (Yukarı Akış) tabloları durumları 'Bekleyen' ayarlandığından anlamı Upstreamınpipeline için', ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-256">The 'UpdateType' is set to 'UpstreamInPipeline', which means that statuses of each slice for the table and all the dependent (upstream) tables are set to 'Waiting'.</span></span> <span data-ttu-id="3aea5-257">Bu parametre için diğer olası değer 'Bireysel' dir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-257">The other possible value for this parameter is 'Individual'.</span></span>

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a><span data-ttu-id="3aea5-258">Uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3aea5-258">Create alerts</span></span>
<span data-ttu-id="3aea5-259">Azure günlükleri kullanıcı olayları bir Azure kaynak olduğunda (örneğin, veri fabrikası) oluşturulan, güncelleştirilmiş veya silinmiş.</span><span class="sxs-lookup"><span data-stu-id="3aea5-259">Azure logs user events when an Azure resource (for example, a data factory) is created, updated, or deleted.</span></span> <span data-ttu-id="3aea5-260">Bu olaylara bağlı olarak uyarıları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-260">You can create alerts on these events.</span></span> <span data-ttu-id="3aea5-261">Veri Fabrikası çeşitli ölçümleri yakalamak ve ölçümleri uyarıları oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-261">You can use Data Factory to capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="3aea5-262">Gerçek zamanlı izleme için olayları kullanın ve ölçümleri geçmiş amaçları için kullanmak öneririz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-262">We recommend that you use events for real-time monitoring and use metrics for historical purposes.</span></span>

### <a name="alerts-on-events"></a><span data-ttu-id="3aea5-263">Uyarı olayları</span><span class="sxs-lookup"><span data-stu-id="3aea5-263">Alerts on events</span></span>
<span data-ttu-id="3aea5-264">Azure olayları, Azure kaynaklarınızı neler olduğunu içine yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-264">Azure events provide useful insights into what is happening in your Azure resources.</span></span> <span data-ttu-id="3aea5-265">Azure Data Factory kullanırken, olaylar oluşturulur zaman:</span><span class="sxs-lookup"><span data-stu-id="3aea5-265">When you're using Azure Data Factory, events are generated when:</span></span>

* <span data-ttu-id="3aea5-266">Veri Fabrikası oluşturulduğunda, silinmiş veya güncelleştirildiğinde.</span><span class="sxs-lookup"><span data-stu-id="3aea5-266">A data factory is created, updated, or deleted.</span></span>
* <span data-ttu-id="3aea5-267">Veri işleme ("çalışır") olarak başlatıldı veya tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="3aea5-267">Data processing (as "runs") has started or completed.</span></span>
* <span data-ttu-id="3aea5-268">İsteğe bağlı Hdınsight kümesi oluşturulduğunda veya kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="3aea5-268">An on-demand HDInsight cluster is created or removed.</span></span>

<span data-ttu-id="3aea5-269">Bu kullanıcı olaylarına uyarılar oluşturabilir ve aboneliğin coadministrators ve yönetici e-posta bildirimleri gönderecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-269">You can create alerts on these user events and configure them to send email notifications to the administrator and coadministrators of the subscription.</span></span> <span data-ttu-id="3aea5-270">Ayrıca, koşullar karşılandığında e-posta bildirimleri alması gereken kullanıcıların ek e-posta adresi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-270">In addition, you can specify additional email addresses of users who need to receive email notifications when the conditions are met.</span></span> <span data-ttu-id="3aea5-271">Bu özellik, veri fabrikası sürekli izlemek istemediğiniz ve hatalar hakkında bilgi edinin istediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-271">This feature is useful when you want to get notified on failures and don’t want to continuously monitor your data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="3aea5-272">Şu anda, portal olayları uyarıları göstermez.</span><span class="sxs-lookup"><span data-stu-id="3aea5-272">Currently, the portal doesn't show alerts on events.</span></span> <span data-ttu-id="3aea5-273">Kullanım [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md) tüm uyarıları görmek için.</span><span class="sxs-lookup"><span data-stu-id="3aea5-273">Use the [Monitoring and Management app](data-factory-monitor-manage-app.md) to see all alerts.</span></span>


#### <a name="specify-an-alert-definition"></a><span data-ttu-id="3aea5-274">Bir uyarı tanımı belirtin</span><span class="sxs-lookup"><span data-stu-id="3aea5-274">Specify an alert definition</span></span>
<span data-ttu-id="3aea5-275">Bir uyarı tanımı belirtmek için uyarı almak istediğiniz işlemleri açıklayan bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3aea5-275">To specify an alert definition, you create a JSON file that describes the operations that you want to be alerted on.</span></span> <span data-ttu-id="3aea5-276">Aşağıdaki örnekte, bir e-posta bildirimi RunFinished işlem için uyarı gönderir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-276">In the following example, the alert sends an email notification for the RunFinished operation.</span></span> <span data-ttu-id="3aea5-277">Belirli olması için bir e-posta bildirimi data factory çalıştırılmasıyla tamamladı ve çalıştırma başarısız oldu, gönderilen (durum = FailedExecution).</span><span class="sxs-lookup"><span data-stu-id="3aea5-277">To be specific, an email notification is sent when a run in the data factory has completed and the run has failed (Status = FailedExecution).</span></span>

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
                "description": "One or more of the data slices for the Azure Data Factory has failed processing.",
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

<span data-ttu-id="3aea5-278">Kaldırabileceğiniz **subStatus** belirli hata hakkında uyarı almak istemiyorsanız, JSON tanımından.</span><span class="sxs-lookup"><span data-stu-id="3aea5-278">You can remove **subStatus** from the JSON definition if you don’t want to be alerted on a specific failure.</span></span>

<span data-ttu-id="3aea5-279">Bu örnek, aboneliğinizdeki tüm veri fabrikaları için uyarı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-279">This example sets up the alert for all data factories in your subscription.</span></span> <span data-ttu-id="3aea5-280">Belirli veri fabrikası için ayarlanmış olması için uyarıyı istiyorsanız, veri fabrikası belirtebilirsiniz **resourceUri** içinde **dataSource**:</span><span class="sxs-lookup"><span data-stu-id="3aea5-280">If you want the alert to be set up for a particular data factory, you can specify data factory **resourceUri** in the **dataSource**:</span></span>

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

<span data-ttu-id="3aea5-281">Aşağıdaki tabloda kullanılabilir işlemleri ve durumları (ve alt durumlar) listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3aea5-281">The following table provides the list of available operations and statuses (and substatuses).</span></span>

| <span data-ttu-id="3aea5-282">İşlem adı</span><span class="sxs-lookup"><span data-stu-id="3aea5-282">Operation name</span></span> | <span data-ttu-id="3aea5-283">Durum</span><span class="sxs-lookup"><span data-stu-id="3aea5-283">Status</span></span> | <span data-ttu-id="3aea5-284">Alt durum</span><span class="sxs-lookup"><span data-stu-id="3aea5-284">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3aea5-285">RunStarted</span><span class="sxs-lookup"><span data-stu-id="3aea5-285">RunStarted</span></span> |<span data-ttu-id="3aea5-286">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="3aea5-286">Started</span></span> |<span data-ttu-id="3aea5-287">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="3aea5-287">Starting</span></span> |
| <span data-ttu-id="3aea5-288">RunFinished</span><span class="sxs-lookup"><span data-stu-id="3aea5-288">RunFinished</span></span> |<span data-ttu-id="3aea5-289">Başarısız / başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="3aea5-289">Failed / Succeeded</span></span> |<span data-ttu-id="3aea5-290">FailedResourceAllocation</span><span class="sxs-lookup"><span data-stu-id="3aea5-290">FailedResourceAllocation</span></span><br/><br/><span data-ttu-id="3aea5-291">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="3aea5-291">Succeeded</span></span><br/><br/><span data-ttu-id="3aea5-292">FailedExecution</span><span class="sxs-lookup"><span data-stu-id="3aea5-292">FailedExecution</span></span><br/><br/><span data-ttu-id="3aea5-293">Süresi sona erdi</span><span class="sxs-lookup"><span data-stu-id="3aea5-293">TimedOut</span></span><br/><br/><span data-ttu-id="3aea5-294">< iptal edildi</span><span class="sxs-lookup"><span data-stu-id="3aea5-294"><Canceled</span></span><br/><br/><span data-ttu-id="3aea5-295">FailedValidation</span><span class="sxs-lookup"><span data-stu-id="3aea5-295">FailedValidation</span></span><br/><br/><span data-ttu-id="3aea5-296">terk</span><span class="sxs-lookup"><span data-stu-id="3aea5-296">Abandoned</span></span> |
| <span data-ttu-id="3aea5-297">OnDemandClusterCreateStarted</span><span class="sxs-lookup"><span data-stu-id="3aea5-297">OnDemandClusterCreateStarted</span></span> |<span data-ttu-id="3aea5-298">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="3aea5-298">Started</span></span> | |
| <span data-ttu-id="3aea5-299">OnDemandClusterCreateSuccessful</span><span class="sxs-lookup"><span data-stu-id="3aea5-299">OnDemandClusterCreateSuccessful</span></span> |<span data-ttu-id="3aea5-300">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="3aea5-300">Succeeded</span></span> | |
| <span data-ttu-id="3aea5-301">OnDemandClusterDeleted</span><span class="sxs-lookup"><span data-stu-id="3aea5-301">OnDemandClusterDeleted</span></span> |<span data-ttu-id="3aea5-302">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="3aea5-302">Succeeded</span></span> | |

<span data-ttu-id="3aea5-303">Bkz: [uyarı kuralı oluştur](https://msdn.microsoft.com/library/azure/dn510366.aspx) örnekte kullanılan JSON öğeleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3aea5-303">See [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) for details about the JSON elements that are used in the example.</span></span>

#### <a name="deploy-the-alert"></a><span data-ttu-id="3aea5-304">Uyarı dağıtma</span><span class="sxs-lookup"><span data-stu-id="3aea5-304">Deploy the alert</span></span>
<span data-ttu-id="3aea5-305">Uyarı dağıtmak için Azure PowerShell cmdlet'ini kullanın **New-AzureRmResourceGroupDeployment**, aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="3aea5-305">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

<span data-ttu-id="3aea5-306">Kaynak grubuna dağıtım başarıyla tamamlandıktan sonra aşağıdaki iletiler görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="3aea5-306">After the resource group deployment has finished successfully, you see the following messages:</span></span>

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - The StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts to remove this parameter.
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
> <span data-ttu-id="3aea5-307">Kullanabileceğiniz [uyarı kuralı oluştur](https://msdn.microsoft.com/library/azure/dn510366.aspx) bir uyarı kuralı oluşturmak için REST API.</span><span class="sxs-lookup"><span data-stu-id="3aea5-307">You can use the [Create Alert Rule](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API to create an alert rule.</span></span> <span data-ttu-id="3aea5-308">JSON yükü JSON örnektekine benzer.</span><span class="sxs-lookup"><span data-stu-id="3aea5-308">The JSON payload is similar to the JSON example.</span></span>  


#### <a name="retrieve-the-list-of-azure-resource-group-deployments"></a><span data-ttu-id="3aea5-309">Azure kaynak grubu dağıtımı listesini alma</span><span class="sxs-lookup"><span data-stu-id="3aea5-309">Retrieve the list of Azure resource group deployments</span></span>
<span data-ttu-id="3aea5-310">Dağıtılan Azure kaynak grubu dağıtımı listesini almak için cmdlet'i kullanın **Get-AzureRmResourceGroupDeployment**, aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="3aea5-310">To retrieve the list of deployed Azure resource group deployments, use the cmdlet **Get-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

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

#### <a name="troubleshoot-user-events"></a><span data-ttu-id="3aea5-311">Kullanıcı olaylarına sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3aea5-311">Troubleshoot user events</span></span>
1. <span data-ttu-id="3aea5-312">Tıkladıktan sonra oluşturulan tüm olayları görebilirsiniz **ölçümleri ve işlemleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-312">You can see all the events that are generated after clicking the **Metrics and operations** tile.</span></span>

    ![Ölçümleri ve işlemleri bölmesi](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. <span data-ttu-id="3aea5-314">Tıklatın **olayları** döşeme olaylara bakın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-314">Click the **Events** tile to see the events.</span></span>

    ![Olaylar bölmesi](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. <span data-ttu-id="3aea5-316">Üzerinde **olayları** dikey penceresinde, olaylar, filtrelenmiş olayları ve benzeri ayrıntılarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-316">On the **Events** blade, you can see details about events, filtered events, and so on.</span></span>

    ![Olaylar dikey penceresi](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. <span data-ttu-id="3aea5-318">Tıklatın bir **işlemi** işlemleri listesinde bir hataya neden olur.</span><span class="sxs-lookup"><span data-stu-id="3aea5-318">Click an **Operation** in the operations list that causes an error.</span></span>

    ![Bir işlem seçin](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. <span data-ttu-id="3aea5-320">Tıklatın bir **hata** hata ayrıntılarını görmek için olay.</span><span class="sxs-lookup"><span data-stu-id="3aea5-320">Click an **Error** event to see details about the error.</span></span>

    ![Olay hatası](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

<span data-ttu-id="3aea5-322">Bkz: [Azure Insight cmdlet'leri](https://msdn.microsoft.com/library/mt282452.aspx) eklemek için kullanabileceğiniz PowerShell cmdlet'leri almak veya uyarıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-322">See [Azure Insight cmdlets](https://msdn.microsoft.com/library/mt282452.aspx) for PowerShell cmdlets that you can use to add, get, or remove alerts.</span></span> <span data-ttu-id="3aea5-323">İşte kullanmanın bazı örnekler **Get-AlertRule** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3aea5-323">Here are a few examples of using the **Get-AlertRule** cmdlet:</span></span>

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
Description : One or more of the data slices for the Azure Data Factory has failed processing.
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

<span data-ttu-id="3aea5-324">Ayrıntılar ve Get-AlertRule cmdlet örnekleri görmek için aşağıdaki get-help komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3aea5-324">Run the following get-help commands to see details and examples for the Get-AlertRule cmdlet.</span></span>

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


<span data-ttu-id="3aea5-325">Portal dikey penceresinde uyarı oluşturma olaylarını görme ancak e-posta bildirimleri almadığınız, belirtilen e-posta adresi dış göndericilerden e-postaları için ayarlanmış olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-325">If you see the alert generation events on the portal blade but you don't receive email notifications, check whether the email address that is specified is set to receive emails from external senders.</span></span> <span data-ttu-id="3aea5-326">Uyarı e-postalar, e-posta ayarlarınız tarafından engellenmiş.</span><span class="sxs-lookup"><span data-stu-id="3aea5-326">The alert emails might have been blocked by your email settings.</span></span>

### <a name="alerts-on-metrics"></a><span data-ttu-id="3aea5-327">Ölçümleri uyarılar</span><span class="sxs-lookup"><span data-stu-id="3aea5-327">Alerts on metrics</span></span>
<span data-ttu-id="3aea5-328">Veri fabrikasında çeşitli ölçümleri yakalamak ve ölçümleri uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-328">In Data Factory, you can capture various metrics and create alerts on metrics.</span></span> <span data-ttu-id="3aea5-329">İzleme ve uyarılar dilimleri için aşağıdaki ölçümleri, veri fabrikası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3aea5-329">You can monitor and create alerts on the following metrics for the slices in your data factory:</span></span>

* <span data-ttu-id="3aea5-330">**Başarısız çalıştırır**</span><span class="sxs-lookup"><span data-stu-id="3aea5-330">**Failed Runs**</span></span>
* <span data-ttu-id="3aea5-331">**Başarılı çalıştırır**</span><span class="sxs-lookup"><span data-stu-id="3aea5-331">**Successful Runs**</span></span>

<span data-ttu-id="3aea5-332">Bu ölçümler yararlıdır ve veri fabrikasında genel başarılı ve başarısız çalışır bir bakış elde size yardımcı.</span><span class="sxs-lookup"><span data-stu-id="3aea5-332">These metrics are useful and help you to get an overview of overall failed and successful runs in the data factory.</span></span> <span data-ttu-id="3aea5-333">Olduğundan her zaman dilimi Çalıştır ölçümleri gösterilen.</span><span class="sxs-lookup"><span data-stu-id="3aea5-333">Metrics are emitted every time there is a slice run.</span></span> <span data-ttu-id="3aea5-334">Saat başlangıcında, bu ölçümleri toplanır ve depolama hesabınıza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-334">At the beginning of the hour, these metrics are aggregated and pushed to your storage account.</span></span> <span data-ttu-id="3aea5-335">Ölçümleri etkinleştirmek için bir depolama hesabı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="3aea5-335">To enable metrics, set up a storage account.</span></span>

#### <a name="enable-metrics"></a><span data-ttu-id="3aea5-336">Ölçümleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="3aea5-336">Enable metrics</span></span>
<span data-ttu-id="3aea5-337">Ölçümleri etkinleştirmek için aşağıdakiler arasından tıklatın **Data Factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="3aea5-337">To enable metrics, click the following from the **Data Factory** blade:</span></span>

<span data-ttu-id="3aea5-338">**İzleme** > **ölçüm** > **tanılama ayarlarını** > **tanılama**</span><span class="sxs-lookup"><span data-stu-id="3aea5-338">**Monitoring** > **Metric** > **Diagnostic settings** > **Diagnostics**</span></span>

![Tanılama bağlantı](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

<span data-ttu-id="3aea5-340">Üzerinde **tanılama** dikey penceresinde tıklatın **üzerinde**, depolama hesabını seçin ve'ı tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="3aea5-340">On the **Diagnostics** blade, click **On**, select the storage account, and click **Save**.</span></span>

![Tanılama dikey penceresi](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

<span data-ttu-id="3aea5-342">Görünür olmasını ölçümler bir saat kadar sürebilir **izleme** dikey çünkü ölçümleri toplama saatlik olur.</span><span class="sxs-lookup"><span data-stu-id="3aea5-342">It might take up to one hour for the metrics to be visible on the **Monitoring** blade because metrics aggregation happens hourly.</span></span>

### <a name="set-up-an-alert-on-metrics"></a><span data-ttu-id="3aea5-343">Ölçümler hakkında bir uyarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="3aea5-343">Set up an alert on metrics</span></span>
<span data-ttu-id="3aea5-344">Tıklatın **Data Factory ölçümleri** döşeme:</span><span class="sxs-lookup"><span data-stu-id="3aea5-344">Click the **Data Factory metrics** tile:</span></span>

![Veri Fabrikası ölçümleri kutucuğu](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

<span data-ttu-id="3aea5-346">Üzerinde **ölçüm** dikey penceresinde tıklatın **+ uyarı Ekle** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="3aea5-346">On the **Metric** blade, click **+ Add alert** on the toolbar.</span></span>
<span data-ttu-id="3aea5-347">![Data factory ölçüm dikey penceresi > Uyarı Ekle](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span><span class="sxs-lookup"><span data-stu-id="3aea5-347">![Data factory metric blade > Add alert](./media/data-factory-monitor-manage-pipelines/add-alert.png)</span></span>

<span data-ttu-id="3aea5-348">Üzerinde **uyarı kuralı eklemek** sayfasında, aşağıdaki adımları uygulayın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3aea5-348">On the **Add an alert rule** page, do the following steps, and click **OK**.</span></span>

* <span data-ttu-id="3aea5-349">Uyarı için bir ad girin (örnek: "uyarı başarısız oldu").</span><span class="sxs-lookup"><span data-stu-id="3aea5-349">Enter a name for the alert (example: "failed alert").</span></span>
* <span data-ttu-id="3aea5-350">Uyarı için bir açıklama girin (örnek: "bir hata oluştuğunda bir e-posta Gönder").</span><span class="sxs-lookup"><span data-stu-id="3aea5-350">Enter a description for the alert (example: "send an email when a failure occurs").</span></span>
* <span data-ttu-id="3aea5-351">Bir ("Çalıştığında başarısız oldu" vs. ölçümünü seçin "Başarılı çalışır").</span><span class="sxs-lookup"><span data-stu-id="3aea5-351">Select a metric ("Failed Runs" vs. "Successful Runs").</span></span>
* <span data-ttu-id="3aea5-352">Bir koşul ve bir eşik değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-352">Specify a condition and a threshold value.</span></span>   
* <span data-ttu-id="3aea5-353">Süreyi belirtin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-353">Specify the period of time.</span></span>
* <span data-ttu-id="3aea5-354">Bir e-posta sahipleri, Katkıda Bulunanlar ve okuyucular gönderilmesi gerekip gerekmediğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="3aea5-354">Specify whether an email should be sent to owners, contributors, and readers.</span></span>

![Data factory ölçüm dikey penceresi > Uyarı kuralı Ekle](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

<span data-ttu-id="3aea5-356">Uyarı kuralı başarıyla eklendi, dikey penceresi kapanır ve yeni uyarı gördüğünüz sonra **ölçüm** dikey.</span><span class="sxs-lookup"><span data-stu-id="3aea5-356">After the alert rule is added successfully, the blade closes and you see the new alert on the **Metric** blade.</span></span>

![Data factory ölçüm dikey penceresi > eklenen yeni uyarı](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

<span data-ttu-id="3aea5-358">Uyarıları sayısını görmeniz gerekir **uyarı kuralları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-358">You should also see the number of alerts in the **Alert rules** tile.</span></span> <span data-ttu-id="3aea5-359">Tıklatın **uyarı kuralları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="3aea5-359">Click the **Alert rules** tile.</span></span>

![Data factory ölçüm dikey penceresi - uyarı kuralları](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

<span data-ttu-id="3aea5-361">Üzerinde **uyarı kuralları** dikey penceresinde, var olan tüm uyarıları görebilir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-361">On the **Alerts rules** blade, you see any existing alerts.</span></span> <span data-ttu-id="3aea5-362">Bir uyarı eklemek için tıklatın **uyarı Ekle** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="3aea5-362">To add an alert, click **Add alert** on the toolbar.</span></span>

![Uyarı kuralları dikey penceresi](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a><span data-ttu-id="3aea5-364">Uyarı bildirimleri</span><span class="sxs-lookup"><span data-stu-id="3aea5-364">Alert notifications</span></span>
<span data-ttu-id="3aea5-365">Uyarı kuralı koşulu ile eşleşen sonra uyarı etkinleştirildikten bildiren bir e-posta almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3aea5-365">After the alert rule matches the condition, you should get an email that says the alert is activated.</span></span> <span data-ttu-id="3aea5-366">Sorunun çözümlendiğini ve uyarı koşulu artık eşleşmiyor sonra uyarı çözümlendiğinde bildiren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3aea5-366">After the issue is resolved and the alert condition doesn’t match anymore, you get an email that says the alert is resolved.</span></span>

<span data-ttu-id="3aea5-367">Bu davranış için bir uyarı kuralı niteleyen her hatasında bir bildirim burada gönderilen olaylar farklıdır.</span><span class="sxs-lookup"><span data-stu-id="3aea5-367">This behavior is different than events where a notification is sent on every failure that an alert rule qualifies for.</span></span>

### <a name="deploy-alerts-by-using-powershell"></a><span data-ttu-id="3aea5-368">PowerShell kullanarak uyarıları dağıtma</span><span class="sxs-lookup"><span data-stu-id="3aea5-368">Deploy alerts by using PowerShell</span></span>
<span data-ttu-id="3aea5-369">Ölçümler için uyarı olayları için yaptığınız şekilde dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-369">You can deploy alerts for metrics the same way that you do for events.</span></span>

<span data-ttu-id="3aea5-370">**Uyarı tanımı**</span><span class="sxs-lookup"><span data-stu-id="3aea5-370">**Alert definition**</span></span>

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

<span data-ttu-id="3aea5-371">Değiştir *Subscriptionıd*, *resourceGroupName*, ve *dataFactoryName* uygun değerlerle örnekteki.</span><span class="sxs-lookup"><span data-stu-id="3aea5-371">Replace *subscriptionId*, *resourceGroupName*, and *dataFactoryName* in the sample with appropriate values.</span></span>

<span data-ttu-id="3aea5-372">*metricName* şu anda iki değer destekler:</span><span class="sxs-lookup"><span data-stu-id="3aea5-372">*metricName* currently supports two values:</span></span>

* <span data-ttu-id="3aea5-373">FailedRuns</span><span class="sxs-lookup"><span data-stu-id="3aea5-373">FailedRuns</span></span>
* <span data-ttu-id="3aea5-374">SuccessfulRuns</span><span class="sxs-lookup"><span data-stu-id="3aea5-374">SuccessfulRuns</span></span>

<span data-ttu-id="3aea5-375">**Uyarı dağıtma**</span><span class="sxs-lookup"><span data-stu-id="3aea5-375">**Deploy the alert**</span></span>

<span data-ttu-id="3aea5-376">Uyarı dağıtmak için Azure PowerShell cmdlet'ini kullanın **New-AzureRmResourceGroupDeployment**, aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="3aea5-376">To deploy the alert, use the Azure PowerShell cmdlet **New-AzureRmResourceGroupDeployment**, as shown in the following example:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

<span data-ttu-id="3aea5-377">Başarılı dağıtım sonrasında iletiden görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3aea5-377">You should see following message after a successful deployment:</span></span>

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

<span data-ttu-id="3aea5-378">Aynı zamanda **Ekle AlertRule** bir uyarı kuralı dağıtmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3aea5-378">You can also use the **Add-AlertRule** cmdlet to deploy an alert rule.</span></span> <span data-ttu-id="3aea5-379">Bkz: [Ekle AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) ayrıntı ve örnekler için konu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-379">See the [Add-AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) topic for details and examples.</span></span>  

## <a name="move-a-data-factory-to-a-different-resource-group-or-subscription"></a><span data-ttu-id="3aea5-380">Veri Fabrikası farklı bir kaynak grubuna veya aboneliğe taşıma</span><span class="sxs-lookup"><span data-stu-id="3aea5-380">Move a data factory to a different resource group or subscription</span></span>
<span data-ttu-id="3aea5-381">Kullanarak farklı bir kaynak grubunda veya farklı bir abonelik için bir veri fabrikası taşıyabilirsiniz **taşıma** veri fabrikanızın giriş sayfasında düğme çubuğu komutu.</span><span class="sxs-lookup"><span data-stu-id="3aea5-381">You can move a data factory to a different resource group or a different subscription by using the **Move** command bar button on the home page of your data factory.</span></span>

![Veri Fabrikası taşıma](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

<span data-ttu-id="3aea5-383">Ayrıca, ilgili kaynakları (örneğin, data factory ile ilişkili olan uyarılar), veri fabrikası birlikte taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3aea5-383">You can also move any related resources (such as alerts that are associated with the data factory), along with the data factory.</span></span>

![Taşıma kaynaklar iletişim kutusu](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
