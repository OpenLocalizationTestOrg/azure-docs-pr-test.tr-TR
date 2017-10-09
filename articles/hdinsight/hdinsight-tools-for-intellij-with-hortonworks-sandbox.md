---
title: "aaaUse Hortonworks Sandbox ile Intellij için Azure Araç Seti | Microsoft Docs"
description: "Bilgi toouse Intellij Hortonworks Sandbox ile Azure araç setindeki Hdınsight araçları nasıl."
keywords: "hadoop araçları hive sorgusu, ıntellij, hortonworks korumalı alan, ıntellij için azure Araç Seti"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a><span data-ttu-id="e3c21-104">Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma</span><span class="sxs-lookup"><span data-stu-id="e3c21-104">Use HDInsight Tools for IntelliJ with Hortonworks Sandbox</span></span>

<span data-ttu-id="e3c21-105">Nasıl üzerinde uygulamaları toouse Intellij toodevelop Apache Scala uygulamaları ve ardından test için Hdınsight araçları hello öğrenin [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) iş istasyonunuza çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="e3c21-105">Learn how toouse HDInsight Tools for IntelliJ toodevelop Apache Scala applications and then test hello applications on [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) running on your workstation.</span></span> 

<span data-ttu-id="e3c21-106">[Intellij Idea](https://www.jetbrains.com/idea/) bilgisayar yazılımı geliştirmek için Java tümleşik geliştirme ortamı (IDE) değil.</span><span class="sxs-lookup"><span data-stu-id="e3c21-106">[IntelliJ IDEA](https://www.jetbrains.com/idea/) is a Java-integrated development environment (IDE) for developing computer software.</span></span> <span data-ttu-id="e3c21-107">Geliştirilmiş ve uygulamalarınızı Hortonworks Sandbox test sonra bunları çok taşıyabilirsiniz[Azure Hdınsight](hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-107">After you have developed and tested your applications on Hortonworks Sandbox, you can move them too[Azure HDInsight](hdinsight-hadoop-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3c21-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e3c21-108">Prerequisites</span></span>

<span data-ttu-id="e3c21-109">Bu öğreticiye başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e3c21-109">Before you begin this tutorial, you must have:</span></span>

- <span data-ttu-id="e3c21-110">Hortonworks veri Platformu (HDP) 2.4 Hortonworks yerel ortamınızda çalışan Sandbox.</span><span class="sxs-lookup"><span data-stu-id="e3c21-110">Hortonworks Data Platform (HDP) 2.4 on Hortonworks Sandbox running on your local environment.</span></span> <span data-ttu-id="e3c21-111">tooconfigure HDP, bkz: [hello Hadoop ekosistemindeki bir Hadoop korumalı bir sanal makinede ile çalışmaya başlama](hdinsight-hadoop-emulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-111">tooconfigure HDP, see [Get started in hello Hadoop ecosystem with a Hadoop sandbox on a virtual machine](hdinsight-hadoop-emulator-get-started.md).</span></span> 
    >[!NOTE]
    ><span data-ttu-id="e3c21-112">Intellij için Hdınsight araçları yalnızca HDP 2.4 ile test edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-112">HDInsight Tools for IntelliJ has been tested only with HDP 2.4.</span></span> <span data-ttu-id="e3c21-113">tooget HDP 2.4 genişletin **Hortonworks Sandbox arşiv** hello üzerinde [Hortonworks korumalı alan site yüklemeleri](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="e3c21-113">tooget HDP 2.4, expand **Hortonworks Sandbox Archive** on hello [Hortonworks Sandbox downloads site](http://hortonworks.com/downloads/#sandbox).</span></span>

- <span data-ttu-id="e3c21-114">[Java Geliştirme Seti (JDK) 1.8 veya sonraki bir sürümü](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="e3c21-114">[Java Developer Kit (JDK) version 1.8 or later](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span> <span data-ttu-id="e3c21-115">JDK hello Azure araç takımı tarafından Intellij için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-115">JDK is required by hello Azure Toolkit for IntelliJ.</span></span>

- <span data-ttu-id="e3c21-116">[Intellij Idea community sürümü](https://www.jetbrains.com/idea/download) hello ile [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) eklenti ve hello [Intellij için Azure Araç Seti](../azure-toolkit-for-intellij.md) eklentisi.</span><span class="sxs-lookup"><span data-stu-id="e3c21-116">[IntelliJ IDEA community edition](https://www.jetbrains.com/idea/download) with hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) plug-in and hello [Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij.md) plug-in.</span></span> <span data-ttu-id="e3c21-117">Intellij için Hdınsight araçları hello Intellij için Azure araç seti bir parçası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-117">HDInsight Tools for IntelliJ is available as a part of hello Azure Toolkit for IntelliJ.</span></span> 

  <span data-ttu-id="e3c21-118">tooinstall hello eklentileri hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e3c21-118">tooinstall hello plug-ins, do hello following:</span></span>

  1. <span data-ttu-id="e3c21-119">Intellij Idea açın.</span><span class="sxs-lookup"><span data-stu-id="e3c21-119">Open IntelliJ IDEA.</span></span>
  2. <span data-ttu-id="e3c21-120">Merhaba üzerinde **Hoş Geldiniz** ekran, select **yapılandırma**ve ardından **eklentileri**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-120">On hello **Welcome** screen, select **Configure**, and then select **Plugins**.</span></span>
  3. <span data-ttu-id="e3c21-121">Seçin **yükleme JetBrains eklentisi** hello sol alt köşesindeki.</span><span class="sxs-lookup"><span data-stu-id="e3c21-121">Select **Install JetBrains plugin** in hello lower-left corner.</span></span>
  4. <span data-ttu-id="e3c21-122">Merhaba arama işlevi toosearch için kullanmak **Scala**ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-122">Use hello search function toosearch for **Scala**, and then select **Install**.</span></span>
  5. <span data-ttu-id="e3c21-123">Seçin **yeniden Intellij Idea** toocomplete hello yükleme.</span><span class="sxs-lookup"><span data-stu-id="e3c21-123">Select **Restart IntelliJ IDEA** toocomplete hello installation.</span></span>
  6. <span data-ttu-id="e3c21-124">Yineleme adım 4 ve 5 tooinstall hello **Intellij için Azure Araç Seti**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-124">Repeat step 4 and 5 tooinstall hello **Azure Toolkit for IntelliJ**.</span></span> <span data-ttu-id="e3c21-125">Daha fazla bilgi için bkz: [yükleme hello Intellij için Azure Araç Seti](../azure-toolkit-for-intellij-installation.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-125">For more information, see [Install hello Azure Toolkit for IntelliJ](../azure-toolkit-for-intellij-installation.md).</span></span>

## <a name="create-a-spark-scala-application"></a><span data-ttu-id="e3c21-126">Spark Scala uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3c21-126">Create a Spark Scala application</span></span>

<span data-ttu-id="e3c21-127">Bu bölümde, Intellij Idea kullanarak bir örnek Scala projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e3c21-127">In this section, you create a sample Scala project by using IntelliJ IDEA.</span></span> <span data-ttu-id="e3c21-128">Merhaba proje göndermeden önce hello sonraki bölümde Intellij Idea toohello Hortonworks Sandbox (öykünücüsü) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e3c21-128">In hello next section, you link IntelliJ IDEA toohello Hortonworks Sandbox (emulator) before you submit hello project.</span></span>

1. <span data-ttu-id="e3c21-129">Intellij Idea istasyonunuzdan açın.</span><span class="sxs-lookup"><span data-stu-id="e3c21-129">Open IntelliJ IDEA from your workstation.</span></span> <span data-ttu-id="e3c21-130">Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e3c21-130">In hello **New Project** dialog box, do hello following:</span></span>

   <span data-ttu-id="e3c21-131">a.</span><span class="sxs-lookup"><span data-stu-id="e3c21-131">a.</span></span> <span data-ttu-id="e3c21-132">Seçin **Hdınsight** > **(Scala) hdınsight'ta Spark**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-132">Select **HDInsight** > **Spark on HDInsight (Scala)**.</span></span>

   <span data-ttu-id="e3c21-133">b.</span><span class="sxs-lookup"><span data-stu-id="e3c21-133">b.</span></span> <span data-ttu-id="e3c21-134">Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="e3c21-134">In hello **Build tool** list, select either of hello following, according tooyour need:</span></span>

    * <span data-ttu-id="e3c21-135">**Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği</span><span class="sxs-lookup"><span data-stu-id="e3c21-135">**Maven**, for Scala project-creation wizard support</span></span>
    * <span data-ttu-id="e3c21-136">**SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3c21-136">**SBT**, for managing hello dependencies and building for hello Scala project</span></span>

   ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. <span data-ttu-id="e3c21-138">Seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-138">Select **Next**.</span></span>

3. <span data-ttu-id="e3c21-139">Merhaba, sonraki **yeni proje** iletişim kutusunda, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e3c21-139">In hello next **New Project** dialog box, do hello following:</span></span>

    ![Proje Özellikleri Intellij Scala oluşturma](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    <span data-ttu-id="e3c21-141">a.</span><span class="sxs-lookup"><span data-stu-id="e3c21-141">a.</span></span> <span data-ttu-id="e3c21-142">Merhaba, **proje adı** kutusunda, bir proje adı girin.</span><span class="sxs-lookup"><span data-stu-id="e3c21-142">In hello **Project name** box, enter a project name.</span></span>

    <span data-ttu-id="e3c21-143">b.</span><span class="sxs-lookup"><span data-stu-id="e3c21-143">b.</span></span> <span data-ttu-id="e3c21-144">Merhaba, **proje konumu** kutusunda, bir proje konumu girin.</span><span class="sxs-lookup"><span data-stu-id="e3c21-144">In hello **Project location** box, enter a project location.</span></span>

    <span data-ttu-id="e3c21-145">c.</span><span class="sxs-lookup"><span data-stu-id="e3c21-145">c.</span></span> <span data-ttu-id="e3c21-146">Sonraki toohello **proje SDK** aşağı açılan listesinden, **yeni**seçin **JDK**, ve Java JDK 1,7 veya sonraki bir sürümü hello klasörü belirtin.</span><span class="sxs-lookup"><span data-stu-id="e3c21-146">Next toohello **Project SDK** drop-down list, select **New**, select **JDK**, and then specify hello folder of Java JDK version 1.7 or later.</span></span> <span data-ttu-id="e3c21-147">Seçin **Java 1.8** hello Spark 2.x kümesi ya da seçin **Java 1.7** hello Spark 1.x kümesi için.</span><span class="sxs-lookup"><span data-stu-id="e3c21-147">Select **Java 1.8** for hello Spark 2.x cluster, or select **Java 1.7** for hello Spark 1.x cluster.</span></span> <span data-ttu-id="e3c21-148">Merhaba varsayılan konumu C:\Program Files\Java\jdk1.8.x_xxx şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-148">hello default location is C:\Program Files\Java\jdk1.8.x_xxx.</span></span>

    <span data-ttu-id="e3c21-149">d.</span><span class="sxs-lookup"><span data-stu-id="e3c21-149">d.</span></span> <span data-ttu-id="e3c21-150">Merhaba, **Spark sürüm** aşağı açılan listesinde, Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK hello uygun sürüm tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-150">In hello **Spark version** drop-down list, Scala project creation wizard integrates hello proper version for Spark SDK and Scala SDK.</span></span> <span data-ttu-id="e3c21-151">Merhaba Spark küme sürüm 2.0 eskiyse, seçin **1.x Spark**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-151">If hello Spark cluster version is earlier than 2.0, select **Spark 1.x**.</span></span> <span data-ttu-id="e3c21-152">Aksi takdirde seçin **Spark2.x**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-152">Otherwise, select **Spark2.x**.</span></span> <span data-ttu-id="e3c21-153">Bu örnek, Spark 1.6.2 (Scala 2.10.5) kullanır.</span><span class="sxs-lookup"><span data-stu-id="e3c21-153">This example uses Spark 1.6.2 (Scala 2.10.5).</span></span> <span data-ttu-id="e3c21-154">Scala işaretlenmiş hello deposu kullandığınızdan emin olun 2.10.x.</span><span class="sxs-lookup"><span data-stu-id="e3c21-154">Make sure that you are using hello repository marked Scala 2.10.x.</span></span> <span data-ttu-id="e3c21-155">Scala işaretlenmiş hello deposu kullanmayın 2.11.x.</span><span class="sxs-lookup"><span data-stu-id="e3c21-155">Do not use hello repository marked Scala 2.11.x.</span></span>

4. <span data-ttu-id="e3c21-156">**Son**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="e3c21-156">Select **Finish**.</span></span>

5. <span data-ttu-id="e3c21-157">Merhaba, **proje** görünüm zaten açık, basın **Alt + 1** tooopen onu.</span><span class="sxs-lookup"><span data-stu-id="e3c21-157">If hello **Project** view is not already open, press **Alt+1** tooopen it.</span></span>

6. <span data-ttu-id="e3c21-158">İçinde **Proje Gezgini**hello projenizi genişletin ve ardından **src**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-158">In **Project Explorer**, expand hello project, and then select **src**.</span></span>

7. <span data-ttu-id="e3c21-159">Sağ **src**, çok noktası**yeni**ve ardından **Scala sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-159">Right-click **src**, point too**New**, and then select **Scala class**.</span></span>

8. <span data-ttu-id="e3c21-160">Merhaba, **adı** kutusuna, hello bir ad girin **türü** kutusunda **nesne**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-160">In hello **Name** box, enter a name, in hello **Kind** box, select **Object**, and then select **OK**.</span></span>

    ![Merhaba yeni Scala Sınıf Oluştur penceresi](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. <span data-ttu-id="e3c21-162">Merhaba .scala dosyasında hello aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="e3c21-162">In hello .scala file, paste hello following code:</span></span>

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. <span data-ttu-id="e3c21-163">Merhaba üzerinde **yapı** menüsünde, select **derleme projesi**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-163">On hello **Build** menu, select **Build project**.</span></span> <span data-ttu-id="e3c21-164">Merhaba derleme başarıyla tamamlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e3c21-164">Make sure that hello compilation has been completed successfully.</span></span>


## <a name="link-toohello-hortonworks-sandbox"></a><span data-ttu-id="e3c21-165">Toohello Hortonworks Sandbox bağlantı</span><span class="sxs-lookup"><span data-stu-id="e3c21-165">Link toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="e3c21-166">Tooa Hortonworks Sandbox (öykünücüsü) bağlayabilirsiniz, varolan Intellij uygulamaya sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-166">Before you can link tooa Hortonworks Sandbox (emulator), you must have an existing IntelliJ application.</span></span>

<span data-ttu-id="e3c21-167">toolink tooan öykünücüsü, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e3c21-167">toolink tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="e3c21-168">Intellij projesinde açık hello.</span><span class="sxs-lookup"><span data-stu-id="e3c21-168">Open hello project in IntelliJ.</span></span>

2. <span data-ttu-id="e3c21-169">Merhaba üzerinde **Görünüm** menüsünde, select **Windows Araçları**ve ardından **Azure Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-169">On hello **View** menu, select **Tools Windows**, and then select **Azure Explorer**.</span></span>

3. <span data-ttu-id="e3c21-170">Genişletme **Azure**, sağ **Hdınsight**ve ardından **bir öykünücü bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-170">Expand **Azure**, right-click **HDInsight**, and then select **Link an Emulator**.</span></span>

4. <span data-ttu-id="e3c21-171">Merhaba, **bağlantı A yeni öykünücü** penceresinde hello kök hesabı hello Hortonworks korumalı alan için yapılandırdığınız hello ekran aşağıdaki değerleri benzer toothose girin ve ardından hello parolayı girin **Tamam** .</span><span class="sxs-lookup"><span data-stu-id="e3c21-171">In hello **Link A New Emulator** window, enter hello password that you've configured for hello root account of hello Hortonworks Sandbox, enter values similar toothose in hello following screenshot, and then select **OK**.</span></span> 

   ![Merhaba "Bağlantı bir yeni öykünücü" penceresi](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. <span data-ttu-id="e3c21-173">tooconfigure hello öykünücüsü, select **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-173">tooconfigure hello emulator, select **Yes**.</span></span>

<span data-ttu-id="e3c21-174">Merhaba öykünücü başarıyla bağlandığında hello öykünücü (Hortonworks Sandbox) hello Hdınsight düğümünde listelenir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-174">When hello emulator is connected successfully, hello emulator (Hortonworks Sandbox) is listed in hello HDInsight node.</span></span>

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a><span data-ttu-id="e3c21-175">Merhaba Spark Scala uygulama toohello Hortonworks Sandbox gönderme</span><span class="sxs-lookup"><span data-stu-id="e3c21-175">Submit hello Spark Scala application toohello Hortonworks Sandbox</span></span>

<span data-ttu-id="e3c21-176">Intellij Idea toohello öykünücüsü bağlı sonra projenizi gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3c21-176">After you have linked IntelliJ IDEA toohello emulator, you can submit your project.</span></span>

<span data-ttu-id="e3c21-177">toosubmit bir proje tooan öykünücüsü hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e3c21-177">toosubmit a project tooan emulator, do hello following:</span></span>

1. <span data-ttu-id="e3c21-178">İçinde **Proje Gezgini**hello projesine sağ tıklayın ve ardından **gönderme Spark uygulama tooHDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-178">In **Project Explorer**, right-click hello project, and then select **Submit Spark application tooHDInsight**.</span></span>

2. <span data-ttu-id="e3c21-179">Aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="e3c21-179">Do hello following:</span></span>

    <span data-ttu-id="e3c21-180">a.</span><span class="sxs-lookup"><span data-stu-id="e3c21-180">a.</span></span> <span data-ttu-id="e3c21-181">Merhaba, **Spark kümesi (yalnızca Linux)** aşağı açılan listesinde, yerel Hortonworks korumalı alan seçin.</span><span class="sxs-lookup"><span data-stu-id="e3c21-181">In hello **Spark cluster (Linux only)** drop-down list, select your local Hortonworks Sandbox.</span></span>

    <span data-ttu-id="e3c21-182">b.</span><span class="sxs-lookup"><span data-stu-id="e3c21-182">b.</span></span> <span data-ttu-id="e3c21-183">Merhaba, **ana sınıf adı** kutusunda seçin veya hello ana sınıf adı girin.</span><span class="sxs-lookup"><span data-stu-id="e3c21-183">In hello **Main class name** box, choose or enter hello main class name.</span></span> <span data-ttu-id="e3c21-184">Bu öğretici için hello adıdır **GroupByTest**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-184">For this tutorial, hello name is **GroupByTest**.</span></span>

3. <span data-ttu-id="e3c21-185">Seçin **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="e3c21-185">Select **Submit**.</span></span> <span data-ttu-id="e3c21-186">Merhaba iş gönderme günlüklerini hello Spark gönderme aracı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e3c21-186">hello job submission logs are shown in hello Spark submission tool window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3c21-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3c21-187">Next steps</span></span>

- <span data-ttu-id="e3c21-188">Intellij için Hdınsight araçları kullanarak Hdınsight için toocreate Spark uygulamaları nasıl Git çok toolearn[Hdınsight Spark Linux kümesi için Intellij toocreate Spark uygulamaları için Azure Araç Seti Hdınsight araçlarını kullanın](hdinsight-apache-spark-intellij-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-188">toolearn how toocreate Spark applications for HDInsight by using HDInsight Tools for IntelliJ, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toocreate Spark applications for HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin.md).</span></span>

- <span data-ttu-id="e3c21-189">toowatch, Intellij için Hdınsight Araçları'nın bir video Git çok[Spark geliştirme Intellij için Hdınsight araçları tanıtmak](https://www.youtube.com/watch?v=YTZzYVgut6c).</span><span class="sxs-lookup"><span data-stu-id="e3c21-189">toowatch a video of HDInsight Tools for IntelliJ, go too[Introduce HDInsight Tools for IntelliJ for Spark Development](https://www.youtube.com/watch?v=YTZzYVgut6c).</span></span>

- <span data-ttu-id="e3c21-190">toolearn kullanarak toodebug Spark uygulamalarında uzaktan SSH, aracılığıyla hdınsight'ta Araç Seti hello nasıl Git çok[SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında uzaktan hata ayıklama](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-190">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through SSH, go too[Remotely debug Spark applications on an HDInsight cluster with Azure Toolkit for IntelliJ through SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).</span></span>

- <span data-ttu-id="e3c21-191">toolearn kullanarak toodebug Spark uygulamalarında uzaktan VPN üzerinden hdınsight'ta Araç Seti hello nasıl Git çok[Azure Araç Seti Hdınsight Spark Linux kümesi üzerinde uzaktan Intellij toodebug Spark uygulamalar için Hdınsight araçları kullanın](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-191">toolearn how toodebug Spark applications by using hello toolkit remotely on HDInsight through VPN, go too[Use HDInsight Tools in Azure Toolkit for IntelliJ toodebug Spark applications remotely on HDInsight Spark Linux cluster](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).</span></span>

- <span data-ttu-id="e3c21-192">Eclipse toocreate bir Spark uygulaması için Hdınsight araçları toouse Git çok nasıl toolearn[Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın](hdinsight-apache-spark-eclipse-tool-plugin.md).</span><span class="sxs-lookup"><span data-stu-id="e3c21-192">toolearn how toouse HDInsight Tools for Eclipse toocreate a Spark application, go too[Use HDInsight Tools in Azure Toolkit for Eclipse toocreate Spark applications](hdinsight-apache-spark-eclipse-tool-plugin.md).</span></span>

- <span data-ttu-id="e3c21-193">toowatch Eclipse için Hdınsight Araçları'nın bir video Git çok[kullanımı Hdınsight araç Eclipse toocreate Spark uygulamaları için](https://mix.office.com/watch/1rau2mopb6fha).</span><span class="sxs-lookup"><span data-stu-id="e3c21-193">toowatch a video of HDInsight Tools for Eclipse, go too[Use HDInsight Tool for Eclipse toocreate Spark applications](https://mix.office.com/watch/1rau2mopb6fha).</span></span>
