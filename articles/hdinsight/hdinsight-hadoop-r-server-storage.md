---
title: "R Server hdınsight'ta - Azure depolama çözümleri aaaAzure | Microsoft Docs"
description: "Merhaba farklı depolama seçenekleri kullanılabilir toousers hdınsight'ta R Server ile hakkında bilgi edinin"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="225cd-103">Hdınsight'ta R Server için Azure depolama çözümleri</span><span class="sxs-lookup"><span data-stu-id="225cd-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="225cd-104">Microsoft hdınsight'ta R Server depolama çözümleri toopersist verileri, kod veya Analiz sonuçlarını içeren nesneleri çeşitli vardır.</span><span class="sxs-lookup"><span data-stu-id="225cd-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="225cd-105">Bu seçenekler aşağıdaki hello şunlardır:</span><span class="sxs-lookup"><span data-stu-id="225cd-105">These include hello following options:</span></span>

- [<span data-ttu-id="225cd-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="225cd-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="225cd-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="225cd-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="225cd-108">Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="225cd-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="225cd-109">Birden çok Azure depolama hesapları veya HDI kümesi ile kapsayıcıları erişme hello seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="225cd-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="225cd-110">Azure File storage toomount bir Azure depolama dosya paylaşımı, örneğin, hello Linux dosya sistemi sağlar hello edge düğüm üzerinde kullanım için uygun veri depolama seçeneği ' dir.</span><span class="sxs-lookup"><span data-stu-id="225cd-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="225cd-111">Ancak Azure dosya paylaşımları bağlanır ve Windows veya Linux gibi desteklenen bir işletim sistemi olan sistem tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="225cd-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="225cd-112">Hdınsight'ta Hadoop kümesi oluşturduğunuzda ya da belirttiğiniz bir **Azure depolama** hesabı veya bir **Data Lake deposu**.</span><span class="sxs-lookup"><span data-stu-id="225cd-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="225cd-113">Bu hesaptan belirli depolama kapsayıcısı hello dosya sistemi (örneğin, hello Hadoop dağıtılmış dosya sistemi) oluşturma hello küme için tutar.</span><span class="sxs-lookup"><span data-stu-id="225cd-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="225cd-114">Daha fazla bilgi ve yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="225cd-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="225cd-115">Hdınsight ile Azure depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="225cd-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="225cd-116">[Kullanım Data Lake Store ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="225cd-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="225cd-117">Hello Azure depolama çözümleri hakkında daha fazla bilgi için bkz: [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="225cd-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="225cd-118">Merhaba en uygun depolama seçeneği toouse senaryonuz için seçme ile ilgili yönergeler için bkz: [toouse Azure BLOB'olduğunda Deciding, Azure dosyaları ya da Azure veri diski](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="225cd-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="225cd-119">R Server ile Azure Blob storage hesapları kullanın</span><span class="sxs-lookup"><span data-stu-id="225cd-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="225cd-120">Gerekirse, birden çok Azure depolama hesapları veya kapsayıcıları HDI kümenizle erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="225cd-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="225cd-121">toodo hello Küme oluşturduğunuzda ve bu adımları toouse izleyin, toospecify hello ek depolama alanı hello UI hesaplarında ihtiyacınız R Server ile bunları.</span><span class="sxs-lookup"><span data-stu-id="225cd-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="225cd-122">Performans nedeniyle, hello Hdınsight kümesi hello aynı oluşturulan veri merkezi olarak belirttiğiniz hello birincil depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="225cd-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="225cd-123">Merhaba Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="225cd-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="225cd-124">Bir depolama hesabı adı ile bir Hdınsight kümesi oluşturmayı **storage1** ve varsayılan kapsayıcı adlı **container1**.</span><span class="sxs-lookup"><span data-stu-id="225cd-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="225cd-125">Adlı bir ek depolama alanı hesabı belirtin **storage2**.</span><span class="sxs-lookup"><span data-stu-id="225cd-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="225cd-126">Merhaba mycsv.csv dosyası toohello /share dizinine kopyalayın ve bu dosyada analiz gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="225cd-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="225cd-127">R kodda çok hello adı düğüm kümesi**varsayılan,** ve dizin ve dosya tooprocess ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="225cd-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="225cd-128">Tüm dizin ve dosya başvuruları noktası toohello depolama hesabı hello wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="225cd-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="225cd-129">Merhaba budur **varsayılan depolama hesabı** hello Hdınsight kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="225cd-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="225cd-130">Şimdi, tooprocess istediğinizi düşünelim dosya adında hello /private bulunan mySpecial.csv dizininde **container2** içinde **storage2**.</span><span class="sxs-lookup"><span data-stu-id="225cd-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="225cd-131">R kodunuzda hello adı düğümü başvuru toohello noktası **storage2** depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="225cd-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="225cd-132">Tüm hello dizin ve dosya başvuruları şimdi noktası toohello depolama hesabı wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="225cd-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="225cd-133">Merhaba budur **adı düğümü** belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="225cd-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="225cd-134">Tooconfigure hello/User/RevoShare/sahip<SSH username> dizininde **storage2** gibi:</span><span class="sxs-lookup"><span data-stu-id="225cd-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="225cd-135">R Server ile bir Azure Data Lake deposu kullanın</span><span class="sxs-lookup"><span data-stu-id="225cd-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="225cd-136">Hdınsight hesabınızla toouse Data Lake depolar, toouse istediğiniz küme erişim tooeach Azure Data Lake deponuza toogive gerekir.</span><span class="sxs-lookup"><span data-stu-id="225cd-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="225cd-137">Merhaba varsayılan depolama veya ek bir deposu olarak Azure Data Lake Store hesabı yönergeler nasıl toouse hello Azure portal toocreate bir Hdınsight kümesi için bkz: [AzureportalınıkullanarakDataLakeStoreilebirHdınsightkümesioluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="225cd-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="225cd-138">Merhaba önceki yordamda açıklandığı şekilde ikincil Azure depolama hesabı olduğu gibi daha sonra hello deposu R komut dosyanıza çok kullanın.</span><span class="sxs-lookup"><span data-stu-id="225cd-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="225cd-139">Azure Data Lake depolayan küme erişim tooyour Ekle</span><span class="sxs-lookup"><span data-stu-id="225cd-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="225cd-140">Hdınsight kümenizle ilişkili bir Azure Active Directory (Azure AD) hizmet sorumlusu kullanarak Data Lake deposu erişin.</span><span class="sxs-lookup"><span data-stu-id="225cd-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="225cd-141">bir Azure AD hizmet sorumlusu tooadd:</span><span class="sxs-lookup"><span data-stu-id="225cd-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="225cd-142">Hdınsight kümenize oluşturduğunuzda seçmeniz **kümeye özgü AAD kimliği** hello gelen **veri kaynağı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="225cd-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="225cd-143">Merhaba, **kümeye özgü AAD kimliği** iletişim kutusunda **AD hizmet sorumlusu seçin**seçin **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="225cd-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="225cd-144">Hello hizmet sorumlusu bir ad verin ve parola oluşturulduktan sonra tıklatın **ADLS erişimini yönetme** tooassociate Merhaba, Data Lake hizmet sorumlusuyla depolar.</span><span class="sxs-lookup"><span data-stu-id="225cd-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="225cd-145">Aynı zamanda olası tooadd küme erişim tooone olan veya daha fazla Data Lake küme oluşturma işlemi depolar.</span><span class="sxs-lookup"><span data-stu-id="225cd-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="225cd-146">Merhaba Data Lake store için Azure portal giriş açın ve çok**Veri Gezgini > erişim > Ekle**.</span><span class="sxs-lookup"><span data-stu-id="225cd-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="225cd-147">Data Lake deposu R sunucusundan nasıl tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="225cd-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="225cd-148">Erişim tooa Data Lake deposu verdiniz sonra ikincil Azure depolama hesabı yaptığınız Hdınsight hello yolda R Server hello deposunda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="225cd-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="225cd-149">tek fark bu hello önek hello **wasb: / /** çok değiştirir**adl: / /** gibi:</span><span class="sxs-lookup"><span data-stu-id="225cd-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="225cd-150">Merhaba aşağıdaki komutları kullanılan tooconfigure hello hello RevoShare dizin Data Lake storage hesabıyla olan ve hello örnek .csv dosyası hello önceki örnekten ekleyin:</span><span class="sxs-lookup"><span data-stu-id="225cd-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="225cd-151">R Server ile Azure File storage kullanma</span><span class="sxs-lookup"><span data-stu-id="225cd-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="225cd-152">[Azure dosyaları] ((https://azure.microsoft.com/services/storage/files/). adlı hello edge düğüm üzerinde kullanım için uygun veri depolama seçeneği bulunmaktadır</span><span class="sxs-lookup"><span data-stu-id="225cd-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="225cd-153">Toomount bir Azure depolama dosya paylaşımı toohello Linux dosya sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="225cd-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="225cd-154">Bu seçenek, veri dosyalarını, R betiklerini ve özellikle algılama toouse hello yerel dosya sisteminde HDFS yerine hello kenar düğümüne yaptığında gerekebilecek daha sonra sonuç nesneleri depolamak için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="225cd-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="225cd-155">Önemli bir avantajı Azure dosya paylaşımları bağlanır ve Windows veya Linux gibi desteklenen bir işletim sistemi sahip tüm sistemler tarafından kullanılan bu hello dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="225cd-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="225cd-156">Örneğin, bunu sizin veya ekibiniz birisi sahip başka bir Hdınsight kümesi, bir Azure VM veya bile bir şirket içi sistem tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="225cd-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="225cd-157">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="225cd-157">For more information, see:</span></span>

- [<span data-ttu-id="225cd-158">Nasıl toouse Linux Azure File storage</span><span class="sxs-lookup"><span data-stu-id="225cd-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="225cd-159">Nasıl toouse Windows'da Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="225cd-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="225cd-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="225cd-160">Next steps</span></span>

<span data-ttu-id="225cd-161">Hello Azure depolama seçenekleri anladığınıza göre hdınsight'ta R Server ile yapılan veri bilimi görevleri alma toodiscover yolları kullanım hello aşağıdaki bağlar.</span><span class="sxs-lookup"><span data-stu-id="225cd-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="225cd-162">Hdınsight'ta R Server genel bakış</span><span class="sxs-lookup"><span data-stu-id="225cd-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="225cd-163">Hadoop'ta R server kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="225cd-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="225cd-164">Rstudio'dan Server tooHDInsight (küme oluşturma sırasında eklenmedi varsa) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="225cd-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="225cd-165">HDInsight üzerinde R Server için işlem bağlamı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="225cd-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

