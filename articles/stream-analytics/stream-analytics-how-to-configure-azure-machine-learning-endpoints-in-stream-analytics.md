---
title: "Stream Analytics aaaUse Azure Machine Learning uç noktalarını | Microsoft Docs"
description: "Stream Analytics makine dili kullanıcı tanımlı işlevler"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="daac1-103">Stream Analytics öğrenme tümleştirmesine makine</span><span class="sxs-lookup"><span data-stu-id="daac1-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="daac1-104">Akış analizi, tooAzure Machine Learning uç noktaları arama kullanıcı tanımlı işlevler destekler.</span><span class="sxs-lookup"><span data-stu-id="daac1-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="daac1-105">Bu özellik için REST API desteği hello ayrıntılı [Stream Analytics REST API Kitaplığı](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="daac1-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="daac1-106">Bu makalede bu özelliği Stream Analytics de başarılı uygulama için gerekli ek bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="daac1-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="daac1-107">Öğreticinin Ayrıca gönderilen ve kullanılabilir [burada](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="daac1-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="daac1-108">Genel Bakış: Azure Machine Learning terminolojisi</span><span class="sxs-lookup"><span data-stu-id="daac1-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="daac1-109">Microsoft Azure Machine Learning sağlar kullanabileceğiniz bir işbirliğine dayalı, sürükle ve bırak aracı toobuild, test ve verilerinizi Tahmine dayalı analiz çözümlerini dağıtma.</span><span class="sxs-lookup"><span data-stu-id="daac1-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="daac1-110">Bu aracı hello adlı *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="daac1-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="daac1-111">Merhaba studio hello ile kullanılan toointeract olan Machine Learning kaynakları ve kolayca oluşturmanıza, test ve üzerinde tasarımınızı yinelemek.</span><span class="sxs-lookup"><span data-stu-id="daac1-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="daac1-112">Bu kaynaklar ve tanımları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="daac1-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="daac1-113">**Çalışma alanı**: Merhaba *çalışma* tüm diğer Machine Learning kaynakları birlikte yönetim ve denetimi için bir kapsayıcı tutan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="daac1-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="daac1-114">**Deneme**: *denemeler* machine learning modelini eğitmek ve veri bilimcilerine tooutilize veri kümeleri tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="daac1-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="daac1-115">**Uç nokta**: *uç noktaları* kullanılan nesnesi tootake özellikleri Azure Machine Learning'e giriş olarak Merhaba, belirtilen machine learning modelini uygulamak ve puanlanmış çıktı döndürür.</span><span class="sxs-lookup"><span data-stu-id="daac1-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="daac1-116">**Web hizmeti Puanlama**: A *webservice Puanlama* uç noktaları yukarıda belirtildiği gibi koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="daac1-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="daac1-117">Her uç nokta toplu iş yürütme ve zaman uyumlu yürütme için API'lere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="daac1-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="daac1-118">Akış analizi, zaman uyumlu yürütme kullanır.</span><span class="sxs-lookup"><span data-stu-id="daac1-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="daac1-119">Merhaba belirli hizmet adlandırılan bir [istek/yanıt hizmet](../machine-learning/machine-learning-consume-web-services.md) AzureML Studio'da.</span><span class="sxs-lookup"><span data-stu-id="daac1-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="daac1-120">Machine Learning akış analizi işleri için gerekli kaynakları</span><span class="sxs-lookup"><span data-stu-id="daac1-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="daac1-121">Hello amaçları doğrultusunda Stream Analytics işi, bir istek/yanıt uç noktası işleme bir [apikey ile yapılan](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), ve bir swagger tanımı başarılı yürütme için tüm gerekli.</span><span class="sxs-lookup"><span data-stu-id="daac1-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="daac1-122">Akış analizi swagger uç nokta için hello URL'si oluşturur, hello arabirimi arar ve varsayılan bir UDF tanımı toohello kullanıcı döndüren ek bir uç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="daac1-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="daac1-123">Bir akış analizi ve makine öğrenimi UDF REST API aracılığıyla yapılandırın</span><span class="sxs-lookup"><span data-stu-id="daac1-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="daac1-124">REST API'lerini kullanarak iş toocall Azure makine dili işlevlerinizi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daac1-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="daac1-125">Merhaba adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="daac1-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="daac1-126">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="daac1-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="daac1-127">Bir giriş tanımlayın</span><span class="sxs-lookup"><span data-stu-id="daac1-127">Define an input</span></span>
3. <span data-ttu-id="daac1-128">Bir çıkış tanımlayın</span><span class="sxs-lookup"><span data-stu-id="daac1-128">Define an output</span></span>
4. <span data-ttu-id="daac1-129">Kullanıcı tanımlı bir işlev (UDF) oluşturun</span><span class="sxs-lookup"><span data-stu-id="daac1-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="daac1-130">Stream Analytics dönüştürme çağrıları UDF hello yazma</span><span class="sxs-lookup"><span data-stu-id="daac1-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="daac1-131">Merhaba işi Başlat</span><span class="sxs-lookup"><span data-stu-id="daac1-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="daac1-132">Bir UDF temel özellikleri ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="daac1-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="daac1-133">Örnek olarak, aşağıdaki örnek kod hello adlı bir skaler UDF oluşturur *newudf* tooan Azure Machine Learning uç noktası bağlar.</span><span class="sxs-lookup"><span data-stu-id="daac1-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="daac1-134">Bu hello Not *endpoint* (hizmet URI'si), hizmet ve hello seçilen hello hello API Yardım sayfasında bulunabilir *apikey ile yapılan* hello Services ana sayfasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="daac1-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="daac1-135">Örnek istek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="daac1-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="daac1-136">RetrieveDefaultDefinition uç noktası için varsayılan UDF çağırın</span><span class="sxs-lookup"><span data-stu-id="daac1-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="daac1-137">Bir kez UDF hello tam UDF gerekli hello tanımını oluşturulan çatıyı hello.</span><span class="sxs-lookup"><span data-stu-id="daac1-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="daac1-138">Merhaba RetreiveDefaultDefinition endpoint hello varsayılan tanımı ilişkili tooan Azure Machine Learning uç noktası skaler bir işlev için size yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="daac1-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="daac1-139">Merhaba yükü aşağıdaki ilişkili tooan Azure Machine Learning uç noktası olan skaler bir işlev için tooget hello varsayılan UDF tanımı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="daac1-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="daac1-140">PUT isteği sırasında zaten sağlanmış gibi hello gerçek uç noktasını belirtmiyor.</span><span class="sxs-lookup"><span data-stu-id="daac1-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="daac1-141">Akış analizi açıkça sağlanırsa hello isteğinde sağlanan hello endpoint çağırır.</span><span class="sxs-lookup"><span data-stu-id="daac1-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="daac1-142">Aksi durumda hello bir ilk olarak başvurulan kullanır.</span><span class="sxs-lookup"><span data-stu-id="daac1-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="daac1-143">Tek bir dize parametresi (cümle) ve döndürür bu cümleyi hello "düşünceleri" etiketini gösteren dize türünde tek bir çıktı UDF alır hello.</span><span class="sxs-lookup"><span data-stu-id="daac1-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="daac1-144">Örnek istek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="daac1-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="daac1-145">Bu arama bir şey aşağıda istediğiniz bir örnek çıktı.</span><span class="sxs-lookup"><span data-stu-id="daac1-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="daac1-146">Düzeltme eki UDF hello yanıt</span><span class="sxs-lookup"><span data-stu-id="daac1-146">Patch UDF with hello response</span></span>
<span data-ttu-id="daac1-147">Şimdi hello UDF hello önceki yanıtıyla aşağıda gösterildiği gibi düzeltme eklerinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="daac1-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="daac1-148">İstek gövdesi (RetrieveDefaultDefinition çıktısını):</span><span class="sxs-lookup"><span data-stu-id="daac1-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="daac1-149">Stream Analytics dönüştürme toocall hello UDF uygulama</span><span class="sxs-lookup"><span data-stu-id="daac1-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="daac1-150">Şimdi hello (burada scoreTweet olarak adlandırılır) UDF giriş her olay için sorgu ve bu olay tooan çıkış için bir yanıt yazma.</span><span class="sxs-lookup"><span data-stu-id="daac1-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="daac1-151">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="daac1-151">Get help</span></span>
<span data-ttu-id="daac1-152">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="daac1-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="daac1-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="daac1-153">Next steps</span></span>
* [<span data-ttu-id="daac1-154">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="daac1-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="daac1-155">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="daac1-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="daac1-156">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="daac1-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="daac1-157">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="daac1-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="daac1-158">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="daac1-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
