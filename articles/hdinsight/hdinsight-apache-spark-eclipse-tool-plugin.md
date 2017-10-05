---
title: "Eclipse - Hdınsight Spark oluşturmak Scala uygulamaları için Azure Araç Seti | Microsoft Docs"
description: "Hdınsight araçları Eclipse için Azure Araç Seti Spark Scala içinde yazılmış uygulamalar geliştirmek için kullanabilir ve bunları bir Hdınsight Spark kümesi için doğrudan kendilerinden Eclipse IDE gönderebilirler."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 4bcb1987a62c0b7f4965e6fd257315e820004238
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="007e4-103">Eclipse için Azure Araç Seti Spark Hdınsight kümesi için uygulamalar oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="007e4-103">Use Azure Toolkit for Eclipse to create Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="007e4-104">Spark Scala içinde yazılmış uygulamalar geliştirmek ve bunları bir Azure Hdınsight Spark kümesi için Eclipse IDE içinden doğrudan göndermek için Azure araç setini Eclipse için Hdınsight araçlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="007e4-104">Use HDInsight Tools in Azure Toolkit for Eclipse to develop Spark applications written in Scala and submit them to an Azure HDInsight Spark cluster, directly from the Eclipse IDE.</span></span> <span data-ttu-id="007e4-105">Hdınsight araçları eklentisi birkaç farklı şekillerde kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="007e4-105">You can use the HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="007e4-106">Geliştirmek ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının göndermek için</span><span class="sxs-lookup"><span data-stu-id="007e4-106">To develop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="007e4-107">Azure Hdınsight Spark küme kaynaklarınıza erişmek için</span><span class="sxs-lookup"><span data-stu-id="007e4-107">To access your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="007e4-108">Geliştirmek ve Scala Spark uygulamayı yerel olarak çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="007e4-108">To develop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="007e4-109">Bu araç, oluşturma ve gönderme yalnızca Linux'ta Hdınsight Spark kümesinde uygulamalar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="007e4-109">This tool can be used to create and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="007e4-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="007e4-110">Prerequisites</span></span>

* <span data-ttu-id="007e4-111">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="007e4-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="007e4-112">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="007e4-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="007e4-113">Eclipse IDE çalışma zamanı için kullanılan oracle Java Geliştirme Seti 8 sürümü.</span><span class="sxs-lookup"><span data-stu-id="007e4-113">Oracle Java Development Kit version 8, which is used for the Eclipse IDE runtime.</span></span> <span data-ttu-id="007e4-114">Buradan indirebilirsiniz [Oracle Web sitesi](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="007e4-114">You can download it from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="007e4-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="007e4-115">Eclipse IDE.</span></span> <span data-ttu-id="007e4-116">Bu makalede Eclipse Neon kullanır.</span><span class="sxs-lookup"><span data-stu-id="007e4-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="007e4-117">Şuradan yükleyebilirsiniz [Eclipse Web sitesi](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="007e4-117">You can install it from the [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="007e4-118">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="007e4-118">Spark SDK.</span></span> <span data-ttu-id="007e4-119">Buradan indirebilirsiniz [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="007e4-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="007e4-120">Eclipse ve Scala eklentisi için Azure araç setindeki Hdınsight araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="007e4-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="007e4-121">Hdınsight araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="007e4-121">Install HDInsight Tools</span></span>
<span data-ttu-id="007e4-122">Eclipse için Hdınsight araçları kullanılabilir Eclipse için Azure araç seti bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="007e4-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="007e4-123">Yükleme yönergeleri için bkz: [Eclipse için Azure Araç Seti yükleme](../azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="007e4-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="007e4-124">Scala eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="007e4-124">Install Scala Plugin</span></span>
<span data-ttu-id="007e4-125">Intellij açtığınızda, Hdınsight araçları otomatik veya Scala eklentisi yüklü olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="007e4-125">When you open the Intellij, the HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="007e4-126">Tıklatın **Tamam** devam ve Eclipse Marketi tarafından yüklemek için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="007e4-126">Click **OK** to continue and follow the instructions to install by the Eclipse Marketplace.</span></span>

 ![Otomatik Yükleme Scala eklentisi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-to-your-azure-subscription"></a><span data-ttu-id="007e4-128">Azure aboneliğinizde oturum açın</span><span class="sxs-lookup"><span data-stu-id="007e4-128">Sign in to your Azure subscription</span></span>
1. <span data-ttu-id="007e4-129">Eclipse IDE başlatın ve Azure Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="007e4-129">Start the Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="007e4-130">Üzerinde **penceresi** menüsünde tıklatın **görünümü göster**ve ardından **diğer**.</span><span class="sxs-lookup"><span data-stu-id="007e4-130">On the **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="007e4-131">Açılan iletişim kutusunda genişletin **Azure**, tıklatın **Azure Gezgini**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="007e4-131">In the dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![Görünüm iletişim kutusunu göster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="007e4-133">Sağ **Azure** düğümünü ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="007e4-133">Right-click the **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="007e4-134">İçinde **Azure oturum açma** iletişim kutusunda, kimlik doğrulama yöntemi seçin, **oturum**ve Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="007e4-134">In the **Azure Sign In** dialog box, choose the authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Azure oturum açma iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="007e4-136">' De, oturum açtığınız sonra **seçin abonelikleri** iletişim kutusu kimlik bilgileriyle ilişkili tüm Azure abonelikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="007e4-136">After you're signed in, the **Select Subscriptions** dialog box lists all the Azure subscriptions associated with the credentials.</span></span> <span data-ttu-id="007e4-137">Tıklatın **seçin** iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="007e4-137">Click **Select** to close the dialog box.</span></span>

    ![Abonelikleri iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="007e4-139">Üzerinde **Azure Gezgini** sekmesinde, genişletin **Hdınsight** Hdınsight Spark kümeleri aboneliğinizde görmek için.</span><span class="sxs-lookup"><span data-stu-id="007e4-139">On the **Azure Explorer** tab, expand **HDInsight** to see the HDInsight Spark clusters under your subscription.</span></span>
   
    ![Azure Explorer'da Hdınsight Spark kümeleri](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="007e4-141">Daha fazla kümesi ile ilişkili kaynakları (örneğin, depolama hesapları) görmek için bir küme adı düğümü genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-141">You can further expand a cluster name node to see the resources (for example, storage accounts) associated with the cluster.</span></span>
   
    ![Bir küme adı kaynakları görmek için genişletme](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="007e4-143">Spark Scala proje Hdınsight Spark kümesinde için ayarlama</span><span class="sxs-lookup"><span data-stu-id="007e4-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="007e4-144">Eclipse IDE çalışma alanında tıklatın **dosya**, tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="007e4-144">In the Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="007e4-145">Yeni Proje Sihirbazı'nda genişletin **Hdınsight**seçin **(Scala) hdınsight'ta Spark**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="007e4-145">In the New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![Spark Hdınsight (Scala) projede seçme](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="007e4-147">Scala Proje Oluşturma Sihirbazı'nı otomatik veya Scala eklentisi yüklü olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="007e4-147">The Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="007e4-148">Tıklatın **Tamam** Scala eklentisi indirme devam etmek için Eclipse yeniden başlatmak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="007e4-148">Click **OK** to continue downloading the Scala plugin, then follow the instructions to restart Eclipse.</span></span>

    ![scala denetimi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="007e4-150">İçinde **yeni Hdınsight Scala proje** iletişim kutusunda, aşağıdaki değerleri girin ve ardından **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="007e4-150">In the **New HDInsight Scala Project** dialog box, provide the following values, and then click **Next**:</span></span>
   * <span data-ttu-id="007e4-151">Proje için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="007e4-151">Enter a name for the project.</span></span>
   * <span data-ttu-id="007e4-152">İçinde **JRE** alanı olduğundan emin olun **yürütme ortamı JRE kullanın** ayarlanır **JavaSE 1.7** veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="007e4-152">In the **JRE** area, make sure that **Use an execution environment JRE** is set to **JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="007e4-153">Spark SDK SDK indirdiğiniz konuma ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="007e4-153">Make sure that Spark SDK is set to the location where you downloaded the SDK.</span></span> <span data-ttu-id="007e4-154">Yükleme konumu bağlantısını dahil [Önkoşullar](#prerequisites) bu makalenin önceki.</span><span class="sxs-lookup"><span data-stu-id="007e4-154">The link to the download location is included in the [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="007e4-155">İletişim kutusunda içerdiği bağlantısından SDK de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-155">You can also download the SDK from the link included in the dialog box.</span></span>

    ![Yeni Hdınsight Scala proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="007e4-157">Sonraki iletişim kutusunda tıklatın **kitaplıkları** sekmesinde ve Varsayılanları tutun ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="007e4-157">In the next dialog box, click the **Libraries** tab and keep the defaults, and then click **Finish**.</span></span> 
   
    ![Kitaplıklar sekmesi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="007e4-159">Hdınsight Spark kümesinde için Scala uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="007e4-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="007e4-160">Eclipse IDE'de paketi Gezgini'nden daha önce oluşturduğunuz projenizi genişletin, sağ **src**, işaret **yeni**ve ardından **diğer**.</span><span class="sxs-lookup"><span data-stu-id="007e4-160">In the Eclipse IDE, from Package Explorer, expand the project that you created earlier, right-click **src**, point to **New**, and then click **Other**.</span></span>
2. <span data-ttu-id="007e4-161">İçinde **bir sihirbaz seçin** iletişim kutusunda, genişletin **Scala sihirbazları**, tıklatın **Scala nesne**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="007e4-161">In the **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![Bir sihirbaz iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="007e4-163">İçinde **yeni dosyası oluştur** iletişim kutusu, nesne için bir ad girin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="007e4-163">In the **Create New File** dialog box, enter a name for the object, and then click **Finish**.</span></span>
   
    ![Yeni dosya iletişim kutusu oluşturma](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="007e4-165">Metin Düzenleyicisi'nde aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="007e4-165">Paste the following code in the text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="007e4-166">Uygulamayı bir Hdınsight Spark kümesinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="007e4-166">Run the application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="007e4-167">Paket Gezgini'nde proje adına sağ tıklayın ve ardından **Hdınsight için Spark uygulama gönderme**.</span><span class="sxs-lookup"><span data-stu-id="007e4-167">From Package Explorer, right-click the project name, and then select **Submit Spark Application to HDInsight**.</span></span>        
   2. <span data-ttu-id="007e4-168">İçinde **Spark gönderme** iletişim kutusunda, aşağıdaki değerleri girin ve ardından **gönderme**:</span><span class="sxs-lookup"><span data-stu-id="007e4-168">In the **Spark Submission** dialog box, provide the following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="007e4-169">İçin **küme adı**, istediğiniz uygulamanızı çalıştırmak Hdınsight Spark kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="007e4-169">For **Cluster Name**, select the HDInsight Spark cluster on which you want to run your application.</span></span>
      * <span data-ttu-id="007e4-170">Eclipse projeden bir yapı seçin veya bir sabit sürücüden seçin.</span><span class="sxs-lookup"><span data-stu-id="007e4-170">Select an artifact from the Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="007e4-171">Varsayılan değer paketi Gezgini'nden sağ öğesi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="007e4-171">The default value depends on the item you right-click from package explorer.</span></span>
      * <span data-ttu-id="007e4-172">İçinde **ana sınıf adı** dropdownlist, Gönderme Sihirbazı seçili projenizden tüm nesne adlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="007e4-172">In the **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="007e4-173">Çalıştırmak istediğiniz bir giriş veya seçin.</span><span class="sxs-lookup"><span data-stu-id="007e4-173">Select or input one that you want to run.</span></span> <span data-ttu-id="007e4-174">Yapı sabit diskten seçerseniz, kendi kendinize ana sınıf adı giriş.</span><span class="sxs-lookup"><span data-stu-id="007e4-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="007e4-175">Bu örnek uygulama kodunda herhangi bir komut satırı bağımsız değişkeni gerektirmediği veya Kavanoz veya dosyaları başvurmak için kalan metin kutularını boş bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-175">Because the application code in this example does not require any command-line arguments or reference JARs or files, you can leave the remaining text boxes empty.</span></span>
        
       ![Spark gönderme iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="007e4-177">**Spark gönderme** sekmesi, ilerleme durumunu görüntüleme başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="007e4-177">The **Spark Submission** tab should start displaying the progress.</span></span> <span data-ttu-id="007e4-178">Kırmızı düğmesini tıklatarak uygulama durdurabilirsiniz **Spark gönderme** penceresi.</span><span class="sxs-lookup"><span data-stu-id="007e4-178">You can stop the application by clicking the red button in the **Spark Submission** window.</span></span> <span data-ttu-id="007e4-179">Ayrıca bu belirli uygulama (mavi kutu resim olarak gösterilir) dünya simgesini tıklatarak çalıştırmak için günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-179">You can also view the logs for this specific application run by clicking the globe icon (denoted by the blue box in the image).</span></span>
      
       ![Spark gönderme penceresi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="007e4-181">Erişim ve Hdınsight Spark kümeleri Eclipse için Azure araç setindeki Hdınsight araçları kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="007e4-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="007e4-182">İş çıktısı erişim dahil olmak üzere, Hdınsight araçları kullanarak çeşitli işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-182">You can perform various operations by using HDInsight Tools, including accessing the job output.</span></span>

### <a name="access-the-job-view"></a><span data-ttu-id="007e4-183">İş görünüme erişme</span><span class="sxs-lookup"><span data-stu-id="007e4-183">Access the job view</span></span>
1. <span data-ttu-id="007e4-184">Azure Explorer'da genişletin **Hdınsight**, Spark küme adını genişletin ve ardından **işleri**.</span><span class="sxs-lookup"><span data-stu-id="007e4-184">In Azure Explorer, expand **HDInsight**, expand the Spark cluster name, and then click **Jobs**.</span></span> 

    ![Proje görünümü düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="007e4-186">Tıklayın **işleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="007e4-186">Click on the **Jobs** node.</span></span> <span data-ttu-id="007e4-187">Hdınsight araçları otomatik-E (fx) clipse eklentisi veya yüklü olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="007e4-187">The HDInsight Tools auto-detects whether you installed the E(fx)clipse plugin or not.</span></span> <span data-ttu-id="007e4-188">Tıklatın **Tamam** devam ve Eclipse Market yükleme ve Eclipse yeniden başlatmak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="007e4-188">Click **OK** to continue and follow the instructions to install the Eclipse Marketplace and restart Eclipse.</span></span>

    ![E (fx) clipse yükleyin](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="007e4-190">İş görünümünden **işleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="007e4-190">Open the Job View from the **Jobs** node.</span></span> <span data-ttu-id="007e4-191">Sağ bölmede **Spark iş görünümünde** sekmesi, küme üzerinde çalıştırılan tüm uygulamaları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="007e4-191">In the right pane, the **Spark Job View** tab displays all the applications that were run on the cluster.</span></span> <span data-ttu-id="007e4-192">Daha fazla ayrıntı görmek istediğiniz uygulamanın adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="007e4-192">Click the name of the application for which you want to see more details.</span></span>

    ![Uygulama Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="007e4-194">İş grafiğinin getirirseniz, temel çalışan iş bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="007e4-194">If you hover on the job graph, it displays basic running job info.</span></span> <span data-ttu-id="007e4-195">İş grafiği tıklatarak aşamaları grafik ve her iş oluşturur bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="007e4-195">Clicking on the job graph shows the stages graph and info that every job generates.</span></span>

    ![İş aşama ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="007e4-197">Sürücü Stderr, sürücü Stdout ve dizin bilgisi gibi sık kullanılan günlükleri içinde listelenen **günlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="007e4-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in the **Log** tab.</span></span>

    ![Günlük Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="007e4-199">Spark geçmişi kullanıcı Arabirimi ve YARN kullanıcı Arabiriminde (uygulama düzeyinde) pencerenin üstündeki ilgili köprüyü tıklatarak da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-199">You can also open the Spark history UI and the YARN UI (at the application level) by clicking the respective hyperlink at the top of the window.</span></span>

### <a name="access-the-storage-container-for-the-cluster"></a><span data-ttu-id="007e4-200">Küme depolama kapsayıcısını erişim</span><span class="sxs-lookup"><span data-stu-id="007e4-200">Access the storage container for the cluster</span></span>
1. <span data-ttu-id="007e4-201">Azure Explorer'da genişletin **Hdınsight** kullanılabilir Hdınsight Spark kümeleri listesini görmek için kök düğümü.</span><span class="sxs-lookup"><span data-stu-id="007e4-201">In Azure Explorer, expand the **HDInsight** root node to see a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="007e4-202">Depolama hesabı ve kümenin varsayılan depolama kapsayıcısını görmek için küme adını genişletin.</span><span class="sxs-lookup"><span data-stu-id="007e4-202">Expand the cluster name to see the storage account and the default storage container for the cluster.</span></span>
   
    ![Depolama hesabı ve varsayılan depolama kapsayıcısı](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="007e4-204">Kümeyle ilişkili depolama kapsayıcı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="007e4-204">Click the storage container name associated with the cluster.</span></span> <span data-ttu-id="007e4-205">Sağ bölmede, çift **HVACOut** klasör.</span><span class="sxs-lookup"><span data-stu-id="007e4-205">In the right pane, double-click the **HVACOut** folder.</span></span> <span data-ttu-id="007e4-206">Birini açın **bölümü -** uygulamanın çıkışı görmek için dosyaları.</span><span class="sxs-lookup"><span data-stu-id="007e4-206">Open one of the **part-** files to see the output of the application.</span></span>

### <a name="access-the-spark-history-server"></a><span data-ttu-id="007e4-207">Spark geçmişi sunucusuna erişim</span><span class="sxs-lookup"><span data-stu-id="007e4-207">Access the Spark history server</span></span>
1. <span data-ttu-id="007e4-208">Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık Spark geçmişi kullanıcı Arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="007e4-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="007e4-209">İstendiğinde, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="007e4-209">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="007e4-210">Bu küme hazırlama sırasında belirttiğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="007e4-210">You must have specified these while provisioning the cluster.</span></span>
2. <span data-ttu-id="007e4-211">Spark geçmişi server panosunda, uygulama için yalnızca çalışması sona aramak için uygulama adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="007e4-211">In the Spark history server dashboard, you use the application name to look for the application that you just finished running.</span></span> <span data-ttu-id="007e4-212">Önceki kod, uygulamanın adını kullanarak ayarladığınız `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="007e4-212">In the preceding code, you set the application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="007e4-213">Bu nedenle, Spark uygulamanızın adı olan **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="007e4-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-the-ambari-portal"></a><span data-ttu-id="007e4-214">Ambari Portalı'nı Başlat</span><span class="sxs-lookup"><span data-stu-id="007e4-214">Start the Ambari portal</span></span>
1. <span data-ttu-id="007e4-215">Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık küme yönetim portalı (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="007e4-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="007e4-216">İstendiğinde, küme için yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="007e4-216">When you're prompted, enter the admin credentials for the cluster.</span></span> <span data-ttu-id="007e4-217">Bu küme hazırlama sırasında belirttiğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="007e4-217">You must have specified these while provisioning the cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="007e4-218">Azure Aboneliklerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="007e4-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="007e4-219">Varsayılan olarak, tüm Azure aboneliklerinden Spark kümeleri Azure araç setini Eclipse için Hdınsight araçları listeler.</span><span class="sxs-lookup"><span data-stu-id="007e4-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists the Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="007e4-220">Gerekirse, kümeye erişmek istediğiniz abonelikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-220">If necessary, you can specify the subscriptions for which you want to access the cluster.</span></span> 

1. <span data-ttu-id="007e4-221">Azure Gezgini'nde sağ **Azure** kök düğümünü ve ardından **Aboneliklerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="007e4-221">In Azure Explorer, right-click the **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="007e4-222">İletişim kutusunda, erişim ve ardından istemediğiniz abonelik için onay kutularını temizleyin **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="007e4-222">In the dialog box, clear the check boxes for the subscription that you don't want to access, and then click **Close**.</span></span> <span data-ttu-id="007e4-223">Tıklatarak **oturum kapatma** dışında Azure aboneliğinizin imzalanacak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="007e4-223">You can also click **Sign Out** if you want to sign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="007e4-224">Spark Scala uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="007e4-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="007e4-225">Spark Scala uygulamaları iş istasyonunuza yerel olarak çalıştırmak için Hdınsight araçları Azure araç setini Eclipse için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-225">You can use HDInsight Tools in Azure Toolkit for Eclipse to run Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="007e4-226">Genellikle, bu uygulamaları bir depolama kapsayıcısı gibi küme kaynaklarına erişimi gerekmez ve çalıştırma ve bunları yerel olarak test etme.</span><span class="sxs-lookup"><span data-stu-id="007e4-226">Typically, these applications don't need access to cluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="007e4-227">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="007e4-227">Prerequisite</span></span>
<span data-ttu-id="007e4-228">Bir Windows bilgisayarda yerel Spark Scala uygulama çalıştırıyorsanız, ancak açıklandığı gibi bir özel durum alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="007e4-228">While you're running the local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="007e4-229">Bu özel durum oluşur **WinUtils.exe** Windows eksik.</span><span class="sxs-lookup"><span data-stu-id="007e4-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="007e4-230">Bu hatayı gidermek için şunları yapmanız gerekir [yürütülebilir dosya indirme](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) gibi bir konuma **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="007e4-230">To resolve this error, you must [download the executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) to a location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="007e4-231">Ortam değişkeni sonra eklemelisiniz **HADOOP_HOME** ve değişkenin değerini ayarlamak **C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="007e4-231">You must then add the environment variable **HADOOP_HOME** and set the value of the variable to **C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="007e4-232">Yerel bir Spark Scala uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="007e4-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="007e4-233">Eclipse'i başlatın ve bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="007e4-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="007e4-234">İçinde **yeni proje** iletişim kutusunda, aşağıdaki seçimleri yapın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="007e4-234">In the **New Project** dialog box, make the following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="007e4-235">Sol bölmede seçin **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="007e4-235">In the left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="007e4-236">Sağ bölmede seçin **Spark Hdınsight yerel çalıştırma örneği (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="007e4-236">In the right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![Yeni Proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="007e4-238">Proje ayrıntılarını sağlamak için önceki bölümdeki 3 ile 6 arasındaki adımları izleyin [Hdınsight Spark kümesi için Spark Scala proje ayarlama](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span><span class="sxs-lookup"><span data-stu-id="007e4-238">To provide the project details, follow steps 3 through 6 from the earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="007e4-239">Örnek kod şablonunu ekler (**LogQuery**) altında **src** bilgisayarınızda yerel olarak çalıştırabilirsiniz klasör.</span><span class="sxs-lookup"><span data-stu-id="007e4-239">The template adds a sample code (**LogQuery**) under the **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery konumu](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="007e4-241">Sağ **LogQuery** uygulama, noktasına **Çalıştır**ve ardından **1 Scala uygulama**.</span><span class="sxs-lookup"><span data-stu-id="007e4-241">Right-click the **LogQuery** application, point to **Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="007e4-242">Bu gibi bir çıktı göreceksiniz **konsol** sekmesi altındaki:</span><span class="sxs-lookup"><span data-stu-id="007e4-242">You will see an output like this in the **Console** tab at the bottom:</span></span>
   
   ![Spark çalıştırma sonucu uygulama yerel](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="007e4-244">SSS</span><span class="sxs-lookup"><span data-stu-id="007e4-244">FAQ</span></span>
<span data-ttu-id="007e4-245">Azure Data Lake Store uygulamaya göndermek için tercih **etkileşimli** Azure oturum açma işlemi sırasında modu.</span><span class="sxs-lookup"><span data-stu-id="007e4-245">To submit an application to Azure Data Lake Store, choose **Interactive** mode during the Azure sign-in process.</span></span> <span data-ttu-id="007e4-246">Seçerseniz **otomatik** modu, bir hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-246">If you select **Automated** mode, you can get an error.</span></span>

![signın etkileşim](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="007e4-248">Şimdi, biz bunu çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="007e4-248">Now, we resolved it.</span></span> <span data-ttu-id="007e4-249">Uygulamanız herhangi bir oturum açma yöntemi göndermek için bir Azure Data Lake küme seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="007e4-249">You can choose an Azure Data Lake Cluster to submit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="007e4-250">Geri bildirim ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="007e4-250">Feedback and known issues</span></span>
<span data-ttu-id="007e4-251">Şu anda, Spark çıkışları doğrudan görüntüleme desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="007e4-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="007e4-252">Tüm öneriler veya Geri bildiriminiz varsa veya bu aracı kullanırken herhangi bir sorunla karşılaşırsanız, bize bir e-postası göndermek çekinmeyin hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="007e4-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free to send us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="007e4-253"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="007e4-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="007e4-254">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="007e4-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="007e4-255">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="007e4-255">Scenarios</span></span>
* [<span data-ttu-id="007e4-256">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="007e4-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="007e4-257">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="007e4-258">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-258">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="007e4-259">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="007e4-260">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="007e4-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="007e4-261">Oluşturma ve uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="007e4-261">Creating and running applications</span></span>
* [<span data-ttu-id="007e4-262">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="007e4-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="007e4-263">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="007e4-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="007e4-264">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="007e4-264">Tools and extensions</span></span>
* [<span data-ttu-id="007e4-265">Oluşturma ve Spark Scala uygulamaları göndermek amacıyla Intellij için Azure araç seti kullanın</span><span class="sxs-lookup"><span data-stu-id="007e4-265">Use Azure Toolkit for IntelliJ to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="007e4-266">Spark uygulamalarında VPN üzerinden uzaktan hata ayıklamak için Azure araç Intellij için kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-266">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="007e4-267">Spark uygulamalarında SSH üzerinden uzaktan hata ayıklamak için Azure araç Intellij için kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-267">Use Azure Toolkit for IntelliJ to debug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="007e4-268">Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="007e4-269">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="007e4-270">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="007e4-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="007e4-271">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="007e4-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="007e4-272">Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="007e4-272">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="007e4-273">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="007e4-273">Managing resources</span></span>
* [<span data-ttu-id="007e4-274">Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="007e4-274">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="007e4-275">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="007e4-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

