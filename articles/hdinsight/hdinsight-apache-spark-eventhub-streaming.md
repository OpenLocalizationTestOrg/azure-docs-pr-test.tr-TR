---
title: "aaaUse ile olay hub'ları Azure hdınsight'ta Apache Spark akış | Microsoft Docs"
description: "Nasıl toosend veri akışı tooAzure olay hub'ı ve sonra bu olayları bir scala uygulaması kullanarak Hdınsight Spark kümesinde almak bir Apache Spark akış örnek oluşturun."
keywords: "Apache spark akış, spark akış, spark örnek, apache spark akış örneği, olay hub'ı azure örneği, spark örnek"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Apache Spark akış: Hdınsight'ta Spark ile Azure Event Hubs işlem verilerini küme

Bu makalede, aşağıdaki adımları hello içerir örnek akış bir Apache Spark oluşturun:

1. Bir Azure olay Hub'ına bir tek başına uygulama tooingest iletileri kullanın.

2. İki farklı yaklaşım ile gerçek zamanlı Azure Hdınsight'ta Spark kümesinde çalışan bir uygulama kullanarak olay Hub'ından Merhaba iletileri alır.

3. Toopersist veri toodifferent depolama sistemlerini akış analitik komut zincirleri oluşturun veya hello kolay bir şekilde verilerinden öngörü edinme.

## <a name="prerequisites"></a>Ön koşullar

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Spark akış kavramları

Spark akış ayrıntılı bir açıklaması için bkz: [Apache Spark genel bakış akış](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). Hdınsight aynı akış özellikleri tooa Spark küme Azure'da hello getirir.  

## <a name="what-does-this-solution-do"></a>Bu çözüm ne yapar?

Bu makalede, toocreate bir Spark akış örneği hello aşağıdaki adımları gerçekleştirin:

1. Bir akış olayların alacak bir Azure Event Hub oluşturun.

2. Bir yerel tek başına uygulamayı çalıştırmak olaylar oluşturur ve toohello Azure olay hub'ı iter. Bu örnek uygulama hello konumunda yayımlanır [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Çeşitli veri işleme/analiz gerçekleştirmek ve bir akış uygulaması Azure olay Hub'ından akış olayları okur bir Spark kümesi üzerinde uzaktan çalıştırabilirsiniz.

## <a name="create-an-azure-event-hub"></a>Bir Azure olay hub'ı Oluştur

1. Toohello üzerinde oturum [Azure Portal](https://ms.portal.azure.com), tıklatıp **yeni** hello adresindeki hello ekranın sol üst.

2. **Nesnelerin İnterneti**’ne ve ardından **Event Hubs**’a tıklayın.

    ![Örnek Spark akış Create event hub](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "örnek Spark akış Create event hub")

3. Merhaba, **ad alanı oluşturma** dikey penceresinde, bir ad alanı adı girin. Merhaba fiyatlandırma Katmanı (temel veya standart) seçin. Ayrıca, hangi toocreate hello kaynak bir Azure aboneliği, kaynak grubunu ve konumu seçin. Tıklatın **oluşturma** toocreate hello ad alanı.

      ![Bir örnek Spark akış için olay hub'ı ad](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "örnek Spark akış için bir olay hub'ı adı belirtin")

    > [!NOTE]
    > Select aynı hello **konumu** Apache Spark kümeniz Hdınsight tooreduce gecikme ve maliyetlerin.
    >
    >

4. Merhaba olay hub'ları ad listesinde hello yeni oluşturulan ad alanı tıklayın.      


5. Merhaba ad alanı dikey penceresinde tıklayın **Event Hubs**ve ardından **+ olay hub'ı** toocreate yeni bir olay hub'ı.
   
    ![Örnek Spark akış Create event hub](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "örnek Spark akış Create event hub")

6. Olay hub'ı, kümesi hello bölüm sayısı too10 ve ileti bekletme too1 için bir ad yazın. Böylece hello geri kalan varsayılan olarak bırakın ve ardından Biz bu çözümdeki Merhaba iletileri arşivleme değil **oluşturma**.
   
    ![Olay hub'ı ayrıntılarını sağlamak için örnek akış Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "için Spark akış örnek olay hub'ı ayrıntılarını sağlayın")

7. Olay hub'ı yeni oluşturulan hello hello Event Hub dikey penceresinde listelenir.
    
     ![Merhaba Spark akış örneği için olay hub'ı görüntülemek](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "görünüm Event Hub'hello için Spark akış örneği")

8. Geri hello ad alanı dikey penceresinde (değil hello belirli olay Hub dikey) tıklayın **paylaşılan erişim ilkeleri**ve ardından **RootManageSharedAccessKey**.
    
     ![Merhaba Spark akış örneği için olay hub'ı ilkeler ayarlama](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "hello için Event Hub'ı ayarlamak ilkeleri Spark akış örneği")

9. Merhaba Kopyala düğmesine toocopy hello tıklatın **RootManageSharedAccessKey** birincil anahtar ve bağlantı dizesi toohello Pano. Bu toouse daha sonra hello öğreticide kaydedin.
    
     ![Merhaba Spark akış örneği için olay hub'ı ilke anahtarları görüntülemek](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "görünüm olay hub'ı ilke anahtarları hello için Spark akış örneği")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>İletileri tooAzure olay hub'ı kullanan bir örnek Scala uygulamaları Gönder

Bu bölümdeki olayların bir akış oluşturur ve tooAzure daha önce oluşturduğunuz olay Hub gönderen bir tek başına yerel Scala uygulama kullanın. Bu uygulama github'da kullanılabilir [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). Bu GitHub deposunu zaten çatallanmış Hello adımlar burada varsayar.

1. Merhaba aşağıdaki bu uygulamayı çalıştırdığınız hello bilgisayarda yüklü olduğundan emin olun.

    * Oracle Java Geliştirme Seti. Şuradan yükleyebilirsiniz [burada](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. Buradan indirebilirsiniz [burada](https://maven.apache.org/download.cgi). Yönergeler tooinstall Maven kullanılabilir [burada](https://maven.apache.org/install.html).

2. Bir komut istemi açın ve hello GitHub deposuna Merhaba örnek Scala uygulaması için klonlanmış toohello konuma gidin ve komut toobuild Merhaba uygulaması aşağıdaki hello çalıştırın.

        mvn package

3. Merhaba çıkış jar Merhaba uygulaması için **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, altında oluşturulan **/target** dizin. Bu makale tootest hello eksiksiz çözüm içinde daha sonra bu JAR kullanın.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Uygulama tooreceive iletileri olay Hub'ından bir Spark kümesi oluşturma 

İki yaklaşım tooconnect Spark akış ve Azure Event Hubs, alıcı tabanlı bağlantı ve doğrudan-DStream tabanlı bağlantı sunuyoruz. Doğrudan-DStream tabanlı 2017 Oca üzerinde hello 2.0.3 sürümde sunulmuştur. Daha fazla kullanıcı olarak tooreplace hello özgün alıcı tabanlı bağlantı beklenir ve verimli kaynak. Daha fazla ayrıntı bulunan [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). Doğrudan DStream yalnızca Spark 2.0 + destekler.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Merhaba bağımlılık toospark eventhubs Bağlayıcısı ile uygulamaları derleme

Biz de Spark-EventHubs github'da sürümü hazırlama hello yayımlar. toouse hello hazırlama Spark EventHubs, hello ilk adımı tooindicate girişi toopom.xml aşağıdaki hello ekleyerek kaynak deposu hello olarak GitHub sürümüdür:

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

Bağımlılık tooyour proje tootake hello yayın öncesi sürüm aşağıdaki hello daha sonra ekleyebilirsiniz.

Maven bağımlılığı

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

SBT bağımlılık

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Doğrudan DStream bağlantı

İçinde doğrudan DStream kullanan örnekler içeren bir önceden derlenmiş jar dosyasını karşıdan [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).

Merhaba jar dosyasını içeren kaynak kodu kullanılabilir üç örnekler [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Alma [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) bir örnek olarak:

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

Örneğin, yukarıdaki hello içinde `eventhubParameters` hello parametreleri belirli tooa tek EventHubs örnek ve sahip toopass, toohello `createDirectStreams` doğrudan DStream nesne eşleme tooa olay hub'ları ad alanı oluşturur API. Merhaba doğrudan DStream nesnesi üzerinde Spark akış API çerçevesi tarafından sağlanan herhangi bir DStream API'yi çağırabilirsiniz. Bu örnekte, biz hello son 3 mikro toplu aralıkları her sözcüğün hello sıklığını hesaplayın.

### <a name="receiver-based-connection"></a>Alıcı tabanlı bağlantı

Olaylar ve yol hello toodifferent hedeflerine alır, Scala içinde yazılmış örnek uygulama yayınlamayı Spark şu adresten edinilebilir [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Merhaba tooupdate hello uygulama olay hub'ı yapılandırmanız için aşağıdaki adımları izleyin ve hello çıkış jar oluşturun.

1. Intellij Idea başlatın ve ekran seçin hello başlatma **sürüm denetiminden kullanıma** ve ardından **Git**.
   
    ![Apache Spark örnek - Git get kaynaklardan akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark örnek - Git get kaynaklardan akış")

2. Merhaba, **kopya deposu** iletişim kutusu, hello URL toohello Git deposu tooclone gelen sağlamak, hello dizin tooclone belirtin ve ardından **kopya**.
   
    ![Apache Spark örnek - Git kopya akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark örnek - Git kopya akış")
3. Merhaba proje tamamen kopyalanması kadar hello istemleri izleyin. Tuşuna **Alt + 1** tooopen hello **proje görünümü**. Merhaba aşağıdaki benzemelidir.
   
    ![Apache Spark örnek - proje görünümü akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark akış örnek - proje görünümü")
4. Merhaba uygulama kodu ile Java8 derlendiğinden emin olun. tooensure bunu, **dosya**, tıklatın **proje yapısını**ve hello **proje** sekmesi, proje dil düzeyi çok ayarlandığından emin olun**8 - Lambda'lar, türü Ek açıklamalar, vb.**.
   
    ![Apache Spark örnek - kümesi derleyici akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark örnek - kümesi derleyici akış")
5. Açık hello **pom.xml** ve hello Spark sürüm doğru olduğundan emin olun. Altında `<properties>` düğümü, aşağıdaki kod parçacığında Merhaba arayın ve hello Spark sürüm doğrulayın.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. Merhaba uygulaması gerektirir adlı bir bağımlılık jar **JDBC sürücüsü jar**. Bir Azure SQL veritabanına olay Hub'ından alınan gerekli toowrite Merhaba iletileri budur. Bu jar yükleyebilirsiniz (v4.1 veya sonrası) gelen [burada](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Başvuru toothis jar hello proje kitaplığa ekleyebilirsiniz. Merhaba aşağıdaki adımları gerçekleştirin:
     
     1. Merhaba uygulaması açık olduğu Intellij Idea penceresinden tıklatın **dosya**, tıklatın **Proje yapısı**ve ardından **kitaplıkları**. 
     2. Hello tıklatın Ekle simgesi (![Ekle simgesi](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), tıklatın **Java**ve ardından hello JDBC sürücüsü jar indirdiğiniz toohello konumuna gidin. Merhaba istemleri tooadd hello jar dosyasını toohello projesi kitaplık izleyin.

         ![eksik bağımlılıkları ekleyin](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "eksik bağımlılık Kavanoz ekleme")
     3. **Uygula**'ya tıklayın.

7. Merhaba çıkış jar dosyasını oluşturun. Merhaba aşağıdaki adımları gerçekleştirin.

   1. Merhaba, **Proje yapısı** iletişim kutusu, tıklatın **yapıları** ve hello artı simgesi'ye tıklayın. Merhaba açılan iletişim kutusunda tıklatın **JAR**ve ardından **bağımlılıkları olan modüller gelen**.      
       
       ![Apache Spark akış örnek - JAR oluşturma](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark akış örnek - JAR oluşturma")
   2. Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, hello üç nokta düğmesine (![üç nokta](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) hello karşı **ana sınıfı**.
   3. Merhaba, **ana sınıftan** iletişim kutusunda, hello kullanılabilir sınıfların birini seçin ve ardından **Tamam**.
      
       ![Apache Spark örnek - select sınıfı jar için akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark akış örnek - jar için select sınıfı")
   4. Merhaba, **oluşturma JAR modüllerden** iletişim kutusunda, o hello seçeneği çok emin olun**toohello hedef JAR ayıklamak** seçilir ve ardından **Tamam**. Bu, tüm bağımlılıkları olan tek bir JAR oluşturur.
      
       ![Apache Spark akış örnek - jar modüllerden oluşturma](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark akış örnek - jar modüllerden oluşturma")
   5. Merhaba **çıkış düzeni** sekmesi hello Maven projenin bir parçası olarak dahil tüm hello Kavanoz listeler. Seçebileceğiniz ve hiçbir doğrudan bağımlılık olanları üretileceği Scala uygulama hello delete hello sahiptir. Biz burada oluşturma Merhaba uygulaması için kaldırdığınız dışındaki tüm sonuncu hello (**spark-akış-data-Kalıcılık-örnekleri derleme çıktı**). Merhaba Kavanoz toodelete seçin ve hello **silmek** simgesi (![Sil simgesi](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Apache Spark örnek - ayıklanan delete Kavanoz akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark örnek - ayıklanan delete Kavanoz akış")
      
       Emin olun **olun yapı** kutusu seçiliyse, o hello jar hello proje oluşturulmuş veya güncelleştirilmiş her zaman oluşturulan sağlar. **Uygula**'ya tıklayın.
   6. Merhaba, **çıkış düzeni** sekmesini sağ hello hello altındaki **kullanılabilir öğeleri** kutusu, önceki toohello proje kitaplık eklenebilir hello SQL JDBC jar sahip. Bu toohello eklemelisiniz **çıkış düzeni** sekmesi. Merhaba jar dosyasını sağ tıklatın ve ardından **ayıklamak halinde çıkış kök**.
      
       ![Apache Spark örnek - extract bağımlılık jar akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark örnek - extract bağımlılık jar akış")  
      
       Merhaba **çıkış düzeni** sekmesini şimdi şöyle görünmelidir.
      
       ![Apache Spark örnek - son çıktı sekmesi akış](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark akış örnek - son çıktı sekmesi")        
      
       Merhaba, **proje yapısını** iletişim kutusu, tıklatın **Uygula** ve ardından **Tamam**.    
   7. Merhaba menü çubuğundaki **yapı**ve ardından **olun proje**. Tıklatarak **derleme yapıları** toocreate hello jar. Merhaba çıkış jar altında oluşturulan **\classes\artifacts**.
      
       ![Apache Spark akış örnek - çıktı JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark akış örnek - çıktı JAR")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Merhaba uygulaması Livy kullanarak Spark kümesinde uzaktan çalıştırın

Bu makalede, Livy toorun Merhaba Apache Spark akış uygulaması uzaktan Spark kümesinde kullanın. Nasıl toouse Livy Hdınsight Spark ile küme hakkında ayrıntılı bilgi için bkz: [gönderme işleri uzaktan tooan Apache Spark küme Azure Hdınsight'ta](hdinsight-apache-spark-livy-rest-interface.md). Merhaba Spark akış uygulaması çalıştıran başlamadan önce şunları yapmalısınız vardır:

1. Merhaba yerel tek başına uygulama toogenerate olayları başlatmak ve tooEvent Hub gönderilir. Komut toodo şekilde aşağıdaki hello kullan:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Kopya hello jar akış (**spark akış-data-Kalıcılık-examples.jar**) toohello hello kümesi ile ilişkili Azure Blob Depolama. Bu hello jar erişilebilir tooLivy hale getirir. Kullanabileceğiniz [ **AzCopy**](../storage/common/storage-use-azcopy.md), bir komut satırı yardımcı programı, toodo şekilde. Var olan çok diğer istemcileri tooupload verileri kullanabilirsiniz. Onları hakkında daha fazla bilgiyi [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).
3. CURL Bu uygulamalardan çalıştırdığınız hello bilgisayara yükleyin. Livy uç noktaları toorun hello uzaktan işleri CURL tooinvoke hello kullanırız.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Merhaba Spark akış uygulama tooreceive hello olayları bir Azure depolama blob'a metin olarak çalıştırın.

Bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) hello çalıştırın:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Merhaba hello dosyasındaki parametreleri **inputBlob.txt** şu şekilde tanımlanır:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Bize hello giriş dosyası hello parametrelerinde neler olduğunu anlama:

* **Dosya** hello yolu toohello uygulama jar hello kümesi ile ilişkili hello Azure depolama hesabı üzerinde bir dosyadır.
* **className** hello jar hello sınıfında hello adıdır.
* **bağımsız değişken** hello hello sınıfı tarafından gerekli bağımsız değişkenleri listesi
* **numExecutors** uygulama yayınlamayı Spark toorun hello tarafından kullanılan çekirdek hello sayısıdır. Bu, her zaman en az iki kez hello olay hub'ı bölüm sayısı olmalıdır.
* **executorMemory**, **executorCores**, **driverMemory** kullanılan parametreler gerekli tooassign kaynaklardır toohello akış uygulama.

> [!NOTE]
> Parametre olarak kullanılan toocreate hello Çıkış klasörleri (EventCheckpoint, EventCount/EventCount10) gerekli değildir. Uygulama yayınlamayı hello bunları sizin için oluşturur.
>
>

Merhaba komutu çalıştırdığınızda, hello aşağıdaki gibi bir çıktı görmeniz gerekir:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Hello son satırında hello çıktı ('1'. Bu örnekte) hello toplu iş Kimliğini not edin. Uygulama hello tooverify çalıştırıyorsa başarıyla hello kümesi ile ilişkili Azure depolama hesabınızın bakabilir ve hello görmeniz gerekir **/EventCount/EventCount10** oluşturulan klasör. Bu klasör hello hello içinde belirtilen süre hello parametresi için işlenen olay sayısı yakalar BLOB'ları içermelidir **saniye içinde toplu iş aralığı**.

Bunu KILL kadar Merhaba Spark akış uygulaması toorun devam eder. toodo, bu nedenle, komutu aşağıdaki hello kullanın:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Merhaba uygulamaları tooreceive hello olayları bir Azure depolama blob'a JSON olarak çalıştırın
Bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) hello çalıştırın:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Merhaba hello dosyasındaki parametreleri **inputJSON.txt** şu şekilde tanımlanır:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Merhaba, hello önceki adımda hello metin çıktısı için belirtilen benzer toowhat parametreleridir. Yeniden, parametre olarak kullanılan toocreate hello Çıkış klasörleri (EventCheckpoint, EventCount/EventCount10) gerekmez. Uygulama yayınlamayı hello bunları sizin için oluşturur.

 Sonra hello komutunu çalıştırın, hello kümesi ile ilişkili Azure depolama hesabınızın bakabilir ve hello görmelisiniz **/EventStore10** oluşturulan klasör. Açık herhangi bir dosyayı önekine sahip **bölümü -** ve bir JSON biçiminde işlenen hello olayların görmeniz gerekir.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Merhaba uygulamaları tooreceive hello olayları Hive tabloya çalıştırın.
toorun hello Spark akış uygulaması bir Hive akışları olayları, tablo bazı ek bileşenleri gerekir. Bunlar:

* API jdo 3.2.6.jar datanucleus
* datanucleus rdbms 3.2.9.jar
* datanucleus çekirdek 3.2.10.jar
* Hive-site.xml

Merhaba **.jar** konumunda Hdınsight Spark kümenize dosyaları kullanılabilir `/usr/hdp/current/spark-client/lib`. Merhaba **hive-site.xml** şu adresten edinilebilir `/usr/hdp/current/spark-client/conf`.

Kullanabileceğiniz [WinScp](http://winscp.net/eng/download.php) toocopy hello küme tooyour yerel bilgisayardan bu dosyalar üzerinde. Daha sonra bu dosyalar tooyour depolama hesabı hello kümesi ile ilişkili araçları toocopy kullanabilirsiniz. Nasıl tooupload toohello depolama hesabı dosyaları ile ilgili daha fazla bilgi için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).

Merhaba dosyaları tooyour Azure depolama hesabı üzerinde kopyalandıktan sonra bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve aşağıdaki komutu (kullanıcı adı/parola ve küme adı değiştir) hello çalıştırın:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Merhaba hello dosyasındaki parametreleri **inputHive.txt** şu şekilde tanımlanır:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Merhaba, önceki adımlarda hello hello metin çıktısı için belirtilen benzer toowhat parametreleridir. Yeniden toocreate hello çıkış gerekmez klasörleri (EventCheckpoint, EventCount/EventCount10) veya hello çıktı parametreleri olarak kullanılan Hive tablosu (EventHiveTable10). Uygulama yayınlamayı hello bunları sizin için oluşturur. Bu hello Not **Kavanoz** ve **dosyaları** yolları toohello .jar dosyaları ve toohello depolama hesabı üzerinde kopyaladığınız hello hive-site.xml seçeneği içerir.

hive tablosu hello tooverify başarıyla oluşturuldu, SSH hello küme ve çalışma Hive sorguları halinde kullanabilirsiniz. Yönergeler için bkz: [SSH ile hdınsight'ta Hadoop ile Hive kullanma](hdinsight-hadoop-use-hive-ssh.md). SSH kullanarak bağlandıktan sonra o hello Hive tablosu komutu tooverify aşağıdaki hello çalıştırabilirsiniz **EventHiveTable10**, oluşturulur.

    show tables;

Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:

    OK
    eventhivetable10
    hivesampletable

SEÇME sorgusu hello tablosunun tooview Merhaba içeriğine de çalıştırabilirsiniz.

    SELECT * FROM eventhivetable10 LIMIT 10;

Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Merhaba uygulamaları tooreceive hello olayları bir Azure SQL veritabanı tablosuna çalıştırın.
Bu adımı çalıştırmadan önce oluşturulan bir Azure SQL veritabanı olduğundan emin olun. Yönergeler için bkz: [dakika içinde bir SQL veritabanı oluşturma](../sql-database/sql-database-get-started.md). toocomplete Bu bölüm, veritabanı adı, veritabanı sunucusu adı ve parametre olarak hello veritabanı yöneticisi kimlik bilgileri değerlerine ihtiyacı vardır. Toocreate hello veritabanı tablosu ancak gerekmez. Merhaba Spark akış uygulamanın, sizin için oluşturur.

Bir komut istemi açın, CURL yüklendiği toohello dizinine gidin ve hello aşağıdaki komutu çalıştırın:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Merhaba hello dosyasındaki parametreleri **inputSQL.txt** şu şekilde tanımlanır:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Uygulama hello tooverify başarıyla çalışır, toohello Azure SQL veritabanını SQL Server Management Studio'yu kullanarak bağlanabilir. Yönergeler için bkz: toodo [tooSQL veritabanı SQL Server Management Studio ile bağlanma](../sql-database/sql-database-connect-query-ssms.md). Bağlı toohello veritabanı olduktan sonra toohello gidebilirsiniz **EventContent** uygulama yayınlamayı hello tarafından oluşturulan tablo. Hızlı sorgu tooget hello veri hello tablosundan çalıştırabilirsiniz. Sorgu aşağıdaki hello çalıştırın:

    SELECT * FROM EventCount

Çıktı benzer toohello aşağıdaki görmeniz gerekir:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)
* [Alıcı tabanlı bağlantı ve doğrudan DStream tasarımı](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Uygulamaları oluşturma ve çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
