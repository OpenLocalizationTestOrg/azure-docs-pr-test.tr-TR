---
title: "Azure HDInsight’ta güvenli aktarım depolama hesapları ile Hadoop kümesi oluşturma | Microsoft Docs"
description: "Güvenli aktarım özellikli Azure depolama hesapları ile HDInsight kümeleri oluşturma hakkında bilgi edinin."
keywords: "hadoop kullanmaya başlama,hadoop linux,hadoop hızlı başlangıç,güvenli aktarım,azure depolama hesabı"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 370b2f081930fe88527436a1a127309aed6681f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Azure HDInsight’ta güvenli aktarım depolama hesapları ile Hadoop kümesi oluşturma

[Güvenli aktarım gereklidir](../storage/common/storage-require-secure-transfer.md) özelliği, güvenli bir bağlantı üzerinden tüm istekleri hesabınıza uygulayarak Azure Depolama hesabınızın güvenliğini artırır. Bu özellik ve wasbs şeması yalnızca HDInsight kümesi 3.6 veya sonraki sürümlerde desteklenir. 

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce

* **Azure aboneliği** gereklidir. Bir aylık ücretsiz deneme hesabı oluşturmak için [azure.microsoft.com/free](https://azure.microsoft.com/free) adresine gidin.
* **Güvenli aktarım özellikli bir Azure depolama hesabı**. Yönergeler için bkz. [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) ve [Güvenli aktarım isteme](../storage/common/storage-require-secure-transfer.md).
* **Depolama hesabındaki bir Blob kapsayıcı**. 
## <a name="create-cluster"></a>Küme oluşturma

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


Bu bölümde, [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) kullanarak HDInsight'ta Hadoop kümesi oluşturacaksınız. Şablon [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/)’da vardır. Bu öğreticiyi kullanmak için Resource Manager şablonuyla deneyim sahibi olmak gerekli değildir. Diğer küme oluşturma yöntemleri ve bu öğreticide kullanılan özellikler hakkında bilgi edinmek için bkz. [HDInsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

1. Aşağıdaki resme tıklayarak Azure'da oturum açın ve Azure portalında Resource Manager şablonunu açın. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. Aşağıdaki özelliklerle kümeyi oluşturmak için yönergeleri izleyin: 

    - HDInsight sürümü 3.6’yı belirtin.  Varsayılan sürüm 3.5'tir. 3.6 veya daha yeni bir sürüm gereklidir.
    - Güvenli aktarım özellikli bir depolama hesabı belirtin.
    - Depolama hesabı için kısa bir ad kullanın.
    - Hem depolama hesabı hem de blob kapsayıcı önceden oluşturulmalıdır. 

    Yönergeler için bkz. [Küme oluşturma](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Kendi yapılandırma dosyalarınızı sağlamak için betik eylemi kullanıyorsanız, aşağıdaki ayarlarda wasbs kullanmanız gerekir:

- fs.defaultFS (çekirdek-site)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Başka depolama hesapları ekleme

Güvenli aktarım özellikli başka depolama hesapları eklemek için birkaç seçenek vardır:

- Son bölümdeki Azure Resource Manager şablonunu değiştirin.
- [Azure portalını](https://portal.azure.com) kullanarak bir küme oluşturun ve bağlı depolama hesabını belirtin.
- Var olan bir HDInsight kümesine güvenli aktarım özellikli başka depolama hesapları eklemek için betik eylemini kullanın.  Daha fazla bilgi için bkz. [HDInsight’a başka depolama hesapları ekleme](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide bir HDInsight kümesi oluşturmayı ve depolama hesaplarına güvenli aktarımı etkinleştirmeyi öğrendiniz.

HDInsight ile veri çözümleme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

* Visual Studio'da Hive sorguları gerçekleştirme dahil, HDInsight ile Hive kullanma hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].
* Verileri dönüştürmek için kullanılan bir dil olan Pig hakkında bilgi için bkz. [HDInsight ile Pig kullanma][hdinsight-use-pig].
* Hadoop’ta verileri işleyen programları yazmanın bir yöntemi olan MapReduce hakkında bilgi edinmek için bkz. [HDInsight ile MapReduce kullanma][hdinsight-use-mapreduce].
* HDInsight’taki verileri çözümlemek amacıyla Visual Studio için HDInsight Araçları kullanma hakkında bilgi edinmek için bkz. [HDInsight için Visual Studio Hadoop araçlarını kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

HDInsight’ın verileri nasıl depoladığı veya HDInsight’a verilerin nasıl alındığı hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

* HDInsight’ın Azure Depolama’yı nasıl kullandığı hakkında daha fazla bilgi için bkz. [HDInsight ile Azure Depolama kullanma](hdinsight-hadoop-use-blob-storage.md).
* HDInsight’a veril yükleme hakkında daha fazla bilgi için bkz. [Verileri HDInsight’a yükleme][hdinsight-upload-data].

HDInsight kümesi oluşturma ve yönetme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:

* Linux tabanlı HDInsight kümenizi yönetme hakkında bilgi edinmek için bkz. [Ambari kullanarak HDInsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).
* HDInsight kümesi oluştururken tercih edebileceğiniz seçenekler hakkında daha fazla bilgi için bkz. [Özel seçenekleri kullanarak Linux’ta HDInsight oluşturma](hdinsight-hadoop-provision-linux-clusters.md).
* Linux ve Hadoop hakkında bilgi sahibiyseniz, ancak HDInsight’ta Hadoop’a ilişkin teknik özellikleri öğrenmek istiyorsanız, bkz: [Linux’ta HDInsight ile çalışma](hdinsight-hadoop-linux-information.md). Bu makale aşağıdaki gibi bilgiler sağlar:
  
  * Ambari ve WebHCat gibi küme üzerinde barındırılan hizmetlerin URL'leri
  * Yerel dosya sisteminde Hadoop dosyalarının ve örneklerin konumu
  * Varsayılan veri depolama olarak HDFS yerine Azure Storage (WASB) kullanımı

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


