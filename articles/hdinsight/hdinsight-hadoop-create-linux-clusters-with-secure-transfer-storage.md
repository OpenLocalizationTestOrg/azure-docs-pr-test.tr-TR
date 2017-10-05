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
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="d0b32-104">Azure HDInsight’ta güvenli aktarım depolama hesapları ile Hadoop kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0b32-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="d0b32-105">[Güvenli aktarım gereklidir](../storage/common/storage-require-secure-transfer.md) özelliği, güvenli bir bağlantı üzerinden tüm istekleri hesabınıza uygulayarak Azure Depolama hesabınızın güvenliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="d0b32-105">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span></span> <span data-ttu-id="d0b32-106">Bu özellik ve wasbs şeması yalnızca HDInsight kümesi 3.6 veya sonraki sürümlerde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d0b32-106">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d0b32-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d0b32-107">Prerequisites</span></span>
<span data-ttu-id="d0b32-108">Bu öğreticiye başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d0b32-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="d0b32-109">**Azure aboneliği** gereklidir. Bir aylık ücretsiz deneme hesabı oluşturmak için [azure.microsoft.com/free](https://azure.microsoft.com/free) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="d0b32-109">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="d0b32-110">**Güvenli aktarım özellikli bir Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="d0b32-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="d0b32-111">Yönergeler için bkz. [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) ve [Güvenli aktarım isteme](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-111">For the instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="d0b32-112">**Depolama hesabındaki bir Blob kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="d0b32-112">**A Blob container on the storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="d0b32-113">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0b32-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="d0b32-114">Bu bölümde, [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) kullanarak HDInsight'ta Hadoop kümesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d0b32-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="d0b32-115">Şablon [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/)’da vardır.</span><span class="sxs-lookup"><span data-stu-id="d0b32-115">The template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="d0b32-116">Bu öğreticiyi kullanmak için Resource Manager şablonuyla deneyim sahibi olmak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d0b32-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="d0b32-117">Diğer küme oluşturma yöntemleri ve bu öğreticide kullanılan özellikler hakkında bilgi edinmek için bkz. [HDInsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-117">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="d0b32-118">Aşağıdaki resme tıklayarak Azure'da oturum açın ve Azure portalında Resource Manager şablonunu açın.</span><span class="sxs-lookup"><span data-stu-id="d0b32-118">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="d0b32-119">Aşağıdaki özelliklerle kümeyi oluşturmak için yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="d0b32-119">Follow the instructions to create the cluster with the following specifications:</span></span> 

    - <span data-ttu-id="d0b32-120">HDInsight sürümü 3.6’yı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0b32-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="d0b32-121">Varsayılan sürüm 3.5'tir.</span><span class="sxs-lookup"><span data-stu-id="d0b32-121">The default version is 3.5.</span></span> <span data-ttu-id="d0b32-122">3.6 veya daha yeni bir sürüm gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d0b32-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="d0b32-123">Güvenli aktarım özellikli bir depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0b32-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="d0b32-124">Depolama hesabı için kısa bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0b32-124">Use short name for the storage account.</span></span>
    - <span data-ttu-id="d0b32-125">Hem depolama hesabı hem de blob kapsayıcı önceden oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0b32-125">Both the storage account and the blob container must be created beforehand.</span></span> 

    <span data-ttu-id="d0b32-126">Yönergeler için bkz. [Küme oluşturma](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="d0b32-126">For the instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="d0b32-127">Kendi yapılandırma dosyalarınızı sağlamak için betik eylemi kullanıyorsanız, aşağıdaki ayarlarda wasbs kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0b32-127">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span></span>

- <span data-ttu-id="d0b32-128">fs.defaultFS (çekirdek-site)</span><span class="sxs-lookup"><span data-stu-id="d0b32-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="d0b32-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="d0b32-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="d0b32-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="d0b32-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="d0b32-131">Başka depolama hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="d0b32-131">Add additional storage accounts</span></span>

<span data-ttu-id="d0b32-132">Güvenli aktarım özellikli başka depolama hesapları eklemek için birkaç seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="d0b32-132">There are several options to add additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="d0b32-133">Son bölümdeki Azure Resource Manager şablonunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d0b32-133">Modify the Azure Resource Manager template in the last section.</span></span>
- <span data-ttu-id="d0b32-134">[Azure portalını](https://portal.azure.com) kullanarak bir küme oluşturun ve bağlı depolama hesabını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0b32-134">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="d0b32-135">Var olan bir HDInsight kümesine güvenli aktarım özellikli başka depolama hesapları eklemek için betik eylemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0b32-135">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span></span>  <span data-ttu-id="d0b32-136">Daha fazla bilgi için bkz. [HDInsight’a başka depolama hesapları ekleme](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-136">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0b32-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0b32-137">Next steps</span></span>
<span data-ttu-id="d0b32-138">Bu öğreticide bir HDInsight kümesi oluşturmayı ve depolama hesaplarına güvenli aktarımı etkinleştirmeyi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="d0b32-138">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span></span>

<span data-ttu-id="d0b32-139">HDInsight ile veri çözümleme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="d0b32-139">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="d0b32-140">Visual Studio'da Hive sorguları gerçekleştirme dahil, HDInsight ile Hive kullanma hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="d0b32-140">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="d0b32-141">Verileri dönüştürmek için kullanılan bir dil olan Pig hakkında bilgi için bkz. [HDInsight ile Pig kullanma][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="d0b32-141">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="d0b32-142">Hadoop’ta verileri işleyen programları yazmanın bir yöntemi olan MapReduce hakkında bilgi edinmek için bkz. [HDInsight ile MapReduce kullanma][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="d0b32-142">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="d0b32-143">HDInsight’taki verileri çözümlemek amacıyla Visual Studio için HDInsight Araçları kullanma hakkında bilgi edinmek için bkz. [HDInsight için Visual Studio Hadoop araçlarını kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-143">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="d0b32-144">HDInsight’ın verileri nasıl depoladığı veya HDInsight’a verilerin nasıl alındığı hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="d0b32-144">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="d0b32-145">HDInsight’ın Azure Depolama’yı nasıl kullandığı hakkında daha fazla bilgi için bkz. [HDInsight ile Azure Depolama kullanma](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="d0b32-146">HDInsight’a veril yükleme hakkında daha fazla bilgi için bkz. [Verileri HDInsight’a yükleme][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="d0b32-146">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="d0b32-147">HDInsight kümesi oluşturma ve yönetme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="d0b32-147">To learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="d0b32-148">Linux tabanlı HDInsight kümenizi yönetme hakkında bilgi edinmek için bkz. [Ambari kullanarak HDInsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-148">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="d0b32-149">HDInsight kümesi oluştururken tercih edebileceğiniz seçenekler hakkında daha fazla bilgi için bkz. [Özel seçenekleri kullanarak Linux’ta HDInsight oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-149">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="d0b32-150">Linux ve Hadoop hakkında bilgi sahibiyseniz, ancak HDInsight’ta Hadoop’a ilişkin teknik özellikleri öğrenmek istiyorsanız, bkz: [Linux’ta HDInsight ile çalışma](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="d0b32-150">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="d0b32-151">Bu makale aşağıdaki gibi bilgiler sağlar:</span><span class="sxs-lookup"><span data-stu-id="d0b32-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="d0b32-152">Ambari ve WebHCat gibi küme üzerinde barındırılan hizmetlerin URL'leri</span><span class="sxs-lookup"><span data-stu-id="d0b32-152">URLs for services hosted on the cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="d0b32-153">Yerel dosya sisteminde Hadoop dosyalarının ve örneklerin konumu</span><span class="sxs-lookup"><span data-stu-id="d0b32-153">The location of Hadoop files and examples on the local file system</span></span>
  * <span data-ttu-id="d0b32-154">Varsayılan veri depolama olarak HDFS yerine Azure Storage (WASB) kullanımı</span><span class="sxs-lookup"><span data-stu-id="d0b32-154">The use of Azure Storage (WASB) instead of HDFS as the default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


