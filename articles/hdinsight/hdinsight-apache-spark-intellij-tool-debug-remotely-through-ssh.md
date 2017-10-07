---
title: "Intellij için Azure Araç Seti: SSH üzerinden uzaktan hata ayıklama Spark uygulamaları | Microsoft Docs"
description: "Hdınsight üzerinde uzaktan Intellij toodebug uygulamalar için Hdınsight araçları Azure Araç Seti toouse SSH nasıl kümeleri üzerinde adım adım yönergeler"
keywords: "ıntellij, debugging ıntellij, ssh, uzak ıntellij, hdınsight uzaktan hata ayıklama, ıntellij, hata ayıklama hata ayıklama"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a><span data-ttu-id="5336f-104">SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5336f-104">Debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH</span></span>

<span data-ttu-id="5336f-105">Bu makalede hakkında adım adım yönergeler sağlar toouse Hdınsight araçları Azure araç seti, Hdınsight kümesi üzerinde uzaktan Intellij toodebug uygulamalar için.</span><span class="sxs-lookup"><span data-stu-id="5336f-105">This article provides step-by-step guidance on how toouse HDInsight Tools in Azure Toolkit for IntelliJ toodebug applications remotely on an HDInsight cluster.</span></span> <span data-ttu-id="5336f-106">toodebug, projenizin hello de görüntüleyebilirsiniz [Intellij için Hdınsight Spark hata ayıklama uygulamaları Azure araç seti ile](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="5336f-106">toodebug your project, you can also view hello [Debug HDInsight Spark applications with Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.</span></span>

<span data-ttu-id="5336f-107">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="5336f-107">**Prerequisites**</span></span>

* <span data-ttu-id="5336f-108">**Azure Araç Seti Intellij için Hdınsight Araçları**.</span><span class="sxs-lookup"><span data-stu-id="5336f-108">**HDInsight Tools in Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="5336f-109">Bu araç Intellij için Azure araç seti bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="5336f-109">This tool is part of Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="5336f-110">Daha fazla bilgi için bkz: [Intellij için Azure Araç Seti yüklemek](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span><span class="sxs-lookup"><span data-stu-id="5336f-110">For more information, see [Install Azure Toolkit for IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).</span></span>
* <span data-ttu-id="5336f-111">**Intellij için Azure Araç Seti**.</span><span class="sxs-lookup"><span data-stu-id="5336f-111">**Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="5336f-112">Bu araç seti toocreate Spark uygulamaları bir Hdınsight kümesi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5336f-112">Use this toolkit toocreate Spark applications for an HDInsight cluster.</span></span> <span data-ttu-id="5336f-113">Daha fazla bilgi için hello yönergeleri izleyin [Hdınsight kümesi için Intellij toocreate Spark uygulamaları için kullanım Azure Araç Seti](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span><span class="sxs-lookup"><span data-stu-id="5336f-113">For more information, follow hello instructions in [Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).</span></span>
* <span data-ttu-id="5336f-114">**Hdınsight SSH hizmeti kullanıcı adı ve parola yönetimi ile**.</span><span class="sxs-lookup"><span data-stu-id="5336f-114">**HDInsight SSH service with username and password management**.</span></span> <span data-ttu-id="5336f-115">Daha fazla bilgi için bkz: [tooHDInsight (Hadoop) SSH kullanarak bağlanmak](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) ve [kullanım SSH tünel tooaccess Ambari web kullanıcı Arabirimi, kaynak, iş, Oozie ve diğer web Uı'lar](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span><span class="sxs-lookup"><span data-stu-id="5336f-115">For more information, see [Connect tooHDInsight (Hadoop) by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Use SSH tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel).</span></span> 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a><span data-ttu-id="5336f-116">Spark Scala uygulama oluşturma ve uzaktan hata ayıklama için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5336f-116">Create a Spark Scala application and configure it for remote debugging</span></span>

1. <span data-ttu-id="5336f-117">Intellij Idea başlatın ve bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5336f-117">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="5336f-118">Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="5336f-118">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="5336f-119">a.</span><span class="sxs-lookup"><span data-stu-id="5336f-119">a.</span></span> <span data-ttu-id="5336f-120">Seçin **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="5336f-120">Select **HDInsight**.</span></span> 

   <span data-ttu-id="5336f-121">b.</span><span class="sxs-lookup"><span data-stu-id="5336f-121">b.</span></span> <span data-ttu-id="5336f-122">Tercihinize bağlı bir Java veya Scala şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="5336f-122">Select a Java or Scala template based on your preference.</span></span> <span data-ttu-id="5336f-123">Seçenekler aşağıdaki hello arasında seçin:</span><span class="sxs-lookup"><span data-stu-id="5336f-123">Select between hello following options:</span></span>

      - <span data-ttu-id="5336f-124">**(Scala) hdınsight'ta Spark**</span><span class="sxs-lookup"><span data-stu-id="5336f-124">**Spark on HDInsight (Scala)**</span></span>

      - <span data-ttu-id="5336f-125">**(Java) hdınsight'ta Spark**</span><span class="sxs-lookup"><span data-stu-id="5336f-125">**Spark on HDInsight (Java)**</span></span>

      - <span data-ttu-id="5336f-126">**Spark Hdınsight kümesi çalışma örneği (Scala)**</span><span class="sxs-lookup"><span data-stu-id="5336f-126">**Spark on HDInsight Cluster Run Sample (Scala)**</span></span>

      <span data-ttu-id="5336f-127">Bu örnekte bir **Spark Hdınsight küme çalıştırmak örneği (Scala)** şablonu.</span><span class="sxs-lookup"><span data-stu-id="5336f-127">This example uses a **Spark on HDInsight Cluster Run Sample (Scala)** template.</span></span>

   <span data-ttu-id="5336f-128">c.</span><span class="sxs-lookup"><span data-stu-id="5336f-128">c.</span></span> <span data-ttu-id="5336f-129">Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="5336f-129">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      - <span data-ttu-id="5336f-130">**Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği</span><span class="sxs-lookup"><span data-stu-id="5336f-130">**Maven**, for Scala project-creation wizard support</span></span>

      -  <span data-ttu-id="5336f-131">**SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5336f-131">**SBT**, for managing hello dependencies and building for hello Scala project</span></span> 

      ![Hata ayıklama projesi oluşturma](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   <span data-ttu-id="5336f-133">d.</span><span class="sxs-lookup"><span data-stu-id="5336f-133">d.</span></span> <span data-ttu-id="5336f-134">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5336f-134">Select **Next**.</span></span>     
 
3. <span data-ttu-id="5336f-135">Merhaba, sonraki **yeni proje** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="5336f-135">In hello next **New Project** window, do hello following:</span></span>

   ![Merhaba Spark SDK'yı seçin](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   <span data-ttu-id="5336f-137">a.</span><span class="sxs-lookup"><span data-stu-id="5336f-137">a.</span></span> <span data-ttu-id="5336f-138">Bir proje adı ve proje konumu girin.</span><span class="sxs-lookup"><span data-stu-id="5336f-138">Enter a project name and project location.</span></span>

   <span data-ttu-id="5336f-139">b.</span><span class="sxs-lookup"><span data-stu-id="5336f-139">b.</span></span> <span data-ttu-id="5336f-140">Merhaba, **proje SDK** aşağı açılan listesinden, **Java 1.8** için **2.x Spark** seçin ya da küme **Java 1.7** için **Spark 1. x** küme.</span><span class="sxs-lookup"><span data-stu-id="5336f-140">In hello **Project SDK** drop-down list, select **Java 1.8** for **Spark 2.x** cluster or select **Java 1.7** for **Spark 1.x** cluster.</span></span>

   <span data-ttu-id="5336f-141">c.</span><span class="sxs-lookup"><span data-stu-id="5336f-141">c.</span></span> <span data-ttu-id="5336f-142">Merhaba, **Spark sürüm** aşağı açılan listesinde, hello Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK hello doğru sürümü tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="5336f-142">In hello **Spark Version** drop-down list, hello Scala project creation wizard integrates hello correct version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="5336f-143">Merhaba spark küme sürüm 2.0 eskiyse, seçin **1.x Spark**.</span><span class="sxs-lookup"><span data-stu-id="5336f-143">If hello spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="5336f-144">Aksi takdirde seçin **2.x Spark.**</span><span class="sxs-lookup"><span data-stu-id="5336f-144">Otherwise, select **Spark 2.x.**</span></span> <span data-ttu-id="5336f-145">Bu örnekte **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="5336f-145">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

   <span data-ttu-id="5336f-146">d.</span><span class="sxs-lookup"><span data-stu-id="5336f-146">d.</span></span> <span data-ttu-id="5336f-147">**Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="5336f-147">Select **Finish**.</span></span>

4. <span data-ttu-id="5336f-148">Seçin **src** > **ana** > **scala** tooopen hello proje kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="5336f-148">Select **src** > **main** > **scala** tooopen your code in hello project.</span></span> <span data-ttu-id="5336f-149">Bu örnek hello kullanır **SparkCore_wasbloTest** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="5336f-149">This example uses hello **SparkCore_wasbloTest** script.</span></span>

5. <span data-ttu-id="5336f-150">tooaccess hello **yapılandırmalarını Düzenle** menüsü, hello sağ üst köşesinde select hello simgesi.</span><span class="sxs-lookup"><span data-stu-id="5336f-150">tooaccess hello **Edit Configurations** menu, select hello icon in hello upper-right corner.</span></span> <span data-ttu-id="5336f-151">Bu menüden oluşturabilir veya uzaktan hata ayıklama için hello yapılandırmaları düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5336f-151">From this menu, you can create or edit hello configurations for remote debugging.</span></span>

   ![Yapılandırmaları Düzenle](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. <span data-ttu-id="5336f-153">Merhaba, **Çalıştır/hata ayıklama yapılandırmaları** iletişim kutusu, select hello artı işareti (**+**).</span><span class="sxs-lookup"><span data-stu-id="5336f-153">In hello **Run/Debug Configurations** dialog box, select hello plus sign (**+**).</span></span> <span data-ttu-id="5336f-154">Merhaba seçip **Spark işi Gönder** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5336f-154">Then select hello **Submit Spark Job** option.</span></span>

   ![Yeni yapılandırma ekleyin](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. <span data-ttu-id="5336f-156">İçin bilgileri girin **adı**, **Spark kümesi**, ve **ana sınıf adı**.</span><span class="sxs-lookup"><span data-stu-id="5336f-156">Enter information for **Name**, **Spark cluster**, and **Main class name**.</span></span> <span data-ttu-id="5336f-157">Ardından **Gelişmiş Yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="5336f-157">Then select **Advanced configuration**.</span></span> 

   ![Hata ayıklama yapılandırmaları çalıştırma](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. <span data-ttu-id="5336f-159">Merhaba, **Spark gönderimi Gelişmiş Yapılandırma** iletişim kutusunda **etkinleştirmek Spark uzaktan hata ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="5336f-159">In hello **Spark Submission Advanced Configuration** dialog box, select **Enable Spark remote debug**.</span></span> <span data-ttu-id="5336f-160">Merhaba SSH kullanıcı adı girin ve ardından bir parola girin veya özel bir anahtar dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="5336f-160">Enter hello SSH username, and then enter a password or use a private key file.</span></span> <span data-ttu-id="5336f-161">toosave hello yapılandırma, select **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5336f-161">toosave hello configuration, select **OK**.</span></span>

   ![Spark uzaktan hata ayıklama etkinleştirme](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. <span data-ttu-id="5336f-163">Merhaba yapılandırma şimdi sağladığınız hello adıyla kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5336f-163">hello configuration is now saved with hello name you provided.</span></span> <span data-ttu-id="5336f-164">tooview hello yapılandırma ayrıntılarını, select hello yapılandırma adı.</span><span class="sxs-lookup"><span data-stu-id="5336f-164">tooview hello configuration details, select hello configuration name.</span></span> <span data-ttu-id="5336f-165">toomake değişiklikleri seçin **yapılandırmalarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="5336f-165">toomake changes, select **Edit Configurations**.</span></span> 

10. <span data-ttu-id="5336f-166">Merhaba yapılandırma ayarlarını tamamladığınızda hello uzaktan küme karşı Merhaba projeyi çalıştırın veya uzaktan hata ayıklama gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5336f-166">After you complete hello configurations settings, you can run hello project against hello remote cluster or perform remote debugging.</span></span>

## <a name="learn-how-tooperform-remote-debugging"></a><span data-ttu-id="5336f-167">Bilgi nasıl tooperform uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5336f-167">Learn how tooperform remote debugging</span></span>
### <a name="scenario-1-perform-remote-run"></a><span data-ttu-id="5336f-168">Senaryo 1: Uzak çalışma gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="5336f-168">Scenario 1: Perform remote run</span></span>

<span data-ttu-id="5336f-169">Bu bölümde, nasıl gösteriyoruz toodebug sürücüleri ve yürütücüler.</span><span class="sxs-lookup"><span data-stu-id="5336f-169">In this section, we show you how toodebug drivers and executors.</span></span>

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. <span data-ttu-id="5336f-170">Kesme noktaları kurulumu ve hello ardından **hata ayıklama** simgesi.</span><span class="sxs-lookup"><span data-stu-id="5336f-170">Set up breaking points, and then select hello **Debug** icon.</span></span>

   ![Merhaba hata ayıklama simgesini seçin](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. <span data-ttu-id="5336f-172">Merhaba program yürütme hello kesme noktası ulaştığında, gördüğünüz bir **sürücü** sekmesi ve iki **Yürütücü** hello sekmeleri **hata ayıklayıcı** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5336f-172">When hello program execution reaches hello breaking point, you see a **Driver** tab and two **Executor** tabs in hello **Debugger** pane.</span></span> <span data-ttu-id="5336f-173">Select hello **Sürdür Program** sonra hello sonraki kesme ulaştığında ve hello karşılık gelen üzerinde odaklanır hello kod çalıştırmasını simgesi toocontinue **Yürütücü** sekmesi. Merhaba karşılık gelen üzerinde hello yürütme günlüklerini gözden geçirebilirsiniz **konsol** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5336f-173">Select hello **Resume Program** icon toocontinue running hello code, which then reaches hello next breakpoint and focuses on hello corresponding **Executor** tab. You can review hello execution logs on hello corresponding **Console** tab.</span></span>

   ![Hata ayıklama sekmesi](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="5336f-175">Senaryo 2: uzaktan hata ayıklama ve hata düzeltme gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="5336f-175">Scenario 2: Perform remote debugging and bug fixing</span></span>
<span data-ttu-id="5336f-176">Bu bölümde, nasıl kullanarak toodynamically güncelleştirme hello değişken değeri hello yetenek basit bir düzeltme için hata ayıklama Intellij gösteriyoruz.</span><span class="sxs-lookup"><span data-stu-id="5336f-176">In this section, we show you how toodynamically update hello variable value by using hello IntelliJ debugging capability for a simple fix.</span></span> <span data-ttu-id="5336f-177">Aşağıdaki kod örneğine hello Hello hedef dosyası zaten mevcut olduğundan özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="5336f-177">In hello following code example, an exception is thrown because hello target file already exists.</span></span>
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a><span data-ttu-id="5336f-178">tooperform uzaktan hata ayıklama ve hata düzeltme</span><span class="sxs-lookup"><span data-stu-id="5336f-178">tooperform remote debugging and bug fixing</span></span>
1. <span data-ttu-id="5336f-179">İki kesme noktaları kurulumu ve hello ardından **hata ayıklama** simgesi toostart hello uzaktan hata ayıklama işlemi.</span><span class="sxs-lookup"><span data-stu-id="5336f-179">Set up two breaking points, and then select hello **Debug** icon toostart hello remote debugging process.</span></span>

2. <span data-ttu-id="5336f-180">Merhaba kod hello ilk kesme noktası durdurur ve hello parametre ve değişken bilgileri hello gösterilen **değişkenleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5336f-180">hello code stops at hello first breaking point, and hello parameter and variable information are shown in hello **Variables** pane.</span></span> 

3. <span data-ttu-id="5336f-181">Select hello **Sürdür Program** simgesi toocontinue.</span><span class="sxs-lookup"><span data-stu-id="5336f-181">Select hello **Resume Program** icon toocontinue.</span></span> <span data-ttu-id="5336f-182">Merhaba kod hello ikinci noktada durdurur.</span><span class="sxs-lookup"><span data-stu-id="5336f-182">hello code stops at hello second point.</span></span> <span data-ttu-id="5336f-183">beklendiği gibi Hello özel durum yakalandı.</span><span class="sxs-lookup"><span data-stu-id="5336f-183">hello exception is caught as expected.</span></span>

  ![Hata durum](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. <span data-ttu-id="5336f-185">Select hello **Sürdür Program** yeniden simgesi.</span><span class="sxs-lookup"><span data-stu-id="5336f-185">Select hello **Resume Program** icon again.</span></span> <span data-ttu-id="5336f-186">Merhaba **Hdınsight Spark gönderme** penceresi bir "işi çalıştırma başarısız oldu" hatasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5336f-186">hello **HDInsight Spark Submission** window displays a "job run failed" error.</span></span>

  ![Hata gönderme](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. <span data-ttu-id="5336f-188">Merhaba Intellij hata ayıklama özelliğini kullanarak toodynamically güncelleştirme hello değişken değerini seçin **hata ayıklama** yeniden.</span><span class="sxs-lookup"><span data-stu-id="5336f-188">toodynamically update hello variable value by using hello IntelliJ debugging capability, select **Debug** again.</span></span> <span data-ttu-id="5336f-189">Merhaba **değişkenleri** yeniden bölmesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="5336f-189">hello **Variables** pane appears again.</span></span> 

6. <span data-ttu-id="5336f-190">Sağ hello hello hedefte **hata ayıklama** sekmesini tıklatın ve ardından **değeri ayarlanmış**.</span><span class="sxs-lookup"><span data-stu-id="5336f-190">Right-click hello target on hello **Debug** tab, and then select **Set Value**.</span></span> <span data-ttu-id="5336f-191">Ardından, hello değişken için yeni bir değer girin.</span><span class="sxs-lookup"><span data-stu-id="5336f-191">Next, enter a new value for hello variable.</span></span> <span data-ttu-id="5336f-192">Ardından **Enter** toosave hello değeri.</span><span class="sxs-lookup"><span data-stu-id="5336f-192">Then select **Enter** toosave hello value.</span></span> 

  ![Değerini ayarla](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. <span data-ttu-id="5336f-194">Select hello **Sürdür Program** simgesi toocontinue toorun hello program.</span><span class="sxs-lookup"><span data-stu-id="5336f-194">Select hello **Resume Program** icon toocontinue toorun hello program.</span></span> <span data-ttu-id="5336f-195">Bu süre, hiçbir özel durum yakalandı.</span><span class="sxs-lookup"><span data-stu-id="5336f-195">This time, no exception is caught.</span></span> <span data-ttu-id="5336f-196">Merhaba Proje başarıyla tüm özel durumlar çalışır görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5336f-196">You can see that hello project runs successfully without any exceptions.</span></span>

  ![Özel durum olmadan hata ayıklama](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <span data-ttu-id="5336f-198"><a name="seealso"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5336f-198"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="5336f-199">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="5336f-199">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="5336f-200">Tanıtım</span><span class="sxs-lookup"><span data-stu-id="5336f-200">Demo</span></span>
* <span data-ttu-id="5336f-201">Scala proje oluştur (video): [Spark Scala uygulamaları oluşturma](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5336f-201">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="5336f-202">Uzaktan hata ayıklama (video): [Hdınsight kümesi üzerinde uzaktan Intellij toodebug Spark uygulamalar için kullanım Azure Araç Seti](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5336f-202">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on an HDInsight cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="5336f-203">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="5336f-203">Scenarios</span></span>
* [<span data-ttu-id="5336f-204">BI ile Spark: BI araçlarıyla Hdınsight'ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="5336f-204">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5336f-205">Machine Learning ile Spark: HVAC verilerini kullanarak sıcaklık oluşturma Hdınsight tooanalyze kullanım Spark</span><span class="sxs-lookup"><span data-stu-id="5336f-205">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5336f-206">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-206">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5336f-207">Spark akış: Spark Hdınsight toobuild gerçek zamanlı akış uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-207">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="5336f-208">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="5336f-208">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5336f-209">Uygulamaları oluşturma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5336f-209">Create and run applications</span></span>
* [<span data-ttu-id="5336f-210">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="5336f-210">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5336f-211">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5336f-211">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5336f-212">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="5336f-212">Tools and extensions</span></span>
* [<span data-ttu-id="5336f-213">Hdınsight kümesi için Intellij toocreate Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-213">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5336f-214">VPN üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-214">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5336f-215">Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-215">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="5336f-216">Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="5336f-216">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="5336f-217">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-217">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5336f-218">Merhaba Hdınsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="5336f-218">Kernels available for Jupyter notebook in hello Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5336f-219">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="5336f-219">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5336f-220">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="5336f-220">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5336f-221">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="5336f-221">Manage resources</span></span>
* [<span data-ttu-id="5336f-222">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="5336f-222">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5336f-223">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5336f-223">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
