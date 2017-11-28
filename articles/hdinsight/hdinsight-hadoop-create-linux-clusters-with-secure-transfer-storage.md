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
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="b36fd-104">Azure HDInsight’ta güvenli aktarım depolama hesapları ile Hadoop kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b36fd-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="b36fd-105">Merhaba [güvenli aktarımı gerekli](../storage/common/storage-require-secure-transfer.md) özelliğini, tüm istekleri tooyour hesabı güvenli bir bağlantı üzerinden zorlayarak hello Azure depolama hesabınızın güvenliğini geliştirir.</span><span class="sxs-lookup"><span data-stu-id="b36fd-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="b36fd-106">Bu özellik ve hello wasbs şeması yalnızca 3,6 ya da daha yeni Hdınsight küme sürümü tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b36fd-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b36fd-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b36fd-107">Prerequisites</span></span>
<span data-ttu-id="b36fd-108">Bu öğreticiye başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b36fd-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="b36fd-109">**Azure aboneliği**: toocreate ücretsiz bir aylık deneme hesabı, Gözat çok[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b36fd-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="b36fd-110">**Güvenli aktarım özellikli bir Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="b36fd-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="b36fd-111">Merhaba yönergeler için bkz: [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) ve [güvenli aktarımı gerektiren](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="b36fd-112">**Merhaba depolama hesabındaki bir Blob kapsayıcısını**.</span><span class="sxs-lookup"><span data-stu-id="b36fd-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="b36fd-113">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="b36fd-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="b36fd-114">Bu bölümde, [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md) kullanarak HDInsight'ta Hadoop kümesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b36fd-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="b36fd-115">Merhaba şablon bulunduğu [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="b36fd-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="b36fd-116">Bu öğreticiyi kullanmak için Resource Manager şablonuyla deneyim sahibi olmak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b36fd-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="b36fd-117">Diğer küme oluşturma yöntemleri ve Bu öğreticide kullanılan hello özellikler hakkında bilgi edinmek bkz [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="b36fd-118">Görüntü toosign tooAzure olarak ve açık hello Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b36fd-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="b36fd-119">Merhaba yönergeleri toocreate hello küme belirtimleri aşağıdaki hello ile izleyin:</span><span class="sxs-lookup"><span data-stu-id="b36fd-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="b36fd-120">HDInsight sürümü 3.6’yı belirtin.</span><span class="sxs-lookup"><span data-stu-id="b36fd-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="b36fd-121">3.5 Hello varsayılan sürümdür.</span><span class="sxs-lookup"><span data-stu-id="b36fd-121">hello default version is 3.5.</span></span> <span data-ttu-id="b36fd-122">3.6 veya daha yeni bir sürüm gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b36fd-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="b36fd-123">Güvenli aktarım özellikli bir depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="b36fd-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="b36fd-124">Merhaba depolama hesabı için kısa bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="b36fd-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="b36fd-125">Merhaba depolama hesabı ve hello blob kapsayıcısı önceden oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b36fd-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="b36fd-126">Merhaba yönergeler için bkz: [küme oluştur](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="b36fd-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="b36fd-127">Betik eylemi tooprovide kendi yapılandırma dosyaları kullanırsanız, ayarlar aşağıdaki hello wasbs kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b36fd-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="b36fd-128">fs.defaultFS (çekirdek-site)</span><span class="sxs-lookup"><span data-stu-id="b36fd-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="b36fd-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="b36fd-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="b36fd-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="b36fd-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="b36fd-131">Başka depolama hesapları ekleme</span><span class="sxs-lookup"><span data-stu-id="b36fd-131">Add additional storage accounts</span></span>

<span data-ttu-id="b36fd-132">Çeşitli seçenekler tooadd etkin ek güvenli aktarımı depolama hesapları vardır:</span><span class="sxs-lookup"><span data-stu-id="b36fd-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="b36fd-133">Hello Azure Resource Manager şablonu hello son bölümünde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b36fd-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="b36fd-134">Hello kullanarak bir küme oluşturmak [Azure portal](https://portal.azure.com) ve bağlantılı depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="b36fd-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="b36fd-135">Betik eylemi tooadd ek güvenli aktarımı kullanın depolama hesapları tooan varolan Hdınsight kümesi etkin.</span><span class="sxs-lookup"><span data-stu-id="b36fd-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="b36fd-136">Daha fazla bilgi için bkz: [ek depolama hesapları tooHDInsight eklemek](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b36fd-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b36fd-137">Next steps</span></span>
<span data-ttu-id="b36fd-138">Bu öğreticide, nasıl toohello depolama hesapları toocreate Hdınsight kümesi ve etkinleştir güvenli aktarımı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="b36fd-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="b36fd-139">Hdınsight ile verileri çözümleme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b36fd-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="b36fd-140">Visual Studio'dan nasıl tooperform Hive sorguları dahil, Hdınsight ile Hive kullanma hakkında daha fazla toolearn bkz [Hdınsight ile Hive kullanma][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="b36fd-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="b36fd-141">toolearn Pig hakkında bir dilde kullanılan tootransform veri bkz [Hdınsight ile Pig kullanma][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="b36fd-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="b36fd-142">toolearn MapReduce, hadoop'ta verileri işleyen bir şekilde toowrite programlar hakkında bkz [Hdınsight ile MapReduce kullanma][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="b36fd-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="b36fd-143">Hdınsight, Visual Studio tooanalyze verileri hello Hdınsight araçları kullanma hakkında toolearn bkz [Hdınsight için Visual Studio Hadoop araçlarını kullanmaya başlamanıza](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="b36fd-144">Hdınsight veri saklama biçimi hakkında daha fazla toolearn veya nasıl Hdınsight, tooget verisine makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b36fd-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="b36fd-145">HDInsight’ın Azure Depolama’yı nasıl kullandığı hakkında daha fazla bilgi için bkz. [HDInsight ile Azure Depolama kullanma](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="b36fd-146">Hakkında bilgi için tooupload veri tooHDInsight bkz [karşıya veri tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="b36fd-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="b36fd-147">oluşturma veya bir Hdınsight kümesi yönetme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="b36fd-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="b36fd-148">Linux tabanlı Hdınsight kümenizi yönetme hakkında toolearn bkz [Ambari kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="b36fd-149">toolearn daha seçebileceğiniz bir Hdınsight kümesi oluştururken hello seçenekleri hakkında bkz [özel seçenekleri kullanarak Linux'ta Hdınsight oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="b36fd-150">Linux ve Hadoop hakkında bilginiz ancak tooknow hadoop'a ilişkin teknik özellikleri hello Hdınsight üzerinde istiyorsanız bkz [Linux'ta Hdınsight ile çalışma](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="b36fd-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="b36fd-151">Bu makale aşağıdaki gibi bilgiler sağlar:</span><span class="sxs-lookup"><span data-stu-id="b36fd-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="b36fd-152">Ambari ve WebHCat gibi hello kümesi üzerinde barındırılan hizmetlerin URL'leri</span><span class="sxs-lookup"><span data-stu-id="b36fd-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="b36fd-153">Hadoop dosyalarının ve örneklerin hello yerel dosya sisteminde Hello konumu</span><span class="sxs-lookup"><span data-stu-id="b36fd-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="b36fd-154">Merhaba varsayılan veri deposu olarak, Azure Storage (WASB) HDFS yerine Hello kullan</span><span class="sxs-lookup"><span data-stu-id="b36fd-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


