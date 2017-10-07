---
title: "Hdınsight Linux tabanlı kümelerde - Azure Hadoop ile aaaHue | Microsoft Docs"
description: "Nasıl tooinstall ton hdınsight kümeleri öğrenin ve tünel tooroute hello istekleri tooHue kullanın. Hue toobrowse depolama kullanın ve Hive veya Pig çalıştırın."
keywords: Hue hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Yükleme ve Hue Hdınsight Hadoop kümeleri kullanma

Nasıl tooinstall ton hdınsight kümeleri öğrenin ve tünel tooroute hello istekleri tooHue kullanın.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-is-hue"></a>Hue nedir?
Hue Web uygulamaları toointeract Hadoop kümesi ile kullanılır. Bir Hadoop kümesine (Hdınsight kümelerinin hello durumda, WASB) ile ilişkili ton toobrowse hello depolama kullanan, Hive işleri ve Pig betikleri çalıştırmak ve benzeri. Merhaba aşağıdaki bileşenleri bir Hdınsight Hadoop kümesi ton yüklemelerinde ile kullanılabilir.

* Beeswax Hive Düzenleyicisi
* Pig
* Meta depo Yöneticisi
* Oozie
* (Hangi tooWASB varsayılan kapsayıcı ettiği) FileBrowser
* İş tarayıcı

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.
>
> Özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Merhaba sorunu çözmek veya tooengage kullanılabilir kanalları hello için bu teknoloji derin uzmanlık bulunduğu kaynak teknolojileri açtığınız isteyen neden olabilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).
>
>

## <a name="install-hue-using-script-actions"></a>Betik eylemleri kullanılarak Hue yüklemek

Merhaba betik tooinstall Linux tabanlı Hdınsight kümesine Hue https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh kullanılabilir. Bu komut dosyası tooinstall ton varsayılan depolama alanı olarak Azure Storage Blobları (WASB) veya Azure Data Lake Store ile kümelerde kullanabilirsiniz.

Bu bölümde nasıl toouse hello betik hello Azure portal kullanarak hello küme sağlamada hakkında yönergeler sağlar.

> [!NOTE]
> Azure PowerShell, hello Azure CLI, hello Hdınsight .NET SDK veya Azure Resource Manager şablonları kullanılan tooapply betik eylemleri de olabilir. Betik eylemleri tooalready kümeleri çalıştıran uygulayabilir. Daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Merhaba adımları kullanarak bir küme hazırlama Başlat [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md), ancak sağlama tamamlamayın.

   > [!NOTE]
   > Hdınsight üzerinde tooinstall ton kümeleri, hello önerilen headnode boyutu en az A4 (8 çekirdek, 14 GB bellek).
   >
   >
2. Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **betik eylemleri**ve aşağıda gösterildiği gibi hello bilgileri sağlayın:

    ![Betik eylemi parametreler sağlayın ton için](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "sağlamak betik eylem parametrelerini ton için")

   * **AD**: hello betik eylemi için kolay bir ad girin.
   * **BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**: Bu seçeneği işaretleyin.
   * **ÇALIŞAN**: Bu alanı boş bırakın.
   * **ZOOKEEPER**: Bu alanı boş bırakın.
   * **PARAMETRELERİ**: Bu alanı boş bırakın.
3. Merhaba hello sonundaki **betik eylemleri**, hello kullan **seçin** düğme toosave hello yapılandırması. Son olarak, hello kullan **seçin** düğmesi hello hello sonundaki **isteğe bağlı yapılandırma** dikey toosave hello isteğe bağlı yapılandırma bilgileri.
4. Bölümünde açıklandığı gibi Hello küme hazırlama devam [Hdınsight kümeleri hazırlama Linux'ta](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Hdınsight kümeleri ile ton kullanın

Çalışmaya başladıktan sonra SSH tünel hello hello kümede yalnızca ton yolu tooaccess ' dir. Merhaba, toohello headnode küme doğrudan ton çalıştığı SSH yoluyla tünel hello trafiği toogo sağlar. Merhaba küme Sağlama tamamlandıktan sonra bir Hdınsight Linux kümede adımları toouse ton aşağıdaki hello kullanın.

> [!NOTE]
> Firefox web tarayıcısı toofollow hello yönergelerde kullanmanızı öneririz.
>
>

1. Merhaba bilgileri kullanın [kullanım SSH tünel tooaccess Ambari web kullanıcı Arabirimi, ResourceManager, kaynak, iş, Oozie ve diğer web kullanıcı Arabiriminin](hdinsight-linux-ambari-ssh-tunnel.md) toocreate bir SSH tünel, istemci sistem toohello Hdınsight kümenizden ve yapılandırın Web tarayıcısı toouse hello SSH tüneli proxy olarak.

2. SSH tüneli oluşturduktan ve tarayıcı tooproxy trafiğinizi aracılığıyla yapılandırdıktan sonra hello ana bilgisayar adı hello birincil baş düğümü bulmanız gerekir. Bu, SSH bağlantı noktası 22 kullanarak toohello küme bağlanarak yapabilirsiniz. Örneğin, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` nerede **kullanıcıadı** SSH kullanıcı adınız ve **CLUSTERNAME** hello kümenizin adıdır.

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Bağlantı kurulduktan sonra komutu tooobtain hello tam etki alanı adı hello birincil headnode aşağıdaki hello kullan:

        hostname -f

    Bu ad benzer toohello aşağıdaki döndürür:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Bu, hello birincil headnode hello ana hello Hue Web sitesi bulunduğu adıdır.
4. Merhaba tarayıcı tooopen hello Hue portalını http://HOSTNAME:8888 kullanın. Ana bilgisayar adı hello önceki adımda elde ettiğiniz hello adla değiştirin.

   > [!NOTE]
   > Merhaba ilk kez oturum açtığınızda, istendiğinde toocreate toohello ton Portalı'nda bir hesap toolog olacaktır. Burada belirttiğiniz hello kimlik sınırlı toohello portal olacaktır ve ilgili toohello yönetici veya SSH kullanıcı kimlik bilgileri sağlama hello küme sırasında belirtilen değildir.
   >
   >

    ![Oturum açma toohello Hue portalını](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Hue portalını için kimlik bilgilerini belirtin")

### <a name="run-a-hive-query"></a>Hive sorgusu çalıştırma
1. Merhaba ton portalından tıklatın **sorgu düzenleyicileri**ve ardından **Hive** tooopen hello Hive düzenleyicisinin.

    ![Hive kullanma](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Hive kullanma")
2. Merhaba üzerinde **yardımcı** sekmesinde, altında **veritabanı**, görmeniz gerekir **hivesampletable**. Hdınsight üzerinde tüm Hadoop kümeleri ile birlikte gelen bir örnek tablo budur. Merhaba sağ bölmede bir örnek sorgu girin ve üzerinde hello hello çıktı görmeniz **sonuçları** sekmesinde bulunan aşağıdaki hello bölmesini hello ekran görüntüsünde gösterildiği gibi.

    ![Hive sorgusu çalıştırmak](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "çalıştırmak Hive sorgusu")

    Merhaba de kullanabilirsiniz **grafik** toosee görsel bir hello sonuç sekmesinde.

### <a name="browse-hello-cluster-storage"></a>Merhaba küme depolama Gözat
1. Merhaba ton portalından tıklatın **dosya tarayıcısı** hello sağ üst köşesindeki hello menü çubuğu.
2. Varsayılan olarak hello hello dosya tarayıcısı açılır **/kullanıcı/myuser** dizini. Merhaba eğik hello kullanıcı hello kümesi ile ilişkili hello Azure storage kapsayıcısının hello yolu toogo toohello kök dizininde önce sağ tıklayın.

    ![Kullanım dosya tarayıcısı](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "kullanım dosya tarayıcısı")
3. Bir dosya veya klasör toosee hello kullanılabilir işlemleri sağ tıklayın. Kullanım hello **karşıya** hello köşedeki tooupload dosyaları toohello geçerli dizinde düğmesi. Kullanım hello **yeni** toocreate yeni dosya veya dizinlerin düğmesine tıklayın.

> [!NOTE]
> Merhaba ton dosya tarayıcısı sadece hello varsayılan kapsayıcı hello Hdınsight kümesi ile ilişkili Merhaba içeriğine gösterebilir. Tüm ek depolama hesapları/hello kümesi ile ilişkili kapsayıcıları hello dosya tarayıcısı kullanılarak erişilebilir olmaz. Ancak, hello ek kapsayıcıları hello kümesi ile ilişkili her zaman hello Hive işleri için erişilebilir olacaktır. Merhaba komutu girin, örneğin, `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` hello Hive Düzenleyicisi'nde hello içeriğini diğer kapsayıcıları görebilirsiniz. Bu komutta **newcontainer** değil bir kümeyle ilişkili hello varsayılan kapsayıcı.
>
>

## <a name="important-considerations"></a>İle ilgili önemli noktalar
1. Merhaba kullanılan komut dosyası tooinstall ton yalnızca hello birincil headnode hello küme üzerinde yükler.

2. Yükleme sırasında birden çok Hadoop Hizmetleri (HDFS, YARN, MR2, Oozie) hello yapılandırmasını güncelleştirmek için yeniden başlatılır. Merhaba betik ton yükleme tamamlandıktan sonra diğer Hadoop Hizmetleri toostart biraz zaman sürebilir. Başlangıçta bu ton'ın performansını etkileyebilir. Tüm hizmetler başlatma sonra ton tamamen işlevsel olacaktır.
3. Hue Tez işlerinde Hive için geçerli varsayılan hello olduğu anlamıyor. Hive yürütme altyapısı hello gibi toouse MapReduce istiyorsanız, komut dosyanızı komutunda aşağıdaki hello betik toouse hello güncelleştirin:

        set hive.execution.engine=mr;

4. Linux kümeleriyle hello Resource Manager ikincil hello gerçekleştirdiğinizde burada hizmetlerinizi hello birincil headnode üzerinde çalışan bir senaryo olabilir. Böyle bir senaryo (aşağıda gösterilen) hataları ton tooview çalışan işlerinin ayrıntılarını hello kümede kullanırken neden olabilir. Ancak, Hello iş tamamlandığında hello iş ayrıntılarını görüntüleyebilirsiniz.

   ![Hue portal hata](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "ton portal hata")

   Bu bilinen sorun tooa. Geçici bir çözüm olarak, Ambari Hello etkin Kaynak Yöneticisi'ni de hello birincil headnode üzerinde çalışan şekilde değiştirin.
5. Hdınsight kümeleri Azure Storage kullanarak kullanırken ton anlar WebHDFS `wasb://`. Bu nedenle, betik eylemi ile kullanılan hello özel komut dosyası tooWASB Konuşmayı için WebHDFS ile uyumlu hizmeti WebWasb yükler. Bunu, HDFS yerlerde hello Hue portalını diyor olsa bile (Merhaba farenizi taşıdığınızda gibi **dosya tarayıcısı**), WASB yorumlanıp.

## <a name="next-steps"></a>Sonraki adımlar
* [Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md). Giraph üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın. Giraph tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.
* [Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md). Solr üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın. Solr tooperform güçlü arama işlemleri depolanan verileri sağlar.
* [Hdınsight kümelerinde R yüklemek](hdinsight-hadoop-r-scripts-linux.md). Küme özelleştirme tooinstall R Hdınsight Hadoop kümeleri üzerinde kullanın. R bir açık kaynaklı dil ve istatistiksel bilgi işlem ortamı ' dir. Yüzlerce yerleşik istatistik işlevleri ve işlev ve nesne odaklı programlama yönlerini birleştirir kendi programlama dili sağlar. Yoğun grafik yetenekleri de sağlar.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
