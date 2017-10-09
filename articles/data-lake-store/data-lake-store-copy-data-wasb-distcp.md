---
title: "aaaCopy veri tooand WASB Distcp'yi kullanarak Data Lake Store içine gelen | Microsoft Docs"
description: "Azure depolama BLOB'lar tooData Lake deposundan Distcp'yi aracı toocopy veri tooand kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="61266-103">Azure Storage Bloblarında ve Data Lake Store arasında Distcp'yi toocopy veri kullanın</span><span class="sxs-lookup"><span data-stu-id="61266-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61266-104">DistCp’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="61266-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="61266-105">AdlCopy’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="61266-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="61266-106">Erişim tooa Data Lake Store hesabı olan bir Hdınsight kümesi oluşturduktan sonra Distcp'yi toocopy veri gibi Hadoop ekosistemi araçları kullanabilirsiniz **tooand gelen** Data Lake Store hesabında bir Hdınsight küme depolama (WASB).</span><span class="sxs-lookup"><span data-stu-id="61266-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="61266-107">Bu makalede hakkında yönergeler sağlar tooachieve bu.</span><span class="sxs-lookup"><span data-stu-id="61266-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61266-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="61266-108">Prerequisites</span></span>
<span data-ttu-id="61266-109">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="61266-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="61266-110">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="61266-110">**An Azure subscription**.</span></span> <span data-ttu-id="61266-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61266-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="61266-112">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="61266-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="61266-113">Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="61266-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="61266-114">**Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="61266-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="61266-115">Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61266-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="61266-116">Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="61266-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="61266-117">Videolarla daha hızlı mı öğreniyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="61266-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="61266-118">[Bu videoyu izleyin](https://mix.office.com/watch/1liuojvdx6sie) nasıl toocopy verileri Azure Storage Bloblarında ve Distcp'yi kullanarak Data Lake Store arasında.</span><span class="sxs-lookup"><span data-stu-id="61266-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="61266-119">Bir Hdınsight Linux kümeden Distcp'yi kullanın</span><span class="sxs-lookup"><span data-stu-id="61266-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="61266-120">Bir Hdınsight kümesine farklı kaynaklardan kullanılan toocopy veri olabilir hello Distcp'yi yardımcı olan bir Hdınsight kümesi gelir.</span><span class="sxs-lookup"><span data-stu-id="61266-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="61266-121">Ek depolama alanı hello Hdınsight küme toouse Data Lake Store yapılandırdıysanız, hello yardımcı olabilir Distcp'yi Giden kutusu toocopy veri tooand da Data Lake Store hesabından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="61266-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="61266-122">Bu bölümde nasıl toouse hello adresindeki Distcp'yi yardımcı programı arayın.</span><span class="sxs-lookup"><span data-stu-id="61266-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="61266-123">Masaüstünüzdeki, SSH tooconnect toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="61266-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="61266-124">Bkz: [Bağlan tooa Linux tabanlı Hdınsight kümesi](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="61266-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="61266-125">Merhaba SSH isteminden Hello komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="61266-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="61266-126">Hello Azure Storage Blobları (WASB) erişim olup olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="61266-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="61266-127">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="61266-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="61266-128">Bu depolama blobu Merhaba içeriğine listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61266-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="61266-129">Benzer şekilde, hello kümeden hello Data Lake Store hesabı erişip erişemeyeceğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="61266-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="61266-130">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="61266-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="61266-131">Bu dosyalar/klasörler hello Data Lake Store hesabı içinde listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61266-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="61266-132">Distcp'yi toocopy verileri WASB tooa Data Lake Store hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="61266-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="61266-133">Bu hello Merhaba içeriğine kopyalayacak **/örnek/data/gutenberg/** WASB klasöründe çok**/myfolder** hello Data Lake Store hesabı içinde.</span><span class="sxs-lookup"><span data-stu-id="61266-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="61266-134">Benzer şekilde, Data Lake Store hesabı tooWASB Distcp'yi toocopy verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="61266-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="61266-135">Bu Merhaba içeriğine kopyalayacak **/myfolder** çok hello Data Lake Store hesabı**/örnek/data/gutenberg/** WASB klasöründe.</span><span class="sxs-lookup"><span data-stu-id="61266-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="61266-136">Distcp'yi kullanırken performans etkenleri</span><span class="sxs-lookup"><span data-stu-id="61266-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="61266-137">Distcp'yi düşük olduğundan ayrıntı düzeyi tek bir dosya, ayar hello en fazla sayıda eşzamanlı kopyasını hello en önemli parametre toooptimize Data Lake Store karşı.</span><span class="sxs-lookup"><span data-stu-id="61266-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="61266-138">Bu mappers hello sayısını ayarlayarak denetlenir ('M ') hello komut satırı parametresi.</span><span class="sxs-lookup"><span data-stu-id="61266-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="61266-139">Bu parametre kullanılan toocopy verileri mappers hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="61266-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="61266-140">Varsayılan değer 20'dir.</span><span class="sxs-lookup"><span data-stu-id="61266-140">Default value is 20.</span></span>

<span data-ttu-id="61266-141">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="61266-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="61266-142">Mappers toouse hello sayısını nasıl belirlerim?</span><span class="sxs-lookup"><span data-stu-id="61266-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="61266-143">Aşağıda kullanabileceğiniz bazı yönergeler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="61266-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="61266-144">**1. adım: toplam YARN bellek belirlemek** -hello ilk adımdır hello Distcp'yi iş çalıştırdığı toodetermine hello YARN bellek kullanılabilir toohello küme.</span><span class="sxs-lookup"><span data-stu-id="61266-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="61266-145">Bu bilgiler, hello kümesi ile ilişkili hello Ambari portalında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="61266-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="61266-146">TooYARN gidin ve hello yapılandırmalar sekmesi toosee hello YARN bellek görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="61266-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="61266-147">tooget hello toplam YARN bellek, Çarp hello hello düğüm sayısı ile düğüm başına YARN bellek kümenizdeki sahip.</span><span class="sxs-lookup"><span data-stu-id="61266-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="61266-148">**2. adım: mappers hello sayısını hesaplayın** -hello değerini **m** eşit toohello sayının toplam YARN bellek YARN kapsayıcı boyutu hello tarafından ayrılmış olan.</span><span class="sxs-lookup"><span data-stu-id="61266-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="61266-149">Merhaba YARN kapsayıcı boyutu bilgileri hello Ambari Portalı'nda da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="61266-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="61266-150">TooYARN gidin ve görünüm hello yapılandırmalar sekmesini hello YARN kapsayıcı boyutu Bu pencerede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="61266-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="61266-151">Eşitlik tooarrive mappers hello numarasına hello (**m**) değil</span><span class="sxs-lookup"><span data-stu-id="61266-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="61266-152">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="61266-152">**Example**</span></span>

<span data-ttu-id="61266-153">Merhaba kümede 4 D14v2s düğüm varsa ve tootransfer 10 TB çalıştığınız varsayalım 10 farklı klasörlerden veri.</span><span class="sxs-lookup"><span data-stu-id="61266-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="61266-154">Hello klasörlerinin her biri değişen miktarda veri içerir ve her klasördeki hello dosya boyutları farklıdır.</span><span class="sxs-lookup"><span data-stu-id="61266-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="61266-155">Toplam YARN bellekten - hello Ambari portal bu hello YARN bellek belirlemek için bir D14 düğümü 96 GB'dir.</span><span class="sxs-lookup"><span data-stu-id="61266-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="61266-156">Bu nedenle, 4 düğümlü bir küme için toplam YARN bellek şöyledir:</span><span class="sxs-lookup"><span data-stu-id="61266-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="61266-157">Mappers - hello 3072 D14 küme düğümü için bu hello YARN kapsayıcı boyutu olup Ambari Portalı'ndan sayısı.</span><span class="sxs-lookup"><span data-stu-id="61266-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="61266-158">Bu nedenle, mappers sayısıdır:</span><span class="sxs-lookup"><span data-stu-id="61266-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="61266-159">Diğer uygulamalar bellek kullanıyorsanız için Distcp'yi kümenizin YARN belleğin bir kısmını tooonly kullanım seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61266-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="61266-160">Büyük veri kümelerini kopyalama</span><span class="sxs-lookup"><span data-stu-id="61266-160">Copying large datasets</span></span>

<span data-ttu-id="61266-161">Ne zaman hello dataset toobe hello boyutunu taşınmış çok büyükse (örneğin > 1TB) veya birçok farklı klasörleri varsa, birden çok Distcp'yi işleri kullanmayı düşünmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="61266-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="61266-162">Büyük olasılıkla bir performans kazancı yoktur, ancak herhangi bir işi başarısız olursa, toorestart hello tüm iş yerine, belirli iş yalnızca gerekir böylece hello işleri yayılır.</span><span class="sxs-lookup"><span data-stu-id="61266-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="61266-163">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="61266-163">Limitations</span></span>

* <span data-ttu-id="61266-164">Distcp'yi boyutu toooptimize performans benzer toocreate mappers çalışır.</span><span class="sxs-lookup"><span data-stu-id="61266-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="61266-165">Mappers Hello sayısını artırmak her zaman performansı artırabilir değil.</span><span class="sxs-lookup"><span data-stu-id="61266-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="61266-166">Distcp'yi sınırlı tooonly bir Eşleyici dosya başına ' dir.</span><span class="sxs-lookup"><span data-stu-id="61266-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="61266-167">Bu nedenle, dosyaları olandan daha fazla mappers olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="61266-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="61266-168">Distcp'yi tooa dosyası yalnızca bir Eşleyici atayabilirsiniz olduğundan, bu kullanılan toocopy büyük dosyalar olabilir eşzamanlılık hello miktarını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="61266-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="61266-169">Büyük dosyaların küçük bir sayıya sahip sonra 256 MB dosya öbekleri toogive bölme, daha fazla olası eşzamanlılık.</span><span class="sxs-lookup"><span data-stu-id="61266-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="61266-170">Bir Azure Blob Depolama hesabından kopyalıyorsanız kopyalama işini hello blob depolama tarafında kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="61266-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="61266-171">Bu kopyalama işinin hello performansının düşmesine neden.</span><span class="sxs-lookup"><span data-stu-id="61266-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="61266-172">Azure Blob Storage ' hello sınırları hakkında daha fazla toolearn adresindeki Azure depolama sınırları bkz [Azure aboneliği ve hizmet sınırları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="61266-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="61266-173">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="61266-173">See also</span></span>
* [<span data-ttu-id="61266-174">Azure Storage Blobları tooData Lake Mağazası'ndan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="61266-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="61266-175">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="61266-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="61266-176">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="61266-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="61266-177">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="61266-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
