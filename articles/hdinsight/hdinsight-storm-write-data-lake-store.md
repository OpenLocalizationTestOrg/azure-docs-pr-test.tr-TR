---
title: "aaaApache Storm yazma tooStorage/Data Lake Store - Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse hello Apache Storm toowrite toohello HDFS uyumlu depolama Hdınsight için öğrenin. Azure Storage veya Azure Data Lake Store, Hdınsight için hello HDFS comptabile depolama sağlar. Bu belge ve hello ilişkili örnek hello HdfsBolt bileşeni kullanılan toowrite toohello varsayılan Hdınsight kümesinde bir Storm depolanmasını nasıl olabilir göstermektedir."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Hdınsight üzerinde Apache Storm tooHDFS yazma

Hdınsight üzerinde Apache Storm nasıl toouse Storm toowrite veri toohello HDFS uyumlu depolama kullandığı öğrenin. Hdınsight kullanma her ikisi de Azure depolama ve Azure Data Lake depolama HDFS comptabile depolama. Storm sağlayan bir [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) veri tooHDFS Yazar bileşeni. Bu belge, depolama tooeither türü HdfsBolt hello yazma konusunda bilgi sağlar. 

> [!IMPORTANT]
> Hdınsight üzerinde Storm ile dahil olan bileşenleri topoloji bu belgede kullanılan Merhaba örneği kullanır. Diğer Apache Storm kümeleri ile kullanıldığında Azure Data Lake Store ile değiştirilmesi toowork gerektirebilir.

## <a name="get-hello-code"></a>Merhaba kod alın

Bu topoloji içeren hello proje yükleme yoluyla kullanılabilir [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile bu proje için geliştirme ortamınızı yapılandırma aşağıdaki hello gerekir:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek. Java 8 Hdınsight 3.5 veya daha yükseğini gerektirir.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Geliştirme iş istasyonunuza Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir. Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.

* `JAVA_HOME`-hello JDK yüklendiği toohello dizin işaret etmelidir.
* `PATH`-yolları aşağıdaki hello içermelidir:
  
    * `JAVA_HOME`(veya eşdeğer yolu hello).
    * `JAVA_HOME\bin`(veya eşdeğer yolu hello).
    * Maven'ın yüklendiği başlangıç dizini.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Nasıl toouse hello HdfsBolt Hdınsight ile

> [!IMPORTANT]
> Hdınsight üzerinde Storm ile Merhaba HdfsBolt kullanmadan önce önce bir eylem gerekli toocopy jar betiklerinin hello kullanmanız gerekir `extpath` Storm için. Merhaba daha fazla bilgi için bkz: [yapılandırma hello küme](#configure) bölümü.

Merhaba HdfsBolt toounderstand nasıl sağladığını hello dosyası şemasını kullanır toowrite tooHDFS. Hdınsight ile düzenleri aşağıdaki hello birini kullanın:

* `wasb://`: Bir Azure depolama hesabıyla kullanılır.
* `adl://`: Azure Data Lake Store ile kullanılır.

Merhaba aşağıdaki tabloda farklı senaryolar için hello dosya düzeni kullanma örnekleri verilmiştir:

| Düzeni | Notlar |
| ----- | ----- |
| `wasb:///` | bir Azure depolama hesabı blob kapsayıcısında Hello varsayılan depolama hesabı değil |
| `adl:///` | Merhaba varsayılan depolama hesabı, Azure Data Lake Store dizinindedir. Küme oluşturma sırasında Data Lake Store'da hello kümenin HDFS hello köküdür hello dizinini belirtin. Örneğin, hello `/clusters/myclustername/` dizin. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Merhaba kümesi ile ilişkili bir varsayılan olmayan (ek) Azure depolama hesabı. |
| `adl://STORENAME/` | Merhaba Data Lake Store hello küme tarafından kullanılan Hello kök dizini. Bu düzen hello küme dosya sistemi içeriyor hello dizininin dışında bulunan tooaccess verileri sağlar. |

Daha fazla bilgi için bkz: Merhaba [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) Apache.org başvuru.

### <a name="example-configuration"></a>Örnek yapılandırma

Merhaba aşağıdaki YAML olan hello yapılan bir alıntı `resources/writetohdfs.yaml` hello örnekte bulunan dosyası. Bu dosya hello kullanarak hello Storm topolojisini tanımlar [Flux](https://storm.apache.org/releases/1.1.0/flux.html) Apache Storm için çerçevesi.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Bu YAML öğeleri aşağıdaki hello tanımlar:

* `syncPolicy`: Dosyaları synched ve Temizlenen toohello dosya sistemi olduğunda tanımlar. Bu örnekte, her 1000 diziler.
* `fileNameFormat`: Hello yolu ve dosya adı deseni toouse dosyaları yazılırken tanımlar. Bu örnekte, bir filtre kullanarak çalışma zamanında hello yolu sağlanır ve hello dosya uzantısı `.txt`.
* `recordFormat`: Yazılmış hello dosyaları hello iç biçimini tanımlar. Bu örnekte, alanlar hello tarafından sınırlandırılmıştır `|` karakter.
* `rotationPolicy`: Ne zaman tanımlar toorotate dosyaları. Bu örnekte, hiçbir döndürme gerçekleştirilir.
* `hdfs-bolt`: Kullanır hello yapılandırma parametreleri olarak önceki bileşenleri hello `HdfsBolt` sınıfı.

Merhaba Flux framework hakkında daha fazla bilgi için bkz: [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Merhaba küme yapılandırma

Varsayılan olarak, Hdınsight üzerinde Storm HdfsBolt toocommunicate Azure Storage veya Data Lake Store ile Storm'ın sınıf yolunda kullandığını hello bileşenleri içermez. Kullanım hello aşağıdaki komut dosyası eylemi tooadd bu bileşenleri toohello `extlib` kümenizdeki Storm için dizin:

| Betik URI'si | Düğümleri tooapply kendisine | Parametreleri || `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, yönetici | None |

Merhaba kümenizle bu komut dosyası kullanma hakkında daha fazla bilgi için bkz [özelleştirme Hdınsight kümeleri betik eylemleri kullanılarak](./hdinsight-hadoop-customize-cluster-linux.md) belge.

## <a name="build-and-package-hello-topology"></a>Derleme ve paket hello topolojisi

1. Merhaba örnek projesinden indirmeniz [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour geliştirme ortamı.

2. Bir komut isteminden hello terminal veya kabuk oturumu değişiklik dizinleri toohello kök proje indirilir. toobuild ve paket topoloji Merhaba, hello aşağıdaki komutu kullanın:
   
        mvn compile package
   
    Merhaba yapı ve paket oluşturma işlemi tamamlandıktan sonra adlı yeni bir dizin yok `target`, adlı bir dosyayı içeren `StormToHdfs-1.0-SNAPSHOT.jar`. Bu dosya derlenmiş hello topoloji içerir.

## <a name="deploy-and-run-hello-topology"></a>Dağıtma ve çalıştırma hello topolojisi

1. Komut toocopy hello topoloji toohello Hdınsight kümesi aşağıdaki hello kullanın. Değiştir **kullanıcı** hello SSH kullanıcı adı ile Merhaba küme oluşturulurken kullanılır. Değiştir **CLUSTERNAME** hello küme hello adı.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    İstendiğinde, hello SSH kullanıcı hello küme oluştururken kullanılan hello parola girin. Parola yerine bir ortak anahtar kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yolu toohello eşleşen özel anahtarı.
   
   > [!NOTE]
   > Kullanma hakkında daha fazla bilgi için `scp` Hdınsight ile bkz [Hdınsight ile SSH kullanma](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Merhaba karşıya yükleme işlemi tamamlandıktan sonra SSH kullanarak tooconnect toohello Hdınsight kümesi aşağıdaki hello kullanın. Değiştir **kullanıcı** hello SSH kullanıcı adı ile Merhaba küme oluşturulurken kullanılır. Değiştir **CLUSTERNAME** hello küme hello adı.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    İstendiğinde, hello SSH kullanıcı hello küme oluştururken kullanılan hello parola girin. Parola yerine bir ortak anahtar kullandıysanız, toouse hello gerekebilir `-i` parametresi toospecify hello yolu toohello eşleşen özel anahtarı.
   
   Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Bağlandıktan sonra kullanım hello aşağıdaki adlı bir dosya toocreate komut `dev.properties`:

        nano dev.properties

4. Metin hello Merhaba içeriğine aşağıdaki kullanım hello `dev.properties` dosyası:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > Bu örnek, kümenizi hello varsayılan depolama alanı olarak Azure Storage hesabı kullandığını varsayar. Kümenizi Azure Data Lake Store kullanıyorsa kullanın `hdfs.url: adl:///` yerine.
    
    toosave hello dosya, kullanım __Ctrl + X__, ardından __Y__ve son olarak __Enter__. Bu dosyadaki Hello değerlerini hello Data Lake deposu URL'sini ve veri yazılır hello dizin adını ayarlayın.

3. Komut toostart hello topolojisi aşağıdaki hello kullan:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Bu komut toohello Nimbus düğümü hello kümesinin göndererek hello Flux framework kullanarak hello topolojisi başlatır. Merhaba topoloji hello tarafından tanımlanan `writetohdfs.yaml` hello jar bulunan dosyası. Merhaba `dev.properties` dosya filtre olarak geçirilir ve hello dosyasında yer alan hello değerleri hello topolojisi tarafından okunur.

## <a name="view-output-data"></a>Çıktı verilerini görüntüleme

tooview hello veri hello aşağıdaki komutu kullanın:

    hdfs dfs -ls /stormdata/

Bu topoloji tarafından oluşturulan hello dosyaların listesi görüntülenir.

Merhaba aşağıdaki listede, hello önceki komutları tarafından döndürülen hello veri örneğidir:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Merhaba topolojiyi durdurma

Durdurulana kadar Storm topolojileri çalıştırmak veya hello kümesi silindi. toostop topoloji Merhaba, hello aşağıdaki komutu kullanın:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Kümenizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toouse Storm toowrite tooAzure depolama ve Azure Data Lake Store, Bul diğer öğrendiğinize göre [örnekler için Hdınsight Storm](hdinsight-storm-example-topology.md).

