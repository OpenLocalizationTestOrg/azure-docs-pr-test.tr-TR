---
title: "Windows tabanlı Hdınsight - Azure ile Tez UI aaaUse | Microsoft Docs"
description: "Windows tabanlı Hdınsight Hdınsight'ta nasıl toouse hello Tez UI toodebug Tez işleri öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="75171-103">Windows tabanlı Hdınsight üzerinde Hello Tez UI toodebug Tez işlerinde kullanın</span><span class="sxs-lookup"><span data-stu-id="75171-103">Use hello Tez UI toodebug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="75171-104">Merhaba Tez UI hello yürütme altyapısı Windows tabanlı Hdınsight kümelerinde olarak Tez kullanan kullanılan toounderstand ve hata ayıklama işleri olabilecek bir web sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="75171-104">hello Tez UI is a web page that can be used toounderstand and debug jobs that use Tez as hello execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="75171-105">bir grafik bağlı öğelerinin her öğenin ayrıntısına ve istatistikleri ve günlük kaydı bilgilerini almak gibi hello Tez UI toovisualize hello iş sağlar.</span><span class="sxs-lookup"><span data-stu-id="75171-105">hello Tez UI allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75171-106">Bu belgedeki Hello adımlar Windows kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="75171-106">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="75171-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="75171-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="75171-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="75171-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75171-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="75171-109">Prerequisites</span></span>
* <span data-ttu-id="75171-110">Bir Windows tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="75171-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="75171-111">Yeni küme oluşturma adımları için bkz: [Windows tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="75171-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="75171-112">Merhaba Tez UI yalnızca 8 Şubat 2016 sonrasında oluşturulan Windows tabanlı Hdınsight kümeleri üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75171-112">hello Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="75171-113">Bir Windows tabanlı uzak masaüstü istemcisi.</span><span class="sxs-lookup"><span data-stu-id="75171-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="75171-114">Tez anlama</span><span class="sxs-lookup"><span data-stu-id="75171-114">Understanding Tez</span></span>
<span data-ttu-id="75171-115">Tez geleneksel MapReduce işleme büyük hızlarından sağlayan hadoop'ta veri işleme için genişletilebilir bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="75171-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="75171-116">Windows tabanlı Hdınsight kümeleri için komutu aşağıdaki Hive sorgunuzu bir parçası olarak hello kullanarak Hive için etkinleştirebilirsiniz bir isteğe bağlı altyapısıdır:</span><span class="sxs-lookup"><span data-stu-id="75171-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using hello following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="75171-117">İş gönderilen tooTez olduğunda, yönlendirilmiş Çevrimsiz grafik (hello yürütme hello iş tarafından gerekli hello eylemlerin sırasını açıklayan DAG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="75171-117">When work is submitted tooTez, it creates a Directed Acyclic Graph (DAG) that describes hello order of execution of hello actions required by hello job.</span></span> <span data-ttu-id="75171-118">Tek tek Eylemler köşeleri olarak adlandırılır ve hello parçası yürütmek genel işi.</span><span class="sxs-lookup"><span data-stu-id="75171-118">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="75171-119">Merhaba gerçek yürütme hello iş köşe tarafından tanımlanan bir görev çağrılır ve hello kümedeki birden çok düğüm arasında dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="75171-119">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-ui"></a><span data-ttu-id="75171-120">Anlama hello Tez kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="75171-120">Understanding hello Tez UI</span></span>
<span data-ttu-id="75171-121">Merhaba Tez UI Tez kullanma, çalışmakta olan veya sahip işlemler hakkında bilgi daha önce çalışan bir web sayfası sağlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="75171-121">hello Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="75171-122">Tooview hello Tez tarafından oluşturulan DAG tanır kümeler arasında nasıl dağıtıldığını sayaçları görevleri ve köşeleri ve hata bilgilerini tarafından kullanılan bellek gibi.</span><span class="sxs-lookup"><span data-stu-id="75171-122">It allows you tooview hello DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="75171-123">Aşağıdaki senaryolar hello yararlı bilgiler teklif edebilir:</span><span class="sxs-lookup"><span data-stu-id="75171-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="75171-124">Uzun süre çalışan işlemleri görüntüleme, izleme harita ilerlemesini hello ve görevleri azaltır.</span><span class="sxs-lookup"><span data-stu-id="75171-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="75171-125">Başarılı veya başarısız işlemler toolearn ilişkin geçmiş verileri analiz etme işleme nasıl geliştirilmiş veya neden başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="75171-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="75171-126">Bir DAG oluştur</span><span class="sxs-lookup"><span data-stu-id="75171-126">Generate a DAG</span></span>
<span data-ttu-id="75171-127">kullanan bir iş altyapısı şu anda çalışıyor veya sahip hello son çalıştırılan edilmiş Tez hello varsa hello Tez UI yalnızca veri içermez.</span><span class="sxs-lookup"><span data-stu-id="75171-127">hello Tez UI will only contain data if a job that uses hello Tez engine is currently running, or has been ran in hello past.</span></span> <span data-ttu-id="75171-128">Basit Hive sorguları genellikle Tez, yapan filtreleme, gruplama, sıralama, birleşimler, vb. Tez genellikle gerektirir ancak daha karmaşık sorgular kullanmadan çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="75171-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="75171-129">Aşağıdaki adımları toorun Tez kullanma yürütecek bir Hive sorgusu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="75171-129">Use hello following steps toorun a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="75171-130">Toohttps://CLUSTERNAME.azurehdinsight.net, bir web tarayıcısında gidin nerede **CLUSTERNAME** Hdınsight kümenize hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="75171-130">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="75171-131">Merhaba hello sayfanın üst kısmındaki hello Hello menüsünden seçin **Hive Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="75171-131">From hello menu at hello top of hello page, select hello **Hive Editor**.</span></span> <span data-ttu-id="75171-132">Bu örnek sorgu aşağıdaki hello ile bir sayfa görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75171-132">This will display a page with hello following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="75171-133">Merhaba örnek sorgu silebilir ve hello şununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75171-133">Erase hello example query and replace it with hello following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="75171-134">Select hello **gönderme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="75171-134">Select hello **Submit** button.</span></span> <span data-ttu-id="75171-135">Merhaba **proje oturumunu** hello sayfanın hello kısmına hello sorgu hello durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-135">hello **Job Session** section at hello bottom of hello page will display hello status of hello query.</span></span> <span data-ttu-id="75171-136">Bir kez durum değişikliklerini çok hello**tamamlandı**seçin hello **ayrıntıları görüntüle** bağlantı tooview hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="75171-136">Once hello status changes too**Completed**, select hello **View Details** link tooview hello results.</span></span> <span data-ttu-id="75171-137">Merhaba **iş çıktısı** benzer toohello aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="75171-137">hello **Job Output** should be similar toohello following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a><span data-ttu-id="75171-138">Merhaba Tez UI kullanın</span><span class="sxs-lookup"><span data-stu-id="75171-138">Use hello Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="75171-139">Uzak Masaüstü tooconnect toohello baş düğümler kullanmalısınız hello Tez UI yalnızca hello küme baş düğümü hello masaüstünden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="75171-139">hello Tez UI is only available from hello desktop of hello cluster head nodes, so you must use Remote Desktop tooconnect toohello head nodes.</span></span>
>
>

1. <span data-ttu-id="75171-140">Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="75171-140">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="75171-141">Merhaba Hdınsight dikey penceresinde Hello üstten hello seçin **Uzak Masaüstü** simgesi.</span><span class="sxs-lookup"><span data-stu-id="75171-141">From hello top of hello HDInsight blade, select hello **Remote Desktop** icon.</span></span> <span data-ttu-id="75171-142">Bu hello Uzak Masaüstü dikey penceresinde görüntülenir</span><span class="sxs-lookup"><span data-stu-id="75171-142">This will display hello remote desktop blade</span></span>

    ![Uzak Masaüstü simgesi](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="75171-144">Merhaba Uzak Masaüstü dikey penceresinden seçin **Bağlan** tooconnect toohello küme baş düğümüne.</span><span class="sxs-lookup"><span data-stu-id="75171-144">From hello Remote Desktop blade, select **Connect** tooconnect toohello cluster head node.</span></span> <span data-ttu-id="75171-145">İstendiğinde, hello küme Uzak Masaüstü kullanıcı adı ve parola tooauthenticate hello bağlantısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="75171-145">When prompted, use hello cluster Remote Desktop user name and password tooauthenticate hello connection.</span></span>

    ![Uzak Masaüstü Bağlantısı simgesi](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="75171-147">Uzak Masaüstü bağlantısı etkin değil, bir kullanıcı adı, parola ve sona erme tarihi sağlayın, sonra seçin **etkinleştirmek** tooenable Uzak Masaüstü.</span><span class="sxs-lookup"><span data-stu-id="75171-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** tooenable Remote Desktop.</span></span> <span data-ttu-id="75171-148">Etkinleştirildikten sonra hello önceki adımları tooconnect kullanın.</span><span class="sxs-lookup"><span data-stu-id="75171-148">Once it has been enabled, use hello previous steps tooconnect.</span></span>
   >
   >
3. <span data-ttu-id="75171-149">Bağlantı kurulduktan sonra hello Uzak Masaüstü, select hello dişli simgesine hello sağ üst tarafındaki hello tarayıcı, Internet Explorer'ı açın ve ardından **Uyumluluk Görünümü Ayarları**.</span><span class="sxs-lookup"><span data-stu-id="75171-149">Once connected, open Internet Explorer on hello remote desktop, select hello gear icon in hello upper right of hello browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="75171-150">Merhaba altından **Uyumluluk Görünümü Ayarları**temizleyin hello onay kutusunu **görüntüleme intranet sitelerini Uyumluluk Görünümü'nde** ve **kullanım Microsoft Uyumluluk listeleri**, ve ardından **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="75171-150">From hello bottom of **Compatibility View Settings**, clear hello check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="75171-151">Internet Explorer'da toohttp://headnodehost:8188 Gözat/tezui / #/.</span><span class="sxs-lookup"><span data-stu-id="75171-151">In Internet Explorer, browse toohttp://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="75171-152">Bu hello Tez kullanıcı Arabirimi görüntüler</span><span class="sxs-lookup"><span data-stu-id="75171-152">This will display hello Tez UI</span></span>

    ![Tez kullanıcı Arabirimi](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="75171-154">Merhaba Tez UI yüklediğinde, çalışmakta olan ya da silinmiş Dag'leri listesini hello küme üzerinde çalışan görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="75171-154">When hello Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on hello cluster.</span></span> <span data-ttu-id="75171-155">Merhaba Dag adı, kimliği, gönderen, durumu, başlangıç saati, bitiş zamanı, süresi, uygulama kimliği ve kuyruk Hello varsayılan görünümü içerir.</span><span class="sxs-lookup"><span data-stu-id="75171-155">hello default view includes hello Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="75171-156">Daha fazla sütun hello sayfasının sağ hello hello dişli simgesini kullanarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="75171-156">More columns can be added using hello gear icon at hello right of hello page.</span></span>

    <span data-ttu-id="75171-157">Yalnızca bir giriş varsa, önceki bölümde hello çalıştırdığınız hello sorgu için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="75171-157">If you have only one entry, it will be for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="75171-158">Birden çok girdi varsa, arama hello Dag'leri yukarıda hello alanlarında arama ölçütü girerek, ardından isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="75171-158">If you have multiple entries, you can search by entering search criteria in hello fields above hello DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="75171-159">Select hello **Dag adı** hello en son DAG girişi.</span><span class="sxs-lookup"><span data-stu-id="75171-159">Select hello **Dag Name** for hello most recent DAG entry.</span></span> <span data-ttu-id="75171-160">Bu hello seçeneği toodownload hello DAG hakkında bilgi içeren JSON dosyaları zip yanı sıra hello DAG hakkında bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-160">This will display information about hello DAG, as well as hello option toodownload a zip of JSON files that contain information about hello DAG.</span></span>

    ![DAG ayrıntıları](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="75171-162">Merhaba yukarıda **DAG ayrıntıları** hello DAG kullanılan toodisplay bilgilerini olabilir birkaç bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="75171-162">Above hello **DAG Details** are several links that can be used toodisplay information about hello DAG.</span></span>

   * <span data-ttu-id="75171-163">**DAG sayaçları** bu DAG sayaçları bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="75171-164">**Grafik görünümü** bu DAG grafik gösterimi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="75171-165">**Tüm köşeleri** bu DAG hello köşeleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-165">**All Vertices** displays a list of hello vertices in this DAG.</span></span>
   * <span data-ttu-id="75171-166">**Tüm Görevler** bu DAG tüm köşeleri hello görevlerde listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-166">**All Tasks** displays a list of hello tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="75171-167">**Tüm TaskAttempts** hello hakkında bilgi görüntüler toorun görevler için bu DAG çalışır.</span><span class="sxs-lookup"><span data-stu-id="75171-167">**All TaskAttempts** displays information about hello attempts toorun tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="75171-168">Merhaba sütun görüntü köşeleri, görevleri ve TaskAttempts kaydırırsanız olduğuna dikkat edin tooview bağlantıları **sayaçları** ve **görüntülemek veya günlükleri indirmek** her satır için.</span><span class="sxs-lookup"><span data-stu-id="75171-168">If you scroll hello column display for Vertices, Tasks and TaskAttempts, notice that there are links tooview **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="75171-169">Merhaba işlemiyle hatası varsa, hello DAG ayrıntıları hello başarısız görev hakkında bağlantılar tooinformation birlikte başarısız oldu, durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-169">If there was a failure with hello job, hello DAG Details will display a status of FAILED, along with links tooinformation about hello failed task.</span></span> <span data-ttu-id="75171-170">Tanılama bilgileri hello DAG Ayrıntılar altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="75171-170">Diagnostics information will be displayed beneath hello DAG details.</span></span>
8. <span data-ttu-id="75171-171">Seçin **grafik görünümü**.</span><span class="sxs-lookup"><span data-stu-id="75171-171">Select **Graphical View**.</span></span> <span data-ttu-id="75171-172">Bu grafik gösterimi hello DAG görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-172">This displays a graphical representation of hello DAG.</span></span> <span data-ttu-id="75171-173">Merhaba görünüm toodisplay bilgi ilgili her köşe üzerinden hello fare yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75171-173">You can place hello mouse over each vertex in hello view toodisplay information about it.</span></span>

    ![Grafik görünümü](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="75171-175">Bir köşe tıklatarak hello yükler **köşe ayrıntıları** bu öğe için.</span><span class="sxs-lookup"><span data-stu-id="75171-175">Clicking on a vertex will load hello **Vertex Details** for that item.</span></span> <span data-ttu-id="75171-176">Tıklatın hello üzerinde **harita 1** köşe toodisplay ayrıntılar bu öğe için.</span><span class="sxs-lookup"><span data-stu-id="75171-176">Click on hello **Map 1** vertex toodisplay details for this item.</span></span> <span data-ttu-id="75171-177">Seçin **Onayla** tooconfirm hello gezinti.</span><span class="sxs-lookup"><span data-stu-id="75171-177">Select **Confirm** tooconfirm hello navigation.</span></span>

    ![Köşe ayrıntıları](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="75171-179">Şimdi ilgili toovertices ve görevleri bağlantıları hello sayfanın üst kısmındaki hello gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75171-179">Note that you now have links at hello top of hello page that are related toovertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75171-180">Bu sayfaya geri çok giderek de ulaşması**DAG ayrıntıları**, seçme **köşe ayrıntıları**ve ardından hello seçerek **harita 1** köşe.</span><span class="sxs-lookup"><span data-stu-id="75171-180">You can also arrive at this page by going back too**DAG Details**, selecting **Vertex Details**, and then selecting hello **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="75171-181">**Köşe sayaçları** bu köşe sayaç bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="75171-182">**Görevleri** bu köşe için görevleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="75171-183">**Görev denemeleri** bu köşe için deneme toorun görevler hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-183">**Task Attempts** displays information about attempts toorun tasks for this vertex.</span></span>
    * <span data-ttu-id="75171-184">**Kaynakları & iç havuzlar** bu köşe için iç havuzlar ve veri kaynakları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="75171-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="75171-185">Merhaba önceki menüsüyle hello sütun görüntü görevler için kaydırabilirsiniz gibi görev denemeleri ve kaynakları & Sinks__ toodisplay toomore bilgileri her öğe için bağlar.</span><span class="sxs-lookup"><span data-stu-id="75171-185">As with hello previous menu, you can scroll hello column display for Tasks, Task Attempts, and Sources & Sinks__ toodisplay links toomore information for each item.</span></span>
      >
      >
11. <span data-ttu-id="75171-186">Seçin **görevleri**, ve select hello öğesi adlı **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="75171-186">Select **Tasks**, and then select hello item named **00_000000**.</span></span> <span data-ttu-id="75171-187">Bu görüntüler **görev ayrıntıları** bu görev için.</span><span class="sxs-lookup"><span data-stu-id="75171-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="75171-188">Bu ekranda görüntüleyebileceğiniz **görev sayaçları** ve **görev denemeleri**.</span><span class="sxs-lookup"><span data-stu-id="75171-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Görev Ayrıntıları](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="75171-190">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="75171-190">Next Steps</span></span>
<span data-ttu-id="75171-191">Toouse hello Tez nasıl görüntüleyebilirim öğrendiniz, daha fazla bilgi edinmek [hdınsight'ta Hive kullanarak](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="75171-191">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="75171-192">Daha ayrıntılı Tez teknik bilgi için bkz: Merhaba [Hortonworks Tez sayfanın](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="75171-192">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
