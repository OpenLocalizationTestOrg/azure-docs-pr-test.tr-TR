---
title: "Azure Data Factory kullanarak aaaCreate Tahmine dayalı veri ardışık | Microsoft Docs"
description: "Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı ardışık düzen toocreate oluşturma nasıl açıklar"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="cbb2f-103">Azure Machine Learning ve Azure Data Factory kullanarak Tahmine dayalı ardışık düzen oluşturun</span><span class="sxs-lookup"><span data-stu-id="cbb2f-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="cbb2f-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="cbb2f-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="cbb2f-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="cbb2f-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="cbb2f-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="cbb2f-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="cbb2f-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="cbb2f-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="cbb2f-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="cbb2f-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="cbb2f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="cbb2f-114">Giriş</span><span class="sxs-lookup"><span data-stu-id="cbb2f-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="cbb2f-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cbb2f-115">Azure Machine Learning</span></span>
<span data-ttu-id="cbb2f-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) , toobuild sınamak ve Tahmine dayalı analiz çözümlerini dağıtmak etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="cbb2f-117">Bir üst düzey açısından bakıldığında, üç adımda gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="cbb2f-118">**Eğitim denemenizi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-118">**Create a training experiment**.</span></span> <span data-ttu-id="cbb2f-119">Bu adımı hello Azure ML Studio kullanarak yapın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="cbb2f-120">Merhaba ML studio tootrain kullanın ve eğitim verileri kullanarak bir Tahmine dayalı bir analiz modeli test bir görsel işbirlikçi geliştirme ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="cbb2f-121">**Tooa Tahmine dayalı denemeye Dönüştür**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="cbb2f-122">Modelinizi var olan verilerle eğitilmiş ve hazır toouse olduğunuz sonra onu tooscore yeni verileri hazırlamak ve puanlama için denemenizi kolaylaştırmak.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="cbb2f-123">**Web hizmeti olarak dağıtabilir**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="cbb2f-124">Puanlama denemenizi bir Azure web hizmeti olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="cbb2f-125">Bu web hizmeti uç noktası aracılığıyla veri tooyour modeli gönderebilir ve sonuç tahminleri hello model Excel'den alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="cbb2f-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cbb2f-126">Azure Data Factory</span></span>
<span data-ttu-id="cbb2f-127">Veri fabrikası, düzenleyen ve hello otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir **taşıma** ve **dönüştürme** veri.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="cbb2f-128">Çeşitli veri depolarına verilerden alma, hello veri dönüştürme/işlemi ve yayımlama hello sonuç veri toohello veri depolarına Azure Data Factory kullanarak veri tümleştirme çözümleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="cbb2f-129">Data Factory Hizmeti'ne taşıyın ve veri dönüştürme toocreate veri ardışık sağlar ve belirtilen bir zamanlamayla (saatlik, günlük, haftalık, vb.) hello ardışık düzen çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="cbb2f-130">Ayrıca zengin Görselleştirmelerini toodisplay hello çizgileri ve veri işlem hatlarınızı, arasındaki bağımlılıkları sağlar ve tüm veri işlem hatlarınızı tek bir birleşik görünüm tooeasily tam olarak belirlemenizde sorunlardan izlemek ve izleme uyarıları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="cbb2f-131">Bkz: [giriş tooAzure Data Factory](data-factory-introduction.md) ve [ilk işlem hattınızı oluşturma](data-factory-build-your-first-pipeline.md) makaleleri tooquickly hello Azure Data Factory hizmeti ile başlayın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="cbb2f-132">Veri Fabrikası ve Machine Learning birlikte</span><span class="sxs-lookup"><span data-stu-id="cbb2f-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="cbb2f-133">Azure Data Factory etkinleştirir, tooeasily bir yayımlanan kullanmak ardışık düzen oluşturma [Azure Machine Learning] [ azure-machine-learning] web hizmeti Tahmine dayalı analiz için.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="cbb2f-134">Hello kullanarak **toplu iş yürütme etkinliği** bir Azure Data Factory işlem hattı bir Azure ML web hizmeti toomake tahminleri toplu hello veriler üzerinde çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="cbb2f-135">Bkz: [çağırma Azure ML toplu iş yürütme etkinliği hello web hizmetini kullanarak](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="cbb2f-136">Zaman içinde yeni giriş veri kümeleri kullanarak retrained toobe hello Tahmine dayalı modelleri hello Azure ML Puanlama denemeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="cbb2f-137">Aşağıdaki adımları hello yaparak Data Factory işlem hattı Azure ML modelden yeniden eğitme:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="cbb2f-138">Merhaba eğitim denemenizi (değil Tahmine dayalı denemeye) bir web hizmeti olarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="cbb2f-139">Merhaba önceki senaryoda bir web hizmeti olarak tooexpose tahmini deneme yaptığınız gibi hello Azure ML Studio bu adımda yapın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="cbb2f-140">Hello Azure ML toplu iş yürütme etkinliği tooinvoke hello web hizmetini hello eğitim denemenizi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="cbb2f-141">Temel olarak, web hizmeti eğitim hem web hizmeti Puanlama hello Azure ML toplu iş yürütme etkinliği tooinvoke kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="cbb2f-142">Yeniden eğitme ile tamamladıktan sonra web hizmeti (web hizmeti olarak sunulan Tahmine dayalı denemeye) hello kullanarak hello yeni eğitilen modeli Puanlama hello güncelleştirme **Azure ML güncelleştirme kaynak etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="cbb2f-143">Bkz: [kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştirme](data-factory-azure-ml-update-resource-activity.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="cbb2f-144">Toplu iş yürütme etkinliği kullanarak bir web hizmeti çağırma</span><span class="sxs-lookup"><span data-stu-id="cbb2f-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="cbb2f-145">Azure Data Factory tooorchestrate veri hareketlerini ve işleme kullanın ve sonra da toplu iş yürütme Azure Machine Learning kullanarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="cbb2f-146">Merhaba en üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="cbb2f-147">Bir Azure Machine Learning bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="cbb2f-148">Değerleri aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-148">You need hello following values:</span></span>

   1. <span data-ttu-id="cbb2f-149">**İstek URI'si** hello toplu iş yürütme API için.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="cbb2f-150">Merhaba tıklatarak hello istek URI'si bulabilirsiniz **toplu iş yürütme** hello web Hizmetleri sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="cbb2f-151">**API anahtarı** hello Azure Machine Learning web hizmeti yayımlanmış.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="cbb2f-152">Yayımladığınız hello web hizmeti tıklatarak hello API anahtarı bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="cbb2f-153">Kullanım hello **AzureMLBatchExecution** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![Machine Learning Panosu](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Toplu URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="cbb2f-156">Senaryo: Web hizmeti girişleri/Azure Blob Depolama toodata başvuran çıkışları kullanarak denemelerini</span><span class="sxs-lookup"><span data-stu-id="cbb2f-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="cbb2f-157">Bu senaryoda, hello Azure Machine Learning Web hizmeti bir Azure blob depolama alanındaki bir dosyadan veri kullanarak tahminleri yapar ve hello tahmin sonuçlarını hello blob depolama alanında depolar.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="cbb2f-158">Merhaba aşağıdaki JSON Data Factory işlem hattı AzureMLBatchExecution etkinliği ile tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="cbb2f-159">Merhaba etkinlik sahip hello dataset **DecisionTreeInputBlob** giriş olarak ve **DecisionTreeResultBlob** hello çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="cbb2f-160">Merhaba **DecisionTreeInputBlob** hello kullanılarak geçirilen bir giriş toohello web hizmeti tarafından olarak **WebServiceInput etkinliğine** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="cbb2f-161">Merhaba **DecisionTreeResultBlob** hello kullanılarak geçirilen bir çıktı toohello Web hizmeti tarafından olarak **webServiceOutputs** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="cbb2f-162">Merhaba web hizmeti birden fazla girdi aldığı durumlarda hello kullan **webServiceInputs** kullanmak yerine özelliği **WebServiceInput etkinliğine**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="cbb2f-163">Merhaba bkz [Web hizmeti birden çok girişi gerektiren](#web-service-requires-multiple-inputs) hello webServiceInputs özelliğini kullanarak bir örnek için bölüm.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="cbb2f-164">Merhaba tarafından başvurulan veri kümeleri **WebServiceInput etkinliğine**/**webServiceInputs** ve **webServiceOutputs** özellikleri (içinde  **typeProperties**) de dahil hello etkinlik **girişleri** ve **çıkarır**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="cbb2f-165">Azure ML denemenizde web hizmeti giriş ve çıkış bağlantı noktaları ve genel parametreleri özelleştirebileceğiniz varsayılan adları ("input1", "input2") sahip.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="cbb2f-166">webServiceInputs, webServiceOutputs ve globalParameters ayarları için kullandığınız hello adlarının hello denemeler hello adlarında tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="cbb2f-167">Azure ML uç nokta tooverify beklenen hello eşleme için hello örnek isteği yükü hello toplu iş yürütme Yardım sayfasında görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="cbb2f-168">Yalnızca girişleri ve çıkışları hello AzureMLBatchExecution etkinlik parametreleri toohello Web hizmeti geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="cbb2f-169">Örneğin, yukarıdaki JSON parçacığı hello DecisionTreeInputBlob bir giriş toohello WebServiceInput etkinliğine parametresi ile bir giriş toohello Web hizmeti geçirilen AzureMLBatchExecution etkinlik ' dir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="cbb2f-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="cbb2f-170">Example</span></span>
<span data-ttu-id="cbb2f-171">Bu örnek kullanan Azure depolama toohold her ikisi de hello girdi ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="cbb2f-172">Merhaba Git öneririz [Data Factory ile ilk işlem hattınızı oluşturma] [ adf-build-1st-pipeline] Bu örnek geçmeden önce Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="cbb2f-173">Bu örnekte Hello Data Factory Düzenleyici toocreate Data Factory yapıtlarının (bağlı hizmetler, veri kümelerini, ardışık düzen) kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="cbb2f-174">Oluşturma bir **bağlantılı hizmeti** için **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="cbb2f-175">Merhaba girdi ve çıktı dosyası farklı depolama hesapları yoksa, iki bağlı hizmet gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="cbb2f-176">Bir JSON örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="cbb2f-177">Merhaba oluşturma **giriş** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="cbb2f-178">Bazı diğer Data Factory veri kümeleri farklı olarak, bu veri kümeleri her ikisini de içermelidir **folderPath** ve **fileName** değerleri.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="cbb2f-179">Her toplu iş yürütme (her veri dilimi) tooprocess bölümleme toocause kullanın veya benzersiz giriş ve çıkış dosyaları.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="cbb2f-180">Bazı Yukarı Akış etkinliği tootransform hello hello CSV dosya biçiminde giriş ve her dilim için hello depolama hesabındaki yerleştirin tooinclude gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="cbb2f-181">Bu durumda, hello içermeyen **dış** ve **externalData** örnek ve, DecisionTreeInputBlob hello çıkış veri kümesi farklı bir etkinliğe olacaktır aşağıdaki hello gösterilen ayarları.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    <span data-ttu-id="cbb2f-182">Giriş csv dosyanızda hello sütun başlık satırı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="cbb2f-183">Merhaba kullanıyorsanız **kopyalama etkinliği** toocreate/taşıma hello csv hello blob depolama alanına hello havuz özelliği ayarlanmış olmalıdır **blobWriterAddHeader** çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="cbb2f-184">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="cbb2f-185">Merhaba csv dosyası hello başlık satırı yoksa, aşağıdaki hata hello görebilirsiniz: **etkinliğinde hata: dize okunurken hata oluştu. Beklenmeyen bir belirteç: StartObject. Yol '', satır 1, 1, konum**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="cbb2f-186">Merhaba oluşturma **çıkış** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="cbb2f-187">Bu örnek için her bir dilim yürütme bölümleme toocreate benzersiz çıkış yolu kullanır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="cbb2f-188">Merhaba bölümleme olmadan hello etkinlik hello dosyanın üzerine.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="cbb2f-189">Oluşturma bir **bağlantılı hizmeti** türü: **AzureMLLinkedService**, hello API anahtarı sağlayarak ve toplu yürütme URL'si model.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="cbb2f-190">Son olarak, içeren bir ardışık düzen Yazar bir **AzureMLBatchExecution** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="cbb2f-191">Çalışma zamanında, ardışık düzen hello aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="cbb2f-192">Giriş kümeleriniz Hello hello giriş dosyasının konumunu alır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="cbb2f-193">Hello Azure Machine Learning toplu iş yürütme API çağırır</span><span class="sxs-lookup"><span data-stu-id="cbb2f-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="cbb2f-194">Kopya, çıkış veri kümesinde bulunan verilen toplu iş yürütme çıktı toohello blob hello.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="cbb2f-195">AzureMLBatchExecution etkinlik sıfır veya daha fazla girişleri ve çıkışları bir veya daha fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="cbb2f-196">Her ikisi de **Başlat** ve **son** tarih/saat olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="cbb2f-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="cbb2f-197">Örneğin: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="cbb2f-198">Merhaba **son** zaman isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-198">hello **end** time is optional.</span></span> <span data-ttu-id="cbb2f-199">Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 hours.**"</span><span class="sxs-lookup"><span data-stu-id="cbb2f-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="cbb2f-200">toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="cbb2f-201">JSON özellikleri hakkında ayrıntılı bilgi için bkz. [JSON Betik Oluşturma Başvurusu](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbb2f-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="cbb2f-202">Merhaba AzureMLBatchExecution etkinlik için giriş belirten isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="cbb2f-203">Senaryo: Okuyucu/Yazıcı modülleri toorefer toodata içinde çeşitli depolarını kullanarak denemelerini</span><span class="sxs-lookup"><span data-stu-id="cbb2f-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="cbb2f-204">Azure ML denemeler oluştururken, başka bir ortak toouse okuyucu ve yazıcı modülleri senaryodur.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="cbb2f-205">Merhaba okuyucu modülü bir denemeyi kullanılan tooload verilerini ve hello yazıcı modülü denemelerinizi toosave verileri.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="cbb2f-206">Okuyucu ve yazıcı modüller hakkında daha fazla ayrıntı için bkz: [okuyucu](https://msdn.microsoft.com/library/azure/dn905997.aspx) ve [yazan](https://msdn.microsoft.com/library/azure/dn905984.aspx) MSDN Kitaplığı konularda.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="cbb2f-207">Merhaba okuyucu ve yazıcı modülleri kullanırken, iyi bir uygulama toouse bu Okuyucu/Yazıcı modüllerin her bir özellik için bir Web hizmeti parametresi var.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="cbb2f-208">Bu web parametreleri çalışma zamanı sırasında tooconfigure hello değerlerini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="cbb2f-209">Örneğin, bir Azure SQL veritabanı kullanan bir okuyucu modülü ile bir deneme oluşturabilirsiniz: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="cbb2f-210">Merhaba web hizmeti dağıtıldıktan sonra YYY.database.windows.net adlı başka bir Azure SQL Server hello web hizmeti toospecify tooenable hello tüketicileri istiyor.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="cbb2f-211">Bu değer toobe yapılandırılmış bir Web hizmeti parametresi tooallow kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="cbb2f-212">Web hizmeti giriş ve çıkış Web hizmeti parametrelerinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="cbb2f-213">Merhaba ilk senaryoda, bir giriş ve çıkış için bir Azure ML Web hizmeti nasıl belirtilebilir gördünüz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="cbb2f-214">Bu senaryoda, Okuyucu/Yazıcı modüllerin tooproperties karşılık gelen bir Web hizmeti parametreleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="cbb2f-215">Web hizmeti parametreleri kullanarak bir senaryo bakalım.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="cbb2f-216">Azure Machine Learning tarafından desteklenen hello veri kaynakları birinden bir okuyucu modülü tooread veri kullanan bir dağıtılan Azure Machine Learning web hizmetine sahip (örneğin: Azure SQL veritabanı).</span><span class="sxs-lookup"><span data-stu-id="cbb2f-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="cbb2f-217">Merhaba toplu yürütme işlemi yapıldıktan sonra hello sonuçları yazıcı Modülü (Azure SQL veritabanı) kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="cbb2f-218">Hiçbir web hizmeti girişleri ve çıkışları hello denemeler tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="cbb2f-219">Bu durumda, ilgili web hizmeti parametreleri hello okuyucu ve yazıcı modüller yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="cbb2f-220">Bu yapılandırma hello Okuyucu/Yazıcı hello AzureMLBatchExecution etkinlik kullanılırken modülleri toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="cbb2f-221">Web hizmeti parametreleri hello belirttiğiniz **globalParameters** hello etkinlik JSON gibi bölüm.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="cbb2f-222">Aynı zamanda [veri fabrikası işlevleri](data-factory-functions-variables.md) hello değerlerini hello aşağıdaki örnekte gösterildiği gibi Web hizmeti parametreleri geçirme içinde:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="cbb2f-223">Merhaba Web hizmeti parametreleri büyük/küçük harfe duyarlıdır, bu nedenle hello etkinliğinde belirttiğiniz hello adlarıyla JSON eşleşmesini hello hello Web hizmeti tarafından sunulan olanları olun.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="cbb2f-224">Azure Blob içinde birden çok dosyadan bir okuyucu modülü tooread veri kullanma</span><span class="sxs-lookup"><span data-stu-id="cbb2f-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="cbb2f-225">Pig gibi etkinlikleri ile büyük veri ardışık düzenleri ve Hive bir oluşturabilir veya hiçbir uzantı ile daha fazla çıkış dosyaları.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="cbb2f-226">Dış bir Hive tablosu belirttiğinizde, örneğin, hello veri hello dış Hive tablosu için adı 000000_0 aşağıdaki hello ile Azure blob depolama alanında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="cbb2f-227">Birden çok dosya hello okuyucu modülünde deneme tooread kullanın ve bunları tahminleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="cbb2f-228">Merhaba okuyucu modülü bir Azure Machine Learning deneme kullanırken, Azure Blob girdi olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="cbb2f-229">hello Azure blob depolama Hello dosyalarında hello çıktı dosyaları olabilir (örnek: 000000_0) Hdınsight üzerinde çalışan bir Pig ve Hive komut dosyası tarafından üretilen.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="cbb2f-230">Merhaba okuyucu Modülü (hiçbir uzantılı) tooread dosyaları hello yapılandırarak sağlar **yolu toocontainer, dizin/blob**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="cbb2f-231">Merhaba **yolu toocontainer** noktaları toohello kapsayıcı ve **dizin/blob** hello görüntü aşağıdaki gösterildiği gibi hello dosyalarını içeren toofolder işaret eder.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="cbb2f-232">Merhaba diğer bir deyişle, yıldız işareti \*) **tüm hello kapsayıcı/klasöründeki dosyaları hello belirtir (diğer bir deyişle, aggregateddata/data/yıl ay/2014-6 = /\*)** hello deneme bir parçası olarak okuyun.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Azure Blob özellikleri](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="cbb2f-234">Örnek</span><span class="sxs-lookup"><span data-stu-id="cbb2f-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="cbb2f-235">Web hizmeti parametreleri ile AzureMLBatchExecution aktivitesiyle kanalı</span><span class="sxs-lookup"><span data-stu-id="cbb2f-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
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
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="cbb2f-236">Yukarıdaki JSON örnek Hello:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-236">In hello above JSON example:</span></span>

* <span data-ttu-id="cbb2f-237">Merhaba dağıtılan Azure Machine Learning hizmetinin kullandığı bir okuyucu ve yazıcı modülü tooread/yazma verilerden Web / tooan Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="cbb2f-238">Bu Web hizmetini şu dört parametreler hello sunar: veritabanı sunucu adı, veritabanı adı, sunucu kullanıcı hesabı adı ve sunucu kullanıcı hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="cbb2f-239">Her ikisi de **Başlat** ve **son** tarih/saat olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="cbb2f-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="cbb2f-240">Örneğin: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="cbb2f-241">Merhaba **son** zaman isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-241">hello **end** time is optional.</span></span> <span data-ttu-id="cbb2f-242">Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 hours.**"</span><span class="sxs-lookup"><span data-stu-id="cbb2f-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="cbb2f-243">toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="cbb2f-244">JSON özellikleri hakkında ayrıntılı bilgi için bkz. [JSON Betik Oluşturma Başvurusu](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbb2f-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="cbb2f-245">Diğer senaryolar</span><span class="sxs-lookup"><span data-stu-id="cbb2f-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="cbb2f-246">Web hizmeti birden çok giriş gerektiriyor</span><span class="sxs-lookup"><span data-stu-id="cbb2f-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="cbb2f-247">Merhaba web hizmeti birden fazla girdi aldığı durumlarda hello kullan **webServiceInputs** kullanmak yerine özelliği **WebServiceInput etkinliğine**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="cbb2f-248">Merhaba tarafından başvurulan veri kümeleri **webServiceInputs** hello etkinliği de dahil edilmesi **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="cbb2f-249">Azure ML denemenizde web hizmeti giriş ve çıkış bağlantı noktaları ve genel parametreleri özelleştirebileceğiniz varsayılan adları ("input1", "input2") sahip.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="cbb2f-250">webServiceInputs, webServiceOutputs ve globalParameters ayarları için kullandığınız hello adlarının hello denemeler hello adlarında tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="cbb2f-251">Azure ML uç nokta tooverify beklenen hello eşleme için hello örnek isteği yükü hello toplu iş yürütme Yardım sayfasında görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="cbb2f-252">Web hizmeti bir giriş gerektirmez</span><span class="sxs-lookup"><span data-stu-id="cbb2f-252">Web Service does not require an input</span></span>
<span data-ttu-id="cbb2f-253">Azure ML toplu iş yürütme web Hizmetleri, örnek R veya Python komut dosyaları için değil gerektirebilecek tüm girişleri kullanılan toorun herhangi bir iş akışını olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="cbb2f-254">Ya da hello deneme herhangi GlobalParameters kullanıma sunmuyor okuyucu modülü ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="cbb2f-255">Bu durumda, hello AzureMLBatchExecution etkinlik şu şekilde yapılandırılması:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="cbb2f-256">Web hizmeti bir giriş/çıkış gerektirmez</span><span class="sxs-lookup"><span data-stu-id="cbb2f-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="cbb2f-257">Hello Azure ML toplu iş yürütme web hizmeti yapılandırılmış herhangi bir Web hizmeti çıktı sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="cbb2f-258">Bu örnekte, Web hizmeti girişi veya çıkışı yok veya tüm GlobalParameters yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="cbb2f-259">Hala hello faaliyete kendisini yapılandırılmış bir çıktı yoktur, ancak bir webServiceOutput verilmedi.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="cbb2f-260">Web hizmeti kullanan okuyucular ve yazarlar ve diğer etkinlikler yalnızca başarılı olduğunda hello etkinlik çalışması</span><span class="sxs-lookup"><span data-stu-id="cbb2f-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="cbb2f-261">Okuyucu ve yazıcı Hello Azure ML web hizmeti modülleri yapılandırılmış toorun ile veya olmadan herhangi GlobalParameters olabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="cbb2f-262">Ancak, yalnızca bir Yukarı Akış işlem tamamlandığında, veri kümesi bağımlılıkları tooinvoke hello hizmetinin kullandığı bir ardışık düzende tooembed hizmetini çağırır isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="cbb2f-263">Bu yaklaşımı kullanarak Hello toplu iş yürütme tamamlandıktan sonra başka bir eylemi de tetikleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="cbb2f-264">Bu durumda, etkinlik girişleri ve çıkışları, bunlardan herhangi birinin Web hizmeti girişleri veya çıkışları adlandırma olmadan kullanarak hello bağımlılıkları hızlı.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="cbb2f-265">Merhaba **paketler** şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="cbb2f-266">Deneme uç noktanızı bir WebServiceInput etkinliğine kullanıyorsa: blob veri kümesi tarafından temsil edilen ve hello etkinlik girişlerinde ve hello WebServiceInput etkinliğine özelliği dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="cbb2f-267">Aksi takdirde hello WebServiceInput etkinliğine özelliği atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="cbb2f-268">Deneme uç noktanızı webServiceOutput(s) kullanıyorsa: blob veri kümeleri tarafından temsil edilen ve hello etkinlik çıkışları ve hello webServiceOutputs özelliğinde dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="cbb2f-269">Merhaba etkinlik çıkarır ve webServiceOutputs hello deneme her bir çıkış hello adıyla eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="cbb2f-270">Aksi takdirde hello webServiceOutputs özelliği atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="cbb2f-271">GlobalParameter(s), deneme uç noktasını kullanıma sunar, bunlar hello etkinlik globalParameters özelliğinde anahtar, değer çiftleri olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="cbb2f-272">Aksi takdirde hello globalParameters özelliği atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="cbb2f-273">Merhaba anahtarlar büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="cbb2f-274">[Azure Data Factory işlevleri](data-factory-functions-variables.md) hello değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="cbb2f-275">Ek veri kümeleri hello etkinlik girişleri ve çıkışları Özellikleri'nde hello etkinlik typeProperties başvurulan olmadan eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="cbb2f-276">Bu veri kümeleri dilim bağımlılıkları kullanılarak yürütme yöneten ancak hello AzureMLBatchExecution etkinlik tarafından aksi halde yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="cbb2f-277">Kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="cbb2f-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="cbb2f-278">Yeniden eğitme ile tamamladıktan sonra web hizmeti (web hizmeti olarak sunulan Tahmine dayalı denemeye) hello kullanarak hello yeni eğitilen modeli Puanlama hello güncelleştirme **Azure ML güncelleştirme kaynak etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="cbb2f-279">Bkz: [kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştirme](data-factory-azure-ml-update-resource-activity.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="cbb2f-280">Okuyucu ve yazıcı modülleri</span><span class="sxs-lookup"><span data-stu-id="cbb2f-280">Reader and Writer Modules</span></span>
<span data-ttu-id="cbb2f-281">Web hizmeti parametreleri kullanarak için yaygın bir senaryo hello Azure SQL okuyucuları ve yazıcıları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="cbb2f-282">Merhaba okuyucu modülü, veri yönetimi hizmetlerinden Azure Machine Learning Studio dışında bir deneme içine kullanılan tooload verilerdir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="cbb2f-283">Merhaba yazıcı modülü denemelerinizi veri Yönetim hizmetlerine Azure Machine Learning Studio dışında toosave verilerdir.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="cbb2f-284">Azure Blob/Azure SQL Okuyucu/Yazıcı hakkında daha fazla ayrıntı için bkz: [okuyucu](https://msdn.microsoft.com/library/azure/dn905997.aspx) ve [yazan](https://msdn.microsoft.com/library/azure/dn905984.aspx) MSDN Kitaplığı konularda.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="cbb2f-285">Merhaba önceki bölümdeki Hello örnek hello Azure Blob okuyucu ve Azure Blob yazıcı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="cbb2f-286">Bu bölümde, Azure SQL okuyucu ve Azure SQL yazıcı kullanarak anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="cbb2f-287">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="cbb2f-287">Frequently asked questions</span></span>
<span data-ttu-id="cbb2f-288">**S:** my büyük veri ardışık düzen tarafından üretilen birden çok dosya vardır.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="cbb2f-289">Tüm hello dosyalarda hello AzureMLBatchExecution etkinlik toowork kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="cbb2f-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="cbb2f-290">**Y:** Evet.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-290">**A:** Yes.</span></span> <span data-ttu-id="cbb2f-291">Merhaba bkz **bir okuyucu modülü tooread verileri Azure Blob içinde birden çok dosyadan kullanarak** ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="cbb2f-292">Azure ML toplu iş Puanlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="cbb2f-293">Merhaba kullanıyorsanız **AzureMLBatchScoring** etkinlik toointegrate Azure Machine Learning ile öneririz hello son kullanma **AzureMLBatchExecution** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="cbb2f-294">Merhaba AzureMLBatchExecution etkinlik hello Ağustos 2015 sürümünde Azure PowerShell ve Azure SDK'sını sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="cbb2f-295">Merhaba AzureMLBatchScoring etkinliğini kullanarak toocontinue istiyorsanız, bu bölümde okuma devam edin.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="cbb2f-296">Giriş/çıkış için Azure Storage kullanarak azure ML toplu Puanlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="cbb2f-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="cbb2f-297">Web hizmeti parametreleri</span><span class="sxs-lookup"><span data-stu-id="cbb2f-297">Web Service Parameters</span></span>
<span data-ttu-id="cbb2f-298">Web hizmeti parametreleri için değerleri toospecify ekleme bir **typeProperties** bölüm toohello **AzureMLBatchScoringActivty** hello ardışık düzen hello aşağıdaki örnekte gösterildiği gibi JSON bölümünde:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="cbb2f-299">Aynı zamanda [veri fabrikası işlevleri](data-factory-functions-variables.md) hello değerlerini hello aşağıdaki örnekte gösterildiği gibi Web hizmeti parametreleri geçirme içinde:</span><span class="sxs-lookup"><span data-stu-id="cbb2f-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="cbb2f-300">Merhaba Web hizmeti parametreleri büyük/küçük harfe duyarlıdır, bu nedenle hello etkinliğinde belirttiğiniz hello adlarıyla JSON eşleşmesini hello hello Web hizmeti tarafından sunulan olanları olun.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="cbb2f-301">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="cbb2f-301">See Also</span></span>
* [<span data-ttu-id="cbb2f-302">Azure blog gönderisi: Azure Machine Learning ve Azure Data Factory ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="cbb2f-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
