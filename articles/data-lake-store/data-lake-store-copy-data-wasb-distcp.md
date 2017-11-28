---
title: Veri WASB gelen ve giden Distcp'yi kullanarak Data Lake Store kopyalama | Microsoft Docs
description: "Azure Storage Bloblarında gelen ve Data Lake Store'a veri kopyalamak için Distcp'yi aracını kullanın"
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="f0bce-103">Azure Depolama Blobları ile Data Lake Store arasında veri kopyalamak için Distcp kullanma</span><span class="sxs-lookup"><span data-stu-id="f0bce-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0bce-104">DistCp’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="f0bce-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="f0bce-105">AdlCopy’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="f0bce-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="f0bce-106">Bir Data Lake Store hesabına erişimi olan bir Hdınsight kümesi oluşturduktan sonra verileri kopyalamak için Distcp'yi gibi Hadoop ekosistemi araçları kullanabilirsiniz **ve ondan** Data Lake Store hesabında bir Hdınsight küme depolama (WASB).</span><span class="sxs-lookup"><span data-stu-id="f0bce-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="f0bce-107">Bu makalede, bunu elde etme hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0bce-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0bce-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f0bce-108">Prerequisites</span></span>
<span data-ttu-id="f0bce-109">Bu makaleye başlamadan önce aşağıdakilere sahip olmanız ve aşağıdaki işlemleri yapmış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f0bce-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="f0bce-110">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="f0bce-110">**An Azure subscription**.</span></span> <span data-ttu-id="f0bce-111">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0bce-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f0bce-112">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="f0bce-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="f0bce-113">Bir oluşturma hakkında yönergeler için bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f0bce-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="f0bce-114">**Azure Hdınsight kümesi** bir Data Lake Store hesabına erişim.</span><span class="sxs-lookup"><span data-stu-id="f0bce-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="f0bce-115">Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f0bce-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="f0bce-116">Küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f0bce-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="f0bce-117">Videolarla daha hızlı mı öğreniyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="f0bce-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="f0bce-118">[Bu videoyu izleyin](https://mix.office.com/watch/1liuojvdx6sie) Azure Storage Bloblarında ve Distcp'yi kullanarak Data Lake Store arasında veri kopyalama hakkında.</span><span class="sxs-lookup"><span data-stu-id="f0bce-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="f0bce-119">Bir Hdınsight Linux kümeden Distcp'yi kullanın</span><span class="sxs-lookup"><span data-stu-id="f0bce-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="f0bce-120">Hdınsight kümesi bir Hdınsight kümesine farklı kaynaklardan veri kopyalamak için kullanılan Distcp'yi yardımcı programı ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="f0bce-121">Hdınsight kümesi Data Lake Store ek depolama alanı kullanmak için yapılandırdıysanız, kullanılan out-of-- ve da Data Lake Store hesabından veri kopyalamak için box Distcp'yi yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="f0bce-122">Bu bölümde Distcp'yi yardımcı programını kullanmak üzere nasıl tümleştirildiği incelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="f0bce-123">Masaüstünüzdeki, SSH kümeye bağlanmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="f0bce-124">Bkz: [Linux tabanlı Hdınsight kümesine bağlanma](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f0bce-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="f0bce-125">Komutları SSH isteminden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="f0bce-126">Azure Storage Blobları (WASB) erişim olup olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="f0bce-127">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f0bce-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="f0bce-128">Bu depolama blobu içeriğini listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="f0bce-129">Benzer şekilde, Data Lake Store hesabı kümeden erişip erişemeyeceğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="f0bce-130">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f0bce-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="f0bce-131">Bu dosyalar/klasörler Data Lake Store hesabındaki listesini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="f0bce-132">Verileri WASB bir Data Lake Store hesabına kopyalamak için Distcp'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="f0bce-133">Bu içeriği kopyalayacak **/örnek/data/gutenberg/** için WASB klasöründe **/myfolder** Data Lake Store hesabındaki.</span><span class="sxs-lookup"><span data-stu-id="f0bce-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="f0bce-134">Benzer şekilde, WASB için Data Lake Store hesabından veri kopyalamak için Distcp'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="f0bce-135">Bu içeriği kopyalayacak **/myfolder** için Data Lake Store hesabındaki **/örnek/data/gutenberg/** WASB klasöründe.</span><span class="sxs-lookup"><span data-stu-id="f0bce-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="f0bce-136">Distcp'yi kullanırken performans etkenleri</span><span class="sxs-lookup"><span data-stu-id="f0bce-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="f0bce-137">Distcp'yi'nin en düşük ayrıntı düzeyi tek bir dosya olduğundan, en fazla sayıda eşzamanlı kopyasını Data Lake Store karşı iyileştirmek için en önemli parametre ayardır.</span><span class="sxs-lookup"><span data-stu-id="f0bce-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="f0bce-138">Bu mappers sayısını ayarlayarak denetlenir ('M ') komut satırı parametresi.</span><span class="sxs-lookup"><span data-stu-id="f0bce-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="f0bce-139">Bu parametre veri kopyalamak için kullanılan mappers üst sınırını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="f0bce-140">Varsayılan değer 20'dir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-140">Default value is 20.</span></span>

<span data-ttu-id="f0bce-141">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="f0bce-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="f0bce-142">Kullanılacak mappers sayısını nasıl belirlerim?</span><span class="sxs-lookup"><span data-stu-id="f0bce-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="f0bce-143">Aşağıda kullanabileceğiniz bazı yönergeler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="f0bce-144">**1. adım: toplam YARN bellek belirlemek** -Distcp'yi iş çalıştırdığı küme için kullanılabilir YARN bellek belirlemek için ilk adımdır.</span><span class="sxs-lookup"><span data-stu-id="f0bce-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="f0bce-145">Bu bilgiler, kümeyle ilişkili ambarı portalında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="f0bce-146">YARN için gidin ve YARN bellek görmek için yapılandırmalar sekmesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f0bce-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="f0bce-147">Toplam YARN bellek almak için kümedeki sahip YARN bellek düğüm sayısı ile düğümü başına çarpın.</span><span class="sxs-lookup"><span data-stu-id="f0bce-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="f0bce-148">**2. adım: mappers sayısını hesaplayın** -değerini **m** bölü YARN kapsayıcı boyutundan toplam YARN bellek sayının eşittir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="f0bce-149">YARN kapsayıcı boyutu bilgileri Ambari Portalı'nda da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="f0bce-150">YARN için gidin ve yapılandırmalar sekmesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f0bce-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="f0bce-151">YARN kapsayıcı boyutu Bu pencerede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="f0bce-152">Mappers numaradan gelmesi denklemi (**m**) değil</span><span class="sxs-lookup"><span data-stu-id="f0bce-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="f0bce-153">**Örnek**</span><span class="sxs-lookup"><span data-stu-id="f0bce-153">**Example**</span></span>

<span data-ttu-id="f0bce-154">Kümede 4 D14v2s düğüm varsa ve 10 farklı klasörlerden 10 TB'lık veriyi aktarmaya çalıştığınız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="f0bce-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="f0bce-155">Klasörlerinin her biri değişen miktarda veri içerir ve her klasördeki dosya boyutları farklıdır.</span><span class="sxs-lookup"><span data-stu-id="f0bce-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="f0bce-156">Toplam YARN bellek - gelen Ambari portal YARN bellek D14 düğümü için 96 GB olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="f0bce-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="f0bce-157">Bu nedenle, 4 düğümlü bir küme için toplam YARN bellek şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f0bce-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="f0bce-158">Sayısı mappers - gelen Ambari portal YARN kapsayıcı boyutu D14 küme düğümü için 3072 olduğunu belirler.</span><span class="sxs-lookup"><span data-stu-id="f0bce-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="f0bce-159">Bu nedenle, mappers sayısıdır:</span><span class="sxs-lookup"><span data-stu-id="f0bce-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="f0bce-160">Daha sonra diğer uygulamaları bellek kullanıyorsanız, yalnızca kümenizin YARN belleğin bir kısmını için Distcp'yi kullanmayı da tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0bce-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="f0bce-161">Büyük veri kümelerini kopyalama</span><span class="sxs-lookup"><span data-stu-id="f0bce-161">Copying large datasets</span></span>

<span data-ttu-id="f0bce-162">Ne zaman taşınacak veri kümesi boyutu çok büyük olduğu (örneğin > 1TB) veya birçok farklı klasörleri varsa, birden çok Distcp'yi işleri kullanmayı düşünmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0bce-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="f0bce-163">Büyük olasılıkla bir performans kazancı yoktur, ancak herhangi bir işi başarısız olursa, yalnızca tüm iş yerine özel bir işi yeniden başlatmanız gerekir böylece işleri yayılır.</span><span class="sxs-lookup"><span data-stu-id="f0bce-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="f0bce-164">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="f0bce-164">Limitations</span></span>

* <span data-ttu-id="f0bce-165">Distcp'yi boyutunun performansını iyileştirmek için benzer mappers oluşturmayı dener.</span><span class="sxs-lookup"><span data-stu-id="f0bce-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="f0bce-166">Mappers sayısını artırmak her zaman performansı artırabilir değil.</span><span class="sxs-lookup"><span data-stu-id="f0bce-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="f0bce-167">Dosya başına yalnızca bir Eşleyici Distcp'yi sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="f0bce-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="f0bce-168">Bu nedenle, dosyaları olandan daha fazla mappers olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0bce-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="f0bce-169">Distcp'yi yalnızca bir dosyaya bir Eşleyici atayabilirsiniz olduğundan, bu büyük dosyaları kopyalamak için kullanılan eşzamanlılık miktarını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="f0bce-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="f0bce-170">Az sayıda büyük dosyalar varsa, bunları daha fazla olası eşzamanlılık vermek için 256 MB dosya parçalara bölünmesi.</span><span class="sxs-lookup"><span data-stu-id="f0bce-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="f0bce-171">Bir Azure Blob Depolama hesabından kopyalıyorsanız kopyalama işini blob depolama tarafında kısıtlanan.</span><span class="sxs-lookup"><span data-stu-id="f0bce-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="f0bce-172">Bu, kopyalama işini performansını bozar.</span><span class="sxs-lookup"><span data-stu-id="f0bce-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="f0bce-173">Azure Blob Depolama sınırları hakkında daha fazla bilgi için bkz: Azure Storage sınırlarını adresindeki [Azure aboneliği ve hizmet sınırları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f0bce-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f0bce-174">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f0bce-174">See also</span></span>
* [<span data-ttu-id="f0bce-175">Azure Storage Bloblarından Data Lake Store'a veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="f0bce-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="f0bce-176">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="f0bce-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="f0bce-177">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="f0bce-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f0bce-178">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="f0bce-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
