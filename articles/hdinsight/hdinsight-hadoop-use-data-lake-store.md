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
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="c2fc4-104">Data Lake Store’u Azure HDInsight kümeleriyle kullanma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="c2fc4-105">Hdınsight kümesi tooanalyze verilerin depolayabileceğiniz hello veri ya da içinde [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), veya her ikisini de.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="c2fc4-106">Her iki depolama seçeneklerini kullanıcı verilerini kaybetmeden hesaplama için kullanılan Hdınsight kümeleri toosafely delete etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="c2fc4-107">Bu makalede Data Lake Store’un HDInsight kümeleri ile nasıl çalıştığı hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="c2fc4-108">Azure Storage Hdınsight kümeleri ile nasıl çalışır toolearn bkz [kullanım Azure Storage ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c2fc4-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="c2fc4-109">HDInsight kümesi oluşturma hakkında daha fazla bilgi için bkz. [HDInsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c2fc4-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c2fc4-110">Data Lake Store’a her zaman güvenli bir kanal üzerinden erişildiğinden, `adls` dosya sistemi düzen adı yoktur.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="c2fc4-111">Her zaman `adl` kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="c2fc4-112">HDInsight kümeleri için kullanılabilirlik durumları</span><span class="sxs-lookup"><span data-stu-id="c2fc4-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="c2fc4-113">Hadoop hello varsayılan dosya sistemi kavramını destekler.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="c2fc4-114">Merhaba varsayılan dosya sistemi varsayılan şema ve yetkilisi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="c2fc4-115">Kullanılan tooresolve göreli yollar da olabilir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="c2fc4-116">Merhaba Hdınsight küme oluşturma işlemi sırasında hello varsayılan dosya sistemi olarak Azure storage'da bir blob kapsayıcısını belirtebilirsiniz ya da Hdınsight 3.5 ve yeni sürümler ile Azure Storage veya Azure Data Lake Store ile Merhaba varsayılan dosya sistemi olarak seçebileceğiniz bir birkaç özel durum.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="c2fc4-117">HDInsight kümeleri Data Lake Store’u iki şekilde kullanabilir:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="c2fc4-118">Merhaba varsayılan depolama alanı olarak</span><span class="sxs-lookup"><span data-stu-id="c2fc4-118">As hello default storage</span></span>
* <span data-ttu-id="c2fc4-119">Azure Depolama Blobunun varsayılan depolama alanı olduğu durumlarda ek depolama alanı olarak.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="c2fc4-120">Şimdi itibariyle hello Hdınsight yalnızca bazıları varsayılan depolama ve ek depolama hesapları Data Lake Store kullanan türleri/sürümleri desteği küme:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="c2fc4-121">HDInsight küme türü</span><span class="sxs-lookup"><span data-stu-id="c2fc4-121">HDInsight cluster type</span></span> | <span data-ttu-id="c2fc4-122">Varsayılan depolama alanı olarak Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c2fc4-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="c2fc4-123">Ek depolama alanı olarak Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c2fc4-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="c2fc4-124">Notlar</span><span class="sxs-lookup"><span data-stu-id="c2fc4-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="c2fc4-125">HDInsight sürümü 3.6</span><span class="sxs-lookup"><span data-stu-id="c2fc4-125">HDInsight version 3.6</span></span> | <span data-ttu-id="c2fc4-126">Evet</span><span class="sxs-lookup"><span data-stu-id="c2fc4-126">Yes</span></span> | <span data-ttu-id="c2fc4-127">Evet</span><span class="sxs-lookup"><span data-stu-id="c2fc4-127">Yes</span></span> | |
| <span data-ttu-id="c2fc4-128">HDInsight sürümü 3.5</span><span class="sxs-lookup"><span data-stu-id="c2fc4-128">HDInsight version 3.5</span></span> | <span data-ttu-id="c2fc4-129">Evet</span><span class="sxs-lookup"><span data-stu-id="c2fc4-129">Yes</span></span> | <span data-ttu-id="c2fc4-130">Evet</span><span class="sxs-lookup"><span data-stu-id="c2fc4-130">Yes</span></span> | <span data-ttu-id="c2fc4-131">HBase Hello özel durumuyla</span><span class="sxs-lookup"><span data-stu-id="c2fc4-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="c2fc4-132">HDInsight sürümü 3.4</span><span class="sxs-lookup"><span data-stu-id="c2fc4-132">HDInsight version 3.4</span></span> | <span data-ttu-id="c2fc4-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2fc4-133">No</span></span> | <span data-ttu-id="c2fc4-134">Evet</span><span class="sxs-lookup"><span data-stu-id="c2fc4-134">Yes</span></span> | |
| <span data-ttu-id="c2fc4-135">HDInsight sürümü 3.3</span><span class="sxs-lookup"><span data-stu-id="c2fc4-135">HDInsight version 3.3</span></span> | <span data-ttu-id="c2fc4-136">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2fc4-136">No</span></span> | <span data-ttu-id="c2fc4-137">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2fc4-137">No</span></span> | |
| <span data-ttu-id="c2fc4-138">HDInsight sürümü 3.2</span><span class="sxs-lookup"><span data-stu-id="c2fc4-138">HDInsight version 3.2</span></span> | <span data-ttu-id="c2fc4-139">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2fc4-139">No</span></span> | <span data-ttu-id="c2fc4-140">Evet</span><span class="sxs-lookup"><span data-stu-id="c2fc4-140">Yes</span></span> | |
| <span data-ttu-id="c2fc4-141">HDInsight Premium (katman)</span><span class="sxs-lookup"><span data-stu-id="c2fc4-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="c2fc4-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2fc4-142">No</span></span> | <span data-ttu-id="c2fc4-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="c2fc4-143">No</span></span> | |
| <span data-ttu-id="c2fc4-144">Storm</span><span class="sxs-lookup"><span data-stu-id="c2fc4-144">Storm</span></span> | | |<span data-ttu-id="c2fc4-145">Data Lake Store toowrite veri bir Storm topolojisinin kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="c2fc4-146">Data Lake Store’u daha sonra bir Storm topolojisinden okunabilecek başvuru verileri için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="c2fc4-147">Data Lake Store ek depolama alanı hesabı olarak kullanarak performans veya hello özelliği tooread etkilemez veya hello kümeden tooAzure depolama yazma.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="c2fc4-148">Azure Data Lake Store’u varsayılan depolama alanı olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="c2fc4-149">Hdınsight, Data Lake Store varsayılan depolama ile dağıtıldığında, hello küme ilgili dosyaları konumu aşağıdaki hello Data Lake Store içinde depolanır:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="c2fc4-150">Burada `<cluster_root_path>` Data Lake Store içinde oluşturduğunuz bir klasöre hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="c2fc4-151">Her küme için kök yolu belirterek kullanabilirsiniz hello birden fazla küme için aynı Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="c2fc4-152">Bunu yaptığınızda şöyle bir durum olabilir:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="c2fc4-153">Cluster1 hello yolu kullanabilirsiniz`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="c2fc4-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="c2fc4-154">Cluster2 hello yolu kullanabilirsiniz`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="c2fc4-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="c2fc4-155">Her ikisi de kümeleri kullanım hello bildirimi hello aynı Data Lake Store hesabı **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="c2fc4-156">Her küme Data Lake Store'da kök dosya sistemine sahip erişim tooits sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="c2fc4-157">Hello Azure portalı dağıtımının deneyimi özellikle sizden toouse bir klasör adı gibi **/clusters/\<clustername >** hello kök yolu.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="c2fc4-158">toobe mümkün toouse varsayılan depolama olarak Data Lake Store, yolları aşağıdaki hello hizmet asıl erişim toohello vermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="c2fc4-159">Merhaba Data Lake Store hesabı kökü.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="c2fc4-160">Örneğin: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="c2fc4-161">tüm küme klasörleri için başlangıç klasörü.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="c2fc4-162">Örneğin: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="c2fc4-163">Merhaba küme için başlangıç klasörü.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="c2fc4-164">Örneğin: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="c2fc4-165">Hizmet sorumlusu oluşturma ve erişim verme hakkında daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="c2fc4-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="c2fc4-166">Azure Data Lake Store’u ek depolama alanı olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="c2fc4-167">Data Lake Store de hello küme için ek depolama alanı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="c2fc4-168">Böyle durumlarda, hello kümenin varsayılan depolama ya da bir Azure depolama Blob veya bir Data Lake Store hesabı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="c2fc4-169">Ek depolama alanı olarak Data Lake Store'da depolanan hello verileri karşı Hdınsight iş devam ediyorsa, hello tam yolu toohello dosyalarını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="c2fc4-170">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="c2fc4-171">Unutmayın hiçbir **cluster_root_path** şimdi hello URL'de.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="c2fc4-172">Tüm toodo gereken hello yolu toohello dosyalarını sağlamak Data Lake Store varsayılan depolama bu durumda olmadığından olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="c2fc4-173">toobe mümkün toouse ek depolama alanı olarak Data Lake Store, yalnızca toogrant hello hizmet asıl erişim toohello yolları dosyalarınızı nerede depolanacağını gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="c2fc4-174">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="c2fc4-175">Hizmet sorumlusu oluşturma ve erişim verme hakkında daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="c2fc4-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="c2fc4-176">Birden çok Data Lake Store hesabı kullanma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="c2fc4-177">Bir Data Lake Store hesabına ek olarak ekleme ve birden fazla Data Lake Store ekleyerek bir veya daha fazla Data Lake Store hesapları veriler üzerinde hello Hdınsight küme izin vererek hesapları gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="c2fc4-178">Bkz. [Data Lake Store erişimini yapılandırma](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="c2fc4-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="c2fc4-179">Data Lake Store erişimini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-179">Configure Data Lake store access</span></span>

<span data-ttu-id="c2fc4-180">Data Lake deposu erişimini Hdınsight kümenize tooconfigure, bir Azure Active directory (Azure AD) hizmet asıl olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="c2fc4-181">Hizmet sorumlusu yalnızca bir Azure AD yöneticisi tarafından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="c2fc4-182">Merhaba hizmet sorumlusu sahip bir sertifika oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="c2fc4-183">Daha fazla bilgi edinmek için bkz. [Data Lake Store erişimini yapılandırma](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) ve [Otomatik olarak imzalanan sertifika ile hizmet sorumlusu oluşturma](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="c2fc4-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="c2fc4-184">Hdınsight kümesi için ek depolama alanı olarak toouse Azure Data Lake Store kullanacaksanız, bu makalede anlatıldığı gibi hello küme oluştururken bunu yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="c2fc4-185">Ek depolama alanı tooan Azure Data Lake Store ekleme olan bir Hdınsight kümesine bir karmaşık bir işlem yatkın tooerrors ise.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="c2fc4-186">Merhaba kümeden Access dosyalarını</span><span class="sxs-lookup"><span data-stu-id="c2fc4-186">Access files from hello cluster</span></span>

<span data-ttu-id="c2fc4-187">Bir Hdınsight kümeden Data Lake Store hello dosyalarına erişebilirsiniz birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="c2fc4-188">**Merhaba tam adını kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="c2fc4-189">Bu yaklaşımda, sağladığınız hello tam yol toohello dosya tooaccess istiyor.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="c2fc4-190">**Merhaba kısaltılmış yol biçimi kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="c2fc4-191">Bu yaklaşımda, adl ile toohello küme kök hello yolu değiştirin: / / /.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="c2fc4-192">Bu nedenle, hello yukarıdaki örnekte, değiştirebilirsiniz `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` ile `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="c2fc4-193">**Merhaba göreli yolu kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-193">**Using hello relative path**.</span></span> <span data-ttu-id="c2fc4-194">Bu yaklaşımda, yalnızca hello göreli yol toohello dosya sağladığınız tooaccess istiyor.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="c2fc4-195">Örneğin, Hello tam yolunu toohello dosyası ise:</span><span class="sxs-lookup"><span data-stu-id="c2fc4-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="c2fc4-196">Erişebilmeniz için bu göreli yolu kullanarak aynı sample.log dosya hello.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="c2fc4-197">Hdınsight kümeleri oluşturma ile tooData Lake deposuna erişim</span><span class="sxs-lookup"><span data-stu-id="c2fc4-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="c2fc4-198">Ayrıntılı yönergeleri için bağlantıları nasıl ile Hdınsight kümeleri toocreate erişim tooData Lake Store aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="c2fc4-199">Portalı kullanma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="c2fc4-200">PowerShell kullanma (varsayılan depolama alanı olarak Data Lake Store ile)</span><span class="sxs-lookup"><span data-stu-id="c2fc4-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="c2fc4-201">PowerShell kullanma (ek depolama alanı olarak Data Lake Store ile)</span><span class="sxs-lookup"><span data-stu-id="c2fc4-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="c2fc4-202">Azure şablonlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="c2fc4-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="c2fc4-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2fc4-203">Next steps</span></span>
<span data-ttu-id="c2fc4-204">Bu makalede, nasıl öğrenilen toouse Hdınsight ile HDFS uyumlu Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="c2fc4-205">Bu, toobuild ölçeklenebilir, uzun vadeli, arşivleme verileri edinme çözümleri ve kullanım depolanan hello içindeki Hdınsight toounlock hello bilgileri yapılandırılmış ve yapılandırılmamış verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="c2fc4-206">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="c2fc4-206">For more information, see:</span></span>

* <span data-ttu-id="c2fc4-207">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c2fc4-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="c2fc4-208">Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c2fc4-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="c2fc4-209">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c2fc4-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c2fc4-210">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c2fc4-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c2fc4-211">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c2fc4-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c2fc4-212">[Hdınsight ile Azure Storage paylaşılan erişim imzaları toorestrict erişim toodata kullanma][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="c2fc4-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
