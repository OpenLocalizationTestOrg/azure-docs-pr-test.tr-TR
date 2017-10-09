---
title: "Python bileşenleri - Azure Hdınsight ile aaaApache Storm | Microsoft Docs"
description: "Bilgi nasıl toocreate Python bileşenleri kullanan bir Apache Storm topolojisini."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: Apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Python kullanarak Hdınsight üzerinde Apache Storm topolojileri geliştirme

Bilgi nasıl toocreate Python bileşenleri kullanan bir Apache Storm topolojisini. Apache Storm, bir topoloji çeşitli dillerde toocombine bileşenlerini izin verme bile birden çok dili destekler. Merhaba (0.10.0 Storm ile sunulan) Flux framework sağlar tooeasily Python bileşenleri kullanan çözümler oluşturun.

> [!IMPORTANT]
> Bu belgedeki bilgiler Hello Hdınsight 3.6 üzerinde Storm kullanılarak test edilmiştir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Bu proje için Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Ön koşullar

* Python 2.7 ya da daha yüksek

* Java JDK 1.8 veya üzeri

* Maven 3

* (İsteğe bağlı) Yerel bir Storm geliştirme ortamı. Yerel olarak toorun hello topoloji isterseniz, yerel bir Storm ortam yalnızca gereklidir. Daha fazla bilgi için bkz: [bir geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).

## <a name="storm-multi-language-support"></a>Storm çoklu dil desteği

Apache Storm bileşenleri herhangi bir programlama dili kullanılarak yazılmış ile tasarlanmış toowork oluştu. gereken Hello bileşenlerini anlama nasıl hello ile toowork [Thrift tanımıdır Storm için](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Python için bir modül Storm tooeasily arabirim sağlayan hello Apache Storm projesinin bir parçası olarak sağlanır. Bu modülü bulabilirsiniz [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Storm Java sanal makine (JVM) hello üzerinde çalışan Java bir işlemdir. Diğer dillerde yazılmış bileşenleri alt yürütülür. Merhaba Storm stdin/stdout gönderilen JSON iletileri kullanarak bu alt iletişim kurar. Hello bileşenleri arasındaki iletişim hakkında daha fazla ayrıntı bulunabilir [çoklu dil Protokolü](https://storm.apache.org/documentation/Multilang-protocol.html) belgeleri.

## <a name="python-with-hello-flux-framework"></a>Python hello Flux framework ile

Merhaba Flux framework toodefine Storm topolojilerini hello bileşenlerinden ayrı olarak verir. Merhaba Flux framework YAML toodefine hello Storm topolojisini kullanır. Merhaba aşağıdaki nasıl bir örnek metindir tooreference hello YAML belge Python bileşeninde:

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

Merhaba sınıfı `FluxShellSpout` kullanılan toostart hello olduğu `sentencespout.py` hello spout uygulayan komut dosyası.

Flux bekliyor hello Python komut dosyaları toobe hello `/resources` hello topoloji içeren hello jar dosyasını içinde dizin. Bu örnek hello hello Python betiklerini depolamasının `/multilang/resources` dizin. Merhaba `pom.xml` XML aşağıdaki hello kullanarak bu dosyayı içerir:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Daha önce belirtildiği gibi bir `storm.py` hello Thrift tanımıdır Storm için uygulayan dosyası. Merhaba Flux framework içerir `storm.py` otomatik olarak zaman hello projesi yapılandırıldığında, bunu dahil olmak üzere ilgili tooworry gerekmez.

## <a name="build-hello-project"></a>Merhaba projeyi derleme

Merhaba proje Hello kökünden hello aşağıdaki komutu kullanın:

```bash
mvn clean compile package
```

Bu komut oluşturur bir `target/WordCount-1.0-SNAPSHOT.jar` hello içeren dosya derlenmiş topolojisi.

## <a name="run-hello-topology-locally"></a>Merhaba topoloji yerel olarak çalıştırma

toorun hello yerel olarak topoloji hello aşağıdaki komutu kullanın:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Bu komut, bir yerel Storm geliştirme ortamını gerektirir. Daha fazla bilgi için bkz: [bir geliştirme ortamını ayarlama](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)

Bir kez hello topolojisini başlatır, bilgi toohello yerel konsol benzer toohello metin aşağıdaki gösterir:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


toostop hello topoloji, kullanım __Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Hdınsight üzerinde Hello Storm topolojisini çalıştırın

1. Kullanım hello şu komutu toocopy hello `WordCount-1.0-SNAPSHOT.jar` Hdınsight kümesinde Storm tooyour dosya:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Değiştir `sshuser` kümenizin hello SSH kullanıcıyla. Değiştir `mycluster` hello küme adı ile. İstendiğinde tooenter hello hello SSH kullanıcı parolasını olabilir.

    SSH ve SCP kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Hello dosya karşıya yüklendikten sonra SSH kullanarak toohello kümesine bağlanın:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Merhaba SSH oturumundan komutu toostart hello topoloji hello kümede aşağıdaki hello kullan:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. Merhaba kümede hello Storm kullanıcı Arabirimi tooview hello topoloji kullanabilirsiniz. Merhaba Storm kullanıcı Arabirimi https://mycluster.azurehdinsight.net/stormui bulunur. Değiştir `mycluster` küme adıyla.

> [!NOTE]
> Başladıktan sonra Storm topolojisini durdurulana kadar çalışır. toostop topoloji Merhaba, yöntemler aşağıdaki hello birini kullanın:
>
> * Merhaba `storm kill TOPOLOGYNAME` hello komut satırından komutu
> * Merhaba **KILL** düğmesini hello Storm kullanıcı Arabirimi.


## <a name="next-steps"></a>Sonraki adımlar

Belgeleri diğer yolları toouse Hdınsight ile Python için aşağıdaki hello bakın:

* [Nasıl MapReduce işleri akış için Python toouse](hdinsight-hadoop-streaming-python.md)
* [Nasıl toouse Python kullanıcı tanımlı işlevler (UDF), Pig ve Hive](hdinsight-python.md)
