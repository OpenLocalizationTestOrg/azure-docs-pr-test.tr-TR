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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Hdınsight'ta R Server için Azure depolama çözümleri

Microsoft hdınsight'ta R Server depolama çözümleri toopersist verileri, kod veya Analiz sonuçlarını içeren nesneleri çeşitli vardır. Bu seçenekler aşağıdaki hello şunlardır:

- [Azure Blob](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/)
- [Azure dosya depolama](https://azure.microsoft.com/services/storage/files/)

Birden çok Azure depolama hesapları veya HDI kümesi ile kapsayıcıları erişme hello seçeneğiniz de vardır. Azure File storage toomount bir Azure depolama dosya paylaşımı, örneğin, hello Linux dosya sistemi sağlar hello edge düğüm üzerinde kullanım için uygun veri depolama seçeneği ' dir. Ancak Azure dosya paylaşımları bağlanır ve Windows veya Linux gibi desteklenen bir işletim sistemi olan sistem tarafından kullanılır. 

Hdınsight'ta Hadoop kümesi oluşturduğunuzda ya da belirttiğiniz bir **Azure depolama** hesabı veya bir **Data Lake deposu**. Bu hesaptan belirli depolama kapsayıcısı hello dosya sistemi (örneğin, hello Hadoop dağıtılmış dosya sistemi) oluşturma hello küme için tutar. Daha fazla bilgi ve yönergeler için bkz:

- [Hdınsight ile Azure depolama kullanma](hdinsight-hadoop-use-blob-storage.md)
- [Kullanım Data Lake Store ile Azure Hdınsight kümeleri](hdinsight-hadoop-use-data-lake-store.md). 

Hello Azure depolama çözümleri hakkında daha fazla bilgi için bkz: [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md). 

Merhaba en uygun depolama seçeneği toouse senaryonuz için seçme ile ilgili yönergeler için bkz: [toouse Azure BLOB'olduğunda Deciding, Azure dosyaları ya da Azure veri diski](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>R Server ile Azure Blob storage hesapları kullanın

Gerekirse, birden çok Azure depolama hesapları veya kapsayıcıları HDI kümenizle erişebilirsiniz. toodo hello Küme oluşturduğunuzda ve bu adımları toouse izleyin, toospecify hello ek depolama alanı hello UI hesaplarında ihtiyacınız R Server ile bunları.

> [!WARNING]
> Performans nedeniyle, hello Hdınsight kümesi hello aynı oluşturulan veri merkezi olarak belirttiğiniz hello birincil depolama hesabı. Merhaba Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.

1. Bir depolama hesabı adı ile bir Hdınsight kümesi oluşturmayı **storage1** ve varsayılan kapsayıcı adlı **container1**.
2. Adlı bir ek depolama alanı hesabı belirtin **storage2**.  
3. Merhaba mycsv.csv dosyası toohello /share dizinine kopyalayın ve bu dosyada analiz gerçekleştirin.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. R kodda çok hello adı düğüm kümesi**varsayılan,** ve dizin ve dosya tooprocess ayarlayın.  

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

Tüm dizin ve dosya başvuruları noktası toohello depolama hesabı hello wasb://container1@storage1.blob.core.windows.net. Merhaba budur **varsayılan depolama hesabı** hello Hdınsight kümesi ile ilişkili.

Şimdi, tooprocess istediğinizi düşünelim dosya adında hello /private bulunan mySpecial.csv dizininde **container2** içinde **storage2**.

R kodunuzda hello adı düğümü başvuru toohello noktası **storage2** depolama hesabı.


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

Tüm hello dizin ve dosya başvuruları şimdi noktası toohello depolama hesabı wasb://container2@storage2.blob.core.windows.net. Merhaba budur **adı düğümü** belirttiğiniz.

Tooconfigure hello/User/RevoShare/sahip<SSH username> dizininde **storage2** gibi:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>R Server ile bir Azure Data Lake deposu kullanın

Hdınsight hesabınızla toouse Data Lake depolar, toouse istediğiniz küme erişim tooeach Azure Data Lake deponuza toogive gerekir. Merhaba varsayılan depolama veya ek bir deposu olarak Azure Data Lake Store hesabı yönergeler nasıl toouse hello Azure portal toocreate bir Hdınsight kümesi için bkz: [AzureportalınıkullanarakDataLakeStoreilebirHdınsightkümesioluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Merhaba önceki yordamda açıklandığı şekilde ikincil Azure depolama hesabı olduğu gibi daha sonra hello deposu R komut dosyanıza çok kullanın.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Azure Data Lake depolayan küme erişim tooyour Ekle
Hdınsight kümenizle ilişkili bir Azure Active Directory (Azure AD) hizmet sorumlusu kullanarak Data Lake deposu erişin.

bir Azure AD hizmet sorumlusu tooadd:

1. Hdınsight kümenize oluşturduğunuzda seçmeniz **kümeye özgü AAD kimliği** hello gelen **veri kaynağı** sekmesi.

2. Merhaba, **kümeye özgü AAD kimliği** iletişim kutusunda **AD hizmet sorumlusu seçin**seçin **Yeni Oluştur**.

Hello hizmet sorumlusu bir ad verin ve parola oluşturulduktan sonra tıklatın **ADLS erişimini yönetme** tooassociate Merhaba, Data Lake hizmet sorumlusuyla depolar.

Aynı zamanda olası tooadd küme erişim tooone olan veya daha fazla Data Lake küme oluşturma işlemi depolar. Merhaba Data Lake store için Azure portal giriş açın ve çok**Veri Gezgini > erişim > Ekle**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Data Lake deposu R sunucusundan nasıl tooaccess hello

Erişim tooa Data Lake deposu verdiniz sonra ikincil Azure depolama hesabı yaptığınız Hdınsight hello yolda R Server hello deposunda kullanabilirsiniz. tek fark bu hello önek hello **wasb: / /** çok değiştirir**adl: / /** gibi:


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


Merhaba aşağıdaki komutları kullanılan tooconfigure hello hello RevoShare dizin Data Lake storage hesabıyla olan ve hello örnek .csv dosyası hello önceki örnekten ekleyin:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>R Server ile Azure File storage kullanma

[Azure dosyaları] ((https://azure.microsoft.com/services/storage/files/). adlı hello edge düğüm üzerinde kullanım için uygun veri depolama seçeneği bulunmaktadır Toomount bir Azure depolama dosya paylaşımı toohello Linux dosya sistemi sağlar. Bu seçenek, veri dosyalarını, R betiklerini ve özellikle algılama toouse hello yerel dosya sisteminde HDFS yerine hello kenar düğümüne yaptığında gerekebilecek daha sonra sonuç nesneleri depolamak için kullanışlı olabilir. 

Önemli bir avantajı Azure dosya paylaşımları bağlanır ve Windows veya Linux gibi desteklenen bir işletim sistemi sahip tüm sistemler tarafından kullanılan bu hello dosyasıdır. Örneğin, bunu sizin veya ekibiniz birisi sahip başka bir Hdınsight kümesi, bir Azure VM veya bile bir şirket içi sistem tarafından kullanılabilir. Daha fazla bilgi için bkz.

- [Nasıl toouse Linux Azure File storage](../storage/files/storage-how-to-use-files-linux.md)
- [Nasıl toouse Windows'da Azure dosya depolama](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Sonraki adımlar

Hello Azure depolama seçenekleri anladığınıza göre hdınsight'ta R Server ile yapılan veri bilimi görevleri alma toodiscover yolları kullanım hello aşağıdaki bağlar.

* [Hdınsight'ta R Server genel bakış](hdinsight-hadoop-r-server-overview.md)
* [Hadoop'ta R server kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md)
* [Rstudio'dan Server tooHDInsight (küme oluşturma sırasında eklenmedi varsa) ekleyin.](hdinsight-hadoop-r-server-install-r-studio.md)
* [HDInsight üzerinde R Server için işlem bağlamı seçenekleri](hdinsight-hadoop-r-server-compute-contexts.md)

