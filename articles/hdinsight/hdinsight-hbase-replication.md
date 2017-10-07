---
title: "sanal ağlar - Azure içinde aaaConfigure HBase kümesi çoğaltma | Microsoft Docs"
description: "Bilgi nasıl tooconfigure HBase çoğaltmayı Yük Dengeleme, yüksek kullanılabilirlik, sıfır kapalı kalma süresi geçiş/güncelleştirme bir Hdınsight sürüm tooanother ve olağanüstü durum kurtarma."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>Sanal ağlar içinde HBase kümesi çoğaltma yapılandırma

Bilgi nasıl tooconfigure HBase çoğaltmayı bir sanal ağ (VNet) içinde ya da iki sanal ağ arasında.

Küme çoğaltma, bir kaynak itme Metodoloji kullanır. Her iki rolleri aynı anda gerçekleştirebilir veya bir kaynak veya hedef bir HBase kümesi olabilir. Çoğaltma uyumsuzdur ve hello çoğaltma nihai tutarlılık hedefidir. Merhaba kaynak çoğaltmanın etkinleştirilmiş olduğu bir düzenleme tooa sütun ailesi aldığında, bu düzenleme yayılan tooall hedef küme sayısıdır. Bir küme tooanother veri çoğaltıldığında hello kaynak kümesi ve hello veri zaten tüketilen tüm kümeleri izlenen tooprevent çoğaltma döngüleri var.

Bu öğreticide, bir kaynak hedef çoğaltma yapılandırır. Diğer küme Topolojileri için bkz: [Apache HBase Başvuru Kılavuzu](http://hbase.apache.org/book.html#_cluster_replication).

HBase çoğaltma kullanım durumları tek bir sanal ağ için:

* --Örneğin, tarama veya MapReduce işleri hello hedef küme üzerinde çalışan ve veri hello kaynak kümesi alma Yük Dengeleme
* Yüksek kullanılabilirlik
* Bir HBase kümesi tooanother gelen verileri geçirme
* Azure Hdınsight kümesi bir sürüm tooanother yükseltme

HBase çoğaltma kullanım durumları iki sanal ağ için:

* Olağanüstü durum kurtarma
* Yük Dengeleme ve Merhaba uygulaması bölümlendirme
* Yüksek kullanılabilirlik

Kümeleri kullanarak çoğaltma [betik eylemi](hdinsight-hadoop-customize-cluster-linux.md) betikleri bulunan [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="configure-hello-environments"></a>Merhaba ortamları yapılandırma

Üç olası yapılandırmaları vardır:

- Bir Azure sanal ağı iki HBase kümelerini
- Aynı bölge içinde iki farklı sanal ağlar iki HBase kümelerini hello
- İki HBase kümelerini iki farklı bölgelerde (coğrafi çoğaltma) iki farklı sanal ağlar

toomake bunu daha kolay tooconfigure hello ortamları oluşturduğumuz bazı [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-overview.md). Diğer yöntemleri kullanarak tooconfigure hello ortamları tercih ederseniz, bkz:

- [Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md)
- [Azure sanal ağında HBase kümeleri oluşturma](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>Bir sanal ağ yapılandırma

Merhaba görüntü toocreate iki HBase kümelerini aşağıdaki hello tıklatın aynı sanal ağ. Merhaba şablon depolanır [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>Hello iki sanal ağ yapılandırma aynı bölge

Görüntü toocreate iki sanal ağ VNet eşlemesi ve hello iki HBase kümeleri ile aşağıdaki hello tıklatın aynı bölgede. Merhaba şablon depolanır [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



Bu senaryo gerektirir [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md). VNet eşlemesi Hello şablonu sağlar.   

HBase çoğaltmayı hello ZooKeeper VM'ler IP adreslerini kullanır. Merhaba hedef HBase ZooKeeper düğümleri için statik IP adresi yapılandırmanız gerekir.

**tooconfigure statik IP adresleri**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba sol menüden **kaynak grupları**.
3. Merhaba hedef HBase kümesi içeren kaynak grubunuz'ı tıklatın. Merhaba Resource Manager şablonu toocreate hello ortamı kullanıldığında, belirttiğiniz hello kaynak grubu budur. Merhaba filtre toonarrow hello listesini aşağı kullanabilirsiniz. Merhaba iki sanal ağ içeren kaynakların bir listesini görebilirsiniz.
4. Merhaba hedef HBase kümesi içeren hello sanal ağ'ı tıklatın. Örneğin, **xxxx-vnet2'yi**. İle başlayan üç aygıtlarla adlarını görebilirsiniz **NIC-zookeepermode -**. Bu cihazların Merhaba üç ZooKeeper VM'ler ' dir.
5. Merhaba ZooKeeper VM'ler birini tıklatın.
6. Tıklatın **IP yapılandırmaları**.
7. Tıklatın **ipConfig1** hello listeden.
8. Tıklatın **statik**ve hello gerçek IP adresini yazın. Merhaba betik eylemi tooenable çoğaltma çalıştırdığınızda, başlangıç IP adresi gerekir.

  ![Hdınsight HBase çoğaltma ZooKeeper statik IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. Adım 6 tooset hello statik IP adresi, diğer iki ZooKeeper düğümleri hello için yineleyin.

Merhaba arası VNet senaryosu için hello kullanmalısınız **- IP** hello çağrılırken geçiş **hdi_enable_replication.sh** betik eylemi.

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>İki farklı bölgelerde iki sanal ağ yapılandırma

Görüntü toocreate iki sanal ağ iki farklı bölgelerdeki aşağıdaki hello'ı tıklatın. Merhaba şablonu bir ortak Azure Blob kapsayıcısında depolanır.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

Merhaba iki sanal ağ arasında bir VPN ağ geçidi oluşturun. Yönergeler için bkz: [bir siteden siteye bağlantısı olan bir VNet oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

HBase çoğaltmayı hello ZooKeeper VM'ler IP adreslerini kullanır. Merhaba hedef HBase ZooKeeper düğümleri için statik IP adresi yapılandırmanız gerekir. statik IP tooconfigure, bu makaledeki hello "yapılandırma iki sanal ağlarda aynı bölgede hello" bölümüne bakın.

Merhaba arası VNet senaryosu için hello kullanmalısınız **- IP** hello çağrılırken geçiş **hdi_enable_replication.sh** betik eylemi.

## <a name="load-test-data"></a>Yük testi verileri

Bir küme çoğalttığınızda, hello tabloları tooreplicate belirtmeniz gerekir. Bu bölümde, bazı veriler hello kaynak kümesine yükler. Merhaba sonraki bölümde hello iki küme arasında çoğaltmayı etkinleştirir.

Merhaba yönergeleri izleyin [HBase Öğreticisi: hdınsight'ta Linux tabanlı Hadoop ile Apache HBase kullanmaya başlamanıza](hdinsight-hbase-tutorial-get-started-linux.md) toocreate bir **kişiler** tablo ve bazı verileri hello tabloya ekleyin.

## <a name="enable-replication"></a>Çoğaltmayı etkinleştirme

Aşağıdaki adımları hello nasıl toocall hello betik eylemi hello Azure portal betikten gösterir. Azure PowerShell ve hello Azure komut satırı arabirimi (CLI) kullanarak bir komut dosyası eylemi çalıştırmak için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).

**tooenable HBase çoğaltmayı hello Azure portalı**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba kaynak HBase kümesi'ni açın.
3. Merhaba küme menüden **betik eylemleri**.
4. Tıklatın **gönderme yeni** hello dikey hello üstten.
5. Aşağıdaki bilgilerle hello girin veya seçin:

  - **Ad**: girin **çoğaltmasını etkinleştir**.
  - **Komut dosyası URL'si bash**: girin **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.
  - **HEAD**: Seçili. Clear diğer düğüm türleri hello.
  - **Parametreleri**: hello aşağıdaki örnek parametreleri tüm hello varolan tablolar için çoğaltma etkinleştirme ve tüm hello veri hello kaynak küme toohello hedef kümeden kopyalayın:

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. **Oluştur**'a tıklayın. Merhaba betik biraz zaman alabilir özellikle zaman hello - copydata bağımsız değişkeninin değeri kullanılır.

Gerekli bağımsız değişkenler:

|Ad|Açıklama|
|----|-----------|
|-s--src-küme | Merhaba kaynak HBase kümesi Hello DNS adını belirtin. Örneğin: -s hbsrccluster,--src küme hbsrccluster = |
|-d--dst küme | Merhaba hedef (Çoğaltma) HBase kümesi Hello DNS adını belirtin. Örneğin: -s dsthbcluster,--src küme dsthbcluster = |
|-sp,--src ambari parolası | Merhaba yönetici parolası için Ambari hello kaynak HBase kümesi üzerinde belirtin. |
|-dp,--dst ambari parolası | Merhaba yönetici parolası için Ambari hello hedef HBase kümesi üzerinde belirtin.|

İsteğe bağlı bağımsız değişkenler:

|Ad|Açıklama|
|----|-----------|
|-su,--src ambari kullanıcı | Merhaba yönetici kullanıcı için Ambari hello kaynak HBase kümesi üzerinde belirtin. Merhaba varsayılan değer **yönetici**. |
|-du,--dst ambari kullanıcı | Merhaba yönetici kullanıcı için Ambari hello hedef HBase kümesi üzerinde belirtin. Merhaba varsayılan değer **yönetici**. |
|-t,--Tablo listesi | Çoğaltılan hello tabloları toobe belirtin. Örneğin: – Tablo listesi = "tablo1; tablo2; Tablo3". Tabloları belirtmezseniz, tüm var olan HBase tablolarını çoğaltılır.|
|-m,--makine | Merhaba betik eylemi çalıştırılacağı hello baş düğüm belirtin. Merhaba hn1 veya hn0 değerdir. Hn0 genellikle yoğun olduğundan hn1 kullanmanızı öneririz. Merhaba $0 betik hello Hdınsight portal ya da Azure PowerShell betik eylemi çalıştırıyorsanız bu seçeneği kullanın.|
|-IP | İki sanal ağ arasında çoğaltmayı etkinleştirirken bu bağımsız değişkeni gereklidir. Bir anahtar toouse hello statik IP, ZooKeeper çoğaltma küme düğümü FQDN adları yerine bu bağımsız değişken görür. Merhaba statik IP çoğaltma etkinleştirmeden önce önceden yapılandırılmış toobe gerekir. |
|-TP, - copydata | Çoğaltma etkinleştirdiğiniz hello tablolarda varolan verilerin Hello geçişi etkinleştirin. |
|-rpm, - replicate-phoenix-meta | Phoenix Sistem tabloları çoğaltmayı etkinleştirin. <br><br>*Bu seçeneği dikkatli kullanın.* Bu komut dosyasını kullanmadan önce çoğaltma kümeleri Phoenix tablolarda yeniden oluşturmanızı öneririz. |
|-h,--Yardım | Kullanım bilgilerini görüntüler. |

Merhaba hello print_usage() bölümünü [betik](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) parametreleri ayrıntılı bir açıklamasını sağlar.

Merhaba betik eylemi başarıyla tamamlandıktan sonra dağıtılmış, size SSH tooconnect toohello hedef HBase kümesi, kullanıp hello veri çoğaltıldığını doğrulayın.

### <a name="replication-scenarios"></a>Çoğaltma senaryoları

Merhaba aşağıdaki listede, bazı genel kullanım örnekleri ve parametre ayarlarına gösterir:

- **Tüm tablolarda hello iki küme arasında çoğaltmayı etkinleştirmek**. Bu senaryo hello Kopyala/hello tablolarda mevcut verilerin geçişini gerektirmez ve Phoenix tabloları kullanmaz. Şu parametreler hello kullan:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **Belirli tablolarda çoğaltmayı etkinleştirme**. Tablo1, tablo2 ve Tablo3 parametreleri tooenable çoğaltma aşağıdaki hello kullan:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **Belirli tablolarda çoğaltmayı etkinleştirmek ve hello mevcut veri kopyalama**. Tablo1, tablo2 ve Tablo3 parametreleri tooenable çoğaltma aşağıdaki hello kullan:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **Phoenix meta veri kaynağı toodestination çoğaltma ile tüm tablolarda çoğaltmayı etkinleştirme**. Phoenix meta veri çoğaltma kusursuz değildir ve dikkatli bir şekilde etkinleştirilmiş olmalıdır.

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>Kopyalama ve verileri geçirme

Kopyalama ve taşıma için iki ayrı komut dosyası eylemi betikleri vardır çoğaltma etkinleştirildikten sonra verileri:

- [Küçük tablolar için komut dosyası](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (birkaç gigabayttan boyut ve genel kopyasında olduğu beklenen toofinish bir saatten kısa bir süre içinde)

- [Büyük tablolar için komut dosyası](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (beklenen tootake bir saat toocopy uzun)

İzleyebileceğiniz hello aynı yordamda [çoğaltmasını etkinleştir](#enable-replication) toocall hello betik eylemi şu parametreler hello ile:

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

Merhaba hello print_usage() bölümünü [betik](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) parametreleri ayrıntılı bir açıklaması verilmiştir.

### <a name="scenarios"></a>Senaryolar

- **Şimdi düzenlenen tüm satırlar için belirli tabloları (test1, test2 ve test3) kopyalayın (geçerli zaman damgası)**:

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  or

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **Belirtilen zaman aralığı belirli tablolarla kopyalama**:

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>Çoğaltma devre dışı bırak

toodisable çoğaltma konumunda bulunan başka bir komut dosyası eylemi komut dosyasını kullanın [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh). İzleyebileceğiniz hello aynı yordamda [çoğaltmasını etkinleştir](#enable-replication) toocall hello betik eylemi şu parametreler hello ile:

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

Merhaba hello print_usage() bölümünü [betik](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) parametreleri ayrıntılı bir açıklamasını sağlar.

### <a name="scenarios"></a>Senaryolar

- **Çoğaltma tüm tablolarda devre dışı**:

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  or

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **Çoğaltmayı belirtilen tablolarda (tablo1, tablo2 ve Tablo3) devre dışı**:

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, nasıl öğrenilen tooconfigure HBase çoğaltmayı iki veri merkezi arasında. Hdınsight ve HBase, hakkında daha fazla toolearn bakın:

* [Hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started]
* [Hdınsight Hbase'e genel bakış][hdinsight-hbase-overview]
* [Azure sanal ağında HBase kümeleri oluşturma][hdinsight-hbase-provision-vnet]
* [HBase ile Twitter düşüncelerini gerçek zamanlı analiz][hdinsight-hbase-twitter-sentiment]
* [Storm ve HBase hdınsight'ta (Hadoop) ile sensör verilerini analiz etme][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
