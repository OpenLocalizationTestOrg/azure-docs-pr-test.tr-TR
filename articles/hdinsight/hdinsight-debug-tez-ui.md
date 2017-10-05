---
title: "Tez UI Windows tabanlı Hdınsight ile - Azure kullanma | Microsoft Docs"
description: "Windows tabanlı Hdınsight hdınsight'ta Tez işlerinde hata ayıklamak için Tez UI kullanmayı öğrenin."
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
ms.openlocfilehash: 3889fa1c3523eb0330cbe3b7640fd8590a5ceadf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="441b2-103">Windows tabanlı Hdınsight üzerinde Tez işlerinde hata ayıklamak için Tez kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="441b2-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="441b2-104">Tez UI anlamak ve Tez yürütme altyapısı Windows tabanlı Hdınsight kümelerinde olarak kullanan işleri hata ayıklamak için kullanılan bir web sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="441b2-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="441b2-105">Tez kullanıcı Arabirimi iş bağlı öğelerinin bir grafik olarak görselleştirme, her öğenin ayrıntısına ve istatistikler ve günlük bilgileri almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="441b2-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="441b2-106">Bu belgede yer alan adımlar Windows kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="441b2-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="441b2-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="441b2-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="441b2-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="441b2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="441b2-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="441b2-109">Prerequisites</span></span>
* <span data-ttu-id="441b2-110">Bir Windows tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="441b2-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="441b2-111">Yeni küme oluşturma adımları için bkz: [Windows tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="441b2-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="441b2-112">Tez UI yalnızca 8 Şubat 2016 sonrasında oluşturulan Windows tabanlı Hdınsight kümeleri üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="441b2-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="441b2-113">Bir Windows tabanlı uzak masaüstü istemcisi.</span><span class="sxs-lookup"><span data-stu-id="441b2-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="441b2-114">Tez anlama</span><span class="sxs-lookup"><span data-stu-id="441b2-114">Understanding Tez</span></span>
<span data-ttu-id="441b2-115">Tez geleneksel MapReduce işleme büyük hızlarından sağlayan hadoop'ta veri işleme için genişletilebilir bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="441b2-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="441b2-116">Windows tabanlı Hdınsight kümeleri için Hive sorgunuzu bir parçası olarak aşağıdaki komutu kullanarak Hive için etkinleştirebilirsiniz bir isteğe bağlı altyapısıdır:</span><span class="sxs-lookup"><span data-stu-id="441b2-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="441b2-117">İş için Tez gönderildiğinde, yönlendirilmiş Çevrimsiz grafik (yürütme iş tarafından gereken eylemlerin sırasını açıklayan DAG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="441b2-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="441b2-118">Tek tek Eylemler köşeleri olarak adlandırılır ve genel iş parçası yürütün.</span><span class="sxs-lookup"><span data-stu-id="441b2-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="441b2-119">Gerçek yürütme köşe tarafından açıklanan iş bir görev çağrılır ve kümedeki birden çok düğüm arasında dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="441b2-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="441b2-120">Tez UI anlama</span><span class="sxs-lookup"><span data-stu-id="441b2-120">Understanding the Tez UI</span></span>
<span data-ttu-id="441b2-121">Tez kullanıcı Arabirimi, bir web sayfası, çalıştırılan veya olan işlemler hakkında bilgi, daha önce Tez kullanılarak çalıştırıldı sağlar ' dir.</span><span class="sxs-lookup"><span data-stu-id="441b2-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="441b2-122">Tez tarafından oluşturulan DAG görüntülemenize izin verir kümeler arasında nasıl dağıtıldığını sayaçları görevleri ve köşeleri ve hata bilgilerini tarafından kullanılan bellek gibi.</span><span class="sxs-lookup"><span data-stu-id="441b2-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="441b2-123">Aşağıdaki senaryolarda yararlı bilgiler teklif edebilir:</span><span class="sxs-lookup"><span data-stu-id="441b2-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="441b2-124">Uzun süre çalışan izleme harita ilerlemesini görüntüleme, işler ve görevler azaltır.</span><span class="sxs-lookup"><span data-stu-id="441b2-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="441b2-125">İşleme nasıl geliştirilmiş veya neden başarısız öğrenmek başarılı veya başarısız işlemler için geçmiş verileri analiz etme.</span><span class="sxs-lookup"><span data-stu-id="441b2-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="441b2-126">Bir DAG oluştur</span><span class="sxs-lookup"><span data-stu-id="441b2-126">Generate a DAG</span></span>
<span data-ttu-id="441b2-127">Tez UI geçmişte Tez Altyapısı şu anda çalışıyor ya da bırakıldı kullanan çalışan bir iş, yalnızca veri içermez.</span><span class="sxs-lookup"><span data-stu-id="441b2-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="441b2-128">Basit Hive sorguları genellikle Tez, yapan filtreleme, gruplama, sıralama, birleşimler, vb. Tez genellikle gerektirir ancak daha karmaşık sorgular kullanmadan çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="441b2-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="441b2-129">Tez kullanma yürütecek bir Hive sorgusu çalıştırmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="441b2-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="441b2-130">Bir web tarayıcısında https://CLUSTERNAME.azurehdinsight.net için gidin nerede **CLUSTERNAME** Hdınsight kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="441b2-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="441b2-131">Sayfanın üstündeki menüsünden seçin **Hive Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="441b2-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="441b2-132">Bu, aşağıdaki örnek sorgu içeren bir sayfa görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="441b2-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="441b2-133">Örnek sorgu silebilir ve aşağıdakiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="441b2-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="441b2-134">Seçin **gönderme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="441b2-134">Select the **Submit** button.</span></span> <span data-ttu-id="441b2-135">**Proje oturumunu** sayfanın alt kısmına sorgu durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="441b2-136">Durum değişikliklerini sonra **tamamlandı**seçin **ayrıntıları görüntüle** sonuçları görüntülemek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="441b2-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="441b2-137">**İş çıktısı** aşağıdakine benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="441b2-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="441b2-138">Tez kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="441b2-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="441b2-139">Baş düğümler bağlanmak için Uzak Masaüstü'nü kullanmanız gerekir böylece Tez UI yalnızca küme baş düğümler masaüstünden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="441b2-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="441b2-140">Gelen [Azure portal](https://portal.azure.com), Hdınsight kümenize seçin.</span><span class="sxs-lookup"><span data-stu-id="441b2-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="441b2-141">Hdınsight dikey üstten seçin **Uzak Masaüstü** simgesi.</span><span class="sxs-lookup"><span data-stu-id="441b2-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="441b2-142">Bu Uzak Masaüstü dikey penceresinde görüntülenir</span><span class="sxs-lookup"><span data-stu-id="441b2-142">This will display the remote desktop blade</span></span>

    ![Uzak Masaüstü simgesi](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="441b2-144">Uzak Masaüstü dikey penceresinden seçin **Bağlan** küme baş düğümüne bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="441b2-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="441b2-145">İstendiğinde, bağlantı kimliğini doğrulamak için küme Uzak Masaüstü kullanıcı adı ve parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="441b2-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Uzak Masaüstü Bağlantısı simgesi](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="441b2-147">Uzak Masaüstü bağlantısı etkin değil, bir kullanıcı adı, parola ve sona erme tarihi sağlayın, sonra seçin **etkinleştirmek** Uzak Masaüstü'nü etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="441b2-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="441b2-148">Etkinleştirildikten sonra bağlanmak için önceki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="441b2-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="441b2-149">Bağlantı kurulduktan sonra Internet Explorer'ı Uzak Masaüstü'nü açın, sağ üst tarafındaki tarayıcı içinde dişli simgesini seçin ve ardından **Uyumluluk Görünümü Ayarları**.</span><span class="sxs-lookup"><span data-stu-id="441b2-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="441b2-150">Aşağıdan **Uyumluluk Görünümü Ayarları**, onay kutusunu temizleyin **görüntüleme intranet sitelerini Uyumluluk Görünümü'nde** ve **kullanım Microsoft Uyumluluk listeleri**ve ardından **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="441b2-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="441b2-151">Internet Explorer'da tezui/http://headnodehost:8188 / # Gözat /.</span><span class="sxs-lookup"><span data-stu-id="441b2-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="441b2-152">Bu Tez kullanıcı arabirimini görüntüler</span><span class="sxs-lookup"><span data-stu-id="441b2-152">This will display the Tez UI</span></span>

    ![Tez kullanıcı Arabirimi](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="441b2-154">Tez UI yüklediğinde, çalışmakta olan ya da silinmiş Dag'leri listesini küme üzerinde çalışan görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="441b2-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="441b2-155">Varsayılan görünüm Dag adı, kimliği, gönderen, durumu, başlangıç saati, bitiş zamanı, süresi, uygulama kimliği ve kuyruk içerir.</span><span class="sxs-lookup"><span data-stu-id="441b2-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="441b2-156">Daha fazla sütun, sayfanın sağ taraftaki dişli simgesini kullanarak eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="441b2-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="441b2-157">Yalnızca bir giriş varsa, önceki bölümde çalıştırdığınız bir sorgu için olacaktır.</span><span class="sxs-lookup"><span data-stu-id="441b2-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="441b2-158">Birden çok girdi varsa, Dag'leri yukarıda alanlarında arama ölçütü girerek arayın, ardından isabet **Enter**.</span><span class="sxs-lookup"><span data-stu-id="441b2-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="441b2-159">Seçin **Dag adı** en son DAG girişi.</span><span class="sxs-lookup"><span data-stu-id="441b2-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="441b2-160">Bu, DAG hakkında bilgi içeren JSON dosyaları zip yükleme seçeneği yanı sıra DAG hakkında bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![DAG ayrıntıları](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="441b2-162">Yukarıdaki **DAG ayrıntıları** DAG hakkındaki bilgileri görüntülemek için kullanılan birkaç bağlantılardır.</span><span class="sxs-lookup"><span data-stu-id="441b2-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="441b2-163">**DAG sayaçları** bu DAG sayaçları bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="441b2-164">**Grafik görünümü** bu DAG grafik gösterimi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="441b2-165">**Tüm köşeleri** bu DAG köşeleri listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="441b2-166">**Tüm Görevler** bu DAG tüm köşeleri görevlerde listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="441b2-167">**Tüm TaskAttempts** görevleri çalıştırmak için bu DAG girişimleri hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="441b2-168">Sütun görüntü köşeleri, görevleri ve TaskAttempts kaydırırsanız, görüntülemek için bağlantıları olduğuna dikkat edin **sayaçları** ve **görüntülemek veya günlükleri indirmek** her satır için.</span><span class="sxs-lookup"><span data-stu-id="441b2-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="441b2-169">İşi ile hatası varsa, DAG ayrıntıları durumunu başarısız oldu, başarısız görev hakkında bilgi için bağlantılar ile birlikte görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="441b2-170">Tanılama bilgileri DAG Ayrıntılar altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="441b2-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="441b2-171">Seçin **grafik görünümü**.</span><span class="sxs-lookup"><span data-stu-id="441b2-171">Select **Graphical View**.</span></span> <span data-ttu-id="441b2-172">Bu grafik gösterimi DAG görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="441b2-173">Her köşe ilgili bilgileri görüntülemek için görünümünde üzerinden fare yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="441b2-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Grafik görünümü](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="441b2-175">Bir köşe tıklatarak yükler **köşe ayrıntıları** bu öğe için.</span><span class="sxs-lookup"><span data-stu-id="441b2-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="441b2-176">Tıklayın **harita 1** köşe bu öğenin ayrıntılarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="441b2-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="441b2-177">Seçin **Onayla** Gezinti onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="441b2-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Köşe ayrıntıları](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="441b2-179">Şimdi köşeleri ve görevlerle ilgili bağlantıları sayfanın üst kısmındaki gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="441b2-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="441b2-180">Bu sayfaya geri giderek de ulaşması **DAG ayrıntıları**, seçme **köşe ayrıntıları**ve ardından seçerek **harita 1** köşe.</span><span class="sxs-lookup"><span data-stu-id="441b2-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="441b2-181">**Köşe sayaçları** bu köşe sayaç bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="441b2-182">**Görevleri** bu köşe için görevleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="441b2-183">**Görev denemeleri** bu köşe için görevleri çalıştırma denemelerini hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="441b2-184">**Kaynakları & iç havuzlar** bu köşe için iç havuzlar ve veri kaynakları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="441b2-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="441b2-185">Olarak önceki menüsüyle, görevler, görev denemeleri ve kaynakları & Sinks__ her öğe için daha fazla bilgi için bağlantılar görüntülenecek sütun görüntü gezinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="441b2-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="441b2-186">Seçin **görevleri**ve ardından adlı bir öğe seçin **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="441b2-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="441b2-187">Bu görüntüler **görev ayrıntıları** bu görev için.</span><span class="sxs-lookup"><span data-stu-id="441b2-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="441b2-188">Bu ekranda görüntüleyebileceğiniz **görev sayaçları** ve **görev denemeleri**.</span><span class="sxs-lookup"><span data-stu-id="441b2-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Görev Ayrıntıları](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="441b2-190">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="441b2-190">Next Steps</span></span>
<span data-ttu-id="441b2-191">Tez görünümü kullanmak öğrendiniz, daha fazla bilgi edinmek [hdınsight'ta Hive kullanarak](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="441b2-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="441b2-192">Daha ayrıntılı Tez teknik bilgi için bkz: [Hortonworks Tez sayfanın](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="441b2-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
