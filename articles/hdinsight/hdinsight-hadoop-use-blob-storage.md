---
title: "aaaQuery verileri HDFS uyumlu Azure depolama - Azure Hdınsight | Microsoft Docs"
description: "Azure depolama ve Azure Data Lake Store toostore tooquery verilerini nasıl sonuçları öğrenin çözümleme."
keywords: "blob depolama,hdfs,yapılandırılmış veriler,yapılandırılmamış veriler,data lake store,Hadoop girdisi,Hadoop çıktısı, hadoop depolama, hdfs girdisi,hdfs çıktısı,hdfs depolama,wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="ddca7-104">Azure HDInsight kümeleri ile Azure Depolama'yı kullanma</span><span class="sxs-lookup"><span data-stu-id="ddca7-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="ddca7-105">Hdınsight kümesi tooanalyze verilerin hello verileri Azure Storage, Azure Data Lake Store veya her ikisi de depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="ddca7-106">Her iki depolama seçeneklerini kullanıcı verilerini kaybetmeden hesaplama için kullanılan Hdınsight kümeleri toosafely delete etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ddca7-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="ddca7-107">Hadoop hello varsayılan dosya sistemi kavramını destekler.</span><span class="sxs-lookup"><span data-stu-id="ddca7-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="ddca7-108">Merhaba varsayılan dosya sistemi varsayılan şema ve yetkilisi anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="ddca7-109">Kullanılan tooresolve göreli yollar da olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="ddca7-110">Merhaba Hdınsight küme oluşturma işlemi sırasında hello varsayılan dosya sistemi olarak Azure storage'da bir blob kapsayıcısını belirtin veya Hdınsight 3.5 ile birlikte, Azure Storage veya Azure Data Lake Store birkaç istisna dışında hello varsayılan dosya sistemi olarak seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="ddca7-111">Merhaba desteklenebilirlik Data Lake Store hello varsayılan ve bağlantılı depolama alanı kullanma Bkz [Hdınsight kümesi için kullanılabilirliklerinin](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="ddca7-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="ddca7-112">Bu makalede Azure Depolama'nın HDInsight kümeleri ile nasıl çalıştığı hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="ddca7-113">Data Lake Store Hdınsight kümeleri ile nasıl çalışır toolearn bkz [kullanım Azure Data Lake Store ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="ddca7-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="ddca7-114">HDInsight kümesi oluşturma hakkında daha fazla bilgi için bkz. [HDInsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="ddca7-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="ddca7-115">Azure depolama, HDInsight ile sorunsuz bir şekilde tümleşen, sağlam ve genel amaçlı bir depolama çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="ddca7-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="ddca7-116">Hdınsight bir blob kapsayıcısını Azure Storage'da hello varsayılan dosya sistemi olarak hello küme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="ddca7-117">Hadoop dağıtılmış dosya sistemi (HDFS) arabirimi aracılığıyla, Hdınsight'taki bileşenler hello kümesini BLOB olarak depolanan doğrudan yapılandırılmış veya yapılandırılmamış veriler üzerinde çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="ddca7-118">Azure Depolama hesabı oluşturmanın birden fazla yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="ddca7-119">Aşağıdaki tablonun hello Hdınsight ile hangi seçenekleri desteklenen bilgileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="ddca7-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="ddca7-120">Depolama hesabı türü</span><span class="sxs-lookup"><span data-stu-id="ddca7-120">Storage account type</span></span> | <span data-ttu-id="ddca7-121">Depolama katmanı</span><span class="sxs-lookup"><span data-stu-id="ddca7-121">Storage tier</span></span> | <span data-ttu-id="ddca7-122">HDInsight ile desteklenen</span><span class="sxs-lookup"><span data-stu-id="ddca7-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="ddca7-123">Genel amaçlı Depolama Hesabı</span><span class="sxs-lookup"><span data-stu-id="ddca7-123">General-purpose Storage Account</span></span> | <span data-ttu-id="ddca7-124">Standart</span><span class="sxs-lookup"><span data-stu-id="ddca7-124">Standard</span></span> | <span data-ttu-id="ddca7-125">__Evet__</span><span class="sxs-lookup"><span data-stu-id="ddca7-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="ddca7-126">Premium</span><span class="sxs-lookup"><span data-stu-id="ddca7-126">Premium</span></span> | <span data-ttu-id="ddca7-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="ddca7-127">No</span></span> |
> | <span data-ttu-id="ddca7-128">Blob Depolama Hesabı</span><span class="sxs-lookup"><span data-stu-id="ddca7-128">Blob Storage Account</span></span> | <span data-ttu-id="ddca7-129">Sık Erişimli</span><span class="sxs-lookup"><span data-stu-id="ddca7-129">Hot</span></span> | <span data-ttu-id="ddca7-130">Hayır</span><span class="sxs-lookup"><span data-stu-id="ddca7-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="ddca7-131">Seyrek Erişimli</span><span class="sxs-lookup"><span data-stu-id="ddca7-131">Cool</span></span> | <span data-ttu-id="ddca7-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="ddca7-132">No</span></span> |

<span data-ttu-id="ddca7-133">Hello varsayılan blob kapsayıcısı iş verilerini depolamak için kullanmanızı önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="ddca7-134">Her kullanım tooreduce sonra Hello varsayılan blob kapsayıcısını silmek depolama maliyeti iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="ddca7-135">Not Bu hello varsayılan kapsayıcı içeren uygulama ve sistem günlükleri.</span><span class="sxs-lookup"><span data-stu-id="ddca7-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="ddca7-136">Emin tooretrieve hello günlükleri hello kapsayıcı silmeden önce yapın.</span><span class="sxs-lookup"><span data-stu-id="ddca7-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="ddca7-137">Bir blob kapsayıcısının birden fazla küme için paylaşımı desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ddca7-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="ddca7-138">HDInsight depolama mimarisi</span><span class="sxs-lookup"><span data-stu-id="ddca7-138">HDInsight storage architecture</span></span>
<span data-ttu-id="ddca7-139">Aşağıdaki diyagramda hello hello Azure Storage kullanarak Hdınsight depolama mimarisine ilişkin özet görünümünü sağlar:</span><span class="sxs-lookup"><span data-stu-id="ddca7-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="ddca7-140">![Hadoop kümeleri Blob storage'da yapılandırılmış ve yapılandırılmamış verileri depolamak ve hello HDFS API'sini tooaccess kullanın. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Hdınsight depolama mimarisi")</span><span class="sxs-lookup"><span data-stu-id="ddca7-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="ddca7-141">Hdınsight, yerel olarak erişim toohello dağıtılmış dosya sistemi toohello işlem düğümlerine ekli sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="ddca7-142">Bu dosya sistemi kullanılarak erişilebilir hello tam URI, örneğin:</span><span class="sxs-lookup"><span data-stu-id="ddca7-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="ddca7-143">Ayrıca, Hdınsight Azure depolama alanında depolanır tooaccess veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="ddca7-144">Merhaba sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ddca7-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="ddca7-145">HDInsight kümeleriyle Azure Depolama hesabını kullanırken dikkat etmeniz gereken bazı noktalar mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="ddca7-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="ddca7-146">**Bağlı tooa küme hello depolama hesaplarındaki kapsayıcılar:** hello hesap adı ve anahtar oluşturma sırasında hello kümeyle ilişkilendirildiğinden, bu kapsayıcılardaki blob'lara tam erişim toohello sahip.</span><span class="sxs-lookup"><span data-stu-id="ddca7-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="ddca7-147">**Genel kapsayıcılar veya genel BLOB'lar olmayan depolama hesaplarındaki bağlı tooa küme:** salt okunur izni toohello bloblar hello kapsayıcılarında sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ddca7-148">Genel kapsayıcılar tooget kapsayıcı meta verilerini almak ve bu kapsayıcıda bulunan tüm BLOB listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="ddca7-149">Yalnızca hello tam URL'yi biliyorsanız genel BLOB'lar tooaccess hello BLOB'lar izin verin.</span><span class="sxs-lookup"><span data-stu-id="ddca7-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="ddca7-150">Daha fazla bilgi için bkz: <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">kısıtlamak erişim toocontainers ve blobları</a>.</span><span class="sxs-lookup"><span data-stu-id="ddca7-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="ddca7-151">**Tooa küme bağlı olmayan depolama hesaplarındaki özel kapsayıcılar:** hello WebHCat işleri gönderdiğinizde hello depolama hesabını tanımlamadığınız sürece Merhaba kapsayıcılara hello blobları erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="ddca7-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="ddca7-152">Bu, bu makalenin sonraki bölümlerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-152">This is explained later in this article.</span></span>

<span data-ttu-id="ddca7-153">Merhaba oluşturma işlemi ve bunların anahtarların tanımlanan hello depolama hesapları %HADOOP_HOME%/conf/core-site.xml hello küme düğümlerinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="ddca7-154">Hdınsight Hello varsayılan davranışı hello core-site.xml dosyasında tanımlanan toouse hello depolama hesapları değildir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="ddca7-155">[Ambari](./hdinsight-hadoop-manage-ambari.md) kullanarak bu ayarı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="ddca7-156">Hive, MapReduce, Hadoop akış ve Pig dahil olmak üzere birden çok WebHCat işleri kendileriyle birlikte depolama hesapları açıklaması ve meta veriler taşıyabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="ddca7-157">(Bu şu anda yalnızca Pig depolama hesapları ile çalışmakta, ancak meta verilerle çalışmamaktadır.) Daha fazla bilgi için bkz. [Alternatif Depolama Hesapları ve Meta Depolarla HDInsight Kümesi kullanma](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddca7-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="ddca7-158">Bloblar yapılandırılmış ve yapılandırılmamış veriler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="ddca7-159">Blob kapsayıcıları, verileri anahtar/değer çiftleri olarak depolar ve dizin hiyerarşisi bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="ddca7-160">Ancak, Hello eğik çizgi karakteri (/) görünür bir dosyayı dizin yapısında depolanmış gibi hello anahtar adı toomake içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="ddca7-161">Örneğin, bir blob'un anahtarı *input/log1.txt* şeklinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="ddca7-162">Gerçek *giriş* dizin var, ancak hello hello anahtar adında eğik çizgi karakteri varlığını toohello, bir dosya yolu hello görünümünü sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="ddca7-163"><a id="benefits"></a>Azure Depolamanın yararları</span><span class="sxs-lookup"><span data-stu-id="ddca7-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="ddca7-164">performans maliyetini birlikte bulunduruyorsanız hesaplama kümeleri ve depolama kaynaklarını hello hesaplama kümeleri Kapat toohello depolama hesabı kaynaklarına hello Azure bölgesi, burada hello yüksek hızlı ağ kolaylaştırır oluşturulan hello yolu tarafından azaltılan Hello kapsanan Merhaba işlem düğümleri için etkili verileri Azure depolama içinde tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="ddca7-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="ddca7-165">HDFS yerine Azure depolama alanında hello veri depolamanın çeşitli avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="ddca7-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="ddca7-166">**Verileri yeniden kullanma ve paylaşma:** HDFS hello verilerde hello işlem kümesi içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="ddca7-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="ddca7-167">Erişim toohello yalnızca hello uygulamaları hesaplamak için küme hello verileri HDFS API'lerini kullanarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="ddca7-168">Azure depolama alanında Hello veriler erişilebilir hello HDFS API'lerini veya hello aracılığıyla [Blob Storage REST API'leri][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="ddca7-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="ddca7-169">Bu nedenle, daha büyük bir uygulamaları (diğer Hdınsight kümeleri dahil olmak üzere) ve araçları kullanılan tooproduce olması ve hello verileri kullanmak.</span><span class="sxs-lookup"><span data-stu-id="ddca7-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="ddca7-170">**Veri arşivleme:** verileri Azure depolama alanında depolamak hello Hdınsight kümelerini kullanıcı verilerini kaybetmeden güvenle silinmiş hesaplama toobe için kullanılan sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="ddca7-171">**Veri depolama maliyeti:** hello uzun vadeli bir işlem kümesi hello maliyeti Azure depolama hello Maliyet değerinden yüksek olduğundan hello veri Azure storage'da depolamaktan daha maliyetlidir; DFS veri depolama.</span><span class="sxs-lookup"><span data-stu-id="ddca7-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="ddca7-172">Ek olarak, Hello veri her işlem kümesi oluşturmada yeniden toobe sahip olmadığından veri yükleme maliyetlerinden de tasarruf edersiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="ddca7-173">**Esnek ölçeklendirme:** hdfs size ölçeklendirilmiş dosya sistemi ile hello ölçek, kümeniz için oluşturduğunuz düğüm hello sayısı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="ddca7-174">Merhaba ölçeğin değiştirilmesi hello esnek ölçeklendirme Azure depolama alanında otomatik olarak Al özelliklere bağlı olan daha daha karmaşık bir işlem haline gelebilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="ddca7-175">**Coğrafi çoğaltma:** Azure depolamanız coğrafi olarak çoğaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="ddca7-176">Bu size coğrafi kurtarma ve veri yedekliği sağlamakla birlikte, coğrafi olarak çoğaltılmış bir yük devretme toohello konum performansınızı ciddi bir şekilde etkiler ve ek ücrete neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="ddca7-177">Bizim önerimiz toochoose hello coğrafi çoğaltma akıllıca gelir ve yalnızca hello verilerin hello değerini hello ek maliyetlere ise.</span><span class="sxs-lookup"><span data-stu-id="ddca7-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="ddca7-178">Bazı MapReduce işleri ve paketleri Azure depolama alanında toostore gerçekten istemediğiniz Ara sonuçlar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="ddca7-179">Talebi toostore hello verilerde seçebilirler, yerel HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="ddca7-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="ddca7-180">Aslında, HDInsight Hive işleri ve diğer işlemlerdeki bu ara sonuçların bazıları için DFS kullanır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="ddca7-181">Çoğu HDFS komutu (örneğin, <b>ls</b>, <b>copyFromLocal</b> ve <b>mkdir</b>) hala beklendiği gibi çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="ddca7-182">(Başvurulan tooas DFS olan) belirli toohello yerel HDFS uygulamasına, gibi komutları yalnızca hello <b>fschk</b> ve <b>dfsadmin</b>, Azure depolama alanında farklı bir davranış gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="ddca7-183">Blob kapsayıcıları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddca7-183">Create Blob containers</span></span>
<span data-ttu-id="ddca7-184">toouse BLOB'ları önce oluşturduğunuz bir [Azure depolama hesabı][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="ddca7-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="ddca7-185">Bunun bir parçası olarak hello depolama hesabının oluşturulduğu bir Azure bölgesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="ddca7-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="ddca7-186">Merhaba küme ve hello depolama hesabı hello barındırılmalıdır aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="ddca7-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="ddca7-187">Merhaba Hive meta depo SQL Server veritabanı ve Oozie meta depo SQL Server veritabanı içinde de bulunmalıdır aynı bölgede hello.</span><span class="sxs-lookup"><span data-stu-id="ddca7-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="ddca7-188">Nerede olursa olsun, oluşturduğunuz her blob Azure Storage hesabınızı tooa kapsayıcısında aittir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="ddca7-189">Bu kapsayıcı HDInsight dışında oluşturulmuş bir blob veya bir HDInsight kümesi için oluşturulan bir kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="ddca7-190">Merhaba varsayılan Blob kapsayıcısı iş geçmişi ve günlükleri gibi kümeye özel bilgileri depolar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="ddca7-191">Varsayılan Blob kapsayıcısını birden çok HDInsight kümesiyle paylaşmayın.</span><span class="sxs-lookup"><span data-stu-id="ddca7-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="ddca7-192">Bu durum iş geçmişinin bozulmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-192">This might corrupt job history.</span></span> <span data-ttu-id="ddca7-193">Her biri için farklı bir kapsayıcı küme ve paylaşılan veri hello varsayılan depolama hesabı yerine tüm ilgili kümelerin dağıtımında belirtilen bağlantılı depolama hesabına yerleştirmek toouse önerilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="ddca7-194">Bağlantılı Depolama hesaplarını yapılandırma hakkında daha fazla bilgi için bkz: [HDInsight kümeleri oluşturma][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="ddca7-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="ddca7-195">Ancak Hello özgün Hdınsight kümesi silindikten sonra varsayılan depolama kapsayıcısını yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="ddca7-196">HBase kümeleri için aslında hello HBase tablo şemasını ve verileri silinmiş bir HBase kümesi tarafından kullanılan hello varsayılan blob kapsayıcısını kullanarak yeni bir HBase kümesi oluşturarak tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="ddca7-197">Hello Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="ddca7-197">Use hello Azure portal</span></span>
<span data-ttu-id="ddca7-198">Hello Portalı ' bir Hdınsight kümesi oluştururken, hello (aşağıda gösterildiği gibi) seçenekleri tooprovide hello depolama hesabı ayrıntıları sahip.</span><span class="sxs-lookup"><span data-stu-id="ddca7-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="ddca7-199">Bir ek depolama alanı hesabı hello kümesi ile ilişkili ve bu durumda, Data Lake Store hello ek depolama alanı olarak başka bir Azure Storage blobu seçin veya isteyip istemediğinizi de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![HDInsight hadoop oluşturma veri kaynağı](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="ddca7-201">Merhaba Hdınsight kümesi farklı bir konumda bir ek depolama alanı hesabı kullanarak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ddca7-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="ddca7-202">Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="ddca7-202">Use Azure PowerShell</span></span>
<span data-ttu-id="ddca7-203">Varsa, [Azure PowerShell'i yükleyip][powershell-install], bir depolama hesabı ve kapsayıcı hello Azure PowerShell komut istemi toocreate aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ddca7-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="ddca7-204">Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="ddca7-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="ddca7-205">Varsa [hello Azure CLI yükleyip](../cli-install-nodejs.md), hello şu komutu kullanılan tooa depolama hesabı ve kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="ddca7-206">Merhaba `--type` parametresi hello depolama hesabı nasıl yinelendiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="ddca7-207">Daha fazla bilgi için bkz. [Azure Storage çoğaltma](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ddca7-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="ddca7-208">ZRS, sayfa blobu, dosya, tablo veya kuyruğu desteklemediğinden, ZRS kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="ddca7-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="ddca7-209">Merhaba depolama hesabı oluşturulur istendiğinde toospecify hello coğrafi bölge var.</span><span class="sxs-lookup"><span data-stu-id="ddca7-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="ddca7-210">Hello hello depolama hesabı oluşturmanız gerekir Hdınsight kümenizi oluşturmayı planladığınızla aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="ddca7-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="ddca7-211">Merhaba depolama hesabı oluşturulduktan sonra komutu tooretrieve hello depolama hesabı anahtarlarını aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ddca7-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="ddca7-212">toocreate bir kapsayıcı hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ddca7-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="ddca7-213">Azure depolamada dosyaları adresleme</span><span class="sxs-lookup"><span data-stu-id="ddca7-213">Address files in Azure storage</span></span>
<span data-ttu-id="ddca7-214">Hdınsight'ta Azure depolama alanında dosyalara erişmek için hello URI düzeni şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ddca7-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="ddca7-215">Merhaba URI şeması şifrelenmemiş erişim sağlar (Merhaba ile *wasb:* önek) ve SSL şifreli erişim (ile *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="ddca7-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="ddca7-216">Kullanmanızı öneririz *wasbs* mümkün olduğunda, içinde bulunduğu erişilirken verileri azure'da aynı bölgede bile hello olduğunda.</span><span class="sxs-lookup"><span data-stu-id="ddca7-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="ddca7-217">Merhaba &lt;BlobStorageContainerName&gt; Azure depolama hello blob kapsayıcısında hello adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="ddca7-218">Merhaba &lt;StorageAccountName&gt; hello Azure depolama hesabı adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="ddca7-219">Tam uygun etki alanı adı (FQDN) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="ddca7-220">Ne &lt;BlobStorageContainerName&gt; ya da &lt;StorageAccountName&gt; belirtildiyse, hello varsayılan dosya sistemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="ddca7-221">Merhaba varsayılan dosya sistemindeki Hello dosyaları için göreli bir yol veya mutlak bir yol kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="ddca7-222">Örneğin, hello *hadoop mapreduce examples.jar* Hdınsight kümeleriyle gelen dosya hello aşağıdakilerden birini kullanarak başvurulan tooby olabilir:</span><span class="sxs-lookup"><span data-stu-id="ddca7-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="ddca7-223">Merhaba dosya adı <i>hadoop examples.jar</i> Hdınsight sürüm 2.1 ve 1.6 kümelerinde.</span><span class="sxs-lookup"><span data-stu-id="ddca7-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="ddca7-224">Merhaba &lt;yolu&gt; hello dosya veya dizin HDFS yol adıdır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="ddca7-225">Azure depolamadaki kapsayıcılar anahtar-değer depoları olduğundan, doğru hiyerarşik dosya sistemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="ddca7-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="ddca7-226">Bir blob anahtarındaki bir eğik çizgi karakteri (/) dizin ayırıcı olarak yorumlanır.</span><span class="sxs-lookup"><span data-stu-id="ddca7-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="ddca7-227">Örneğin, hello blob adı *hadoop mapreduce examples.jar* değil:</span><span class="sxs-lookup"><span data-stu-id="ddca7-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="ddca7-228">Hdınsight dışındaki BLOB'lar ile çalışırken, yardımcı programların çoğu değil hello WASB biçimini tanımaz ve bunun yerine bir temel yol biçimi gibi bekler `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="ddca7-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="ddca7-229">Bloblara erişme</span><span class="sxs-lookup"><span data-stu-id="ddca7-229">Access blobs</span></span> 


### <span data-ttu-id="ddca7-230"><a name="access-blobs-using-azure-powershell"></a> Azure PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="ddca7-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="ddca7-231">Bu bölümdeki Hello komutlar blob'larda depolanan PowerShell tooaccess verileri kullanarak, temel bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="ddca7-232">Hdınsight ile çalışmak için özelleştirilmiş daha tam özellikli bir örneğin hello bkz [Hdınsight Araçları](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="ddca7-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="ddca7-233">Komut toolist hello blob ile ilgili cmdlet'leri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ddca7-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Blob’la ilgili PowerShell cmdlet’lerinin listesi.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="ddca7-235">Dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="ddca7-235">Upload files</span></span>
<span data-ttu-id="ddca7-236">Bkz: [karşıya veri tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="ddca7-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="ddca7-237">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="ddca7-237">Download files</span></span>
<span data-ttu-id="ddca7-238">Merhaba aşağıdaki komut dosyasını bir blok blobu toohello geçerli klasöre indirir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="ddca7-239">Önce çalışan hello betik, yazma izinlerine sahip olduğu hello dizin tooa klasörü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ddca7-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="ddca7-240">Merhaba kaynak grubu adı ve hello küme adını vererek, hello aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ddca7-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="ddca7-241">Dosyaları silme</span><span class="sxs-lookup"><span data-stu-id="ddca7-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="ddca7-242">Dosyaları listeleme</span><span class="sxs-lookup"><span data-stu-id="ddca7-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="ddca7-243">Tanımlanmamış depolama hesabı kullanarak Hive sorgularını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ddca7-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="ddca7-244">Bu örnek nasıl toolist sırasında tanımlanmamış depolama hesabındaki bir klasör hello oluşturma işlemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ddca7-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="ddca7-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="ddca7-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="ddca7-246">Azure CLI kullanma</span><span class="sxs-lookup"><span data-stu-id="ddca7-246">Use Azure CLI</span></span>
<span data-ttu-id="ddca7-247">Komut toolist hello blob ile ilgili komutları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ddca7-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="ddca7-248">**Azure CLI tooupload bir dosya kullanma örneği**</span><span class="sxs-lookup"><span data-stu-id="ddca7-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="ddca7-249">**Azure CLI toodownload bir dosya kullanma örneği**</span><span class="sxs-lookup"><span data-stu-id="ddca7-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="ddca7-250">**Azure CLI toodelete bir dosya kullanma örneği**</span><span class="sxs-lookup"><span data-stu-id="ddca7-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="ddca7-251">**Azure CLI toolist dosyaları kullanma örneği**</span><span class="sxs-lookup"><span data-stu-id="ddca7-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="ddca7-252">Ek depolama hesaplarını kullanma</span><span class="sxs-lookup"><span data-stu-id="ddca7-252">Use additional storage accounts</span></span>

<span data-ttu-id="ddca7-253">Hdınsight kümesi oluştururken, onunla tooassociate istediğiniz hello Azure depolama hesabı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ddca7-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="ddca7-254">Ayrıca toothis depolama hesabı, ek depolama hesapları hello aynı ekleyebileceğiniz Azure aboneliği veya farklı Azure abonelikleri hello oluşturma işlemi sırasında veya bir küme oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="ddca7-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="ddca7-255">Ek depolama hesapları ekleme hakkında yönergeler için bkz. [HDInsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="ddca7-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="ddca7-256">Merhaba Hdınsight kümesi farklı bir konumda bir ek depolama alanı hesabı kullanarak desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ddca7-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddca7-257">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddca7-257">Next steps</span></span>
<span data-ttu-id="ddca7-258">Bu makalede, nasıl öğrenilen toouse HDFS uyumlu Azure storage Hdınsight ile.</span><span class="sxs-lookup"><span data-stu-id="ddca7-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="ddca7-259">Bu, toobuild ölçeklenebilir, uzun vadeli, arşivleme verileri edinme çözümleri ve kullanım depolanan hello içindeki Hdınsight toounlock hello bilgileri yapılandırılmış ve yapılandırılmamış verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddca7-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="ddca7-260">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="ddca7-260">For more information, see:</span></span>

* <span data-ttu-id="ddca7-261">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ddca7-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="ddca7-262">Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ddca7-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="ddca7-263">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ddca7-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ddca7-264">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ddca7-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="ddca7-265">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ddca7-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ddca7-266">[Hdınsight ile Azure Storage paylaşılan erişim imzaları toorestrict erişim toodata kullanma][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="ddca7-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
