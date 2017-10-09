Azure Data Factory eklenen toopipelines ayrı ayrı olabilir veya zincirleme dönüştürme etkinlikleri başka bir etkinliği ile aşağıdaki hello destekler.

| Veri dönüştürme etkinliği | İşlem ortamı |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop Akışı](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Machine Learning etkinlikleri: Toplu Yürütme ve Kaynak Güncelleştirme](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [Saklı Yordam](../articles/data-factory/data-factory-stored-proc-activity.md) |Azure SQL, Azure SQL Veri Ambarı veya SQL Server |
| [Data Lake Analytics U-SQL](../articles/data-factory/data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] veya Azure Batch |

> [!NOTE]
> MapReduce etkinliği toorun Spark programları Hdınsight Spark kümesinde kullanabilirsiniz. Ayrıntılar için bkz. [Azure Data Factory’den Spark programlarını çağırma](../articles/data-factory/data-factory-spark.md).
> Özel Etkinlik toorun R komut dosyaları yüklü R ile Hdınsight kümenize oluşturabilirsiniz. Bkz. [Azure Data Factory kullanarak R Betiği çalıştırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).
> 
> 

