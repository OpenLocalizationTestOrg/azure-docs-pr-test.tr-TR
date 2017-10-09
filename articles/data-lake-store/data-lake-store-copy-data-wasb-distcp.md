---
title: "aaaCopy veri tooand WASB Distcp'yi kullanarak Data Lake Store içine gelen | Microsoft Docs"
description: "Azure depolama BLOB'lar tooData Lake deposundan Distcp'yi aracı toocopy veri tooand kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Azure Storage Bloblarında ve Data Lake Store arasında Distcp'yi toocopy veri kullanın
> [!div class="op_single_selector"]
> * [DistCp’yi kullanma](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy’yi kullanma](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Erişim tooa Data Lake Store hesabı olan bir Hdınsight kümesi oluşturduktan sonra Distcp'yi toocopy veri gibi Hadoop ekosistemi araçları kullanabilirsiniz **tooand gelen** Data Lake Store hesabında bir Hdınsight küme depolama (WASB). Bu makalede hakkında yönergeler sağlar tooachieve bu.

## <a name="prerequisites"></a>Ön koşullar
Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* **Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile. Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md). Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.

## <a name="do-you-learn-fast-with-videos"></a>Videolarla daha hızlı mı öğreniyorsunuz?
[Bu videoyu izleyin](https://mix.office.com/watch/1liuojvdx6sie) nasıl toocopy verileri Azure Storage Bloblarında ve Distcp'yi kullanarak Data Lake Store arasında.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>Bir Hdınsight Linux kümeden Distcp'yi kullanın

Bir Hdınsight kümesine farklı kaynaklardan kullanılan toocopy veri olabilir hello Distcp'yi yardımcı olan bir Hdınsight kümesi gelir. Ek depolama alanı hello Hdınsight küme toouse Data Lake Store yapılandırdıysanız, hello yardımcı olabilir Distcp'yi Giden kutusu toocopy veri tooand da Data Lake Store hesabından kullanılır. Bu bölümde nasıl toouse hello adresindeki Distcp'yi yardımcı programı arayın.

1. Masaüstünüzdeki, SSH tooconnect toohello küme kullanın. Bkz: [Bağlan tooa Linux tabanlı Hdınsight kümesi](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md). Merhaba SSH isteminden Hello komutları çalıştırın.

2. Hello Azure Storage Blobları (WASB) erişim olup olmadığını doğrulayın. Merhaba aşağıdaki komutu çalıştırın:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    Bu depolama blobu Merhaba içeriğine listesini sağlamanız gerekir.
3. Benzer şekilde, hello kümeden hello Data Lake Store hesabı erişip erişemeyeceğini doğrulayın. Merhaba aşağıdaki komutu çalıştırın:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    Bu dosyalar/klasörler hello Data Lake Store hesabı içinde listesini sağlamanız gerekir.
4. Distcp'yi toocopy verileri WASB tooa Data Lake Store hesabı kullanın.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    Bu hello Merhaba içeriğine kopyalayacak **/örnek/data/gutenberg/** WASB klasöründe çok**/myfolder** hello Data Lake Store hesabı içinde.
5. Benzer şekilde, Data Lake Store hesabı tooWASB Distcp'yi toocopy verileri kullanın.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    Bu Merhaba içeriğine kopyalayacak **/myfolder** çok hello Data Lake Store hesabı**/örnek/data/gutenberg/** WASB klasöründe.

## <a name="performance-considerations-while-using-distcp"></a>Distcp'yi kullanırken performans etkenleri

Distcp'yi düşük olduğundan ayrıntı düzeyi tek bir dosya, ayar hello en fazla sayıda eşzamanlı kopyasını hello en önemli parametre toooptimize Data Lake Store karşı. Bu mappers hello sayısını ayarlayarak denetlenir ('M ') hello komut satırı parametresi. Bu parametre kullanılan toocopy verileri mappers hello sayısını belirtir. Varsayılan değer 20'dir.

**Örnek**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>Mappers toouse hello sayısını nasıl belirlerim?

Aşağıda kullanabileceğiniz bazı yönergeler verilmiştir.

* **1. adım: toplam YARN bellek belirlemek** -hello ilk adımdır hello Distcp'yi iş çalıştırdığı toodetermine hello YARN bellek kullanılabilir toohello küme. Bu bilgiler, hello kümesi ile ilişkili hello Ambari portalında kullanılabilir. TooYARN gidin ve hello yapılandırmalar sekmesi toosee hello YARN bellek görüntüleyin. tooget hello toplam YARN bellek, Çarp hello hello düğüm sayısı ile düğüm başına YARN bellek kümenizdeki sahip.

* **2. adım: mappers hello sayısını hesaplayın** -hello değerini **m** eşit toohello sayının toplam YARN bellek YARN kapsayıcı boyutu hello tarafından ayrılmış olan. Merhaba YARN kapsayıcı boyutu bilgileri hello Ambari Portalı'nda da kullanılabilir. TooYARN gidin ve görünüm hello yapılandırmalar sekmesini hello YARN kapsayıcı boyutu Bu pencerede görüntülenir. Eşitlik tooarrive mappers hello numarasına hello (**m**) değil

        m = (number of nodes * YARN memory for each node) / YARN container size

**Örnek**

Merhaba kümede 4 D14v2s düğüm varsa ve tootransfer 10 TB çalıştığınız varsayalım 10 farklı klasörlerden veri. Hello klasörlerinin her biri değişen miktarda veri içerir ve her klasördeki hello dosya boyutları farklıdır.

* Toplam YARN bellekten - hello Ambari portal bu hello YARN bellek belirlemek için bir D14 düğümü 96 GB'dir. Bu nedenle, 4 düğümlü bir küme için toplam YARN bellek şöyledir: 

        YARN memory = 4 * 96GB = 384GB

* Mappers - hello 3072 D14 küme düğümü için bu hello YARN kapsayıcı boyutu olup Ambari Portalı'ndan sayısı. Bu nedenle, mappers sayısıdır:

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

Diğer uygulamalar bellek kullanıyorsanız için Distcp'yi kümenizin YARN belleğin bir kısmını tooonly kullanım seçebilirsiniz.

### <a name="copying-large-datasets"></a>Büyük veri kümelerini kopyalama

Ne zaman hello dataset toobe hello boyutunu taşınmış çok büyükse (örneğin > 1TB) veya birçok farklı klasörleri varsa, birden çok Distcp'yi işleri kullanmayı düşünmeniz gerekir. Büyük olasılıkla bir performans kazancı yoktur, ancak herhangi bir işi başarısız olursa, toorestart hello tüm iş yerine, belirli iş yalnızca gerekir böylece hello işleri yayılır.

### <a name="limitations"></a>Sınırlamalar

* Distcp'yi boyutu toooptimize performans benzer toocreate mappers çalışır. Mappers Hello sayısını artırmak her zaman performansı artırabilir değil.

* Distcp'yi sınırlı tooonly bir Eşleyici dosya başına ' dir. Bu nedenle, dosyaları olandan daha fazla mappers olmamalıdır. Distcp'yi tooa dosyası yalnızca bir Eşleyici atayabilirsiniz olduğundan, bu kullanılan toocopy büyük dosyalar olabilir eşzamanlılık hello miktarını sınırlar.

* Büyük dosyaların küçük bir sayıya sahip sonra 256 MB dosya öbekleri toogive bölme, daha fazla olası eşzamanlılık. 
 
* Bir Azure Blob Depolama hesabından kopyalıyorsanız kopyalama işini hello blob depolama tarafında kısıtlanan. Bu kopyalama işinin hello performansının düşmesine neden. Azure Blob Storage ' hello sınırları hakkında daha fazla toolearn adresindeki Azure depolama sınırları bkz [Azure aboneliği ve hizmet sınırları](../azure-subscription-service-limits.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama](data-lake-store-copy-data-azure-storage-blob.md)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)
