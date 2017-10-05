---
title: "Azure Data Factory - JSON betik oluşturma başvurusu | Microsoft Docs"
description: "Data Factory varlıkları için JSON şemaları sağlar."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="21f3d-103">Azure Data Factory - JSON betik oluşturma başvurusu</span><span class="sxs-lookup"><span data-stu-id="21f3d-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="21f3d-104">Bu makalede, Azure Data Factory varlıkları (ardışık düzen, etkinlik, veri kümesi ve bağlantılı hizmet) tanımlamak için JSON şemaları ve örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="21f3d-105">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="21f3d-105">Pipeline</span></span> 
<span data-ttu-id="21f3d-106">Ardışık düzen tanımı için üst düzey yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="21f3d-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="21f3d-107">Aşağıdaki tabloda özellikleri JSON tanımını ardışık düzen içinde açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="21f3d-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="21f3d-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-108">Property</span></span> | <span data-ttu-id="21f3d-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-109">Description</span></span> | <span data-ttu-id="21f3d-110">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="21f3d-111">ad</span><span class="sxs-lookup"><span data-stu-id="21f3d-111">name</span></span> | <span data-ttu-id="21f3d-112">Ardışık Düzen adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-112">Name of the pipeline.</span></span> <span data-ttu-id="21f3d-113">Eylemi temsil eden bir ad belirtin etkinlik veya ardışık düzen yapmak için yapılandırılır</span><span class="sxs-lookup"><span data-stu-id="21f3d-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="21f3d-114">En fazla karakter sayısı: 260</span><span class="sxs-lookup"><span data-stu-id="21f3d-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="21f3d-115">Bir harf sayı veya alt çizgi (_) ile başlamalıdır</span><span class="sxs-lookup"><span data-stu-id="21f3d-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="21f3d-116">Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="21f3d-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="21f3d-117">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-117">Yes</span></span> |
| <span data-ttu-id="21f3d-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-118">description</span></span> |<span data-ttu-id="21f3d-119">Hangi etkinlik veya ardışık düzen açıklayan metin için kullanılır</span><span class="sxs-lookup"><span data-stu-id="21f3d-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="21f3d-120">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-120">No</span></span> |
| <span data-ttu-id="21f3d-121">Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="21f3d-121">activities</span></span> | <span data-ttu-id="21f3d-122">Etkinliklerin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-122">Contains a list of activities.</span></span> | <span data-ttu-id="21f3d-123">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-123">Yes</span></span> |
| <span data-ttu-id="21f3d-124">start</span><span class="sxs-lookup"><span data-stu-id="21f3d-124">start</span></span> |<span data-ttu-id="21f3d-125">Ardışık düzeni için başlangıç tarihi / saati.</span><span class="sxs-lookup"><span data-stu-id="21f3d-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="21f3d-126">Olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="21f3d-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="21f3d-127">Örneğin: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="21f3d-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="21f3d-128">Yerel saat örneğin tahmini süre belirlemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="21f3d-129">Örnek aşağıda verilmiştir: `2016-02-27T06:00:00**-05:00`, 6'da tahmini olduğu</span><span class="sxs-lookup"><span data-stu-id="21f3d-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="21f3d-130">Başlangıç ve bitiş özellikleri birlikte ardışık düzen etkin süresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="21f3d-131">Çıktı dilimler yalnızca ile etkin bu dönemde üretilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="21f3d-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-132">No</span></span><br/><br/><span data-ttu-id="21f3d-133">End özelliği için bir değer belirtirseniz, başlangıç özelliği için değer belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="21f3d-134">Başlangıç ve bitiş zamanlarını hem de bir işlem hattı oluşturmak için boş olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="21f3d-135">Çalıştırmak ardışık düzeni için etkin bir süre ayarlamak için her iki değer belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="21f3d-136">Başlangıç ve bitiş zamanlarını belirtmezseniz, bir işlem hattı oluştururken, bunları daha sonra Set-AzureRmDataFactoryPipelineActivePeriod cmdlet'ini kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="21f3d-137">Bitiş</span><span class="sxs-lookup"><span data-stu-id="21f3d-137">end</span></span> |<span data-ttu-id="21f3d-138">Ardışık düzeni için bitiş tarihi / saati.</span><span class="sxs-lookup"><span data-stu-id="21f3d-138">End date-time for the pipeline.</span></span> <span data-ttu-id="21f3d-139">Belirtilen ISO biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-139">If specified must be in ISO format.</span></span> <span data-ttu-id="21f3d-140">Örneğin: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="21f3d-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="21f3d-141">Yerel saat örneğin tahmini süre belirlemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="21f3d-142">Örnek aşağıda verilmiştir: `2016-02-27T06:00:00**-05:00`, 6'da tahmini olduğu</span><span class="sxs-lookup"><span data-stu-id="21f3d-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="21f3d-143">İşlem hattını süresiz olarak çalışacak şekilde 9999-09-09 end özelliği için değer olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="21f3d-144">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-144">No</span></span> <br/><br/><span data-ttu-id="21f3d-145">Başlangıç özellik için bir değer belirtirseniz, son özelliği için değer belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="21f3d-146">İçin notlarına bakın **Başlat** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="21f3d-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="21f3d-147">isPaused</span></span> |<span data-ttu-id="21f3d-148">Ardışık Düzen true olarak ayarlandığında çalışmazsa.</span><span class="sxs-lookup"><span data-stu-id="21f3d-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="21f3d-149">Varsayılan değer = false.</span><span class="sxs-lookup"><span data-stu-id="21f3d-149">Default value = false.</span></span> <span data-ttu-id="21f3d-150">Bu özelliği etkinleştirmek veya devre dışı bırakmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="21f3d-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-151">No</span></span> |
| <span data-ttu-id="21f3d-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="21f3d-152">pipelineMode</span></span> |<span data-ttu-id="21f3d-153">Zamanlama için yöntem ardışık düzeni için çalışır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="21f3d-154">İzin verilen değerler: (varsayılan), zamanlanmış kez.</span><span class="sxs-lookup"><span data-stu-id="21f3d-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="21f3d-155">'Zamanlanmış' ardışık düzen belirtilen süre aralığında etkin süresinin (başlangıç ve bitiş saati) göre çalıştırıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="21f3d-156">'Kez' ardışık düzen yalnızca bir kez çalıştırıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="21f3d-157">Oluşturulduktan sonra kez ardışık düzen şu anda değiştiren/güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="21f3d-158">Bkz: [Onetime ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) kez ayar hakkındaki ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="21f3d-159">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-159">No</span></span> |
| <span data-ttu-id="21f3d-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="21f3d-160">expirationTime</span></span> |<span data-ttu-id="21f3d-161">Kendisi için ardışık düzeni geçerli olduğunu ve sağlanan kalacağı oluşturulduktan sonra süre.</span><span class="sxs-lookup"><span data-stu-id="21f3d-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="21f3d-162">Tüm etkin başarısız oldu, yok veya sona erme zamanı ulaştığında çalıştığında, ardışık düzen otomatik olarak silinmesi durumunda.</span><span class="sxs-lookup"><span data-stu-id="21f3d-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="21f3d-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="21f3d-164">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="21f3d-164">Activity</span></span> 
<span data-ttu-id="21f3d-165">Ardışık düzen tanımı (etkinlikleri öğesi) içinde bir etkinlik için üst düzey yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="21f3d-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="21f3d-166">Tablo Özellikleri JSON tanımını etkinlik içinde açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="21f3d-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="21f3d-167">Etiket</span><span class="sxs-lookup"><span data-stu-id="21f3d-167">Tag</span></span> | <span data-ttu-id="21f3d-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-168">Description</span></span> | <span data-ttu-id="21f3d-169">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-170">ad</span><span class="sxs-lookup"><span data-stu-id="21f3d-170">name</span></span> |<span data-ttu-id="21f3d-171">Etkinlik adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-171">Name of the activity.</span></span> <span data-ttu-id="21f3d-172">Eylemi temsil eden bir ad belirtin, etkinlik yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="21f3d-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="21f3d-173">En fazla karakter sayısı: 260</span><span class="sxs-lookup"><span data-stu-id="21f3d-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="21f3d-174">Bir harf sayı veya alt çizgi (_) ile başlamalıdır</span><span class="sxs-lookup"><span data-stu-id="21f3d-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="21f3d-175">Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="21f3d-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="21f3d-176">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-176">Yes</span></span> |
| <span data-ttu-id="21f3d-177">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-177">description</span></span> |<span data-ttu-id="21f3d-178">Etkinlik hangi amaçla kullanıldığına açıklayan metin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="21f3d-179">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-179">Yes</span></span> |
| <span data-ttu-id="21f3d-180">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-180">type</span></span> |<span data-ttu-id="21f3d-181">Etkinlik türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-181">Specifies the type of the activity.</span></span> <span data-ttu-id="21f3d-182">Bkz: [veri DEPOLARINA](#data-stores) ve [veri dönüştürme etkinlikleri](#data-transformation-activities) bölümleri etkinlikler farklı türde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="21f3d-183">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-183">Yes</span></span> |
| <span data-ttu-id="21f3d-184">Girişleri</span><span class="sxs-lookup"><span data-stu-id="21f3d-184">inputs</span></span> |<span data-ttu-id="21f3d-185">Etkinlik tarafından kullanılan giriş tabloları</span><span class="sxs-lookup"><span data-stu-id="21f3d-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="21f3d-186">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-186">Yes</span></span> |
| <span data-ttu-id="21f3d-187">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="21f3d-187">outputs</span></span> |<span data-ttu-id="21f3d-188">Etkinlik tarafından kullanılan çıkış tabloları.</span><span class="sxs-lookup"><span data-stu-id="21f3d-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="21f3d-189">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-189">Yes</span></span> |
| <span data-ttu-id="21f3d-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="21f3d-190">linkedServiceName</span></span> |<span data-ttu-id="21f3d-191">Etkinlik tarafından kullanılan bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="21f3d-192">Bir etkinlik için gerekli hesaplama ortamı bağlantılar bağlantılı hizmeti belirtin gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="21f3d-193">Hdınsight etkinlikleri, Azure Machine Learning etkinlikleri ve saklı yordam etkinliği için Evet.</span><span class="sxs-lookup"><span data-stu-id="21f3d-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="21f3d-194">Diğer tüm kullanıcılar için Hayır'ı</span><span class="sxs-lookup"><span data-stu-id="21f3d-194">No for all others</span></span> |
| <span data-ttu-id="21f3d-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="21f3d-195">typeProperties</span></span> |<span data-ttu-id="21f3d-196">Özellikler typeProperties bölümünde etkinlik türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="21f3d-197">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-197">No</span></span> |
| <span data-ttu-id="21f3d-198">İlke</span><span class="sxs-lookup"><span data-stu-id="21f3d-198">policy</span></span> |<span data-ttu-id="21f3d-199">Etkinlik çalışma zamanı davranışını etkileyen ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="21f3d-200">Belirtilmezse, varsayılan ilkeler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="21f3d-201">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-201">No</span></span> |
| <span data-ttu-id="21f3d-202">Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="21f3d-202">scheduler</span></span> |<span data-ttu-id="21f3d-203">"Zamanlayıcı" özelliği, istenen etkinliği için zamanlama tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="21f3d-204">Onun alt Listedekilerin aynıdır [dataset kullanılabilirliği özelliğinde](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="21f3d-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="21f3d-205">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="21f3d-206">İlkeler</span><span class="sxs-lookup"><span data-stu-id="21f3d-206">Policies</span></span>
<span data-ttu-id="21f3d-207">İlkeler, özellikle bir tablonun dilim işlendiğinde bir etkinlik çalışma zamanı davranışını etkiler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="21f3d-208">Aşağıdaki tabloda ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-208">The following table provides the details.</span></span>

| <span data-ttu-id="21f3d-209">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-209">Property</span></span> | <span data-ttu-id="21f3d-210">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-210">Permitted values</span></span> | <span data-ttu-id="21f3d-211">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="21f3d-211">Default Value</span></span> | <span data-ttu-id="21f3d-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-213">Eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="21f3d-213">concurrency</span></span> |<span data-ttu-id="21f3d-214">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="21f3d-214">Integer</span></span> <br/><br/><span data-ttu-id="21f3d-215">En yüksek değeri: 10</span><span class="sxs-lookup"><span data-stu-id="21f3d-215">Max value: 10</span></span> |<span data-ttu-id="21f3d-216">1</span><span class="sxs-lookup"><span data-stu-id="21f3d-216">1</span></span> |<span data-ttu-id="21f3d-217">Etkinliğin eşzamanlı yürütmeleri sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="21f3d-218">Üzerinde farklı dilimler oluşabilir paralel etkinlik yürütmeleri sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="21f3d-219">Örneğin, bir etkinlik geçtikleri gerekiyorsa bir büyük daha büyük bir eşzamanlılık değer sahip kullanılabilir veri kümesi, veri işleme hızı artar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="21f3d-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="21f3d-220">executionPriorityOrder</span></span> |<span data-ttu-id="21f3d-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="21f3d-221">NewestFirst</span></span><br/><br/><span data-ttu-id="21f3d-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="21f3d-222">OldestFirst</span></span> |<span data-ttu-id="21f3d-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="21f3d-223">OldestFirst</span></span> |<span data-ttu-id="21f3d-224">İşlenen veri dilimleri sıralama belirler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="21f3d-225">Örneğin, varsa (bir oluşmasını 4 pm adresindeki ve 17: 00 saatleri sırasında başka bir) 2 böler ve hem de yürütme olması.</span><span class="sxs-lookup"><span data-stu-id="21f3d-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="21f3d-226">ExecutionPriorityOrder NewestFirst olacak şekilde ayarlarsanız, 17: 00 saatleri sırasında dilim önce işlenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="21f3d-227">ExecutionPriorityORder OldestFIrst olacak şekilde ayarlarsanız, benzer şekilde ardından 4 PM adresindeki dilim işlenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="21f3d-228">Yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="21f3d-228">retry</span></span> |<span data-ttu-id="21f3d-229">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="21f3d-229">Integer</span></span><br/><br/><span data-ttu-id="21f3d-230">En büyük değer 10 olabilir</span><span class="sxs-lookup"><span data-stu-id="21f3d-230">Max value can be 10</span></span> |<span data-ttu-id="21f3d-231">0</span><span class="sxs-lookup"><span data-stu-id="21f3d-231">0</span></span> |<span data-ttu-id="21f3d-232">Veri işleme ve dilim için hata olarak işaretlenmiş önce yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="21f3d-233">Etkinlik yürütme veri dilimi için belirtilen yeniden deneme sayısı kadar yeniden denenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="21f3d-234">Yeniden deneme mümkün olan en kısa sürede hatasından sonra yapılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="21f3d-235">Zaman aşımı</span><span class="sxs-lookup"><span data-stu-id="21f3d-235">timeout</span></span> |<span data-ttu-id="21f3d-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-236">TimeSpan</span></span> |<span data-ttu-id="21f3d-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="21f3d-237">00:00:00</span></span> |<span data-ttu-id="21f3d-238">Etkinlik için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-238">Timeout for the activity.</span></span> <span data-ttu-id="21f3d-239">Örnek: 00:10: (zaman aşımı 10 dakika anlamına gelir) 00</span><span class="sxs-lookup"><span data-stu-id="21f3d-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="21f3d-240">Bir değer belirtilmemiş ya da 0'dır, zaman aşımını sonsuz olur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="21f3d-241">Dilim üzerinde veri işleme süresi zaman aşımı değerini aşarsa, iptal edilir ve sistem işlemeyi yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="21f3d-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="21f3d-242">Yeniden deneme sayısı yeniden deneme özelliğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="21f3d-243">Zaman aşımı oluştuğunda durumu süresi sona erdi için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="21f3d-244">gecikme</span><span class="sxs-lookup"><span data-stu-id="21f3d-244">delay</span></span> |<span data-ttu-id="21f3d-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-245">TimeSpan</span></span> |<span data-ttu-id="21f3d-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="21f3d-246">00:00:00</span></span> |<span data-ttu-id="21f3d-247">Veri işleme dilim başlatır gecikme belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="21f3d-248">Beklenen yürütme süresi gecikme tamamlandıktan sonra bir veri dilimi için etkinlik yürütülmesini başlatılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="21f3d-249">Örnek: 00:10: (10 dakika gecikme anlamına gelir) 00</span><span class="sxs-lookup"><span data-stu-id="21f3d-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="21f3d-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="21f3d-250">longRetry</span></span> |<span data-ttu-id="21f3d-251">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="21f3d-251">Integer</span></span><br/><br/><span data-ttu-id="21f3d-252">En yüksek değeri: 10</span><span class="sxs-lookup"><span data-stu-id="21f3d-252">Max value: 10</span></span> |<span data-ttu-id="21f3d-253">1</span><span class="sxs-lookup"><span data-stu-id="21f3d-253">1</span></span> |<span data-ttu-id="21f3d-254">Dilim yürütme başarısız olmadan önce uzun yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="21f3d-255">longRetry girişimleri tarafından longRetryInterval aralarına aralık eklenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="21f3d-256">Yeniden deneme girişimleri arasındaki süre belirtmeniz gerekiyorsa, bu nedenle longRetry kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="21f3d-257">Yeniden deneme ve longRetry belirtilirse, her bir longRetry denemesi denemeleri içerir ve en fazla deneme sayısını yeniden deneme * longRetry.</span><span class="sxs-lookup"><span data-stu-id="21f3d-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="21f3d-258">Örneğin, biz etkinlik ilkesinde aşağıdaki ayarları varsa:</span><span class="sxs-lookup"><span data-stu-id="21f3d-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="21f3d-259">Yeniden deneme: 3</span><span class="sxs-lookup"><span data-stu-id="21f3d-259">Retry: 3</span></span><br/><span data-ttu-id="21f3d-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="21f3d-260">longRetry: 2</span></span><br/><span data-ttu-id="21f3d-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="21f3d-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="21f3d-262">Yürütmek için yalnızca bir dilim olduğu varsayılır (Durum Bekliyor) ve Etkinlik yürütme her zaman başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="21f3d-263">Başlangıçta 3 ardışık yürütme deneme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="21f3d-264">Her girişiminden sonra Yeniden Dene'yi dilim durum olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="21f3d-265">İlk 3 deneme üzerinden sonra dilim durum LongRetry olur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="21f3d-266">Bir saat sonra (diğer bir deyişle, longRetryInteval'ın değeri), 3 ardışık yürütme deneme başka bir dizi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="21f3d-267">Bundan sonra dilim durumu başarısız ve daha fazla yeniden deneme yok denenmesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="21f3d-268">Bu nedenle genel 6 deneme yapıldı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="21f3d-269">Hiçbir yürütme başarılı olursa, dilim durum hazır olur ve daha fazla yeniden deneme yok çalıştı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="21f3d-270">longRetry, belirleyici olmayan zamanlarda bağımlı veri ulaştığında veya genel ortamında hangi veri işleme gerçekleşir altında anormal olduğu durumlarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="21f3d-271">Böyle durumlarda, yeniden deneme birbiri ardından yardımcı yapmak ve sonra bir aralık böylece istenen çıkış sonuçlarında zaman.</span><span class="sxs-lookup"><span data-stu-id="21f3d-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="21f3d-272">Uyarı: longRetry veya longRetryInterval yüksek değerleri ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="21f3d-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="21f3d-273">Genellikle, daha yüksek değerleri sistemle ilgili diğer sorunlar kapsıyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="21f3d-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="21f3d-274">longRetryInterval</span></span> |<span data-ttu-id="21f3d-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-275">TimeSpan</span></span> |<span data-ttu-id="21f3d-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="21f3d-276">00:00:00</span></span> |<span data-ttu-id="21f3d-277">Uzun yeniden deneme girişimleri arasında gecikme</span><span class="sxs-lookup"><span data-stu-id="21f3d-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="21f3d-278">typeProperties bölümü</span><span class="sxs-lookup"><span data-stu-id="21f3d-278">typeProperties section</span></span>
<span data-ttu-id="21f3d-279">Her etkinlik için farklı typeProperties bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="21f3d-280">Dönüştürme etkinlikleri yalnızca türü özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="21f3d-281">Bkz: [veri dönüştürme etkinlikleri](#data-transformation-activities) ardışık düzeninde dönüştürme etkinlikleri tanımlayan JSON örnekleri için bu makalenin bölümünde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="21f3d-282">**Kopya etkinliği** typeProperties bölümünde iki alt bölümleri vardır: **kaynak** ve **havuz**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="21f3d-283">Bkz: [veri DEPOLARINA](#data-stores) veri kullanmayı gösteren JSON örnekleri bir kaynak ve/veya havuz depolamak için bu makaledeki bölüm.</span><span class="sxs-lookup"><span data-stu-id="21f3d-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="21f3d-284">Örnek kopyalama işlem hattı</span><span class="sxs-lookup"><span data-stu-id="21f3d-284">Sample copy pipeline</span></span>
<span data-ttu-id="21f3d-285">Aşağıdaki örnek ardışık düzeninde türünde bir etkinlik olduğundan **kopya** içinde **etkinlikleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="21f3d-286">Bu örnekte [kopyalama etkinliğini](data-factory-data-movement-activities.md) verileri Azure Blob depolama alanından Azure SQL veritabanına kopyalar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="21f3d-287">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-287">Note the following points:</span></span>

* <span data-ttu-id="21f3d-288">Etkinlikler bölümünde, **türü** **Copy** olarak ayarlanmış yalnızca bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="21f3d-289">Etkinlik girdisi **InputDataset** olarak, etkinlik çıktısı ise **OutputDataset** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="21f3d-290">**typeProperties** bölümünde **BlobSource** kaynak türü, **SqlSink** de havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="21f3d-291">Bkz: [veri DEPOLARINA](#data-stores) veri kullanmayı gösteren JSON örnekleri bir kaynak ve/veya havuz depolamak için bu makaledeki bölüm.</span><span class="sxs-lookup"><span data-stu-id="21f3d-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="21f3d-292">Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: veri kopyalama Blob depolama alanından SQL veritabanına](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="21f3d-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="21f3d-293">Örnek dönüşüm işlem hattı</span><span class="sxs-lookup"><span data-stu-id="21f3d-293">Sample transformation pipeline</span></span>
<span data-ttu-id="21f3d-294">Aşağıdaki örnek ardışık düzeninde türünde bir etkinlik olduğundan **Hdınsighthive** içinde **etkinlikleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="21f3d-295">Bu örnekte [Hdınsight Hive etkinliği](data-factory-hive-activity.md) Azure Hdınsight Hadoop kümesindeki Hive betiği çalıştırılarak verileri Azure Blob depolama biriminden dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="21f3d-296">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-296">Note the following points:</span></span> 

* <span data-ttu-id="21f3d-297">Etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** ayarlanır **Hdınsighthive**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="21f3d-298">**partitionweblogs.hql** Hive betik dosyası Azure depolama hesabında (scriptLinkedService tarafından belirtilen **AzureStorageLinkedService** adıyla) ve **adfgetstarted** kapsayıcısındaki **betik** klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="21f3d-299">**Tanımlar** bölümü hive betiğine Hive yapılandırma değerleri olarak geçirilir çalışma zamanı ayarlarını belirtmek için kullanılır (örneğin `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="21f3d-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="21f3d-300">Bkz: [veri dönüştürme etkinlikleri](#data-transformation-activities) ardışık düzeninde dönüştürme etkinlikleri tanımlayan JSON örnekleri için bu makalenin bölümünde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="21f3d-301">Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Hadoop kümesi kullanarak verileri işlemek için ilk işlem hattınızı oluşturma](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="21f3d-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="21f3d-302">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-302">Linked service</span></span>
<span data-ttu-id="21f3d-303">Bağlantılı hizmet tanımı için üst düzey yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="21f3d-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="21f3d-304">Tablo Özellikleri JSON tanımını etkinlik içinde açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="21f3d-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="21f3d-305">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-305">Property</span></span> | <span data-ttu-id="21f3d-306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-306">Description</span></span> | <span data-ttu-id="21f3d-307">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="21f3d-308">ad</span><span class="sxs-lookup"><span data-stu-id="21f3d-308">name</span></span> | <span data-ttu-id="21f3d-309">Bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-309">Name of the linked service.</span></span> | <span data-ttu-id="21f3d-310">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-310">Yes</span></span> | 
| <span data-ttu-id="21f3d-311">özellikleri - türü</span><span class="sxs-lookup"><span data-stu-id="21f3d-311">properties - type</span></span> | <span data-ttu-id="21f3d-312">Bağlantılı hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-312">Type of the linked service.</span></span> <span data-ttu-id="21f3d-313">Örneğin: Azure Storage, Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="21f3d-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="21f3d-314">typeProperties</span></span> | <span data-ttu-id="21f3d-315">TypeProperties bölüm için her bir veri deposu farklı veya ortam işlem öğesine sahip.</span><span class="sxs-lookup"><span data-stu-id="21f3d-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="21f3d-316">Bkz: [veri depoları](#datastores) bağlı hizmetler tüm verileri depolamak için bölüm ve [ortamları işlem](#compute-environments) için tüm işlem bağlı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="21f3d-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="21f3d-317">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-317">Dataset</span></span> 
<span data-ttu-id="21f3d-318">Azure Data Factory kümesinde aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="21f3d-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="21f3d-319">Aşağıdaki tabloda yukarıdaki JSON özelliklerinde açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="21f3d-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="21f3d-320">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-320">Property</span></span> | <span data-ttu-id="21f3d-321">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-321">Description</span></span> | <span data-ttu-id="21f3d-322">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-322">Required</span></span> | <span data-ttu-id="21f3d-323">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="21f3d-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-324">ad</span><span class="sxs-lookup"><span data-stu-id="21f3d-324">name</span></span> | <span data-ttu-id="21f3d-325">Veri kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-325">Name of the dataset.</span></span> <span data-ttu-id="21f3d-326">Bkz: [Azure Data Factory - adlandırma kuralları](data-factory-naming-rules.md) adlandırma kuralları.</span><span class="sxs-lookup"><span data-stu-id="21f3d-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="21f3d-327">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-327">Yes</span></span> |<span data-ttu-id="21f3d-328">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-328">NA</span></span> |
| <span data-ttu-id="21f3d-329">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-329">type</span></span> | <span data-ttu-id="21f3d-330">Veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-330">Type of the dataset.</span></span> <span data-ttu-id="21f3d-331">Azure Data Factory ile desteklenen türlerden biri belirtin (örneğin: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="21f3d-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="21f3d-332">Bkz: [veri DEPOLARINA](#data-stores) tüm veri depoları ve veri fabrikası tarafından desteklenen veri türleri için bölüm.</span><span class="sxs-lookup"><span data-stu-id="21f3d-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="21f3d-333">yapısı</span><span class="sxs-lookup"><span data-stu-id="21f3d-333">structure</span></span> | <span data-ttu-id="21f3d-334">Veri kümesi şemasını.</span><span class="sxs-lookup"><span data-stu-id="21f3d-334">Schema of the dataset.</span></span> <span data-ttu-id="21f3d-335">Bu sütun, türleri, vb. içerir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="21f3d-336">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-336">No</span></span> |<span data-ttu-id="21f3d-337">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-337">NA</span></span> |
| <span data-ttu-id="21f3d-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="21f3d-338">typeProperties</span></span> | <span data-ttu-id="21f3d-339">Seçili türüne karşılık gelen özellikler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="21f3d-340">Bkz: [veri DEPOLARINA](#data-stores) desteklenen türlerini ve bunların özelliklerini bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="21f3d-341">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-341">Yes</span></span> |<span data-ttu-id="21f3d-342">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-342">NA</span></span> |
| <span data-ttu-id="21f3d-343">external</span><span class="sxs-lookup"><span data-stu-id="21f3d-343">external</span></span> | <span data-ttu-id="21f3d-344">Bir veri kümesi açıkça data factory işlem hattı tarafından veya üretilen olup olmadığını belirlemek için mantıksal bayrak.</span><span class="sxs-lookup"><span data-stu-id="21f3d-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="21f3d-345">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-345">No</span></span> |<span data-ttu-id="21f3d-346">False</span><span class="sxs-lookup"><span data-stu-id="21f3d-346">false</span></span> |
| <span data-ttu-id="21f3d-347">availability</span><span class="sxs-lookup"><span data-stu-id="21f3d-347">availability</span></span> | <span data-ttu-id="21f3d-348">İşleme penceresi veya veri kümesi üretim dilimleme modelini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="21f3d-349">Model dilimleme veri kümesi hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="21f3d-350">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-350">Yes</span></span> |<span data-ttu-id="21f3d-351">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-351">NA</span></span> |
| <span data-ttu-id="21f3d-352">İlke</span><span class="sxs-lookup"><span data-stu-id="21f3d-352">policy</span></span> |<span data-ttu-id="21f3d-353">Ölçüt ya da veri kümesi dilimler karşılamanız gerekmektedir koşulu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="21f3d-354">Ayrıntılar için bkz [Dataset İlkesi](#Policy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="21f3d-355">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-355">No</span></span> |<span data-ttu-id="21f3d-356">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-356">NA</span></span> |

<span data-ttu-id="21f3d-357">Her sütunda **yapısı** bölüm, aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="21f3d-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="21f3d-358">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-358">Property</span></span> | <span data-ttu-id="21f3d-359">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-359">Description</span></span> | <span data-ttu-id="21f3d-360">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-361">ad</span><span class="sxs-lookup"><span data-stu-id="21f3d-361">name</span></span> |<span data-ttu-id="21f3d-362">Sütunun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-362">Name of the column.</span></span> |<span data-ttu-id="21f3d-363">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-363">Yes</span></span> |
| <span data-ttu-id="21f3d-364">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-364">type</span></span> |<span data-ttu-id="21f3d-365">Sütunun veri türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-365">Data type of the column.</span></span>  |<span data-ttu-id="21f3d-366">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-366">No</span></span> |
| <span data-ttu-id="21f3d-367">Kültür</span><span class="sxs-lookup"><span data-stu-id="21f3d-367">culture</span></span> |<span data-ttu-id="21f3d-368">.NET tabanlı türü belirtilir ve .NET türü olduğunda kullanılacak kültürü `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="21f3d-369">Varsayılan değer `en-us`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-369">Default is `en-us`.</span></span> |<span data-ttu-id="21f3d-370">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-370">No</span></span> |
| <span data-ttu-id="21f3d-371">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-371">format</span></span> |<span data-ttu-id="21f3d-372">Biçim türü belirtilir ve .NET türü olduğunda kullanılacak dize `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="21f3d-373">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-373">No</span></span> |

<span data-ttu-id="21f3d-374">Aşağıdaki örnekte, üç sütun kümesi sahip `slicetimestamp`, `projectname`, ve `pageviews` ve bunlar türü: dize, dize ve ondalık sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="21f3d-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="21f3d-375">Aşağıdaki tabloda, kullanabileceğiniz özellikleri açıklanmaktadır **kullanılabilirlik** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="21f3d-376">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-376">Property</span></span> | <span data-ttu-id="21f3d-377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-377">Description</span></span> | <span data-ttu-id="21f3d-378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-378">Required</span></span> | <span data-ttu-id="21f3d-379">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="21f3d-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-380">Sıklık</span><span class="sxs-lookup"><span data-stu-id="21f3d-380">frequency</span></span> |<span data-ttu-id="21f3d-381">Veri kümesi dilim üretim için zaman birimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="21f3d-382"><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay</span><span class="sxs-lookup"><span data-stu-id="21f3d-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="21f3d-383">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-383">Yes</span></span> |<span data-ttu-id="21f3d-384">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-384">NA</span></span> |
| <span data-ttu-id="21f3d-385">aralığı</span><span class="sxs-lookup"><span data-stu-id="21f3d-385">interval</span></span> |<span data-ttu-id="21f3d-386">Sıklığı çarpanı belirtir</span><span class="sxs-lookup"><span data-stu-id="21f3d-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="21f3d-387">"X sıklığı aralığını" ne sıklıkta dilim üretilen belirler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="21f3d-388">Saatlik olarak başka bir dilimlenebilir dataset gerekiyorsa, ayarladığınız <b>sıklığı</b> için <b>saat</b>, ve <b>aralığı</b> için <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="21f3d-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="21f3d-389"><b>Not</b>: sıklığını dakika belirtirseniz, aralık en az 15'e ayarlayın öneririz</span><span class="sxs-lookup"><span data-stu-id="21f3d-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="21f3d-390">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-390">Yes</span></span> |<span data-ttu-id="21f3d-391">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-391">NA</span></span> |
| <span data-ttu-id="21f3d-392">stili</span><span class="sxs-lookup"><span data-stu-id="21f3d-392">style</span></span> |<span data-ttu-id="21f3d-393">Dilim aralığı başlangıç/bitiş üretilen olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="21f3d-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="21f3d-394">StartOfInterval</span></span></li><li><span data-ttu-id="21f3d-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="21f3d-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="21f3d-396">Sıklık aya ayarlanır ve stil EndOfInterval için dilim ayın son gününde üretilmez.</span><span class="sxs-lookup"><span data-stu-id="21f3d-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="21f3d-397">Stil StartOfInterval için ayarlarsanız, dilim ayın ilk günü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="21f3d-398">Sıklığı gün olarak ayarlanır ve stili için EndOfInterval dilim günün son bir saatte üretilmez.</span><span class="sxs-lookup"><span data-stu-id="21f3d-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="21f3d-399">Sıklık saate ayarlanır ve stil EndOfInterval için dilim saat sonunda üretilmez.</span><span class="sxs-lookup"><span data-stu-id="21f3d-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="21f3d-400">Örneğin, 13'te – 2 PM dönem için bir dilim için 2 saat dilimi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="21f3d-401">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-401">No</span></span> |<span data-ttu-id="21f3d-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="21f3d-402">EndOfInterval</span></span> |
| <span data-ttu-id="21f3d-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="21f3d-403">anchorDateTime</span></span> |<span data-ttu-id="21f3d-404">Veri kümesi dilim sınırlarını işlem için Zamanlayıcı tarafından kullanılan zaman içinde mutlak konum tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="21f3d-405"><b>Not</b>: AnchorDateTime sıklığından daha ayrıntılı tarih bölümden oluşur sonra daha ayrıntılı bölümleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="21f3d-406">Örneğin, varsa <b>aralığı</b> olan <b>saatlik</b> (sıklığı: saat ve aralığı: 1) ve <b>AnchorDateTime</b> içeren <b>dakika ve saniyeleri</b> sonra <b>dakika ve saniyeleri</b> AnchorDateTime bölümlerini yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="21f3d-407">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-407">No</span></span> |<span data-ttu-id="21f3d-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="21f3d-408">01/01/0001</span></span> |
| <span data-ttu-id="21f3d-409">uzaklık</span><span class="sxs-lookup"><span data-stu-id="21f3d-409">offset</span></span> |<span data-ttu-id="21f3d-410">Tarafından başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan.</span><span class="sxs-lookup"><span data-stu-id="21f3d-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="21f3d-411"><b>Not</b>: anchorDateTime ve uzaklık belirtilirse, birleştirilmiş shift sonucudur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="21f3d-412">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-412">No</span></span> |<span data-ttu-id="21f3d-413">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-413">NA</span></span> |

<span data-ttu-id="21f3d-414">Aşağıdaki kullanılabilirlik bölümü çıktı veri kümesi üretilen saatlik (veya) giriş olduğunu belirtir dataset kullanılabilir saatlik:</span><span class="sxs-lookup"><span data-stu-id="21f3d-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="21f3d-415">**İlkesi** veri kümesi tanımı bölümünde ölçütleri veya veri kümesi dilimler karşılamanız gerekmektedir koşulu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="21f3d-416">İlke adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-416">Policy Name</span></span> | <span data-ttu-id="21f3d-417">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-417">Description</span></span> | <span data-ttu-id="21f3d-418">Uygulanan</span><span class="sxs-lookup"><span data-stu-id="21f3d-418">Applied To</span></span> | <span data-ttu-id="21f3d-419">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-419">Required</span></span> | <span data-ttu-id="21f3d-420">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="21f3d-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="21f3d-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="21f3d-421">minimumSizeMB</span></span> |<span data-ttu-id="21f3d-422">Doğrular verilerde bir **Azure blob** (megabayt cinsinden) en düşük boyut gereksinimlerini karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="21f3d-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="21f3d-423">Azure Blob</span></span> |<span data-ttu-id="21f3d-424">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-424">No</span></span> |<span data-ttu-id="21f3d-425">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-425">NA</span></span> |
| <span data-ttu-id="21f3d-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="21f3d-426">minimumRows</span></span> |<span data-ttu-id="21f3d-427">Doğrular verilerde bir **Azure SQL veritabanı** veya bir **Azure tablo** en az satır sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="21f3d-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="21f3d-428">Azure SQL Database</span></span></li><li><span data-ttu-id="21f3d-429">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="21f3d-429">Azure Table</span></span></li></ul> |<span data-ttu-id="21f3d-430">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-430">No</span></span> |<span data-ttu-id="21f3d-431">NA</span><span class="sxs-lookup"><span data-stu-id="21f3d-431">NA</span></span> |

<span data-ttu-id="21f3d-432">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="21f3d-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="21f3d-433">Azure Data Factory tarafından üretilen bir veri kümesi sürece bunu olarak işaretlenmelidir **dış**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="21f3d-434">Etkinlik veya ardışık düzen zincirleme kullanılmadığı sürece bu ayar genellikle bir ardışık düzendeki ilk etkinlik girişleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="21f3d-435">Ad</span><span class="sxs-lookup"><span data-stu-id="21f3d-435">Name</span></span> | <span data-ttu-id="21f3d-436">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-436">Description</span></span> | <span data-ttu-id="21f3d-437">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-437">Required</span></span> | <span data-ttu-id="21f3d-438">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="21f3d-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="21f3d-439">dataDelay</span></span> |<span data-ttu-id="21f3d-440">Verilen dilim için dış veri kullanılabilirliğini onay gecikme süresi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="21f3d-441">Verilerin saatlik varsa, örneğin, dış veri kullanılabilir ve karşılık gelen dilimi hazır denetleyin dataDelay kullanılarak ertelenebilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="21f3d-442">Yalnızca mevcut süre için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-442">Only applies to the present time.</span></span>  <span data-ttu-id="21f3d-443">Örneğin, 1:00 PM şimdi ise ve bu değer 10 dakikadır doğrulama 13: 10'te başlatır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="21f3d-444">Bu ayar, geçmişte dilimler etkilemez (dilimler dilim bitiş saati + dataDelay < şimdi) herhangi bir gecikme işlenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="21f3d-445">Saat 23:59 saatleri gereken kullanarak belirtilen büyük `day.hours:minutes:seconds` biçimi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="21f3d-446">Örneğin, 24 saat belirtmek için 24:00:00 kullanmayın; Bunun yerine, 1.00:00:00 kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="21f3d-447">24:00:00 kullanırsanız, 24 gün (24.00:00:00) kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="21f3d-448">1 gün ve 4 saat için 1:04:00:00 belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="21f3d-449">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-449">No</span></span> |<span data-ttu-id="21f3d-450">0</span><span class="sxs-lookup"><span data-stu-id="21f3d-450">0</span></span> |
| <span data-ttu-id="21f3d-451">Retryınterval</span><span class="sxs-lookup"><span data-stu-id="21f3d-451">retryInterval</span></span> |<span data-ttu-id="21f3d-452">Bir hata ile sonraki arasındaki bekleme süresini girişimi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="21f3d-453">Bir deneme başarısız olursa, sonraki deneyin sonra Retryınterval olur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="21f3d-454">1:00 PM şimdi ise, ilk denemede başlamadan.</span><span class="sxs-lookup"><span data-stu-id="21f3d-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="21f3d-455">İlk doğrulama denetimi tamamlamak için süre 1 dakika ve işlem başarısız oldu, sonraki yeniden deneme ise 1:00 1 dak (süresi) + 1 dak (yeniden deneme aralığı) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="21f3d-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="21f3d-456">Geçmişte dilimler için gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="21f3d-457">Yeniden deneme hemen gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-457">The retry happens immediately.</span></span> |<span data-ttu-id="21f3d-458">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-458">No</span></span> |<span data-ttu-id="21f3d-459">00:01:00 (1 dakika)</span><span class="sxs-lookup"><span data-stu-id="21f3d-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="21f3d-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-460">retryTimeout</span></span> |<span data-ttu-id="21f3d-461">Yeniden deneme girişimleri için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="21f3d-462">Bu özellik 10 dakika olarak ayarlanırsa, doğrulama 10 dakika içinde tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="21f3d-463">Yeniden deneme doğrulamayı gerçekleştirmek için 10 dakikadan uzun sürüyorsa, zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="21f3d-464">Tüm denemeleri doğrulama için zaman aşımına uğrarsa, dilim süresi sona erdi işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="21f3d-465">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-465">No</span></span> |<span data-ttu-id="21f3d-466">00:10:00 (10 dakika)</span><span class="sxs-lookup"><span data-stu-id="21f3d-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="21f3d-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="21f3d-467">maximumRetry</span></span> |<span data-ttu-id="21f3d-468">Dış veri kullanılabilirliğini denetleyin sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="21f3d-469">İzin verilen en büyük değer 10'dur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="21f3d-470">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-470">No</span></span> |<span data-ttu-id="21f3d-471">3</span><span class="sxs-lookup"><span data-stu-id="21f3d-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="21f3d-472">VERİ DEPOLARI</span><span class="sxs-lookup"><span data-stu-id="21f3d-472">DATA STORES</span></span>
<span data-ttu-id="21f3d-473">[Bağlantılı hizmeti](#linked-service) tüm türleri bağlı hizmetler için ortak olan JSON öğeleri için sağlanan bölüm açıklamalar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="21f3d-474">Bu bölümde her veri deposuna belirli JSON öğeleri hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="21f3d-475">[Dataset](#dataset) veri kümeleri tüm türleri için ortak olan JSON öğeleri için sağlanan bölüm açıklamalar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="21f3d-476">Bu bölümde her veri deposuna belirli JSON öğeleri hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="21f3d-477">[Etkinlik](#activity) tüm türleri etkinlikler için ortak olan JSON öğeleri için sağlanan bölüm açıklamalar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="21f3d-478">Bu bölümde bir kopyalama etkinliği kaynak/havuz olarak kullanıldığında, her veri deposuna özel JSON öğeleri hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="21f3d-479">Bağlantılı hizmeti, veri kümesi ve kaynak/havuz kopyalama etkinliği için JSON şemaları görmek ilgilendiğiniz deposu için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="21f3d-480">Kategori</span><span class="sxs-lookup"><span data-stu-id="21f3d-480">Category</span></span> | <span data-ttu-id="21f3d-481">Veri deposu</span><span class="sxs-lookup"><span data-stu-id="21f3d-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="21f3d-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="21f3d-482">**Azure**</span></span> |[<span data-ttu-id="21f3d-483">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="21f3d-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="21f3d-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="21f3d-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="21f3d-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="21f3d-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="21f3d-486">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="21f3d-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="21f3d-487">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="21f3d-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="21f3d-488">Azure Search</span><span class="sxs-lookup"><span data-stu-id="21f3d-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="21f3d-489">Azure Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="21f3d-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="21f3d-490">**Veritabanları**</span><span class="sxs-lookup"><span data-stu-id="21f3d-490">**Databases**</span></span> |[<span data-ttu-id="21f3d-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="21f3d-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="21f3d-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="21f3d-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="21f3d-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="21f3d-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="21f3d-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="21f3d-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="21f3d-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="21f3d-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="21f3d-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="21f3d-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="21f3d-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="21f3d-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="21f3d-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="21f3d-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="21f3d-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="21f3d-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="21f3d-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="21f3d-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="21f3d-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="21f3d-501">**NoSQL**</span></span> |[<span data-ttu-id="21f3d-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="21f3d-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="21f3d-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="21f3d-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="21f3d-504">**Dosya**</span><span class="sxs-lookup"><span data-stu-id="21f3d-504">**File**</span></span> |[<span data-ttu-id="21f3d-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="21f3d-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="21f3d-506">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="21f3d-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="21f3d-507">FTP</span><span class="sxs-lookup"><span data-stu-id="21f3d-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="21f3d-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="21f3d-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="21f3d-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="21f3d-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="21f3d-510">**Diğer**</span><span class="sxs-lookup"><span data-stu-id="21f3d-510">**Others**</span></span> |[<span data-ttu-id="21f3d-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="21f3d-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="21f3d-512">OData</span><span class="sxs-lookup"><span data-stu-id="21f3d-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="21f3d-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="21f3d-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="21f3d-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="21f3d-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="21f3d-515">Web tablo</span><span class="sxs-lookup"><span data-stu-id="21f3d-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="21f3d-516">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="21f3d-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-517">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-517">Linked service</span></span>
<span data-ttu-id="21f3d-518">Bağlı hizmetler iki tür vardır: Azure depolama bağlantılı hizmeti ve Azure depolama SAS bağlantılı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21f3d-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="21f3d-519">Azure Storage Bağlı Hizmeti</span><span class="sxs-lookup"><span data-stu-id="21f3d-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="21f3d-520">Azure storage hesabınızı kullanarak bir data factory'ye bağlamak için **hesap anahtarı**, bir Azure Storage bağlı hizmeti oluşturma.</span><span class="sxs-lookup"><span data-stu-id="21f3d-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="21f3d-521">Bağlantılı hizmeti bir Azure depolama alanını tanımlayın, Ayarla **türü** bağlantılı hizmetinin **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="21f3d-522">Ardından, aşağıdaki özellikleri belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-523">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-523">Property</span></span> | <span data-ttu-id="21f3d-524">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-524">Description</span></span> | <span data-ttu-id="21f3d-525">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-526">connectionString</span></span> |<span data-ttu-id="21f3d-527">ConnectionString özelliği için Azure depolama alanına bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="21f3d-528">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="21f3d-529">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="21f3d-530">Azure Storage SAS bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="21f3d-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="21f3d-531">Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak Azure data factory için bir Azure depolama hesabı bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="21f3d-532">Veri Fabrikası depolama alanındaki tüm/özel kaynakları (blob/kapsayıcısı) kısıtlanmış/zaman sınırlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="21f3d-533">Paylaşılan erişim imzası kullanarak bir veri fabrikası Azure depolama hesabınıza bağlamak için bir Azure depolama bağlı SAS hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f3d-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="21f3d-534">Bağlantılı hizmeti bir Azure depolama SAS tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="21f3d-535">Ardından, aşağıdaki özellikleri belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="21f3d-536">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-536">Property</span></span> | <span data-ttu-id="21f3d-537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-537">Description</span></span> | <span data-ttu-id="21f3d-538">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="21f3d-539">sasUri</span></span> |<span data-ttu-id="21f3d-540">Blob, kapsayıcı ya da tablo gibi Azure Storage kaynakları için paylaşılan erişim imzası URI belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="21f3d-541">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="21f3d-542">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="21f3d-543">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Blob Storage bağlayıcı](data-factory-azure-blob-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-544">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-544">Dataset</span></span>
<span data-ttu-id="21f3d-545">Bir Azure Blob veri kümesini tanımlamak için **türü** için veri kümesinin **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="21f3d-546">Ardından aşağıdaki Azure Blob belirli özelliklerinde belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-547">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-547">Property</span></span> | <span data-ttu-id="21f3d-548">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-548">Description</span></span> | <span data-ttu-id="21f3d-549">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-550">folderPath</span></span> |<span data-ttu-id="21f3d-551">Kapsayıcı ve klasöre blob depolamada yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="21f3d-552">Örnek: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="21f3d-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="21f3d-553">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-553">Yes</span></span> |
| <span data-ttu-id="21f3d-554">fileName</span><span class="sxs-lookup"><span data-stu-id="21f3d-554">fileName</span></span> |<span data-ttu-id="21f3d-555">Blob adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-555">Name of the blob.</span></span> <span data-ttu-id="21f3d-556">isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="21f3d-557">Bir dosya adı belirtirseniz, (kopyalama dahil) etkinlik belirli Blob üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="21f3d-558">Dosya adı belirtilmediğinde kopyalama tüm BLOB'lar girdi veri kümesi için folderPath içerir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="21f3d-559">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan dosya adı aşağıdaki olacaktır Bu biçim: veri. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="21f3d-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="21f3d-560">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-560">No</span></span> |
| <span data-ttu-id="21f3d-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="21f3d-561">partitionedBy</span></span> |<span data-ttu-id="21f3d-562">partitionedBy isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="21f3d-563">Bir dinamik folderPath ve zaman serisi verileri için dosya adı belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="21f3d-564">Örneğin, folderPath için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="21f3d-565">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-565">No</span></span> |
| <span data-ttu-id="21f3d-566">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-566">format</span></span> | <span data-ttu-id="21f3d-567">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-568">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-569">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-570">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-571">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-571">No</span></span> |
| <span data-ttu-id="21f3d-572">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-572">compression</span></span> | <span data-ttu-id="21f3d-573">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-574">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="21f3d-575">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-576">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-577">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-578">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-578">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="21f3d-579">Daha fazla bilgi için bkz: [Azure Blob bağlayıcı](data-factory-azure-blob-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="21f3d-580">Kopyalama etkinliğinde BlobSource</span><span class="sxs-lookup"><span data-stu-id="21f3d-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="21f3d-581">Bir Azure Blob depolama alanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **BlobSource**ve aşağıdaki özellikleri belirtin ** kaynak ** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="21f3d-582">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-582">Property</span></span> | <span data-ttu-id="21f3d-583">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-583">Description</span></span> | <span data-ttu-id="21f3d-584">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-584">Allowed values</span></span> | <span data-ttu-id="21f3d-585">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-586">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-586">recursive</span></span> |<span data-ttu-id="21f3d-587">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="21f3d-588">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="21f3d-588">True (default value), False</span></span> |<span data-ttu-id="21f3d-589">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="21f3d-590">Örnek: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="21f3d-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="21f3d-591">Kopyalama etkinliğinde BlobSink</span><span class="sxs-lookup"><span data-stu-id="21f3d-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="21f3d-592">Bir Azure Blob depolama alanına veri kopyalıyorsanız ayarlamak **Havuz türü** kopyalama etkinliği **BlobSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-593">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-593">Property</span></span> | <span data-ttu-id="21f3d-594">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-594">Description</span></span> | <span data-ttu-id="21f3d-595">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-595">Allowed values</span></span> | <span data-ttu-id="21f3d-596">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="21f3d-597">copyBehavior</span></span> |<span data-ttu-id="21f3d-598">Kaynak BlobSource veya dosya sistemi olduğunda kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="21f3d-599"><b>PreserveHierarchy</b>: Dosya hiyerarşisi hedef klasördeki korur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="21f3d-600">Kaynak dosyanın kaynak klasöre göreli yol, hedef dosya hedef klasöre göreli yolunu aynıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="21f3d-601"><b>FlattenHierarchy</b>: tüm kaynak klasörü hedef klasör ilk düzeyi dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="21f3d-602">Hedef dosyalar otomatik adına sahip.</span><span class="sxs-lookup"><span data-stu-id="21f3d-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="21f3d-603"><b>MergeFiles (varsayılan):</b> bir dosya için kaynak klasöründeki tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="21f3d-604">Birleştirilmiş Dosya adı, dosya/Blob adı belirtilirse, belirtilen ad olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="21f3d-605">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="21f3d-606">Örnek: BlobSink</span><span class="sxs-lookup"><span data-stu-id="21f3d-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-607">Daha fazla bilgi için bkz: [Azure Blob bağlayıcı](data-factory-azure-blob-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="21f3d-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="21f3d-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-609">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-609">Linked service</span></span>
<span data-ttu-id="21f3d-610">Bağlantılı hizmeti bir Azure Data Lake Store tanımlamak için bağlantılı hizmet türüne ayarlayın **AzureDataLakeStore**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-611">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-611">Property</span></span> | <span data-ttu-id="21f3d-612">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-612">Description</span></span> | <span data-ttu-id="21f3d-613">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-614">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-614">type</span></span> | <span data-ttu-id="21f3d-615">Type özelliği ayarlanmalıdır: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="21f3d-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="21f3d-616">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-616">Yes</span></span> |
| <span data-ttu-id="21f3d-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="21f3d-617">dataLakeStoreUri</span></span> | <span data-ttu-id="21f3d-618">Azure Data Lake Store hesabı bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="21f3d-619">Aşağıdaki biçimdedir: `https://[accountname].azuredatalakestore.net/webhdfs/v1` veya `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="21f3d-620">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-620">Yes</span></span> |
| <span data-ttu-id="21f3d-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="21f3d-621">subscriptionId</span></span> | <span data-ttu-id="21f3d-622">Data Lake Store ait olduğu azure abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="21f3d-623">Havuz için gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-623">Required for sink</span></span> |
| <span data-ttu-id="21f3d-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="21f3d-624">resourceGroupName</span></span> | <span data-ttu-id="21f3d-625">Data Lake Store ait olduğu azure kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="21f3d-626">Havuz için gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-626">Required for sink</span></span> |
| <span data-ttu-id="21f3d-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="21f3d-627">servicePrincipalId</span></span> | <span data-ttu-id="21f3d-628">Uygulamanın istemci kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-628">Specify the application's client ID.</span></span> | <span data-ttu-id="21f3d-629">Evet (hizmet sorumlusu kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="21f3d-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="21f3d-630">servicePrincipalKey</span></span> | <span data-ttu-id="21f3d-631">Uygulamanın anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-631">Specify the application's key.</span></span> | <span data-ttu-id="21f3d-632">Evet (hizmet sorumlusu kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="21f3d-633">Kiracı</span><span class="sxs-lookup"><span data-stu-id="21f3d-633">tenant</span></span> | <span data-ttu-id="21f3d-634">Uygulamanızın bulunduğu altında Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="21f3d-635">Azure portalının sağ üst köşedeki fare gelerek alabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="21f3d-636">Evet (hizmet sorumlusu kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="21f3d-637">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="21f3d-637">authorization</span></span> | <span data-ttu-id="21f3d-638">Tıklatın **Authorize** düğmesini **Data Factory düzenleyici** ve bu özelliği otomatik olarak oluşturulan yetkilendirme URL'si atar kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="21f3d-639">Evet (kullanıcı kimlik bilgileri doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="21f3d-640">SessionID</span><span class="sxs-lookup"><span data-stu-id="21f3d-640">sessionId</span></span> | <span data-ttu-id="21f3d-641">OAuth yetkilendirme oturumundan OAuth oturum kimliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="21f3d-642">Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="21f3d-643">Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="21f3d-644">Evet (kullanıcı kimlik bilgileri doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="21f3d-645">Örnek: hizmet asıl kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="21f3d-646">Örnek: kullanıcı kimlik bilgilerinin kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="21f3d-647">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-648">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-648">Dataset</span></span>
<span data-ttu-id="21f3d-649">Bir Azure Data Lake Store veri kümesini tanımlamak için **türü** için veri kümesinin **AzureDataLakeStore**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-650">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-650">Property</span></span> | <span data-ttu-id="21f3d-651">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-651">Description</span></span> | <span data-ttu-id="21f3d-652">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-653">folderPath</span></span> |<span data-ttu-id="21f3d-654">Kapsayıcı ve Azure Data Lake klasörü yoluna depolar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="21f3d-655">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-655">Yes</span></span> |
| <span data-ttu-id="21f3d-656">fileName</span><span class="sxs-lookup"><span data-stu-id="21f3d-656">fileName</span></span> |<span data-ttu-id="21f3d-657">Azure Data Lake Store'da dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="21f3d-658">isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="21f3d-659">Bir dosya adı belirtirseniz, (kopyalama dahil) etkinlik belirli bir dosya üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="21f3d-660">FileName belirtilmediğinde kopyalama folderPath girdi veri kümesi için tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="21f3d-661">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan dosya adı aşağıdaki olacaktır Bu biçim: veri. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="21f3d-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="21f3d-662">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-662">No</span></span> |
| <span data-ttu-id="21f3d-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="21f3d-663">partitionedBy</span></span> |<span data-ttu-id="21f3d-664">partitionedBy isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="21f3d-665">Bir dinamik folderPath ve zaman serisi verileri için dosya adı belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="21f3d-666">Örneğin, folderPath için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="21f3d-667">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-667">No</span></span> |
| <span data-ttu-id="21f3d-668">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-668">format</span></span> | <span data-ttu-id="21f3d-669">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-670">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-671">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-672">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-673">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-673">No</span></span> |
| <span data-ttu-id="21f3d-674">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-674">compression</span></span> | <span data-ttu-id="21f3d-675">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-676">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="21f3d-677">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-678">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-679">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-680">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-681">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="21f3d-682">Kopya etkinliği Azure Data Lake Store kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-683">Bir Azure Data Lake Deposu'ndan veri veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **AzureDataLakeStoreSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="21f3d-684">**AzureDataLakeStoreSource** aşağıdaki özellikleri destekler **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="21f3d-685">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-685">Property</span></span> | <span data-ttu-id="21f3d-686">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-686">Description</span></span> | <span data-ttu-id="21f3d-687">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-687">Allowed values</span></span> | <span data-ttu-id="21f3d-688">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-689">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-689">recursive</span></span> |<span data-ttu-id="21f3d-690">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="21f3d-691">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="21f3d-691">True (default value), False</span></span> |<span data-ttu-id="21f3d-692">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="21f3d-693">Örnek: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="21f3d-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-694">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="21f3d-695">Kopya etkinliği Azure Data Lake Store havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-696">Bir Azure Data Lake Store'a veri kopyalamak istiyorsanız, ayarlayın **Havuz türü** kopyalama etkinliği **AzureDataLakeStoreSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-697">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-697">Property</span></span> | <span data-ttu-id="21f3d-698">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-698">Description</span></span> | <span data-ttu-id="21f3d-699">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-699">Allowed values</span></span> | <span data-ttu-id="21f3d-700">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="21f3d-701">copyBehavior</span></span> |<span data-ttu-id="21f3d-702">Kopyalama davranışını belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="21f3d-703"><b>PreserveHierarchy</b>: Dosya hiyerarşisi hedef klasördeki korur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="21f3d-704">Kaynak dosyanın kaynak klasöre göreli yol, hedef dosya hedef klasöre göreli yolunu aynıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="21f3d-705"><b>FlattenHierarchy</b>: tüm dosyaları kaynak klasörden hedef klasöre ilk düzeyi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="21f3d-706">Hedef dosyalar otomatik adıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="21f3d-707"><b>MergeFiles</b>: bir dosya için kaynak klasöründeki tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="21f3d-708">Birleştirilmiş Dosya adı, dosya/Blob adı belirtilirse, belirtilen ad olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="21f3d-709">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="21f3d-710">Örnek: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="21f3d-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-711">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="21f3d-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="21f3d-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="21f3d-713">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-713">Linked service</span></span>
<span data-ttu-id="21f3d-714">Bağlantılı hizmeti bir Azure Cosmos DB tanımlamak için Ayarla **türü** bağlantılı hizmetinin **DocumentDb**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-715">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="21f3d-715">**Property**</span></span> | <span data-ttu-id="21f3d-716">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="21f3d-716">**Description**</span></span> | <span data-ttu-id="21f3d-717">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="21f3d-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-718">connectionString</span></span> |<span data-ttu-id="21f3d-719">Azure Cosmos DB veritabanına bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="21f3d-720">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-721">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="21f3d-722">Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-723">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-723">Dataset</span></span>
<span data-ttu-id="21f3d-724">Bir Azure Cosmos DB veri kümesini tanımlamak için **türü** için veri kümesinin **DocumentDbCollection**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-725">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="21f3d-725">**Property**</span></span> | <span data-ttu-id="21f3d-726">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="21f3d-726">**Description**</span></span> | <span data-ttu-id="21f3d-727">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="21f3d-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="21f3d-728">collectionName</span></span> |<span data-ttu-id="21f3d-729">Azure Cosmos DB koleksiyonunun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="21f3d-730">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-731">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="21f3d-732">Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="21f3d-733">Kopya etkinliği Azure Cosmos DB koleksiyon kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-734">Bir Azure Cosmos Veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **DocumentDbCollectionSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-735">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="21f3d-735">**Property**</span></span> | <span data-ttu-id="21f3d-736">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="21f3d-736">**Description**</span></span> | <span data-ttu-id="21f3d-737">**İzin verilen değerler**</span><span class="sxs-lookup"><span data-stu-id="21f3d-737">**Allowed values**</span></span> | <span data-ttu-id="21f3d-738">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="21f3d-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-739">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-739">query</span></span> |<span data-ttu-id="21f3d-740">Verileri okumak için sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-740">Specify the query to read data.</span></span> |<span data-ttu-id="21f3d-741">Sorgu dizesindeki Azure Cosmos DB tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="21f3d-742">Örnek:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="21f3d-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="21f3d-743">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-743">No</span></span> <br/><br/><span data-ttu-id="21f3d-744">Belirtilmezse, yürütülen SQL deyimi:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="21f3d-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="21f3d-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="21f3d-745">nestingSeparator</span></span> |<span data-ttu-id="21f3d-746">Belge iç içe geçmiş belirtmek için özel karakter</span><span class="sxs-lookup"><span data-stu-id="21f3d-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="21f3d-747">Herhangi bir karakter.</span><span class="sxs-lookup"><span data-stu-id="21f3d-747">Any character.</span></span> <br/><br/><span data-ttu-id="21f3d-748">Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="21f3d-749">Azure Data Factory sağlar hiyerarşisi olan nestingSeparator aracılığıyla belirtmek kullanıcı "."</span><span class="sxs-lookup"><span data-stu-id="21f3d-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="21f3d-750">Yukarıdaki örneklerde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-750">in the above examples.</span></span> <span data-ttu-id="21f3d-751">Ayırıcı olmadan kopyalama etkinliği üç alt öğeleri "Ad" nesnesiyle ilk olarak, oluşturacak Orta ve son "Name.First", "Name.Middle" ve "Name.Last" Tablo tanımında göre.</span><span class="sxs-lookup"><span data-stu-id="21f3d-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="21f3d-752">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-753">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="21f3d-754">Kopya etkinliği Azure Cosmos DB koleksiyonu havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-755">Azure Cosmos Veritabanına veri kopyalamak istiyorsanız, ayarlayın **Havuz türü** kopyalama etkinliği **DocumentDbCollectionSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-756">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="21f3d-756">**Property**</span></span> | <span data-ttu-id="21f3d-757">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="21f3d-757">**Description**</span></span> | <span data-ttu-id="21f3d-758">**İzin verilen değerler**</span><span class="sxs-lookup"><span data-stu-id="21f3d-758">**Allowed values**</span></span> | <span data-ttu-id="21f3d-759">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="21f3d-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="21f3d-760">nestingSeparator</span></span> |<span data-ttu-id="21f3d-761">Bir özel karakter iç içe geçmiş belge belirtmek için kaynak sütun adı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="21f3d-762">Örneğin yukarıdaki: `Name.First` çıktıda tablo Cosmos DB belgede aşağıdaki JSON yapısını oluşturur:</span><span class="sxs-lookup"><span data-stu-id="21f3d-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="21f3d-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="21f3d-763">"Name": {</span></span><br/>    <span data-ttu-id="21f3d-764">"İlk": "John"</span><span class="sxs-lookup"><span data-stu-id="21f3d-764">"First": "John"</span></span><br/><span data-ttu-id="21f3d-765">},</span><span class="sxs-lookup"><span data-stu-id="21f3d-765">},</span></span> |<span data-ttu-id="21f3d-766">İç içe geçme düzeylerini ayırmak için kullanılan karakterdir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="21f3d-767">Varsayılan değer `.` (nokta).</span><span class="sxs-lookup"><span data-stu-id="21f3d-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="21f3d-768">İç içe geçme düzeylerini ayırmak için kullanılan karakterdir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="21f3d-769">Varsayılan değer `.` (nokta).</span><span class="sxs-lookup"><span data-stu-id="21f3d-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="21f3d-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-770">writeBatchSize</span></span> |<span data-ttu-id="21f3d-771">Azure Cosmos DB hizmeti belgeleri oluşturmak için paralel isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="21f3d-772">Bu özelliği kullanarak Azure Cosmos DB öğesine/öğesinden veri kopyalama işlemi sırasında performans ince ayar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="21f3d-773">Daha fazla paralel istekler için Azure Cosmos DB'ye gönderildiğinden writeBatchSize artırdığınızda daha iyi bir performans düşüklüğü görebilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="21f3d-774">Ancak, azaltma önlemek gerekir, hata iletisi atabilirsiniz: "oranıdır büyük istek".</span><span class="sxs-lookup"><span data-stu-id="21f3d-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="21f3d-775">Azaltmayı bir dizi etkene, belgeler, belgeleri koşullarını sayısı boyutunu dahil olmak üzere, hedef koleksiyon, vb. İlkesi dizin tarafından belirlenir. Kopyalama işlemleri için en çok kullanılabilir verimlilik sağlamak için daha iyi bir koleksiyonunu (örneğin, S3) kullanabilirsiniz (2.500 istek birimleri/saniye).</span><span class="sxs-lookup"><span data-stu-id="21f3d-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="21f3d-776">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="21f3d-776">Integer</span></span> |<span data-ttu-id="21f3d-777">Hayır (varsayılan: 5)</span><span class="sxs-lookup"><span data-stu-id="21f3d-777">No (default: 5)</span></span> |
| <span data-ttu-id="21f3d-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-778">writeBatchTimeout</span></span> |<span data-ttu-id="21f3d-779">İşlemin zaman aşımına uğramadan önce tamamlanması için bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="21f3d-780">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-780">timespan</span></span><br/><br/> <span data-ttu-id="21f3d-781">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="21f3d-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="21f3d-782">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-783">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="21f3d-784">Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="21f3d-785">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="21f3d-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-786">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-786">Linked service</span></span>
<span data-ttu-id="21f3d-787">Bağlantılı hizmeti bir Azure SQL veritabanı tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureSqlDatabase**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-788">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-788">Property</span></span> | <span data-ttu-id="21f3d-789">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-789">Description</span></span> | <span data-ttu-id="21f3d-790">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-791">connectionString</span></span> |<span data-ttu-id="21f3d-792">ConnectionString özelliği için Azure SQL veritabanı örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="21f3d-793">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-794">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="21f3d-795">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-796">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-796">Dataset</span></span>
<span data-ttu-id="21f3d-797">Bir Azure SQL veritabanı veri kümesini tanımlamak için **türü** için veri kümesinin **AzureSqlTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-798">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-798">Property</span></span> | <span data-ttu-id="21f3d-799">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-799">Description</span></span> | <span data-ttu-id="21f3d-800">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-801">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-801">tableName</span></span> |<span data-ttu-id="21f3d-802">Tablo veya Görünüm bağlantılı hizmetinin Azure SQL veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="21f3d-803">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-804">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="21f3d-805">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="21f3d-806">Kopyalama etkinliğinde SQL kaynağı</span><span class="sxs-lookup"><span data-stu-id="21f3d-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-807">Bir Azure SQL veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **SqlSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-808">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-808">Property</span></span> | <span data-ttu-id="21f3d-809">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-809">Description</span></span> | <span data-ttu-id="21f3d-810">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-810">Allowed values</span></span> | <span data-ttu-id="21f3d-811">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-812">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="21f3d-812">sqlReaderQuery</span></span> |<span data-ttu-id="21f3d-813">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-813">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-814">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-814">SQL query string.</span></span> <span data-ttu-id="21f3d-815">Örnek: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-816">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-816">No</span></span> |
| <span data-ttu-id="21f3d-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="21f3d-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="21f3d-818">Kaynak tablodan veri okuyan saklı yordamın adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="21f3d-819">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-819">Name of the stored procedure.</span></span> |<span data-ttu-id="21f3d-820">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-820">No</span></span> |
| <span data-ttu-id="21f3d-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-821">storedProcedureParameters</span></span> |<span data-ttu-id="21f3d-822">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="21f3d-823">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-823">Name/value pairs.</span></span> <span data-ttu-id="21f3d-824">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="21f3d-825">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-826">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="21f3d-827">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="21f3d-828">Kopyalama etkinliği SQL havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-829">Azure SQL veritabanına veri kopyalamak istiyorsanız, ayarlayın **Havuz türü** kopyalama etkinliği **SqlSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-830">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-830">Property</span></span> | <span data-ttu-id="21f3d-831">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-831">Description</span></span> | <span data-ttu-id="21f3d-832">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-832">Allowed values</span></span> | <span data-ttu-id="21f3d-833">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-834">writeBatchTimeout</span></span> |<span data-ttu-id="21f3d-835">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="21f3d-836">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-836">timespan</span></span><br/><br/> <span data-ttu-id="21f3d-837">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="21f3d-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="21f3d-838">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-838">No</span></span> |
| <span data-ttu-id="21f3d-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-839">writeBatchSize</span></span> |<span data-ttu-id="21f3d-840">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="21f3d-841">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="21f3d-841">Integer (number of rows)</span></span> |<span data-ttu-id="21f3d-842">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="21f3d-842">No (default: 10000)</span></span> |
| <span data-ttu-id="21f3d-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="21f3d-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="21f3d-844">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="21f3d-845">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-845">A query statement.</span></span> |<span data-ttu-id="21f3d-846">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-846">No</span></span> |
| <span data-ttu-id="21f3d-847">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="21f3d-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="21f3d-848">Ne zaman yeniden çalıştırılacağını belirli bir dilim verileri temizlemek için kullanılan otomatik dilim tanımlayıcı doldurmak kopyalama etkinliği için bir sütun adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="21f3d-849">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="21f3d-850">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-850">No</span></span> |
| <span data-ttu-id="21f3d-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="21f3d-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="21f3d-852">Saklı yordam adı hedef tabloda bu upserts (güncelleştirmeler/ekler) verileri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="21f3d-853">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-853">Name of the stored procedure.</span></span> |<span data-ttu-id="21f3d-854">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-854">No</span></span> |
| <span data-ttu-id="21f3d-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-855">storedProcedureParameters</span></span> |<span data-ttu-id="21f3d-856">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="21f3d-857">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-857">Name/value pairs.</span></span> <span data-ttu-id="21f3d-858">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="21f3d-859">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-859">No</span></span> |
| <span data-ttu-id="21f3d-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="21f3d-860">sqlWriterTableType</span></span> |<span data-ttu-id="21f3d-861">Saklı yordam, kullanılacak bir tablo türü adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="21f3d-862">Kopyalama etkinliği taşınan veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="21f3d-863">Saklı yordam kodu ardından var olan verilerle kopyalanan verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="21f3d-864">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-864">A table type name.</span></span> |<span data-ttu-id="21f3d-865">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-866">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-867">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="21f3d-868">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="21f3d-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-869">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-869">Linked service</span></span>
<span data-ttu-id="21f3d-870">Bağlantılı hizmetinin Azure SQL Data Warehouse tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureSqlDW**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-871">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-871">Property</span></span> | <span data-ttu-id="21f3d-872">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-872">Description</span></span> | <span data-ttu-id="21f3d-873">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-874">connectionString</span></span> |<span data-ttu-id="21f3d-875">ConnectionString özelliği için Azure SQL Data Warehouse örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="21f3d-876">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="21f3d-877">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="21f3d-878">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-879">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-879">Dataset</span></span>
<span data-ttu-id="21f3d-880">Bir Azure SQL Data Warehouse veri kümesini tanımlamak için **türü** için veri kümesinin **AzureSqlDWTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-881">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-881">Property</span></span> | <span data-ttu-id="21f3d-882">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-882">Description</span></span> | <span data-ttu-id="21f3d-883">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-884">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-884">tableName</span></span> |<span data-ttu-id="21f3d-885">Tablo veya Görünüm başvuran bağlı hizmetin Azure SQL veri ambarı veritabanındaki adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="21f3d-886">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-887">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-888">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="21f3d-889">Kopyalama etkinliğinde SQL DW kaynağı</span><span class="sxs-lookup"><span data-stu-id="21f3d-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-890">Azure SQL veri ambarından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **SqlDWSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-891">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-891">Property</span></span> | <span data-ttu-id="21f3d-892">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-892">Description</span></span> | <span data-ttu-id="21f3d-893">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-893">Allowed values</span></span> | <span data-ttu-id="21f3d-894">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-895">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="21f3d-895">sqlReaderQuery</span></span> |<span data-ttu-id="21f3d-896">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-896">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-897">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-897">SQL query string.</span></span> <span data-ttu-id="21f3d-898">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-899">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-899">No</span></span> |
| <span data-ttu-id="21f3d-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="21f3d-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="21f3d-901">Kaynak tablodan veri okuyan saklı yordamın adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="21f3d-902">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-902">Name of the stored procedure.</span></span> |<span data-ttu-id="21f3d-903">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-903">No</span></span> |
| <span data-ttu-id="21f3d-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-904">storedProcedureParameters</span></span> |<span data-ttu-id="21f3d-905">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="21f3d-906">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-906">Name/value pairs.</span></span> <span data-ttu-id="21f3d-907">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="21f3d-908">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-909">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-910">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="21f3d-911">SQL DW havuz kopyalama etkinliğinde</span><span class="sxs-lookup"><span data-stu-id="21f3d-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-912">Azure SQL Data Warehouse'a veri kopyalıyorsanız ayarlamak **Havuz türü** kopyalama etkinliği **SqlDWSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-913">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-913">Property</span></span> | <span data-ttu-id="21f3d-914">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-914">Description</span></span> | <span data-ttu-id="21f3d-915">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-915">Allowed values</span></span> | <span data-ttu-id="21f3d-916">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="21f3d-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="21f3d-918">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="21f3d-919">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-919">A query statement.</span></span> |<span data-ttu-id="21f3d-920">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-920">No</span></span> |
| <span data-ttu-id="21f3d-921">Bulunan'allowpolybase</span><span class="sxs-lookup"><span data-stu-id="21f3d-921">allowPolyBase</span></span> |<span data-ttu-id="21f3d-922">BULKINSERT mekanizması yerine PolyBase (varsa) kullanılıp kullanılmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="21f3d-923">**PolyBase kullanarak SQL Data Warehouse'a veri yükleme için önerilen yoldur.**</span><span class="sxs-lookup"><span data-stu-id="21f3d-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="21f3d-924">True</span><span class="sxs-lookup"><span data-stu-id="21f3d-924">True</span></span> <br/><span data-ttu-id="21f3d-925">False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-925">False (default)</span></span> |<span data-ttu-id="21f3d-926">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-926">No</span></span> |
| <span data-ttu-id="21f3d-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="21f3d-927">polyBaseSettings</span></span> |<span data-ttu-id="21f3d-928">Bir grup olabilir özellik belirtilen **Bulunan'allowpolybase** özelliği ayarlanmış **doğru**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="21f3d-929">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-929">No</span></span> |
| <span data-ttu-id="21f3d-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="21f3d-930">rejectValue</span></span> |<span data-ttu-id="21f3d-931">Sayı veya yüzde değeri sorgu başarısız önce reddedilemiyor satır belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="21f3d-932">PolyBase'nın reddetme seçenekleri hakkında daha fazla bilgi **bağımsız değişkenleri** bölümünü [CREATE dış TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="21f3d-933">0 (varsayılan), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="21f3d-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="21f3d-934">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-934">No</span></span> |
| <span data-ttu-id="21f3d-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="21f3d-935">rejectType</span></span> |<span data-ttu-id="21f3d-936">RejectValue seçeneği bir hazır değer veya bir yüzde belirtilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="21f3d-937">Değer (varsayılan), yüzde</span><span class="sxs-lookup"><span data-stu-id="21f3d-937">Value (default), Percentage</span></span> |<span data-ttu-id="21f3d-938">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-938">No</span></span> |
| <span data-ttu-id="21f3d-939">Havuzu'na ilişkin</span><span class="sxs-lookup"><span data-stu-id="21f3d-939">rejectSampleValue</span></span> |<span data-ttu-id="21f3d-940">PolyBase reddedilen satırları yüzdesini yeniden hesaplar önce almak için satır sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="21f3d-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="21f3d-941">1, 2, …</span></span> |<span data-ttu-id="21f3d-942">Evet, varsa **rejectType** olan **yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="21f3d-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="21f3d-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="21f3d-943">useTypeDefault</span></span> |<span data-ttu-id="21f3d-944">PolyBase metin dosyasından veri aldığında sınırlandırılmış metin dosyaları eksik değerleri nasıl ele alınacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="21f3d-945">Bağımsız değişkenler bölümünde bu özelliği hakkında daha fazla bilgi [oluşturma EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="21f3d-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="21f3d-946">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-946">True, False (default)</span></span> |<span data-ttu-id="21f3d-947">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-947">No</span></span> |
| <span data-ttu-id="21f3d-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-948">writeBatchSize</span></span> |<span data-ttu-id="21f3d-949">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="21f3d-950">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="21f3d-950">Integer (number of rows)</span></span> |<span data-ttu-id="21f3d-951">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="21f3d-951">No (default: 10000)</span></span> |
| <span data-ttu-id="21f3d-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-952">writeBatchTimeout</span></span> |<span data-ttu-id="21f3d-953">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="21f3d-954">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-954">timespan</span></span><br/><br/> <span data-ttu-id="21f3d-955">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="21f3d-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="21f3d-956">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-957">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-958">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="21f3d-959">Azure Search</span><span class="sxs-lookup"><span data-stu-id="21f3d-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-960">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-960">Linked service</span></span>
<span data-ttu-id="21f3d-961">Bağlantılı hizmeti bir Azure Search tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureSearch**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-962">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-962">Property</span></span> | <span data-ttu-id="21f3d-963">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-963">Description</span></span> | <span data-ttu-id="21f3d-964">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="21f3d-965">URL</span><span class="sxs-lookup"><span data-stu-id="21f3d-965">url</span></span> | <span data-ttu-id="21f3d-966">Azure Search hizmeti için URL.</span><span class="sxs-lookup"><span data-stu-id="21f3d-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="21f3d-967">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-967">Yes</span></span> |
| <span data-ttu-id="21f3d-968">anahtar</span><span class="sxs-lookup"><span data-stu-id="21f3d-968">key</span></span> | <span data-ttu-id="21f3d-969">Azure Search hizmeti için yönetici anahtarı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="21f3d-970">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-971">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="21f3d-972">Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-973">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-973">Dataset</span></span>
<span data-ttu-id="21f3d-974">Bir Azure Search veri kümesini tanımlamak için **türü** için veri kümesinin **AzureSearchIndex**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-975">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-975">Property</span></span> | <span data-ttu-id="21f3d-976">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-976">Description</span></span> | <span data-ttu-id="21f3d-977">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="21f3d-978">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-978">type</span></span> | <span data-ttu-id="21f3d-979">Type özelliği ayarlamak **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="21f3d-980">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-980">Yes</span></span> |
| <span data-ttu-id="21f3d-981">indexName</span><span class="sxs-lookup"><span data-stu-id="21f3d-981">indexName</span></span> | <span data-ttu-id="21f3d-982">Azure Search dizini adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-982">Name of the Azure Search index.</span></span> <span data-ttu-id="21f3d-983">Veri Fabrikası dizinini oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-983">Data Factory does not create the index.</span></span> <span data-ttu-id="21f3d-984">Azure Search'te dizin mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="21f3d-985">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-986">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="21f3d-987">Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="21f3d-988">Kopya etkinliği Azure arama dizini havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-989">Bir Azure Search dizinine veri kopyalıyorsanız ayarlamak **Havuz türü** kopyalama etkinliği **AzureSearchIndexSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-990">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-990">Property</span></span> | <span data-ttu-id="21f3d-991">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-991">Description</span></span> | <span data-ttu-id="21f3d-992">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-992">Allowed values</span></span> | <span data-ttu-id="21f3d-993">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="21f3d-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="21f3d-994">WriteBehavior</span></span> | <span data-ttu-id="21f3d-995">Birleştir veya bir belge dizinde zaten mevcut olduğunda Değiştir belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="21f3d-996">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-996">Merge (default)</span></span><br/><span data-ttu-id="21f3d-997">Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="21f3d-997">Upload</span></span>| <span data-ttu-id="21f3d-998">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-998">No</span></span> |
| <span data-ttu-id="21f3d-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-999">WriteBatchSize</span></span> | <span data-ttu-id="21f3d-1000">Arabellek boyutu writeBatchSize ulaştığında Azure Search dizinine veri yükler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="21f3d-1001">1 için 1.000.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1001">1 to 1,000.</span></span> <span data-ttu-id="21f3d-1002">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1002">Default value is 1000.</span></span> | <span data-ttu-id="21f3d-1003">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1004">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-1005">Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="21f3d-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="21f3d-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1007">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1007">Linked service</span></span>
<span data-ttu-id="21f3d-1008">Bağlı hizmetler iki tür vardır: Azure depolama bağlantılı hizmeti ve Azure depolama SAS bağlantılı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="21f3d-1009">Azure Storage Bağlı Hizmeti</span><span class="sxs-lookup"><span data-stu-id="21f3d-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="21f3d-1010">Azure storage hesabınızı kullanarak bir data factory'ye bağlamak için **hesap anahtarı**, bir Azure Storage bağlı hizmeti oluşturma.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="21f3d-1011">Bağlantılı hizmeti bir Azure depolama alanını tanımlayın, Ayarla **türü** bağlantılı hizmetinin **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="21f3d-1012">Ardından, aşağıdaki özellikleri belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1013">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1013">Property</span></span> | <span data-ttu-id="21f3d-1014">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1014">Description</span></span> | <span data-ttu-id="21f3d-1015">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-1016">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-1016">type</span></span> |<span data-ttu-id="21f3d-1017">Type özelliği ayarlanmalıdır: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="21f3d-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="21f3d-1018">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1018">Yes</span></span> |
| <span data-ttu-id="21f3d-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-1019">connectionString</span></span> |<span data-ttu-id="21f3d-1020">ConnectionString özelliği için Azure depolama alanına bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="21f3d-1021">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1021">Yes</span></span> |

<span data-ttu-id="21f3d-1022">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="21f3d-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="21f3d-1023">Azure Storage SAS bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="21f3d-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="21f3d-1024">Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak Azure data factory için bir Azure depolama hesabı bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="21f3d-1025">Veri Fabrikası depolama alanındaki tüm/özel kaynakları (blob/kapsayıcısı) kısıtlanmış/zaman sınırlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="21f3d-1026">Paylaşılan erişim imzası kullanarak bir veri fabrikası Azure depolama hesabınıza bağlamak için bir Azure depolama bağlı SAS hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="21f3d-1027">Bağlantılı hizmeti bir Azure depolama SAS tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="21f3d-1028">Ardından, aşağıdaki özellikleri belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="21f3d-1029">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1029">Property</span></span> | <span data-ttu-id="21f3d-1030">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1030">Description</span></span> | <span data-ttu-id="21f3d-1031">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-1032">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-1032">type</span></span> |<span data-ttu-id="21f3d-1033">Type özelliği ayarlanmalıdır: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="21f3d-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="21f3d-1034">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1034">Yes</span></span> |
| <span data-ttu-id="21f3d-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="21f3d-1035">sasUri</span></span> |<span data-ttu-id="21f3d-1036">Blob, kapsayıcı ya da tablo gibi Azure Storage kaynakları için paylaşılan erişim imzası URI belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="21f3d-1037">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1037">Yes</span></span> |

<span data-ttu-id="21f3d-1038">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="21f3d-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="21f3d-1039">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1040">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1040">Dataset</span></span>
<span data-ttu-id="21f3d-1041">Bir Azure Table veri kümesini tanımlamak için **türü** için veri kümesinin **AzureTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1042">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1042">Property</span></span> | <span data-ttu-id="21f3d-1043">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1043">Description</span></span> | <span data-ttu-id="21f3d-1044">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1045">tableName</span></span> |<span data-ttu-id="21f3d-1046">Bağlantılı hizmet başvurduğu Azure tablo veritabanı örneğinde tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="21f3d-1047">Evet.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1047">Yes.</span></span> <span data-ttu-id="21f3d-1048">Bir tableName bir azureTableSourceQuery belirtildiğinde, tablodaki tüm kayıtları hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="21f3d-1049">Bir azureTableSourceQuery de belirtilirse, sorgu karşılayan tablodaki kayıtları hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1050">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1051">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="21f3d-1052">Kopya etkinliği Azure tablo kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1053">Azure tablo depolamasından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **AzureTableSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1054">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1054">Property</span></span> | <span data-ttu-id="21f3d-1055">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1055">Description</span></span> | <span data-ttu-id="21f3d-1056">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1056">Allowed values</span></span> | <span data-ttu-id="21f3d-1057">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1058">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="21f3d-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="21f3d-1059">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1060">Azure tablo sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1060">Azure table query string.</span></span> <span data-ttu-id="21f3d-1061">Sonraki bölümdeki örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1061">See examples in the next section.</span></span> |<span data-ttu-id="21f3d-1062">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1062">No.</span></span> <span data-ttu-id="21f3d-1063">Bir tableName bir azureTableSourceQuery belirtildiğinde, tablodaki tüm kayıtları hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="21f3d-1064">Bir azureTableSourceQuery de belirtilirse, sorgu karşılayan tablodaki kayıtları hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="21f3d-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="21f3d-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="21f3d-1066">Swallow tablosunun özel durum var olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="21f3d-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="21f3d-1067">TRUE</span></span><br/><span data-ttu-id="21f3d-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="21f3d-1068">FALSE</span></span> |<span data-ttu-id="21f3d-1069">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1070">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-1071">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="21f3d-1072">Kopya etkinliği Azure tablo havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-1073">Azure Table depolama alanına veri kopyalıyorsanız ayarlamak **Havuz türü** kopyalama etkinliği **AzureTableSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-1074">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1074">Property</span></span> | <span data-ttu-id="21f3d-1075">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1075">Description</span></span> | <span data-ttu-id="21f3d-1076">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1076">Allowed values</span></span> | <span data-ttu-id="21f3d-1077">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="21f3d-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="21f3d-1079">Havuzu tarafından kullanılan varsayılan bölüm anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="21f3d-1080">Bir dize değeri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1080">A string value.</span></span> |<span data-ttu-id="21f3d-1081">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1081">No</span></span> |
| <span data-ttu-id="21f3d-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="21f3d-1083">Değerleri bölüm anahtarları olarak kullanılan sütun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="21f3d-1084">Belirtilmezse, AzureTableDefaultPartitionKeyValue bölüm anahtarı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="21f3d-1085">Sütun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1085">A column name.</span></span> |<span data-ttu-id="21f3d-1086">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1086">No</span></span> |
| <span data-ttu-id="21f3d-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="21f3d-1088">Sütun değerleri satır anahtarı olarak kullanılan sütun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="21f3d-1089">Belirtilmezse, her satır için bir GUID kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="21f3d-1090">Sütun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1090">A column name.</span></span> |<span data-ttu-id="21f3d-1091">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1091">No</span></span> |
| <span data-ttu-id="21f3d-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1092">azureTableInsertType</span></span> |<span data-ttu-id="21f3d-1093">Azure tabloya veri ekleme modu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="21f3d-1094">Bu özellik, var olan satırları eşleşen bölüm ve satır anahtarlarla çıkış tablosuna birleştirilmiş veya değiştirilmesi değerlerine sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="21f3d-1095">Bu ayarları (birleştirme ve Değiştir) nasıl çalıştığı hakkında bilgi edinmek için [ekleme veya birleştirme varlık](https://msdn.microsoft.com/library/azure/hh452241.aspx) ve [ekleme veya değiştirme varlık](https://msdn.microsoft.com/library/azure/hh452242.aspx) Konular.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="21f3d-1096">Bu ayar, tablo düzeyinde değil satır düzeyinde uygulanır ve girdide var olmayan satır çıkış tablosuna hiçbiri seçeneği siler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="21f3d-1097">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1097">merge (default)</span></span><br/><span data-ttu-id="21f3d-1098">Değiştir</span><span class="sxs-lookup"><span data-stu-id="21f3d-1098">replace</span></span> |<span data-ttu-id="21f3d-1099">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1099">No</span></span> |
| <span data-ttu-id="21f3d-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1100">writeBatchSize</span></span> |<span data-ttu-id="21f3d-1101">WriteBatchSize veya writeBatchTimeout gelindiğinde veri Azure tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="21f3d-1102">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1102">Integer (number of rows)</span></span> |<span data-ttu-id="21f3d-1103">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="21f3d-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-1104">writeBatchTimeout</span></span> |<span data-ttu-id="21f3d-1105">WriteBatchSize veya writeBatchTimeout gelindiğinde veri Azure tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="21f3d-1106">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-1106">timespan</span></span><br/><br/><span data-ttu-id="21f3d-1107">Örnek: "00: 20:00" (20 dakika)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="21f3d-1108">Hayır (depolama İstemcisi varsayılan zaman aşımı için varsayılan değer 90 saniye)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1109">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="21f3d-1110">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="21f3d-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="21f3d-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1112">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1112">Linked service</span></span>
<span data-ttu-id="21f3d-1113">Bağlantılı hizmetinin bir Amazon Redshift tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AmazonRedshift**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1114">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1114">Property</span></span> | <span data-ttu-id="21f3d-1115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1115">Description</span></span> | <span data-ttu-id="21f3d-1116">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1117">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1117">server</span></span> |<span data-ttu-id="21f3d-1118">IP adresi veya ana bilgisayar Amazon Redshift sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="21f3d-1119">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1119">Yes</span></span> |
| <span data-ttu-id="21f3d-1120">port</span><span class="sxs-lookup"><span data-stu-id="21f3d-1120">port</span></span> |<span data-ttu-id="21f3d-1121">İstemci bağlantılarını dinlemek için Amazon Redshift sunucunun kullandığı TCP bağlantı noktası numarası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="21f3d-1122">Hayır, varsayılan değer: 5439</span><span class="sxs-lookup"><span data-stu-id="21f3d-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="21f3d-1123">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1123">database</span></span> |<span data-ttu-id="21f3d-1124">Amazon Redshift veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="21f3d-1125">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1125">Yes</span></span> |
| <span data-ttu-id="21f3d-1126">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1126">username</span></span> |<span data-ttu-id="21f3d-1127">Veritabanına erişimi olan kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="21f3d-1128">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1128">Yes</span></span> |
| <span data-ttu-id="21f3d-1129">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1129">password</span></span> |<span data-ttu-id="21f3d-1130">Kullanıcı hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1130">Password for the user account.</span></span> |<span data-ttu-id="21f3d-1131">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1132">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="21f3d-1133">Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1134">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1134">Dataset</span></span>
<span data-ttu-id="21f3d-1135">Bir Amazon Redshift veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1136">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1136">Property</span></span> | <span data-ttu-id="21f3d-1137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1137">Description</span></span> | <span data-ttu-id="21f3d-1138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1139">tableName</span></span> |<span data-ttu-id="21f3d-1140">Amazon Redshift veritabanında bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="21f3d-1141">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="21f3d-1142">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="21f3d-1143">Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1144">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="21f3d-1145">Amazon Redshift veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1146">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1146">Property</span></span> | <span data-ttu-id="21f3d-1147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1147">Description</span></span> | <span data-ttu-id="21f3d-1148">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1148">Allowed values</span></span> | <span data-ttu-id="21f3d-1149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1150">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1150">query</span></span> |<span data-ttu-id="21f3d-1151">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1152">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1152">SQL query string.</span></span> <span data-ttu-id="21f3d-1153">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-1154">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1155">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="21f3d-1156">Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="21f3d-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="21f3d-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1158">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1158">Linked service</span></span>
<span data-ttu-id="21f3d-1159">Bağlantılı hizmetinin bir IBM DB2 tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OnPremisesDB2**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1160">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1160">Property</span></span> | <span data-ttu-id="21f3d-1161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1161">Description</span></span> | <span data-ttu-id="21f3d-1162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1163">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1163">server</span></span> |<span data-ttu-id="21f3d-1164">DB2 sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="21f3d-1165">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1165">Yes</span></span> |
| <span data-ttu-id="21f3d-1166">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1166">database</span></span> |<span data-ttu-id="21f3d-1167">DB2 veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="21f3d-1168">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1168">Yes</span></span> |
| <span data-ttu-id="21f3d-1169">Şema</span><span class="sxs-lookup"><span data-stu-id="21f3d-1169">schema</span></span> |<span data-ttu-id="21f3d-1170">Veritabanı şemasında adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1170">Name of the schema in the database.</span></span> <span data-ttu-id="21f3d-1171">Şema adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="21f3d-1172">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1172">No</span></span> |
| <span data-ttu-id="21f3d-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1173">authenticationType</span></span> |<span data-ttu-id="21f3d-1174">DB2 veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="21f3d-1175">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21f3d-1176">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1176">Yes</span></span> |
| <span data-ttu-id="21f3d-1177">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1177">username</span></span> |<span data-ttu-id="21f3d-1178">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="21f3d-1179">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1179">No</span></span> |
| <span data-ttu-id="21f3d-1180">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1180">password</span></span> |<span data-ttu-id="21f3d-1181">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-1182">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1182">No</span></span> |
| <span data-ttu-id="21f3d-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1183">gatewayName</span></span> |<span data-ttu-id="21f3d-1184">Data Factory hizmetinin şirket içi DB2 veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="21f3d-1185">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1186">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="21f3d-1187">Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1188">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1188">Dataset</span></span>
<span data-ttu-id="21f3d-1189">Bir DB2 veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="21f3d-1190">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1190">Property</span></span> | <span data-ttu-id="21f3d-1191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1191">Description</span></span> | <span data-ttu-id="21f3d-1192">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1193">tableName</span></span> |<span data-ttu-id="21f3d-1194">DB2 veritabanına örneğinde bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="21f3d-1195">TableName büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="21f3d-1196">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="21f3d-1197">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1198">Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1199">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1200">IBM DB2'den veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1201">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1201">Property</span></span> | <span data-ttu-id="21f3d-1202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1202">Description</span></span> | <span data-ttu-id="21f3d-1203">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1203">Allowed values</span></span> | <span data-ttu-id="21f3d-1204">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1205">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1205">query</span></span> |<span data-ttu-id="21f3d-1206">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1207">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1207">SQL query string.</span></span> <span data-ttu-id="21f3d-1208">Örneğin: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="21f3d-1209">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1210">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="21f3d-1211">Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="21f3d-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="21f3d-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1213">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1213">Linked service</span></span>
<span data-ttu-id="21f3d-1214">Bağlantılı hizmetinin bir MySQL tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OnPremisesMySql**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1215">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1215">Property</span></span> | <span data-ttu-id="21f3d-1216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1216">Description</span></span> | <span data-ttu-id="21f3d-1217">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1218">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1218">server</span></span> |<span data-ttu-id="21f3d-1219">MySQL sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="21f3d-1220">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1220">Yes</span></span> |
| <span data-ttu-id="21f3d-1221">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1221">database</span></span> |<span data-ttu-id="21f3d-1222">MySQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="21f3d-1223">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1223">Yes</span></span> |
| <span data-ttu-id="21f3d-1224">Şema</span><span class="sxs-lookup"><span data-stu-id="21f3d-1224">schema</span></span> |<span data-ttu-id="21f3d-1225">Veritabanı şemasında adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="21f3d-1226">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1226">No</span></span> |
| <span data-ttu-id="21f3d-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1227">authenticationType</span></span> |<span data-ttu-id="21f3d-1228">MySQL veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="21f3d-1229">Olası değerler şunlardır: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="21f3d-1230">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1230">Yes</span></span> |
| <span data-ttu-id="21f3d-1231">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1231">username</span></span> |<span data-ttu-id="21f3d-1232">MySQL veritabanına bağlanmak için kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="21f3d-1233">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1233">Yes</span></span> |
| <span data-ttu-id="21f3d-1234">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1234">password</span></span> |<span data-ttu-id="21f3d-1235">Belirttiğiniz kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="21f3d-1236">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1236">Yes</span></span> |
| <span data-ttu-id="21f3d-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1237">gatewayName</span></span> |<span data-ttu-id="21f3d-1238">Data Factory hizmetinin şirket içi MySQL veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="21f3d-1239">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1240">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="21f3d-1241">Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1242">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1242">Dataset</span></span>
<span data-ttu-id="21f3d-1243">Bir MySQL veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1244">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1244">Property</span></span> | <span data-ttu-id="21f3d-1245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1245">Description</span></span> | <span data-ttu-id="21f3d-1246">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1247">tableName</span></span> |<span data-ttu-id="21f3d-1248">MySQL veritabanı örneğinde bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="21f3d-1249">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1250">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="21f3d-1251">Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1252">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1253">Bir MySQL veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1254">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1254">Property</span></span> | <span data-ttu-id="21f3d-1255">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1255">Description</span></span> | <span data-ttu-id="21f3d-1256">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1256">Allowed values</span></span> | <span data-ttu-id="21f3d-1257">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1258">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1258">query</span></span> |<span data-ttu-id="21f3d-1259">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1260">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1260">SQL query string.</span></span> <span data-ttu-id="21f3d-1261">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-1262">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="21f3d-1263">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1264">Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="21f3d-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="21f3d-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-1266">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1266">Linked service</span></span>
<span data-ttu-id="21f3d-1267">Bağlantılı hizmetinin bir Oracle tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OnPremisesOracle**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1268">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1268">Property</span></span> | <span data-ttu-id="21f3d-1269">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1269">Description</span></span> | <span data-ttu-id="21f3d-1270">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1271">driverType</span></span> | <span data-ttu-id="21f3d-1272">Hangi sürücünün/Oracle veritabanına veri kopyalamak için kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="21f3d-1273">İzin verilen değerler **Microsoft** veya **ODP** (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="21f3d-1274">Bkz: [desteklenen sürümü ve yükleme](#supported-versions-and-installation) sürücü ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="21f3d-1275">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1275">No</span></span> |
| <span data-ttu-id="21f3d-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-1276">connectionString</span></span> | <span data-ttu-id="21f3d-1277">ConnectionString özelliği için Oracle veritabanı örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="21f3d-1278">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1278">Yes</span></span> |
| <span data-ttu-id="21f3d-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1279">gatewayName</span></span> | <span data-ttu-id="21f3d-1280">Ağ geçidinin adı, şirket içi Oracle sunucusuna bağlanmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="21f3d-1281">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1282">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="21f3d-1283">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1284">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1284">Dataset</span></span>
<span data-ttu-id="21f3d-1285">Bir Oracle veri kümesini tanımlamak için **türü** için veri kümesinin **OracleTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1286">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1286">Property</span></span> | <span data-ttu-id="21f3d-1287">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1287">Description</span></span> | <span data-ttu-id="21f3d-1288">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1289">tableName</span></span> |<span data-ttu-id="21f3d-1290">Oracle veritabanında bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="21f3d-1291">Hayır (varsa **oracleReaderQuery** , **OracleSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1292">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="21f3d-1293">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="21f3d-1294">Kopyalama etkinliği Oracle kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1295">Bir Oracle veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **OracleSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1296">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1296">Property</span></span> | <span data-ttu-id="21f3d-1297">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1297">Description</span></span> | <span data-ttu-id="21f3d-1298">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1298">Allowed values</span></span> | <span data-ttu-id="21f3d-1299">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="21f3d-1300">oracleReaderQuery</span></span> |<span data-ttu-id="21f3d-1301">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1302">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1302">SQL query string.</span></span> <span data-ttu-id="21f3d-1303">Örneğin, `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="21f3d-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="21f3d-1304">Belirtilmezse, yürütülen SQL deyimi:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="21f3d-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="21f3d-1305">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1306">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-1307">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="21f3d-1308">Kopyalama etkinliği Oracle havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-1309">Am Oracle veritabanına veri kopyalamak istiyorsanız, ayarlayın **Havuz türü** kopyalama etkinliği **OracleSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-1310">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1310">Property</span></span> | <span data-ttu-id="21f3d-1311">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1311">Description</span></span> | <span data-ttu-id="21f3d-1312">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1312">Allowed values</span></span> | <span data-ttu-id="21f3d-1313">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-1314">writeBatchTimeout</span></span> |<span data-ttu-id="21f3d-1315">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="21f3d-1316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-1316">timespan</span></span><br/><br/> <span data-ttu-id="21f3d-1317">Örnek: 00:30:00 (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="21f3d-1318">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1318">No</span></span> |
| <span data-ttu-id="21f3d-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1319">writeBatchSize</span></span> |<span data-ttu-id="21f3d-1320">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="21f3d-1321">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1321">Integer (number of rows)</span></span> |<span data-ttu-id="21f3d-1322">Hayır (varsayılan: 100)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1322">No (default: 100)</span></span> |
| <span data-ttu-id="21f3d-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="21f3d-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="21f3d-1324">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="21f3d-1325">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1325">A query statement.</span></span> |<span data-ttu-id="21f3d-1326">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1326">No</span></span> |
| <span data-ttu-id="21f3d-1327">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="21f3d-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="21f3d-1328">Kopyalama etkinliği'nin ne zaman yeniden çalıştırılacağını belirli bir dilim verileri temizlemek için kullanılan otomatik dilim tanımlayıcı doldurmak için sütun adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="21f3d-1329">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="21f3d-1330">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1331">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="21f3d-1332">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="21f3d-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="21f3d-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1334">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1334">Linked service</span></span>
<span data-ttu-id="21f3d-1335">Bağlantılı hizmetinin bir PostgreSQL tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OnPremisesPostgreSql**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1336">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1336">Property</span></span> | <span data-ttu-id="21f3d-1337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1337">Description</span></span> | <span data-ttu-id="21f3d-1338">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1339">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1339">server</span></span> |<span data-ttu-id="21f3d-1340">PostgreSQL sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="21f3d-1341">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1341">Yes</span></span> |
| <span data-ttu-id="21f3d-1342">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1342">database</span></span> |<span data-ttu-id="21f3d-1343">PostgreSQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="21f3d-1344">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1344">Yes</span></span> |
| <span data-ttu-id="21f3d-1345">Şema</span><span class="sxs-lookup"><span data-stu-id="21f3d-1345">schema</span></span> |<span data-ttu-id="21f3d-1346">Veritabanı şemasında adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1346">Name of the schema in the database.</span></span> <span data-ttu-id="21f3d-1347">Şema adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="21f3d-1348">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1348">No</span></span> |
| <span data-ttu-id="21f3d-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1349">authenticationType</span></span> |<span data-ttu-id="21f3d-1350">PostgreSQL veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="21f3d-1351">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21f3d-1352">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1352">Yes</span></span> |
| <span data-ttu-id="21f3d-1353">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1353">username</span></span> |<span data-ttu-id="21f3d-1354">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="21f3d-1355">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1355">No</span></span> |
| <span data-ttu-id="21f3d-1356">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1356">password</span></span> |<span data-ttu-id="21f3d-1357">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-1358">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1358">No</span></span> |
| <span data-ttu-id="21f3d-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1359">gatewayName</span></span> |<span data-ttu-id="21f3d-1360">Data Factory hizmetinin şirket içi PostgreSQL veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="21f3d-1361">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1362">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="21f3d-1363">Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1364">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1364">Dataset</span></span>
<span data-ttu-id="21f3d-1365">Bir PostgreSQL veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1366">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1366">Property</span></span> | <span data-ttu-id="21f3d-1367">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1367">Description</span></span> | <span data-ttu-id="21f3d-1368">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1369">tableName</span></span> |<span data-ttu-id="21f3d-1370">Bağlantılı hizmet başvurduğu PostgreSQL veritabanı örneğinde tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="21f3d-1371">TableName büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="21f3d-1372">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1373">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="21f3d-1374">Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1375">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1376">Bir PostgreSQL veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1377">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1377">Property</span></span> | <span data-ttu-id="21f3d-1378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1378">Description</span></span> | <span data-ttu-id="21f3d-1379">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1379">Allowed values</span></span> | <span data-ttu-id="21f3d-1380">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1381">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1381">query</span></span> |<span data-ttu-id="21f3d-1382">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1383">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1383">SQL query string.</span></span> <span data-ttu-id="21f3d-1384">Örneğin: "sorgu": "seçin * gelen \"MySchema\".\" MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="21f3d-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="21f3d-1385">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1386">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1387">Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="21f3d-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="21f3d-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-1389">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1389">Linked service</span></span>
<span data-ttu-id="21f3d-1390">Bağlantılı hizmetinin SAP Business Warehouse (BW) tanımlamak için Ayarla **türü** bağlantılı hizmetinin **SapBw**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="21f3d-1391">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1391">Property</span></span> | <span data-ttu-id="21f3d-1392">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1392">Description</span></span> | <span data-ttu-id="21f3d-1393">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1393">Allowed values</span></span> | <span data-ttu-id="21f3d-1394">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="21f3d-1395">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1395">server</span></span> | <span data-ttu-id="21f3d-1396">SAP BW örneği bulunduğu sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="21f3d-1397">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1397">string</span></span> | <span data-ttu-id="21f3d-1398">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1398">Yes</span></span>
<span data-ttu-id="21f3d-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="21f3d-1399">systemNumber</span></span> | <span data-ttu-id="21f3d-1400">SAP BW sisteminin sistem numarası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="21f3d-1401">Bir dize olarak gösterilen iki basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="21f3d-1402">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1402">Yes</span></span>
<span data-ttu-id="21f3d-1403">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-1403">clientId</span></span> | <span data-ttu-id="21f3d-1404">SAP W sistem istemcisinde istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="21f3d-1405">Bir dize olarak gösterilen üç basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="21f3d-1406">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1406">Yes</span></span>
<span data-ttu-id="21f3d-1407">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1407">username</span></span> | <span data-ttu-id="21f3d-1408">SAP sunucusuna erişimi olan kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="21f3d-1409">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1409">string</span></span> | <span data-ttu-id="21f3d-1410">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1410">Yes</span></span>
<span data-ttu-id="21f3d-1411">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1411">password</span></span> | <span data-ttu-id="21f3d-1412">Kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1412">Password for the user.</span></span> | <span data-ttu-id="21f3d-1413">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1413">string</span></span> | <span data-ttu-id="21f3d-1414">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1414">Yes</span></span>
<span data-ttu-id="21f3d-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1415">gatewayName</span></span> | <span data-ttu-id="21f3d-1416">Data Factory hizmetinin şirket içi SAP BW örneğine bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="21f3d-1417">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1417">string</span></span> | <span data-ttu-id="21f3d-1418">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1418">Yes</span></span>
<span data-ttu-id="21f3d-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-1419">encryptedCredential</span></span> | <span data-ttu-id="21f3d-1420">Şifrelenmiş kimlik bilgileri dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1420">The encrypted credential string.</span></span> | <span data-ttu-id="21f3d-1421">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1421">string</span></span> | <span data-ttu-id="21f3d-1422">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-1423">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="21f3d-1424">Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1425">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1425">Dataset</span></span>
<span data-ttu-id="21f3d-1426">SAP BW veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="21f3d-1427">SAP BW veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="21f3d-1428">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="21f3d-1429">Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1430">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1431">SAP Business Warehouse veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1432">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1432">Property</span></span> | <span data-ttu-id="21f3d-1433">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1433">Description</span></span> | <span data-ttu-id="21f3d-1434">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1434">Allowed values</span></span> | <span data-ttu-id="21f3d-1435">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1436">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1436">query</span></span> | <span data-ttu-id="21f3d-1437">SAP BW örneğinden verileri okumak için MDX Sorgusu belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="21f3d-1438">MDX Sorgusu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1438">MDX query.</span></span> | <span data-ttu-id="21f3d-1439">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1440">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1441">Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="21f3d-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="21f3d-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1443">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1443">Linked service</span></span>
<span data-ttu-id="21f3d-1444">Bağlantılı hizmetinin SAP HANA tanımlamak için Ayarla **türü** bağlantılı hizmetinin **SapHana**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="21f3d-1445">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1445">Property</span></span> | <span data-ttu-id="21f3d-1446">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1446">Description</span></span> | <span data-ttu-id="21f3d-1447">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1447">Allowed values</span></span> | <span data-ttu-id="21f3d-1448">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="21f3d-1449">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1449">server</span></span> | <span data-ttu-id="21f3d-1450">SAP HANA örneği bulunduğu sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="21f3d-1451">Sunucunuz özelleştirilmiş bir bağlantı noktası kullanıyorsa belirtin `server:port`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="21f3d-1452">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1452">string</span></span> | <span data-ttu-id="21f3d-1453">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1453">Yes</span></span>
<span data-ttu-id="21f3d-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1454">authenticationType</span></span> | <span data-ttu-id="21f3d-1455">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1455">Type of authentication.</span></span> | <span data-ttu-id="21f3d-1456">Dize.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1456">string.</span></span> <span data-ttu-id="21f3d-1457">"Temel" veya "Windows"</span><span class="sxs-lookup"><span data-stu-id="21f3d-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="21f3d-1458">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1458">Yes</span></span> 
<span data-ttu-id="21f3d-1459">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1459">username</span></span> | <span data-ttu-id="21f3d-1460">SAP sunucusuna erişimi olan kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="21f3d-1461">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1461">string</span></span> | <span data-ttu-id="21f3d-1462">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1462">Yes</span></span>
<span data-ttu-id="21f3d-1463">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1463">password</span></span> | <span data-ttu-id="21f3d-1464">Kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1464">Password for the user.</span></span> | <span data-ttu-id="21f3d-1465">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1465">string</span></span> | <span data-ttu-id="21f3d-1466">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1466">Yes</span></span>
<span data-ttu-id="21f3d-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1467">gatewayName</span></span> | <span data-ttu-id="21f3d-1468">Data Factory hizmetinin şirket içi SAP HANA örneğine bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="21f3d-1469">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1469">string</span></span> | <span data-ttu-id="21f3d-1470">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1470">Yes</span></span>
<span data-ttu-id="21f3d-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-1471">encryptedCredential</span></span> | <span data-ttu-id="21f3d-1472">Şifrelenmiş kimlik bilgileri dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1472">The encrypted credential string.</span></span> | <span data-ttu-id="21f3d-1473">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1473">string</span></span> | <span data-ttu-id="21f3d-1474">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-1475">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="21f3d-1476">Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="21f3d-1477">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1477">Dataset</span></span>
<span data-ttu-id="21f3d-1478">SAP HANA veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="21f3d-1479">SAP HANA veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="21f3d-1480">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="21f3d-1481">Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1482">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1483">SAP HANA veri deposundan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1484">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1484">Property</span></span> | <span data-ttu-id="21f3d-1485">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1485">Description</span></span> | <span data-ttu-id="21f3d-1486">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1486">Allowed values</span></span> | <span data-ttu-id="21f3d-1487">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1488">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1488">query</span></span> | <span data-ttu-id="21f3d-1489">SAP HANA örneğinden verileri okumak için SQL sorgusu belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="21f3d-1490">SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1490">SQL query.</span></span> | <span data-ttu-id="21f3d-1491">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="21f3d-1492">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1493">Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="21f3d-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="21f3d-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1495">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1495">Linked service</span></span>
<span data-ttu-id="21f3d-1496">Bağlı hizmet türü oluşturma **OnPremisesSqlServer** bir şirket içi SQL Server veritabanını data factory'ye bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="21f3d-1497">Aşağıdaki tabloda şirket içi SQL Server bağlantılı hizmete özgü JSON öğeleri açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="21f3d-1498">Aşağıdaki tabloda, SQL Server bağlantılı hizmete özgü JSON öğeleri açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="21f3d-1499">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1499">Property</span></span> | <span data-ttu-id="21f3d-1500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1500">Description</span></span> | <span data-ttu-id="21f3d-1501">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1502">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-1502">type</span></span> |<span data-ttu-id="21f3d-1503">Type özelliği ayarlanmalıdır: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="21f3d-1504">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1504">Yes</span></span> |
| <span data-ttu-id="21f3d-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-1505">connectionString</span></span> |<span data-ttu-id="21f3d-1506">SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak şirket içi SQL Server veritabanına bağlanmak için gereken connectionString bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="21f3d-1507">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1507">Yes</span></span> |
| <span data-ttu-id="21f3d-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1508">gatewayName</span></span> |<span data-ttu-id="21f3d-1509">Data Factory hizmetinin şirket içi SQL Server veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="21f3d-1510">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1510">Yes</span></span> |
| <span data-ttu-id="21f3d-1511">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1511">username</span></span> |<span data-ttu-id="21f3d-1512">Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="21f3d-1513">Örnek: **domainname\\kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="21f3d-1514">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1514">No</span></span> |
| <span data-ttu-id="21f3d-1515">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1515">password</span></span> |<span data-ttu-id="21f3d-1516">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-1517">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1517">No</span></span> |

<span data-ttu-id="21f3d-1518">Kimlik bilgilerini kullanarak şifreleyebilirsiniz **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları aşağıdaki örnekte gösterildiği gibi bağlantı dizesini kullanın (**EncryptedCredential** özellik):</span><span class="sxs-lookup"><span data-stu-id="21f3d-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="21f3d-1519">Örnek: SQL kimlik doğrulaması kullanmak için JSON</span><span class="sxs-lookup"><span data-stu-id="21f3d-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="21f3d-1520">Örnek: JSON'ı Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="21f3d-1521">Kullanıcı adı ve parolası belirtilmişse, ağ geçidi bunları şirket içi SQL Server veritabanına bağlanmak için belirtilen kullanıcı hesabının kimliğine bürün kullanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="21f3d-1522">Aksi takdirde, ağ geçidi SQL Server Ağ Geçidi (kendi başlangıç hesabı) güvenlik bağlamı ile doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="21f3d-1523">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1524">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1524">Dataset</span></span>
<span data-ttu-id="21f3d-1525">Bir SQL Server veri kümesini tanımlamak için **türü** için veri kümesinin **SqlServerTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1526">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1526">Property</span></span> | <span data-ttu-id="21f3d-1527">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1527">Description</span></span> | <span data-ttu-id="21f3d-1528">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1529">tableName</span></span> |<span data-ttu-id="21f3d-1530">Tablo veya Görünüm hizmeti bağlı SQL Server veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="21f3d-1531">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1532">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1533">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="21f3d-1534">Kopyalama etkinliğinde SQL kaynağı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1535">Bir SQL Server veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **SqlSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1536">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1536">Property</span></span> | <span data-ttu-id="21f3d-1537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1537">Description</span></span> | <span data-ttu-id="21f3d-1538">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1538">Allowed values</span></span> | <span data-ttu-id="21f3d-1539">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1540">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="21f3d-1540">sqlReaderQuery</span></span> |<span data-ttu-id="21f3d-1541">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1542">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1542">SQL query string.</span></span> <span data-ttu-id="21f3d-1543">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="21f3d-1544">Birden çok tablo girdi veri kümesi tarafından başvurulan veritabanından başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="21f3d-1545">Belirtilmezse, yürütülen SQL deyimi: MyTable arasından seçin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="21f3d-1546">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1546">No</span></span> |
| <span data-ttu-id="21f3d-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="21f3d-1548">Kaynak tablodan veri okuyan saklı yordamın adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="21f3d-1549">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="21f3d-1550">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1550">No</span></span> |
| <span data-ttu-id="21f3d-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-1551">storedProcedureParameters</span></span> |<span data-ttu-id="21f3d-1552">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="21f3d-1553">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1553">Name/value pairs.</span></span> <span data-ttu-id="21f3d-1554">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="21f3d-1555">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1555">No</span></span> |

<span data-ttu-id="21f3d-1556">Varsa **sqlReaderQuery** belirtilen SqlSource için kopyalama etkinliği veri almak için SQL Server veritabanı kaynağında bu sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="21f3d-1557">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="21f3d-1558">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz yapısı bölümünde tanımlanan sütunları SQL Server veritabanına karşı çalıştırmak için seçme sorgusu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="21f3d-1559">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="21f3d-1560">Kullandığınızda **sqlReaderStoredProcedureName**, yine de için bir değer belirtmeniz gerekiyorsa **tableName** JSON veri kümesi bir özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="21f3d-1561">Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="21f3d-1562">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-1563">Bu örnekte, **sqlReaderQuery** SqlSource için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="21f3d-1564">Kopyalama etkinliği bu sorguyu veri almak için SQL Server veritabanı kaynağına karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="21f3d-1565">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="21f3d-1566">SqlReaderQuery girdi veri kümesi tarafından başvurulan veritabanına birden çok tablolarına başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="21f3d-1567">Yalnızca veri kümesi'nin tableName typeProperty ayarlamak tabloya sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="21f3d-1568">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz yapısı bölümünde tanımlanan sütunları SQL Server veritabanına karşı çalıştırmak için seçme sorgusu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="21f3d-1569">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="21f3d-1570">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="21f3d-1571">Kopyalama etkinliği SQL havuzunda</span><span class="sxs-lookup"><span data-stu-id="21f3d-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-1572">Bir SQL Server veritabanına veri kopyalamak istiyorsanız, ayarlayın **Havuz türü** kopyalama etkinliği **SqlSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-1573">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1573">Property</span></span> | <span data-ttu-id="21f3d-1574">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1574">Description</span></span> | <span data-ttu-id="21f3d-1575">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1575">Allowed values</span></span> | <span data-ttu-id="21f3d-1576">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-1577">writeBatchTimeout</span></span> |<span data-ttu-id="21f3d-1578">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="21f3d-1579">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21f3d-1579">timespan</span></span><br/><br/> <span data-ttu-id="21f3d-1580">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="21f3d-1581">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1581">No</span></span> |
| <span data-ttu-id="21f3d-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1582">writeBatchSize</span></span> |<span data-ttu-id="21f3d-1583">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="21f3d-1584">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1584">Integer (number of rows)</span></span> |<span data-ttu-id="21f3d-1585">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="21f3d-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="21f3d-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="21f3d-1587">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği sorgusunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="21f3d-1588">Daha fazla bilgi için bkz: [Yinelenebilirlik](#repeatability-during-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="21f3d-1589">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1589">A query statement.</span></span> |<span data-ttu-id="21f3d-1590">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1590">No</span></span> |
| <span data-ttu-id="21f3d-1591">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="21f3d-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="21f3d-1592">Kopyalama etkinliği'nin ne zaman yeniden çalıştırılacağını belirli bir dilim verileri temizlemek için kullanılan otomatik dilim tanımlayıcı doldurmak için sütun adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="21f3d-1593">Daha fazla bilgi için bkz: [Yinelenebilirlik](#repeatability-during-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="21f3d-1594">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="21f3d-1595">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1595">No</span></span> |
| <span data-ttu-id="21f3d-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="21f3d-1597">Saklı yordam adı hedef tabloda bu upserts (güncelleştirmeler/ekler) verileri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="21f3d-1598">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="21f3d-1599">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1599">No</span></span> |
| <span data-ttu-id="21f3d-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-1600">storedProcedureParameters</span></span> |<span data-ttu-id="21f3d-1601">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="21f3d-1602">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1602">Name/value pairs.</span></span> <span data-ttu-id="21f3d-1603">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="21f3d-1604">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1604">No</span></span> |
| <span data-ttu-id="21f3d-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1605">sqlWriterTableType</span></span> |<span data-ttu-id="21f3d-1606">Saklı yordam, kullanılacak tablo türü adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="21f3d-1607">Kopyalama etkinliği taşınan veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="21f3d-1608">Saklı yordam kodu ardından var olan verilerle kopyalanan verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="21f3d-1609">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1609">A table type name.</span></span> |<span data-ttu-id="21f3d-1610">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1611">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1611">Example</span></span>
<span data-ttu-id="21f3d-1612">Ardışık Düzen bu girdi ve çıktı veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="21f3d-1613">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **BlobSource** ve **havuz** türü ayarlanmış **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-1614">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="21f3d-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="21f3d-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1616">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1616">Linked service</span></span>
<span data-ttu-id="21f3d-1617">Bir Sybase tanımlamak için hizmeti bağlı, Ayarla **türü** bağlantılı hizmetinin **OnPremisesSybase**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1618">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1618">Property</span></span> | <span data-ttu-id="21f3d-1619">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1619">Description</span></span> | <span data-ttu-id="21f3d-1620">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1621">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1621">server</span></span> |<span data-ttu-id="21f3d-1622">Sybase sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="21f3d-1623">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1623">Yes</span></span> |
| <span data-ttu-id="21f3d-1624">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1624">database</span></span> |<span data-ttu-id="21f3d-1625">Sybase veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="21f3d-1626">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1626">Yes</span></span> |
| <span data-ttu-id="21f3d-1627">Şema</span><span class="sxs-lookup"><span data-stu-id="21f3d-1627">schema</span></span> |<span data-ttu-id="21f3d-1628">Veritabanı şemasında adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="21f3d-1629">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1629">No</span></span> |
| <span data-ttu-id="21f3d-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1630">authenticationType</span></span> |<span data-ttu-id="21f3d-1631">Sybase veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="21f3d-1632">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21f3d-1633">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1633">Yes</span></span> |
| <span data-ttu-id="21f3d-1634">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1634">username</span></span> |<span data-ttu-id="21f3d-1635">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="21f3d-1636">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1636">No</span></span> |
| <span data-ttu-id="21f3d-1637">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1637">password</span></span> |<span data-ttu-id="21f3d-1638">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-1639">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1639">No</span></span> |
| <span data-ttu-id="21f3d-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1640">gatewayName</span></span> |<span data-ttu-id="21f3d-1641">Data Factory hizmetinin şirket içi Sybase veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="21f3d-1642">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1643">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="21f3d-1644">Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1645">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1645">Dataset</span></span>
<span data-ttu-id="21f3d-1646">Bir Sybase veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1647">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1647">Property</span></span> | <span data-ttu-id="21f3d-1648">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1648">Description</span></span> | <span data-ttu-id="21f3d-1649">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1650">tableName</span></span> |<span data-ttu-id="21f3d-1651">Sybase veritabanı örneğinde bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="21f3d-1652">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1653">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1654">Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1655">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1656">Bir Sybase veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1657">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1657">Property</span></span> | <span data-ttu-id="21f3d-1658">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1658">Description</span></span> | <span data-ttu-id="21f3d-1659">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1659">Allowed values</span></span> | <span data-ttu-id="21f3d-1660">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1661">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1661">query</span></span> |<span data-ttu-id="21f3d-1662">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1663">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1663">SQL query string.</span></span> <span data-ttu-id="21f3d-1664">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-1665">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1666">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1667">Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="21f3d-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="21f3d-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1669">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1669">Linked service</span></span>
<span data-ttu-id="21f3d-1670">Bir Teradata tanımlamak için hizmeti bağlı, Ayarla **türü** bağlantılı hizmetinin **OnPremisesTeradata**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1671">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1671">Property</span></span> | <span data-ttu-id="21f3d-1672">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1672">Description</span></span> | <span data-ttu-id="21f3d-1673">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1674">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1674">server</span></span> |<span data-ttu-id="21f3d-1675">Teradata sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="21f3d-1676">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1676">Yes</span></span> |
| <span data-ttu-id="21f3d-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1677">authenticationType</span></span> |<span data-ttu-id="21f3d-1678">Teradata veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="21f3d-1679">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21f3d-1680">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1680">Yes</span></span> |
| <span data-ttu-id="21f3d-1681">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1681">username</span></span> |<span data-ttu-id="21f3d-1682">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="21f3d-1683">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1683">No</span></span> |
| <span data-ttu-id="21f3d-1684">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1684">password</span></span> |<span data-ttu-id="21f3d-1685">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-1686">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1686">No</span></span> |
| <span data-ttu-id="21f3d-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1687">gatewayName</span></span> |<span data-ttu-id="21f3d-1688">Data Factory hizmetinin şirket içi Teradata veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="21f3d-1689">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1690">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="21f3d-1691">Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1692">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1692">Dataset</span></span>
<span data-ttu-id="21f3d-1693">Bir Teradata Blob veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="21f3d-1694">Şu anda Teradata veri kümesi için desteklenen tür özellik yok.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="21f3d-1695">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1696">Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-1697">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1698">Bir Teradata veritabanından veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1699">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1699">Property</span></span> | <span data-ttu-id="21f3d-1700">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1700">Description</span></span> | <span data-ttu-id="21f3d-1701">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1701">Allowed values</span></span> | <span data-ttu-id="21f3d-1702">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1703">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1703">query</span></span> |<span data-ttu-id="21f3d-1704">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1705">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1705">SQL query string.</span></span> <span data-ttu-id="21f3d-1706">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-1707">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1708">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="21f3d-1709">Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="21f3d-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="21f3d-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-1711">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1711">Linked service</span></span>
<span data-ttu-id="21f3d-1712">Bir bağlı Cassandra hizmet tanımlamak için **türü** bağlantılı hizmetinin **OnPremisesCassandra**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1713">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1713">Property</span></span> | <span data-ttu-id="21f3d-1714">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1714">Description</span></span> | <span data-ttu-id="21f3d-1715">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1716">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="21f3d-1716">host</span></span> |<span data-ttu-id="21f3d-1717">Bir veya daha fazla IP adresleri veya ana bilgisayar adlarını Cassandra sunucuları.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="21f3d-1718">IP adreslerini veya aynı anda tüm sunucularına bağlanmak için ana bilgisayar adlarını virgülle ayrılmış listesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="21f3d-1719">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1719">Yes</span></span> |
| <span data-ttu-id="21f3d-1720">port</span><span class="sxs-lookup"><span data-stu-id="21f3d-1720">port</span></span> |<span data-ttu-id="21f3d-1721">İstemci bağlantılarını dinlemek için Cassandra sunucusunun kullandığı TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="21f3d-1722">Hayır, varsayılan değer: 9042</span><span class="sxs-lookup"><span data-stu-id="21f3d-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="21f3d-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1723">authenticationType</span></span> |<span data-ttu-id="21f3d-1724">Basic veya Anonymous</span><span class="sxs-lookup"><span data-stu-id="21f3d-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="21f3d-1725">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1725">Yes</span></span> |
| <span data-ttu-id="21f3d-1726">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1726">username</span></span> |<span data-ttu-id="21f3d-1727">Kullanıcı hesabının kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="21f3d-1728">Evet, authenticationType temel olarak ayarlanmışsa.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="21f3d-1729">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1729">password</span></span> |<span data-ttu-id="21f3d-1730">Kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1730">Specify password for the user account.</span></span> |<span data-ttu-id="21f3d-1731">Evet, authenticationType temel olarak ayarlanmışsa.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="21f3d-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1732">gatewayName</span></span> |<span data-ttu-id="21f3d-1733">Şirket içi Cassandra veritabanına bağlanmak için kullanılan ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="21f3d-1734">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1734">Yes</span></span> |
| <span data-ttu-id="21f3d-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-1735">encryptedCredential</span></span> |<span data-ttu-id="21f3d-1736">Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="21f3d-1737">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1738">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="21f3d-1739">Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-1740">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1740">Dataset</span></span>
<span data-ttu-id="21f3d-1741">Cassandra veri kümesini tanımlamak için **türü** için veri kümesinin **CassandraTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1742">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1742">Property</span></span> | <span data-ttu-id="21f3d-1743">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1743">Description</span></span> | <span data-ttu-id="21f3d-1744">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="21f3d-1745">keyspace</span></span> |<span data-ttu-id="21f3d-1746">Keyspace veya Cassandra veritabanındaki şema adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="21f3d-1747">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="21f3d-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1748">tableName</span></span> |<span data-ttu-id="21f3d-1749">Cassandra veritabanı tablosunun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="21f3d-1750">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1751">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1752">Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="21f3d-1753">Kopyalama etkinliği Cassandra kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1754">Cassandra veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **CassandraSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1755">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1755">Property</span></span> | <span data-ttu-id="21f3d-1756">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1756">Description</span></span> | <span data-ttu-id="21f3d-1757">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1757">Allowed values</span></span> | <span data-ttu-id="21f3d-1758">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1759">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1759">query</span></span> |<span data-ttu-id="21f3d-1760">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1761">SQL-92 sorgusu veya CQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="21f3d-1762">Bkz: [CQL başvuru](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="21f3d-1763">SQL sorgusu kullanırken belirtin **keyspace name.table adı** sorgulamak istediğiniz tabloyu temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="21f3d-1764">Hayır (tableName ve veri kümesi üzerinde keyspace tanımlanmışsa).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="21f3d-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="21f3d-1765">consistencyLevel</span></span> |<span data-ttu-id="21f3d-1766">Tutarlılık düzeyi kaç çoğaltmaları Okuma isteği için veri istemci uygulamasına geri dönmeden önce yanıt vermesi gereken belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="21f3d-1767">Cassandra Okuma isteği karşılamak veriler için çoğaltmaları belirtilen sayısını denetler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="21f3d-1768">BİR, İKİ, ÜÇ, ÇEKİRDEK, TÜMÜ, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="21f3d-1769">Bkz: [veri tutarlılığını yapılandırma](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="21f3d-1770">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1770">No.</span></span> <span data-ttu-id="21f3d-1771">Varsayılan değer biridir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1772">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-1773">Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="21f3d-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="21f3d-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-1775">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1775">Linked service</span></span>
<span data-ttu-id="21f3d-1776">Bağlantılı hizmetinin bir MongoDB tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OnPremisesMongoDB**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1777">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1777">Property</span></span> | <span data-ttu-id="21f3d-1778">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1778">Description</span></span> | <span data-ttu-id="21f3d-1779">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1780">sunucu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1780">server</span></span> |<span data-ttu-id="21f3d-1781">IP adresi veya ana bilgisayar MongoDB sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="21f3d-1782">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1782">Yes</span></span> |
| <span data-ttu-id="21f3d-1783">port</span><span class="sxs-lookup"><span data-stu-id="21f3d-1783">port</span></span> |<span data-ttu-id="21f3d-1784">İstemci bağlantılarını dinlemek için MongoDB sunucusunun kullandığı TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="21f3d-1785">İsteğe bağlı, varsayılan değer: 27017</span><span class="sxs-lookup"><span data-stu-id="21f3d-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="21f3d-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-1786">authenticationType</span></span> |<span data-ttu-id="21f3d-1787">Basic veya Anonymous.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="21f3d-1788">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1788">Yes</span></span> |
| <span data-ttu-id="21f3d-1789">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1789">username</span></span> |<span data-ttu-id="21f3d-1790">MongoDB erişmek için kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="21f3d-1791">Evet (Temel kimlik doğrulaması kullanılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="21f3d-1792">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1792">password</span></span> |<span data-ttu-id="21f3d-1793">Kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1793">Password for the user.</span></span> |<span data-ttu-id="21f3d-1794">Evet (Temel kimlik doğrulaması kullanılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="21f3d-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="21f3d-1795">authSource</span></span> |<span data-ttu-id="21f3d-1796">Kimlik doğrulaması için kimlik bilgilerinizi denetlemek için kullanmak istediğiniz MongoDB veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="21f3d-1797">(Temel kimlik doğrulaması kullanılıyorsa) isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="21f3d-1798">Varsayılan: yönetici hesabı ve databaseName özelliği kullanılarak belirtilen veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="21f3d-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1799">databaseName</span></span> |<span data-ttu-id="21f3d-1800">Erişmek istediğiniz MongoDB veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="21f3d-1801">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1801">Yes</span></span> |
| <span data-ttu-id="21f3d-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1802">gatewayName</span></span> |<span data-ttu-id="21f3d-1803">Veri deposu erişen ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="21f3d-1804">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1804">Yes</span></span> |
| <span data-ttu-id="21f3d-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-1805">encryptedCredential</span></span> |<span data-ttu-id="21f3d-1806">Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="21f3d-1807">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="21f3d-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1808">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="21f3d-1809">Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1810">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1810">Dataset</span></span>
<span data-ttu-id="21f3d-1811">MongoDB veri kümesini tanımlamak için **türü** için veri kümesinin **MongoDbCollection**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1812">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1812">Property</span></span> | <span data-ttu-id="21f3d-1813">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1813">Description</span></span> | <span data-ttu-id="21f3d-1814">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1815">collectionName</span></span> |<span data-ttu-id="21f3d-1816">MongoDB veritabanı koleksiyonunda adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="21f3d-1817">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1818">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="21f3d-1819">Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="21f3d-1820">Kopyalama etkinliği MongoDB kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1821">Veri adresinden kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **MongoDbSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1822">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1822">Property</span></span> | <span data-ttu-id="21f3d-1823">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1823">Description</span></span> | <span data-ttu-id="21f3d-1824">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1824">Allowed values</span></span> | <span data-ttu-id="21f3d-1825">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1826">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-1826">query</span></span> |<span data-ttu-id="21f3d-1827">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-1828">SQL-92 sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1828">SQL-92 query string.</span></span> <span data-ttu-id="21f3d-1829">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-1830">Hayır (varsa **collectionName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1831">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1832">Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="21f3d-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="21f3d-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-1834">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1834">Linked service</span></span>
<span data-ttu-id="21f3d-1835">Bağlantılı hizmetinin bir Amazon S3 tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AwsAccessKey**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-1836">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1836">Property</span></span> | <span data-ttu-id="21f3d-1837">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1837">Description</span></span> | <span data-ttu-id="21f3d-1838">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1838">Allowed values</span></span> | <span data-ttu-id="21f3d-1839">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="21f3d-1840">accessKeyID</span></span> |<span data-ttu-id="21f3d-1841">Gizli erişim anahtarı kimliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1841">ID of the secret access key.</span></span> |<span data-ttu-id="21f3d-1842">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1842">string</span></span> |<span data-ttu-id="21f3d-1843">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1843">Yes</span></span> |
| <span data-ttu-id="21f3d-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="21f3d-1844">secretAccessKey</span></span> |<span data-ttu-id="21f3d-1845">Gizli erişim anahtar kendisi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1845">The secret access key itself.</span></span> |<span data-ttu-id="21f3d-1846">Şifrelenmiş gizli dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1846">Encrypted secret string</span></span> |<span data-ttu-id="21f3d-1847">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-1848">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="21f3d-1849">Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1850">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1850">Dataset</span></span>
<span data-ttu-id="21f3d-1851">Bir Amazon S3 dataset tanımlamak için **türü** için veri kümesinin **AmazonS3**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1852">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1852">Property</span></span> | <span data-ttu-id="21f3d-1853">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1853">Description</span></span> | <span data-ttu-id="21f3d-1854">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1854">Allowed values</span></span> | <span data-ttu-id="21f3d-1855">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1856">bucketName</span></span> |<span data-ttu-id="21f3d-1857">S3 demetini adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1857">The S3 bucket name.</span></span> |<span data-ttu-id="21f3d-1858">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1858">String</span></span> |<span data-ttu-id="21f3d-1859">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1859">Yes</span></span> |
| <span data-ttu-id="21f3d-1860">anahtar</span><span class="sxs-lookup"><span data-stu-id="21f3d-1860">key</span></span> |<span data-ttu-id="21f3d-1861">S3 nesne anahtarı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1861">The S3 object key.</span></span> |<span data-ttu-id="21f3d-1862">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1862">String</span></span> |<span data-ttu-id="21f3d-1863">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1863">No</span></span> |
| <span data-ttu-id="21f3d-1864">önek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1864">prefix</span></span> |<span data-ttu-id="21f3d-1865">S3 nesne anahtarı için önek.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="21f3d-1866">Seçilen nesneler, anahtarları Bu önek ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="21f3d-1867">Yalnızca anahtar boş olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="21f3d-1868">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1868">String</span></span> |<span data-ttu-id="21f3d-1869">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1869">No</span></span> |
| <span data-ttu-id="21f3d-1870">Sürüm</span><span class="sxs-lookup"><span data-stu-id="21f3d-1870">version</span></span> |<span data-ttu-id="21f3d-1871">S3 sürüm etkinleştirilirse S3 nesne sürümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="21f3d-1872">Dize</span><span class="sxs-lookup"><span data-stu-id="21f3d-1872">String</span></span> |<span data-ttu-id="21f3d-1873">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1873">No</span></span> |
| <span data-ttu-id="21f3d-1874">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1874">format</span></span> | <span data-ttu-id="21f3d-1875">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-1876">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-1877">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-1878">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-1879">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1879">No</span></span> | |
| <span data-ttu-id="21f3d-1880">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-1880">compression</span></span> | <span data-ttu-id="21f3d-1881">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-1882">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="21f3d-1883">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-1884">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-1885">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="21f3d-1886">bucketName + anahtarı burada demet S3 nesneleri için kök kapsayıcı ve anahtar S3 nesnenin tam yolunun S3 nesnenin konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="21f3d-1887">Örnek: Örnek veri kümesi önekiyle</span><span class="sxs-lookup"><span data-stu-id="21f3d-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="21f3d-1888">Örnek: Örnek veri kümesiyle (sürüm)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="21f3d-1889">Örnek: S3 dinamik yollar</span><span class="sxs-lookup"><span data-stu-id="21f3d-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="21f3d-1890">Örnekte, Amazon S3 dataset içindeki anahtar ve bucketName özellikler için sabit değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="21f3d-1891">Veri Fabrikası sistem değişkenleri SliceStart gibi kullanarak anahtar ve çalışma zamanında dinamik olarak bucketName hesaplama olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="21f3d-1892">Bir Amazon S3 dataset önek özelliği için aynı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="21f3d-1893">Bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md) desteklenen işlevleri ve değişkenler listesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="21f3d-1894">Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="21f3d-1895">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1896">Verileri Amazon S3'ten kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **FileSystemSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="21f3d-1897">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1897">Property</span></span> | <span data-ttu-id="21f3d-1898">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1898">Description</span></span> | <span data-ttu-id="21f3d-1899">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1899">Allowed values</span></span> | <span data-ttu-id="21f3d-1900">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1901">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1901">recursive</span></span> |<span data-ttu-id="21f3d-1902">Özyinelemeli S3 listesinde olup olmadığını belirtir dizini altındaki nesneleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="21f3d-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="21f3d-1903">true/false</span></span> |<span data-ttu-id="21f3d-1904">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="21f3d-1905">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-1906">Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="21f3d-1907">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-1908">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1908">Linked service</span></span>
<span data-ttu-id="21f3d-1909">Bir Azure data factory ile bir şirket içi dosya sistemi bağlayabilirsiniz **şirket içi dosya sunucusu** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="21f3d-1910">Aşağıdaki tabloda şirket içi dosya sunucusu bağlantılı hizmete özgü JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="21f3d-1911">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1911">Property</span></span> | <span data-ttu-id="21f3d-1912">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1912">Description</span></span> | <span data-ttu-id="21f3d-1913">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1914">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-1914">type</span></span> |<span data-ttu-id="21f3d-1915">Type özelliği ayarlandığından emin olun **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="21f3d-1916">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1916">Yes</span></span> |
| <span data-ttu-id="21f3d-1917">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="21f3d-1917">host</span></span> |<span data-ttu-id="21f3d-1918">Kopyalamak istediğiniz klasörün kök yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="21f3d-1919">Kaçış karakteri kullanmak ' \ ' dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="21f3d-1920">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="21f3d-1921">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1921">Yes</span></span> |
| <span data-ttu-id="21f3d-1922">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-1922">userid</span></span> |<span data-ttu-id="21f3d-1923">Sunucusuna erişimi olan kullanıcı Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="21f3d-1924">Hayır (encryptedCredential seçerseniz)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="21f3d-1925">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-1925">password</span></span> |<span data-ttu-id="21f3d-1926">(UserID) kullanıcının parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="21f3d-1927">Hayır (encryptedCredential seçerseniz</span><span class="sxs-lookup"><span data-stu-id="21f3d-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="21f3d-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-1928">encryptedCredential</span></span> |<span data-ttu-id="21f3d-1929">Yeni AzureRmDataFactoryEncryptValue cmdlet'ini çalıştırarak alabilirsiniz şifreli kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="21f3d-1930">Hayır (kullanıcı kimliği ve parola düz metin olarak belirtmek isterseniz)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="21f3d-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1931">gatewayName</span></span> |<span data-ttu-id="21f3d-1932">Veri Fabrikası şirket içi dosya sunucusuna bağlanmak için kullanması gereken ağ geçidi adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="21f3d-1933">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="21f3d-1934">Örnek klasör yolu tanımları</span><span class="sxs-lookup"><span data-stu-id="21f3d-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="21f3d-1935">Senaryo</span><span class="sxs-lookup"><span data-stu-id="21f3d-1935">Scenario</span></span> | <span data-ttu-id="21f3d-1936">Bağlantılı hizmet tanımında ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="21f3d-1936">Host in linked service definition</span></span> | <span data-ttu-id="21f3d-1937">veri kümesi tanımında folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1938">Veri Yönetimi ağ geçidi makine üzerinde yerel klasör:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="21f3d-1939">Örnekler: D:\\ \* veya D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="21f3d-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="21f3d-1940">D:\\ \\ (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="21f3d-1941">localhost (daha önceki sürümler için veri yönetimi ağ geçidi 2. 0)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="21f3d-1942">. \\ \\ veya klasör\\\\alt klasör (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="21f3d-1943">D:\\ \\ veya D:\\\\klasörü\\\\alt klasör (için ağ geçidi sürüm 2.0 altında)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="21f3d-1944">Uzak paylaşılan klasör:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="21f3d-1945">Örnekler: \\ \\myserver\\paylaşmak\\ \* veya \\ \\myserver\\paylaşmak\\klasörü\\alt klasör\\*</span><span class="sxs-lookup"><span data-stu-id="21f3d-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="21f3d-1946">\\\\\\\\myserver\\\\paylaşma</span><span class="sxs-lookup"><span data-stu-id="21f3d-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="21f3d-1947">. \\ \\ veya klasör\\\\alt klasör</span><span class="sxs-lookup"><span data-stu-id="21f3d-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="21f3d-1948">Örnek: kullanıcı adı ve parola düz metin olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="21f3d-1949">Örnek: encryptedcredential kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="21f3d-1950">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-1951">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1951">Dataset</span></span>
<span data-ttu-id="21f3d-1952">Bir dosya sistemi veri kümesini tanımlamak için **türü** için veri kümesinin **FileShare**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-1953">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1953">Property</span></span> | <span data-ttu-id="21f3d-1954">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1954">Description</span></span> | <span data-ttu-id="21f3d-1955">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-1956">folderPath</span></span> |<span data-ttu-id="21f3d-1957">Alt klasöre belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="21f3d-1958">Kaçış karakteri kullanmak ' \' dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="21f3d-1959">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="21f3d-1960">Bu özellik ile birleştirebilirsiniz **partitionBy** klasörün dilimine dayalı yol başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="21f3d-1961">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-1961">Yes</span></span> |
| <span data-ttu-id="21f3d-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="21f3d-1962">fileName</span></span> |<span data-ttu-id="21f3d-1963">Dosya adını belirtin **folderPath** klasöründeki belirli bir dosya belirtmek için tablo istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="21f3d-1964">Bu özellik için herhangi bir değer belirtmezseniz, tablonun klasördeki tüm dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="21f3d-1965">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan dosya adı şu biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="21f3d-1966">`Data.<Guid>.txt`(Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="21f3d-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="21f3d-1967">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1967">No</span></span> |
| <span data-ttu-id="21f3d-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="21f3d-1968">fileFilter</span></span> |<span data-ttu-id="21f3d-1969">Tüm dosyalar yerine folderPath dosyaları kümesini seçmek için kullanılacak bir filtre belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="21f3d-1970">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="21f3d-1971">Örnek 1: "fileFilter": "* .log"</span><span class="sxs-lookup"><span data-stu-id="21f3d-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="21f3d-1972">Örnek 2: "fileFilter": 2016 - 1-? txt"</span><span class="sxs-lookup"><span data-stu-id="21f3d-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="21f3d-1973">Bu fileFilter bir giriş FileShare veri kümesi için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="21f3d-1974">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1974">No</span></span> |
| <span data-ttu-id="21f3d-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="21f3d-1975">partitionedBy</span></span> |<span data-ttu-id="21f3d-1976">PartitionedBy dinamik folderPath/için bir dosya adı time series verilerini belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="21f3d-1977">İçin verileri saatte parametreli folderPath örneğidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="21f3d-1978">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1978">No</span></span> |
| <span data-ttu-id="21f3d-1979">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-1979">format</span></span> | <span data-ttu-id="21f3d-1980">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-1981">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-1982">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-1983">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-1984">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1984">No</span></span> |
| <span data-ttu-id="21f3d-1985">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-1985">compression</span></span> | <span data-ttu-id="21f3d-1986">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-1987">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**; ve desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-1988">bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-1989">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="21f3d-1990">Dosya adı ve fileFilter aynı anda kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="21f3d-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-1991">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-1992">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="21f3d-1993">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-1994">Dosya sisteminden veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **FileSystemSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-1995">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-1995">Property</span></span> | <span data-ttu-id="21f3d-1996">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-1996">Description</span></span> | <span data-ttu-id="21f3d-1997">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-1997">Allowed values</span></span> | <span data-ttu-id="21f3d-1998">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-1999">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-1999">recursive</span></span> |<span data-ttu-id="21f3d-2000">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="21f3d-2001">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2001">True, False (default)</span></span> |<span data-ttu-id="21f3d-2002">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2003">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="21f3d-2004">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="21f3d-2005">Dosya sistemi havuzu kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="21f3d-2006">Dosya sistemi veri kopyalıyorsanız ayarlamak **Havuz türü** kopyalama etkinliği **FileSystemSink**ve aşağıdaki özellikleri belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="21f3d-2007">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2007">Property</span></span> | <span data-ttu-id="21f3d-2008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2008">Description</span></span> | <span data-ttu-id="21f3d-2009">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2009">Allowed values</span></span> | <span data-ttu-id="21f3d-2010">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="21f3d-2011">copyBehavior</span></span> |<span data-ttu-id="21f3d-2012">Kaynak BlobSource veya dosya sistemi olduğunda kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="21f3d-2013">**PreserveHierarchy:** dosya hiyerarşisi hedef klasördeki korur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="21f3d-2014">Diğer bir deyişle, kaynak dosyanın kaynak klasöre göreli yol hedef dosya hedef klasöre göreli yol aynıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="21f3d-2015">**FlattenHierarchy:** tüm dosyaları kaynak klasörden hedef klasöre ilk düzeyi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="21f3d-2016">Hedef dosyalar otomatik olarak oluşturulur adıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="21f3d-2017">**MergeFiles:** bir dosya için kaynak klasöründeki tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="21f3d-2018">Dosya adı/blob adı belirtilirse, birleştirilmiş dosya adı belirtilen addır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="21f3d-2019">Aksi halde, bir otomatik olarak oluşturulan dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="21f3d-2020">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2020">No</span></span> |
<span data-ttu-id="21f3d-2021">otomatik-</span><span class="sxs-lookup"><span data-stu-id="21f3d-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-2022">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-2023">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="21f3d-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="21f3d-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-2025">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2025">Linked service</span></span>
<span data-ttu-id="21f3d-2026">Bağlantılı hizmetinin FTP tanımlamak için Ayarla **türü** bağlantılı hizmetinin **Ftp_sunucusu**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2027">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2027">Property</span></span> | <span data-ttu-id="21f3d-2028">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2028">Description</span></span> | <span data-ttu-id="21f3d-2029">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2029">Required</span></span> | <span data-ttu-id="21f3d-2030">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="21f3d-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2031">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="21f3d-2031">host</span></span> |<span data-ttu-id="21f3d-2032">FTP sunucusunun adı veya IP adresi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="21f3d-2033">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="21f3d-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2034">authenticationType</span></span> |<span data-ttu-id="21f3d-2035">Kimlik doğrulama türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2035">Specify authentication type</span></span> |<span data-ttu-id="21f3d-2036">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2036">Yes</span></span> |<span data-ttu-id="21f3d-2037">Temel, anonim</span><span class="sxs-lookup"><span data-stu-id="21f3d-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="21f3d-2038">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2038">username</span></span> |<span data-ttu-id="21f3d-2039">FTP sunucusuna erişimi olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="21f3d-2040">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="21f3d-2041">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2041">password</span></span> |<span data-ttu-id="21f3d-2042">(Kullanıcı adı) kullanıcı parolası</span><span class="sxs-lookup"><span data-stu-id="21f3d-2042">Password for the user (username)</span></span> |<span data-ttu-id="21f3d-2043">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="21f3d-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-2044">encryptedCredential</span></span> |<span data-ttu-id="21f3d-2045">FTP sunucusuna erişmek için şifrelenmiş kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="21f3d-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="21f3d-2046">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="21f3d-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2047">gatewayName</span></span> |<span data-ttu-id="21f3d-2048">Şirket içi FTP sunucusuna bağlanmak için veri yönetimi ağ geçidi ağ geçidinin adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="21f3d-2049">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="21f3d-2050">port</span><span class="sxs-lookup"><span data-stu-id="21f3d-2050">port</span></span> |<span data-ttu-id="21f3d-2051">FTP sunucusunun dinlediği bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="21f3d-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="21f3d-2052">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2052">No</span></span> |<span data-ttu-id="21f3d-2053">21</span><span class="sxs-lookup"><span data-stu-id="21f3d-2053">21</span></span> |
| <span data-ttu-id="21f3d-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="21f3d-2054">enableSsl</span></span> |<span data-ttu-id="21f3d-2055">FTP SSL/TLS kanalı üzerinden kullanıp kullanmayacağınızı belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="21f3d-2056">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2056">No</span></span> |<span data-ttu-id="21f3d-2057">TRUE</span><span class="sxs-lookup"><span data-stu-id="21f3d-2057">true</span></span> |
| <span data-ttu-id="21f3d-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="21f3d-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="21f3d-2059">Sunucu SSL sertifika doğrulamasını FTP SSL/TLS kanalı üzerinden kullanırken etkinleştirilip etkinleştirilmeyeceğini belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="21f3d-2060">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2060">No</span></span> |<span data-ttu-id="21f3d-2061">TRUE</span><span class="sxs-lookup"><span data-stu-id="21f3d-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="21f3d-2062">Örnek: Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="21f3d-2063">Örnek: kullanıcı adı ve parola düz metin olarak temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="21f3d-2064">Örnek: Bağlantı noktası, enableSsl, enableServerCertificateValidation kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="21f3d-2065">Örnek: kimlik doğrulama ve ağ geçidi encryptedCredential kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="21f3d-2066">Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-2067">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2067">Dataset</span></span>
<span data-ttu-id="21f3d-2068">Bir FTP veri kümesini tanımlamak için **türü** için veri kümesinin **FileShare**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2069">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2069">Property</span></span> | <span data-ttu-id="21f3d-2070">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2070">Description</span></span> | <span data-ttu-id="21f3d-2071">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-2072">folderPath</span></span> |<span data-ttu-id="21f3d-2073">Klasörün alt yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2073">Sub path to the folder.</span></span> <span data-ttu-id="21f3d-2074">Kaçış karakteri kullanmak ' \ ' dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="21f3d-2075">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="21f3d-2076">Bu özellik ile birleştirebilirsiniz **partitionBy** klasörün dilimine dayalı yol başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="21f3d-2077">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2077">Yes</span></span> 
| <span data-ttu-id="21f3d-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2078">fileName</span></span> |<span data-ttu-id="21f3d-2079">Dosya adını belirtin **folderPath** klasöründeki belirli bir dosya belirtmek için tablo istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="21f3d-2080">Bu özellik için herhangi bir değer belirtmezseniz, tablonun klasördeki tüm dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="21f3d-2081">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan dosya adı aşağıdaki olacaktır bu biçimi:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="21f3d-2082">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="21f3d-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="21f3d-2083">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2083">No</span></span> |
| <span data-ttu-id="21f3d-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="21f3d-2084">fileFilter</span></span> |<span data-ttu-id="21f3d-2085">Tüm dosyalar yerine folderPath dosyaları kümesini seçmek için kullanılacak bir filtre belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="21f3d-2086">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="21f3d-2087">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="21f3d-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="21f3d-2088">Örnek 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="21f3d-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="21f3d-2089">fileFilter bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="21f3d-2090">Bu özellik ile HDFS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="21f3d-2091">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2091">No</span></span> |
| <span data-ttu-id="21f3d-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="21f3d-2092">partitionedBy</span></span> |<span data-ttu-id="21f3d-2093">partitionedBy filename zaman serisi veri için dinamik bir folderPath belirtmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="21f3d-2094">Örneğin, her veri saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="21f3d-2095">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2095">No</span></span> |
| <span data-ttu-id="21f3d-2096">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2096">format</span></span> | <span data-ttu-id="21f3d-2097">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-2098">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-2099">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-2100">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-2101">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2101">No</span></span> |
| <span data-ttu-id="21f3d-2102">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2102">compression</span></span> | <span data-ttu-id="21f3d-2103">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-2104">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**; ve desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-2105">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-2106">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2106">No</span></span> |
| <span data-ttu-id="21f3d-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="21f3d-2107">useBinaryTransfer</span></span> |<span data-ttu-id="21f3d-2108">Belirtin olup ikili aktarım modunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="21f3d-2109">İkili mod ve false ASCII için true.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="21f3d-2110">Varsayılan değer: True.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2110">Default value: True.</span></span> <span data-ttu-id="21f3d-2111">İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="21f3d-2112">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="21f3d-2113">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-2114">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="21f3d-2115">Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="21f3d-2116">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2117">Bir FTP sunucusundan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **FileSystemSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-2118">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2118">Property</span></span> | <span data-ttu-id="21f3d-2119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2119">Description</span></span> | <span data-ttu-id="21f3d-2120">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2120">Allowed values</span></span> | <span data-ttu-id="21f3d-2121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2122">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2122">recursive</span></span> |<span data-ttu-id="21f3d-2123">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="21f3d-2124">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2124">True, False (default)</span></span> |<span data-ttu-id="21f3d-2125">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2126">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-2127">Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="21f3d-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="21f3d-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-2129">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2129">Linked service</span></span>
<span data-ttu-id="21f3d-2130">Bağlantılı hizmetinin bir HDFS tanımlamak için Ayarla **türü** bağlantılı hizmetinin **Hdfs**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2131">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2131">Property</span></span> | <span data-ttu-id="21f3d-2132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2132">Description</span></span> | <span data-ttu-id="21f3d-2133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2134">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-2134">type</span></span> |<span data-ttu-id="21f3d-2135">Type özelliği ayarlanmalıdır: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="21f3d-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="21f3d-2136">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2136">Yes</span></span> |
| <span data-ttu-id="21f3d-2137">Url</span><span class="sxs-lookup"><span data-stu-id="21f3d-2137">Url</span></span> |<span data-ttu-id="21f3d-2138">HDFS URL'si</span><span class="sxs-lookup"><span data-stu-id="21f3d-2138">URL to the HDFS</span></span> |<span data-ttu-id="21f3d-2139">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2139">Yes</span></span> |
| <span data-ttu-id="21f3d-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2140">authenticationType</span></span> |<span data-ttu-id="21f3d-2141">Anonim veya Windows.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="21f3d-2142">Kullanılacak **Kerberos kimlik doğrulaması** HDFS bağlayıcı için başvurmak [Bu bölümde](#use-kerberos-authentication-for-hdfs-connector) şirket içi ortamınıza uygun şekilde ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="21f3d-2143">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2143">Yes</span></span> |
| <span data-ttu-id="21f3d-2144">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2144">userName</span></span> |<span data-ttu-id="21f3d-2145">Kullanıcı adı için Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="21f3d-2146">Evet (Windows kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="21f3d-2147">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2147">password</span></span> |<span data-ttu-id="21f3d-2148">Windows kimlik doğrulaması için parola.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="21f3d-2149">Evet (Windows kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="21f3d-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2150">gatewayName</span></span> |<span data-ttu-id="21f3d-2151">Data Factory hizmetinin HDFS bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="21f3d-2152">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2152">Yes</span></span> |
| <span data-ttu-id="21f3d-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-2153">encryptedCredential</span></span> |<span data-ttu-id="21f3d-2154">[AzureRMDataFactoryEncryptValue yeni](https://msdn.microsoft.com/library/mt603802.aspx) erişim kimlik bilgisi çıktısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="21f3d-2155">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="21f3d-2156">Örnek: Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="21f3d-2157">Örnek: Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="21f3d-2158">Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-2159">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2159">Dataset</span></span>
<span data-ttu-id="21f3d-2160">HDFS veri kümesini tanımlamak için **türü** için veri kümesinin **FileShare**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2161">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2161">Property</span></span> | <span data-ttu-id="21f3d-2162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2162">Description</span></span> | <span data-ttu-id="21f3d-2163">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-2164">folderPath</span></span> |<span data-ttu-id="21f3d-2165">Klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2165">Path to the folder.</span></span> <span data-ttu-id="21f3d-2166">Örnek:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="21f3d-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="21f3d-2167">Kaçış karakteri kullanmak ' \ ' dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="21f3d-2168">Örneğin: folder\subfolder için klasör belirtin\\\\alt ve d:\samplefolder için d: belirtin\\\\ÖrnekKlasör.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="21f3d-2169">Bu özellik ile birleştirebilirsiniz **partitionBy** klasörün dilimine dayalı yol başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="21f3d-2170">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2170">Yes</span></span> |
| <span data-ttu-id="21f3d-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2171">fileName</span></span> |<span data-ttu-id="21f3d-2172">Dosya adını belirtin **folderPath** klasöründeki belirli bir dosya belirtmek için tablo istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="21f3d-2173">Bu özellik için herhangi bir değer belirtmezseniz, tablonun klasördeki tüm dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="21f3d-2174">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan dosya adı aşağıdaki olacaktır bu biçimi:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="21f3d-2175">Veriler. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="21f3d-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="21f3d-2176">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2176">No</span></span> |
| <span data-ttu-id="21f3d-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="21f3d-2177">partitionedBy</span></span> |<span data-ttu-id="21f3d-2178">partitionedBy filename zaman serisi veri için dinamik bir folderPath belirtmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="21f3d-2179">Örnek: veri her saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="21f3d-2180">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2180">No</span></span> |
| <span data-ttu-id="21f3d-2181">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2181">format</span></span> | <span data-ttu-id="21f3d-2182">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-2183">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-2184">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-2185">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-2186">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2186">No</span></span> |
| <span data-ttu-id="21f3d-2187">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2187">compression</span></span> | <span data-ttu-id="21f3d-2188">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-2189">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="21f3d-2190">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-2191">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-2192">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="21f3d-2193">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-2194">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="21f3d-2195">Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="21f3d-2196">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2197">HDFS veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **FileSystemSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="21f3d-2198">**FileSystemSource** aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="21f3d-2199">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2199">Property</span></span> | <span data-ttu-id="21f3d-2200">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2200">Description</span></span> | <span data-ttu-id="21f3d-2201">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2201">Allowed values</span></span> | <span data-ttu-id="21f3d-2202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2203">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2203">recursive</span></span> |<span data-ttu-id="21f3d-2204">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="21f3d-2205">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2205">True, False (default)</span></span> |<span data-ttu-id="21f3d-2206">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2207">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-2208">Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="21f3d-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="21f3d-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-2210">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2210">Linked service</span></span>
<span data-ttu-id="21f3d-2211">Bağlantılı hizmetinin bir SFTP tanımlamak için Ayarla **türü** bağlantılı hizmetinin **Sftp**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2212">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2212">Property</span></span> | <span data-ttu-id="21f3d-2213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2213">Description</span></span> | <span data-ttu-id="21f3d-2214">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2215">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="21f3d-2215">host</span></span> | <span data-ttu-id="21f3d-2216">SFTP sunucunun adı veya IP adresi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="21f3d-2217">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2217">Yes</span></span> |
| <span data-ttu-id="21f3d-2218">port</span><span class="sxs-lookup"><span data-stu-id="21f3d-2218">port</span></span> |<span data-ttu-id="21f3d-2219">SFTP sunucunun dinlediği bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="21f3d-2220">Varsayılan değer: 21</span><span class="sxs-lookup"><span data-stu-id="21f3d-2220">The default value is: 21</span></span> |<span data-ttu-id="21f3d-2221">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2221">No</span></span> |
| <span data-ttu-id="21f3d-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2222">authenticationType</span></span> |<span data-ttu-id="21f3d-2223">Kimlik doğrulama türü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2223">Specify authentication type.</span></span> <span data-ttu-id="21f3d-2224">İzin verilen değerler: **temel**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="21f3d-2225">Başvurmak [kullanarak temel kimlik doğrulaması](#using-basic-authentication) ve [kullanarak SSH ortak anahtar kimlik doğrulaması](#using-ssh-public-key-authentication) daha fazla özellikleri ve JSON örnekleri sırasıyla bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="21f3d-2226">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2226">Yes</span></span> |
| <span data-ttu-id="21f3d-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="21f3d-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="21f3d-2228">Ana anahtar doğrulama atlamak bu seçeneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="21f3d-2229">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2229">No.</span></span> <span data-ttu-id="21f3d-2230">Varsayılan değeri: false</span><span class="sxs-lookup"><span data-stu-id="21f3d-2230">The default value: false</span></span> |
| <span data-ttu-id="21f3d-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="21f3d-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="21f3d-2232">Ana makine anahtarı, parmak izi belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="21f3d-2233">Yanıt Evet ise `skipHostKeyValidation` false olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="21f3d-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2234">gatewayName</span></span> |<span data-ttu-id="21f3d-2235">Bir şirket içi SFTP sunucusuna bağlanmak için veri yönetimi ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="21f3d-2236">Bir şirket içi SFTP sunucusundan veri kopyalama, Evet.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="21f3d-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-2237">encryptedCredential</span></span> | <span data-ttu-id="21f3d-2238">SFTP sunucuya erişmek için şifrelenmiş kimlik bilgileri'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="21f3d-2239">Otomatik olarak oluşturulan Kopyalama Sihirbazı'nı veya ClickOnce açılan iletişim temel kimlik doğrulaması (kullanıcı adı + parola) veya SshPublicKey kimlik (kullanıcı adı + özel anahtar yolu veya içerik) belirttiğinizde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="21f3d-2240">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2240">No.</span></span> <span data-ttu-id="21f3d-2241">Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="21f3d-2242">Örnek: temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="21f3d-2243">Temel kimlik doğrulaması kullanmak üzere ayarlanmış `authenticationType` olarak `Basic`ve SFTP bağlayıcı son bölümde sunulan genel kaynakların yanı sıra aşağıdaki özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="21f3d-2244">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2244">Property</span></span> | <span data-ttu-id="21f3d-2245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2245">Description</span></span> | <span data-ttu-id="21f3d-2246">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2247">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2247">username</span></span> | <span data-ttu-id="21f3d-2248">SFTP sunucusuna erişimi olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="21f3d-2249">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2249">Yes</span></span> |
| <span data-ttu-id="21f3d-2250">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2250">password</span></span> | <span data-ttu-id="21f3d-2251">(Kullanıcı adı) kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2251">Password for the user (username).</span></span> | <span data-ttu-id="21f3d-2252">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="21f3d-2253">Örnek: Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri **</span><span class="sxs-lookup"><span data-stu-id="21f3d-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="21f3d-2254">SSH ortak anahtar kimlik doğrulaması kullanarak: **</span><span class="sxs-lookup"><span data-stu-id="21f3d-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="21f3d-2255">Temel kimlik doğrulaması kullanmak üzere ayarlanmış `authenticationType` olarak `SshPublicKey`ve SFTP bağlayıcı son bölümde sunulan genel kaynakların yanı sıra aşağıdaki özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="21f3d-2256">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2256">Property</span></span> | <span data-ttu-id="21f3d-2257">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2257">Description</span></span> | <span data-ttu-id="21f3d-2258">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2259">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2259">username</span></span> |<span data-ttu-id="21f3d-2260">SFTP sunucusuna erişimi olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="21f3d-2261">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2261">Yes</span></span> |
| <span data-ttu-id="21f3d-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-2262">privateKeyPath</span></span> | <span data-ttu-id="21f3d-2263">Belirtin özel anahtar dosyasının mutlak yolu, ağ geçidi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="21f3d-2264">Belirtin `privateKeyPath` veya `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="21f3d-2265">Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="21f3d-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="21f3d-2266">privateKeyContent</span></span> | <span data-ttu-id="21f3d-2267">Özel anahtar içeriğinin seri hale getirilmiş bir dize.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="21f3d-2268">Kopyalama Sihirbazı'nı, özel anahtar dosyası okumak ve özel anahtar içeriği otomatik olarak ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="21f3d-2269">Tüm diğer aracı/SDK kullanıyorsanız, bunun yerine privateKeyPath özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="21f3d-2270">Belirtin `privateKeyPath` veya `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="21f3d-2271">Parola</span><span class="sxs-lookup"><span data-stu-id="21f3d-2271">passPhrase</span></span> | <span data-ttu-id="21f3d-2272">Geçişi tümcecik/anahtar dosyası bir parola deyimi tarafından korunuyorsa, özel anahtarın şifresini çözmek için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="21f3d-2273">Evet, özel anahtar dosyası bir parola deyimi tarafından korunuyorsa.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="21f3d-2274">Örnek: kullanarak özel anahtar içerik ** SshPublicKey kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="21f3d-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="21f3d-2275">Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-2276">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2276">Dataset</span></span>
<span data-ttu-id="21f3d-2277">SFTP veri kümesini tanımlamak için **türü** için veri kümesinin **FileShare**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2278">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2278">Property</span></span> | <span data-ttu-id="21f3d-2279">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2279">Description</span></span> | <span data-ttu-id="21f3d-2280">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-2281">folderPath</span></span> |<span data-ttu-id="21f3d-2282">Klasörün alt yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2282">Sub path to the folder.</span></span> <span data-ttu-id="21f3d-2283">Kaçış karakteri kullanmak ' \ ' dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="21f3d-2284">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="21f3d-2285">Bu özellik ile birleştirebilirsiniz **partitionBy** klasörün dilimine dayalı yol başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="21f3d-2286">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2286">Yes</span></span> |
| <span data-ttu-id="21f3d-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2287">fileName</span></span> |<span data-ttu-id="21f3d-2288">Dosya adını belirtin **folderPath** klasöründeki belirli bir dosya belirtmek için tablo istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="21f3d-2289">Bu özellik için herhangi bir değer belirtmezseniz, tablonun klasördeki tüm dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="21f3d-2290">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan dosya adı aşağıdaki olacaktır bu biçimi:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="21f3d-2291">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="21f3d-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="21f3d-2292">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2292">No</span></span> |
| <span data-ttu-id="21f3d-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="21f3d-2293">fileFilter</span></span> |<span data-ttu-id="21f3d-2294">Tüm dosyalar yerine folderPath dosyaları kümesini seçmek için kullanılacak bir filtre belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="21f3d-2295">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="21f3d-2296">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="21f3d-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="21f3d-2297">Örnek 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="21f3d-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="21f3d-2298">fileFilter bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="21f3d-2299">Bu özellik ile HDFS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="21f3d-2300">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2300">No</span></span> |
| <span data-ttu-id="21f3d-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="21f3d-2301">partitionedBy</span></span> |<span data-ttu-id="21f3d-2302">partitionedBy filename zaman serisi veri için dinamik bir folderPath belirtmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="21f3d-2303">Örneğin, her veri saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="21f3d-2304">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2304">No</span></span> |
| <span data-ttu-id="21f3d-2305">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2305">format</span></span> | <span data-ttu-id="21f3d-2306">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-2307">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="21f3d-2308">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="21f3d-2309">İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="21f3d-2310">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2310">No</span></span> |
| <span data-ttu-id="21f3d-2311">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2311">compression</span></span> | <span data-ttu-id="21f3d-2312">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-2313">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="21f3d-2314">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-2315">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-2316">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2316">No</span></span> |
| <span data-ttu-id="21f3d-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="21f3d-2317">useBinaryTransfer</span></span> |<span data-ttu-id="21f3d-2318">Belirtin olup ikili aktarım modunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="21f3d-2319">İkili mod ve false ASCII için true.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="21f3d-2320">Varsayılan değer: True.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2320">Default value: True.</span></span> <span data-ttu-id="21f3d-2321">İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="21f3d-2322">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="21f3d-2323">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-2324">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="21f3d-2325">Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="21f3d-2326">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2327">SFTP kaynaktan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **FileSystemSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-2328">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2328">Property</span></span> | <span data-ttu-id="21f3d-2329">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2329">Description</span></span> | <span data-ttu-id="21f3d-2330">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2330">Allowed values</span></span> | <span data-ttu-id="21f3d-2331">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2332">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2332">recursive</span></span> |<span data-ttu-id="21f3d-2333">Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="21f3d-2334">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2334">True, False (default)</span></span> |<span data-ttu-id="21f3d-2335">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="21f3d-2336">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-2337">Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="21f3d-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="21f3d-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-2339">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2339">Linked service</span></span>
<span data-ttu-id="21f3d-2340">Bağlantılı hizmeti bir HTTP tanımlama, Ayarla **türü** bağlantılı hizmetinin **Http**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2341">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2341">Property</span></span> | <span data-ttu-id="21f3d-2342">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2342">Description</span></span> | <span data-ttu-id="21f3d-2343">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2344">URL</span><span class="sxs-lookup"><span data-stu-id="21f3d-2344">url</span></span> | <span data-ttu-id="21f3d-2345">Web sunucusu için temel URL</span><span class="sxs-lookup"><span data-stu-id="21f3d-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="21f3d-2346">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2346">Yes</span></span> |
| <span data-ttu-id="21f3d-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2347">authenticationType</span></span> | <span data-ttu-id="21f3d-2348">Kimlik doğrulama türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2348">Specifies the authentication type.</span></span> <span data-ttu-id="21f3d-2349">İzin verilen değerler: **anonim**, **temel**, **Özet**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="21f3d-2350">Daha fazla özellikleri ve bu kimlik doğrulama türleri için JSON örnekleri bu tabloda aşağıdaki bölümlerde sırasıyla bakın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="21f3d-2351">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2351">Yes</span></span> |
| <span data-ttu-id="21f3d-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="21f3d-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="21f3d-2353">Sunucu SSL sertifika doğrulamasını kaynak HTTPS Web sunucusu ise etkinleştirilip etkinleştirilmeyeceğini belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="21f3d-2354">Hayır, varsayılan değer true şeklindedir</span><span class="sxs-lookup"><span data-stu-id="21f3d-2354">No, default is true</span></span> |
| <span data-ttu-id="21f3d-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2355">gatewayName</span></span> | <span data-ttu-id="21f3d-2356">Bir şirket içi HTTP kaynağına bağlanmak için veri yönetimi ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="21f3d-2357">Bir şirket içi HTTP kaynaktan veri kopyalama, Evet.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="21f3d-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-2358">encryptedCredential</span></span> | <span data-ttu-id="21f3d-2359">HTTP uç noktasına erişmek için şifrelenmiş kimlik bilgileri'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="21f3d-2360">Otomatik olarak oluşturulan Kopyalama Sihirbazı'nı veya ClickOnce açılan iletişim kimlik doğrulama bilgilerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="21f3d-2361">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2361">No.</span></span> <span data-ttu-id="21f3d-2362">Yalnızca bir şirket içi HTTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="21f3d-2363">Örnek: Temel, Özet veya Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="21f3d-2364">Ayarlama `authenticationType` olarak `Basic`, `Digest`, veya `Windows`ve HTTP Bağlayıcısı yukarıda sunulan genel kaynakların yanı sıra aşağıdaki özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="21f3d-2365">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2365">Property</span></span> | <span data-ttu-id="21f3d-2366">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2366">Description</span></span> | <span data-ttu-id="21f3d-2367">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2368">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2368">username</span></span> | <span data-ttu-id="21f3d-2369">HTTP uç noktasına erişmek için kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="21f3d-2370">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2370">Yes</span></span> |
| <span data-ttu-id="21f3d-2371">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2371">password</span></span> | <span data-ttu-id="21f3d-2372">(Kullanıcı adı) kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2372">Password for the user (username).</span></span> | <span data-ttu-id="21f3d-2373">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="21f3d-2374">Örnek: ClientCertificate kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="21f3d-2375">Temel kimlik doğrulaması kullanmak üzere ayarlanmış `authenticationType` olarak `ClientCertificate`ve HTTP Bağlayıcısı yukarıda sunulan genel kaynakların yanı sıra aşağıdaki özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="21f3d-2376">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2376">Property</span></span> | <span data-ttu-id="21f3d-2377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2377">Description</span></span> | <span data-ttu-id="21f3d-2378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="21f3d-2379">embeddedCertData</span></span> | <span data-ttu-id="21f3d-2380">İkili veriler kişisel bilgi değişimi (PFX) dosyası Base64 ile kodlanmış içeriği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="21f3d-2381">Belirtin `embeddedCertData` veya `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="21f3d-2382">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="21f3d-2382">certThumbprint</span></span> | <span data-ttu-id="21f3d-2383">Ağ geçidi makinenizin sertifika deposunda yüklü sertifika parmak izi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="21f3d-2384">Yalnızca bir şirket içi HTTP kaynaktan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="21f3d-2385">Belirtin `embeddedCertData` veya `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="21f3d-2386">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2386">password</span></span> | <span data-ttu-id="21f3d-2387">Sertifikayla ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="21f3d-2388">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2388">No</span></span> |

<span data-ttu-id="21f3d-2389">Kullanırsanız `certThumbprint` kimlik doğrulaması ve sertifika yüklü için yerel bilgisayarın kişisel deposunda, ağ geçidi hizmeti okuma izni vermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="21f3d-2390">Microsoft Yönetim Konsolu (MMC) başlatın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="21f3d-2391">Ekleme **sertifikaları** hedefleyen eklentisi **yerel bilgisayar**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="21f3d-2392">Genişletme **sertifikaları**, **kişisel**, tıklatıp **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="21f3d-2393">Kişisel deposundaki sertifikayı sağ tıklatın ve seçin **tüm görevler**->**özel anahtarları Yönet...**</span><span class="sxs-lookup"><span data-stu-id="21f3d-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="21f3d-2394">Üzerinde **güvenlik** sekmesinde, altında veri yönetimi ağ geçidi ana bilgisayar hizmeti çalıştığı okuma erişimi sertifikayı kullanıcı hesabını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="21f3d-2395">**Örnek: istemci sertifikası kullanarak:** bu hizmeti, veri fabrikası bir şirket içi HTTP web sunucusuna bağlı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="21f3d-2396">Veri Yönetimi ağ ile geçidi yüklü olduğu makinede yüklü bir istemci sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="21f3d-2397">Örnek: istemci sertifikası bir dosyada kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="21f3d-2398">Bu hizmet bağlantılar, veri fabrikası bir şirket içi HTTP web sunucusuna bağlı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="21f3d-2399">Veri Yönetimi ağ ile geçidi yüklü olduğu makinedeki bir istemci sertifikası dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="21f3d-2400">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-2401">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2401">Dataset</span></span>
<span data-ttu-id="21f3d-2402">Bir HTTP veri kümesini tanımlamak için **türü** için veri kümesinin **Http**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2403">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2403">Property</span></span> | <span data-ttu-id="21f3d-2404">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2404">Description</span></span> | <span data-ttu-id="21f3d-2405">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="21f3d-2406">relativeUrl</span></span> | <span data-ttu-id="21f3d-2407">Verileri içeren kaynak için göreli bir URL.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="21f3d-2408">Bağlantılı hizmet tanımında belirtilen URL yolu belirtilmediğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="21f3d-2409">Dinamik URL oluşturmak için kullanabileceğiniz [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md), örneğin: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="21f3d-2410">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2410">No</span></span> |
| <span data-ttu-id="21f3d-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="21f3d-2411">requestMethod</span></span> | <span data-ttu-id="21f3d-2412">HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2412">Http method.</span></span> <span data-ttu-id="21f3d-2413">İzin verilen değerler **almak** veya **POST**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="21f3d-2414">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2414">No.</span></span> <span data-ttu-id="21f3d-2415">Varsayılan değer `GET`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="21f3d-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="21f3d-2416">additionalHeaders</span></span> | <span data-ttu-id="21f3d-2417">Ek HTTP isteği üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="21f3d-2418">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2418">No</span></span> |
| <span data-ttu-id="21f3d-2419">RequestBody</span><span class="sxs-lookup"><span data-stu-id="21f3d-2419">requestBody</span></span> | <span data-ttu-id="21f3d-2420">HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2420">Body for HTTP request.</span></span> | <span data-ttu-id="21f3d-2421">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2421">No</span></span> |
| <span data-ttu-id="21f3d-2422">Biçimi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2422">format</span></span> | <span data-ttu-id="21f3d-2423">Yalnızca istiyorsanız, **HTTP uç noktası olarak veri almak-olduğu** ayrıştırma olmadan, bu biçim ayarlarını atla.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="21f3d-2424">HTTP yanıt içeriği kopyalama sırasında ayrıştırma istiyorsanız, aşağıdaki biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="21f3d-2425">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="21f3d-2426">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2426">No</span></span> |
| <span data-ttu-id="21f3d-2427">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2427">compression</span></span> | <span data-ttu-id="21f3d-2428">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="21f3d-2429">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="21f3d-2430">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="21f3d-2431">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="21f3d-2432">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="21f3d-2433">Örnek: (varsayılan) GET yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="21f3d-2434">Örnek: POST yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="21f3d-2435">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="21f3d-2436">Kopyalama etkinliğinde HTTP kaynağı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2437">Bir HTTP kaynaktan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **HttpSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-2438">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2438">Property</span></span> | <span data-ttu-id="21f3d-2439">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2439">Description</span></span> | <span data-ttu-id="21f3d-2440">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="21f3d-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="21f3d-2441">httpRequestTimeout</span></span> | <span data-ttu-id="21f3d-2442">Zaman aşımı (TimeSpan) için bir yanıt almak HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="21f3d-2443">Bu zaman aşımı yanıt verileri okumak için zaman aşımına bir yanıt elde etmektir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="21f3d-2444">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2444">No.</span></span> <span data-ttu-id="21f3d-2445">Varsayılan değer: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="21f3d-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="21f3d-2446">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-2447">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="21f3d-2448">OData</span><span class="sxs-lookup"><span data-stu-id="21f3d-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-2449">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2449">Linked service</span></span>
<span data-ttu-id="21f3d-2450">Bağlantılı hizmetinin bir OData tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OData**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2451">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2451">Property</span></span> | <span data-ttu-id="21f3d-2452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2452">Description</span></span> | <span data-ttu-id="21f3d-2453">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2454">URL</span><span class="sxs-lookup"><span data-stu-id="21f3d-2454">url</span></span> |<span data-ttu-id="21f3d-2455">OData hizmeti URL'si.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2455">Url of the OData service.</span></span> |<span data-ttu-id="21f3d-2456">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2456">Yes</span></span> |
| <span data-ttu-id="21f3d-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2457">authenticationType</span></span> |<span data-ttu-id="21f3d-2458">OData kaynağına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="21f3d-2459">OData bulut için olası değerler şunlardır anonim, temel ve OAuth (Not OAuth Azure Active Directory tabanlı şu anda yalnızca Azure Data Factory destek).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="21f3d-2460">Anonim, temel ve Windows, şirket içi OData için olası değerler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21f3d-2461">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2461">Yes</span></span> |
| <span data-ttu-id="21f3d-2462">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2462">username</span></span> |<span data-ttu-id="21f3d-2463">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="21f3d-2464">Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="21f3d-2465">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2465">password</span></span> |<span data-ttu-id="21f3d-2466">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-2467">Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="21f3d-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="21f3d-2468">authorizedCredential</span></span> |<span data-ttu-id="21f3d-2469">OAuth kullanıyorsanız **Authorize** veri fabrikası Kopyalama Sihirbazı'nı veya düzenleyicide düğmesine tıklayın ve sonra da bu özelliğin değeri otomatik olarak oluşturulan kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="21f3d-2470">Evet (yalnızca OAuth kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="21f3d-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2471">gatewayName</span></span> |<span data-ttu-id="21f3d-2472">Data Factory hizmetinin şirket içi OData hizmetine bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="21f3d-2473">Yalnızca şirket içi OData kaynak sunucudan kopyaladığınız verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="21f3d-2474">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="21f3d-2475">Temel kimlik doğrulaması kullanan örnek-</span><span class="sxs-lookup"><span data-stu-id="21f3d-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="21f3d-2476">Anonim kimlik doğrulaması kullanan örnek-</span><span class="sxs-lookup"><span data-stu-id="21f3d-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="21f3d-2477">Örnek - kullanan Windows kimlik doğrulaması erişme OData kaynağı şirket içi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="21f3d-2478">Örnek - bulut OData kaynağı erişme OAuth kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="21f3d-2479">Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="21f3d-2480">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2480">Dataset</span></span>
<span data-ttu-id="21f3d-2481">Bir OData veri kümesini tanımlamak için **türü** için veri kümesinin **ODataResource**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2482">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2482">Property</span></span> | <span data-ttu-id="21f3d-2483">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2483">Description</span></span> | <span data-ttu-id="21f3d-2484">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2485">Yol</span><span class="sxs-lookup"><span data-stu-id="21f3d-2485">path</span></span> |<span data-ttu-id="21f3d-2486">OData kaynak yolu</span><span class="sxs-lookup"><span data-stu-id="21f3d-2486">Path to the OData resource</span></span> |<span data-ttu-id="21f3d-2487">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2488">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="21f3d-2489">Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-2490">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2491">Bir OData kaynaktan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-2492">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2492">Property</span></span> | <span data-ttu-id="21f3d-2493">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2493">Description</span></span> | <span data-ttu-id="21f3d-2494">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2494">Example</span></span> | <span data-ttu-id="21f3d-2495">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2496">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-2496">query</span></span> |<span data-ttu-id="21f3d-2497">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-2498">"? $select adı, açıklama ve $top = 5 ="</span><span class="sxs-lookup"><span data-stu-id="21f3d-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="21f3d-2499">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2500">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="21f3d-2501">Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="21f3d-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="21f3d-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-2503">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2503">Linked service</span></span>
<span data-ttu-id="21f3d-2504">Bağlantılı hizmetinin bir ODBC tanımlamak için Ayarla **türü** bağlantılı hizmetinin **OnPremisesOdbc**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2505">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2505">Property</span></span> | <span data-ttu-id="21f3d-2506">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2506">Description</span></span> | <span data-ttu-id="21f3d-2507">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-2508">connectionString</span></span> |<span data-ttu-id="21f3d-2509">Bağlantı dizesi ve isteğe bağlı şifrelenmiş kimlik bilgileri olmayan erişim kimlik bilgileri bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="21f3d-2510">Aşağıdaki bölümlerde örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2510">See examples in the following sections.</span></span> |<span data-ttu-id="21f3d-2511">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2511">Yes</span></span> |
| <span data-ttu-id="21f3d-2512">kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2512">credential</span></span> |<span data-ttu-id="21f3d-2513">Sürücü özgü özellik değer biçiminde belirtilen bağlantı dizesi erişim kimlik bilgisi bölümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="21f3d-2514">Örnek: "Uid =<user ID>; PWD =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="21f3d-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="21f3d-2515">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2515">No</span></span> |
| <span data-ttu-id="21f3d-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2516">authenticationType</span></span> |<span data-ttu-id="21f3d-2517">ODBC veri deposuna bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="21f3d-2518">Olası değerler şunlardır: anonim ve temel.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="21f3d-2519">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2519">Yes</span></span> |
| <span data-ttu-id="21f3d-2520">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2520">username</span></span> |<span data-ttu-id="21f3d-2521">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="21f3d-2522">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2522">No</span></span> |
| <span data-ttu-id="21f3d-2523">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2523">password</span></span> |<span data-ttu-id="21f3d-2524">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-2525">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2525">No</span></span> |
| <span data-ttu-id="21f3d-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2526">gatewayName</span></span> |<span data-ttu-id="21f3d-2527">Data Factory hizmetinin ODBC veri deposuna bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="21f3d-2528">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="21f3d-2529">Temel kimlik doğrulaması kullanan örnek-</span><span class="sxs-lookup"><span data-stu-id="21f3d-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="21f3d-2530">Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri kullanılarak örnek-</span><span class="sxs-lookup"><span data-stu-id="21f3d-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="21f3d-2531">Kullanarak kimlik bilgilerini şifrelemek [yeni AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0 sürümü) cmdlet'ini veya [yeni AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (Azure PowerShell 0,9 veya önceki sürüm).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="21f3d-2532">Örnek: Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="21f3d-2533">Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-2534">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2534">Dataset</span></span>
<span data-ttu-id="21f3d-2535">Bir ODBC veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2536">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2536">Property</span></span> | <span data-ttu-id="21f3d-2537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2537">Description</span></span> | <span data-ttu-id="21f3d-2538">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2539">tableName</span></span> |<span data-ttu-id="21f3d-2540">ODBC veri deposundaki tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="21f3d-2541">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="21f3d-2542">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-2543">Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-2544">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2545">Bir ODBC veri deposundan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-2546">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2546">Property</span></span> | <span data-ttu-id="21f3d-2547">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2547">Description</span></span> | <span data-ttu-id="21f3d-2548">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2548">Allowed values</span></span> | <span data-ttu-id="21f3d-2549">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2550">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-2550">query</span></span> |<span data-ttu-id="21f3d-2551">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-2552">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2552">SQL query string.</span></span> <span data-ttu-id="21f3d-2553">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="21f3d-2554">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2555">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="21f3d-2556">Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="21f3d-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="21f3d-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="21f3d-2558">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2558">Linked service</span></span>
<span data-ttu-id="21f3d-2559">Bağlantılı hizmetinin bir Salesforce tanımlamak için Ayarla **türü** bağlantılı hizmetinin **Salesforce**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2560">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2560">Property</span></span> | <span data-ttu-id="21f3d-2561">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2561">Description</span></span> | <span data-ttu-id="21f3d-2562">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="21f3d-2563">environmentUrl</span></span> | <span data-ttu-id="21f3d-2564">URL, Salesforce örneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="21f3d-2565">-Varsayılan değer "https://login.salesforce.com" dir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="21f3d-2566">Korumalı alan veri kopyalamak için "https://test.salesforce.com" belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="21f3d-2567">Özel etki alanından veri kopyalamak için örneğin, "https://[domain].my.salesforce.com" belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="21f3d-2568">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2568">No</span></span> |
| <span data-ttu-id="21f3d-2569">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2569">username</span></span> |<span data-ttu-id="21f3d-2570">Kullanıcı hesabı için bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="21f3d-2571">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2571">Yes</span></span> |
| <span data-ttu-id="21f3d-2572">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2572">password</span></span> |<span data-ttu-id="21f3d-2573">Kullanıcı hesabı için bir parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="21f3d-2574">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2574">Yes</span></span> |
| <span data-ttu-id="21f3d-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="21f3d-2575">securityToken</span></span> |<span data-ttu-id="21f3d-2576">Kullanıcı hesabı için bir güvenlik belirteci belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="21f3d-2577">Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) bir güvenlik belirteci sıfırlama/get ilgili yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="21f3d-2578">Güvenlik belirteçleri hakkında genel bilgi edinmek için [güvenlik ve API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="21f3d-2579">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2580">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="21f3d-2581">Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-2582">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2582">Dataset</span></span>
<span data-ttu-id="21f3d-2583">Salesforce veri kümesini tanımlamak için **türü** için veri kümesinin **RelationalTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2584">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2584">Property</span></span> | <span data-ttu-id="21f3d-2585">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2585">Description</span></span> | <span data-ttu-id="21f3d-2586">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2587">tableName</span></span> |<span data-ttu-id="21f3d-2588">Salesforce tablo adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="21f3d-2589">Hayır (varsa bir **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2590">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21f3d-2591">Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="21f3d-2592">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="21f3d-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2593">Salesforce veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **RelationalSource**ve aşağıdaki özellikleri belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="21f3d-2594">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2594">Property</span></span> | <span data-ttu-id="21f3d-2595">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2595">Description</span></span> | <span data-ttu-id="21f3d-2596">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2596">Allowed values</span></span> | <span data-ttu-id="21f3d-2597">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21f3d-2598">sorgu</span><span class="sxs-lookup"><span data-stu-id="21f3d-2598">query</span></span> |<span data-ttu-id="21f3d-2599">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="21f3d-2600">Bir SQL-92 sorgu veya [Salesforce nesnesi sorgu dili (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) sorgu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="21f3d-2601">Örneğin:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="21f3d-2602">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2603">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="21f3d-2604">API adı "__c" bölümü için herhangi bir özel nesne gereklidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="21f3d-2605">Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="21f3d-2606">Web verileri</span><span class="sxs-lookup"><span data-stu-id="21f3d-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2607">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2607">Linked service</span></span>
<span data-ttu-id="21f3d-2608">Bağlantılı hizmetinin Web tanımlamak için Ayarla **türü** bağlantılı hizmetinin **Web**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2609">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2609">Property</span></span> | <span data-ttu-id="21f3d-2610">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2610">Description</span></span> | <span data-ttu-id="21f3d-2611">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2612">Url</span><span class="sxs-lookup"><span data-stu-id="21f3d-2612">Url</span></span> |<span data-ttu-id="21f3d-2613">Web kaynağı URL'si</span><span class="sxs-lookup"><span data-stu-id="21f3d-2613">URL to the Web source</span></span> |<span data-ttu-id="21f3d-2614">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2614">Yes</span></span> |
| <span data-ttu-id="21f3d-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2615">authenticationType</span></span> |<span data-ttu-id="21f3d-2616">Anonim.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2616">Anonymous.</span></span> |<span data-ttu-id="21f3d-2617">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="21f3d-2618">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="21f3d-2619">Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="21f3d-2620">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2620">Dataset</span></span>
<span data-ttu-id="21f3d-2621">Bir Web veri kümesini tanımlamak için **türü** için veri kümesinin **WebTable**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="21f3d-2622">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2622">Property</span></span> | <span data-ttu-id="21f3d-2623">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2623">Description</span></span> | <span data-ttu-id="21f3d-2624">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-2625">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-2625">type</span></span> |<span data-ttu-id="21f3d-2626">Veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2626">type of the dataset.</span></span> <span data-ttu-id="21f3d-2627">ayarlanmalıdır **WebTable**</span><span class="sxs-lookup"><span data-stu-id="21f3d-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="21f3d-2628">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2628">Yes</span></span> |
| <span data-ttu-id="21f3d-2629">Yol</span><span class="sxs-lookup"><span data-stu-id="21f3d-2629">path</span></span> |<span data-ttu-id="21f3d-2630">Tabloyu içeren kaynak için göreli bir URL.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="21f3d-2631">Hayır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2631">No.</span></span> <span data-ttu-id="21f3d-2632">Bağlantılı hizmet tanımında belirtilen URL yolu belirtilmediğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="21f3d-2633">Dizin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2633">index</span></span> |<span data-ttu-id="21f3d-2634">Tablo kaynak dizini.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2634">The index of the table in the resource.</span></span> <span data-ttu-id="21f3d-2635">Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) bir HTML sayfasında bir tablo dizininin alma adımları için bölüm.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="21f3d-2636">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="21f3d-2637">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="21f3d-2638">Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="21f3d-2639">Kopyalama etkinliğinde Web kaynağı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="21f3d-2640">Bir web tablodan veri kopyalıyorsanız ayarlamak **kaynak türünü** kopyalama etkinliği **WebSource**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="21f3d-2641">Şu anda kopyalama etkinliği kaynağında olduğunda türü **WebSource**, hiçbir ek özellikler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="21f3d-2642">Örnek</span><span class="sxs-lookup"><span data-stu-id="21f3d-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="21f3d-2643">Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="21f3d-2644">ORTAMLAR İŞLEM</span><span class="sxs-lookup"><span data-stu-id="21f3d-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="21f3d-2645">Aşağıdaki tablo, veri fabrikası ve bunlar üzerinde çalışan dönüştürme etkinlikleri tarafından desteklenen bilgi işlem ortamları listeler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="21f3d-2646">Bir data factory'ye bağlamak bağlı hizmet JSON şemaları görmek ilgilendiğiniz işlem bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="21f3d-2647">İşlem ortamı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2647">Compute environment</span></span> | <span data-ttu-id="21f3d-2648">Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="21f3d-2649">[İsteğe bağlı Hdınsight kümesi](#on-demand-azure-hdinsight-cluster) veya [kendi Hdınsight kümenizi](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="21f3d-2650">[.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinliği](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="21f3d-2651">Azure toplu işlem</span><span class="sxs-lookup"><span data-stu-id="21f3d-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="21f3d-2652">.NET özel etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="21f3d-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="21f3d-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="21f3d-2654">[Toplu iş yürütme etkinliği makine](#machine-learning-batch-execution-activity), [kaynak güncelleştirme etkinliği makine](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="21f3d-2655">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="21f3d-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="21f3d-2656">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="21f3d-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="21f3d-2657">[Azure SQL veritabanı](#azure-sql-database-1), [Azure SQL veri ambarı](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="21f3d-2658">Saklı Yordam</span><span class="sxs-lookup"><span data-stu-id="21f3d-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="21f3d-2659">İsteğe bağlı Azure Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="21f3d-2660">Azure Data Factory hizmetinin otomatik olarak bir Windows/Linux tabanlı isteğe bağlı Hdınsight kümesi verileri işlemek için oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="21f3d-2661">Küme kümeyle ilişkili depolama hesabı (JSON özelliğinde linkedServiceName) ile aynı bölgede oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="21f3d-2662">Bu bağlı hizmete aşağıdaki dönüştürme etkinlikleri çalıştırabilirsiniz: [.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinlik](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2663">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2663">Linked service</span></span> 
<span data-ttu-id="21f3d-2664">Aşağıdaki tabloda bir isteğe bağlı Hdınsight bağlı hizmeti Azure JSON tanımında kullanılan özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="21f3d-2665">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2665">Property</span></span> | <span data-ttu-id="21f3d-2666">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2666">Description</span></span> | <span data-ttu-id="21f3d-2667">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2668">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-2668">type</span></span> |<span data-ttu-id="21f3d-2669">Type özelliği ayarlanmalı **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="21f3d-2670">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2670">Yes</span></span> |
| <span data-ttu-id="21f3d-2671">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="21f3d-2671">clusterSize</span></span> |<span data-ttu-id="21f3d-2672">Kümedeki çalışan/veri düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="21f3d-2673">Hdınsight kümesi için bu özelliği belirtmeniz çalışan düğüm sayısı ile birlikte 2 baş düğümler ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="21f3d-2674">Düğüm boyutu 4 çalışan düğümlü bir küme 24 çekirdek alır, böylece 4 çekirdeğe sahip Standard_D3 olduğundan (4\*4 = 16 çekirdek çalışan düğümleri artı 2\*4 = 8 çekirdek baş düğümler için).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="21f3d-2675">Bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) Standard_D3 katmanı hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="21f3d-2676">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2676">Yes</span></span> |
| <span data-ttu-id="21f3d-2677">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="21f3d-2677">timetolive</span></span> |<span data-ttu-id="21f3d-2678">İsteğe bağlı Hdınsight kümesi için izin verilen boşta kalma süresi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="21f3d-2679">Ne kadar süreyle isteğe bağlı Hdınsight kümesi kümedeki diğer etkin iş yok varsa bir etkinlik tamamlandıktan sonra canlı kalır belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="21f3d-2680">Örneğin, bir etkinlik Çalıştır 6 dakika sürer ve timetolive 5 dakika olarak ayarlanmıştır, küme 6 etkinlik işleme dakika çalıştırdıktan sonra 5 dakika boyunca etkin kalır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="21f3d-2681">Başka bir etkinlik 6 dakika penceresiyle yürütülürse, aynı küme tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="21f3d-2682">İsteğe bağlı Hdınsight kümesi oluşturma bir pahalı işlemi (işlem zaman alabilir), bunu kullanımı isteğe bağlı Hdınsight kümesi yeniden kullanarak bir veri fabrikası performansını artırmak için bu ayarı olarak gerekli olur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="21f3d-2683">Timetolive değeri 0 olarak ayarlarsanız, etkinliği çalıştırmak hemen işlenen küme silinir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="21f3d-2684">Diğer taraftan, yüksek bir değer ayarlarsanız, kümenin yüksek maliyetlerini gereksiz yere kaynaklanan boşta kalır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="21f3d-2685">Bu nedenle, gereksinimlerinize göre uygun değere ayarlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="21f3d-2686">Timetolive özellik değerini uygun şekilde ayarlanmışsa, birden çok ardışık düzen isteğe bağlı Hdınsight kümesi aynı kopyasını paylaştığında</span><span class="sxs-lookup"><span data-stu-id="21f3d-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="21f3d-2687">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2687">Yes</span></span> |
| <span data-ttu-id="21f3d-2688">Sürüm</span><span class="sxs-lookup"><span data-stu-id="21f3d-2688">version</span></span> |<span data-ttu-id="21f3d-2689">Hdınsight küme sürümü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="21f3d-2690">Ayrıntılar için bkz [desteklenen Azure Data Factory'de Hdınsight sürümleri](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="21f3d-2691">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2691">No</span></span> |
| <span data-ttu-id="21f3d-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2692">linkedServiceName</span></span> |<span data-ttu-id="21f3d-2693">Depolamak ve veri işleme için isteğe bağlı küme tarafından kullanılacak azure depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="21f3d-2694">Şu anda bir Azure Data Lake Store depolama alanı olarak kullanan bir isteğe bağlı Hdınsight kümesi oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="21f3d-2695">Bir Azure Data Lake Store'da işleme Hdınsight sonuç verileri depolamak istiyorsanız, Azure Blob depolama alanından Azure Data Lake Store'a veri kopyalamak için kopyalama etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="21f3d-2696">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2696">Yes</span></span> |
| <span data-ttu-id="21f3d-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="21f3d-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="21f3d-2698">Data Factory hizmetinin bunları sizin adınıza kaydedebilirsiniz böylece Hdınsight için ek depolama hesapları hizmeti bağlı belirtir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="21f3d-2699">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2699">No</span></span> |
| <span data-ttu-id="21f3d-2700">osType</span><span class="sxs-lookup"><span data-stu-id="21f3d-2700">osType</span></span> |<span data-ttu-id="21f3d-2701">İşletim sistemi türü.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2701">Type of operating system.</span></span> <span data-ttu-id="21f3d-2702">İzin verilen değerler: (varsayılan) Windows ve Linux</span><span class="sxs-lookup"><span data-stu-id="21f3d-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="21f3d-2703">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2703">No</span></span> |
| <span data-ttu-id="21f3d-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="21f3d-2705">Azure SQL adını HCatalog veritabanına işaret hizmeti bağlı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="21f3d-2706">İsteğe bağlı Hdınsight kümesi meta depo Azure SQL veritabanı kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="21f3d-2707">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="21f3d-2708">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2708">JSON example</span></span>
<span data-ttu-id="21f3d-2709">Aşağıdaki JSON Linux tabanlı isteğe bağlı Hdınsight bağlı hizmeti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="21f3d-2710">Data Factory hizmetinin otomatik olarak oluşturur bir **Linux tabanlı** veri dilimi işlerken Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="21f3d-2711">Daha fazla bilgi için bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="21f3d-2712">Var olan Azure Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="21f3d-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="21f3d-2713">Kendi Hdınsight kümenizi Data Factory ile kaydetmek için bir Azure Hdınsight bağlı hizmeti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="21f3d-2714">Bu bağlı hizmete aşağıdaki veri dönüştürme etkinlikleri çalıştırabilirsiniz: [.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinlik](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2715">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2715">Linked service</span></span>
<span data-ttu-id="21f3d-2716">Aşağıdaki tabloda Azure Hdınsight bağlı hizmeti Azure JSON tanımında kullanılan özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="21f3d-2717">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2717">Property</span></span> | <span data-ttu-id="21f3d-2718">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2718">Description</span></span> | <span data-ttu-id="21f3d-2719">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2720">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-2720">type</span></span> |<span data-ttu-id="21f3d-2721">Type özelliği ayarlanmalı **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="21f3d-2722">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2722">Yes</span></span> |
| <span data-ttu-id="21f3d-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="21f3d-2723">clusterUri</span></span> |<span data-ttu-id="21f3d-2724">Hdınsight küme URI'si.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="21f3d-2725">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2725">Yes</span></span> |
| <span data-ttu-id="21f3d-2726">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2726">username</span></span> |<span data-ttu-id="21f3d-2727">Var olan bir Hdınsight kümesine bağlanmak için kullanılacak kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="21f3d-2728">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2728">Yes</span></span> |
| <span data-ttu-id="21f3d-2729">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2729">password</span></span> |<span data-ttu-id="21f3d-2730">Kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2730">Specify password for the user account.</span></span> |<span data-ttu-id="21f3d-2731">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2731">Yes</span></span> |
| <span data-ttu-id="21f3d-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2732">linkedServiceName</span></span> | <span data-ttu-id="21f3d-2733">Hdınsight küme tarafından kullanılan Azure blob depolama başvurduğu Azure Storage bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="21f3d-2734">Şu anda bu özellik için bir Azure Data Lake Store bağlı belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="21f3d-2735">Hdınsight kümesi için Data Lake Store erişimi varsa Azure Data Lake Store'da verileri Hive/Pig komut dosyalarından erişebilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="21f3d-2736">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2736">Yes</span></span> |

<span data-ttu-id="21f3d-2737">Hdınsight kümeleri desteklenen sürümleri için bkz: [desteklenen Hdınsight sürümleri](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="21f3d-2738">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="21f3d-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="21f3d-2739">Azure Batch</span></span>
<span data-ttu-id="21f3d-2740">Batch havuzundaki sanal makineler (VM'ler) kaydetmek için bir Azure Batch bağlantılı hizmeti bir data factory ile oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="21f3d-2741">.NET özel etkinlikler Azure Batch ya da Azure Hdınsight kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="21f3d-2742">Çalıştırabilirsiniz bir [.NET özel etkinlik](#net-custom-activity) bu hizmeti bağlı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2743">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2743">Linked service</span></span>
<span data-ttu-id="21f3d-2744">Aşağıdaki tabloda bir Azure Batch bağlı hizmeti Azure JSON tanımında kullanılan özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="21f3d-2745">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2745">Property</span></span> | <span data-ttu-id="21f3d-2746">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2746">Description</span></span> | <span data-ttu-id="21f3d-2747">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2748">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-2748">type</span></span> |<span data-ttu-id="21f3d-2749">Type özelliği ayarlanmalı **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="21f3d-2750">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2750">Yes</span></span> |
| <span data-ttu-id="21f3d-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2751">accountName</span></span> |<span data-ttu-id="21f3d-2752">Azure toplu işlem hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="21f3d-2753">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2753">Yes</span></span> |
| <span data-ttu-id="21f3d-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="21f3d-2754">accessKey</span></span> |<span data-ttu-id="21f3d-2755">Azure Batch hesabı için erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="21f3d-2756">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2756">Yes</span></span> |
| <span data-ttu-id="21f3d-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2757">poolName</span></span> |<span data-ttu-id="21f3d-2758">Sanal makinelerin havuzunun adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="21f3d-2759">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2759">Yes</span></span> |
| <span data-ttu-id="21f3d-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2760">linkedServiceName</span></span> |<span data-ttu-id="21f3d-2761">Azure depolama adı hizmeti bağlı Azure Batch hizmeti ile ilişkili bağlı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="21f3d-2762">Bu bağlı hizmetin etkinlik ve Etkinlik yürütme günlüklerini depolamak çalıştırmak için gerekli hazırlama dosyaları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="21f3d-2763">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="21f3d-2764">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="21f3d-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="21f3d-2765">Azure Machine Learning</span></span>
<span data-ttu-id="21f3d-2766">Bir Machine Learning toplu Puanlama uç noktası data factory ile kaydetmek için bir Azure Machine Learning bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="21f3d-2767">Bu bilgisayarda çalıştırabilir iki veri dönüştürme etkinlikleri bağlantılı hizmeti: [Machine Learning toplu iş yürütme etkinliği](#machine-learning-batch-execution-activity), [Machine Learning kaynak güncelleştirme etkinliği](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2768">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2768">Linked service</span></span>
<span data-ttu-id="21f3d-2769">Aşağıdaki tabloda bir Azure Machine Learning bağlı hizmeti Azure JSON tanımında kullanılan özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="21f3d-2770">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2770">Property</span></span> | <span data-ttu-id="21f3d-2771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2771">Description</span></span> | <span data-ttu-id="21f3d-2772">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2773">Tür</span><span class="sxs-lookup"><span data-stu-id="21f3d-2773">Type</span></span> |<span data-ttu-id="21f3d-2774">Type özelliği ayarlanmalıdır: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="21f3d-2775">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2775">Yes</span></span> |
| <span data-ttu-id="21f3d-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="21f3d-2776">mlEndpoint</span></span> |<span data-ttu-id="21f3d-2777">Toplu Puanlama URL.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2777">The batch scoring URL.</span></span> |<span data-ttu-id="21f3d-2778">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2778">Yes</span></span> |
| <span data-ttu-id="21f3d-2779">apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="21f3d-2779">apiKey</span></span> |<span data-ttu-id="21f3d-2780">Yayımlanan çalışma alanı modelinin API.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="21f3d-2781">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="21f3d-2782">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="21f3d-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="21f3d-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="21f3d-2784">Oluşturduğunuz bir **Azure Data Lake Analytics** bir Azure Data Lake Analytics bağlamak için bağlı hizmet kullanmadan önce bir Azure data factory hizmetine işlem [Data Lake Analytics U-SQL etkinliği](data-factory-usql-activity.md) ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="21f3d-2785">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2785">Linked service</span></span>

<span data-ttu-id="21f3d-2786">Aşağıdaki tabloda bir Azure Data Lake Analytics bağlantılı hizmeti JSON tanımında kullanılan özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="21f3d-2787">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2787">Property</span></span> | <span data-ttu-id="21f3d-2788">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2788">Description</span></span> | <span data-ttu-id="21f3d-2789">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2790">Tür</span><span class="sxs-lookup"><span data-stu-id="21f3d-2790">Type</span></span> |<span data-ttu-id="21f3d-2791">Type özelliği ayarlanmalıdır: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="21f3d-2792">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2792">Yes</span></span> |
| <span data-ttu-id="21f3d-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2793">accountName</span></span> |<span data-ttu-id="21f3d-2794">Azure Data Lake Analytics hesap adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="21f3d-2795">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2795">Yes</span></span> |
| <span data-ttu-id="21f3d-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="21f3d-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="21f3d-2797">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="21f3d-2798">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2798">No</span></span> |
| <span data-ttu-id="21f3d-2799">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="21f3d-2799">authorization</span></span> |<span data-ttu-id="21f3d-2800">Yetkilendirme kodu, tıkladıktan sonra otomatik olarak alınır **Authorize** Data Factory Düzenleyici'düğmesine tıklayın ve OAuth oturum açma tamamlanıyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="21f3d-2801">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2801">Yes</span></span> |
| <span data-ttu-id="21f3d-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="21f3d-2802">subscriptionId</span></span> |<span data-ttu-id="21f3d-2803">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2803">Azure subscription id</span></span> |<span data-ttu-id="21f3d-2804">Hayır (belirtilmezse, data Factory abonelik kullanılır).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="21f3d-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2805">resourceGroupName</span></span> |<span data-ttu-id="21f3d-2806">Azure kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2806">Azure resource group name</span></span> |<span data-ttu-id="21f3d-2807">Hayır (belirtilmezse, kaynak grubu data Factory kullanılır).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="21f3d-2808">SessionID</span><span class="sxs-lookup"><span data-stu-id="21f3d-2808">sessionId</span></span> |<span data-ttu-id="21f3d-2809">OAuth yetkilendirme oturumundan oturum kimliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="21f3d-2810">Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="21f3d-2811">Data Factory Düzenleyici kullandığınızda, bu otomatik olarak oluşturulan kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="21f3d-2812">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="21f3d-2813">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2813">JSON example</span></span>
<span data-ttu-id="21f3d-2814">Aşağıdaki örnek bir Azure Data Lake Analytics bağlantılı hizmeti için JSON tanımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="21f3d-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="21f3d-2815">Azure SQL Database</span></span>
<span data-ttu-id="21f3d-2816">Azure SQL bağlı hizmeti oluşturma ve onunla kullanma [saklı yordam etkinliği](#stored-procedure-activity) Data Factory işlem hattı bir saklı yordam çağırmak için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2817">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2817">Linked service</span></span>
<span data-ttu-id="21f3d-2818">Bağlantılı hizmeti bir Azure SQL veritabanı tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureSqlDatabase**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2819">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2819">Property</span></span> | <span data-ttu-id="21f3d-2820">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2820">Description</span></span> | <span data-ttu-id="21f3d-2821">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-2822">connectionString</span></span> |<span data-ttu-id="21f3d-2823">ConnectionString özelliği için Azure SQL veritabanı örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="21f3d-2824">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="21f3d-2825">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="21f3d-2826">Bkz: [Azure SQL Bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makale bu bağlı hizmetin hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="21f3d-2827">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="21f3d-2828">Bir Azure SQL Data Warehouse bağlı hizmet oluşturma ve onunla kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) Data Factory işlem hattı bir saklı yordam çağırmak için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2829">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2829">Linked service</span></span>
<span data-ttu-id="21f3d-2830">Bağlantılı hizmetinin Azure SQL Data Warehouse tanımlamak için Ayarla **türü** bağlantılı hizmetinin **AzureSqlDW**ve aşağıdaki özellikleri belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="21f3d-2831">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2831">Property</span></span> | <span data-ttu-id="21f3d-2832">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2832">Description</span></span> | <span data-ttu-id="21f3d-2833">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-2834">connectionString</span></span> |<span data-ttu-id="21f3d-2835">ConnectionString özelliği için Azure SQL Data Warehouse örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="21f3d-2836">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="21f3d-2837">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="21f3d-2838">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="21f3d-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="21f3d-2839">SQL Server</span></span> 
<span data-ttu-id="21f3d-2840">Bir SQL Server bağlantılı hizmet oluşturma ve onunla kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) Data Factory işlem hattı bir saklı yordam çağırmak için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="21f3d-2841">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2841">Linked service</span></span>
<span data-ttu-id="21f3d-2842">Bağlı hizmet türü oluşturma **OnPremisesSqlServer** bir şirket içi SQL Server veritabanını data factory'ye bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="21f3d-2843">Aşağıdaki tabloda şirket içi SQL Server bağlantılı hizmete özgü JSON öğeleri açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="21f3d-2844">Aşağıdaki tabloda, SQL Server bağlantılı hizmete özgü JSON öğeleri açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="21f3d-2845">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2845">Property</span></span> | <span data-ttu-id="21f3d-2846">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2846">Description</span></span> | <span data-ttu-id="21f3d-2847">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2848">type</span><span class="sxs-lookup"><span data-stu-id="21f3d-2848">type</span></span> |<span data-ttu-id="21f3d-2849">Type özelliği ayarlanmalıdır: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="21f3d-2850">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2850">Yes</span></span> |
| <span data-ttu-id="21f3d-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="21f3d-2851">connectionString</span></span> |<span data-ttu-id="21f3d-2852">SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak şirket içi SQL Server veritabanına bağlanmak için gereken connectionString bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="21f3d-2853">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2853">Yes</span></span> |
| <span data-ttu-id="21f3d-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21f3d-2854">gatewayName</span></span> |<span data-ttu-id="21f3d-2855">Data Factory hizmetinin şirket içi SQL Server veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="21f3d-2856">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2856">Yes</span></span> |
| <span data-ttu-id="21f3d-2857">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2857">username</span></span> |<span data-ttu-id="21f3d-2858">Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="21f3d-2859">Örnek: **domainname\\kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="21f3d-2860">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2860">No</span></span> |
| <span data-ttu-id="21f3d-2861">password</span><span class="sxs-lookup"><span data-stu-id="21f3d-2861">password</span></span> |<span data-ttu-id="21f3d-2862">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="21f3d-2863">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2863">No</span></span> |

<span data-ttu-id="21f3d-2864">Kimlik bilgilerini kullanarak şifreleyebilirsiniz **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları aşağıdaki örnekte gösterildiği gibi bağlantı dizesini kullanın (**EncryptedCredential** özellik):</span><span class="sxs-lookup"><span data-stu-id="21f3d-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="21f3d-2865">Örnek: SQL kimlik doğrulaması kullanmak için JSON</span><span class="sxs-lookup"><span data-stu-id="21f3d-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="21f3d-2866">Örnek: JSON'ı Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="21f3d-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="21f3d-2867">Kullanıcı adı ve parolası belirtilmişse, ağ geçidi bunları şirket içi SQL Server veritabanına bağlanmak için belirtilen kullanıcı hesabının kimliğine bürün kullanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="21f3d-2868">Aksi takdirde, ağ geçidi SQL Server Ağ Geçidi (kendi başlangıç hesabı) güvenlik bağlamı ile doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="21f3d-2869">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="21f3d-2870">VERİ DÖNÜŞTÜRME ETKİNLİKLERİ</span><span class="sxs-lookup"><span data-stu-id="21f3d-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="21f3d-2871">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2871">Activity</span></span> | <span data-ttu-id="21f3d-2872">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="21f3d-2873">Hdınsight Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="21f3d-2874">Data Factory işlem hattı Hdınsight Hive etkinliğinde, Hive sorguları kendi veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="21f3d-2875">Hdınsight Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="21f3d-2876">Data Factory işlem hattı Hdınsight Pig etkinliğinde kendi Pig sorgular veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="21f3d-2877">HDInsight MapReduce Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="21f3d-2878">Data Factory işlem hattı Hdınsight MapReduce etkinliğinde kendi MapReduce programları veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="21f3d-2879">HDInsight Akış Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="21f3d-2880">Hdınsight akış etkinliğinde Data Factory işlem hattı Hadoop akış programlar kendi veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="21f3d-2881">HDInsight Spark Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="21f3d-2882">Data Factory işlem hattı Hdınsight Spark etkinliğinde Spark programlar kendi Hdınsight kümesinde yürütür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="21f3d-2883">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="21f3d-2884">Azure Data Factory, Tahmine dayalı analiz için yayımlanan bir Azure Machine Learning web hizmetini kullan ardışık düzen kolayca oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="21f3d-2885">Toplu iş yürütme etkinliği Azure Data Factory ardışık düzeninde kullanarak, bir Machine Learning web hizmeti toplu veriler üzerinde tahminlerde çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="21f3d-2886">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="21f3d-2887">Zaman içinde denemeler Puanlama Machine Learning Tahmine dayalı modelleri yeni giriş veri kümeleri kullanarak retrained gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="21f3d-2888">Yeniden eğitme ile tamamladıktan sonra ile retrained Machine Learning modeli Puanlama web hizmetini güncelleştirmek istiyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="21f3d-2889">Web hizmeti ile yeni eğitilen modeli güncelleştirmek için güncelleştirme kaynağı etkinliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="21f3d-2890">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="21f3d-2891">Aşağıdaki veri depolarına birinde bir saklı yordam çağrılacak bir Data Factory işlem hattı saklı yordam etkinliği kullanabilirsiniz: Azure SQL Database, Azure SQL Data Warehouse, SQL Server veritabanı kuruluşunuzdaki veya bir Azure VM.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="21f3d-2892">Data Lake Analytics U-SQL etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="21f3d-2893">Data Lake Analytics U-SQL etkinliği Azure Data Lake Analytics kümede bir U-SQL komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="21f3d-2894">.NET özel etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="21f3d-2895">Veri fabrikası tarafından desteklenmeyen bir şekilde veri dönüştürme ihtiyacınız varsa, kendi veri işleme mantığı ile özel bir etkinlik oluşturmak ve ardışık düzeninde etkinlik kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="21f3d-2896">Bir Azure Batch hizmeti ya da Azure Hdınsight kümesi kullanarak çalıştırmak için özel .NET etkinliği yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="21f3d-2897">HDInsight Hive Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="21f3d-2898">Bir Hive etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="21f3d-2899">Etkinlik türü özelliği olması gerekir: **Hdınsighthive**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="21f3d-2900">Hdınsight bağlı hizmeti ilk oluşturun ve değeri olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-2901">Aşağıdaki özellikler de desteklenen **typeProperties** bölüm için Hdınsighthive etkinliği türünü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="21f3d-2902">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2902">Property</span></span> | <span data-ttu-id="21f3d-2903">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2903">Description</span></span> | <span data-ttu-id="21f3d-2904">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2905">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="21f3d-2905">script</span></span> |<span data-ttu-id="21f3d-2906">Hive betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="21f3d-2907">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2907">No</span></span> |
| <span data-ttu-id="21f3d-2908">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="21f3d-2908">script path</span></span> |<span data-ttu-id="21f3d-2909">Hive betiği bir Azure blob storage'da depolamak ve dosyanın yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="21f3d-2910">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="21f3d-2911">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2911">Both cannot be used together.</span></span> <span data-ttu-id="21f3d-2912">Dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="21f3d-2913">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2913">No</span></span> |
| <span data-ttu-id="21f3d-2914">tanımlar</span><span class="sxs-lookup"><span data-stu-id="21f3d-2914">defines</span></span> |<span data-ttu-id="21f3d-2915">'Hiveconf' kullanarak Hive betiğini içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="21f3d-2916">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2916">No</span></span> |

<span data-ttu-id="21f3d-2917">Bu tür özellikleri için Hive etkinliği özgüdür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="21f3d-2918">Diğer özellikler (dışında typeProperties bölüm) tüm etkinlikler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="21f3d-2919">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2919">JSON example</span></span>
<span data-ttu-id="21f3d-2920">Aşağıdaki JSON ardışık düzeninde Hdınsight Hive etkinliği tanımlar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
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

<span data-ttu-id="21f3d-2921">Daha fazla bilgi için bkz: [Hive etkinliği](data-factory-hive-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="21f3d-2922">HDInsight Pig Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="21f3d-2923">Pig etkinlik JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="21f3d-2924">Etkinlik türü özelliği olması gerekir: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="21f3d-2925">Hdınsight bağlı hizmeti ilk oluşturun ve değeri olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-2926">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için HDInsightPig ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="21f3d-2927">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2927">Property</span></span> | <span data-ttu-id="21f3d-2928">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2928">Description</span></span> | <span data-ttu-id="21f3d-2929">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2930">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="21f3d-2930">script</span></span> |<span data-ttu-id="21f3d-2931">Pig betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="21f3d-2932">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2932">No</span></span> |
| <span data-ttu-id="21f3d-2933">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="21f3d-2933">script path</span></span> |<span data-ttu-id="21f3d-2934">Pig betiği bir Azure blob storage'da depolamak ve dosyanın yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="21f3d-2935">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="21f3d-2936">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2936">Both cannot be used together.</span></span> <span data-ttu-id="21f3d-2937">Dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="21f3d-2938">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2938">No</span></span> |
| <span data-ttu-id="21f3d-2939">tanımlar</span><span class="sxs-lookup"><span data-stu-id="21f3d-2939">defines</span></span> |<span data-ttu-id="21f3d-2940">Pig betiği içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="21f3d-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="21f3d-2941">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2941">No</span></span> |

<span data-ttu-id="21f3d-2942">Bu tür özellikleri, Pig etkinlik özgüdür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="21f3d-2943">Diğer özellikler (dışında typeProperties bölüm) tüm etkinlikler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="21f3d-2944">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2944">JSON example</span></span>

```json
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

<span data-ttu-id="21f3d-2945">Daha fazla bilgi için bkz: [Pig etkinlik](#data-factory-pig-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="21f3d-2946">HDInsight MapReduce Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="21f3d-2947">Bir MapReduce etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="21f3d-2948">Etkinlik türü özelliği olması gerekir: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="21f3d-2949">Hdınsight bağlı hizmeti ilk oluşturun ve değeri olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-2950">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için HDInsightMapReduce ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="21f3d-2951">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2951">Property</span></span> | <span data-ttu-id="21f3d-2952">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2952">Description</span></span> | <span data-ttu-id="21f3d-2953">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="21f3d-2954">jarLinkedService</span></span> | <span data-ttu-id="21f3d-2955">JAR dosyasını içeren Azure depolama bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="21f3d-2956">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2956">Yes</span></span> |
| <span data-ttu-id="21f3d-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="21f3d-2957">jarFilePath</span></span> | <span data-ttu-id="21f3d-2958">Azure storage'da JAR dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="21f3d-2959">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2959">Yes</span></span> | 
| <span data-ttu-id="21f3d-2960">className</span><span class="sxs-lookup"><span data-stu-id="21f3d-2960">className</span></span> | <span data-ttu-id="21f3d-2961">JAR dosyasını ana sınıfının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="21f3d-2962">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-2962">Yes</span></span> | 
| <span data-ttu-id="21f3d-2963">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2963">arguments</span></span> | <span data-ttu-id="21f3d-2964">Bağımsız değişkenleri MapReduce program virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="21f3d-2965">Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) MapReduce çerçeveden.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="21f3d-2966">MapReduce bağımsız değişkenleriyle ayırt etmek için seçeneği ve değer bağımsız değişken olarak aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. olan göre bunların değerleri hemen ardından seçenekleri)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="21f3d-2967">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="21f3d-2968">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="21f3d-2969">Daha fazla bilgi için bkz: [MapReduce etkinliği](data-factory-map-reduce.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="21f3d-2970">HDInsight Akış Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="21f3d-2971">Bir Hadoop akış etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="21f3d-2972">Etkinlik türü özelliği olması gerekir: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="21f3d-2973">Hdınsight bağlı hizmeti ilk oluşturun ve değeri olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-2974">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için HDInsightStreaming ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="21f3d-2975">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-2975">Property</span></span> | <span data-ttu-id="21f3d-2976">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="21f3d-2977">Eşleyici</span><span class="sxs-lookup"><span data-stu-id="21f3d-2977">mapper</span></span> | <span data-ttu-id="21f3d-2978">Yürütülebilir Eşleyici adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2978">Name of the mapper executable.</span></span> <span data-ttu-id="21f3d-2979">Örnekte, cat.exe yürütülebilir Eşleyici ' dir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="21f3d-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="21f3d-2980">reducer</span></span> | <span data-ttu-id="21f3d-2981">Yürütülebilir reducer adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2981">Name of the reducer executable.</span></span> <span data-ttu-id="21f3d-2982">Örnekte, wc.exe yürütülebilir reducer ' dir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="21f3d-2983">Giriş</span><span class="sxs-lookup"><span data-stu-id="21f3d-2983">input</span></span> | <span data-ttu-id="21f3d-2984">Eşleyici için girdi dosyası (konum dahil).</span><span class="sxs-lookup"><span data-stu-id="21f3d-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="21f3d-2985">Örnekte: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample blob kapsayıcısı, veri/örnek/Gutenberg klasördür ve davinci.txt blob.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="21f3d-2986">Çıktı</span><span class="sxs-lookup"><span data-stu-id="21f3d-2986">output</span></span> | <span data-ttu-id="21f3d-2987">Çıktı dosyası (konum dahil) reducer için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="21f3d-2988">Hadoop akış işi çıkışı, bu özellik için belirtilen konuma yazılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="21f3d-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="21f3d-2989">filePaths</span></span> | <span data-ttu-id="21f3d-2990">Eşleyici ve reducer yürütülebilir dosyalar için yollar.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="21f3d-2991">Örnekte: "adfsample/example/apps/wc.exe" adfsample blob kapsayıcısı, örnek/uygulamaları klasördür ve wc.exe çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="21f3d-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="21f3d-2992">fileLinkedService</span></span> | <span data-ttu-id="21f3d-2993">FilePaths bölümünde belirtilen dosyaları içeren Azure depolama temsil eden azure depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="21f3d-2994">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="21f3d-2994">arguments</span></span> | <span data-ttu-id="21f3d-2995">Bağımsız değişkenleri MapReduce program virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="21f3d-2996">Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) MapReduce çerçeveden.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="21f3d-2997">MapReduce bağımsız değişkenleriyle ayırt etmek için seçeneği ve değer bağımsız değişken olarak aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. olan göre bunların değerleri hemen ardından seçenekleri)</span><span class="sxs-lookup"><span data-stu-id="21f3d-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="21f3d-2998">Getdebugınfo</span><span class="sxs-lookup"><span data-stu-id="21f3d-2998">getDebugInfo</span></span> | <span data-ttu-id="21f3d-2999">İsteğe bağlı bir öğe.</span><span class="sxs-lookup"><span data-stu-id="21f3d-2999">An optional element.</span></span> <span data-ttu-id="21f3d-3000">Hata için ayarlandığında, günlükleri yalnızca hatada indirilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="21f3d-3001">Tüm ayarlandığında, günlükleri yürütme durumu bağımsız olarak daima yüklenir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="21f3d-3002">Hadoop akış etkinliği için bir çıkış veri kümesi belirtmelisiniz **çıkarır** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="21f3d-3003">Bu veri kümesi yalnızca ardışık düzen zamanlama (saatlik, günlük, vs.) sürücü için gereken bir kukla dataset olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="21f3d-3004">Etkinliği bir girdi almazsa, etkinliği için bir giriş veri kümesi belirtme atlayabilirsiniz **girişleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="21f3d-3005">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3005">JSON example</span></span>

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="21f3d-3006">Daha fazla bilgi için bkz: [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="21f3d-3007">HDInsight Spark Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="21f3d-3008">Bir Spark etkinlik JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="21f3d-3009">Etkinlik türü özelliği olması gerekir: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="21f3d-3010">Hdınsight bağlı hizmeti ilk oluşturun ve değeri olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-3011">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için HDInsightSpark ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="21f3d-3012">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3012">Property</span></span> | <span data-ttu-id="21f3d-3013">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-3013">Description</span></span> | <span data-ttu-id="21f3d-3014">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="21f3d-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-3015">rootPath</span></span> | <span data-ttu-id="21f3d-3016">Azure Blob kapsayıcısı ve Spark dosyasını içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="21f3d-3017">Dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="21f3d-3018">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3018">Yes</span></span> |
| <span data-ttu-id="21f3d-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="21f3d-3019">entryFilePath</span></span> | <span data-ttu-id="21f3d-3020">Spark kod/paketi kök klasörüne göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="21f3d-3021">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3021">Yes</span></span> |
| <span data-ttu-id="21f3d-3022">className</span><span class="sxs-lookup"><span data-stu-id="21f3d-3022">className</span></span> | <span data-ttu-id="21f3d-3023">Uygulamanın Java/Spark ana sınıfı</span><span class="sxs-lookup"><span data-stu-id="21f3d-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="21f3d-3024">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3024">No</span></span> | 
| <span data-ttu-id="21f3d-3025">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="21f3d-3025">arguments</span></span> | <span data-ttu-id="21f3d-3026">Spark programın komut satırı bağımsız değişkenleri listesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="21f3d-3027">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3027">No</span></span> | 
| <span data-ttu-id="21f3d-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="21f3d-3028">proxyUser</span></span> | <span data-ttu-id="21f3d-3029">Spark program yürütülmeye kimliğine bürünmek için kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="21f3d-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="21f3d-3030">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3030">No</span></span> | 
| <span data-ttu-id="21f3d-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="21f3d-3031">sparkConfig</span></span> | <span data-ttu-id="21f3d-3032">Spark yapılandırma özellikleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3032">Spark configuration properties.</span></span> | <span data-ttu-id="21f3d-3033">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3033">No</span></span> | 
| <span data-ttu-id="21f3d-3034">Getdebugınfo</span><span class="sxs-lookup"><span data-stu-id="21f3d-3034">getDebugInfo</span></span> | <span data-ttu-id="21f3d-3035">Hdınsight küme tarafından kullanılan Azure depolama Spark günlük dosyalarının ne zaman kopyalanır belirtir (veya) sparkJobLinkedService tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="21f3d-3036">İzin verilen değerler: None, her zaman veya hata.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="21f3d-3037">Varsayılan değer: yok.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3037">Default value: None.</span></span> | <span data-ttu-id="21f3d-3038">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3038">No</span></span> | 
| <span data-ttu-id="21f3d-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="21f3d-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="21f3d-3040">Azure Storage bağlı Spark iş dosyası, bağımlılıklar ve günlükleri tutan hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="21f3d-3041">Bu özellik için bir değer belirtmezseniz, Hdınsight kümesi ile ilişkili depolama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="21f3d-3042">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="21f3d-3043">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="21f3d-3044">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3044">Note the following points:</span></span> 

- <span data-ttu-id="21f3d-3045">**Türü** özelliği ayarlanmış **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="21f3d-3046">**RootPath** ayarlanır **adfspark\\pyFiles** burada adfspark, Azure Blob kapsayıcısında ve pyFiles kapsayıcıdaki ince klasördür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="21f3d-3047">Bu örnekte, Azure Blob Storage Spark kümesi ile ilişkili adrestir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="21f3d-3048">Farklı bir Azure depolama dosyayı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="21f3d-3049">Bunu yaparsanız, bu depolama hesabı data factory'ye bağlamak için bir Azure depolama bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="21f3d-3050">Ardından, bağlı hizmetin adı için bir değer olarak belirtin **sparkJobLinkedService** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="21f3d-3051">Bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bu özellik ve Spark etkinlik tarafından desteklenen diğer özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="21f3d-3052">**EntryFilePath** ayarlanır **test.py**, python dosyası değil.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="21f3d-3053">**Getdebugınfo** özelliği ayarlanmış **her zaman**, günlük dosyaları her zaman anlamına gelir (başarılı veya başarısız) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="21f3d-3054">Bir sorunu gidermeye çalışıyor değilseniz, bu özellik her zaman bir üretim ortamında ayarlamak değil kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="21f3d-3055">**Çıkarır** bölümü bir çıkış veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="21f3d-3056">Spark program herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="21f3d-3057">Çıktı veri kümesi, ardışık düzen (saatlik, günlük, vs.) için zamanlamayı sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="21f3d-3058">Etkinliği hakkında daha fazla bilgi için bkz: [Spark etkinlik](data-factory-spark.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="21f3d-3059">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="21f3d-3060">Azure ML toplu iş yürütme etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="21f3d-3061">Etkinlik türü özelliği olması gerekir: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="21f3d-3062">Bağlantılı hizmet ilk öğrenme Azure bir makine oluşturma ve için bir değer olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-3063">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için AzureMLBatchExecution ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="21f3d-3064">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3064">Property</span></span> | <span data-ttu-id="21f3d-3065">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-3065">Description</span></span> | <span data-ttu-id="21f3d-3066">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="21f3d-3067">WebServiceInput etkinliğine</span><span class="sxs-lookup"><span data-stu-id="21f3d-3067">webServiceInput</span></span> | <span data-ttu-id="21f3d-3068">Azure ML web hizmeti için bir giriş olarak geçirilecek veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="21f3d-3069">Bu veri kümesi de etkinliğinin girdi bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="21f3d-3070">WebServiceInput etkinliğine veya webServiceInputs kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="21f3d-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="21f3d-3071">webServiceInputs</span></span> | <span data-ttu-id="21f3d-3072">Azure ML web hizmeti girişleri olarak geçirilecek veri kümeleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="21f3d-3073">Web hizmeti birden fazla girdi aldığı durumlarda WebServiceInput etkinliğine özelliğini kullanmak yerine webServiceInputs özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="21f3d-3074">Tarafından başvurulan veri kümeleri **webServiceInputs** de dahil etkinliğin **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="21f3d-3075">WebServiceInput etkinliğine veya webServiceInputs kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="21f3d-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="21f3d-3076">webServiceOutputs</span></span> | <span data-ttu-id="21f3d-3077">Çıktı Azure ML web hizmeti olarak atanan veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="21f3d-3078">Web hizmeti, bu veri kümesini çıktı verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="21f3d-3079">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3079">Yes</span></span> | 
<span data-ttu-id="21f3d-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-3080">globalParameters</span></span> | <span data-ttu-id="21f3d-3081">Bu bölümde web hizmeti parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="21f3d-3082">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="21f3d-3083">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3083">JSON example</span></span>
<span data-ttu-id="21f3d-3084">Bu örnekte, etkinlik bir veri kümesine sahiptir **MLSqlInput** giriş olarak ve **MLSqlOutput** çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="21f3d-3085">**MLSqlInput** kullanarak geçirilen web hizmeti tarafından bir girdi olarak **WebServiceInput etkinliğine** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="21f3d-3086">**MLSqlOutput** çıkış olarak Web hizmeti tarafından kullanılarak geçirilir **webServiceOutputs** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="21f3d-3087">JSON örnekte dağıtılan Azure Machine Learning Web hizmeti, başlangıç/bitiş bir Azure SQL veritabanı veri okuma/yazma için bir okuyucu ve yazıcı modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="21f3d-3088">Aşağıdaki dört parametre bu Web hizmetini sunar: veritabanı sunucu adı, veritabanı adı, sunucu kullanıcı hesabı adı ve sunucu kullanıcı hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="21f3d-3089">Yalnızca girişleri ve çıkışları AzureMLBatchExecution etkinliğin Web hizmeti parametreleri olarak geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="21f3d-3090">Örneğin, yukarıdaki JSON parçacığında, bir giriş WebServiceInput etkinliğine parametresi Web hizmeti için bir girdi olarak geçirilen AzureMLBatchExecution etkinliğine MLSqlInput olabilir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="21f3d-3091">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="21f3d-3092">Azure ML güncelleştirme kaynak etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="21f3d-3093">Etkinlik türü özelliği olması gerekir: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="21f3d-3094">Bağlantılı hizmet ilk öğrenme Azure bir makine oluşturma ve için bir değer olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-3095">Aşağıdaki özellikler de desteklenen **typeProperties** bölüm için AzureMLUpdateResource etkinliği türünü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="21f3d-3096">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3096">Property</span></span> | <span data-ttu-id="21f3d-3097">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-3097">Description</span></span> | <span data-ttu-id="21f3d-3098">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="21f3d-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="21f3d-3099">trainedModelName</span></span> | <span data-ttu-id="21f3d-3100">Retrained modelin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3100">Name of the retrained model.</span></span> | <span data-ttu-id="21f3d-3101">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3101">Yes</span></span> |  
<span data-ttu-id="21f3d-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="21f3d-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="21f3d-3103">Yeniden eğitme işlem tarafından döndürülen iLearner dosyasını işaret eden bir veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="21f3d-3104">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="21f3d-3105">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3105">JSON example</span></span>
<span data-ttu-id="21f3d-3106">Ardışık düzen iki etkinlik vardır: **AzureMLBatchExecution** ve **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="21f3d-3107">Azure ML toplu iş yürütme etkinliği giriş olarak eğitim verileri alır ve bir iLearner dosya bir çıktı olarak üretir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="21f3d-3108">Etkinlik giriş eğitim verilerle eğitim web hizmeti (web hizmeti olarak sunulan eğitim denemenizi) çağırır ve ilearner dosya webservice alır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="21f3d-3109">PlaceholderBlob Azure Data Factory hizmeti tarafından ardışık çalıştırmak için gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="21f3d-3110">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="21f3d-3111">U-SQL etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="21f3d-3112">Etkinlik türü özelliği olması gerekir: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="21f3d-3113">Bir Azure Data Lake Analytics bağlı hizmeti oluşturma ve için bir değer olarak adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-3114">Aşağıdaki özellikler de desteklenen **typeProperties** DataLakeAnalyticsU-SQL etkinliği türünü ayarladığınızda, bölüm:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="21f3d-3115">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3115">Property</span></span> | <span data-ttu-id="21f3d-3116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-3116">Description</span></span> | <span data-ttu-id="21f3d-3117">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="21f3d-3118">scriptPath</span></span> |<span data-ttu-id="21f3d-3119">U-SQL komut dosyasını içeren klasörün yolu.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="21f3d-3120">Dosyanın adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="21f3d-3121">Hayır (komut dosyası kullanırsanız)</span><span class="sxs-lookup"><span data-stu-id="21f3d-3121">No (if you use script)</span></span> |
| <span data-ttu-id="21f3d-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="21f3d-3122">scriptLinkedService</span></span> |<span data-ttu-id="21f3d-3123">Veri Fabrikası için komut dosyasını içeren depolamayı bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="21f3d-3124">Hayır (komut dosyası kullanırsanız)</span><span class="sxs-lookup"><span data-stu-id="21f3d-3124">No (if you use script)</span></span> |
| <span data-ttu-id="21f3d-3125">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="21f3d-3125">script</span></span> |<span data-ttu-id="21f3d-3126">ScriptPath ve scriptLinkedService belirtme yerine satır içi betiği belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="21f3d-3127">Örneğin: "komut dosyası": "Veritabanı oluştur test".</span><span class="sxs-lookup"><span data-stu-id="21f3d-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="21f3d-3128">Hayır (scriptPath ve scriptLinkedService kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="21f3d-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="21f3d-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="21f3d-3129">degreeOfParallelism</span></span> |<span data-ttu-id="21f3d-3130">Aynı anda işi çalıştırmak için kullanılan düğümlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="21f3d-3131">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3131">No</span></span> |
| <span data-ttu-id="21f3d-3132">Öncelik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3132">priority</span></span> |<span data-ttu-id="21f3d-3133">İlk çalıştırmak için sıraya alınan tüm işlerden seçili belirler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="21f3d-3134">Alt sayısı, öncelik o kadar yüksektir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="21f3d-3135">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3135">No</span></span> |
| <span data-ttu-id="21f3d-3136">Parametreleri</span><span class="sxs-lookup"><span data-stu-id="21f3d-3136">parameters</span></span> |<span data-ttu-id="21f3d-3137">U-SQL betiği için parametreler</span><span class="sxs-lookup"><span data-stu-id="21f3d-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="21f3d-3138">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="21f3d-3139">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="21f3d-3140">Daha fazla bilgi için bkz: [Data Lake Analytics U-SQL etkinliği](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="21f3d-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="21f3d-3141">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="21f3d-3142">Bir saklı yordam etkinliği JSON tanımında aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="21f3d-3143">Etkinlik türü özelliği olması gerekir: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="21f3d-3144">Aşağıdaki bağlı hizmetler, bir tane oluşturun ve değeri olarak bağlı hizmetin adı belirtmeniz gerekir **linkedServiceName** özelliği:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="21f3d-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="21f3d-3145">SQL Server</span></span> 
- <span data-ttu-id="21f3d-3146">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="21f3d-3146">Azure SQL Database</span></span>
- <span data-ttu-id="21f3d-3147">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="21f3d-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="21f3d-3148">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için SqlServerStoredProcedure ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="21f3d-3149">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3149">Property</span></span> | <span data-ttu-id="21f3d-3150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-3150">Description</span></span> | <span data-ttu-id="21f3d-3151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21f3d-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="21f3d-3152">storedProcedureName</span></span> |<span data-ttu-id="21f3d-3153">Azure SQL veritabanı ya da çıktı tablosu kullanır bağlantılı hizmet tarafından temsil edilen Azure SQL Data Warehouse saklı yordamın adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="21f3d-3154">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3154">Yes</span></span> |
| <span data-ttu-id="21f3d-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="21f3d-3155">storedProcedureParameters</span></span> |<span data-ttu-id="21f3d-3156">Saklı yordam parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="21f3d-3157">Bir parametre için null geçmesi gerekiyorsa, söz dizimini kullanın: "param1": null (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="21f3d-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="21f3d-3158">Bu özellik kullanma hakkında bilgi edinmek için aşağıdaki örnek bakın.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="21f3d-3159">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3159">No</span></span> |

<span data-ttu-id="21f3d-3160">Bir giriş veri kümesi belirtirseniz, ('Hazır' durumunda) kullanılabilir olmalıdır çalıştırmak saklı yordam etkinliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="21f3d-3161">Girdi veri kümesi saklı yordam, bir parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="21f3d-3162">Yalnızca saklı yordam etkinliği başlatmadan önce bağımlılık denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="21f3d-3163">Bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="21f3d-3164">Çıktı veri kümesi belirtir **zamanlama** saklı yordam etkinliği (saatlik, haftalık, aylık, vb.).</span><span class="sxs-lookup"><span data-stu-id="21f3d-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="21f3d-3165">Çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** bir Azure SQL Database veya bir Azure SQL Data Warehouse veya çalıştırmak için saklı yordam istediğiniz SQL Server veritabanı başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="21f3d-3166">Çıktı veri kümesi için saklı yordam sonucunu başka bir etkinlik tarafından işleme sonraki geçirmek için bir yol olarak hizmet verebilir ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="21f3d-3167">Ancak, veri fabrikası otomatik olarak bir saklı yordam çıktısını bu veri kümesine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="21f3d-3168">Çıktı veri kümesi işaret eden bir SQL tablosuna Yazar saklı yordam değil.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="21f3d-3169">Bazı durumlarda, çıktı veri kümesi olabilir bir **kukla dataset**, yalnızca saklı yordam etkinliği çalıştırmak için zamanlama belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="21f3d-3170">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="21f3d-3171">Daha fazla bilgi için bkz: [saklı yordam etkinliği](data-factory-stored-proc-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="21f3d-3172">.NET özel etkinliği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3172">.NET custom activity</span></span>
<span data-ttu-id="21f3d-3173">.NET özel etkinliğinde JSON tanımını aşağıdaki özellikleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="21f3d-3174">Etkinlik türü özelliği olması gerekir: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="21f3d-3175">Azure Hdınsight bağlı hizmeti oluşturmak veya bağlı bir Azure Batch hizmeti ve bağlı hizmetin adı için bir değer olarak belirtin **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="21f3d-3176">Aşağıdaki özellikler de desteklenen **typeProperties** bölümünde etkinlik türü için DotNetActivity ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="21f3d-3177">Özellik</span><span class="sxs-lookup"><span data-stu-id="21f3d-3177">Property</span></span> | <span data-ttu-id="21f3d-3178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21f3d-3178">Description</span></span> | <span data-ttu-id="21f3d-3179">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21f3d-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="21f3d-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="21f3d-3180">AssemblyName</span></span> | <span data-ttu-id="21f3d-3181">Derleme adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3181">Name of the assembly.</span></span> <span data-ttu-id="21f3d-3182">Örnek,: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="21f3d-3183">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3183">Yes</span></span> |
| <span data-ttu-id="21f3d-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="21f3d-3184">EntryPoint</span></span> |<span data-ttu-id="21f3d-3185">IDotNetActivity arabirimini uygulayan sınıfı adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="21f3d-3186">Örnek,: **MyDotNetActivityNS.MyDotNetActivity** burada MyDotNetActivityNS ad alanı ve MyDotNetActivity sınıfı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="21f3d-3187">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3187">Yes</span></span> | 
| <span data-ttu-id="21f3d-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="21f3d-3188">PackageLinkedService</span></span> | <span data-ttu-id="21f3d-3189">Özel Etkinlik zip dosyasını içeren blob depolama alanına işaret Azure Storage bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="21f3d-3190">Örnek,: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="21f3d-3191">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3191">Yes</span></span> |
| <span data-ttu-id="21f3d-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="21f3d-3192">PackageFile</span></span> | <span data-ttu-id="21f3d-3193">ZIP dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3193">Name of the zip file.</span></span> <span data-ttu-id="21f3d-3194">Örnek,: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="21f3d-3195">Evet</span><span class="sxs-lookup"><span data-stu-id="21f3d-3195">Yes</span></span> |
| <span data-ttu-id="21f3d-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="21f3d-3196">extendedProperties</span></span> | <span data-ttu-id="21f3d-3197">Tanımlayın ve .NET kodu için geçirin genişletilmiş özellikler.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="21f3d-3198">Bu örnekte, **SliceStart** değişkeni SliceStart sistem değişkeni göre bir değere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="21f3d-3199">Hayır</span><span class="sxs-lookup"><span data-stu-id="21f3d-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="21f3d-3200">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="21f3d-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="21f3d-3201">Ayrıntılı bilgi için bkz: [veri fabrikasında özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="21f3d-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="21f3d-3202">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="21f3d-3202">Next Steps</span></span>
<span data-ttu-id="21f3d-3203">Aşağıdaki öğreticiler bakın:</span><span class="sxs-lookup"><span data-stu-id="21f3d-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="21f3d-3204">Öğretici: kopyalama etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="21f3d-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="21f3d-3205">Öğretici: hive etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="21f3d-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)