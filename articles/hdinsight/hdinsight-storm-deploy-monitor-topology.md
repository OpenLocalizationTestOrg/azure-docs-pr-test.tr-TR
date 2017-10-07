---
title: "aaaDeploy ve Hdınsight üzerinde Apache Storm topolojilerini yönetme | Microsoft Docs"
description: "Nasıl toodeploy, izlemek ve hello Storm panosunu kullanarak Hdınsight üzerinde Apache Storm topolojilerini yönetmek öğrenin. Visual Studio Hadoop araçlarını kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Dağıtma ve Windows tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme

Merhaba Storm Panosu tooeasily verir dağıtın ve Apache Storm topolojileri tooyour Hdınsight kümesi, web tarayıcısı kullanarak çalıştırın. Ayrıca, hello Pano toomonitor kullanın ve çalışan topolojileri izleyip yönetmek. Visual Studio kullanırsanız, Visual Studio için Hdınsight araçları hello Visual Studio'da benzer özellikleri sağlar.

Merhaba Storm panosu ve hello Storm hello Hdınsight araçları özelliklerinde kullanılan toocreate olabilen Storm REST API hello üzerinde kendi izleme ve yönetim çözümleri kullanır.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Windows hello işletim sistemi olarak kullanan Hdınsight kümesi üzerinde Storm gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Dağıtma ve Storm topolojileri Linux kullanan bir Hdınsight kümesi ile yönetme hakkında daha fazla bilgi için bkz: [dağıtma ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Ön koşullar

* **Hdınsight üzerinde Apache Storm** -bkz [Hdınsight üzerinde Apache Storm ile çalışmaya başlama](hdinsight-apache-storm-tutorial-get-started.md) küme oluşturma adımları için.

* Hello için **Storm Panosu**: HTML5 destekleyen modern bir web tarayıcısı.

* İçin **Visual Studio** -Azure SDK'sı 2.5.1 ya da daha yeni ve Visual Studio için Hdınsight araçları hello. Bkz: [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall ve hello Hdınsight araçları Visual Studio için yapılandırın.

    Visual Studio sürümleri aşağıdaki hello biri:

  * Visual Studio 2012 güncelleştirme 4 ile

  * Visual Studio 2013 güncelleştirme 4 veya Visual Studio 2013 Community

  * Visual Studio 2015 (herhangi bir sürümünü)

  * Visual Studio 2017 (herhangi bir sürümünü)

## <a name="storm-dashboard"></a>Storm Panosu

Merhaba Storm Panosu Storm kümenizde kullanılabilir bir web sayfasıdır. Merhaba URL **https://&lt;clustername >.azurehdinsight.net/**, burada **clustername** Hdınsight kümesi üzerinde Storm'a hello adıdır.

Merhaba Storm Panosu Hello üstten seçin **gönderme topoloji**. Başlangıç sayfası toorun örnek topoloji Hello yönergeler veya tooupload izleyin ve sizin oluşturduğunuz bir topoloji çalıştırın.

![Merhaba topolojisi sayfasında Gönder][storm-dashboard-submit]

### <a name="storm-ui"></a>Storm kullanıcı Arabirimi

Storm Panosu Hello hello seçin **Storm kullanıcı Arabirimi** bağlantı. Bu, çalışan topolojilerle toplama tooany içinde hello küme hakkındaki bilgileri görüntüler.

![Merhaba storm kullanıcı arabirimi][storm-dashboard-ui]

> [!NOTE]
> Internet Explorer'ın bazı sürümleriyle ilk ziyaret ettikten sonra Storm kullanıcı Arabirimi yenilemez bu hello fark edebilirsiniz. Örneğin, bunu hello yeni topolojileri gönderdiğiniz ya da daha önce etkinliği, bir topoloji etkin olarak gösterebilir göstermeyebilir. Microsoft bu sorunun farkındadır ve bir çözüm üzerinde çalışmaktadır.

#### <a name="main-page"></a>Ana sayfa

Merhaba Storm kullanıcı Arabirimi ana sayfasının Hello bilgisinden hello sağlar:

* **Küme Özet**: hello Storm kümesi hakkında temel bilgiler.

* **Topoloji özeti**: topolojileri çalışan bir listesi. Bu bölümde tooview Hello bağlantıları belirli topolojileri hakkında daha fazla bilgi kullanın.

* **Yönetici Özeti**: hello Storm İdarecisi hakkında bilgi.

* **Nimbus yapılandırma**: hello küme Nimbus yapılandırması.

#### <a name="topology-summary"></a>Topoloji özeti

Merhaba bir bağlantı seçme **topoloji özeti** bölümü hello topolojisi hakkında bilgi aşağıdaki hello görüntüler:

* **Topoloji özeti**: hello topolojisi hakkında temel bilgiler.

* **Topoloji eylemleri**: hello topolojisi gerçekleştirebilen yönetim işlemleri.

  * **Etkinleştirme**: devre dışı bırakılan bir topolojiyi işlemeyi sürdürür.

  * **Devre dışı**: çalışan topolojiyi duraklatır.

  * **Yeniden dengelemeniz**: hello hello topolojisinin paralelliğini ayarlar. Merhaba hello kümedeki düğüm sayısını değiştirdikten sonra çalışan topolojileri yeniden dengelemeniz gerekir. Bu, hello topoloji tooadjust paralellik toocompensate hello için artırılabilir veya hello kümedeki düğüm sayısını azaltılabilir sağlar.

      Daha fazla bilgi için bkz: [hello (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) bir Storm topolojisinin paralelliğini anlama](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **KILL**: hello belirtilen zaman aşımı sonra Storm topolojisini sonlandırır.

* **Topoloji istatistikleri**: hello topoloji hakkındaki istatistiklerdir. Hello Hello bağlantıları kullanın **penceresi** sütun tooset hello hello sayfasında girişleri kalan hello ilişkin zaman çerçevesini.

* **Spout'lar**: Merhaba spout'lar hello topolojisi tarafından kullanılır. Bu bölümde tooview Hello bağlantıları belirli spout'lar hakkında daha fazla bilgi kullanın.

* **Cıvatalar**: Merhaba Cıvatalar hello topolojisi tarafından kullanılır. Bu bölümde tooview Hello bağlantıları belirli Cıvatalar hakkında daha fazla bilgi kullanın.

* **Topoloji Yapılandırması**: Seçili hello topolojisinin hello yapılandırma.

#### <a name="spout-and-bolt-summary"></a>Spout ve Cıvata özeti

Bir spout hello seçme **Spout'lar** veya **Cıvatalar** bölümleri hello seçili öğe hakkında bilgileri aşağıdaki hello görüntüler:

* **Bileşen özeti**: Merhaba spout veya Cıvata hakkında temel bilgiler.

* **Spout/Cıvata istatistikleri**: hello hakkındaki istatistiklerdir spout veya Cıvata. Hello Hello bağlantıları kullanın **penceresi** sütun tooset hello hello sayfasında girişleri kalan hello ilişkin zaman çerçevesini.

* **Giriş İstatistikleri** (yalnızca Cıvata): hello hakkında bilgi giriş hello Cıvata tarafından kullanılan akışı.

* **Çıkış istatistikleri**: spout veya Cıvata bu tarafından gösterilen hello akışları hakkında bilgi.

* **Yürütücüler**: hello örneklerini hello spout veya Cıvata hakkında bilgi. Select hello **bağlantı noktası** girişi belirli Yürütücü tooview için tanılama bilgileri günlüğünü üretilen Bu örneği için.

* **Hataları**: Bu hata bilgilerini spout veya Cıvata.

## <a name="hdinsight-tools-for-visual-studio"></a>Visual Studio için HDInsight Araçları

Merhaba Hdınsight araçları kullanılan toosubmit C# veya karma topolojiler tooyour Storm kümesi olabilir. Aşağıdaki adımları hello örnek bir uygulama kullanın. Merhaba Hdınsight araçları kullanarak kendi topolojileri oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio için Hdınsight araçları hello kullanarak C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Adımları toodeploy örnek tooyour Storm Hdınsight kümesinde aşağıdaki hello kullanın, sonra görüntüleyin ve hello topoloji yönetin.

1. Visual Studio için Hdınsight araçları hello en son sürümünü hello yüklemediyseniz, bkz: [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Visual Studio'ni açın, **dosya** > **yeni** > **proje**.

3. Merhaba, **yeni proje** iletişim kutusunda, genişletin **yüklü** > **şablonları**ve ardından **Hdınsight**. Merhaba şablonları listesinden **Storm örnek**. Merhaba iletişim kutusunun Hello altında hello uygulama için bir ad yazın.

    ![Görüntü](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **hdınsight'ta tooStorm gönderme**.

   > [!NOTE]
   > İstenirse, Azure aboneliğinizin hello oturum açma kimlik bilgilerini girin. Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açın.

5. Hdınsight kümesi üzerinde Storm'a hello seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**. Hello kullanarak Hello gönderme başarılı olup olmadığını izleyebilirsiniz **çıkış** penceresi.

6. Merhaba topoloji başarıyla gönderildi, hello **Storm topolojilerini** hello küme görünür. Merhaba topoloji hello listesi tooview topoloji çalıştıran hello bilgilerini seçin.

    ![Visual studio İzleyicisi](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > De görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini** genişleterek **Azure** > **Hdınsight**ve Hdınsight kümesinde bir Storm sağ tıklayıp seçerek **görünüm Storm topolojilerini**.

    Merhaba spout'lar ya da bu bileşenler hakkında bilgi tooview Cıvatalar hello şekli seçin. Yeni bir pencere için seçilen her öğenin açar.

   > [!NOTE]
   > Merhaba hello topoloji adıdır hello topolojisinin hello sınıf adı (Bu durumda, `HelloWord`,) eklenmiş bir zaman damgasına sahip.

7. Merhaba gelen **topoloji özeti** görünümü, select **KILL** toostop hello topolojisi.

   > [!NOTE]
   > Storm topolojilerini durdurulmuş veya hello küme silinene kadar çalışmaya devam edin.


## <a name="rest-api"></a>REST API

benzer yönetim ve izleme işlevselliği hello REST API kullanarak gerçekleştirebilmek için hello Storm kullanıcı Arabirimi REST API hello üzerinde oluşturulmuştur. Merhaba REST API toocreate özel araçlar yönetmek ve Storm topolojilerini izlemek için kullanabilirsiniz.

Daha fazla bilgi için bkz: [Storm kullanıcı Arabirimi REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Merhaba aşağıdaki bilgiler belirli toousing hello Hdınsight üzerinde Apache Storm ile REST API sağlar.

### <a name="base-uri"></a>Taban URI

Hdınsight kümelerinde hello REST API için ana Uri hello **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, burada **clustername** hello Storm'a üzerinde adıdır Hdınsight kümesi.

### <a name="authentication"></a>Kimlik Doğrulaması

REST API kullanmalıdır istekleri toohello **temel kimlik doğrulaması**, hello Hdınsight Küme Yönetici adı ve parola kullanın.

> [!NOTE]
> Temel kimlik doğrulaması düz metin kullanarak gönderildiğinden, aşağıdakileri yapmalısınız **her zaman** hello kümeyle HTTPS toosecure iletişimleri kullanın.

### <a name="return-values"></a>Dönüş değerleri

Hello REST API yalnızca hello küme içinde kullanılabilir olabilir veya sanal makinelerde hello küme aynı Azure sanal ağ hello döndürülen bilgi. Örneğin, Zookeeper sunucuları için döndürülen hello tam etki alanı adı (FQDN) değil olması Internet hello erişilebilir.

## <a name="next-steps"></a>Sonraki Adımlar

Storm panosunu kullanarak toodeploy ve İzleyici topolojileri nasıl hello öğrendiğinize göre öğrenin nasıl yapılır:

* [Visual Studio için Hdınsight araçları Hello kullanarak C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Maven kullanarak Java tabanlı topolojiler geliştirme](hdinsight-storm-develop-java-topology.md)

Daha fazla örnek topolojileri listesi için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
