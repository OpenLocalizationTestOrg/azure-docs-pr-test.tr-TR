---
title: "pig etkinliği Azure Data Factory kullanarak aaaTransform veri | Microsoft Docs"
description: "Bir üzerinde-isteğe bağlı/bilgisayarınızı kendi Hdınsight kümesinde bir Azure data factory toorun Pig betikleri hello Pig etkinlik nasıl kullanabileceğinizi öğrenin."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Pig etkinliği Azure Data Factory kullanarak veri dönüştürme
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

Merhaba Data Factory Hdınsight Pig etkinliğinde [ardışık düzen](data-factory-create-pipelines.md) üzerinde Pig sorguları yürüten [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi. Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.

> [!NOTE] 
> Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce. 

## <a name="syntax"></a>Sözdizimi

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
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
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a>Sözdizimi ayrıntıları
| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba etkinlik adı |Evet |
| açıklama |Hangi hello etkinliği için kullanılan açıklayan metin |Hayır |
| type |HDinsightPig |Evet |
| Girişleri |Bir veya daha fazla girdi, Pig etkinlik hello tarafından kullanılan |Hayır |
| Çıkışları |Bir veya daha fazla çıkış Pig etkinlik hello tarafından üretilen |Evet |
| linkedServiceName |Veri fabrikasında bağlı hizmet olarak kayıtlı toohello Hdınsight kümesi başvurusu |Evet |
| Komut dosyası |Merhaba Pig betiği satır içi belirtin |Hayır |
| komut dosyası yolu |Bir Azure blob depolama alanına Hello Pig betiği depolar ve hello yol toohello dosyası sağlayın. 'Komut dosyası' veya 'scriptPath' özelliğini kullanın. Her ikisi birlikte kullanılamaz. Merhaba dosya adı büyük/küçük harf duyarlıdır. |Hayır |
| tanımlar |Pig betiği hello içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin |Hayır |

## <a name="example"></a>Örnek
Şimdi göz önünde bulundurun oyun örneği, şirketiniz tarafından başlatılan oyunlar oynamak oyuncu tarafından tooidentify hello zamanın istediğiniz analytics günlüğe kaydeder.

Aşağıdaki örnek oyun günlük hello bir virgülle (,) dosyasıdır. Alanlar – Profileıd, SessionStart, süre, Srcıpaddress ve GameType aşağıdaki hello içerir.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

Merhaba **Pig betiği** tooprocess bu veriler:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

Bu Pig komut dosyası, bir Data Factory işlem hattı tooexecute hello adımları izleyin:

1. Bağlantılı hizmet tooregister oluşturma [kendi Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya yapılandırma [isteğe bağlı Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service). Şimdi bu bağlı hizmetin çağrısı **HDInsightLinkedService**.
2. Oluşturma bir [bağlantılı hizmeti](data-factory-azure-blob-connector.md) hello verileri barındıran tooconfigure hello bağlantı tooAzure Blob Depolama. Şimdi bu bağlı hizmetin çağrısı **StorageLinkedService**.
3. Oluşturma [veri kümeleri](data-factory-create-datasets.md) toohello giriş ve hello işaret eden çıkış verileri. Şimdi hello girdi veri kümesi çağrısı **PigSampleIn** ve çıktı veri kümesi hello **PigSampleOut**.
4. Merhaba Pig sorgu dosyası hello Azure Blob Storage'nın #2. adımda yapılandırılmış kopyalayın. Merhaba hello verilerini barındıran Azure depolama hello sorgu dosyası barındıran hello bir farklıysa, ayrı bir Azure depolama bağlantılı hizmet oluşturun. Merhaba etkinlik yapılandırması bağlı toohello hizmetinde bakın. Kullanım ** scriptPath ** toospecify hello yolu toopig komut dosyası ve **scriptLinkedService**. 
   
   > [!NOTE]
   > Hello kullanarak hello Pig betiği satır hello etkinlik tanımı içinde sağlayabilir **betik** özelliği. Ancak, bu yaklaşım hello komut dosyasındaki tüm özel karakterleri olarak kaçışlı toobe gerekir ve hata ayıklama sorunlara neden olabilir önermiyoruz. Merhaba en iyi uygulama toofollow #4 adımdır.
   > 
   > 
5. Merhaba ardışık düzen HDInsightPig etkinlik hello ile oluşturun. Bu etkinlik, Hdınsight kümesinde Pig betiği çalıştırarak hello giriş verilerini işler.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. Merhaba ardışık düzen dağıtın. Bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) Ayrıntılar için makale. 
7. Fabrika Hello izleme verilerini kullanarak hello ardışık düzen ve Yönetimi görünümlerini izleyin. Bkz: [izleme ve Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale.

## <a name="specifying-parameters-for-a-pig-script"></a>Pig betiği parametrelerini belirtme
Aşağıdaki örnek hello göz önünde bulundurun: oyun günlükleri günlük Azure Blob depolama alanına alınan ve bölümlenmiş temel alınarak tarih ve saat bir klasörde depolanır. Hello giriş klasörü konumunu çalışma zamanı sırasında dinamik olarak geçirmek istediğiniz tooparameterize hello Pig betiği ve ayrıca hello çıkış tarihi ve saati ile bölümlenmiş oluşturabilir.

Pig betiği toouse parametreli, aşağıdaki hello yapın:

* Merhaba parametrelerinde tanımlamak **tanımlar**.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* Hello Pig betiği'da, kullanarak toohello parametrelerini başvuran '**$parameterName**' hello aşağıdaki örnekte gösterildiği gibi:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>Ayrıca Bkz.
* [Hive etkinliği](data-factory-hive-activity.md)
* [MapReduce etkinliği](data-factory-map-reduce.md)
* [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md)
* [Spark programlarını çağırma](data-factory-spark.md)
* [R betiklerini çağırma](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

