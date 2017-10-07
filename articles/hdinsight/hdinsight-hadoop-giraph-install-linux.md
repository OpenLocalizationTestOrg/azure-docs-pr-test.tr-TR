---
title: "aaaInstall ve Hdınsight (Hadoop) - Azure Giraph kullanma | Microsoft Docs"
description: "Betik eylemleri kullanılarak nasıl tooinstall Giraph Linux tabanlı hdınsight kümeleri hakkında bilgi edinin. Betik eylemleri toocustomize hello küme oluşturma sırasında küme yapılandırmasını değiştirme veya hizmetleri ve yardımcı programları yükleme sağlar."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>Giraph Hdınsight Hadoop kümelerine yükleme ve Giraph tooprocess büyük ölçekli grafikleri kullanma

Bilgi nasıl tooinstall Apache Giraph Hdınsight kümesinde. hdınsight Hello betik eylemi özelliği sağlar, toocustomize bash komut dosyası çalıştırarak, küme. Komut dosyaları kullanılan toocustomize kümeleri sırasında ve Küme oluşturulduktan sonra olabilir.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="whatis"></a>Giraph nedir

[Apache Giraph](http://giraph.apache.org/) tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir. Grafik nesneleri arasındaki ilişkiler model. Örneğin, Internet veya sosyal ağlar üzerindeki kişiler arasındaki ilişkileri hello gibi büyük bir ağ yönlendiricileri arasındaki bağlantıları hello. Grafik işleme hello bir grafik nesneleri arasındaki ilişkiler hakkında tooreason gibi sağlar:

* Geçerli ilişkilere dayanan olası arkadaş tanımlama.

* Merhaba kısa rotayı bir ağda iki bilgisayar arasında tanımlayıcı.

* Web sayfalarının Hello sayfa derecesini hesaplama.

> [!WARNING]
> Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenen - Microsoft Support tooisolate yardımcı olur ve sorunları ilgili toothese bileşenler çözümlenemiyor.
>
> Giraph gibi özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme. Microsoft Support mümkün tooresolving hello sorun olabilir. Aksi durumda, bu teknoloji derin uzmanlık bulunduğu açık kaynak toplulukları başvurmanız gerekir. Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/).


## <a name="what-hello-script-does"></a>Hangi hello komut dosyası gerçekleştirir

Bu komut dosyası hello aşağıdaki eylemleri gerçekleştirir:

* Giraph çok yükler`/usr/hdp/current/giraph`

* Kopya hello `giraph-examples.jar` dosya kümenizin toodefault storage (WASB):`/example/jars/giraph-examples.jar`

## <a name="install"></a>Betik eylemleri kullanılarak Giraph yükleyin

Hdınsight kümesinde bir örnek komut dosyası tooinstall Giraph konumu aşağıdaki hello kullanılabilir:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

Bu bölümde, nasıl toouse hello örnek betik hello Azure portal kullanarak hello küme oluşturulurken hakkında yönergeler sağlar.

> [!NOTE]
> Betik eylemi, yöntemler aşağıdaki hello birini kullanarak uygulanabilir:
> * Azure PowerShell
> * Hello Azure CLI
> * Merhaba Hdınsight .NET SDK'sı
> * Azure Resource Manager şablonları
> 
> Betik eylemleri tooalready kümeleri çalıştıran uygulayabilir. Daha fazla bilgi için bkz: [özelleştirme Hdınsight betik eylemleri ile kümeleri](hdinsight-hadoop-customize-cluster-linux.md).

1. Merhaba adımları kullanarak bir küme oluşturmaya başlamak [oluşturma Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md), ancak oluşturma tamamlamayın.

2. Merhaba üzerinde **isteğe bağlı yapılandırma** dikey penceresinde, select **betik eylemleri**ve aşağıdaki bilgilerle hello sağlayın:

   * **AD**: hello betik eylemi için kolay bir ad girin.

   * **BETİK URI'si**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**: Bu girişi denetleyin

   * **ÇALIŞAN**: Bu girdi işaretlemeden bırakın

   * **ZOOKEEPER**: Bu girdi işaretlemeden bırakın

   * **PARAMETRELERİ**: Bu alanı boş bırakın

3. Merhaba hello sonundaki **betik eylemleri**, hello kullan **seçin** düğme toosave hello yapılandırması. Son olarak, hello kullan **seçin** düğmesi hello hello sonundaki **isteğe bağlı yapılandırma** dikey toosave hello isteğe bağlı yapılandırma bilgileri.

4. Bölümünde açıklandığı gibi Hello küme oluşturmaya devam [oluşturma Linux tabanlı Hdınsight kümeleri](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="usegiraph"></a>Hdınsight'ta nasıl Giraph kullanıyor?

Merhaba Küme oluşturulduktan sonra aşağıdaki adımları toorun hello SimpleShortestPathsComputation örneğine Giraph dahil hello kullanın. Bu örnek hello basic kullanan [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) hello en kısa yolu bir grafik nesneler arasındaki bulmak için uygulama.

1. SSH kullanarak toohello Hdınsight kümesine bağlanın:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Kullanım hello şu komutu toocreate adlı bir dosya **tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    Bu dosyanın içeriğini hello metin aşağıdaki hello kullan:

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    Bu veri hello biçimi kullanarak bir yönlendirilmiş grafik nesneler arasındaki ilişkiyi tanımlayan `[source_id, source_value,[[dest_id], [edge_value],...]]`. Her satır arasındaki bir ilişkiyi temsil eden bir `source_id` nesne ve bir veya daha fazla `dest_id` nesneleri. Merhaba `edge_value` , hello gücü veya hello bağlantı uzaklığı olarak düşünülebilir `source_id` ve `dest\_id`.

    Çıkış çizilmiş ve nesneleri arasındaki hello uzaklığı olarak hello değeri (veya ağırlık) kullanarak, hello veri diyagramı aşağıdaki hello gibi görünebilir:

    ![Daireler arasında değişen uzaklığı satır olarak çizilen tiny_graph.txt](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. toosave hello dosya, kullanım **Ctrl + X**, ardından **Y**ve son olarak **Enter** tooaccept hello dosya adı.

4. Hdınsight kümeniz için birincil depolama alanına toostore hello veri aşağıdaki hello kullan:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. Merhaba SimpleShortestPathsComputation örnek komut aşağıdaki hello kullanarak çalıştırın:

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    Bu komutla birlikte kullanılan hello parametreleri aşağıdaki tablonun hello açıklanmaktadır:

   | Parametre | Neler yapar? |
   | --- | --- |
   | `jar` |Merhaba örnekleri içeren hello jar dosyasını. |
   | `org.apache.giraph.GiraphRunner` |Merhaba sınıfı toostart hello örnekler kullanılır. |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |kullanılan Merhaba örneği. Bu örnekte, hello en kısa yolu kimliği 1 ile Merhaba Grafikteki tüm diğer kimlikleri arasında hesaplar. |
   | `-ca mapred.job.tracker` |Merhaba headnode hello kümesi için. |
   | `-vif` |Merhaba giriş biçimi toouse hello giriş verileri için. |
   | `-vip` |Merhaba giriş veri dosyasını. |
   | `-vof` |Merhaba çıktı biçimi. Bu örnek, kimlik ve düz metin olarak değeri. |
   | `-op` |Merhaba çıkış konumu. |
   | `-w 2` |Çalışanlar toouse Hello sayısı. Bu örnekte, 2. |

    Bu ve Giraph örnekleri ile kullanılan diğer parametreleri hakkında daha fazla bilgi için bkz: Merhaba [Giraph quickstart](http://giraph.apache.org/quick_start.html).

6. Merhaba işi tamamlandıktan sonra hello sonuçları hello depolanır **/example/out/shotestpaths** dizini. Merhaba çıktı dosyası adları ile başlayan **bölümü-m -** ve vb. dosya hello ilk olarak, ikinci olarak, belirten bir sayı ile bitmelidir. Komut tooview hello çıktısı aşağıdaki hello kullan:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    Merhaba çıkış metnini izleyen benzer toohello görünmelidir:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    Merhaba SimpleShortestPathComputation örnek nesne kimliği 1 ile sabit kodlanmış toostart olan ve hello en kısa yolu tooother nesneleri bulun. Merhaba çıktı hello biçiminde olduğunu `destination_id` ve `distance`. Merhaba `distance` hello değeri (veya ağırlık) seyahat hello kenarları nesne kimliği 1 ile Merhaba hedef kimliği arasında olmalıdır

    Bu veri görselleştirme, hello kısa yolları kimliği 1 ile tüm diğer nesnelerin arasında seyahat hello sonuçları doğrulayabilirsiniz. Merhaba en kısa yolu kimliği 1 ile kimliği 4 arasında 5'tir. Bu değer arasındaki hello toplam uzaklığı: <span style="color:orange">kimliği 1 ve 3</span>ve ardından <span style="color:red">kimliği 3 ve 4</span>.

    ![Nesnelerin arasında çizilmiş kısa yolları daireler olarak çizme](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>Sonraki adımlar

* [Yükleme ve Hdınsight kümelerinde ton kullanma](hdinsight-hadoop-hue-linux.md).

* [Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md).
