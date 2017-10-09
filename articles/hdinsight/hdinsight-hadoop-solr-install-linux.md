---
title: "aaaUse betik eylemi tooinstall hdınsight'ta Linux tabanlı - Azure Solr | Microsoft Docs"
description: "Betik eylemleri kullanılarak nasıl tooinstall Solr üzerinde Linux tabanlı Hdınsight Hadoop kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Yükleme ve Solr Hdınsight Hadoop kümeleri kullanma

Bilgi nasıl betik eylemi kullanarak Azure hdınsight'ta Solr tooinstall. Solr güçlü arama platformudur ve Hadoop tarafından yönetilen veri kuruluş düzeyinde arama yetenekleri sağlar.

> [!IMPORTANT]
    > Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!IMPORTANT]
> Bu belgede kullanılan hello örnek betik, belirli bir yapılandırmayla Solr 4.9 yükler. Farklı Koleksiyonlara, parça, şemalar, çoğaltmalar, vb. ile tooconfigure hello Solr kümesi istiyorsanız hello komut dosyası ve Solr ikili dosyaları değiştirmeniz gerekir.

## <a name="whatis"></a>Solr nedir

[Apache Solr](http://lucene.apache.org/solr/features.html) güçlü tam metin araması verileri sağlayan bir kurumsal arama platformudur. Hadoop depolamak ve çok büyük miktarda veri yönetme olanak sağlarken, Apache Solr tooquickly hello verileri almak hello arama yetenekleri sağlar.

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak Microsoft tarafından desteklenir.
>
> Solr gibi özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Microsoft destek özel bileşenlerle mümkün tooresolve sorunları olabilir. Yardım için tooengage hello açık kaynak toplulukları gerekebilir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).

## <a name="what-hello-script-does"></a>Hangi hello komut dosyası gerçekleştirir

Bu komut dosyası değişiklikleri toohello Hdınsight kümesi aşağıdaki hello yapar:

* Solr 4.9 içine yükler`/usr/hdp/current/solr`
* Bir kullanıcı oluşturur **solrusr**, kullanılan toorun hello Solr hizmet olduğu
* Ayarlar **solruser** hello sahibi olarak`/usr/hdp/current/solr`
* Ekler bir [Upstart](http://upstart.ubuntu.com/) Solr otomatik olarak başlar yapılandırma.

## <a name="install"></a>Betik eylemleri kullanılarak Solr yükleyin

Hdınsight kümesinde bir örnek komut dosyası tooinstall Solr konumu aşağıdaki hello kullanılabilir:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate Solr yüklü olan bir küme, kullanım hello adımları hello [Hdınsight kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md) belge. Merhaba oluşturma işlemi sırasında aşağıdaki adımları tooinstall Solr hello kullanın:

1. Merhaba gelen __küme Özet__ dikey penceresinde, select__Advanced settings__, ardından __betik eylemleri__. Bilgi toopopulate hello formu aşağıdaki hello kullan:

   * **AD**: hello betik eylemi için kolay bir ad girin.
   * **BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**: Bu seçeneği işaretleyin.
   * **ÇALIŞAN**: Bu seçeneği işaretleyin.
   * **ZOOKEEPER**: Bu seçenek tooinstall hello Zookeeper düğümde denetleyin
   * **PARAMETRELERİ**: Bu alanı boş bırakın

2. Merhaba hello sonundaki **betik eylemleri** dikey penceresinde, kullanım hello **seçin** düğme toosave hello yapılandırması. Son olarak, hello kullan **sonraki** düğmesini tooreturn toohello __küme özeti__

3. Merhaba gelen __küme Özet__ sayfasında, __oluşturma__ toocreate hello küme.

## <a name="usesolr"></a>Hdınsight'ta nasıl Solr kullanıyor

> [!IMPORTANT]
> Bu bölümdeki Hello adımları temel Solr işlevleri göstermektedir. Merhaba Solr kullanma hakkında daha fazla bilgi için bkz: [Apache Solr site](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Dizin verileri

Aşağıdaki adımları tooadd örnek veri tooSolr hello kullanın ve ardından sorgu:

1. SSH kullanarak toohello Hdınsight kümesine bağlanın:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > Adımları bu belgenin sonraki bölümlerinde bir SSL tünel tooconnect toohello Solr web kullanıcı arabirimini kullanın. Aşağıdaki adımları toouse, bir SSL kurmak gerekir tünel ve tarayıcı toouse yapılandırmak.
     >
     > Daha fazla bilgi için bkz: Merhaba [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.

2. Aşağıdaki komutları toohave Solr dizin örnek verileri hello kullan:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Merhaba aşağıdaki çıktı toohello konsol döndürülür:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Merhaba `post.jar` yardımcı programı ekler hello **solr.xml** ve **monitor.xml** belgeleri toohello dizini.
  
3. Komut tooquery hello Solr REST API aşağıdaki hello kullan:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Bu komut arar **collection1** eşleşen herhangi bir belgeniz için  **\*:\***  (olarak kodlanmış \*% 3A\* hello sorgu dizesinde). JSON belgesini aşağıdaki hello hello yanıt örneğidir:

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>Merhaba Solr panosunu kullanma

Merhaba Solr Pano web tarayıcınız üzerinden Solr ile toowork veren UI bir web uygulamasıdır. Merhaba Solr Pano doğrudan Hdınsight kümenize gelen hello Internet üzerinde açık değil. Bir SSH tünel tooaccess kullanabilirsiniz. SSH tüneli kullanma hakkında daha fazla bilgi için bkz: Merhaba [kullanım SSH tünel Hdınsight ile](hdinsight-linux-ambari-ssh-tunnel.md) belge.

SSH tüneli kurduktan sonra aşağıdaki adımları toouse hello Solr Pano hello kullan:

1. Merhaba birincil headnode Hello ana bilgisayar adını belirleyin:

   1. SSH tooconnect toohello küme baş düğümüne kullanın. Örneğin, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Merhaba SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Tooget hello tam ana bilgisayar adı komutu aşağıdaki hello kullan:

        ```bash
        hostname -f
        ```

        Bu komut, ana bilgisayar adından bir değer benzer toohello döndürür:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Daha sonra kullanılmak üzere döndürülen, hello değeri kaydedin.

2. Tarayıcınızda, çok bağlantı**solr/http://HOSTNAME:8983 / #/**, burada **ana bilgisayar adı** hello önceki adımlarda belirlenen hello adıdır.

    Merhaba isteği kümenizde hello SSH tünel toohello Solr web kullanıcı Arabirimi üzerinden yönlendirilir. Görüntü aşağıdaki benzer toohello Hello sayfası görünür:

    ![Solr Pano görüntüsü](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. Merhaba Hello sol bölmesinden kullanmak **çekirdek Seçici** açılan tooselect **collection1**. Birden çok girişi bunları altında görünmelidir **collection1**.

4. Aşağıdaki hello girişlerinden **collection1**seçin **sorgu**. Değerleri toopopulate hello arama sayfası aşağıdaki hello kullan:

   * Merhaba, **q** metin kutusuna  **\*:**\*. Bu sorgu Solr dizini tüm hello belgeleri döndürür. Belirli bir dizeyi hello belgelerde toosearch istiyorsanız, o dizeyi buraya girebilirsiniz.
   * Merhaba, **wt** metin kutusunda, select hello çıktı biçimi. Varsayılan değer **json**.

     Son olarak, hello seçin **sorgu yürütme** hello arama pate hello sonundaki düğmesi.

     ![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     Merhaba çıkış iki belge toohello eklenen önceki dizini hello döndürür. Merhaba, benzer toohello JSON belgesi aşağıdaki çıktı:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Başlatma ve durdurma Solr

Toomanually durdurma ve Solr başlatma komutları aşağıdaki hello kullan:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Veri yedekleme dizini

Solr veri toohello varsayılan depolamayı kümeniz için adımları tooback aşağıdaki hello kullan:

1. SSH kullanarak toohello kümesine bağlanın, sonra komutu tooget hello ana bilgisayar adı hello baş düğümü için aşağıdaki hello kullanın:

    ```bash
    hostname -f
    ```

2. Komut toocreate dizine hello verilerin bir anlık görüntüsünü aşağıdaki hello kullanın. Değiştir **ana bilgisayar adı** hello önceki komuttan döndürülen hello adı ile:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    Merhaba yanıt benzer toohello XML aşağıdaki gibidir:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Dizinleri çok değiştirin`/usr/hdp/current/solr/example/solr`. Bir alt burada her koleksiyon için yoktur. Her koleksiyon dizini içeren bir `data` hello koleksiyon için başlangıç anlık görüntü içeren dizini.

4. toocreate hello anlık görüntü klasörü, komutu aşağıdaki kullanım hello sıkıştırılmış bir arşiv:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Hello yerine `snapshot.20150806185338855` koleksiyonunuz için başlangıç anlık görüntüsünün hello ad değerlerle.

    Bu komut, adlandırılmış bir arşiv oluşturur **snapshot.20150806185338855.tgz**, hello Merhaba içeriğine içeren **snapshot.20150806185338855** dizini.

5. Sonra komutu aşağıdaki hello kullanarak hello arşiv toohello kümenin birincil depolama depolayabilirsiniz:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Solr yedekleme ve geri yükleme ile çalışma hakkında daha fazla bilgi için bkz: [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Sonraki adımlar

* [Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install-linux.md). Giraph üzerinde Hdınsight Hadoop kümeleri küme özelleştirme tooinstall kullanın. Giraph tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.

* [Hdınsight kümelerinde Hue yüklemek](hdinsight-hadoop-hue-linux.md). Küme özelleştirme tooinstall ton Hdınsight Hadoop kümeleri üzerinde kullanın. Hue Web uygulamaları toointeract Hadoop kümesi ile kullanılır.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
