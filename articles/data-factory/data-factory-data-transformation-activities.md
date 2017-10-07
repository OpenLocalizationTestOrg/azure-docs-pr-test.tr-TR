---
title: "Veri dönüştürme: İşlem & dönüştürme veri | Microsoft Docs"
description: "Bilgi nasıl tootransform veya Hadoop, Machine Learning veya Azure Data Lake Analytics kullanarak Azure Data factory'de işlem verilerini."
keywords: "veri dönüştürme, işlem verileri, veri dönüştürme etkinliğine dönüştürme"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Azure Data Factory veri dönüştürme
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Hadoop Akışı](data-factory-hadoop-streaming-activity.md)
> * [Machine Learning](data-factory-azure-ml-batch-execution-activity.md) 
> * [Saklı Yordam](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL](data-factory-usql-activity.md)
> * [.NET özel](data-factory-use-custom-activities.md)

## <a name="overview"></a>Genel Bakış
Bu makalede Azure Data factory'de tootransform kullanabilirsiniz ve ham verilerinizi Öngörüler ve öngörü işler veri dönüştürme etkinlikleri açıklar. Azure Hdınsight kümesini veya bir Azure Batch gibi bilgi işlem ortamında dönüştürme etkinliğine yürütür. Bağlantılar tooarticles her dönüştürme etkinliği hakkında ayrıntılı bilgi sağlar.

Veri Fabrikası destekleyen çok eklenebilir veri dönüştürme etkinlikleri izleyerek hello[ardışık düzen](data-factory-create-pipelines.md) ya da ayrı ayrı veya başka bir etkinlikle zincirleme.

> [!NOTE]
> Adım adım yönergeler içeren bir anlatım için bkz: [ile Hive dönüşüm işlem hattı oluşturma](data-factory-build-your-first-pipeline.md) makalesi.  
> 
> 

## <a name="hdinsight-hive-activity"></a>Hdınsight Hive etkinliği
Merhaba Data Factory işlem hattı Hdınsight Hive etkinliğiyle kendi Hive sorguları ya da isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür. Bkz: [Hive etkinliği](data-factory-hive-activity.md) bu etkinliği hakkında ayrıntılı bilgi için makalenin. 

## <a name="hdinsight-pig-activity"></a>Hdınsight Pig etkinliği
Merhaba Data Factory işlem hattı Hdınsight Pig etkinlik kendi Pig sorgular veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür. Bkz: [Pig etkinlik](data-factory-pig-activity.md) bu etkinliği hakkında ayrıntılı bilgi için makalenin. 

## <a name="hdinsight-mapreduce-activity"></a>Hdınsight MapReduce etkinliği
Merhaba Data Factory işlem hattı Hdınsight MapReduce etkinlik kendi MapReduce programları veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür. Bkz: [MapReduce etkinliği](data-factory-map-reduce.md) bu etkinliği hakkında ayrıntılı bilgi için makalenin.

## <a name="hdinsight-streaming-activity"></a>Hdınsight akış etkinliği
Data Factory işlem hattı Hello Hdınsight akış etkinliği Hadoop akış programlar kendi veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür. Bkz: [Hdınsight akış etkinliği](data-factory-hadoop-streaming-activity.md) bu etkinliği hakkında ayrıntılı bilgi için.

## <a name="hdinsight-spark-activity"></a>HDInsight Spark Etkinliği
Merhaba Data Factory işlem hattı Hdınsight Spark etkinliğinde Spark programlar kendi Hdınsight kümesinde yürütür. Ayrıntılar için bkz [Azure Data Factory çağırma Spark programlardan](data-factory-spark.md). 

## <a name="machine-learning-activities"></a>Machine Learning etkinlikleri
Web hizmeti Tahmine dayalı analiz için azure Data Factory etkinleştirir, tooeasily yayımlanan bir Azure Machine Learning kullanan komut zincirleri oluşturun. Hello kullanarak [toplu iş yürütme etkinliği](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) bir Azure Data Factory işlem hattı bir Machine Learning web hizmeti toomake tahminleri toplu hello veriler üzerinde çağırabilirsiniz.

Zaman içinde veri kümeleri hello Machine Learning Puanlama denemeler retrained toobe yeni kullanarak gereken Tahmine dayalı modelleri hello girin. Yeniden eğitme ile tamamladıktan sonra web hizmeti ile Merhaba Puanlama tooupdate hello Machine Learning modelini retrained istiyor. Merhaba kullanabilirsiniz [kaynak güncelleştirme etkinliği](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) tooupdate hello web hizmeti ile Merhaba yeni eğitilen model.  

Bkz: [kullanım Machine Learning etkinlikleri](data-factory-azure-ml-batch-execution-activity.md) bu Machine Learning etkinlikler hakkında ayrıntılı bilgi için. 

## <a name="stored-procedure-activity"></a>Saklı yordam etkinliği
Data Factory işlem hattı tooinvoke bir saklı yordam veri depolarına aşağıdaki hello birinde hello SQL Server saklı yordam etkinliği kullanabilirsiniz: Azure SQL Database, Azure SQL Data Warehouse, SQL Server veritabanı kuruluşunuzdaki veya bir Azure VM. Bkz: [saklı yordam etkinliği](data-factory-stored-proc-activity.md) Ayrıntılar için makale.  

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL etkinliği
Data Lake Analytics U-SQL etkinliği Azure Data Lake Analytics kümede bir U-SQL komut dosyasını çalıştırır. Bkz: [veri analizi U-SQL etkinliği](data-factory-usql-activity.md) Ayrıntılar için makale. 

## <a name="net-custom-activity"></a>.NET özel etkinliği
Tootransform verileri Data Factory tarafından desteklenmeyen bir şekilde ihtiyacınız varsa, kendi veri işleme mantığı ile özel bir etkinlik oluşturmak ve hello ardışık düzeninde hello etkinliği kullanın. Bir Azure Batch hizmeti ya da Azure Hdınsight kümesi kullanarak hello özel .NET etkinliği toorun yapılandırabilirsiniz. Bkz: [özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) Ayrıntılar için makale. 

Özel Etkinlik toorun R komut dosyaları yüklü R ile Hdınsight kümenize oluşturabilirsiniz. Bkz. [Azure Data Factory kullanarak R Betiği çalıştırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). 

## <a name="compute-environments"></a>Ortamlar işlem
Merhaba bilgi işlem ortamı için bağlı hizmet oluşturup ardından hello bağlantılı hizmet dönüştürme etkinliğine tanımlarken kullanabilirsiniz. Bilgi işlem ortamları Data Factory ile desteklenen iki tür vardır. 

1. **İsteğe bağlı**: Bu durumda, hello bilgi işlem ortamı Data Factory ile tam olarak yönetilir. Bu otomatik olarak bir iş gönderilen tooprocess veri önce hello Data Factory hizmeti tarafından oluşturulan ve hello iş tamamlandığında kaldırıldı. Yapılandırma ve iş yürütme, küme yönetim ve eylemler önyükleme hello isteğe bağlı işlem ortamının ayrıntılı ayarlarını denetleyebilirsiniz. 
2. **Kendi bilgisayarınızı getirin**: Bu durumda, veri fabrikasında bağlı hizmet olarak kendi bilgi işlem ortamı (örneğin, Hdınsight kümesi) kaydedebilirsiniz. Merhaba bilgi işlem ortamı sizin tarafınızdan yönetilen ve hello Data Factory hizmetinin tooexecute hello etkinliklerini kullanır. 

Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) hakkında makale toolearn işlem Data Factory ile desteklenen Hizmetleri. 

## <a name="summary"></a>Özet
Veri dönüştürme etkinlikleri izleyerek hello ve bilgi işlem ortamları hello etkinlikler için hello Azure Data Factory destekler. Merhaba dönüştürme etkinlikleri eklenen toopipelines ayrı ayrı olabilir veya başka bir etkinlikle zincirleme.

| Veri dönüştürme etkinliği | İşlem ortamı |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Akışı](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Machine Learning etkinlikleri: Toplu Yürütme ve Kaynak Güncelleştirme](data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [Saklı Yordam](data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Veri Ambarı veya SQL Server |
| [Data Lake Analytics U-SQL](data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] veya Azure Batch |

