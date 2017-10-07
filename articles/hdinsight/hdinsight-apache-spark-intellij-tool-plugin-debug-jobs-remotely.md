---
title: "aaaAzure Intellij - Hdınsight Spark üzerinde uzaktan hata ayıklama uygulamalar için araç seti | Microsoft Docs"
description: "Bilgi nasıl vpn aracılığıyla Hdınsight Spark kümeleri üzerinde çalışan Intellij tooremotely hata ayıklama uygulamaları için Azure araç setindeki Hdınsight araçlarını kullanın."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>VPN üzerinden Hdınsight Spark üzerinde uzaktan Intellij toodebug uygulamalar için Azure araç kullanma

Spark applicaltion uzaktan ile ssh ayıklama hello şekilde öneririz. Yönergeler için bkz: [SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında uzaktan hata ayıklama](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Bu makalede, nasıl toouse Intellij toosubmit Hdınsight Spark kümesi üzerinde Spark iş için Hdınsight araçları Azure Araç Seti hello ve masaüstü bilgisayarınızdan uzaktan debug hakkında adım adım yönergeler sağlar. toodo bu nedenle, aşağıdaki üst düzey adımları hello gerçekleştirmeniz gerekir:

1. Siteden siteye veya noktadan siteye Azure sanal ağı oluşturun. Bu belgedeki Hello adımlar bir siteden siteye ağ kullandığınızı varsayar.
2. Merhaba-siteye Azure sanal ağı parçası olan Azure Hdınsight'ta Spark kümesi oluşturun.
3. Merhaba küme headnode ve masaüstünüzü arasında Hello bağlanabildiğini doğrulayın.
4. Intellij Idea Scala uygulama oluşturun ve uzaktan hata ayıklama için yapılandırın.
5. Merhaba uygulamada hata ayıklama ve çalıştırın.

## <a name="prerequisites"></a>Ön koşullar
* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Geliştirme Seti. Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Intellij Idea. Bu makalede sürümünü 2017.1 kullanır. Şuradan yükleyebilirsiniz [burada](https://www.jetbrains.com/idea/download/).
* Azure Araç Seti Intellij için Hdınsight araçları. Intellij için Hdınsight araçları kullanılabilir hello Intellij için Azure araç seti bir parçası olarak. Nasıl tooinstall hello Azure araç seti ile ilgili yönergeler için bkz: [yükleme hello Intellij için Azure Araç Seti](../azure-toolkit-for-intellij-installation.md).
* Intellij Idea Azure aboneliğinizden günlüğüne. Merhaba yönergeleri izleyerek [burada](hdinsight-apache-spark-intellij-tool-plugin.md).
* Bir Windows bilgisayarda uzaktan hata ayıklama için Spark Scala uygulama çalışırken, bir özel durum açıklandığı gibi alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) tooa eksik nedeniyle oluşan Windows WinUtils.exe. Bu hata geçici toowork, şunları yapmalısınız [hello yürütülebilir buradan indirin](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa konumu ister **C:\WinUtils\bin**. Bir ortam değişkeni sonra eklemelisiniz **HADOOP_HOME** ve çok hello hello değişkenin değerini ayarlamak**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>1. adım: Azure sanal ağı oluşturma
Bağlantılar toocreate bir Azure sanal ağı aşağıda hello Hello yönergeleri takip ederek ve hello Masaüstü ve Azure sanal ağ arasında hello bağlantısını kontrol edin.

* [Azure Portal kullanarak siteden siteye VPN bağlantısı olan bir VNet oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [PowerShell kullanarak siteden siteye VPN bağlantısı olan bir VNet oluşturma](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [PowerShell kullanarak bir noktadan siteye bağlantı tooa sanal bir ağ yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>2. adım: bir Hdınsight Spark kümesi oluşturma
Merhaba, oluşturduğunuz Azure Virtual Network parçası olan Azure Hdınsight'ta Apache Spark kümesi da oluşturmanız gerekir. Merhaba bilgileri adresinde kullanın [Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-provision-linux-clusters.md). İsteğe bağlı yapılandırmasının bir parçası olarak hello hello önceki adımda oluşturduğunuz Azure sanal ağı seçin.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Adım 3: hello küme headnode ve masaüstünüzü arasında hello bağlantısını doğrulama
1. Merhaba headnode Hello IP adresini alın. Ambari UI hello küme için açın. Merhaba küme dikey penceresinden tıklayın **Pano**.

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Merhaba sağ üst köşesinden hello Ambari UI'ı tıklatın **ana**.

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Headnodes, çalışan düğümleri ve zookeeper düğümleri listesini görmelisiniz. Merhaba headnodes sahip hello **hn*** öneki. Merhaba ilk headnode'ı tıklatın.

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Açılır ve hello hello sayfanın hello sonundaki **Özet** kutusunda kopyalama hello IP adresi hello headnode ve hello ana bilgisayar adı.

    ![Headnode IP Bul](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Başlangıç IP adresi ve hello headnode toohello hello ana bilgisayar adını içeren **ana** nerede toorun istediğiniz ve hello Spark işleri uzaktan hata ayıklama hello bilgisayarda dosya. Bu, toocommunicate ile başlangıç IP adresi gibi hello ana bilgisayar adı kullanarak hello headnode olanak tanır.

   1. Yükseltilmiş izinleri olan bir Not Defteri'ni açın. Merhaba Dosya menüsünde tıklatın **açık** ve hello hosts dosyasını toohello konumuna gidin. Bir Windows bilgisayarda olmasından `C:\Windows\System32\Drivers\etc\hosts`.
   2. Toohello aşağıdaki hello eklemek **ana** dosyası.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Toohello hello Hdınsight küme tarafından kullanılan Azure Virtual Network bağlı hello bilgisayardan hello IP adresi gibi hello ana bilgisayar adı kullanarak her iki hello headnodes ping atabildiğinizi doğrulayın.
7. Merhaba yönergeleri kullanarak hello küme headnode içine SSH [SSH kullanarak bağlan tooan Hdınsight kümesi](hdinsight-hadoop-linux-use-ssh-unix.md). Merhaba küme headnode hello masaüstü bilgisayar hello IP adresine ping komutu. Bağlantı tooboth hello IP adreslerini hello ağ bağlantısı için bir tane toohello bilgisayar atanan test etmeniz gerekir ve hello hello bilgisayar hello Azure sanal ağ için diğer bağlı.
8. Merhaba adımları da diğer headnode hello için yineleyin.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>4. adım: Intellij için Azure araç setindeki hello Hdınsight araçları kullanarak Spark Scala uygulama oluşturma ve uzaktan hata ayıklama için yapılandırma
1. Intellij Idea başlatın ve yeni bir proje oluşturun. Merhaba yeni proje iletişim kutusunda, aşağıdaki seçimleri hello ve ardından olun **sonraki**.

    ![Spark Scala uygulaması oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Merhaba sol bölmeden seçin **Hdınsight**.
   * Merhaba sağ bölmeden seçin **(Scala) hdınsight'ta Spark**.
   * **İleri**’ye tıklayın.
2. Proje ayrıntılarını aşağıdaki hello Hello sonraki penceresinde sağlayın ve ardından **son**.  
   - Bir proje adı ve proje konumunu belirtin.
   - İçin **proje SDK**, spark 2.x küme, Java 1.7 spark 1.x kümesi için kullanım Java 1.8.
   - İçin **Spark sürüm**, Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK için uygun sürüm tümleştirir. Merhaba spark küme sürümü alt 2.0 ise seçmeniz 1.x spark. Aksi takdirde spark2.x seçmeniz gerekir. Bu örnek Spark2.0.2 (Scala 2.11.8) kullanır.
       ![Spark Scala uygulaması oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. Merhaba Spark proje bir yapı sizin için otomatik olarak oluşturur. toosee hello yapı, şu adımları izleyin.

   1. Merhaba gelen **dosya** menüsünde tıklatın **proje yapısını**.
   2. Merhaba, **Proje yapısı** iletişim kutusu, tıklatın **yapıları** oluşturulan toosee hello varsayılan yapı.
   ![JAR oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      Kendi yapı oluşturabilirsiniz hello üzerinde tıklatarak bly  **+**  yukarıdaki hello görüntü vurgulanmış simgesi.

4. Kitaplıkları tooyour projeye ekleyin. bir kitaplık tooadd hello proje ağacında hello proje adına sağ tıklayın ve ardından **açık modülü ayarları**. Merhaba, **proje yapısını** hello sol bölmesinde, iletişim kutusu **kitaplıkları**hello (+) simgesine tıklayın ve ardından **gelen Maven**.

    ![Kitaplığı ekleyin](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    Merhaba, **Uzaktan Yükleme Kitaplığı Maven depodan** iletişim kutusuna, aramak ve kitaplıkları aşağıdaki hello ekleyin.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Kopya `yarn-site.xml` ve `core-site.xml` hello gelen headnode küme ve toohello proje ekleyin. Aşağıdaki komutları toocopy hello dosyaları hello kullanın. Kullanabileceğiniz [Cygwin](https://cygwin.com/install.html) toorun hello aşağıdaki `scp` toocopy hello hello küme headnodes dosyalarından komutları.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Zaten hello küme headnode IP adresi ve ana bilgisayar adları fo hello hosts dosyasını hello masaüstünde eklediğimiz olduğundan, biz hello kullanabilirsiniz **scp** hello şekilde aşağıdaki komutlarda.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Merhaba altında kopyalayarak bu dosyaları tooyour projesi eklemek **/src** , proje ağacında, örneğin klasör `<your project directory>\src`.
6. Güncelleştirme hello `core-site.xml` toomake hello aşağıdaki değişiklikler.

   1. `core-site.xml`Merhaba kümesi ile ilişkili hello şifrelenmiş anahtar toohello depolama hesabını içerir. Merhaba, `core-site.xml` toohello projesi Değiştir hello şifrelenmiş anahtar hello varsayılan depolama hesabıyla ilişkili hello gerçek depolama anahtarı eklendi. Bkz: [depolama erişim tuşlarınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Hello girişleri aşağıdaki hello kaldırmak `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Merhaba dosyasını kaydedin.
7. Uygulamanız için Hello ana sınıf ekleyin. Merhaba gelen **Proje Gezgini**, sağ **src**, çok noktası**yeni**ve ardından **Scala sınıfı**.

    ![Kaynak kodu ekleyin](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. Merhaba, **yeni Scala Sınıf Oluştur** iletişim kutusunda, için bir ad sağlayın **türü** seçin **nesne**ve ardından **Tamam**.

    ![Kaynak kodu ekleyin](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. Merhaba, `MyClusterAppMain.scala` dosya, hello aşağıdaki kodu yapıştırın. Bu kod hello Spark bağlam oluşturur ve başlatır bir `executeJob` hello yönteminden `SparkSample` nesnesi.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Yeni bir Scala nesnesi adlı tooadd yukarıdaki adımları 8 ve 9 `SparkSample`. toothis sınıf hello aşağıdaki kodu ekleyin. Bu kod hello HVAC.csv (tüm Hdınsight Spark kümeleri üzerinde kullanılabilir) hello verileri okur, yalnızca bir rakam hello yedinci hello CSV sütununda hello satırları alır ve hello çıkış çok yazar**/HVACOut** hello varsayılan altında Merhaba küme depolama kapsayıcısı.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. 8. ve 9 adlı yeni bir sınıf tooadd yukarıdaki adımları yineleyin `RemoteClusterDebugging`. Bu sınıf uygulamalarında hata ayıklama için kullanılan hello Spark test çerçevesi uygular. Aşağıdaki kodu toohello hello eklemek `RemoteClusterDebugging` sınıfı.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Önemli noktalar toonote burada birkaç:

   * İçin `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, hello Spark derleme JAR hello küme depolama hello belirtilen yolda kullanılabilir olduğundan emin olun.
   * İçin `setJars`, burada hello yapı jar oluşturulacak hello konumu belirtin. Genellikle `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. Merhaba, `RemoteClusterDebugging` sınıfı, hello sağ `test` anahtar sözcüğü ve seçin **RemoteClusterDebugging yapılandırma oluşturmak**.

    ![Uzaktan yapılandırma oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Hello iletişim kutusunda, hello yapılandırması için bir ad sağlayın ve seçin hello **Test türü** olarak **Test adı**. Diğer tüm değerler varsayılan olarak bırakın, tıklatın **Uygula**ve ardından **Tamam**.

    ![Uzaktan yapılandırma oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Artık görmelisiniz bir **uzaktan çalıştırmak** yapılandırma açılan hello menü çubuğunda.

    ![Uzaktan yapılandırma oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>5. adım: hello uygulamayı hata ayıklama modunda çalıştırın.
1. Intellij Idea projenizi açın `SparkSample.scala` ve bir kesme noktası sonraki too'val rdd1 Oluştur '. Bir kesme noktası oluşturmak için hello açılır menüsünden seçin **işlevi executeJob satırında**.

    ![Kesme noktası ekleme](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Merhaba tıklatın **hata ayıklama çalıştırmak** düğmesine bir sonraki toohello **uzaktan çalıştırmak** yapılandırma açılan toostart Merhaba uygulaması çalıştıran.

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Merhaba program yürütme hello kesme noktasına ulaştığında, görmelisiniz bir **hata ayıklayıcı** hello alt bölmedeki sekmesi.

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Merhaba tıklayın (**+**) simgesi tooadd hello resimde gösterildiği gibi bir izleme.

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Burada, önce hello değişkeni Merhaba uygulaması ihlal çünkü `rdd1` , biz hello değişkeninde ilk 5 satırları hello ne görebilirsiniz bu izleme kullanılarak oluşturulmuş `rdd`. **ENTER**'a basın.

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    Yukarıdaki hello resimde gördüğünüz çalışma zamanında veri ve hata ayıklama terrabytes sorgulayabilir olduğunu nasıl uygulama ilerler. Örneğin, yukarıdaki hello resimde gösterilen hello çıktısında bu hello gördüğünüz ilk hello çıktı satırıdır üstbilgi. Bunu temel alarak, gerekirse, uygulama kodu tooskip hello başlık satırı değiştirebilirsiniz.
5. Merhaba artık tıklatabilir **Sürdür Program** simgesi tooproceed ile uygulamanızı çalıştırın.

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Merhaba uygulaması başarıyla tamamlarsa, hello aşağıdaki gibi bir çıktı görmeniz gerekir.

    ![Hata ayıklama modunda Hello programı çalıştır](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Tanıtım
* Scala projesi (Video) oluşturun: [Spark Scala uygulamaları oluşturma](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Uzaktan hata ayıklama (Video): [Intellij toodebug Spark uygulamalarında uzaktan Hdınsight kümesinde için kullanım Azure Araç Seti](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Uygulamaları oluşturma ve çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Intellij toocreate için Hdınsight Araçları'nı Azure araç setindeki kullanın ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [SSH üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)
