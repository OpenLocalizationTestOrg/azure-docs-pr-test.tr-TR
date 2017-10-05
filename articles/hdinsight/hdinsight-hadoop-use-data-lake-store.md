---
title: "Azure HDInsight'ta Data Lake Store’u Hadoop ile Kullanma | Microsoft Docs"
description: "Azure Data Lake Store’daki verileri sorgulama ve analiz sonuçlarınızı depolama işlemlerinin nasıl gerçekleştirildiğini öğrenin."
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
ms.openlocfilehash: 28a836aff65636ef0031ac63f633d746436d7e4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="d5268-104">Data Lake Store’u Azure HDInsight kümeleriyle kullanma</span><span class="sxs-lookup"><span data-stu-id="d5268-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="d5268-105">HDInsight kümesinde çözümlemek istediğiniz verileri [Azure Depolama](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) veya her ikisinde birden depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-105">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="d5268-106">İki depolama seçeneği de işlem için kullanılan HDInsight kümelerini kullanıcı verilerini kaybetmeden güvenle silmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5268-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="d5268-107">Bu makalede Data Lake Store’un HDInsight kümeleri ile nasıl çalıştığı hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="d5268-108">Azure Depolama’nın HDInsight kümeleriyle nasıl çalıştığı hakkında bilgi edinmek için bkz. [Azure Depolama’yı Azure HDInsight kümeleri ile kullanma](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d5268-108">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="d5268-109">HDInsight kümesi oluşturma hakkında daha fazla bilgi edinmek için bkz. [HDInsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d5268-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d5268-110">Data Lake Store’a her zaman güvenli bir kanal üzerinden erişildiğinden, `adls` dosya sistemi düzen adı yoktur.</span><span class="sxs-lookup"><span data-stu-id="d5268-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="d5268-111">Her zaman `adl` kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="d5268-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="d5268-112">HDInsight kümeleri için kullanılabilirlik durumları</span><span class="sxs-lookup"><span data-stu-id="d5268-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="d5268-113">Hadoop varsayılan dosya sistemi kavramını destekler.</span><span class="sxs-lookup"><span data-stu-id="d5268-113">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="d5268-114">Varsayılan dosya sistemi varsayılan şema ve yetkilisi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d5268-114">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="d5268-115">Bu göreceli yolları çözümlemek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-115">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="d5268-116">HDInsight kümesi oluşturma işlemi sırasında Azure Depolama'da bir blob kapsayıcısını varsayılan dosya sistemi olarak belirtebilir veya HDInsight 3.5 veya daha yeni sürümlerde, birkaç özel durum dışında Azure Depolama'yı ya da Azure Data Lake Store'u varsayılan dosya sistemi olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-116">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> 

<span data-ttu-id="d5268-117">HDInsight kümeleri Data Lake Store’u iki şekilde kullanabilir:</span><span class="sxs-lookup"><span data-stu-id="d5268-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="d5268-118">Varsayılan depolama alanı olarak</span><span class="sxs-lookup"><span data-stu-id="d5268-118">As the default storage</span></span>
* <span data-ttu-id="d5268-119">Azure Depolama Blobunun varsayılan depolama alanı olduğu durumlarda ek depolama alanı olarak.</span><span class="sxs-lookup"><span data-stu-id="d5268-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="d5268-120">Şu anda, Data Lake Store’un varsayılan depolama alanı ve ek depolama hesapları olarak kullanılmasını yalnızca bazı HDInsight küme türleri/sürümleri destekler:</span><span class="sxs-lookup"><span data-stu-id="d5268-120">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="d5268-121">HDInsight küme türü</span><span class="sxs-lookup"><span data-stu-id="d5268-121">HDInsight cluster type</span></span> | <span data-ttu-id="d5268-122">Varsayılan depolama alanı olarak Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d5268-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="d5268-123">Ek depolama alanı olarak Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d5268-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="d5268-124">Notlar</span><span class="sxs-lookup"><span data-stu-id="d5268-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="d5268-125">HDInsight sürümü 3.6</span><span class="sxs-lookup"><span data-stu-id="d5268-125">HDInsight version 3.6</span></span> | <span data-ttu-id="d5268-126">Evet</span><span class="sxs-lookup"><span data-stu-id="d5268-126">Yes</span></span> | <span data-ttu-id="d5268-127">Evet</span><span class="sxs-lookup"><span data-stu-id="d5268-127">Yes</span></span> | |
| <span data-ttu-id="d5268-128">HDInsight sürümü 3.5</span><span class="sxs-lookup"><span data-stu-id="d5268-128">HDInsight version 3.5</span></span> | <span data-ttu-id="d5268-129">Evet</span><span class="sxs-lookup"><span data-stu-id="d5268-129">Yes</span></span> | <span data-ttu-id="d5268-130">Evet</span><span class="sxs-lookup"><span data-stu-id="d5268-130">Yes</span></span> | <span data-ttu-id="d5268-131">HBase dışında</span><span class="sxs-lookup"><span data-stu-id="d5268-131">With the exception of HBase</span></span>|
| <span data-ttu-id="d5268-132">HDInsight sürümü 3.4</span><span class="sxs-lookup"><span data-stu-id="d5268-132">HDInsight version 3.4</span></span> | <span data-ttu-id="d5268-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="d5268-133">No</span></span> | <span data-ttu-id="d5268-134">Evet</span><span class="sxs-lookup"><span data-stu-id="d5268-134">Yes</span></span> | |
| <span data-ttu-id="d5268-135">HDInsight sürümü 3.3</span><span class="sxs-lookup"><span data-stu-id="d5268-135">HDInsight version 3.3</span></span> | <span data-ttu-id="d5268-136">Hayır</span><span class="sxs-lookup"><span data-stu-id="d5268-136">No</span></span> | <span data-ttu-id="d5268-137">Hayır</span><span class="sxs-lookup"><span data-stu-id="d5268-137">No</span></span> | |
| <span data-ttu-id="d5268-138">HDInsight sürümü 3.2</span><span class="sxs-lookup"><span data-stu-id="d5268-138">HDInsight version 3.2</span></span> | <span data-ttu-id="d5268-139">Hayır</span><span class="sxs-lookup"><span data-stu-id="d5268-139">No</span></span> | <span data-ttu-id="d5268-140">Evet</span><span class="sxs-lookup"><span data-stu-id="d5268-140">Yes</span></span> | |
| <span data-ttu-id="d5268-141">HDInsight Premium (katman)</span><span class="sxs-lookup"><span data-stu-id="d5268-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="d5268-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="d5268-142">No</span></span> | <span data-ttu-id="d5268-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="d5268-143">No</span></span> | |
| <span data-ttu-id="d5268-144">Storm</span><span class="sxs-lookup"><span data-stu-id="d5268-144">Storm</span></span> | | |<span data-ttu-id="d5268-145">Data Lake Store’u kullanarak bir Storm topolojisinden veri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-145">You can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="d5268-146">Data Lake Store’u daha sonra bir Storm topolojisinden okunabilecek başvuru verileri için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="d5268-147">Data Lake Store’un ek depolama hesabı olarak kullanılması, kümeden Azure depolamaya yazma veya buradan okuma performansını ya da bu özelliğin kullanılabilirliğini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="d5268-147">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="d5268-148">Azure Data Lake Store’u varsayılan depolama alanı olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="d5268-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="d5268-149">HDInsight ile varsayılan depolama alanı olarak Data Lake Store dağıtıldığında, kümeyle ilişkili dosyalar Data Lake Store içindeki şu konumda depolanır:</span><span class="sxs-lookup"><span data-stu-id="d5268-149">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="d5268-150">Buradaki `<cluster_root_path>`, Azure Data Lake Store’da oluşturduğunuz klasörün adıdır.</span><span class="sxs-lookup"><span data-stu-id="d5268-150">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="d5268-151">Her küme için bir kök yolu belirterek, birden fazla küme için aynı Data Lake Store hesabını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-151">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="d5268-152">Bunu yaptığınızda şöyle bir durum olabilir:</span><span class="sxs-lookup"><span data-stu-id="d5268-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="d5268-153">Cluster1 `adl://mydatalakestore/cluster1storage` yolunu kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-153">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="d5268-154">Cluster2 `adl://mydatalakestore/cluster2storage` yolunu kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-154">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="d5268-155">Her iki kümenin aynı **mydatalakestore** Data Lake Store hesabını kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d5268-155">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="d5268-156">Her küme Data Lake Store içinde kendi kök dosya sistemine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-156">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="d5268-157">Özellikle Azure portalı dağıtımı deneyimi sizden kök yol olarak **/clusters/\<clustername>** gibi bir klasör adı kullanmanızı ister.</span><span class="sxs-lookup"><span data-stu-id="d5268-157">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

<span data-ttu-id="d5268-158">Bir Data Lake Store’u varsayılan depolama alanı olarak kullanabilmeniz için aşağıdaki yollara hizmet sorumlusu erişimi vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d5268-158">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span></span>

- <span data-ttu-id="d5268-159">Data Lake Store hesabının kökü.</span><span class="sxs-lookup"><span data-stu-id="d5268-159">The Data Lake Store account root.</span></span>  <span data-ttu-id="d5268-160">Örneğin: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="d5268-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="d5268-161">Tüm küme klasörlerine yönelik klasör.</span><span class="sxs-lookup"><span data-stu-id="d5268-161">The folder for all cluster folders.</span></span>  <span data-ttu-id="d5268-162">Örneğin: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="d5268-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="d5268-163">Kümenin klasörü.</span><span class="sxs-lookup"><span data-stu-id="d5268-163">The folder for the cluster.</span></span>  <span data-ttu-id="d5268-164">Örneğin: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="d5268-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="d5268-165">Hizmet sorumlusu oluşturma ve erişim verme hakkında daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="d5268-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="d5268-166">Azure Data Lake Store’u ek depolama alanı olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="d5268-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="d5268-167">Data Lake Store'u da küme için ek depolama alanı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-167">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="d5268-168">Böyle durumlarda, kümenin varsayılan depolama alanı Azure Depolama Blobu veya Data Lake Store hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-168">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="d5268-169">HDInsight işlerini ek depolama alanı olarak kullanılan Data Lake Store'da depolanan verilere göre çalıştırıyorsanız, dosyaların tam yolunu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5268-169">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="d5268-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d5268-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="d5268-171">Artık URL'de **cluster_root_path** olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d5268-171">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="d5268-172">Bunun nedeni Data Lake Store’un artık varsayılan depolama alanı olmamasıdır. Artık tüm yapmanız gereken dosyaların yolunu belirtmektir.</span><span class="sxs-lookup"><span data-stu-id="d5268-172">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>

<span data-ttu-id="d5268-173">Data Lake Store’u ek depolama alanı olarak kullanabilmeniz için yalnızca dosyalarınızın depolandığı konumlara hizmet sorumlusu erişimi vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5268-173">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span></span>  <span data-ttu-id="d5268-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d5268-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="d5268-175">Hizmet sorumlusu oluşturma ve erişim verme hakkında daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="d5268-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="d5268-176">Birden çok Data Lake Store hesabı kullanma</span><span class="sxs-lookup"><span data-stu-id="d5268-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="d5268-177">Bir Data Lake Store hesabını ek depolama olarak ekleme ve birden fazla Data Lake Store hesabı ekleme işlemi, bir veya daha çok Data Lake Store hesabındaki veriler için HDInsight kümesine izin verilerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="d5268-178">Bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="d5268-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="d5268-179">Data Lake Store erişimini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d5268-179">Configure Data Lake store access</span></span>

<span data-ttu-id="d5268-180">HDInsight kümenizden Data Lake store erişimini yapılandırabilmeniz için bir Azure Active Directory (Azure AD) hizmet sorumlunuz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d5268-180">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="d5268-181">Hizmet sorumlusu yalnızca bir Azure AD yöneticisi tarafından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="d5268-182">Hizmet sorumlusunun bir sertifika ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d5268-182">The service principal must be created with a certificate.</span></span> <span data-ttu-id="d5268-183">Daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) ve [Otomatik olarak imzalanan sertifika ile hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="d5268-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="d5268-184">Azure Data Lake Store’u HDInsight kümesi için ek depolama alanı olarak kullanacaksanız, bunu bu makalede açıklandığı gibi kümeyi oluştururken yapmanız önemle önerilir.</span><span class="sxs-lookup"><span data-stu-id="d5268-184">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="d5268-185">Azure Data Lake Store’u mevcut bir HDInsight kümesine ek depolama alanı olarak ekleme, karmaşık ve hatalara yol açabilecek bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d5268-185">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

## <a name="access-files-from-the-cluster"></a><span data-ttu-id="d5268-186">Kümeden dosyalara erişme</span><span class="sxs-lookup"><span data-stu-id="d5268-186">Access files from the cluster</span></span>

<span data-ttu-id="d5268-187">Data Lake Store dosyalarına bir HDInsight kümesinden erişmenin çeşitli yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="d5268-187">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="d5268-188">**Tam adı kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="d5268-188">**Using the fully qualified name**.</span></span> <span data-ttu-id="d5268-189">Bu yöntemle, erişmek istediğiniz dosyanın tam yolunu girersiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-189">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="d5268-190">**Kısaltılmış yol biçimi kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="d5268-190">**Using the shortened path format**.</span></span> <span data-ttu-id="d5268-191">Bu yöntemle, yolu küme kökü ve adl ile değiştirirsiniz: / / /.</span><span class="sxs-lookup"><span data-stu-id="d5268-191">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="d5268-192">Yukarıdaki örnekte `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` ile `adl:///` değerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-192">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="d5268-193">**Göreli yolu kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="d5268-193">**Using the relative path**.</span></span> <span data-ttu-id="d5268-194">Bu yöntemle, erişmek istediğiniz dosyanın yalnızca göreli yolunu girersiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-194">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="d5268-195">Örneğin dosyanın tam yolu şöyleyse:</span><span class="sxs-lookup"><span data-stu-id="d5268-195">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="d5268-196">Aynı sample.log dosyasına göreli yolu kullanarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-196">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="d5268-197">Data Lake Store erişimi olan HDInsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5268-197">Create HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="d5268-198">Data Lake Store erişimi olan HDInsight kümeleri oluşturma hakkındaki ayrıntılı yönergeler için aşağıdaki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d5268-198">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="d5268-199">Portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="d5268-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="d5268-200">PowerShell kullanma (varsayılan depolama alanı olarak Data Lake Store ile)</span><span class="sxs-lookup"><span data-stu-id="d5268-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="d5268-201">PowerShell kullanma (ek depolama alanı olarak Data Lake Store ile)</span><span class="sxs-lookup"><span data-stu-id="d5268-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="d5268-202">Azure şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="d5268-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="d5268-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5268-203">Next steps</span></span>
<span data-ttu-id="d5268-204">Bu makalede, HDInsight ile HDFS uyumlu Azure Data Lake Store’u kullanmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="d5268-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="d5268-205">Bu, ölçeklenebilir, uzun vadeli, arşivlemeli veri edinme çözümleri oluşturmanıza ve depolanan yapılandırılmış ve yapılandırılmamış verilerdeki bilgilerin kilidini açmak için HDInsight kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5268-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="d5268-206">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="d5268-206">For more information, see:</span></span>

* <span data-ttu-id="d5268-207">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d5268-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="d5268-208">Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d5268-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="d5268-209">[HDInsight'a veri yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d5268-209">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d5268-210">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d5268-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d5268-211">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d5268-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="d5268-212">[HDInsight ile verilere erişimi kısıtlamak için Azure Depolama Paylaşılan Erişim İmzaları kullanma][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="d5268-212">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
