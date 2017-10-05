---
title: "Azure Data Factory kullanarak Tahmine dayalı veri ardışık düzen oluşturun | Microsoft Docs"
description: "Nasıl oluşturulacağını açıklar Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı ardışık düzen oluşturun"
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
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="e43d1-103">Azure Machine Learning ve Azure Data Factory kullanarak Tahmine dayalı ardışık düzen oluşturun</span><span class="sxs-lookup"><span data-stu-id="e43d1-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e43d1-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e43d1-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e43d1-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e43d1-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e43d1-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e43d1-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e43d1-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e43d1-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e43d1-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e43d1-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="e43d1-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="e43d1-114">Giriş</span><span class="sxs-lookup"><span data-stu-id="e43d1-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="e43d1-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e43d1-115">Azure Machine Learning</span></span>
<span data-ttu-id="e43d1-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) derleme, test ve Tahmine dayalı analiz çözümlerini dağıtma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="e43d1-117">Bir üst düzey açısından bakıldığında, üç adımda gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="e43d1-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="e43d1-118">**Eğitim denemenizi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-118">**Create a training experiment**.</span></span> <span data-ttu-id="e43d1-119">Azure ML Studio kullanarak bu adımı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="e43d1-120">ML studio eğitmek ve eğitim verileri kullanarak bir Tahmine dayalı bir analiz modeli test etmek için kullandığınız bir görsel işbirlikçi geliştirme ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="e43d1-121">**Tahmine dayalı bir deneme Dönüştür**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="e43d1-122">Modelinizi var olan verilerle eğitilmiş ve yeni verilerinizi puanlamada için kullanıma hazır sonra hazırlamak ve puanlama için denemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="e43d1-123">**Web hizmeti olarak dağıtabilir**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="e43d1-124">Puanlama denemenizi bir Azure web hizmeti olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="e43d1-125">Bu web hizmeti uç noktası aracılığıyla modelde veri gönderebilir ve sonuç tahminleri model Excel'den alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="e43d1-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e43d1-126">Azure Data Factory</span></span>
<span data-ttu-id="e43d1-127">Data Factory, verilerin **taşınmasını** ve **dönüştürülmesini** düzenleyen ve otomatikleştiren bulut tabanlı bir veri tümleştirme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="e43d1-128">Çeşitli veri depolarına verilerden alma, veri dönüştürme/işlemi ve sonuç verileri veri depoları yayımlama Azure Data Factory kullanarak veri tümleştirme çözümleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="e43d1-129">Data Factory hizmeti verileri taşıyıp dönüştüren ve ardından işlem hattını belirli bir zamanlamaya (saatlik, günlük, haftalık, vb.) göre çalıştıran veri işlem hatları oluşturmanıza imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="e43d1-130">Ayrıca, veri işlem hatlarınız arasındaki çizgileri ve bağımlılıkları gösteren ve sorunları kolayca saptamak ve izleme uyarılarını ayarlamak üzere tek bir birleşik görünümden tüm veri işlem hatlarınızı izleyen zengin görsel öğeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e43d1-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="e43d1-131">Bkz: [Azure Data Factory'ye giriş](data-factory-introduction.md) ve [ilk işlem hattınızı oluşturma](data-factory-build-your-first-pipeline.md) makaleler Azure Data Factory hizmetiyle hızlıca başlamak için.</span><span class="sxs-lookup"><span data-stu-id="e43d1-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="e43d1-132">Veri Fabrikası ve Machine Learning birlikte</span><span class="sxs-lookup"><span data-stu-id="e43d1-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="e43d1-133">Azure Data Factory bir yayımlanan kullanmak ardışık düzen kolayca oluşturmanıza olanak sağlar [Azure Machine Learning] [ azure-machine-learning] web hizmeti Tahmine dayalı analiz için.</span><span class="sxs-lookup"><span data-stu-id="e43d1-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="e43d1-134">Kullanarak **toplu iş yürütme etkinliği** bir Azure Data Factory işlem hattı verileri toplu tahminleri yapmak için bir Azure ML web hizmeti çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="e43d1-135">Bkz: [toplu iş yürütme etkinliği kullanarak bir Azure ML web Hizmeti'ni çağırmadan](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="e43d1-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="e43d1-136">Zaman içinde denemeler Puanlama Azure ML Tahmine dayalı modelleri yeni giriş veri kümeleri kullanarak retrained gerekir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="e43d1-137">Aşağıdakileri yaparak bir Data Factory işlem hattı Azure ML modelden yeniden eğitme:</span><span class="sxs-lookup"><span data-stu-id="e43d1-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="e43d1-138">Eğitim denemenizi (değil Tahmine dayalı denemeye) bir web hizmeti olarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="e43d1-139">Tahmine dayalı denemeye önceki senaryoda bir web hizmeti olarak kullanıma sunmak için yaptığınız gibi Azure ML Studio'da bu adımı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="e43d1-140">Eğitim denemenizi web hizmetini çağırmak için Azure ML toplu iş yürütme etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="e43d1-141">Temel olarak, eğitim web hizmeti ve puanlama web hizmetini çağırmak için Azure ML toplu iş yürütme etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="e43d1-142">Yeniden eğitme ile tamamladıktan sonra Puanlama web hizmeti (web hizmeti olarak sunulan Tahmine dayalı denemeye) ile yeni eğitilen modelini kullanarak güncelleştirme **Azure ML güncelleştirme kaynak etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="e43d1-143">Bkz: [kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştirme](data-factory-azure-ml-update-resource-activity.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="e43d1-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="e43d1-144">Toplu iş yürütme etkinliği kullanarak bir web hizmeti çağırma</span><span class="sxs-lookup"><span data-stu-id="e43d1-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="e43d1-145">Azure Data Factory veri hareketlerini ve işleme düzenlemek için kullanın ve sonra da toplu iş yürütme Azure Machine Learning kullanarak gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e43d1-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="e43d1-146">Üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e43d1-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="e43d1-147">Bir Azure Machine Learning bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e43d1-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="e43d1-148">Aşağıdaki değerleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="e43d1-148">You need the following values:</span></span>

   1. <span data-ttu-id="e43d1-149">**İstek URI'si** toplu iş yürütme API.</span><span class="sxs-lookup"><span data-stu-id="e43d1-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="e43d1-150">İstek URI'Sİ'i tıklatarak bulabilirsiniz **toplu iş yürütme** web Hizmetleri sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e43d1-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="e43d1-151">**API anahtarı** için yayımlanan Azure Machine Learning web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e43d1-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="e43d1-152">API anahtarını yayımladığınız web hizmeti tıklatarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="e43d1-153">Kullanım **AzureMLBatchExecution** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="e43d1-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Machine Learning Panosu](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Toplu URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="e43d1-156">Senaryo: Web hizmeti girişleri/verileri Azure Blob Depolama başvuran çıkışları kullanarak denemelerini</span><span class="sxs-lookup"><span data-stu-id="e43d1-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="e43d1-157">Bu senaryoda, Azure Machine Learning Web hizmeti bir Azure blob depolama alanındaki bir dosyadan veri kullanarak tahminleri yapar ve tahmin sonuçlarını blob depolama alanında depolar.</span><span class="sxs-lookup"><span data-stu-id="e43d1-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="e43d1-158">Aşağıdaki JSON Data Factory işlem hattı AzureMLBatchExecution etkinliği ile tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e43d1-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="e43d1-159">Veri kümesini etkinlik sahip **DecisionTreeInputBlob** giriş olarak ve **DecisionTreeResultBlob** çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="e43d1-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="e43d1-160">**DecisionTreeInputBlob** kullanarak geçirilen web hizmeti tarafından bir girdi olarak **WebServiceInput etkinliğine** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="e43d1-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="e43d1-161">**DecisionTreeResultBlob** çıkış olarak Web hizmeti tarafından kullanılarak geçirilir **webServiceOutputs** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="e43d1-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="e43d1-162">Web hizmeti birden fazla girdi aldığı durumlarda kullanmak **webServiceInputs** kullanmak yerine özelliği **WebServiceInput etkinliğine**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="e43d1-163">Bkz: [Web hizmeti birden çok girişi gerektiren](#web-service-requires-multiple-inputs) webServiceInputs özelliğini kullanarak bir örnek için bölüm.</span><span class="sxs-lookup"><span data-stu-id="e43d1-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="e43d1-164">Tarafından başvurulan veri kümeleri **WebServiceInput etkinliğine**/**webServiceInputs** ve **webServiceOutputs** özellikleri (içinde  **typeProperties**) de dahil etkinliğin **girişleri** ve **çıkarır**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="e43d1-165">Azure ML denemenizde web hizmeti giriş ve çıkış bağlantı noktaları ve genel parametreleri özelleştirebileceğiniz varsayılan adları ("input1", "input2") sahip.</span><span class="sxs-lookup"><span data-stu-id="e43d1-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="e43d1-166">WebServiceInputs, webServiceOutputs ve globalParameters ayarları için kullandığınız adlarının denemeler adlarında tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="e43d1-167">Örnek istek yükü, beklenen eşleme doğrulamak Azure ML uç noktanız için toplu iş yürütme Yardım sayfasında görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
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
> <span data-ttu-id="e43d1-168">Yalnızca girişleri ve çıkışları AzureMLBatchExecution etkinliğin Web hizmeti parametreleri olarak geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="e43d1-169">Örneğin, yukarıdaki JSON parçacığında, bir giriş WebServiceInput etkinliğine parametresi Web hizmeti için bir girdi olarak geçirilen AzureMLBatchExecution etkinliğine DecisionTreeInputBlob olabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="e43d1-170">Örnek</span><span class="sxs-lookup"><span data-stu-id="e43d1-170">Example</span></span>
<span data-ttu-id="e43d1-171">Bu örnek, girdi ve çıktı verilerini saklamak için Azure Storage kullanır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="e43d1-172">Gitmenizi öneririz [Data Factory ile ilk işlem hattınızı oluşturma] [ adf-build-1st-pipeline] Bu örnek geçmeden önce Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="e43d1-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="e43d1-173">Bu örnekte, veri fabrikası yapıları (bağlı hizmetler, veri kümelerini, ardışık düzen) oluşturmak için Data Factory düzenleyici kullanın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="e43d1-174">Oluşturma bir **bağlantılı hizmeti** için **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="e43d1-175">Girdi ve çıktı dosyası farklı depolama hesapları yoksa, iki bağlı hizmet gerekir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="e43d1-176">Bir JSON örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="e43d1-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="e43d1-177">Oluşturma **giriş** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="e43d1-178">Bazı diğer Data Factory veri kümeleri farklı olarak, bu veri kümeleri her ikisini de içermelidir **folderPath** ve **fileName** değerleri.</span><span class="sxs-lookup"><span data-stu-id="e43d1-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="e43d1-179">İşlem veya benzersiz giriş ve çıkış dosyaları her toplu iş yürütme (her veri dilimi) için bölümlendirme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="e43d1-180">Giriş CSV dosya biçimine dönüştürmek ve her dilim için depolama hesabındaki yerleştirmek için bazı Yukarı Akış etkinliği eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="e43d1-181">Bu durumda, dahil **dış** ve **externalData** aşağıdaki örnekte ve, DecisionTreeInputBlob gösterilen ayarları çıkış veri kümesi farklı bir etkinliğe olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="e43d1-182">Giriş csv dosyanızda sütun başlık satırı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="e43d1-183">Kullanıyorsanız **kopyalama etkinliği** csv blob depolama alanına oluşturun/taşıma için havuz özelliğini ayarlamalıdır **blobWriterAddHeader** için **doğru**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="e43d1-184">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e43d1-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="e43d1-185">Csv dosyası üstbilgi satırındaki yoksa, aşağıdaki hatayı görebilirsiniz: **etkinliğinde hata: dize okunurken hata oluştu. Beklenmeyen bir belirteç: StartObject. Yol '', satır 1, 1, konum**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="e43d1-186">Oluşturma **çıkış** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="e43d1-187">Bu örnekte, her dilim yürütme için bir benzersiz çıkış yolu oluşturmak için bölümleme kullanır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="e43d1-188">Bölümleme olmadan, etkinliği dosyanın üzerine.</span><span class="sxs-lookup"><span data-stu-id="e43d1-188">Without the partitioning, the activity would overwrite the file.</span></span>

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
4. <span data-ttu-id="e43d1-189">Oluşturma bir **bağlantılı hizmeti** türü: **AzureMLLinkedService**, API anahtarı sağlayarak ve toplu yürütme URL'si model.</span><span class="sxs-lookup"><span data-stu-id="e43d1-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="e43d1-190">Son olarak, içeren bir ardışık düzen Yazar bir **AzureMLBatchExecution** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="e43d1-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="e43d1-191">Çalışma zamanında, ardışık düzen aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e43d1-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="e43d1-192">Giriş dosyası konumunu giriş kümeleriniz alır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="e43d1-193">Azure Machine Learning toplu iş yürütme API çağırır</span><span class="sxs-lookup"><span data-stu-id="e43d1-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="e43d1-194">Toplu iş yürütme çıktısını çıkış veri kümesinde bulunan verilen blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e43d1-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e43d1-195">AzureMLBatchExecution etkinlik sıfır veya daha fazla girişleri ve çıkışları bir veya daha fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="e43d1-196">Her ikisi de **Başlat** ve **son** tarih/saat olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e43d1-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e43d1-197">Örneğin: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="e43d1-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="e43d1-198">**Son** zaman isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="e43d1-198">The **end** time is optional.</span></span> <span data-ttu-id="e43d1-199">İçin değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 hours.**"</span><span class="sxs-lookup"><span data-stu-id="e43d1-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="e43d1-200">İşlem hattını süresiz olarak çalıştırmak için **end** özelliği değerini **9999-09-09** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="e43d1-201">JSON özellikleri hakkında ayrıntılı bilgi için bkz. [JSON Betik Oluşturma Başvurusu](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="e43d1-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="e43d1-202">AzureMLBatchExecution için giriş belirtme etkinliği isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="e43d1-203">Senaryo: Denemelerini çeşitli depolarını verilerde başvurmak için Okuyucu/Yazıcı modüllerini kullanma</span><span class="sxs-lookup"><span data-stu-id="e43d1-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="e43d1-204">Azure ML denemeler oluştururken, başka bir yaygın bir senaryo, okuyucu ve yazıcı modülleri kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="e43d1-205">Okuyucu modülü bir deneme veri yüklemek için kullanılır ve yazıcı modülü denemelerinizden verileri kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="e43d1-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="e43d1-206">Okuyucu ve yazıcı modüller hakkında daha fazla ayrıntı için bkz: [okuyucu](https://msdn.microsoft.com/library/azure/dn905997.aspx) ve [yazan](https://msdn.microsoft.com/library/azure/dn905984.aspx) MSDN Kitaplığı konularda.</span><span class="sxs-lookup"><span data-stu-id="e43d1-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="e43d1-207">Okuyucu ve yazıcı modülleri kullanırken, bu Okuyucu/Yazıcı modülleri her bir özellik için bir Web hizmeti parametresi kullanmak iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="e43d1-208">Bu web parametreleri değerlerini çalışma zamanı sırasında yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e43d1-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="e43d1-209">Örneğin, bir Azure SQL veritabanı kullanan bir okuyucu modülü ile bir deneme oluşturabilirsiniz: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="e43d1-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="e43d1-210">Web hizmeti dağıtıldıktan sonra YYY.database.windows.net adlı başka bir Azure SQL Server belirtmek web hizmeti sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="e43d1-211">Yapılandırılması için bu değeri izin vermek için Web hizmeti parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="e43d1-212">Web hizmeti giriş ve çıkış Web hizmeti parametrelerinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="e43d1-213">İlk senaryoda, bir giriş ve çıkış için bir Azure ML Web hizmeti nasıl belirtilebilir gördünüz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="e43d1-214">Bu senaryoda, Okuyucu/Yazıcı modülleri özelliklerine karşılık gelen bir Web hizmeti parametreleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="e43d1-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="e43d1-215">Web hizmeti parametreleri kullanarak bir senaryo bakalım.</span><span class="sxs-lookup"><span data-stu-id="e43d1-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="e43d1-216">Verileri Azure Machine Learning tarafından desteklenen veri kaynaklarından biri okunacak okuyucu modülü kullanan bir dağıtılan Azure Machine Learning web hizmetine sahip (örneğin: Azure SQL veritabanı).</span><span class="sxs-lookup"><span data-stu-id="e43d1-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="e43d1-217">Toplu yürütme işlemi yapıldıktan sonra sonuçları yazıcı Modülü (Azure SQL veritabanı) kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="e43d1-218">Hiçbir web hizmeti girişleri ve çıkışları denemeler tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="e43d1-219">Bu durumda, okuyucu ve yazıcı modülleri için ilgili web hizmeti parametreleri yapılandırmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="e43d1-220">Bu yapılandırma Okuyucu/Yazıcı AzureMLBatchExecution etkinlik kullanırken yapılandırılması için modül sağlar.</span><span class="sxs-lookup"><span data-stu-id="e43d1-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="e43d1-221">Web hizmeti parametreleri belirtin **globalParameters** JSON etkinliğinde gibi bölüm.</span><span class="sxs-lookup"><span data-stu-id="e43d1-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="e43d1-222">Aynı zamanda [veri fabrikası işlevleri](data-factory-functions-variables.md) Web değerleri geçirme içinde parametreleri aşağıdaki örnekte gösterildiği gibi hizmet:</span><span class="sxs-lookup"><span data-stu-id="e43d1-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="e43d1-223">Web hizmeti parametreleri büyük/küçük harfe duyarlıdır, bu nedenle etkinliğin belirttiğiniz adları JSON Web hizmeti tarafından sunulan olanları eşleşmesini.</span><span class="sxs-lookup"><span data-stu-id="e43d1-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="e43d1-224">Verileri Azure Blob içinde birden çok dosya okuma için bir okuyucu modülü kullanma</span><span class="sxs-lookup"><span data-stu-id="e43d1-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="e43d1-225">Pig gibi etkinlikleri ile büyük veri ardışık düzenleri ve Hive bir oluşturabilir veya hiçbir uzantı ile daha fazla çıkış dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e43d1-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="e43d1-226">Örneğin, bir dış Hive tablo belirttiğinizde, dış Hive tablosu için veri aşağıdaki adı 000000_0 ile Azure blob storage depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="e43d1-227">Birden çok dosya okumak için bir deneme okuyucu modülü kullanın ve bunları tahminleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="e43d1-228">Okuyucu modülü bir Azure Machine Learning deneme kullanırken, Azure Blob girdi olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="e43d1-229">Azure blob depolama alanındaki dosyalar çıktı dosyaları olabilir (örnek: 000000_0) Hdınsight üzerinde çalışan bir Pig ve Hive komut dosyası tarafından üretilen.</span><span class="sxs-lookup"><span data-stu-id="e43d1-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="e43d1-230">Okuyucu modülü yapılandırarak (hiçbir uzantılı) dosyaları okumasına izin verir **kapsayıcısına yol dizin/blob**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="e43d1-231">**Kapsayıcı yoluna** işaret kapsayıcıya ve **dizin/blob** aşağıdaki görüntüde gösterildiği gibi dosyaları içeren klasör işaret eder.</span><span class="sxs-lookup"><span data-stu-id="e43d1-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="e43d1-232">Yıldız işareti diğer bir deyişle, \*) **belirtir kapsayıcı/klasöründeki tüm dosyalar (diğer bir deyişle, aggregateddata/data/yıl ay/2014-6 = /\*)** deneme bir parçası olarak okuyun.</span><span class="sxs-lookup"><span data-stu-id="e43d1-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Azure Blob özellikleri](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="e43d1-234">Örnek</span><span class="sxs-lookup"><span data-stu-id="e43d1-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="e43d1-235">Web hizmeti parametreleri ile AzureMLBatchExecution aktivitesiyle kanalı</span><span class="sxs-lookup"><span data-stu-id="e43d1-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="e43d1-236">Yukarıdaki JSON örnekte:</span><span class="sxs-lookup"><span data-stu-id="e43d1-236">In the above JSON example:</span></span>

* <span data-ttu-id="e43d1-237">Dağıtılan Azure Machine Learning Web hizmeti, başlangıç/bitiş bir Azure SQL veritabanı veri okuma/yazma için bir okuyucu ve yazıcı modülü kullanır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="e43d1-238">Aşağıdaki dört parametre bu Web hizmetini sunar: veritabanı sunucu adı, veritabanı adı, sunucu kullanıcı hesabı adı ve sunucu kullanıcı hesabı parolası.</span><span class="sxs-lookup"><span data-stu-id="e43d1-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="e43d1-239">Her ikisi de **Başlat** ve **son** tarih/saat olmalıdır [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="e43d1-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e43d1-240">Örneğin: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="e43d1-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="e43d1-241">**Son** zaman isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="e43d1-241">The **end** time is optional.</span></span> <span data-ttu-id="e43d1-242">İçin değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 hours.**"</span><span class="sxs-lookup"><span data-stu-id="e43d1-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="e43d1-243">İşlem hattını süresiz olarak çalıştırmak için **end** özelliği değerini **9999-09-09** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e43d1-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="e43d1-244">JSON özellikleri hakkında ayrıntılı bilgi için bkz. [JSON Betik Oluşturma Başvurusu](https://msdn.microsoft.com/library/dn835050.aspx).</span><span class="sxs-lookup"><span data-stu-id="e43d1-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="e43d1-245">Diğer senaryolar</span><span class="sxs-lookup"><span data-stu-id="e43d1-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="e43d1-246">Web hizmeti birden çok giriş gerektiriyor</span><span class="sxs-lookup"><span data-stu-id="e43d1-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="e43d1-247">Web hizmeti birden fazla girdi aldığı durumlarda kullanmak **webServiceInputs** kullanmak yerine özelliği **WebServiceInput etkinliğine**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="e43d1-248">Tarafından başvurulan veri kümeleri **webServiceInputs** de dahil etkinliğin **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="e43d1-249">Azure ML denemenizde web hizmeti giriş ve çıkış bağlantı noktaları ve genel parametreleri özelleştirebileceğiniz varsayılan adları ("input1", "input2") sahip.</span><span class="sxs-lookup"><span data-stu-id="e43d1-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="e43d1-250">WebServiceInputs, webServiceOutputs ve globalParameters ayarları için kullandığınız adlarının denemeler adlarında tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="e43d1-251">Örnek istek yükü, beklenen eşleme doğrulamak Azure ML uç noktanız için toplu iş yürütme Yardım sayfasında görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="e43d1-252">Web hizmeti bir giriş gerektirmez</span><span class="sxs-lookup"><span data-stu-id="e43d1-252">Web Service does not require an input</span></span>
<span data-ttu-id="e43d1-253">Azure ML toplu iş yürütme web Hizmetleri, tüm girişleri gerektirmeyebilir örnek R veya Python komut dosyası için tüm iş akışlarını çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="e43d1-254">Ya da deneme herhangi GlobalParameters kullanıma sunmuyor okuyucu modülü ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="e43d1-255">Bu durumda, AzureMLBatchExecution etkinlik şu şekilde yapılandırılması:</span><span class="sxs-lookup"><span data-stu-id="e43d1-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="e43d1-256">Web hizmeti bir giriş/çıkış gerektirmez</span><span class="sxs-lookup"><span data-stu-id="e43d1-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="e43d1-257">Azure ML toplu iş yürütme web hizmeti yapılandırılmış herhangi bir Web hizmeti çıktı sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="e43d1-258">Bu örnekte, Web hizmeti girişi veya çıkışı yok veya tüm GlobalParameters yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="e43d1-259">Hala faaliyete yapılandırılmış bir çıktı yoktur, ancak bir webServiceOutput verilmedi.</span><span class="sxs-lookup"><span data-stu-id="e43d1-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="e43d1-260">Web hizmeti kullanan okuyucular ve yazarlar ve diğer etkinlikler yalnızca başarılı olduğunda etkinlik çalışması</span><span class="sxs-lookup"><span data-stu-id="e43d1-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="e43d1-261">Azure ML web hizmeti okuyucu ve yazıcı modülleri ile veya olmadan herhangi GlobalParameters çalıştırmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="e43d1-262">Ancak, yalnızca bir Yukarı Akış işlem tamamlandığında hizmetini çağırmak için veri kümesi bağımlılıkları kullanan bir ardışık düzen hizmeti çağrıları katıştırmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="e43d1-263">Bu yaklaşımı kullanarak toplu iş yürütme tamamlandıktan sonra başka bir eylemi de tetikleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="e43d1-264">Bu durumda, etkinlik girişleri ve çıkışları, bunlardan herhangi birinin Web hizmeti girişleri veya çıkışları adlandırma olmadan kullanarak bağımlılıkları hızlı.</span><span class="sxs-lookup"><span data-stu-id="e43d1-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="e43d1-265">**Paketler** şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e43d1-265">The **takeaways** are:</span></span>

* <span data-ttu-id="e43d1-266">Deneme uç noktanızı bir WebServiceInput etkinliğine kullanıyorsa: blob veri kümesi temsil edilir ve etkinlik girişlerinde ve WebServiceInput etkinliğine özelliği dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="e43d1-267">Aksi takdirde WebServiceInput etkinliğine özelliği atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="e43d1-268">Deneme uç noktanızı webServiceOutput(s) kullanıyorsa: blob veri kümeleri ile temsil edilir ve etkinlik çıkışları ve webServiceOutputs özelliğinde dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="e43d1-269">Etkinlik çıkarır ve webServiceOutputs her çıktı denemede ada göre eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="e43d1-270">Aksi takdirde, webServiceOutputs özelliği atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="e43d1-271">GlobalParameter(s), deneme uç noktasını kullanıma sunar, bunlar etkinlik globalParameters özelliğinde anahtar, değer çiftleri olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="e43d1-272">Aksi takdirde, globalParameters özelliği atlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="e43d1-273">Anahtarlar büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-273">The keys are case-sensitive.</span></span> <span data-ttu-id="e43d1-274">[Azure Data Factory işlevleri](data-factory-functions-variables.md) değerleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="e43d1-275">Ek veri kümeleri içinde etkinlik typeProperties başvurulan olmadan etkinlik girişleri ve çıkışları özelliklerinde eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="e43d1-276">Bu veri kümeleri dilim bağımlılıkları kullanılarak yürütme yöneten ancak aksi AzureMLBatchExecution etkinlik tarafından göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="e43d1-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="e43d1-277">Kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="e43d1-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="e43d1-278">Yeniden eğitme ile tamamladıktan sonra Puanlama web hizmeti (web hizmeti olarak sunulan Tahmine dayalı denemeye) ile yeni eğitilen modelini kullanarak güncelleştirme **Azure ML güncelleştirme kaynak etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="e43d1-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="e43d1-279">Bkz: [kaynak güncelleştirme etkinliği kullanarak modelleri güncelleştirme](data-factory-azure-ml-update-resource-activity.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="e43d1-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="e43d1-280">Okuyucu ve yazıcı modülleri</span><span class="sxs-lookup"><span data-stu-id="e43d1-280">Reader and Writer Modules</span></span>
<span data-ttu-id="e43d1-281">Web hizmeti parametreleri kullanarak için yaygın bir senaryo Azure SQL okuyucuları ve yazıcıları kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="e43d1-282">Okuyucu modülü bir denemeyi Azure Machine Learning Studio dışında veri management hizmetlerinden veri yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="e43d1-283">Veri Yönetimi Hizmetleri Azure Machine Learning Studio dışında içine denemelerinizden verileri kaydetmek için yazıcı modülüdür.</span><span class="sxs-lookup"><span data-stu-id="e43d1-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="e43d1-284">Azure Blob/Azure SQL Okuyucu/Yazıcı hakkında daha fazla ayrıntı için bkz: [okuyucu](https://msdn.microsoft.com/library/azure/dn905997.aspx) ve [yazan](https://msdn.microsoft.com/library/azure/dn905984.aspx) MSDN Kitaplığı konularda.</span><span class="sxs-lookup"><span data-stu-id="e43d1-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="e43d1-285">Önceki bölümdeki örnek, Azure Blob okuyucu ve Azure Blob yazıcı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="e43d1-286">Bu bölümde, Azure SQL okuyucu ve Azure SQL yazıcı kullanarak anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="e43d1-287">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="e43d1-287">Frequently asked questions</span></span>
<span data-ttu-id="e43d1-288">**S:** my büyük veri ardışık düzen tarafından üretilen birden çok dosya vardır.</span><span class="sxs-lookup"><span data-stu-id="e43d1-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="e43d1-289">Tüm dosyalar üzerinde çalışmak için AzureMLBatchExecution etkinliği kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="e43d1-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="e43d1-290">**Y:** Evet.</span><span class="sxs-lookup"><span data-stu-id="e43d1-290">**A:** Yes.</span></span> <span data-ttu-id="e43d1-291">Bkz: **verileri Azure Blob içinde birden çok dosya okuma için bir okuyucu modülü kullanılarak** ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="e43d1-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="e43d1-292">Azure ML toplu iş Puanlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="e43d1-293">Kullanıyorsanız **AzureMLBatchScoring** Azure Machine Learning ile tümleştirmek için etkinlik en son kullanmanızı öneririz **AzureMLBatchExecution** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="e43d1-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="e43d1-294">AzureMLBatchExecution etkinlik sunulan Azure PowerShell ve Azure SDK'sını Ağustos 2015 sürümünde.</span><span class="sxs-lookup"><span data-stu-id="e43d1-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="e43d1-295">AzureMLBatchScoring etkinlik kullanmaya devam etmek istiyorsanız, bu bölümde okuma devam edin.</span><span class="sxs-lookup"><span data-stu-id="e43d1-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="e43d1-296">Giriş/çıkış için Azure Storage kullanarak azure ML toplu Puanlama etkinliği</span><span class="sxs-lookup"><span data-stu-id="e43d1-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="e43d1-297">Web hizmeti parametreleri</span><span class="sxs-lookup"><span data-stu-id="e43d1-297">Web Service Parameters</span></span>
<span data-ttu-id="e43d1-298">Web hizmeti parametreleri için değerleri belirlemek için ekleyin bir **typeProperties** için bölüm **AzureMLBatchScoringActivty** aşağıdaki örnekte gösterildiği gibi JSON ardışık düzeninde bölümünde:</span><span class="sxs-lookup"><span data-stu-id="e43d1-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="e43d1-299">Aynı zamanda [veri fabrikası işlevleri](data-factory-functions-variables.md) Web değerleri geçirme içinde parametreleri aşağıdaki örnekte gösterildiği gibi hizmet:</span><span class="sxs-lookup"><span data-stu-id="e43d1-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="e43d1-300">Web hizmeti parametreleri büyük/küçük harfe duyarlıdır, bu nedenle etkinliğin belirttiğiniz adları JSON Web hizmeti tarafından sunulan olanları eşleşmesini.</span><span class="sxs-lookup"><span data-stu-id="e43d1-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="e43d1-301">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e43d1-301">See Also</span></span>
* [<span data-ttu-id="e43d1-302">Azure blog gönderisi: Azure Machine Learning ve Azure Data Factory ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e43d1-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
