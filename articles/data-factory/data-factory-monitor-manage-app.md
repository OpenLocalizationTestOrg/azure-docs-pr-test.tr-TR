---
title: "aaaMonitor ve veri ardışık - Azure yönetme | Microsoft Docs"
description: "Nasıl toouse izleme ve yönetim uygulaması toomonitor hello ve Azure data factory'leri ve ardışık düzen yönetmek öğrenin."
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
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a><span data-ttu-id="91cc0-103">İzleme ve hello izleme ve yönetim uygulaması kullanarak Azure Data Factory işlem hatlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="91cc0-103">Monitor and manage Azure Data Factory pipelines by using hello Monitoring and Management app</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91cc0-104">Azure portal/Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="91cc0-104">Using Azure portal/Azure PowerShell</span></span>](data-factory-monitor-manage-pipelines.md)
> * [<span data-ttu-id="91cc0-105">Kullanılarak izleme ve yönetim uygulaması</span><span class="sxs-lookup"><span data-stu-id="91cc0-105">Using Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)
>
>

<span data-ttu-id="91cc0-106">Bu makalede nasıl toouse izleme ve yönetim uygulaması toomonitor Merhaba, yönetmek ve Data Factory işlem hatlarınızı hata ayıklama açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-106">This article describes how toouse hello Monitoring and Management app toomonitor, manage, and debug your Data Factory pipelines.</span></span> <span data-ttu-id="91cc0-107">Toocreate hatalarında bildirim tooget nasıl uyarıları bilgi de sağlar.</span><span class="sxs-lookup"><span data-stu-id="91cc0-107">It also provides information on how toocreate alerts tooget notified on failures.</span></span> <span data-ttu-id="91cc0-108">Merhaba uygulaması tarafından izledikleri hello aşağıdaki video kullanmaya başlamak:</span><span class="sxs-lookup"><span data-stu-id="91cc0-108">You can get started with using hello application by watching hello following video:</span></span>

> [!NOTE]
> <span data-ttu-id="91cc0-109">hello Portalı'nda bkz Hello video gösterilen hello kullanıcı arabirimi tam olarak eşleşmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-109">hello user interface shown in hello video may not exactly match what you see in hello portal.</span></span> <span data-ttu-id="91cc0-110">Biraz daha eski olduğu, ancak kavramları kalır hello aynı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-110">It's slightly older, but concepts remain hello same.</span></span> 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a><span data-ttu-id="91cc0-111">Merhaba izleme ve yönetim uygulamasını başlatın</span><span class="sxs-lookup"><span data-stu-id="91cc0-111">Launch hello Monitoring and Management app</span></span>
<span data-ttu-id="91cc0-112">toolaunch hello izleme ve yönetim uygulaması hello'ı tıklatın **İzleyici & Yönet** döşeme hello üzerinde **Data Factory** veri fabrikanızın dikey.</span><span class="sxs-lookup"><span data-stu-id="91cc0-112">toolaunch hello Monitor and Management app, click hello **Monitor & Manage** tile on hello **Data Factory** blade for your data factory.</span></span>

![Döşeme hello Data Factory giriş sayfasında izleme](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

<span data-ttu-id="91cc0-114">Ayrı bir pencerede açmak hello izleme ve yönetim uygulaması görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-114">You should see hello Monitoring and Management app open in a separate window.</span></span>  

![İzleme ve Yönetim uygulaması](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> <span data-ttu-id="91cc0-116">Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, hello temizleyin **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** onay kutusu--veya seçili, Canlı oluşturmak için bir özel durum **login.microsoftonline.com** ve tooopen hello uygulama yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-116">If you see that hello web browser is stuck at "Authorizing...", clear hello **Block third-party cookies and site data** check box--or keep it selected, create an exception for **login.microsoftonline.com**, and then try tooopen hello app again.</span></span>


<span data-ttu-id="91cc0-117">Merhaba etkinlik Windows hello Orta bölmesindeki listesinde, her bir etkinlik çalışması için bir etkinlik penceresine bakın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-117">In hello Activity Windows list in hello middle pane, you see an activity window for each run of an activity.</span></span> <span data-ttu-id="91cc0-118">Örneğin, hello zamanlanan etkinlik toorun için beş saatten saatlik varsa, beş veri dilimi ile ilişkili beş etkinlik windows bakın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-118">For example, if you have hello activity scheduled toorun hourly for five hours, you see five activity windows associated with five data slices.</span></span> <span data-ttu-id="91cc0-119">Etkinlik windows hello altındaki hello listesinde görmüyorsanız, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="91cc0-119">If you don't see activity windows in hello list at hello bottom, do hello following:</span></span>
 
- <span data-ttu-id="91cc0-120">Güncelleştirme hello **başlangıç zamanı** ve **bitiş saati** hello üst toomatch hello filtreler başlangıç ve bitiş zamanları, ardışık ve hello ardından **Uygula** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-120">Update hello **start time** and **end time** filters at hello top toomatch hello start and end times of your pipeline, and then click hello **Apply** button.</span></span>  
- <span data-ttu-id="91cc0-121">Merhaba etkinlik Windows listesi otomatik olarak yenilenmez.</span><span class="sxs-lookup"><span data-stu-id="91cc0-121">hello Activity Windows list is not automatically refreshed.</span></span> <span data-ttu-id="91cc0-122">Merhaba tıklatın **yenileme** hello hello araç çubuğundan düğme **etkinlik Windows** listesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-122">Click hello **Refresh** button on hello toolbar in hello **Activity Windows** list.</span></span>  

<span data-ttu-id="91cc0-123">Bu adımları bir Data Factory uygulama tootest yoksa, öğretici hello: [veritabanını Data Factory kullanarak Blob Storage tooSQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="91cc0-123">If you don't have a Data Factory application tootest these steps with, do hello tutorial: [copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="understand-hello-monitoring-and-management-app"></a><span data-ttu-id="91cc0-124">Merhaba izleme ve yönetim uygulaması anlama</span><span class="sxs-lookup"><span data-stu-id="91cc0-124">Understand hello Monitoring and Management app</span></span>
<span data-ttu-id="91cc0-125">Merhaba soldaki üç sekme vardır: **kaynak Gezgini**, **izleme görünümleri**, ve **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-125">There are three tabs on hello left: **Resource Explorer**, **Monitoring Views**, and **Alerts**.</span></span> <span data-ttu-id="91cc0-126">Merhaba ilk sekme (**kaynak Gezgini**) varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-126">hello first tab (**Resource Explorer**) is selected by default.</span></span>

### <a name="resource-explorer"></a><span data-ttu-id="91cc0-127">Kaynak Gezgini</span><span class="sxs-lookup"><span data-stu-id="91cc0-127">Resource Explorer</span></span>
<span data-ttu-id="91cc0-128">Merhaba aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="91cc0-128">You see hello following:</span></span>

* <span data-ttu-id="91cc0-129">Merhaba kaynak Gezgini **ağaç görünümü** hello sol bölmede.</span><span class="sxs-lookup"><span data-stu-id="91cc0-129">hello Resource Explorer **tree view** in hello left pane.</span></span>
* <span data-ttu-id="91cc0-130">Merhaba **diyagram görünümü** hello orta bölmesinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="91cc0-130">hello **Diagram View** at hello top in hello middle pane.</span></span>
* <span data-ttu-id="91cc0-131">Merhaba **etkinlik Windows** hello orta bölmesinde hello altındaki listesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-131">hello **Activity Windows** list at hello bottom in hello middle pane.</span></span>
* <span data-ttu-id="91cc0-132">Merhaba **özellikleri**, **etkinlik penceresini Explorer**, ve **betik** hello sağ bölmedeki sekmeleri.</span><span class="sxs-lookup"><span data-stu-id="91cc0-132">hello **Properties**, **Activity Window Explorer**, and **Script** tabs in hello right pane.</span></span>

<span data-ttu-id="91cc0-133">Kaynak Gezgini, ağaç görünümünde hello veri fabrikasında tüm kaynakları (komut zincirleri, veri kümeleri, bağlı hizmetler) bakın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-133">In Resource Explorer, you see all resources (pipelines, datasets, linked services) in hello data factory in a tree view.</span></span> <span data-ttu-id="91cc0-134">Ne zaman kaynak Gezgini, bir nesne seçin:</span><span class="sxs-lookup"><span data-stu-id="91cc0-134">When you select an object in Resource Explorer:</span></span>

* <span data-ttu-id="91cc0-135">Merhaba Data Factory varlığı hello diyagram görünümü vurgulanan ilişkili.</span><span class="sxs-lookup"><span data-stu-id="91cc0-135">hello associated Data Factory entity is highlighted in hello Diagram View.</span></span>
* <span data-ttu-id="91cc0-136">[Etkinlik pencerelerine ilişkili](data-factory-scheduling-and-execution.md) hello altındaki hello etkinlik Windows listesinde vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-136">[Associated activity windows](data-factory-scheduling-and-execution.md) are highlighted in hello Activity Windows list at hello bottom.</span></span>  
* <span data-ttu-id="91cc0-137">Merhaba hello seçili nesnenin özelliklerini hello Özellikler penceresinde hello sağ bölmede gösterilir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-137">hello properties of hello selected object are shown in hello Properties window in hello right pane.</span></span>
* <span data-ttu-id="91cc0-138">Merhaba hello seçili nesnenin JSON tanımını gösterilir, varsa.</span><span class="sxs-lookup"><span data-stu-id="91cc0-138">hello JSON definition of hello selected object is shown, if applicable.</span></span> <span data-ttu-id="91cc0-139">Örneğin: bağlı hizmet, bir veri kümesi veya işlem hattı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-139">For example: a linked service, a dataset, or a pipeline.</span></span>

![Kaynak Gezgini](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

<span data-ttu-id="91cc0-141">Merhaba bkz [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) etkinlik windows hakkında ayrıntılı kavramsal bilgi için makalenin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-141">See hello [Scheduling and Execution](data-factory-scheduling-and-execution.md) article for detailed conceptual information about activity windows.</span></span>

### <a name="diagram-view"></a><span data-ttu-id="91cc0-142">Diyagram Görünümü</span><span class="sxs-lookup"><span data-stu-id="91cc0-142">Diagram View</span></span>
<span data-ttu-id="91cc0-143">Hello diyagram görünümü veri fabrikasının bölmeden cam toomonitor sağlar ve bir veri fabrikası ve varlıklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-143">hello Diagram View of a data factory provides a single pane of glass toomonitor and manage a data factory and its assets.</span></span> <span data-ttu-id="91cc0-144">Ne zaman bir Data Factory varlığı (dataset/ardışık düzeni) hello diyagram görünümü seçin:</span><span class="sxs-lookup"><span data-stu-id="91cc0-144">When you select a Data Factory entity (dataset/pipeline) in hello Diagram View:</span></span>

* <span data-ttu-id="91cc0-145">Merhaba veri fabrikası varlık hello ağaç görünümünde seçilir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-145">hello data factory entity is selected in hello tree view.</span></span>
* <span data-ttu-id="91cc0-146">Merhaba, windows hello etkinlik Windows listesinde vurgulanan etkinlik ilişkili.</span><span class="sxs-lookup"><span data-stu-id="91cc0-146">hello associated activity windows are highlighted in hello Activity Windows list.</span></span>
* <span data-ttu-id="91cc0-147">Hello hello seçili nesnenin özelliklerini hello Özellikleri penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-147">hello properties of hello selected object are shown in hello Properties window.</span></span>

<span data-ttu-id="91cc0-148">Merhaba ardışık düzen (duraklatılmış durumda değil) etkin olduğunda, yeşil bir çizgiyle gösterilir:</span><span class="sxs-lookup"><span data-stu-id="91cc0-148">When hello pipeline is enabled (not in a paused state), it's shown with a green line:</span></span>

![Çalışan işlem hattı](./media/data-factory-monitor-manage-app/PipelineRunning.png)

<span data-ttu-id="91cc0-150">Duraklatma, sürdürme veya hello diyagram görünümünde seçerek ve hello komut çubuğunda hello düğmelerini kullanarak bir ardışık düzen sonlandırmak.</span><span class="sxs-lookup"><span data-stu-id="91cc0-150">You can pause, resume, or terminate a pipeline by selecting it in hello diagram view and using hello buttons on hello command bar.</span></span>

![Merhaba komut çubuğunda Duraklat/Sürdür](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
<span data-ttu-id="91cc0-152">Merhaba ardışık düzeninde hello diyagram görünümü için üç komut çubuğu düğmelerini vardır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-152">There are three command bar buttons for hello pipeline in hello Diagram View.</span></span> <span data-ttu-id="91cc0-153">Merhaba ikinci düğme toopause hello ardışık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-153">You can use hello second button toopause hello pipeline.</span></span> <span data-ttu-id="91cc0-154">Duraklatma etkinliklerini çalışmakta hello sonlandırmak değil ve bunları toocompletion devam olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-154">Pausing doesn't terminate hello currently running activities and lets them proceed toocompletion.</span></span> <span data-ttu-id="91cc0-155">Merhaba üçüncü düğme hello ardışık düzen duraklatır ve kendi etkinlikleri yürütme varolan sona erer.</span><span class="sxs-lookup"><span data-stu-id="91cc0-155">hello third button pauses hello pipeline and terminates its existing executing activities.</span></span> <span data-ttu-id="91cc0-156">Merhaba ilk düğme hello ardışık düzen sürdürür.</span><span class="sxs-lookup"><span data-stu-id="91cc0-156">hello first button resumes hello pipeline.</span></span> <span data-ttu-id="91cc0-157">İşlem hattınızı duraklatıldığında hello ardışık hello rengi değişir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-157">When your pipeline is paused, hello color of hello pipeline changes.</span></span> <span data-ttu-id="91cc0-158">Örneğin, duraklatılmış bir ardışık düzen görüntü aşağıdaki hello şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="91cc0-158">For example, a paused pipeline looks like in hello following image:</span></span> 

![Ardışık Düzen duraklatıldı](./media/data-factory-monitor-manage-app/PipelinePaused.png)

<span data-ttu-id="91cc0-160">Çoklu seçim iki veya daha fazla ardışık düzen hello Ctrl tuşunu kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-160">You can multi-select two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="91cc0-161">Aynı anda birden çok ardışık düzen hello komut çubuğu düğmelerini toopause/sürdürmeden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-161">You can use hello command bar buttons toopause/resume multiple pipelines at a time.</span></span>

<span data-ttu-id="91cc0-162">Ayrıca sağ ardışık düzen ve seçenekleri belirleyin toosuspend sürdürün veya bir işlem hattı sonlandırılacak.</span><span class="sxs-lookup"><span data-stu-id="91cc0-162">You can also right-click a pipeline and select options toosuspend, resume, or terminate a pipeline.</span></span> 

![Ardışık düzeni için bağlam menüsü](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

<span data-ttu-id="91cc0-164">Merhaba tıklatın **açık işlem hattı** hello ardışık düzende tüm hello etkinlik toosee seçeneği.</span><span class="sxs-lookup"><span data-stu-id="91cc0-164">Click hello **Open pipeline** option toosee all hello activities in hello pipeline.</span></span> 

![İşlem hattı menüsünü açma](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

<span data-ttu-id="91cc0-166">Açılan hello ardışık düzen Görünümü'nde hello ardışık düzende tüm etkinlik bakın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-166">In hello opened pipeline view, you see all activities in hello pipeline.</span></span> <span data-ttu-id="91cc0-167">Bu örnekte, yalnızca bir etkinlik yok: kopyalama etkinliği.</span><span class="sxs-lookup"><span data-stu-id="91cc0-167">In this example, there is only one activity: Copy Activity.</span></span> 

![Açılan ardışık düzen](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

<span data-ttu-id="91cc0-169">toogo toohello önceki görünüme geri hello veri fabrikası adı hello üstünde hello içerik haritası menüsünde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-169">toogo back toohello previous view, click hello data factory name in hello breadcrumb menu at hello top.</span></span>

<span data-ttu-id="91cc0-170">Bir çıkış veri kümesi veya hello çıktı veri kümesi üzerinde farenizi taşıdığınızda seçtiğinizde hello ardışık düzen görünümünde bu veri kümesi için hello etkinlik Windows açılır pencere görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-170">In hello pipeline view, when you select an output dataset or when you move your mouse over hello output dataset, you see hello Activity Windows pop-up window for that dataset.</span></span>

![Etkinlik Windows açılır penceresi](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

<span data-ttu-id="91cc0-172">Hello bir etkinlik penceresini toosee ayrıntıları tıklattığınız **özellikleri** hello sağ bölmedeki penceresi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-172">You can click an activity window toosee details for it in hello **Properties** window in hello right pane.</span></span>

![Etkinlik penceresini özellikleri](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

<span data-ttu-id="91cc0-174">Merhaba sağ bölmede, toohello geçiş **etkinlik penceresini Explorer** toosee Ayrıntılar sekmesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-174">In hello right pane, switch toohello **Activity Window Explorer** tab toosee more details.</span></span>

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

<span data-ttu-id="91cc0-176">Ayrıca bkz: **değişkenleri çözülmüş** hello bir etkinliğin her çalıştırma denemesi için **denemeleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="91cc0-176">You also see **resolved variables** for each run attempt for an activity in hello **Attempts** section.</span></span>

![Çözümlenen değişkenleri](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

<span data-ttu-id="91cc0-178">Geçiş toohello **betik** sekmesinde hello seçili nesne için toosee hello JSON betik tanımı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-178">Switch toohello **Script** tab toosee hello JSON script definition for hello selected object.</span></span>   

![Komut dosyası sekmesi](./media/data-factory-monitor-manage-app/ScriptTab.png)

<span data-ttu-id="91cc0-180">Etkinlik pencerelerine üç yerde görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="91cc0-180">You can see activity windows in three places:</span></span>

* <span data-ttu-id="91cc0-181">Merhaba etkinlik Windows hello diyagram görünümü (Orta bölme) açılır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-181">hello Activity Windows pop-up in hello Diagram View (middle pane).</span></span>
* <span data-ttu-id="91cc0-182">Etkinlik penceresini Explorer Hello hello sağ bölmedeki.</span><span class="sxs-lookup"><span data-stu-id="91cc0-182">hello Activity Window Explorer in hello right pane.</span></span>
* <span data-ttu-id="91cc0-183">Merhaba alt bölmesinde Hello etkinlik Windows listesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-183">hello Activity Windows list in hello bottom pane.</span></span>

<span data-ttu-id="91cc0-184">Hello etkinlik Windows açılır ve etkinlik penceresini Gezgini'nde, önceki hafta toohello kaydırın ve hello kullanarak sonraki hafta hello sol ve sağ ok.</span><span class="sxs-lookup"><span data-stu-id="91cc0-184">In hello Activity Windows pop-up and Activity Window Explorer, you can scroll toohello previous week and hello next week by using hello left and right arrows.</span></span>

![Etkinlik penceresini Explorer sol/sağ ok](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

<span data-ttu-id="91cc0-186">Merhaba diyagram görünümü Hello kısımda bu düğmeleri Bkz: yakınlaştırma, uzaklaştırma, yakınlaştırma tooFit yakınlaştırma % 100, kilit düzeni.</span><span class="sxs-lookup"><span data-stu-id="91cc0-186">At hello bottom of hello Diagram View, you see these buttons: Zoom In, Zoom Out, Zoom tooFit, Zoom 100%, Lock layout.</span></span> <span data-ttu-id="91cc0-187">Merhaba **kilit düzeni** düğmesi önler yanlışlıkla tablolar ve ardışık düzen hello diyagram görünümü taşınmasını.</span><span class="sxs-lookup"><span data-stu-id="91cc0-187">hello **Lock layout** button prevents you from accidentally moving tables and pipelines in hello Diagram View.</span></span> <span data-ttu-id="91cc0-188">Bu varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-188">It's on by default.</span></span> <span data-ttu-id="91cc0-189">Uygulamayı kapatın ve varlıkları hello diyagramında hareket ettirin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-189">You can turn it off and move entities around in hello diagram.</span></span> <span data-ttu-id="91cc0-190">Devre dışı bıraktığınızda, hello Son düğmesine tooautomatically konumu tablolar ve ardışık düzen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-190">When you turn it off, you can use hello last button tooautomatically position tables and pipelines.</span></span> <span data-ttu-id="91cc0-191">Giriş veya çıkış hello fare tekerleği kullanarak da yakınlaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-191">You can also zoom in or out by using hello mouse wheel.</span></span>

![Diyagram görünümü yakınlaştırma komutları](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a><span data-ttu-id="91cc0-193">Etkinlik Windows listesi</span><span class="sxs-lookup"><span data-stu-id="91cc0-193">Activity Windows list</span></span>
<span data-ttu-id="91cc0-194">Merhaba etkinlik Windows hello orta bölmesinde hello altındaki tüm etkinlik windows hello kaynak Gezgini veya hello diyagram görünümü seçili hello veri kümesi için görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91cc0-194">hello Activity Windows list at hello bottom of hello middle pane displays all activity windows for hello dataset that you selected in hello Resource Explorer or hello Diagram View.</span></span> <span data-ttu-id="91cc0-195">Varsayılan olarak, hello hello son etkinlik penceresini hello üstünde görmek anlamına gelir, azalan sırada listesidir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-195">By default, hello list is in descending order, which means that you see hello latest activity window at hello top.</span></span>

![Etkinlik Windows listesi](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

<span data-ttu-id="91cc0-197">Bu liste, kullanım hello Yenile düğmesini hello araç toomanually üzerinde yenilemek için otomatik olarak yenilenmez.</span><span class="sxs-lookup"><span data-stu-id="91cc0-197">This list doesn't refresh automatically, so use hello refresh button on hello toolbar toomanually refresh it.</span></span>  

<span data-ttu-id="91cc0-198">Etkinlik windows hello durumları aşağıdaki biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="91cc0-198">Activity windows can be in one of hello following statuses:</span></span>

<table>
<tr>
    <th align="left"><span data-ttu-id="91cc0-199">Durum</span><span class="sxs-lookup"><span data-stu-id="91cc0-199">Status</span></span></th><th align="left"><span data-ttu-id="91cc0-200">Alt durum</span><span class="sxs-lookup"><span data-stu-id="91cc0-200">Substatus</span></span></th><th align="left"><span data-ttu-id="91cc0-201">Açıklama</span><span class="sxs-lookup"><span data-stu-id="91cc0-201">Description</span></span></th>
</tr>
<tr>
    <td rowspan="8"><span data-ttu-id="91cc0-202">Bekleniyor</span><span class="sxs-lookup"><span data-stu-id="91cc0-202">Waiting</span></span></td><td><span data-ttu-id="91cc0-203">ScheduleTime</span><span class="sxs-lookup"><span data-stu-id="91cc0-203">ScheduleTime</span></span></td><td><span data-ttu-id="91cc0-204">Başlangıç saati hello etkinlik penceresini toorun için gelen kurmadı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-204">hello time hasn't come for hello activity window toorun.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-205">DatasetDependencies</span><span class="sxs-lookup"><span data-stu-id="91cc0-205">DatasetDependencies</span></span></td><td><span data-ttu-id="91cc0-206">Merhaba Yukarı Akış bağımlılıkları hazır değil.</span><span class="sxs-lookup"><span data-stu-id="91cc0-206">hello upstream dependencies aren't ready.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-207">ComputeResources</span><span class="sxs-lookup"><span data-stu-id="91cc0-207">ComputeResources</span></span></td><td><span data-ttu-id="91cc0-208">Merhaba işlem kaynakları kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="91cc0-208">hello compute resources aren't available.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-209">ConcurrencyLimit</span><span class="sxs-lookup"><span data-stu-id="91cc0-209">ConcurrencyLimit</span></span></td> <td><span data-ttu-id="91cc0-210">Tüm hello etkinlik örnekleri diğer etkinlik windows çalıştıran meşgul.</span><span class="sxs-lookup"><span data-stu-id="91cc0-210">All hello activity instances are busy running other activity windows.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-211">ActivityResume</span><span class="sxs-lookup"><span data-stu-id="91cc0-211">ActivityResume</span></span></td><td><span data-ttu-id="91cc0-212">Merhaba etkinlik duraklatıldı ve sürdürülene kadar hello etkinlik windows çalıştıramaz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-212">hello activity is paused and can't run hello activity windows until it's resumed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-213">Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="91cc0-213">Retry</span></span></td><td><span data-ttu-id="91cc0-214">Merhaba Etkinlik yürütme yeniden deneniyor.</span><span class="sxs-lookup"><span data-stu-id="91cc0-214">hello activity execution is being retried.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-215">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="91cc0-215">Validation</span></span></td><td><span data-ttu-id="91cc0-216">Doğrulama henüz başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-216">Validation hasn't started yet.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-217">ValidationRetry</span><span class="sxs-lookup"><span data-stu-id="91cc0-217">ValidationRetry</span></span></td><td><span data-ttu-id="91cc0-218">Doğrulama denenen bekleme toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-218">Validation is waiting toobe retried.</span></span></td>
</tr>
<tr>
<tr>
<td rowspan="2"><span data-ttu-id="91cc0-219">Devam ediyor</span><span class="sxs-lookup"><span data-stu-id="91cc0-219">InProgress</span></span></td><td><span data-ttu-id="91cc0-220">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="91cc0-220">Validating</span></span></td><td><span data-ttu-id="91cc0-221">Doğrulama devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="91cc0-221">Validation is in progress.</span></span></td>
</tr>
<td>-</td>
<td><span data-ttu-id="91cc0-222">Merhaba etkinlik penceresini işleniyor.</span><span class="sxs-lookup"><span data-stu-id="91cc0-222">hello activity window is being processed.</span></span></td>
</tr>
<tr>
<td rowspan="4"><span data-ttu-id="91cc0-223">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-223">Failed</span></span></td><td><span data-ttu-id="91cc0-224">Süresi sona erdi</span><span class="sxs-lookup"><span data-stu-id="91cc0-224">TimedOut</span></span></td><td><span data-ttu-id="91cc0-225">Merhaba Etkinlik yürütme hello etkinliği tarafından izin daha uzun sürdü.</span><span class="sxs-lookup"><span data-stu-id="91cc0-225">hello activity execution took longer than what is allowed by hello activity.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-226">İptal edildi</span><span class="sxs-lookup"><span data-stu-id="91cc0-226">Canceled</span></span></td><td><span data-ttu-id="91cc0-227">Merhaba etkinlik penceresini kullanıcı eylemi tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-227">hello activity window was canceled by user action.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-228">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="91cc0-228">Validation</span></span></td><td><span data-ttu-id="91cc0-229">Doğrulama başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="91cc0-229">Validation has failed.</span></span></td>
</tr>
<tr>
<td>-</td><td><span data-ttu-id="91cc0-230">Merhaba etkinlik penceresini oluşturulan veya doğrulanmamış toobe başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="91cc0-230">hello activity window failed toobe generated or validated.</span></span></td>
</tr>
<td><span data-ttu-id="91cc0-231">Hazır</span><span class="sxs-lookup"><span data-stu-id="91cc0-231">Ready</span></span></td><td>-</td><td><span data-ttu-id="91cc0-232">Merhaba etkinlik penceresini tüketimi için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-232">hello activity window is ready for consumption.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-233">Atlandı</span><span class="sxs-lookup"><span data-stu-id="91cc0-233">Skipped</span></span></td><td>-</td><td><span data-ttu-id="91cc0-234">Merhaba etkinlik penceresini işlenen değildi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-234">hello activity window wasn't processed.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="91cc0-235">None</span><span class="sxs-lookup"><span data-stu-id="91cc0-235">None</span></span></td><td>-</td><td><span data-ttu-id="91cc0-236">Bir etkinlik penceresi tooexist farklı bir durum ile kullanılan ancak sıfırlandı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-236">An activity window used tooexist with a different status, but has been reset.</span></span></td>
</tr>
</table>


<span data-ttu-id="91cc0-237">Merhaba listesi etkinliği penceresindeki tıklattığınızda hello onunla ilgili ayrıntıları görürsünüz **etkinlik Windows Explorer** veya hello **özellikleri** penceresinde hello sağ.</span><span class="sxs-lookup"><span data-stu-id="91cc0-237">When you click an activity window in hello list, you see details about it in hello **Activity Windows Explorer** or hello **Properties** window on hello right.</span></span>

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a><span data-ttu-id="91cc0-239">Etkinlik pencerelerine Yenile</span><span class="sxs-lookup"><span data-stu-id="91cc0-239">Refresh activity windows</span></span>
<span data-ttu-id="91cc0-240">Merhaba ayrıntıları otomatik olarak yenilenir değil, bu nedenle toomanually yenileme hello etkinlik windows listesi çubuğu hello komutunda hello Yenile düğmesini (Merhaba ikinci düğme) kullanın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-240">hello details aren't automatically refreshed, so use hello refresh button (hello second button) on hello command bar toomanually refresh hello activity windows list.</span></span>  

### <a name="properties-window"></a><span data-ttu-id="91cc0-241">Özellik penceresi</span><span class="sxs-lookup"><span data-stu-id="91cc0-241">Properties window</span></span>
<span data-ttu-id="91cc0-242">Merhaba Özellikleri penceresinde hello en sağ bölmesinde hello izleme ve yönetim uygulaması bulunur.</span><span class="sxs-lookup"><span data-stu-id="91cc0-242">hello Properties window is in hello right-most pane of hello Monitoring and Management app.</span></span>

![Özellik penceresi](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

<span data-ttu-id="91cc0-244">Merhaba kaynak Gezgini (ağaç görünümü) seçili hello öğenin özelliklerini görüntüler diyagram görünümü veya etkinlik Windows listesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-244">It displays properties for hello item that you selected in hello Resource Explorer (tree view), Diagram View, or Activity Windows list.</span></span>

### <a name="activity-window-explorer"></a><span data-ttu-id="91cc0-245">Etkinlik penceresini Gezgini</span><span class="sxs-lookup"><span data-stu-id="91cc0-245">Activity Window Explorer</span></span>
<span data-ttu-id="91cc0-246">Merhaba **etkinlik penceresini Explorer** ' hello izleme ve yönetim uygulaması hello en sağ bölmesinde bir penceredir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-246">hello **Activity Window Explorer** window is in hello right-most pane of hello Monitoring and Management app.</span></span> <span data-ttu-id="91cc0-247">Merhaba etkinlik Windows açılır penceresi veya hello etkinlik Windows listedeki seçili hello etkinlik penceresini hakkındaki ayrıntıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91cc0-247">It displays details about hello activity window that you selected in hello Activity Windows pop-up window or hello Activity Windows list.</span></span>

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

<span data-ttu-id="91cc0-249">Merhaba üstünde hello Takvim görünümünde tıklatarak tooanother faaliyet penceresi arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-249">You can switch tooanother activity window by clicking it in hello calendar view at hello top.</span></span> <span data-ttu-id="91cc0-250">Ayrıca, önceki hafta hello üst toosee etkinlik windows hello adresindeki hello sol ok/sağ ok düğmelerini kullanın veya sonraki hafta hello.</span><span class="sxs-lookup"><span data-stu-id="91cc0-250">You can also use hello left arrow/right arrow buttons at hello top toosee activity windows from hello previous week or hello next week.</span></span>

<span data-ttu-id="91cc0-251">Merhaba alt bölmesinde toorerun hello etkinlik penceresinde hello araç çubuğu düğmelerini kullanın veya hello bölmesini hello ayrıntılarında yenileyin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-251">You can use hello toolbar buttons in hello bottom pane toorerun hello activity window or refresh hello details in hello pane.</span></span>

### <a name="script"></a><span data-ttu-id="91cc0-252">Betik</span><span class="sxs-lookup"><span data-stu-id="91cc0-252">Script</span></span>
<span data-ttu-id="91cc0-253">Merhaba kullanabilirsiniz **betik** sekmesini tooview hello hello JSON tanımını seçili Data Factory varlığı (bağlı hizmet, veri kümesi veya işlem hattı).</span><span class="sxs-lookup"><span data-stu-id="91cc0-253">You can use hello **Script** tab tooview hello JSON definition of hello selected Data Factory entity (linked service, dataset, or pipeline).</span></span>

![Komut dosyası sekmesi](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a><span data-ttu-id="91cc0-255">Sistem görünümleri kullanma</span><span class="sxs-lookup"><span data-stu-id="91cc0-255">Use system views</span></span>
<span data-ttu-id="91cc0-256">Merhaba izleme ve yönetim uygulamasını içeren önceden derlenmiş sistem görünümleri (**son etkinlik windows**, **başarısız etkinliği windows**, **ilerleme durumu etkinlik windows**), Veri fabrikanızın tooview son/başarısız/Süren etkinlik pencerelerine izin verin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-256">hello Monitoring and Management app includes pre-built system views (**Recent activity windows**, **Failed activity windows**, **In-Progress activity windows**) that allow you tooview recent/failed/in-progress activity windows for your data factory.</span></span>

<span data-ttu-id="91cc0-257">Geçiş toohello **izleme görünümleri** tıklatarak hello sol sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="91cc0-257">Switch toohello **Monitoring Views** tab on hello left by clicking it.</span></span>

![İzleme görünümleri sekmesi](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

<span data-ttu-id="91cc0-259">Şu anda desteklenen üç sistem görünümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-259">Currently, there are three system views that are supported.</span></span> <span data-ttu-id="91cc0-260">Bir seçenek toosee seçin son etkinlik windows, başarısız olan etkinliği windows veya devam eden etkinlik windows hello etkinlik Windows listesinde (sonundaki hello hello orta bölmesinde).</span><span class="sxs-lookup"><span data-stu-id="91cc0-260">Select an option toosee recent activity windows, failed activity windows, or in-progress activity windows in hello Activity Windows list (at hello bottom of hello middle pane).</span></span>

<span data-ttu-id="91cc0-261">Merhaba seçtiğinizde **son etkinlik windows** seçeneği, gördüğünüz hello azalan tüm son etkinlik windows **zaman'son deneme**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-261">When you select hello **Recent activity windows** option, you see all recent activity windows in descending order of hello **last attempt time**.</span></span>

<span data-ttu-id="91cc0-262">Merhaba kullanabilirsiniz **başarısız etkinliği windows** toosee tüm başarısız etkinliği windows hello listesinde görüntülemek.</span><span class="sxs-lookup"><span data-stu-id="91cc0-262">You can use hello **Failed activity windows** view toosee all failed activity windows in hello list.</span></span> <span data-ttu-id="91cc0-263">Itanium tabanlı sistemler için hello listesi toosee ayrıntıları ilgili hello içinde başarısız olan etkinliği penceresi seçin **özellikleri** penceresi veya hello **etkinlik penceresini Explorer**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-263">Select a failed activity window in hello list toosee details about it in hello **Properties** window or hello **Activity Window Explorer**.</span></span> <span data-ttu-id="91cc0-264">Ayrıca, başarısız olan etkinliği penceresi için herhangi bir günlük indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-264">You can also download any logs for a failed activity window.</span></span>

## <a name="sort-and-filter-activity-windows"></a><span data-ttu-id="91cc0-265">Sıralama ve filtreleme etkinliği windows</span><span class="sxs-lookup"><span data-stu-id="91cc0-265">Sort and filter activity windows</span></span>
<span data-ttu-id="91cc0-266">Değişiklik hello **başlangıç zamanı** ve **bitiş saati** hello komut çubuğu toofilter etkinlik pencereleri ayarlarında.</span><span class="sxs-lookup"><span data-stu-id="91cc0-266">Change hello **start time** and **end time** settings in hello command bar toofilter activity windows.</span></span> <span data-ttu-id="91cc0-267">Hello başlangıç ve bitiş zamanı değiştirdikten sonra hello düğmesi sonraki toohello bitiş saati toorefresh hello etkinlik Windows listesi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-267">After you change hello start time and end time, click hello button next toohello end time toorefresh hello Activity Windows list.</span></span>

![Başlangıç ve bitiş zamanlarını](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> <span data-ttu-id="91cc0-269">Şu anda tüm saatler UTC biçiminde hello izleme ve yönetim uygulaması arasındadır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-269">Currently, all times are in UTC format in hello Monitoring and Management app.</span></span>
>
>

<span data-ttu-id="91cc0-270">Merhaba, **etkinlik Windows listesi**, bir sütun hello adına tıklayın (örneğin: durum).</span><span class="sxs-lookup"><span data-stu-id="91cc0-270">In hello **Activity Windows list**, click hello name of a column (for example: Status).</span></span>

![Etkinlik Windows liste sütun menüsü](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

<span data-ttu-id="91cc0-272">Yapabileceğiniz hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="91cc0-272">You can do hello following:</span></span>

* <span data-ttu-id="91cc0-273">Artan sırada Sırala.</span><span class="sxs-lookup"><span data-stu-id="91cc0-273">Sort in ascending order.</span></span>
* <span data-ttu-id="91cc0-274">Azalan sırada sıralayın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-274">Sort in descending order.</span></span>
* <span data-ttu-id="91cc0-275">Bir veya daha fazla değerlerle (hazır, bekliyor vb.) filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="91cc0-275">Filter by one or more values (Ready, Waiting, and so on).</span></span>

<span data-ttu-id="91cc0-276">Bir sütunda bir filtre belirttiğinizde, filtrelenmiş değerleri hello sütundaki hello değerleri gösterir bu sütun için etkin hello filtre düğmesini bakın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-276">When you specify a filter on a column, you see hello filter button enabled for that column, which indicates that hello values in hello column are filtered values.</span></span>

![Merhaba etkinlik Windows listesinin bir sütuna filtre](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

<span data-ttu-id="91cc0-278">Kullanabileceğiniz hello aynı açılır pencere tooclear filtreler.</span><span class="sxs-lookup"><span data-stu-id="91cc0-278">You can use hello same pop-up window tooclear filters.</span></span> <span data-ttu-id="91cc0-279">tüm filtreleri hello etkinlik Windows listesi için tooclear hello komut çubuğunda hello filtreyi düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-279">tooclear all filters for hello Activity Windows list, click hello clear filter button on hello command bar.</span></span>

![Merhaba etkinlik Windows listesi için tüm filtreleri temizlemek](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a><span data-ttu-id="91cc0-281">Toplu işlemleri</span><span class="sxs-lookup"><span data-stu-id="91cc0-281">Perform batch actions</span></span>
### <a name="rerun-selected-activity-windows"></a><span data-ttu-id="91cc0-282">Seçili etkinlik windows yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="91cc0-282">Rerun selected activity windows</span></span>
<span data-ttu-id="91cc0-283">Bir etkinlik penceresi seçin, aşağı ok hello ilk komut çubuğu düğmesi için hello tıklatın ve seçin **yeniden Çalıştır** / **ile upstream ardışık düzeninde yeniden**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-283">Select an activity window, click hello down arrow for hello first command bar button, and select **Rerun** / **Rerun with upstream in pipeline**.</span></span> <span data-ttu-id="91cc0-284">Merhaba seçtiğinizde **ile upstream ardışık düzeninde yeniden** seçeneği, tüm Yukarı Akış etkinliği windows de yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="91cc0-284">When you select hello **Rerun with upstream in pipeline** option, it reruns all upstream activity windows as well.</span></span>
    <span data-ttu-id="91cc0-285">![Bir etkinlik penceresi yeniden](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span><span class="sxs-lookup"><span data-stu-id="91cc0-285">![Rerun an activity window](./media/data-factory-monitor-manage-app/ReRunSlice.png)</span></span>

<span data-ttu-id="91cc0-286">Ayrıca birden çok etkinlik windows hello listesinden seçin ve hello yeniden aynı anda.</span><span class="sxs-lookup"><span data-stu-id="91cc0-286">You can also select multiple activity windows in hello list and rerun them at hello same time.</span></span> <span data-ttu-id="91cc0-287">Toofilter etkinlik windows hello durumlarına dayalı isteyebilirsiniz (örneğin: **başarısız**)--ve başarısız hello etkinlik windows hello etkinlik windows toofail neden hello sorunu düzelttikten sonra yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-287">You might want toofilter activity windows based on hello status (for example: **Failed**)--and then rerun hello failed activity windows after correcting hello issue that causes hello activity windows toofail.</span></span> <span data-ttu-id="91cc0-288">Merhaba bölümden etkinlik windows hello listesinde filtreleme hakkında ayrıntılar için bkz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-288">See hello following section for details about filtering activity windows in hello list.</span></span>  

### <a name="pauseresume-multiple-pipelines"></a><span data-ttu-id="91cc0-289">Birden çok ardışık düzen Duraklat/Sürdür</span><span class="sxs-lookup"><span data-stu-id="91cc0-289">Pause/resume multiple pipelines</span></span>
<span data-ttu-id="91cc0-290">Çoklu iki veya daha fazla ardışık düzen hello Ctrl tuşunu kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-290">You can multiselect two or more pipelines by using hello Ctrl key.</span></span> <span data-ttu-id="91cc0-291">(Hangi görüntü aşağıdaki hello hello kırmızı dikdörtgende içinde vurgulanır) hello komut çubuğu düğmelerini kullanabilirsiniz toopause/sürdürmeden bunları.</span><span class="sxs-lookup"><span data-stu-id="91cc0-291">You can use hello command bar buttons (which are highlighted in hello red rectangle in hello following image) toopause/resume them.</span></span>

![Merhaba komut çubuğunda Duraklat/Sürdür](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a><span data-ttu-id="91cc0-293">Uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91cc0-293">Create alerts</span></span>
<span data-ttu-id="91cc0-294">Merhaba **uyarıları** sayfası, bir uyarı ve görünüm/düzenleme/silme mevcut uyarıları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="91cc0-294">hello **Alerts** page lets you create an alert and view/edit/delete existing alerts.</span></span> <span data-ttu-id="91cc0-295">Sizin de devre dışı bırak/uyarı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91cc0-295">You can also disable/enable an alert.</span></span> <span data-ttu-id="91cc0-296">toosee uyarılar sayfasında Merhaba, hello tıklatın **uyarıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="91cc0-296">toosee hello Alerts page, click hello **Alerts** tab.</span></span>

![Uyarılar sekmesi](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a><span data-ttu-id="91cc0-298">toocreate bir uyarı</span><span class="sxs-lookup"><span data-stu-id="91cc0-298">toocreate an alert</span></span>
1. <span data-ttu-id="91cc0-299">Tıklatın **eklemek uyarı** tooadd bir uyarı.</span><span class="sxs-lookup"><span data-stu-id="91cc0-299">Click **Add Alert** tooadd an alert.</span></span> <span data-ttu-id="91cc0-300">Merhaba gördüğünüz **ayrıntıları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="91cc0-300">You see hello **Details** page.</span></span>

    ![Uyarılar - ayrıntılar sayfası oluşturma](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. <span data-ttu-id="91cc0-302">Merhaba belirtin **adı** ve **açıklama** tıklatın ve hello uyarı için **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-302">Specify hello **Name** and **Description** for hello alert, and click **Next**.</span></span> <span data-ttu-id="91cc0-303">Merhaba görmelisiniz **filtreleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="91cc0-303">You should see hello **Filters** page.</span></span>

    ![Uyarılar - filtreleri sayfa oluşturma](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. <span data-ttu-id="91cc0-305">Select hello **olay**, **durum**, ve **substatus** (isteğe bağlı) toocreate istediğiniz bir Data Factory hizmeti için uyarı öğesini tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-305">Select hello **event**, **status**, and **substatus** (optional) that you want toocreate a Data Factory service alert for, and click **Next**.</span></span> <span data-ttu-id="91cc0-306">Merhaba görmelisiniz **alıcılar** sayfası.</span><span class="sxs-lookup"><span data-stu-id="91cc0-306">You should see hello **Recipients** page.</span></span>

    ![Uyarılar - alıcılar sayfa oluşturma](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. <span data-ttu-id="91cc0-308">Select hello **abonelik yöneticileri e-posta** seçeneği ve/veya girin bir **ek yönetici e-posta**, tıklatıp **son**.</span><span class="sxs-lookup"><span data-stu-id="91cc0-308">Select hello **Email subscription admins** option and/or enter an **additional administrator email**, and click **Finish**.</span></span> <span data-ttu-id="91cc0-309">Merhaba uyarı hello listesinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="91cc0-309">You should see hello alert in hello list.</span></span>

    ![Uyarılar listesinde](./media/data-factory-monitor-manage-app/AlertsList.png)

<span data-ttu-id="91cc0-311">Merhaba Uyarılar listesinde hello uyarı tooedit/silme/devre dışı bırak/etkinleştir ile bir uyarı ilişkili hello düğmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-311">In hello Alerts list, use hello buttons that are associated with hello alert tooedit/delete/disable/enable an alert.</span></span>

### <a name="eventstatussubstatus"></a><span data-ttu-id="91cc0-312">Alt olay/durumu/durum</span><span class="sxs-lookup"><span data-stu-id="91cc0-312">Event/status/substatus</span></span>
<span data-ttu-id="91cc0-313">Merhaba aşağıdaki tabloda kullanılabilir olayları ve durumları (ve alt durumlar) hello listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="91cc0-313">hello following table provides hello list of available events and statuses (and substatuses).</span></span>

| <span data-ttu-id="91cc0-314">Olay adı</span><span class="sxs-lookup"><span data-stu-id="91cc0-314">Event name</span></span> | <span data-ttu-id="91cc0-315">Durum</span><span class="sxs-lookup"><span data-stu-id="91cc0-315">Status</span></span> | <span data-ttu-id="91cc0-316">Alt durum</span><span class="sxs-lookup"><span data-stu-id="91cc0-316">Substatus</span></span> |
| --- | --- | --- |
| <span data-ttu-id="91cc0-317">Başlatılan Çalıştır etkinliği</span><span class="sxs-lookup"><span data-stu-id="91cc0-317">Activity Run Started</span></span> |<span data-ttu-id="91cc0-318">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="91cc0-318">Started</span></span> |<span data-ttu-id="91cc0-319">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="91cc0-319">Starting</span></span> |
| <span data-ttu-id="91cc0-320">Tamamlanan etkinlik</span><span class="sxs-lookup"><span data-stu-id="91cc0-320">Activity Run Finished</span></span> |<span data-ttu-id="91cc0-321">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-321">Succeeded</span></span> |<span data-ttu-id="91cc0-322">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-322">Succeeded</span></span> |
| <span data-ttu-id="91cc0-323">Tamamlanan etkinlik</span><span class="sxs-lookup"><span data-stu-id="91cc0-323">Activity Run Finished</span></span> |<span data-ttu-id="91cc0-324">Başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-324">Failed</span></span> |<span data-ttu-id="91cc0-325">Başarısız olan kaynak ayırma</span><span class="sxs-lookup"><span data-stu-id="91cc0-325">Failed Resource Allocation</span></span><br/><br/><span data-ttu-id="91cc0-326">Başarısız yürütme</span><span class="sxs-lookup"><span data-stu-id="91cc0-326">Failed Execution</span></span><br/><br/><span data-ttu-id="91cc0-327">Zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="91cc0-327">Timed Out</span></span><br/><br/><span data-ttu-id="91cc0-328">Başarısız doğrulamayı</span><span class="sxs-lookup"><span data-stu-id="91cc0-328">Failed Validation</span></span><br/><br/><span data-ttu-id="91cc0-329">terk</span><span class="sxs-lookup"><span data-stu-id="91cc0-329">Abandoned</span></span> |
| <span data-ttu-id="91cc0-330">İsteğe bağlı HDI kümesi oluşturma başlatıldı</span><span class="sxs-lookup"><span data-stu-id="91cc0-330">On-Demand HDI Cluster Create Started</span></span> |<span data-ttu-id="91cc0-331">başlatıldı</span><span class="sxs-lookup"><span data-stu-id="91cc0-331">Started</span></span> |-|
| <span data-ttu-id="91cc0-332">İsteğe bağlı HDI kümesi başarıyla oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-332">On-Demand HDI Cluster Created Successfully</span></span> |<span data-ttu-id="91cc0-333">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-333">Succeeded</span></span> |-|
| <span data-ttu-id="91cc0-334">İsteğe bağlı HDI kümesi silindi</span><span class="sxs-lookup"><span data-stu-id="91cc0-334">On-Demand HDI Cluster Deleted</span></span> |<span data-ttu-id="91cc0-335">Başarılı oldu</span><span class="sxs-lookup"><span data-stu-id="91cc0-335">Succeeded</span></span> |-|

### <a name="tooedit-delete-or-disable-an-alert"></a><span data-ttu-id="91cc0-336">tooedit, silmek veya uyarıyı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="91cc0-336">tooedit, delete, or disable an alert</span></span>

<span data-ttu-id="91cc0-337">(Kırmızı ile vurgulanan) düğmeleri tooedit, silmek veya devre dışı bir uyarı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="91cc0-337">Use hello following buttons (highlighted in red) tooedit, delete, or disable an alert.</span></span>

![Uyarıları düğmeleri](./media/data-factory-monitor-manage-app/AlertButtons.png)
