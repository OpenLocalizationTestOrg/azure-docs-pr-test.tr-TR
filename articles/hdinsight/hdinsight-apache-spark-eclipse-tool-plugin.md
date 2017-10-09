---
title: "aaaAzure Eclipse - Hdınsight Spark oluşturmak Scala uygulamaları için araç seti | Microsoft Docs"
description: "Eclipse toodevelop Spark Scala içinde yazılmış uygulamalar için Hdınsight araçları Azure araç setindeki kullanın ve tooan Hdınsight Spark kümesi göndermek, doğrudan kendilerinden Eclipse IDE hello."
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
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a><span data-ttu-id="79cf2-103">Hdınsight kümesi için Eclipse toocreate Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-103">Use Azure Toolkit for Eclipse toocreate Spark applications for an HDInsight cluster</span></span>

<span data-ttu-id="79cf2-104">Eclipse toodevelop Spark Scala içinde yazılmış uygulamalar için Azure araç setindeki Hdınsight araçlarını kullanın ve bunları hello Eclipse IDE doğrudan tooan Azure Hdınsight Spark küme gönderin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-104">Use HDInsight Tools in Azure Toolkit for Eclipse toodevelop Spark applications written in Scala and submit them tooan Azure HDInsight Spark cluster, directly from hello Eclipse IDE.</span></span> <span data-ttu-id="79cf2-105">Merhaba Hdınsight araçları eklentisi birkaç farklı şekillerde kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79cf2-105">You can use hello HDInsight Tools plug-in in a few different ways:</span></span>

* <span data-ttu-id="79cf2-106">toodevelop ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının gönderin</span><span class="sxs-lookup"><span data-stu-id="79cf2-106">toodevelop and submit a Scala Spark application on an HDInsight Spark cluster</span></span>
* <span data-ttu-id="79cf2-107">tooaccess Azure Hdınsight Spark küme kaynakları</span><span class="sxs-lookup"><span data-stu-id="79cf2-107">tooaccess your Azure HDInsight Spark cluster resources</span></span>
* <span data-ttu-id="79cf2-108">toodevelop ve Scala Spark uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="79cf2-108">toodevelop and run a Scala Spark application locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79cf2-109">Bu araç, kullanılan toocreate olması ve yalnızca Linux'ta Hdınsight Spark kümesinde uygulamalar gönderin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-109">This tool can be used toocreate and submit applications only for an HDInsight Spark cluster on Linux.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="79cf2-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79cf2-110">Prerequisites</span></span>

* <span data-ttu-id="79cf2-111">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="79cf2-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="79cf2-112">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="79cf2-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="79cf2-113">Merhaba Eclipse IDE çalışma zamanı için kullanılan oracle Java Geliştirme Seti 8 sürümü.</span><span class="sxs-lookup"><span data-stu-id="79cf2-113">Oracle Java Development Kit version 8, which is used for hello Eclipse IDE runtime.</span></span> <span data-ttu-id="79cf2-114">Hello karşıdan [Oracle Web sitesi](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="79cf2-114">You can download it from hello [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="79cf2-115">Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="79cf2-115">Eclipse IDE.</span></span> <span data-ttu-id="79cf2-116">Bu makalede Eclipse Neon kullanır.</span><span class="sxs-lookup"><span data-stu-id="79cf2-116">This article uses Eclipse Neon.</span></span> <span data-ttu-id="79cf2-117">Merhaba yükleme [Eclipse Web sitesi](https://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="79cf2-117">You can install it from hello [Eclipse website](https://www.eclipse.org/downloads/).</span></span>   
* <span data-ttu-id="79cf2-118">Spark SDK.</span><span class="sxs-lookup"><span data-stu-id="79cf2-118">Spark SDK.</span></span> <span data-ttu-id="79cf2-119">Buradan indirebilirsiniz [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="79cf2-119">You can download it from [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).</span></span>


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a><span data-ttu-id="79cf2-120">Eclipse ve Scala eklentisi için Azure araç setindeki Hdınsight araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="79cf2-120">Install HDInsight Tools in Azure Toolkit for Eclipse and Scala Plugin</span></span>
### <a name="install-hdinsight-tools"></a><span data-ttu-id="79cf2-121">Hdınsight araçlarını yükleme</span><span class="sxs-lookup"><span data-stu-id="79cf2-121">Install HDInsight Tools</span></span>
<span data-ttu-id="79cf2-122">Eclipse için Hdınsight araçları kullanılabilir Eclipse için Azure araç seti bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="79cf2-122">HDInsight Tools for Eclipse is available as part of Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="79cf2-123">Yükleme yönergeleri için bkz: [Eclipse için Azure Araç Seti yükleme](../azure-toolkit-for-eclipse-installation.md).</span><span class="sxs-lookup"><span data-stu-id="79cf2-123">For installation instructions, see [Installing Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse-installation.md).</span></span>
### <a name="install-scala-plugin"></a><span data-ttu-id="79cf2-124">Scala eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="79cf2-124">Install Scala Plugin</span></span>
<span data-ttu-id="79cf2-125">Merhaba Intellij açtığınızda hello Hdınsight araçları otomatik veya Scala eklentisi yüklü olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="79cf2-125">When you open hello Intellij, hello HDInsight Tools auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="79cf2-126">Tıklatın **Tamam** hello Eclipse Market tarafından hello yönergeleri tooinstall toocontinue ve izleyin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-126">Click **OK** toocontinue and follow hello instructions tooinstall by hello Eclipse Marketplace.</span></span>

 ![Otomatik Yükleme Scala eklentisi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a><span data-ttu-id="79cf2-128">Azure aboneliği tooyour oturum</span><span class="sxs-lookup"><span data-stu-id="79cf2-128">Sign in tooyour Azure subscription</span></span>
1. <span data-ttu-id="79cf2-129">Merhaba Eclipse IDE başlatın ve Azure Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="79cf2-129">Start hello Eclipse IDE and open Azure Explorer.</span></span> <span data-ttu-id="79cf2-130">Merhaba üzerinde **penceresi** menüsünde tıklatın **görünümü göster**ve ardından **diğer**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-130">On hello **Window** menu, click **Show View**, and then click **Other**.</span></span> <span data-ttu-id="79cf2-131">Açılan hello iletişim kutusunda, genişletin **Azure**, tıklatın **Azure Gezgini**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-131">In hello dialog box that opens, expand **Azure**, click **Azure Explorer**, and then click **OK**.</span></span>

    ![Görünüm iletişim kutusunu göster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. <span data-ttu-id="79cf2-133">Sağ hello **Azure** düğümünü ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-133">Right-click hello **Azure** node, and then click **Sign in**.</span></span>
3. <span data-ttu-id="79cf2-134">Merhaba, **Azure oturum açma** iletişim kutusunda, hello kimlik doğrulaması yöntemi seçin, **oturum**ve Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-134">In hello **Azure Sign In** dialog box, choose hello authentication method, click **Sign in**, and enter your Azure credentials.</span></span>
   
    ![Azure oturum açma iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. <span data-ttu-id="79cf2-136">Oturum açtınız sonra hello **seçin abonelikleri** tüm hello hello kimlik bilgileriyle ilişkili Azure abonelik iletişim kutusu listeler.</span><span class="sxs-lookup"><span data-stu-id="79cf2-136">After you're signed in, hello **Select Subscriptions** dialog box lists all hello Azure subscriptions associated with hello credentials.</span></span> <span data-ttu-id="79cf2-137">Tıklatın **seçin** tooclose hello iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="79cf2-137">Click **Select** tooclose hello dialog box.</span></span>

    ![Abonelikleri iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. <span data-ttu-id="79cf2-139">Merhaba üzerinde **Azure Gezgini** sekmesinde, genişletin **Hdınsight** toosee hello Hdınsight Spark kümeleri, abonelik altında.</span><span class="sxs-lookup"><span data-stu-id="79cf2-139">On hello **Azure Explorer** tab, expand **HDInsight** toosee hello HDInsight Spark clusters under your subscription.</span></span>
   
    ![Azure Explorer'da Hdınsight Spark kümeleri](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. <span data-ttu-id="79cf2-141">Daha fazla hello kümesi ile ilişkili bir küme adı düğümü toosee hello kaynakları (örneğin, depolama hesapları) genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-141">You can further expand a cluster name node toosee hello resources (for example, storage accounts) associated with hello cluster.</span></span>
   
    ![Bir küme adı toosee kaynakları genişletme](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="79cf2-143">Spark Scala proje Hdınsight Spark kümesinde için ayarlama</span><span class="sxs-lookup"><span data-stu-id="79cf2-143">Set up a Spark Scala project for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="79cf2-144">Merhaba Eclipse IDE çalışma alanında tıklatın **dosya**, tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-144">In hello Eclipse IDE workspace, click **File**, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="79cf2-145">Merhaba Yeni Proje Sihirbazı'nda genişletin **Hdınsight**seçin **(Scala) hdınsight'ta Spark**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-145">In hello New Project wizard, expand **HDInsight**, select **Spark on HDInsight (Scala)**, and then click **Next**.</span></span>

    ![Merhaba Spark Hdınsight (Scala) projede seçme](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. <span data-ttu-id="79cf2-147">Merhaba Scala Proje Oluşturma Sihirbazı'nı otomatik veya Scala eklentisi yüklü olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="79cf2-147">hello Scala project creation wizard auto detects whether you installed Scala plugin or not.</span></span> <span data-ttu-id="79cf2-148">Tıklatın **Tamam** toocontinue hello Scala eklentisi sonra izleme hello yönergeleri toorestart Eclipse yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="79cf2-148">Click **OK** toocontinue downloading hello Scala plugin, then follow hello instructions toorestart Eclipse.</span></span>

    ![scala denetimi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. <span data-ttu-id="79cf2-150">Merhaba, **yeni Hdınsight Scala proje** iletişim kutusu, değerleri aşağıdaki hello sağlayın ve ardından **sonraki**:</span><span class="sxs-lookup"><span data-stu-id="79cf2-150">In hello **New HDInsight Scala Project** dialog box, provide hello following values, and then click **Next**:</span></span>
   * <span data-ttu-id="79cf2-151">Başlangıç projesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-151">Enter a name for hello project.</span></span>
   * <span data-ttu-id="79cf2-152">Merhaba, **JRE** alanı olduğundan emin olun **yürütme ortamı JRE kullanın** çok ayarlanır**JavaSE 1.7** ya da daha sonra.</span><span class="sxs-lookup"><span data-stu-id="79cf2-152">In hello **JRE** area, make sure that **Use an execution environment JRE** is set too**JavaSE-1.7** or later.</span></span>
   * <span data-ttu-id="79cf2-153">Spark SDK hello SDK indirdiğiniz kümesi toohello konumunun olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="79cf2-153">Make sure that Spark SDK is set toohello location where you downloaded hello SDK.</span></span> <span data-ttu-id="79cf2-154">Merhaba bağlantı toohello indirme konumu hello dahil [Önkoşullar](#prerequisites) bu makalenin önceki.</span><span class="sxs-lookup"><span data-stu-id="79cf2-154">hello link toohello download location is included in hello [prerequisites](#prerequisites) earlier in this article.</span></span> <span data-ttu-id="79cf2-155">Merhaba SDK hello indirebilirsiniz hello iletişim kutusunda içerdiği bağlantı.</span><span class="sxs-lookup"><span data-stu-id="79cf2-155">You can also download hello SDK from hello link included in hello dialog box.</span></span>

    ![Yeni Hdınsight Scala proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  <span data-ttu-id="79cf2-157">Merhaba Hello sonraki iletişim kutusunda tıklatın **kitaplıkları** sekmesinde ve hello Varsayılanları tutun ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-157">In hello next dialog box, click hello **Libraries** tab and keep hello defaults, and then click **Finish**.</span></span> 
   
    ![Kitaplıklar sekmesi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a><span data-ttu-id="79cf2-159">Hdınsight Spark kümesinde için Scala uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="79cf2-159">Create a Scala application for an HDInsight Spark cluster</span></span>

1. <span data-ttu-id="79cf2-160">Merhaba paketi Gezgini'nden Eclipse IDE içinde daha önce oluşturduğunuz hello proje genişletin, sağ tıklatın **src**, çok noktası**yeni**ve ardından **diğer**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-160">In hello Eclipse IDE, from Package Explorer, expand hello project that you created earlier, right-click **src**, point too**New**, and then click **Other**.</span></span>
2. <span data-ttu-id="79cf2-161">Merhaba, **bir sihirbaz seçin** iletişim kutusunda, genişletin **Scala sihirbazları**, tıklatın **Scala nesne**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-161">In hello **Select a wizard** dialog box, expand **Scala Wizards**, click **Scala Object**, and then click **Next**.</span></span>
   
    ![Bir sihirbaz iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. <span data-ttu-id="79cf2-163">Merhaba, **yeni dosyası oluştur** iletişim kutusu, hello nesnesi için bir ad girin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-163">In hello **Create New File** dialog box, enter a name for hello object, and then click **Finish**.</span></span>
   
    ![Yeni dosya iletişim kutusu oluşturma](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. <span data-ttu-id="79cf2-165">Merhaba metin düzenleyicisinde koddan hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="79cf2-165">Paste hello following code in hello text editor:</span></span>
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. <span data-ttu-id="79cf2-166">Bir Hdınsight Spark kümesinde Hello uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="79cf2-166">Run hello application on an HDInsight Spark cluster:</span></span>
   
   1. <span data-ttu-id="79cf2-167">Paketi Gezgini'nden hello proje adına sağ tıklayın ve ardından **gönderme Spark uygulama tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-167">From Package Explorer, right-click hello project name, and then select **Submit Spark Application tooHDInsight**.</span></span>        
   2. <span data-ttu-id="79cf2-168">Merhaba, **Spark gönderme** iletişim kutusu, değerleri aşağıdaki hello sağlayın ve ardından **gönderme**:</span><span class="sxs-lookup"><span data-stu-id="79cf2-168">In hello **Spark Submission** dialog box, provide hello following values, and then click **Submit**:</span></span>
      
      * <span data-ttu-id="79cf2-169">İçin **küme adı**, uygulamanızı seçin hello toorun istediğiniz Hdınsight Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="79cf2-169">For **Cluster Name**, select hello HDInsight Spark cluster on which you want toorun your application.</span></span>
      * <span data-ttu-id="79cf2-170">Bir yapı hello Eclipse projeden seçin veya bir sabit sürücüden seçin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-170">Select an artifact from hello Eclipse project, or select one from a hard drive.</span></span> <span data-ttu-id="79cf2-171">Hello varsayılan değer paketi Gezgini'nden sağ hello öğesi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="79cf2-171">hello default value depends on hello item you right-click from package explorer.</span></span>
      * <span data-ttu-id="79cf2-172">Merhaba, **ana sınıf adı** dropdownlist, Gönderme Sihirbazı seçili projenizden tüm nesne adlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79cf2-172">In hello **Main class name** dropdownlist, submission wizard displays all object names from your selected project.</span></span> <span data-ttu-id="79cf2-173">Seçin veya bir giriş toorun istiyor.</span><span class="sxs-lookup"><span data-stu-id="79cf2-173">Select or input one that you want toorun.</span></span> <span data-ttu-id="79cf2-174">Yapı sabit diskten seçerseniz, kendi kendinize ana sınıf adı giriş.</span><span class="sxs-lookup"><span data-stu-id="79cf2-174">If you select artifact from hard disk, you need input main class name by yourself.</span></span> 
      * <span data-ttu-id="79cf2-175">Bu örnekte Hello uygulama kodu herhangi bir komut satırı bağımsız değişkeni gerektirmediği veya Kavanoz veya dosyaları başvurmak için metin kutusu boş kalan hello bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-175">Because hello application code in this example does not require any command-line arguments or reference JARs or files, you can leave hello remaining text boxes empty.</span></span>
        
       ![Spark gönderme iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. <span data-ttu-id="79cf2-177">Merhaba **Spark gönderme** sekmesini hello ilerleme durumunu görüntüleme başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="79cf2-177">hello **Spark Submission** tab should start displaying hello progress.</span></span> <span data-ttu-id="79cf2-178">Merhaba hello kırmızı düğmesini tıklatarak Merhaba uygulaması durdurabilirsiniz **Spark gönderme** penceresi.</span><span class="sxs-lookup"><span data-stu-id="79cf2-178">You can stop hello application by clicking hello red button in hello **Spark Submission** window.</span></span> <span data-ttu-id="79cf2-179">Merhaba Dünya simgesi (Merhaba mavi kutu hello resim olarak gösterilir) tıklayarak çalıştırın özel bu uygulama için hello günlüklerini de görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-179">You can also view hello logs for this specific application run by clicking hello globe icon (denoted by hello blue box in hello image).</span></span>
      
       ![Spark gönderme penceresi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a><span data-ttu-id="79cf2-181">Erişim ve Hdınsight Spark kümeleri Eclipse için Azure araç setindeki Hdınsight araçları kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="79cf2-181">Access and manage HDInsight Spark clusters by using HDInsight Tools in Azure Toolkit for Eclipse</span></span>
<span data-ttu-id="79cf2-182">Merhaba iş çıktısı erişim dahil olmak üzere, Hdınsight araçları kullanarak çeşitli işlemler gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-182">You can perform various operations by using HDInsight Tools, including accessing hello job output.</span></span>

### <a name="access-hello-job-view"></a><span data-ttu-id="79cf2-183">Erişim hello işi görüntüle</span><span class="sxs-lookup"><span data-stu-id="79cf2-183">Access hello job view</span></span>
1. <span data-ttu-id="79cf2-184">Azure Explorer'da genişletin **Hdınsight**hello Spark küme adını genişletin ve ardından **işleri**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-184">In Azure Explorer, expand **HDInsight**, expand hello Spark cluster name, and then click **Jobs**.</span></span> 

    ![Proje görünümü düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. <span data-ttu-id="79cf2-186">Tıklatın hello üzerinde **işleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="79cf2-186">Click on hello **Jobs** node.</span></span> <span data-ttu-id="79cf2-187">Merhaba Hdınsight araçları otomatik-hello E (fx) clipse eklentisi veya yüklü olup olmadığını algılar.</span><span class="sxs-lookup"><span data-stu-id="79cf2-187">hello HDInsight Tools auto-detects whether you installed hello E(fx)clipse plugin or not.</span></span> <span data-ttu-id="79cf2-188">Tıklatın **Tamam** tooinstall Eclipse Market hello ve Eclipse'i yeniden toocontinue ve izleme hello yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="79cf2-188">Click **OK** toocontinue and follow hello instructions tooinstall hello Eclipse Marketplace and restart Eclipse.</span></span>

    ![E (fx) clipse yükleyin](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. <span data-ttu-id="79cf2-190">Açık hello iş görünümünde hello gelen **işleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="79cf2-190">Open hello Job View from hello **Jobs** node.</span></span> <span data-ttu-id="79cf2-191">Merhaba sağ bölmede, hello **Spark iş görünümünde** sekmesi hello küme üzerinde çalıştırılan tüm hello uygulamaları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79cf2-191">In hello right pane, hello **Spark Job View** tab displays all hello applications that were run on hello cluster.</span></span> <span data-ttu-id="79cf2-192">Merhaba uygulaması toosee daha fazla ayrıntı istediğiniz Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79cf2-192">Click hello name of hello application for which you want toosee more details.</span></span>

    ![Uygulama Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. <span data-ttu-id="79cf2-194">Hello iş grafiğinin getirirseniz, temel çalışan iş bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79cf2-194">If you hover on hello job graph, it displays basic running job info.</span></span> <span data-ttu-id="79cf2-195">Merhaba iş grafikte tıklatarak hello aşamaları grafik ve her iş oluşturur bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="79cf2-195">Clicking on hello job graph shows hello stages graph and info that every job generates.</span></span>

    ![İş aşama ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. <span data-ttu-id="79cf2-197">Sık kullanılan günlükleri, sürücü Stderr, sürücü Stdout ve dizin bilgisi gibi hello listelenen **günlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="79cf2-197">Frequently used logs, including Driver Stderr, Driver Stdout, and Directory Info, are listed in hello **Log** tab.</span></span>

    ![Günlük Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. <span data-ttu-id="79cf2-199">Merhaba Spark geçmişi kullanıcı Arabirimi ve hello YARN kullanıcı Arabiriminde (Merhaba uygulama düzeyinde) hello penceresinde hello üstündeki hello ilgili köprüyü tıklatarak da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-199">You can also open hello Spark history UI and hello YARN UI (at hello application level) by clicking hello respective hyperlink at hello top of hello window.</span></span>

### <a name="access-hello-storage-container-for-hello-cluster"></a><span data-ttu-id="79cf2-200">Erişim hello depolama kapsayıcısını hello küme</span><span class="sxs-lookup"><span data-stu-id="79cf2-200">Access hello storage container for hello cluster</span></span>
1. <span data-ttu-id="79cf2-201">Hello Azure Explorer'da genişletin **Hdınsight** kök düğümü toosee kullanılabilir Hdınsight Spark kümeleri listesi.</span><span class="sxs-lookup"><span data-stu-id="79cf2-201">In Azure Explorer, expand hello **HDInsight** root node toosee a list of HDInsight Spark clusters that are available.</span></span>
2. <span data-ttu-id="79cf2-202">Merhaba küme adı toosee hello depolama hesabı ve hello küme hello varsayılan depolama kapsayıcısını genişletin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-202">Expand hello cluster name toosee hello storage account and hello default storage container for hello cluster.</span></span>
   
    ![Depolama hesabı ve varsayılan depolama kapsayıcısı](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. <span data-ttu-id="79cf2-204">Merhaba kümesi ile ilişkili hello depolama kapsayıcı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79cf2-204">Click hello storage container name associated with hello cluster.</span></span> <span data-ttu-id="79cf2-205">Merhaba Hello sağ bölmede, çift **HVACOut** klasör.</span><span class="sxs-lookup"><span data-stu-id="79cf2-205">In hello right pane, double-click hello **HVACOut** folder.</span></span> <span data-ttu-id="79cf2-206">Merhaba birini açın **bölümü -** toosee hello çıktı hello uygulamasının dosyaları.</span><span class="sxs-lookup"><span data-stu-id="79cf2-206">Open one of hello **part-** files toosee hello output of hello application.</span></span>

### <a name="access-hello-spark-history-server"></a><span data-ttu-id="79cf2-207">Erişim hello Spark geçmişi sunucusu</span><span class="sxs-lookup"><span data-stu-id="79cf2-207">Access hello Spark history server</span></span>
1. <span data-ttu-id="79cf2-208">Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık Spark geçmişi kullanıcı Arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-208">In Azure Explorer, right-click your Spark cluster name, and then select **Open Spark History UI**.</span></span> <span data-ttu-id="79cf2-209">İstendiğinde, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-209">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="79cf2-210">Bunlar hello küme hazırlama sırasında belirttiğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79cf2-210">You must have specified these while provisioning hello cluster.</span></span>
2. <span data-ttu-id="79cf2-211">Merhaba Spark geçmişi server panosunda hello uygulama adı toolook yalnızca çalışması sona Merhaba uygulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="79cf2-211">In hello Spark history server dashboard, you use hello application name toolook for hello application that you just finished running.</span></span> <span data-ttu-id="79cf2-212">Kod önceki hello hello uygulama adı kullanarak ayarladığınız `val conf = new SparkConf().setAppName("MyClusterApp")`.</span><span class="sxs-lookup"><span data-stu-id="79cf2-212">In hello preceding code, you set hello application name by using `val conf = new SparkConf().setAppName("MyClusterApp")`.</span></span> <span data-ttu-id="79cf2-213">Bu nedenle, Spark uygulamanızın adı olan **MyClusterApp**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-213">Hence, your Spark application name was **MyClusterApp**.</span></span>

### <a name="start-hello-ambari-portal"></a><span data-ttu-id="79cf2-214">Merhaba Ambari portal Başlat</span><span class="sxs-lookup"><span data-stu-id="79cf2-214">Start hello Ambari portal</span></span>
1. <span data-ttu-id="79cf2-215">Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık küme yönetim portalı (Ambari)**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-215">In Azure Explorer, right-click your Spark cluster name, and then select **Open Cluster Management Portal (Ambari)**.</span></span> 
2. <span data-ttu-id="79cf2-216">İstendiğinde, hello küme için hello yönetici kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="79cf2-216">When you're prompted, enter hello admin credentials for hello cluster.</span></span> <span data-ttu-id="79cf2-217">Bunlar hello küme hazırlama sırasında belirttiğiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79cf2-217">You must have specified these while provisioning hello cluster.</span></span>

### <a name="manage-azure-subscriptions"></a><span data-ttu-id="79cf2-218">Azure Aboneliklerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="79cf2-218">Manage Azure subscriptions</span></span>
<span data-ttu-id="79cf2-219">Varsayılan olarak, tüm Azure aboneliklerinden hello Spark kümeleri Azure araç setini Eclipse için Hdınsight araçları listeler.</span><span class="sxs-lookup"><span data-stu-id="79cf2-219">By default, HDInsight Tools in Azure Toolkit for Eclipse lists hello Spark clusters from all your Azure subscriptions.</span></span> <span data-ttu-id="79cf2-220">Gerekirse, hello abonelikleri tooaccess hello kümenin istediğinizi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-220">If necessary, you can specify hello subscriptions for which you want tooaccess hello cluster.</span></span> 

1. <span data-ttu-id="79cf2-221">Hello Azure Gezgini'nde sağ **Azure** kök düğümünü ve ardından **Aboneliklerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-221">In Azure Explorer, right-click hello **Azure** root node, and then click **Manage Subscriptions**.</span></span> 
2. <span data-ttu-id="79cf2-222">Merhaba iletişim kutusunda, yoksa tooaccess istediğiniz ve ardından, hello abonelik hello onay kutularını temizleyin **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-222">In hello dialog box, clear hello check boxes for hello subscription that you don't want tooaccess, and then click **Close**.</span></span> <span data-ttu-id="79cf2-223">Tıklatarak **oturum kapatma** dışında Azure aboneliğinizin toosign istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="79cf2-223">You can also click **Sign Out** if you want toosign out of your Azure subscription.</span></span>

## <a name="run-a-spark-scala-application-locally"></a><span data-ttu-id="79cf2-224">Spark Scala uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="79cf2-224">Run a Spark Scala application locally</span></span>
<span data-ttu-id="79cf2-225">Hdınsight araçları Azure araç setindeki Eclipse toorun Spark Scala uygulamaları için yerel olarak iş istasyonunuza kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-225">You can use HDInsight Tools in Azure Toolkit for Eclipse toorun Spark Scala applications locally on your workstation.</span></span> <span data-ttu-id="79cf2-226">Genellikle, bu uygulamalar gibi bir depolama kapsayıcısı toocluster erişimine gerek yoktur ve çalıştırın ve yerel olarak test.</span><span class="sxs-lookup"><span data-stu-id="79cf2-226">Typically, these applications don't need access toocluster resources such as a storage container, and you can run and test them locally.</span></span>

### <a name="prerequisite"></a><span data-ttu-id="79cf2-227">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="79cf2-227">Prerequisite</span></span>
<span data-ttu-id="79cf2-228">Bir Windows bilgisayarda hello yerel Spark Scala uygulama çalıştırıyorsanız, ancak açıklandığı gibi bir özel durum alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356).</span><span class="sxs-lookup"><span data-stu-id="79cf2-228">While you're running hello local Spark Scala application on a Windows computer, you might get an exception as explained in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356).</span></span> <span data-ttu-id="79cf2-229">Bu özel durum oluşur **WinUtils.exe** Windows eksik.</span><span class="sxs-lookup"><span data-stu-id="79cf2-229">This exception occurs because **WinUtils.exe** is missing in Windows.</span></span> 

<span data-ttu-id="79cf2-230">tooresolve bu hata, gereken [hello yürütülebilir karşıdan](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa konumu ister **C:\WinUtils\bin**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-230">tooresolve this error, you must [download hello executable](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa location like **C:\WinUtils\bin**.</span></span> <span data-ttu-id="79cf2-231">Merhaba ortam değişkeni sonra eklemelisiniz **HADOOP_HOME** ve çok hello hello değişkenin değerini ayarlamak**C\WinUtils**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-231">You must then add hello environment variable **HADOOP_HOME** and set hello value of hello variable too**C\WinUtils**.</span></span>

### <a name="run-a-local-spark-scala-application"></a><span data-ttu-id="79cf2-232">Yerel bir Spark Scala uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="79cf2-232">Run a local Spark Scala application</span></span>
1. <span data-ttu-id="79cf2-233">Eclipse'i başlatın ve bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="79cf2-233">Start Eclipse and create a project.</span></span> <span data-ttu-id="79cf2-234">Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki seçimleri hello olun ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-234">In hello **New Project** dialog box, make hello following choices, and then click **Next**.</span></span>
   
   * <span data-ttu-id="79cf2-235">Merhaba sol bölmesinde seçin **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-235">In hello left pane, select **HDInsight**.</span></span>
   * <span data-ttu-id="79cf2-236">Merhaba sağ bölmede seçin **Spark Hdınsight yerel çalıştırma örneği (Scala)**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-236">In hello right pane, select **Spark on HDInsight Local Run Sample (Scala)**.</span></span>

    ![Yeni Proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. <span data-ttu-id="79cf2-238">tooprovide hello proje ayrıntılarını, 6'dan aracılığıyla 3 adımları hello önceki bölümde [Hdınsight Spark kümesi için Spark Scala proje ayarlama](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span><span class="sxs-lookup"><span data-stu-id="79cf2-238">tooprovide hello project details, follow steps 3 through 6 from hello earlier section [Set up a Spark Scala project for an HDInsight Spark cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).</span></span>
3. <span data-ttu-id="79cf2-239">Merhaba şablon ekler örnek kod (**LogQuery**) hello altında **src** bilgisayarınızda yerel olarak çalıştırabilirsiniz klasör.</span><span class="sxs-lookup"><span data-stu-id="79cf2-239">hello template adds a sample code (**LogQuery**) under hello **src** folder that you can run locally on your computer.</span></span>
   
    ![LogQuery konumu](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. <span data-ttu-id="79cf2-241">Sağ hello **LogQuery** uygulama, çok noktası**Çalıştır**ve ardından **1 Scala uygulama**.</span><span class="sxs-lookup"><span data-stu-id="79cf2-241">Right-click hello **LogQuery** application, point too**Run As**, and then click **1 Scala Application**.</span></span> <span data-ttu-id="79cf2-242">Aşağıdaki hello şuna benzer bir çıktı göreceksiniz **konsol** hello altındaki sekmesi:</span><span class="sxs-lookup"><span data-stu-id="79cf2-242">You will see an output like this in hello **Console** tab at hello bottom:</span></span>
   
   ![Spark çalıştırma sonucu uygulama yerel](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a><span data-ttu-id="79cf2-244">SSS</span><span class="sxs-lookup"><span data-stu-id="79cf2-244">FAQ</span></span>
<span data-ttu-id="79cf2-245">bir uygulama tooAzure Data Lake Store toosubmit seçin **etkileşimli** hello Azure oturum açma işlemi sırasında modu.</span><span class="sxs-lookup"><span data-stu-id="79cf2-245">toosubmit an application tooAzure Data Lake Store, choose **Interactive** mode during hello Azure sign-in process.</span></span> <span data-ttu-id="79cf2-246">Seçerseniz **otomatik** modu, bir hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-246">If you select **Automated** mode, you can get an error.</span></span>

![signın etkileşim](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

<span data-ttu-id="79cf2-248">Şimdi, biz bunu çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="79cf2-248">Now, we resolved it.</span></span> <span data-ttu-id="79cf2-249">Uygulamanız herhangi bir oturum açma yöntemi bir Azure Data Lake küme toosubmit seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-249">You can choose an Azure Data Lake Cluster toosubmit your application with any sign-in method.</span></span>

## <a name="feedback-and-known-issues"></a><span data-ttu-id="79cf2-250">Geri bildirim ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="79cf2-250">Feedback and known issues</span></span>
<span data-ttu-id="79cf2-251">Şu anda, Spark çıkışları doğrudan görüntüleme desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="79cf2-251">Currently, viewing Spark outputs directly is not supported.</span></span>

<span data-ttu-id="79cf2-252">Tüm öneriler veya Geri bildiriminiz varsa veya bu aracı kullanırken herhangi bir sorunla karşılaşırsanız, bize ücretsiz toosend düşündüğünüz bir e-postası hdivstool@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="79cf2-252">If you have any suggestions or feedback, or if you encounter any problems when using this tool, feel free toosend us an email at hdivstool@microsoft.com.</span></span>

## <span data-ttu-id="79cf2-253"><a name="seealso"></a>Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="79cf2-253"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="79cf2-254">Genel Bakış: Azure HDInsight’ta Apache Spark</span><span class="sxs-lookup"><span data-stu-id="79cf2-254">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="79cf2-255">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="79cf2-255">Scenarios</span></span>
* [<span data-ttu-id="79cf2-256">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="79cf2-256">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="79cf2-257">Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-257">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="79cf2-258">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-258">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="79cf2-259">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-259">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="79cf2-260">HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="79cf2-260">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a><span data-ttu-id="79cf2-261">Oluşturma ve uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="79cf2-261">Creating and running applications</span></span>
* [<span data-ttu-id="79cf2-262">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="79cf2-262">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="79cf2-263">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="79cf2-263">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="79cf2-264">Araçlar ve uzantılar</span><span class="sxs-lookup"><span data-stu-id="79cf2-264">Tools and extensions</span></span>
* [<span data-ttu-id="79cf2-265">Intellij toocreate için Azure araç kullanma ve Spark Scala uygulamaları gönderin</span><span class="sxs-lookup"><span data-stu-id="79cf2-265">Use Azure Toolkit for IntelliJ toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="79cf2-266">VPN üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-266">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through VPN</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="79cf2-267">SSH üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-267">Use Azure Toolkit for IntelliJ toodebug Spark applications remotely through SSH</span></span>](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [<span data-ttu-id="79cf2-268">Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-268">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [<span data-ttu-id="79cf2-269">HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-269">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="79cf2-270">HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler</span><span class="sxs-lookup"><span data-stu-id="79cf2-270">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="79cf2-271">Jupyter not defterleri ile dış paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="79cf2-271">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="79cf2-272">Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın</span><span class="sxs-lookup"><span data-stu-id="79cf2-272">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a><span data-ttu-id="79cf2-273">Kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="79cf2-273">Managing resources</span></span>
* [<span data-ttu-id="79cf2-274">Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="79cf2-274">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="79cf2-275">HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="79cf2-275">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

