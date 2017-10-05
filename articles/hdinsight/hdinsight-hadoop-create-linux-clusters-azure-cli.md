---
title: "Komut satırı-Azure Hdınsight kullanarak Hadoop kümeleri oluşturma | Microsoft Docs"
description: "Platformlar arası Azure CLI 1.0 kullanarak Hdınsight kümelerini oluşturmayı öğrenin."
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
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="004f2-103">Azure CLI kullanarak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="004f2-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="004f2-104">Azure CLI 1.0 kullanarak Hdınsight 3.5 küme oluşturma bu belgeyi gözden geçirme adımları.</span><span class="sxs-lookup"><span data-stu-id="004f2-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="004f2-105">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="004f2-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="004f2-106">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="004f2-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="004f2-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="004f2-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="004f2-108">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="004f2-108">**An Azure subscription**.</span></span> <span data-ttu-id="004f2-109">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="004f2-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="004f2-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="004f2-110">**Azure CLI**.</span></span> <span data-ttu-id="004f2-111">Bu belgede yer alan adımlar, en son Azure CLI Sürüm 0.10.14 test edilmiş.</span><span class="sxs-lookup"><span data-stu-id="004f2-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="004f2-112">Bu belgede yer alan adımlar, Azure CLI 2.0 ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="004f2-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="004f2-113">Azure CLI 2.0 Hdınsight kümesi oluşturmayı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="004f2-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="004f2-114">Azure aboneliğinizde oturum açın</span><span class="sxs-lookup"><span data-stu-id="004f2-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="004f2-115">[Azure Komut Satırı Arabirimi'nden (Azure CLI) bir Azure aboneliğine bağlanma](../xplat-cli-connect.md) konusunda belgelenen adımları izleyin ve **oturum açma** yöntemini kullanarak aboneliğinze bağlanın.</span><span class="sxs-lookup"><span data-stu-id="004f2-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="004f2-116">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="004f2-116">Create a cluster</span></span>

<span data-ttu-id="004f2-117">Aşağıdaki adımlar, PowerShell veya Bash gibi bir komut satırından gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="004f2-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="004f2-118">Azure aboneliğinize kimliğini doğrulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="004f2-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="004f2-119">Adınızı ve parolanızı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="004f2-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="004f2-120">Birden çok Azure aboneliğiniz varsa, kullanmak `azure account set <subscriptionname>` Azure CLI komutları kullanın aboneliği ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="004f2-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="004f2-121">Şu komutu kullanarak Azure Resource Manager moduna geçin:</span><span class="sxs-lookup"><span data-stu-id="004f2-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="004f2-122">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="004f2-122">Create a resource group.</span></span> <span data-ttu-id="004f2-123">Bu kaynak grubu ve depolama hesabı ilişkili Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="004f2-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="004f2-124">Değiştir `groupname` grubu için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="004f2-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="004f2-125">Değiştir `location` grubunda oluşturmak istediğiniz coğrafi bölge ile.</span><span class="sxs-lookup"><span data-stu-id="004f2-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="004f2-126">Geçerli konumların bir listesini için kullanmak `azure location list` komut ve konumlardan birini kullanın `Name` sütun.</span><span class="sxs-lookup"><span data-stu-id="004f2-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="004f2-127">Bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="004f2-127">Create a storage account.</span></span> <span data-ttu-id="004f2-128">Bu depolama hesabı Hdınsight kümesi için varsayılan depolama alanı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="004f2-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="004f2-129">Değiştir `groupname` önceki adımda oluşturulan grup adı.</span><span class="sxs-lookup"><span data-stu-id="004f2-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="004f2-130">Değiştir `location` önceki adımda kullanılan aynı konum.</span><span class="sxs-lookup"><span data-stu-id="004f2-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="004f2-131">Değiştir `storagename` depolama hesabı için benzersiz bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="004f2-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="004f2-132">Bu komutta kullanılan parametreler hakkında daha fazla bilgi için kullanmak `azure storage account create -h` bu komut için Yardım görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="004f2-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="004f2-133">Depolama hesabına erişmek için kullanılan anahtarı alır.</span><span class="sxs-lookup"><span data-stu-id="004f2-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="004f2-134">Değiştir `groupname` kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="004f2-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="004f2-135">Değiştir `storagename` depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="004f2-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="004f2-136">Döndürülen verilerin Kaydet `key` değerini `key1`.</span><span class="sxs-lookup"><span data-stu-id="004f2-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="004f2-137">Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="004f2-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="004f2-138">Değiştir `groupname` kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="004f2-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="004f2-139">Değiştir `Hadoop` oluşturmak istediğiniz küme türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="004f2-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="004f2-140">Örneğin, `Hadoop`, `HBase`, `Kafka`, `Spark`, veya `Storm`.</span><span class="sxs-lookup"><span data-stu-id="004f2-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="004f2-141">Hdınsight kümeleri gelen iş yükü veya küme için ayarlanmış teknoloji karşılık çeşitli türlerde.</span><span class="sxs-lookup"><span data-stu-id="004f2-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="004f2-142">Bir küme üzerinde Storm ve HBase gibi birden çok tür birleştiren bir küme oluşturmak için desteklenen yöntem yoktur.</span><span class="sxs-lookup"><span data-stu-id="004f2-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="004f2-143">Değiştir `location` önceki adımlarda kullanılan aynı konum.</span><span class="sxs-lookup"><span data-stu-id="004f2-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="004f2-144">Değiştir `storagename` depolama hesabı adı ile.</span><span class="sxs-lookup"><span data-stu-id="004f2-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="004f2-145">Değiştir `storagekey` önceki adımda elde anahtara sahip.</span><span class="sxs-lookup"><span data-stu-id="004f2-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="004f2-146">İçin `--defaultStorageContainer` parametresi, kullanım, aynı adı küme için kullanma.</span><span class="sxs-lookup"><span data-stu-id="004f2-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="004f2-147">Değiştir `admin` ve `httppassword` adı ve parolayla istediğiniz küme HTTPS erişirken kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="004f2-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="004f2-148">Değiştir `sshuser` ve `sshuserpassword` kullanıcı adı ve SSH kullanarak kümeye erişirken kullanmak istediğiniz parolayı</span><span class="sxs-lookup"><span data-stu-id="004f2-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="004f2-149">Bu örnek iki alt notes ile bir küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="004f2-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="004f2-150">Çalışan düğüm sayısı ayrıca Küme oluşturulduktan sonra ölçeklendirme işlemleri gerçekleştirerek de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="004f2-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="004f2-151">32'den fazla çalışan düğümleri kullanmayı planlıyorsanız, bir baş düğüm boyutu en az 8 çekirdek ve 14 GB RAM ile seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="004f2-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="004f2-152">Baş düğüm boyutu kullanarak ayarlayabilirsiniz `--headNodeSize` küme oluşturma sırasında parametre.</span><span class="sxs-lookup"><span data-stu-id="004f2-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="004f2-153">Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="004f2-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="004f2-154">Küme oluşturma işleminin tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="004f2-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="004f2-155">Genellikle yaklaşık 15.</span><span class="sxs-lookup"><span data-stu-id="004f2-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="004f2-156">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="004f2-156">Troubleshoot</span></span>

<span data-ttu-id="004f2-157">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="004f2-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="004f2-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="004f2-158">Next steps</span></span>

<span data-ttu-id="004f2-159">Azure CLI kullanarak bir Hdınsight kümesi başarıyla oluşturuldu, kümenizi ile çalışmayı öğrenmek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="004f2-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="004f2-160">Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="004f2-160">Hadoop clusters</span></span>

* [<span data-ttu-id="004f2-161">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="004f2-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="004f2-162">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="004f2-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="004f2-163">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="004f2-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="004f2-164">HBase kümeleri</span><span class="sxs-lookup"><span data-stu-id="004f2-164">HBase clusters</span></span>

* [<span data-ttu-id="004f2-165">Hdınsight'ta HBase kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="004f2-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="004f2-166">Hdınsight'ta HBase için Java uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="004f2-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="004f2-167">Storm kümeleri</span><span class="sxs-lookup"><span data-stu-id="004f2-167">Storm clusters</span></span>

* [<span data-ttu-id="004f2-168">Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="004f2-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="004f2-169">Hdınsight üzerinde Storm Python bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="004f2-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="004f2-170">Dağıtma ve hdınsight'ta Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="004f2-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
