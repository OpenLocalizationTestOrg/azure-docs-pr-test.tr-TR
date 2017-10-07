---
title: "aaaDeploy ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme | Microsoft Docs"
description: "Nasıl toodeploy, izlemek ve hello Storm panosunu kullanarak Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetmek öğrenin. Visual Studio Hadoop araçlarını kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetme

Bu belgede, yönetme ve izleme üzerinde Storm Hdınsight kümelerinde çalışan Storm topolojilerini hello temellerini öğrenin.

> [!IMPORTANT]
> Merhaba bu makaledeki adımlarda Hdınsight kümesinde Linux tabanlı Storm gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). 
>
> Dağıtma ve Windows tabanlı Hdınsight üzerinde topolojileri izleme hakkında daha fazla bilgi için bkz: [dağıtma ve Windows tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Ön koşullar

* **Hdınsight kümesinde Linux tabanlı Storm**: bkz [Hdınsight üzerinde Apache Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md) küme oluşturma adımları

* (İsteğe bağlı) **SSH ve SCP**: daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

* (İsteğe bağlı) **Visual Studio**: Azure SDK'sı 2.5.1 ya da daha yeni ve Visual Studio için Data Lake araçları hello. Daha fazla bilgi için bkz: [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Visual Studio sürümleri aşağıdaki hello biri:

  * Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (herhangi bir sürümünü)

  * Visual Studio 2017 (herhangi bir sürümünü). Visual Studio 2017 için Data Lake araçları hello Azure iş yükü bir parçası olarak yüklenir.

## <a name="submit-a-topology-visual-studio"></a>Bir topoloji gönderin: Visual Studio

Merhaba Hdınsight araçları kullanılan toosubmit C# veya karma topolojiler tooyour Storm kümesi olabilir. Aşağıdaki adımları hello örnek bir uygulama kullanın. Merhaba Hdınsight araçları kullanarak kendi topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio için Hdınsight araçları hello kullanarak C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Visual Studio için hello Data Lake Araçları'nın en son sürümünü hello yüklemediyseniz, bkz: [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Visual Studio için Data Lake araçları Hello adıysa hello Hdınsight araçları Visual Studio için.
    >
    > Visual Studio için Data Lake araçları hello dahil __Azure iş yükü__ Visual Studio 2017 için.

2. Visual Studio'ni açın, **dosya** > **yeni** > **proje**.

3. Merhaba, **yeni proje** iletişim kutusunda, genişletin **yüklü** > **şablonları**ve ardından **Hdınsight**. Merhaba şablonları listesinden **Storm örnek**. Merhaba iletişim kutusunun Hello altında hello uygulama için bir ad yazın.

    ![Görüntü](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **hdınsight'ta tooStorm gönderme**.

   > [!NOTE]
   > İstenirse, Azure aboneliğinizin hello oturum açma kimlik bilgilerini girin. Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açın.

5. Hdınsight kümesi üzerinde Storm'a hello seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**. Hello kullanarak Hello gönderme başarılı olup olmadığını izleyebilirsiniz **çıkış** penceresi.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Bir topoloji gönderin: SSH ve hello komutu Storm

1. SSH tooconnect toohello Hdınsight kümesi kullanın. Değiştir **kullanıcıadı** SSH oturumunuzla hello adı. Değiştir **CLUSTERNAME** Hdınsight küme adıyla:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    SSH tooconnect tooyour Hdınsight kullanma hakkında daha fazla bilgi için küme için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Aşağıdaki komut toostart örnek bir topoloji hello kullan:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Bu komut hello kümede hello örnek WordCount topolojisini başlatır. Bu topoloji rastgele oluşturmak cümleleri ve her sözcüğün sayısı hello oluşma hello cümlelerde.

   > [!NOTE]
   > Topoloji toohello küme gönderirken, ilk hello kullanmadan önce hello kümeyi içeren hello jar dosyasını kopyalamanız gerekir `storm` komutu. toocopy hello dosya toohello kümesi hello kullanabileceğiniz `scp` komutu. Örneğin, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > Merhaba WordCount örneği ve diğer storm starter örnekleri zaten eklenir konumunda kümenize `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Bir topoloji gönderin: program aracılığıyla

Hdınsight'ta bir topoloji tooStorm hello kümenizdeki barındırılan Nimbus hizmeti ile iletişim kurarak programlı olarak dağıtabilirsiniz. [https://github.com/Azure-Samples/hdinsight-Java-Deploy-Storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) gösteren bir Java uygulama örneğidir nasıl toodeploy ve hello Nimbus hizmeti aracılığıyla bir topoloji başlatın.

## <a name="monitor-and-manage-visual-studio"></a>İzleme ve yönetme: Visual Studio

Bir topoloji Visual Studio kullanarak başarıyla gönderildi, hello **Storm topolojilerini** hello küme görünür görüntüleyin. Merhaba topoloji hello listesi tooview topoloji çalıştıran hello bilgilerini seçin.

![Visual studio İzleyicisi](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> De görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini** genişleterek **Azure** > **Hdınsight**ve Hdınsight kümesinde bir Storm sağ tıklayıp seçerek **görünüm Storm topolojilerini**.

Merhaba spout'lar ya da bu bileşenler hakkında bilgi tooview Cıvatalar hello şekli seçin. Yeni bir pencere için seçilen her öğenin açar.

### <a name="deactivate-and-reactivate"></a>Devre dışı bırakın ve yeniden etkinleştirin

Sonlandırıldı veya yeniden kadar bir topoloji devre dışı bırakma, duraklatır. tooperform şu işlemleri kullanın hello __devre dışı bırak__ ve __yeniden__ hello hello üstündeki düğmeleri __topoloji özeti__.

### <a name="rebalance"></a>Yeniden dengelemeniz

Bir topoloji dengelenmesi hello sistem toorevise hello paralellik hello topolojisinin sağlar. Daha fazla Not hello küme tooadd yeniden boyutlandırılabilir, örneğin, yeniden dengelenmesi bir topoloji toosee hello yeni düğümler imkan tanır.

toorebalance bir topoloji kullanmak hello __yeniden dengelemeniz__ düğmesi hello hello üstündeki __topoloji özeti__.

> [!WARNING]
> Bir topoloji ilk dengelenmesi hello topoloji, devre dışı bırakır çalışanları hello küme arasında eşit olarak yeniden dağıtır, sonra son olarak yeniden dengelenmesi oluşmadan önce durumla hello topoloji toohello durum döndürür. Hello topolojisi etkin olduğunda, bu nedenle onu yeniden etkin hale gelir. Devre dışı bırakıldı, devre dışı kalır.

### <a name="kill-a-topology"></a>Bir topoloji Sonlandır

Storm topolojilerini durdurulmuş veya hello küme silinene kadar çalışmaya devam edin. toostop bir topoloji kullanmak hello __KILL__ düğmesi hello hello üstündeki __topoloji özeti__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>İzleme ve yönetme: SSH ve hello komutu Storm

Merhaba `storm` yardımcı programı topolojileri hello komut satırından çalıştırma ile toowork sağlar. Kullanım `storm -h` komutları tam listesi için.

### <a name="list-topologies"></a>Liste topolojileri

Komut toolist aşağıdaki hello tüm çalışan topolojileri kullanın:

    storm list

Bu komut, metin aşağıdaki bilgileri benzer toohello döndürür:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Devre dışı bırakın ve yeniden etkinleştirin

Sonlandırıldı veya yeniden kadar bir topoloji devre dışı bırakma, duraklatır. Komut toodeactivate aşağıdaki hello kullanın ve yeniden etkinleştirin:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Çalışan bir topoloji Sonlandır

Storm topolojileri, başlatıldığında, devam durdurulana kadar çalışıyor. toostop bir topoloji hello aşağıdaki komutu kullanın:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Yeniden dengelemeniz

Bir topoloji dengelenmesi hello sistem toorevise hello paralellik hello topolojisinin sağlar. Daha fazla Not hello küme tooadd yeniden boyutlandırılabilir, örneğin, yeniden dengelenmesi bir topoloji toosee hello yeni düğümler imkan tanır.

> [!WARNING]
> Bir topoloji ilk dengelenmesi hello topoloji, devre dışı bırakır çalışanları hello küme arasında eşit olarak yeniden dağıtır, sonra son olarak yeniden dengelenmesi oluşmadan önce durumla hello topoloji toohello durum döndürür. Hello topolojisi etkin olduğunda, bu nedenle onu yeniden etkin hale gelir. Devre dışı bırakıldı, devre dışı kalır.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>İzleme ve yönetme: Storm kullanıcı Arabirimi

Merhaba Storm kullanıcı Arabirimi çalışan topolojilerle çalışmaya yönelik bir web arabirimi sağlar ve Hdınsight kümenize dahil edilir. tooview hello Storm kullanıcı Arabirimi, bir web tarayıcısı tooopen kullanmak **https://CLUSTERNAME.azurehdinsight.net/stormui**, burada **CLUSTERNAME** hello kümenizin adıdır.

> [!NOTE]
> Hello Yöneticisi (Yönetici) ve ne zaman kullanılan parola tooprovide bir kullanıcı adı ve parola istenirse, girin oluşturma hello küme.

### <a name="main-page"></a>Ana sayfa

Merhaba Storm kullanıcı Arabirimi ana sayfasının Hello bilgisinden hello sağlar:

* **Küme Özet**: hello Storm kümesi hakkında temel bilgiler.
* **Topoloji özeti**: topolojileri çalışan bir listesi. Bu bölümde tooview Hello bağlantıları belirli topolojileri hakkında daha fazla bilgi kullanın.
* **Yönetici Özeti**: hello Storm İdarecisi hakkında bilgi.
* **Nimbus yapılandırma**: hello küme Nimbus yapılandırması.

### <a name="topology-summary"></a>Topoloji özeti

Merhaba bir bağlantı seçme **topoloji özeti** bölümü hello topolojisi hakkında bilgi aşağıdaki hello görüntüler:

* **Topoloji özeti**: hello topolojisi hakkında temel bilgiler.
* **Topoloji eylemleri**: hello topolojisi gerçekleştirebilen yönetim işlemleri.

  * **Etkinleştirme**: devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.
  * **Devre dışı**: çalışan topolojiyi duraklatır.
  * **Yeniden dengelemeniz**: hello hello topolojisinin paralelliğini ayarlar. Merhaba hello kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir. Bu işlem hello topoloji tooadjust paralellik toocompensate hello için artırılabilir veya hello kümedeki düğüm sayısını azaltılabilir sağlar.

    Daha fazla bilgi için bkz: <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">hello bir Storm topolojisinin paralelliğini anlama</a>.
  * **KILL**: hello belirtilen zaman aşımı sonra Storm topolojisini sonlandırır.
* **Topoloji istatistikleri**: hello topoloji hakkındaki istatistiklerdir. tooset girişleri hello sayfasında kalan hello ilişkin zaman çerçevesini Merhaba, hello hello bağlantıları kullanın **penceresi** sütun.
* **Spout'lar**: Merhaba spout'lar hello topolojisi tarafından kullanılır. Bu bölümde tooview Hello bağlantıları belirli spout'lar hakkında daha fazla bilgi kullanın.
* **Cıvatalar**: Merhaba Cıvatalar hello topolojisi tarafından kullanılır. Bu bölümde tooview Hello bağlantıları belirli Cıvatalar hakkında daha fazla bilgi kullanın.
* **Topoloji Yapılandırması**: Seçili hello topolojisinin hello yapılandırma.

### <a name="spout-and-bolt-summary"></a>Spout ve Cıvata özeti

Bir spout hello seçme **Spout'lar** veya **Cıvatalar** bölümleri hello seçili öğe hakkında bilgileri aşağıdaki hello görüntüler:

* **Bileşen özeti**: Merhaba spout veya Cıvata hakkında temel bilgiler.
* **Spout/Cıvata istatistikleri**: hello hakkındaki istatistiklerdir spout veya Cıvata. tooset girişleri hello sayfasında kalan hello ilişkin zaman çerçevesini Merhaba, hello hello bağlantıları kullanın **penceresi** sütun.
* **Giriş İstatistikleri** (yalnızca Cıvata): hello hakkında bilgi giriş hello Cıvata tarafından kullanılan akışı.
* **Çıkış istatistikleri**: spout veya Cıvata bu tarafından gösterilen hello akışları hakkında bilgi.
* **Yürütücüler**: hello örneklerini hello spout veya Cıvata hakkında bilgi. Select hello **bağlantı noktası** girişi belirli Yürütücü tooview için tanılama bilgileri günlüğünü üretilen Bu örneği için.
* **Hataları**: Bu hata bilgilerini spout veya Cıvata.

## <a name="monitor-and-manage-rest-api"></a>İzleme ve yönetme: REST API'si

benzer yönetim ve izleme işlevselliği hello REST API kullanarak gerçekleştirebilmek için hello Storm kullanıcı Arabirimi REST API hello üzerinde oluşturulmuştur. Merhaba REST API toocreate özel araçlar yönetmek ve Storm topolojilerini izlemek için kullanabilirsiniz.

Daha fazla bilgi için bkz: [Storm kullanıcı Arabirimi REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Merhaba aşağıdaki bilgiler belirli toousing hello Hdınsight üzerinde Apache Storm ile REST API sağlar.

> [!IMPORTANT]
> Merhaba Storm REST API genel kullanıma açık değil üzerinde Internet hello ve bir SSH tünel toohello Hdınsight küme baş düğümüne kullanarak erişilmesi gerekir. Oluşturma ve SSH tüneli kullanma hakkında daha fazla bilgi için bkz: [kullanım SSH tünel tooaccess Ambari web kullanıcı Arabirimi, ResourceManager, kaynak, iş, Oozie ve diğer web Uı'lar](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>Taban URI

Merhaba Linux tabanlı Hdınsight kümelerinde hello REST API için taban URI hello baş düğümü üzerinde kullanılabilir **API/https://HEADNODEFQDN:8744/v1/**. Merhaba etki alanı adı hello baş düğümü küme oluşturma sırasında oluşturulur ve statik değil.

Merhaba küme baş düğümüne hello tam etki alanı adı (FQDN) birkaç farklı şekilde bulabilirsiniz:

* **Bir SSH oturumundan**: hello komutunu `headnode -f` bir SSH oturumu toohello kümeden.
* **Ambari Web**: seçin **Hizmetleri** hello sayfa hello üstten seçip **Storm**. Merhaba gelen **Özet** sekmesine **Storm kullanıcı Arabirimi sunucu**. Merhaba hello Storm kullanıcı Arabirimi ve REST API çalışıyor hello düğümü FQDN'sini hello hello sayfanın başında ' dir.
* **Ambari REST API öğesinden**: hello komutunu `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` üzerinde çalışan Storm kullanıcı Arabirimi ve REST API hello hello düğüm hakkında tooretrieve bilgi. Değiştir **parola** hello küme hello yönetici parolası ile. Değiştir **CLUSTERNAME** hello küme adı ile. Merhaba yanıtta hello hello düğümü FQDN'sini hello "host_name" giriş içeriyor.

### <a name="authentication"></a>Kimlik Doğrulaması

REST API kullanmalıdır istekleri toohello **temel kimlik doğrulaması**, hello Hdınsight Küme Yönetici adı ve parola kullanın.

> [!NOTE]
> Temel kimlik doğrulaması düz metin kullanarak gönderildiğinden, aşağıdakileri yapmalısınız **her zaman** hello kümeyle HTTPS toosecure iletişimleri kullanın.

### <a name="return-values"></a>Dönüş değerleri

Hello REST API yalnızca hello küme içinde kullanılabilir olabilir veya sanal makinelerde hello küme aynı Azure sanal ağ hello döndürülen bilgi. Örneğin, Zookeeper sunucuları için döndürülen hello tam etki alanı adı (FQDN) olduğu değil Internet hello erişilebilir.

## <a name="next-steps"></a>Sonraki Adımlar

Storm panosunu kullanarak toodeploy ve İzleyici topolojileri nasıl hello öğrendiğinize göre nasıl çok öğrenin[Maven kullanarak geliştirme Java tabanlı topolojiler](hdinsight-storm-develop-java-topology.md).

Daha fazla örnek topolojileri listesi için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).
