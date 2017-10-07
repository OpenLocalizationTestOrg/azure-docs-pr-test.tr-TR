---
title: "Visual Studio Hortonworks Sandbox - Azure Hdınsight ile aaaData Lake araçları | Microsoft Docs"
description: "Nasıl toouse hello Azure Data Lake araçları Visual Studio için yerel bir VM'de çalıştıran hello Hortonworks sandbox ile bilgi edinin. Bu araçları ile oluşturun ve Hive veya Pig işleri hello sandbox ve görünüm iş çıktısı ve geçmiş çalıştırın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="7d010-104">Hello Azure Data Lake araçları Visual Studio için Hortonworks Sandbox hello ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d010-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="7d010-105">Azure Data Lake genel Hadoop kümeleri ile çalışma araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="7d010-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="7d010-106">Bu belge, toouse hello Data Lake araçları ile Hortonworks yerel bir sanal makinede çalışan Sandbox hello hello adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="7d010-107">Merhaba Hortonworks Sandbox kullanarak geliştirme ortamınızı yerel olarak Hadoop ile toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="7d010-108">Bir çözümü geliştirilmiştir ve toodeploy istediğiniz sonra onu ölçekte tooan Hdınsight kümesi sonra taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d010-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d010-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7d010-109">Prerequisites</span></span>

* <span data-ttu-id="7d010-110">Merhaba Hortonworks korumalı alan, geliştirme ortamınızı bir sanal makinede çalışan.</span><span class="sxs-lookup"><span data-stu-id="7d010-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="7d010-111">Bu belge yazılmış ve Oracle VirtualBox çalıştıran hello sandbox ile test.</span><span class="sxs-lookup"><span data-stu-id="7d010-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="7d010-112">Merhaba hello sandbox ayarlama hakkında daha fazla bilgi için bkz: [hello Hortonworks sandbox ile başlayın.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7d010-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="7d010-113">Belge.</span><span class="sxs-lookup"><span data-stu-id="7d010-113">document.</span></span>

* <span data-ttu-id="7d010-114">Visual Studio 2013, Visual Studio 2015 ve Visual Studio 2017 (herhangi bir sürümünü).</span><span class="sxs-lookup"><span data-stu-id="7d010-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="7d010-115">Merhaba [.NET için Azure SDK](https://azure.microsoft.com/downloads/) 2.7.1 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="7d010-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="7d010-116">Merhaba [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="7d010-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="7d010-117">Parolalar hello korumalı alan için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7d010-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="7d010-118">Hortonworks Sandbox çalıştıran bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="7d010-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="7d010-119">Ardından hello hello adımları [hello Hortonworks Sandbox başlamak](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) belge.</span><span class="sxs-lookup"><span data-stu-id="7d010-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="7d010-120">Bu adımları hello SSH hello parolasını yapılandırma `root` hesap ve Ambari hello `admin` hesabı.</span><span class="sxs-lookup"><span data-stu-id="7d010-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="7d010-121">Bu parolalar, Visual Studio'dan toohello sandbox bağlandığınızda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d010-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="7d010-122">Merhaba araçları toohello sandbox Bağlan</span><span class="sxs-lookup"><span data-stu-id="7d010-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="7d010-123">Visual Studio'ni açın, **Görünüm**ve ardından **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="7d010-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="7d010-124">Gelen **Sunucu Gezgini**, sağ hello **Hdınsight** giriş ve ardından **tooHDInsight öykünücüsü bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="7d010-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, ile Bağlan tooHDInsight vurgulanmış öykünücüsü](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="7d010-126">Merhaba gelen **tooHDInsight öykünücüsü bağlanmak** iletişim kutusunda, Ambari için yapılandırılmış hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="7d010-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Vurgulanan parola metin kutusu ile iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="7d010-128">Seçin **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7d010-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="7d010-129">Kullanım hello **parola** hello için yapılandırdığınız alan tooenter hello parola `root` hesabı.</span><span class="sxs-lookup"><span data-stu-id="7d010-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="7d010-130">Merhaba diğer alanlarını hello varsayılan değeri bırakın.</span><span class="sxs-lookup"><span data-stu-id="7d010-130">Leave hello other fields at hello default value.</span></span>

    ![Vurgulanan parola metin kutusu ile iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="7d010-132">Seçin **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7d010-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="7d010-133">Merhaba Hizmetleri toofinish doğrulamasının tamamlanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d010-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="7d010-134">Bazı durumlarda, doğrulama başarısız ve tooupdate hello yapılandırma sor.</span><span class="sxs-lookup"><span data-stu-id="7d010-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="7d010-135">Doğrulama başarısız olursa, seçin **güncelleştirme**ve hello yapılandırma ve doğrulama hello hizmet toofinish için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d010-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Güncelleştirme düğmesi vurgulanan iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="7d010-137">Merhaba güncelleştirme işlemini Hortonworks Sandbox yapılandırma toowhat Visual Studio için hello Data Lake araçları tarafından beklenen Ambari toomodify hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d010-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="7d010-138">Doğrulama tamamlandıktan sonra seçin **son** toocomplete yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="7d010-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="7d010-139">![Bitiş düğmesi vurgulanan iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="7d010-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="7d010-140">Merhaba, geliştirme ortamı ve hello toohello sanal makine ayrılmış bellek miktarı hızını bağlı olarak, bu birkaç dakika tooconfigure alın ve hello Hizmetleri Doğrula.</span><span class="sxs-lookup"><span data-stu-id="7d010-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="7d010-141">Bu adımları uyguladıktan sonra artık elinizde bir **Hdınsight yerel küme** hello altında Sunucu Gezgininde girdisi **Hdınsight** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7d010-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="7d010-142">Bir Hive sorgusu Yaz</span><span class="sxs-lookup"><span data-stu-id="7d010-142">Write a Hive query</span></span>

<span data-ttu-id="7d010-143">Hive yapılandırılmış verilerle çalışmak için bir SQL benzeri sorgu dili (HiveQL) sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="7d010-144">Aşağıdaki adımları toolearn toorun isteğe bağlı hello yerel küme karşı nasıl sorgular hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d010-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="7d010-145">İçinde **Sunucu Gezgini**, daha önce eklediğiniz hello yerel küme hello girişini sağ tıklatın ve ardından **Hive sorgusu yaz**.</span><span class="sxs-lookup"><span data-stu-id="7d010-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, yazma vurgulanmış Hive sorgusu ile](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="7d010-147">Yeni bir sorgu penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="7d010-147">A new query window appears.</span></span> <span data-ttu-id="7d010-148">Burada hızla yapabilecekleriniz yazma ve bir sorgu toohello yerel küme gönderin.</span><span class="sxs-lookup"><span data-stu-id="7d010-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="7d010-149">Merhaba yeni sorgu penceresinde hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="7d010-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="7d010-150">toorun hello sorgu, select **gönderme** hello penceresinin hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="7d010-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="7d010-151">Merhaba diğer değerleri bırakın (**toplu** ve sunucu adı) hello varsayılan değerleri.</span><span class="sxs-lookup"><span data-stu-id="7d010-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Merhaba Gönder düğmesi vurgulanan Sorgu penceresinin ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="7d010-153">Ayrıca hello açılır menü sonraki çok kullanabileceğiniz**gönderme** tooselect **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="7d010-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="7d010-154">Gelişmiş Seçenekleri hello iş gönderdiğinizde tooprovide ek seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Gönderme betik ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="7d010-156">Merhaba sorgu gönderdikten sonra hello iş durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7d010-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="7d010-157">Hadoop tarafından işlendiği hello iş durumu hello işi hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7d010-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="7d010-158">**İş durumu** hello hello işinin durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="7d010-159">Merhaba durumu düzenli aralıklarla güncelleştirilir veya hello simgesi toorefresh hello durumunu Yenile el ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d010-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![İş vurgulanmış durumu ile iş görünümünde ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="7d010-161">Merhaba sonra **iş durumu** çok değiştirir**tamamlandı**, yönlendirilmiş Çevrimsiz grafik (DAG) görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7d010-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="7d010-162">Bu diyagramda tarafından Tez hello Hive sorgusu işlenirken belirlendi hello yürütme yolu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7d010-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="7d010-163">Tez hello varsayılan yürütme Hive için hello yerel kümede altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="7d010-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d010-164">Linux tabanlı Hdınsight kümelerini kullanırken Tez ayrıca hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="7d010-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="7d010-165">Merhaba varsayılan Windows tabanlı Hdınsight üzerinde değil.</span><span class="sxs-lookup"><span data-stu-id="7d010-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="7d010-166">toouse, burada, hello satırı ekleyin `set hive.execution.engine = tez;` Hive sorgunuzu toohello başlangıcı.</span><span class="sxs-lookup"><span data-stu-id="7d010-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="7d010-167">Kullanım hello **iş çıktısı** bağlantı tooview hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="7d010-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="7d010-168">Bu durumda, bu 823, hello hello sample_08 tablodaki satır sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d010-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="7d010-169">Hello kullanarak hello işle ilgili tanılama bilgileri görüntüleyebilirsiniz **iş günlüğü** ve **karşıdan YARN günlüğü** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="7d010-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="7d010-170">Ayrıca Hive işleri etkileşimli olarak hello değiştirerek çalıştırabilirsiniz **toplu** çok alan**etkileşimli**.</span><span class="sxs-lookup"><span data-stu-id="7d010-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="7d010-171">Ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="7d010-171">Then select **Execute**.</span></span>

    ![Vurgulanan etkileşimli ekran ve yürütme düğmeleri](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="7d010-173">Akışlar hello işleme toohello sırasında oluşturulan çıktı günlüğünü etkileşimli bir sorgu **HiveServer2 çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7d010-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d010-174">Merhaba bilgi olduğu hello hello kullanılabilir aynı **iş günlüğü** bir işi tamamlandıktan sonra bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7d010-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Çıktı oturum ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="7d010-176">Bir Hive projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d010-176">Create a Hive project</span></span>

<span data-ttu-id="7d010-177">Ayrıca, birden çok Hive betiği içeren bir proje oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d010-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="7d010-178">Komut dosyaları ilgili ya da bir sürüm denetim sisteminde toostore betikleri istediğiniz bir proje kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d010-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="7d010-179">Visual Studio'da seçin **dosya**, **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="7d010-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="7d010-180">Projeleri Hello listeden genişletin **şablonları**, genişletin **Azure Data Lake**ve ardından **HIVE (Hdınsight)**.</span><span class="sxs-lookup"><span data-stu-id="7d010-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="7d010-181">Merhaba şablonları listesinden **örnek Hive**.</span><span class="sxs-lookup"><span data-stu-id="7d010-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="7d010-182">Bir ad ve konum girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7d010-182">Enter a name and location, and then select **OK**.</span></span>

    ![Yeni Proje penceresinin ekran penceresiyle Azure Data Lake, HIVE, örnek Hive ve Tamam'ı vurgulanmış](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="7d010-184">Merhaba **örnek Hive** projeyi içeren iki komut **WebLogAnalysis.hql** ve **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="7d010-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="7d010-185">Bu komut dosyalarını kullanarak aynı hello gönderebilirsiniz **gönderme** hello penceresinde hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7d010-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="7d010-186">Pig proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d010-186">Create a Pig project</span></span>

<span data-ttu-id="7d010-187">Hive yapılandırılmış verilerle çalışmak için SQL benzeri bir dille sağlarken, Pig verileri dönüşümleri gerçekleştirerek çalışır.</span><span class="sxs-lookup"><span data-stu-id="7d010-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="7d010-188">Pig toodevelop sağlayan bir dil (Pig Latin) bir ardışık düzen Dönüşümlerin sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="7d010-189">toouse Pig hello yerel kümeyle şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7d010-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="7d010-190">Visual Studio'yu açın ve seçin **dosya**, **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="7d010-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="7d010-191">Projeleri Hello listeden genişletin **şablonları**, genişletin **Azure Data Lake**ve ardından **Pig (Hdınsight)**.</span><span class="sxs-lookup"><span data-stu-id="7d010-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="7d010-192">Merhaba şablonları listesinden **Pig uygulama**.</span><span class="sxs-lookup"><span data-stu-id="7d010-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="7d010-193">Konum, bir ad girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7d010-193">Enter a name, location, and then select **OK**.</span></span>

    ![Yeni Proje penceresinin ekran penceresiyle Azure Data Lake, Pig, Pig uygulama ve Tamam'ı vurgulanmış](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="7d010-195">Metin hello Merhaba içeriğine aşağıdaki hello girin **script.pig** bu proje ile oluşturulmuş dosyası.</span><span class="sxs-lookup"><span data-stu-id="7d010-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="7d010-196">Pig, Hive farklı bir dil kullanıyor, ancak hello işleri çalıştırma nasıl hello aracılığıyla her iki dilleri arasında tutarlıdır **gönderme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7d010-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="7d010-197">Seçme hello yanında aşağı açılan **gönderme** Pig için Gelişmiş Gönder iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7d010-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Gönderme betik ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="7d010-199">Merhaba iş durumunu ve çıkışını de görüntülenir, aynı bir Hive sorgusu hello.</span><span class="sxs-lookup"><span data-stu-id="7d010-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Tamamlanan Pig işi ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="7d010-201">İşleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="7d010-201">View jobs</span></span>

<span data-ttu-id="7d010-202">Data Lake araçları de tooeasily Hadoop üzerinde çalışan işleri hakkındaki bilgileri görüntüleyin olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d010-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="7d010-203">Merhaba yerel kümede çalışan adımları toosee hello işleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d010-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="7d010-204">Gelen **Sunucu Gezgini**hello yerel kümeye sağ tıklayın ve ardından **işleri görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="7d010-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="7d010-205">Gönderilen toohello küme silinmiş işlerinin listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7d010-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, ile vurgulanan işleri görüntüle](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="7d010-207">İşlerini Hello listeden bir tooview hello iş ayrıntılarını seçin.</span><span class="sxs-lookup"><span data-stu-id="7d010-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Ekran görüntüsü, iş tarayıcı vurgulanmış hello işleri biriyle](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="7d010-209">Görüntülenen hello bağlantılar, tooview hello çıkış ve günlük bilgileri de dahil olmak üzere bir Hive veya Pig sorgu çalıştırdıktan sonra gördüğünüz benzer toowhat bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="7d010-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="7d010-210">Ayrıca, değiştirebilir ve buradan hello işi yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="7d010-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="7d010-211">Hive veritabanları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="7d010-211">View Hive databases</span></span>

1. <span data-ttu-id="7d010-212">İçinde **Sunucu Gezgini**, hello genişletin **Hdınsight yerel küme** girişi genişletin ve ardından **Hive veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="7d010-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="7d010-213">Merhaba **varsayılan** ve **xademo** veritabanları hello yerel kümede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7d010-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="7d010-214">Bir veritabanını genişletmeden hello veritabanı içinde hello tabloları gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d010-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Sunucu Gezgini ekran veritabanları ile genişletilmiş](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="7d010-216">Bir tablo genişleterek bu tablonun hello sütunlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7d010-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="7d010-217">tooquickly görünümü hello verileri, bir tablo sağ tıklatın ve seçin **ilk 100 satırı görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="7d010-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, Genişletilmiş Tablo ve Görünüm ilk 100 seçilen satırı ile](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="7d010-219">Veritabanı ve tablo özellikleri</span><span class="sxs-lookup"><span data-stu-id="7d010-219">Database and table properties</span></span>

<span data-ttu-id="7d010-220">Bir veritabanı veya tablo hello özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d010-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="7d010-221">Seçme **özellikleri** hello Özellikler penceresinde seçili hello öğenin ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7d010-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="7d010-222">Örneğin, ekran aşağıdaki hello gösterilen hello bilgileri bakın:</span><span class="sxs-lookup"><span data-stu-id="7d010-222">For example, see hello information shown in hello following screenshot:</span></span>

![Ekran görüntüsü, Özellikler penceresi](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="7d010-224">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d010-224">Create a table</span></span>

<span data-ttu-id="7d010-225">toocreate bir tabloda bir veritabanını sağ tıklatın ve ardından **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="7d010-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Ekran görüntüsü, Sunucu Gezgini, ile vurgulanan Tablo Oluştur](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="7d010-227">Daha sonra bir form kullanarak hello tablosu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d010-227">You can then create hello table using a form.</span></span> <span data-ttu-id="7d010-228">Ekran aşağıdaki hello Hello altındaki gördüğünüz kullanılan toocreate hello tablosu ham HiveQL hello.</span><span class="sxs-lookup"><span data-stu-id="7d010-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Ekran görüntüsü hello form toocreate tablo kullanılan](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="7d010-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d010-230">Next steps</span></span>

* [<span data-ttu-id="7d010-231">Merhaba ipleri hello Hortonworks korumalı alan, öğrenme</span><span class="sxs-lookup"><span data-stu-id="7d010-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="7d010-232">Hadoop Öğreticisi - HDP ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7d010-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
