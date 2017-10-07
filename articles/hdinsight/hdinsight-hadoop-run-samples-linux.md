---
title: "hdınsight'ta - Azure aaaRun Hadoop MapReduce örnekleri | Microsoft Docs"
description: "MapReduce örnekleri Hdınsight'ta dahil jar dosyalarında kullanmaya başlayın. SSH tooconnect toohello küme kullanıp hello Hadoop komutu toorun örnek işleri kullanın."
keywords: "hadoop örnek jar, hadoop örnekler jar, hadoop mapreduce örnekler, mapreduce örnekleri"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Hdınsight'ta dahil hello MapReduce örnekler çalıştırın

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Hdınsight'ta Hadoop ile nasıl toorun hello MapReduce örnekler dahil öğrenin.

## <a name="prerequisites"></a>Ön koşullar

* **Hdınsight kümesi**: bkz [Hadoop ile Linux'ta Hdınsight Hive kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Bir SSH istemcisi**: daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>Merhaba MapReduce örnekleri

**Konum**: hello örnekleri Hdınsight küme adresindeki hello bulunur `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**İçeriği**: örnekleri aşağıdaki hello bu arşivde bulunur:

* `aggregatewordcount`: Bir toplama hello giriş dosyaları hello sözcükleri sayar mapreduce program temel.
* `aggregatewordhist`: Bir toplama hello giriş dosyaları hello sözcükleri hello histogram hesaplar mapreduce program temel.
* `bbp`Pi sayısının Bailey Borwein Plouffe toocompute tam basamak kullanır mapreduce program.
* `dbcount`: Bir veritabanında depolanan hello sayfa görünümü günlükleri sayar bir örnek işi.
* `distbbp`Pi sayısının BBP türü formül toocompute tam BITS kullanır mapreduce program.
* `grep`Regex hello girişte, hello sayar mapreduce program eşleşir.
* `join`: Üzerinde birleştirme gerçekleştirir bir iş sıralanmış, veri kümeleri eşit olarak bölümlenmiş.
* `multifilewc`: Birkaç dosyalarından sözcükleri sayar bir iş.
* `pentomino`: Program toofind çözümleri toopentomino sorunları yerleştirmede mapreduce kutucuk.
* `pi`Yarı Monte kullanarak Pi tahminleri mapreduce program Carlo yöntemi.
* `randomtextwriter`Düğüm başına rastgele metinsel veri 10 GB Yazar mapreduce program.
* `randomwriter`Düğüm başına rastgele veri 10 GB Yazar mapreduce program.
* `secondarysort`: İkincil sıralama toohello tanımlama bir örnek aşaması azaltın.
* `sort`Merhaba rastgele yazıcı tarafından yazılan hello veri sıralar mapreduce program.
* `sudoku`: Bir sudoku Çözücü.
* `teragen`: Merhaba terasort verilerini oluşturur.
* `terasort`: Merhaba terasort çalıştırın.
* `teravalidate`: Terasort sonuçlarını denetleniyor.
* `wordcount`Merhaba hello sözcükleri sayar mapreduce program dosyaları girin.
* `wordmean`Hello ortalama uzunluğu hello hello sözcükleri sayar mapreduce program dosyaları girin.
* `wordmedian`Merhaba Medyan hello hello sözcükleri uzunluğu sayar mapreduce program dosyaları girin.
* `wordstandarddeviation`Hello standart sapmasını hello uzunluğu hello hello sözcükleri sayar mapreduce program dosyaları girin.

**Kaynak kodu**: Hdınsight küme adresindeki hello üzerinde bu örnekleri için kaynak kodunu dahil `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Merhaba `2.2.4.9-1` hello yolu hello Hdınsight kümesi için Hortonworks veri platformu hello hello sürümüdür ve kümeniz için farklı olabilir.

## <a name="run-hello-wordcount-example"></a>Merhaba wordcount örneği çalıştırma

1. SSH kullanarak tooHDInsight bağlayın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Merhaba gelen `username@#######:~$` isteminde, komut toolist hello örnekleri aşağıdaki hello kullanın:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Bu komut hello önceki bölümden bu belgenin hello örnek listesi oluşturur.

3. Kullanım hello aşağıdaki belirli bir örneği tooget Yardım komutu. Bu durumda, hello **wordcount** örnek:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    İletiden hello alırsınız:

        Usage: wordcount <in> [<in>...] <out>

    Bu ileti hello kaynak belgeler için birkaç giriş yollarının sağlayabilir gösterir. Merhaba son yol hello çıkış (Merhaba kaynak belgeleri sözcükleri sayısı) depolandığı yerdir.

4. Toocount aşağıdaki hello hello dizüstü bilgisayarlar, Leonardo Da örnek veri kümenizle sağlanan Vinci, tüm sözcükleri kullanın:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    Bu işi okuma girdisi `/example/data/gutenberg/davinci.txt`. Bu örnek depolanan çıktısı `/example/data/davinciwordcount`. Her iki yolları hello kümesi, hello yerel dosya sistemi için varsayılan depolama bulunur.

   > [!NOTE]
   > Merhaba wordcount örneği hello Yardımı'nda belirtildiği gibi birden fazla girdi dosyası da belirtebilirsiniz. Örneğin, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` davinci.txt ve ulysses.txt sözcükleri sayar.

5. Merhaba işi tamamlandıktan sonra komutu tooview hello çıktısı aşağıdaki hello kullanın:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Bu komut hello iş tarafından üretilen tüm hello çıktı dosyaları art arda ekler. Merhaba çıktı toohello Konsolu görüntüler. Merhaba, benzer toohello metin aşağıdaki çıktı:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Her satır bir sözcük ve hello oluştu kaç kez giriş temsil eder.

## <a name="hello-sudoku-example"></a>Merhaba Sudoku örneği

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) olan dokuz 3 x 3 ızgaralar oluşan bir mantık Bulmacanın. Hello kılavuzunda bazı hücreler, diğerleri boş ve toosolve hello boş hücrelerin hello hedeftir numaraları içeriyor. Merhaba önceki bağlantı hello Bulmacanın hakkında daha fazla bilgi gerekiyor, ancak bu örnek hello amacı toosolve hello boş hücreler için. Bu nedenle bizim giriş hello biçimini izleyen bir dosya olmalıdır:

* Dokuz sütunların dokuz satırları
* Her sütunun bir sayı içerebilir veya `?` (boş bir hücre gösterir)
* Hücreleri boşlukla ayrılmış

Sudoku yapbozlar belirli bir şekilde tooconstruct yoktur; bir sütun veya satır numarasında yinelenemez. Doğru şekilde oluşturulduğundan hello Hdınsight kümesinde bir örnek verilmiştir. Şu konumdadır: `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` ve metin aşağıdaki hello içerir:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

Bu örnek sorunu hello Sudoku örnek aracılığıyla toorun kullanmak hello komutu:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

Merhaba sonuçları metin aşağıdaki benzer toohello görüntülenir:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Pi (π) örneği

Merhaba pi örnek bir istatistik kullanır (yarı Monte Carlo) yöntemi tooestimate hello pi değerini. Noktaları rastgele bir birim kare yerleştirilir. Merhaba kare bir daire de içerir. Merhaba hello noktaları hello daire içinde kalan olasılığı olan hello eşit toohello alanı yuvarlak, pi/4. pi değerini Hello 4R başlangıç değerinden tahmin edilebilir. R hello daire toohello toplam sayısı hello kare içinde noktalarını içinde olduğunda puan hello sayısının hello orandır. Merhaba büyük hello kullanılan noktaları, hello daha iyi hello tahmin örneğidir.

Bu örnek komut toorun aşağıdaki hello kullanın. Bu komut, 10,000,000 örnekleri tooestimate hello pi değerini ile 16 eşlemeleri kullanır:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Merhaba bu komut tarafından döndürülen değeri çok benzer**3.14159155000000000000**. Başvurular için hello ilk 10 ondalık pi'nin 3.1415926535 yerlerdir.

## <a name="10-gb-greysort-example"></a>10 GB Greysort örneği

GraySort Kıyaslama sıralama ' dir. Merhaba, büyük miktarlarda verinin, genellikle en az bir 100 TB sıralama sırasında elde edilen hello sıralama oranı (TB dakikada) ölçümüdür.

Bu örnek uygun bir 10 GB veri kullanır, böylece oldukça hızlı bir şekilde çalıştırılabilir. Owen O'Malley ve Arun Murthy tarafından geliştirilen hello MapReduce uygulamaları kullanır. Bu uygulamalar hello yıllık genel amaçlı ("daytona") terabayt sıralama Kıyaslama 0.578 TB/dak (100 TB 173 dakika cinsinden) oranı ile 2009 kazanmıştır. Bu ve diğer sıralama değerlendirmeleri hakkında daha fazla bilgi için bkz: Merhaba [Sortbenchmark](http://sortbenchmark.org/) site.

Bu örnek, MapReduce programlar üç kümesi kullanır:

* **TeraGen**: veri toosort satırlarını oluşturur A MapReduce programı

* **TeraSort**: örnekler hello giriş verilerini ve MapReduce toosort hello verilerini toplam sıralamaya kullanır

    TeraSort özel bölümleyici dışında bir standart MapReduce sıralama ' dir. Merhaba bölümleyici her azaltın hello anahtar aralığını tanımlamak örneklenen N-1 anahtarları sıralı listesini kullanır. Özellikle, [i-1] örnek tüm anahtarları böyle < = anahtar < örnek [i] tooreduce gönderilen ediyorum. Bu bölümleyici hello çıktısını azaltmak i + 1 değerinden hello çıkışları i azaltmak garanti tüm.

* **TeraValidate**: Bu hello çıkışı doğrular A MapReduce program Genel sıralanmış

    Merhaba çıktı dizini içinde dosya başına bir harita oluşturur ve her eşleme her anahtar değerinden küçük veya buna eşit olmasını sağlar toohello öncekinin. Merhaba harita işlevi hello kayıtlarının ilk oluşturur ve anahtarları her dosyanın en son. Merhaba azaltmak işlevi bu hello sağlar i dosyasının ilk anahtar hello son anahtarı dosyası i-1 büyük. Herhangi bir sorun bozuk hello anahtarlarla aşaması, hello çıktısı azaltmak olarak bildirilir.

Kullanım hello aşağıdaki adımları toogenerate verileri sıralamak ve ardından hello çıkış doğrulayın:

1. 10 GB saklı toohello Hdınsight kümenin varsayılan depolama veri oluşturmak, `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Merhaba `-Dmapred.map.tasks` Hadoop bu proje için kaç tane harita görevleri toouse söyler. Merhaba son iki parametreleri istemeniz hello iş toocreate 10 GB veri ve toostore adresinden `/example/data/10GB-sort-input`.

2. Komut toosort hello verileri aşağıdaki hello kullan:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Merhaba `-Dmapred.reduce.tasks` görevleri toouse hello işi için kaç tane azaltmak Hadoop söyler. Hello son iki Parametreler yalnızca hello girdi ve çıktı verileri için konumları.

3. Merhaba sıralama ölçütü oluşturulan toovalidate hello veri aşağıdaki hello kullan:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, nasıl toorun başlangıç örnekleri Linux tabanlı Hdınsight kümeleri ile Merhaba dahil öğrendiniz. Hdınsight ile Pig, Hive ve MapReduce kullanma hakkında daha fazla öğreticileri için aşağıdaki konularda hello bakın:

* [Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]
* [Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]
* [Hdınsight'ta Hadoop ile MapReduce kullanma][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
