---
title: "aaaCreate Hadoop küme Azure hdınsight'ta güvenli aktarımı depolama hesaplarıyla | Microsoft Docs"
description: "Azure depolama hesapları toocreate Hdınsight kümeleri güvenli aktarımı ile nasıl etkin öğrenin."
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
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Azure HDInsight’ta güvenli aktarım depolama hesapları ile Hadoop kümesi oluşturma

Merhaba [güvenli aktarımı gerekli](../storage/common/storage-require-secure-transfer.md) özelliğini, tüm istekleri tooyour hesabı güvenli bir bağlantı üzerinden zorlayarak hello Azure depolama hesabınızın güvenliğini geliştirir. Bu özellik ve hello wasbs şeması yalnızca 3,6 ya da daha yeni Hdınsight küme sürümü tarafından desteklenir. 

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce

* **Azure aboneliği**: toocreate ücretsiz bir aylık deneme hesabı, Gözat çok[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Güvenli aktarım özellikli bir Azure depolama hesabı**. Merhaba yönergeler için bkz: [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) ve [güvenli aktarımı gerektiren](../storage/common/storage-require-secure-transfer.md).
* **Merhaba depolama hesabındaki bir Blob kapsayıcısını**. 
## <a name="create-cluster"></a>Küme oluşturma

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


Bu bölümde, [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) kullanarak HDInsight'ta Hadoop kümesi oluşturacaksınız. Merhaba şablon bulunduğu [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Bu öğreticiyi kullanmak için Resource Manager şablonuyla deneyim sahibi olmak gerekli değildir. Diğer küme oluşturma yöntemleri ve Bu öğreticide kullanılan hello özellikler hakkında bilgi edinmek bkz [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).

1. Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Merhaba yönergeleri toocreate hello küme belirtimleri aşağıdaki hello ile izleyin: 

    - HDInsight sürümü 3.6’yı belirtin.  3.5 Hello varsayılan sürümdür. 3.6 veya daha yeni bir sürüm gereklidir.
    - Güvenli aktarım özellikli bir depolama hesabı belirtin.
    - Merhaba depolama hesabı için kısa bir ad kullanın.
    - Merhaba depolama hesabı ve hello blob kapsayıcısı önceden oluşturulmuş olması gerekir. 

    Merhaba yönergeler için bkz: [küme oluştur](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Betik eylemi tooprovide kendi yapılandırma dosyaları kullanırsanız, ayarlar aşağıdaki hello wasbs kullanmanız gerekir:

- fs.defaultFS (çekirdek-site)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Başka depolama hesapları ekleme

Çeşitli seçenekler tooadd etkin ek güvenli aktarımı depolama hesapları vardır:

- Hello Azure Resource Manager şablonu hello son bölümünde değiştirin.
- Hello kullanarak bir küme oluşturmak [Azure portal](https://portal.azure.com) ve bağlantılı depolama hesabı belirtin.
- Betik eylemi tooadd ek güvenli aktarımı kullanın depolama hesapları tooan varolan Hdınsight kümesi etkin.  Daha fazla bilgi için bkz: [ek depolama hesapları tooHDInsight eklemek](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide, nasıl toohello depolama hesapları toocreate Hdınsight kümesi ve etkinleştir güvenli aktarımı öğrendiniz.

Hdınsight ile verileri çözümleme hakkında daha fazla toolearn makaleler hello bakın:

* Visual Studio'dan nasıl tooperform Hive sorguları dahil, Hdınsight ile Hive kullanma hakkında daha fazla toolearn bkz [Hdınsight ile Hive kullanma][hdinsight-use-hive].
* toolearn Pig hakkında bir dilde kullanılan tootransform veri bkz [Hdınsight ile Pig kullanma][hdinsight-use-pig].
* toolearn MapReduce, hadoop'ta verileri işleyen bir şekilde toowrite programlar hakkında bkz [Hdınsight ile MapReduce kullanma][hdinsight-use-mapreduce].
* Hdınsight, Visual Studio tooanalyze verileri hello Hdınsight araçları kullanma hakkında toolearn bkz [Hdınsight için Visual Studio Hadoop araçlarını kullanmaya başlamanıza](hdinsight-hadoop-visual-studio-tools-get-started.md).

Hdınsight veri saklama biçimi hakkında daha fazla toolearn veya nasıl Hdınsight, tooget verisine makaleler hello bakın:

* HDInsight’ın Azure Depolama’yı nasıl kullandığı hakkında daha fazla bilgi için bkz. [HDInsight ile Azure Depolama kullanma](hdinsight-hadoop-use-blob-storage.md).
* Hakkında bilgi için tooupload veri tooHDInsight bkz [karşıya veri tooHDInsight][hdinsight-upload-data].

oluşturma veya bir Hdınsight kümesi yönetme hakkında daha fazla toolearn makaleler hello bakın:

* Linux tabanlı Hdınsight kümenizi yönetme hakkında toolearn bkz [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).
* toolearn daha seçebileceğiniz bir Hdınsight kümesi oluştururken hello seçenekleri hakkında bkz [özel seçenekleri kullanarak Linux'ta Hdınsight oluşturma](hdinsight-hadoop-provision-linux-clusters.md).
* Linux ve Hadoop hakkında bilginiz ancak tooknow hadoop'a ilişkin teknik özellikleri hello Hdınsight üzerinde istiyorsanız bkz [Linux'ta Hdınsight ile çalışma](hdinsight-hadoop-linux-information.md). Bu makale aşağıdaki gibi bilgiler sağlar:
  
  * Ambari ve WebHCat gibi hello kümesi üzerinde barındırılan hizmetlerin URL'leri
  * Hadoop dosyalarının ve örneklerin hello yerel dosya sisteminde Hello konumu
  * Merhaba varsayılan veri deposu olarak, Azure Storage (WASB) HDFS yerine Hello kullan

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


