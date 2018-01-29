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
ms.openlocfilehash: 863277294fc0462e9221edffab1dd4e2001d7493
ms.sourcegitcommit: 4ac89872f4c86c612a71eb7ec30b755e7df89722
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Hdınsight'ta R Server için Azure depolama çözümleri

Microsoft hdınsight'ta R Server depolama çözümleri verileri, kod veya Analiz sonuçlarını içeren nesneleri kalıcı olması için çeşitli sahiptir. Bunlar, aşağıdaki seçenekleri içerir:

- [Azure Blob](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/)
- [Azure dosya depolama](https://azure.microsoft.com/services/storage/files/)

Ayrıca birden çok Azure depolama hesapları veya HDI kümesi ile kapsayıcıları erişme seçeneğiniz vardır. Azure File storage sağlayan bir Azure depolama dosya paylaşımı bağlamak Örneğin, kenar düğümüne Linux dosya sistemi üzerinde kullanım için uygun veri depolama seçeneği ' dir. Ancak Azure dosya paylaşımları bağlanır ve Windows veya Linux gibi desteklenen bir işletim sistemi olan sistem tarafından kullanılır. 

Hdınsight'ta Hadoop kümesi oluşturduğunuzda ya da belirttiğiniz bir **Azure depolama** hesabı veya bir **Data Lake deposu**. Bu hesaptan belirli depolama kapsayıcısı dosya sistemi (örneğin, Hadoop dağıtılmış dosya sistemi) oluşturmak küme tutar. Daha fazla bilgi ve yönergeler için bkz:

- [Hdınsight ile Azure depolama kullanma](../hdinsight-hadoop-use-blob-storage.md)
- [Kullanım Data Lake Store ile Azure Hdınsight kümeleri](../hdinsight-hadoop-use-data-lake-store.md). 

Azure depolama çözümleri hakkında daha fazla bilgi için bkz: [Microsoft Azure Storage'a giriş](../../storage/common/storage-introduction.md). 

Senaryonuz için kullanmak için en uygun depolama seçeneği ile ilgili yönergeler için bkz: [Azure BLOB'ları, Azure dosyaları ya da Azure veri diski kullanmaya karar verme](../../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>R Server ile Azure Blob storage hesapları kullanın

R Server kümenizi oluştururken birden fazla depolama hesabı belirtilmişse, aşağıdaki yönergeleri veri erişimi ve işlemleri R Server için ikincil bir hesabı kullanacak şekilde açıklanmaktadır. Aşağıdaki depolama hesapları ve kapsayıcı varsayalım: **storage1** ve varsayılan kapsayıcı adlı **container1**, ve **storage2**.

> [!WARNING]
> Performans nedeniyle, belirttiğiniz birincil depolama hesabıyla aynı veri merkezinde Hdınsight kümesi oluşturulur. Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.

1. Bir SSH İstemcisi'ni kullanarak kümenizi kenar düğümüne remoteuser bağlayın.  

  + Azure portalında > HDI Küme hizmeti sayfasına > genel bakış, tıklatın **güvenli Kabuk (SSH)**.
  + Ana bilgisayar adı, kenar düğümü seçin (içerdiği *ed-ssh.azurehdinsight.net* adında).
  + Ana bilgisayar adını kopyalayın.
  + PutTY veya SmartTY gibi bir SSH istemcisi açın ve ana bilgisayar adı girin.
  + Remoteuser tarafından küme parolasını ve ardından kullanıcı adı girin.
  
2. Mycsv.csv dosyasını /share dizinine kopyalayın. 

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

3. Geçiş R Studio veya başka bir R konsol ve R kodu adı düğümü ayarlamak için yazma **varsayılan** ve erişmek istediğiniz dosyanın konumu.  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(nameNode=myNameNode, consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

Depolama hesabı için tüm dizin ve dosya başvuruları noktası wasb://container1@storage1.blob.core.windows.net. Bu **varsayılan depolama hesabı** Hdınsight kümesi ile ilişkili.

Şimdi, /private bulunan mySpecial.csv adlı bir dosya işlemek istediğiniz varsayalım dizininde **container2** içinde **storage2**.

R kodunuzda adı düğümü referansı noktası **storage2** depolama hesabı.


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

Tüm dizin ve dosya başvurularını şimdi noktası depolama hesabına wasb://container2@storage2.blob.core.windows.net. Bu **adı düğümü** belirttiğiniz.

/ User/RevoShare/yapılandırmak zorunda<SSH username> dizininde **storage2** gibi:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>R Server ile bir Azure Data Lake deposu kullanın

Hdınsight hesabınızla Data Lake depoları kullanmak üzere kullanmak istediğiniz her Azure Data Lake store, küme erişim vermeniz gerekir. Varsayılan depolama veya ek bir deposu olarak Azure Data Lake Store hesabı olan bir Hdınsight kümesi oluşturmak için Azure portalını kullanma hakkında daha fazla yönerge için bkz: [Azure portalını kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Önceki yordamda açıklandığı şekilde ikincil Azure depolama hesabı olduğu gibi ardından deposu R komut dosyanıza çok kullanın.

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a>Azure Data Lake mağazalarının küme erişim Ekle
Hdınsight kümenizle ilişkili bir Azure Active Directory (Azure AD) hizmet sorumlusu kullanarak Data Lake deposu erişin.

Bir Azure AD hizmet sorumlusu eklemek için:

1. Hdınsight kümenize oluşturduğunuzda seçmeniz **kümeye özgü AAD kimliği** gelen **veri kaynağı** sekmesi.

2. İçinde **kümeye özgü AAD kimliği** iletişim kutusunda **AD hizmet sorumlusu seçin**seçin **Yeni Oluştur**.

Hizmet sorumlusu bir ad verin ve parola oluşturulduktan sonra tıklayın **ADLS erişimini yönetme** hizmet sorumlusu Data Lake depoları ile ilişkilendirilecek.

Küme oluşturma aşağıdaki bir veya daha fazla Data Lake depoları için Küme erişimi eklemek mümkündür. Bir Data Lake store için Azure portal giriş açın ve gidin **Veri Gezgini > erişim > Ekle**. 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a>Data Lake deposu R sunucudan erişme

Bir Data Lake deposu için access verdiniz sonra ikincil Azure depolama hesabı yaptığınız şekilde Hdınsight'ta R Server deposunda kullanabilirsiniz. Tek fark, önektir **wasb: / /** değişikliklerini **adl: / /** gibi:


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


Aşağıdaki komutları RevoShare dizinle Data Lake depolama hesabı yapılandırın ve önceki örnekten örnek .csv dosyası eklemek için kullanılır:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>R Server ile Azure File storage kullanma

[Azure dosyaları] ((https://azure.microsoft.com/services/storage/files/). adlı edge düğüm üzerinde kullanım için uygun veri depolama seçeneği bulunmaktadır Bir Azure depolama alanı dosya paylaşımını Linux dosya sistemine bağlama sağlar. Bu seçenek, veri dosyalarını, R betiklerini ve özellikle kenar düğümüne HDFS yerine yerel dosya sistemini kullanmak üzere mantıklıdır zaman gerekebilecek daha sonra sonuç nesneleri depolamak için kullanışlı olabilir. 

Azure dosyaları önemli bir avantajı dosya paylaşımları takılı ve Windows veya Linux gibi desteklenen bir işletim sistemi sahip tüm sistemler tarafından kullanılan olmasıdır. Örneğin, bunu sizin veya ekibiniz birisi sahip başka bir Hdınsight kümesi, bir Azure VM veya bile bir şirket içi sistem tarafından kullanılabilir. Daha fazla bilgi için bkz.

- [Azure Dosya depolamayı Linux ile kullanma](../../storage/files/storage-how-to-use-files-linux.md)
- [Windows Azure File storage kullanma](../../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Sonraki adımlar

Azure depolama seçenekleri anladığınıza göre hdınsight'ta R Server ile yapılan veri bilimi görevleri alma yollarını keşfetmek için aşağıdaki bağlantıları kullanın.

* [Hdınsight'ta R Server genel bakış](r-server-overview.md)
* [Hadoop'ta R server kullanmaya başlama](r-server-get-started.md)
* [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](r-server-compute-contexts.md)

