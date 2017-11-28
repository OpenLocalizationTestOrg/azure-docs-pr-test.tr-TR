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
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="5fb05-103">Hive etkinliği Azure Data Factory kullanarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="5fb05-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="5fb05-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="5fb05-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="5fb05-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="5fb05-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="5fb05-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="5fb05-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="5fb05-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="5fb05-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="5fb05-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="5fb05-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="5fb05-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="5fb05-114">Merhaba Data Factory Hdınsight Hive etkinliğiyle [ardışık düzen](data-factory-create-pipelines.md) üzerinde Hive sorguları yürüten [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="5fb05-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5fb05-115">Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="5fb05-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="5fb05-116">Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="5fb05-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="5fb05-117">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5fb05-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="5fb05-118">Sözdizimi ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="5fb05-118">Syntax details</span></span>
| <span data-ttu-id="5fb05-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="5fb05-119">Property</span></span> | <span data-ttu-id="5fb05-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5fb05-120">Description</span></span> | <span data-ttu-id="5fb05-121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5fb05-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5fb05-122">ad</span><span class="sxs-lookup"><span data-stu-id="5fb05-122">name</span></span> |<span data-ttu-id="5fb05-123">Merhaba etkinlik adı</span><span class="sxs-lookup"><span data-stu-id="5fb05-123">Name of hello activity</span></span> |<span data-ttu-id="5fb05-124">Evet</span><span class="sxs-lookup"><span data-stu-id="5fb05-124">Yes</span></span> |
| <span data-ttu-id="5fb05-125">açıklama</span><span class="sxs-lookup"><span data-stu-id="5fb05-125">description</span></span> |<span data-ttu-id="5fb05-126">Hangi hello etkinliği için kullanılan açıklayan metin</span><span class="sxs-lookup"><span data-stu-id="5fb05-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="5fb05-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fb05-127">No</span></span> |
| <span data-ttu-id="5fb05-128">type</span><span class="sxs-lookup"><span data-stu-id="5fb05-128">type</span></span> |<span data-ttu-id="5fb05-129">Hdınsighthive</span><span class="sxs-lookup"><span data-stu-id="5fb05-129">HDinsightHive</span></span> |<span data-ttu-id="5fb05-130">Evet</span><span class="sxs-lookup"><span data-stu-id="5fb05-130">Yes</span></span> |
| <span data-ttu-id="5fb05-131">Girişleri</span><span class="sxs-lookup"><span data-stu-id="5fb05-131">inputs</span></span> |<span data-ttu-id="5fb05-132">Merhaba Hive etkinlik tarafından kullanılan girişleri</span><span class="sxs-lookup"><span data-stu-id="5fb05-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="5fb05-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fb05-133">No</span></span> |
| <span data-ttu-id="5fb05-134">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="5fb05-134">outputs</span></span> |<span data-ttu-id="5fb05-135">Merhaba Hive etkinliği tarafından üretilen çıkış</span><span class="sxs-lookup"><span data-stu-id="5fb05-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="5fb05-136">Evet</span><span class="sxs-lookup"><span data-stu-id="5fb05-136">Yes</span></span> |
| <span data-ttu-id="5fb05-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="5fb05-137">linkedServiceName</span></span> |<span data-ttu-id="5fb05-138">Veri fabrikasında bağlı hizmet olarak kayıtlı toohello Hdınsight kümesi başvurusu</span><span class="sxs-lookup"><span data-stu-id="5fb05-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="5fb05-139">Evet</span><span class="sxs-lookup"><span data-stu-id="5fb05-139">Yes</span></span> |
| <span data-ttu-id="5fb05-140">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5fb05-140">script</span></span> |<span data-ttu-id="5fb05-141">Merhaba Hive betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="5fb05-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="5fb05-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fb05-142">No</span></span> |
| <span data-ttu-id="5fb05-143">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="5fb05-143">script path</span></span> |<span data-ttu-id="5fb05-144">Mağaza hello Hive betiği bir Azure blob depolama alanındaki ve hello yol toohello dosyası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5fb05-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="5fb05-145">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5fb05-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="5fb05-146">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5fb05-146">Both cannot be used together.</span></span> <span data-ttu-id="5fb05-147">Merhaba dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="5fb05-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="5fb05-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fb05-148">No</span></span> |
| <span data-ttu-id="5fb05-149">tanımlar</span><span class="sxs-lookup"><span data-stu-id="5fb05-149">defines</span></span> |<span data-ttu-id="5fb05-150">İçinde hello Hive betiği 'hiveconf' kullanarak başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="5fb05-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="5fb05-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="5fb05-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="5fb05-152">Örnek</span><span class="sxs-lookup"><span data-stu-id="5fb05-152">Example</span></span>
<span data-ttu-id="5fb05-153">Şimdi göz önünde bulundurun oyun örneği, şirketiniz tarafından başlatılan oyunlar oynamak kullanıcılar tarafından tooidentify hello zamanın istediğiniz analytics günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="5fb05-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="5fb05-154">Merhaba aşağıdaki virgül bir örnek oyun günlük günlüktür (`,`) ayrılmış ve alanlar – Profileıd, SessionStart, süre, Srcıpaddress ve GameType aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="5fb05-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="5fb05-155">Merhaba **Hive betiği** tooprocess bu veriler:</span><span class="sxs-lookup"><span data-stu-id="5fb05-155">hello **Hive script** tooprocess this data:</span></span>

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

<span data-ttu-id="5fb05-156">Bu kovana komut dosyası, bir Data Factory işlem hattı tooexecute toodo hello aşağıdaki gerekir</span><span class="sxs-lookup"><span data-stu-id="5fb05-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="5fb05-157">Bağlantılı hizmet tooregister oluşturma [kendi Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya yapılandırma [isteğe bağlı Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="5fb05-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="5fb05-158">Şimdi bu bağlı hizmetin "HDInsightLinkedService" çağırın.</span><span class="sxs-lookup"><span data-stu-id="5fb05-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="5fb05-159">Oluşturma bir [bağlantılı hizmeti](data-factory-azure-blob-connector.md) hello verileri barındıran tooconfigure hello bağlantı tooAzure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="5fb05-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="5fb05-160">Şimdi bu bağlı hizmetin "StorageLinkedService" çağırın</span><span class="sxs-lookup"><span data-stu-id="5fb05-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="5fb05-161">Oluşturma [veri kümeleri](data-factory-create-datasets.md) toohello giriş ve hello işaret eden çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="5fb05-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="5fb05-162">Şimdi hello girdi veri kümesi "HiveSampleIn" arayın ve çıkış veri kümesi "HiveSampleOut" Merhaba</span><span class="sxs-lookup"><span data-stu-id="5fb05-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="5fb05-163">Dosya tooAzure Blob Storage'nın #2. adımda yapılandırılmış olarak Hello Hive sorgusu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5fb05-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="5fb05-164">Merhaba depolama hello verileri barındırmak için bir bu sorgu dosyası barındırma hello farklı ise, ayrı bir Azure Storage bağlı hizmeti oluşturma ve hello etkinliğinde tooit bakın.</span><span class="sxs-lookup"><span data-stu-id="5fb05-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="5fb05-165">Kullanım ** scriptPath ** toospecify hello yolu toohive sorgu dosyası ve **scriptLinkedService** toospecify hello hello komut dosyasını içeren Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="5fb05-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5fb05-166">Hello kullanarak hello Hive betiği satır hello etkinlik tanımı içinde sağlayabilir **betik** özelliği.</span><span class="sxs-lookup"><span data-stu-id="5fb05-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="5fb05-167">Hello komut dosyası hello JSON belgesi içinde bulunan tüm özel karakterleri kaçışlı toobe ihtiyaç duyar ve neden hata ayıklama sorunlar gibi bu yaklaşım önerilmez.</span><span class="sxs-lookup"><span data-stu-id="5fb05-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="5fb05-168">Merhaba en iyi uygulama toofollow #4 adımdır.</span><span class="sxs-lookup"><span data-stu-id="5fb05-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="5fb05-169">Merhaba Hdınsighthive etkinliği ile işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5fb05-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="5fb05-170">Merhaba etkinlik işlemler/hello veri dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="5fb05-170">hello activity processes/transforms hello data.</span></span>

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
6. <span data-ttu-id="5fb05-171">Merhaba ardışık düzen dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5fb05-171">Deploy hello pipeline.</span></span> <span data-ttu-id="5fb05-172">Bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="5fb05-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="5fb05-173">Fabrika Hello izleme verilerini kullanarak hello ardışık düzen ve Yönetimi görünümlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="5fb05-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="5fb05-174">Bkz: [izleme ve Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="5fb05-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="5fb05-175">Bir Hive betiği parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="5fb05-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="5fb05-176">Bu örnekte, oyun günlükleri Azure Blob depolama alanına günlük alınan ve tarih ve saat ile bölümlenmiş bir klasörde depolanır.</span><span class="sxs-lookup"><span data-stu-id="5fb05-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="5fb05-177">Merhaba giriş klasörü konumunu çalışma zamanı sırasında dinamik olarak geçirmek tooparameterize hello Hive betiğini istediğiniz ve ayrıca hello çıkış tarihi ve saati ile bölümlenmiş oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="5fb05-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="5fb05-178">Hive betiğini toouse parametreli, aşağıdaki hello yapın</span><span class="sxs-lookup"><span data-stu-id="5fb05-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="5fb05-179">Merhaba parametrelerinde tanımlamak **tanımlar**.</span><span class="sxs-lookup"><span data-stu-id="5fb05-179">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="5fb05-180">Hello Hive betiği'da, toohello parametresini kullanarak başvurmak **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="5fb05-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="5fb05-181">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="5fb05-181">See Also</span></span>
* [<span data-ttu-id="5fb05-182">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="5fb05-183">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="5fb05-184">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="5fb05-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="5fb05-185">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="5fb05-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="5fb05-186">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="5fb05-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

