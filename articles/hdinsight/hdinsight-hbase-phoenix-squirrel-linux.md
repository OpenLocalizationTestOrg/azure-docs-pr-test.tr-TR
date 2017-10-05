---
title: "Apache kullanmak Phoenix & HBase - Azure Hdınsight ile SQuirreL | Microsoft Docs"
description: "Hdınsight'ta Apache Phoenix kullanmayı ve yüklemek ve hdınsight'ta HBase kümesi bağlanmak için istasyonunuzda SQuirreL yapılandırmak nasıl öğrenin."
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Hdınsight'ta Linux tabanlı HBase kümeleriyle Apache Phoenix kullanın
Nasıl kullanacağınızı öğrenin [Apache Phoenix](http://phoenix.apache.org/) ve SQLLine kullanma. Phoenix hakkında daha fazla bilgi için bkz: [Phoenix 15 dakika veya daha az](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Phoenix dilbilgisi için bkz: [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Phoenix sürümünü hdınsight'ta bilgi için [Hdınsight tarafından sağlanan Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>SQLLine kullanın
[SQLLine](http://sqlline.sourceforge.net/) SQL yürütülecek bir komut satırı yardımcı programıdır.

### <a name="prerequisites"></a>Ön koşullar
SQLLine kullanmadan önce aşağıdakilere sahip olmanız gerekir:

* **Hdınsight'ta HBase kümesi**. Küme hazırlama HBase hakkında bilgi için bkz: [hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started].
* **Uzak Masaüstü Protokolü aracılığıyla HBase kümesi bağlanmak**. Yönergeler için bkz: [yönetmek Hdınsight'ta Hadoop kümeleri Azure portalını kullanarak][hdinsight-manage-portal].

Bir HBase kümesi bağlandığınızda, Zookeepers birine bağlanmanız gerekir. Her Hdınsight kümesi üç Zookeepers sahiptir.

**Zookeeper ana bilgisayar adı bulunamıyor**

1. Açık Ambari göz atarak **https://<ClusterName>. azurehdinsight.net**.
2. Oturum açma için HTTP (küme) kullanıcı adı ve parola girin.
3. Tıklatın **ZooKeeper** sol menüden. Üç gördüğünüz **ZooKeeper sunucusu** listelenir.
4. Birini tıklatın **ZooKeeper sunucusu** listelenir. Özet bölmesinde, bulma **ana bilgisayar adı**. Aşağıdakine benzer *zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**SQLLine kullanmak için**

1. SSH kullanarak kümeye bağlanın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH, SQLLine çalıştırmak için aşağıdaki komutları çalıştırın:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Bir HBase tablosu oluşturmak için aşağıdaki komutları çalıştırın ve bazı verileri ekleyin:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Daha fazla bilgi için bkz: [SQLLine el ile](http://sqlline.sourceforge.net/#manual) ve [Phoenix Dilbilgisi](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, Hdınsight'ta Apache Phoenix kullanmayı öğrendiniz.  Daha fazla bilgi için bkz:

* [HDInsight HBase'e genel bakış][hdinsight-hbase-overview]: HBase büyük miktarda yapılandırılmamış ve yarı yapılandırılmış veri için rastgele erişim ve güçlü tutarlılık sağlayan, Hadoop'ta yerleşik bir Apache, açık kaynak, NoSQL veritabanıdır.
* [Azure Virtual Network HBase kümelerine sağlamak][hdinsight-hbase-provision-vnet]: uygulamalar HBase ile iletişim kurabilmesi için sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın dağıtılabilir doğrudan.
* [Hdınsight'ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md): HBase çoğaltmayı iki Azure veri merkezi arasında yapılandırmayı öğrenin.
* [Hdınsight'ta HBase ile twitter düşüncelerini çözümleme][hbase-twitter-sentiment]: Gerçek zamanlı nasıl [düşünceleri analiz](http://en.wikipedia.org/wiki/Sentiment_analysis) HBase hdınsight'ta Hadoop kümesi kullanarak büyük veri.

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
