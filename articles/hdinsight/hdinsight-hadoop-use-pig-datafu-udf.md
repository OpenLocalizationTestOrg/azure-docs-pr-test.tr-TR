---
title: "Pig hdınsight'ta - Azure ile DataFu kullanma | Microsoft Docs"
description: "DataFu Hadoop ile kullanmak için kitaplıkları koleksiyonudur. DataFu ile Pig Hdınsight kümenize kullanma hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4de55f5f6c5605e9c6c8dd7ccac902b811d1b062
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a>Hdınsight üzerinde pig ile DataFu kullanma

Hdınsight ile DataFu kullanmayı öğrenin. DataFu, hadoop'ta Pig ile kullanılmak üzere açık kaynak kitaplıkları koleksiyonudur.

## <a name="prerequisites"></a>Ön koşullar

* Azure aboneliği.

* Azure Hdınsight kümesi (Linux veya Windows tabanlı)

  > [!IMPORTANT]
  > Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Temel olarak bilindiğini [Pig kullanarak](hdinsight-use-pig.md)

## <a name="install-datafu-on-linux-based-hdinsight"></a>Linux tabanlı Hdınsight üzerinde DataFu yükleyin

> [!IMPORTANT]
> DataFu, Linux tabanlı kümelerde sürüm 3.3 ve üzeri ve Windows tabanlı kümeler yüklenir. Linux tabanlı kümelerde 3.3'den önceki yüklü değildir.
>
> Windows tabanlı bir küme veya Linux tabanlı küme 3.3 sürümünden daha yüksek kullanıyorsanız, bu bölümü atlayabilirsiniz.

DataFu indirilir ve Maven deposundan yüklenir. Hdınsight kümenize DataFu eklemek için aşağıdaki adımları kullanın:

1. SSH kullanarak Linux tabanlı Hdınsight kümenize bağlanın. Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Wget yardımcı programını kullanarak DataFu jar dosyasını karşıdan yüklemek için aşağıdaki komutu kullanın veya kopyalamak ve bağlantıyı yüklemeye başlamak için tarayıcınıza yapıştırın.

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. Ardından, Hdınsight kümeniz için varsayılan depolama dosyası yükleyin. Dosyanın varsayılan yerleştirme depolama tüm düğümler için kullanılabilir kümede kolaylaştırır.

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > Önceki komut jar depolar `/example/jars` bu dizin küme depolama alanında zaten mevcut olduğundan. Hdınsight küme depolama alanında istediğiniz herhangi bir yerde kullanabilirsiniz.

## <a name="use-datafu-with-pig"></a>DataFu ile Pig kullanma

Bu bölümdeki adımları Pig Hdınsight'ta kullandıysanız olduğunu varsayar. Hdınsight ile Pig kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile Pig kullanma](hdinsight-use-pig.md).

> [!IMPORTANT]
> Önceki bölümde yer alan adımları kullanarak DataFu el ile yüklediyseniz, kullanmadan önce kaydetmelisiniz.
>
> * Kümenizi Azure Storage kullanıyorsa kullanın bir `wasb://` yolu. Örneğin, `register wasb:///example/jars/datafu-1.2.0.jar`.
>
> * Kümenizi Azure Data Lake Store kullanıyorsa kullanın bir `adl://` yolu. Örneğin, `register adl://home/example/jars/datafu-1.2.0.jar`.

Genellikle DataFu işlevler için diğer ad tanımlayabilirsiniz. Aşağıdaki örnek, bir diğer ad tanımlar `SHA`:

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

Ardından bu diğer adı Pig Latin komut dosyasında giriş verileri için karma oluşturmak için kullanabilirsiniz. Örneğin, aşağıdaki kodu giriş verilerini konumda karma değeri ile değiştirir:

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

Şu çıkışı üretir:

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a>Sonraki adımlar

DataFu veya Pig hakkında daha fazla bilgi için aşağıdaki belgelere bakın:

* [Apache DataFu Pig Kılavuzu](http://datafu.incubator.apache.org/docs/datafu/guide.html).
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
