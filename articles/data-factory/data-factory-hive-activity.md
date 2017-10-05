---
title: "Hive etkinliği - Azure kullanarak veri dönüştürme | Microsoft Docs"
description: "Hive etkinliği bir Azure data factory'de bir üzerinde-isteğe bağlı/bilgisayarınızı kendi Hdınsight kümesinde Hive sorguları çalıştırmak için nasıl kullanabileceğinizi öğrenin."
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="4fe65-103">Hive etkinliği Azure Data Factory kullanarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="4fe65-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4fe65-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4fe65-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4fe65-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4fe65-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4fe65-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4fe65-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4fe65-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4fe65-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4fe65-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4fe65-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="4fe65-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="4fe65-114">Veri Fabrikası Hdınsight Hive etkinliğiyle [ardışık düzen](data-factory-create-pipelines.md) üzerinde Hive sorguları yürüten [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="4fe65-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4fe65-115">Bu makalede derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="4fe65-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="4fe65-116">Azure Data Factory yeniyseniz okuyun [Azure Data Factory'ye giriş](data-factory-introduction.md) ve öğretici: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="4fe65-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="4fe65-117">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4fe65-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="4fe65-118">Sözdizimi ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4fe65-118">Syntax details</span></span>
| <span data-ttu-id="4fe65-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="4fe65-119">Property</span></span> | <span data-ttu-id="4fe65-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4fe65-120">Description</span></span> | <span data-ttu-id="4fe65-121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4fe65-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fe65-122">ad</span><span class="sxs-lookup"><span data-stu-id="4fe65-122">name</span></span> |<span data-ttu-id="4fe65-123">Etkinlik adı</span><span class="sxs-lookup"><span data-stu-id="4fe65-123">Name of the activity</span></span> |<span data-ttu-id="4fe65-124">Evet</span><span class="sxs-lookup"><span data-stu-id="4fe65-124">Yes</span></span> |
| <span data-ttu-id="4fe65-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4fe65-125">description</span></span> |<span data-ttu-id="4fe65-126">Etkinlik hangi amaçla kullanıldığına açıklayan metin</span><span class="sxs-lookup"><span data-stu-id="4fe65-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="4fe65-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="4fe65-127">No</span></span> |
| <span data-ttu-id="4fe65-128">type</span><span class="sxs-lookup"><span data-stu-id="4fe65-128">type</span></span> |<span data-ttu-id="4fe65-129">Hdınsighthive</span><span class="sxs-lookup"><span data-stu-id="4fe65-129">HDinsightHive</span></span> |<span data-ttu-id="4fe65-130">Evet</span><span class="sxs-lookup"><span data-stu-id="4fe65-130">Yes</span></span> |
| <span data-ttu-id="4fe65-131">Girişleri</span><span class="sxs-lookup"><span data-stu-id="4fe65-131">inputs</span></span> |<span data-ttu-id="4fe65-132">Hive etkinlik tarafından kullanılan girişleri</span><span class="sxs-lookup"><span data-stu-id="4fe65-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="4fe65-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="4fe65-133">No</span></span> |
| <span data-ttu-id="4fe65-134">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="4fe65-134">outputs</span></span> |<span data-ttu-id="4fe65-135">Hive etkinliği tarafından üretilen çıkış</span><span class="sxs-lookup"><span data-stu-id="4fe65-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="4fe65-136">Evet</span><span class="sxs-lookup"><span data-stu-id="4fe65-136">Yes</span></span> |
| <span data-ttu-id="4fe65-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4fe65-137">linkedServiceName</span></span> |<span data-ttu-id="4fe65-138">Veri fabrikasında bağlı hizmet olarak kayıtlı bir Hdınsight kümesine başvuru</span><span class="sxs-lookup"><span data-stu-id="4fe65-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="4fe65-139">Evet</span><span class="sxs-lookup"><span data-stu-id="4fe65-139">Yes</span></span> |
| <span data-ttu-id="4fe65-140">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4fe65-140">script</span></span> |<span data-ttu-id="4fe65-141">Hive betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="4fe65-141">Specify the Hive script inline</span></span> |<span data-ttu-id="4fe65-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="4fe65-142">No</span></span> |
| <span data-ttu-id="4fe65-143">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="4fe65-143">script path</span></span> |<span data-ttu-id="4fe65-144">Hive betiği bir Azure blob storage'da depolamak ve dosyanın yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="4fe65-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="4fe65-145">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4fe65-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="4fe65-146">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="4fe65-146">Both cannot be used together.</span></span> <span data-ttu-id="4fe65-147">Dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="4fe65-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="4fe65-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="4fe65-148">No</span></span> |
| <span data-ttu-id="4fe65-149">tanımlar</span><span class="sxs-lookup"><span data-stu-id="4fe65-149">defines</span></span> |<span data-ttu-id="4fe65-150">'Hiveconf' kullanarak Hive betiğini içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="4fe65-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="4fe65-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="4fe65-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="4fe65-152">Örnek</span><span class="sxs-lookup"><span data-stu-id="4fe65-152">Example</span></span>
<span data-ttu-id="4fe65-153">Şimdi, şirketiniz tarafından başlatılan oyunlar oynamak kullanıcılar tarafından harcanan süre istediğiniz analytics tanımlamak oyun günlükleri örneği göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="4fe65-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="4fe65-154">Aşağıdaki günlük virgül bir örnek oyun günlük olduğu (`,`) ayrılmış ve aşağıdaki alanları – Profileıd, SessionStart, süre, Srcıpaddress ve GameType içerir.</span><span class="sxs-lookup"><span data-stu-id="4fe65-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="4fe65-155">**Hive betiği** bu verileri işlemek için:</span><span class="sxs-lookup"><span data-stu-id="4fe65-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="4fe65-156">Bir Data Factory işlem hattı bu Hive betiğini çalıştırmak için aşağıdakileri yapmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="4fe65-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="4fe65-157">Kaydetmek için bağlı hizmet oluşturma [kendi Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya yapılandırma [isteğe bağlı Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="4fe65-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="4fe65-158">Şimdi bu bağlı hizmetin "HDInsightLinkedService" çağırın.</span><span class="sxs-lookup"><span data-stu-id="4fe65-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="4fe65-159">Oluşturma bir [bağlantılı hizmeti](data-factory-azure-blob-connector.md) verileri barındıran Azure Blob Depolama bağlantısını yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="4fe65-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="4fe65-160">Şimdi bu bağlı hizmetin "StorageLinkedService" çağırın</span><span class="sxs-lookup"><span data-stu-id="4fe65-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="4fe65-161">Oluşturma [veri kümeleri](data-factory-create-datasets.md) girdi ve çıktı verilerini işaret ediyor.</span><span class="sxs-lookup"><span data-stu-id="4fe65-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="4fe65-162">Girdi veri kümesi "HiveSampleIn" şimdi arayın ve çıkış veri kümesi "HiveSampleOut"</span><span class="sxs-lookup"><span data-stu-id="4fe65-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="4fe65-163">Kopya Azure Blob Depolama dosyası olarak Hive sorgusu #2. adımda yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="4fe65-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="4fe65-164">verileri barındırmak için depolama alanı bu sorgu dosyası barındırma farklı ise, ayrı bir Azure depolama bağlantılı hizmet oluşturun ve ona etkinliğin bakın.</span><span class="sxs-lookup"><span data-stu-id="4fe65-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="4fe65-165">Kullanım ** scriptPath ** sorgu dosyası yığın yolunu belirtmek için ve **scriptLinkedService** komut dosyasını içeren Azure depolama belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="4fe65-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4fe65-166">Kullanarak Hive betiği satır etkinlik tanımı içinde sağlayabilirsiniz **betik** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4fe65-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="4fe65-167">Biz bu yaklaşım, komut dosyası JSON belgesi gereksinimlerini kaçış içinde bulunan tüm özel karakterleri olarak önerilmez ve hata ayıklama sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="4fe65-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="4fe65-168">En iyi uygulama #4. adım izlemektir.</span><span class="sxs-lookup"><span data-stu-id="4fe65-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="4fe65-169">Hdınsighthive etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fe65-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="4fe65-170">Etkinlik işlemler / veri dönüşümler.</span><span class="sxs-lookup"><span data-stu-id="4fe65-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="4fe65-171">Ardışık Düzen dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4fe65-171">Deploy the pipeline.</span></span> <span data-ttu-id="4fe65-172">Bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="4fe65-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="4fe65-173">Veri Fabrikası izleme ve yönetim görünümlerini kullanarak işlem hattını izleme.</span><span class="sxs-lookup"><span data-stu-id="4fe65-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="4fe65-174">Bkz: [izleme ve Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="4fe65-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="4fe65-175">Bir Hive betiği parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="4fe65-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="4fe65-176">Bu örnekte, oyun günlükleri Azure Blob depolama alanına günlük alınan ve tarih ve saat ile bölümlenmiş bir klasörde depolanır.</span><span class="sxs-lookup"><span data-stu-id="4fe65-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="4fe65-177">Hive betiğini Parametreleştirme ve giriş klasörü konumunu çalışma zamanı sırasında dinamik olarak geçirmek ve ayrıca tarih ve saat ile bölümlenmiş bir çıktı oluşturmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4fe65-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="4fe65-178">Parametreli Hive betiğini kullanmak için aşağıdakileri yapın</span><span class="sxs-lookup"><span data-stu-id="4fe65-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="4fe65-179">Parametre tanımlayın **tanımlar**.</span><span class="sxs-lookup"><span data-stu-id="4fe65-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="4fe65-180">Parametresini kullanarak Hive betiği başvuran **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="4fe65-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="4fe65-181">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="4fe65-181">See Also</span></span>
* [<span data-ttu-id="4fe65-182">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="4fe65-183">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="4fe65-184">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="4fe65-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="4fe65-185">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="4fe65-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="4fe65-186">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="4fe65-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

