---
title: "Azure Hdınsight Linux üzerinde Presto aaaInstall kümeleri | Microsoft Docs"
description: "Nasıl tooinstall Presto ve Linux tabanlı Hdınsight Hadoop üzerinde Airpal betik eylemleri kullanarak kümelerini öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Yükleme ve Presto Hdınsight Hadoop kümeleri kullanma

Bu konuda, betik eylemi kullanarak nasıl tooinstall Presto üzerinde Hdınsight Hadoop kümeleri öğrenin. Da bilgi nasıl tooinstall Airpal varolan Presto Hdınsight kümesinde.

> [!IMPORTANT]
> Merhaba bu belgedeki adımlar gerektiren bir **Hdınsight 3.5 Hadoop kümesi** Linux kullanır. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight sürümleri](hdinsight-component-versioning.md).

## <a name="what-is-presto"></a>Presto nedir?
[Presto](https://prestodb.io/overview.html) bir hızlı dağıtılmış SQL sorgu alt büyük veri yapısıdır. Presto etkileşimli veri petabaytlarca sorgulamak için uygundur. Presto ve nasıl çalıştıkları hello bileşenler hakkında daha fazla bilgi için bkz: [Presto kavramları](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.
> 
> Presto gibi özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Merhaba sorunu çözmek veya tooengage kullanılabilir kanalları hello için bu teknoloji derin uzmanlık bulunduğu kaynak teknolojileri açtığınız isteyen neden olabilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).
> 
> 


## <a name="install-presto-using-script-action"></a>Betik eylemi kullanarak Presto yükleyin

Bu bölümde, nasıl kullanarak yeni bir küme oluştururken, toouse hello örnek betik hello üzerinde Azure portal yönergeler sağlar. 

1. Merhaba adımları kullanarak bir küme hazırlama Başlat [sağlama Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md). Hello kullanarak hello küme oluşturduğunuzdan emin olun **özel** küme oluşturma akış. Oluşturduğunuz bu hello küme hello gereksinimleri aşağıdaki karşıladığından emin olmalısınız.

    a. Bir Hadoop kümesine Hdınsight sürüm 3.5 ile olmalıdır.

    b. Azure Storage hello veri deposu olarak kullanmanız gerekir. Azure Data Lake Store hello depolama seçeneği olarak kullanan bir kümede presto kullanarak henüz desteklenmiyor. 

    ![Özel seçenekleri kullanarak Hdınsight kümesi oluşturma](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. Merhaba üzerinde **Gelişmiş ayarları** dikey penceresinde, select **betik eylemleri**ve aşağıdaki hello bilgileri sağlayın:
   
   * **AD**: hello betik eylemi için kolay bir ad girin.
   * **Bash betiği URI’si**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **HEAD**: Bu seçeneği işaretleyin.
   * **ÇALIŞAN**: Bu seçeneği işaretleyin.
   * **ZOOKEEPER**: Bu onay kutusunu temizleyin
   * **PARAMETRELERİ**: Bu alanı boş bırakın


3. Merhaba hello sonundaki **betik eylemleri** dikey penceresinde hello tıklatın **seçin** düğme toosave hello yapılandırması. Son olarak, hello tıklatın **seçin** hello hello sonundaki düğmesi **Gelişmiş ayarlar** dikey toosave hello yapılandırma bilgileri.

4. Bölümünde açıklandığı gibi Hello küme hazırlama devam [sağlama Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Azure PowerShell, hello Azure CLI, hello Hdınsight .NET SDK veya Azure Resource Manager şablonları kullanılan tooapply betik eylemleri de olabilir. Betik eylemleri tooalready kümeleri çalıştıran uygulayabilir. Daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Hdınsight ile presto kullanma

Yukarıda açıklanan başlangıç adımları kullanarak yükledikten sonra bir Hdınsight kümesindeki adımları toouse Presto aşağıdaki hello gerçekleştirin.

1. SSH kullanarak toohello Hdınsight kümesine bağlanın:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Merhaba Presto Kabuk komut aşağıdaki hello kullanarak başlatın.
   
        presto --schema default

3. Bir örnek tablo sorgusu **hivesampletable**, varsayılan olarak tüm Hdınsight kümeleri üzerinde kullanılabilir olduğu.
   
        select count (*) from hivesampletable;
   
    Varsayılan olarak, [Hive](https://prestodb.io/docs/current/connector/hive.html) ve [TPCH](https://prestodb.io/docs/current/connector/tpch.html) bağlayıcıları Presto için zaten yapılandırılmış. Hive tüm hello tablolardan Presto içinde otomatik olarak görünür olacak şekilde hive yapılandırılmış toouse hello varsayılan olarak yüklenen Hive yükleme Bağlayıcıdır.

    Presto nasıl kullanabileceğiniz hakkında ayrıntılı bir açıklaması için bkz: [Presto belgelerine](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Airpal Presto ile kullanma

[Airpal](https://github.com/airbnb/airpal#airpal) Presto için bir açık kaynak web tabanlı sorgu arabirimdir. Airpal hakkında daha fazla bilgi için bkz: [Airpal belgelerine](https://github.com/airbnb/airpal#airpal).

Bu bölümde, biz hello adımları çok Ara**Airpal hello edgenode üzerinde yükleme** Presto önceden sahip olan bir Hdınsight Hadoop kümesini yüklü. Bu, hello Airpal web sorgu arabirimi hello Internet kullanılabilir sağlar.

1. SSH kullanarak, toohello headnode Presto yüklediği hello Hdınsight kümesinin Bağlan:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Bağlandıktan sonra komutu aşağıdaki hello çalıştırın.

        sudo slider registry  --name presto1 --getexp presto 
   
    Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. Merhaba çıktısını hello için başlangıç değerini not edin **değeri** özelliği. Bu, üzerinde hello küme edgenode Airpal yüklenirken gerekir. İhtiyacınız olacak hello değerin üzerinde hello çıktısından olan **10.0.0.12:9090**.

4. Merhaba şablonu kullan  **[burada](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate bir Hdınsight edgenode küme ve hello ekran aşağıdaki gösterildiği gibi hello değerler sağlayın.

    ![Hdınsight yükle Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. **Satın al**’a tıklayın.

6. Merhaba değişiklikleri uygulanan toohello küme yapılandırması olduktan sonra aşağıdaki adımları hello kullanarak hello Airpal web arabirimi erişebilir.

    a. Merhaba küme dikey penceresinden tıklayın **uygulamaları**.

    ![Hdınsight başlatılırken Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. Merhaba gelen **yüklü uygulamalar** dikey penceresinde tıklatın **Portal** airpal karşı.

    ![Hdınsight başlatılırken Airpal Presto küme](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. İstendiğinde, hello Hdınsight Hadoop kümesi oluşturulurken belirtilen hello yönetici kimlik bilgilerini girin.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Hdınsight kümesinde Presto yüklemeyi özelleştirme

Bir Hdınsight Hadoop kümesinde Presto yükledikten sonra hello yükleme toomake değişiklikleri güncelleştirme bellek ayarları gibi özelleştirin, bağlayıcılar, vb. değiştirin. Adımları toodo şekilde aşağıdaki hello gerçekleştirin.

1. SSH kullanarak, toohello headnode Presto yüklediği hello Hdınsight kümesinin Bağlan:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Yapılandırma değişiklik hello dosyasında `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Presto yapılandırma hakkında daha fazla bilgi için bkz: [YARN tabanlı kümeler için Presto yapılandırma](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).

3. Durdurun ve hello geçerli çalışan örneği Presto sonlandırın.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Presto yeni bir örneğini hello özelleştirme ile başlatın.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Merhaba yeni örnek toobe için hazır bekleyin ve presto Düzenleyicisi adresi unutmayın.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Kıyaslama verileri Presto çalıştırmak Hdınsight kümeleri oluşturma

TPC DS birçok karar destek büyük veri sistemlerini sistemlerle hello performansını ölçmek için standart hello endüstri standardıdır. Hdınsight kümeleri toogenerate verileri Presto kullanın ve nasıl kendi Hdınsight Kıyaslama verilerle karşılaştırır değerlendirin. Daha fazla bilgi için bkz: [burada](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>Ayrıca bkz.
* [Yükleme ve Hdınsight kümelerinde ton kullanma](hdinsight-hadoop-hue-linux.md). Hue web çalışması kolay toocreate kolaylaştırır kullanıcı Arabirimi olan ve Pig ve Hive işleri de olarak hello varsayılan depolama Hdınsight kümeniz için göz atın.

* [Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md). Giraph üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın. Giraph tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.

* [Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md). Solr üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın. Solr tooperform güçlü arama işlemleri depolanan verileri sağlar.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
