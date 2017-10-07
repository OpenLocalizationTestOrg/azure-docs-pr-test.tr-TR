---
title: "Merhaba komut satırı - Azure Hdınsight kullanarak aaaCreate Hadoop kümelerini | Microsoft Docs"
description: "Platformlar arası Azure CLI 1.0 kullanarak toocreate Hdınsight kümelerini nasıl hello öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Hello Azure CLI kullanarak Hdınsight kümeleri oluşturma

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Merhaba, bu belge kılavuz hello Azure CLI 1.0 kullanarak bir Hdınsight 3.5 kümesi oluşturma adımları.

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Ön koşullar

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Azure CLI**. Bu belgedeki Hello adımlar en son Azure CLI Sürüm 0.10.14 sınanmıştır.

    > [!IMPORTANT]
    > Merhaba adımları bu belgede, Azure CLI 2.0 ile çalışmaz. Azure CLI 2.0 Hdınsight kümesi oluşturmayı desteklemez.

## <a name="log-in-tooyour-azure-subscription"></a>Azure aboneliği tooyour oturum

İçinde belirtilen başlangıç adımları [hello Azure komut satırı arabirimi (Azure CLI) tooan Azure aboneliğine bağlanma](../xplat-cli-connect.md) ve tooyour abonelik hello kullanarak bağlanmak **oturum açma** yöntemi.

## <a name="create-a-cluster"></a>Küme oluşturma

Aşağıdaki adımları Merhaba, PowerShell veya Bash gibi bir komut satırından gerçekleştirilmelidir.

1. Komut tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullan:

        azure login

    Adı ve parola istendiğinde tooprovide şunlardır. Birden çok Azure aboneliğiniz varsa, kullanmak `azure account set <subscriptionname>` Azure CLI hello tooset hello abonelik komutları kullanın.

2. Komutu aşağıdaki hello kullanarak tooAzure Resource Manager moduna geçin:

        azure config mode arm

3. Bir kaynak grubu oluşturun. Bu kaynak grubu ve depolama hesabı ilişkili hello Hdınsight kümesi içerir.

        azure group create groupname location

    * Değiştir `groupname` hello grubu için benzersiz bir ada sahip.

    * Değiştir `location` toocreate hello Grup istediğiniz hello coğrafi bölge ile.

       Geçerli konumların bir listesini için hello kullan `azure location list` komut ve hello hello konumlardan birini kullanın `Name` sütun.

4. Bir depolama hesabı oluşturun. Bu depolama hesabı hello varsayılan depolama alanı olarak hello Hdınsight kümesi için kullanılır.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Değiştir `groupname` hello önceki adımda oluşturduğunuz hello grubunun hello ada sahip.

    * Değiştir `location` aynı konuma hello önceki adımda kullanılan hello ile.

    * Değiştir `storagename` hello depolama hesabı için benzersiz bir ad ile.

        > [!NOTE]
        > Bu komutta kullanılan hello parametreler hakkında daha fazla bilgi için kullanmak `azure storage account create -h` tooview Yardım için bu komutu.

5. Alma hello anahtar tooaccess hello depolama hesabı kullanılır.

        azure storage account keys list -g groupname storagename

    * Değiştir `groupname` hello kaynak grubu adı ile.
    * Değiştir `storagename` hello depolama hesabı hello adı.

     Döndürülen hello verilerde hello Kaydet `key` değerini `key1`.

6. Hdınsight kümesi oluşturun.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Değiştir `groupname` hello kaynak grubu adı ile.

    * Değiştir `Hadoop` hello küme türüyle toocreate istiyor. Örneğin, `Hadoop`, `HBase`, `Kafka`, `Spark`, veya `Storm`.

     > [!IMPORTANT]
     > Hdınsight kümeleri gelen toohello iş yükü karşılık gelen, çeşitli türlerinde veya için küme hello teknolojisi ayarlanmış. Bir küme üzerinde Storm ve HBase gibi birden çok tür birleştiren bir küme için desteklenen yöntem toocreate yoktur.

    * Değiştir `location` aynı konuma kullanılan önceki adımlarda hello ile.

    * Değiştir `storagename` hello depolama hesabı adı ile.

    * Değiştir `storagekey` hello önceki adımda elde hello anahtara sahip.

    * Hello için `--defaultStorageContainer` parametresi, kullanım hello hello küme için kullandığınız gibi aynı adı.

    * Değiştir `admin` ve `httppassword` hello adı ve parola ile toouse hello küme HTTPS erişirken istiyor.

    * Değiştir `sshuser` ve `sshuserpassword` hello kullanıcı adı ve parola ile toouse SSH kullanarak hello küme erişirken istediğiniz

    > [!IMPORTANT]
    > Bu örnek iki alt notes ile bir küme oluşturur. Çalışan düğüm sayısı hello Küme oluşturulduktan sonra ölçeklendirme işlemleri gerçekleştirerek de değiştirebilirsiniz. 32'den fazla çalışan düğümleri kullanmayı planlıyorsanız, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB RAM ile seçmeniz gerekir. Hello kullanarak hello baş düğüm boyutu ayarlayabilirsiniz `--headNodeSize` küme oluşturma sırasında parametre.
    >
    > Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).

    Merhaba küme oluşturma işlemi toofinish için birkaç dakika sürebilir. Genellikle yaklaşık 15.

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI kullanarak bir Hdınsight kümesi başarıyla oluşturuldu, toolearn nasıl aşağıdaki hello kullan toowork kümenizi ile:

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
