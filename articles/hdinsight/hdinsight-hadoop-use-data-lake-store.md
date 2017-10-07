---
title: "Data Lake Store Azure hdınsight'ta Hadoop ile aaaUse | Microsoft Docs"
description: "Azure Data Lake Store ve toostore tooquery verilerini nasıl sonuçları öğrenin çözümleme."
keywords: "blob depolama,hdfs,yapılandırılmış veriler,yapılandırılmamış veriler, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Data Lake Store’u Azure HDInsight kümeleriyle kullanma

Hdınsight kümesi tooanalyze verilerin depolayabileceğiniz hello veri ya da içinde [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), veya her ikisini de. Her iki depolama seçeneklerini kullanıcı verilerini kaybetmeden hesaplama için kullanılan Hdınsight kümeleri toosafely delete etkinleştirin.

Bu makalede Data Lake Store’un HDInsight kümeleri ile nasıl çalıştığı hakkında bilgi edinebilirsiniz. Azure Storage Hdınsight kümeleri ile nasıl çalışır toolearn bkz [kullanım Azure Storage ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-blob-storage.md). HDInsight kümesi oluşturma hakkında daha fazla bilgi için bkz. [HDInsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

> [!NOTE]
> Data Lake Store’a her zaman güvenli bir kanal üzerinden erişildiğinden, `adls` dosya sistemi düzen adı yoktur. Her zaman `adl` kullanırsınız.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>HDInsight kümeleri için kullanılabilirlik durumları

Hadoop hello varsayılan dosya sistemi kavramını destekler. Merhaba varsayılan dosya sistemi varsayılan şema ve yetkilisi anlamına gelir. Kullanılan tooresolve göreli yollar da olabilir. Merhaba Hdınsight küme oluşturma işlemi sırasında hello varsayılan dosya sistemi olarak Azure storage'da bir blob kapsayıcısını belirtebilirsiniz ya da Hdınsight 3.5 ve yeni sürümler ile Azure Storage veya Azure Data Lake Store ile Merhaba varsayılan dosya sistemi olarak seçebileceğiniz bir birkaç özel durum. 

HDInsight kümeleri Data Lake Store’u iki şekilde kullanabilir:

* Merhaba varsayılan depolama alanı olarak
* Azure Depolama Blobunun varsayılan depolama alanı olduğu durumlarda ek depolama alanı olarak.

Şimdi itibariyle hello Hdınsight yalnızca bazıları varsayılan depolama ve ek depolama hesapları Data Lake Store kullanan türleri/sürümleri desteği küme:

| HDInsight küme türü | Varsayılan depolama alanı olarak Azure Data Lake Store | Ek depolama alanı olarak Azure Data Lake Store| Notlar |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight sürümü 3.6 | Evet | Evet | |
| HDInsight sürümü 3.5 | Evet | Evet | HBase Hello özel durumuyla|
| HDInsight sürümü 3.4 | Hayır | Evet | |
| HDInsight sürümü 3.3 | Hayır | Hayır | |
| HDInsight sürümü 3.2 | Hayır | Evet | |
| HDInsight Premium (katman)| Hayır | Hayır | |
| Storm | | |Data Lake Store toowrite veri bir Storm topolojisinin kullanabilirsiniz. Data Lake Store’u daha sonra bir Storm topolojisinden okunabilecek başvuru verileri için de kullanabilirsiniz.|

Data Lake Store ek depolama alanı hesabı olarak kullanarak performans veya hello özelliği tooread etkilemez veya hello kümeden tooAzure depolama yazma.


## <a name="use-data-lake-store-as-default-storage"></a>Azure Data Lake Store’u varsayılan depolama alanı olarak kullanma

Hdınsight, Data Lake Store varsayılan depolama ile dağıtıldığında, hello küme ilgili dosyaları konumu aşağıdaki hello Data Lake Store içinde depolanır:

    adl://mydatalakestore/<cluster_root_path>/

Burada `<cluster_root_path>` Data Lake Store içinde oluşturduğunuz bir klasöre hello adıdır. Her küme için kök yolu belirterek kullanabilirsiniz hello birden fazla küme için aynı Data Lake Store hesabı. Bunu yaptığınızda şöyle bir durum olabilir:

* Cluster1 hello yolu kullanabilirsiniz`adl://mydatalakestore/cluster1storage`
* Cluster2 hello yolu kullanabilirsiniz`adl://mydatalakestore/cluster2storage`

Her ikisi de kümeleri kullanım hello bildirimi hello aynı Data Lake Store hesabı **mydatalakestore**. Her küme Data Lake Store'da kök dosya sistemine sahip erişim tooits sahiptir. Hello Azure portalı dağıtımının deneyimi özellikle sizden toouse bir klasör adı gibi **/clusters/\<clustername >** hello kök yolu.

toobe mümkün toouse varsayılan depolama olarak Data Lake Store, yolları aşağıdaki hello hizmet asıl erişim toohello vermesi gerekir:

- Merhaba Data Lake Store hesabı kökü.  Örneğin: adl://mydatalakestore/.
- tüm küme klasörleri için başlangıç klasörü.  Örneğin: adl://mydatalakestore/clusters.
- Merhaba küme için başlangıç klasörü.  Örneğin: adl://mydatalakestore/clusters/cluster1storage.

Hizmet sorumlusu oluşturma ve erişim verme hakkında daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).


## <a name="use-data-lake-store-as-additional-storage"></a>Azure Data Lake Store’u ek depolama alanı olarak kullanma

Data Lake Store de hello küme için ek depolama alanı olarak kullanabilirsiniz. Böyle durumlarda, hello kümenin varsayılan depolama ya da bir Azure depolama Blob veya bir Data Lake Store hesabı olabilir. Ek depolama alanı olarak Data Lake Store'da depolanan hello verileri karşı Hdınsight iş devam ediyorsa, hello tam yolu toohello dosyalarını kullanmanız gerekir. Örneğin:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Unutmayın hiçbir **cluster_root_path** şimdi hello URL'de. Tüm toodo gereken hello yolu toohello dosyalarını sağlamak Data Lake Store varsayılan depolama bu durumda olmadığından olmasıdır.

toobe mümkün toouse ek depolama alanı olarak Data Lake Store, yalnızca toogrant hello hizmet asıl erişim toohello yolları dosyalarınızı nerede depolanacağını gerekir.  Örneğin:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Hizmet sorumlusu oluşturma ve erişim verme hakkında daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).


## <a name="use-more-than-one-data-lake-store-accounts"></a>Birden çok Data Lake Store hesabı kullanma

Bir Data Lake Store hesabına ek olarak ekleme ve birden fazla Data Lake Store ekleyerek bir veya daha fazla Data Lake Store hesapları veriler üzerinde hello Hdınsight küme izin vererek hesapları gerçekleştirilebilir. Bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Data Lake Store erişimini yapılandırma

Data Lake deposu erişimini Hdınsight kümenize tooconfigure, bir Azure Active directory (Azure AD) hizmet asıl olması gerekir. Hizmet sorumlusu yalnızca bir Azure AD yöneticisi tarafından oluşturulabilir. Merhaba hizmet sorumlusu sahip bir sertifika oluşturulması gerekir. Daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) ve [Otomatik olarak imzalanan sertifika ile hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Hdınsight kümesi için ek depolama alanı olarak toouse Azure Data Lake Store kullanacaksanız, bu makalede anlatıldığı gibi hello küme oluştururken bunu yapmanızı öneririz. Ek depolama alanı tooan Azure Data Lake Store ekleme olan bir Hdınsight kümesine bir karmaşık bir işlem yatkın tooerrors ise.
>

## <a name="access-files-from-hello-cluster"></a>Merhaba kümeden Access dosyalarını

Bir Hdınsight kümeden Data Lake Store hello dosyalarına erişebilirsiniz birkaç yolu vardır.

* **Merhaba tam adını kullanarak**. Bu yaklaşımda, sağladığınız hello tam yol toohello dosya tooaccess istiyor.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Merhaba kısaltılmış yol biçimi kullanarak**. Bu yaklaşımda, adl ile toohello küme kök hello yolu değiştirin: / / /. Bu nedenle, hello yukarıdaki örnekte, değiştirebilirsiniz `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` ile `adl:///`.

        adl:///<file path>

* **Merhaba göreli yolu kullanarak**. Bu yaklaşımda, yalnızca hello göreli yol toohello dosya sağladığınız tooaccess istiyor. Örneğin, Hello tam yolunu toohello dosyası ise:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    Erişebilmeniz için bu göreli yolu kullanarak aynı sample.log dosya hello.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>Hdınsight kümeleri oluşturma ile tooData Lake deposuna erişim

Ayrıntılı yönergeleri için bağlantıları nasıl ile Hdınsight kümeleri toocreate erişim tooData Lake Store aşağıdaki hello kullanın.

* [Portalı kullanma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [PowerShell kullanma (varsayılan depolama alanı olarak Data Lake Store ile)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [PowerShell kullanma (ek depolama alanı olarak Data Lake Store ile)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Azure şablonlarını kullanma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, nasıl öğrenilen toouse Hdınsight ile HDFS uyumlu Azure Data Lake Store. Bu, toobuild ölçeklenebilir, uzun vadeli, arşivleme verileri edinme çözümleri ve kullanım depolanan hello içindeki Hdınsight toounlock hello bilgileri yapılandırılmış ve yapılandırılmamış verileri sağlar.

Daha fazla bilgi için bkz.

* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]
* [Azure Data Lake Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md)
* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [HDInsight ile Hive kullanma][hdinsight-use-hive]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight ile Azure Storage paylaşılan erişim imzaları toorestrict erişim toodata kullanma][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
