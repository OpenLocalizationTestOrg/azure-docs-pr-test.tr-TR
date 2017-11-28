---
title: "Pig etkinliği Azure Data Factory kullanarak veri dönüştürme | Microsoft Docs"
description: "Pig etkinlik bir Azure data factory'de bir üzerinde-isteğe bağlı/bilgisayarınızı kendi Hdınsight kümesinde Pig betikleri çalıştırmak için nasıl kullanabileceğinizi öğrenin."
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
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="19f18-103">Pig etkinliği Azure Data Factory kullanarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="19f18-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="19f18-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="19f18-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="19f18-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="19f18-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="19f18-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="19f18-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="19f18-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="19f18-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="19f18-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="19f18-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="19f18-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="19f18-114">Veri Fabrikası Hdınsight Pig etkinliğinde [ardışık düzen](data-factory-create-pipelines.md) üzerinde Pig sorguları yürüten [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="19f18-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="19f18-115">Bu makalede derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="19f18-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="19f18-116">Azure Data Factory yeniyseniz okuyun [Azure Data Factory'ye giriş](data-factory-introduction.md) ve öğretici: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="19f18-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="19f18-117">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="19f18-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="19f18-118">Sözdizimi ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="19f18-118">Syntax details</span></span>
| <span data-ttu-id="19f18-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="19f18-119">Property</span></span> | <span data-ttu-id="19f18-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="19f18-120">Description</span></span> | <span data-ttu-id="19f18-121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="19f18-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19f18-122">ad</span><span class="sxs-lookup"><span data-stu-id="19f18-122">name</span></span> |<span data-ttu-id="19f18-123">Etkinlik adı</span><span class="sxs-lookup"><span data-stu-id="19f18-123">Name of the activity</span></span> |<span data-ttu-id="19f18-124">Evet</span><span class="sxs-lookup"><span data-stu-id="19f18-124">Yes</span></span> |
| <span data-ttu-id="19f18-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="19f18-125">description</span></span> |<span data-ttu-id="19f18-126">Etkinlik hangi amaçla kullanıldığına açıklayan metin</span><span class="sxs-lookup"><span data-stu-id="19f18-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="19f18-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="19f18-127">No</span></span> |
| <span data-ttu-id="19f18-128">type</span><span class="sxs-lookup"><span data-stu-id="19f18-128">type</span></span> |<span data-ttu-id="19f18-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="19f18-129">HDinsightPig</span></span> |<span data-ttu-id="19f18-130">Evet</span><span class="sxs-lookup"><span data-stu-id="19f18-130">Yes</span></span> |
| <span data-ttu-id="19f18-131">Girişleri</span><span class="sxs-lookup"><span data-stu-id="19f18-131">inputs</span></span> |<span data-ttu-id="19f18-132">Pig etkinlik tarafından kullanılan bir veya daha fazla giriş</span><span class="sxs-lookup"><span data-stu-id="19f18-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="19f18-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="19f18-133">No</span></span> |
| <span data-ttu-id="19f18-134">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="19f18-134">outputs</span></span> |<span data-ttu-id="19f18-135">Pig etkinlik tarafından oluşturulan bir veya daha fazla çıkışları</span><span class="sxs-lookup"><span data-stu-id="19f18-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="19f18-136">Evet</span><span class="sxs-lookup"><span data-stu-id="19f18-136">Yes</span></span> |
| <span data-ttu-id="19f18-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="19f18-137">linkedServiceName</span></span> |<span data-ttu-id="19f18-138">Veri fabrikasında bağlı hizmet olarak kayıtlı bir Hdınsight kümesine başvuru</span><span class="sxs-lookup"><span data-stu-id="19f18-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="19f18-139">Evet</span><span class="sxs-lookup"><span data-stu-id="19f18-139">Yes</span></span> |
| <span data-ttu-id="19f18-140">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="19f18-140">script</span></span> |<span data-ttu-id="19f18-141">Pig betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="19f18-141">Specify the Pig script inline</span></span> |<span data-ttu-id="19f18-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="19f18-142">No</span></span> |
| <span data-ttu-id="19f18-143">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="19f18-143">script path</span></span> |<span data-ttu-id="19f18-144">Pig betiği bir Azure blob storage'da depolamak ve dosyanın yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="19f18-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="19f18-145">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="19f18-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="19f18-146">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="19f18-146">Both cannot be used together.</span></span> <span data-ttu-id="19f18-147">Dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="19f18-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="19f18-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="19f18-148">No</span></span> |
| <span data-ttu-id="19f18-149">tanımlar</span><span class="sxs-lookup"><span data-stu-id="19f18-149">defines</span></span> |<span data-ttu-id="19f18-150">Pig betiği içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="19f18-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="19f18-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="19f18-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="19f18-152">Örnek</span><span class="sxs-lookup"><span data-stu-id="19f18-152">Example</span></span>
<span data-ttu-id="19f18-153">Şimdi, şirketiniz tarafından başlatılan oyunlar oynamak oynatıcıları kullandığı zamanın istediğiniz analytics tanımlamak oyun günlükleri örneği göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="19f18-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="19f18-154">Aşağıdaki örnek oyun günlük bir virgülle (,) dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="19f18-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="19f18-155">Aşağıdaki alanları – Profileıd, SessionStart, süre, Srcıpaddress ve GameType içerir.</span><span class="sxs-lookup"><span data-stu-id="19f18-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="19f18-156">**Pig betiği** bu verileri işlemek için:</span><span class="sxs-lookup"><span data-stu-id="19f18-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="19f18-157">Bir Data Factory işlem hattı bu Pig betiği çalıştırmak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="19f18-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="19f18-158">Kaydetmek için bağlı hizmet oluşturma [kendi Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya yapılandırma [isteğe bağlı Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="19f18-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="19f18-159">Şimdi bu bağlı hizmetin çağrısı **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="19f18-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="19f18-160">Oluşturma bir [bağlantılı hizmeti](data-factory-azure-blob-connector.md) verileri barındıran Azure Blob Depolama bağlantısını yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="19f18-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="19f18-161">Şimdi bu bağlı hizmetin çağrısı **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="19f18-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="19f18-162">Oluşturma [veri kümeleri](data-factory-create-datasets.md) girdi ve çıktı verilerini işaret ediyor.</span><span class="sxs-lookup"><span data-stu-id="19f18-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="19f18-163">Şimdi girdi veri kümesi çağrısı **PigSampleIn** ve çıktı veri kümesi **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="19f18-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="19f18-164">Bir dosyayı Azure Blob Storage #2. adımda yapılandırılmış Pig sorgu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="19f18-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="19f18-165">Verileri barındıran Azure depolama birinden sorgu dosyası barındıran farklıysa, ayrı bir Azure depolama bağlantılı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19f18-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="19f18-166">Etkinlik yapılandırması bağlantılı hizmetteki bakın.</span><span class="sxs-lookup"><span data-stu-id="19f18-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="19f18-167">Kullanım ** scriptPath ** pig komut dosyasının yolunu belirtmek için ve **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="19f18-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="19f18-168">Pig betiği satır etkinlik tanımı içinde kullanarak da sağlayabilirsiniz **betik** özelliği.</span><span class="sxs-lookup"><span data-stu-id="19f18-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="19f18-169">Ancak, biz bu yaklaşım, tüm özel komut dosyası gereksinimlerini kaçış karakteri olarak önerilmez ve hata ayıklama sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="19f18-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="19f18-170">En iyi uygulama #4. adım izlemektir.</span><span class="sxs-lookup"><span data-stu-id="19f18-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="19f18-171">HDInsightPig etkinliği ile işlem hattı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="19f18-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="19f18-172">Bu etkinlik, Hdınsight kümesinde Pig betiği çalıştırarak giriş verilerini işler.</span><span class="sxs-lookup"><span data-stu-id="19f18-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="19f18-173">Ardışık Düzen dağıtın.</span><span class="sxs-lookup"><span data-stu-id="19f18-173">Deploy the pipeline.</span></span> <span data-ttu-id="19f18-174">Bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="19f18-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="19f18-175">Veri Fabrikası izleme ve yönetim görünümlerini kullanarak işlem hattını izleme.</span><span class="sxs-lookup"><span data-stu-id="19f18-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="19f18-176">Bkz: [izleme ve Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="19f18-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="19f18-177">Pig betiği parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="19f18-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="19f18-178">Aşağıdaki örneği göz önünde bulundurun: oyun günlükleri günlük Azure Blob depolama alanına alınan ve bölümlenmiş temel alınarak tarih ve saat bir klasörde depolanır.</span><span class="sxs-lookup"><span data-stu-id="19f18-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="19f18-179">Pig betiği Parametreleştirme ve giriş klasörü konumunu çalışma zamanı sırasında dinamik olarak geçirmek ve ayrıca tarih ve saat ile bölümlenmiş bir çıktı oluşturmak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="19f18-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="19f18-180">Parametreli Pig betiği kullanmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="19f18-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="19f18-181">Parametre tanımlayın **tanımlar**.</span><span class="sxs-lookup"><span data-stu-id="19f18-181">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="19f18-182">Pig betiği kullanarak parametreler başvuruda '**$parameterName**' aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="19f18-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="19f18-183">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="19f18-183">See Also</span></span>
* [<span data-ttu-id="19f18-184">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="19f18-185">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="19f18-186">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="19f18-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="19f18-187">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="19f18-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="19f18-188">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="19f18-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

