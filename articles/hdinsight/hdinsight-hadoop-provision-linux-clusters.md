---
title: "Hadoop, Spark, Kafka, HBase veya R Server - Azure Hdınsight için aaaCluster Kurulumu | Microsoft Docs"
description: "Hadoop, Kafka, Spark, HBase, R Server veya Storm kümelerini Hdınsight için bir tarayıcı, hello Azure CLI, Azure PowerShell, REST veya SDK ayarlayın."
keywords: "hadoop kümesi kurulumu, kafka Küme kurulumu, spark Küme kurulumu, hadoop kümesinde nedir"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Hdınsight Hadoop, Spark, Kafka ve daha fazla ile kümelerde ayarlama

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Bilgi nasıl tooset ayarlama ve kümeleri Hdınsight Hadoop, Spark, Kafka, etkileşimli Hive, HBase, R Server veya Storm ile yapılandırın. Ayrıca, nasıl toocustomize kümeleri öğrenin ve güvenlik tooa etki alanına katılma olarak ekleyin.

Hadoop kümesi birkaç sanal makinelerin görevleri dağıtılmış işlem için kullanılan (düğümler) oluşur. Bu nedenle yalnızca tooprovide genel yapılandırma bilgilerini zorunda azure Hdınsight uygulama ayrıntıları yükleme ve yapılandırma tek tek düğümlerinin işler. 

> [!IMPORTANT]
>Hdınsight küme faturalandırma bir küme oluşturulur ve hello küme silindiğinde durdurur sonra başlar. Artık kullanımda olmadığında, küme her zaman silmelisiniz Faturalaması dakika başına Faturalaması olduğundan. Nasıl çok öğrenin[bir küme silin.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Küme kurulumu yöntemleri
Merhaba aşağıdaki tabloda hello farklı yöntemler tooset bir Hdınsight kümesi kullanabileceğiniz gösterilmektedir.

| Oluşturulan kümeleri | Web tarayıcısı | Komut satırı | REST API | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Azure portal](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Azure Resource Manager şablonları](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Hızlı oluştur: temel Küme kurulumu
Bu makalede, hello kurulumunda anlatılmaktadır [Azure portal](https://portal.azure.com), bir Hdınsight kümesi kullanarak oluşturabileceğiniz *hızlı Oluştur* veya *özel*. 

Merhaba ekranında toodo temel Küme kurulumu üzerinde yönergeleri izleyin. Ayrıntılar için aşağıda verilmiştir:

* [Kaynak grubu adı](#resource-group-name)
* [Küme türleri ve yapılandırma](#cluster-types) 
* [Küme oturum açma ve SSH kullanıcı adı](#cluster-login-and-ssh-username)
* [Konum](#location)

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight 3.3 devre dışı bırakma](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Kaynak grubu adı 

[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) çalışma hello kaynaklarla bir grup, başvurulan tooas olarak bir Azure kaynak grubu yardımcı olur. Dağıtma, güncelleştirme, izlemek veya uygulamanızın tek ve eşgüdümlü bir işlemde tüm hello kaynakları silin.

## <a name="cluster-types"></a>Küme türleri ve yapılandırma
Azure Hdınsight şu anda hello aşağıdaki türleri, her bir dizi bileşenleri tooprovide belirli işlevlerin küme sağlar.

> [!IMPORTANT]
> Hdınsight kümeleri, her bir tek iş yükü veya teknoloji için çeşitli türlerde kullanılabilir. Bir küme üzerinde Storm ve HBase gibi birden çok tür birleştiren bir küme için desteklenen yöntem toocreate yoktur. Çözümünüzün birden çok Hdınsight küme türleri arasında yayılır teknolojileri gerektiriyorsa bir [Azure sanal ağı](https://docs.microsoft.com/azure/virtual-network) gerekli hello küme türleri bağlanabilir. 
>
>

| Küme türü | İşlev |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Toplu sorgu ve depolanan veri analizi |
| [HBase](hdinsight-hbase-overview.md) |Büyük miktarlarda şemasız, NoSQL veri işleme |
| [Storm](hdinsight-storm-overview.md) |Gerçek zamanlı olay işleme |
| [Spark](hdinsight-apache-spark-overview.md) |Bellek içi işleme, etkileşimli sorgular mikro toplu iş akışı işleme |
| [Kafka (Önizleme)](hdinsight-apache-kafka-introduction.md) | Kullanılan toobuild gerçek zamanlı akış veri ardışık ve uygulamaları dağıtılmış bir akış platformu |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Çeşitli büyük veri istatistikleri, Tahmine dayalı modelleme ve makine öğrenimi özellikleri |
| [Etkileşimli Hive (Önizleme)](hdinsight-hadoop-use-interactive-hive.md) |Etkileşimli ve daha hızlı Hive sorguları için bellek içi önbelleğe alma |

### <a name="number-of-nodes-for-each-cluster-type"></a>Her küme türü için düğüm sayısı
Her küme türü düğümleri, düğümleri ve varsayılan VM boyutu terminolojisi kendi sayısına sahip. Aşağıdaki tablonun hello hello düğümleri her düğüm türü için parantez içinde sayısıdır.

| Tür | Düğümler | Diyagram |
| --- | --- | --- |
| Hadoop |Baş düğümü (2) veri düğümü (1 +) |![Hdınsight Hadoop küme düğümleri](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |HEAD sunucusu (2), bölge (1 +), ana/ZooKeeper düğümü (3) |![Hdınsight HBase küme düğümleri](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nimbus düğümü (2), yönetici sunucu (1 +), ZooKeeper düğümü (3) |![Hdınsight Storm küme düğümleri](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Baş düğümü (2), çalışan düğümüne (1 +), ZooKeeper düğümü (3) (A1 ZooKeeper VM boyutu için boş) |![Hdınsight Spark küme düğümleri](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Daha fazla bilgi için bkz: [varsayılan düğümü yapılandırması ve sanal makine boyutları kümeleri için](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) "Merhaba Hadoop bileşenleri ve Hdınsight sürümlerde nedir?",

### <a name="hdinsight-version"></a>Hdınsight sürümü
Bu küme için Hdınsight Hello sürümünü seçin. Daha fazla bilgi için bkz: [desteklenen Hdınsight sürümleri](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Küme katmanı: Hdınsight hizmet katmanları

Azure Hdınsight iki hizmet katmanları hello büyük veri Bulutu teklifleri sunar: standart ve Premium.  Daha fazla bilgi için bkz: [Hdınsight standart ve Hdınsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Merhaba aşağıdaki ekran görüntüsü hello küme türü seçme Azure portalı bilgileri gösterir.

![Hdınsight premium yapılandırma](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Küme oturum açma ve SSH kullanıcı adı
Hdınsight kümeleri ile küme oluşturma sırasında iki kullanıcı hesapları yapılandırabilirsiniz:

* HTTP kullanıcı: hello varsayılan kullanıcı adı *yönetici*. Hello Azure portalı üzerinde hello temel yapılandırmasını kullanır. Bazen "kullanıcı küme." çağrılır
* SSH kullanıcı (Linux kümeleri): SSH aracılığıyla kullanılan tooconnect toohello kümesi. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Kümeleri ve depolama için konum (bölge)

Toospecify hello küme konumu açıkça gerekmez: hello kümedir hello hello varsayılan depolama ile aynı konumda. Desteklenen bölgelerin bir listesi için hello tıklatın **bölge** aşağı açılan listede [Hdınsight fiyatlandırma](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Küme için depolama uç noktaları

Hadoop şirket içi yüklemesini hello kümesindeki depolama için hello Hadoop dağıtılmış dosya sistemi (HDFS) kullansa da, hello depolama uç noktaları kullandığınız bulut toocluster bağlı. Hdınsight kümeleri kullanın ya da [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) veya [Azure Storage blobları](hdinsight-hadoop-use-blob-storage.md). Azure Storage veya Data Lake Store kullanarak, verilerinizi bekletirken hesaplama için kullanılan hello Hdınsight kümeleri silebileceğiniz anlamına gelir. 

> [!WARNING]
> Merhaba Hdınsight kümesinden farklı bir konumda bir ek depolama alanı hesabı kullanarak desteklenmiyor.

Yapılandırması sırasında hello varsayılan depolama uç noktası için bir Azure Storage hesabı veya bir Data Lake Store bir blob kapsayıcısını belirtin. Merhaba varsayılan depolama uygulama ve sistem içeren günlükleri. İsteğe bağlı olarak, ek bağlı Azure Storage hesaplarını ve küme hello Data Lake Store hesapları erişebilmeniz için belirtebilirsiniz. Merhaba Hdınsight kümesi ve hello bağımlı depolama hesapları olmalıdır aynı Azure konumuna hello.

![Küme depolama ayarları: HDFS uyumlu depolama uç noktaları](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>İsteğe bağlı meta deponuz
İsteğe bağlı Hive veya Oozie meta depolar oluşturabilirsiniz. Ancak, tüm küme türleri meta deponuz desteklemez ve Azure SQL Data Warehouse meta deponuz ile uyumlu değil. 

> [!IMPORTANT]
> Özel bir meta depo oluşturduğunuzda, kısa çizgiler, kısa çizgi veya hello veritabanı adında boşluk kullanmayın. Bu hello küme oluşturma işlemi toofail neden olabilir.

### <a name="use-hiveoozie-metastore"></a>Hive meta depo

Hdınsight kümesi silindikten sonra Hive tablolarını tooretain istiyorsanız, özel bir meta depo kullanın. Ardından, hello meta depo tooanother Hdınsight küme de ekleyebilirsiniz.

Bir Hdınsight kümesi sürüm oluşturulan Hdınsight meta depo farklı Hdınsight küme sürümleri arasında paylaşılamaz. Hdınsight sürümlerinin listesi için bkz: [desteklenen Hdınsight sürümleri](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Oozie meta depo

Oozie, kullanırken tooincrease performans özel bir meta depo kullanın. Kümenizi sildikten sonra bir meta depo erişim tooOozie iş verilerini de sağlayabilirsiniz. 

> [!IMPORTANT]
> Özel bir Oozie meta depo tekrar kullanamazsınız. özel bir Oozie meta depo toouse, boş bir Azure SQL veritabanı hello Hdınsight kümesi oluştururken sağlamanız gerekir.

## <a name="configure-cluster-size"></a>Küme boyutunu yapılandırın

Merhaba küme var olduğu sürece için düğüm kullanım için faturalandırılır. Bir küme oluşturulur ve hello küme silindiğinde durdurduğunda faturalama başlatır. Kümeleri XML'deki ayrıldı veya beklemeye.

Hdınsight kümeleri Hello maliyetini düğümleri hello sanal makineler için ve boyutları hello düğümleri hello sayısı tarafından belirlenir. 

Farklı küme türü farklı düğüm türleri, düğümleri ve düğümü boyutları sayısı vardır:
* Hadoop küme türü varsayılan: 
    * İki *baş düğümler*  
    * Dört *veri düğümler*
* Storm kümesi türü varsayılan: 
    * İki *Nimbus düğümü*
    * Üç *ZooKeeper düğümleri*
    * Dört *yönetici düğümler* 

Yalnızca Hdınsight çalışıyorsanız, bir veri düğümü kullanmanızı öneririz. Hdınsight fiyatlandırma hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> Hello küme boyutu Azure abonelikleri arasında değişiklik gösterir. Kişi [Azure Fatura Desteği](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello sınırı.
>

Hello Azure portal tooconfigure hello küme kullandığınızda hello düğüm boyutu hello kullanılabilir **düğüm fiyatlandırma katmanları** dikey. Merhaba Portalı'nda da görebilirsiniz hello hello farklı düğümü boyutları ile ilişkili maliyeti. 

![Hdınsight VM düğümü boyutları](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Sanal makine boyutları 
Kümeleri dağıttığınızda, temel bilgi işlem kaynakları seçin. hello çözüm üzerinde toodeploy planlayın. Merhaba aşağıdaki VM'ler Hdınsight kümeleri için kullanılır:
* A ve D1 4 serisi VMs: [genel amaçlı Linux VM boyutları](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* D11-14 serisi VM: [bellek için iyileştirilmiş Linux VM boyutları](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

hangi değerin çıkışı toofind kullanarak bir küme oluşturma sırasında bir VM boyutu farklı SDK'ları hello veya Azure PowerShell kullanırken, bkz. toospecify kullanması gereken [VM boyutları Hdınsight kümeleri toouse](../cloud-services/cloud-services-sizes-specs.md#size-tables). Bu bağlantılı makaleden hello değeri hello kullanın **boyutu** Merhaba tablonun sütun.

> [!IMPORTANT]
> Bir kümede 32'den fazla alt düğüm gerekirse, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB RAM ile seçmeniz gerekir.
>
>

Daha fazla bilgi için bkz: [sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md). Merhaba çeşitli boyutlarda fiyatlandırma hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Özel küme Kurulumu
Özel küme Kurulumu derlemelerinde hello hızlı ayarlarını oluşturun ve aşağıdaki seçenekleri şu hello ekler:
- [Hdınsight uygulamaları](#hdinsight-applications)
- [Küme boyutu](#cluster-size)
- Gelişmiş ayarlar
  - [Betik eylemleri](#customize-clusters-using-script-action)
  - [Sanal ağ](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Kümelere HDInsight uygulamaları yükleme

HDInsight uygulaması kullanıcıların Linux tabanlı HDInsight kümesine yükleyebileceği bir uygulamadır. Microsoft, üçüncü tarafların veya, kendi ürettiğiniz sağlanan uygulamaları kullanabilir. Daha fazla bilgi için bkz: [Azure Hdınsight'ta üçüncü taraf Hadoop uygulamaları yükleme](hdinsight-apps-install-applications.md).

Merhaba Hdınsight uygulamalarının çoğunu bir boş kenar düğümüne yüklenir.  Linux sanal makineyle aynı istemci araçları yüklü ve yapılandırılmış olduğu gibi hello baş düğüm hello bir boş kenar düğümdür. Merhaba kenar düğümüne hello küme erişmek, istemci uygulamalarınızı test etme ve istemci uygulamalarını barındırmak için kullanabilirsiniz. Daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Gelişmiş ayarlar: betik eylemleri

Ek bileşenleri yüklemek veya oluşturma sırasında komut dosyalarını kullanarak küme yapılandırmasını özelleştirebilirsiniz. Bu tür komut dosyaları aracılığıyla çağrılır **betik eylemi**, hello Azure portal, Hdınsight Windows PowerShell cmdlet'lerini veya Hdınsight .NET SDK'sı hello kullanılabilir bir yapılandırma seçeneği değil. Daha fazla bilgi için bkz: [betik eylemi kullanarak özelleştirme Hdınsight kümesi](hdinsight-hadoop-customize-cluster-linux.md).

Mahout ve basamaklama, gibi yerel bazı Java bileşenleri hello kümede Java arşiv (JAR) dosyaları olarak çalıştırabilirsiniz. Bu JAR dosyalarını dağıtılmış tooAzure depolama olabilir ve Hadoop iş gönderme mekanizmalarıyla tooHDInsight kümeleri gönderildi. Daha fazla bilgi için bkz: [gönderme Hadoop işleri program aracılığıyla](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> JAR dosyalarını tooHDInsight kümelerini dağıtma sorunları varsa veya Hdınsight kümelerinde JAR dosyalarını çağırma başvurun [Microsoft Support](https://azure.microsoft.com/support/options/).
>
> Geçişli Hdınsight tarafından desteklenmiyor ve Microsoft Support uygun değil. Desteklenen bileşenlerin bir listesi için bkz: [Hdınsight tarafından sağlanan hello küme sürümlerindeki yenilikler](hdinsight-component-versioning.md).
>
>

Bazı durumlarda, aşağıdaki yapılandırma dosyaları hello oluşturma işlemi sırasında tooconfigure hello istiyor:

* clusterIdentity.xml
* Core-site.xml
* Gateway.XML
* hbase env.xml
* hbase-site.xml
* hdfs-site.xml
* Hive env.xml
* Hive-site.xml
* mapred site
* oozie-site.xml
* oozie env.xml
* Storm-site.xml
* Tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Daha fazla bilgi için bkz: [önyükleme kullanarak özelleştirme Hdınsight kümelerini](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Gelişmiş ayarlar: sanal ağ kümeleriyle genişletme
Çözümünüzün birden çok Hdınsight küme türleri arasında yayılır teknolojileri gerektiriyorsa bir [Azure sanal ağı](https://docs.microsoft.com/azure/virtual-network) gerekli hello küme türleri bağlanabilir. Bu yapılandırma izin veren hello kümeleri ve toothem dağıttığınız herhangi bir kod toodirectly birbiriyle.

Hdınsight ile Azure sanal ağı kullanma hakkında daha fazla bilgi için bkz: [genişletmek Hdınsight Azure sanal ağlar ile](hdinsight-extend-hadoop-virtual-network.md).

Bir Azure sanal ağı içindeki iki küme türleri kullanma örneği için bkz: [Storm ve HBase ile algılayıcı verilerini çözümleme](hdinsight-storm-sensor-data-analysis.md). Hdınsight hello sanal ağ için belirli yapılandırma gereksinimlerini içeren bir sanal ağ ile kullanma hakkında daha fazla bilgi için bkz: [Azure Virtual Network kullanarak genişletme Hdınsight yetenekleri](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Erişim denetimi sorunlarını giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar

- [Hdınsight, hello Hadoop ekosistemi ve Hadoop kümeleri nelerdir?](hdinsight-hadoop-introduction.md)
- [HDInsight'ta Hadoop kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Bir Windows PC Hdınsight'ta Hadoop ile çalışma](hdinsight-hadoop-windows-tools.md)
