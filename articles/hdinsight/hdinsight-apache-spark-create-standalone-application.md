---
title: "Spark kümeleri - Azure Hdınsight üzerinde aaaCreate Scala uygulama toorun | Microsoft Docs"
description: "Merhaba yapı olarak sistemi ve var olan bir Maven archetype Intellij Idea tarafından sağlanan Scala için Scala Apache Maven ile yazılmış bir Spark uygulaması oluşturun."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="7b3b0-103">Scala Maven uygulama toorun hdınsight'ta Apache Spark kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b3b0-103">Create a Scala Maven application toorun on Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="7b3b0-104">Bilgi nasıl toocreate Intellij Idea ile Maven kullanarak Scala içinde yazılmış bir Spark uygulaması.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-104">Learn how toocreate a Spark application written in Scala using Maven with IntelliJ IDEA.</span></span> <span data-ttu-id="7b3b0-105">Merhaba sistem oluşturma ve Intellij Idea tarafından sağlanan Scala için var olan bir Maven archetype ile başlayan gibi hello makale Apache Maven kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-105">hello article uses Apache Maven as hello build system and starts with an existing Maven archetype for Scala provided by IntelliJ IDEA.</span></span>  <span data-ttu-id="7b3b0-106">Intellij Idea Scala uygulaması oluşturma hello aşağıdaki adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="7b3b0-106">Creating a Scala application in IntelliJ IDEA involves hello following steps:</span></span>

* <span data-ttu-id="7b3b0-107">Maven hello yapı sistem olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-107">Use Maven as hello build system.</span></span>
* <span data-ttu-id="7b3b0-108">Proje nesne modeli (POM) dosya tooresolve Spark modülü bağımlılıkları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-108">Update Project Object Model (POM) file tooresolve Spark module dependencies.</span></span>
* <span data-ttu-id="7b3b0-109">Uygulamanızı Scala içinde yazın.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-109">Write your application in Scala.</span></span>
* <span data-ttu-id="7b3b0-110">Gönderilen tooHDInsight Spark kümeleri olabilir jar dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-110">Generate a jar file that can be submitted tooHDInsight Spark clusters.</span></span>
* <span data-ttu-id="7b3b0-111">Merhaba uygulaması Livy kullanarak Spark kümesi üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-111">Run hello application on Spark cluster using Livy.</span></span>

> [!NOTE]
> <span data-ttu-id="7b3b0-112">Hdınsight de oluşturma ve uygulamaları tooan Linux'ta Hdınsight Spark kümesi gönderme bir Intellij Idea eklentisi aracı tooease hello işlemi sunar.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-112">HDInsight also provides an IntelliJ IDEA plugin tool tooease hello process of creating and submitting applications tooan HDInsight Spark cluster on Linux.</span></span> <span data-ttu-id="7b3b0-113">Daha fazla bilgi için bkz: [toocreate Intellij Idea için Hdınsight araçları eklentisi kullanma ve Spark uygulamaları gönderme](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-113">For more information, see [Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark applications](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7b3b0-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7b3b0-114">Prerequisites</span></span>

* <span data-ttu-id="7b3b0-115">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-115">An Azure subscription.</span></span> <span data-ttu-id="7b3b0-116">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-116">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7b3b0-117">Hdınsight'ta bir Apache Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-117">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7b3b0-118">Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-118">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>
* <span data-ttu-id="7b3b0-119">Oracle Java Geliştirme Seti.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-119">Oracle Java Development kit.</span></span> <span data-ttu-id="7b3b0-120">Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-120">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="7b3b0-121">Bir Java IDE.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-121">A Java IDE.</span></span> <span data-ttu-id="7b3b0-122">Bu makalede Intellij Idea 15.0.1 kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-122">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="7b3b0-123">Şuradan yükleyebilirsiniz [burada](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-123">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>

## <a name="install-scala-plugin-for-intellij-idea"></a><span data-ttu-id="7b3b0-124">Intellij Idea için Scala eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="7b3b0-124">Install Scala plugin for IntelliJ IDEA</span></span>
<span data-ttu-id="7b3b0-125">Intellij Idea yükleme değil Scala eklentisini etkinleştirmek için komut istemine değil, Intellij Idea başlatın ve aşağıdaki adımları tooinstall hello eklentisi hello gidin:</span><span class="sxs-lookup"><span data-stu-id="7b3b0-125">If IntelliJ IDEA installation did not not prompt for enabling Scala plugin, launch IntelliJ IDEA and go through hello following steps tooinstall hello plugin:</span></span>

1. <span data-ttu-id="7b3b0-126">Intellij Idea başlatın ve Hoş Geldiniz ekranında tıklatın **yapılandırma** ve ardından **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-126">Start IntelliJ IDEA and from welcome screen click **Configure** and then click **Plugins**.</span></span>
   
    ![Scala eklentisini etkinleştirme](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. <span data-ttu-id="7b3b0-128">Merhaba sonraki ekranda, tıklatın **yükleme JetBrains eklentisi** hello sol alt köşesinde gelen.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-128">In hello next screen, click **Install JetBrains plugin** from hello lower left corner.</span></span> <span data-ttu-id="7b3b0-129">Merhaba, **Gözat JetBrains eklentileri** açar, Scala için arama yapın ve ardından iletişim kutusunu **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-129">In hello **Browse JetBrains Plugins** dialog box that opens, search for Scala and then click **Install**.</span></span>
   
    ![Scala eklentisini yükleme](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. <span data-ttu-id="7b3b0-131">Merhaba eklentisi başarıyla yüklendikten sonra hello tıklatın **yeniden Intellij Idea düğmesi** toorestart hello IDE.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-131">After hello plugin installs successfully, click hello **Restart IntelliJ IDEA button** toorestart hello IDE.</span></span>

## <a name="create-a-standalone-scala-project"></a><span data-ttu-id="7b3b0-132">Bir tek başına Scala projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b3b0-132">Create a standalone Scala project</span></span>
1. <span data-ttu-id="7b3b0-133">Intellij Idea başlatın ve yeni bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-133">Launch IntelliJ IDEA and create a new project.</span></span> <span data-ttu-id="7b3b0-134">Merhaba yeni proje iletişim kutusunda, aşağıdaki seçimleri hello ve ardından olun **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-134">In hello new project dialog box, make hello following choices, and then click **Next**.</span></span>
   
    ![Bir Maven projesi oluşturun](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * <span data-ttu-id="7b3b0-136">Seçin **Maven** hello proje türü olarak.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-136">Select **Maven** as hello project type.</span></span>
   * <span data-ttu-id="7b3b0-137">Belirtin bir **proje SDK**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-137">Specify a **Project SDK**.</span></span> <span data-ttu-id="7b3b0-138">Yeni'yi tıklatın ve genellikle toohello Java yükleme dizinine gidin `C:\Program Files\Java\jdk1.8.0_66`.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-138">Click New and navigate toohello Java installation directory, typically `C:\Program Files\Java\jdk1.8.0_66`.</span></span>
   * <span data-ttu-id="7b3b0-139">Select hello **archetype Oluştur** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-139">Select hello **Create from archetype** option.</span></span>
   * <span data-ttu-id="7b3b0-140">Mimarisi türleri Hello listeden seçin **org.scala tools.archetypes:scala archetype basit**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-140">From hello list of archetypes, select **org.scala-tools.archetypes:scala-archetype-simple**.</span></span> <span data-ttu-id="7b3b0-141">Bu hello sağ dizin yapısını oluşturun ve gerekli hello varsayılan bağımlılıkları toowrite Scala programı indirin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-141">This will create hello right directory structure and download hello required default dependencies toowrite Scala program.</span></span>
2. <span data-ttu-id="7b3b0-142">İlgili değerlerini sağlamanız **GroupID**, **Artifactıd**, ve **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-142">Provide relevant values for **GroupId**, **ArtifactId**, and **Version**.</span></span> <span data-ttu-id="7b3b0-143">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-143">Click **Next**.</span></span>
3. <span data-ttu-id="7b3b0-144">Burada belirttiğiniz Maven giriş dizini ve diğer kullanıcı ayarları, hello sonraki iletişim kutusunda, hello Varsayılanları kabul edin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-144">In hello next dialog box, where you specify Maven home directory and other user settings, accept hello defaults and click **Next**.</span></span>
4. <span data-ttu-id="7b3b0-145">Merhaba son iletişim kutusunda, bir proje adı ve konum belirtin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-145">In hello last dialog box, specify a project name and location and then click **Finish**.</span></span>
5. <span data-ttu-id="7b3b0-146">Merhaba silme **MySpec.Scala** adresindeki dosya **src\test\scala\com\microsoft\spark\example**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-146">Delete hello **MySpec.Scala** file at **src\test\scala\com\microsoft\spark\example**.</span></span> <span data-ttu-id="7b3b0-147">Bu hello uygulama için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-147">You do not need this for hello application.</span></span>
6. <span data-ttu-id="7b3b0-148">Gerekirse, hello varsayılan kaynak ve test dosyalarını yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-148">If required, rename hello default source and test files.</span></span> <span data-ttu-id="7b3b0-149">Merhaba sol bölmesinde hello Intellij Idea, çok gidin**src\main\scala\com.microsoft.spark.example**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-149">From hello left pane in hello IntelliJ IDEA, navigate too**src\main\scala\com.microsoft.spark.example**.</span></span> <span data-ttu-id="7b3b0-150">Sağ **App.scala**, tıklatın **yeniden düzenlemeniz**, dosyayı yeniden adlandır, tıklayın ve hello iletişim kutusunda, Merhaba uygulaması için yeni ad hello sağlayın ve ardından **yeniden düzenlemeniz**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-150">Right-click **App.scala**, click **Refactor**, click Rename file, and in hello dialog box, provide hello new name for hello application and then click **Refactor**.</span></span>
   
    ![Dosyaları yeniden adlandırma](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. <span data-ttu-id="7b3b0-152">Merhaba sonraki adımlarda hello pom.xml toodefine hello bağımlılıkları hello Spark Scala uygulama için güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-152">In hello subsequent steps, you will update hello pom.xml toodefine hello dependencies for hello Spark Scala application.</span></span> <span data-ttu-id="7b3b0-153">Bu bağımlılıklar için toobe indirilir ve Maven uygun biçimde yapılandırın otomatik olarak çözülür.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-153">For those dependencies toobe downloaded and resolved automatically, you must configure Maven accordingly.</span></span>
   
    ![Maven otomatik yüklemeler için yapılandırma](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. <span data-ttu-id="7b3b0-155">Merhaba gelen **dosya** menüsünde tıklatın **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-155">From hello **File** menu, click **Settings**.</span></span>
   2. <span data-ttu-id="7b3b0-156">Merhaba, **ayarları** iletişim kutusunda, çok gidin**derleme, yürütme, dağıtımı** > **derleme Araçları** > **Maven**  >  **Alma**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-156">In hello **Settings** dialog box, navigate too**Build, Execution, Deployment** > **Build Tools** > **Maven** > **Importing**.</span></span>
   3. <span data-ttu-id="7b3b0-157">Çok olarak Hello seçeneğini**Import Maven projeleri otomatik olarak**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-157">Select hello option too**Import Maven projects automatically**.</span></span>
   4. <span data-ttu-id="7b3b0-158">Tıklatın **Uygula**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-158">Click **Apply**, and then click **OK**.</span></span>
8. <span data-ttu-id="7b3b0-159">Merhaba Scala kaynak dosya tooinclude uygulama kodunuzu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-159">Update hello Scala source file tooinclude your application code.</span></span> <span data-ttu-id="7b3b0-160">Açın ve örnek kod var olan koddan hello ile Merhaba değiştirin ve hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-160">Open and replace hello existing sample code with hello following code and save hello changes.</span></span> <span data-ttu-id="7b3b0-161">Bu kod hello HVAC.csv (tüm Hdınsight Spark kümeleri üzerinde kullanılabilir) hello verileri okur, yalnızca bir rakam hello altıncı sütununda hello satırları alır ve hello çıkış çok yazar**/HVACOut** hello varsayılan depolama altında Merhaba küme için kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-161">This code reads hello data from hello HVAC.csv (available on all HDInsight Spark clusters), retrieves hello rows that only have one digit in hello sixth column, and writes hello output too**/HVACOut** under hello default storage container for hello cluster.</span></span>
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. <span data-ttu-id="7b3b0-162">Merhaba pom.xml güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-162">Update hello pom.xml.</span></span>
   
   1. <span data-ttu-id="7b3b0-163">İçinde `<project>\<properties>` hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7b3b0-163">Within `<project>\<properties>` add hello following:</span></span>
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. <span data-ttu-id="7b3b0-164">İçinde `<project>\<dependencies>` hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7b3b0-164">Within `<project>\<dependencies>` add hello following:</span></span>
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      <span data-ttu-id="7b3b0-165">Değişiklikleri toopom.xml kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-165">Save changes toopom.xml.</span></span>
10. <span data-ttu-id="7b3b0-166">Merhaba .jar dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-166">Create hello .jar file.</span></span> <span data-ttu-id="7b3b0-167">Intellij Idea JAR oluşturulmasını projesinin bir yapı olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-167">IntelliJ IDEA enables creation of JAR as an artifact of a project.</span></span> <span data-ttu-id="7b3b0-168">Merhaba aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-168">Perform hello following steps.</span></span>
    
    1. <span data-ttu-id="7b3b0-169">Merhaba gelen **dosya** menüsünde tıklatın **proje yapısını**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-169">From hello **File** menu, click **Project Structure**.</span></span>
    2. <span data-ttu-id="7b3b0-170">Merhaba, **Proje yapısı** iletişim kutusu, tıklatın **yapıları** ve hello artı simgesi'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-170">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="7b3b0-171">Merhaba açılan iletişim kutusunda tıklatın **JAR**ve ardından **bağımlılıkları olan modüller gelen**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-171">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. <span data-ttu-id="7b3b0-173">Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, hello üç nokta düğmesine (![üç nokta](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) hello karşı **ana sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-173">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) against hello **Main Class**.</span></span>
    4. <span data-ttu-id="7b3b0-174">Merhaba, **ana sınıftan** iletişim kutusu, varsayılan olarak görünür ve ardından select hello sınıfı **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-174">In hello **Select Main Class** dialog box, select hello class that appears by default and then click **OK**.</span></span>
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. <span data-ttu-id="7b3b0-176">Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, o hello seçeneği çok emin olun**toohello hedef JAR ayıklamak** seçilir ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-176">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="7b3b0-177">Bu, tüm bağımlılıkları olan tek bir JAR oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-177">This creates a single JAR with all dependencies.</span></span>
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. <span data-ttu-id="7b3b0-179">Merhaba çıkış düzeni sekmesi hello Maven projenin bir parçası olarak dahil tüm hello Kavanoz listeler.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-179">hello output layout tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="7b3b0-180">Seçebileceğiniz ve hiçbir doğrudan bağımlılık olanları üretileceği Scala uygulama hello delete hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-180">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="7b3b0-181">Biz burada oluşturma Merhaba uygulaması için kaldırdığınız dışındaki tüm sonuncu hello (**SparkSimpleApp derleme çıktı**).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-181">For hello application we are creating here, you can remove all but hello last one (**SparkSimpleApp compile output**).</span></span> <span data-ttu-id="7b3b0-182">Merhaba Kavanoz toodelete seçin ve hello **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-182">Select hello jars toodelete and then click hello **Delete** icon.</span></span>
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        <span data-ttu-id="7b3b0-184">Emin olun **olun yapı** kutusu seçiliyse, o hello jar hello proje oluşturulmuş veya güncelleştirilmiş her zaman oluşturulan sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-184">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="7b3b0-185">Tıklatın **uygulamak** ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-185">Click **Apply** and then **OK**.</span></span>
    7. <span data-ttu-id="7b3b0-186">Merhaba menü çubuğundaki **yapı**ve ardından **olun proje**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-186">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="7b3b0-187">Tıklatarak **derleme yapıları** toocreate hello jar.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-187">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="7b3b0-188">Merhaba çıkış jar altında oluşturulan **\out\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-188">hello output jar is created under **\out\artifacts**.</span></span>
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a><span data-ttu-id="7b3b0-190">Merhaba Spark kümesinde Hello uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="7b3b0-190">Run hello application on hello Spark cluster</span></span>
<span data-ttu-id="7b3b0-191">toorun Merhaba uygulaması hello kümede gerçekleştirmelisiniz hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="7b3b0-191">toorun hello application on hello cluster, you must do hello following:</span></span>

* <span data-ttu-id="7b3b0-192">**Kopya hello uygulama jar toohello Azure depolama blobunu** hello kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-192">**Copy hello application jar toohello Azure storage blob** associated with hello cluster.</span></span> <span data-ttu-id="7b3b0-193">Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bir komut satırı yardımcı programı, toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-193">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="7b3b0-194">Çok sayıda tooupload veri kullanabileceğiniz diğer istemciler de vardır.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-194">There are a lot of other clients as well that you can use tooupload data.</span></span> <span data-ttu-id="7b3b0-195">Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-195">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
* <span data-ttu-id="7b3b0-196">**Livy toosubmit bir uygulama işi uzaktan kullanmak** toohello Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-196">**Use Livy toosubmit an application job remotely** toohello Spark cluster.</span></span> <span data-ttu-id="7b3b0-197">Hdınsight'ta Spark kümeleri REST uç noktaları tooremotely gönderme Spark işlerinin sunan Livy içerir.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-197">Spark clusters on HDInsight includes Livy that exposes REST endpoints tooremotely submit Spark jobs.</span></span> <span data-ttu-id="7b3b0-198">Daha fazla bilgi için bkz: [Livy kullanarak Spark ile uzaktan kümeleri Hdınsight'ta Spark gönderme işleri](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b0-198">For more information, see [Submit Spark jobs remotely using Livy with Spark clusters on HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="7b3b0-199">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="7b3b0-199">Next step</span></span>

<span data-ttu-id="7b3b0-200">Bu, nasıl öğrenilen makale toocreate Spark scala uygulama.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-200">In this article you learned how toocreate a Spark scala application.</span></span> <span data-ttu-id="7b3b0-201">Gelişmiş toohello sonraki makalede toolearn nasıl toorun bu uygulamaya bir Hdınsight Spark küme Livy kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7b3b0-201">Advance toohello next article toolearn how toorun this application on an HDInsight Spark cluster using Livy.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="7b3b0-202">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7b3b0-202">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

