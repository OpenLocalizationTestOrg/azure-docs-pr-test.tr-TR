---
title: "Hive etkinliği - Azure kullanarak aaaTransform veri | Microsoft Docs"
description: "Bir Azure data factory toorun Hive sorguları hello Hive etkinliği bir üzerinde-isteğe bağlı/bilgisayarınızı kendi Hdınsight kümesinde nasıl kullanabileceğiniz hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a>Hive etkinliği Azure Data Factory kullanarak veri dönüştürme 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive etkinliği](data-factory-hive-activity.md) 
> * [Pig etkinliği](data-factory-pig-activity.md)
> * [MapReduce etkinliği](data-factory-map-reduce.md)
> * [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
> * [Spark etkinliği](data-factory-spark.md)
> * [Machine Learning Batch Yürütme Etkinliği](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Kaynak Güncelleştirme Etkinliği](data-factory-azure-ml-update-resource-activity.md)
> * [Saklı Yordam Etkinliği](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Etkinliği](data-factory-usql-activity.md)
> * [.NET özel etkinlik](data-factory-use-custom-activities.md)

Merhaba Data Factory Hdınsight Hive etkinliğiyle [ardışık düzen](data-factory-create-pipelines.md) üzerinde Hive sorguları yürüten [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi. Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.

> [!NOTE] 
> Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce. 

## <a name="syntax"></a>Sözdizimi

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a>Sözdizimi ayrıntıları
| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba etkinlik adı |Evet |
| açıklama |Hangi hello etkinliği için kullanılan açıklayan metin |Hayır |
| type |Hdınsighthive |Evet |
| Girişleri |Merhaba Hive etkinlik tarafından kullanılan girişleri |Hayır |
| Çıkışları |Merhaba Hive etkinliği tarafından üretilen çıkış |Evet |
| linkedServiceName |Veri fabrikasında bağlı hizmet olarak kayıtlı toohello Hdınsight kümesi başvurusu |Evet |
| Komut dosyası |Merhaba Hive betiği satır içi belirtin |Hayır |
| komut dosyası yolu |Mağaza hello Hive betiği bir Azure blob depolama alanındaki ve hello yol toohello dosyası sağlayın. 'Komut dosyası' veya 'scriptPath' özelliğini kullanın. Her ikisi birlikte kullanılamaz. Merhaba dosya adı büyük/küçük harf duyarlıdır. |Hayır |
| tanımlar |İçinde hello Hive betiği 'hiveconf' kullanarak başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin |Hayır |

## <a name="example"></a>Örnek
Şimdi göz önünde bulundurun oyun örneği, şirketiniz tarafından başlatılan oyunlar oynamak kullanıcılar tarafından tooidentify hello zamanın istediğiniz analytics günlüğe kaydeder. 

Merhaba aşağıdaki virgül bir örnek oyun günlük günlüktür (`,`) ayrılmış ve alanlar – Profileıd, SessionStart, süre, Srcıpaddress ve GameType aşağıdaki hello içerir.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Merhaba **Hive betiği** tooprocess bu veriler:

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

Bu kovana komut dosyası, bir Data Factory işlem hattı tooexecute toodo hello aşağıdaki gerekir

1. Bağlantılı hizmet tooregister oluşturma [kendi Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya yapılandırma [isteğe bağlı Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Şimdi bu bağlı hizmetin "HDInsightLinkedService" çağırın.
2. Oluşturma bir [bağlantılı hizmeti](data-factory-azure-blob-connector.md) hello verileri barındıran tooconfigure hello bağlantı tooAzure Blob Depolama. Şimdi bu bağlı hizmetin "StorageLinkedService" çağırın
3. Oluşturma [veri kümeleri](data-factory-create-datasets.md) toohello giriş ve hello işaret eden çıkış verileri. Şimdi hello girdi veri kümesi "HiveSampleIn" arayın ve çıkış veri kümesi "HiveSampleOut" Merhaba
4. Dosya tooAzure Blob Storage'nın #2. adımda yapılandırılmış olarak Hello Hive sorgusu kopyalayın. Merhaba depolama hello verileri barındırmak için bir bu sorgu dosyası barındırma hello farklı ise, ayrı bir Azure Storage bağlı hizmeti oluşturma ve hello etkinliğinde tooit bakın. Kullanım ** scriptPath ** toospecify hello yolu toohive sorgu dosyası ve **scriptLinkedService** toospecify hello hello komut dosyasını içeren Azure depolama. 
   
   > [!NOTE]
   > Hello kullanarak hello Hive betiği satır hello etkinlik tanımı içinde sağlayabilir **betik** özelliği. Hello komut dosyası hello JSON belgesi içinde bulunan tüm özel karakterleri kaçışlı toobe ihtiyaç duyar ve neden hata ayıklama sorunlar gibi bu yaklaşım önerilmez. Merhaba en iyi uygulama toofollow #4 adımdır.
   > 
   > 
5. Merhaba Hdınsighthive etkinliği ile işlem hattı oluşturacaksınız. Merhaba etkinlik işlemler/hello veri dönüşümler.

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. Merhaba ardışık düzen dağıtın. Bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) Ayrıntılar için makale. 
7. Fabrika Hello izleme verilerini kullanarak hello ardışık düzen ve Yönetimi görünümlerini izleyin. Bkz: [izleme ve Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale. 

## <a name="specifying-parameters-for-a-hive-script"></a>Bir Hive betiği parametrelerini belirtme
Bu örnekte, oyun günlükleri Azure Blob depolama alanına günlük alınan ve tarih ve saat ile bölümlenmiş bir klasörde depolanır. Merhaba giriş klasörü konumunu çalışma zamanı sırasında dinamik olarak geçirmek tooparameterize hello Hive betiğini istediğiniz ve ayrıca hello çıkış tarihi ve saati ile bölümlenmiş oluşturabilir.

Hive betiğini toouse parametreli, aşağıdaki hello yapın

* Merhaba parametrelerinde tanımlamak **tanımlar**.

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* Hello Hive betiği'da, toohello parametresini kullanarak başvurmak **${hiveconf:parameterName}**. 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a>Ayrıca Bkz.
* [Pig etkinliği](data-factory-pig-activity.md)
* [MapReduce etkinliği](data-factory-map-reduce.md)
* [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
* [Spark programlarını çağırma](data-factory-spark.md)
* [R betiklerini çağırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

