---
title: "aaaUse Apache Phoenix & HBase - Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Bilgi nasıl toouse, hdınsight'ta Apache Phoenix ve nasıl tooinstall ve SQuirreL iş istasyonu tooconnect tooan HBase kümeniz hdınsight'ta yapılandırın."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Hdınsight'ta Linux tabanlı HBase kümeleriyle Apache Phoenix kullanın
Bilgi nasıl toouse [Apache Phoenix](http://phoenix.apache.org/) , hdınsight'ta ve nasıl toouse SQLLine. Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Hello Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Hello hdınsight'ta Phoenix sürüm bilgileri için bkz: [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>SQLLine kullanın
[SQLLine](http://sqlline.sourceforge.net/) komut satırı yardımcı programını tooexecute SQL değil.

### <a name="prerequisites"></a>Ön koşullar
SQLLine kullanmadan önce hello şunlara sahip olmanız gerekir:

* **Hdınsight'ta HBase kümesi**. Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].
* **Toohello HBase kümesi hello Uzak Masaüstü Protokolü aracılığıyla bağlanma**. Yönergeler için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello][hdinsight-manage-portal].

Tooan HBase kümesi bağlandığınızda, hello Zookeepers, tooconnect tooone gerekir. Her Hdınsight kümesi üç Zookeepers sahiptir.

**toofind hello Zookeeper ana bilgisayar adı çıkışı**

1. Açık Ambari çok göz atarak**https://<ClusterName>. azurehdinsight.net**.
2. Merhaba HTTP (küme) kullanıcı adı ve parola toologin girin.
3. Tıklatın **ZooKeeper** hello sol menüden. Üç gördüğünüz **ZooKeeper sunucusu** listelenir.
4. Merhaba birini tıklatın **ZooKeeper sunucusu** listelenir. Merhaba Özet bölmesinde hello bulur **ana bilgisayar adı**. Çok benzer*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. SSH kullanarak toohello kümesine bağlanın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH'den aşağıdaki komutları toorun SQLLine hello çalıştırın:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Bir HBase tablosu komutları toocreate aşağıdaki hello çalıştırın ve bazı verileri ekleyin:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, öğrendiğiniz nasıl toouse hdınsight'ta Apache Phoenix.  toolearn daha bakın:

* [HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.
* [Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın böylece dağıtılan toohello olabilir uygulamalar ile iletişim kurabilir Doğrudan HBase.
* [Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): öğrenin nasıl tooconfigure HBase çoğaltmayı iki Azure veri merkezleri arasında.
* [Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: öğrenin nasıl toodo gerçek zamanlı [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
