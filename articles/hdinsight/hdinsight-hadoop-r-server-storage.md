---
title: "Hdınsight'ta - Azure R Server için Azure depolama çözümleri | Microsoft Docs"
description: "Hdınsight'ta R Server ile kullanıcılar için kullanılabilir farklı depolama seçenekleri hakkında bilgi edinin"
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="5bf65-103">Hdınsight'ta R Server için Azure depolama çözümleri</span><span class="sxs-lookup"><span data-stu-id="5bf65-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="5bf65-104">Microsoft hdınsight'ta R Server depolama çözümleri verileri, kod veya Analiz sonuçlarını içeren nesneleri kalıcı olması için çeşitli sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5bf65-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="5bf65-105">Bunlar, aşağıdaki seçenekleri içerir:</span><span class="sxs-lookup"><span data-stu-id="5bf65-105">These include the following options:</span></span>

- [<span data-ttu-id="5bf65-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="5bf65-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="5bf65-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="5bf65-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="5bf65-108">Azure dosya depolama</span><span class="sxs-lookup"><span data-stu-id="5bf65-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="5bf65-109">Ayrıca birden çok Azure depolama hesapları veya HDI kümesi ile kapsayıcıları erişme seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="5bf65-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="5bf65-110">Azure File storage sağlayan bir Azure depolama dosya paylaşımı bağlamak Örneğin, kenar düğümüne Linux dosya sistemi üzerinde kullanım için uygun veri depolama seçeneği ' dir.</span><span class="sxs-lookup"><span data-stu-id="5bf65-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="5bf65-111">Ancak Azure dosya paylaşımları bağlanır ve Windows veya Linux gibi desteklenen bir işletim sistemi olan sistem tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5bf65-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="5bf65-112">Hdınsight'ta Hadoop kümesi oluşturduğunuzda ya da belirttiğiniz bir **Azure depolama** hesabı veya bir **Data Lake deposu**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="5bf65-113">Bu hesaptan belirli depolama kapsayıcısı dosya sistemi (örneğin, Hadoop dağıtılmış dosya sistemi) oluşturmak küme tutar.</span><span class="sxs-lookup"><span data-stu-id="5bf65-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="5bf65-114">Daha fazla bilgi ve yönergeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="5bf65-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="5bf65-115">Hdınsight ile Azure depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="5bf65-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="5bf65-116">[Kullanım Data Lake Store ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="5bf65-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="5bf65-117">Azure depolama çözümleri hakkında daha fazla bilgi için bkz: [Microsoft Azure Storage'a giriş](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5bf65-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="5bf65-118">Senaryonuz için kullanmak için en uygun depolama seçeneği ile ilgili yönergeler için bkz: [Azure BLOB'ları, Azure dosyaları ya da Azure veri diski kullanmaya karar verme](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="5bf65-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="5bf65-119">R Server ile Azure Blob storage hesapları kullanın</span><span class="sxs-lookup"><span data-stu-id="5bf65-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="5bf65-120">Gerekirse, birden çok Azure depolama hesapları veya kapsayıcıları HDI kümenizle erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5bf65-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="5bf65-121">Bunu yapmak için Küme oluşturduğunuzda ve ardından R Server ile kullanmak için aşağıdaki adımları izleyin ek depolama hesapları kullanıcı Arabiriminde belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5bf65-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="5bf65-122">Performans nedeniyle, belirttiğiniz birincil depolama hesabıyla aynı veri merkezinde Hdınsight kümesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5bf65-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="5bf65-123">Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5bf65-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="5bf65-124">Bir depolama hesabı adı ile bir Hdınsight kümesi oluşturmayı **storage1** ve varsayılan kapsayıcı adlı **container1**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="5bf65-125">Adlı bir ek depolama alanı hesabı belirtin **storage2**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="5bf65-126">Mycsv.csv dosyasını /share dizinine kopyalayın ve bu dosyada analiz gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5bf65-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="5bf65-127">R kodda adı düğüm kümesi **varsayılan,** ve işlemek için dosya ve dizin ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5bf65-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="5bf65-128">Depolama hesabı için tüm dizin ve dosya başvuruları noktası wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5bf65-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="5bf65-129">Bu **varsayılan depolama hesabı** Hdınsight kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="5bf65-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="5bf65-130">Şimdi, /private bulunan mySpecial.csv adlı bir dosya işlemek istediğiniz varsayalım dizininde **container2** içinde **storage2**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="5bf65-131">R kodunuzda adı düğümü referansı noktası **storage2** depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="5bf65-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="5bf65-132">Tüm dizin ve dosya başvurularını şimdi noktası depolama hesabına wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5bf65-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="5bf65-133">Bu **adı düğümü** belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="5bf65-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="5bf65-134">/ User/RevoShare/yapılandırmak zorunda<SSH username> dizininde **storage2** gibi:</span><span class="sxs-lookup"><span data-stu-id="5bf65-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="5bf65-135">R Server ile bir Azure Data Lake deposu kullanın</span><span class="sxs-lookup"><span data-stu-id="5bf65-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="5bf65-136">Hdınsight hesabınızla Data Lake depoları kullanmak üzere kullanmak istediğiniz her Azure Data Lake store, küme erişim vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5bf65-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="5bf65-137">Varsayılan depolama veya ek bir deposu olarak Azure Data Lake Store hesabı olan bir Hdınsight kümesi oluşturmak için Azure portalını kullanma hakkında daha fazla yönerge için bkz: [Azure portalını kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5bf65-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="5bf65-138">Önceki yordamda açıklandığı şekilde ikincil Azure depolama hesabı olduğu gibi ardından deposu R komut dosyanıza çok kullanın.</span><span class="sxs-lookup"><span data-stu-id="5bf65-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="5bf65-139">Azure Data Lake mağazalarının küme erişim Ekle</span><span class="sxs-lookup"><span data-stu-id="5bf65-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="5bf65-140">Hdınsight kümenizle ilişkili bir Azure Active Directory (Azure AD) hizmet sorumlusu kullanarak Data Lake deposu erişin.</span><span class="sxs-lookup"><span data-stu-id="5bf65-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="5bf65-141">Bir Azure AD hizmet sorumlusu eklemek için:</span><span class="sxs-lookup"><span data-stu-id="5bf65-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="5bf65-142">Hdınsight kümenize oluşturduğunuzda seçmeniz **kümeye özgü AAD kimliği** gelen **veri kaynağı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5bf65-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="5bf65-143">İçinde **kümeye özgü AAD kimliği** iletişim kutusunda **AD hizmet sorumlusu seçin**seçin **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="5bf65-144">Hizmet sorumlusu bir ad verin ve parola oluşturulduktan sonra tıklayın **ADLS erişimini yönetme** hizmet sorumlusu Data Lake depoları ile ilişkilendirilecek.</span><span class="sxs-lookup"><span data-stu-id="5bf65-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="5bf65-145">Küme oluşturma aşağıdaki bir veya daha fazla Data Lake depoları için Küme erişimi eklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="5bf65-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="5bf65-146">Bir Data Lake store için Azure portal giriş açın ve gidin **Veri Gezgini > erişim > Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5bf65-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="5bf65-147">Data Lake deposu R sunucudan erişme</span><span class="sxs-lookup"><span data-stu-id="5bf65-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="5bf65-148">Bir Data Lake deposu için access verdiniz sonra ikincil Azure depolama hesabı yaptığınız şekilde Hdınsight'ta R Server deposunda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5bf65-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="5bf65-149">Tek fark, önektir **wasb: / /** değişikliklerini **adl: / /** gibi:</span><span class="sxs-lookup"><span data-stu-id="5bf65-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="5bf65-150">Aşağıdaki komutları RevoShare dizinle Data Lake depolama hesabı yapılandırın ve önceki örnekten örnek .csv dosyası eklemek için kullanılır:</span><span class="sxs-lookup"><span data-stu-id="5bf65-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="5bf65-151">R Server ile Azure File storage kullanma</span><span class="sxs-lookup"><span data-stu-id="5bf65-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="5bf65-152">[Azure dosyaları] ((https://azure.microsoft.com/services/storage/files/). adlı edge düğüm üzerinde kullanım için uygun veri depolama seçeneği bulunmaktadır</span><span class="sxs-lookup"><span data-stu-id="5bf65-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="5bf65-153">Bir Azure depolama alanı dosya paylaşımını Linux dosya sistemine bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="5bf65-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="5bf65-154">Bu seçenek, veri dosyalarını, R betiklerini ve özellikle kenar düğümüne HDFS yerine yerel dosya sistemini kullanmak üzere mantıklıdır zaman gerekebilecek daha sonra sonuç nesneleri depolamak için kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5bf65-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="5bf65-155">Azure dosyaları önemli bir avantajı dosya paylaşımları takılı ve Windows veya Linux gibi desteklenen bir işletim sistemi sahip tüm sistemler tarafından kullanılan olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="5bf65-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="5bf65-156">Örneğin, bunu sizin veya ekibiniz birisi sahip başka bir Hdınsight kümesi, bir Azure VM veya bile bir şirket içi sistem tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5bf65-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="5bf65-157">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="5bf65-157">For more information, see:</span></span>

- [<span data-ttu-id="5bf65-158">Azure Dosya depolamayı Linux ile kullanma</span><span class="sxs-lookup"><span data-stu-id="5bf65-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="5bf65-159">Windows Azure File storage kullanma</span><span class="sxs-lookup"><span data-stu-id="5bf65-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="5bf65-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5bf65-160">Next steps</span></span>

<span data-ttu-id="5bf65-161">Azure depolama seçenekleri anladığınıza göre hdınsight'ta R Server ile yapılan veri bilimi görevleri alma yollarını keşfetmek için aşağıdaki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="5bf65-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="5bf65-162">Hdınsight'ta R Server genel bakış</span><span class="sxs-lookup"><span data-stu-id="5bf65-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="5bf65-163">Hadoop'ta R server kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5bf65-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="5bf65-164">Hdınsight'a Rstudio'dan sunucu ekleme (değilse küme oluşturma sırasında eklenen)</span><span class="sxs-lookup"><span data-stu-id="5bf65-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="5bf65-165">HDInsight üzerinde R Server için işlem bağlamı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5bf65-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

