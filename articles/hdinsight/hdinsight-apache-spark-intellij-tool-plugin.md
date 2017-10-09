---
title: "Intellij için Azure Araç Seti: Spark Hdınsight kümesi için uygulama oluşturma | Microsoft Docs"
description: "Intellij toodevelop Spark Scala içinde yazılmış uygulamalar için Hello Azure araç seti kullanın ve bunları tooan Hdınsight Spark kümesi gönderin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="bc59e-103">Hdınsight kümesi için Intellij toocreate Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-103">Use Azure Toolkit for IntelliJ toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="bc59e-104">Intellij eklenti toodevelop Spark Scala içinde yazılmış uygulamalar için Hello Azure araç seti kullanın ve bunları tooan Hdınsight Spark kümesi hello Intellij tümleşik geliştirme ortamı (IDE) doğrudan gönderebilirler.</span><span class="sxs-lookup"><span data-stu-id="bc59e-104">Use hello Azure Toolkit for IntelliJ plug-in toodevelop Spark applications written in Scala, and then submit them tooan HDInsight Spark cluster directly from hello IntelliJ integrated development environment (IDE).</span></span> <span data-ttu-id="bc59e-105">Merhaba birkaç yolla eklentisi kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc59e-105">You can use hello plug-in in a few ways:</span></span>

* <span data-ttu-id="bc59e-106">Geliştirme ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının gönderin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-106">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="bc59e-107">Azure Hdınsight Spark küme kaynaklarına erişim.</span><span class="sxs-lookup"><span data-stu-id="bc59e-107">Access your Azure HDInsight Spark cluster resources.</span></span>
* <span data-ttu-id="bc59e-108">Geliştirme ve Scala Spark uygulama yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc59e-108">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="bc59e-109">toocreate proje, görünüm hello [hello Intellij için Azure araç seti ile Spark uygulamaları oluşturmak](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span><span class="sxs-lookup"><span data-stu-id="bc59e-109">toocreate your project, view hello [Create Spark Applications with hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc59e-110">Bu eklenti toocreate kullanın ve yalnızca Linux'ta Hdınsight Spark kümesinde uygulamalar gönderin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-110">You can use this plug-in toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="bc59e-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc59e-111">Prerequisites</span></span>

- <span data-ttu-id="bc59e-112">Hdınsight Linux üzerinde Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="bc59e-112">An Apache Spark cluster on HDInsight Linux.</span></span> <span data-ttu-id="bc59e-113">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="bc59e-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
- <span data-ttu-id="bc59e-114">Oracle Java Geliştirme Seti.</span><span class="sxs-lookup"><span data-stu-id="bc59e-114">Oracle Java Development Kit.</span></span> <span data-ttu-id="bc59e-115">Merhaba yükleme [Oracle Web sitesi](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="bc59e-115">You can install it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
- <span data-ttu-id="bc59e-116">Intellij Idea.</span><span class="sxs-lookup"><span data-stu-id="bc59e-116">IntelliJ IDEA.</span></span> <span data-ttu-id="bc59e-117">Bu makalede sürümünü 2017.1 kullanır.</span><span class="sxs-lookup"><span data-stu-id="bc59e-117">This article uses version 2017.1.</span></span> <span data-ttu-id="bc59e-118">Merhaba yükleme [JetBrains Web sitesi](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="bc59e-118">You can install it from hello [JetBrains website](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-azure-toolkit-for-intellij"></a><span data-ttu-id="bc59e-119">Intellij için Azure Araç Seti yükleyin</span><span class="sxs-lookup"><span data-stu-id="bc59e-119">Install Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="bc59e-120">Yükleme yönergeleri için bkz: [Intellij için Azure Araç Seti yüklemek](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="bc59e-120">For installation instructions, see [Install Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="bc59e-121">Azure aboneliği tooyour oturum</span><span class="sxs-lookup"><span data-stu-id="bc59e-121">Sign in tooyour Azure subscription</span></span>

1. <span data-ttu-id="bc59e-122">Merhaba Intellij IDE başlatın ve Azure Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="bc59e-122">Start hello IntelliJ IDE, and open Azure Explorer.</span></span> <span data-ttu-id="bc59e-123">Merhaba üzerinde **Görünüm** menüsünde, select **aracı Windows**ve ardından **Azure Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-123">On hello **View** menu, select **Tool Windows**, and then select **Azure Explorer**.</span></span>
       
   ![Hello Azure Gezgini bağlantısı](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. <span data-ttu-id="bc59e-125">Sağ hello **Azure** düğümünü ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-125">Right-click hello **Azure** node, and then select **Sign In**.</span></span>

3. <span data-ttu-id="bc59e-126">Merhaba, **Azure oturum açma** iletişim kutusunda **oturum**ve ardından Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-126">In hello **Azure Sign In** dialog box, select **Sign in**, and then enter your Azure credentials.</span></span>

    ![Hello Azure oturum açma iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. <span data-ttu-id="bc59e-128">Oturum açtınız sonra hello **seçin abonelikleri** tüm hello ile ilişkili Azure abonelikleri iletişim kutusu listeleri hello kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bc59e-128">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions that are associated with hello credentials.</span></span> <span data-ttu-id="bc59e-129">Select hello **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bc59e-129">Select hello **Select** button.</span></span>

    ![Merhaba abonelikleri seçin iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. <span data-ttu-id="bc59e-131">Merhaba üzerinde **Azure Gezgini** sekmesinde, genişletin **Hdınsight** aboneliğinizde olan Hdınsight Spark kümeleri tooview hello.</span><span class="sxs-lookup"><span data-stu-id="bc59e-131">On hello **Azure Explorer** tab, expand **HDInsight** tooview hello HDInsight Spark clusters that are in your subscription.</span></span>
   
    ![Azure Explorer'da Hdınsight Spark kümeleri](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. <span data-ttu-id="bc59e-133">hello kümeyle ilişkili tooview hello kaynaklarını (örneğin, depolama hesapları), başka bir küme adı düğümü genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-133">tooview hello resources (for example, storage accounts) that are associated with hello cluster, you can further expand a cluster-name node.</span></span>
   
    ![Genişletilmiş bir küme adı düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="bc59e-135">Hdınsight Spark kümesi üzerinde Spark Scala uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc59e-135">Run a Spark Scala application on an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="bc59e-136">Intellij Idea başlatın ve bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc59e-136">Start IntelliJ IDEA, and then create a project.</span></span> <span data-ttu-id="bc59e-137">Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bc59e-137">In hello **New Project** dialog box, do hello following:</span></span> 

   <span data-ttu-id="bc59e-138">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-138">a.</span></span> <span data-ttu-id="bc59e-139">Seçin **Hdınsight** > **(Scala) hdınsight'ta Spark**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-139">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="bc59e-140">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-140">b.</span></span> <span data-ttu-id="bc59e-141">Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="bc59e-141">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="bc59e-142">**Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği</span><span class="sxs-lookup"><span data-stu-id="bc59e-142">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="bc59e-143">**SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc59e-143">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. <span data-ttu-id="bc59e-145">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-145">Select **Next**.</span></span>

3. <span data-ttu-id="bc59e-146">Merhaba Scala Proje Oluşturma Sihirbazı'nı otomatik olarak hello Scala eklenti yüklediğiniz olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="bc59e-146">hello Scala project-creation wizard automatically detects whether you've installed hello Scala plug-in.</span></span> <span data-ttu-id="bc59e-147">Seçin **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-147">Select **Install**.</span></span>

   ![Scala eklentisi onay](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. <span data-ttu-id="bc59e-149">toodownload hello Scala eklentisi, select **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-149">toodownload hello Scala plug-in, select **OK**.</span></span> <span data-ttu-id="bc59e-150">Merhaba yönergeleri toorestart Intellij izleyin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-150">Follow hello instructions toorestart IntelliJ.</span></span> 

   ![Merhaba Scala eklentisi yükleme iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. <span data-ttu-id="bc59e-152">Merhaba, **yeni proje** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bc59e-152">In hello **New Project** window, do hello following:</span></span>  

    ![Merhaba Spark SDK seçme](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   <span data-ttu-id="bc59e-154">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-154">a.</span></span> <span data-ttu-id="bc59e-155">Bir proje adı ve konum girin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-155">Enter a project name and location.</span></span>

   <span data-ttu-id="bc59e-156">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-156">b.</span></span> <span data-ttu-id="bc59e-157">Merhaba, **proje SDK** aşağı açılan listesinden, **Java 1.8** hello Spark 2.x kümesi ya da seçin **Java 1.7** hello Spark 1.x kümesi için.</span><span class="sxs-lookup"><span data-stu-id="bc59e-157">In hello **Project SDK** drop-down list, select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span>

   <span data-ttu-id="bc59e-158">c.</span><span class="sxs-lookup"><span data-stu-id="bc59e-158">c.</span></span> <span data-ttu-id="bc59e-159">Merhaba, **Spark sürüm** aşağı açılan listesinde, Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK hello uygun sürüm tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="bc59e-159">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="bc59e-160">Merhaba Spark küme sürüm 2.0 eskiyse, seçin **1.x Spark**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-160">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="bc59e-161">Aksi takdirde seçin **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-161">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="bc59e-162">Bu örnekte **Spark 2.0.2 (Scala 2.11.8)**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-162">This example uses **Spark 2.0.2 (Scala 2.11.8)**.</span></span>

6. <span data-ttu-id="bc59e-163">**Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-163">Select **Finish**.</span></span>

7. <span data-ttu-id="bc59e-164">Merhaba Spark proje bir yapı sizin için otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc59e-164">hello Spark project automatically creates an artifact for you.</span></span> <span data-ttu-id="bc59e-165">tooview hello yapı aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bc59e-165">tooview hello artifact, do hello following:</span></span>

   <span data-ttu-id="bc59e-166">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-166">a.</span></span> <span data-ttu-id="bc59e-167">Merhaba üzerinde **dosya** menüsünde, select **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-167">On hello **File** menu, select **Project Structure**.</span></span>

   <span data-ttu-id="bc59e-168">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-168">b.</span></span> <span data-ttu-id="bc59e-169">Merhaba, **proje yapısını** iletişim kutusunda **yapıları** oluşturulan tooview hello varsayılan yapı.</span><span class="sxs-lookup"><span data-stu-id="bc59e-169">In hello **Project Structure** dialog box, select **Artifacts** tooview hello default artifact that is created.</span></span> <span data-ttu-id="bc59e-170">Merhaba artı işaretini seçerek kendi yapı de oluşturabilirsiniz (**+**).</span><span class="sxs-lookup"><span data-stu-id="bc59e-170">You can also create your own artifact by selecting hello plus sign (**+**).</span></span>

      ![Yapı bilgisi hello iletişim kutusunda](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. <span data-ttu-id="bc59e-172">Uygulama kaynak koduna hello aşağıdakileri yaparak ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bc59e-172">Add your application source code by doing hello following:</span></span>

   <span data-ttu-id="bc59e-173">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-173">a.</span></span> <span data-ttu-id="bc59e-174">Proje Gezgini'nde sağ **src**, çok noktası**yeni**ve ardından **Scala sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-174">In Project Explorer, right-click **src**, point too**New**, and then select **Scala Class**.</span></span>
      
      ![Proje Gezgini'nde Scala sınıfı oluşturmak için komutları](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   <span data-ttu-id="bc59e-176">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-176">b.</span></span> <span data-ttu-id="bc59e-177">Merhaba, **yeni Scala Sınıf Oluştur** iletişim kutusunda, bir ad sağlayın, seçin **nesne** hello içinde **türü** kutusuna ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-177">In hello **Create New Scala Class** dialog box, provide a name, select **Object** in hello **Kind** box, and then select **OK**.</span></span>
      
      ![Yeni Scala sınıf iletişim kutusu oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   <span data-ttu-id="bc59e-179">c.</span><span class="sxs-lookup"><span data-stu-id="bc59e-179">c.</span></span> <span data-ttu-id="bc59e-180">Merhaba, **MyClusterApp.scala** dosya, hello aşağıdaki kodu yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc59e-180">In hello **MyClusterApp.scala** file, paste hello following code.</span></span> <span data-ttu-id="bc59e-181">Merhaba kodu HVAC.csv (tüm Hdınsight Spark kümeleri üzerinde kullanılabilir) hello verileri okur, sütununda hello yedinci hello CSV dosyası yalnızca bir rakam olması hello satır alır ve hello çıkış çok yazar**/HVACOut** hello varsayılan altında Merhaba küme depolama kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="bc59e-181">hello code reads hello data from HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that have only one digit in hello seventh column in hello CSV file, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. <span data-ttu-id="bc59e-182">Merhaba uygulaması hello aşağıdakileri yaparak bir Hdınsight Spark kümesinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bc59e-182">Run hello application on an HDInsight Spark cluster by doing hello following:</span></span>

   <span data-ttu-id="bc59e-183">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-183">a.</span></span> <span data-ttu-id="bc59e-184">Proje Gezgini'nde hello proje adına sağ tıklayın ve ardından **gönderme Spark uygulama tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-184">In Project Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>
      
      ![Merhaba gönderme Spark uygulama tooHDInsight komutu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   <span data-ttu-id="bc59e-186">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-186">b.</span></span> <span data-ttu-id="bc59e-187">Azure aboneliği kimlik bilgileriniz istendiğinde tooenter şunlardır.</span><span class="sxs-lookup"><span data-stu-id="bc59e-187">You are prompted tooenter your Azure subscription credentials.</span></span> <span data-ttu-id="bc59e-188">Merhaba, **Spark gönderme** iletişim kutusu, değerleri aşağıdaki hello sağlayın ve ardından **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-188">In hello **Spark Submission** dialog box, provide hello following values, and then select **Submit**.</span></span>
      
      * <span data-ttu-id="bc59e-189">İçin **Spark kümeleri (yalnızca Linux)**, uygulamanızı seçin hello toorun istediğiniz Hdınsight Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="bc59e-189">For **Spark clusters (Linux only)**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>

      * <span data-ttu-id="bc59e-190">Merhaba Intellij projeden bir yapı seçin veya bir hello sabit sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-190">Select an artifact from hello IntelliJ project, or select one from hello hard drive.</span></span>

      * <span data-ttu-id="bc59e-191">Merhaba, **ana sınıf adı** kutusunda, select hello üç nokta (**...** ), uygulamanın kaynak kodunda hello ana sınıfı seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-191">In hello **Main class name** box, select hello ellipsis (**...**), select hello main class in your application source code, and then select **OK**.</span></span>

        ![Merhaba ana sınıf Seç iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * <span data-ttu-id="bc59e-193">Bu örnekte Hello uygulama kodu komut satırı bağımsız değişkenleri gerektirmediği veya Kavanoz veya dosyaları başvurmak için kutuları boş kalan hello bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-193">Because hello application code in this example does not require command-line arguments or reference JARs or files, you can leave hello remaining boxes empty.</span></span> <span data-ttu-id="bc59e-194">Tüm hello bilgileri verdikten sonra hello iletişim kutusu görüntü aşağıdaki hello benzemelidir.</span><span class="sxs-lookup"><span data-stu-id="bc59e-194">After you provide all hello information, hello dialog box should resemble hello following image.</span></span>
        
        ![Merhaba Spark gönderme iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   <span data-ttu-id="bc59e-196">c.</span><span class="sxs-lookup"><span data-stu-id="bc59e-196">c.</span></span> <span data-ttu-id="bc59e-197">Merhaba **Spark gönderme** sekmesini hello pencerenin hello altındaki hello ilerleme durumunu görüntüleme başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc59e-197">hello **Spark Submission** tab at hello bottom of hello window should start displaying hello progress.</span></span> <span data-ttu-id="bc59e-198">Hello hello kırmızı düğmesini seçerek Merhaba uygulaması durdurabilirsiniz **Spark gönderme** penceresi.</span><span class="sxs-lookup"><span data-stu-id="bc59e-198">You can also stop hello application by selecting hello red button in hello **Spark Submission** window.</span></span>
      
      ![Merhaba Spark gönderme penceresi](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      <span data-ttu-id="bc59e-200">toolearn tooaccess iş çıktısı hello nasıl hello bkz "erişim ve Intellij için Azure Araç Seti kullanarak Hdınsight Spark kümeleri yönetmek" bölümünde bu makalenin sonraki bölümlerinde yer.</span><span class="sxs-lookup"><span data-stu-id="bc59e-200">toolearn how tooaccess hello job output, see hello "Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ" section later in this article.</span></span>

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a><span data-ttu-id="bc59e-201">Çalıştırabilir veya bir Hdınsight Spark kümesi üzerinde Spark Scala uygulamanızın hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="bc59e-201">Run or debug a Spark Scala application on an HDInsight Spark cluster</span></span>
<span data-ttu-id="bc59e-202">Merhaba Spark uygulama toohello küme gönderilmesi bir başka yolu da öneririz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-202">We also recommend another way of submitting hello Spark application toohello cluster.</span></span> <span data-ttu-id="bc59e-203">Hello hello parametrelerini ayarlayarak yapabilirsiniz **Çalıştır/hata ayıklama yapılandırmaları** IDE.</span><span class="sxs-lookup"><span data-stu-id="bc59e-203">You can do so by setting hello parameters in hello **Run/Debug configurations** IDE.</span></span> <span data-ttu-id="bc59e-204">Daha fazla bilgi için bkz: [SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında uzaktan hata ayıklama](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span><span class="sxs-lookup"><span data-stu-id="bc59e-204">For more information, see [Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).</span></span>

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a><span data-ttu-id="bc59e-205">Erişim ve Hdınsight Spark kümeleri Intellij için Azure Araç Seti kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="bc59e-205">Access and manage HDInsight Spark clusters by using Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="bc59e-206">Intellij için Azure Araç Seti kullanarak çeşitli işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-206">You can perform various operations by using Azure Toolkit for IntelliJ.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="bc59e-207">Erişim hello işi görüntüle</span><span class="sxs-lookup"><span data-stu-id="bc59e-207">Access hello job view</span></span>
1. <span data-ttu-id="bc59e-208">Azure Explorer'da genişletin **Hdınsight**hello Spark küme adını genişletin ve ardından **işleri**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-208">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then select **Jobs**.</span></span>  

    ![Proje görünümü düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="bc59e-210">Merhaba sağ bölmede, hello **Spark iş görünümünde** sekmesi hello küme üzerinde çalıştırılan tüm hello uygulamaları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bc59e-210">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="bc59e-211">Merhaba uygulaması toosee daha fazla ayrıntı istediğiniz Hello adını seçin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-211">Select hello name of hello application for which you want toosee more details.</span></span>

    ![Uygulama Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. <span data-ttu-id="bc59e-213">toodisplay temel çalışan iş bilgileri hello iş grafiğinin üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-213">toodisplay basic running job information, hover over hello job graph.</span></span> <span data-ttu-id="bc59e-214">tooview hello aşamaları grafik ve her iş oluşturur, bilgileri bir düğümde hello iş grafiği seçin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-214">tooview hello stages graph and information that every job generates, select a node on hello job graph.</span></span>

    ![İş aşama ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. <span data-ttu-id="bc59e-216">tooview sık kullanılan günlükleri gibi *sürücü Stderr*, *sürücü Stdout*, ve *dizin bilgisi*seçin hello **günlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="bc59e-216">tooview frequently used logs, such as *Driver Stderr*, *Driver Stdout*, and *Directory Info*, select hello **Log** tab.</span></span>

    ![Günlük Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. <span data-ttu-id="bc59e-218">Ayrıca hello Spark geçmişi kullanıcı Arabirimi ve hello YARN kullanıcı Arabiriminde (Merhaba uygulama düzeyinde) hello penceresinde hello üstündeki bağlantısını seçerek görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-218">You can also view hello Spark history UI and hello YARN UI (at hello application level) by selecting a link at hello top of hello window.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="bc59e-219">Erişim hello Spark geçmişi sunucusu</span><span class="sxs-lookup"><span data-stu-id="bc59e-219">Access hello Spark history server</span></span>
1. <span data-ttu-id="bc59e-220">Azure Explorer'da genişletin **Hdınsight**Spark küme adına sağ tıklayın ve ardından **açık Spark geçmişi kullanıcı Arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-220">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> 

2. <span data-ttu-id="bc59e-221">İstendiğinde, hello küme ayarlandığında belirtilen hello kümenin yönetici kimlik girin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-221">When you're prompted, enter hello cluster's admin credentials, which you specified when you set up hello cluster.</span></span>

3. <span data-ttu-id="bc59e-222">Merhaba Spark geçmişi server panosunda hello uygulama adı toolook yalnızca çalışması sona Merhaba uygulaması için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-222">On hello Spark history server dashboard, you can use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="bc59e-223">Kod önceki hello hello uygulama adı kullanarak ayarladığınız `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="bc59e-223">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="bc59e-224">Bu nedenle, Spark uygulamanızın adı olan **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-224">Therefore, your Spark application name is **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="bc59e-225">Merhaba Ambari portal Başlat</span><span class="sxs-lookup"><span data-stu-id="bc59e-225">Start hello Ambari portal</span></span>
1. <span data-ttu-id="bc59e-226">Azure Explorer'da genişletin **Hdınsight**Spark küme adına sağ tıklayın ve ardından **açık küme yönetim portalı (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-226">In Azure Explorer, expand **HDInsight**, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 

2. <span data-ttu-id="bc59e-227">İstendiğinde, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-227">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="bc59e-228">Merhaba küme kurulum işlemi sırasında bu kimlik bilgileri belirttiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-228">You specified these credentials during hello cluster setup process.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="bc59e-229">Azure Aboneliklerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="bc59e-229">Manage Azure subscriptions</span></span>
<span data-ttu-id="bc59e-230">Varsayılan olarak, tüm Azure aboneliklerinden hello Spark kümeleri Intellij için Azure Araç Seti listeler.</span><span class="sxs-lookup"><span data-stu-id="bc59e-230">By default, Azure Toolkit for IntelliJ lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="bc59e-231">Gerekirse, hello abonelikleri tooaccess istediğinizi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-231">If necessary, you can specify hello subscriptions that you want tooaccess.</span></span> 

1. <span data-ttu-id="bc59e-232">Hello Azure Gezgini'nde sağ **Azure** kök düğümünü ve ardından **Aboneliklerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-232">In Azure Explorer, right-click hello **Azure** root node, and then select **Manage Subscriptions**.</span></span> 

2. <span data-ttu-id="bc59e-233">Merhaba iletişim kutusunda, yoksa tooaccess istediğiniz ve ardından, hello onay kutularını sonraki toohello abonelikleri temizleyin **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-233">In hello dialog box, clear hello check boxes next toohello subscriptions that you don't want tooaccess, and then select **Close**.</span></span> <span data-ttu-id="bc59e-234">Öğesini de seçebilirsiniz **oturum kapatma** dışında Azure aboneliğinizin toosign istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="bc59e-234">You can also select **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="bc59e-235">Spark Scala uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc59e-235">Run a Spark Scala application locally</span></span>
<span data-ttu-id="bc59e-236">Azure Araç Seti Intellij toorun Spark Scala uygulamaları için yerel olarak iş istasyonunuza kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-236">You can use Azure Toolkit for IntelliJ toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="bc59e-237">Merhaba uygulamalar genellikle depolama kapsayıcıları gibi toocluster kaynakları erişmeyin ve çalıştırma ve bunları yerel olarak test etme.</span><span class="sxs-lookup"><span data-stu-id="bc59e-237">hello applications usually don't need access toocluster resources, such as storage containers, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="bc59e-238">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="bc59e-238">Prerequisite</span></span>
<span data-ttu-id="bc59e-239">Bir Windows bilgisayarda hello yerel Spark Scala uygulama çalıştırıyorsanız, ancak açıklandığı gibi bir özel durum alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="bc59e-239">While you're running hello local Spark Scala application on a Windows computer, you might get an exception, as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="bc59e-240">WinUtils.exe olmadığından, Windows hello özel durum oluşur.</span><span class="sxs-lookup"><span data-stu-id="bc59e-240">hello exception occurs because WinUtils.exe is missing on Windows.</span></span> 

<span data-ttu-id="bc59e-241">tooresolve bu hatayı [hello yürütülebilir karşıdan](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa konum gibi **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-241">tooresolve this error, [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location such as **C:\WinUtils\bin**.</span></span> <span data-ttu-id="bc59e-242">Ardından, hello ortam değişkenine ekleyin **HADOOP_HOME**ve çok hello hello değişkenin değerini ayarlamak**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-242">Then, add hello environment variable **HADOOP_HOME**, and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="bc59e-243">Yerel bir Spark Scala uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc59e-243">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="bc59e-244">Intellij Idea başlatın ve bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc59e-244">Start IntelliJ IDEA, and create a project.</span></span> 

2. <span data-ttu-id="bc59e-245">Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bc59e-245">In hello **New Project** dialog box, do hello following:</span></span>
   
    <span data-ttu-id="bc59e-246">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-246">a.</span></span> <span data-ttu-id="bc59e-247">Seçin **Hdınsight** > **Spark Hdınsight yerel çalışma örneği (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-247">Select **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    <span data-ttu-id="bc59e-248">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-248">b.</span></span> <span data-ttu-id="bc59e-249">Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="bc59e-249">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

      * <span data-ttu-id="bc59e-250">**Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği</span><span class="sxs-lookup"><span data-stu-id="bc59e-250">**Maven**, for Scala project-creation wizard support</span></span>
      * <span data-ttu-id="bc59e-251">**SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc59e-251">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

    ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. <span data-ttu-id="bc59e-253">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-253">Select **Next**.</span></span>
 
4. <span data-ttu-id="bc59e-254">Merhaba sonraki penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="bc59e-254">In hello next window, do hello following:</span></span>
   
    <span data-ttu-id="bc59e-255">a.</span><span class="sxs-lookup"><span data-stu-id="bc59e-255">a.</span></span> <span data-ttu-id="bc59e-256">Bir proje adı ve konum girin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-256">Enter a project name and location.</span></span>

    <span data-ttu-id="bc59e-257">b.</span><span class="sxs-lookup"><span data-stu-id="bc59e-257">b.</span></span> <span data-ttu-id="bc59e-258">Merhaba, **proje SDK** aşağı açılan listesinde, 1.7 sürümünden daha yeni bir Java sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-258">In hello **Project SDK** drop-down list, select a Java version that's later than version 1.7.</span></span>

    <span data-ttu-id="bc59e-259">c.</span><span class="sxs-lookup"><span data-stu-id="bc59e-259">c.</span></span> <span data-ttu-id="bc59e-260">Merhaba, **Spark sürüm** açılan listesinden, select hello sürümü toouse istediğiniz Scala: Scala Spark 2.0 veya Scala 2.11.x 2.10.x Spark 1.6 için.</span><span class="sxs-lookup"><span data-stu-id="bc59e-260">In hello **Spark Version** drop-down list, select hello version of Scala that you want toouse: Scala 2.11.x for Spark 2.0 or Scala 2.10.x for Spark 1.6.</span></span>

    ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. <span data-ttu-id="bc59e-262">**Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-262">Select **Finish**.</span></span>

6. <span data-ttu-id="bc59e-263">Merhaba şablon ekler örnek kod (**LogQuery**) hello altında **src** bilgisayarınızda yerel olarak çalıştırabilirsiniz klasör.</span><span class="sxs-lookup"><span data-stu-id="bc59e-263">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery konumu](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. <span data-ttu-id="bc59e-265">Sağ hello **LogQuery** uygulama ve ardından **Çalıştır 'LogQuery'**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-265">Right-click hello **LogQuery** application, and then select **Run 'LogQuery'**.</span></span> <span data-ttu-id="bc59e-266">Merhaba üzerinde **çalıştırmak** sekmesini hello altındaki hello aşağıdaki gibi bir çıktı görmeniz:</span><span class="sxs-lookup"><span data-stu-id="bc59e-266">On hello **Run** tab at hello bottom, you see an output like hello following:</span></span>
   
   ![Spark uygulama yerel çalıştırma sonucu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a><span data-ttu-id="bc59e-268">Intellij için varolan Intellij Idea uygulamaları toouse Azure Araç Seti Dönüştür</span><span class="sxs-lookup"><span data-stu-id="bc59e-268">Convert existing IntelliJ IDEA applications toouse Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="bc59e-269">Intellij Idea toobe Intellij için Azure araç seti ile uyumlu oluşturduğunuz hello varolan Spark Scala uygulamaları dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-269">You can convert hello existing Spark Scala applications that you created in IntelliJ IDEA toobe compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="bc59e-270">Daha sonra hello eklenti toosubmit hello uygulamaları tooan Hdınsight Spark kümesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-270">You can then use hello plug-in toosubmit hello applications tooan HDInsight Spark cluster.</span></span>

1. <span data-ttu-id="bc59e-271">Intellij Idea ile oluşturulmuş bir varolan Spark Scala uygulama için hello ilişkili .iml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bc59e-271">For an existing Spark Scala application that was created through IntelliJ IDEA, open hello associated .iml file.</span></span>

2. <span data-ttu-id="bc59e-272">Merhaba kökünde düzeyidir bir **Modülü** öğesi hello aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="bc59e-272">At hello root level is a **module** element like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   <span data-ttu-id="bc59e-273">Merhaba öğesi tooadd Düzenle `UniqueKey="HDInsightTool"` , bu nedenle hello **Modülü** öğesi hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="bc59e-273">Edit hello element tooadd `UniqueKey="HDInsightTool"` so that hello **module** element looks like hello following:</span></span>
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. <span data-ttu-id="bc59e-274">Merhaba değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bc59e-274">Save hello changes.</span></span> <span data-ttu-id="bc59e-275">Uygulamanız artık Intellij için Azure araç seti ile uyumlu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc59e-275">Your application should now be compatible with Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="bc59e-276">Merhaba proje Gezgini'nde proje adına sağ tıklayarak test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-276">You can test it by right-clicking hello project name in Project Explorer.</span></span> <span data-ttu-id="bc59e-277">Hello açılır menüsünden başlangıç seçeneği artık sahiptir **gönderme Spark uygulama tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bc59e-277">hello pop-up menu now has hello option **Submit Spark Application tooHDInsight**.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bc59e-278">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="bc59e-278">Troubleshooting</span></span>

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a><span data-ttu-id="bc59e-279">Yerel çalıştırma hatası: *Lütfen daha büyük bir öbek boyutu kullanın*</span><span class="sxs-lookup"><span data-stu-id="bc59e-279">Error in local run: *Please use a larger heap size*</span></span>
<span data-ttu-id="bc59e-280">Yerel çalıştırma sırasında bir 32 bit Java SDK'sı kullanıyorsanız, Spark 1.6 içinde aşağıdaki hatalar hello karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc59e-280">In Spark 1.6, if you're using a 32-bit Java SDK during local run, you might encounter hello following errors:</span></span>

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

<span data-ttu-id="bc59e-281">Merhaba yığın boyutu Spark toorun için yeterince büyük olduğundan bu hataları gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="bc59e-281">These errors happen because hello heap size is not large enough for Spark toorun.</span></span> <span data-ttu-id="bc59e-282">Spark en az 471 MB gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bc59e-282">Spark requires at least 471 MB.</span></span> <span data-ttu-id="bc59e-283">(Daha fazla bilgi için bkz: [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Bir basit toouse bir 64-bit Java SDK'sı çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="bc59e-283">(For more information, see [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) One simple solution is toouse a 64-bit Java SDK.</span></span> <span data-ttu-id="bc59e-284">Seçenekler aşağıdaki hello ekleyerek de Intellij hello JVM ayarları değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc59e-284">You can also change hello JVM settings in IntelliJ by adding hello following options:</span></span>

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

!["VM Seçenekleri" içinde Intellij kutusunda seçenekleri toohello ekleme](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a><span data-ttu-id="bc59e-286">SSS</span><span class="sxs-lookup"><span data-stu-id="bc59e-286">FAQ</span></span>
<span data-ttu-id="bc59e-287">bir uygulama tooAzure Data Lake Store toosubmit seçin **etkileşimli** hello Azure oturum açma işlemi sırasında modu.</span><span class="sxs-lookup"><span data-stu-id="bc59e-287">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="bc59e-288">Seçerseniz **otomatik** modu, bir hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-288">If you select **Automated** mode, you can get an error.</span></span>

![signın etkileşim](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

<span data-ttu-id="bc59e-290">Şimdi, biz bunu çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="bc59e-290">Now, we resolved it.</span></span> <span data-ttu-id="bc59e-291">Uygulamanız herhangi bir oturum açma yöntemi bir Azure Data Lake küme toosubmit seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc59e-291">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="bc59e-292">Geri bildirim ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="bc59e-292">Feedback and known issues</span></span>
<span data-ttu-id="bc59e-293">Şu anda, Spark çıkışları doğrudan görüntüleme desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bc59e-293">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="bc59e-294">Tüm öneriler veya Geri bildiriminiz varsa veya bu eklenti kullandığınızda herhangi bir sorunla karşılaşırsanız, adresinden bize e-posta hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="bc59e-294">If you have any suggestions or feedback, or if you encounter any problems when you use this plug-in, email us at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="bc59e-295"><a name="seealso"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc59e-295"><a name="seealso"></a>Next steps</span></span>
* [<span data-ttu-id="bc59e-296">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="bc59e-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="demo"></a><span data-ttu-id="bc59e-297">Tanıtım</span><span class="sxs-lookup"><span data-stu-id="bc59e-297">Demo</span></span>
* <span data-ttu-id="bc59e-298">Scala proje oluştur (video): [Spark Scala uygulamaları oluşturma](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="bc59e-298">Create Scala project (video): [Create Spark Scala Applications](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)</span></span>
* <span data-ttu-id="bc59e-299">Uzaktan hata ayıklama (video): [Intellij toodebug Spark uygulamalarında uzaktan Hdınsight kümesinde için kullanım Azure Araç Seti](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="bc59e-299">Remote debug (video): [Use Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)</span></span>

### <a name="scenarios"></a><span data-ttu-id="bc59e-300">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="bc59e-300">Scenarios</span></span>
* [<span data-ttu-id="bc59e-301">BI ile Spark: BI araçlarıyla Hdınsight'ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="bc59e-301">Spark with BI: Perform interactive data analysis by using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="bc59e-302">Machine Learning ile Spark: HVAC verilerini kullanarak sıcaklık oluşturma Hdınsight tooanalyze kullanım Spark</span><span class="sxs-lookup"><span data-stu-id="bc59e-302">Spark with Machine Learning: Use Spark in HDInsight tooanalyze building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="bc59e-303">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-303">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="bc59e-304">Spark akış: Spark Hdınsight toobuild gerçek zamanlı akış uygulamaları kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-304">Spark Streaming: Use Spark in HDInsight toobuild real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="bc59e-305">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="bc59e-305">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="bc59e-306">Oluşturma ve uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc59e-306">Creating and running applications</span></span>
* [<span data-ttu-id="bc59e-307">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc59e-307">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="bc59e-308">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bc59e-308">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="bc59e-309">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="bc59e-309">Tools and extensions</span></span>
* [<span data-ttu-id="bc59e-310">VPN üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-310">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="bc59e-311">SSH üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-311">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="bc59e-312">Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-312">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="bc59e-313">Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="bc59e-313">Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications</span></span>](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [<span data-ttu-id="bc59e-314">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-314">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="bc59e-315">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="bc59e-315">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="bc59e-316">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="bc59e-316">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="bc59e-317">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="bc59e-317">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="bc59e-318">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="bc59e-318">Managing resources</span></span>
* [<span data-ttu-id="bc59e-319">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="bc59e-319">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="bc59e-320">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="bc59e-320">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

