---
title: "Apache Storm hdınsight'ta - Azure aaaStorm başlangıç örneklerine | Microsoft Docs"
description: "Bilgi nasıl toodo büyük veri analizi ve gerçek zamanlı verileri işlemek Apache Storm kullanarak Hdınsight üzerinde storm-starter örnekleri hello."
keywords: "Storm-starter, Apache Storm örneği"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Merhaba storm starter örneklerini kullanarak Hdınsight üzerinde Apache Storm kullanmaya başlama

Nasıl kullanarak Hdınsight'ta Apache Storm toouse hello storm-starter örnekleri hakkında bilgi edinin.

Apache Storm, veri akışlarını işlemeye yönelik ölçeklenebilir, hataya dayanıklı, dağıtılmış ve gerçek zamanlı bir işlem sistemidir. Azure HDInsight’ta Storm ile büyük veri analizini gerçek zamanlı olarak gerçekleştiren bulut tabanlı bir Storm kümesi oluşturabilirsiniz.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Ön koşullar

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **SSH ve SCP hakkında bilgi**. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Storm kümesi oluşturma

Hdınsight kümesinde bir Storm adımları toocreate aşağıdaki hello kullan:

1. Merhaba gelen [Azure portal](https://portal.azure.com)seçin **+ yeni**, **Intelligence + analiz**ve ardından **Hdınsight**.

    ![HDInsight kümesi oluşturma](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. Merhaba gelen **Temelleri** dikey penceresinde, aşağıdaki bilgilerle hello girin:

    * **Küme adı**: Merhaba Hdınsight kümesi hello adı.
    * **Abonelik**: hello abonelik toouse seçin.
    * **Oturum açma kullanıcı küme** ve **küme oturum açma parolasını**: hello küme HTTPS üzerinden erişirken hello oturum açma. Bu kimlik bilgileri tooaccess Hizmetleri gibi hello Ambari Web kullanıcı Arabirimi veya REST API'yi kullanın.
    * **Güvenli Kabuk (SSH) kullanıcıadı**: hello küme SSH üzerinden erişirken kullanılan hello oturum açma. Varsayılan olarak hello parola olduğu hello hello küme oturum açma parolası ile aynı.
    * **Kaynak grubu**: hello kaynak grubu toocreate hello kümede.
    * **Konum**: hello Azure bölgesi toocreate hello kümede.

    ![Abonelik seçme](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Seçin **küme türü**, ve ardından kümesi hello aşağıdaki değerleri üzerinde hello **küme yapılandırması** dikey penceresinde:

    * **Küme Türü**: Storm

    * **İşletim Sistemi**: Linux

    * **Sürüm**: Storm 1.1.0 (HDI 3.6)

    * **Küme Katmanı**: Standart

    Son olarak, hello kullan **seçin** düğmesini toosave ayarlar.

    ![Küme türü seçme](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Merhaba küme türü seçtikten sonra hello kullan __seçin__ düğme tooset hello küme türü. Ardından, hello kullanın __sonraki__ düğme toofinish temel yapılandırması.

5. Merhaba gelen **depolama** dikey penceresinde, bir depolama hesabı oluşturun veya seçin. Bu belgedeki Hello adımlar için bu dikey penceresinde hello varsayılan değerleri diğer alanları hello bırakın. Kullanım hello __sonraki__ düğme toosave depolama yapılandırması.

    ![Hdınsight için Hello depolama hesabı ayarlarını belirleme](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. Merhaba gelen **Özet** dikey penceresinde hello kümesi için hello yapılandırmayı gözden geçir. Kullanım hello __Düzenle__ toochange yanlış ayarları bağlar. Son olarak, the__Create__ düğmesini toocreate hello küme kullanın.

    ![Küme yapılandırma özeti](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Too20 dakika toocreate hello küme alabilir.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>HDInsight'ta bir storm-starter örneği çalıştırma

1. SSH kullanarak toohello Hdınsight kümesine bağlanın:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    SSH kullanıcı hesabınızın parolası toosecure kullandıysanız, istendiğinde tooenter olan bu. Bir ortak anahtar kullandıysanız, hello kullanabilirsiniz `-i` parametresi toospecify hello eşleşen özel anahtarı. Örneğin, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Aşağıdaki komut toostart örnek bir topoloji hello kullan:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > Hdınsight önceki sürümlerinde hello sınıfı hello topoloji adıdır `storm.starter.WordCountTopology` yerine `org.apache.storm.starter.WordCountTopology`.

    Bu komut, hello kümede 'WordCount' kolay adı ile Merhaba örnek WordCount topolojisini başlatır. Bu rastgele cümleleri ve her sözcüğün sayısı hello oluşma hello cümlelerde oluşturur.

    > [!NOTE]
    > Kendi topolojileri toohello küme gönderirken, ilk hello kullanmadan önce hello kümeyi içeren hello jar dosyasını kopyalamanız gerekir `storm` komutu. Kullanım hello `scp` komut toocopy hello dosyası. Örneğin, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > Merhaba WordCount örneği ve diğer storm starter örnekleri zaten eklenir konumunda kümenize `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Merhaba kaynak hello storm-starter örnekleri için görüntüleme ilgileniyorsanız hello kodu bulabilirsiniz [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). Bu bağlantı, HDInsight 3.6 ile birlikte sağlanan Storm 1.1.x içindir. Storm diğer sürümleri için hello kullanın __şube__ farklı bir Storm sürüm hello sayfa tooselect hello üstünde düğmesi.

## <a name="monitor-hello-topology"></a>İzleyici hello topolojisi

Merhaba Storm kullanıcı Arabirimi çalışan topolojilerle çalışmaya yönelik bir web arabirimi sağlar ve Hdınsight kümenize dahil edilir.

Merhaba Storm kullanıcı arabirimini kullanarak adımları toomonitor hello topolojisi aşağıdaki hello kullan:

1. toodisplay hello Storm kullanıcı Arabirimi, bir web tarayıcısı toohttps://CLUSTERNAME.azurehdinsight.net/stormui açın. Değiştir **CLUSTERNAME** kümenizin hello ada sahip.

    > [!NOTE]
    > Hello Yöneticisi (Yönetici) ve ne zaman kullanılan parola tooprovide bir kullanıcı adı ve parola istenirse, girin oluşturma hello küme.

2. Altında **topoloji özeti**seçin hello **wordcount** hello girişi **adı** sütun. Merhaba topolojisi hakkında bilgi görüntülenir.

    ![Storm-starter WordCount topoloji bilgilerini içeren Storm Panosu.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Bu sayfa aşağıdaki bilgilerle hello sağlar:

    * **Topoloji istatistikleri** -temel bilgileri hello topoloji performansı hakkında zaman pencereleri halinde düzenlenmiş.

        > [!NOTE]
        > Merhaba sayfanın diğer bölümlerinde gösterilen bilgileri için belirli bir zaman penceresi değişiklikleri hello zaman penceresi seçme.

    * **Spout'lar** -her bir spout'un döndürdüğü hello son hata dahil olmak üzere spout'lar hakkında temel bilgiler.

    * **Cıvatalar** - Cıvatalar hakkında temel bilgiler.

    * **Topoloji Yapılandırması** -hello topoloji yapılandırması hakkında ayrıntılı bilgi.

    Bu sayfa ayrıca hello topolojisine gerçekleştirilecek eylemleri sağlar:

    * **Etkinleştir** - Devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.

    * **Devre dışı bırak** - Çalışan topolojiyi duraklatır.

    * **Yeniden dengelemeniz** -hello hello topolojisinin paralelliğini ayarlar. Merhaba hello kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir. Dengelenmesi paralellik toocompensate hello artan/azalan düğüm sayısını hello kümedeki için ayarlar. Daha fazla bilgi için bkz: [hello bir Storm topolojisinin paralelliğini anlama](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **KILL** -hello belirtilen zaman aşımı sonra Storm topolojisini sonlandırır.

3. Bu sayfadan hello bir giriş seçin **Spout'lar** veya **Cıvatalar** bölümü. Merhaba seçilen bileşenle ilgili bilgileri görüntülenir.

    ![Seçili bileşenler hakkında bilgi içeren Storm Panosu.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Bu sayfa aşağıdaki bilgilerle hello görüntüler:

    * **Spout/Cıvata istatistikleri** -temel bilgileri hello bileşen performansı hakkında zaman pencereleri halinde düzenlenmiş.

        > [!NOTE]
        > Merhaba sayfanın diğer bölümlerinde gösterilen bilgileri için belirli bir zaman penceresi değişiklikleri hello zaman penceresi seçme.

    * **Giriş İstatistikleri** (yalnızca Cıvata) - hello Cıvata tarafından kullanılan verileri üreten bileşenler hakkında bilgi.

    * **Çıktı istatistikleri** - Bu cıvata tarafından yayılan veriler hakkında bilgi.

    * **Yürütücüler** - Bu bileşenin örnekleri hakkında bilgi.

    * **Hatalar** - Bu bileşenden kaynaklanan hatalar.

4. Merhaba spout veya Cıvata ayrıntılarını görüntülerken hello bir girişi seçin **bağlantı noktası** hello sütununda **yürütücüler** bölümünde hello bileşenin belirli bir örneği için tooview ayrıntıları.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    Bu örnekte, word hello **yedi** sözcüğünün 1493957 kez oluştu. Bu topoloji başlatıldığından beri hello word karşılaşıldı kaç kez sayısıdır.

## <a name="stop-hello-topology"></a>Merhaba topolojiyi durdurma

Toohello iade **topoloji özeti** sayfasında hello word-count topolojisi için ve hello ardından **KILL** hello düğmesinden **topoloji eylemleri** bölümü. İstendiğinde, 10 hello topolojiyi durdurmadan önce hello saniye toowait için girin. Merhaba ziyaret ettiğinizde hello zaman aşımı süresinden sonra hello topoloji artık görünür **Storm kullanıcı Arabirimi** başlangıç Panosu bölümü.

## <a name="delete-hello-cluster"></a>Merhaba küme silme

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight kümesi oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Sonraki adımlar

Bu Apache Storm öğreticisinde Hdınsight üzerinde Storm ile çalışmanın temelleri hello öğrendiniz. Ardından, nasıl çok öğrenin[Maven kullanarak geliştirme Java tabanlı topolojiler](hdinsight-storm-develop-java-topology.md).

Zaten Java tabanlı topolojiler geliştirme ile tanıdık ve toodeploy var olan bir topoloji tooHDInsight istiyorsanız, bkz [dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetmek](hdinsight-storm-deploy-monitor-topology-linux.md).

.NET geliştiricisiyseniz Visual Studio'yu kullanarak C# veya karma C#/Java topolojileri oluşturabilirsiniz. Daha fazla bilgi edinmek için bkz. [Visual Studio için Hadoop araçlarını kullanarak HDInsight'ta Apache Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Hdınsight üzerinde Storm ile kullanılan örnek Topolojileri için örnek hello bakın:

* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
