---
title: "Apache Storm ve HBase ile algılayıcı verilerini aaaAnalyze | Microsoft Docs"
description: "Bilgi nasıl tooconnect tooApache Storm ile bir sanal ağ. İle D3.js görselleştirmek ve Storm HBase tooprocess algılayıcı verilerle bir olay hub'ı kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Apache Storm, olay hub'ı ve (Hadoop) hdınsight'ta HBase ile algılayıcı verilerini çözümleme

Bilgi toouse Azure olay hub'ı Hdınsight tooprocess algılayıcı verileri üzerinde Apache Storm nasıl. Merhaba veri sonra Hdınsight üzerinde Apache HBase içine depolanır ve D3.js kullanarak görselleştirilen.

Bu belgede kullanılan hello Azure Resource Manager şablonu gösteren nasıl toocreate bir kaynak grubunda birden çok Azure kaynağı. Merhaba şablon bir Azure sanal ağı, iki Hdınsight kümesi (Storm ve HBase) ve Azure Web uygulaması oluşturur. Gerçek zamanlı web Panosu bir node.js uygulaması otomatik olarak dağıtılan toohello web uygulamasıdır.

> [!NOTE]
> Bu belge ve bu belgedeki örnek Hello bilgileri, Hdınsight sürüm 3.6 gerektirir.
>
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Ön koşullar

* Azure aboneliği.
* [Node.js](http://nodejs.org/): geliştirme ortamınızı yerel olarak kullanılan toopreview hello web Panosu.
* [Java ve hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): toodevelop hello Storm topolojisini kullanılır.
* [Maven](http://maven.apache.org/what-is-maven.html): kullanılan toobuild ve derleme hello projesi.
* [Git](http://git-scm.com/): kullanılan toodownload Merhaba projeyi github'dan.
* Bir **SSH** istemci: tooconnect toohello Linux tabanlı Hdınsight kümeleri kullanılır. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Mevcut bir Hdınsight kümesine gerek yoktur. Bu belgedeki Hello adımlar kaynakları aşağıdaki hello oluşturun:
> 
> * Bir Azure sanal ağı
> * Hdınsight kümesinde bir Storm (Linux tabanlı iki alt düğümleri)
> * Hdınsight kümesinde bir HBase (Linux tabanlı iki alt düğümleri)
> * Merhaba web Pano barındıran bir Azure Web uygulaması

## <a name="architecture"></a>Mimari

![mimarisi diyagramı](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

Bu örnek bileşenleri aşağıdaki Merhaba oluşur:

* **Azure Event Hubs**: algılayıcı toplanan verileri içerir.
* **Hdınsight üzerinde Storm**: olay Hub'ından veri gerçek zamanlı işlenmesini sağlar.
* **Hdınsight'ta HBase**: Storm tarafından işlendikten sonra kalıcı NoSQL veri deposu için veri sağlar.
* **Azure sanal ağ hizmeti**: Hdınsight kümelerinde hello Hdınsight üzerinde Storm ve HBase arasında güvenli iletişim sağlar.
  
  > [!NOTE]
  > Bir sanal ağ hello Java HBase istemci API kullanılırken gereklidir. Merhaba HBase kümeleri için ortak ağ geçidi üzerinden açık değil. Yükleme HBase ve Storm kümeleri aynı sanal ağ sağlar hello içine hello Storm kümesi (veya başka bir sistem hello sanal ağ üzerinde) toodirectly istemci API kullanarak HBase erişim.

* **Pano Web sitesi**: Gerçek zamanlı veri grafikleri bir örnek Pano.
  
  * Merhaba Web sitesi Node.js içinde uygulanmıştır.
  * [Socket.IO](http://socket.io/) hello Storm topolojisini hello Web sitesi arasındaki gerçek zamanlı iletişim için kullanılır.
    
    > [!NOTE]
    > Socket.IO iletişim için bir uygulama ayrıntılarını kullanmaktır. Ham WebSockets veya SignalR gibi tüm iletişimler çerçevesi kullanabilirsiniz.

  * [D3.js](http://d3js.org/) toohello Web gönderilen kullanılan toograph hello veriler.

> [!IMPORTANT]
> Hiçbir desteklenen yöntem toocreate bir Hdınsight kümesi için Storm ve HBase olarak iki küme gereklidir.

Merhaba topoloji verileri olay Hub'ından hello kullanarak okur [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) sınıfı ve hello kullanarak HBase yazma verisine [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) sınıf. Merhaba Web sitesiyle iletişim kullanarak gerçekleştirilir [Socket.IO client.java](https://github.com/nkzawa/socket.io-client.java).

Diyagram aşağıdaki hello hello topoloji hello düzenini açıklanmaktadır:

![Topoloji diyagramı](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Bu diyagramda, hello topoloji Basitleştirilmiş görünümüdür. Her bileşen örneği, olay hub'ınızdaki her bir bölümü için oluşturulur. Bu örnekler hello kümedeki hello düğümler arasında dağıtılır ve veri aralarında gibi yönlendirilir:
> 
> * Merhaba spout toohello ayrıştırıcı yükü dengelenmiş verilerdir.
> * Merhaba ayrıştırıcı toohello Pano ve HBase verilerini cihaz Kimliğine göre gruplandırılmış, böylece her zaman aynı aygıt iletilerden hello toohello akış aynı bileşeni.

### <a name="topology-components"></a>Topoloji bileşenleri

* **Event Hubs Spout**: Merhaba spout 0.10.0 Apache Storm sürümünün parçası olarak sağlanan ve daha yüksek.
  
  > [!NOTE]
  > Bu örnekte kullanılan hello olay hub'ı spout Hdınsight kümesi sürüm 3.5 veya 3.6 Storm gerektirir.

* **ParserBolt.java**: Merhaba spout'un yayılan hello verilerinin ham JSON ve bazen birden fazla olay aynı anda gösterilen. Bu Cıvata tarafından hello yayılan hello veriler spout ve hello JSON ileti ayrıştırır okur. Merhaba Cıvata sonra birden çok alan içeren bir tanımlama grubu hello veri yayar.
* **DashboardBolt.java**: Bu bileşen nasıl toouse hello Java toosend verileri gerçek zamanlı toohello web Pano için Socket.IO istemci kitaplığı gösterir.
* **Hayır-hbase.yaml**: Merhaba yerel modda çalışırken kullanılan topoloji tanımı. HBase bileşenleri kullanmaz.
* **hbase.yaml ile**: Merhaba hello topoloji Merhaba kümede çalışırken kullanılan topoloji tanımı. HBase bileşenlerini kullanın.
* **dev.Properties**: Merhaba hello olay hub'ı spout, HBase Cıvata ve Panosu bileşenleri için yapılandırma bilgilerini.

## <a name="prepare-your-environment"></a>Ortamınızı hazırlama

Bu örneğini kullanmadan önce hangi hello Storm topolojisinin okur bir Azure Event Hub oluşturmanız gerekir.

### <a name="configure-event-hub"></a>Olay hub'ı yapılandırma

Olay hub'ı hello veri bu örneğin kaynağıdır. Aşağıdaki adımları toocreate bir Event Hub'hello kullanın.

1. Merhaba gelen [Azure portal](https://portal.azure.com)seçin **+ yeni** -> **nesnelerin interneti** -> **olay hub'ları**.
2. Merhaba, **oluşturma Namespace** bölümünde, hello aşağıdaki görevleri gerçekleştirin:
   
   1. Girin bir **adı** hello ad alanı için.
   2. Fiyatlandırma katmanını seçin. **Temel** Bu örnek için yeterlidir.
   3. Select hello Azure **abonelik** toouse.
   4. Varolan bir kaynak grubu seçin veya yeni bir tane oluşturun.
   5. Select hello **konumu** hello olay hub'ı için.
   6. Seçin **PIN toodashboard**ve ardından **oluşturma**.

3. Merhaba oluşturma işlemi tamamlandığında hello ad alanınız için olay hub'ları bilgileri görüntülenir. Buradan, seçin **+ olay hub'ı eklemek**. Merhaba, **Event Hub'ı oluşturma** bölümünde, bir ad girin **sensordata**ve ardından **oluşturma**. Merhaba diğer alanları hello varsayılan değerleri bırakın.
4. Merhaba olay hub'larından görüntülemek, ad alanı için select **olay hub'ları**. Select hello **sensordata** girişi.
5. Merhaba sensordata Event Hub ' seçin **paylaşılan erişim ilkeleri**. Kullanım hello **+ Ekle** ilkelere bağlantı tooadd hello:

    | İlke adı | Talepleri |
    | ----- | ----- |
    | cihazlar | Gönder |
    | Storm | Dinleme |

1. Her iki ilkeyi seçin ve hello Not **birincil anahtar** değeri. Sonraki adımlarda hem ilkeleri için hello değer gerekir.

## <a name="download-and-configure-hello-project"></a>İndirme ve başlangıç projesi yapılandırma

Toodownload Merhaba projeyi Github'dan aşağıdaki hello kullanın.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Merhaba komutu tamamlandıktan sonra aşağıdaki dizin yapısını hello vardır:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Bu belgede, bu örnekteki hello kodunun toofull ayrıntılarını geçmez. Ancak, hello kodu tam olarak geçersiz kılınan.

Olay Hub'ı Aç hello gelen tooconfigure hello proje tooread `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` dosya ve izleyerek, olay hub'ı bilgi toohello ekleyin:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Derleme ve yerel olarak test etme

> [!IMPORTANT]
> Merhaba topolojisi kullanarak yerel olarak çalışan bir Storm geliştirme ortamını gerektirir. Daha fazla bilgi için bkz: [bir Storm geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) Apache.org.

> [!WARNING]
> Bir Windows geliştirme ortamını kullanıyorsanız, alabileceğiniz bir `java.io.IOException` çalışırken hello topoloji yerel olarak. Bu durumda, Hdınsight toorunning hello topolojisini taşıyın.

Test etmeden önce hello Pano tooview hello çıktı hello topolojisinin başlatmalı ve Event Hub'ında veri toostore oluşturur.

> [!IMPORTANT]
> Bu topoloji Hello HBase bileşeni, yerel olarak test edilirken etkin değil. Merhaba Java API hello HBase kümesi için dış hello hello kümeleri içeren Azure Virtual Network erişilemiyor.

### <a name="start-hello-web-application"></a>Merhaba web uygulamasını Başlat

1. Bir komut istemi açın ve dizinleri çok`hdinsight-eventhub-example/dashboard`. Merhaba web uygulama tarafından gerek duyulan komutu tooinstall hello bağımlılıklar aşağıdaki hello kullan:
   
    ```bash
    npm install
    ```

2. Komut toostart hello web uygulama aşağıdaki hello kullan:
   
    ```bash
    node server.js
    ```
   
    Metin aşağıdaki ileti benzer toohello bakın:
   
        Server listening at port 3000

3. Bir web tarayıcısı açın ve girin `http://localhost:3000/` hello adresi olarak. Aşağıdaki görüntü bir sayfa benzer toohello görüntülenir:
   
    ![Web Panosu](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Bu komut istemini açık bırakın. Test sonra Ctrl-C toostop hello web sunucusu kullanın.

### <a name="generate-data"></a>Veri oluştur

> [!NOTE]
> herhangi bir platformda kullanılabilir hello bu bölümdeki adımları Node.js kullanın. Merhaba diğer dil örnekler için bkz: `SendEvents` dizin.

1. Yeni istemi, kabuk veya terminal açın ve dizinleri çok değiştirin`hdinsight-eventhub-example/SendEvents/nodejs`. Merhaba uygulama tarafından gerek duyulan tooinstall hello bağımlılıkları hello aşağıdaki komutu kullanın:

    ```bash
    npm install
    ```

2. Açık hello `app.js` dosyasını bir metin düzenleyicisinde ve hello daha önce aldığınız olay hub'ı bilgileri ekleyin:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > Bu örnekte, kullandığınız varsayılır `sensordata` olay Hub'ınızı hello adından farklı. Ve `devices` sahip hello İlkesi hello adından farklı bir `Send` talep.

3. Komut tooinsert yeni girişler Event Hub'ındaki aşağıdaki hello kullan:
   
    ```bash
    node app.js
    ```
   
    Merhaba veri içeren birkaç satırlık çıktı tooEvent Hub gönderilen bakın:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Oluşturun ve hello topoloji başlatın

1. Yeni bir komut istemi açın ve dizinleri çok`hdinsight-eventhub-example/TemperatureMonitor`. toobuild ve paket topoloji Merhaba, hello aşağıdaki komutu kullanın: 

    ```bash
    mvn clean package
    ```

2. toostart yerel mod topolojisinde Merhaba, hello aşağıdaki komutu kullanın:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`Merhaba topoloji yerel modunda başlatır.
    * `--filter`kullandığı hello `dev.properties` hello topoloji tanımı'nda dosya toopopulate parametreleri.
    * `resources/no-hbase.yaml`kullandığı hello `no-hbase.yaml` topoloji tanımı.
 
   Başladıktan sonra hello topoloji girişleri olay Hub'ından okur ve onları yerel makine üzerinde çalışan toohello Pano gönderir. Merhaba web Pano görüntü aşağıdaki benzer toohello görünen satırlarını görmeniz gerekir:
   
    ![verilerle Panosu](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Merhaba Pano çalışırken hello kullan `node app.js` hello önceki komuttan adımları toosend yeni veri tooEvent hub. Merhaba sıcaklık değerleri rastgele oluşturulur çünkü hello grafik sıcaklık tooshow büyük değişiklikleri güncelleştirmeniz gerekir.
   
   > [!NOTE]
   > Hello olmalıdır **hdınsight-eventhub-örnek/SendEvents/Nodejs** hello kullanırken dizin `node app.js` komutu.

3. Bu hello Pano güncelleştirmeleri, Ctrl + C kullanarak Dur hello topolojisi doğruladıktan sonra. Ctrl + C toostop hello yerel web sunucusu de kullanabilirsiniz.

## <a name="create-a-storm-and-hbase-cluster"></a>Bir Storm ve HBase kümesi oluşturma

Merhaba adımları bölümüne kullanması durumunda bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) toocreate hello sanal ağda bir Azure sanal ağı ve bir Storm ve HBase kümesi. Hello şablonu ayrıca bir Azure Web uygulaması oluşturur ve hello panonun bir kopyasını uygulamasına dağıtır.

> [!NOTE]
> Bir sanal ağ Hello Storm kümesi üzerinde çalışan hello topoloji hello HBase Java API kullanarak hello HBase kümesi ile doğrudan iletişim kurabilmesi için kullanılır.

Bu belgede kullanılan hello Resource Manager şablonu ortak blob kapsayıcısında bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Düğme toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure portal'ın aşağıdaki hello'ı tıklatın.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Merhaba gelen **özel dağıtım** bölümünde, aşağıdaki değerleri hello girin:
   
    ![Hdınsight parametreleri](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Temel küme adı**: Bu değer hello Storm ve HBase kümeleri için hello temel adı olarak kullanılır. Örneğin, **abc** adlı bir Storm kümesi oluşturur **storm abc** ve adlı bir HBase kümesi **hbase abc**.
   * **Oturum açma kullanıcı adı küme**: hello Storm ve HBase kümeleri için hello yönetici kullanıcı adı.
   * **Oturum açma parolası küme**: hello Storm ve HBase kümeleri için hello yönetici kullanıcı parolası.
   * **SSH kullanıcı adı**: hello Storm ve HBase kümeleri için SSH kullanıcı toocreate hello.
   * **SSH parolası**: hello SSH kullanıcı hello Storm ve HBase kümeleri için başlangıç parolası.
   * **Konum**: hello kümeleri oluşturulan hello bölgesi.
     
     Tıklatın **Tamam** toosave hello parametreleri.

3. Kullanım hello **Temelleri** bölümünde toocreate bir kaynak grubu veya varolan bir tanesini seçin.
4. Merhaba, **kaynak grubu konumu** açılır menüsünde, select hello aynı konuma Merhaba seçtiğinizde **konumu** hello parametresinde **ayarları** bölümü.
5. Merhaba hüküm ve koşulları okuyun ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.
6. Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**. Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.

Merhaba kaynakları oluşturduktan sonra hello kaynak grubu hakkında bilgi görüntülenir.

![Merhaba vnet ve kümeler için kaynak grubu](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **storm BASENAME** ve **hbase BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu. Bu adları toohello kümeleri bağlanırken bir sonraki adımda kullanın. Aynı zamanda hello Pano sitenin adını hello Not olan **basename Pano**. Bu değer, bu belgenin sonraki bölümlerinde kullanılır.

## <a name="configure-hello-dashboard-bolt"></a>Merhaba Pano Cıvata yapılandırın

toosend veri toohello Pano, bir web uygulaması dağıtılan hello satırında aşağıdaki hello değiştirmelisiniz `dev.properties`dosyası:

```yaml
dashboard.uri: http://localhost:3000
```

Değişiklik `http://localhost:3000` çok`http://BASENAME-dashboard.azurewebsites.net` ve hello dosyasını kaydedin. Değiştir **BASENAME** hello önceki adımda sağlanan hello temel ada sahip. Daha önce tooselect hello panoyu ve görünüm hello URL oluşturulan hello kaynak grubuna de kullanabilirsiniz.

## <a name="create-hello-hbase-table"></a>Merhaba HBase tablosu oluşturma

HBase toostore verileri, biz öncelikle bir tablo oluşturmanız gerekir. Storm toowrite için gereken kaynakları önceden oluşturmak, bir Storm topolojisinin içinde çalışırken toocreate kaynaklardan çalışırken birden çok örneğinde neden olabileceğinden toocreate hello aynı kaynak. Merhaba topoloji dışındaki Hello kaynaklar oluşturun ve okuma/yazma ve analizi için Storm kullanın.

1. Merhaba SSH kullanıcı ve küme oluşturma sırasında toohello şablonu sağlanan parola kullanarak SSH tooconnect toohello HBase kümesi kullanın. Örneğin, hello kullanarak bağlanma `ssh` komutunu kullanma sözdizimi aşağıdaki hello:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Değiştir `sshuser` hello SSH kullanıcı adı ile Merhaba küme oluştururken verdiğiniz. Değiştir `clustername` hello HBase kümesi ada sahip.

2. Merhaba SSH oturumundan hello HBase Kabuğu'nu başlatın.
   
    ```bash
    hbase shell
    ```
   
    Merhaba Kabuk yüklendikten sonra gördüğünüz bir `hbase(main):001:0>` istemi.

3. Hello ifadesini HBase Kabuğu komut toocreate bir tablo toostore hello algılayıcı verilerini aşağıdaki hello girin:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Hello tablosunun komutu aşağıdaki hello kullanılarak oluşturulup oluşturulmadığını doğrulayın:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Aşağıdaki örnek, hello tabloda 0 satır olduğunu belirten bilgi benzer toohello döndürür.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Girin `exit` tooexit hello HBase Kabuğu:

## <a name="configure-hello-hbase-bolt"></a>Merhaba HBase Cıvata yapılandırın

toowrite tooHBase hello Storm kümeden hello yapılandırma ayrıntılarını, HBase kümesi ile Merhaba HBase Cıvata sağlamanız gerekir.

1. Örnekler tooretrieve hello Zookeeper çekirdek HBase kümesi için aşağıdaki hello birini kullanın:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Değiştir `your_HDInsight_cluster_name` Hdınsight kümenize hello adı. Merhaba yükleme hakkında daha fazla bilgi için `jq` yardımcı programı, bkz: [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > İstendiğinde, hello Hdınsight yönetici oturum açma hello parolayı girin.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Değiştir ' your_HDInsight_cluster_name Hdınsight kümenize hello adı. İstendiğinde, hello Hdınsight yönetici oturum açma hello parolayı girin.
    >
    > Bu örnek, Azure PowerShell gerektirir. Azure PowerShell kullanma hakkında daha fazla bilgi için bkz: [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    Bu örnekler tarafından döndürülen hello bilgi metnini izleyen benzer toohello şöyledir:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Bu bilgiler, Storm toocommunicate ile Merhaba HBase kümesi tarafından kullanılır.

2. Merhaba değiştirme `dev.properties` dosya ve hello Zookeeper çekirdek bilgi toohello aşağıdaki satırı ekleyin:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>, Paketi, derleme ve hello çözüm tooHDInsight dağıtma

Geliştirme ortamınızı adımları toodeploy hello Storm topolojisini toohello storm kümesi aşağıdaki hello kullanın.

1. Merhaba gelen `TemperatureMonitor` dizin kullanım hello aşağıdakiler komut tooperform yeni bir yapı ve projenizden JAR paketi oluşturun:
   
        mvn clean package
   
    Bu komut adlı bir dosya oluşturur `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `hedef ' projenizin dizin.

2. Kullanım scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` ve `dev.properties` dosyaları tooyour Storm kümesi. Örneğin, aşağıdaki Hello yerine `sshuser` hello küme oluştururken verdiğiniz hello SSH kullanıcı ile ve `clustername` Storm kümenizin hello ada sahip. İstendiğinde, hello SSH kullanıcı için hello parola girin.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Tooupload hello dosyaları bu işlem birkaç dakika sürebilir.

    Merhaba kullanma hakkında daha fazla bilgi için `scp` ve `ssh` komutları, Hdınsight ile bkz [Hdınsight ile SSH kullanma](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Hello dosya karşıya yüklendikten sonra SSH kullanarak toohello Storm kümesine bağlanın.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Değiştir `sshuser` hello SSH kullanıcı adı. Değiştir `clustername` hello Storm kümesi ada sahip.

4. toostart topoloji Merhaba, hello SSH oturumundan komutu aşağıdaki hello kullanın:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`Merhaba topoloji toohello toohello supervisor hello küme düğümünde IT Nimbus hizmet gönderir.
    * `--filter`kullandığı hello `dev.properties` hello topoloji tanımı'nda dosya toopopulate parametreleri.
    * `-R /with-hbase.yaml`kullandığı hello `with-hbase.yaml` hello paketindeki topolojisi.

5. Merhaba topoloji başlatıldıktan sonra sonra kullanım hello Azure üzerinde yayımlanan bir tarayıcı toohello Web sitesini açın `node app.js` komutu toosend veri tooEvent Hub. Merhaba web Pano güncelleştirme toodisplay hello bilgileri görmeniz gerekir.
   
    ![pano](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>HBase verileri görüntüleme

Aşağıdaki adımları tooconnect tooHBase hello kullanın ve hello veri toohello tablo yazılmış emin olun:

1. SSH tooconnect toohello HBase kümesi kullanın.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Değiştir `sshuser` hello SSH kullanıcı adı. Değiştir `clustername` hello HBase kümesi ada sahip.

2. Merhaba SSH oturumundan hello HBase Kabuğu'nu başlatın.
   
    ```bash
    hbase shell
    ```
   
    Merhaba Kabuk yüklendikten sonra gördüğünüz bir `hbase(main):001:0>` istemi.

3. Merhaba tablodan satırları görüntüleyin:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Bu komut metnini izleyen, hello tabloda veri olduğunu belirten bilgi benzer toohello döndürür.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Bu tarama işlemi hello tablodan en fazla 10 satır döndürür.

## <a name="delete-your-clusters"></a>Kümelerinizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

aynı anda toodelete hello kümeleri, depolama ve web uygulaması bunları içeren hello kaynak grubunu silin.

## <a name="next-steps"></a>Sonraki adımlar

Storm topolojileri Hdınsight ile daha fazla örnekleri için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)

Apache Storm hakkında daha fazla bilgi için bkz: Merhaba [Apache Storm](https://storm.incubator.apache.org/) site.

Hdınsight'ta HBase hakkında daha fazla bilgi için bkz: Merhaba [Hdınsight genel bakış ile HBase](hdinsight-hbase-overview.md).

Merhaba Socket.IO hakkında daha fazla bilgi için bkz: [Socket.IO](http://socket.io/) site.

D3.js hakkında daha fazla bilgi için bkz: [D3.js - veri güdümlü belgeleri](http://d3js.org/).

Java topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Apache Storm için geliştirme Java topolojileri](hdinsight-storm-develop-java-topology.md).

.NET topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
