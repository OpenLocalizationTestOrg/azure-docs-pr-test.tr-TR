---
title: "İzleme ve veri ardışık - Azure yönetme | Microsoft Docs"
description: "Azure data factory'leri ve ardışık düzen yönetmek ve izlemek için izleme ve yönetim uygulaması kullanmayı öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: d5a2d1f3d85b8a2212326cfcfd0ba5d80356b769
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-the-monitoring-and-management-app"></a><span data-ttu-id="5b6c1-103">İzleme ve Azure Data Factory işlem hatlarını izleme ve yönetim uygulaması kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="5b6c1-103">Monitor and manage Azure Data Factory pipelines by using the Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5b6c1-104">Azure portal/Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="5b6c1-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="5b6c1-105">Kullanılarak izleme ve yönetim uygulaması</span><span class="sxs-lookup"><span data-stu-id="5b6c1-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="5b6c1-106">Bu makalede izleme ve yönetim uygulama izleme, yönetme ve Data Factory işlem hatlarınızı hata ayıklamak için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-106">This article describes how to use the Monitoring and Management app to monitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="5b6c1-107">Ayrıca hatalarında bildirim almak için uyarı oluşturma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-107">It also provides information on how to create alerts to get notified on failures.</span></span> <span data-ttu-id="5b6c1-108">Aşağıdaki videoyu izleyerek uygulamayı kullanmaya başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-108">You can get started with using the application by watching the following video:</span></span>

> [!NOTE]
> <span data-ttu-id="5b6c1-109">Portalı'nda bkz videoda gösterilen kullanıcı arabirimi tam olarak eşleşmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-109">The user interface shown in the video may not exactly match what you see in the portal.</span></span> <span data-ttu-id="5b6c1-110">Biraz daha eski olduğu, ancak kavramları aynı kalır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-110">It's slightly older, but concepts remain the same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-the-monitoring-and-management-app"></a><span data-ttu-id="5b6c1-111">İzleme ve yönetim uygulama başlatma</span><span class="sxs-lookup"><span data-stu-id="5b6c1-111">Launch the Monitoring and Management app</span></span>
<span data-ttu-id="5b6c1-112">İzleme ve yönetim uygulaması başlatmak için tıklatın **İzleyici & Yönet** döşemesinin **Data Factory** veri fabrikanızın dikey.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-112">To launch the Monitor and Management app, click the **Monitor & Manage** tile on the **Data Factory** blade for your data factory.</span></span>

![Data Factory giriş sayfasında izleme kutucuğu](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="5b6c1-114">Ayrı bir pencerede açmak izleme ve yönetim uygulaması görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-114">You should see the Monitoring and Management app open in a separate window.</span></span>  

![İzleme ve Yönetim uygulaması](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="5b6c1-116">Web tarayıcısının "Yetkilendiriliyor..." durumunda takıldığını görürseniz, temizleyin **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** onay kutusu--veya seçili, Canlı oluşturmak için bir özel durum **login.microsoftonline.com**, ve ardından uygulamayı açmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-116">If you see that the web browser is stuck at "Authorizing...", clear the **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>


<span data-ttu-id="5b6c1-117">Orta bölmede etkinlik Windows listesinde, her bir etkinlik çalışması için bir etkinlik penceresini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-117">In the Activity Windows list in the middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="5b6c1-118">Örneğin, beş saatlik saatte bir çalışacak şekilde zamanlanmış etkinlik varsa, beş veri dilimi ile ilişkili beş etkinlik windows bakın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-118">For example, if you have the activity scheduled to run hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="5b6c1-119">Etkinlik pencerelerine alttaki listede görmüyorsanız, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-119">If you don't see activity windows in the list at the bottom, do the following:</span></span>
 
- <span data-ttu-id="5b6c1-120">Güncelleştirme **başlangıç zamanı** ve **bitiş saati** filtreleri hattınızı başlangıç ve bitiş zamanları eşleşen ve ardından üst **Uygula** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-120">Update the **start time** and **end time** filters at the top to match the start and end times of your pipeline, and then click the **Apply** button.</span></span>  
- <span data-ttu-id="5b6c1-121">Etkinlik Windows listesi otomatik olarak yenilenmez.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-121">The Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="5b6c1-122">Tıklatın **yenileme** araç çubuğunda **etkinlik Windows** listesi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-122">Click the **Refresh** button on the toolbar in the **Activity Windows** list.</span></span>  

<span data-ttu-id="5b6c1-123">Bu adımları ile test etmek için bir veri fabrikası uygulaması yoksa, öğreticiyi yapın: [veri kopyalama Blob depolama alanından SQL Data Factory kullanarak veritabanına](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="5b6c1-123">If you don't have a Data Factory application to test these steps with, do the tutorial: [copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-the-monitoring-and-management-app"></a><span data-ttu-id="5b6c1-124">İzleme ve yönetim uygulaması anlama</span><span class="sxs-lookup"><span data-stu-id="5b6c1-124">Understand the Monitoring and Management app</span></span>
<span data-ttu-id="5b6c1-125">Soldaki bölmede üç sekme vardır: **kaynak Gezgini**, **izleme görünümleri**, ve **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-125">There are three tabs on the left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="5b6c1-126">İlk sekme (**kaynak Gezgini**) varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-126">The first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="5b6c1-127">Kaynak Gezgini</span><span class="sxs-lookup"><span data-stu-id="5b6c1-127">Resource Explorer</span></span>
<span data-ttu-id="5b6c1-128">Aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-128">You see the following:</span></span>

* <span data-ttu-id="5b6c1-129">Kaynak Gezgini **ağaç görünümü** sol bölmede.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-129">The Resource Explorer **tree view** in the left pane.</span></span>
* <span data-ttu-id="5b6c1-130">**Diyagram görünümü** Orta bölmede üstünde.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-130">The **Diagram View** at the top in the middle pane.</span></span>
* <span data-ttu-id="5b6c1-131">**Etkinlik Windows** Orta bölmede altındaki listesi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-131">The **Activity Windows** list at the bottom in the middle pane.</span></span>
* <span data-ttu-id="5b6c1-132">**Özellikleri**, **etkinlik penceresini Explorer**, ve **betik** sağ bölmedeki sekmeleri.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-132">The **Properties**, **Activity Window Explorer**, and **Script** tabs in the right pane.</span></span>

<span data-ttu-id="5b6c1-133">Kaynak Gezgini, ağaç görünümünde veri fabrikasında tüm kaynakları (komut zincirleri, veri kümeleri, bağlı hizmetler) bakın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in the data factory in a tree view.</span></span> <span data-ttu-id="5b6c1-134">Ne zaman kaynak Gezgini, bir nesne seçin:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="5b6c1-135">İlişkili veri fabrikası Varlık diyagram Görünümü'nde vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-135">The associated Data Factory entity is highlighted in the Diagram View.</span></span>
* <span data-ttu-id="5b6c1-136">[Etkinlik pencerelerine ilişkili](data-factory-scheduling-and-execution.md) altındaki etkinlik Windows listesinde vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in the Activity Windows list at the bottom.</span></span>  
* <span data-ttu-id="5b6c1-137">Sağ bölmede Özellikleri penceresinde seçili nesnenin özelliklerini gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-137">The properties of the selected object are shown in the Properties window in the right pane.</span></span>
* <span data-ttu-id="5b6c1-138">Seçilen nesneyi JSON tanımını gösterilen varsa.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-138">The JSON definition of the selected object is shown, if applicable.</span></span> <span data-ttu-id="5b6c1-139">Örneğin: bağlı hizmet, bir veri kümesi veya işlem hattı.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Kaynak Gezgini](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="5b6c1-141">Bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) etkinlik windows hakkında ayrıntılı kavramsal bilgi için makalenin.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-141">See the [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="5b6c1-142">Diyagram Görünümü</span><span class="sxs-lookup"><span data-stu-id="5b6c1-142">Diagram View</span></span>
<span data-ttu-id="5b6c1-143">Veri Fabrikası diyagram görünümünü bölmeden bir veri fabrikası ve varlıklarını yönetmek ve izlemek için cam sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-143">The Diagram View of a data factory provides a single pane of glass to monitor and manage a data factory and its assets.</span></span> <span data-ttu-id="5b6c1-144">Diyagram Görünümü'nde bir Data Factory varlığı (dataset/ardışık düzeni) seçtiğinizde:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-144">When you select a Data Factory entity (dataset/pipeline) in the Diagram View:</span></span>

* <span data-ttu-id="5b6c1-145">Veri Fabrikası varlık ağaç görünümünde seçilir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-145">The data factory entity is selected in the tree view.</span></span>
* <span data-ttu-id="5b6c1-146">İlişkili etkinlik windows etkinlik Windows listesinde vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-146">The associated activity windows are highlighted in the Activity Windows list.</span></span>
* <span data-ttu-id="5b6c1-147">Özellikler penceresinde seçili nesnenin özelliklerini gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-147">The properties of the selected object are shown in the Properties window.</span></span>

<span data-ttu-id="5b6c1-148">Ardışık Düzen (duraklatılmış durumda değil) etkin olduğunda, yeşil bir çizgiyle gösterilir:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-148">When the pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Çalışan işlem hattı](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="5b6c1-150">Duraklatma, sürdürme veya diyagram görünümünde seçerek ve komut çubuğunda düğmeleri kullanarak bir ardışık düzen sonlandırmak.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-150">You can pause, resume, or terminate a pipeline by selecting it in the diagram view and using the buttons on the command bar.</span></span>

![Komut çubuğunda Duraklat/Sürdür](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="5b6c1-152">Diyagram görünümünde ardışık düzeni için üç komut çubuğu düğmelerini vardır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-152">There are three command bar buttons for the pipeline in the Diagram View.</span></span> <span data-ttu-id="5b6c1-153">Ardışık Düzen duraklatmak için ikinci düğmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-153">You can use the second button to pause the pipeline.</span></span> <span data-ttu-id="5b6c1-154">Duraklatma çalışmakta etkinlikleri sonlandırmak değil ve bunları tamamlanıncaya kadar devam olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-154">Pausing doesn't terminate the currently running activities and lets them proceed to completion.</span></span> <span data-ttu-id="5b6c1-155">Üçüncü düğme ardışık duraklatır ve onun etkinlikleri yürütme varolan sona erer.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-155">The third button pauses the pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="5b6c1-156">İlk düğme ardışık sürdürür.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-156">The first button resumes the pipeline.</span></span> <span data-ttu-id="5b6c1-157">İşlem hattınızı duraklatıldığında, ardışık düzen rengini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-157">When your pipeline is paused, the color of the pipeline changes.</span></span> <span data-ttu-id="5b6c1-158">Örneğin, duraklatılmış bir ardışık düzen aşağıdaki görüntüde şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-158">For example, a paused pipeline looks like in the following image:</span></span> 

![Ardışık Düzen duraklatıldı](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="5b6c1-160">Ctrl tuşunu kullanarak çoklu seçim iki veya daha fazla ardışık düzen olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-160">You can multi-select two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="5b6c1-161">Komut çubuğu düğmelerini Duraklat/birden çok ardışık düzen aynı anda Sürdür için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-161">You can use the command bar buttons to pause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="5b6c1-162">Ayrıca, bir işlem hattı sağ tıklatın ve askıya alma, sürdürme veya bir işlem hattı sonlandırmak için seçenekleri seçin.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-162">You can also right-click a pipeline and select options to suspend, resume, or terminate a pipeline.</span></span> 

![Ardışık düzeni için bağlam menüsü](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="5b6c1-164">Tıklatın **açık işlem hattı** işlem hattındaki tüm etkinlikleri görmek için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-164">Click the **Open pipeline** option to see all the activities in the pipeline.</span></span> 

![İşlem hattı menüsünü açma](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="5b6c1-166">Açılan ardışık düzen Görünümü'nde, işlem hattındaki tüm etkinlikleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-166">In the opened pipeline view, you see all activities in the pipeline.</span></span> <span data-ttu-id="5b6c1-167">Bu örnekte, yalnızca bir etkinlik yok: kopyalama etkinliği.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Açılan ardışık düzen](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="5b6c1-169">Önceki görünüme geri dönmek için veri fabrikası adı üstteki içerik haritası menüsünde tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-169">To go back to the previous view, click the data factory name in the breadcrumb menu at the top.</span></span>

<span data-ttu-id="5b6c1-170">Bir çıkış veri kümesini veya çıkış veri kümesinde farenizi taşıdığınızda seçtiğinizde ardışık düzen görünümünde, bu veri kümesi için etkinlik Windows açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-170">In the pipeline view, when you select an output dataset or when you move your mouse over the output dataset, you see the Activity Windows pop-up window for that dataset.</span></span>

![Etkinlik Windows açılır penceresi](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="5b6c1-172">İçinde için ayrıntıları görmek için bir etkinlik penceresini tıklayabilirsiniz **özellikleri** penceresinin sağ bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-172">You can click an activity window to see details for it in the **Properties** window in the right pane.</span></span>

![Etkinlik penceresini özellikleri](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="5b6c1-174">Sağ bölmede geçmek **etkinlik penceresini Explorer** daha fazla ayrıntı için sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-174">In the right pane, switch to the **Activity Window Explorer** tab to see more details.</span></span>

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="5b6c1-176">Ayrıca bkz: **değişkenleri çözülmüş** bir etkinliğin her çalıştırma denemesi için **denemeleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-176">You also see **resolved variables** for each run attempt for an activity in the **Attempts** section.</span></span>

![Çözümlenen değişkenleri](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="5b6c1-178">Geçiş **betik** sekmesi seçili nesne için JSON betik tanımına bakın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-178">Switch to the **Script** tab to see the JSON script definition for the selected object.</span></span>   

![Komut dosyası sekmesi](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="5b6c1-180">Etkinlik pencerelerine üç yerde görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="5b6c1-181">Diyagram görünümünde (Orta bölme) etkinlik Windows açılır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-181">The Activity Windows pop-up in the Diagram View (middle pane).</span></span>
* <span data-ttu-id="5b6c1-182">Sağ bölmede etkinlik penceresini Gezgini.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-182">The Activity Window Explorer in the right pane.</span></span>
* <span data-ttu-id="5b6c1-183">Alt bölme etkinlik Windows listesinde.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-183">The Activity Windows list in the bottom pane.</span></span>

<span data-ttu-id="5b6c1-184">Etkinlik pencerelerine açılır ve etkinlik penceresini Gezgini sol ve sağ ok kullanarak önceki hafta ve sonraki hafta gezinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-184">In the Activity Windows pop-up and Activity Window Explorer, you can scroll to the previous week and the next week by using the left and right arrows.</span></span>

![Etkinlik penceresini Explorer sol/sağ ok](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="5b6c1-186">Diyagram görünümü en altında bu düğmeleri Bkz: Yakınlaştır, uzaklaştırma, yakınlaştırma sığacak şekilde, yakınlaştırma % 100, kilit düzeni.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-186">At the bottom of the Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom to Fit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="5b6c1-187">**Kilit düzeni** düğmesi önler yanlışlıkla tablolar ve ardışık düzen diyagram Görünümü'nde taşınmasını.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-187">The **Lock layout** button prevents you from accidentally moving tables and pipelines in the Diagram View.</span></span> <span data-ttu-id="5b6c1-188">Bu varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-188">It's on by default.</span></span> <span data-ttu-id="5b6c1-189">Uygulamayı kapatın ve varlıkları diyagramında hareket ettirin.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-189">You can turn it off and move entities around in the diagram.</span></span> <span data-ttu-id="5b6c1-190">Devre dışı bıraktığınızda, tablolar ve ardışık düzen otomatik Konumlandır için Son düğmesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-190">When you turn it off, you can use the last button to automatically position tables and pipelines.</span></span> <span data-ttu-id="5b6c1-191">Fare tekerleği kullanarak içeri veya dışarı ayrıca yakınlaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-191">You can also zoom in or out by using the mouse wheel.</span></span>

![Diyagram görünümü yakınlaştırma komutları](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="5b6c1-193">Etkinlik Windows listesi</span><span class="sxs-lookup"><span data-stu-id="5b6c1-193">Activity Windows list</span></span>
<span data-ttu-id="5b6c1-194">Etkinlik Windows orta bölmesinde altındaki tüm etkinlik windows kaynak Gezgini ya da diyagram görünümünde seçilen veri kümesi için görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-194">The Activity Windows list at the bottom of the middle pane displays all activity windows for the dataset that you selected in the Resource Explorer or the Diagram View.</span></span> <span data-ttu-id="5b6c1-195">Varsayılan olarak, en son etkinlik pencerenin en üstünde gördüğünüz anlamına gelir, azalan sırada listesidir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-195">By default, the list is in descending order, which means that you see the latest activity window at the top.</span></span>

![Etkinlik Windows listesi](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="5b6c1-197">Bu liste otomatik yenileme değil, bu nedenle el ile yenilemek için araç çubuğunda Yenile düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-197">This list doesn't refresh automatically, so use the refresh button on the toolbar to manually refresh it.</span></span>  

<span data-ttu-id="5b6c1-198">Etkinlik pencerelerine aşağıdaki durumlardan biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-198">Activity windows can be in one of the following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="5b6c1-199">Durum</span><span class="sxs-lookup"><span data-stu-id="5b6c1-199">Status</span></span></th><th align="left"><span data-ttu-id="5b6c1-200">Alt durum</span><span class="sxs-lookup"><span data-stu-id="5b6c1-200">Substatus</span></span></th><th align="left"><span data-ttu-id="5b6c1-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5b6c1-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="5b6c1-202">Bekleniyor</span><span class="sxs-lookup"><span data-stu-id="5b6c1-202">Waiting</span></span></td><td><span data-ttu-id="5b6c1-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="5b6c1-203">ScheduleTime</span></span></td><td><span data-ttu-id="5b6c1-204">Zaman çalıştırmak ilişkin etkinlik penceresinin gelen kurmadı.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-204">The time hasn't come for the activity window to run.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="5b6c1-205">DatasetDependencies</span></span></td><td><span data-ttu-id="5b6c1-206">Yukarı Akış bağımlılıkları hazır değil.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-206">The upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="5b6c1-207">ComputeResources</span></span></td><td><span data-ttu-id="5b6c1-208">İşlem kaynakları kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-208">The compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="5b6c1-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="5b6c1-210">Tüm etkinlik örnekleri diğer etkinlik windows çalıştıran meşgul.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-210">All the activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="5b6c1-211">ActivityResume</span></span></td><td><span data-ttu-id="5b6c1-212">Etkinlik duraklatıldı ve sürdürülene kadar etkinlik windows çalıştıramaz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-212">The activity is paused and can't run the activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-213">Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="5b6c1-213">Retry</span></span></td><td><span data-ttu-id="5b6c1-214">Etkinlik yürütme yeniden deneniyor.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-214">The activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-215">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="5b6c1-215">Validation</span></span></td><td><span data-ttu-id="5b6c1-216">Doğrulama henüz başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="5b6c1-217">ValidationRetry</span></span></td><td><span data-ttu-id="5b6c1-218">Doğrulama işleminin yeniden gerçekleştirilmesi bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-218">Validation is waiting to be retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="5b6c1-219">Devam ediyor</span><span class="sxs-lookup"><span data-stu-id="5b6c1-219">InProgress</span></span></td><td><span data-ttu-id="5b6c1-220">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="5b6c1-220">Validating</span></span></td><td><span data-ttu-id="5b6c1-221">Doğrulama devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="5b6c1-222">Etkinlik penceresinin işleniyor.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-222">The activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="5b6c1-223">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-223">Failed</span></span></td><td><span data-ttu-id="5b6c1-224">Süresi sona erdi</span><span class="sxs-lookup"><span data-stu-id="5b6c1-224">TimedOut</span></span></td><td><span data-ttu-id="5b6c1-225">Etkinlik yürütme etkinlik tarafından izin daha uzun sürdü.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-225">The activity execution took longer than what is allowed by the activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-226">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="5b6c1-226">Canceled</span></span></td><td><span data-ttu-id="5b6c1-227">Etkinlik penceresinin kullanıcı eylemi tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-227">The activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-228">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="5b6c1-228">Validation</span></span></td><td><span data-ttu-id="5b6c1-229">Doğrulama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="5b6c1-230">Etkinlik penceresinin oluşturulan ya da doğrulanması başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-230">The activity window failed to be generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="5b6c1-231">Hazır</span><span class="sxs-lookup"><span data-stu-id="5b6c1-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="5b6c1-232">Etkinlik penceresinin tüketimi için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-232">The activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-233">Atlandı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="5b6c1-234">Etkinlik penceresinin işlenen değildi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-234">The activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5b6c1-235">None</span><span class="sxs-lookup"><span data-stu-id="5b6c1-235">None</span></span></td><td>-</td><td><span data-ttu-id="5b6c1-236">Bir etkinlik penceresini farklı bir durum ile var olmuş ancak sıfırlanmış.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-236">An activity window used to exist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="5b6c1-237">Listenin etkinliği penceresindeki tıklattığınızda içinde ayrıntılarını görmek **etkinlik Windows Explorer** veya **özellikleri** penceresini sağdaki.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-237">When you click an activity window in the list, you see details about it in the **Activity Windows Explorer** or the **Properties** window on the right.</span></span>

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="5b6c1-239">Etkinlik pencerelerine Yenile</span><span class="sxs-lookup"><span data-stu-id="5b6c1-239">Refresh activity windows</span></span>
<span data-ttu-id="5b6c1-240">Ayrıntıları otomatik olarak yenilenir değil, bu nedenle etkinlik windows listesini el ile yenilemek için komut çubuğunda (ikinci düğme) Yenile düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-240">The details aren't automatically refreshed, so use the refresh button (the second button) on the command bar to manually refresh the activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="5b6c1-241">Özellik penceresi</span><span class="sxs-lookup"><span data-stu-id="5b6c1-241">Properties window</span></span>
<span data-ttu-id="5b6c1-242">Özellikler penceresini izleme ve yönetim uygulaması en sağ bölmesinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-242">The Properties window is in the right-most pane of the Monitoring and Management app.</span></span>

![Özellik penceresi](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="5b6c1-244">Kaynak Gezgini (ağaç görünümü), diyagram görünümü veya etkinlik Windows liste seçili öğenin özelliklerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-244">It displays properties for the item that you selected in the Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="5b6c1-245">Etkinlik penceresini Gezgini</span><span class="sxs-lookup"><span data-stu-id="5b6c1-245">Activity Window Explorer</span></span>
<span data-ttu-id="5b6c1-246">**Etkinlik penceresini Explorer** izleme ve yönetim uygulaması en sağdaki bölmede bir penceredir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-246">The **Activity Window Explorer** window is in the right-most pane of the Monitoring and Management app.</span></span> <span data-ttu-id="5b6c1-247">Etkinlik Windows açılır penceresi veya etkinlik Windows listedeki seçili etkinlik penceresinin hakkındaki ayrıntıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-247">It displays details about the activity window that you selected in the Activity Windows pop-up window or the Activity Windows list.</span></span>

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="5b6c1-249">Üst Takvim görünümünde tıklayarak başka bir etkinlik penceresine geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-249">You can switch to another activity window by clicking it in the calendar view at the top.</span></span> <span data-ttu-id="5b6c1-250">Etkinlik Windows'dan önceki haftanın ya da sonraki hafta görmek için sayfanın üstünde sol ok/sağ ok düğmelerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-250">You can also use the left arrow/right arrow buttons at the top to see activity windows from the previous week or the next week.</span></span>

<span data-ttu-id="5b6c1-251">Etkinlik penceresinin yeniden çalıştırın veya ayrıntılar bölmesinde yenilemek için alt bölmesinde araç çubuğu düğmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-251">You can use the toolbar buttons in the bottom pane to rerun the activity window or refresh the details in the pane.</span></span>

### <a name="script"></a><span data-ttu-id="5b6c1-252">Betik</span><span class="sxs-lookup"><span data-stu-id="5b6c1-252">Script</span></span>
<span data-ttu-id="5b6c1-253">Kullanabileceğiniz **betik** seçili Data Factory varlığı (bağlantılı hizmet, veri kümesi veya işlem hattı) JSON tanımını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-253">You can use the **Script** tab to view the JSON definition of the selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Komut dosyası sekmesi](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="5b6c1-255">Sistem görünümleri kullanma</span><span class="sxs-lookup"><span data-stu-id="5b6c1-255">Use system views</span></span>
<span data-ttu-id="5b6c1-256">İzleme ve yönetim uygulaması önceden derlenmiş sistem görünümleri içerir (**son etkinlik windows**, **başarısız etkinliği windows**, **ilerleme durumu etkinlik windows**), izin ver en son/başarısız/Süren etkinlik windows veri fabrikanızın görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-256">The Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you to view recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="5b6c1-257">Geçiş **izleme görünümleri** sekmesini tıklatarak soldaki.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-257">Switch to the **Monitoring Views** tab on the left by clicking it.</span></span>

![İzleme görünümleri sekmesi](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="5b6c1-259">Şu anda desteklenen üç sistem görünümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="5b6c1-260">Son Etkinlik windows, başarısız etkinliği windows veya devam eden etkinlik windows etkinlik Windows listesinde (orta bölmesinde altındaki) görmek için bir seçenek belirleyin.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-260">Select an option to see recent activity windows, failed activity windows, or in-progress activity windows in the Activity Windows list (at the bottom of the middle pane).</span></span>

<span data-ttu-id="5b6c1-261">Seçtiğinizde, **son etkinlik windows** seçeneği, azalan sırada olan tüm son etkinlik windows görmek **zaman'son deneme**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-261">When you select the **Recent activity windows** option, you see all recent activity windows in descending order of the **last attempt time**.</span></span>

<span data-ttu-id="5b6c1-262">Kullanabileceğiniz **başarısız etkinliği windows** listesindeki tüm başarısız etkinliği windows görmek için görünümü.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-262">You can use the **Failed activity windows** view to see all failed activity windows in the list.</span></span> <span data-ttu-id="5b6c1-263">İçinde ayrıntılarını görmek için listedeki bir başarısız etkinliği penceresi seçin **özellikleri** penceresi veya **etkinlik penceresini Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-263">Select a failed activity window in the list to see details about it in the **Properties** window or the **Activity Window Explorer**.</span></span> <span data-ttu-id="5b6c1-264">Ayrıca, başarısız olan etkinliği penceresi için herhangi bir günlük indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="5b6c1-265">Sıralama ve filtreleme etkinliği windows</span><span class="sxs-lookup"><span data-stu-id="5b6c1-265">Sort and filter activity windows</span></span>
<span data-ttu-id="5b6c1-266">Değişiklik **başlangıç zamanı** ve **bitiş saati** filtre etkinlik Windows Komut çubuğunda ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-266">Change the **start time** and **end time** settings in the command bar to filter activity windows.</span></span> <span data-ttu-id="5b6c1-267">Başlangıç ve bitiş zamanı değiştirdikten sonra etkinlik Windows listesini yenilemek için bitiş zamanı yanındaki düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-267">After you change the start time and end time, click the button next to the end time to refresh the Activity Windows list.</span></span>

![Başlangıç ve bitiş zamanlarını](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="5b6c1-269">Şu anda, izleme ve yönetim uygulaması UTC biçiminde her zaman uygun.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-269">Currently, all times are in UTC format in the Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="5b6c1-270">İçinde **etkinlik Windows listesi**, bir sütun adına tıklayın (örneğin: durum).</span><span class="sxs-lookup"><span data-stu-id="5b6c1-270">In the **Activity Windows list**, click the name of a column (for example: Status).</span></span>

![Etkinlik Windows liste sütun menüsü](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="5b6c1-272">Aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b6c1-272">You can do the following:</span></span>

* <span data-ttu-id="5b6c1-273">Artan sırada Sırala.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-273">Sort in ascending order.</span></span>
* <span data-ttu-id="5b6c1-274">Azalan sırada sıralayın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-274">Sort in descending order.</span></span>
* <span data-ttu-id="5b6c1-275">Bir veya daha fazla değerlerle (hazır, bekliyor vb.) filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="5b6c1-276">Bir sütunda bir filtre belirttiğinizde, filtrelenmiş değerleri sütundaki değerleri gösterir bu sütun için etkin filtre düğmesini bakın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-276">When you specify a filter on a column, you see the filter button enabled for that column, which indicates that the values in the column are filtered values.</span></span>

![Etkinlik pencerelerine listesinin bir sütuna filtre](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="5b6c1-278">Aynı açılır pencere Filtreleri temizlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-278">You can use the same pop-up window to clear filters.</span></span> <span data-ttu-id="5b6c1-279">Etkinlik pencerelerine listesi için tüm filtreleri temizlemek için komut çubuğunda Filtreyi düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-279">To clear all filters for the Activity Windows list, click the clear filter button on the command bar.</span></span>

![Etkinlik pencerelerine listesi için tüm filtreleri temizlemek](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="5b6c1-281">Toplu işlemleri</span><span class="sxs-lookup"><span data-stu-id="5b6c1-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="5b6c1-282">Seçili etkinlik windows yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5b6c1-282">Rerun selected activity windows</span></span>
<span data-ttu-id="5b6c1-283">Bir etkinlik penceresi seçin, ilk komut çubuğu düğmesi için aşağı oka tıklayın ve seçin **yeniden Çalıştır** / **ile upstream ardışık düzeninde yeniden**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-283">Select an activity window, click the down arrow for the first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="5b6c1-284">Seçtiğinizde, **ile upstream ardışık düzeninde yeniden** seçeneği, tüm Yukarı Akış etkinliği windows de yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-284">When you select the **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="5b6c1-285">![Bir etkinlik penceresi yeniden](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="5b6c1-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="5b6c1-286">Ayrıca, birden çok etkinlik windows listeden seçin ve bunları aynı anda yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-286">You can also select multiple activity windows in the list and rerun them at the same time.</span></span> <span data-ttu-id="5b6c1-287">Etkinlik windows durumlarına göre filtre uygulamak istediğiniz (örneğin: **başarısız**)--ve başarısız olan etkinliği windows etkinlik windows başarısız olmasına neden olan sorunu düzelttikten sonra yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-287">You might want to filter activity windows based on the status (for example: **Failed**)--and then rerun the failed activity windows after correcting the issue that causes the activity windows to fail.</span></span> <span data-ttu-id="5b6c1-288">Etkinlik pencerelerine listesinde filtreleme hakkında ayrıntılar için aşağıdaki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-288">See the following section for details about filtering activity windows in the list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="5b6c1-289">Birden çok ardışık düzen Duraklat/Sürdür</span><span class="sxs-lookup"><span data-stu-id="5b6c1-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="5b6c1-290">Ctrl tuşunu kullanarak çoklu iki veya daha fazla ardışık düzen olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-290">You can multiselect two or more pipelines by using the Ctrl key.</span></span> <span data-ttu-id="5b6c1-291">Bunları Duraklat/Sürdür için (hangi aşağıdaki görüntüde kırmızı dikdörtgen içinde vurgulanır) komut çubuğu düğmelerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-291">You can use the command bar buttons (which are highlighted in the red rectangle in the following image) to pause/resume them.</span></span>

![Komut çubuğunda Duraklat/Sürdür](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="5b6c1-293">Uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b6c1-293">Create alerts</span></span>
<span data-ttu-id="5b6c1-294">**Uyarıları** sayfası, bir uyarı ve görünüm/düzenleme/silme mevcut uyarıları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-294">The **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="5b6c1-295">Sizin de devre dışı bırak/uyarı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="5b6c1-296">Uyarılar sayfasında görmek için tıklatın **uyarıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-296">To see the Alerts page, click the **Alerts** tab.</span></span>

![Uyarılar sekmesi](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="to-create-an-alert"></a><span data-ttu-id="5b6c1-298">Bir uyarı oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="5b6c1-298">To create an alert</span></span>
1. <span data-ttu-id="5b6c1-299">Tıklatın **eklemek uyarı** bir uyarı eklemek için.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-299">Click **Add Alert** to add an alert.</span></span> <span data-ttu-id="5b6c1-300">Gördüğünüz **ayrıntıları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-300">You see the **Details** page.</span></span>

    ![Uyarılar - ayrıntılar sayfası oluşturma](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="5b6c1-302">Belirtin **adı** ve **açıklama** uyarı ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-302">Specify the **Name** and **Description** for the alert, and click **Next**.</span></span> <span data-ttu-id="5b6c1-303">Görmeniz gerekir **filtreleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-303">You should see the **Filters** page.</span></span>

    ![Uyarılar - filtreleri sayfa oluşturma](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="5b6c1-305">Seçin **olay**, **durum**, ve **substatus** (isteğe bağlı) bir Data Factory hizmeti uyarı oluşturup tıklatın istediğiniz **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-305">Select the **event**, **status**, and **substatus** (optional) that you want to create a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="5b6c1-306">Görmeniz gerekir **alıcılar** sayfası.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-306">You should see the **Recipients** page.</span></span>

    ![Uyarılar - alıcılar sayfa oluşturma](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="5b6c1-308">Seçin **abonelik yöneticileri e-posta** seçeneği ve/veya girin bir **ek yönetici e-posta**, tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-308">Select the **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="5b6c1-309">Uyarı listesinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-309">You should see the alert in the list.</span></span>

    ![Uyarılar listesinde](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="5b6c1-311">Uyarılar listesinde düzenleme/silme/devre dışı bırak/etkinleştir bir uyarı uyarı ile ilişkili düğmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-311">In the Alerts list, use the buttons that are associated with the alert to edit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="5b6c1-312">Alt olay/durumu/durum</span><span class="sxs-lookup"><span data-stu-id="5b6c1-312">Event/status/substatus</span></span>
<span data-ttu-id="5b6c1-313">Aşağıdaki tabloda kullanılabilir olayları ve durumları (ve alt durumlar) listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-313">The following table provides the list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="5b6c1-314">Olay adı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-314">Event name</span></span> | <span data-ttu-id="5b6c1-315">Durum</span><span class="sxs-lookup"><span data-stu-id="5b6c1-315">Status</span></span> | <span data-ttu-id="5b6c1-316">Alt durum</span><span class="sxs-lookup"><span data-stu-id="5b6c1-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b6c1-317">Başlatılan Çalıştır etkinliği</span><span class="sxs-lookup"><span data-stu-id="5b6c1-317">Activity Run Started</span></span> |<span data-ttu-id="5b6c1-318">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-318">Started</span></span> |<span data-ttu-id="5b6c1-319">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="5b6c1-319">Starting</span></span> |
| <span data-ttu-id="5b6c1-320">Tamamlanan etkinlik</span><span class="sxs-lookup"><span data-stu-id="5b6c1-320">Activity Run Finished</span></span> |<span data-ttu-id="5b6c1-321">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-321">Succeeded</span></span> |<span data-ttu-id="5b6c1-322">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-322">Succeeded</span></span> |
| <span data-ttu-id="5b6c1-323">Tamamlanan etkinlik</span><span class="sxs-lookup"><span data-stu-id="5b6c1-323">Activity Run Finished</span></span> |<span data-ttu-id="5b6c1-324">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-324">Failed</span></span> |<span data-ttu-id="5b6c1-325">Başarısız olan kaynak ayırma</span><span class="sxs-lookup"><span data-stu-id="5b6c1-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="5b6c1-326">Başarısız yürütme</span><span class="sxs-lookup"><span data-stu-id="5b6c1-326">Failed Execution</span></span><br/><br/><span data-ttu-id="5b6c1-327">Zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-327">Timed Out</span></span><br/><br/><span data-ttu-id="5b6c1-328">Başarısız doğrulamayı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-328">Failed Validation</span></span><br/><br/><span data-ttu-id="5b6c1-329">terk</span><span class="sxs-lookup"><span data-stu-id="5b6c1-329">Abandoned</span></span> |
| <span data-ttu-id="5b6c1-330">İsteğe bağlı HDI kümesi oluşturma başlatıldı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="5b6c1-331">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="5b6c1-331">Started</span></span> |-|
| <span data-ttu-id="5b6c1-332">İsteğe bağlı HDI kümesi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="5b6c1-333">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-333">Succeeded</span></span> |-|
| <span data-ttu-id="5b6c1-334">İsteğe bağlı HDI kümesi silindi</span><span class="sxs-lookup"><span data-stu-id="5b6c1-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="5b6c1-335">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="5b6c1-335">Succeeded</span></span> |-|

### <a name="to-edit-delete-or-disable-an-alert"></a><span data-ttu-id="5b6c1-336">Düzenleme, silme veya bir uyarıyı devre dışı bırakmak için</span><span class="sxs-lookup"><span data-stu-id="5b6c1-336">To edit, delete, or disable an alert</span></span>

<span data-ttu-id="5b6c1-337">Düzenleme, silme veya devre dışı bir uyarı (kırmızı ile vurgulanan) aşağıdaki düğmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b6c1-337">Use the following buttons (highlighted in red) to edit, delete, or disable an alert.</span></span>

![Uyarıları düğmeleri](./media/data-factory-monitor-manage-app/AlertButtons.png)
