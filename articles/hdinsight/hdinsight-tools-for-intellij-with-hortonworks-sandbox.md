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
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma

Nasıl üzerinde uygulamaları toouse Intellij toodevelop Apache Scala uygulamaları ve ardından test için Hdınsight araçları hello öğrenin [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/) iş istasyonunuza çalışıyor. 

[Intellij Idea](https://www.jetbrains.com/idea/) bilgisayar yazılımı geliştirmek için Java tümleşik geliştirme ortamı (IDE) değil. Geliştirilmiş ve uygulamalarınızı Hortonworks Sandbox test sonra bunları çok taşıyabilirsiniz[Azure Hdınsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Ön koşullar

Bu öğreticiye başlamadan önce

- Hortonworks veri Platformu (HDP) 2.4 Hortonworks yerel ortamınızda çalışan Sandbox. tooconfigure HDP, bkz: [hello Hadoop ekosistemindeki bir Hadoop korumalı bir sanal makinede ile çalışmaya başlama](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Intellij için Hdınsight araçları yalnızca HDP 2.4 ile test edilmiştir. tooget HDP 2.4 genişletin **Hortonworks Sandbox arşiv** hello üzerinde [Hortonworks korumalı alan site yüklemeleri](http://hortonworks.com/downloads/#sandbox).

- [Java Geliştirme Seti (JDK) 1.8 veya sonraki bir sürümü](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK hello Azure araç takımı tarafından Intellij için gereklidir.

- [Intellij Idea community sürümü](https://www.jetbrains.com/idea/download) hello ile [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) eklenti ve hello [Intellij için Azure Araç Seti](../azure-toolkit-for-intellij.md) eklentisi. Intellij için Hdınsight araçları hello Intellij için Azure araç seti bir parçası olarak kullanılabilir. 

  tooinstall hello eklentileri hello aşağıdaki:

  1. Intellij Idea açın.
  2. Merhaba üzerinde **Hoş Geldiniz** ekran, select **yapılandırma**ve ardından **eklentileri**.
  3. Seçin **yükleme JetBrains eklentisi** hello sol alt köşesindeki.
  4. Merhaba arama işlevi toosearch için kullanmak **Scala**ve ardından **yükleme**.
  5. Seçin **yeniden Intellij Idea** toocomplete hello yükleme.
  6. Yineleme adım 4 ve 5 tooinstall hello **Intellij için Azure Araç Seti**. Daha fazla bilgi için bkz: [yükleme hello Intellij için Azure Araç Seti](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Spark Scala uygulaması oluşturma

Bu bölümde, Intellij Idea kullanarak bir örnek Scala projesi oluşturun. Merhaba proje göndermeden önce hello sonraki bölümde Intellij Idea toohello Hortonworks Sandbox (öykünücüsü) bağlayın.

1. Intellij Idea istasyonunuzdan açın. Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:

   a. Seçin **Hdınsight** > **(Scala) hdınsight'ta Spark**.

   b. Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:

    * **Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği
    * **SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma

   ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Seçin **sonraki**.

3. Merhaba, sonraki **yeni proje** iletişim kutusunda, aşağıdaki hello:

    ![Proje Özellikleri Intellij Scala oluşturma](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    a. Merhaba, **proje adı** kutusunda, bir proje adı girin.

    b. Merhaba, **proje konumu** kutusunda, bir proje konumu girin.

    c. Sonraki toohello **proje SDK** aşağı açılan listesinden, **yeni**seçin **JDK**, ve Java JDK 1,7 veya sonraki bir sürümü hello klasörü belirtin. Seçin **Java 1.8** hello Spark 2.x kümesi ya da seçin **Java 1.7** hello Spark 1.x kümesi için. Merhaba varsayılan konumu C:\Program Files\Java\jdk1.8.x_xxx şeklindedir.

    d. Merhaba, **Spark sürüm** aşağı açılan listesinde, Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK hello uygun sürüm tümleştirir. Merhaba Spark küme sürüm 2.0 eskiyse, seçin **1.x Spark**. Aksi takdirde seçin **Spark2.x**. Bu örnek, Spark 1.6.2 (Scala 2.10.5) kullanır. Scala işaretlenmiş hello deposu kullandığınızdan emin olun 2.10.x. Scala işaretlenmiş hello deposu kullanmayın 2.11.x.

4. **Son**’u seçin.

5. Merhaba, **proje** görünüm zaten açık, basın **Alt + 1** tooopen onu.

6. İçinde **Proje Gezgini**hello projenizi genişletin ve ardından **src**.

7. Sağ **src**, çok noktası**yeni**ve ardından **Scala sınıfı**.

8. Merhaba, **adı** kutusuna, hello bir ad girin **türü** kutusunda **nesne**ve ardından **Tamam**.

    ![Merhaba yeni Scala Sınıf Oluştur penceresi](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. Merhaba .scala dosyasında hello aşağıdaki kodu yapıştırın:

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

10. Merhaba üzerinde **yapı** menüsünde, select **derleme projesi**. Merhaba derleme başarıyla tamamlandığını doğrulayın.


## <a name="link-toohello-hortonworks-sandbox"></a>Toohello Hortonworks Sandbox bağlantı

Tooa Hortonworks Sandbox (öykünücüsü) bağlayabilirsiniz, varolan Intellij uygulamaya sahip olmanız gerekir.

toolink tooan öykünücüsü, aşağıdaki hello:

1. Intellij projesinde açık hello.

2. Merhaba üzerinde **Görünüm** menüsünde, select **Windows Araçları**ve ardından **Azure Gezgini**.

3. Genişletme **Azure**, sağ **Hdınsight**ve ardından **bir öykünücü bağlantı**.

4. Merhaba, **bağlantı A yeni öykünücü** penceresinde hello kök hesabı hello Hortonworks korumalı alan için yapılandırdığınız hello ekran aşağıdaki değerleri benzer toothose girin ve ardından hello parolayı girin **Tamam** . 

   ![Merhaba "Bağlantı bir yeni öykünücü" penceresi](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. tooconfigure hello öykünücüsü, select **Evet**.

Merhaba öykünücü başarıyla bağlandığında hello öykünücü (Hortonworks Sandbox) hello Hdınsight düğümünde listelenir.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Merhaba Spark Scala uygulama toohello Hortonworks Sandbox gönderme

Intellij Idea toohello öykünücüsü bağlı sonra projenizi gönderebilirsiniz.

toosubmit bir proje tooan öykünücüsü hello aşağıdaki:

1. İçinde **Proje Gezgini**hello projesine sağ tıklayın ve ardından **gönderme Spark uygulama tooHDInsight**.

2. Aşağıdaki hello:

    a. Merhaba, **Spark kümesi (yalnızca Linux)** aşağı açılan listesinde, yerel Hortonworks korumalı alan seçin.

    b. Merhaba, **ana sınıf adı** kutusunda seçin veya hello ana sınıf adı girin. Bu öğretici için hello adıdır **GroupByTest**.

3. Seçin **gönderme**. Merhaba iş gönderme günlüklerini hello Spark gönderme aracı penceresinde görüntülenir.

## <a name="next-steps"></a>Sonraki adımlar

- Intellij için Hdınsight araçları kullanarak Hdınsight için toocreate Spark uygulamaları nasıl Git çok toolearn[Hdınsight Spark Linux kümesi için Intellij toocreate Spark uygulamaları için Azure Araç Seti Hdınsight araçlarını kullanın](hdinsight-apache-spark-intellij-tool-plugin.md).

- toowatch, Intellij için Hdınsight Araçları'nın bir video Git çok[Spark geliştirme Intellij için Hdınsight araçları tanıtmak](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn kullanarak toodebug Spark uygulamalarında uzaktan SSH, aracılığıyla hdınsight'ta Araç Seti hello nasıl Git çok[SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında uzaktan hata ayıklama](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn kullanarak toodebug Spark uygulamalarında uzaktan VPN üzerinden hdınsight'ta Araç Seti hello nasıl Git çok[Azure Araç Seti Hdınsight Spark Linux kümesi üzerinde uzaktan Intellij toodebug Spark uygulamalar için Hdınsight araçları kullanın](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- Eclipse toocreate bir Spark uygulaması için Hdınsight araçları toouse Git çok nasıl toolearn[Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch Eclipse için Hdınsight Araçları'nın bir video Git çok[kullanımı Hdınsight araç Eclipse toocreate Spark uygulamaları için](https://mix.office.com/watch/1rau2mopb6fha).
