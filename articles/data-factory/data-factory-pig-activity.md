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
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="8cc7e-103">Pig etkinliği Azure Data Factory kullanarak veri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="8cc7e-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="8cc7e-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="8cc7e-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="8cc7e-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="8cc7e-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="8cc7e-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="8cc7e-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="8cc7e-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="8cc7e-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="8cc7e-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="8cc7e-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="8cc7e-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="8cc7e-114">Merhaba Data Factory Hdınsight Pig etkinliğinde [ardışık düzen](data-factory-create-pipelines.md) üzerinde Pig sorguları yürüten [kendi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya [isteğe bağlı](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8cc7e-115">Bu makale üzerinde hello derlemeler [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) makalesi, veri dönüştürme ve desteklenen hello dönüştürme etkinliklerinin genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="8cc7e-116">Yeni tooAzure Data Factory varsa okuyun [giriş tooAzure Data Factory](data-factory-introduction.md) ve öğretici hello: [ilk veri hattınızı yapı](data-factory-build-your-first-pipeline.md) bu makaleyi okumadan önce.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="8cc7e-117">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8cc7e-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="8cc7e-118">Sözdizimi ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="8cc7e-118">Syntax details</span></span>
| <span data-ttu-id="8cc7e-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="8cc7e-119">Property</span></span> | <span data-ttu-id="8cc7e-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cc7e-120">Description</span></span> | <span data-ttu-id="8cc7e-121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cc7e-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8cc7e-122">ad</span><span class="sxs-lookup"><span data-stu-id="8cc7e-122">name</span></span> |<span data-ttu-id="8cc7e-123">Merhaba etkinlik adı</span><span class="sxs-lookup"><span data-stu-id="8cc7e-123">Name of hello activity</span></span> |<span data-ttu-id="8cc7e-124">Evet</span><span class="sxs-lookup"><span data-stu-id="8cc7e-124">Yes</span></span> |
| <span data-ttu-id="8cc7e-125">açıklama</span><span class="sxs-lookup"><span data-stu-id="8cc7e-125">description</span></span> |<span data-ttu-id="8cc7e-126">Hangi hello etkinliği için kullanılan açıklayan metin</span><span class="sxs-lookup"><span data-stu-id="8cc7e-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="8cc7e-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cc7e-127">No</span></span> |
| <span data-ttu-id="8cc7e-128">type</span><span class="sxs-lookup"><span data-stu-id="8cc7e-128">type</span></span> |<span data-ttu-id="8cc7e-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="8cc7e-129">HDinsightPig</span></span> |<span data-ttu-id="8cc7e-130">Evet</span><span class="sxs-lookup"><span data-stu-id="8cc7e-130">Yes</span></span> |
| <span data-ttu-id="8cc7e-131">Girişleri</span><span class="sxs-lookup"><span data-stu-id="8cc7e-131">inputs</span></span> |<span data-ttu-id="8cc7e-132">Bir veya daha fazla girdi, Pig etkinlik hello tarafından kullanılan</span><span class="sxs-lookup"><span data-stu-id="8cc7e-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="8cc7e-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cc7e-133">No</span></span> |
| <span data-ttu-id="8cc7e-134">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="8cc7e-134">outputs</span></span> |<span data-ttu-id="8cc7e-135">Bir veya daha fazla çıkış Pig etkinlik hello tarafından üretilen</span><span class="sxs-lookup"><span data-stu-id="8cc7e-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="8cc7e-136">Evet</span><span class="sxs-lookup"><span data-stu-id="8cc7e-136">Yes</span></span> |
| <span data-ttu-id="8cc7e-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8cc7e-137">linkedServiceName</span></span> |<span data-ttu-id="8cc7e-138">Veri fabrikasında bağlı hizmet olarak kayıtlı toohello Hdınsight kümesi başvurusu</span><span class="sxs-lookup"><span data-stu-id="8cc7e-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="8cc7e-139">Evet</span><span class="sxs-lookup"><span data-stu-id="8cc7e-139">Yes</span></span> |
| <span data-ttu-id="8cc7e-140">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="8cc7e-140">script</span></span> |<span data-ttu-id="8cc7e-141">Merhaba Pig betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="8cc7e-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="8cc7e-142">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cc7e-142">No</span></span> |
| <span data-ttu-id="8cc7e-143">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="8cc7e-143">script path</span></span> |<span data-ttu-id="8cc7e-144">Bir Azure blob depolama alanına Hello Pig betiği depolar ve hello yol toohello dosyası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="8cc7e-145">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="8cc7e-146">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-146">Both cannot be used together.</span></span> <span data-ttu-id="8cc7e-147">Merhaba dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="8cc7e-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cc7e-148">No</span></span> |
| <span data-ttu-id="8cc7e-149">tanımlar</span><span class="sxs-lookup"><span data-stu-id="8cc7e-149">defines</span></span> |<span data-ttu-id="8cc7e-150">Pig betiği hello içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="8cc7e-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="8cc7e-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="8cc7e-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="8cc7e-152">Örnek</span><span class="sxs-lookup"><span data-stu-id="8cc7e-152">Example</span></span>
<span data-ttu-id="8cc7e-153">Şimdi göz önünde bulundurun oyun örneği, şirketiniz tarafından başlatılan oyunlar oynamak oyuncu tarafından tooidentify hello zamanın istediğiniz analytics günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="8cc7e-154">Aşağıdaki örnek oyun günlük hello bir virgülle (,) dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="8cc7e-155">Alanlar – Profileıd, SessionStart, süre, Srcıpaddress ve GameType aşağıdaki hello içerir.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="8cc7e-156">Merhaba **Pig betiği** tooprocess bu veriler:</span><span class="sxs-lookup"><span data-stu-id="8cc7e-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="8cc7e-157">Bu Pig komut dosyası, bir Data Factory işlem hattı tooexecute hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8cc7e-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="8cc7e-158">Bağlantılı hizmet tooregister oluşturma [kendi Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) veya yapılandırma [isteğe bağlı Hdınsight işlem kümesi](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="8cc7e-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="8cc7e-159">Şimdi bu bağlı hizmetin çağrısı **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="8cc7e-160">Oluşturma bir [bağlantılı hizmeti](data-factory-azure-blob-connector.md) hello verileri barındıran tooconfigure hello bağlantı tooAzure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="8cc7e-161">Şimdi bu bağlı hizmetin çağrısı **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="8cc7e-162">Oluşturma [veri kümeleri](data-factory-create-datasets.md) toohello giriş ve hello işaret eden çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="8cc7e-163">Şimdi hello girdi veri kümesi çağrısı **PigSampleIn** ve çıktı veri kümesi hello **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="8cc7e-164">Merhaba Pig sorgu dosyası hello Azure Blob Storage'nın #2. adımda yapılandırılmış kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="8cc7e-165">Merhaba hello verilerini barındıran Azure depolama hello sorgu dosyası barındıran hello bir farklıysa, ayrı bir Azure depolama bağlantılı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="8cc7e-166">Merhaba etkinlik yapılandırması bağlı toohello hizmetinde bakın.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="8cc7e-167">Kullanım ** scriptPath ** toospecify hello yolu toopig komut dosyası ve **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8cc7e-168">Hello kullanarak hello Pig betiği satır hello etkinlik tanımı içinde sağlayabilir **betik** özelliği.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="8cc7e-169">Ancak, bu yaklaşım hello komut dosyasındaki tüm özel karakterleri olarak kaçışlı toobe gerekir ve hata ayıklama sorunlara neden olabilir önermiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="8cc7e-170">Merhaba en iyi uygulama toofollow #4 adımdır.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="8cc7e-171">Merhaba ardışık düzen HDInsightPig etkinlik hello ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="8cc7e-172">Bu etkinlik, Hdınsight kümesinde Pig betiği çalıştırarak hello giriş verilerini işler.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="8cc7e-173">Merhaba ardışık düzen dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-173">Deploy hello pipeline.</span></span> <span data-ttu-id="8cc7e-174">Bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="8cc7e-175">Fabrika Hello izleme verilerini kullanarak hello ardışık düzen ve Yönetimi görünümlerini izleyin.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="8cc7e-176">Bkz: [izleme ve Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-pipelines.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="8cc7e-177">Pig betiği parametrelerini belirtme</span><span class="sxs-lookup"><span data-stu-id="8cc7e-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="8cc7e-178">Aşağıdaki örnek hello göz önünde bulundurun: oyun günlükleri günlük Azure Blob depolama alanına alınan ve bölümlenmiş temel alınarak tarih ve saat bir klasörde depolanır.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="8cc7e-179">Hello giriş klasörü konumunu çalışma zamanı sırasında dinamik olarak geçirmek istediğiniz tooparameterize hello Pig betiği ve ayrıca hello çıkış tarihi ve saati ile bölümlenmiş oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="8cc7e-180">Pig betiği toouse parametreli, aşağıdaki hello yapın:</span><span class="sxs-lookup"><span data-stu-id="8cc7e-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="8cc7e-181">Merhaba parametrelerinde tanımlamak **tanımlar**.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="8cc7e-182">Hello Pig betiği'da, kullanarak toohello parametrelerini başvuran '**$parameterName**' hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="8cc7e-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="8cc7e-183">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8cc7e-183">See Also</span></span>
* [<span data-ttu-id="8cc7e-184">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="8cc7e-185">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="8cc7e-186">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="8cc7e-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="8cc7e-187">Spark programlarını çağırma</span><span class="sxs-lookup"><span data-stu-id="8cc7e-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="8cc7e-188">R betiklerini çağırma</span><span class="sxs-lookup"><span data-stu-id="8cc7e-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

