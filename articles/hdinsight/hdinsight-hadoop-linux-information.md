---
title: "Linux tabanlı Hdınsight üzerinde - Azure Hadoop kullanmaya aaaTips | Microsoft Docs"
description: "Hello Azure bulut çalıştıran tanıdık bir Linux ortamda Linux tabanlı Hdınsight (Hadoop) kümeleri kullanarak uygulama ipuçları alın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Linux'ta Hdınsight kullanma hakkında bilgi

Azure Hdınsight kümeleri Hadoop hello Azure bulut çalıştıran bir bilinen Linux ortamı sağlar. Çoğu işlemler için tam olarak herhangi diğer Linux üzerinde Hadoop yükleme çalışması gerekir. Bu belge farkında olmanız gereken belirli farklılıkları çağırır.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Ön koşullar

Birçok hello adımları bu belgede, sisteminizde yüklü toobe gerekebilir yardımcı programlarını aşağıdaki hello kullanın.

* [cURL](https://curl.haxx.se/) -toocommunicate web tabanlı hizmetler ile kullanılan
* [jq](https://stedolan.github.io/jq/) -kullandığınız tooparse JSON belgeleri
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (Önizleme) - kullanılan tooremotely Azure hizmetlerini yönetme

## <a name="users"></a>Kullanıcılar

Sürece [etki alanına katılmış](hdinsight-domain-joined-introduction.md), Hdınsight sayılacağı bir **tek kullanıcı** sistem. Tek bir SSH kullanıcı hesabı, yönetici düzeyi izinler ile Merhaba kümesi ile oluşturulur. Ek SSH hesapları oluşturulabilir, ancak aynı zamanda yönetici erişimi toohello küme sahiptirler.

Etki alanına katılmış Hdınsight birden çok kullanıcı ve daha ayrıntılı izni ve rol ayarlarını destekler. Daha fazla bilgi için bkz: [yönetmek etki alanına katılmış Hdınsight kümeleri](hdinsight-domain-joined-manage.md).

## <a name="domain-names"></a>Etki alanı adları

Merhaba tam etki alanı adı (FQDN) toouse toohello küme Internet hello bağlanırken  **&lt;clustername >. azurehdinsight.net** veya (yalnızca SSH)  **&lt;clustername-ssh >. azurehdinsight.net**.

Dahili olarak, hello kümedeki her düğümde Küme yapılandırması sırasında atanmış bir adı vardır. bkz: Merhaba toofind hello Küme adları, **ana** hello Ambari Web kullanıcı arabirimini sayfasında. Tooreturn hello Ambari REST API konaklardan listesini aşağıdaki hello de kullanabilirsiniz:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Değiştir **parola** hello yönetici hesabının hello parolayla ve **CLUSTERNAME** kümenizin hello ada sahip. Bu komut hello kümedeki hello ana bilgisayarların listesini içeren bir JSON belgesi döndürür. Jq olan kullanılan tooextract hello `host_name` her ana bilgisayar için öğe değeri.

Belirli bir hizmet için hello düğümünün toofind hello adı gerekiyorsa, bu bileşen için Ambari sorgulayabilirsiniz. Örneğin, toofind hello konakları hello HDFS adı düğümü için komutu aşağıdaki hello kullan:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Bu komut hello hizmet açıklayan bir JSON belgesi döndürür ve sonra yalnızca hello jq çeker `host_name` hello konakları için değer.

## <a name="remote-access-tooservices"></a>Uzaktan erişim tooservices

* **Ambari (web)** -https://&lt;clustername >. azurehdinsight.net

    Merhaba küme yönetici kullanıcı ve parola kullanarak kimlik doğrulaması ve tooAmbari oturum açın.

    Kimlik doğrulama düz metin - kullanım HTTPS toohelp her zaman hello bağlantı güvenli olduğundan emin olun.

    > [!IMPORTANT]
    > Bazı hello web Uı'lar bir iç etki alanı adını kullanarak Ambari erişim düğümler kullanılabilir. Merhaba Internet iç etki alanı adları üzerinden genel olarak erişilebilir değildir. "Sunucu bulunamadı" hatalarını tooaccess hello Internet bazı özellikler çalışırken alabilirsiniz.
    >
    > toouse hello tam işlevselliğini hello Ambari web kullanıcı Arabirimi, bir SSH tünel tooproxy web trafiği toohello küme baş düğümüne kullanın. Bkz: [kullanım SSH tünel tooaccess Ambari web kullanıcı Arabirimi, ResourceManager, kaynak, iş, Oozie ve diğer web Uı'lar](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** -https://&lt;clustername >.azurehdinsight.net/ambari

    > [!NOTE]
    > Merhaba küme yönetici kullanıcı ve parola kullanarak kimlik doğrulaması.
    >
    > Kimlik doğrulama düz metin - kullanım HTTPS toohelp her zaman hello bağlantı güvenli olduğundan emin olun.

* **WebHCat (Templeton)** -https://&lt;clustername >.azurehdinsight.net/templeton

    > [!NOTE]
    > Merhaba küme yönetici kullanıcı ve parola kullanarak kimlik doğrulaması.
    >
    > Kimlik doğrulama düz metin - kullanım HTTPS toohelp her zaman hello bağlantı güvenli olduğundan emin olun.

* **SSH** - &lt;clustername >-ssh.azurehdinsight.net bağlantı noktası 22 veya 23. Bağlantı noktası 22 kullanılan tooconnect toohello birincil headnode, açıkken kullanılan tooconnect toohello ikincil 23'tür. Merhaba baş düğümler hakkında daha fazla bilgi için bkz: [kullanılabilirliği ve güvenilirliği hadoop kümeleri Hdınsight'ta](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > Yalnızca bir istemci makinesinden SSH hello küme baş düğümler erişebilir. Bağlandıktan sonra daha sonra bir headnode SSH kullanarak hello çalışan düğümleri erişebilirsiniz.

## <a name="file-locations"></a>Dosya konumları

Hadoop ilgili dosyaları hello küme düğümlerinde bulunabilir `/usr/hdp`. Bu dizin alt dizinleri izleyen hello içerir:

* **2.2.4.9-1**: hello dizin adı sürümüdür hello hello Hortonworks veri platformu Hdınsight tarafından kullanılır. Kümenizde Hello sayı burada listelenen hello farklı olabilir.
* **Geçerli**: Bu dizin altında hello bağlantılar toosubdirectories içerir **2.2.4.9-1** dizini. Böylece tooremember hello sürüm numarası yoksa bu dizin zaten var.

Hadoop dağıtılmış dosya sistemi üzerinde örnek veriler ve JAR dosyalarını bulunabilir `/example` ve`/HdiSamples`

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, Azure depolama ve veri Gölü deposu

Çoğu Hadoop dağıtımları içinde HDFS hello kümedeki hello makinelerde yerel depolama birimi tarafından desteklenmektedir. Kullanarak yerel depolama burada saat veya dakika işlem kaynakları için ücretlendirilirsiniz için bir bulut tabanlı çözüm pahalı olabilir.

Hdınsight Azure Storage blobları ya da Azure Data Lake Store hello varsayılan deposu olarak kullanır. Bu hizmetler hello aşağıdaki avantajları sağlar:

* Ucuz uzun vadeli depolama
* Web siteleri, dosya karşıya yükleme/indirme yardımcı programlar, çeşitli dil SDK'lar ve web tarayıcıları gibi dış hizmetler erişilebilirlik

> [!WARNING]
> Hdınsight yalnızca destekler __genel amaçlı__ Azure depolama hesapları. Merhaba şu anda desteklemiyor __Blob storage__ hesap türü.

Tek tek bloblar (veya bir Hdınsight açısından dosyaları) too195 GB yalnızca gidebilirsiniz rağmen bir Azure Storage hesabı TB, too4.75 basılı tutabilirsiniz. Azure Data Lake Store, tek tek dosyaların bir petabyte büyük ile toohold trilyonlarca dosyalarının, dinamik olarak büyüyebilir. Daha fazla bilgi için bkz: [anlama BLOB'ları](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) ve [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Azure Storage veya Data Lake Store kullanılırken toodo Hdınsight tooaccess hello verileri özel bir şey yok. Örneğin, komutu aşağıdaki hello hello dosyalarında listeler `/example/data` olup Azure Storage veya Data Lake Store üzerinde depolandığı bağımsız olarak klasörü:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>URI ve düzeni

Bazı komutlar toospecify hello şema hello URI parçası olarak bir dosya erişirken gerektirebilir. Örneğin, hello Storm HDFS bileşen toospecify hello düzeni gerektirir. Varsayılan olmayan depolama ("ek" depolama alanı toohello kümesi olarak eklenen depolama alanı) kullanırken, hello URI bir parçası olarak her zaman hello şeması kullanması gerekir.

Kullanırken __Azure Storage__, URI şemaları aşağıdaki hello birini kullanın:

* `wasb:///`: Şifrelenmemiş iletişimi kullanarak erişim varsayılan depolama.

* `wasbs:///`: Şifreli iletişim kullanarak erişim varsayılan depolama.  Merhaba wasbs düzeni yalnızca Hdınsight sürüm 3.6 sonraki sürümlerde desteklenir.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: Bir varsayılan olmayan depolama hesabı ile iletişim kurarken kullanılır. Örneğin, bir ek depolama alanı hesabı veya ne zaman verilere genel olarak erişilebilir depolama hesabında depolanan olduğunda.

Kullanırken __Data Lake Store__, URI şemaları aşağıdaki hello birini kullanın:

* `adl:///`: Hello varsayılan Data Lake Store hello kümesi için erişim.

* `adl://<storage-name>.azuredatalakestore.net/`: Varsayılan olmayan Data Lake Store ile iletişim kurarken kullanılır. Ayrıca tooaccess veri Hdınsight kümenizin hello kök dizini dışındaki kullanılır.

> [!IMPORTANT]
> Data Lake Store Hdınsight için hello varsayılan deposu olarak kullanırken, Hdınsight depolama hello kök olarak hello deposu toouse içinde bir yol belirtmeniz gerekir. Merhaba varsayılan yolu `/clusters/<cluster-name>/`.
>
> Kullanırken `/` veya `adl:///` tooaccess veri hello kök dizininde depolanan veriler yalnızca erişebilir (örneğin, `/clusters/<cluster-name>/`) hello kümesi. Merhaba deposu, başka bir yerindeki tooaccess verileri kullanmak hello `adl://<storage-name>.azuredatalakestore.net/` biçimi.

### <a name="what-storage-is-hello-cluster-using"></a>Hangi depolama hello küme kullanıyor mu

Ambari tooretrieve hello varsayılan depolama yapılandırması hello küme için kullanabilirsiniz. Kullanım hello aşağıdaki komut curl kullanarak tooretrieve HDFS yapılandırma bilgilerini ve kullanarak filtre [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Bu hello ilk uygulanan yapılandırma toohello sunucusu döndürür (`service_config_version=1`), bu bilgiler içerir. Tüm yapılandırma sürümlerini toofind hello en son toolist gerekebilir.

Bu komut, URI'ler aşağıdaki değer benzer toohello döndürür:

* `wasb://<container-name>@<account-name>.blob.core.windows.net`bir Azure depolama hesabı kullanıyorsanız.

    Merhaba hesap adı hello hello Azure depolama hesabı adını, hello kapsayıcı adı hello blob kapsayıcısı olsa da, hello kök hello küme depolama.

* `adl://home`Azure Data Lake Store kullanıyorsanız. tooget hello Data Lake Store adı, REST çağrısı aşağıdaki hello kullan:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Bu komut, ana bilgisayar adından hello döndürür: `<data-lake-store-account-name>.azuredatalakestore.net`.

    Hdınsight, REST çağrısı aşağıdaki kullanım hello hello kök hello deposundaki tooget hello dizini:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Bu komut yolu izleyerek bir yolu benzer toohello döndürür: `/clusters/<hdinsight-cluster-name>/`.

Ayrıca hello aşağıdaki adımları kullanarak hello Azure portal kullanarak hello depolama bilgi bulabilirsiniz:

1. Merhaba, [Azure portal](https://portal.azure.com/), Hdınsight kümenize seçin.

2. Merhaba gelen **özellikleri** bölümünde, select **depolama hesapları**. Merhaba depolama bilgi hello küme için görüntülenir.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Dış Hdınsight'ta dosyaları nasıl erişirim

Dış hello Hdınsight kümesi tooaccess verileri çeşitli yolları vardır. Merhaba birkaç bağlantılar tooutilities ve verilerinizle kullanılan toowork olabilir SDK şunlardır:

Kullanıyorsanız __Azure Storage__, bağlantılar yolları verilerinize erişmek için aşağıdaki hello bakın:

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): komut satırı arabirimi komutları Azure ile çalışmak için. Yükledikten sonra hello kullan `az storage` depolama kullanma hakkında Yardım için komut veya `az storage blob` blob özgü komutlar için.
* [blobxfer.PY](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): bir python komut dosyası Azure depolama alanında BLOB'lar ile çalışmak için.
* Çeşitli SDK'lar:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [Depolama REST API’si](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Kullanıyorsanız __Azure Data Lake Store__, bağlantılar yolları verilerinize erişmek için aşağıdaki hello bakın:

* [Web tarayıcısı](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Azure CLI 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [WebHDFS REST API](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Visual Studio için Data Lake araçları](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Kümenizi ölçeklendirme

özellik ölçeklendirme hello küme toodynamically değişiklik hello bir küme tarafından kullanılan veri düğüm sayısını sağlar. Diğer işleri sırasında ölçeklendirme işlemleri gerçekleştirebilir veya işlemleri bir kümede çalışmıyor.

Merhaba farklı küme türü gibi ölçeklendirme tarafından etkilenir:

* **Hadoop**: hello kümedeki düğüm sayısını aşağı Ölçeklendirmesi, bazı hello kümedeki hello hizmetleri yeniden başlatılır. Operations ölçeklendirme işleri çalıştırma veya toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olabilir. Merhaba işlemi tamamlandıktan sonra hello işleri yeniden gönderebilirsiniz.
* **HBase**: bölgesel sunucular otomatik olarak hello ölçeklendirme işlemi tamamlandıktan sonra birkaç dakika içinde dengeli. toomanually Bakiye bölgesel sunucular, hello aşağıdaki adımları kullanın:

    1. SSH kullanarak toohello Hdınsight kümesine bağlanın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Toostart hello HBase Kabuğu'nu aşağıdaki hello kullan:

            hbase shell

    3. Merhaba HBase kabuğunu yüklendikten sonra toomanually Bakiye hello bölgesel sunucular aşağıdaki hello kullan:

            balancer

* **Storm**: bir ölçeklendirme işlemi gerçekleştirildikten sonra tüm çalışan Storm topolojileri yeniden dengelemeniz gerekir. Dengelenmesi hello topoloji tooreadjust paralellik ayarlarını hello yeni hello kümedeki düğüm sayısını temel sağlar. toorebalance çalışan topolojileri, aşağıdaki seçenekleri şu hello birini kullanın:

    * **SSH**: toohello sunucusuna bağlanmak ve kullanım hello şu komutu toorebalance bir topoloji:

            storm rebalance TOPOLOGYNAME

        Başlangıçta hello topolojisi tarafından sağlanan parametreleri toooverride hello paralellik ipuçları de belirtebilirsiniz. Örneğin, `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` hello topoloji too5 çalışan işlemleri, hello mavi spout bileşeni için 3 yürütücüler ve 10 yürütücüler hello sarı Cıvata bileşeni için yeniden yapılandırır.

    * **Storm kullanıcı Arabirimi**: kullanım hello aşağıdaki adımları toorebalance hello Storm kullanıcı arabirimini kullanarak bir topoloji.

        1. Açık **https://CLUSTERNAME.azurehdinsight.net/stormui** CLUSTERNAME Storm kümenizin hello adı olduğu için web tarayıcınızdaki. İstenirse, hello Hdınsight Küme Yöneticisi (Yönetici) adı ve hello küme oluştururken belirttiğiniz parolayı girin.
        2. Toorebalance istediğiniz sonra seçin hello hello topolojisini seçmenize **yeniden dengelemeniz** düğmesi. Merhaba yeniden dengeleyin işlem gerçekleştirilmeden önce hello gecikme girin.

Hdınsight kümenize ölçeklendirme ile ilgili ayrıntılı bilgi için bkz:

* [Hello Azure portal kullanarak hdınsight'ta Hadoop kümelerini yönetme](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Azure PowerShell kullanarak hdınsight'ta Hadoop kümelerini yönetme](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Hue (veya başka bir Hadoop bileşeni) nasıl yüklerim?

Hdınsight yönetilen bir hizmettir. Azure hello kümesi ile ilgili bir sorun algılarsa, bu düğüm başarısız hello silin ve bir düğüm tooreplace oluşturun. Merhaba kümede şeyler el ile yüklerseniz, bu işlemi oluştuğunda bunlar kalıcı değildir. Bunun yerine, kullanın [Hdınsight betik eylemleri](hdinsight-hadoop-customize-cluster.md). Betik eylemi kullanılan toomake hello aşağıdaki değişiklikler şunlar olabilir:

* Yükleyin ve bir hizmeti veya web sitesi Spark veya ton gibi yapılandırın.
* Yükleme ve yapılandırma değişikliklerini hello kümedeki birden çok düğümde gerektiren bir bileşen yapılandırın. Gerekli ortam değişkeni, bir günlük dizini veya bir yapılandırma dosyası oluşturulmasını oluşturuluyor.

Betik eylemleri Bash betikleridir. Merhaba betikleri küme hazırlama sırasında çalıştırmak ve kullanılan tooinstall olması ve hello kümede ek bileşenleri yapılandırın. Örnek betikler hello aşağıdaki bileşenleri yüklemek için sağlanmıştır:

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Kendi Betik Eylemlerinizi geliştirme hakkında daha fazla bilgi için bkz. [HDInsight ile Betik Eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).

### <a name="jar-files"></a>Jar dosyaları

Bazı Hadoop teknolojiler bir MapReduce işi ya da bir parçası olarak kullanılan işlevler içeren müstakil jar dosyalarını sağlanan Pig veya Hive içinde. Bu betik eylemleri kullanılarak yüklenebilir, ancak bunlar genellikle herhangi bir ayar gerektirmez ve karşıya yüklenen toohello küme sağladıktan sonra olabilir ve doğrudan kullanılacaktır. Merhaba kümesini yeniden görüntüsünü oluşturuyor toomake emin hello bileşen şekilde kalmıştır istiyorsanız, küme için (WASB veya ADL) hello varsayılan depolama hello jar dosyasını depolayabilirsiniz.

Örneğin, toouse hello en son sürümünü istiyorsanız [DataFu](http://datafu.incubator.apache.org/), Merhaba projeyi içeren jar indirin ve toohello Hdınsight kümesi yükleyin. Ardından hello DataFu belgeleri nasıl izleyin toouse Pig veya Hive.

> [!IMPORTANT]
> Tek başına jar dosyalarını olan bazı bileşenleri Hdınsight ile sağlanır, ancak hello yolunda değildir. Belirli bir bileşen için arıyorsanız, kümenizde için hello izleyin toosearch kullanabilirsiniz:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Bu komut tüm eşleşen jar dosyalarını hello yolunu döndürür.

toouse bir bileşeni gerekir ve işlerinizde kullanabilirsiniz karşıya yükleme hello sürüm farklı bir sürümü.

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support tooisolate yardımcı olur ve sorunları ilgili toothese bileşenler çözümlenemiyor.
>
> Özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Merhaba sorunu çözmek veya tooengage kullanılabilir kanalları hello için bu teknoloji derin uzmanlık bulunduğu kaynak teknolojileri açtığınız isteyen neden olabilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Sonraki adımlar

* [Windows tabanlı Hdınsight tooLinux tabanlı geçirme](hdinsight-migrate-from-windows-to-linux.md)
* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [HDInsight ile MapReduce işleri kullanma](hdinsight-use-mapreduce.md)
