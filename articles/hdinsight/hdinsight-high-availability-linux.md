---
title: "Hadoop - Azure Hdınsight için aaaHigh kullanılabilirlik | Microsoft Docs"
description: "Nasıl Hdınsight kümeleri güvenilirlik ve kullanılabilirlik ek bir baş düğüm kullanarak iyileştirmek öğrenin. Tooindividually bağlanmak tooeach baş düğüm SSH kullanarak nasıl bu Ambari ve Hive gibi Hadoop hizmetleri nasıl etkilediğini de öğrenin."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "hadoop yüksek kullanılabilirlik"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>HDInsight'ta Hadoop kümelerinin kullanılabilirliği ve güvenilirliği

Hdınsight kümeleri iki baş düğümler tooincrease hello kullanılabilirliği ve güvenilirliği Hadoop Hizmetleri ve çalışan işlerin sağlar.

Hadoop bir kümede birden çok düğüm arasında Hizmetleri ve veri çoğaltma tarafından yüksek kullanılabilirlik ve güvenilirlik elde eder. Ancak standart dağıtımları hadoop genellikle yalnızca tek bir baş düğüm vardır. Merhaba tek baş düğümü herhangi kesinti hello küme toostop çalışma neden olabilir. Hdınsight iki headnodes tooimprove Hadoop'ın kullanılabilirliği ve güvenilirliği sağlar.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="availability-and-reliability-of-nodes"></a>Kullanılabilirliği ve güvenilirliği düğümlerinin

Hdınsight kümesi düğümünde, Azure sanal makineleri kullanarak uygulanır. Merhaba aşağıdaki bölümlerde Hdınsight ile kullanılan hello tek tek düğüm türleri açıklanmaktadır. 

> [!NOTE]
> Tüm düğüm türleri için bir küme türü kullanılır. Örneğin, Hadoop küme türü hiçbir Nimbus düğümü yok. Hdınsight küme türleri tarafından kullanılan düğümleri hakkında daha fazla bilgi için hello hello küme türleri bölümüne bakın [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) belge.

### <a name="head-nodes"></a>Baş düğümler

Hadoop Hizmetleri tooensure yüksek kullanılabilirlik, Hdınsight iki baş düğümler sağlar. Her iki baş düğümler aynı anda etkin ve hello Hdınsight kümesi içinde çalışır durumda. HDFS veya YARN gibi bazı hizmetler, herhangi bir anda yalnızca bir baş düğüm üzerinde ' active'. HiveServer2 veya Hive meta depo gibi başka hizmetleri hello hem baş düğüm üzerinde etkin olan aynı anda.

Baş düğümler (ve diğer düğümlere hdınsight'ta) hello hostname hello düğümün bir parçası olarak sayısal bir değere sahip. Örneğin, `hn0-CLUSTERNAME` veya `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> Merhaba sayısal değer, bir düğüm birincil veya ikincil ile ilişkilendirmeyin. Merhaba sayısal değer yalnızca mevcut tooprovide her düğüm için benzersiz bir ad değil.

### <a name="nimbus-nodes"></a>Nimbus Düğümleri

Nimbus düğümü Storm kümeleri ile kullanılabilir. Merhaba Nimbus düğümü benzer işlevselliği toohello Hadoop Jobtracker'a dağıtma ve çalışan düğümleri arasında işleme izleme sağlar. Hdınsight iki Nimbus düğümü Storm kümeleri için sağlar.

### <a name="zookeeper-nodes"></a>Zookeeper düğümleri

[ZooKeeper](http://zookeeper.apache.org/) düğümleri öncü seçim baş düğümler üzerinde ana Hizmetleri için kullanılır. Ayrıca hizmet ana üzerinde etkin olan baş düğümü Hizmetleri, veri (çalışan) düğümlerini ve ağ geçitleri bilmeniz kullanılan tooinsure oldukları. Varsayılan olarak, Hdınsight üç ZooKeeper düğümleri sağlar.

### <a name="worker-nodes"></a>Çalışan düğümü

Bir işi gönderilen toohello küme olduğunda çalışan düğümleri hello gerçek veri çözümlemesi gerçekleştirme. Bir alt düğüm başarısız olursa, onu gerçekleştiren hello gönderilen tooanother çalışan düğüme bir görevdir. Varsayılan olarak, dört alt düğüm Hdınsight oluşturur. Hem sırasında hem de Küme oluşturulduktan sonra bu sayı toosuit gereksinimlerinizi değiştirebilirsiniz.

### <a name="edge-node"></a>Kenar düğümüne

Bir kenar düğümüne, veri analizi hello kümedeki etkin olarak katılmıyor. Hadoop ile çalışırken, geliştiriciler veya veri bilimcilerine tarafından kullanılır. Hello kenar düğümü yaşamlarını hello aynı Azure sanal ağ hello kümedeki diğer düğümlere hello ve tüm diğer düğümlere doğrudan erişebilirsiniz. Merhaba kenar düğümüne kritik Hadoop Hizmetleri veya analiz işleri çıktığınızda kaynakları bırakmadan kullanılabilir.

Şu anda, hdınsight'ta R Server varsayılan olarak bir kenar düğümüne sağlayan hello yalnızca küme türü budur. Merhaba kenar düğümüne hdınsight'ta R Server için kullanılan yerel olarak hello düğümünde toohello küme dağıtılmış işlem için göndermeden önce test R kodu.

Merhaba küme türleri R Server dışındaki bir edge düğümünü kullanarak hakkında daha fazla bilgi için bkz [Hdınsight'ta kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md) belge.

## <a name="accessing-hello-nodes"></a>Merhaba düğümlere erişme

Merhaba üzerinden erişim toohello küme Internet ortak ağ geçidi üzerinden sağlanır. Erişim sınırlı tooconnecting toohello baş düğümler ve (varsa,) kenar düğümüne hello. Erişim tooservices Hello baş düğümler üzerinde çalışan birden çok baş düğümler sağlayarak parametreden etkilenir değil. İstenen hizmet hello barındıran hello ortak ağ geçidi yollarını istekleri toohello baş düğüm. Örneğin, Ambari şu anda hello ikincil baş düğüm üzerinde barındırılıyorsa hello ağ geçidi Ambari toothat düğümü için gelen istekleri yönlendirir.

Merhaba ortak ağ geçidi üzerinden erişim sınırlı tooport 443 (HTTPS), 22 ve 23 ' dir.

* Bağlantı noktası __443__ kullanılan tooaccess olan Ambari ve diğer web kullanıcı Arabirimi veya hello baş düğümler üzerinde barındırılan REST API'leri.

* Bağlantı noktası __22__ kullanılan tooaccess hello birincil baş düğüm veya kenar düğümüne SSH ile.

* Bağlantı noktası __23__ kullanılan tooaccess hello ikincil baş düğüm SSH. Örneğin, `ssh username@mycluster-ssh.azurehdinsight.net` toohello adlı hello kümesinin birincil baş düğümüne bağlanan **mycluster**.

Merhaba SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>İç tam etki alanı adları (FQDN)

Bir Hdınsight küme düğümlerinde bir iç IP adresi ve yalnızca hello kümeden erişilebilir FQDN vardır. Merhaba iç FQDN veya IP adresini kullanarak hello küme hizmetlerini erişirken Ambari, tooverify hello IP veya FQDN toouse hello hizmet erişirken kullanmanız gerekir.

Örneğin, hizmet yalnızca bir baş düğüm üzerinde çalıştırmak Oozie hello ve hello kullanarak `oozie` bir SSH oturumu komuttan hello URL toohello hizmetinin gerektirir. Bu URL, komutu aşağıdaki hello kullanarak Ambari alınabilir:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

Bu komut bir değer benzer toohello hello İç URL toouse hello ile içeren komutu aşağıdaki döndürür `oozie` komutu:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Merhaba Ambari REST API ile çalışma hakkında daha fazla bilgi için bkz: [izleme ve yönetme hello Ambari REST API kullanarak Hdınsight'ta](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Diğer düğüm türleri erişme

Değil erişilebilir üzerinden hello doğrudan internet yöntemler aşağıdaki hello kullanarak olan toonodes bağlanabilir:

* **SSH**: tooa baş düğüm SSH, kullanarak bağlandıktan sonra hello baş düğüm tooconnect tooother düğümlerinden hello kümedeki SSH kullanabilirsiniz. Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

* **SSH tüneli**: bir web hizmeti barındırılan tooaccess gerekiyorsa değil hello düğümlerinden biri toohello sunulan Internet, SSH tüneli kullanmanız gerekir. Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH tüneli kullanma](hdinsight-linux-ambari-ssh-tunnel.md) belge.

* **Azure sanal ağı**: küme herhangi bir kaynak bir Azure sanal ağının parçası olduğundan, Hdınsight aynı Merhaba, sanal ağ hello kümedeki tüm düğümlere doğrudan erişebilirsiniz. Daha fazla bilgi için bkz: Merhaba [Azure sanal ağını kullanarak Hdınsight genişletmek](hdinsight-extend-hadoop-virtual-network.md) belge.

## <a name="how-toocheck-on-a-service-status"></a>Nasıl toocheck hizmet durumu hakkında

toocheck hello durum hello baş düğümler üzerinde çalışan hizmetleri veya Ambari REST API hello hello Ambari Web kullanıcı arabirimini kullanın.

### <a name="ambari-web-ui"></a>Ambari Web kullanıcı Arabirimi

Merhaba Ambari Web kullanıcı arabirimini https://CLUSTERNAME.azurehdinsight.net görülebilir. Değiştir **CLUSTERNAME** kümenizin hello ada sahip. İstenirse, kümeniz için hello HTTP kullanıcı kimlik bilgilerini girin. Merhaba varsayılan HTTP kullanıcı adı **yönetici** ve hello parola hello kümesi oluştururken girdiğiniz hello parola.

Hello Ambari sayfasında geldiğinde, yüklü hello Hizmetleri hello sayfa hello sol tarafında listelenir.

![Yüklü hizmetleri](./media/hdinsight-high-availability-linux/services.png)

Sonraki tooa hizmet tooindicate durumu görünebilir simgeleri bir dizi vardır. İlgili tüm uyarıları tooa hizmet hello kullanarak görüntülenebilir **uyarıları** hello sayfanın üst kısmındaki hello bağlantı. Daha fazla bilgi her hizmet tooview seçebilirsiniz.

Merhaba hizmet sayfası hello durumu ve her hizmetin yapılandırma hakkında bilgi sağlarken, baş düğüm hello hizmeti çalıştığı hakkında bilgi sağlamaz. tooview bu bilgiler, kullanım hello **ana** hello sayfanın üst kısmındaki hello bağlantı. Bu sayfa hello baş düğümler de dahil olmak üzere hello kümedeki konaklar görüntüler.

![ana bilgisayarların listesi](./media/hdinsight-high-availability-linux/hosts.png)

Hello baş düğümlerden seçme hello bağlantısını hello Hizmetleri ve bileşenleri bu düğümde çalışan görüntüler.

![Bileşen Durumu](./media/hdinsight-high-availability-linux/nodeservices.png)

Ambari kullanarak daha fazla bilgi için bkz: [İzleyici ve hello Ambari Web kullanıcı arabirimini kullanarak Hdınsight yönetmek](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>Ambari REST API

Merhaba Ambari REST API hello kullanılabilir Internet. Merhaba Hdınsight ortak ağ geçidi şu anda hello REST API barındıran yönlendirme istekleri toohello baş düğümü işler.

Komut toocheck hello hello Ambari REST API aracılığıyla bir hizmetin durumunu izleyen hello kullanabilirsiniz:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Değiştir **parola** hello HTTP kullanıcı (Yönetici) hesap parolası ile.
* Değiştir **CLUSTERNAME** hello küme hello adı.
* Değiştir **SERVICENAME** hello hello hizmet adıyla toocheck hello durumunu istiyor.

Örneğin, toocheck hello durumunu hello **HDFS** adlı bir kümede hizmet **mycluster**, bir parola ile **parola**, komutu aşağıdaki hello kullanırsınız:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

Merhaba yanıt benzer toohello JSON aşağıdaki gibidir:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Merhaba URL bize hello Hizmet şu anda adlı bir baş düğüm üzerinde çalışan söyler **hn0 CLUSTERNAME**.

Merhaba durumu bize hello Hizmet şu anda çalışıyor söyler veya **başlatıldı**.

Hangi hizmetlerin hello kümeye yüklü bilmiyorsanız komutu tooretrieve listesini aşağıdaki hello kullanabilirsiniz:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Merhaba Ambari REST API ile çalışma hakkında daha fazla bilgi için bkz: [izleme ve yönetme hello Ambari REST API kullanarak Hdınsight'ta](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Hizmet bileşenleri

Hizmetleri toocheck hello durumunu tek tek istediğiniz bileşenleri içeriyor olabilir. Örneğin, HDFS hello iş bileşeni içerir. tooview bir bileşen hakkında bilgi hello komut şöyle olacaktır:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Hangi bileşenlerin bir hizmeti tarafından sağlanan bilmiyorsanız komutu tooretrieve listesini aşağıdaki hello kullanabilirsiniz:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Nasıl tooaccess günlük dosyalarını hello baş düğümler

### <a name="ssh"></a>SSH

Bağlı tooa baş düğüm sırasında SSH aracılığıyla, günlük dosyalarını altında bulunabilir **/var/log**. Örneğin, **/var/log/hadoop-yarn/yarn** için YARN günlüklerini içerir.

Merhaba hem günlüklerini denetleyin böylece her baş düğüm benzersiz günlük girişlerini olabilir.

### <a name="sftp"></a>SFTP

Merhaba SSH Dosya Aktarım Protokolü veya güvenli Dosya Aktarım Protokolü (SFTP) kullanarak toohello baş düğümüne bağlanmak ve doğrudan hello günlük dosyalarını indirin.

Benzer toousing sağlamanız gereken toohello küme bağlanırken bir SSH istemcisi SSH kullanıcı hesabı adını ve hello SSH adresini hello küme hello. Örneğin, `sftp username@mycluster-ssh.azurehdinsight.net`. İstendiğinde hello hesabı için Hello parola sağlayın veya hello kullanarak bir ortak anahtarı `-i` parametresi.

Bağlantı kurulduktan sonra size sunulan bir `sftp>` istemi. Bu isteminde dizinleri değiştirebilir, dosyaları yükleme ve indirme. Örneğin, aşağıdaki komutları hello değiştirmek dizinleri toohello **/var/log/hadoop/hdfs** dizini ve tüm dosyaların hello dizininde sonra yükleme.

    cd /var/log/hadoop/hdfs
    get *

Kullanılabilir komutlar listesi için girin `help` hello adresindeki `sftp>` istemi.

> [!NOTE]
> SFTP kullanarak bağlandığında toovisualize hello dosya sistemi izin grafik arabirimleri vardır. Örneğin, [MobaXTerm](http://mobaxterm.mobatek.net/) bir arabirim benzer tooWindows Explorer kullanarak toobrowse hello dosya sistemi sağlar.

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess günlük dosyaları Ambari kullanarak, SSH tüneli kullanmanız gerekir. Merhaba web arabirimleri hello tek tek Hizmetleri için hello Internet üzerinde herkese açık şekilde sunulmaz. SSH tüneli kullanma hakkında daha fazla bilgi için bkz: hello [kullanım SSH tünel](hdinsight-linux-ambari-ssh-tunnel.md) belge.

Ambari Web kullanıcı arabirimini Hello tooview günlükleri (örneğin, YARN için) ister hello hizmeti seçin. Ardından **hızlı bağlantılar** tooselect hangi baş düğüm tooview hello günlüğe kaydeder.

![Hızlı kullanarak tooview günlükleri bağlar](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Nasıl tooconfigure hello düğüm boyutu

bir düğümün başlangıç boyutu, küme oluşturma sırasında yalnızca seçilebilir. Kullanılabilir farklı VM boyutları üzerinde hello Hdınsight için hello listesini bulabilirsiniz [Hdınsight fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/hdinsight/).

Bir küme oluştururken, hello düğümleri hello boyutunu belirtebilirsiniz. Merhaba aşağıdaki bilgileri kılavuz nasıl toospecify hello boyutu kullanarak hello üzerinde sağlar [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], ve hello [Azure CLI][azure-cli]:

* **Azure portal**: bir küme oluştururken, hello küme tarafından kullanılan hello düğümleri hello boyutunu ayarlayabilirsiniz:

    ![Düğüm boyutu seçimi ile küme oluşturma Sihirbazı'nın resmi](./media/hdinsight-high-availability-linux/headnodesize.png)

* **Azure CLI**: hello kullanırken `azure hdinsight cluster create` komutunu hello kullanarak hello head, çalışan ve ZooKeeper düğümleri hello boyutunu ayarlayabilirsiniz `--headNodeSize`, `--workerNodeSize`, ve `--zookeeperNodeSize` parametreleri.

* **Azure PowerShell**: hello kullanırken `New-AzureRmHDInsightCluster` cmdlet'ini hello kullanarak hello head, çalışan ve ZooKeeper düğümleri hello boyutunu ayarlayabilirsiniz `-HeadNodeVMSize`, `-WorkerNodeSize`, ve `-ZookeeperNodeSize` parametreleri.

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede belirtilen noktalar hakkında daha fazla bağlantılar toolearn aşağıdaki hello kullanın.

* [Ambari REST başvurusu](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Hello Azure CLI yükleyip](../cli-install-nodejs.md)
* [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview)
* [Ambari kullanarak Hdınsight yönetme](hdinsight-hadoop-manage-ambari.md)
* [Linux tabanlı Hdınsight kümeleri hazırlama](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
