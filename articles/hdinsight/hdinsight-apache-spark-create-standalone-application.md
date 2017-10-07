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
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Scala Maven uygulama toorun hdınsight'ta Apache Spark kümesi oluşturma

Bilgi nasıl toocreate Intellij Idea ile Maven kullanarak Scala içinde yazılmış bir Spark uygulaması. Merhaba sistem oluşturma ve Intellij Idea tarafından sağlanan Scala için var olan bir Maven archetype ile başlayan gibi hello makale Apache Maven kullanır.  Intellij Idea Scala uygulaması oluşturma hello aşağıdaki adımları içerir:

* Maven hello yapı sistem olarak kullanın.
* Proje nesne modeli (POM) dosya tooresolve Spark modülü bağımlılıkları güncelleştirin.
* Uygulamanızı Scala içinde yazın.
* Gönderilen tooHDInsight Spark kümeleri olabilir jar dosyasını oluşturun.
* Merhaba uygulaması Livy kullanarak Spark kümesi üzerinde çalıştırın.

> [!NOTE]
> Hdınsight de oluşturma ve uygulamaları tooan Linux'ta Hdınsight Spark kümesi gönderme bir Intellij Idea eklentisi aracı tooease hello işlemi sunar. Daha fazla bilgi için bkz: [toocreate Intellij Idea için Hdınsight araçları eklentisi kullanma ve Spark uygulamaları gönderme](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Geliştirme Seti. Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Bir Java IDE. Bu makalede Intellij Idea 15.0.1 kullanır. Şuradan yükleyebilirsiniz [burada](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Intellij Idea için Scala eklentisini yükleme
Intellij Idea yükleme değil Scala eklentisini etkinleştirmek için komut istemine değil, Intellij Idea başlatın ve aşağıdaki adımları tooinstall hello eklentisi hello gidin:

1. Intellij Idea başlatın ve Hoş Geldiniz ekranında tıklatın **yapılandırma** ve ardından **eklentileri**.
   
    ![Scala eklentisini etkinleştirme](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Merhaba sonraki ekranda, tıklatın **yükleme JetBrains eklentisi** hello sol alt köşesinde gelen. Merhaba, **Gözat JetBrains eklentileri** açar, Scala için arama yapın ve ardından iletişim kutusunu **yükleme**.
   
    ![Scala eklentisini yükleme](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Merhaba eklentisi başarıyla yüklendikten sonra hello tıklatın **yeniden Intellij Idea düğmesi** toorestart hello IDE.

## <a name="create-a-standalone-scala-project"></a>Bir tek başına Scala projesi oluşturma
1. Intellij Idea başlatın ve yeni bir proje oluşturun. Merhaba yeni proje iletişim kutusunda, aşağıdaki seçimleri hello ve ardından olun **sonraki**.
   
    ![Bir Maven projesi oluşturun](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Seçin **Maven** hello proje türü olarak.
   * Belirtin bir **proje SDK**. Yeni'yi tıklatın ve genellikle toohello Java yükleme dizinine gidin `C:\Program Files\Java\jdk1.8.0_66`.
   * Select hello **archetype Oluştur** seçeneği.
   * Mimarisi türleri Hello listeden seçin **org.scala tools.archetypes:scala archetype basit**. Bu hello sağ dizin yapısını oluşturun ve gerekli hello varsayılan bağımlılıkları toowrite Scala programı indirin.
2. İlgili değerlerini sağlamanız **GroupID**, **Artifactıd**, ve **sürüm**. **İleri**’ye tıklayın.
3. Burada belirttiğiniz Maven giriş dizini ve diğer kullanıcı ayarları, hello sonraki iletişim kutusunda, hello Varsayılanları kabul edin ve tıklatın **sonraki**.
4. Merhaba son iletişim kutusunda, bir proje adı ve konum belirtin ve ardından **son**.
5. Merhaba silme **MySpec.Scala** adresindeki dosya **src\test\scala\com\microsoft\spark\example**. Bu hello uygulama için gerekli değildir.
6. Gerekirse, hello varsayılan kaynak ve test dosyalarını yeniden adlandırın. Merhaba sol bölmesinde hello Intellij Idea, çok gidin**src\main\scala\com.microsoft.spark.example**. Sağ **App.scala**, tıklatın **yeniden düzenlemeniz**, dosyayı yeniden adlandır, tıklayın ve hello iletişim kutusunda, Merhaba uygulaması için yeni ad hello sağlayın ve ardından **yeniden düzenlemeniz**.
   
    ![Dosyaları yeniden adlandırma](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. Merhaba sonraki adımlarda hello pom.xml toodefine hello bağımlılıkları hello Spark Scala uygulama için güncelleştirir. Bu bağımlılıklar için toobe indirilir ve Maven uygun biçimde yapılandırın otomatik olarak çözülür.
   
    ![Maven otomatik yüklemeler için yapılandırma](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. Merhaba gelen **dosya** menüsünde tıklatın **ayarları**.
   2. Merhaba, **ayarları** iletişim kutusunda, çok gidin**derleme, yürütme, dağıtımı** > **derleme Araçları** > **Maven**  >  **Alma**.
   3. Çok olarak Hello seçeneğini**Import Maven projeleri otomatik olarak**.
   4. Tıklatın **Uygula**ve ardından **Tamam**.
8. Merhaba Scala kaynak dosya tooinclude uygulama kodunuzu güncelleştirin. Açın ve örnek kod var olan koddan hello ile Merhaba değiştirin ve hello değişiklikleri kaydedin. Bu kod hello HVAC.csv (tüm Hdınsight Spark kümeleri üzerinde kullanılabilir) hello verileri okur, yalnızca bir rakam hello altıncı sütununda hello satırları alır ve hello çıkış çok yazar**/HVACOut** hello varsayılan depolama altında Merhaba küme için kapsayıcı.
   
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
9. Merhaba pom.xml güncelleştirin.
   
   1. İçinde `<project>\<properties>` hello aşağıdakileri ekleyin:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. İçinde `<project>\<dependencies>` hello aşağıdakileri ekleyin:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Değişiklikleri toopom.xml kaydedin.
10. Merhaba .jar dosyası oluşturun. Intellij Idea JAR oluşturulmasını projesinin bir yapı olarak sağlar. Merhaba aşağıdaki adımları gerçekleştirin.
    
    1. Merhaba gelen **dosya** menüsünde tıklatın **proje yapısını**.
    2. Merhaba, **Proje yapısı** iletişim kutusu, tıklatın **yapıları** ve hello artı simgesi'ye tıklayın. Merhaba açılan iletişim kutusunda tıklatın **JAR**ve ardından **bağımlılıkları olan modüller gelen**.
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, hello üç nokta düğmesine (![üç nokta](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) hello karşı **ana sınıfı**.
    4. Merhaba, **ana sınıftan** iletişim kutusu, varsayılan olarak görünür ve ardından select hello sınıfı **Tamam**.
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, o hello seçeneği çok emin olun**toohello hedef JAR ayıklamak** seçilir ve ardından **Tamam**. Bu, tüm bağımlılıkları olan tek bir JAR oluşturur.
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. Merhaba çıkış düzeni sekmesi hello Maven projenin bir parçası olarak dahil tüm hello Kavanoz listeler. Seçebileceğiniz ve hiçbir doğrudan bağımlılık olanları üretileceği Scala uygulama hello delete hello sahiptir. Biz burada oluşturma Merhaba uygulaması için kaldırdığınız dışındaki tüm sonuncu hello (**SparkSimpleApp derleme çıktı**). Merhaba Kavanoz toodelete seçin ve hello **silmek** simgesi.
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Emin olun **olun yapı** kutusu seçiliyse, o hello jar hello proje oluşturulmuş veya güncelleştirilmiş her zaman oluşturulan sağlar. Tıklatın **uygulamak** ve ardından **Tamam**.
    7. Merhaba menü çubuğundaki **yapı**ve ardından **olun proje**. Tıklatarak **derleme yapıları** toocreate hello jar. Merhaba çıkış jar altında oluşturulan **\out\artifacts**.
       
        ![JAR oluşturma](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Merhaba Spark kümesinde Hello uygulamayı çalıştırın
toorun Merhaba uygulaması hello kümede gerçekleştirmelisiniz hello aşağıdaki:

* **Kopya hello uygulama jar toohello Azure depolama blobunu** hello kümesi ile ilişkili. Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bir komut satırı yardımcı programı, toodo şekilde. Çok sayıda tooupload veri kullanabileceğiniz diğer istemciler de vardır. Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).
* **Livy toosubmit bir uygulama işi uzaktan kullanmak** toohello Spark kümesi. Hdınsight'ta Spark kümeleri REST uç noktaları tooremotely gönderme Spark işlerinin sunan Livy içerir. Daha fazla bilgi için bkz: [Livy kullanarak Spark ile uzaktan kümeleri Hdınsight'ta Spark gönderme işleri](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Sonraki adım

Bu, nasıl öğrenilen makale toocreate Spark scala uygulama. Gelişmiş toohello sonraki makalede toolearn nasıl toorun bu uygulamaya bir Hdınsight Spark küme Livy kullanarak.

> [!div class="nextstepaction"]
>[Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

