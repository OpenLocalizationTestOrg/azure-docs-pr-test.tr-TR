---
title: "aaaWhat Azure Hdınsight'ta HBase mi? | Microsoft Belgeleri"
description: "Giriş tooApache hdınsight'ta HBase, Hadoop'ta bir NoSQL veritabanı oluşturun. Kullanım örnekleri hakkında bilgi edinin ve HBase tooother Hadoop kümeleri karşılaştırın."
keywords: "bigtable,nosql,hbase nedir,apache hbase,hbase,habase genel bakış,"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>HDInsight’ta HBase nedir: Hadoop için BigTable benzeri özellikler sağlayan bir NoSQL veritabanıdır.
Apache HBase, Hadoop’ta oluşturulan ve Google BigTable’a göre modellenen açık kaynaklı bir NoSQL veritabanıdır. HBase, sütun aileleri tarafından veritabanında büyük miktarlardaki yapılandırılmamış ve yarı yapılandırılmış veriler için rasgele erişim ve güçlü tutarlılık sağlar.

Veri Merhaba tablonun satırlarında depolanır ve satır içindeki veriler sütun ailesi tarafından gruplandırılır. HBase hiçbiri sütunların ya da bunlarda depolanan veri hello türü hello hello algılama şemasız bir veritabanında kullanmadan önce tanımlanan toobe ihtiyacınız olur. Merhaba açık kaynak kodu, binlerce üzerinde toohandle petabaytlarca verileri doğrusal olarak ölçeklendirir. Veri yedekleme, toplu işleme ve hello Hadoop ekosistemindeki dağıtılmış uygulamalar tarafından sağlanan diğer özellikleri güvenebilirsiniz.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Azure HDInsight’ta HBase nasıl uygulanır?
Hdınsight HBase, Azure ortamı hello tümleştirilmiş yönetilen bir küme olarak sunulur. Merhaba kümesi olan yapılandırılmış toostore verileri doğrudan [Azure Storage](./hdinsight-hadoop-use-blob-storage.md) veya [Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md), düşük gecikme süresi ve performans ve maliyet seçeneklerinde artan esneklik sağlar. Bu, büyük veri kümeleri, milyonlarca uç noktaları ve tooanalyze algılayıcı ve telemetri verilerini depolayan toobuild Hizmetleri ile bu verileri Hadoop işleriyle çalışan müşteriler toobuild etkileşimli Web siteleri sağlar. HBase ve Hadoop Azure'da; başlangıç noktaları büyük veri projeleri için Özellikle, bunlar büyük veri kümeleri ile gerçek zamanlı uygulamaları toowork etkinleştirebilirsiniz.

Merhaba Hdınsight uygulaması HBase tooprovide tabloların otomatik parçalanmasını, okuma, yazma ve otomatik yük devretme için güçlü tutarlılık hello genişleme mimarisi yararlanır. Performans, okumalar için bellek içi önbelleğe alma ve yazmalar için yüksek verimlilikli akış tarafından geliştirilmiştir. HBase kümesi sanal ağda oluşturulabilir. Ayrıntılar için bkz. [Azure Sanal Ağ'da HDInsight kümeleri oluşturma][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Veriler HDInsight HBase’de nasıl yönetilir?
Veri yönetilebilir HBase hello kullanarak `create`, `get`, `put`, ve `scan` hello HBase kabuğunu komutları. Veri yazılmış toohello veritabanı kullanarak `put` okuyup kullanarak `get`. Merhaba `scan` kullanılan tooobtain verileri bir tabloda birden çok satırdaki bir komuttur. Veri hello hello HBase REST API'SİNİN üstünde bir istemci kitaplığı sağlayan HBase C# API'si kullanılarak da yönetilebilir. Bir HBase veritabanı, Hive kullanarak da sorgulanabilir. Programlama modelleri bir giriş toothese için bkz: [hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza][hbase-get-started]. Ortak işlemciler de konak hello veritabanının hello düğümleri veri işlemeye olanak, kullanılabilir.

> [!NOTE]
> Thrift, HDInsight’ta HBase tarafından desteklenmez.
>

## <a name="scenarios-use-cases-for-hbase"></a>Senaryolar: HBase kullanım örnekleri
Merhaba kurallı kullanım örneği bigtable (ve uzantılarının, HBase) oluşturulmuş web aramasıydı. Arama motorları terimleri toohello web sayfalarını bunları içeren eşleme dizinler oluşturur. Ancak HBase için uygun olan diğer birçok kullanım örneği vardır; bunların birkaçı bu bölümde listelenmektedir.

* Anahtar değeri deposu
  
    HBase bir anahtar değeri deposu olarak kullanılabilir ve ileti sistemlerini yönetmeye uygundur. Facebook kendi ileti sistemi için HBase kullanır ve Internet iletişimlerini depolamak ve yönetmek için idealdir. WebTable Web sayfalarından çıkarılan tabloları yönetin ve HBase toosearch için kullanır.
* Algılayıcı verileri
  
    HBase çeşitli kaynaklardan artımlı olarak toplanan verileri yakalamak için yararlıdır. Bu, sosyal analizler, zaman serileri, etkileşimli panoları eğilimler ve sayaçlar ile güncel tutma ve denetim günlüğü sistemlerini yönetmeyi içerir. Örnekler Bloomberg Tüccar Terminali ve sunucu sistemlerinin hello durumuyla ilgili hello açık zaman serisi depolar ve erişim toometrics sağlayan veritabanı (OpenTSDB) toplanır.
* Gerçek zamanlı sorgu
  
    [Phoenix](http://phoenix.apache.org/) Apache HBase için bir SQL sorgu alt yapısıdır. Buna JDBC sürücüsü olarak erişilir ve bu SQL kullanarak HBase tablolarını sorgulamayı ve yönetmeyi sağlar.
* Bir platform olarak HBase
  
    Uygulamalar, bir veri deposu olarak kullanarak HBase’in üstünde çalışabilir. Örnek olarak Phoenix, OpenTSDB, Kiji ve Titan verilebilir. Uygulamalar HBase ile de tümleştirebilir. Örnek olarak, Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia ve Dril verilebilir.

## <a name="next-steps"></a>Sonraki adımlar
* [HDInsight'ta Hadoop ile HBase kullanmaya başlama][hbase-get-started]
* [Azure Sanal Ağ'da HDInsight kümeleri oluşturma][hbase-provision-vnet]
* [HDInsight’ta HBase çoğaltmayı yapılandırma](hdinsight-hbase-replication.md)
* [HDInsight'ta HBase ile Twitter düşüncelerini çözümleme][hbase-twitter-sentiment]
* [Hdınsight (Hadoop) ile HBase kullanan Maven toobuild Java uygulamaları kullanın][hbase-build-java-maven]

## <a name="see-also"></a>Ayrıca bkz.
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable: Yapılandırılmış Veriler için Dağıtılmış Depolama Sistemi](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
