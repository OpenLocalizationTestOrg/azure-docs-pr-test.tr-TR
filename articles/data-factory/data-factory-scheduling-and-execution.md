---
title: "aaaScheduling ve Data Factory ile yürütme | Microsoft Docs"
description: "Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="09c9f-103">Veri Fabrikası zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="09c9f-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="09c9f-104">Bu makalede hello hello Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="09c9f-105">Bu makalede, etkinlik, ardışık düzen, bağlı hizmetler ve veri kümeleri dahil olmak üzere, veri fabrikası uygulama modeli kavramlarını temelleri anladığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="09c9f-106">Azure Data Factory temel kavramları makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="09c9f-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="09c9f-107">Giriş tooData Fabrika</span><span class="sxs-lookup"><span data-stu-id="09c9f-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="09c9f-108">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="09c9f-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="09c9f-109">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="09c9f-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="09c9f-110">Başlangıç ve bitiş zamanlarını ardışık</span><span class="sxs-lookup"><span data-stu-id="09c9f-110">Start and end times of pipeline</span></span>
<span data-ttu-id="09c9f-111">İşlem hattı yalnızca arasında etkin olduğu kendi **Başlat** zaman ve **son** saat.</span><span class="sxs-lookup"><span data-stu-id="09c9f-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="09c9f-112">Bunu hello başlangıç saatinden önce veya sonra hello bitiş saati yürütülmedi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="09c9f-113">Merhaba ardışık düzen duraklatıldığında, kendi başlangıç ve bitiş zamanı bağımsız olarak yürütülemiyor.</span><span class="sxs-lookup"><span data-stu-id="09c9f-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="09c9f-114">Ardışık Düzen toorun için bunu duraklatılması değil.</span><span class="sxs-lookup"><span data-stu-id="09c9f-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="09c9f-115">Bu ayarları (Başlangıç, son, duraklatıldı) hello ardışık düzen tanımında bulun:</span><span class="sxs-lookup"><span data-stu-id="09c9f-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="09c9f-116">Bu özellikleri daha fazla bilgi için bkz: [işlem hatlarını oluşturmak](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="09c9f-117">Bir etkinlik için zamanlamayı belirtin</span><span class="sxs-lookup"><span data-stu-id="09c9f-117">Specify schedule for an activity</span></span>
<span data-ttu-id="09c9f-118">Yürütülen hello ardışık düzen değil.</span><span class="sxs-lookup"><span data-stu-id="09c9f-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="09c9f-119">Hello yürütülen hello ardışık düzendeki hello etkinlik olduğu hello ardışık genel bağlam.</span><span class="sxs-lookup"><span data-stu-id="09c9f-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="09c9f-120">Hello kullanarak bir etkinlik için yinelenen bir zamanlama belirtebilirsiniz **Zamanlayıcı** JSON etkinliği bölümü.</span><span class="sxs-lookup"><span data-stu-id="09c9f-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="09c9f-121">Örneğin, bir etkinlik toorun saatlik şu şekilde zamanlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09c9f-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="09c9f-122">Hello Aşağıdaki diyagramda gösterildiği gibi hello dönen windows ile birlikte bir dizi etkinlik için bir zamanlama oluşturur belirtme kanal başlangıç ve bitiş saatlerini.</span><span class="sxs-lookup"><span data-stu-id="09c9f-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="09c9f-123">Dönen windows sabit boyutlu çakışmayan, bitişik zaman aralıkları bir dizi var.</span><span class="sxs-lookup"><span data-stu-id="09c9f-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="09c9f-124">Bir etkinlik için bu mantıksal dönen windows adlı **etkinlik windows**.</span><span class="sxs-lookup"><span data-stu-id="09c9f-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Etkinlik Zamanlayıcısı örneği](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="09c9f-126">Merhaba **Zamanlayıcı** özelliği bir etkinlik için isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="09c9f-127">Bu özelliği belirtirseniz, hello tanımında hello etkinliğinin çıkış veri kümesi, belirttiğiniz hello tempoyla eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="09c9f-128">Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="09c9f-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="09c9f-129">Bu nedenle, Hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="09c9f-130">Bir veri kümesi için zamanlamayı belirtin</span><span class="sxs-lookup"><span data-stu-id="09c9f-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="09c9f-131">Data Factory işlem hattı bir etkinlikte sıfır veya daha fazla giriş alabilir **veri kümeleri** ve bir veya daha fazla çıkış veri kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="09c9f-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="09c9f-132">Bir etkinlik için hangi hello giriş verileri kullanılabilir hello tempoyla belirtebilir ya da hello çıktı verilerini hello kullanarak oluşturulur **kullanılabilirlik** hello dataset tanımları bölümünde.</span><span class="sxs-lookup"><span data-stu-id="09c9f-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="09c9f-133">**Sıklık** hello içinde **kullanılabilirlik** bölümü hello zaman birimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="09c9f-134">Merhaba izin verilen değerler Sıklık: dakika, saat, gün, hafta ve ay.</span><span class="sxs-lookup"><span data-stu-id="09c9f-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="09c9f-135">Merhaba **aralığı** özelliği hello kullanılabilirlik bölümünde sıklığı çarpanı belirtir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="09c9f-136">Örneğin: hello sıklığını tooDay ayarlamak ve aralığı too1 bir çıkış veri kümesi için ayarlamak, hello çıktı verilerini günlük üretilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="09c9f-137">Merhaba sıklığını dakika belirtirseniz, 15'den küçük hello aralığı toono ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="09c9f-138">Aşağıdaki örneğine hello hello giriş verisi saatlik kullanılabilir ve hello çıktı verilerini saatlik üretilen (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="09c9f-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="09c9f-139">**Girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="09c9f-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="09c9f-140">**Çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="09c9f-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="09c9f-141">Şu anda **çıkış veri kümesi sürücüleri hello zamanlama**.</span><span class="sxs-lookup"><span data-stu-id="09c9f-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="09c9f-142">Diğer bir deyişle, hello çıkış veri kümesi için belirtilen hello kullanılan toorun çalışma zamanında bir etkinlik zamanlamadır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="09c9f-143">Bu nedenle, Hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="09c9f-144">Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="09c9f-145">Merhaba aşağıdakileri tanımı hello kanal **Zamanlayıcı** hello etkinliği için kullanılan toospecify zamanlama bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="09c9f-146">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-146">This property is optional.</span></span> <span data-ttu-id="09c9f-147">Şu anda hello zamanlama hello etkinliğinin hello çıkış veri kümesi için belirtilen hello zamanlaması eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="09c9f-148">Bu örnekte, saatlik hello etkinlik çalışması hello arasında başlangıç ve bitiş hello ardışık saatlerini.</span><span class="sxs-lookup"><span data-stu-id="09c9f-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="09c9f-149">Merhaba çıktı verilerini saatlik üç saatlik windows (8: 00 - 9'da, 09: 00 - 10'da ve 10: 00 - 11: 00) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="09c9f-150">Her birim tüketilen veya bir etkinlik tarafından üretilen verilerin adlı bir **veri dilimi**.</span><span class="sxs-lookup"><span data-stu-id="09c9f-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="09c9f-151">Aşağıdaki diyagramda hello bir giriş veri kümesi ve bir çıkış veri kümesi olmayan bir etkinliği örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="09c9f-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Kullanılabilirlik Zamanlayıcı](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="09c9f-153">Merhaba diyagramı hello saatlik hello veri dilimleri giriş ve çıkış dataset gösterir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="09c9f-154">Merhaba diyagramı işlenmeye hazır üç girdi dilimlerinin gösterir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="09c9f-155">Merhaba 10-11 AM etkinlik hello 10-11 AM çıktı diliminin oluşturan devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="09c9f-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="09c9f-156">Değişkenleri kullanılarak JSON hello kümesindeki geçerli dilimin hello ilişkili hello zaman aralığı erişebilirsiniz: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) ve [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="09c9f-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="09c9f-157">Benzer şekilde, bir etkinlik penceresiyle hello WindowStart ve WindowEnd kullanarak ilişkili hello zaman aralığı erişebilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="09c9f-158">Etkinliğin başlangıç zamanlama hello çıktı veri kümesi hello etkinliğinin hello zamanlamasını eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="09c9f-159">Bu nedenle, hello SliceStart ve SliceEnd değerlerini olduğunuz hello aynı WindowStart ve WindowEnd değerleri olarak sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="09c9f-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="09c9f-160">Bu değişkenleri hakkında daha fazla bilgi için bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md#data-factory-system-variables) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="09c9f-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="09c9f-161">Etkinlik JSON farklı amaçlar için bu değişkenleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="09c9f-162">Örneğin, bunları zaman serisi verilerini temsil eden giriş ve çıkış veri kümeleri tooselect verileri kullanabilirsiniz (örneğin: 8 AM too9 'M).</span><span class="sxs-lookup"><span data-stu-id="09c9f-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="09c9f-163">Bu örnek ayrıca kullanır **WindowStart** ve **WindowEnd** tooselect ilgili verileri etkinlik için çalıştırın ve uygun hello ile tooa blob kopyalama **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="09c9f-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="09c9f-164">Merhaba **folderPath** parametreli toohave her saat için ayrı bir klasör değil.</span><span class="sxs-lookup"><span data-stu-id="09c9f-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="09c9f-165">Örnek önceki hello girdi ve çıktı veri kümeleri için belirtilen hello zamanlaması olan hello aynı (saat).</span><span class="sxs-lookup"><span data-stu-id="09c9f-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="09c9f-166">Hello hello etkinliğinin girdi veri kümesi deyin 15 dakikada bir farklı bir sıklık, varsa, hangi sürücü etkinlik zamanlaması hello hello çıktı veri kümesi olduğu gibi bu çıkış veri kümesini üreten hello etkinlik hala saatte bir kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="09c9f-167">Daha fazla bilgi için bkz: [modeli farklı sıklıklarını veri kümeleriyle](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="09c9f-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="09c9f-168">DataSet kullanılabilirliği ve ilkeleri</span><span class="sxs-lookup"><span data-stu-id="09c9f-168">Dataset availability and policies</span></span>
<span data-ttu-id="09c9f-169">Veri kümesi tanımı hello kullanılabilirlik bölümünü sıklık ve aralığı özelliklerinde hello kullanımını gördünüz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="09c9f-170">Merhaba zamanlama ve yürütme etkinliğin etkileyen birkaç diğer özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="09c9f-171">DataSet kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="09c9f-171">Dataset availability</span></span> 
<span data-ttu-id="09c9f-172">Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanabileceğiniz özellikleri **kullanılabilirlik** bölümü:</span><span class="sxs-lookup"><span data-stu-id="09c9f-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="09c9f-173">Özellik</span><span class="sxs-lookup"><span data-stu-id="09c9f-173">Property</span></span> | <span data-ttu-id="09c9f-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09c9f-174">Description</span></span> | <span data-ttu-id="09c9f-175">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09c9f-175">Required</span></span> | <span data-ttu-id="09c9f-176">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="09c9f-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09c9f-177">frequency</span><span class="sxs-lookup"><span data-stu-id="09c9f-177">frequency</span></span> |<span data-ttu-id="09c9f-178">Veri kümesi dilim üretim Hello zaman birimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="09c9f-179"><b>Sıklık desteklenen</b>: dakika, saat, gün, hafta, ay</span><span class="sxs-lookup"><span data-stu-id="09c9f-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="09c9f-180">Evet</span><span class="sxs-lookup"><span data-stu-id="09c9f-180">Yes</span></span> |<span data-ttu-id="09c9f-181">NA</span><span class="sxs-lookup"><span data-stu-id="09c9f-181">NA</span></span> |
| <span data-ttu-id="09c9f-182">interval</span><span class="sxs-lookup"><span data-stu-id="09c9f-182">interval</span></span> |<span data-ttu-id="09c9f-183">Sıklığı çarpanı belirtir</span><span class="sxs-lookup"><span data-stu-id="09c9f-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="09c9f-184">"X sıklığı aralığını" ne sıklıkta hello dilim üretilen belirler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="09c9f-185">Saatlik olarak başka bir dilimlenebilir dataset toobe hello varsa, ayarladığınız <b>sıklığı</b> çok<b>saat</b>, ve <b>aralığı</b> çok<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="09c9f-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="09c9f-186"><b>Not</b>: sıklığını dakika belirtirseniz, 15'den küçük hello aralığı toono ayarlamanızı öneririz</span><span class="sxs-lookup"><span data-stu-id="09c9f-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="09c9f-187">Evet</span><span class="sxs-lookup"><span data-stu-id="09c9f-187">Yes</span></span> |<span data-ttu-id="09c9f-188">NA</span><span class="sxs-lookup"><span data-stu-id="09c9f-188">NA</span></span> |
| <span data-ttu-id="09c9f-189">stili</span><span class="sxs-lookup"><span data-stu-id="09c9f-189">style</span></span> |<span data-ttu-id="09c9f-190">Merhaba dilim hello başlangıç/bitiş hello aralığının üretilen olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="09c9f-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="09c9f-191">StartOfInterval</span></span></li><li><span data-ttu-id="09c9f-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="09c9f-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="09c9f-193">Sıklık tooMonth ayarlanır ve stil tooEndOfInterval hello dilim ayın son günü hello üzerinde üretilmez.</span><span class="sxs-lookup"><span data-stu-id="09c9f-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="09c9f-194">Merhaba stili tooStartOfInterval ayarlarsanız hello dilim ayın ilk günü hello üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="09c9f-195">Sıklık tooDay ayarlanır ve stil tooEndOfInterval hello dilim hello hello günün son bir saat üretilmez.</span><span class="sxs-lookup"><span data-stu-id="09c9f-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="09c9f-196">Sıklık tooHour ayarlanır ve stil tooEndOfInterval hello dilim hello hello saat sonunda üretilmez.</span><span class="sxs-lookup"><span data-stu-id="09c9f-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="09c9f-197">Örneğin, 13'te – 2 PM dönem için bir dilim için 2 saat hello dilim oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="09c9f-198">Hayır</span><span class="sxs-lookup"><span data-stu-id="09c9f-198">No</span></span> |<span data-ttu-id="09c9f-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="09c9f-199">EndOfInterval</span></span> |
| <span data-ttu-id="09c9f-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="09c9f-200">anchorDateTime</span></span> |<span data-ttu-id="09c9f-201">Zamanlayıcı toocompute dataset dilim sınırları tarafından kullanılan süre içinde mutlak konum Hello tanımlar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="09c9f-202"><b>Not</b>: Merhaba AnchorDateTime sahip hello sıklığından daha ayrıntılı tarih kısımlarını sonra hello daha ayrıntılı bölümleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="09c9f-203">Örneğin, hello <b>aralığı</b> olan <b>saatlik</b> (sıklığı: saat ve aralığı: 1) ve hello <b>AnchorDateTime</b> içeren <b>dakika ve saniyeleri</b>, ardından hello <b>dakika ve saniyeleri</b> hello AnchorDateTime bölümlerini yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="09c9f-204">Hayır</span><span class="sxs-lookup"><span data-stu-id="09c9f-204">No</span></span> |<span data-ttu-id="09c9f-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="09c9f-205">01/01/0001</span></span> |
| <span data-ttu-id="09c9f-206">uzaklık</span><span class="sxs-lookup"><span data-stu-id="09c9f-206">offset</span></span> |<span data-ttu-id="09c9f-207">Tarafından hangi hello başlangıç ve bitiş tüm veri kümesi dilim gölgeye Timespan.</span><span class="sxs-lookup"><span data-stu-id="09c9f-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="09c9f-208"><b>Not</b>: anchorDateTime ve uzaklık belirtilirse, hello birleştirilmiş hello shift sonucudur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="09c9f-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="09c9f-209">No</span></span> |<span data-ttu-id="09c9f-210">NA</span><span class="sxs-lookup"><span data-stu-id="09c9f-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="09c9f-211">uzaklık örneği</span><span class="sxs-lookup"><span data-stu-id="09c9f-211">offset example</span></span>
<span data-ttu-id="09c9f-212">Varsayılan olarak, her gün (`"frequency": "Day", "interval": 1`) dilimler 00: 00 UTC zaman (gece yarısı) başlatın.</span><span class="sxs-lookup"><span data-stu-id="09c9f-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="09c9f-213">Merhaba başlangıç saati toobe 6'da UTC saati bunun yerine isterseniz, hello aşağıdaki kod parçacığında gösterildiği gibi uzaklığı hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="09c9f-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="09c9f-214">anchorDateTime örneği</span><span class="sxs-lookup"><span data-stu-id="09c9f-214">anchorDateTime example</span></span>
<span data-ttu-id="09c9f-215">Aşağıdaki örneğine hello hello dataset 23 saatte bir kez oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="09c9f-216">Merhaba ilk dilim çok ayarlanır hello anchorDateTime tarafından belirtilen hello süresi başlar`2017-04-19T08:00:00` (UTC saati).</span><span class="sxs-lookup"><span data-stu-id="09c9f-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="09c9f-217">uzaklık/örnek stili</span><span class="sxs-lookup"><span data-stu-id="09c9f-217">offset/style Example</span></span>
<span data-ttu-id="09c9f-218">Merhaba aşağıdaki veri kümesi bir aylık veri kümesidir ve 8: 00'da her ayın 3 üretilir (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="09c9f-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="09c9f-219">Veri kümesi İlkesi</span><span class="sxs-lookup"><span data-stu-id="09c9f-219">Dataset policy</span></span>
<span data-ttu-id="09c9f-220">Bir veri kümesi kullanıma hazır hale gelmeden önce bir dilim yürütme tarafından oluşturulan hello verilerini nasıl doğrulanabilir belirten bir doğrulama ilkesi tanımlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="09c9f-221">Merhaba dilim yürütme sona erdikten sonra bu gibi durumlarda hello çıkış dilim durumu çok değiştirilir**bekleyen** substatus ile **doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="09c9f-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="09c9f-222">Merhaba dilimler doğrulandıktan sonra hello dilim çok durumuna**hazır**.</span><span class="sxs-lookup"><span data-stu-id="09c9f-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="09c9f-223">Veri dilimi üretilen ancak hello doğrulamayı geçemedi, etkinlik çalışması için bu dilimine bağlıdır aşağı akış dilimleri işlenmez.</span><span class="sxs-lookup"><span data-stu-id="09c9f-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="09c9f-224">[İzleme ve ardışık düzen yönetme](data-factory-monitor-manage-pipelines.md) kapsar hello veri fabrikasında veri dilimleri çeşitli durumları.</span><span class="sxs-lookup"><span data-stu-id="09c9f-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="09c9f-225">Merhaba **İlkesi** gerekir dataset dilimler hello hello koşulu karşılayan veya veri kümesi tanımı bölümünde hello ölçütleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="09c9f-226">Merhaba aşağıdaki tabloda açıklanmaktadır hello kullanabileceğiniz özellikleri **İlkesi** bölümü:</span><span class="sxs-lookup"><span data-stu-id="09c9f-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="09c9f-227">İlke adı</span><span class="sxs-lookup"><span data-stu-id="09c9f-227">Policy Name</span></span> | <span data-ttu-id="09c9f-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09c9f-228">Description</span></span> | <span data-ttu-id="09c9f-229">Çok uygulanan</span><span class="sxs-lookup"><span data-stu-id="09c9f-229">Applied too</span></span>| <span data-ttu-id="09c9f-230">Gerekli</span><span class="sxs-lookup"><span data-stu-id="09c9f-230">Required</span></span> | <span data-ttu-id="09c9f-231">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="09c9f-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="09c9f-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="09c9f-232">minimumSizeMB</span></span> | <span data-ttu-id="09c9f-233">Merhaba verilerin doğrulayan bir **Azure blob** karşılıyor hello minimum boyut gereksinimlerini (megabayt cinsinden).</span><span class="sxs-lookup"><span data-stu-id="09c9f-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="09c9f-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="09c9f-234">Azure Blob</span></span> |<span data-ttu-id="09c9f-235">Hayır</span><span class="sxs-lookup"><span data-stu-id="09c9f-235">No</span></span> |<span data-ttu-id="09c9f-236">NA</span><span class="sxs-lookup"><span data-stu-id="09c9f-236">NA</span></span> |
| <span data-ttu-id="09c9f-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="09c9f-237">minimumRows</span></span> | <span data-ttu-id="09c9f-238">Merhaba verilerin doğrulayan bir **Azure SQL veritabanı** veya bir **Azure tablo** hello en az satır sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="09c9f-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="09c9f-239">Azure SQL Database</span></span></li><li><span data-ttu-id="09c9f-240">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="09c9f-240">Azure Table</span></span></li></ul> |<span data-ttu-id="09c9f-241">Hayır</span><span class="sxs-lookup"><span data-stu-id="09c9f-241">No</span></span> |<span data-ttu-id="09c9f-242">NA</span><span class="sxs-lookup"><span data-stu-id="09c9f-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="09c9f-243">Örnekler</span><span class="sxs-lookup"><span data-stu-id="09c9f-243">Examples</span></span>
<span data-ttu-id="09c9f-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="09c9f-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="09c9f-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="09c9f-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="09c9f-246">Bu özellikler ve örnekler hakkında daha fazla bilgi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="09c9f-247">Etkinlik ilkeleri</span><span class="sxs-lookup"><span data-stu-id="09c9f-247">Activity policies</span></span>
<span data-ttu-id="09c9f-248">İlkeler, özellikle bir tablonun hello dilim işlendiğinde bir etkinlik hello çalışma zamanı davranışını etkiler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="09c9f-249">Aşağıdaki tablonun hello hello ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="09c9f-250">Özellik</span><span class="sxs-lookup"><span data-stu-id="09c9f-250">Property</span></span> | <span data-ttu-id="09c9f-251">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="09c9f-251">Permitted values</span></span> | <span data-ttu-id="09c9f-252">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="09c9f-252">Default Value</span></span> | <span data-ttu-id="09c9f-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="09c9f-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="09c9f-254">Eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="09c9f-254">concurrency</span></span> |<span data-ttu-id="09c9f-255">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="09c9f-255">Integer</span></span> <br/><br/><span data-ttu-id="09c9f-256">En yüksek değeri: 10</span><span class="sxs-lookup"><span data-stu-id="09c9f-256">Max value: 10</span></span> |<span data-ttu-id="09c9f-257">1</span><span class="sxs-lookup"><span data-stu-id="09c9f-257">1</span></span> |<span data-ttu-id="09c9f-258">Eşzamanlı yürütmeleri hello etkinlik sayısı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="09c9f-259">Üzerinde farklı dilimler oluşabilir paralel etkinlik yürütmeleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="09c9f-260">Örneğin, bir etkinlik toogo aracılığıyla gerekiyorsa kullanılabilir veri, daha büyük bir eşzamanlılık değer sahip büyük bir dizi hello veri işleme hızı artar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="09c9f-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="09c9f-261">executionPriorityOrder</span></span> |<span data-ttu-id="09c9f-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="09c9f-262">NewestFirst</span></span><br/><br/><span data-ttu-id="09c9f-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="09c9f-263">OldestFirst</span></span> |<span data-ttu-id="09c9f-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="09c9f-264">OldestFirst</span></span> |<span data-ttu-id="09c9f-265">İşlenen veri dilimleri Hello sıralama belirler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="09c9f-266">Örneğin, varsa (bir oluşmasını 4 pm adresindeki ve 17: 00 saatleri sırasında başka bir) 2 böler ve hem de yürütme olması.</span><span class="sxs-lookup"><span data-stu-id="09c9f-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="09c9f-267">Merhaba executionPriorityOrder toobe NewestFirst ayarlarsanız, 17: 00 saatleri sırasında hello dilim önce işlenir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="09c9f-268">Merhaba executionPriorityORder toobe OldestFIrst ayarlarsanız, benzer şekilde ardından 4 PM adresindeki hello dilim işlenir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="09c9f-269">retry</span><span class="sxs-lookup"><span data-stu-id="09c9f-269">retry</span></span> |<span data-ttu-id="09c9f-270">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="09c9f-270">Integer</span></span><br/><br/><span data-ttu-id="09c9f-271">En büyük değer 10 olabilir</span><span class="sxs-lookup"><span data-stu-id="09c9f-271">Max value can be 10</span></span> |<span data-ttu-id="09c9f-272">0</span><span class="sxs-lookup"><span data-stu-id="09c9f-272">0</span></span> |<span data-ttu-id="09c9f-273">Hata olarak işaretlenmiş hello veri işleme hello dilim için önce yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="09c9f-274">Etkinlik yürütme veri dilimi için belirtilen toohello denenen yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="09c9f-275">mümkün olan en kısa sürede hello hatasından sonra Hello yeniden deneme yapılır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="09c9f-276">timeout</span><span class="sxs-lookup"><span data-stu-id="09c9f-276">timeout</span></span> |<span data-ttu-id="09c9f-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="09c9f-277">TimeSpan</span></span> |<span data-ttu-id="09c9f-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="09c9f-278">00:00:00</span></span> |<span data-ttu-id="09c9f-279">Merhaba etkinlik için zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-279">Timeout for hello activity.</span></span> <span data-ttu-id="09c9f-280">Örnek: 00:10: (zaman aşımı 10 dakika anlamına gelir) 00</span><span class="sxs-lookup"><span data-stu-id="09c9f-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="09c9f-281">Bir değer belirtilmemiş ya da 0 hello zaman aşımı sonsuzdur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="09c9f-282">Merhaba veri işleme saat dilimi hello zaman aşımı değerini aşarsa, iptal edilir ve tooretry hello işleme hello sistem dener.</span><span class="sxs-lookup"><span data-stu-id="09c9f-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="09c9f-283">yeniden deneme sayısı Hello hello yeniden deneme özelliğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="09c9f-284">Zaman aşımı oluştuğunda hello durumu tooTimedOut ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="09c9f-285">gecikme</span><span class="sxs-lookup"><span data-stu-id="09c9f-285">delay</span></span> |<span data-ttu-id="09c9f-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="09c9f-286">TimeSpan</span></span> |<span data-ttu-id="09c9f-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="09c9f-287">00:00:00</span></span> |<span data-ttu-id="09c9f-288">Veri işleme hello dilim başlatır önce Hello gecikme belirtin.</span><span class="sxs-lookup"><span data-stu-id="09c9f-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="09c9f-289">Merhaba gecikme hello beklenen yürütme zamanı geçmişte sonra veri dilimi için etkinliğin hello yürütme başlatılır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="09c9f-290">Örnek: 00:10: (10 dakika gecikme anlamına gelir) 00</span><span class="sxs-lookup"><span data-stu-id="09c9f-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="09c9f-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="09c9f-291">longRetry</span></span> |<span data-ttu-id="09c9f-292">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="09c9f-292">Integer</span></span><br/><br/><span data-ttu-id="09c9f-293">En yüksek değeri: 10</span><span class="sxs-lookup"><span data-stu-id="09c9f-293">Max value: 10</span></span> |<span data-ttu-id="09c9f-294">1</span><span class="sxs-lookup"><span data-stu-id="09c9f-294">1</span></span> |<span data-ttu-id="09c9f-295">Dilim yürütülemedi Hello hello uzun yeniden deneme girişimi sayısı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="09c9f-296">longRetry girişimleri tarafından longRetryInterval aralarına aralık eklenir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="09c9f-297">Yeniden deneme girişimleri arasındaki süre toospecify gerekiyorsa, bu nedenle longRetry kullanın.</span><span class="sxs-lookup"><span data-stu-id="09c9f-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="09c9f-298">Yeniden deneme ve longRetry belirtilirse, her bir longRetry denemesi denemeleri içerir ve hello en fazla deneme sayısı yeniden deneme * longRetry.</span><span class="sxs-lookup"><span data-stu-id="09c9f-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="09c9f-299">Örneğin, biz hello etkinlik İlkesi ayarlarında aşağıdaki hello varsa:</span><span class="sxs-lookup"><span data-stu-id="09c9f-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="09c9f-300">Yeniden deneme: 3</span><span class="sxs-lookup"><span data-stu-id="09c9f-300">Retry: 3</span></span><br/><span data-ttu-id="09c9f-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="09c9f-301">longRetry: 2</span></span><br/><span data-ttu-id="09c9f-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="09c9f-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="09c9f-303">Yalnızca bir dilim tooexecute olduğu varsayılır (Durum Bekliyor) ve hello Etkinlik yürütme her zaman başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="09c9f-304">Başlangıçta 3 ardışık yürütme deneme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="09c9f-305">Her girişiminden sonra Yeniden Dene'yi hello dilim durum olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="09c9f-306">İlk 3 deneme üzerinden sonra hello dilim durumunu LongRetry olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="09c9f-307">Bir saat sonra (diğer bir deyişle, longRetryInteval'ın değeri), 3 ardışık yürütme deneme başka bir dizi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="09c9f-308">Bundan sonra hello dilim durumu başarısız ve daha fazla yeniden deneme yok denenmesi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="09c9f-309">Bu nedenle genel 6 deneme yapıldı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="09c9f-310">Hiçbir yürütme başarılı olursa, hello dilim durum hazır olur ve daha fazla yeniden deneme yok çalıştı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="09c9f-311">longRetry, belirleyici olmayan zamanlarda bağımlı veri ulaştığında veya hello genel ortamında hangi veri işleme gerçekleşir altında anormal olduğu durumlarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="09c9f-312">Böyle durumlarda, yeniden deneme birbiri ardından yapılması yardımcı ve bunun hello sonuçlarında zaman aralığını sonra yapılması istenen çıkış.</span><span class="sxs-lookup"><span data-stu-id="09c9f-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="09c9f-313">Uyarı: longRetry veya longRetryInterval yüksek değerleri ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="09c9f-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="09c9f-314">Genellikle, daha yüksek değerleri sistemle ilgili diğer sorunlar kapsıyor.</span><span class="sxs-lookup"><span data-stu-id="09c9f-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="09c9f-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="09c9f-315">longRetryInterval</span></span> |<span data-ttu-id="09c9f-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="09c9f-316">TimeSpan</span></span> |<span data-ttu-id="09c9f-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="09c9f-317">00:00:00</span></span> |<span data-ttu-id="09c9f-318">uzun yeniden deneme girişimleri arasında gecikme Hello</span><span class="sxs-lookup"><span data-stu-id="09c9f-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="09c9f-319">Daha fazla bilgi için bkz: [ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="09c9f-320">Veri dilimi paralel işlenmesi</span><span class="sxs-lookup"><span data-stu-id="09c9f-320">Parallel processing of data slices</span></span>
<span data-ttu-id="09c9f-321">Merhaba hello ardışık düzeni için başlangıç tarihi geçmiş hello ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="09c9f-322">Bunu yaptığınızda, veri fabrikası otomatik olarak hello geçen tüm veri dilimleri (arka dolgu) hesaplar ve bunları işlemeye başlar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="09c9f-323">Örneğin: 2017-04-01 başlangıç tarihi ile işlem hattı oluşturma ve hello geçerli tarih olan 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="09c9f-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="09c9f-324">Merhaba tempoyla Merhaba, veri kümesi günlük 2017-04-01 gelen tüm hello dilimler işleme Data Factory başlatır olduğundan çıktısını alırsanız hello başlangıç tarihi too2017-04-09 hemen hello son olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="09c9f-325">Stil özelliği hello kullanılabilirlik bölümdeki Hello değeri EndOfInterval olduğundan 2017-04-10 hello dilimden varsayılan olarak henüz işlenmedi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="09c9f-326">Merhaba eski dilim işlenir ilk hello varsayılan olarak executionPriorityOrder OldestFirst değeri.</span><span class="sxs-lookup"><span data-stu-id="09c9f-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="09c9f-327">Merhaba stil özelliği açıklaması için bkz: [dataset kullanılabilirliği](#dataset-availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="09c9f-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="09c9f-328">Merhaba hello executionPriorityOrder bölüm açıklaması için bkz: [etkinlik ilkeleri](#activity-policies) bölümü.</span><span class="sxs-lookup"><span data-stu-id="09c9f-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="09c9f-329">Paralel olarak ayarlama hello tarafından işlenen geri doldurulmuş veri dilimleri toobe yapılandırabilirsiniz **eşzamanlılık** hello özelliğinde **İlkesi** JSON hello etkinliği bölümü.</span><span class="sxs-lookup"><span data-stu-id="09c9f-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="09c9f-330">Bu özellik üzerinde farklı dilimler oluşabilir paralel etkinlik yürütmeleri hello sayısını belirler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="09c9f-331">Merhaba hello eşzamanlılık özelliği için varsayılan değer 1'dir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="09c9f-332">Bu nedenle, bir dilim aynı anda varsayılan olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="09c9f-333">Merhaba en büyük değer 10'dur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-333">hello maximum value is 10.</span></span> <span data-ttu-id="09c9f-334">Bir işlem hattı aracılığıyla kullanılabilir veri, daha büyük bir eşzamanlılık değer sahip büyük bir dizi toogo gerektiği zaman hello veri işleme hızı artar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="09c9f-335">Başarısız olan veri dilimi yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="09c9f-335">Rerun a failed data slice</span></span>
<span data-ttu-id="09c9f-336">Veri dilimi işlenirken bir hata ortaya çıkarsa, Azure portal dikey penceresi veya izleme ve yönetme uygulaması'nı kullanarak bir dilim hello işlenmesini neden başarısız anlamak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="09c9f-337">Bkz: [izleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-pipelines.md) veya [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="09c9f-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="09c9f-338">Aşağıdaki iki etkinlik gösterir örneğine hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="09c9f-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="09c9f-339">Activity1 ve aktivite 2.</span><span class="sxs-lookup"><span data-stu-id="09c9f-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="09c9f-340">Activity1 Dataset1 dilimin kullanır ve bir giriş olarak Activity2 tooproduce hello son veri kümesi, bir dilim tarafından tüketilen Dataset2 dilimin üretir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Başarısız dilim](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="09c9f-342">Merhaba diyagramı hatası üretmeye hello 9-10'da dilim Dataset2 için vardı üç son dilim dışında gösterir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="09c9f-343">Veri Fabrikası bağımlılık hello zaman serisi veri kümesi için otomatik olarak izler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="09c9f-344">Sonuç olarak, hello 9-10'da aşağı akış dilimi çalıştırın hello etkinlik başlatılmaz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="09c9f-345">Merhaba başarısız dilim tooeasily Bul hello kök hello sorunu neden ve düzeltmek için data Factory izleme ve Yönetim Araçları toodrill hello tanılama günlüklerine sağlar.</span><span class="sxs-lookup"><span data-stu-id="09c9f-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="09c9f-346">Merhaba sorunu düzelttikten sonra tooproduce hello başarısız dilim hello etkinlik kolayca başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="09c9f-347">Hakkında daha fazla bilgi için toorerun ve veri dilimi için durumu geçişleri anlamak, [izleme ve Azure portal dikey penceresi kullanılarak işlem hatlarını yönetme](data-factory-monitor-manage-pipelines.md) veya [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="09c9f-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="09c9f-348">Merhaba yeniden sonra için 9-10'da dilim **Dataset2**, veri fabrikası başlatır hello hello 9-10'da bağımlı dilimi için hello son dataset üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09c9f-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Başarısız dilimi yeniden çalıştırın](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="09c9f-350">Bir işlem hattında birden çok etkinlik</span><span class="sxs-lookup"><span data-stu-id="09c9f-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="09c9f-351">Bir işlem hattında birden fazla etkinliğiniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="09c9f-352">Merhaba etkinlikler için giriş veri dilimi hazır olup olmadığını hello etkinlikleri bir ardışık düzende birden çok etkinliği varsa ve bir etkinlik hello çıktısını başka bir etkinliğin bir giriş değil, paralel olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="09c9f-353">Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="09c9f-354">Merhaba etkinlikleri hello olabilir aynı ardışık düzen veya farklı ardışık düzenler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="09c9f-355">yalnızca hello önce bir başarıyla tamamlandığında hello ikinci etkinlik yürütür.</span><span class="sxs-lookup"><span data-stu-id="09c9f-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="09c9f-356">Örneğin, bir işlem hattı iki etkinlik sahip olduğu durumda aşağıdaki hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="09c9f-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="09c9f-357">Dış giriş veri kümesi D1 ve D2 üretir çıktı veri kümesi gerektiren etkinlik A1.</span><span class="sxs-lookup"><span data-stu-id="09c9f-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="09c9f-358">Çıkış dataset D3 D2 kümesinden giriş gerektirir ve üreten etkinlik A2.</span><span class="sxs-lookup"><span data-stu-id="09c9f-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="09c9f-359">Bu senaryo, etkinlikleri A1 ve A2 olan hello aynı kanalı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="09c9f-360">Merhaba etkinliği hello dış veriler kullanılabilir ve zamanlanmış hello kullanılabilirlik sıklığı sınırına a1 çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="09c9f-361">Merhaba etkinlik A2 hello D2 gelen zamanlanmış dilimler kullanılabilir hale gelir ve hello zamanlanan kullanılabilirlik sıklığı ulaşıldığında çalışır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="09c9f-362">Veri kümesi D2 hello dilimleri birinde bir hata varsa, kullanılabilir oluncaya kadar A2 bu dilim için çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="09c9f-363">aynı ardışık düzen hello diyagramı aşağıdaki gibi görünür diyagram görünümü hello hem etkinliklerle hello:</span><span class="sxs-lookup"><span data-stu-id="09c9f-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Merhaba aktivitelerde zincirleme aynı kanalı](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="09c9f-365">Daha önce belirtildiği gibi hello etkinlikler farklı ardışık düzenlerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="09c9f-366">Böyle bir senaryoda hello diyagram görünümü diyagramda aşağıdaki hello gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="09c9f-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![İki ardışık düzende zincirleme etkinlikleri](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="09c9f-368">Merhaba bkz [sırayla kopyalamak](#copy-sequentially) hello ek bir örnek bölümünde.</span><span class="sxs-lookup"><span data-stu-id="09c9f-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="09c9f-369">Farklı sıklıklarını modeli kümeleriyle</span><span class="sxs-lookup"><span data-stu-id="09c9f-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="09c9f-370">Merhaba örnekleri için girdi ve çıktı veri kümelerini ve hello etkinlik zamanlama penceresi hello sıklıkları olan hello aynı.</span><span class="sxs-lookup"><span data-stu-id="09c9f-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="09c9f-371">Bazı senaryolar hello özelliği tooproduce çıktıyı bir veya daha fazla girdi hello sıklık farklı bir sıklık gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="09c9f-372">Veri Fabrikası bu senaryo modelleme destekler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="09c9f-373">Örnek 1: her saat kullanılabilir giriş verileri için bir günlük çıkışı raporu oluşturmak</span><span class="sxs-lookup"><span data-stu-id="09c9f-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="09c9f-374">Azure Blob storage'da her saat algılayıcılar kullanılabilir ölçüm verileri Giriş bir senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="09c9f-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="09c9f-375">Tooproduce ortalama, maksimum ve minimum gibi istatistikleri içeren bir günlük toplama rapor ile Merhaba gün için istediğiniz [Data Factory hive etkinliği](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="09c9f-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="09c9f-376">Bu senaryo Data Factory ile nasıl model aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="09c9f-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="09c9f-377">**Girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="09c9f-377">**Input dataset**</span></span>

<span data-ttu-id="09c9f-378">Merhaba, saatlik gün verilen hello hello klasöründeki dosyaları bırakılan giriş.</span><span class="sxs-lookup"><span data-stu-id="09c9f-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="09c9f-379">Giriş için kullanılabilirlik ayarlanırsa **saat** (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="09c9f-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="09c9f-380">**Çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="09c9f-380">**Output dataset**</span></span>

<span data-ttu-id="09c9f-381">Bir çıkış dosyası her gün hello günün klasöründe oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="09c9f-382">Çıktı kullanılabilirliğini ayarlanırsa **gün** (sıklığı: gün ve aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="09c9f-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="09c9f-383">**Etkinlik: ardışık düzeninde hive etkinliği**</span><span class="sxs-lookup"><span data-stu-id="09c9f-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="09c9f-384">Merhaba hive betiğini alır hello uygun *DateTime* bilgileri hello kullandığınız parametre olarak **WindowStart** hello aşağıdaki kod parçacığında gösterildiği gibi değişkeni.</span><span class="sxs-lookup"><span data-stu-id="09c9f-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="09c9f-385">Merhaba hive betiğini Bu değişken tooload hello veri hello doğru klasöründen hello gün için kullanır ve hello toplama toogenerate hello çıkış çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09c9f-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="09c9f-386">Merhaba Aşağıdaki diyagramda açısından bir veri bağımlılığı hello senaryo gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Veri bağımlılığı](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="09c9f-388">Merhaba çıktı diliminin her gün için bir giriş veri kümesinden 24 saat dilimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="09c9f-389">Veri Fabrikası hesaplar çözülmesi tarafından otomatik olarak bu bağımlılıklar hello kalan giriş veri dilimleri hello aynı üretilen çıkış dilim toobe hello olarak süre.</span><span class="sxs-lookup"><span data-stu-id="09c9f-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="09c9f-390">Merhaba 24 girdi dilimlerinin hiçbirinde yoksa, veri fabrikası hello girdi dilimi toobe hello günlük etkinlik başlatmadan önce hazır bekler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="09c9f-391">Örnek 2: bağımlılık, ifadeler ve Data Factory işlevleri ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="09c9f-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="09c9f-392">Şirketinizdeki başka bir senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="09c9f-392">Let’s consider another scenario.</span></span> <span data-ttu-id="09c9f-393">İki giriş veri kümesi işleyen bir hive etkinliği olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="09c9f-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="09c9f-394">Bunlardan birini yeni veri günlük olsa da, bunlardan biri her hafta yeni verileri alır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="09c9f-395">Merhaba iki girdi arasında toodo bir birleştirme istediğinizi varsayın ve her gün bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="09c9f-396">Merhaba basit yaklaşım, veri fabrikası hello sağ girişi otomatik olarak rakamları toohello çıkış veri dilimin zaman dönemi çalışmıyor hizalayarak tooprocess böler.</span><span class="sxs-lookup"><span data-stu-id="09c9f-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="09c9f-397">Çalıştıran her etkinlik için hello haftalık girdi veri kümesi için geçen haftaki veri dilimi hello Data Factory kullanmalısınız belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="09c9f-398">Bu davranış hello parçacığı tooimplement aşağıdaki gösterildiği gibi Azure Data Factory işlevlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="09c9f-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="09c9f-399">**Input1: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="09c9f-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="09c9f-400">Merhaba, ilk hello Azure blob günlük güncelleştiriliyor giriş.</span><span class="sxs-lookup"><span data-stu-id="09c9f-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="09c9f-401">**Input2: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="09c9f-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="09c9f-402">Input2 hello haftalık güncelleştirilmekte Azure blob ' dir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="09c9f-403">**Çıkış: Azure blob**</span><span class="sxs-lookup"><span data-stu-id="09c9f-403">**Output: Azure blob**</span></span>

<span data-ttu-id="09c9f-404">Bir çıkış dosyası her gün hello gün için hello klasöründe oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09c9f-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="09c9f-405">Çıktı kullanılabilirliğini çok ayarlamak**gün** (sıklığı: Day, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="09c9f-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="09c9f-406">**Etkinlik: ardışık düzeninde hive etkinliği**</span><span class="sxs-lookup"><span data-stu-id="09c9f-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="09c9f-407">Merhaba hive etkinliği hello iki girdi alır ve her gün bir çıktı diliminin üretir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="09c9f-408">Her günün çıkış dilim toodepend üzerinde hello önceki haftanın girdi dilimi haftalık girişi için şu şekilde belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="09c9f-409">Bkz: [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md) işlevler ve Data Factory destekleyen sistem değişkenleri listesi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="09c9f-410">Ek</span><span class="sxs-lookup"><span data-stu-id="09c9f-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="09c9f-411">Örnek: sıralı olarak Kopyala</span><span class="sxs-lookup"><span data-stu-id="09c9f-411">Example: copy sequentially</span></span>
<span data-ttu-id="09c9f-412">Bu olası toorun birden çok kopyalama işlemleri birbiri ardından sıralı/sıralı bir biçimde değil.</span><span class="sxs-lookup"><span data-stu-id="09c9f-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="09c9f-413">Örneğin, iki kopyalama aşağıdaki hello ile bir ardışık düzendeki (CopyActivity1 ve CopyActivity2) etkinlik giriş verileri çıkış veri kümeleri olabilir:</span><span class="sxs-lookup"><span data-stu-id="09c9f-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="09c9f-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="09c9f-414">CopyActivity1</span></span>

<span data-ttu-id="09c9f-415">Giriş: veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="09c9f-415">Input: Dataset.</span></span> <span data-ttu-id="09c9f-416">Çıkış: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="09c9f-416">Output: Dataset2.</span></span>

<span data-ttu-id="09c9f-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="09c9f-417">CopyActivity2</span></span>

<span data-ttu-id="09c9f-418">Giriş: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="09c9f-418">Input: Dataset2.</span></span>  <span data-ttu-id="09c9f-419">Çıkış: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="09c9f-419">Output: Dataset3.</span></span>

<span data-ttu-id="09c9f-420">CopyActivity2 yalnızca hello CopyActivity1 başarıyla çalıştırıldı ve Dataset2 kullanılabilir çalışır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="09c9f-421">Merhaba örnek JSON ardışık düzeni şöyledir:</span><span class="sxs-lookup"><span data-stu-id="09c9f-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="09c9f-422">Merhaba ikinci etkinlik için giriş olarak hello çıkış veri kümesi hello ilk kopyalama etkinliği (Dataset2) Hello örnekte belirtilen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="09c9f-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="09c9f-423">Bu nedenle, yalnızca hello ilk etkinliğinden hello çıktı veri kümesi hazır olduğunda hello ikinci etkinliği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="09c9f-424">Merhaba örnekte CopyActivity2 Dataset3 gibi farklı bir giriş olabilir ancak CopyActivity1 tamamlanana kadar hello etkinlik çalışmaz için bir giriş tooCopyActivity2 Dataset2 belirtin.</span><span class="sxs-lookup"><span data-stu-id="09c9f-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="09c9f-425">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09c9f-425">For example:</span></span>

<span data-ttu-id="09c9f-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="09c9f-426">CopyActivity1</span></span>

<span data-ttu-id="09c9f-427">Giriş: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="09c9f-427">Input: Dataset1.</span></span> <span data-ttu-id="09c9f-428">Çıkış: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="09c9f-428">Output: Dataset2.</span></span>

<span data-ttu-id="09c9f-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="09c9f-429">CopyActivity2</span></span>

<span data-ttu-id="09c9f-430">Girişler: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="09c9f-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="09c9f-431">Çıkış: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="09c9f-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="09c9f-432">Merhaba ikinci kopya etkinliği için iki giriş veri kümesi Hello örnekte belirtilen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="09c9f-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="09c9f-433">Birden çok girişi belirtildiğinde, yalnızca hello ilk girdi veri kümesi veri kopyalamak için kullanılır, ancak diğer veri kümeleri bağımlılıklar olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="09c9f-434">Yalnızca hello aşağıdaki koşulların karşılandığından sonra CopyActivity2 başlatmak:</span><span class="sxs-lookup"><span data-stu-id="09c9f-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="09c9f-435">CopyActivity1 başarıyla tamamlandı ve Dataset2 kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="09c9f-436">Bu veri kümesi, veri tooDataset4 kopyalarken kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="09c9f-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="09c9f-437">Yalnızca CopyActivity2 için zamanlama bağımlılık olarak davranır.</span><span class="sxs-lookup"><span data-stu-id="09c9f-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="09c9f-438">Dataset3 kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09c9f-438">Dataset3 is available.</span></span> <span data-ttu-id="09c9f-439">Bu veri kümesi kopyalanan toohello hedef hello verileri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="09c9f-439">This dataset represents hello data that is copied toohello destination.</span></span> 
