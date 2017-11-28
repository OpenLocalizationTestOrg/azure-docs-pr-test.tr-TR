---
title: "aaaAzure Data Factory - JSON betik oluşturma başvurusu | Microsoft Docs"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="222f2-103">Azure Data Factory - JSON betik oluşturma başvurusu</span><span class="sxs-lookup"><span data-stu-id="222f2-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="222f2-104">Bu makalede, Azure Data Factory varlıkları (ardışık düzen, etkinlik, veri kümesi ve bağlantılı hizmet) tanımlamak için JSON şemaları ve örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="222f2-105">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="222f2-105">Pipeline</span></span> 
<span data-ttu-id="222f2-106">Ardışık düzen tanımı için üst düzey yapısı Hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="222f2-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="222f2-107">Aşağıdaki tabloda hello özellikleri hello ardışık düzen JSON tanımı içinde açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="222f2-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="222f2-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-108">Property</span></span> | <span data-ttu-id="222f2-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-109">Description</span></span> | <span data-ttu-id="222f2-110">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="222f2-111">ad</span><span class="sxs-lookup"><span data-stu-id="222f2-111">name</span></span> | <span data-ttu-id="222f2-112">Merhaba ardışık düzen adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-112">Name of hello pipeline.</span></span> <span data-ttu-id="222f2-113">Etkinlik hello hello eylemi temsil eden bir ad belirtin veya yapılandırılmış toodo ardışık düzen değil</span><span class="sxs-lookup"><span data-stu-id="222f2-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="222f2-114">En fazla karakter sayısı: 260</span><span class="sxs-lookup"><span data-stu-id="222f2-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="222f2-115">Bir harf, sayı veya alt çizgi (_) ile başlamalıdır</span><span class="sxs-lookup"><span data-stu-id="222f2-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="222f2-116">Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="222f2-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="222f2-117">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-117">Yes</span></span> |
| <span data-ttu-id="222f2-118">açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-118">description</span></span> |<span data-ttu-id="222f2-119">Hangi hello etkinlik veya ardışık düzen açıklayan metin için kullanılır</span><span class="sxs-lookup"><span data-stu-id="222f2-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="222f2-120">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-120">No</span></span> |
| <span data-ttu-id="222f2-121">etkinlikler</span><span class="sxs-lookup"><span data-stu-id="222f2-121">activities</span></span> | <span data-ttu-id="222f2-122">Etkinliklerin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="222f2-122">Contains a list of activities.</span></span> | <span data-ttu-id="222f2-123">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-123">Yes</span></span> |
| <span data-ttu-id="222f2-124">start</span><span class="sxs-lookup"><span data-stu-id="222f2-124">start</span></span> |<span data-ttu-id="222f2-125">Merhaba ardışık düzeni için başlangıç tarihi / saati.</span><span class="sxs-lookup"><span data-stu-id="222f2-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="222f2-126">Olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="222f2-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="222f2-127">Örneğin: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="222f2-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="222f2-128">Olası toospecify yerel saat örneğin bir EST zamanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="222f2-129">Örnek aşağıda verilmiştir: `2016-02-27T06:00:00**-05:00`, 6'da tahmini olduğu</span><span class="sxs-lookup"><span data-stu-id="222f2-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="222f2-130">Merhaba başlangıç ve bitiş özellikleri birlikte hello ardışık düzen etkin süresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="222f2-131">Çıktı dilimler yalnızca ile etkin bu dönemde üretilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="222f2-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-132">No</span></span><br/><br/><span data-ttu-id="222f2-133">Merhaba end özelliği için bir değer belirtirseniz, hello başlangıç özelliği için değer belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="222f2-134">Merhaba başlangıç ve bitiş zamanlarını hem de boş toocreate işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="222f2-135">Her iki değeri de belirtilmelisiniz tooset etkin dönem hello ardışık düzen toorun için bir.</span><span class="sxs-lookup"><span data-stu-id="222f2-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="222f2-136">Başlangıç ve bitiş zamanlarını belirtmezseniz, bir işlem hattı oluştururken, bunları ayarlayabilirsiniz daha sonra hello kümesi AzureRmDataFactoryPipelineActivePeriod cmdlet'ini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="222f2-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="222f2-137">Bitiş</span><span class="sxs-lookup"><span data-stu-id="222f2-137">end</span></span> |<span data-ttu-id="222f2-138">Merhaba ardışık düzeni için bitiş tarihi / saati.</span><span class="sxs-lookup"><span data-stu-id="222f2-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="222f2-139">Belirtilen ISO biçiminde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-139">If specified must be in ISO format.</span></span> <span data-ttu-id="222f2-140">Örneğin: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="222f2-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="222f2-141">Olası toospecify yerel saat örneğin bir EST zamanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="222f2-142">Örnek aşağıda verilmiştir: `2016-02-27T06:00:00**-05:00`, 6'da tahmini olduğu</span><span class="sxs-lookup"><span data-stu-id="222f2-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="222f2-143">toorun hello ardışık kalıcı olarak belirtin 9999-09-09 hello end özelliği hello değeri olarak.</span><span class="sxs-lookup"><span data-stu-id="222f2-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="222f2-144">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-144">No</span></span> <br/><br/><span data-ttu-id="222f2-145">Merhaba başlangıç özelliği için bir değer belirtirseniz, hello end özelliği için değer belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="222f2-146">Hello için notlarına bakın **Başlat** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="222f2-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="222f2-147">isPaused</span></span> |<span data-ttu-id="222f2-148">Set tootrue hello ardışık çalışmazsa.</span><span class="sxs-lookup"><span data-stu-id="222f2-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="222f2-149">Varsayılan değer = false.</span><span class="sxs-lookup"><span data-stu-id="222f2-149">Default value = false.</span></span> <span data-ttu-id="222f2-150">Bu özellik tooenable kullanın veya devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="222f2-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-151">No</span></span> |
| <span data-ttu-id="222f2-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="222f2-152">pipelineMode</span></span> |<span data-ttu-id="222f2-153">zamanlama için başlangıç yöntemi hello ardışık düzeni için çalışır.</span><span class="sxs-lookup"><span data-stu-id="222f2-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="222f2-154">İzin verilen değerler: (varsayılan), zamanlanmış kez.</span><span class="sxs-lookup"><span data-stu-id="222f2-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="222f2-155">'Zamanlanmış' Bu hello ardışık düzen tooits etkin dönemi (başlangıç ve bitiş saati) göre belirli bir zaman aralığında çalışır gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="222f2-156">'Kez' Bu hello ardışık düzen yalnızca bir kez çalışır gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="222f2-157">Oluşturulduktan sonra kez ardışık düzen şu anda değiştiren/güncelleştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="222f2-158">Bkz: [Onetime ardışık düzen](data-factory-create-pipelines.md#onetime-pipeline) kez ayar hakkındaki ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="222f2-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="222f2-159">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-159">No</span></span> |
| <span data-ttu-id="222f2-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="222f2-160">expirationTime</span></span> |<span data-ttu-id="222f2-161">Hangi hello ardışık düzeni geçerli değil ve sağlanan kalacağı oluşturulduktan sonra süre.</span><span class="sxs-lookup"><span data-stu-id="222f2-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="222f2-162">Tüm etkin başarısız oldu, yok veya hello süre Dolum zamanına ulaştığında çalıştırır hello ardışık düzen otomatik olarak silinmesi durumunda.</span><span class="sxs-lookup"><span data-stu-id="222f2-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="222f2-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="222f2-164">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="222f2-164">Activity</span></span> 
<span data-ttu-id="222f2-165">Ardışık düzen tanımı (etkinlikleri öğesi) içinde bir etkinlik için üst düzey yapısı Hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="222f2-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="222f2-166">Tablo hello etkinlik JSON tanımını hello özellikleri açıklar:</span><span class="sxs-lookup"><span data-stu-id="222f2-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="222f2-167">Etiket</span><span class="sxs-lookup"><span data-stu-id="222f2-167">Tag</span></span> | <span data-ttu-id="222f2-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-168">Description</span></span> | <span data-ttu-id="222f2-169">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-170">ad</span><span class="sxs-lookup"><span data-stu-id="222f2-170">name</span></span> |<span data-ttu-id="222f2-171">Merhaba etkinlik adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-171">Name of hello activity.</span></span> <span data-ttu-id="222f2-172">Merhaba etkinlik hello eylemi temsil eden adını toodo yapılandırılmış belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="222f2-173">En fazla karakter sayısı: 260</span><span class="sxs-lookup"><span data-stu-id="222f2-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="222f2-174">Bir harf, sayı veya alt çizgi (_) ile başlamalıdır</span><span class="sxs-lookup"><span data-stu-id="222f2-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="222f2-175">Şu karakterler kullanılamaz: ".", "+","?", "/", "<",">", "*", "%", "&", ":","\\"</span><span class="sxs-lookup"><span data-stu-id="222f2-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="222f2-176">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-176">Yes</span></span> |
| <span data-ttu-id="222f2-177">açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-177">description</span></span> |<span data-ttu-id="222f2-178">Hangi hello etkinliği açıklayan bir metin için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="222f2-179">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-179">Yes</span></span> |
| <span data-ttu-id="222f2-180">type</span><span class="sxs-lookup"><span data-stu-id="222f2-180">type</span></span> |<span data-ttu-id="222f2-181">Merhaba etkinlik Hello türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="222f2-182">Merhaba bkz [veri DEPOLARINA](#data-stores) ve [veri dönüştürme etkinlikleri](#data-transformation-activities) bölümleri etkinlikler farklı türde.</span><span class="sxs-lookup"><span data-stu-id="222f2-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="222f2-183">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-183">Yes</span></span> |
| <span data-ttu-id="222f2-184">Girişleri</span><span class="sxs-lookup"><span data-stu-id="222f2-184">inputs</span></span> |<span data-ttu-id="222f2-185">Merhaba etkinlik tarafından kullanılan giriş tabloları</span><span class="sxs-lookup"><span data-stu-id="222f2-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="222f2-186">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-186">Yes</span></span> |
| <span data-ttu-id="222f2-187">Çıkışları</span><span class="sxs-lookup"><span data-stu-id="222f2-187">outputs</span></span> |<span data-ttu-id="222f2-188">Merhaba etkinlik tarafından kullanılan çıkış tabloları.</span><span class="sxs-lookup"><span data-stu-id="222f2-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="222f2-189">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-189">Yes</span></span> |
| <span data-ttu-id="222f2-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="222f2-190">linkedServiceName</span></span> |<span data-ttu-id="222f2-191">Merhaba etkinlik tarafından kullanılan hello bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="222f2-192">Bir etkinlik toohello gerekli hesaplama ortamı bağlantılar hello bağlantılı hizmeti belirtin gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="222f2-193">Hdınsight etkinlikleri, Azure Machine Learning etkinlikleri ve saklı yordam etkinliği için Evet.</span><span class="sxs-lookup"><span data-stu-id="222f2-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="222f2-194">Diğer tümü için hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-194">No for all others</span></span> |
| <span data-ttu-id="222f2-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="222f2-195">typeProperties</span></span> |<span data-ttu-id="222f2-196">Merhaba typeProperties bölümündeki özellikler hello etkinlik türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="222f2-197">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-197">No</span></span> |
| <span data-ttu-id="222f2-198">ilke</span><span class="sxs-lookup"><span data-stu-id="222f2-198">policy</span></span> |<span data-ttu-id="222f2-199">Merhaba etkinlik hello çalışma zamanı davranışını etkileyen ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="222f2-200">Belirtilmezse, varsayılan ilkeler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="222f2-201">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-201">No</span></span> |
| <span data-ttu-id="222f2-202">Zamanlayıcı</span><span class="sxs-lookup"><span data-stu-id="222f2-202">scheduler</span></span> |<span data-ttu-id="222f2-203">"Zamanlayıcı" Merhaba etkinliği için zamanlama kullanılan toodefine istenen özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="222f2-204">Onun alt olanları hello içinde hello aynı hello olan [dataset kullanılabilirliği özelliğinde](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="222f2-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="222f2-205">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="222f2-206">İlkeler</span><span class="sxs-lookup"><span data-stu-id="222f2-206">Policies</span></span>
<span data-ttu-id="222f2-207">İlkeler, özellikle bir tablonun hello dilim işlendiğinde bir etkinlik hello çalışma zamanı davranışını etkiler.</span><span class="sxs-lookup"><span data-stu-id="222f2-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="222f2-208">Aşağıdaki tablonun hello hello ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="222f2-209">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-209">Property</span></span> | <span data-ttu-id="222f2-210">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-210">Permitted values</span></span> | <span data-ttu-id="222f2-211">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="222f2-211">Default Value</span></span> | <span data-ttu-id="222f2-212">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-213">Eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="222f2-213">concurrency</span></span> |<span data-ttu-id="222f2-214">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="222f2-214">Integer</span></span> <br/><br/><span data-ttu-id="222f2-215">En yüksek değeri: 10</span><span class="sxs-lookup"><span data-stu-id="222f2-215">Max value: 10</span></span> |<span data-ttu-id="222f2-216">1</span><span class="sxs-lookup"><span data-stu-id="222f2-216">1</span></span> |<span data-ttu-id="222f2-217">Eşzamanlı yürütmeleri hello etkinlik sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="222f2-218">Üzerinde farklı dilimler oluşabilir paralel etkinlik yürütmeleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="222f2-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="222f2-219">Örneğin, bir etkinlik toogo aracılığıyla gerekiyorsa kullanılabilir veri, daha büyük bir eşzamanlılık değer sahip büyük bir dizi hello veri işleme hızı artar.</span><span class="sxs-lookup"><span data-stu-id="222f2-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="222f2-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="222f2-220">executionPriorityOrder</span></span> |<span data-ttu-id="222f2-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="222f2-221">NewestFirst</span></span><br/><br/><span data-ttu-id="222f2-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="222f2-222">OldestFirst</span></span> |<span data-ttu-id="222f2-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="222f2-223">OldestFirst</span></span> |<span data-ttu-id="222f2-224">İşlenen veri dilimleri Hello sıralama belirler.</span><span class="sxs-lookup"><span data-stu-id="222f2-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="222f2-225">Örneğin, varsa (bir oluşmasını 4 pm adresindeki ve 17: 00 saatleri sırasında başka bir) 2 böler ve hem de yürütme olması.</span><span class="sxs-lookup"><span data-stu-id="222f2-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="222f2-226">Merhaba executionPriorityOrder toobe NewestFirst ayarlarsanız, 17: 00 saatleri sırasında hello dilim önce işlenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="222f2-227">Merhaba executionPriorityORder toobe OldestFIrst ayarlarsanız, benzer şekilde ardından 4 PM adresindeki hello dilim işlenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="222f2-228">retry</span><span class="sxs-lookup"><span data-stu-id="222f2-228">retry</span></span> |<span data-ttu-id="222f2-229">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="222f2-229">Integer</span></span><br/><br/><span data-ttu-id="222f2-230">En büyük değer 10 olabilir</span><span class="sxs-lookup"><span data-stu-id="222f2-230">Max value can be 10</span></span> |<span data-ttu-id="222f2-231">0</span><span class="sxs-lookup"><span data-stu-id="222f2-231">0</span></span> |<span data-ttu-id="222f2-232">Hata olarak işaretlenmiş hello veri işleme hello dilim için önce yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="222f2-233">Etkinlik yürütme veri dilimi için belirtilen toohello denenen yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="222f2-234">mümkün olan en kısa sürede hello hatasından sonra Hello yeniden deneme yapılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="222f2-235">timeout</span><span class="sxs-lookup"><span data-stu-id="222f2-235">timeout</span></span> |<span data-ttu-id="222f2-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-236">TimeSpan</span></span> |<span data-ttu-id="222f2-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="222f2-237">00:00:00</span></span> |<span data-ttu-id="222f2-238">Merhaba etkinlik için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="222f2-238">Timeout for hello activity.</span></span> <span data-ttu-id="222f2-239">Örnek: 00:10: (zaman aşımı 10 dakika anlamına gelir) 00</span><span class="sxs-lookup"><span data-stu-id="222f2-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="222f2-240">Bir değer belirtilmemiş ya da 0 hello zaman aşımı sonsuzdur.</span><span class="sxs-lookup"><span data-stu-id="222f2-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="222f2-241">Merhaba veri işleme saat dilimi hello zaman aşımı değerini aşarsa, iptal edilir ve tooretry hello işleme hello sistem dener.</span><span class="sxs-lookup"><span data-stu-id="222f2-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="222f2-242">yeniden deneme sayısı Hello hello yeniden deneme özelliğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="222f2-243">Zaman aşımı oluştuğunda hello durumu tooTimedOut ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="222f2-244">gecikme</span><span class="sxs-lookup"><span data-stu-id="222f2-244">delay</span></span> |<span data-ttu-id="222f2-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-245">TimeSpan</span></span> |<span data-ttu-id="222f2-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="222f2-246">00:00:00</span></span> |<span data-ttu-id="222f2-247">Veri işleme hello dilim başlatır önce Hello gecikme belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="222f2-248">Merhaba gecikme hello beklenen yürütme zamanı geçmişte sonra veri dilimi için etkinliğin hello yürütme başlatılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="222f2-249">Örnek: 00:10: (10 dakika gecikme anlamına gelir) 00</span><span class="sxs-lookup"><span data-stu-id="222f2-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="222f2-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="222f2-250">longRetry</span></span> |<span data-ttu-id="222f2-251">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="222f2-251">Integer</span></span><br/><br/><span data-ttu-id="222f2-252">En yüksek değeri: 10</span><span class="sxs-lookup"><span data-stu-id="222f2-252">Max value: 10</span></span> |<span data-ttu-id="222f2-253">1</span><span class="sxs-lookup"><span data-stu-id="222f2-253">1</span></span> |<span data-ttu-id="222f2-254">Dilim yürütülemedi Hello hello uzun yeniden deneme girişimi sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="222f2-255">longRetry girişimleri tarafından longRetryInterval aralarına aralık eklenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="222f2-256">Yeniden deneme girişimleri arasındaki süre toospecify gerekiyorsa, bu nedenle longRetry kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="222f2-257">Yeniden deneme ve longRetry belirtilirse, her bir longRetry denemesi denemeleri içerir ve hello en fazla deneme sayısı yeniden deneme * longRetry.</span><span class="sxs-lookup"><span data-stu-id="222f2-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="222f2-258">Örneğin, biz hello etkinlik İlkesi ayarlarında aşağıdaki hello varsa:</span><span class="sxs-lookup"><span data-stu-id="222f2-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="222f2-259">Yeniden deneme: 3</span><span class="sxs-lookup"><span data-stu-id="222f2-259">Retry: 3</span></span><br/><span data-ttu-id="222f2-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="222f2-260">longRetry: 2</span></span><br/><span data-ttu-id="222f2-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="222f2-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="222f2-262">Yalnızca bir dilim tooexecute olduğu varsayılır (Durum Bekliyor) ve hello Etkinlik yürütme her zaman başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="222f2-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="222f2-263">Başlangıçta 3 ardışık yürütme deneme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="222f2-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="222f2-264">Her girişiminden sonra Yeniden Dene'yi hello dilim durum olacaktır.</span><span class="sxs-lookup"><span data-stu-id="222f2-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="222f2-265">İlk 3 deneme üzerinden sonra hello dilim durumunu LongRetry olacaktır.</span><span class="sxs-lookup"><span data-stu-id="222f2-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="222f2-266">Bir saat sonra (diğer bir deyişle, longRetryInteval'ın değeri), 3 ardışık yürütme deneme başka bir dizi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="222f2-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="222f2-267">Bundan sonra hello dilim durumu başarısız ve daha fazla yeniden deneme yok denenmesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="222f2-268">Bu nedenle genel 6 deneme yapıldı.</span><span class="sxs-lookup"><span data-stu-id="222f2-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="222f2-269">Hiçbir yürütme başarılı olursa, hello dilim durum hazır olur ve daha fazla yeniden deneme yok çalıştı.</span><span class="sxs-lookup"><span data-stu-id="222f2-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="222f2-270">longRetry, belirleyici olmayan zamanlarda bağımlı veri ulaştığında veya hello genel ortamında hangi veri işleme gerçekleşir altında anormal olduğu durumlarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="222f2-271">Böyle durumlarda, yeniden deneme birbiri ardından yapılması yardımcı ve bunun hello sonuçlarında zaman aralığını sonra yapılması istenen çıkış.</span><span class="sxs-lookup"><span data-stu-id="222f2-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="222f2-272">Uyarı: longRetry veya longRetryInterval yüksek değerleri ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="222f2-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="222f2-273">Genellikle, daha yüksek değerleri sistemle ilgili diğer sorunlar kapsıyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="222f2-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="222f2-274">longRetryInterval</span></span> |<span data-ttu-id="222f2-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-275">TimeSpan</span></span> |<span data-ttu-id="222f2-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="222f2-276">00:00:00</span></span> |<span data-ttu-id="222f2-277">uzun yeniden deneme girişimleri arasında gecikme Hello</span><span class="sxs-lookup"><span data-stu-id="222f2-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="222f2-278">typeProperties bölümü</span><span class="sxs-lookup"><span data-stu-id="222f2-278">typeProperties section</span></span>
<span data-ttu-id="222f2-279">Merhaba typeProperties bölümü, her etkinlik için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="222f2-280">Dönüştürme etkinlikleri yalnızca hello türü özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="222f2-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="222f2-281">Bkz: [veri dönüştürme etkinlikleri](#data-transformation-activities) ardışık düzeninde dönüştürme etkinlikleri tanımlayan JSON örnekleri için bu makalenin bölümünde.</span><span class="sxs-lookup"><span data-stu-id="222f2-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="222f2-282">**Kopya etkinliği** hello typeProperties bölümünde iki alt bölümleri vardır: **kaynak** ve **havuz**.</span><span class="sxs-lookup"><span data-stu-id="222f2-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="222f2-283">Bkz: [veri DEPOLARINA](#data-stores) nasıl toouse veri depolayan bir kaynak ve/veya havuz gösteren JSON örnekleri için bu makaledeki bölüm.</span><span class="sxs-lookup"><span data-stu-id="222f2-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="222f2-284">Örnek kopyalama işlem hattı</span><span class="sxs-lookup"><span data-stu-id="222f2-284">Sample copy pipeline</span></span>
<span data-ttu-id="222f2-285">Aşağıdaki örnek ardışık düzen hello türünde bir etkinlik yok **kopyalama** hello içinde **etkinlikleri** bölüm.</span><span class="sxs-lookup"><span data-stu-id="222f2-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="222f2-286">Bu örnekte, hello [kopyalama etkinliğini](data-factory-data-movement-activities.md) Azure Blob Depolama tooan Azure SQL veritabanından veri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="222f2-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
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

<span data-ttu-id="222f2-287">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="222f2-287">Note hello following points:</span></span>

* <span data-ttu-id="222f2-288">Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="222f2-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="222f2-289">Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="222f2-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="222f2-290">Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="222f2-291">Bkz: [veri DEPOLARINA](#data-stores) nasıl toouse veri depolayan bir kaynak ve/veya havuz gösteren JSON örnekleri için bu makaledeki bölüm.</span><span class="sxs-lookup"><span data-stu-id="222f2-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="222f2-292">Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="222f2-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="222f2-293">Örnek dönüştürme işlem hattı</span><span class="sxs-lookup"><span data-stu-id="222f2-293">Sample transformation pipeline</span></span>
<span data-ttu-id="222f2-294">Aşağıdaki örnek ardışık düzen hello türünde bir etkinlik yok **Hdınsighthive** hello içinde **etkinlikleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="222f2-295">Bu örnekte, hello [Hdınsight Hive etkinliği](data-factory-hive-activity.md) Azure Hdınsight Hadoop kümesindeki Hive betiği çalıştırılarak verileri Azure Blob depolama biriminden dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="222f2-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="222f2-296">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="222f2-296">Note hello following points:</span></span> 

* <span data-ttu-id="222f2-297">Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**Hdınsighthive**.</span><span class="sxs-lookup"><span data-stu-id="222f2-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="222f2-298">Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **AzureStorageLinkedService**) ve  **komut dosyası** hello kapsayıcı klasöründe **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="222f2-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="222f2-299">Merhaba **tanımlar** bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örneğin `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="222f2-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="222f2-300">Bkz: [veri dönüştürme etkinlikleri](#data-transformation-activities) ardışık düzeninde dönüştürme etkinlikleri tanımlayan JSON örnekleri için bu makalenin bölümünde.</span><span class="sxs-lookup"><span data-stu-id="222f2-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="222f2-301">Bu ardışık düzen oluşturma izlenecek tam yol için bkz: [Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tooprocess verilerinizi yapı](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="222f2-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="222f2-302">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-302">Linked service</span></span>
<span data-ttu-id="222f2-303">bağlantılı hizmet tanımı için üst düzey yapısı Hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="222f2-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="222f2-304">Tablo hello etkinlik JSON tanımını hello özellikleri açıklar:</span><span class="sxs-lookup"><span data-stu-id="222f2-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="222f2-305">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-305">Property</span></span> | <span data-ttu-id="222f2-306">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-306">Description</span></span> | <span data-ttu-id="222f2-307">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="222f2-308">ad</span><span class="sxs-lookup"><span data-stu-id="222f2-308">name</span></span> | <span data-ttu-id="222f2-309">Merhaba bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-309">Name of hello linked service.</span></span> | <span data-ttu-id="222f2-310">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-310">Yes</span></span> | 
| <span data-ttu-id="222f2-311">özellikleri - türü</span><span class="sxs-lookup"><span data-stu-id="222f2-311">properties - type</span></span> | <span data-ttu-id="222f2-312">Merhaba bağlantılı hizmet türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-312">Type of hello linked service.</span></span> <span data-ttu-id="222f2-313">Örneğin: Azure Storage, Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="222f2-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="222f2-314">typeProperties</span></span> | <span data-ttu-id="222f2-315">Merhaba typeProperties bölüm için her bir veri deposu farklı veya ortam işlem öğesine sahip.</span><span class="sxs-lookup"><span data-stu-id="222f2-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="222f2-316">Bkz: [veri depolarına](#datastores) bağlı hizmetler tüm hello verilerini depolamak için bölüm ve [ortamları işlem](#compute-environments) tüm Merhaba işlem bağlı Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="222f2-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="222f2-317">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-317">Dataset</span></span> 
<span data-ttu-id="222f2-318">Azure Data Factory kümesinde aşağıdaki gibi tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="222f2-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="222f2-319">Aşağıdaki tablonun hello JSON yukarıda hello özelliklerinde açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="222f2-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="222f2-320">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-320">Property</span></span> | <span data-ttu-id="222f2-321">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-321">Description</span></span> | <span data-ttu-id="222f2-322">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-322">Required</span></span> | <span data-ttu-id="222f2-323">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="222f2-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-324">ad</span><span class="sxs-lookup"><span data-stu-id="222f2-324">name</span></span> | <span data-ttu-id="222f2-325">Merhaba DataSet'in adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-325">Name of hello dataset.</span></span> <span data-ttu-id="222f2-326">Bkz: [Azure Data Factory - adlandırma kuralları](data-factory-naming-rules.md) adlandırma kuralları.</span><span class="sxs-lookup"><span data-stu-id="222f2-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="222f2-327">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-327">Yes</span></span> |<span data-ttu-id="222f2-328">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-328">NA</span></span> |
| <span data-ttu-id="222f2-329">type</span><span class="sxs-lookup"><span data-stu-id="222f2-329">type</span></span> | <span data-ttu-id="222f2-330">Merhaba veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-330">Type of hello dataset.</span></span> <span data-ttu-id="222f2-331">Azure Data Factory ile desteklenen hello türlerinden birini belirtin (örneğin: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="222f2-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="222f2-332">Bkz: [veri DEPOLARINA](#data-stores) tüm veri depoları ve veri fabrikası tarafından desteklenen veri türleri hello için bölüm.</span><span class="sxs-lookup"><span data-stu-id="222f2-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="222f2-333">yapısı</span><span class="sxs-lookup"><span data-stu-id="222f2-333">structure</span></span> | <span data-ttu-id="222f2-334">Merhaba dataset şema.</span><span class="sxs-lookup"><span data-stu-id="222f2-334">Schema of hello dataset.</span></span> <span data-ttu-id="222f2-335">Bu sütun, türleri, vb. içerir.</span><span class="sxs-lookup"><span data-stu-id="222f2-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="222f2-336">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-336">No</span></span> |<span data-ttu-id="222f2-337">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-337">NA</span></span> |
| <span data-ttu-id="222f2-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="222f2-338">typeProperties</span></span> | <span data-ttu-id="222f2-339">Özellikler toohello karşılık gelen seçili türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="222f2-340">Bkz: [veri DEPOLARINA](#data-stores) desteklenen türlerini ve bunların özelliklerini bölümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="222f2-341">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-341">Yes</span></span> |<span data-ttu-id="222f2-342">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-342">NA</span></span> |
| <span data-ttu-id="222f2-343">external</span><span class="sxs-lookup"><span data-stu-id="222f2-343">external</span></span> | <span data-ttu-id="222f2-344">Boole veya bir veri kümesi açıkça data factory işlem hattı tarafından üretilir olup olmadığını toospecify bayrağı.</span><span class="sxs-lookup"><span data-stu-id="222f2-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="222f2-345">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-345">No</span></span> |<span data-ttu-id="222f2-346">False</span><span class="sxs-lookup"><span data-stu-id="222f2-346">false</span></span> |
| <span data-ttu-id="222f2-347">availability</span><span class="sxs-lookup"><span data-stu-id="222f2-347">availability</span></span> | <span data-ttu-id="222f2-348">Pencere veya model hello dataset üretim için dilimleme hello işleme hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="222f2-349">Model dilimleme hello veri kümesi hakkında daha fazla bilgi için bkz: [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="222f2-350">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-350">Yes</span></span> |<span data-ttu-id="222f2-351">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-351">NA</span></span> |
| <span data-ttu-id="222f2-352">ilke</span><span class="sxs-lookup"><span data-stu-id="222f2-352">policy</span></span> |<span data-ttu-id="222f2-353">Merhaba ölçütleri veya hello dataset dilimler karşılamanız gerekmektedir hello koşulu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="222f2-354">Ayrıntılar için bkz [Dataset İlkesi](#Policy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="222f2-355">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-355">No</span></span> |<span data-ttu-id="222f2-356">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-356">NA</span></span> |

<span data-ttu-id="222f2-357">Her sütunda hello **yapısı** bölüm, aşağıdaki özelliklere hello içerir:</span><span class="sxs-lookup"><span data-stu-id="222f2-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="222f2-358">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-358">Property</span></span> | <span data-ttu-id="222f2-359">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-359">Description</span></span> | <span data-ttu-id="222f2-360">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-361">ad</span><span class="sxs-lookup"><span data-stu-id="222f2-361">name</span></span> |<span data-ttu-id="222f2-362">Merhaba sütunun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-362">Name of hello column.</span></span> |<span data-ttu-id="222f2-363">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-363">Yes</span></span> |
| <span data-ttu-id="222f2-364">type</span><span class="sxs-lookup"><span data-stu-id="222f2-364">type</span></span> |<span data-ttu-id="222f2-365">Merhaba sütununun veri türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-365">Data type of hello column.</span></span>  |<span data-ttu-id="222f2-366">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-366">No</span></span> |
| <span data-ttu-id="222f2-367">Kültür</span><span class="sxs-lookup"><span data-stu-id="222f2-367">culture</span></span> |<span data-ttu-id="222f2-368">.NET tabanlı türü belirtilir ve .NET türü olduğunda kullanılan kültür toobe `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="222f2-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="222f2-369">Varsayılan değer `en-us`.</span><span class="sxs-lookup"><span data-stu-id="222f2-369">Default is `en-us`.</span></span> |<span data-ttu-id="222f2-370">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-370">No</span></span> |
| <span data-ttu-id="222f2-371">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-371">format</span></span> |<span data-ttu-id="222f2-372">Biçim türü belirtilir ve .NET türü olduğunda kullanılan dize toobe `Datetime` veya `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="222f2-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="222f2-373">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-373">No</span></span> |

<span data-ttu-id="222f2-374">Aşağıdaki örneğine hello hello dataset üç sütun sahip `slicetimestamp`, `projectname`, ve `pageviews` ve bunlar türü: dize, dize ve ondalık sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="222f2-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="222f2-375">Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanabileceğiniz özellikleri **kullanılabilirlik** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="222f2-376">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-376">Property</span></span> | <span data-ttu-id="222f2-377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-377">Description</span></span> | <span data-ttu-id="222f2-378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-378">Required</span></span> | <span data-ttu-id="222f2-379">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="222f2-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-380">frequency</span><span class="sxs-lookup"><span data-stu-id="222f2-380">frequency</span></span> |<span data-ttu-id="222f2-381">Veri kümesi dilim üretim Hello zaman birimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="222f2-382"><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay</span><span class="sxs-lookup"><span data-stu-id="222f2-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="222f2-383">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-383">Yes</span></span> |<span data-ttu-id="222f2-384">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-384">NA</span></span> |
| <span data-ttu-id="222f2-385">interval</span><span class="sxs-lookup"><span data-stu-id="222f2-385">interval</span></span> |<span data-ttu-id="222f2-386">Sıklığı çarpanı belirtir</span><span class="sxs-lookup"><span data-stu-id="222f2-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="222f2-387">"X sıklığı aralığını" ne sıklıkta hello dilim üretilen belirler.</span><span class="sxs-lookup"><span data-stu-id="222f2-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="222f2-388">Saatlik olarak başka bir dilimlenebilir dataset toobe hello varsa, ayarladığınız <b>sıklığı</b> çok<b>saat</b>, ve <b>aralığı</b> çok<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="222f2-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="222f2-389"><b>Not</b>: sıklığını dakika belirtirseniz, 15'den küçük hello aralığı toono ayarlamanızı öneririz</span><span class="sxs-lookup"><span data-stu-id="222f2-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="222f2-390">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-390">Yes</span></span> |<span data-ttu-id="222f2-391">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-391">NA</span></span> |
| <span data-ttu-id="222f2-392">stili</span><span class="sxs-lookup"><span data-stu-id="222f2-392">style</span></span> |<span data-ttu-id="222f2-393">Merhaba dilim hello başlangıç/bitiş hello aralığının üretilen olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="222f2-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="222f2-394">StartOfInterval</span></span></li><li><span data-ttu-id="222f2-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="222f2-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="222f2-396">Sıklık tooMonth ayarlanır ve stil tooEndOfInterval hello dilim ayın son günü hello üzerinde üretilmez.</span><span class="sxs-lookup"><span data-stu-id="222f2-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="222f2-397">Merhaba stili tooStartOfInterval ayarlarsanız hello dilim ayın ilk günü hello üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="222f2-398">Sıklık tooDay ayarlanır ve stil tooEndOfInterval hello dilim hello hello günün son bir saat üretilmez.</span><span class="sxs-lookup"><span data-stu-id="222f2-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="222f2-399">Sıklık tooHour ayarlanır ve stil tooEndOfInterval hello dilim hello hello saat sonunda üretilmez.</span><span class="sxs-lookup"><span data-stu-id="222f2-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="222f2-400">Örneğin, 13'te – 2 PM dönem için bir dilim için 2 saat hello dilim oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="222f2-401">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-401">No</span></span> |<span data-ttu-id="222f2-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="222f2-402">EndOfInterval</span></span> |
| <span data-ttu-id="222f2-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="222f2-403">anchorDateTime</span></span> |<span data-ttu-id="222f2-404">Zamanlayıcı toocompute dataset dilim sınırları tarafından kullanılan süre içinde mutlak konum Hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="222f2-405"><b>Not</b>: Merhaba AnchorDateTime sahip hello sıklığından daha ayrıntılı tarih kısımlarını sonra hello daha ayrıntılı bölümleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="222f2-406">Örneğin, hello <b>aralığı</b> olan <b>saatlik</b> (sıklığı: saat ve aralığı: 1) ve hello <b>AnchorDateTime</b> içeren <b>dakika ve saniyeleri</b>sonra hello <b>dakika ve saniyeleri</b> hello AnchorDateTime bölümlerini yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="222f2-407">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-407">No</span></span> |<span data-ttu-id="222f2-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="222f2-408">01/01/0001</span></span> |
| <span data-ttu-id="222f2-409">uzaklık</span><span class="sxs-lookup"><span data-stu-id="222f2-409">offset</span></span> |<span data-ttu-id="222f2-410">Tarafından hangi hello başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan.</span><span class="sxs-lookup"><span data-stu-id="222f2-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="222f2-411"><b>Not</b>: anchorDateTime ve uzaklık belirtilirse, hello birleştirilmiş hello shift sonucudur.</span><span class="sxs-lookup"><span data-stu-id="222f2-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="222f2-412">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-412">No</span></span> |<span data-ttu-id="222f2-413">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-413">NA</span></span> |

<span data-ttu-id="222f2-414">Kullanılabilirlik bölümden hello belirtir, hello çıktı veri kümesi olan üretilen saatlik (veya) giriş veri kümesi kullanılabilir saatlik:</span><span class="sxs-lookup"><span data-stu-id="222f2-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="222f2-415">Merhaba **İlkesi** gerekir dataset dilimler hello hello koşulu karşılayan veya veri kümesi tanımı bölümünde hello ölçütleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="222f2-416">İlke adı</span><span class="sxs-lookup"><span data-stu-id="222f2-416">Policy Name</span></span> | <span data-ttu-id="222f2-417">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-417">Description</span></span> | <span data-ttu-id="222f2-418">Çok uygulanan</span><span class="sxs-lookup"><span data-stu-id="222f2-418">Applied too</span></span>| <span data-ttu-id="222f2-419">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-419">Required</span></span> | <span data-ttu-id="222f2-420">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="222f2-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="222f2-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="222f2-421">minimumSizeMB</span></span> |<span data-ttu-id="222f2-422">Merhaba verilerin doğrulayan bir **Azure blob** karşılıyor hello minimum boyut gereksinimlerini (megabayt cinsinden).</span><span class="sxs-lookup"><span data-stu-id="222f2-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="222f2-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="222f2-423">Azure Blob</span></span> |<span data-ttu-id="222f2-424">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-424">No</span></span> |<span data-ttu-id="222f2-425">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-425">NA</span></span> |
| <span data-ttu-id="222f2-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="222f2-426">minimumRows</span></span> |<span data-ttu-id="222f2-427">Merhaba verilerin doğrulayan bir **Azure SQL veritabanı** veya bir **Azure tablo** hello en az satır sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="222f2-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="222f2-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="222f2-428">Azure SQL Database</span></span></li><li><span data-ttu-id="222f2-429">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="222f2-429">Azure Table</span></span></li></ul> |<span data-ttu-id="222f2-430">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-430">No</span></span> |<span data-ttu-id="222f2-431">NA</span><span class="sxs-lookup"><span data-stu-id="222f2-431">NA</span></span> |

<span data-ttu-id="222f2-432">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="222f2-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="222f2-433">Azure Data Factory tarafından üretilen bir veri kümesi sürece bunu olarak işaretlenmelidir **dış**.</span><span class="sxs-lookup"><span data-stu-id="222f2-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="222f2-434">Etkinlik veya ardışık düzen zincirleme kullanılmadığı sürece bu ayar genellikle bir ardışık düzendeki ilk etkinliğin toohello girişleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="222f2-435">Ad</span><span class="sxs-lookup"><span data-stu-id="222f2-435">Name</span></span> | <span data-ttu-id="222f2-436">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-436">Description</span></span> | <span data-ttu-id="222f2-437">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-437">Required</span></span> | <span data-ttu-id="222f2-438">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="222f2-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="222f2-439">dataDelay</span></span> |<span data-ttu-id="222f2-440">Dilim verilen hello için dış veri hello hello kullanılabilirliğine zaman toodelay hello denetleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="222f2-441">Örneğin, hello veri saatlik varsa, hello onay toosee hello dış veriler kullanılabilir ve hello karşılık gelen dilim hazır dataDelay kullanılarak ertelenebilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="222f2-442">Yalnızca toohello şimdiki zaman geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-442">Only applies toohello present time.</span></span>  <span data-ttu-id="222f2-443">Örneğin, 1:00 PM şimdi ise ve bu değer 10 dakikadır hello doğrulama 13: 10'te başlatır.</span><span class="sxs-lookup"><span data-stu-id="222f2-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="222f2-444">Bu ayar hello geçmiş dilimleri etkilemez (dilimler dilim bitiş saati + dataDelay < şimdi) herhangi bir gecikme işlenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="222f2-445">Saat 23: saat gereksinim hello kullanarak toospecified 59'dan büyük `day.hours:minutes:seconds` biçimi.</span><span class="sxs-lookup"><span data-stu-id="222f2-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="222f2-446">Örneğin, toospecify 24 saat 24:00:00 kullanmayın; Bunun yerine, 1.00:00:00 kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="222f2-447">24:00:00 kullanırsanız, 24 gün (24.00:00:00) kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="222f2-448">1 gün ve 4 saat için 1:04:00:00 belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="222f2-449">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-449">No</span></span> |<span data-ttu-id="222f2-450">0</span><span class="sxs-lookup"><span data-stu-id="222f2-450">0</span></span> |
| <span data-ttu-id="222f2-451">Retryınterval</span><span class="sxs-lookup"><span data-stu-id="222f2-451">retryInterval</span></span> |<span data-ttu-id="222f2-452">Merhaba hatası ve hello sonraki yeniden deneme girişimi arasındaki süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="222f2-453">Bir deneme başarısız olursa hello sonraki deneyin sonra Retryınterval olur.</span><span class="sxs-lookup"><span data-stu-id="222f2-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="222f2-454">1:00 PM şimdi ise, biz hello ilk denemede başlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="222f2-455">Merhaba süresi toocomplete hello ilk doğrulama denetimi hello işlemi başarısız oldu ve 1 dakikalık hello sonraki yeniden deneme ise, 1:00 1 dak (süresi) + 1 dak (yeniden deneme aralığı) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="222f2-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="222f2-456">Merhaba son dilim için gecikme yoktur.</span><span class="sxs-lookup"><span data-stu-id="222f2-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="222f2-457">Merhaba yeniden deneme hemen gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="222f2-457">hello retry happens immediately.</span></span> |<span data-ttu-id="222f2-458">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-458">No</span></span> |<span data-ttu-id="222f2-459">00:01:00 (1 dakika)</span><span class="sxs-lookup"><span data-stu-id="222f2-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="222f2-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-460">retryTimeout</span></span> |<span data-ttu-id="222f2-461">yeniden deneme girişimleri için Hello zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="222f2-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="222f2-462">Bu özellik ayarlanırsa too10 dakika hello doğrulama gereksinimlerini toobe 10 dakika içinde tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="222f2-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="222f2-463">10 dakika tooperform hello doğrulama uzun sürerse hello zaman aşımına yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="222f2-464">Tüm denemeleri hello doğrulama için zaman aşımına uğrarsa, hello dilim süresi sona erdi işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="222f2-465">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-465">No</span></span> |<span data-ttu-id="222f2-466">00:10:00 (10 dakika)</span><span class="sxs-lookup"><span data-stu-id="222f2-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="222f2-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="222f2-467">maximumRetry</span></span> |<span data-ttu-id="222f2-468">Sayısı toocheck hello dış veri hello kullanılabilirlik için zaman.</span><span class="sxs-lookup"><span data-stu-id="222f2-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="222f2-469">Merhaba izin verilen en büyük değer 10'dur.</span><span class="sxs-lookup"><span data-stu-id="222f2-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="222f2-470">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-470">No</span></span> |<span data-ttu-id="222f2-471">3</span><span class="sxs-lookup"><span data-stu-id="222f2-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="222f2-472">VERİ DEPOLARI</span><span class="sxs-lookup"><span data-stu-id="222f2-472">DATA STORES</span></span>
<span data-ttu-id="222f2-473">Merhaba [bağlantılı hizmeti](#linked-service) bağlı hizmetler ortak tooall türleri JSON öğeleri için sağlanan bölüm açıklamalar.</span><span class="sxs-lookup"><span data-stu-id="222f2-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="222f2-474">Bu bölümde, belirli tooeach veri deposu JSON öğelerini hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="222f2-475">Merhaba [Dataset](#dataset) veri kümeleri ortak tooall türleri JSON öğeleri için sağlanan bölüm açıklamalar.</span><span class="sxs-lookup"><span data-stu-id="222f2-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="222f2-476">Bu bölümde, belirli tooeach veri deposu JSON öğelerini hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="222f2-477">Merhaba [etkinlik](#activity) etkinlik ortak tooall türlerini JSON öğeleri için sağlanan bölüm açıklamalar.</span><span class="sxs-lookup"><span data-stu-id="222f2-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="222f2-478">Bu bölümde bir kopyalama etkinliği kaynak/havuz olarak kullanıldığında, belirli tooeach veri deposu JSON öğelerini hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="222f2-479">Şemalardaki toosee hello JSON bağlantılı hizmeti, veri kümesi, ilgilendiğiniz ve kaynak/havuz hello kopyalama etkinliği için hello hello deposu Hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="222f2-480">Kategori</span><span class="sxs-lookup"><span data-stu-id="222f2-480">Category</span></span> | <span data-ttu-id="222f2-481">Veri deposu</span><span class="sxs-lookup"><span data-stu-id="222f2-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="222f2-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="222f2-482">**Azure**</span></span> |[<span data-ttu-id="222f2-483">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="222f2-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="222f2-484">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="222f2-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="222f2-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="222f2-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="222f2-486">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="222f2-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="222f2-487">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="222f2-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="222f2-488">Azure Search</span><span class="sxs-lookup"><span data-stu-id="222f2-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="222f2-489">Azure Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="222f2-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="222f2-490">**Veritabanları**</span><span class="sxs-lookup"><span data-stu-id="222f2-490">**Databases**</span></span> |[<span data-ttu-id="222f2-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="222f2-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="222f2-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="222f2-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="222f2-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="222f2-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="222f2-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="222f2-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="222f2-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="222f2-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="222f2-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="222f2-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="222f2-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="222f2-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="222f2-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="222f2-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="222f2-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="222f2-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="222f2-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="222f2-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="222f2-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="222f2-501">**NoSQL**</span></span> |[<span data-ttu-id="222f2-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="222f2-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="222f2-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="222f2-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="222f2-504">**Dosya**</span><span class="sxs-lookup"><span data-stu-id="222f2-504">**File**</span></span> |[<span data-ttu-id="222f2-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="222f2-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="222f2-506">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="222f2-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="222f2-507">FTP</span><span class="sxs-lookup"><span data-stu-id="222f2-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="222f2-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="222f2-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="222f2-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="222f2-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="222f2-510">**Diğer**</span><span class="sxs-lookup"><span data-stu-id="222f2-510">**Others**</span></span> |[<span data-ttu-id="222f2-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="222f2-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="222f2-512">OData</span><span class="sxs-lookup"><span data-stu-id="222f2-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="222f2-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="222f2-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="222f2-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="222f2-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="222f2-515">Web tablo</span><span class="sxs-lookup"><span data-stu-id="222f2-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="222f2-516">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="222f2-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-517">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-517">Linked service</span></span>
<span data-ttu-id="222f2-518">Bağlı hizmetler iki tür vardır: Azure depolama bağlantılı hizmeti ve Azure depolama SAS bağlantılı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="222f2-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="222f2-519">Azure Storage Bağlı Hizmeti</span><span class="sxs-lookup"><span data-stu-id="222f2-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="222f2-520">toolink hello kullanarak Azure depolama hesabı tooa veri fabrikası **hesap anahtarı**, bir Azure Storage bağlı hizmeti oluşturma.</span><span class="sxs-lookup"><span data-stu-id="222f2-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="222f2-521">toodefine bir Azure depolama bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="222f2-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="222f2-522">Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-523">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-523">Property</span></span> | <span data-ttu-id="222f2-524">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-524">Description</span></span> | <span data-ttu-id="222f2-525">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-526">connectionString</span></span> |<span data-ttu-id="222f2-527">Tooconnect tooAzure depolama hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="222f2-528">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="222f2-529">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="222f2-530">Azure Storage SAS bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="222f2-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="222f2-531">Hello Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak toolink bir Azure depolama hesabı tooan Azure data factory sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="222f2-532">Kısıtlanmış/zaman sınırlı erişimi hello veri fabrikası hello depolama tooall/özel kaynakları (blob/kapsayıcısı) sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="222f2-533">bir Azure depolama bağlı SAS hizmeti toolink paylaşılan erişim imzası kullanarak Azure depolama hesabı tooa veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="222f2-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="222f2-534">toodefine bir Azure depolama SAS bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="222f2-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="222f2-535">Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="222f2-536">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-536">Property</span></span> | <span data-ttu-id="222f2-537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-537">Description</span></span> | <span data-ttu-id="222f2-538">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="222f2-539">sasUri</span></span> |<span data-ttu-id="222f2-540">Blob, kapsayıcı ya da tablo gibi paylaşılan erişim imzası URI toohello Azure Storage kaynakları belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="222f2-541">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="222f2-542">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-542">Example</span></span>

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

<span data-ttu-id="222f2-543">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Blob Storage bağlayıcı](data-factory-azure-blob-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-544">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-544">Dataset</span></span>
<span data-ttu-id="222f2-545">toodefine bir Azure Blob dataset kümesi hello **türü** hello kümesinin çok**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="222f2-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="222f2-546">Ardından, Azure Blob belirli hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-547">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-547">Property</span></span> | <span data-ttu-id="222f2-548">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-548">Description</span></span> | <span data-ttu-id="222f2-549">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-550">folderPath</span></span> |<span data-ttu-id="222f2-551">Yol toohello kapsayıcı ve klasöre hello blob depolama.</span><span class="sxs-lookup"><span data-stu-id="222f2-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="222f2-552">Örnek: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="222f2-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="222f2-553">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-553">Yes</span></span> |
| <span data-ttu-id="222f2-554">fileName</span><span class="sxs-lookup"><span data-stu-id="222f2-554">fileName</span></span> |<span data-ttu-id="222f2-555">Merhaba blob adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-555">Name of hello blob.</span></span> <span data-ttu-id="222f2-556">isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="222f2-557">Üzerinde bir dosya adı, hello (kopyalama dahil) etkinlik works belirtirseniz, belirli Blob hello.</span><span class="sxs-lookup"><span data-stu-id="222f2-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="222f2-558">FileName belirtilmediğinde kopyalama tüm BLOB'lar girdi veri kümesi için hello folderPath içerir.</span><span class="sxs-lookup"><span data-stu-id="222f2-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="222f2-559">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: veri. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="222f2-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="222f2-560">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-560">No</span></span> |
| <span data-ttu-id="222f2-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="222f2-561">partitionedBy</span></span> |<span data-ttu-id="222f2-562">partitionedBy isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="222f2-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="222f2-563">Bunu toospecify dinamik folderPath ve dosya adı için zaman serisi veri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="222f2-564">Örneğin, folderPath için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="222f2-565">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-565">No</span></span> |
| <span data-ttu-id="222f2-566">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-566">format</span></span> | <span data-ttu-id="222f2-567">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-568">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-569">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-570">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-571">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-571">No</span></span> |
| <span data-ttu-id="222f2-572">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-572">compression</span></span> | <span data-ttu-id="222f2-573">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-574">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="222f2-575">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-576">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-577">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-578">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-578">Example</span></span>

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


<span data-ttu-id="222f2-579">Daha fazla bilgi için bkz: [Azure Blob bağlayıcı](data-factory-azure-blob-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="222f2-580">Kopyalama etkinliğinde BlobSource</span><span class="sxs-lookup"><span data-stu-id="222f2-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="222f2-581">Bir Azure Blob depolama alanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**BlobSource**ve hello özelliklerinde aşağıdaki belirtin ** kaynak ** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="222f2-582">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-582">Property</span></span> | <span data-ttu-id="222f2-583">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-583">Description</span></span> | <span data-ttu-id="222f2-584">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-584">Allowed values</span></span> | <span data-ttu-id="222f2-585">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-586">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-586">recursive</span></span> |<span data-ttu-id="222f2-587">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="222f2-588">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="222f2-588">True (default value), False</span></span> |<span data-ttu-id="222f2-589">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="222f2-590">Örnek: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="222f2-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="222f2-591">Kopyalama etkinliğinde BlobSink</span><span class="sxs-lookup"><span data-stu-id="222f2-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="222f2-592">Veri tooan Azure Blob Storage kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**BlobSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-593">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-593">Property</span></span> | <span data-ttu-id="222f2-594">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-594">Description</span></span> | <span data-ttu-id="222f2-595">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-595">Allowed values</span></span> | <span data-ttu-id="222f2-596">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="222f2-597">copyBehavior</span></span> |<span data-ttu-id="222f2-598">Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="222f2-599"><b>PreserveHierarchy</b>: korur hello hello hedef klasörü içinde dosya hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="222f2-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="222f2-600">Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="222f2-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="222f2-601"><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hello ilk hedef klasörü düzeyi.</span><span class="sxs-lookup"><span data-stu-id="222f2-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="222f2-602">Merhaba hedef dosyalara otomatik adına sahip.</span><span class="sxs-lookup"><span data-stu-id="222f2-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="222f2-603"><b>MergeFiles (varsayılan):</b> hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="222f2-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="222f2-604">Merhaba dosya/Blob adı belirtilirse, hello birleştirilmiş dosya adı hello belirtilen adı olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="222f2-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="222f2-605">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="222f2-606">Örnek: BlobSink</span><span class="sxs-lookup"><span data-stu-id="222f2-606">Example: BlobSink</span></span>

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

<span data-ttu-id="222f2-607">Daha fazla bilgi için bkz: [Azure Blob bağlayıcı](data-factory-azure-blob-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="222f2-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="222f2-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-609">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-609">Linked service</span></span>
<span data-ttu-id="222f2-610">bir Azure Data Lake Store bağlantılı hizmeti toodefine, kümesi hello tür hello bağlı hizmeti çok**AzureDataLakeStore**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-611">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-611">Property</span></span> | <span data-ttu-id="222f2-612">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-612">Description</span></span> | <span data-ttu-id="222f2-613">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-614">type</span><span class="sxs-lookup"><span data-stu-id="222f2-614">type</span></span> | <span data-ttu-id="222f2-615">Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="222f2-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="222f2-616">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-616">Yes</span></span> |
| <span data-ttu-id="222f2-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="222f2-617">dataLakeStoreUri</span></span> | <span data-ttu-id="222f2-618">Hello Azure Data Lake Store hesabı bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="222f2-619">Biçim aşağıdaki hello olduğu: `https://[accountname].azuredatalakestore.net/webhdfs/v1` veya `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="222f2-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="222f2-620">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-620">Yes</span></span> |
| <span data-ttu-id="222f2-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="222f2-621">subscriptionId</span></span> | <span data-ttu-id="222f2-622">Azure abonelik kimliği toowhich Data Lake Store aittir.</span><span class="sxs-lookup"><span data-stu-id="222f2-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="222f2-623">Havuz için gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-623">Required for sink</span></span> |
| <span data-ttu-id="222f2-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="222f2-624">resourceGroupName</span></span> | <span data-ttu-id="222f2-625">Azure kaynak grubu adı toowhich Data Lake Store aittir.</span><span class="sxs-lookup"><span data-stu-id="222f2-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="222f2-626">Havuz için gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-626">Required for sink</span></span> |
| <span data-ttu-id="222f2-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="222f2-627">servicePrincipalId</span></span> | <span data-ttu-id="222f2-628">Merhaba uygulamanın istemci kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="222f2-629">Evet (hizmet sorumlusu kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="222f2-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="222f2-630">servicePrincipalKey</span></span> | <span data-ttu-id="222f2-631">Merhaba uygulamanın anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-631">Specify hello application's key.</span></span> | <span data-ttu-id="222f2-632">Evet (hizmet sorumlusu kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="222f2-633">Kiracı</span><span class="sxs-lookup"><span data-stu-id="222f2-633">tenant</span></span> | <span data-ttu-id="222f2-634">Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="222f2-635">Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="222f2-636">Evet (hizmet sorumlusu kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="222f2-637">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="222f2-637">authorization</span></span> | <span data-ttu-id="222f2-638">Tıklatın **Authorize** hello düğmesini **Data Factory düzenleyici** ve hello otomatik olarak oluşturulan yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="222f2-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="222f2-639">Evet (kullanıcı kimlik bilgileri doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="222f2-640">SessionID</span><span class="sxs-lookup"><span data-stu-id="222f2-640">sessionId</span></span> | <span data-ttu-id="222f2-641">Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="222f2-642">Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="222f2-643">Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="222f2-644">Evet (kullanıcı kimlik bilgileri doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="222f2-645">Örnek: hizmet asıl kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="222f2-646">Örnek: kullanıcı kimlik bilgilerinin kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="222f2-647">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-648">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-648">Dataset</span></span>
<span data-ttu-id="222f2-649">toodefine bir Azure Data Lake Store dataset kümesi hello **türü** hello kümesinin çok**AzureDataLakeStore**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-650">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-650">Property</span></span> | <span data-ttu-id="222f2-651">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-651">Description</span></span> | <span data-ttu-id="222f2-652">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-653">folderPath</span></span> |<span data-ttu-id="222f2-654">Yol toohello kapsayıcı ve hello Azure Data Lake klasöründe depolayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="222f2-655">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-655">Yes</span></span> |
| <span data-ttu-id="222f2-656">fileName</span><span class="sxs-lookup"><span data-stu-id="222f2-656">fileName</span></span> |<span data-ttu-id="222f2-657">Hello Azure Data Lake Store'da hello dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="222f2-658">isteğe bağlıdır ve büyük küçük harfe duyarlı dosya adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="222f2-659">Bir dosya adı belirtirseniz, (kopyalama dahil) hello etkinlik hello belirli dosya üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="222f2-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="222f2-660">FileName belirtilmediğinde kopyalama hello folderPath girdi veri kümesi için tüm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="222f2-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="222f2-661">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır: veri. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="222f2-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="222f2-662">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-662">No</span></span> |
| <span data-ttu-id="222f2-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="222f2-663">partitionedBy</span></span> |<span data-ttu-id="222f2-664">partitionedBy isteğe bağlı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="222f2-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="222f2-665">Bunu toospecify dinamik folderPath ve dosya adı için zaman serisi veri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="222f2-666">Örneğin, folderPath için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="222f2-667">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-667">No</span></span> |
| <span data-ttu-id="222f2-668">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-668">format</span></span> | <span data-ttu-id="222f2-669">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-670">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-671">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-672">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-673">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-673">No</span></span> |
| <span data-ttu-id="222f2-674">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-674">compression</span></span> | <span data-ttu-id="222f2-675">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-676">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="222f2-677">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-678">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-679">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-680">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-680">Example</span></span>
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

<span data-ttu-id="222f2-681">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="222f2-682">Kopya etkinliği Azure Data Lake Store kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="222f2-683">Bir Azure Data Lake Deposu'ndan veri veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**AzureDataLakeStoreSource**ve hello özelliklerinde aşağıdaki belirtin **kaynağı**  bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="222f2-684">**AzureDataLakeStoreSource** aşağıdaki özelliklere hello destekleyen **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="222f2-685">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-685">Property</span></span> | <span data-ttu-id="222f2-686">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-686">Description</span></span> | <span data-ttu-id="222f2-687">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-687">Allowed values</span></span> | <span data-ttu-id="222f2-688">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-689">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-689">recursive</span></span> |<span data-ttu-id="222f2-690">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="222f2-691">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="222f2-691">True (default value), False</span></span> |<span data-ttu-id="222f2-692">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="222f2-693">Örnek: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="222f2-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="222f2-694">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="222f2-695">Kopya etkinliği Azure Data Lake Store havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-696">Veri tooan Azure Data Lake Store kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**AzureDataLakeStoreSink**ve hello özelliklerinde aşağıdaki belirtin **havuz**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-697">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-697">Property</span></span> | <span data-ttu-id="222f2-698">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-698">Description</span></span> | <span data-ttu-id="222f2-699">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-699">Allowed values</span></span> | <span data-ttu-id="222f2-700">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="222f2-701">copyBehavior</span></span> |<span data-ttu-id="222f2-702">Merhaba kopyalama davranışını belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="222f2-703"><b>PreserveHierarchy</b>: korur hello hello hedef klasörü içinde dosya hiyerarşisi.</span><span class="sxs-lookup"><span data-stu-id="222f2-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="222f2-704">Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="222f2-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="222f2-705"><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hedef klasörün hello ilk düzeyi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="222f2-706">Merhaba hedef dosyaları otomatik adıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="222f2-707"><b>MergeFiles</b>: hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="222f2-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="222f2-708">Merhaba dosya/Blob adı belirtilirse, hello birleştirilmiş dosya adı hello belirtilen adı olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="222f2-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="222f2-709">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="222f2-710">Örnek: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="222f2-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="222f2-711">Daha fazla bilgi için bkz: [Azure Data Lake Store bağlayıcı](data-factory-azure-datalake-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="222f2-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="222f2-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="222f2-713">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-713">Linked service</span></span>
<span data-ttu-id="222f2-714">bir Azure Cosmos DB toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**DocumentDb**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-715">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="222f2-715">**Property**</span></span> | <span data-ttu-id="222f2-716">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="222f2-716">**Description**</span></span> | <span data-ttu-id="222f2-717">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="222f2-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-718">connectionString</span></span> |<span data-ttu-id="222f2-719">Gerekli bilgiler tooconnect tooAzure Cosmos DB veritabanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="222f2-720">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-721">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-721">Example</span></span>

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
<span data-ttu-id="222f2-722">Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-723">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-723">Dataset</span></span>
<span data-ttu-id="222f2-724">toodefine bir Azure Cosmos DB dataset kümesi hello **türü** hello kümesinin çok**DocumentDbCollection**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-725">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="222f2-725">**Property**</span></span> | <span data-ttu-id="222f2-726">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="222f2-726">**Description**</span></span> | <span data-ttu-id="222f2-727">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="222f2-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="222f2-728">collectionName</span></span> |<span data-ttu-id="222f2-729">Hello Azure Cosmos DB koleksiyon adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="222f2-730">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-731">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-731">Example</span></span>

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
<span data-ttu-id="222f2-732">Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="222f2-733">Kopya etkinliği Azure Cosmos DB koleksiyon kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="222f2-734">Bir Azure Cosmos Veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**DocumentDbCollectionSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-735">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="222f2-735">**Property**</span></span> | <span data-ttu-id="222f2-736">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="222f2-736">**Description**</span></span> | <span data-ttu-id="222f2-737">**İzin verilen değerler**</span><span class="sxs-lookup"><span data-stu-id="222f2-737">**Allowed values**</span></span> | <span data-ttu-id="222f2-738">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="222f2-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-739">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-739">query</span></span> |<span data-ttu-id="222f2-740">Merhaba sorgu tooread verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="222f2-741">Sorgu dizesindeki Azure Cosmos DB tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="222f2-742">Örnek:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="222f2-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="222f2-743">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-743">No</span></span> <br/><br/><span data-ttu-id="222f2-744">Belirtilmezse, yürütülen SQL deyimini hello:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="222f2-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="222f2-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="222f2-745">nestingSeparator</span></span> |<span data-ttu-id="222f2-746">Belge hello özel karakter tooindicate iç içe geçmiş</span><span class="sxs-lookup"><span data-stu-id="222f2-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="222f2-747">Herhangi bir karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-747">Any character.</span></span> <br/><br/><span data-ttu-id="222f2-748">Azure Cosmos DB iç içe geçmiş yapılar burada izin verilen bir NoSQL JSON belgeleri için deposudur.</span><span class="sxs-lookup"><span data-stu-id="222f2-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="222f2-749">Azure Data Factory sağlayan kullanıcı toodenote hiyerarşisi olan nestingSeparator aracılığıyla "."</span><span class="sxs-lookup"><span data-stu-id="222f2-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="222f2-750">Yukarıdaki örneklerde Hello.</span><span class="sxs-lookup"><span data-stu-id="222f2-750">in hello above examples.</span></span> <span data-ttu-id="222f2-751">Merhaba ayırıcı ile üç alt öğeleri olan hello "Ad" nesne hello kopyalama etkinliği oluşturacaktır ilk, Orta ve son, according too"Name.First", "Name.Middle" ve "Name.Last" hello, tablo tanımı.</span><span class="sxs-lookup"><span data-stu-id="222f2-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="222f2-752">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-753">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="222f2-754">Kopya etkinliği Azure Cosmos DB koleksiyonu havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-755">Veri tooAzure Cosmos DB kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**DocumentDbCollectionSink**ve hello özelliklerinde aşağıdaki belirtin **havuz**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-756">**Özellik**</span><span class="sxs-lookup"><span data-stu-id="222f2-756">**Property**</span></span> | <span data-ttu-id="222f2-757">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="222f2-757">**Description**</span></span> | <span data-ttu-id="222f2-758">**İzin verilen değerler**</span><span class="sxs-lookup"><span data-stu-id="222f2-758">**Allowed values**</span></span> | <span data-ttu-id="222f2-759">**Gerekli**</span><span class="sxs-lookup"><span data-stu-id="222f2-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="222f2-760">nestingSeparator</span></span> |<span data-ttu-id="222f2-761">Bir özel karakter belge iç içe geçmiş hello kaynak sütun adı tooindicate gereklidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="222f2-762">Örneğin yukarıdaki: `Name.First` hello çıktısında JSON yapısındaki hello Cosmos DB belgede aşağıdaki hello tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="222f2-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="222f2-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="222f2-763">"Name": {</span></span><br/>    <span data-ttu-id="222f2-764">"İlk": "John"</span><span class="sxs-lookup"><span data-stu-id="222f2-764">"First": "John"</span></span><br/><span data-ttu-id="222f2-765">},</span><span class="sxs-lookup"><span data-stu-id="222f2-765">},</span></span> |<span data-ttu-id="222f2-766">Kullanılan tooseparate iç içe geçme düzeyi karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="222f2-767">Varsayılan değer `.` (nokta).</span><span class="sxs-lookup"><span data-stu-id="222f2-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="222f2-768">Kullanılan tooseparate iç içe geçme düzeyi karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="222f2-769">Varsayılan değer `.` (nokta).</span><span class="sxs-lookup"><span data-stu-id="222f2-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="222f2-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-770">writeBatchSize</span></span> |<span data-ttu-id="222f2-771">TooAzure Cosmos DB hizmet toocreate belgeleri istekleri paralel sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="222f2-772">Bu özelliği kullanarak Azure Cosmos DB öğesine/öğesinden veri kopyalama işlemi sırasında hello performans ince ayar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="222f2-773">Daha fazla paralel istekler tooAzure Cosmos DB gönderilir çünkü writeBatchSize artırdığınızda daha iyi bir performans düşüklüğü görebilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="222f2-774">Ancak, azaltma tooavoid gerekir hello hata iletisi atabilirsiniz: "oranıdır büyük istek".</span><span class="sxs-lookup"><span data-stu-id="222f2-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="222f2-775">Azaltmayı bir dizi etkene, belgeler, belgeleri koşullarını sayısı boyutunu dahil olmak üzere, hedef koleksiyon, vb. İlkesi dizin tarafından belirlenir. Kopyalama işlemleri için daha iyi bir koleksiyonu (örneğin, S3) toohave hello çoğu üretilen iş kullanabilirsiniz (2.500 istek birimleri/saniye).</span><span class="sxs-lookup"><span data-stu-id="222f2-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="222f2-776">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="222f2-776">Integer</span></span> |<span data-ttu-id="222f2-777">Hayır (varsayılan: 5)</span><span class="sxs-lookup"><span data-stu-id="222f2-777">No (default: 5)</span></span> |
| <span data-ttu-id="222f2-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-778">writeBatchTimeout</span></span> |<span data-ttu-id="222f2-779">Zaman aşımına uğramadan önce hello işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="222f2-780">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-780">timespan</span></span><br/><br/> <span data-ttu-id="222f2-781">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="222f2-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="222f2-782">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-783">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="222f2-784">Daha fazla bilgi için bkz: [Azure Cosmos DB bağlayıcı](data-factory-azure-documentdb-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="222f2-785">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="222f2-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-786">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-786">Linked service</span></span>
<span data-ttu-id="222f2-787">bir Azure SQL veritabanı toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDatabase**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-788">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-788">Property</span></span> | <span data-ttu-id="222f2-789">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-789">Description</span></span> | <span data-ttu-id="222f2-790">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-791">connectionString</span></span> |<span data-ttu-id="222f2-792">Tooconnect toohello Azure SQL veritabanı örneğinde hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="222f2-793">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-794">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-794">Example</span></span>
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

<span data-ttu-id="222f2-795">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-796">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-796">Dataset</span></span>
<span data-ttu-id="222f2-797">toodefine bir Azure SQL veritabanı veri kümesini kümesi hello **türü** hello kümesinin çok**AzureSqlTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-798">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-798">Property</span></span> | <span data-ttu-id="222f2-799">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-799">Description</span></span> | <span data-ttu-id="222f2-800">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-801">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-801">tableName</span></span> |<span data-ttu-id="222f2-802">Merhaba tablo veya Görünüm hizmeti bağlı hello Azure SQL veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="222f2-803">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-804">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-804">Example</span></span>

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
<span data-ttu-id="222f2-805">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="222f2-806">Kopyalama etkinliğinde SQL kaynağı</span><span class="sxs-lookup"><span data-stu-id="222f2-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="222f2-807">Bir Azure SQL veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**SqlSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-808">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-808">Property</span></span> | <span data-ttu-id="222f2-809">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-809">Description</span></span> | <span data-ttu-id="222f2-810">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-810">Allowed values</span></span> | <span data-ttu-id="222f2-811">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-812">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="222f2-812">sqlReaderQuery</span></span> |<span data-ttu-id="222f2-813">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-814">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-814">SQL query string.</span></span> <span data-ttu-id="222f2-815">Örnek: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-816">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-816">No</span></span> |
| <span data-ttu-id="222f2-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="222f2-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="222f2-818">Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="222f2-819">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="222f2-820">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-820">No</span></span> |
| <span data-ttu-id="222f2-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-821">storedProcedureParameters</span></span> |<span data-ttu-id="222f2-822">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="222f2-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="222f2-823">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-823">Name/value pairs.</span></span> <span data-ttu-id="222f2-824">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="222f2-825">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-826">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-826">Example</span></span>

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
<span data-ttu-id="222f2-827">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="222f2-828">Kopyalama etkinliği SQL havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-829">Veri tooAzure SQL veritabanı kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**SqlSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-830">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-830">Property</span></span> | <span data-ttu-id="222f2-831">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-831">Description</span></span> | <span data-ttu-id="222f2-832">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-832">Allowed values</span></span> | <span data-ttu-id="222f2-833">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-834">writeBatchTimeout</span></span> |<span data-ttu-id="222f2-835">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="222f2-836">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-836">timespan</span></span><br/><br/> <span data-ttu-id="222f2-837">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="222f2-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="222f2-838">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-838">No</span></span> |
| <span data-ttu-id="222f2-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-839">writeBatchSize</span></span> |<span data-ttu-id="222f2-840">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="222f2-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="222f2-841">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="222f2-841">Integer (number of rows)</span></span> |<span data-ttu-id="222f2-842">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="222f2-842">No (default: 10000)</span></span> |
| <span data-ttu-id="222f2-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="222f2-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="222f2-844">Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="222f2-845">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="222f2-845">A query statement.</span></span> |<span data-ttu-id="222f2-846">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-846">No</span></span> |
| <span data-ttu-id="222f2-847">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="222f2-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="222f2-848">Kopyalama etkinliği toofill bir sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="222f2-849">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="222f2-850">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-850">No</span></span> |
| <span data-ttu-id="222f2-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="222f2-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="222f2-852">Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı.</span><span class="sxs-lookup"><span data-stu-id="222f2-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="222f2-853">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="222f2-854">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-854">No</span></span> |
| <span data-ttu-id="222f2-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-855">storedProcedureParameters</span></span> |<span data-ttu-id="222f2-856">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="222f2-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="222f2-857">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-857">Name/value pairs.</span></span> <span data-ttu-id="222f2-858">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="222f2-859">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-859">No</span></span> |
| <span data-ttu-id="222f2-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="222f2-860">sqlWriterTableType</span></span> |<span data-ttu-id="222f2-861">Merhaba saklı yordamda kullanılan bir tablo türü adı toobe belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="222f2-862">Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="222f2-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="222f2-863">Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="222f2-864">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-864">A table type name.</span></span> |<span data-ttu-id="222f2-865">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-866">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-866">Example</span></span>

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

<span data-ttu-id="222f2-867">Daha fazla bilgi için bkz: [Azure SQL bağlayıcı](data-factory-azure-sql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="222f2-868">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="222f2-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-869">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-869">Linked service</span></span>
<span data-ttu-id="222f2-870">Azure SQL Data Warehouse toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDW**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-871">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-871">Property</span></span> | <span data-ttu-id="222f2-872">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-872">Description</span></span> | <span data-ttu-id="222f2-873">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-874">connectionString</span></span> |<span data-ttu-id="222f2-875">Tooconnect toohello Azure SQL Data Warehouse örneğine hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="222f2-876">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="222f2-877">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-877">Example</span></span>

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

<span data-ttu-id="222f2-878">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-879">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-879">Dataset</span></span>
<span data-ttu-id="222f2-880">toodefine bir Azure SQL veri ambarı veri kümesi kümesi hello **türü** hello kümesinin çok**AzureSqlDWTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-881">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-881">Property</span></span> | <span data-ttu-id="222f2-882">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-882">Description</span></span> | <span data-ttu-id="222f2-883">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-884">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-884">tableName</span></span> |<span data-ttu-id="222f2-885">Merhaba tablonun veya bağlantılı hizmet hello hello Azure SQL Data Warehouse Veritabanı görünümünde adı ifade eder.</span><span class="sxs-lookup"><span data-stu-id="222f2-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="222f2-886">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-887">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-887">Example</span></span>

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

<span data-ttu-id="222f2-888">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="222f2-889">Kopyalama etkinliğinde SQL DW kaynağı</span><span class="sxs-lookup"><span data-stu-id="222f2-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="222f2-890">Azure SQL veri ambarından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**SqlDWSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-891">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-891">Property</span></span> | <span data-ttu-id="222f2-892">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-892">Description</span></span> | <span data-ttu-id="222f2-893">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-893">Allowed values</span></span> | <span data-ttu-id="222f2-894">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-895">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="222f2-895">sqlReaderQuery</span></span> |<span data-ttu-id="222f2-896">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-897">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-897">SQL query string.</span></span> <span data-ttu-id="222f2-898">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-899">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-899">No</span></span> |
| <span data-ttu-id="222f2-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="222f2-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="222f2-901">Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="222f2-902">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="222f2-903">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-903">No</span></span> |
| <span data-ttu-id="222f2-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-904">storedProcedureParameters</span></span> |<span data-ttu-id="222f2-905">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="222f2-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="222f2-906">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-906">Name/value pairs.</span></span> <span data-ttu-id="222f2-907">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="222f2-908">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-909">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-909">Example</span></span>

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

<span data-ttu-id="222f2-910">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="222f2-911">SQL DW havuz kopyalama etkinliğinde</span><span class="sxs-lookup"><span data-stu-id="222f2-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-912">SQL veri ambarı veri tooAzure kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**SqlDWSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-913">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-913">Property</span></span> | <span data-ttu-id="222f2-914">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-914">Description</span></span> | <span data-ttu-id="222f2-915">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-915">Allowed values</span></span> | <span data-ttu-id="222f2-916">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="222f2-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="222f2-918">Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="222f2-919">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="222f2-919">A query statement.</span></span> |<span data-ttu-id="222f2-920">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-920">No</span></span> |
| <span data-ttu-id="222f2-921">Bulunan'allowpolybase</span><span class="sxs-lookup"><span data-stu-id="222f2-921">allowPolyBase</span></span> |<span data-ttu-id="222f2-922">Gösterir olup olmadığını BULKINSERT mekanizması yerine toouse PolyBase (varsa).</span><span class="sxs-lookup"><span data-stu-id="222f2-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="222f2-923">**PolyBase kullanarak SQL Data Warehouse'a veri yolu tooload veri önerilen hello değildir.**</span><span class="sxs-lookup"><span data-stu-id="222f2-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="222f2-924">True</span><span class="sxs-lookup"><span data-stu-id="222f2-924">True</span></span> <br/><span data-ttu-id="222f2-925">False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-925">False (default)</span></span> |<span data-ttu-id="222f2-926">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-926">No</span></span> |
| <span data-ttu-id="222f2-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="222f2-927">polyBaseSettings</span></span> |<span data-ttu-id="222f2-928">Bir grup hello belirtilebilir özellik **Bulunan'allowpolybase** özelliği çok ayarlanmış**doğru**.</span><span class="sxs-lookup"><span data-stu-id="222f2-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="222f2-929">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-929">No</span></span> |
| <span data-ttu-id="222f2-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="222f2-930">rejectValue</span></span> |<span data-ttu-id="222f2-931">Merhaba numarası veya hello sorgu başarısız olmadan önce reddedilemiyor satırları yüzdesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="222f2-932">Merhaba seçeneklerinde Reddet hello PolyBase'nın hakkında daha fazla bilgi edinin **bağımsız değişkenleri** bölümünü [CREATE dış TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="222f2-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="222f2-933">0 (varsayılan), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="222f2-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="222f2-934">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-934">No</span></span> |
| <span data-ttu-id="222f2-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="222f2-935">rejectType</span></span> |<span data-ttu-id="222f2-936">Merhaba rejectValue seçeneği bir hazır değer veya bir yüzde belirtilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="222f2-937">Değer (varsayılan), yüzde</span><span class="sxs-lookup"><span data-stu-id="222f2-937">Value (default), Percentage</span></span> |<span data-ttu-id="222f2-938">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-938">No</span></span> |
| <span data-ttu-id="222f2-939">Havuzu'na ilişkin</span><span class="sxs-lookup"><span data-stu-id="222f2-939">rejectSampleValue</span></span> |<span data-ttu-id="222f2-940">Merhaba PolyBase reddedilen satırları hello yüzdesini yeniden hesaplar önce satırları tooretrieve hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="222f2-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="222f2-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="222f2-941">1, 2, …</span></span> |<span data-ttu-id="222f2-942">Evet, varsa **rejectType** olan **yüzdesi**</span><span class="sxs-lookup"><span data-stu-id="222f2-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="222f2-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="222f2-943">useTypeDefault</span></span> |<span data-ttu-id="222f2-944">PolyBase hello metin dosyasından veri aldığında değerlerde eksik toohandle metin dosyaları nasıl ayrılmış belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="222f2-945">Merhaba bağımsız değişkenler bölümünde bu özelliği hakkında daha fazla bilgi [oluşturma EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="222f2-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="222f2-946">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-946">True, False (default)</span></span> |<span data-ttu-id="222f2-947">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-947">No</span></span> |
| <span data-ttu-id="222f2-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-948">writeBatchSize</span></span> |<span data-ttu-id="222f2-949">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="222f2-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="222f2-950">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="222f2-950">Integer (number of rows)</span></span> |<span data-ttu-id="222f2-951">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="222f2-951">No (default: 10000)</span></span> |
| <span data-ttu-id="222f2-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-952">writeBatchTimeout</span></span> |<span data-ttu-id="222f2-953">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="222f2-954">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-954">timespan</span></span><br/><br/> <span data-ttu-id="222f2-955">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="222f2-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="222f2-956">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-957">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-957">Example</span></span>

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

<span data-ttu-id="222f2-958">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="222f2-959">Azure Search</span><span class="sxs-lookup"><span data-stu-id="222f2-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-960">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-960">Linked service</span></span>
<span data-ttu-id="222f2-961">Azure Search toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSearch**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-962">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-962">Property</span></span> | <span data-ttu-id="222f2-963">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-963">Description</span></span> | <span data-ttu-id="222f2-964">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="222f2-965">URL</span><span class="sxs-lookup"><span data-stu-id="222f2-965">url</span></span> | <span data-ttu-id="222f2-966">Hello Azure Search hizmeti için URL.</span><span class="sxs-lookup"><span data-stu-id="222f2-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="222f2-967">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-967">Yes</span></span> |
| <span data-ttu-id="222f2-968">anahtar</span><span class="sxs-lookup"><span data-stu-id="222f2-968">key</span></span> | <span data-ttu-id="222f2-969">Hello Azure Search hizmeti için yönetici anahtarı.</span><span class="sxs-lookup"><span data-stu-id="222f2-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="222f2-970">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-971">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-971">Example</span></span>

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

<span data-ttu-id="222f2-972">Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-973">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-973">Dataset</span></span>
<span data-ttu-id="222f2-974">toodefine bir Azure Search dataset kümesi hello **türü** hello kümesinin çok**AzureSearchIndex**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü :</span><span class="sxs-lookup"><span data-stu-id="222f2-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-975">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-975">Property</span></span> | <span data-ttu-id="222f2-976">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-976">Description</span></span> | <span data-ttu-id="222f2-977">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="222f2-978">type</span><span class="sxs-lookup"><span data-stu-id="222f2-978">type</span></span> | <span data-ttu-id="222f2-979">Merhaba type özelliği çok ayarlanmalıdır**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="222f2-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="222f2-980">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-980">Yes</span></span> |
| <span data-ttu-id="222f2-981">indexName</span><span class="sxs-lookup"><span data-stu-id="222f2-981">indexName</span></span> | <span data-ttu-id="222f2-982">Hello Azure Search dizini adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="222f2-983">Veri Fabrikası hello dizin oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="222f2-984">Başlangıç dizini, Azure Search'te mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="222f2-985">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-986">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-986">Example</span></span>

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

<span data-ttu-id="222f2-987">Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="222f2-988">Kopya etkinliği Azure arama dizini havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-989">Veri tooan Azure Search dizini kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**AzureSearchIndexSink**ve hello özelliklerinde aşağıdaki belirtin **havuz**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-990">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-990">Property</span></span> | <span data-ttu-id="222f2-991">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-991">Description</span></span> | <span data-ttu-id="222f2-992">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-992">Allowed values</span></span> | <span data-ttu-id="222f2-993">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="222f2-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="222f2-994">WriteBehavior</span></span> | <span data-ttu-id="222f2-995">Toomerge veya Değiştir bir belgeyi açtığında hello dizinde zaten olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="222f2-996">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-996">Merge (default)</span></span><br/><span data-ttu-id="222f2-997">Karşıya Yükle</span><span class="sxs-lookup"><span data-stu-id="222f2-997">Upload</span></span>| <span data-ttu-id="222f2-998">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-998">No</span></span> |
| <span data-ttu-id="222f2-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-999">WriteBatchSize</span></span> | <span data-ttu-id="222f2-1000">Hello arabellek boyutu writeBatchSize ulaştığında hello Azure Search dizinine veri yükler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="222f2-1001">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="222f2-1001">1 too1,000.</span></span> <span data-ttu-id="222f2-1002">Varsayılan değer 1000'dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1002">Default value is 1000.</span></span> | <span data-ttu-id="222f2-1003">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1004">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1004">Example</span></span>

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

<span data-ttu-id="222f2-1005">Daha fazla bilgi için bkz: [Azure Search Bağlayıcısı](data-factory-azure-search-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="222f2-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="222f2-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1007">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1007">Linked service</span></span>
<span data-ttu-id="222f2-1008">Bağlı hizmetler iki tür vardır: Azure depolama bağlantılı hizmeti ve Azure depolama SAS bağlantılı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="222f2-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="222f2-1009">Azure Storage Bağlı Hizmeti</span><span class="sxs-lookup"><span data-stu-id="222f2-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="222f2-1010">toolink hello kullanarak Azure depolama hesabı tooa veri fabrikası **hesap anahtarı**, bir Azure Storage bağlı hizmeti oluşturma.</span><span class="sxs-lookup"><span data-stu-id="222f2-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="222f2-1011">toodefine bir Azure depolama bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="222f2-1012">Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1013">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1013">Property</span></span> | <span data-ttu-id="222f2-1014">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1014">Description</span></span> | <span data-ttu-id="222f2-1015">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-1016">type</span><span class="sxs-lookup"><span data-stu-id="222f2-1016">type</span></span> |<span data-ttu-id="222f2-1017">Merhaba type özelliği ayarlanmalıdır: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="222f2-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="222f2-1018">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1018">Yes</span></span> |
| <span data-ttu-id="222f2-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-1019">connectionString</span></span> |<span data-ttu-id="222f2-1020">Tooconnect tooAzure depolama hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="222f2-1021">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1021">Yes</span></span> |

<span data-ttu-id="222f2-1022">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="222f2-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="222f2-1023">Azure Storage SAS bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="222f2-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="222f2-1024">Hello Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak toolink bir Azure depolama hesabı tooan Azure data factory sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="222f2-1025">Kısıtlanmış/zaman sınırlı erişimi hello veri fabrikası hello depolama tooall/özel kaynakları (blob/kapsayıcısı) sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="222f2-1026">bir Azure depolama bağlı SAS hizmeti toolink paylaşılan erişim imzası kullanarak Azure depolama hesabı tooa veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="222f2-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="222f2-1027">toodefine bir Azure depolama SAS bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="222f2-1028">Ardından hello özelliklerinde aşağıdaki belirtebilirsiniz **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="222f2-1029">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1029">Property</span></span> | <span data-ttu-id="222f2-1030">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1030">Description</span></span> | <span data-ttu-id="222f2-1031">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-1032">type</span><span class="sxs-lookup"><span data-stu-id="222f2-1032">type</span></span> |<span data-ttu-id="222f2-1033">Merhaba type özelliği ayarlanmalıdır: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="222f2-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="222f2-1034">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1034">Yes</span></span> |
| <span data-ttu-id="222f2-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="222f2-1035">sasUri</span></span> |<span data-ttu-id="222f2-1036">Blob, kapsayıcı ya da tablo gibi paylaşılan erişim imzası URI toohello Azure Storage kaynakları belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="222f2-1037">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1037">Yes</span></span> |

<span data-ttu-id="222f2-1038">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="222f2-1038">**Example:**</span></span>

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

<span data-ttu-id="222f2-1039">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1040">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1040">Dataset</span></span>
<span data-ttu-id="222f2-1041">toodefine bir Azure tablosu veri kümesi kümesi hello **türü** hello kümesinin çok**AzureTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1042">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1042">Property</span></span> | <span data-ttu-id="222f2-1043">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1043">Description</span></span> | <span data-ttu-id="222f2-1044">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1045">tableName</span></span> |<span data-ttu-id="222f2-1046">Bağlantılı hizmetinin hello Azure tablo veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="222f2-1047">Evet.</span><span class="sxs-lookup"><span data-stu-id="222f2-1047">Yes.</span></span> <span data-ttu-id="222f2-1048">Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="222f2-1049">Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1050">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1050">Example</span></span>

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

<span data-ttu-id="222f2-1051">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="222f2-1052">Kopya etkinliği Azure tablo kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1053">Azure tablo depolamasından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**AzureTableSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1054">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1054">Property</span></span> | <span data-ttu-id="222f2-1055">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1055">Description</span></span> | <span data-ttu-id="222f2-1056">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1056">Allowed values</span></span> | <span data-ttu-id="222f2-1057">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1058">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="222f2-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="222f2-1059">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1060">Azure tablo sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1060">Azure table query string.</span></span> <span data-ttu-id="222f2-1061">Merhaba sonraki bölümdeki örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1061">See examples in hello next section.</span></span> |<span data-ttu-id="222f2-1062">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1062">No.</span></span> <span data-ttu-id="222f2-1063">Bir tableName bir azureTableSourceQuery belirtildiğinde, tüm hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="222f2-1064">Bir azureTableSourceQuery de belirtilirse hello sorguyu karşılayan hello tablosundan kopyalanan toohello hedef kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="222f2-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="222f2-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="222f2-1066">Tablonun swallow hello özel durum var olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="222f2-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="222f2-1067">TRUE</span></span><br/><span data-ttu-id="222f2-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="222f2-1068">FALSE</span></span> |<span data-ttu-id="222f2-1069">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1070">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1070">Example</span></span>

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

<span data-ttu-id="222f2-1071">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="222f2-1072">Kopya etkinliği Azure tablo havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-1073">Veri tooAzure Table Storage kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**AzureTableSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-1074">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1074">Property</span></span> | <span data-ttu-id="222f2-1075">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1075">Description</span></span> | <span data-ttu-id="222f2-1076">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1076">Allowed values</span></span> | <span data-ttu-id="222f2-1077">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="222f2-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="222f2-1079">Merhaba havuzu tarafından kullanılan varsayılan bölüm anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="222f2-1080">Bir dize değeri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1080">A string value.</span></span> |<span data-ttu-id="222f2-1081">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1081">No</span></span> |
| <span data-ttu-id="222f2-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="222f2-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="222f2-1083">Değerleri bölüm anahtarları olarak kullanılan hello sütunun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="222f2-1084">Belirtilmezse, AzureTableDefaultPartitionKeyValue hello bölüm anahtarı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="222f2-1085">Sütun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1085">A column name.</span></span> |<span data-ttu-id="222f2-1086">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1086">No</span></span> |
| <span data-ttu-id="222f2-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="222f2-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="222f2-1088">Sütun değerleri satır anahtarı olarak kullanılan hello sütunun adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="222f2-1089">Belirtilmezse, her satır için bir GUID kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="222f2-1090">Sütun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1090">A column name.</span></span> |<span data-ttu-id="222f2-1091">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1091">No</span></span> |
| <span data-ttu-id="222f2-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="222f2-1092">azureTableInsertType</span></span> |<span data-ttu-id="222f2-1093">başlangıç modu tooinsert verileri Azure tablosuna.</span><span class="sxs-lookup"><span data-stu-id="222f2-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="222f2-1094">Bu özellik, varolan satırlardan eşleşen bölüm ve satır anahtarlarla hello çıkış tablodaki birleştirilmiş veya değiştirilmesi değerlerine sahip olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="222f2-1095">Bu ayarların (birleştirme ve değiştirme) nasıl çalıştığını, ilgili toolearn bkz [ekleme veya birleştirme varlık](https://msdn.microsoft.com/library/azure/hh452241.aspx) ve [ekleme veya değiştirme varlık](https://msdn.microsoft.com/library/azure/hh452242.aspx) konuları.</span><span class="sxs-lookup"><span data-stu-id="222f2-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="222f2-1096">Hello satır düzeyinde, hello tablo düzeyinde değil, bu ayar uygulanır ve her iki seçenek hello giriş yok hello çıkış tablosundaki satırları siler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="222f2-1097">Merge (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-1097">merge (default)</span></span><br/><span data-ttu-id="222f2-1098">Değiştir</span><span class="sxs-lookup"><span data-stu-id="222f2-1098">replace</span></span> |<span data-ttu-id="222f2-1099">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1099">No</span></span> |
| <span data-ttu-id="222f2-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-1100">writeBatchSize</span></span> |<span data-ttu-id="222f2-1101">Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="222f2-1102">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="222f2-1102">Integer (number of rows)</span></span> |<span data-ttu-id="222f2-1103">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="222f2-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="222f2-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-1104">writeBatchTimeout</span></span> |<span data-ttu-id="222f2-1105">Merhaba writeBatchSize veya writeBatchTimeout gelindiğinde veri hello Azure tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="222f2-1106">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-1106">timespan</span></span><br/><br/><span data-ttu-id="222f2-1107">Örnek: "00: 20:00" (20 dakika)</span><span class="sxs-lookup"><span data-stu-id="222f2-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="222f2-1108">Hayır (varsayılan toostorage istemci varsayılan zaman aşımı değeri 90 saniye)</span><span class="sxs-lookup"><span data-stu-id="222f2-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1109">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1109">Example</span></span>

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
<span data-ttu-id="222f2-1110">Bu bağlantılı hizmetler hakkında daha fazla bilgi için bkz: [Azure Table Storage bağlayıcı](data-factory-azure-table-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="222f2-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="222f2-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1112">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1112">Linked service</span></span>
<span data-ttu-id="222f2-1113">toodefine bir Amazon Redshift bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AmazonRedshift**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1114">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1114">Property</span></span> | <span data-ttu-id="222f2-1115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1115">Description</span></span> | <span data-ttu-id="222f2-1116">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1117">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1117">server</span></span> |<span data-ttu-id="222f2-1118">IP adresi veya ana bilgisayar hello Amazon Redshift sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="222f2-1119">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1119">Yes</span></span> |
| <span data-ttu-id="222f2-1120">port</span><span class="sxs-lookup"><span data-stu-id="222f2-1120">port</span></span> |<span data-ttu-id="222f2-1121">Amazon Redshift sunucu hello hello TCP bağlantı noktası sayısı Hello toolisten istemci bağlantıları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="222f2-1122">Hayır, varsayılan değer: 5439</span><span class="sxs-lookup"><span data-stu-id="222f2-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="222f2-1123">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="222f2-1123">database</span></span> |<span data-ttu-id="222f2-1124">Merhaba Amazon Redshift veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="222f2-1125">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1125">Yes</span></span> |
| <span data-ttu-id="222f2-1126">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1126">username</span></span> |<span data-ttu-id="222f2-1127">Erişim toohello veritabanı olan kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="222f2-1128">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1128">Yes</span></span> |
| <span data-ttu-id="222f2-1129">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1129">password</span></span> |<span data-ttu-id="222f2-1130">Merhaba kullanıcı hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-1130">Password for hello user account.</span></span> |<span data-ttu-id="222f2-1131">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1132">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1132">Example</span></span>

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

<span data-ttu-id="222f2-1133">Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1134">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1134">Dataset</span></span>
<span data-ttu-id="222f2-1135">toodefine bir Amazon Redshift dataset kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1136">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1136">Property</span></span> | <span data-ttu-id="222f2-1137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1137">Description</span></span> | <span data-ttu-id="222f2-1138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1139">tableName</span></span> |<span data-ttu-id="222f2-1140">Bağlantılı hizmetinin hello Amazon Redshift veritabanında Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="222f2-1141">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="222f2-1142">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1142">Example</span></span>

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
<span data-ttu-id="222f2-1143">Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1144">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="222f2-1145">Amazon Redshift veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1146">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1146">Property</span></span> | <span data-ttu-id="222f2-1147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1147">Description</span></span> | <span data-ttu-id="222f2-1148">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1148">Allowed values</span></span> | <span data-ttu-id="222f2-1149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1150">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1150">query</span></span> |<span data-ttu-id="222f2-1151">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1152">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1152">SQL query string.</span></span> <span data-ttu-id="222f2-1153">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-1154">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1155">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1155">Example</span></span>

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
<span data-ttu-id="222f2-1156">Daha fazla bilgi için bkz: [Amazon Redshift bağlayıcı](#data-factory-amazon-redshift-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="222f2-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="222f2-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1158">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1158">Linked service</span></span>
<span data-ttu-id="222f2-1159">toodefine bir IBM DB2 bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesDB2**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1160">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1160">Property</span></span> | <span data-ttu-id="222f2-1161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1161">Description</span></span> | <span data-ttu-id="222f2-1162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1163">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1163">server</span></span> |<span data-ttu-id="222f2-1164">Merhaba DB2 sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="222f2-1165">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1165">Yes</span></span> |
| <span data-ttu-id="222f2-1166">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="222f2-1166">database</span></span> |<span data-ttu-id="222f2-1167">Merhaba DB2 veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="222f2-1168">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1168">Yes</span></span> |
| <span data-ttu-id="222f2-1169">Şema</span><span class="sxs-lookup"><span data-stu-id="222f2-1169">schema</span></span> |<span data-ttu-id="222f2-1170">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="222f2-1171">Merhaba şema adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="222f2-1172">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1172">No</span></span> |
| <span data-ttu-id="222f2-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1173">authenticationType</span></span> |<span data-ttu-id="222f2-1174">Kimlik doğrulama türü tooconnect toohello DB2 veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="222f2-1175">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="222f2-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="222f2-1176">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1176">Yes</span></span> |
| <span data-ttu-id="222f2-1177">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1177">username</span></span> |<span data-ttu-id="222f2-1178">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="222f2-1179">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1179">No</span></span> |
| <span data-ttu-id="222f2-1180">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1180">password</span></span> |<span data-ttu-id="222f2-1181">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-1182">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1182">No</span></span> |
| <span data-ttu-id="222f2-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1183">gatewayName</span></span> |<span data-ttu-id="222f2-1184">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi DB2 veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="222f2-1185">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1186">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1186">Example</span></span>
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
<span data-ttu-id="222f2-1187">Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1188">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1188">Dataset</span></span>
<span data-ttu-id="222f2-1189">toodefine bir DB2 veri kümesi, kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="222f2-1190">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1190">Property</span></span> | <span data-ttu-id="222f2-1191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1191">Description</span></span> | <span data-ttu-id="222f2-1192">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1193">tableName</span></span> |<span data-ttu-id="222f2-1194">Bağlantılı hizmetinin hello DB2 veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="222f2-1195">Merhaba tableName büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="222f2-1196">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="222f2-1197">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1197">Example</span></span>
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

<span data-ttu-id="222f2-1198">Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1199">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1200">IBM DB2'den veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1201">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1201">Property</span></span> | <span data-ttu-id="222f2-1202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1202">Description</span></span> | <span data-ttu-id="222f2-1203">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1203">Allowed values</span></span> | <span data-ttu-id="222f2-1204">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1205">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1205">query</span></span> |<span data-ttu-id="222f2-1206">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1207">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1207">SQL query string.</span></span> <span data-ttu-id="222f2-1208">Örneğin: `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="222f2-1209">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1210">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1210">Example</span></span>
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
<span data-ttu-id="222f2-1211">Daha fazla bilgi için bkz: [IBM DB2 Bağlayıcısı](#data-factory-onprem-db2-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="222f2-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="222f2-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1213">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1213">Linked service</span></span>
<span data-ttu-id="222f2-1214">bir MySQL toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesMySql**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1215">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1215">Property</span></span> | <span data-ttu-id="222f2-1216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1216">Description</span></span> | <span data-ttu-id="222f2-1217">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1218">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1218">server</span></span> |<span data-ttu-id="222f2-1219">Merhaba MySQL sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="222f2-1220">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1220">Yes</span></span> |
| <span data-ttu-id="222f2-1221">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="222f2-1221">database</span></span> |<span data-ttu-id="222f2-1222">Merhaba MySQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="222f2-1223">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1223">Yes</span></span> |
| <span data-ttu-id="222f2-1224">Şema</span><span class="sxs-lookup"><span data-stu-id="222f2-1224">schema</span></span> |<span data-ttu-id="222f2-1225">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="222f2-1226">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1226">No</span></span> |
| <span data-ttu-id="222f2-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1227">authenticationType</span></span> |<span data-ttu-id="222f2-1228">Kimlik doğrulama türü tooconnect toohello MySQL veritabanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="222f2-1229">Olası değerler şunlardır: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="222f2-1230">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1230">Yes</span></span> |
| <span data-ttu-id="222f2-1231">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1231">username</span></span> |<span data-ttu-id="222f2-1232">Kullanıcı adı tooconnect toohello MySQL veritabanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="222f2-1233">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1233">Yes</span></span> |
| <span data-ttu-id="222f2-1234">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1234">password</span></span> |<span data-ttu-id="222f2-1235">Belirttiğiniz hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="222f2-1236">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1236">Yes</span></span> |
| <span data-ttu-id="222f2-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1237">gatewayName</span></span> |<span data-ttu-id="222f2-1238">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi MySQL veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="222f2-1239">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1240">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1240">Example</span></span>

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

<span data-ttu-id="222f2-1241">Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1242">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1242">Dataset</span></span>
<span data-ttu-id="222f2-1243">toodefine bir MySQL veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1244">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1244">Property</span></span> | <span data-ttu-id="222f2-1245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1245">Description</span></span> | <span data-ttu-id="222f2-1246">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1247">tableName</span></span> |<span data-ttu-id="222f2-1248">Merhaba bağlı MySQL veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="222f2-1249">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1250">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1250">Example</span></span>

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
<span data-ttu-id="222f2-1251">Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1252">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1253">Bir MySQL veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1254">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1254">Property</span></span> | <span data-ttu-id="222f2-1255">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1255">Description</span></span> | <span data-ttu-id="222f2-1256">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1256">Allowed values</span></span> | <span data-ttu-id="222f2-1257">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1258">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1258">query</span></span> |<span data-ttu-id="222f2-1259">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1260">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1260">SQL query string.</span></span> <span data-ttu-id="222f2-1261">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-1262">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="222f2-1263">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1263">Example</span></span>
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

<span data-ttu-id="222f2-1264">Daha fazla bilgi için bkz: [MySQL bağlayıcı](data-factory-onprem-mysql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="222f2-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="222f2-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-1266">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1266">Linked service</span></span>
<span data-ttu-id="222f2-1267">bir Oracle toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesOracle**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1268">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1268">Property</span></span> | <span data-ttu-id="222f2-1269">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1269">Description</span></span> | <span data-ttu-id="222f2-1270">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="222f2-1271">driverType</span></span> | <span data-ttu-id="222f2-1272">Hangi sürücü toouse toocopy verilerden belirtin / tooOracle veritabanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="222f2-1273">İzin verilen değerler **Microsoft** veya **ODP** (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="222f2-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="222f2-1274">Bkz: [desteklenen sürümü ve yükleme](#supported-versions-and-installation) sürücü ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="222f2-1275">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1275">No</span></span> |
| <span data-ttu-id="222f2-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-1276">connectionString</span></span> | <span data-ttu-id="222f2-1277">Tooconnect toohello Oracle veritabanı örneği hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="222f2-1278">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1278">Yes</span></span> |
| <span data-ttu-id="222f2-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1279">gatewayName</span></span> | <span data-ttu-id="222f2-1280">Kullanılan tooconnect toohello olan şirket içi Oracle Sunucusu hello ağ geçidi adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="222f2-1281">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1282">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1282">Example</span></span>
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

<span data-ttu-id="222f2-1283">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1284">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1284">Dataset</span></span>
<span data-ttu-id="222f2-1285">toodefine bir Oracle veri kümesini kümesi hello **türü** hello kümesinin çok**OracleTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1286">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1286">Property</span></span> | <span data-ttu-id="222f2-1287">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1287">Description</span></span> | <span data-ttu-id="222f2-1288">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1289">tableName</span></span> |<span data-ttu-id="222f2-1290">Merhaba bağlantılı hizmet hello Oracle veritabanı Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="222f2-1291">Hayır (varsa **oracleReaderQuery** , **OracleSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1292">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1292">Example</span></span>

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
<span data-ttu-id="222f2-1293">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="222f2-1294">Kopyalama etkinliği Oracle kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1295">Bir Oracle veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**OracleSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1296">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1296">Property</span></span> | <span data-ttu-id="222f2-1297">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1297">Description</span></span> | <span data-ttu-id="222f2-1298">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1298">Allowed values</span></span> | <span data-ttu-id="222f2-1299">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="222f2-1300">oracleReaderQuery</span></span> |<span data-ttu-id="222f2-1301">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1302">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1302">SQL query string.</span></span> <span data-ttu-id="222f2-1303">Örneğin, `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="222f2-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="222f2-1304">Belirtilmezse, yürütülen SQL deyimini hello:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="222f2-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="222f2-1305">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1306">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1306">Example</span></span>

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

<span data-ttu-id="222f2-1307">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="222f2-1308">Kopyalama etkinliği Oracle havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-1309">Veri tooam Oracle veritabanı kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**OracleSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-1310">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1310">Property</span></span> | <span data-ttu-id="222f2-1311">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1311">Description</span></span> | <span data-ttu-id="222f2-1312">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1312">Allowed values</span></span> | <span data-ttu-id="222f2-1313">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-1314">writeBatchTimeout</span></span> |<span data-ttu-id="222f2-1315">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="222f2-1316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-1316">timespan</span></span><br/><br/> <span data-ttu-id="222f2-1317">Örnek: 00:30:00 (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="222f2-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="222f2-1318">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1318">No</span></span> |
| <span data-ttu-id="222f2-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-1319">writeBatchSize</span></span> |<span data-ttu-id="222f2-1320">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="222f2-1321">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="222f2-1321">Integer (number of rows)</span></span> |<span data-ttu-id="222f2-1322">Hayır (varsayılan: 100)</span><span class="sxs-lookup"><span data-stu-id="222f2-1322">No (default: 100)</span></span> |
| <span data-ttu-id="222f2-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="222f2-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="222f2-1324">Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="222f2-1325">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1325">A query statement.</span></span> |<span data-ttu-id="222f2-1326">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1326">No</span></span> |
| <span data-ttu-id="222f2-1327">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="222f2-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="222f2-1328">Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="222f2-1329">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="222f2-1330">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1331">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1331">Example</span></span>
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
<span data-ttu-id="222f2-1332">Daha fazla bilgi için bkz: [Oracle bağlayıcı](data-factory-onprem-oracle-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="222f2-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="222f2-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1334">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1334">Linked service</span></span>
<span data-ttu-id="222f2-1335">bir PostgreSQL toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesPostgreSql**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1336">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1336">Property</span></span> | <span data-ttu-id="222f2-1337">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1337">Description</span></span> | <span data-ttu-id="222f2-1338">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1339">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1339">server</span></span> |<span data-ttu-id="222f2-1340">Merhaba PostgreSQL sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="222f2-1341">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1341">Yes</span></span> |
| <span data-ttu-id="222f2-1342">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="222f2-1342">database</span></span> |<span data-ttu-id="222f2-1343">Merhaba PostgreSQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="222f2-1344">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1344">Yes</span></span> |
| <span data-ttu-id="222f2-1345">Şema</span><span class="sxs-lookup"><span data-stu-id="222f2-1345">schema</span></span> |<span data-ttu-id="222f2-1346">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="222f2-1347">Merhaba şema adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="222f2-1348">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1348">No</span></span> |
| <span data-ttu-id="222f2-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1349">authenticationType</span></span> |<span data-ttu-id="222f2-1350">Kimlik doğrulama türü tooconnect toohello PostgreSQL veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="222f2-1351">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="222f2-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="222f2-1352">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1352">Yes</span></span> |
| <span data-ttu-id="222f2-1353">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1353">username</span></span> |<span data-ttu-id="222f2-1354">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="222f2-1355">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1355">No</span></span> |
| <span data-ttu-id="222f2-1356">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1356">password</span></span> |<span data-ttu-id="222f2-1357">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-1358">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1358">No</span></span> |
| <span data-ttu-id="222f2-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1359">gatewayName</span></span> |<span data-ttu-id="222f2-1360">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi PostgreSQL veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="222f2-1361">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1362">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1362">Example</span></span>

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
<span data-ttu-id="222f2-1363">Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1364">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1364">Dataset</span></span>
<span data-ttu-id="222f2-1365">toodefine bir PostgreSQL veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1366">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1366">Property</span></span> | <span data-ttu-id="222f2-1367">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1367">Description</span></span> | <span data-ttu-id="222f2-1368">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1369">tableName</span></span> |<span data-ttu-id="222f2-1370">Merhaba bağlı PostgreSQL veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="222f2-1371">Merhaba tableName büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="222f2-1372">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1373">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1373">Example</span></span>
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
<span data-ttu-id="222f2-1374">Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1375">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1376">Bir PostgreSQL veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1377">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1377">Property</span></span> | <span data-ttu-id="222f2-1378">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1378">Description</span></span> | <span data-ttu-id="222f2-1379">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1379">Allowed values</span></span> | <span data-ttu-id="222f2-1380">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1381">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1381">query</span></span> |<span data-ttu-id="222f2-1382">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1383">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1383">SQL query string.</span></span> <span data-ttu-id="222f2-1384">Örneğin: "sorgu": "seçin * gelen \"MySchema\".\" MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="222f2-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="222f2-1385">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1386">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1386">Example</span></span>

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

<span data-ttu-id="222f2-1387">Daha fazla bilgi için bkz: [PostgreSQL bağlayıcı](data-factory-onprem-postgresql-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="222f2-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="222f2-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-1389">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1389">Linked service</span></span>
<span data-ttu-id="222f2-1390">toodefine SAP Business Warehouse (BW) bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**SapBw**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="222f2-1391">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1391">Property</span></span> | <span data-ttu-id="222f2-1392">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1392">Description</span></span> | <span data-ttu-id="222f2-1393">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1393">Allowed values</span></span> | <span data-ttu-id="222f2-1394">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="222f2-1395">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1395">server</span></span> | <span data-ttu-id="222f2-1396">Hangi hello SAP BW örneği bulunduğu hello sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="222f2-1397">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1397">string</span></span> | <span data-ttu-id="222f2-1398">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1398">Yes</span></span>
<span data-ttu-id="222f2-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="222f2-1399">systemNumber</span></span> | <span data-ttu-id="222f2-1400">SAP BW sistem hello sistem sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="222f2-1401">Bir dize olarak gösterilen iki basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="222f2-1402">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1402">Yes</span></span>
<span data-ttu-id="222f2-1403">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="222f2-1403">clientId</span></span> | <span data-ttu-id="222f2-1404">Merhaba SAP W sistem hello istemcisinde istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="222f2-1405">Bir dize olarak gösterilen üç basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="222f2-1406">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1406">Yes</span></span>
<span data-ttu-id="222f2-1407">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1407">username</span></span> | <span data-ttu-id="222f2-1408">Erişim toohello SAP sunucusuna sahip hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="222f2-1409">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1409">string</span></span> | <span data-ttu-id="222f2-1410">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1410">Yes</span></span>
<span data-ttu-id="222f2-1411">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1411">password</span></span> | <span data-ttu-id="222f2-1412">Merhaba kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-1412">Password for hello user.</span></span> | <span data-ttu-id="222f2-1413">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1413">string</span></span> | <span data-ttu-id="222f2-1414">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1414">Yes</span></span>
<span data-ttu-id="222f2-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1415">gatewayName</span></span> | <span data-ttu-id="222f2-1416">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP BW örneğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="222f2-1417">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1417">string</span></span> | <span data-ttu-id="222f2-1418">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1418">Yes</span></span>
<span data-ttu-id="222f2-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-1419">encryptedCredential</span></span> | <span data-ttu-id="222f2-1420">şifrelenmiş hello kimlik dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="222f2-1421">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1421">string</span></span> | <span data-ttu-id="222f2-1422">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-1423">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1423">Example</span></span>

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

<span data-ttu-id="222f2-1424">Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1425">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1425">Dataset</span></span>
<span data-ttu-id="222f2-1426">toodefine bir SAP BW veri kümesi hello **türü** hello kümesinin çok**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="222f2-1427">Merhaba SAP BW veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="222f2-1428">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1428">Example</span></span>

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
<span data-ttu-id="222f2-1429">Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1430">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1431">SAP Business Warehouse veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1432">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1432">Property</span></span> | <span data-ttu-id="222f2-1433">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1433">Description</span></span> | <span data-ttu-id="222f2-1434">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1434">Allowed values</span></span> | <span data-ttu-id="222f2-1435">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1436">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1436">query</span></span> | <span data-ttu-id="222f2-1437">Merhaba MDX Sorgusu tooread veri hello SAP BW örneğinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="222f2-1438">MDX Sorgusu.</span><span class="sxs-lookup"><span data-stu-id="222f2-1438">MDX query.</span></span> | <span data-ttu-id="222f2-1439">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1440">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1440">Example</span></span>

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

<span data-ttu-id="222f2-1441">Daha fazla bilgi için bkz: [SAP Business Warehouse Bağlayıcısı](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="222f2-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="222f2-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1443">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1443">Linked service</span></span>
<span data-ttu-id="222f2-1444">SAP HANA toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**SapHana**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="222f2-1445">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1445">Property</span></span> | <span data-ttu-id="222f2-1446">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1446">Description</span></span> | <span data-ttu-id="222f2-1447">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1447">Allowed values</span></span> | <span data-ttu-id="222f2-1448">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="222f2-1449">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1449">server</span></span> | <span data-ttu-id="222f2-1450">Hangi hello SAP HANA örneği bulunduğu hello sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="222f2-1451">Sunucunuz özelleştirilmiş bir bağlantı noktası kullanıyorsa belirtin `server:port`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="222f2-1452">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1452">string</span></span> | <span data-ttu-id="222f2-1453">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1453">Yes</span></span>
<span data-ttu-id="222f2-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1454">authenticationType</span></span> | <span data-ttu-id="222f2-1455">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-1455">Type of authentication.</span></span> | <span data-ttu-id="222f2-1456">Dize.</span><span class="sxs-lookup"><span data-stu-id="222f2-1456">string.</span></span> <span data-ttu-id="222f2-1457">"Temel" veya "Windows"</span><span class="sxs-lookup"><span data-stu-id="222f2-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="222f2-1458">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1458">Yes</span></span> 
<span data-ttu-id="222f2-1459">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1459">username</span></span> | <span data-ttu-id="222f2-1460">Erişim toohello SAP sunucusuna sahip hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="222f2-1461">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1461">string</span></span> | <span data-ttu-id="222f2-1462">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1462">Yes</span></span>
<span data-ttu-id="222f2-1463">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1463">password</span></span> | <span data-ttu-id="222f2-1464">Merhaba kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-1464">Password for hello user.</span></span> | <span data-ttu-id="222f2-1465">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1465">string</span></span> | <span data-ttu-id="222f2-1466">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1466">Yes</span></span>
<span data-ttu-id="222f2-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1467">gatewayName</span></span> | <span data-ttu-id="222f2-1468">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP HANA örneğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="222f2-1469">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1469">string</span></span> | <span data-ttu-id="222f2-1470">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1470">Yes</span></span>
<span data-ttu-id="222f2-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-1471">encryptedCredential</span></span> | <span data-ttu-id="222f2-1472">şifrelenmiş hello kimlik dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="222f2-1473">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1473">string</span></span> | <span data-ttu-id="222f2-1474">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-1475">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1475">Example</span></span>

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
<span data-ttu-id="222f2-1476">Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="222f2-1477">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1477">Dataset</span></span>
<span data-ttu-id="222f2-1478">toodefine bir SAP HANA veri kümesi hello **türü** hello kümesinin çok**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="222f2-1479">Merhaba SAP HANA dataset türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="222f2-1480">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1480">Example</span></span>

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
<span data-ttu-id="222f2-1481">Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1482">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1483">SAP HANA veri deposundan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1484">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1484">Property</span></span> | <span data-ttu-id="222f2-1485">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1485">Description</span></span> | <span data-ttu-id="222f2-1486">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1486">Allowed values</span></span> | <span data-ttu-id="222f2-1487">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1488">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1488">query</span></span> | <span data-ttu-id="222f2-1489">Merhaba SQL sorgu tooread veri hello SAP HANA örneğinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="222f2-1490">SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="222f2-1490">SQL query.</span></span> | <span data-ttu-id="222f2-1491">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="222f2-1492">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1492">Example</span></span>


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

<span data-ttu-id="222f2-1493">Daha fazla bilgi için bkz: [SAP HANA bağlayıcı](data-factory-sap-hana-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="222f2-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="222f2-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1495">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1495">Linked service</span></span>
<span data-ttu-id="222f2-1496">Bağlı hizmet türü oluşturma **OnPremisesSqlServer** toolink bir şirket içi SQL Server veritabanı tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="222f2-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="222f2-1497">Aşağıdaki tablonun hello JSON öğeleri belirli tooon şirket içi SQL Server bağlantılı hizmet açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="222f2-1498">Aşağıdaki tablonun hello JSON öğeleri belirli tooSQL Server bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="222f2-1499">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1499">Property</span></span> | <span data-ttu-id="222f2-1500">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1500">Description</span></span> | <span data-ttu-id="222f2-1501">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1502">type</span><span class="sxs-lookup"><span data-stu-id="222f2-1502">type</span></span> |<span data-ttu-id="222f2-1503">Merhaba type özelliği ayarlanmalıdır: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="222f2-1504">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1504">Yes</span></span> |
| <span data-ttu-id="222f2-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-1505">connectionString</span></span> |<span data-ttu-id="222f2-1506">SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak tooconnect toohello şirket içi SQL Server veritabanı gerekli connectionString bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="222f2-1507">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1507">Yes</span></span> |
| <span data-ttu-id="222f2-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1508">gatewayName</span></span> |<span data-ttu-id="222f2-1509">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SQL Server veritabanını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="222f2-1510">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1510">Yes</span></span> |
| <span data-ttu-id="222f2-1511">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1511">username</span></span> |<span data-ttu-id="222f2-1512">Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="222f2-1513">Örnek: **domainname\\kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="222f2-1514">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1514">No</span></span> |
| <span data-ttu-id="222f2-1515">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1515">password</span></span> |<span data-ttu-id="222f2-1516">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-1517">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1517">No</span></span> |

<span data-ttu-id="222f2-1518">Hello kullanarak kimlik bilgilerini şifrelemek **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları hello aşağıdaki örnekte gösterildiği gibi hello bağlantı dizesinde kullanabilirsiniz (**EncryptedCredential** özellik):</span><span class="sxs-lookup"><span data-stu-id="222f2-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="222f2-1519">Örnek: SQL kimlik doğrulaması kullanmak için JSON</span><span class="sxs-lookup"><span data-stu-id="222f2-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="222f2-1520">Örnek: JSON'ı Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="222f2-1521">Kullanıcı adı ve parolası belirtilmişse, ağ geçidi bunları tooimpersonate hello kullanır belirtilen kullanıcı hesabı tooconnect toohello şirket içi SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="222f2-1522">Aksi takdirde, ağ geçidi toohello SQL Server doğrudan hello güvenlik bağlamında ağ geçidi (kendi başlangıç hesabı) ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="222f2-1523">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1524">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1524">Dataset</span></span>
<span data-ttu-id="222f2-1525">toodefine bir SQL Server veri kümesi hello **türü** hello kümesinin çok**SqlServerTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1526">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1526">Property</span></span> | <span data-ttu-id="222f2-1527">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1527">Description</span></span> | <span data-ttu-id="222f2-1528">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1529">tableName</span></span> |<span data-ttu-id="222f2-1530">Merhaba tablo veya Görünüm hizmeti bağlı hello SQL Server veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="222f2-1531">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1532">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1532">Example</span></span>
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

<span data-ttu-id="222f2-1533">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="222f2-1534">Kopyalama etkinliğinde SQL kaynağı</span><span class="sxs-lookup"><span data-stu-id="222f2-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1535">Bir SQL Server veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**SqlSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1536">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1536">Property</span></span> | <span data-ttu-id="222f2-1537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1537">Description</span></span> | <span data-ttu-id="222f2-1538">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1538">Allowed values</span></span> | <span data-ttu-id="222f2-1539">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1540">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="222f2-1540">sqlReaderQuery</span></span> |<span data-ttu-id="222f2-1541">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1542">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1542">SQL query string.</span></span> <span data-ttu-id="222f2-1543">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="222f2-1544">Birden çok tablo hello girdi veri kümesi tarafından başvurulan hello veritabanından başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="222f2-1545">Belirtilmezse, yürütülen SQL deyimini hello: MyTable arasından seçin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="222f2-1546">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1546">No</span></span> |
| <span data-ttu-id="222f2-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="222f2-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="222f2-1548">Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="222f2-1549">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="222f2-1550">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1550">No</span></span> |
| <span data-ttu-id="222f2-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-1551">storedProcedureParameters</span></span> |<span data-ttu-id="222f2-1552">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="222f2-1553">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1553">Name/value pairs.</span></span> <span data-ttu-id="222f2-1554">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="222f2-1555">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1555">No</span></span> |

<span data-ttu-id="222f2-1556">Merhaba, **sqlReaderQuery** Merhaba SqlSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello SQL Server veritabanı kaynak tooget hello verileri karşı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="222f2-1557">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="222f2-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="222f2-1558">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="222f2-1559">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="222f2-1560">Kullandığınızda, **sqlReaderStoredProcedureName**, hala toospecify bir değer hello için gereksinim duyduğunuz **tableName** JSON hello kümesindeki özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="222f2-1561">Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="222f2-1562">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1562">Example</span></span>
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

<span data-ttu-id="222f2-1563">Bu örnekte, **sqlReaderQuery** SqlSource hello için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="222f2-1564">Merhaba kopyalama etkinliği bu sorguyu SQL Server veritabanı kaynak tooget hello verileri hello karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="222f2-1565">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="222f2-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="222f2-1566">Merhaba sqlReaderQuery hello girdi veri kümesi tarafından başvurulan hello veritabanı içinde birden çok tablo başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="222f2-1567">Bu veri kümesi'nin tableName typeProperty hello olarak ayarlanmış sınırlı tooonly hello tablosu değil.</span><span class="sxs-lookup"><span data-stu-id="222f2-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="222f2-1568">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="222f2-1569">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="222f2-1570">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="222f2-1571">Kopyalama etkinliği SQL havuzunda</span><span class="sxs-lookup"><span data-stu-id="222f2-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-1572">Veri tooa SQL Server veritabanı kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**SqlSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-1573">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1573">Property</span></span> | <span data-ttu-id="222f2-1574">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1574">Description</span></span> | <span data-ttu-id="222f2-1575">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1575">Allowed values</span></span> | <span data-ttu-id="222f2-1576">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-1577">writeBatchTimeout</span></span> |<span data-ttu-id="222f2-1578">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="222f2-1579">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="222f2-1579">timespan</span></span><br/><br/> <span data-ttu-id="222f2-1580">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="222f2-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="222f2-1581">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1581">No</span></span> |
| <span data-ttu-id="222f2-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="222f2-1582">writeBatchSize</span></span> |<span data-ttu-id="222f2-1583">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="222f2-1584">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="222f2-1584">Integer (number of rows)</span></span> |<span data-ttu-id="222f2-1585">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="222f2-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="222f2-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="222f2-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="222f2-1587">Belirli bir dilimle verilerinin temizlenmesini gibi kopyalama etkinliği tooexecute için sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="222f2-1588">Daha fazla bilgi için bkz: [Yinelenebilirlik](#repeatability-during-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="222f2-1589">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1589">A query statement.</span></span> |<span data-ttu-id="222f2-1590">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1590">No</span></span> |
| <span data-ttu-id="222f2-1591">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="222f2-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="222f2-1592">Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="222f2-1593">Daha fazla bilgi için bkz: [Yinelenebilirlik](#repeatability-during-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="222f2-1594">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="222f2-1595">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1595">No</span></span> |
| <span data-ttu-id="222f2-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="222f2-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="222f2-1597">Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="222f2-1598">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="222f2-1599">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1599">No</span></span> |
| <span data-ttu-id="222f2-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-1600">storedProcedureParameters</span></span> |<span data-ttu-id="222f2-1601">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="222f2-1602">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1602">Name/value pairs.</span></span> <span data-ttu-id="222f2-1603">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="222f2-1604">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1604">No</span></span> |
| <span data-ttu-id="222f2-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="222f2-1605">sqlWriterTableType</span></span> |<span data-ttu-id="222f2-1606">Merhaba saklı yordamda kullanılan tablo türü adı toobe belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="222f2-1607">Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="222f2-1608">Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="222f2-1609">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1609">A table type name.</span></span> |<span data-ttu-id="222f2-1610">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1611">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1611">Example</span></span>
<span data-ttu-id="222f2-1612">Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="222f2-1613">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="222f2-1614">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="222f2-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="222f2-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1616">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1616">Linked service</span></span>
<span data-ttu-id="222f2-1617">bir Sybase toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesSybase**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1618">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1618">Property</span></span> | <span data-ttu-id="222f2-1619">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1619">Description</span></span> | <span data-ttu-id="222f2-1620">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1621">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1621">server</span></span> |<span data-ttu-id="222f2-1622">Merhaba Sybase sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="222f2-1623">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1623">Yes</span></span> |
| <span data-ttu-id="222f2-1624">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="222f2-1624">database</span></span> |<span data-ttu-id="222f2-1625">Merhaba Sybase veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="222f2-1626">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1626">Yes</span></span> |
| <span data-ttu-id="222f2-1627">Şema</span><span class="sxs-lookup"><span data-stu-id="222f2-1627">schema</span></span> |<span data-ttu-id="222f2-1628">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="222f2-1629">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1629">No</span></span> |
| <span data-ttu-id="222f2-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1630">authenticationType</span></span> |<span data-ttu-id="222f2-1631">Kimlik doğrulama türü tooconnect toohello Sybase veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="222f2-1632">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="222f2-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="222f2-1633">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1633">Yes</span></span> |
| <span data-ttu-id="222f2-1634">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1634">username</span></span> |<span data-ttu-id="222f2-1635">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="222f2-1636">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1636">No</span></span> |
| <span data-ttu-id="222f2-1637">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1637">password</span></span> |<span data-ttu-id="222f2-1638">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-1639">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1639">No</span></span> |
| <span data-ttu-id="222f2-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1640">gatewayName</span></span> |<span data-ttu-id="222f2-1641">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi Sybase veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="222f2-1642">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1643">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1643">Example</span></span>
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

<span data-ttu-id="222f2-1644">Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1645">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1645">Dataset</span></span>
<span data-ttu-id="222f2-1646">toodefine bir Sybase veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1647">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1647">Property</span></span> | <span data-ttu-id="222f2-1648">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1648">Description</span></span> | <span data-ttu-id="222f2-1649">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1650">tableName</span></span> |<span data-ttu-id="222f2-1651">Merhaba bağlı Sybase veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="222f2-1652">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1653">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1653">Example</span></span>

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

<span data-ttu-id="222f2-1654">Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1655">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1656">Bir Sybase veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1657">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1657">Property</span></span> | <span data-ttu-id="222f2-1658">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1658">Description</span></span> | <span data-ttu-id="222f2-1659">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1659">Allowed values</span></span> | <span data-ttu-id="222f2-1660">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1661">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1661">query</span></span> |<span data-ttu-id="222f2-1662">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1663">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1663">SQL query string.</span></span> <span data-ttu-id="222f2-1664">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-1665">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1666">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1666">Example</span></span>

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

<span data-ttu-id="222f2-1667">Daha fazla bilgi için bkz: [Sybase bağlayıcı](data-factory-onprem-sybase-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="222f2-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="222f2-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1669">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1669">Linked service</span></span>
<span data-ttu-id="222f2-1670">bir Teradata toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesTeradata**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1671">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1671">Property</span></span> | <span data-ttu-id="222f2-1672">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1672">Description</span></span> | <span data-ttu-id="222f2-1673">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1674">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1674">server</span></span> |<span data-ttu-id="222f2-1675">Merhaba Teradata sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="222f2-1676">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1676">Yes</span></span> |
| <span data-ttu-id="222f2-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1677">authenticationType</span></span> |<span data-ttu-id="222f2-1678">Kimlik doğrulama türü tooconnect toohello Teradata veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="222f2-1679">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="222f2-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="222f2-1680">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1680">Yes</span></span> |
| <span data-ttu-id="222f2-1681">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1681">username</span></span> |<span data-ttu-id="222f2-1682">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="222f2-1683">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1683">No</span></span> |
| <span data-ttu-id="222f2-1684">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1684">password</span></span> |<span data-ttu-id="222f2-1685">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-1686">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1686">No</span></span> |
| <span data-ttu-id="222f2-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1687">gatewayName</span></span> |<span data-ttu-id="222f2-1688">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi Teradata veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="222f2-1689">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1690">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1690">Example</span></span>
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

<span data-ttu-id="222f2-1691">Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1692">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1692">Dataset</span></span>
<span data-ttu-id="222f2-1693">toodefine bir Teradata Blob veri kümesi hello **türü** hello kümesinin çok**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="222f2-1694">Şu anda hello Teradata veri kümesi için desteklenen tür özellik yok.</span><span class="sxs-lookup"><span data-stu-id="222f2-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="222f2-1695">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1695">Example</span></span>
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

<span data-ttu-id="222f2-1696">Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-1697">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1698">Bir Teradata veritabanından veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1699">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1699">Property</span></span> | <span data-ttu-id="222f2-1700">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1700">Description</span></span> | <span data-ttu-id="222f2-1701">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1701">Allowed values</span></span> | <span data-ttu-id="222f2-1702">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1703">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1703">query</span></span> |<span data-ttu-id="222f2-1704">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1705">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1705">SQL query string.</span></span> <span data-ttu-id="222f2-1706">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-1707">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1708">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1708">Example</span></span>

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

<span data-ttu-id="222f2-1709">Daha fazla bilgi için bkz: [Teradata bağlayıcı](data-factory-onprem-teradata-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="222f2-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="222f2-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-1711">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1711">Linked service</span></span>
<span data-ttu-id="222f2-1712">toodefine bir Cassandra bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesCassandra**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1713">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1713">Property</span></span> | <span data-ttu-id="222f2-1714">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1714">Description</span></span> | <span data-ttu-id="222f2-1715">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1716">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="222f2-1716">host</span></span> |<span data-ttu-id="222f2-1717">Bir veya daha fazla IP adresleri veya ana bilgisayar adlarını Cassandra sunucuları.</span><span class="sxs-lookup"><span data-stu-id="222f2-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="222f2-1718">IP adresi veya ana bilgisayar adları tooconnect tooall sunucuları virgülle ayrılmış listesini eşzamanlı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="222f2-1719">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1719">Yes</span></span> |
| <span data-ttu-id="222f2-1720">port</span><span class="sxs-lookup"><span data-stu-id="222f2-1720">port</span></span> |<span data-ttu-id="222f2-1721">Merhaba Cassandra sunucu hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="222f2-1722">Hayır, varsayılan değer: 9042</span><span class="sxs-lookup"><span data-stu-id="222f2-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="222f2-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1723">authenticationType</span></span> |<span data-ttu-id="222f2-1724">Basic veya Anonymous</span><span class="sxs-lookup"><span data-stu-id="222f2-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="222f2-1725">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1725">Yes</span></span> |
| <span data-ttu-id="222f2-1726">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1726">username</span></span> |<span data-ttu-id="222f2-1727">Merhaba kullanıcı hesabının kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="222f2-1728">Evet, authenticationType tooBasic ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="222f2-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="222f2-1729">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1729">password</span></span> |<span data-ttu-id="222f2-1730">Merhaba kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="222f2-1731">Evet, authenticationType tooBasic ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="222f2-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="222f2-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1732">gatewayName</span></span> |<span data-ttu-id="222f2-1733">kullanılan tooconnect toohello şirket içi Cassandra veritabanı hello ağ geçidi Hello adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="222f2-1734">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1734">Yes</span></span> |
| <span data-ttu-id="222f2-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-1735">encryptedCredential</span></span> |<span data-ttu-id="222f2-1736">Merhaba ağ geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="222f2-1737">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1738">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1738">Example</span></span>

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

<span data-ttu-id="222f2-1739">Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-1740">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1740">Dataset</span></span>
<span data-ttu-id="222f2-1741">toodefine bir Cassandra veri kümesi hello **türü** hello kümesinin çok**CassandraTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1742">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1742">Property</span></span> | <span data-ttu-id="222f2-1743">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1743">Description</span></span> | <span data-ttu-id="222f2-1744">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="222f2-1745">keyspace</span></span> |<span data-ttu-id="222f2-1746">Merhaba keyspace veya Cassandra veritabanındaki şema adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="222f2-1747">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="222f2-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="222f2-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-1748">tableName</span></span> |<span data-ttu-id="222f2-1749">Cassandra veritabanındaki Merhaba tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="222f2-1750">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="222f2-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1751">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1751">Example</span></span>

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

<span data-ttu-id="222f2-1752">Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="222f2-1753">Kopyalama etkinliği Cassandra kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1754">Cassandra veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**CassandraSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü :</span><span class="sxs-lookup"><span data-stu-id="222f2-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1755">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1755">Property</span></span> | <span data-ttu-id="222f2-1756">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1756">Description</span></span> | <span data-ttu-id="222f2-1757">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1757">Allowed values</span></span> | <span data-ttu-id="222f2-1758">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1759">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1759">query</span></span> |<span data-ttu-id="222f2-1760">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1761">SQL-92 sorgusu veya CQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="222f2-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="222f2-1762">Bkz: [CQL başvuru](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="222f2-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="222f2-1763">SQL sorgusu kullanırken belirtin **keyspace name.table adı** tooquery istediğiniz toorepresent hello tablo.</span><span class="sxs-lookup"><span data-stu-id="222f2-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="222f2-1764">Hayır (tableName ve veri kümesi üzerinde keyspace tanımlanmışsa).</span><span class="sxs-lookup"><span data-stu-id="222f2-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="222f2-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="222f2-1765">consistencyLevel</span></span> |<span data-ttu-id="222f2-1766">kaç tane çoğaltmaları veri toohello istemci uygulaması döndürmeden önce tooa Okuma isteği yanıtlamalısınız Hello tutarlılık düzeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="222f2-1767">İstek veri toosatisfy hello okumak için Cassandra denetimleri çoğaltmaları belirtilen sayıda hello.</span><span class="sxs-lookup"><span data-stu-id="222f2-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="222f2-1768">BİR, İKİ, ÜÇ, ÇEKİRDEK, TÜMÜ, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="222f2-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="222f2-1769">Bkz: [veri tutarlılığını yapılandırma](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="222f2-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="222f2-1770">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1770">No.</span></span> <span data-ttu-id="222f2-1771">Varsayılan değer biridir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1772">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="222f2-1773">Daha fazla bilgi için bkz: [Cassandra bağlayıcı](data-factory-onprem-cassandra-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="222f2-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="222f2-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-1775">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1775">Linked service</span></span>
<span data-ttu-id="222f2-1776">toodefine bir MongoDB bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesMongoDB**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1777">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1777">Property</span></span> | <span data-ttu-id="222f2-1778">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1778">Description</span></span> | <span data-ttu-id="222f2-1779">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1780">sunucu</span><span class="sxs-lookup"><span data-stu-id="222f2-1780">server</span></span> |<span data-ttu-id="222f2-1781">IP adresi veya ana bilgisayar hello MongoDB sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="222f2-1782">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1782">Yes</span></span> |
| <span data-ttu-id="222f2-1783">port</span><span class="sxs-lookup"><span data-stu-id="222f2-1783">port</span></span> |<span data-ttu-id="222f2-1784">MongoDB sunucusuna hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="222f2-1785">İsteğe bağlı, varsayılan değer: 27017</span><span class="sxs-lookup"><span data-stu-id="222f2-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="222f2-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-1786">authenticationType</span></span> |<span data-ttu-id="222f2-1787">Basic veya Anonymous.</span><span class="sxs-lookup"><span data-stu-id="222f2-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="222f2-1788">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1788">Yes</span></span> |
| <span data-ttu-id="222f2-1789">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-1789">username</span></span> |<span data-ttu-id="222f2-1790">Kullanıcı hesabı tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="222f2-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="222f2-1791">Evet (Temel kimlik doğrulaması kullanılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="222f2-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="222f2-1792">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1792">password</span></span> |<span data-ttu-id="222f2-1793">Merhaba kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-1793">Password for hello user.</span></span> |<span data-ttu-id="222f2-1794">Evet (Temel kimlik doğrulaması kullanılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="222f2-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="222f2-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="222f2-1795">authSource</span></span> |<span data-ttu-id="222f2-1796">Kimlik doğrulaması için kimlik bilgilerinizi toouse toocheck istediğiniz hello MongoDB veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="222f2-1797">(Temel kimlik doğrulaması kullanılıyorsa) isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="222f2-1798">Varsayılan: Merhaba yönetici hesabı ve databaseName özelliği kullanılarak belirtilen hello veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="222f2-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="222f2-1799">databaseName</span></span> |<span data-ttu-id="222f2-1800">Tooaccess istediğiniz hello MongoDB veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="222f2-1801">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1801">Yes</span></span> |
| <span data-ttu-id="222f2-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1802">gatewayName</span></span> |<span data-ttu-id="222f2-1803">Merhaba veri deposu erişen hello ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="222f2-1804">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1804">Yes</span></span> |
| <span data-ttu-id="222f2-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-1805">encryptedCredential</span></span> |<span data-ttu-id="222f2-1806">Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="222f2-1807">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="222f2-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1808">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="222f2-1809">Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="222f2-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1810">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1810">Dataset</span></span>
<span data-ttu-id="222f2-1811">toodefine bir MongoDB veri kümesi hello **türü** hello kümesinin çok**MongoDbCollection**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1812">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1812">Property</span></span> | <span data-ttu-id="222f2-1813">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1813">Description</span></span> | <span data-ttu-id="222f2-1814">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="222f2-1815">collectionName</span></span> |<span data-ttu-id="222f2-1816">MongoDB veritabanı hello koleksiyonunda adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="222f2-1817">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1818">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1818">Example</span></span>

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

<span data-ttu-id="222f2-1819">Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="222f2-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="222f2-1820">Kopyalama etkinliği MongoDB kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1821">Veri adresinden kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**MongoDbSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1822">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1822">Property</span></span> | <span data-ttu-id="222f2-1823">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1823">Description</span></span> | <span data-ttu-id="222f2-1824">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1824">Allowed values</span></span> | <span data-ttu-id="222f2-1825">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1826">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-1826">query</span></span> |<span data-ttu-id="222f2-1827">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-1828">SQL-92 sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1828">SQL-92 query string.</span></span> <span data-ttu-id="222f2-1829">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-1830">Hayır (varsa **collectionName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1831">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1831">Example</span></span>

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

<span data-ttu-id="222f2-1832">Daha fazla bilgi için bkz: [MongoDB bağlayıcı makale](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="222f2-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="222f2-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="222f2-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-1834">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1834">Linked service</span></span>
<span data-ttu-id="222f2-1835">toodefine bir Amazon S3 bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AwsAccessKey**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü :</span><span class="sxs-lookup"><span data-stu-id="222f2-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-1836">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1836">Property</span></span> | <span data-ttu-id="222f2-1837">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1837">Description</span></span> | <span data-ttu-id="222f2-1838">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1838">Allowed values</span></span> | <span data-ttu-id="222f2-1839">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="222f2-1840">accessKeyID</span></span> |<span data-ttu-id="222f2-1841">Merhaba gizli erişim anahtarı kimliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="222f2-1842">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1842">string</span></span> |<span data-ttu-id="222f2-1843">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1843">Yes</span></span> |
| <span data-ttu-id="222f2-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="222f2-1844">secretAccessKey</span></span> |<span data-ttu-id="222f2-1845">Merhaba gizli erişim anahtarı kendisi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1845">hello secret access key itself.</span></span> |<span data-ttu-id="222f2-1846">Şifrelenmiş gizli dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1846">Encrypted secret string</span></span> |<span data-ttu-id="222f2-1847">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-1848">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1848">Example</span></span>
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

<span data-ttu-id="222f2-1849">Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1850">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1850">Dataset</span></span>
<span data-ttu-id="222f2-1851">toodefine bir Amazon S3 dataset, kümesi hello **türü** hello kümesinin çok**AmazonS3**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1852">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1852">Property</span></span> | <span data-ttu-id="222f2-1853">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1853">Description</span></span> | <span data-ttu-id="222f2-1854">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1854">Allowed values</span></span> | <span data-ttu-id="222f2-1855">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="222f2-1856">bucketName</span></span> |<span data-ttu-id="222f2-1857">Merhaba S3 demetini adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="222f2-1858">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1858">String</span></span> |<span data-ttu-id="222f2-1859">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1859">Yes</span></span> |
| <span data-ttu-id="222f2-1860">anahtar</span><span class="sxs-lookup"><span data-stu-id="222f2-1860">key</span></span> |<span data-ttu-id="222f2-1861">Merhaba S3 nesne anahtarı.</span><span class="sxs-lookup"><span data-stu-id="222f2-1861">hello S3 object key.</span></span> |<span data-ttu-id="222f2-1862">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1862">String</span></span> |<span data-ttu-id="222f2-1863">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1863">No</span></span> |
| <span data-ttu-id="222f2-1864">önek</span><span class="sxs-lookup"><span data-stu-id="222f2-1864">prefix</span></span> |<span data-ttu-id="222f2-1865">Merhaba S3 nesne anahtarı için önek.</span><span class="sxs-lookup"><span data-stu-id="222f2-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="222f2-1866">Seçilen nesneler, anahtarları Bu önek ile başlatın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="222f2-1867">Yalnızca anahtar boş olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="222f2-1868">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1868">String</span></span> |<span data-ttu-id="222f2-1869">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1869">No</span></span> |
| <span data-ttu-id="222f2-1870">Sürüm</span><span class="sxs-lookup"><span data-stu-id="222f2-1870">version</span></span> |<span data-ttu-id="222f2-1871">S3 sürüm etkinleştirilirse S3 nesne Hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="222f2-1872">Dize</span><span class="sxs-lookup"><span data-stu-id="222f2-1872">String</span></span> |<span data-ttu-id="222f2-1873">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1873">No</span></span> |
| <span data-ttu-id="222f2-1874">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-1874">format</span></span> | <span data-ttu-id="222f2-1875">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-1876">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-1877">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-1878">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-1879">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1879">No</span></span> | |
| <span data-ttu-id="222f2-1880">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-1880">compression</span></span> | <span data-ttu-id="222f2-1881">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-1882">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="222f2-1883">desteklenen hello düzeyleri şunlardır: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-1884">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-1885">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="222f2-1886">bucketName + anahtarı burada demet hello S3 nesneleri için kök kapsayıcı ve anahtar hello tam yol tooS3 nesnesini hello S3 nesnesinin hello konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="222f2-1887">Örnek: Örnek veri kümesi önekiyle</span><span class="sxs-lookup"><span data-stu-id="222f2-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="222f2-1888">Örnek: Örnek veri kümesiyle (sürüm)</span><span class="sxs-lookup"><span data-stu-id="222f2-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="222f2-1889">Örnek: S3 dinamik yollar</span><span class="sxs-lookup"><span data-stu-id="222f2-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="222f2-1890">Merhaba örnek hello Amazon S3 dataset içindeki anahtar ve bucketName özellikler için sabit değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="222f2-1891">Veri Fabrikası hello anahtar ve çalışma zamanında dinamik olarak bucketName SliceStart gibi sistem değişkenleri kullanarak hesaplar olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="222f2-1892">Yapabileceğiniz aynı hello önek özelliği bir Amazon S3 dataset için hello.</span><span class="sxs-lookup"><span data-stu-id="222f2-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="222f2-1893">Bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md) desteklenen işlevleri ve değişkenler listesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="222f2-1894">Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="222f2-1895">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1896">Verileri Amazon S3'ten kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü :</span><span class="sxs-lookup"><span data-stu-id="222f2-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="222f2-1897">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1897">Property</span></span> | <span data-ttu-id="222f2-1898">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1898">Description</span></span> | <span data-ttu-id="222f2-1899">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1899">Allowed values</span></span> | <span data-ttu-id="222f2-1900">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1901">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-1901">recursive</span></span> |<span data-ttu-id="222f2-1902">Toorecursively listesi S3 hello dizini altında nesneleri olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="222f2-1903">true/false</span><span class="sxs-lookup"><span data-stu-id="222f2-1903">true/false</span></span> |<span data-ttu-id="222f2-1904">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="222f2-1905">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1905">Example</span></span>


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

<span data-ttu-id="222f2-1906">Daha fazla bilgi için bkz: [Amazon S3 bağlayıcı makale](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="222f2-1907">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="222f2-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-1908">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-1908">Linked service</span></span>
<span data-ttu-id="222f2-1909">Bir şirket içi dosya sistemi tooan Azure data factory hello ile bağlayabilirsiniz **şirket içi dosya sunucusu** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="222f2-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="222f2-1910">Aşağıdaki tablonun hello belirli toohello şirket içi dosya sunucusuna bağlı hizmeti olan JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="222f2-1911">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1911">Property</span></span> | <span data-ttu-id="222f2-1912">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1912">Description</span></span> | <span data-ttu-id="222f2-1913">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1914">type</span><span class="sxs-lookup"><span data-stu-id="222f2-1914">type</span></span> |<span data-ttu-id="222f2-1915">Merhaba type özelliği çok ayarlandığından emin olun**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="222f2-1916">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1916">Yes</span></span> |
| <span data-ttu-id="222f2-1917">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="222f2-1917">host</span></span> |<span data-ttu-id="222f2-1918">Toocopy istediğiniz hello klasörü Hello kök yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="222f2-1919">Merhaba kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="222f2-1920">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="222f2-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="222f2-1921">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1921">Yes</span></span> |
| <span data-ttu-id="222f2-1922">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="222f2-1922">userid</span></span> |<span data-ttu-id="222f2-1923">Merhaba erişim toohello sunucusuna sahip hello kullanıcı Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="222f2-1924">Hayır (encryptedCredential seçerseniz)</span><span class="sxs-lookup"><span data-stu-id="222f2-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="222f2-1925">password</span><span class="sxs-lookup"><span data-stu-id="222f2-1925">password</span></span> |<span data-ttu-id="222f2-1926">Merhaba kullanıcı (UserID) Hello parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="222f2-1927">Hayır (encryptedCredential seçerseniz</span><span class="sxs-lookup"><span data-stu-id="222f2-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="222f2-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-1928">encryptedCredential</span></span> |<span data-ttu-id="222f2-1929">Merhaba yeni AzureRmDataFactoryEncryptValue cmdlet'ini çalıştırarak alabilirsiniz hello şifreli kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="222f2-1930">Hayır (toospecify kullanıcı kimliği ve parola düz metin olarak seçerseniz)</span><span class="sxs-lookup"><span data-stu-id="222f2-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="222f2-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-1931">gatewayName</span></span> |<span data-ttu-id="222f2-1932">Veri Fabrikası tooconnect toohello şirket içi dosya sunucusu kullanmalısınız hello ağ geçidi Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="222f2-1933">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="222f2-1934">Örnek klasör yolu tanımları</span><span class="sxs-lookup"><span data-stu-id="222f2-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="222f2-1935">Senaryo</span><span class="sxs-lookup"><span data-stu-id="222f2-1935">Scenario</span></span> | <span data-ttu-id="222f2-1936">Bağlantılı hizmet tanımında ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="222f2-1936">Host in linked service definition</span></span> | <span data-ttu-id="222f2-1937">veri kümesi tanımında folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1938">Veri Yönetimi ağ geçidi makine üzerinde yerel klasör:</span><span class="sxs-lookup"><span data-stu-id="222f2-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="222f2-1939">Örnekler: D:\\ \* veya D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="222f2-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="222f2-1940">D:\\ \\ (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler)</span><span class="sxs-lookup"><span data-stu-id="222f2-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="222f2-1941">localhost (daha önceki sürümler için veri yönetimi ağ geçidi 2. 0)</span><span class="sxs-lookup"><span data-stu-id="222f2-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="222f2-1942">. \\ \\ veya klasör\\\\alt klasör (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler)</span><span class="sxs-lookup"><span data-stu-id="222f2-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="222f2-1943">D:\\ \\ veya D:\\\\klasörü\\\\alt klasör (için ağ geçidi sürüm 2.0 altında)</span><span class="sxs-lookup"><span data-stu-id="222f2-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="222f2-1944">Uzak paylaşılan klasör:</span><span class="sxs-lookup"><span data-stu-id="222f2-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="222f2-1945">Örnekler: \\ \\myserver\\paylaşmak\\ \* veya \\ \\myserver\\paylaşmak\\klasörü\\alt klasör\\*</span><span class="sxs-lookup"><span data-stu-id="222f2-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="222f2-1946">\\\\\\\\myserver\\\\paylaşma</span><span class="sxs-lookup"><span data-stu-id="222f2-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="222f2-1947">. \\ \\ veya klasör\\\\alt klasör</span><span class="sxs-lookup"><span data-stu-id="222f2-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="222f2-1948">Örnek: kullanıcı adı ve parola düz metin olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="222f2-1949">Örnek: encryptedcredential kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="222f2-1950">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-1951">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-1951">Dataset</span></span>
<span data-ttu-id="222f2-1952">toodefine bir dosya sistemi veri kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-1953">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1953">Property</span></span> | <span data-ttu-id="222f2-1954">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1954">Description</span></span> | <span data-ttu-id="222f2-1955">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-1956">folderPath</span></span> |<span data-ttu-id="222f2-1957">Merhaba alt toohello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="222f2-1958">Merhaba kaçış karakteri kullanmak ' \' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="222f2-1959">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="222f2-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="222f2-1960">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="222f2-1961">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-1961">Yes</span></span> |
| <span data-ttu-id="222f2-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="222f2-1962">fileName</span></span> |<span data-ttu-id="222f2-1963">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="222f2-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="222f2-1964">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="222f2-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="222f2-1965">Dosya adı bir çıkış veri kümesi için belirtilmediğinde hello oluşturulan hello dosya biçimini izleyen hello adıdır:</span><span class="sxs-lookup"><span data-stu-id="222f2-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="222f2-1966">`Data.<Guid>.txt`(Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="222f2-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="222f2-1967">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1967">No</span></span> |
| <span data-ttu-id="222f2-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="222f2-1968">fileFilter</span></span> |<span data-ttu-id="222f2-1969">Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="222f2-1970">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="222f2-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="222f2-1971">Örnek 1: "fileFilter": "* .log"</span><span class="sxs-lookup"><span data-stu-id="222f2-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="222f2-1972">Örnek 2: "fileFilter": 2016 - 1-? txt"</span><span class="sxs-lookup"><span data-stu-id="222f2-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="222f2-1973">Bu fileFilter bir giriş FileShare veri kümesi için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="222f2-1974">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1974">No</span></span> |
| <span data-ttu-id="222f2-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="222f2-1975">partitionedBy</span></span> |<span data-ttu-id="222f2-1976">Zaman serisi veri partitionedBy toospecify dinamik folderPath/fileName kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="222f2-1977">İçin verileri saatte parametreli folderPath örneğidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="222f2-1978">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1978">No</span></span> |
| <span data-ttu-id="222f2-1979">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-1979">format</span></span> | <span data-ttu-id="222f2-1980">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-1981">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-1982">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-1983">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-1984">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1984">No</span></span> |
| <span data-ttu-id="222f2-1985">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-1985">compression</span></span> | <span data-ttu-id="222f2-1986">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-1987">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**; ve desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-1988">bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-1989">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="222f2-1990">Dosya adı ve fileFilter aynı anda kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="222f2-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-1991">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-1991">Example</span></span>

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

<span data-ttu-id="222f2-1992">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="222f2-1993">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="222f2-1994">Dosya sisteminden veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-1995">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-1995">Property</span></span> | <span data-ttu-id="222f2-1996">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-1996">Description</span></span> | <span data-ttu-id="222f2-1997">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-1997">Allowed values</span></span> | <span data-ttu-id="222f2-1998">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-1999">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-1999">recursive</span></span> |<span data-ttu-id="222f2-2000">Merhaba klasörlerdeki veya yalnızca klasörden hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="222f2-2001">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-2001">True, False (default)</span></span> |<span data-ttu-id="222f2-2002">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2003">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2003">Example</span></span>

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
<span data-ttu-id="222f2-2004">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="222f2-2005">Dosya sistemi havuzu kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="222f2-2006">Veri tooFile sistem kopyalıyorsanız hello ayarlamak **Havuz türü** Merhaba kopya etkinliği çok**FileSystemSink**ve hello özelliklerinde aşağıdaki belirtin **havuz** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="222f2-2007">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2007">Property</span></span> | <span data-ttu-id="222f2-2008">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2008">Description</span></span> | <span data-ttu-id="222f2-2009">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-2009">Allowed values</span></span> | <span data-ttu-id="222f2-2010">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="222f2-2011">copyBehavior</span></span> |<span data-ttu-id="222f2-2012">Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="222f2-2013">**PreserveHierarchy:** hello dosya hiyerarşisi hello hedef klasörde korur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="222f2-2014">Diğer bir deyişle, hello kaynak dosya toohello kaynak klasörün hello göreli yol olduğundan hello hello hedef dosya toohello hedef klasörü hello göreli yolu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="222f2-2015">**FlattenHierarchy:** hello kaynak klasördeki tüm dosyaları hedef klasörün hello ilk düzeyi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="222f2-2016">Merhaba hedef dosyaları otomatik olarak oluşturulur adıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="222f2-2017">**MergeFiles:** hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="222f2-2018">Merhaba dosya adı/blob adı belirtilirse, hello belirtilen ad hello birleştirilmiş dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="222f2-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="222f2-2019">Aksi halde, bir otomatik olarak oluşturulan dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="222f2-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="222f2-2020">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2020">No</span></span> |
<span data-ttu-id="222f2-2021">otomatik-</span><span class="sxs-lookup"><span data-stu-id="222f2-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-2022">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2022">Example</span></span>

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

<span data-ttu-id="222f2-2023">Daha fazla bilgi için bkz: [dosya sistemi bağlayıcı makale](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="222f2-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="222f2-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="222f2-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-2025">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2025">Linked service</span></span>
<span data-ttu-id="222f2-2026">toodefine FTP bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Ftp_sunucusu**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2027">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2027">Property</span></span> | <span data-ttu-id="222f2-2028">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2028">Description</span></span> | <span data-ttu-id="222f2-2029">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2029">Required</span></span> | <span data-ttu-id="222f2-2030">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="222f2-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2031">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="222f2-2031">host</span></span> |<span data-ttu-id="222f2-2032">Hello FTP sunucusu adı veya IP adresi</span><span class="sxs-lookup"><span data-stu-id="222f2-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="222f2-2033">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="222f2-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2034">authenticationType</span></span> |<span data-ttu-id="222f2-2035">Kimlik doğrulama türünü belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2035">Specify authentication type</span></span> |<span data-ttu-id="222f2-2036">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2036">Yes</span></span> |<span data-ttu-id="222f2-2037">Temel, anonim</span><span class="sxs-lookup"><span data-stu-id="222f2-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="222f2-2038">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2038">username</span></span> |<span data-ttu-id="222f2-2039">Erişim toohello FTP sunucusu olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="222f2-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="222f2-2040">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="222f2-2041">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2041">password</span></span> |<span data-ttu-id="222f2-2042">Parola hello kullanıcının (kullanıcı adı)</span><span class="sxs-lookup"><span data-stu-id="222f2-2042">Password for hello user (username)</span></span> |<span data-ttu-id="222f2-2043">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="222f2-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-2044">encryptedCredential</span></span> |<span data-ttu-id="222f2-2045">Şifrelenmiş kimlik bilgileri tooaccess hello FTP sunucusu</span><span class="sxs-lookup"><span data-stu-id="222f2-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="222f2-2046">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="222f2-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2047">gatewayName</span></span> |<span data-ttu-id="222f2-2048">Merhaba veri yönetimi ağ geçidi ağ geçidi tooconnect tooan adını içi FTP sunucusu</span><span class="sxs-lookup"><span data-stu-id="222f2-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="222f2-2049">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="222f2-2050">port</span><span class="sxs-lookup"><span data-stu-id="222f2-2050">port</span></span> |<span data-ttu-id="222f2-2051">Hangi hello FTP sunucusunun dinleme yaptığı bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="222f2-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="222f2-2052">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2052">No</span></span> |<span data-ttu-id="222f2-2053">21</span><span class="sxs-lookup"><span data-stu-id="222f2-2053">21</span></span> |
| <span data-ttu-id="222f2-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="222f2-2054">enableSsl</span></span> |<span data-ttu-id="222f2-2055">Toouse SSL/TLS kanalı üzerinden FTP olup olmadığını belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="222f2-2056">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2056">No</span></span> |<span data-ttu-id="222f2-2057">TRUE</span><span class="sxs-lookup"><span data-stu-id="222f2-2057">true</span></span> |
| <span data-ttu-id="222f2-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="222f2-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="222f2-2059">Tooenable sunucu SSL FTP SSL/TLS kanalı üzerinden kullanırken doğrulama sertifikası olup olmadığını belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="222f2-2060">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2060">No</span></span> |<span data-ttu-id="222f2-2061">TRUE</span><span class="sxs-lookup"><span data-stu-id="222f2-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="222f2-2062">Örnek: Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="222f2-2063">Örnek: kullanıcı adı ve parola düz metin olarak temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="222f2-2064">Örnek: Bağlantı noktası, enableSsl, enableServerCertificateValidation kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="222f2-2065">Örnek: kimlik doğrulama ve ağ geçidi encryptedCredential kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="222f2-2066">Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-2067">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2067">Dataset</span></span>
<span data-ttu-id="222f2-2068">toodefine FTP veri kümesi, kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2069">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2069">Property</span></span> | <span data-ttu-id="222f2-2070">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2070">Description</span></span> | <span data-ttu-id="222f2-2071">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-2072">folderPath</span></span> |<span data-ttu-id="222f2-2073">Alt yolu toohello klasörü.</span><span class="sxs-lookup"><span data-stu-id="222f2-2073">Sub path toohello folder.</span></span> <span data-ttu-id="222f2-2074">Kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="222f2-2075">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="222f2-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="222f2-2076">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="222f2-2077">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2077">Yes</span></span> 
| <span data-ttu-id="222f2-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="222f2-2078">fileName</span></span> |<span data-ttu-id="222f2-2079">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="222f2-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="222f2-2080">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="222f2-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="222f2-2081">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="222f2-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="222f2-2082">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="222f2-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="222f2-2083">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2083">No</span></span> |
| <span data-ttu-id="222f2-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="222f2-2084">fileFilter</span></span> |<span data-ttu-id="222f2-2085">Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="222f2-2086">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="222f2-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="222f2-2087">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="222f2-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="222f2-2088">Örnek 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="222f2-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="222f2-2089">fileFilter bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="222f2-2090">Bu özellik ile HDFS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="222f2-2091">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2091">No</span></span> |
| <span data-ttu-id="222f2-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="222f2-2092">partitionedBy</span></span> |<span data-ttu-id="222f2-2093">partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="222f2-2094">Örneğin, her veri saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="222f2-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="222f2-2095">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2095">No</span></span> |
| <span data-ttu-id="222f2-2096">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-2096">format</span></span> | <span data-ttu-id="222f2-2097">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-2098">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-2099">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-2100">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-2101">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2101">No</span></span> |
| <span data-ttu-id="222f2-2102">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-2102">compression</span></span> | <span data-ttu-id="222f2-2103">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-2104">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**; ve desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-2105">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-2106">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2106">No</span></span> |
| <span data-ttu-id="222f2-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="222f2-2107">useBinaryTransfer</span></span> |<span data-ttu-id="222f2-2108">Belirtin olup ikili aktarım modunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="222f2-2109">İkili mod ve false ASCII için true.</span><span class="sxs-lookup"><span data-stu-id="222f2-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="222f2-2110">Varsayılan değer: True.</span><span class="sxs-lookup"><span data-stu-id="222f2-2110">Default value: True.</span></span> <span data-ttu-id="222f2-2111">İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="222f2-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="222f2-2112">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="222f2-2113">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-2114">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="222f2-2115">Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="222f2-2116">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2117">Bir FTP sunucusundan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-2118">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2118">Property</span></span> | <span data-ttu-id="222f2-2119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2119">Description</span></span> | <span data-ttu-id="222f2-2120">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-2120">Allowed values</span></span> | <span data-ttu-id="222f2-2121">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2122">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-2122">recursive</span></span> |<span data-ttu-id="222f2-2123">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="222f2-2124">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-2124">True, False (default)</span></span> |<span data-ttu-id="222f2-2125">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2126">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2126">Example</span></span>

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

<span data-ttu-id="222f2-2127">Daha fazla bilgi için bkz: [FTP Bağlayıcısı](data-factory-ftp-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="222f2-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="222f2-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-2129">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2129">Linked service</span></span>
<span data-ttu-id="222f2-2130">toodefine bir HDFS bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Hdfs**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2131">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2131">Property</span></span> | <span data-ttu-id="222f2-2132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2132">Description</span></span> | <span data-ttu-id="222f2-2133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2134">type</span><span class="sxs-lookup"><span data-stu-id="222f2-2134">type</span></span> |<span data-ttu-id="222f2-2135">Merhaba type özelliği ayarlanmalıdır: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="222f2-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="222f2-2136">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2136">Yes</span></span> |
| <span data-ttu-id="222f2-2137">Url</span><span class="sxs-lookup"><span data-stu-id="222f2-2137">Url</span></span> |<span data-ttu-id="222f2-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="222f2-2138">URL toohello HDFS</span></span> |<span data-ttu-id="222f2-2139">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2139">Yes</span></span> |
| <span data-ttu-id="222f2-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2140">authenticationType</span></span> |<span data-ttu-id="222f2-2141">Anonim veya Windows.</span><span class="sxs-lookup"><span data-stu-id="222f2-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="222f2-2142">toouse **Kerberos kimlik doğrulaması** HDFS bağlayıcı için çok başvuran[Bu bölümde](#use-kerberos-authentication-for-hdfs-connector) tooset şirket içi ortamınızı uygun şekilde.</span><span class="sxs-lookup"><span data-stu-id="222f2-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="222f2-2143">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2143">Yes</span></span> |
| <span data-ttu-id="222f2-2144">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2144">userName</span></span> |<span data-ttu-id="222f2-2145">Kullanıcı adı için Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="222f2-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="222f2-2146">Evet (Windows kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="222f2-2147">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2147">password</span></span> |<span data-ttu-id="222f2-2148">Windows kimlik doğrulaması için parola.</span><span class="sxs-lookup"><span data-stu-id="222f2-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="222f2-2149">Evet (Windows kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="222f2-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="222f2-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2150">gatewayName</span></span> |<span data-ttu-id="222f2-2151">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello HDFS kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="222f2-2152">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2152">Yes</span></span> |
| <span data-ttu-id="222f2-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-2153">encryptedCredential</span></span> |<span data-ttu-id="222f2-2154">[AzureRMDataFactoryEncryptValue yeni](https://msdn.microsoft.com/library/mt603802.aspx) hello erişim kimlik bilgisi çıktısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="222f2-2155">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="222f2-2156">Örnek: Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="222f2-2157">Örnek: Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="222f2-2158">Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-2159">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2159">Dataset</span></span>
<span data-ttu-id="222f2-2160">toodefine bir HDFS veri kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2161">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2161">Property</span></span> | <span data-ttu-id="222f2-2162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2162">Description</span></span> | <span data-ttu-id="222f2-2163">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-2164">folderPath</span></span> |<span data-ttu-id="222f2-2165">Yol toohello klasör.</span><span class="sxs-lookup"><span data-stu-id="222f2-2165">Path toohello folder.</span></span> <span data-ttu-id="222f2-2166">Örnek:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="222f2-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="222f2-2167">Kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="222f2-2168">Örneğin: folder\subfolder için klasör belirtin\\\\alt ve d:\samplefolder için d: belirtin\\\\ÖrnekKlasör.</span><span class="sxs-lookup"><span data-stu-id="222f2-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="222f2-2169">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="222f2-2170">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2170">Yes</span></span> |
| <span data-ttu-id="222f2-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="222f2-2171">fileName</span></span> |<span data-ttu-id="222f2-2172">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="222f2-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="222f2-2173">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="222f2-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="222f2-2174">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="222f2-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="222f2-2175">Veriler. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="222f2-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="222f2-2176">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2176">No</span></span> |
| <span data-ttu-id="222f2-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="222f2-2177">partitionedBy</span></span> |<span data-ttu-id="222f2-2178">partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="222f2-2179">Örnek: veri her saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="222f2-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="222f2-2180">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2180">No</span></span> |
| <span data-ttu-id="222f2-2181">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-2181">format</span></span> | <span data-ttu-id="222f2-2182">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-2183">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-2184">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-2185">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-2186">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2186">No</span></span> |
| <span data-ttu-id="222f2-2187">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-2187">compression</span></span> | <span data-ttu-id="222f2-2188">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-2189">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="222f2-2190">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-2191">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-2192">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="222f2-2193">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-2194">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2194">Example</span></span>

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

<span data-ttu-id="222f2-2195">Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="222f2-2196">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2197">HDFS veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="222f2-2198">**FileSystemSource** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="222f2-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="222f2-2199">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2199">Property</span></span> | <span data-ttu-id="222f2-2200">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2200">Description</span></span> | <span data-ttu-id="222f2-2201">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-2201">Allowed values</span></span> | <span data-ttu-id="222f2-2202">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2203">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-2203">recursive</span></span> |<span data-ttu-id="222f2-2204">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="222f2-2205">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-2205">True, False (default)</span></span> |<span data-ttu-id="222f2-2206">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2207">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2207">Example</span></span>

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

<span data-ttu-id="222f2-2208">Daha fazla bilgi için bkz: [HDFS bağlayıcı](#data-factory-hdfs-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="222f2-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="222f2-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-2210">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2210">Linked service</span></span>
<span data-ttu-id="222f2-2211">toodefine bir SFTP bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Sftp**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2212">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2212">Property</span></span> | <span data-ttu-id="222f2-2213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2213">Description</span></span> | <span data-ttu-id="222f2-2214">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2215">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="222f2-2215">host</span></span> | <span data-ttu-id="222f2-2216">Merhaba SFTP sunucu adı veya IP adresi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="222f2-2217">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2217">Yes</span></span> |
| <span data-ttu-id="222f2-2218">port</span><span class="sxs-lookup"><span data-stu-id="222f2-2218">port</span></span> |<span data-ttu-id="222f2-2219">Hangi hello SFTP sunucusunun dinleme yaptığı bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="222f2-2220">Merhaba varsayılan değer: 21</span><span class="sxs-lookup"><span data-stu-id="222f2-2220">hello default value is: 21</span></span> |<span data-ttu-id="222f2-2221">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2221">No</span></span> |
| <span data-ttu-id="222f2-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2222">authenticationType</span></span> |<span data-ttu-id="222f2-2223">Kimlik doğrulama türü belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2223">Specify authentication type.</span></span> <span data-ttu-id="222f2-2224">İzin verilen değerler: **temel**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="222f2-2225">Çok başvuran[kullanarak temel kimlik doğrulaması](#using-basic-authentication) ve [kullanarak SSH ortak anahtar kimlik doğrulaması](#using-ssh-public-key-authentication) daha fazla özellikleri ve JSON örnekleri sırasıyla bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="222f2-2226">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2226">Yes</span></span> |
| <span data-ttu-id="222f2-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="222f2-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="222f2-2228">Tooskip anahtar doğrulama konak olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="222f2-2229">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2229">No.</span></span> <span data-ttu-id="222f2-2230">Merhaba varsayılan değeri: false</span><span class="sxs-lookup"><span data-stu-id="222f2-2230">hello default value: false</span></span> |
| <span data-ttu-id="222f2-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="222f2-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="222f2-2232">Merhaba parmak izi hello ana bilgisayar anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="222f2-2233">Merhaba, Evet `skipHostKeyValidation` toofalse ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="222f2-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2234">gatewayName</span></span> |<span data-ttu-id="222f2-2235">Merhaba veri yönetimi ağ geçidi tooconnect tooan adını SFTP sunucu şirket içi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="222f2-2236">Bir şirket içi SFTP sunucusundan veri kopyalama, Evet.</span><span class="sxs-lookup"><span data-stu-id="222f2-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="222f2-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-2237">encryptedCredential</span></span> | <span data-ttu-id="222f2-2238">Şifrelenmiş kimlik bilgileri tooaccess hello SFTP sunucusu.</span><span class="sxs-lookup"><span data-stu-id="222f2-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="222f2-2239">Otomatik olarak oluşturulan, temel kimlik doğrulaması (kullanıcı adı + parola) veya SshPublicKey kimlik (kullanıcı adı + özel anahtar yolu veya içerik) Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda belirttiğiniz zaman.</span><span class="sxs-lookup"><span data-stu-id="222f2-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="222f2-2240">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2240">No.</span></span> <span data-ttu-id="222f2-2241">Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="222f2-2242">Örnek: temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="222f2-2243">toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `Basic`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="222f2-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="222f2-2244">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2244">Property</span></span> | <span data-ttu-id="222f2-2245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2245">Description</span></span> | <span data-ttu-id="222f2-2246">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2247">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2247">username</span></span> | <span data-ttu-id="222f2-2248">Erişim toohello SFTP sunucusu olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="222f2-2249">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2249">Yes</span></span> |
| <span data-ttu-id="222f2-2250">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2250">password</span></span> | <span data-ttu-id="222f2-2251">Merhaba kullanıcının (kullanıcı adı) parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2251">Password for hello user (username).</span></span> | <span data-ttu-id="222f2-2252">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="222f2-2253">Örnek: Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri **</span><span class="sxs-lookup"><span data-stu-id="222f2-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="222f2-2254">SSH ortak anahtar kimlik doğrulaması kullanarak: **</span><span class="sxs-lookup"><span data-stu-id="222f2-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="222f2-2255">toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `SshPublicKey`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="222f2-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="222f2-2256">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2256">Property</span></span> | <span data-ttu-id="222f2-2257">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2257">Description</span></span> | <span data-ttu-id="222f2-2258">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2259">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2259">username</span></span> |<span data-ttu-id="222f2-2260">Erişim toohello SFTP sunucusu olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="222f2-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="222f2-2261">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2261">Yes</span></span> |
| <span data-ttu-id="222f2-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="222f2-2262">privateKeyPath</span></span> | <span data-ttu-id="222f2-2263">Mutlak yol toohello belirtin özel anahtar dosyası bu ağ geçidi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="222f2-2264">Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="222f2-2265">Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="222f2-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="222f2-2266">privateKeyContent</span></span> | <span data-ttu-id="222f2-2267">Merhaba özel anahtar içeriğinin seri hale getirilmiş bir dize.</span><span class="sxs-lookup"><span data-stu-id="222f2-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="222f2-2268">Merhaba Kopyalama Sihirbazı'nı hello özel anahtar dosyası okuma ve hello özel anahtar içeriği otomatik olarak ayıklar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="222f2-2269">Tüm diğer aracı/SDK kullanıyorsanız, bunun yerine hello privateKeyPath özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="222f2-2270">Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="222f2-2271">Parola</span><span class="sxs-lookup"><span data-stu-id="222f2-2271">passPhrase</span></span> | <span data-ttu-id="222f2-2272">Merhaba anahtar dosyası bir parola deyimi tarafından korunuyorsa hello geçişi tümcecik/parola toodecrypt hello özel anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="222f2-2273">Merhaba özel anahtar dosyası bir parola deyimi tarafından korunuyorsa, Evet.</span><span class="sxs-lookup"><span data-stu-id="222f2-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="222f2-2274">Örnek: kullanarak özel anahtar içerik ** SshPublicKey kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="222f2-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="222f2-2275">Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-2276">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2276">Dataset</span></span>
<span data-ttu-id="222f2-2277">toodefine SFTP dataset kümesi hello **türü** hello kümesinin çok**FileShare**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2278">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2278">Property</span></span> | <span data-ttu-id="222f2-2279">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2279">Description</span></span> | <span data-ttu-id="222f2-2280">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="222f2-2281">folderPath</span></span> |<span data-ttu-id="222f2-2282">Alt yolu toohello klasörü.</span><span class="sxs-lookup"><span data-stu-id="222f2-2282">Sub path toohello folder.</span></span> <span data-ttu-id="222f2-2283">Kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="222f2-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="222f2-2284">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="222f2-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="222f2-2285">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="222f2-2286">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2286">Yes</span></span> |
| <span data-ttu-id="222f2-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="222f2-2287">fileName</span></span> |<span data-ttu-id="222f2-2288">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="222f2-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="222f2-2289">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="222f2-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="222f2-2290">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="222f2-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="222f2-2291">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="222f2-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="222f2-2292">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2292">No</span></span> |
| <span data-ttu-id="222f2-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="222f2-2293">fileFilter</span></span> |<span data-ttu-id="222f2-2294">Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="222f2-2295">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="222f2-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="222f2-2296">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="222f2-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="222f2-2297">Örnek 2:`"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="222f2-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="222f2-2298">fileFilter bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="222f2-2299">Bu özellik ile HDFS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="222f2-2300">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2300">No</span></span> |
| <span data-ttu-id="222f2-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="222f2-2301">partitionedBy</span></span> |<span data-ttu-id="222f2-2302">partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="222f2-2303">Örneğin, her veri saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="222f2-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="222f2-2304">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2304">No</span></span> |
| <span data-ttu-id="222f2-2305">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-2305">format</span></span> | <span data-ttu-id="222f2-2306">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-2307">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="222f2-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="222f2-2308">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="222f2-2309">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="222f2-2310">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2310">No</span></span> |
| <span data-ttu-id="222f2-2311">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-2311">compression</span></span> | <span data-ttu-id="222f2-2312">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-2313">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="222f2-2314">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-2315">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-2316">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2316">No</span></span> |
| <span data-ttu-id="222f2-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="222f2-2317">useBinaryTransfer</span></span> |<span data-ttu-id="222f2-2318">Belirtin olup ikili aktarım modunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="222f2-2319">İkili mod ve false ASCII için true.</span><span class="sxs-lookup"><span data-stu-id="222f2-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="222f2-2320">Varsayılan değer: True.</span><span class="sxs-lookup"><span data-stu-id="222f2-2320">Default value: True.</span></span> <span data-ttu-id="222f2-2321">İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="222f2-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="222f2-2322">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="222f2-2323">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-2324">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="222f2-2325">Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="222f2-2326">Dosya sistem kaynağını kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2327">SFTP kaynaktan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**FileSystemSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-2328">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2328">Property</span></span> | <span data-ttu-id="222f2-2329">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2329">Description</span></span> | <span data-ttu-id="222f2-2330">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-2330">Allowed values</span></span> | <span data-ttu-id="222f2-2331">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2332">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="222f2-2332">recursive</span></span> |<span data-ttu-id="222f2-2333">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="222f2-2334">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="222f2-2334">True, False (default)</span></span> |<span data-ttu-id="222f2-2335">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="222f2-2336">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2336">Example</span></span>

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

<span data-ttu-id="222f2-2337">Daha fazla bilgi için bkz: [SFTP bağlayıcı](data-factory-sftp-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="222f2-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="222f2-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-2339">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2339">Linked service</span></span>
<span data-ttu-id="222f2-2340">bir HTTP toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Http**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2341">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2341">Property</span></span> | <span data-ttu-id="222f2-2342">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2342">Description</span></span> | <span data-ttu-id="222f2-2343">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2344">URL</span><span class="sxs-lookup"><span data-stu-id="222f2-2344">url</span></span> | <span data-ttu-id="222f2-2345">Temel URL toohello Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="222f2-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="222f2-2346">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2346">Yes</span></span> |
| <span data-ttu-id="222f2-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2347">authenticationType</span></span> | <span data-ttu-id="222f2-2348">Merhaba kimlik doğrulama türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="222f2-2349">İzin verilen değerler: **anonim**, **temel**, **Özet**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="222f2-2350">Daha fazla özellikleri ve JSON örnekleri bu tablonun altındaki toosections bu kimlik doğrulama türleri için sırasıyla bakın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="222f2-2351">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2351">Yes</span></span> |
| <span data-ttu-id="222f2-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="222f2-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="222f2-2353">Kaynak HTTPS Web sunucusu ise tooenable sunucu SSL sertifikası doğrulaması olup olmadığını belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="222f2-2354">Hayır, varsayılan değer true şeklindedir</span><span class="sxs-lookup"><span data-stu-id="222f2-2354">No, default is true</span></span> |
| <span data-ttu-id="222f2-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2355">gatewayName</span></span> | <span data-ttu-id="222f2-2356">Merhaba veri yönetimi ağ geçidi tooconnect tooan adını HTTP kaynağı şirket içi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="222f2-2357">Bir şirket içi HTTP kaynaktan veri kopyalama, Evet.</span><span class="sxs-lookup"><span data-stu-id="222f2-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="222f2-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-2358">encryptedCredential</span></span> | <span data-ttu-id="222f2-2359">Şifrelenmiş kimlik bilgileri tooaccess hello HTTP uç noktası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="222f2-2360">Otomatik olarak oluşturulan Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda hello kimlik doğrulama bilgilerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="222f2-2361">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2361">No.</span></span> <span data-ttu-id="222f2-2362">Yalnızca bir şirket içi HTTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="222f2-2363">Örnek: Temel, Özet veya Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="222f2-2364">Ayarlama `authenticationType` olarak `Basic`, `Digest`, veya `Windows`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="222f2-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="222f2-2365">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2365">Property</span></span> | <span data-ttu-id="222f2-2366">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2366">Description</span></span> | <span data-ttu-id="222f2-2367">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2368">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2368">username</span></span> | <span data-ttu-id="222f2-2369">Kullanıcı adı tooaccess hello HTTP uç noktası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="222f2-2370">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2370">Yes</span></span> |
| <span data-ttu-id="222f2-2371">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2371">password</span></span> | <span data-ttu-id="222f2-2372">Merhaba kullanıcının (kullanıcı adı) parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2372">Password for hello user (username).</span></span> | <span data-ttu-id="222f2-2373">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="222f2-2374">Örnek: ClientCertificate kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="222f2-2375">toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `ClientCertificate`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="222f2-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="222f2-2376">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2376">Property</span></span> | <span data-ttu-id="222f2-2377">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2377">Description</span></span> | <span data-ttu-id="222f2-2378">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="222f2-2379">embeddedCertData</span></span> | <span data-ttu-id="222f2-2380">Merhaba Base64 ile kodlanmış içeriğini ikili veri hello kişisel bilgi değişimi (PFX) dosyası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="222f2-2381">Her iki hello belirtin `embeddedCertData` veya `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="222f2-2382">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="222f2-2382">certThumbprint</span></span> | <span data-ttu-id="222f2-2383">ağ geçidi makinenizin sertifika deposunda yüklü hello sertifikanın parmak izini hello.</span><span class="sxs-lookup"><span data-stu-id="222f2-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="222f2-2384">Yalnızca bir şirket içi HTTP kaynaktan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="222f2-2385">Her iki hello belirtin `embeddedCertData` veya `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="222f2-2386">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2386">password</span></span> | <span data-ttu-id="222f2-2387">Merhaba sertifikayla ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="222f2-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="222f2-2388">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2388">No</span></span> |

<span data-ttu-id="222f2-2389">Kullanırsanız `certThumbprint` kimlik doğrulaması ve hello sertifika hello kişisel hello yerel bilgisayar deposunda yüklü için toogrant hello okuma izni toohello ağ geçidi hizmeti gerekir:</span><span class="sxs-lookup"><span data-stu-id="222f2-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="222f2-2390">Microsoft Yönetim Konsolu (MMC) başlatın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="222f2-2391">Merhaba eklemek **sertifikaları** bu hedefleri hello eklentisi **yerel bilgisayar**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="222f2-2392">Genişletme **sertifikaları**, **kişisel**, tıklatıp **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="222f2-2393">Merhaba kişisel deposundan Hello sertifikayı sağ tıklatın ve seçin **tüm görevler**->**özel anahtarları Yönet...**</span><span class="sxs-lookup"><span data-stu-id="222f2-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="222f2-2394">Merhaba üzerinde **güvenlik** sekmesinde, altında veri yönetimi ağ geçidi ana bilgisayar hizmeti çalıştığı hello okuma erişimi toohello sertifikasıyla hello kullanıcı hesabını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="222f2-2395">**Örnek: istemci sertifikası kullanarak:** bu hizmeti, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="222f2-2396">Veri Yönetimi yüklü ağ geçidi ile Merhaba makinede yüklü bir istemci sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="222f2-2397">Örnek: istemci sertifikası bir dosyada kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="222f2-2398">Bu hizmet bağlantılar, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="222f2-2399">Veri Yönetimi yüklü ağ geçidi ile bir istemci sertifika dosyası hello makinede kullanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="222f2-2400">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-2401">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2401">Dataset</span></span>
<span data-ttu-id="222f2-2402">bir HTTP toodefine veri kümesi, kümesi hello **türü** hello kümesinin çok**Http**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2403">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2403">Property</span></span> | <span data-ttu-id="222f2-2404">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2404">Description</span></span> | <span data-ttu-id="222f2-2405">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="222f2-2406">relativeUrl</span></span> | <span data-ttu-id="222f2-2407">Merhaba verileri içeren bir göreli URL toohello kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="222f2-2408">Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="222f2-2409">kullanabileceğiniz tooconstruct dinamik URL [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md), örneğin: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="222f2-2410">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2410">No</span></span> |
| <span data-ttu-id="222f2-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="222f2-2411">requestMethod</span></span> | <span data-ttu-id="222f2-2412">HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2412">Http method.</span></span> <span data-ttu-id="222f2-2413">İzin verilen değerler **almak** veya **POST**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="222f2-2414">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2414">No.</span></span> <span data-ttu-id="222f2-2415">Varsayılan değer `GET`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="222f2-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="222f2-2416">additionalHeaders</span></span> | <span data-ttu-id="222f2-2417">Ek HTTP isteği üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="222f2-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="222f2-2418">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2418">No</span></span> |
| <span data-ttu-id="222f2-2419">RequestBody</span><span class="sxs-lookup"><span data-stu-id="222f2-2419">requestBody</span></span> | <span data-ttu-id="222f2-2420">HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2420">Body for HTTP request.</span></span> | <span data-ttu-id="222f2-2421">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2421">No</span></span> |
| <span data-ttu-id="222f2-2422">Biçimi</span><span class="sxs-lookup"><span data-stu-id="222f2-2422">format</span></span> | <span data-ttu-id="222f2-2423">Toosimply istiyorsanız **HTTP uç noktası olarak hello veri almak-olduğu** ayrıştırma olmadan, bu biçim ayarlarını atla.</span><span class="sxs-lookup"><span data-stu-id="222f2-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="222f2-2424">Kopyalama sırasında tooparse hello HTTP yanıt içerik isterseniz şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="222f2-2425">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="222f2-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="222f2-2426">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2426">No</span></span> |
| <span data-ttu-id="222f2-2427">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="222f2-2427">compression</span></span> | <span data-ttu-id="222f2-2428">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="222f2-2429">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="222f2-2430">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="222f2-2431">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="222f2-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="222f2-2432">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="222f2-2433">Örnek: hello (varsayılan) GET yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="222f2-2434">Örnek: Merhaba POST yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="222f2-2435">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="222f2-2436">Kopyalama etkinliğinde HTTP kaynağı</span><span class="sxs-lookup"><span data-stu-id="222f2-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2437">Bir HTTP kaynaktan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**HttpSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-2438">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2438">Property</span></span> | <span data-ttu-id="222f2-2439">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2439">Description</span></span> | <span data-ttu-id="222f2-2440">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="222f2-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="222f2-2441">httpRequestTimeout</span></span> | <span data-ttu-id="222f2-2442">Merhaba HTTP isteği tooget yanıt için zaman aşımı (TimeSpan) hello.</span><span class="sxs-lookup"><span data-stu-id="222f2-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="222f2-2443">Merhaba zaman aşımı tooget bir yanıt hello zaman aşımı tooread yanıt verileri değil olur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="222f2-2444">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2444">No.</span></span> <span data-ttu-id="222f2-2445">Varsayılan değer: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="222f2-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="222f2-2446">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="222f2-2447">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](data-factory-http-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="222f2-2448">OData</span><span class="sxs-lookup"><span data-stu-id="222f2-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-2449">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2449">Linked service</span></span>
<span data-ttu-id="222f2-2450">bir OData toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OData**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2451">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2451">Property</span></span> | <span data-ttu-id="222f2-2452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2452">Description</span></span> | <span data-ttu-id="222f2-2453">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2454">URL</span><span class="sxs-lookup"><span data-stu-id="222f2-2454">url</span></span> |<span data-ttu-id="222f2-2455">Merhaba OData hizmeti URL'si.</span><span class="sxs-lookup"><span data-stu-id="222f2-2455">Url of hello OData service.</span></span> |<span data-ttu-id="222f2-2456">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2456">Yes</span></span> |
| <span data-ttu-id="222f2-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2457">authenticationType</span></span> |<span data-ttu-id="222f2-2458">Kimlik doğrulama türü tooconnect toohello OData kaynağı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="222f2-2459">OData bulut için olası değerler şunlardır anonim, temel ve OAuth (Not OAuth Azure Active Directory tabanlı şu anda yalnızca Azure Data Factory destek).</span><span class="sxs-lookup"><span data-stu-id="222f2-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="222f2-2460">Anonim, temel ve Windows, şirket içi OData için olası değerler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="222f2-2461">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2461">Yes</span></span> |
| <span data-ttu-id="222f2-2462">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2462">username</span></span> |<span data-ttu-id="222f2-2463">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="222f2-2464">Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="222f2-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="222f2-2465">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2465">password</span></span> |<span data-ttu-id="222f2-2466">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-2467">Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="222f2-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="222f2-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="222f2-2468">authorizedCredential</span></span> |<span data-ttu-id="222f2-2469">OAuth kullanıyorsanız **Authorize** hello Data Factory Kopyalama Sihirbazı veya Düzenleyicisi'nde düğmesine tıklayın ve sonra bu özellik başlangıç değeri otomatik olarak oluşturulan kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="222f2-2470">Evet (yalnızca OAuth kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="222f2-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="222f2-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2471">gatewayName</span></span> |<span data-ttu-id="222f2-2472">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi OData hizmeti kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="222f2-2473">Yalnızca şirket içi OData kaynak sunucudan kopyaladığınız verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="222f2-2474">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="222f2-2475">Temel kimlik doğrulaması kullanan örnek-</span><span class="sxs-lookup"><span data-stu-id="222f2-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="222f2-2476">Anonim kimlik doğrulaması kullanan örnek-</span><span class="sxs-lookup"><span data-stu-id="222f2-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="222f2-2477">Örnek - kullanan Windows kimlik doğrulaması erişme OData kaynağı şirket içi</span><span class="sxs-lookup"><span data-stu-id="222f2-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="222f2-2478">Örnek - bulut OData kaynağı erişme OAuth kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="222f2-2479">Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="222f2-2480">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2480">Dataset</span></span>
<span data-ttu-id="222f2-2481">toodefine bir OData veri kümesini kümesi hello **türü** hello kümesinin çok**ODataResource**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2482">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2482">Property</span></span> | <span data-ttu-id="222f2-2483">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2483">Description</span></span> | <span data-ttu-id="222f2-2484">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2485">Yol</span><span class="sxs-lookup"><span data-stu-id="222f2-2485">path</span></span> |<span data-ttu-id="222f2-2486">Yol toohello OData kaynak</span><span class="sxs-lookup"><span data-stu-id="222f2-2486">Path toohello OData resource</span></span> |<span data-ttu-id="222f2-2487">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2488">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2488">Example</span></span>

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

<span data-ttu-id="222f2-2489">Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-2490">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2491">Bir OData kaynaktan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-2492">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2492">Property</span></span> | <span data-ttu-id="222f2-2493">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2493">Description</span></span> | <span data-ttu-id="222f2-2494">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2494">Example</span></span> | <span data-ttu-id="222f2-2495">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2496">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-2496">query</span></span> |<span data-ttu-id="222f2-2497">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-2498">"? $select adı, açıklama ve $top = 5 ="</span><span class="sxs-lookup"><span data-stu-id="222f2-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="222f2-2499">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2500">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2500">Example</span></span>

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

<span data-ttu-id="222f2-2501">Daha fazla bilgi için bkz: [OData bağlayıcı](data-factory-odata-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="222f2-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="222f2-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-2503">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2503">Linked service</span></span>
<span data-ttu-id="222f2-2504">toodefine bir ODBC bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**OnPremisesOdbc**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2505">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2505">Property</span></span> | <span data-ttu-id="222f2-2506">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2506">Description</span></span> | <span data-ttu-id="222f2-2507">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-2508">connectionString</span></span> |<span data-ttu-id="222f2-2509">Merhaba olmayan erişim kimlik bilgisi kısmı hello bağlantı dizesini ve isteğe bağlı bir kimlik bilgisi şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="222f2-2510">Aşağıdaki bölümlerde hello örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="222f2-2511">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2511">Yes</span></span> |
| <span data-ttu-id="222f2-2512">kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="222f2-2512">credential</span></span> |<span data-ttu-id="222f2-2513">Merhaba erişim kimlik bilgisi bölümü sürücüye özgü özellik değer biçiminde belirtilen hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="222f2-2514">Örnek: "Uid =<user ID>; PWD =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="222f2-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="222f2-2515">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2515">No</span></span> |
| <span data-ttu-id="222f2-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2516">authenticationType</span></span> |<span data-ttu-id="222f2-2517">Kimlik doğrulama türü tooconnect toohello ODBC veri deposu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="222f2-2518">Olası değerler şunlardır: anonim ve temel.</span><span class="sxs-lookup"><span data-stu-id="222f2-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="222f2-2519">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2519">Yes</span></span> |
| <span data-ttu-id="222f2-2520">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2520">username</span></span> |<span data-ttu-id="222f2-2521">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="222f2-2522">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2522">No</span></span> |
| <span data-ttu-id="222f2-2523">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2523">password</span></span> |<span data-ttu-id="222f2-2524">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-2525">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2525">No</span></span> |
| <span data-ttu-id="222f2-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2526">gatewayName</span></span> |<span data-ttu-id="222f2-2527">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello ODBC veri deposu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="222f2-2528">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="222f2-2529">Temel kimlik doğrulaması kullanan örnek-</span><span class="sxs-lookup"><span data-stu-id="222f2-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="222f2-2530">Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri kullanılarak örnek-</span><span class="sxs-lookup"><span data-stu-id="222f2-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="222f2-2531">Merhaba kimlik hello kullanarak şifreleyebilirsiniz [yeni AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0 sürümü) cmdlet'ini veya [yeni AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 veya önceki bir sürümü hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="222f2-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="222f2-2532">Örnek: Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="222f2-2533">Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-2534">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2534">Dataset</span></span>
<span data-ttu-id="222f2-2535">toodefine bir ODBC veri kümesini kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2536">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2536">Property</span></span> | <span data-ttu-id="222f2-2537">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2537">Description</span></span> | <span data-ttu-id="222f2-2538">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-2539">tableName</span></span> |<span data-ttu-id="222f2-2540">Merhaba ODBC veri deposundaki Merhaba tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="222f2-2541">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="222f2-2542">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2542">Example</span></span>

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

<span data-ttu-id="222f2-2543">Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-2544">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2545">Bir ODBC veri deposundan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-2546">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2546">Property</span></span> | <span data-ttu-id="222f2-2547">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2547">Description</span></span> | <span data-ttu-id="222f2-2548">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-2548">Allowed values</span></span> | <span data-ttu-id="222f2-2549">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2550">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-2550">query</span></span> |<span data-ttu-id="222f2-2551">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-2552">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2552">SQL query string.</span></span> <span data-ttu-id="222f2-2553">Örneğin: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="222f2-2554">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2555">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2555">Example</span></span>

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

<span data-ttu-id="222f2-2556">Daha fazla bilgi için bkz: [ODBC bağlayıcı](data-factory-odbc-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="222f2-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="222f2-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="222f2-2558">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2558">Linked service</span></span>
<span data-ttu-id="222f2-2559">bir Salesforce toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Salesforce**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2560">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2560">Property</span></span> | <span data-ttu-id="222f2-2561">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2561">Description</span></span> | <span data-ttu-id="222f2-2562">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="222f2-2563">environmentUrl</span></span> | <span data-ttu-id="222f2-2564">Merhaba, URL Salesforce örneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="222f2-2565">-Varsayılan değer "https://login.salesforce.com" dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="222f2-2566">-Korumalı alan, toocopy verileri "https://test.salesforce.com" belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="222f2-2567">-toocopy verileri özel bir etki alanından belirtin, örneğin, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="222f2-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="222f2-2568">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2568">No</span></span> |
| <span data-ttu-id="222f2-2569">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2569">username</span></span> |<span data-ttu-id="222f2-2570">Merhaba kullanıcı hesabı için bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="222f2-2571">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2571">Yes</span></span> |
| <span data-ttu-id="222f2-2572">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2572">password</span></span> |<span data-ttu-id="222f2-2573">Merhaba kullanıcı hesabı için bir parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="222f2-2574">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2574">Yes</span></span> |
| <span data-ttu-id="222f2-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="222f2-2575">securityToken</span></span> |<span data-ttu-id="222f2-2576">Merhaba kullanıcı hesabı için bir güvenlik belirteci belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="222f2-2577">Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) yönelik yönergeler tooreset/get bir güvenlik belirteci.</span><span class="sxs-lookup"><span data-stu-id="222f2-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="222f2-2578">Genel olarak, toolearn güvenlik belirteçleri hakkında bkz [güvenlik ve hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="222f2-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="222f2-2579">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2580">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2580">Example</span></span>

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

<span data-ttu-id="222f2-2581">Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-2582">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2582">Dataset</span></span>
<span data-ttu-id="222f2-2583">toodefine bir Salesforce veri kümesi hello **türü** hello kümesinin çok**RelationalTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2584">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2584">Property</span></span> | <span data-ttu-id="222f2-2585">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2585">Description</span></span> | <span data-ttu-id="222f2-2586">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="222f2-2587">tableName</span></span> |<span data-ttu-id="222f2-2588">Salesforce Merhaba tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="222f2-2589">Hayır (varsa bir **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2590">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2590">Example</span></span>

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

<span data-ttu-id="222f2-2591">Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="222f2-2592">Kopyalama etkinliği ilişkisel kaynağında</span><span class="sxs-lookup"><span data-stu-id="222f2-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2593">Salesforce veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**RelationalSource**ve hello özelliklerinde aşağıdaki belirtin **kaynak** Bölüm:</span><span class="sxs-lookup"><span data-stu-id="222f2-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="222f2-2594">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2594">Property</span></span> | <span data-ttu-id="222f2-2595">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2595">Description</span></span> | <span data-ttu-id="222f2-2596">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="222f2-2596">Allowed values</span></span> | <span data-ttu-id="222f2-2597">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="222f2-2598">sorgu</span><span class="sxs-lookup"><span data-stu-id="222f2-2598">query</span></span> |<span data-ttu-id="222f2-2599">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="222f2-2600">Bir SQL-92 sorgu veya [Salesforce nesnesi sorgu dili (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) sorgu.</span><span class="sxs-lookup"><span data-stu-id="222f2-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="222f2-2601">Örneğin:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="222f2-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="222f2-2602">Hayır (Merhaba, **tableName** Merhaba, **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="222f2-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2603">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="222f2-2604">Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="222f2-2605">Daha fazla bilgi için bkz: [Salesforce bağlayıcı](data-factory-salesforce-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="222f2-2606">Web verileri</span><span class="sxs-lookup"><span data-stu-id="222f2-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2607">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2607">Linked service</span></span>
<span data-ttu-id="222f2-2608">toodefine Web bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**Web**ve hello özelliklerinde aşağıdaki belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2609">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2609">Property</span></span> | <span data-ttu-id="222f2-2610">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2610">Description</span></span> | <span data-ttu-id="222f2-2611">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2612">Url</span><span class="sxs-lookup"><span data-stu-id="222f2-2612">Url</span></span> |<span data-ttu-id="222f2-2613">URL toohello Web kaynağı</span><span class="sxs-lookup"><span data-stu-id="222f2-2613">URL toohello Web source</span></span> |<span data-ttu-id="222f2-2614">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2614">Yes</span></span> |
| <span data-ttu-id="222f2-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="222f2-2615">authenticationType</span></span> |<span data-ttu-id="222f2-2616">Anonim.</span><span class="sxs-lookup"><span data-stu-id="222f2-2616">Anonymous.</span></span> |<span data-ttu-id="222f2-2617">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="222f2-2618">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2618">Example</span></span>


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

<span data-ttu-id="222f2-2619">Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="222f2-2620">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2620">Dataset</span></span>
<span data-ttu-id="222f2-2621">toodefine bir Web veri kümesi hello **türü** hello kümesinin çok**WebTable**ve hello özelliklerinde aşağıdaki hello belirtin **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="222f2-2622">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2622">Property</span></span> | <span data-ttu-id="222f2-2623">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2623">Description</span></span> | <span data-ttu-id="222f2-2624">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-2625">type</span><span class="sxs-lookup"><span data-stu-id="222f2-2625">type</span></span> |<span data-ttu-id="222f2-2626">Merhaba veri kümesi türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-2626">type of hello dataset.</span></span> <span data-ttu-id="222f2-2627">çok ayarlanmalıdır**WebTable**</span><span class="sxs-lookup"><span data-stu-id="222f2-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="222f2-2628">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2628">Yes</span></span> |
| <span data-ttu-id="222f2-2629">Yol</span><span class="sxs-lookup"><span data-stu-id="222f2-2629">path</span></span> |<span data-ttu-id="222f2-2630">Merhaba tablo içeren bir göreli URL toohello kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="222f2-2631">Hayır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2631">No.</span></span> <span data-ttu-id="222f2-2632">Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="222f2-2633">Dizin</span><span class="sxs-lookup"><span data-stu-id="222f2-2633">index</span></span> |<span data-ttu-id="222f2-2634">hello kaynak hello tabloda başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="222f2-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="222f2-2635">Bkz: [bir HTML sayfasında tablosunun Get dizini](#get-index-of-a-table-in-an-html-page) HTML sayfası bir tablodaki adımları toogetting dizini için bölüm.</span><span class="sxs-lookup"><span data-stu-id="222f2-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="222f2-2636">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="222f2-2637">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2637">Example</span></span>

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

<span data-ttu-id="222f2-2638">Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#dataset-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="222f2-2639">Kopyalama etkinliğinde Web kaynağı</span><span class="sxs-lookup"><span data-stu-id="222f2-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="222f2-2640">Bir web tablodan veri kopyalıyorsanız hello ayarlamak **kaynak türünü** Merhaba kopya etkinliği çok**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="222f2-2641">Şu anda kopyalama etkinliği hello kaynağında olduğunda türü **WebSource**, hiçbir ek özellikler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="222f2-2642">Örnek</span><span class="sxs-lookup"><span data-stu-id="222f2-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="222f2-2643">Daha fazla bilgi için bkz: [Web tablo bağlayıcı](data-factory-web-table-connector.md#copy-activity-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="222f2-2644">ORTAMLAR İŞLEM</span><span class="sxs-lookup"><span data-stu-id="222f2-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="222f2-2645">Merhaba aşağıdaki tabloda, bunlar üzerinde çalışan Data Factory ve hello dönüştürme etkinlikleri tarafından desteklenen hello işlem ortamları listeler.</span><span class="sxs-lookup"><span data-stu-id="222f2-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="222f2-2646">Merhaba işlem olduğunuz Hello bağlantısına tıklayın toosee hello JSON şemalarında bağlantılı hizmet toolink için tooa veri fabrikası ilgileniyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="222f2-2647">İşlem ortamı</span><span class="sxs-lookup"><span data-stu-id="222f2-2647">Compute environment</span></span> | <span data-ttu-id="222f2-2648">Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="222f2-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="222f2-2649">[İsteğe bağlı Hdınsight kümesi](#on-demand-azure-hdinsight-cluster) veya [kendi Hdınsight kümenizi](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="222f2-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="222f2-2650">[.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinliği](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="222f2-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="222f2-2651">Azure toplu işlem</span><span class="sxs-lookup"><span data-stu-id="222f2-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="222f2-2652">.NET özel etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="222f2-2653">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="222f2-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="222f2-2654">[Toplu iş yürütme etkinliği makine](#machine-learning-batch-execution-activity), [kaynak güncelleştirme etkinliği makine](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="222f2-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="222f2-2655">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="222f2-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="222f2-2656">Data Lake Analytics U-SQL</span><span class="sxs-lookup"><span data-stu-id="222f2-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="222f2-2657">[Azure SQL veritabanı](#azure-sql-database-1), [Azure SQL veri ambarı](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="222f2-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="222f2-2658">Saklı Yordam</span><span class="sxs-lookup"><span data-stu-id="222f2-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="222f2-2659">İsteğe bağlı Azure Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="222f2-2660">Hello Azure Data Factory hizmetine otomatik olarak bir Windows/Linux tabanlı isteğe bağlı Hdınsight küme tooprocess veriler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="222f2-2661">Merhaba küme hello depolama hesabı (Merhaba JSON özelliğinde linkedServiceName) ile aynı bölgeye hello kümesi ile ilişkili hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="222f2-2662">Bu bağlı hizmete dönüştürme etkinlikleri izleyerek hello çalıştırabilirsiniz: [.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce etkinliği ](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinlik](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="222f2-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2663">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2663">Linked service</span></span> 
<span data-ttu-id="222f2-2664">Aşağıdaki tablonun hello hello Azure JSON tanımında bir isteğe bağlı Hdınsight bağlı hizmeti kullanılan hello özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="222f2-2665">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2665">Property</span></span> | <span data-ttu-id="222f2-2666">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2666">Description</span></span> | <span data-ttu-id="222f2-2667">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2668">type</span><span class="sxs-lookup"><span data-stu-id="222f2-2668">type</span></span> |<span data-ttu-id="222f2-2669">Merhaba type özelliği çok ayarlanmalıdır**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="222f2-2670">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2670">Yes</span></span> |
| <span data-ttu-id="222f2-2671">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="222f2-2671">clusterSize</span></span> |<span data-ttu-id="222f2-2672">Merhaba kümede çalışan/veri düğüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="222f2-2673">Merhaba Hdınsight kümesi hello için bu özelliği belirtmeniz çalışan düğüm sayısı ile birlikte 2 baş düğümler ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="222f2-2674">Merhaba düğümleri olan 24 çekirdek 4 çalışan düğümlü bir küme alır, böylece 4 çekirdeğe sahip Standard_D3 boyutunu (4\*4 = 16 çekirdek çalışan düğümleri artı 2\*4 = 8 çekirdek baş düğümler için).</span><span class="sxs-lookup"><span data-stu-id="222f2-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="222f2-2675">Bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 katmanı hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="222f2-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="222f2-2676">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2676">Yes</span></span> |
| <span data-ttu-id="222f2-2677">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="222f2-2677">timetolive</span></span> |<span data-ttu-id="222f2-2678">Merhaba boşta kalma süresi hello isteğe bağlı Hdınsight kümesi için izin verilen.</span><span class="sxs-lookup"><span data-stu-id="222f2-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="222f2-2679">Ne kadar süreyle hello isteğe bağlı Hdınsight kümesi hello kümedeki diğer etkin iş yok varsa bir etkinlik tamamlandıktan sonra canlı kalır belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="222f2-2680">Bir etkinlik 6 dakika ve timetolive sürerse Örneğin, too5 dakika, 5 dakika sonra hello için Canlı hello küme kalır hello etkinlik işleme 6 dakika ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="222f2-2681">Başka bir etkinlik hello 6 dakika penceresiyle yürütülürse, hello tarafından işlenir aynı küme.</span><span class="sxs-lookup"><span data-stu-id="222f2-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="222f2-2682">İsteğe bağlı Hdınsight kümesi oluşturma (biraz sürebilir), pahalı bir işlem olduğundan bu ayar isteğe bağlı Hdınsight kümesi yeniden kullanarak bir veri fabrikası gerekli tooimprove performansını kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="222f2-2683">Timetolive değeri too0 ayarlarsanız, hello etkinliği çalıştırmak hemen işlenen hello küme silinir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="222f2-2684">Yüksek bir değer ayarlarsanız hello diğer yandan hello küme gereksiz yere yüksek maliyetlerini kaynaklanan boşta kalır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="222f2-2685">Bu nedenle, gereksinimlerinize göre hello uygun değere ayarlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="222f2-2686">Birden çok ardışık düzen paylaşabilirsiniz hello timetolive özellik değerini uygun şekilde ayarlanmışsa, hello hello isteğe bağlı Hdınsight kümesinin aynı örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="222f2-2687">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2687">Yes</span></span> |
| <span data-ttu-id="222f2-2688">Sürüm</span><span class="sxs-lookup"><span data-stu-id="222f2-2688">version</span></span> |<span data-ttu-id="222f2-2689">Merhaba Hdınsight küme sürümü.</span><span class="sxs-lookup"><span data-stu-id="222f2-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="222f2-2690">Ayrıntılar için bkz [desteklenen Azure Data Factory'de Hdınsight sürümleri](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="222f2-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="222f2-2691">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2691">No</span></span> |
| <span data-ttu-id="222f2-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="222f2-2692">linkedServiceName</span></span> |<span data-ttu-id="222f2-2693">Azure depolama bağlı hizmeti toobe depolamak ve veri işleme için Hello isteğe bağlı küme tarafından kullanılan.</span><span class="sxs-lookup"><span data-stu-id="222f2-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="222f2-2694">Şu anda bir Azure Data Lake Store hello depolama alanı olarak kullanan bir isteğe bağlı Hdınsight kümesi oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="222f2-2695">Bir Azure Data Lake Store'da işleme Hdınsight toostore hello sonuç verileri istiyorsanız hello Azure Blob Storage toohello Azure Data Lake Store kopyalama etkinliği toocopy hello verilerden kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="222f2-2696">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2696">Yes</span></span> |
| <span data-ttu-id="222f2-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="222f2-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="222f2-2698">Böylece Hello Data Factory hizmetinin bunları sizin adınıza kaydedebilirsiniz hello Hdınsight için ek depolama hesapları hizmeti bağlı belirtir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="222f2-2699">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2699">No</span></span> |
| <span data-ttu-id="222f2-2700">osType</span><span class="sxs-lookup"><span data-stu-id="222f2-2700">osType</span></span> |<span data-ttu-id="222f2-2701">İşletim sistemi türü.</span><span class="sxs-lookup"><span data-stu-id="222f2-2701">Type of operating system.</span></span> <span data-ttu-id="222f2-2702">İzin verilen değerler: (varsayılan) Windows ve Linux</span><span class="sxs-lookup"><span data-stu-id="222f2-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="222f2-2703">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2703">No</span></span> |
| <span data-ttu-id="222f2-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="222f2-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="222f2-2705">Azure SQL bağlı Hello adını noktası toohello HCatalog veritabanı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="222f2-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="222f2-2706">Merhaba isteğe bağlı Hdınsight kümesi hello meta depo hello Azure SQL veritabanı kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="222f2-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="222f2-2707">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="222f2-2708">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2708">JSON example</span></span>
<span data-ttu-id="222f2-2709">JSON aşağıdaki hello Linux tabanlı isteğe bağlı Hdınsight bağlı hizmeti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="222f2-2710">Merhaba Data Factory hizmetinin otomatik olarak oluşturur bir **Linux tabanlı** veri dilimi işlerken Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="222f2-2711">Daha fazla bilgi için bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="222f2-2712">Var olan Azure Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="222f2-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="222f2-2713">Data Factory ile kendi Hdınsight kümenizi Azure Hdınsight bağlı hizmeti tooregister oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="222f2-2714">Bu bağlı hizmete veri dönüştürme etkinlikleri izleyerek hello çalıştırabilirsiniz: [.NET özel etkinlik](#net-custom-activity), [Hive etkinliğini](#hdinsight-hive-activity), [Pig etkinlik] (#hdinsight-pig-etkinliği [MapReduce Etkinlik](#hdinsight-mapreduce-activity), [Hadoop etkinlik akış](#hdinsight-streaming-activityd), [Spark etkinlik](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="222f2-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2715">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2715">Linked service</span></span>
<span data-ttu-id="222f2-2716">Aşağıdaki tablonun hello hello Azure JSON tanımında Azure Hdınsight bağlı hizmeti kullanılan hello özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="222f2-2717">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2717">Property</span></span> | <span data-ttu-id="222f2-2718">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2718">Description</span></span> | <span data-ttu-id="222f2-2719">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2720">type</span><span class="sxs-lookup"><span data-stu-id="222f2-2720">type</span></span> |<span data-ttu-id="222f2-2721">Merhaba type özelliği çok ayarlanmalıdır**Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="222f2-2722">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2722">Yes</span></span> |
| <span data-ttu-id="222f2-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="222f2-2723">clusterUri</span></span> |<span data-ttu-id="222f2-2724">Merhaba hello Hdınsight kümesinin URI.</span><span class="sxs-lookup"><span data-stu-id="222f2-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="222f2-2725">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2725">Yes</span></span> |
| <span data-ttu-id="222f2-2726">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2726">username</span></span> |<span data-ttu-id="222f2-2727">Tooconnect tooan olan bir Hdınsight kümesine kullanılan hello kullanıcı toobe Hello adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="222f2-2728">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2728">Yes</span></span> |
| <span data-ttu-id="222f2-2729">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2729">password</span></span> |<span data-ttu-id="222f2-2730">Merhaba kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="222f2-2731">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2731">Yes</span></span> |
| <span data-ttu-id="222f2-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="222f2-2732">linkedServiceName</span></span> | <span data-ttu-id="222f2-2733">Hdınsight kümesi hello tarafından kullanılan hello toohello Azure blob depolama başvuruyor Azure Storage bağlı hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="222f2-2734">Şu anda bu özellik için bir Azure Data Lake Store bağlı belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="222f2-2735">Merhaba Hdınsight kümesine erişim toohello Data Lake Store varsa Hive/Pig komut dosyalarından hello Azure Data Lake Store verilerde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="222f2-2736">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2736">Yes</span></span> |

<span data-ttu-id="222f2-2737">Hdınsight kümeleri desteklenen sürümleri için bkz: [desteklenen Hdınsight sürümleri](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="222f2-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="222f2-2738">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="222f2-2739">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="222f2-2739">Azure Batch</span></span>
<span data-ttu-id="222f2-2740">Bir Azure Batch bağlantılı hizmet tooregister data factory ile sanal makineleri (VM'ler) Batch havuzu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="222f2-2741">.NET özel etkinlikler Azure Batch ya da Azure Hdınsight kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="222f2-2742">Çalıştırabilirsiniz bir [.NET özel etkinlik](#net-custom-activity) bu hizmeti bağlı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2743">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2743">Linked service</span></span>
<span data-ttu-id="222f2-2744">Aşağıdaki tablonun hello hello Azure JSON tanımında bağlı Azure Batch hizmetinin kullanılan hello özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="222f2-2745">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2745">Property</span></span> | <span data-ttu-id="222f2-2746">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2746">Description</span></span> | <span data-ttu-id="222f2-2747">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2748">type</span><span class="sxs-lookup"><span data-stu-id="222f2-2748">type</span></span> |<span data-ttu-id="222f2-2749">Merhaba type özelliği çok ayarlanmalıdır**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="222f2-2750">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2750">Yes</span></span> |
| <span data-ttu-id="222f2-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="222f2-2751">accountName</span></span> |<span data-ttu-id="222f2-2752">Hello Azure Batch hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="222f2-2753">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2753">Yes</span></span> |
| <span data-ttu-id="222f2-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="222f2-2754">accessKey</span></span> |<span data-ttu-id="222f2-2755">Hello Azure Batch hesabı için erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="222f2-2756">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2756">Yes</span></span> |
| <span data-ttu-id="222f2-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="222f2-2757">poolName</span></span> |<span data-ttu-id="222f2-2758">Sanal makinelerin hello havuzunun adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="222f2-2759">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2759">Yes</span></span> |
| <span data-ttu-id="222f2-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="222f2-2760">linkedServiceName</span></span> |<span data-ttu-id="222f2-2761">Hello Azure Storage bağlı hizmeti Azure bağlı Batch hizmeti ile ilişkili adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="222f2-2762">Bu bağlı hizmetin dosyaları hazırlama için kullanılan toorun hello etkinliği ve hello Etkinlik yürütme günlüklerini depolamak gerekli.</span><span class="sxs-lookup"><span data-stu-id="222f2-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="222f2-2763">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="222f2-2764">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="222f2-2765">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="222f2-2765">Azure Machine Learning</span></span>
<span data-ttu-id="222f2-2766">Bir Machine Learning toplu Puanlama uç noktası data factory ile bir Azure Machine Learning bağlantılı hizmet tooregister oluşturun.</span><span class="sxs-lookup"><span data-stu-id="222f2-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="222f2-2767">Bu bilgisayarda çalıştırabilir iki veri dönüştürme etkinlikleri bağlantılı hizmeti: [Machine Learning toplu iş yürütme etkinliği](#machine-learning-batch-execution-activity), [Machine Learning kaynak güncelleştirme etkinliği](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="222f2-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2768">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2768">Linked service</span></span>
<span data-ttu-id="222f2-2769">Aşağıdaki tablonun hello hello Azure JSON tanımında bağlı Azure Machine Learning hizmetinin kullanılan hello özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="222f2-2770">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2770">Property</span></span> | <span data-ttu-id="222f2-2771">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2771">Description</span></span> | <span data-ttu-id="222f2-2772">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2773">Tür</span><span class="sxs-lookup"><span data-stu-id="222f2-2773">Type</span></span> |<span data-ttu-id="222f2-2774">Merhaba type özelliği ayarlanmalıdır: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="222f2-2775">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2775">Yes</span></span> |
| <span data-ttu-id="222f2-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="222f2-2776">mlEndpoint</span></span> |<span data-ttu-id="222f2-2777">Merhaba toplu işlem Puanlama URL'sini.</span><span class="sxs-lookup"><span data-stu-id="222f2-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="222f2-2778">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2778">Yes</span></span> |
| <span data-ttu-id="222f2-2779">apikey ile yapılan</span><span class="sxs-lookup"><span data-stu-id="222f2-2779">apiKey</span></span> |<span data-ttu-id="222f2-2780">Merhaba, çalışma alanı modelinin API yayımladı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="222f2-2781">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="222f2-2782">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="222f2-2783">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="222f2-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="222f2-2784">Oluşturduğunuz bir **Azure Data Lake Analytics** bağlantılı hizmet toolink bir Azure Data Lake Analytics işlem hizmeti tooan Azure data factory hello kullanmadan önce [Data Lake Analytics U-SQL etkinliği](data-factory-usql-activity.md) ardışık düzeninde .</span><span class="sxs-lookup"><span data-stu-id="222f2-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="222f2-2785">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2785">Linked service</span></span>

<span data-ttu-id="222f2-2786">Aşağıdaki tablonun hello hello JSON tanımında bir Azure Data Lake Analytics bağlantılı hizmetinin kullanılan hello özellikleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="222f2-2787">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2787">Property</span></span> | <span data-ttu-id="222f2-2788">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2788">Description</span></span> | <span data-ttu-id="222f2-2789">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2790">Tür</span><span class="sxs-lookup"><span data-stu-id="222f2-2790">Type</span></span> |<span data-ttu-id="222f2-2791">Merhaba type özelliği ayarlanmalıdır: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="222f2-2792">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2792">Yes</span></span> |
| <span data-ttu-id="222f2-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="222f2-2793">accountName</span></span> |<span data-ttu-id="222f2-2794">Azure Data Lake Analytics hesap adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="222f2-2795">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2795">Yes</span></span> |
| <span data-ttu-id="222f2-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="222f2-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="222f2-2797">Azure Data Lake Analytics URI.</span><span class="sxs-lookup"><span data-stu-id="222f2-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="222f2-2798">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2798">No</span></span> |
| <span data-ttu-id="222f2-2799">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="222f2-2799">authorization</span></span> |<span data-ttu-id="222f2-2800">Yetkilendirme kodu, tıkladıktan sonra otomatik olarak alınır **Authorize** hello Data Factory düzenleyici ve Tamamlanıyor hello OAuth oturum açma düğmesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="222f2-2801">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2801">Yes</span></span> |
| <span data-ttu-id="222f2-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="222f2-2802">subscriptionId</span></span> |<span data-ttu-id="222f2-2803">Azure abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2803">Azure subscription id</span></span> |<span data-ttu-id="222f2-2804">Hayır (belirtilmezse, veri fabrikası kullanılan hello abonelik).</span><span class="sxs-lookup"><span data-stu-id="222f2-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="222f2-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="222f2-2805">resourceGroupName</span></span> |<span data-ttu-id="222f2-2806">Azure kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2806">Azure resource group name</span></span> |<span data-ttu-id="222f2-2807">Hayır (belirtilmezse, veri fabrikası kullanılan hello kaynak grubu).</span><span class="sxs-lookup"><span data-stu-id="222f2-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="222f2-2808">SessionID</span><span class="sxs-lookup"><span data-stu-id="222f2-2808">sessionId</span></span> |<span data-ttu-id="222f2-2809">Merhaba OAuth yetkilendirme oturumundan oturum kimliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="222f2-2810">Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="222f2-2811">Merhaba Data Factory Düzenleyici kullandığınızda, bu otomatik olarak oluşturulan kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="222f2-2812">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="222f2-2813">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2813">JSON example</span></span>
<span data-ttu-id="222f2-2814">Aşağıdaki örneğine hello JSON tanımı için bir Azure Data Lake Analytics bağlı hizmet sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="222f2-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="222f2-2815">Azure SQL Database</span></span>
<span data-ttu-id="222f2-2816">Azure SQL bağlı hizmeti oluşturma ve hello ile kullanma [saklı yordam etkinliği](#stored-procedure-activity) tooinvoke Data Factory işlem hattı bir saklı yordam.</span><span class="sxs-lookup"><span data-stu-id="222f2-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2817">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2817">Linked service</span></span>
<span data-ttu-id="222f2-2818">bir Azure SQL veritabanı toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDatabase**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2819">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2819">Property</span></span> | <span data-ttu-id="222f2-2820">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2820">Description</span></span> | <span data-ttu-id="222f2-2821">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-2822">connectionString</span></span> |<span data-ttu-id="222f2-2823">Tooconnect toohello Azure SQL veritabanı örneğinde hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="222f2-2824">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="222f2-2825">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2825">JSON example</span></span>

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

<span data-ttu-id="222f2-2826">Bkz: [Azure SQL Bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makale bu bağlı hizmetin hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="222f2-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="222f2-2827">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="222f2-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="222f2-2828">Bir Azure SQL Data Warehouse bağlı hizmet oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam.</span><span class="sxs-lookup"><span data-stu-id="222f2-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2829">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2829">Linked service</span></span>
<span data-ttu-id="222f2-2830">Azure SQL Data Warehouse toodefine bağlantılı hizmeti, kümesi hello **türü** Merhaba bağlantılı hizmetinin çok**AzureSqlDW**ve hello özelliklerinde aşağıdaki belirtin **typeProperties**bölümü:</span><span class="sxs-lookup"><span data-stu-id="222f2-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="222f2-2831">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2831">Property</span></span> | <span data-ttu-id="222f2-2832">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2832">Description</span></span> | <span data-ttu-id="222f2-2833">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-2834">connectionString</span></span> |<span data-ttu-id="222f2-2835">Tooconnect toohello Azure SQL Data Warehouse örneğine hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="222f2-2836">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="222f2-2837">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2837">JSON example</span></span>

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

<span data-ttu-id="222f2-2838">Daha fazla bilgi için bkz: [Azure SQL Data Warehouse Bağlayıcısı](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="222f2-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="222f2-2839">SQL Server</span></span> 
<span data-ttu-id="222f2-2840">Bir SQL Server bağlantılı hizmet oluşturma ve hello ile kullanma [saklı yordam etkinliği](data-factory-stored-proc-activity.md) tooinvoke Data Factory işlem hattı bir saklı yordam.</span><span class="sxs-lookup"><span data-stu-id="222f2-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="222f2-2841">Bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-2841">Linked service</span></span>
<span data-ttu-id="222f2-2842">Bağlı hizmet türü oluşturma **OnPremisesSqlServer** toolink bir şirket içi SQL Server veritabanı tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="222f2-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="222f2-2843">Aşağıdaki tablonun hello JSON öğeleri belirli tooon şirket içi SQL Server bağlantılı hizmet açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="222f2-2844">Aşağıdaki tablonun hello JSON öğeleri belirli tooSQL Server bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="222f2-2845">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2845">Property</span></span> | <span data-ttu-id="222f2-2846">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2846">Description</span></span> | <span data-ttu-id="222f2-2847">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2848">type</span><span class="sxs-lookup"><span data-stu-id="222f2-2848">type</span></span> |<span data-ttu-id="222f2-2849">Merhaba type özelliği ayarlanmalıdır: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="222f2-2850">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2850">Yes</span></span> |
| <span data-ttu-id="222f2-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="222f2-2851">connectionString</span></span> |<span data-ttu-id="222f2-2852">SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak tooconnect toohello şirket içi SQL Server veritabanı gerekli connectionString bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="222f2-2853">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2853">Yes</span></span> |
| <span data-ttu-id="222f2-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="222f2-2854">gatewayName</span></span> |<span data-ttu-id="222f2-2855">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SQL Server veritabanını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="222f2-2856">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2856">Yes</span></span> |
| <span data-ttu-id="222f2-2857">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="222f2-2857">username</span></span> |<span data-ttu-id="222f2-2858">Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="222f2-2859">Örnek: **domainname\\kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="222f2-2860">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2860">No</span></span> |
| <span data-ttu-id="222f2-2861">password</span><span class="sxs-lookup"><span data-stu-id="222f2-2861">password</span></span> |<span data-ttu-id="222f2-2862">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="222f2-2863">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2863">No</span></span> |

<span data-ttu-id="222f2-2864">Hello kullanarak kimlik bilgilerini şifrelemek **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları hello aşağıdaki örnekte gösterildiği gibi hello bağlantı dizesinde kullanabilirsiniz (**EncryptedCredential** özellik):</span><span class="sxs-lookup"><span data-stu-id="222f2-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="222f2-2865">Örnek: SQL kimlik doğrulaması kullanmak için JSON</span><span class="sxs-lookup"><span data-stu-id="222f2-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="222f2-2866">Örnek: JSON'ı Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="222f2-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="222f2-2867">Kullanıcı adı ve parolası belirtilmişse, ağ geçidi bunları tooimpersonate hello kullanır belirtilen kullanıcı hesabı tooconnect toohello şirket içi SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="222f2-2868">Aksi takdirde, ağ geçidi toohello SQL Server doğrudan hello güvenlik bağlamında ağ geçidi (kendi başlangıç hesabı) ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="222f2-2869">Daha fazla bilgi için bkz: [SQL Server Bağlayıcısı](data-factory-sqlserver-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="222f2-2870">VERİ DÖNÜŞTÜRME ETKİNLİKLERİ</span><span class="sxs-lookup"><span data-stu-id="222f2-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="222f2-2871">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="222f2-2871">Activity</span></span> | <span data-ttu-id="222f2-2872">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="222f2-2873">Hdınsight Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="222f2-2874">Merhaba Data Factory işlem hattı Hdınsight Hive etkinliğiyle kendi Hive sorguları ya da isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="222f2-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="222f2-2875">Hdınsight Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="222f2-2876">Merhaba Data Factory işlem hattı Hdınsight Pig etkinlik kendi Pig sorgular veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="222f2-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="222f2-2877">HDInsight MapReduce Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="222f2-2878">Merhaba Data Factory işlem hattı Hdınsight MapReduce etkinlik kendi MapReduce programları veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="222f2-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="222f2-2879">HDInsight Akış Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="222f2-2880">Data Factory işlem hattı Hello Hdınsight akış etkinliği Hadoop akış programlar kendi veya isteğe bağlı Windows/Linux tabanlı Hdınsight kümesi yürütür.</span><span class="sxs-lookup"><span data-stu-id="222f2-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="222f2-2881">HDInsight Spark Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="222f2-2882">Merhaba Data Factory işlem hattı Hdınsight Spark etkinliğinde Spark programlar kendi Hdınsight kümesinde yürütür.</span><span class="sxs-lookup"><span data-stu-id="222f2-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="222f2-2883">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="222f2-2884">Web hizmeti Tahmine dayalı analiz için azure Data Factory etkinleştirir, tooeasily yayımlanan bir Azure Machine Learning kullanan komut zincirleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="222f2-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="222f2-2885">Bir Azure Data Factory işlem hattı toplu iş yürütme etkinliği Hello kullanarak, Machine Learning web hizmeti toomake tahminleri toplu hello veriler üzerinde çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="222f2-2886">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="222f2-2887">Zaman içinde veri kümeleri hello Machine Learning Puanlama denemeler retrained toobe yeni kullanarak gereken Tahmine dayalı modelleri hello girin.</span><span class="sxs-lookup"><span data-stu-id="222f2-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="222f2-2888">Yeniden eğitme ile tamamladıktan sonra web hizmeti ile Merhaba Puanlama tooupdate hello Machine Learning modelini retrained istiyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="222f2-2889">Merhaba kaynak güncelleştirme etkinliği tooupdate hello web hizmeti ile Merhaba yeni eğitilmiş model kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="222f2-2890">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="222f2-2891">Data Factory işlem hattı tooinvoke bir saklı yordam veri depolarına aşağıdaki hello birinde hello saklı yordam etkinliği kullanabilirsiniz: Azure SQL Database, Azure SQL Data Warehouse, SQL Server veritabanı kuruluşunuzdaki veya bir Azure VM.</span><span class="sxs-lookup"><span data-stu-id="222f2-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="222f2-2892">Data Lake Analytics U-SQL etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="222f2-2893">Data Lake Analytics U-SQL etkinliği Azure Data Lake Analytics kümede bir U-SQL komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="222f2-2894">.NET özel etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="222f2-2895">Tootransform verileri Data Factory tarafından desteklenmeyen bir şekilde ihtiyacınız varsa, kendi veri işleme mantığı ile özel bir etkinlik oluşturmak ve hello ardışık düzeninde hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="222f2-2896">Bir Azure Batch hizmeti ya da Azure Hdınsight kümesi kullanarak hello özel .NET etkinliği toorun yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="222f2-2897">HDInsight Hive Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="222f2-2898">Aşağıdaki özelliklere Hive etkinliği JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="222f2-2899">Merhaba type özelliği hello etkinliğinin olmalıdır: **Hdınsighthive**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="222f2-2900">Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-2901">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightHive hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="222f2-2902">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2902">Property</span></span> | <span data-ttu-id="222f2-2903">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2903">Description</span></span> | <span data-ttu-id="222f2-2904">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2905">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="222f2-2905">script</span></span> |<span data-ttu-id="222f2-2906">Merhaba Hive betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="222f2-2907">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2907">No</span></span> |
| <span data-ttu-id="222f2-2908">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="222f2-2908">script path</span></span> |<span data-ttu-id="222f2-2909">Mağaza hello Hive betiği bir Azure blob depolama alanındaki ve hello yol toohello dosyası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="222f2-2910">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="222f2-2911">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2911">Both cannot be used together.</span></span> <span data-ttu-id="222f2-2912">Merhaba dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="222f2-2913">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2913">No</span></span> |
| <span data-ttu-id="222f2-2914">tanımlar</span><span class="sxs-lookup"><span data-stu-id="222f2-2914">defines</span></span> |<span data-ttu-id="222f2-2915">İçinde hello Hive betiği 'hiveconf' kullanarak başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="222f2-2916">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2916">No</span></span> |

<span data-ttu-id="222f2-2917">Bu tür belirli toohello Hive etkinliği özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="222f2-2918">Diğer özellikleri (Merhaba typeProperties bölüm dışında) tüm etkinlikler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="222f2-2919">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2919">JSON example</span></span>
<span data-ttu-id="222f2-2920">JSON aşağıdaki hello Hdınsight Hive etkinliği ardışık düzeninde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="222f2-2921">Daha fazla bilgi için bkz: [Hive etkinliği](data-factory-hive-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="222f2-2922">HDInsight Pig Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="222f2-2923">Aşağıdaki özelliklere Pig etkinlik JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="222f2-2924">Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="222f2-2925">Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-2926">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightPig hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="222f2-2927">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2927">Property</span></span> | <span data-ttu-id="222f2-2928">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2928">Description</span></span> | <span data-ttu-id="222f2-2929">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2930">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="222f2-2930">script</span></span> |<span data-ttu-id="222f2-2931">Merhaba Pig betiği satır içi belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="222f2-2932">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2932">No</span></span> |
| <span data-ttu-id="222f2-2933">komut dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="222f2-2933">script path</span></span> |<span data-ttu-id="222f2-2934">Bir Azure blob depolama alanına Hello Pig betiği depolar ve hello yol toohello dosyası sağlayın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="222f2-2935">'Komut dosyası' veya 'scriptPath' özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="222f2-2936">Her ikisi birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2936">Both cannot be used together.</span></span> <span data-ttu-id="222f2-2937">Merhaba dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="222f2-2938">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2938">No</span></span> |
| <span data-ttu-id="222f2-2939">tanımlar</span><span class="sxs-lookup"><span data-stu-id="222f2-2939">defines</span></span> |<span data-ttu-id="222f2-2940">Pig betiği hello içinde başvurmak için anahtar/değer çiftleri olarak parametrelerini belirtin</span><span class="sxs-lookup"><span data-stu-id="222f2-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="222f2-2941">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2941">No</span></span> |

<span data-ttu-id="222f2-2942">Bu tür belirli toohello Pig etkinlik özellikleridir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="222f2-2943">Diğer özellikleri (Merhaba typeProperties bölüm dışında) tüm etkinlikler için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="222f2-2944">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2944">JSON example</span></span>

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

<span data-ttu-id="222f2-2945">Daha fazla bilgi için bkz: [Pig etkinlik](#data-factory-pig-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="222f2-2946">HDInsight MapReduce Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="222f2-2947">Aşağıdaki özelliklere MapReduce etkinliği JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="222f2-2948">Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="222f2-2949">Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-2950">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightMapReduce hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="222f2-2951">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2951">Property</span></span> | <span data-ttu-id="222f2-2952">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2952">Description</span></span> | <span data-ttu-id="222f2-2953">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="222f2-2954">jarLinkedService</span></span> | <span data-ttu-id="222f2-2955">Merhaba adını hizmeti hello hello JAR dosyasını içeren Azure Storage için bağlı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="222f2-2956">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2956">Yes</span></span> |
| <span data-ttu-id="222f2-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="222f2-2957">jarFilePath</span></span> | <span data-ttu-id="222f2-2958">Yol toohello JAR dosyasını hello Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="222f2-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="222f2-2959">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2959">Yes</span></span> | 
| <span data-ttu-id="222f2-2960">className</span><span class="sxs-lookup"><span data-stu-id="222f2-2960">className</span></span> | <span data-ttu-id="222f2-2961">Merhaba JAR dosyasına hello Ana sınıfın adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="222f2-2962">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-2962">Yes</span></span> | 
| <span data-ttu-id="222f2-2963">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="222f2-2963">arguments</span></span> | <span data-ttu-id="222f2-2964">Bağımsız değişkenleri hello MapReduce program virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="222f2-2965">Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) hello MapReduce çerçeveden.</span><span class="sxs-lookup"><span data-stu-id="222f2-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="222f2-2966">toodifferentiate, hello MapReduce bağımsız değişkenleriyle seçeneği ve değer bağımsız değişken olarak hello aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. olan göre bunların değerleri hemen ardından seçenekleri)</span><span class="sxs-lookup"><span data-stu-id="222f2-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="222f2-2967">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="222f2-2968">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="222f2-2969">Daha fazla bilgi için bkz: [MapReduce etkinliği](data-factory-map-reduce.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="222f2-2970">HDInsight Akış Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="222f2-2971">Aşağıdaki özelliklere Hadoop akış etkinliği JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="222f2-2972">Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="222f2-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="222f2-2973">Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-2974">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightStreaming hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="222f2-2975">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-2975">Property</span></span> | <span data-ttu-id="222f2-2976">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="222f2-2977">Eşleyici</span><span class="sxs-lookup"><span data-stu-id="222f2-2977">mapper</span></span> | <span data-ttu-id="222f2-2978">Merhaba Eşleyici yürütülebilir adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="222f2-2979">Merhaba örnekte cat.exe hello Eşleyici yürütülebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="222f2-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="222f2-2980">reducer</span></span> | <span data-ttu-id="222f2-2981">Merhaba reducer yürütülebilir adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="222f2-2982">Merhaba örnekte wc.exe hello reducer yürütülebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="222f2-2983">Giriş</span><span class="sxs-lookup"><span data-stu-id="222f2-2983">input</span></span> | <span data-ttu-id="222f2-2984">Merhaba Eşleyici için giriş dosyası (konum dahil).</span><span class="sxs-lookup"><span data-stu-id="222f2-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="222f2-2985">Merhaba örnekte: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample hello blob kapsayıcısı, veri/örnek/Gutenberg hello klasördür ve davinci.txt hello blob.</span><span class="sxs-lookup"><span data-stu-id="222f2-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="222f2-2986">Çıktı</span><span class="sxs-lookup"><span data-stu-id="222f2-2986">output</span></span> | <span data-ttu-id="222f2-2987">Merhaba reducer için (konum dahil) çıktı dosyası.</span><span class="sxs-lookup"><span data-stu-id="222f2-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="222f2-2988">Merhaba çıktısı hello Hadoop akış işi, bu özelliği için belirtilen toohello konumu yazılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="222f2-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="222f2-2989">filePaths</span></span> | <span data-ttu-id="222f2-2990">Merhaba Eşleyici ve reducer yürütülebilir dosyalar için yollar.</span><span class="sxs-lookup"><span data-stu-id="222f2-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="222f2-2991">Merhaba örnekte: "adfsample/example/apps/wc.exe" adfsample hello blob kapsayıcısı, örnek/uygulamaları hello klasördür ve wc.exe hello çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="222f2-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="222f2-2992">fileLinkedService</span></span> | <span data-ttu-id="222f2-2993">Merhaba hello filePaths bölümünde belirtilen hello dosyaları içeren Azure depolama temsil eden azure depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="222f2-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="222f2-2994">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="222f2-2994">arguments</span></span> | <span data-ttu-id="222f2-2995">Bağımsız değişkenleri hello MapReduce program virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="222f2-2996">Çalışma zamanında gördüğünüz birkaç ek bağımsız değişkenler (örneğin: mapreduce.job.tags) hello MapReduce çerçeveden.</span><span class="sxs-lookup"><span data-stu-id="222f2-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="222f2-2997">toodifferentiate, hello MapReduce bağımsız değişkenleriyle seçeneği ve değer bağımsız değişken olarak hello aşağıdaki örnekte gösterildiği gibi kullanmayı düşünün (- s,--giriş,--çıkış vb. olan göre bunların değerleri hemen ardından seçenekleri)</span><span class="sxs-lookup"><span data-stu-id="222f2-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="222f2-2998">Getdebugınfo</span><span class="sxs-lookup"><span data-stu-id="222f2-2998">getDebugInfo</span></span> | <span data-ttu-id="222f2-2999">İsteğe bağlı bir öğe.</span><span class="sxs-lookup"><span data-stu-id="222f2-2999">An optional element.</span></span> <span data-ttu-id="222f2-3000">TooFailure ayarlandığında hello günlükleri yalnızca hatada indirilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="222f2-3001">TooAll ayarlandığında, günlükleri hello yürütme durumu bağımsız olarak daima yüklenir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="222f2-3002">Bir çıkış veri kümesi için Hadoop akış etkinliği Merhaba hello belirtmelisiniz **çıkarır** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="222f2-3003">Bu veri kümesi yalnızca gerekli toodrive hello ardışık düzen zamanlaması (saatlik, günlük, vs.) bir kukla dataset olabilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="222f2-3004">Merhaba etkinliği bir girdi almazsa hello hello etkinliği bir girdi veri kümesi belirtme atlayabilirsiniz **girişleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="222f2-3005">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3005">JSON example</span></span>

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

<span data-ttu-id="222f2-3006">Daha fazla bilgi için bkz: [Hadoop akış etkinliği](data-factory-hadoop-streaming-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="222f2-3007">HDInsight Spark Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="222f2-3008">Aşağıdaki özelliklere Spark etkinlik JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="222f2-3009">Merhaba type özelliği hello etkinliğinin olmalıdır: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="222f2-3010">Hdınsight bağlı hizmeti ilk oluşturun ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-3011">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooHDInsightSpark hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="222f2-3012">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-3012">Property</span></span> | <span data-ttu-id="222f2-3013">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-3013">Description</span></span> | <span data-ttu-id="222f2-3014">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="222f2-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="222f2-3015">rootPath</span></span> | <span data-ttu-id="222f2-3016">Hello Azure Blob kapsayıcısı ve hello Spark dosyasını içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="222f2-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="222f2-3017">Merhaba dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="222f2-3018">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3018">Yes</span></span> |
| <span data-ttu-id="222f2-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="222f2-3019">entryFilePath</span></span> | <span data-ttu-id="222f2-3020">Göreli yol toohello kök klasöründe hello Spark kod/paketi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="222f2-3021">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3021">Yes</span></span> |
| <span data-ttu-id="222f2-3022">className</span><span class="sxs-lookup"><span data-stu-id="222f2-3022">className</span></span> | <span data-ttu-id="222f2-3023">Uygulamanın Java/Spark ana sınıfı</span><span class="sxs-lookup"><span data-stu-id="222f2-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="222f2-3024">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3024">No</span></span> | 
| <span data-ttu-id="222f2-3025">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="222f2-3025">arguments</span></span> | <span data-ttu-id="222f2-3026">Komut satırı bağımsız değişkenleri toohello Spark program listesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="222f2-3027">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3027">No</span></span> | 
| <span data-ttu-id="222f2-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="222f2-3028">proxyUser</span></span> | <span data-ttu-id="222f2-3029">Merhaba kullanıcı hesabı tooimpersonate tooexecute hello Spark programı</span><span class="sxs-lookup"><span data-stu-id="222f2-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="222f2-3030">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3030">No</span></span> | 
| <span data-ttu-id="222f2-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="222f2-3031">sparkConfig</span></span> | <span data-ttu-id="222f2-3032">Spark yapılandırma özellikleri.</span><span class="sxs-lookup"><span data-stu-id="222f2-3032">Spark configuration properties.</span></span> | <span data-ttu-id="222f2-3033">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3033">No</span></span> | 
| <span data-ttu-id="222f2-3034">Getdebugınfo</span><span class="sxs-lookup"><span data-stu-id="222f2-3034">getDebugInfo</span></span> | <span data-ttu-id="222f2-3035">Merhaba Spark günlük dosyalarını kopyalanan toohello Hdınsight küme tarafından kullanılan Azure depolama olduğunda belirtir (veya) sparkJobLinkedService tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="222f2-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="222f2-3036">İzin verilen değerler: None, her zaman veya hata.</span><span class="sxs-lookup"><span data-stu-id="222f2-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="222f2-3037">Varsayılan değer: yok.</span><span class="sxs-lookup"><span data-stu-id="222f2-3037">Default value: None.</span></span> | <span data-ttu-id="222f2-3038">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3038">No</span></span> | 
| <span data-ttu-id="222f2-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="222f2-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="222f2-3040">Merhaba hello Spark iş dosyası, bağımlılıklar ve günlükleri tutan Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="222f2-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="222f2-3041">Bu özellik için bir değer belirtmezseniz, Hdınsight kümesi ile ilişkili hello depolama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="222f2-3042">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="222f2-3043">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3043">JSON example</span></span>

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
<span data-ttu-id="222f2-3044">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="222f2-3044">Note hello following points:</span></span> 

- <span data-ttu-id="222f2-3045">Merhaba **türü** özelliği çok ayarlanmış**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="222f2-3046">Merhaba **rootPath** çok ayarlanır**adfspark\\pyFiles** adfspark hello Azure Blob kapsayıcısı ve pyFiles olduğu ince kapsayıcıdaki klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="222f2-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="222f2-3047">Bu örnekte, hello Azure Blob Storage hello hello Spark kümesi ile ilişkili olan bir ' dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="222f2-3048">Merhaba dosya tooa yükleyebilirsiniz farklı Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="222f2-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="222f2-3049">Bunu yaparsanız, bir Azure Storage bağlı hizmeti toolink bu depolama hesabı toohello veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="222f2-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="222f2-3050">Ardından, hello için bir değer olarak hello hello bağlı hizmetin adını belirtin **sparkJobLinkedService** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="222f2-3051">Bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bu özellik ve Spark etkinlik hello tarafından desteklenen diğer özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="222f2-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="222f2-3052">Merhaba **entryFilePath** toohello ayarlamak **test.py**, hello python dosyası değil.</span><span class="sxs-lookup"><span data-stu-id="222f2-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="222f2-3053">Merhaba **Getdebugınfo** özelliği çok ayarlanmış**her zaman**, yani hello günlük dosyaları her zaman oluşturulan (başarılı veya başarısız).</span><span class="sxs-lookup"><span data-stu-id="222f2-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="222f2-3054">Bir sorun giderme amacıyla sürece bu özellik tooAlways'ı bir üretim ortamında ayarlamayın öneririz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="222f2-3055">Merhaba **çıkarır** bölümü bir çıkış veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="222f2-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="222f2-3056">Merhaba spark program herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="222f2-3057">Merhaba çıkış veri kümesi sürücüleri hello zamanlama hello ardışık düzen (saatlik, günlük, vs.).</span><span class="sxs-lookup"><span data-stu-id="222f2-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="222f2-3058">Merhaba etkinliği hakkında daha fazla bilgi için bkz: [Spark etkinlik](data-factory-spark.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="222f2-3059">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="222f2-3060">Aşağıdaki özelliklere Azure ML toplu iş yürütme etkinliği JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="222f2-3061">Merhaba type özelliği hello etkinliğinin olmalıdır: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="222f2-3062">Bağlantılı hizmet ilk öğrenme Azure bir makine oluşturma ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-3063">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooAzureMLBatchExecution hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="222f2-3064">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-3064">Property</span></span> | <span data-ttu-id="222f2-3065">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-3065">Description</span></span> | <span data-ttu-id="222f2-3066">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="222f2-3067">WebServiceInput etkinliğine</span><span class="sxs-lookup"><span data-stu-id="222f2-3067">webServiceInput</span></span> | <span data-ttu-id="222f2-3068">hello Azure ML web hizmeti için bir giriş olarak Hello dataset toobe geçirildi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="222f2-3069">Bu veri kümesi de hello girişleri hello etkinliğinin bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="222f2-3070">WebServiceInput etkinliğine veya webServiceInputs kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="222f2-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="222f2-3071">webServiceInputs</span></span> | <span data-ttu-id="222f2-3072">Veri kümeleri toobe hello Azure ML web hizmeti için girdi olarak geçirilen belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="222f2-3073">Merhaba web hizmeti birden fazla girdi aldığı durumlarda hello WebServiceInput etkinliğine özelliğini kullanmak yerine hello webServiceInputs özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="222f2-3074">Merhaba tarafından başvurulan veri kümeleri **webServiceInputs** hello etkinliği de dahil edilmesi **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="222f2-3075">WebServiceInput etkinliğine veya webServiceInputs kullanın.</span><span class="sxs-lookup"><span data-stu-id="222f2-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="222f2-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="222f2-3076">webServiceOutputs</span></span> | <span data-ttu-id="222f2-3077">Çıktı hello Azure ML web hizmeti olarak atanan hello veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="222f2-3078">Hello web hizmeti, bu veri kümesini çıktı verilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="222f2-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="222f2-3079">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3079">Yes</span></span> | 
<span data-ttu-id="222f2-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-3080">globalParameters</span></span> | <span data-ttu-id="222f2-3081">Bu bölümde hello web hizmeti parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="222f2-3082">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="222f2-3083">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3083">JSON example</span></span>
<span data-ttu-id="222f2-3084">Bu örnekte, hello etkinlik hello dataset sahip **MLSqlInput** giriş olarak ve **MLSqlOutput** hello çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="222f2-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="222f2-3085">Merhaba **MLSqlInput** hello kullanılarak geçirilen bir giriş toohello web hizmeti tarafından olarak **WebServiceInput etkinliğine** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="222f2-3086">Merhaba **MLSqlOutput** hello kullanılarak geçirilen bir çıktı toohello Web hizmeti tarafından olarak **webServiceOutputs** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="222f2-3087">Merhaba JSON örnekte hello Azure Machine Learning hizmetinin kullandığı bir okuyucu ve yazıcı modülü tooread/yazma verilerden Web dağıtılan / tooan Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="222f2-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="222f2-3088">Bu Web hizmetini şu dört parametreler hello sunar: veritabanı sunucu adı, veritabanı adı, sunucu kullanıcı hesabı adı ve sunucu kullanıcı hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="222f2-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="222f2-3089">Yalnızca girişleri ve çıkışları hello AzureMLBatchExecution etkinlik parametreleri toohello Web hizmeti geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="222f2-3090">Örneğin, yukarıdaki JSON parçacığı hello MLSqlInput bir giriş toohello WebServiceInput etkinliğine parametresi ile bir giriş toohello Web hizmeti geçirilen AzureMLBatchExecution etkinlik ' dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="222f2-3091">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="222f2-3092">Aşağıdaki özelliklere Azure ML güncelleştirme kaynak etkinliği JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="222f2-3093">Merhaba type özelliği hello etkinliğinin olmalıdır: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="222f2-3094">Bağlantılı hizmet ilk öğrenme Azure bir makine oluşturma ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-3095">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooAzureMLUpdateResource hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="222f2-3096">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-3096">Property</span></span> | <span data-ttu-id="222f2-3097">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-3097">Description</span></span> | <span data-ttu-id="222f2-3098">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="222f2-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="222f2-3099">trainedModelName</span></span> | <span data-ttu-id="222f2-3100">Merhaba adını modeli retrained.</span><span class="sxs-lookup"><span data-stu-id="222f2-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="222f2-3101">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3101">Yes</span></span> |  
<span data-ttu-id="222f2-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="222f2-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="222f2-3103">İşlemi yeniden eğitme hello tarafından döndürülen veri kümesi işaret toohello iLearner dosya.</span><span class="sxs-lookup"><span data-stu-id="222f2-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="222f2-3104">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="222f2-3105">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3105">JSON example</span></span>
<span data-ttu-id="222f2-3106">Merhaba işlem hattına sahip iki etkinlik: **AzureMLBatchExecution** ve **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="222f2-3107">Hello Azure ML toplu iş yürütme etkinliği hello eğitim veri giriş olarak alır ve bir iLearner dosya bir çıktı olarak üretir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="222f2-3108">Merhaba etkinlik verileri eğitim hello girişle hello eğitim web hizmeti (web hizmeti olarak sunulan eğitim denemenizi) çağırır ve hello webservice hello ilearner dosya alır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="222f2-3109">Merhaba placeholderBlob hello Azure Data Factory hizmeti toorun hello ardışık düzen tarafından gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="222f2-3110">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="222f2-3111">Aşağıdaki U-SQL etkinliği JSON tanımında özelliklere hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="222f2-3112">Merhaba type özelliği hello etkinliğinin olmalıdır: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="222f2-3113">Bir Azure Data Lake Analytics bağlı hizmeti oluşturma ve hello için bir değer olarak hello adını belirtmeniz gerekir **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-3114">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooDataLakeAnalyticsU-SQL hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="222f2-3115">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-3115">Property</span></span> | <span data-ttu-id="222f2-3116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-3116">Description</span></span> | <span data-ttu-id="222f2-3117">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="222f2-3118">scriptPath</span></span> |<span data-ttu-id="222f2-3119">Merhaba U-SQL betiğini içeren yolu toofolder.</span><span class="sxs-lookup"><span data-stu-id="222f2-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="222f2-3120">Merhaba dosyasının adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="222f2-3121">Hayır (komut dosyası kullanırsanız)</span><span class="sxs-lookup"><span data-stu-id="222f2-3121">No (if you use script)</span></span> |
| <span data-ttu-id="222f2-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="222f2-3122">scriptLinkedService</span></span> |<span data-ttu-id="222f2-3123">Merhaba betik toohello veri fabrikası içeren hello depolamayı bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="222f2-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="222f2-3124">Hayır (komut dosyası kullanırsanız)</span><span class="sxs-lookup"><span data-stu-id="222f2-3124">No (if you use script)</span></span> |
| <span data-ttu-id="222f2-3125">Komut dosyası</span><span class="sxs-lookup"><span data-stu-id="222f2-3125">script</span></span> |<span data-ttu-id="222f2-3126">ScriptPath ve scriptLinkedService belirtme yerine satır içi betiği belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="222f2-3127">Örneğin: "komut dosyası": "Veritabanı oluştur test".</span><span class="sxs-lookup"><span data-stu-id="222f2-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="222f2-3128">Hayır (scriptPath ve scriptLinkedService kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="222f2-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="222f2-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="222f2-3129">degreeOfParallelism</span></span> |<span data-ttu-id="222f2-3130">Merhaba en fazla düğüm sayısını toorun hello işi aynı anda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="222f2-3131">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3131">No</span></span> |
| <span data-ttu-id="222f2-3132">Öncelik</span><span class="sxs-lookup"><span data-stu-id="222f2-3132">priority</span></span> |<span data-ttu-id="222f2-3133">Sıraya alınan tüm işlerden seçili toorun olması gereken ilk belirler.</span><span class="sxs-lookup"><span data-stu-id="222f2-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="222f2-3134">Merhaba alt hello numarası hello yüksek hello önceliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="222f2-3135">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3135">No</span></span> |
| <span data-ttu-id="222f2-3136">parametreler</span><span class="sxs-lookup"><span data-stu-id="222f2-3136">parameters</span></span> |<span data-ttu-id="222f2-3137">Merhaba U-SQL komut dosyası için parametreler</span><span class="sxs-lookup"><span data-stu-id="222f2-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="222f2-3138">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="222f2-3139">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3139">JSON example</span></span>

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

<span data-ttu-id="222f2-3140">Daha fazla bilgi için bkz: [Data Lake Analytics U-SQL etkinliği](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="222f2-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="222f2-3141">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="222f2-3142">Aşağıdaki özelliklere saklı yordam etkinliği JSON tanımında hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="222f2-3143">Merhaba type özelliği hello etkinliğinin olmalıdır: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="222f2-3144">Bir bağlı hizmetler aşağıdaki hello birini oluşturun ve hello için bir değer olarak hello hello bağlı hizmet adını belirtmeniz gerekir **linkedServiceName** özelliği:</span><span class="sxs-lookup"><span data-stu-id="222f2-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="222f2-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="222f2-3145">SQL Server</span></span> 
- <span data-ttu-id="222f2-3146">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="222f2-3146">Azure SQL Database</span></span>
- <span data-ttu-id="222f2-3147">Azure SQL Veri Ambarı</span><span class="sxs-lookup"><span data-stu-id="222f2-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="222f2-3148">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooSqlServerStoredProcedure hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="222f2-3149">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-3149">Property</span></span> | <span data-ttu-id="222f2-3150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-3150">Description</span></span> | <span data-ttu-id="222f2-3151">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="222f2-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="222f2-3152">storedProcedureName</span></span> |<span data-ttu-id="222f2-3153">Hello Azure SQL veritabanı veya çıktı tablosu kullanır hello hello bağlantılı hizmeti tarafından temsil edilen Azure SQL Data Warehouse hello saklı yordamı Hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="222f2-3154">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3154">Yes</span></span> |
| <span data-ttu-id="222f2-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="222f2-3155">storedProcedureParameters</span></span> |<span data-ttu-id="222f2-3156">Saklı yordam parametreleri için değerleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="222f2-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="222f2-3157">Toopass parametresi için null ihtiyacınız varsa, hello sözdizimini kullanın: "param1": null (tüm küçük harf).</span><span class="sxs-lookup"><span data-stu-id="222f2-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="222f2-3158">Bu özellik kullanma hakkında örnek toolearn aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="222f2-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="222f2-3159">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3159">No</span></span> |

<span data-ttu-id="222f2-3160">Bir giriş veri kümesi belirtirseniz, ('Hazır' durumunda) kullanılabilir olmalıdır Merhaba depolanan yordam etkinliği toorun.</span><span class="sxs-lookup"><span data-stu-id="222f2-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="222f2-3161">Merhaba girdi veri kümesi hello saklı yordama parametre olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="222f2-3162">Başlangıç hello saklı yordam etkinliği önce yalnızca kullanılan toocheck hello bağımlılık vardır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="222f2-3163">Bir çıkış veri kümesi için bir saklı yordam etkinliği belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="222f2-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="222f2-3164">Çıktı veri kümesi belirtir hello **zamanlama** hello için saklı yordam etkinliği (saatlik, haftalık, aylık, vb.).</span><span class="sxs-lookup"><span data-stu-id="222f2-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="222f2-3165">Merhaba çıktı veri kümesi kullanmalısınız bir **bağlantılı hizmeti** tooan Azure SQL Database veya bir Azure SQL Data Warehouse veya SQL Server veritabanı istediğiniz saklı yordam toorun hello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="222f2-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="222f2-3166">Merhaba çıktı veri kümesi hello saklı yordamın sonraki işleme biçimini toopass hello sonuç olarak başka bir etkinlik tarafından kullanılabileceği ([etkinlikleri zincirleme](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) hello ardışık düzeninde.</span><span class="sxs-lookup"><span data-stu-id="222f2-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="222f2-3167">Ancak, veri fabrikası otomatik olarak bir saklı yordam toothis dataset hello çıktısını yazmaz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="222f2-3168">Bu, çıktı veri kümesi noktalarına hello o yazma tooa SQL tablosu hello saklı yordamı olur.</span><span class="sxs-lookup"><span data-stu-id="222f2-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="222f2-3169">Bazı durumlarda, hello çıktı veri kümesi olabilir bir **kukla dataset**, toospecify hello zamanlama hello çalıştırmak için depolanan yordam etkinliği yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="222f2-3170">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3170">JSON example</span></span>

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

<span data-ttu-id="222f2-3171">Daha fazla bilgi için bkz: [saklı yordam etkinliği](data-factory-stored-proc-activity.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="222f2-3172">.NET özel etkinliği</span><span class="sxs-lookup"><span data-stu-id="222f2-3172">.NET custom activity</span></span>
<span data-ttu-id="222f2-3173">.NET özel etkinlik JSON tanımını özelliklerinde aşağıdaki hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="222f2-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="222f2-3174">Merhaba type özelliği hello etkinliğinin olmalıdır: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="222f2-3175">Azure Hdınsight bağlı hizmeti oluşturmak veya bağlı bir Azure Batch hizmeti ve hello için bir değer olarak hello hello bağlı hizmet adını belirtin **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="222f2-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="222f2-3176">Merhaba aşağıdaki özellikleri hello desteklenir **typeProperties** bölümünde etkinlik tooDotNetActivity hello türü ayarladığınızda:</span><span class="sxs-lookup"><span data-stu-id="222f2-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="222f2-3177">Özellik</span><span class="sxs-lookup"><span data-stu-id="222f2-3177">Property</span></span> | <span data-ttu-id="222f2-3178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="222f2-3178">Description</span></span> | <span data-ttu-id="222f2-3179">Gerekli</span><span class="sxs-lookup"><span data-stu-id="222f2-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="222f2-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="222f2-3180">AssemblyName</span></span> | <span data-ttu-id="222f2-3181">Merhaba derlemesinin adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-3181">Name of hello assembly.</span></span> <span data-ttu-id="222f2-3182">Merhaba örnek,: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="222f2-3183">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3183">Yes</span></span> |
| <span data-ttu-id="222f2-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="222f2-3184">EntryPoint</span></span> |<span data-ttu-id="222f2-3185">Merhaba IDotNetActivity arabirimini uygulayan hello sınıfının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="222f2-3186">Merhaba örnek,: **MyDotNetActivityNS.MyDotNetActivity** burada MyDotNetActivityNS hello ad alanı ve MyDotNetActivity hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="222f2-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="222f2-3187">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3187">Yes</span></span> | 
| <span data-ttu-id="222f2-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="222f2-3188">PackageLinkedService</span></span> | <span data-ttu-id="222f2-3189">Merhaba hello özel etkinlik zip dosyasını içeren toohello blob depolama işaret Azure Storage bağlı hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="222f2-3190">Merhaba örnek,: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="222f2-3191">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3191">Yes</span></span> |
| <span data-ttu-id="222f2-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="222f2-3192">PackageFile</span></span> | <span data-ttu-id="222f2-3193">Merhaba ZIP dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="222f2-3193">Name of hello zip file.</span></span> <span data-ttu-id="222f2-3194">Merhaba örnek,: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="222f2-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="222f2-3195">Evet</span><span class="sxs-lookup"><span data-stu-id="222f2-3195">Yes</span></span> |
| <span data-ttu-id="222f2-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="222f2-3196">extendedProperties</span></span> | <span data-ttu-id="222f2-3197">Tanımlayın ve toohello .NET kodu geçirin genişletilmiş özellikler.</span><span class="sxs-lookup"><span data-stu-id="222f2-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="222f2-3198">Bu örnekte, hello **SliceStart** değişkeni hello SliceStart system değişkenine göre tooa değere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="222f2-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="222f2-3199">Hayır</span><span class="sxs-lookup"><span data-stu-id="222f2-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="222f2-3200">JSON örneği</span><span class="sxs-lookup"><span data-stu-id="222f2-3200">JSON example</span></span>

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

<span data-ttu-id="222f2-3201">Ayrıntılı bilgi için bkz: [veri fabrikasında özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="222f2-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="222f2-3202">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="222f2-3202">Next Steps</span></span>
<span data-ttu-id="222f2-3203">Eğitim aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="222f2-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="222f2-3204">Öğretici: kopyalama etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="222f2-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="222f2-3205">Öğretici: hive etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="222f2-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)