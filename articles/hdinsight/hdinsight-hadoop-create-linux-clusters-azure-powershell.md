---
title: "aaaCreate Hadoop kümeleri PowerShell - Azure Hdınsight kullanarak | Microsoft Docs"
description: "Nasıl toocreate Hadoop, HBase, Storm ve Spark Linux'ta Hdınsight için Azure PowerShell kullanarak kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Azure PowerShell kullanarak Hdınsight'ta Linux tabanlı kümeleri oluşturma

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell toocontrol kullanın ve hello dağıtımını ve yönetimini Microsoft Azure, iş yüklerini otomatikleştirmek bir güçlü komut dosyası ortamıdır. Bu belge nasıl toocreate Linux tabanlı Hdınsight küme Azure PowerShell kullanarak hakkında bilgi sağlar. Ayrıca, bir örnek komut dosyası içerir.

> [!NOTE]
> Azure PowerShell yalnızca Windows istemcileri üzerinde kullanılabilir. Linux, Unix ya da Mac OS X istemci kullanıyorsanız, bkz: [Azure CLI kullanarak bir Linux tabanlı Hdınsight kümesi oluşturma](hdinsight-hadoop-create-linux-clusters-azure-cli.md) hello Azure CLI toocreate bir küme kullanma hakkında bilgi.

## <a name="prerequisites"></a>Ön koşullar
Bu yordamı başlatmadan önce hello şunlara sahip olmanız gerekir:

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır. Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.
    >
    > Lütfen başlangıç adımları [Azure PowerShell yükleme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello en son Azure PowerShell sürümü. Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.

## <a name="create-cluster"></a>Küme oluşturma

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Azure PowerShell kullanarak bir Hdınsight kümesi toocreate hello yordamları tamamlamanız gerekir:

* Bir Azure kaynak grubu oluşturun
* Azure Depolama hesabı oluşturma
* Bir Azure Blob kapsayıcı oluşturun
* Hdınsight kümesi oluşturma

Merhaba aşağıdaki komut dosyası gösterilmektedir nasıl toocreate yeni bir küme:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

Merhaba küme oturum açma için belirttiğiniz hello kullanılan toocreate hello hello kümesi için Hadoop kullanıcı hesabına değerlerdir. Bu hesap tooconnect tooservices web Uı'lar veya REST API'leri gibi hello kümesi üzerinde barındırılan kullanın.

Merhaba SSH kullanıcı için belirttiğiniz hello hello kümesi için kullanılan toocreate hello SSH kullanıcı değerlerdir. Bu hesap uzak SSH oturumu toostart hello kümede ve işleri çalıştırma. Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

> [!IMPORTANT]
> (Küme oluşturma sırasında veya ölçeklendirme hello Küme oluşturulduktan sonra) 32'den fazla çalışan düğümleri toouse planlıyorsanız, ayrıca bir baş düğüm boyutu, en az 8 çekirdek ve 14 GB RAM belirtmeniz gerekir.
>
> Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).

Bir küme too20 dakika toocreate devam edebilir.

## <a name="create-cluster-configuration-object"></a>Küme oluşturma: Yapılandırma nesnesi

Ayrıca bir Hdınsight yapılandırma nesnesi kullanarak oluşturabileceğiniz `New-AzureRmHDInsightClusterConfig` cmdlet'i. Bu yapılandırma nesnesi tooenable ek yapılandırma seçenekleri, kümeniz için daha sonra değiştirebilirsiniz. Son olarak, hello kullan `-Config` hello parametresinin `New-AzureRmHDInsightCluster` cmdlet toouse hello yapılandırma.

Merhaba aşağıdaki betiği bir yapılandırma nesnesi tooconfigure bir R Server Hdınsight küme türü üzerinde oluşturur. Merhaba yapılandırma bir edge düğümünü, Rstudio'dan ve ek depolama alanı hesabı etkinleştirir.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Merhaba Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor. Bu örnek kullanırken hello hello ek depolama hesabı oluşturma hello sunucusu olarak aynı konumu.

## <a name="customize-clusters"></a>Kümeleri özelleştirme

* Bkz: [önyükleme kullanarak özelleştirme Hdınsight kümelerini](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Merhaba küme silme

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight kümesi başarıyla oluşturduğunuza göre kaynakları toolearn nasıl aşağıdaki hello kullanmak toowork kümenizi ile.

### <a name="hadoop-clusters"></a>Hadoop kümeleri

* [HDInsight ile Hive kullanma](hdinsight-use-hive.md)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase kümeleri

* [Hdınsight'ta HBase kullanmaya başlama](hdinsight-hbase-tutorial-get-started-linux.md)
* [Hdınsight'ta HBase için Java uygulamaları geliştirme](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm kümeleri

* [Hdınsight üzerinde Storm için Java topolojisi geliştirme](hdinsight-storm-develop-java-topology.md)
* [Hdınsight üzerinde Storm Python bileşenleri kullanma](hdinsight-storm-develop-python-topology.md)
* [Dağıtma ve hdınsight'ta Storm topolojileri izleme](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark kümeleri

* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)

