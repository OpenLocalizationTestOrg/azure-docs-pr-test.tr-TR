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
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="ecc3e-103">Hello Azure CLI kullanarak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecc3e-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="ecc3e-104">Merhaba, bu belge kılavuz hello Azure CLI 1.0 kullanarak bir Hdınsight 3.5 kümesi oluşturma adımları.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecc3e-105">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ecc3e-106">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ecc3e-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ecc3e-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ecc3e-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="ecc3e-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-108">**An Azure subscription**.</span></span> <span data-ttu-id="ecc3e-109">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ecc3e-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="ecc3e-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-110">**Azure CLI**.</span></span> <span data-ttu-id="ecc3e-111">Bu belgedeki Hello adımlar en son Azure CLI Sürüm 0.10.14 sınanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ecc3e-112">Merhaba adımları bu belgede, Azure CLI 2.0 ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="ecc3e-113">Azure CLI 2.0 Hdınsight kümesi oluşturmayı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="ecc3e-114">Azure aboneliği tooyour oturum</span><span class="sxs-lookup"><span data-stu-id="ecc3e-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="ecc3e-115">İçinde belirtilen başlangıç adımları [hello Azure komut satırı arabirimi (Azure CLI) tooan Azure aboneliğine bağlanma](../xplat-cli-connect.md) ve tooyour abonelik hello kullanarak bağlanmak **oturum açma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="ecc3e-116">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecc3e-116">Create a cluster</span></span>

<span data-ttu-id="ecc3e-117">Aşağıdaki adımları Merhaba, PowerShell veya Bash gibi bir komut satırından gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="ecc3e-118">Komut tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ecc3e-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="ecc3e-119">Adı ve parola istendiğinde tooprovide şunlardır.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="ecc3e-120">Birden çok Azure aboneliğiniz varsa, kullanmak `azure account set <subscriptionname>` Azure CLI hello tooset hello abonelik komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="ecc3e-121">Komutu aşağıdaki hello kullanarak tooAzure Resource Manager moduna geçin:</span><span class="sxs-lookup"><span data-stu-id="ecc3e-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="ecc3e-122">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-122">Create a resource group.</span></span> <span data-ttu-id="ecc3e-123">Bu kaynak grubu ve depolama hesabı ilişkili hello Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="ecc3e-124">Değiştir `groupname` hello grubu için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="ecc3e-125">Değiştir `location` toocreate hello Grup istediğiniz hello coğrafi bölge ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="ecc3e-126">Geçerli konumların bir listesini için hello kullan `azure location list` komut ve hello hello konumlardan birini kullanın `Name` sütun.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="ecc3e-127">Bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-127">Create a storage account.</span></span> <span data-ttu-id="ecc3e-128">Bu depolama hesabı hello varsayılan depolama alanı olarak hello Hdınsight kümesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="ecc3e-129">Değiştir `groupname` hello önceki adımda oluşturduğunuz hello grubunun hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="ecc3e-130">Değiştir `location` aynı konuma hello önceki adımda kullanılan hello ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="ecc3e-131">Değiştir `storagename` hello depolama hesabı için benzersiz bir ad ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="ecc3e-132">Bu komutta kullanılan hello parametreler hakkında daha fazla bilgi için kullanmak `azure storage account create -h` tooview Yardım için bu komutu.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="ecc3e-133">Alma hello anahtar tooaccess hello depolama hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="ecc3e-134">Değiştir `groupname` hello kaynak grubu adı ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="ecc3e-135">Değiştir `storagename` hello depolama hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="ecc3e-136">Döndürülen hello verilerde hello Kaydet `key` değerini `key1`.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="ecc3e-137">Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="ecc3e-138">Değiştir `groupname` hello kaynak grubu adı ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="ecc3e-139">Değiştir `Hadoop` hello küme türüyle toocreate istiyor.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="ecc3e-140">Örneğin, `Hadoop`, `HBase`, `Kafka`, `Spark`, veya `Storm`.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="ecc3e-141">Hdınsight kümeleri gelen toohello iş yükü karşılık gelen, çeşitli türlerinde veya için küme hello teknolojisi ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="ecc3e-142">Bir küme üzerinde Storm ve HBase gibi birden çok tür birleştiren bir küme için desteklenen yöntem toocreate yoktur.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="ecc3e-143">Değiştir `location` aynı konuma kullanılan önceki adımlarda hello ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="ecc3e-144">Değiştir `storagename` hello depolama hesabı adı ile.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="ecc3e-145">Değiştir `storagekey` hello önceki adımda elde hello anahtara sahip.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="ecc3e-146">Hello için `--defaultStorageContainer` parametresi, kullanım hello hello küme için kullandığınız gibi aynı adı.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="ecc3e-147">Değiştir `admin` ve `httppassword` hello adı ve parola ile toouse hello küme HTTPS erişirken istiyor.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="ecc3e-148">Değiştir `sshuser` ve `sshuserpassword` hello kullanıcı adı ve parola ile toouse SSH kullanarak hello küme erişirken istediğiniz</span><span class="sxs-lookup"><span data-stu-id="ecc3e-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ecc3e-149">Bu örnek iki alt notes ile bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="ecc3e-150">Çalışan düğüm sayısı hello Küme oluşturulduktan sonra ölçeklendirme işlemleri gerçekleştirerek de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="ecc3e-151">32'den fazla çalışan düğümleri kullanmayı planlıyorsanız, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB RAM ile seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="ecc3e-152">Hello kullanarak hello baş düğüm boyutu ayarlayabilirsiniz `--headNodeSize` küme oluşturma sırasında parametre.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="ecc3e-153">Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ecc3e-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="ecc3e-154">Merhaba küme oluşturma işlemi toofinish için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="ecc3e-155">Genellikle yaklaşık 15.</span><span class="sxs-lookup"><span data-stu-id="ecc3e-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="ecc3e-156">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ecc3e-156">Troubleshoot</span></span>

<span data-ttu-id="ecc3e-157">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="ecc3e-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecc3e-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ecc3e-158">Next steps</span></span>

<span data-ttu-id="ecc3e-159">Hello Azure CLI kullanarak bir Hdınsight kümesi başarıyla oluşturuldu, toolearn nasıl aşağıdaki hello kullan toowork kümenizi ile:</span><span class="sxs-lookup"><span data-stu-id="ecc3e-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="ecc3e-160">Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="ecc3e-160">Hadoop clusters</span></span>

* [<span data-ttu-id="ecc3e-161">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ecc3e-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ecc3e-162">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="ecc3e-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ecc3e-163">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="ecc3e-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="ecc3e-164">HBase kümeleri</span><span class="sxs-lookup"><span data-stu-id="ecc3e-164">HBase clusters</span></span>

* [<span data-ttu-id="ecc3e-165">Hdınsight'ta HBase kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ecc3e-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="ecc3e-166">Hdınsight'ta HBase için Java uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="ecc3e-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="ecc3e-167">Storm kümeleri</span><span class="sxs-lookup"><span data-stu-id="ecc3e-167">Storm clusters</span></span>

* [<span data-ttu-id="ecc3e-168">Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="ecc3e-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ecc3e-169">Hdınsight üzerinde Storm Python bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="ecc3e-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="ecc3e-170">Dağıtma ve hdınsight'ta Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="ecc3e-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
