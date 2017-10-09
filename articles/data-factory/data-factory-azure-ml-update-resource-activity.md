---
title: Azure Data Factory kullanarak aaaUpdate Machine Learning modellerini | Microsoft Docs
description: "Azure Data Factory ve Azure Machine Learning kullanarak Tahmine dayalı ardışık düzen toocreate oluşturma nasıl açıklar"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="f10d9-103">Azure Machine Learning modellerini kaynak güncelleştirme etkinliği kullanarak güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f10d9-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="f10d9-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="f10d9-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="f10d9-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="f10d9-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="f10d9-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="f10d9-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="f10d9-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="f10d9-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="f10d9-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="f10d9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="f10d9-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="f10d9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="f10d9-114">Bu makalede hazırlandı hello ana Azure Data Factory - Azure Machine Learning tümleştirme makale: [Azure Machine Learning ve Azure Data Factory kullanarak Tahmine dayalı işlem hatlarını oluşturmak](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="f10d9-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="f10d9-115">Zaten yapmadıysanız, bu makalede okumadan önce hello ana makalesini gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="f10d9-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="f10d9-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f10d9-116">Overview</span></span>
<span data-ttu-id="f10d9-117">Zaman içinde yeni giriş veri kümeleri kullanarak retrained toobe hello Tahmine dayalı modelleri hello Azure ML Puanlama denemeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="f10d9-118">Yeniden eğitme ile tamamladıktan sonra web hizmeti ile Merhaba Puanlama tooupdate hello ML model retrained istiyor.</span><span class="sxs-lookup"><span data-stu-id="f10d9-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="f10d9-119">Merhaba tooenable tipik adımları yeniden eğitme ve web Hizmetleri aracılığıyla güncelleştirme Azure ML modelleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f10d9-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="f10d9-120">Bir deneme oluşturma [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f10d9-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="f10d9-121">Merhaba modeliyle memnun kaldığınızda, her iki hello Azure ML Studio toopublish web hizmetlerini kullanmak **eğitim denemenizi** ve puanlama /**Tahmine dayalı denemeye**.</span><span class="sxs-lookup"><span data-stu-id="f10d9-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="f10d9-122">Merhaba aşağıdaki tabloda bu örnekte kullanılan hello web hizmetleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="f10d9-123">Bkz: [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](../machine-learning/machine-learning-retrain-models-programmatically.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="f10d9-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="f10d9-124">**Web hizmeti eğitim** - eğitim verileri alır ve eğitilmiş modeller üretir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="f10d9-125">Merhaba yeniden eğitme hello çıktı, Azure Blob depolamada .ilearner dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="f10d9-126">Merhaba **endpoint varsayılan** hello eğitim yayımladığınızda, bir web hizmeti olarak denemeler için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f10d9-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="f10d9-127">Daha fazla uç noktaları oluşturabilirsiniz, ancak yalnızca hello varsayılan uç nokta Merhaba örneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="f10d9-128">**Web hizmeti Puanlama** - etiketlenmemiş veri örnekleri alır ve tahminleri yapar.</span><span class="sxs-lookup"><span data-stu-id="f10d9-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="f10d9-129">Tahmin Hello çıktısını bir .csv dosyası veya hello deneme hello yapılandırmasına bağlı olarak bir Azure SQL veritabanında satır gibi çeşitli formlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="f10d9-130">bir web hizmeti olarak hello Tahmine dayalı denemeye yayımladığınızda hello varsayılan uç sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f10d9-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="f10d9-131">Merhaba aşağıdaki resimde eğitim ve uç noktaları Azure ML Puanlama arasında hello ilişki gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![Web Hizmetleri](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="f10d9-133">Merhaba çağırabileceği **web hizmeti eğitim** hello kullanarak **Azure ML toplu iş yürütme etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="f10d9-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="f10d9-134">Eğitim web hizmetini çağırmak için Puanlama verileri (web hizmeti Puanlama) bir Azure ML web Hizmeti'ni çağırmadan olarak aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="f10d9-135">Önceki bölümlerde kapak nasıl tooinvoke bir Azure Data Factory Azure ML web hizmetinden kanal ayrıntılı olarak hello.</span><span class="sxs-lookup"><span data-stu-id="f10d9-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="f10d9-136">Merhaba çağırabileceği **web hizmeti Puanlama** hello kullanarak **Azure ML kaynak güncelleştirme etkinliği** tooupdate hello web hizmeti ile Merhaba yeni eğitilen model.</span><span class="sxs-lookup"><span data-stu-id="f10d9-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="f10d9-137">Örnek hello bağlantılı hizmet tanımlarını sağlar:</span><span class="sxs-lookup"><span data-stu-id="f10d9-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="f10d9-138">Klasik web hizmeti olan Web hizmeti Puanlama</span><span class="sxs-lookup"><span data-stu-id="f10d9-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="f10d9-139">Web hizmeti Puanlama hello ise bir **Klasik web hizmeti**, hello ikinci oluşturma **varsayılan olmayan ve güncelleştirilebilir uç nokta** hello kullanarak [Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f10d9-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="f10d9-140">Bkz [uç noktalar oluşturmak](../machine-learning/machine-learning-create-endpoint.md) adımları makalesinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f10d9-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="f10d9-141">Merhaba varsayılan olmayan güncelleştirilebilir endpoint oluşturduktan sonra aşağıdaki adımları hello:</span><span class="sxs-lookup"><span data-stu-id="f10d9-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="f10d9-142">Tıklatın **toplu iş yürütme** tooget hello URI değeri Merhaba **mlEndpoint** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="f10d9-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="f10d9-143">Tıklatın **güncelleştirme kaynağı** bağlantı tooget hello URI değeri hello **updateResourceEndpoint** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="f10d9-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="f10d9-144">Merhaba API hello uç nokta sayfasının kendinde (Merhaba sağ alt köşedeki) anahtardır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![güncelleştirilebilir uç noktası](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="f10d9-146">Aşağıdaki örnek hello hello AzureML bağlantılı hizmeti için bir örnek JSON tanım sağlar.</span><span class="sxs-lookup"><span data-stu-id="f10d9-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="f10d9-147">Merhaba bağlantılı hizmet hello apikey ile yapılan kimlik doğrulaması için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-147">hello linked service uses hello apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="f10d9-148">Web hizmeti Puanlama Azure Resource Manager web hizmetidir</span><span class="sxs-lookup"><span data-stu-id="f10d9-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="f10d9-149">Merhaba web hizmeti hello yeni bir Azure Kaynak Yöneticisi uç noktasını kullanıma sunar web hizmeti türde ise, tooadd hello ikinci gerekmez **varsayılan olmayan** uç noktası.</span><span class="sxs-lookup"><span data-stu-id="f10d9-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="f10d9-150">Merhaba **updateResourceEndpoint** hello bağlantılı hizmet hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f10d9-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="f10d9-151">Değerleri hello URL'deki yer tutucu için hello hello web hizmeti sorgulanırken alabileceğiniz [Azure Machine Learning Web Hizmetleri portalı](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="f10d9-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="f10d9-152">güncelleştirme kaynağı endpoint Hello yeni tür bir AAD (Azure Active Directory) belirteç gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f10d9-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="f10d9-153">Belirtin **servicePrincipalId** ve **servicePrincipalKey**içinde AzureML bağlantılı hizmetinin.</span><span class="sxs-lookup"><span data-stu-id="f10d9-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="f10d9-154">Bkz: [nasıl toocreate hizmet sorumlusu ve izinleri toomanage Azure kaynak atama](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f10d9-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="f10d9-155">Örnek AzureML bağlantılı hizmet tanımı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f10d9-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="f10d9-156">Merhaba aşağıdaki senaryoyu daha fazla ayrıntı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f10d9-156">hello following scenario provides more details.</span></span> <span data-ttu-id="f10d9-157">Yeniden eğitme ve bir Azure Data Factory işlem hattı Azure ML modellerinden güncelleştirmek için bir örnek vardır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="f10d9-158">Senaryo: yeniden eğitme ve bir Azure ML model güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="f10d9-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="f10d9-159">Bu bölümde hello kullanan örnek bir işlem hattı **Azure ML toplu iş yürütme etkinliği** tooretrain bir model.</span><span class="sxs-lookup"><span data-stu-id="f10d9-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="f10d9-160">Merhaba ardışık düzen de hello kullanır **Azure ML güncelleştirme kaynağı etkinlik** tooupdate hello web hizmeti Puanlama hello modelinde.</span><span class="sxs-lookup"><span data-stu-id="f10d9-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="f10d9-161">bağlı hizmetler, veri kümelerini ve ardışık düzen hello örnekte tüm JSON parçacıklarını hello Hello bölüm de sağlar.</span><span class="sxs-lookup"><span data-stu-id="f10d9-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="f10d9-162">Merhaba diyagram görünümü hello örnek ardışık aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="f10d9-163">Gördüğünüz gibi hello Azure ML toplu iş yürütme etkinliği hello eğitim girdi alır ve eğitim çıktı (iLearner dosyası) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f10d9-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="f10d9-164">Bu eğitim Çıktı Hello Azure ML kaynak güncelleştirme etkinliği alır ve web hizmeti uç noktası Puanlama hello modelinde güncelleştirmeleri hello.</span><span class="sxs-lookup"><span data-stu-id="f10d9-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="f10d9-165">Merhaba kaynak güncelleştirme etkinliği herhangi bir çıktı üretmez.</span><span class="sxs-lookup"><span data-stu-id="f10d9-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="f10d9-166">Merhaba placeholderBlob hello Azure Data Factory hizmeti toorun hello ardışık düzen tarafından gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![ardışık düzeni diyagramı](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="f10d9-168">Azure Blob storage bağlı hizmeti:</span><span class="sxs-lookup"><span data-stu-id="f10d9-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="f10d9-169">Hello Azure Storage veri aşağıdaki hello tutar:</span><span class="sxs-lookup"><span data-stu-id="f10d9-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="f10d9-170">Eğitim verileri.</span><span class="sxs-lookup"><span data-stu-id="f10d9-170">training data.</span></span> <span data-ttu-id="f10d9-171">Merhaba hello Azure ML eğitim web hizmeti için giriş verileri.</span><span class="sxs-lookup"><span data-stu-id="f10d9-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="f10d9-172">iLearner dosya.</span><span class="sxs-lookup"><span data-stu-id="f10d9-172">iLearner file.</span></span> <span data-ttu-id="f10d9-173">Merhaba Hello Azure ML eğitim web hizmetinden çıktı.</span><span class="sxs-lookup"><span data-stu-id="f10d9-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="f10d9-174">Bu ayrıca hello giriş toohello güncelleştirme kaynağı etkinlik dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="f10d9-175">Merhaba örnek JSON hello bağlantılı hizmet tanımını şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f10d9-175">Here is hello sample JSON definition of hello linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="f10d9-176">Eğitim girdi veri kümesi:</span><span class="sxs-lookup"><span data-stu-id="f10d9-176">Training input dataset:</span></span>
<span data-ttu-id="f10d9-177">Merhaba aşağıdaki dataset hello giriş eğitim verilerini hello Azure ML eğitim web hizmeti temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f10d9-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="f10d9-178">Hello Azure ML toplu iş yürütme etkinliği bu veri kümesine bir girdi olarak alır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="f10d9-179">Eğitim çıktı veri kümesi:</span><span class="sxs-lookup"><span data-stu-id="f10d9-179">Training output dataset:</span></span>
<span data-ttu-id="f10d9-180">Merhaba aşağıdaki dataset hello çıktı iLearner dosya hello Azure ML eğitim web hizmetinden temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f10d9-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="f10d9-181">Hello Azure ML toplu iş yürütme etkinliği bu veri kümesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f10d9-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="f10d9-182">Bu veri kümesi de hello giriş toohello Azure ML güncelleştirme kaynağı etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="f10d9-183">Azure ML eğitim uç noktası için bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="f10d9-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="f10d9-184">JSON parçacığı aşağıdaki hello hello eğitim web hizmetinin toohello varsayılan uç noktaları bir Azure Machine Learning bağlantılı hizmeti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f10d9-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="f10d9-185">İçinde **Azure ML Studio**, tooget değerlerini aşağıdaki hello **mlEndpoint** ve **apikey ile yapılan**:</span><span class="sxs-lookup"><span data-stu-id="f10d9-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="f10d9-186">Tıklatın **WEB Hizmetleri** hello sol menüdeki.</span><span class="sxs-lookup"><span data-stu-id="f10d9-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="f10d9-187">Merhaba tıklatın **web hizmeti eğitim** hello listesinde web hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="f10d9-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="f10d9-188">Sonraki çok Kopyala**API anahtarı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="f10d9-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="f10d9-189">Başlangıç anahtarı hello Pano'da hello veri fabrikası JSON düzenleyicisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f10d9-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="f10d9-190">Merhaba, **Azure ML studio**, tıklatın **toplu iş yürütme** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="f10d9-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="f10d9-191">Kopya hello **istek URI'si** hello gelen **isteği** bölümünde ve hello veri fabrikası JSON düzenleyicisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f10d9-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="f10d9-192">Bağlantılı hizmeti Azure ML güncelleştirilebilir Puanlama uç noktası için:</span><span class="sxs-lookup"><span data-stu-id="f10d9-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="f10d9-193">JSON parçacığı aşağıdaki hello toohello varsayılan olmayan web hizmeti Puanlama hello güncelleştirilebilir uç noktaları bir Azure Machine Learning bağlantılı hizmeti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f10d9-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="f10d9-194">Yer tutucu çıktı veri kümesi:</span><span class="sxs-lookup"><span data-stu-id="f10d9-194">Placeholder output dataset:</span></span>
<span data-ttu-id="f10d9-195">Hello Azure ML güncelleştirme kaynağı etkinlik herhangi bir çıktı üretmez.</span><span class="sxs-lookup"><span data-stu-id="f10d9-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="f10d9-196">Ancak, Azure Data Factory işlem hattı bir çıkış veri kümesi toodrive hello zamanlamasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="f10d9-197">Bu nedenle, bir kukla/yer tutucu veri kümesi bu örnekte kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f10d9-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="f10d9-198">İşlem hattı</span><span class="sxs-lookup"><span data-stu-id="f10d9-198">Pipeline</span></span>
<span data-ttu-id="f10d9-199">Merhaba işlem hattına sahip iki etkinlik: **AzureMLBatchExecution** ve **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="f10d9-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="f10d9-200">Hello Azure ML toplu iş yürütme etkinliği hello eğitim veri giriş olarak alır ve bir iLearner dosya bir çıktı olarak üretir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="f10d9-201">Merhaba etkinlik verileri eğitim hello girişle hello eğitim web hizmeti (web hizmeti olarak sunulan eğitim denemenizi) çağırır ve hello webservice hello ilearner dosya alır.</span><span class="sxs-lookup"><span data-stu-id="f10d9-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="f10d9-202">Merhaba placeholderBlob hello Azure Data Factory hizmeti toorun hello ardışık düzen tarafından gerekli olan yalnızca bir kukla çıktı veri kümesi ' dir.</span><span class="sxs-lookup"><span data-stu-id="f10d9-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![ardışık düzeni diyagramı](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
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
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
