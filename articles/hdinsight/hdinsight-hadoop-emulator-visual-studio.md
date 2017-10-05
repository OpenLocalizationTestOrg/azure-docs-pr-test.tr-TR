---
title: "Data Lake araçları Hortonworks Sandbox - Azure Hdınsight ile Visual Studio için | Microsoft Docs"
description: "Azure Data Lake araçları Visual Studio için yerel bir VM'de çalıştıran Hortonworks sandbox ile nasıl kullanacağınızı öğrenin. Bu araçları ile oluşturun ve Hive veya Pig işleri korumalı alan ve görünüm iş çıktısı ve geçmiş çalıştırın."
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
ms.openlocfilehash: 574ccaa8b2d9448a60ddf8adc7f92fa3683b1d61
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-the-azure-data-lake-tools-for-visual-studio-with-the-hortonworks-sandbox"></a><span data-ttu-id="15a81-104">Hortonworks Sandbox ile Visual Studio için Azure Data Lake araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="15a81-104">Use the Azure Data Lake tools for Visual Studio with the Hortonworks Sandbox</span></span>

<span data-ttu-id="15a81-105">Azure Data Lake genel Hadoop kümeleri ile çalışma araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="15a81-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="15a81-106">Bu belge, yerel bir sanal makinede çalışan Data Lake araçları Hortonworks Sandbox ile kullanmak için gerekli adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a81-106">This document provides the steps needed to use the Data Lake tools with the Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="15a81-107">Hortonworks Sandbox kullanarak Hadoop ile yerel olarak geliştirme ortamınızı üzerinde çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a81-107">Using the Hortonworks Sandbox allows you to work with Hadoop locally on your development environment.</span></span> <span data-ttu-id="15a81-108">Bir çözümü geliştirilmiştir ve ölçekte dağıtmak istediğiniz sonra bir Hdınsight kümesine taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a81-108">After you have developed a solution and want to deploy it at scale, you can then move to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15a81-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="15a81-109">Prerequisites</span></span>

* <span data-ttu-id="15a81-110">Hortonworks geliştirme ortamınızı bir sanal makinede çalışan korumalı alan.</span><span class="sxs-lookup"><span data-stu-id="15a81-110">The Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="15a81-111">Bu belge yazılmış ve Oracle VirtualBox çalıştıran korumalı alan ile test.</span><span class="sxs-lookup"><span data-stu-id="15a81-111">This document was written and tested with the sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="15a81-112">Korumalı alan ayarlama hakkında daha fazla bilgi için bkz: [Hortonworks sandbox ile başlayın.](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="15a81-112">For information on setting up the sandbox, see the [Get started with the Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="15a81-113">Belge.</span><span class="sxs-lookup"><span data-stu-id="15a81-113">document.</span></span>

* <span data-ttu-id="15a81-114">Visual Studio 2013, Visual Studio 2015 ve Visual Studio 2017 (herhangi bir sürümünü).</span><span class="sxs-lookup"><span data-stu-id="15a81-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="15a81-115">[.NET için Azure SDK](https://azure.microsoft.com/downloads/) 2.7.1 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="15a81-115">The [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="15a81-116">[Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="15a81-116">The [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-the-sandbox"></a><span data-ttu-id="15a81-117">Korumalı alan için parolaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="15a81-117">Configure passwords for the sandbox</span></span>

<span data-ttu-id="15a81-118">Hortonworks Sandbox çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="15a81-118">Make sure that the Hortonworks Sandbox is running.</span></span> <span data-ttu-id="15a81-119">Ardından adımları [Hortonworks korumalı alanda başlamak](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) belge.</span><span class="sxs-lookup"><span data-stu-id="15a81-119">Then follow the steps in the [Get started in the Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="15a81-120">Bu adımları SSH için parolayı yapılandırmak `root` hesabı ve Ambari `admin` hesabı.</span><span class="sxs-lookup"><span data-stu-id="15a81-120">These steps configure the password for the SSH `root` account, and the Ambari `admin` account.</span></span> <span data-ttu-id="15a81-121">Bu parolalar, Visual Studio'dan korumalı alanda bağlandığınızda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="15a81-121">These passwords are used when you connect to the sandbox from Visual Studio.</span></span>

## <a name="connect-the-tools-to-the-sandbox"></a><span data-ttu-id="15a81-122">Korumalı alan için Araçlar Bağlan</span><span class="sxs-lookup"><span data-stu-id="15a81-122">Connect the tools to the sandbox</span></span>

1. <span data-ttu-id="15a81-123">Visual Studio'ni açın, **Görünüm**ve ardından **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="15a81-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="15a81-124">Gelen **Sunucu Gezgini**, sağ **Hdınsight** giriş ve ardından **Hdınsight öykünücüsünde Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="15a81-124">From **Server Explorer**, right-click the **HDInsight** entry, and then select **Connect to HDInsight Emulator**.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, Hdınsight öykünücüsünde Bağlan ile vurgulanan](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="15a81-126">Gelen **Hdınsight öykünücüsünde Bağlan** iletişim kutusunda, Ambari için yapılandırdığınız parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="15a81-126">From the **Connect to HDInsight Emulator** dialog box, enter the password that you configured for Ambari.</span></span>

    ![Vurgulanan parola metin kutusu ile iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="15a81-128">Seçin **sonraki** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="15a81-128">Select **Next** to continue.</span></span>

4. <span data-ttu-id="15a81-129">Kullanım **parola** için yapılandırılmış parola girmesini alan `root` hesabı.</span><span class="sxs-lookup"><span data-stu-id="15a81-129">Use the **Password** field to enter the password you configured for the `root` account.</span></span> <span data-ttu-id="15a81-130">Diğer alanları varsayılan değeri bırakın.</span><span class="sxs-lookup"><span data-stu-id="15a81-130">Leave the other fields at the default value.</span></span>

    ![Vurgulanan parola metin kutusu ile iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="15a81-132">Seçin **sonraki** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="15a81-132">Select **Next** to continue.</span></span>

5. <span data-ttu-id="15a81-133">Bitirmek için Hizmetleri doğrulamasının tamamlanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="15a81-133">Wait for validation of the services to finish.</span></span> <span data-ttu-id="15a81-134">Bazı durumlarda, doğrulama başarısız ve yapılandırmasını güncelleştirmek ister.</span><span class="sxs-lookup"><span data-stu-id="15a81-134">In some cases, validation may fail and prompt you to update the configuration.</span></span> <span data-ttu-id="15a81-135">Doğrulama başarısız olursa, seçin **güncelleştirme**ve yapılandırma ve doğrulama hizmeti tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="15a81-135">If validation fails, select **Update**, and wait for the configuration and verification for the service to finish.</span></span>

    ![Güncelleştirme düğmesi vurgulanan iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="15a81-137">Güncelleştirme işlemi, Visual Studio için Data Lake araçları tarafından beklenenle için Hortonworks Sandbox yapılandırmasını değiştirmek için Ambari kullanır.</span><span class="sxs-lookup"><span data-stu-id="15a81-137">The update process uses Ambari to modify the Hortonworks Sandbox configuration to what is expected by the Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="15a81-138">Doğrulama tamamlandıktan sonra seçin **son** yapılandırmayı tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="15a81-138">After validation has finished, select **Finish** to complete configuration.</span></span>
    <span data-ttu-id="15a81-139">![Bitiş düğmesi vurgulanan iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="15a81-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="15a81-140">Geliştirme ortamınızı ve sanal makineye ayrılan bellek miktarını hızına bağlı olarak yapılandırın ve Hizmetleri doğrulamak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="15a81-140">Depending on the speed of your development environment, and the amount of memory allocated to the virtual machine, it can take several minutes to configure and validate the services.</span></span>

<span data-ttu-id="15a81-141">Bu adımları uyguladıktan sonra artık elinizde bir **Hdınsight yerel küme** Sunucu Gezgini girişi altında **Hdınsight** bölümü.</span><span class="sxs-lookup"><span data-stu-id="15a81-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under the **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="15a81-142">Bir Hive sorgusu Yaz</span><span class="sxs-lookup"><span data-stu-id="15a81-142">Write a Hive query</span></span>

<span data-ttu-id="15a81-143">Hive yapılandırılmış verilerle çalışmak için bir SQL benzeri sorgu dili (HiveQL) sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a81-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="15a81-144">Yerel küme karşı isteğe bağlı sorguları çalıştırmak öğrenmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="15a81-144">Use the following steps to learn how to run on-demand queries against the local cluster.</span></span>

1. <span data-ttu-id="15a81-145">İçinde **Sunucu Gezgini**, daha önce eklediğiniz yerel küme girişini sağ tıklatın ve ardından **Hive sorgusu yaz**.</span><span class="sxs-lookup"><span data-stu-id="15a81-145">In **Server Explorer**, right-click the entry for the local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, yazma vurgulanmış Hive sorgusu ile](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="15a81-147">Yeni bir sorgu penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="15a81-147">A new query window appears.</span></span> <span data-ttu-id="15a81-148">Burada hızla yapabilecekleriniz yazma ve yerel küme için bir sorgu gönderin.</span><span class="sxs-lookup"><span data-stu-id="15a81-148">Here you can quickly write and submit a query to the local cluster.</span></span>

2. <span data-ttu-id="15a81-149">Yeni Sorgu penceresinde aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="15a81-149">In the new query window, enter the following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="15a81-150">Sorguyu çalıştırmak için seçin **gönderme** pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="15a81-150">To run the query, select **Submit** at the top of the window.</span></span> <span data-ttu-id="15a81-151">Diğer değerleriyle bırakın (**toplu** ve sunucu adı) varsayılan değerleri.</span><span class="sxs-lookup"><span data-stu-id="15a81-151">Leave the other values (**Batch** and server name) at the default values.</span></span>

    ![Gönder düğmesi vurgulanan Sorgu penceresinin ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="15a81-153">Yanında aşağı açılan menüsünü kullanabilirsiniz **gönderme** seçmek için **Gelişmiş**.</span><span class="sxs-lookup"><span data-stu-id="15a81-153">You can also use the drop-down menu next to **Submit** to select **Advanced**.</span></span> <span data-ttu-id="15a81-154">Gelişmiş seçenekleri, iş gönderdiğinizde ek seçenekler sağlar olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="15a81-154">Advanced options allow you to provide additional options when you submit the job.</span></span>

    ![Gönderme betik ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="15a81-156">Sorgu gönderdikten sonra iş durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="15a81-156">After you submit the query, the job status appears.</span></span> <span data-ttu-id="15a81-157">İş durumu Hadoop tarafından işlenen iş hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="15a81-157">The job status displays information about the job as it is processed by Hadoop.</span></span> <span data-ttu-id="15a81-158">**İş durumu** işinin durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a81-158">**Job State** provides the status of the job.</span></span> <span data-ttu-id="15a81-159">Durumu düzenli aralıklarla güncelleştirilir veya durumu el ile yenilemek için Yenile simgesine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a81-159">The state is updated periodically, or you can use the refresh icon to refresh the state manually.</span></span>

    ![İş vurgulanmış durumu ile iş görünümünde ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="15a81-161">Sonra **iş durumu** değişikliklerini **tamamlandı**, yönlendirilmiş Çevrimsiz grafik (DAG) görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="15a81-161">After the **Job State** changes to **Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="15a81-162">Bu diyagramda tarafından Tez Hive sorgusu işlenirken belirlendi yürütme yolu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="15a81-162">This diagram describes the execution path that was determined by Tez when processing the Hive query.</span></span> <span data-ttu-id="15a81-163">Tez Hive için varsayılan yürütme altyapısı yerel kümedeki ' dir.</span><span class="sxs-lookup"><span data-stu-id="15a81-163">Tez is the default execution engine for Hive on the local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15a81-164">Linux tabanlı Hdınsight kümelerini kullanırken Tez de varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="15a81-164">Tez is also the default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="15a81-165">Varsayılan Windows tabanlı Hdınsight üzerinde değil.</span><span class="sxs-lookup"><span data-stu-id="15a81-165">It is not the default on Windows-based HDInsight.</span></span> <span data-ttu-id="15a81-166">Kullanmak için satırın eklemelisiniz `set hive.execution.engine = tez;` Hive sorgunuzu başlangıcına.</span><span class="sxs-lookup"><span data-stu-id="15a81-166">To use it there, you must add the line `set hive.execution.engine = tez;` to the beginning of your Hive query.</span></span>

    <span data-ttu-id="15a81-167">Kullanım **iş çıktısı** çıkışı görüntülemek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="15a81-167">Use the **Job Output** link to view the output.</span></span> <span data-ttu-id="15a81-168">Bu durumda, bu 823, sample_08 tablodaki satır sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="15a81-168">In this case, it is 823, the number of rows in the sample_08 table.</span></span> <span data-ttu-id="15a81-169">Kullanarak işle ilgili tanılama bilgileri görüntüleyebilirsiniz **iş günlüğü** ve **karşıdan YARN günlüğü** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="15a81-169">You can view diagnostics information about the job by using the **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="15a81-170">Ayrıca Hive işleri etkileşimli olarak değiştirerek çalıştırabilirsiniz **toplu** alanı **etkileşimli**.</span><span class="sxs-lookup"><span data-stu-id="15a81-170">You can also run Hive jobs interactively by changing the **Batch** field to **Interactive**.</span></span> <span data-ttu-id="15a81-171">Ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="15a81-171">Then select **Execute**.</span></span>

    ![Vurgulanan etkileşimli ekran ve yürütme düğmeleri](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="15a81-173">Etkileşimli bir sorgu için işleme sırasında oluşturulan çıktı günlüğünü akışları **HiveServer2 çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="15a81-173">An interactive query streams the output log generated during processing to the **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="15a81-174">Kullanılabilir aynı bilgilerdir **iş günlüğü** bir işi tamamlandıktan sonra bağlantı.</span><span class="sxs-lookup"><span data-stu-id="15a81-174">The information is the same that is available from the **Job Log** link after a job has finished.</span></span>

    ![Çıktı oturum ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="15a81-176">Bir Hive projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a81-176">Create a Hive project</span></span>

<span data-ttu-id="15a81-177">Ayrıca, birden çok Hive betiği içeren bir proje oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a81-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="15a81-178">Komut dosyaları ilgili ya da bir sürüm denetim sisteminde komut dosyalarını depolamak istediğiniz zaman bir proje kullanın.</span><span class="sxs-lookup"><span data-stu-id="15a81-178">Use a project when you have related scripts or want to store scripts in a version control system.</span></span>

1. <span data-ttu-id="15a81-179">Visual Studio'da seçin **dosya**, **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="15a81-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="15a81-180">Projeleri listesinden genişletin **şablonları**, genişletin **Azure Data Lake**ve ardından **HIVE (Hdınsight)**.</span><span class="sxs-lookup"><span data-stu-id="15a81-180">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="15a81-181">Şablonları listesinden seçin **örnek Hive**.</span><span class="sxs-lookup"><span data-stu-id="15a81-181">From the list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="15a81-182">Bir ad ve konum girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="15a81-182">Enter a name and location, and then select **OK**.</span></span>

    ![Yeni Proje penceresinin ekran penceresiyle Azure Data Lake, HIVE, örnek Hive ve Tamam'ı vurgulanmış](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="15a81-184">**Örnek Hive** projeyi içeren iki komut **WebLogAnalysis.hql** ve **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="15a81-184">The **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="15a81-185">Bu komut dosyaları aynı kullanarak gönderebilirsiniz **gönderme** pencerenin üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="15a81-185">You can submit these scripts by using the same **Submit** button at the top of the window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="15a81-186">Pig proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a81-186">Create a Pig project</span></span>

<span data-ttu-id="15a81-187">Hive yapılandırılmış verilerle çalışmak için SQL benzeri bir dille sağlarken, Pig verileri dönüşümleri gerçekleştirerek çalışır.</span><span class="sxs-lookup"><span data-stu-id="15a81-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="15a81-188">Pig bir ardışık düzen Dönüşümlerin geliştirmek izin veren bir dil (Pig Latin) sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a81-188">Pig provides a language (Pig Latin) that allows you to develop a pipeline of transformations.</span></span> <span data-ttu-id="15a81-189">Yerel kümeyle pig kullanmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="15a81-189">To use Pig with the local cluster, follow these steps:</span></span>

1. <span data-ttu-id="15a81-190">Visual Studio'yu açın ve seçin **dosya**, **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="15a81-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="15a81-191">Projeleri listesinden genişletin **şablonları**, genişletin **Azure Data Lake**ve ardından **Pig (Hdınsight)**.</span><span class="sxs-lookup"><span data-stu-id="15a81-191">From the list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="15a81-192">Şablonları listesinden seçin **Pig uygulama**.</span><span class="sxs-lookup"><span data-stu-id="15a81-192">From the list of templates, select **Pig Application**.</span></span> <span data-ttu-id="15a81-193">Konum, bir ad girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="15a81-193">Enter a name, location, and then select **OK**.</span></span>

    ![Yeni Proje penceresinin ekran penceresiyle Azure Data Lake, Pig, Pig uygulama ve Tamam'ı vurgulanmış](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="15a81-195">İçeriği aşağıdaki metni girin **script.pig** bu proje ile oluşturulmuş dosyası.</span><span class="sxs-lookup"><span data-stu-id="15a81-195">Enter the following text as the contents of the **script.pig** file that was created with this project.</span></span>

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

    <span data-ttu-id="15a81-196">Pig, Hive farklı bir dil kullanıyor, ancak işler çalışma şeklini iki diller arasında tutarlıdır aracılığıyla **gönderme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="15a81-196">While Pig uses a different language than Hive, how you run the jobs is consistent between both languages, through the **Submit** button.</span></span> <span data-ttu-id="15a81-197">Yanındaki açılan seçme **gönderme** Pig için Gelişmiş Gönder iletişim kutusu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="15a81-197">Selecting the drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Gönderme betik ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="15a81-199">İş durumunu ve çıkışını de görüntülenir, Hive sorgusu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="15a81-199">The job status and output is also displayed, the same as a Hive query.</span></span>

    ![Tamamlanan Pig işi ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="15a81-201">İşleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="15a81-201">View jobs</span></span>

<span data-ttu-id="15a81-202">Data Lake araçları de kolayca Hadoop üzerinde çalışan işleri hakkındaki bilgileri görüntülemek olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="15a81-202">Data Lake tools also allow you to easily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="15a81-203">Yerel kümede çalışan işleri görmek için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="15a81-203">Use the following steps to see the jobs that have been run on the local cluster.</span></span>

1. <span data-ttu-id="15a81-204">Gelen **Sunucu Gezgini**yerel kümeye sağ tıklayın ve ardından **işleri görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="15a81-204">From **Server Explorer**, right-click the local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="15a81-205">Kümesine gönderilen işler listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="15a81-205">A list of jobs that have been submitted to the cluster is displayed.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, ile vurgulanan işleri görüntüle](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="15a81-207">İşlerini listesinden bir iş ayrıntılarını görüntülemek için seçin.</span><span class="sxs-lookup"><span data-stu-id="15a81-207">From the list of jobs, select one to view the job details.</span></span>

    ![Ekran görüntüsü, iş tarayıcıyla, vurgulanmış işlerden biri](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="15a81-209">Görüntülenen bilgiler, çıktı görüntülemek ve bilgileri günlüğe kaydetmek için bağlantılar dahil olmak üzere bir Hive veya Pig sorgu çalıştırdıktan sonra gördüğünüz için benzer.</span><span class="sxs-lookup"><span data-stu-id="15a81-209">The information displayed is similar to what you see after running a Hive or Pig query, including links to view the output and log information.</span></span>

3. <span data-ttu-id="15a81-210">Ayrıca, değiştirebilir ve buradan işi yeniden gönderin.</span><span class="sxs-lookup"><span data-stu-id="15a81-210">You can also modify and resubmit the job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="15a81-211">Hive veritabanları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="15a81-211">View Hive databases</span></span>

1. <span data-ttu-id="15a81-212">İçinde **Sunucu Gezgini**, genişletin **Hdınsight yerel küme** girişi genişletin ve ardından **Hive veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="15a81-212">In **Server Explorer**, expand the **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="15a81-213">**Varsayılan** ve **xademo** veritabanları yerel kümedeki görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="15a81-213">The **Default** and **xademo** databases on the local cluster are displayed.</span></span> <span data-ttu-id="15a81-214">Bir veritabanını genişletmeden veritabanının içindeki tabloları gösterir.</span><span class="sxs-lookup"><span data-stu-id="15a81-214">Expanding a database shows the tables within the database.</span></span>

    ![Sunucu Gezgini ekran veritabanları ile genişletilmiş](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="15a81-216">Bir tablo genişletme tablosunun sütunlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="15a81-216">Expanding a table displays the columns for that table.</span></span> <span data-ttu-id="15a81-217">Verileri hızlı bir şekilde görüntülemek için bir tabloyu sağ tıklatın ve seçin **ilk 100 satırı görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="15a81-217">To quickly view the data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Ekran görüntüsü, Sunucu Gezgini, Genişletilmiş Tablo ve Görünüm ilk 100 seçilen satırı ile](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="15a81-219">Veritabanı ve tablo özellikleri</span><span class="sxs-lookup"><span data-stu-id="15a81-219">Database and table properties</span></span>

<span data-ttu-id="15a81-220">Bir veritabanı veya tablo özelliklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a81-220">You can view the properties of a database or table.</span></span> <span data-ttu-id="15a81-221">Seçme **Özellikler** Özellikler penceresinde seçili öğe için ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="15a81-221">Selecting **Properties** displays details for the selected item in the properties window.</span></span> <span data-ttu-id="15a81-222">Örneğin, aşağıdaki ekran görüntüsünde gösterilen bilgiler bakın:</span><span class="sxs-lookup"><span data-stu-id="15a81-222">For example, see the information shown in the following screenshot:</span></span>

![Ekran görüntüsü, Özellikler penceresi](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="15a81-224">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="15a81-224">Create a table</span></span>

<span data-ttu-id="15a81-225">Bir tablo oluşturmak için bir veritabanına sağ tıklayın ve ardından **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="15a81-225">To create a table, right-click a database, and then select **Create Table**.</span></span>

![Ekran görüntüsü, Sunucu Gezgini, ile vurgulanan Tablo Oluştur](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="15a81-227">Daha sonra bir form kullanarak tablosu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a81-227">You can then create the table using a form.</span></span> <span data-ttu-id="15a81-228">Aşağıdaki ekran görüntüsünde alt kısmındaki tablo oluşturmak için kullanılan ham HiveQL görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15a81-228">At the bottom of the following screenshot, you can see the raw HiveQL that is used to create the table.</span></span>

![Bir tablo oluşturmak için kullanılan formu ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="15a81-230">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15a81-230">Next steps</span></span>

* [<span data-ttu-id="15a81-231">Hortonworks Sandbox ipleri öğrenme</span><span class="sxs-lookup"><span data-stu-id="15a81-231">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="15a81-232">Hadoop Öğreticisi - HDP ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="15a81-232">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
