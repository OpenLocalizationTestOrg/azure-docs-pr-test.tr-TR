---
title: "Stream Analytics Azure Machine Learning uç noktaları kullanma | Microsoft Docs"
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
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="febd4-103">Stream Analytics öğrenme tümleştirmesine makine</span><span class="sxs-lookup"><span data-stu-id="febd4-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="febd4-104">Akış analizi, Azure Machine Learning Uç noktalara duyurmak kullanıcı tanımlı işlevler destekler.</span><span class="sxs-lookup"><span data-stu-id="febd4-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="febd4-105">Bu özellik için REST API desteği ayrıntılı olarak [Stream Analytics REST API Kitaplığı](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="febd4-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="febd4-106">Bu makalede bu özelliği Stream Analytics de başarılı uygulama için gerekli ek bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="febd4-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="febd4-107">Öğreticinin Ayrıca gönderilen ve kullanılabilir [burada](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="febd4-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="febd4-108">Genel Bakış: Azure Machine Learning terminolojisi</span><span class="sxs-lookup"><span data-stu-id="febd4-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="febd4-109">Microsoft Azure Machine Learning derleme, test ve verilerinizi Tahmine dayalı analiz çözümlerini dağıtmak için kullanabileceğiniz bir işbirliğine dayalı, sürükle ve bırak aracı sağlar.</span><span class="sxs-lookup"><span data-stu-id="febd4-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="febd4-110">Bu aracı adlı *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="febd4-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="febd4-111">Studio Machine Learning kaynakları ile etkileşim kurar ve kolayca derleme, test ve üzerinde tasarımınızı yinelemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="febd4-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="febd4-112">Bu kaynaklar ve tanımları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="febd4-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="febd4-113">**Çalışma alanı**: *çalışma* tüm diğer Machine Learning kaynakları birlikte yönetim ve denetimi için bir kapsayıcı tutan bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="febd4-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="febd4-114">**Deneme**: *denemeler* veri kümeleri kullanan ve makine öğrenimi modeli eğitmek için veri bilimcilerine tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="febd4-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="febd4-115">**Uç nokta**: *uç noktaları* özellikleri giriş olarak alın, belirtilen makine öğrenimi modeline uygulayın ve puanlanmış çıkışı döndürmek için kullanılan Azure Machine Learning nesnesi.</span><span class="sxs-lookup"><span data-stu-id="febd4-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="febd4-116">**Web hizmeti Puanlama**: A *webservice Puanlama* uç noktaları yukarıda belirtildiği gibi koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="febd4-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="febd4-117">Her uç nokta toplu iş yürütme ve zaman uyumlu yürütme için API'lere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="febd4-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="febd4-118">Akış analizi, zaman uyumlu yürütme kullanır.</span><span class="sxs-lookup"><span data-stu-id="febd4-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="febd4-119">Belirli hizmet adlı bir [istek/yanıt hizmet](../machine-learning/machine-learning-consume-web-services.md) AzureML Studio'da.</span><span class="sxs-lookup"><span data-stu-id="febd4-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="febd4-120">Machine Learning akış analizi işleri için gerekli kaynakları</span><span class="sxs-lookup"><span data-stu-id="febd4-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="febd4-121">Stream Analytics amaçları doğrultusunda işi, bir istek/yanıt uç noktası işleme bir [apikey ile yapılan](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), ve bir swagger tanımı başarılı yürütme için tüm gerekli.</span><span class="sxs-lookup"><span data-stu-id="febd4-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="febd4-122">Akış analizi için swagger uç nokta URL'si oluşturur, arabirimi arar ve bir varsayılan UDF tanımı kullanıcıya döndürür bir ek bir uç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="febd4-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="febd4-123">Bir akış analizi ve makine öğrenimi UDF REST API aracılığıyla yapılandırın</span><span class="sxs-lookup"><span data-stu-id="febd4-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="febd4-124">REST API'lerini kullanarak işinizi Azure makine dili işlevleri çağırmak üzere yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="febd4-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="febd4-125">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="febd4-125">The steps are as follows:</span></span>

1. <span data-ttu-id="febd4-126">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="febd4-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="febd4-127">Bir giriş tanımlayın</span><span class="sxs-lookup"><span data-stu-id="febd4-127">Define an input</span></span>
3. <span data-ttu-id="febd4-128">Bir çıkış tanımlayın</span><span class="sxs-lookup"><span data-stu-id="febd4-128">Define an output</span></span>
4. <span data-ttu-id="febd4-129">Kullanıcı tanımlı bir işlev (UDF) oluşturun</span><span class="sxs-lookup"><span data-stu-id="febd4-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="febd4-130">UDF çağıran bir akış analizi dönüştürmesi yazma</span><span class="sxs-lookup"><span data-stu-id="febd4-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="febd4-131">İşi Başlat</span><span class="sxs-lookup"><span data-stu-id="febd4-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="febd4-132">Bir UDF temel özellikleri ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="febd4-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="febd4-133">Örnek olarak, aşağıdaki örnek kod adlı bir skaler UDF oluşturur *newudf* bir Azure Machine Learning uç noktasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="febd4-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="febd4-134">Unutmayın *endpoint* (hizmet URI'si), seçtiğiniz hizmet için API Yardım sayfasında bulunabilir ve *apikey ile yapılan* Services ana sayfasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="febd4-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="febd4-135">Örnek istek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="febd4-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="febd4-136">RetrieveDefaultDefinition uç noktası için varsayılan UDF çağırın</span><span class="sxs-lookup"><span data-stu-id="febd4-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="febd4-137">Çatıyı UDF oluşturulduktan sonra UDF tam tanımı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="febd4-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="febd4-138">RetreiveDefaultDefinition uç noktası, bir Azure Machine Learning uç noktasına bağlı skaler bir işlev için varsayılan tanımı alma yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="febd4-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="febd4-139">Yükü bir Azure Machine Learning uç noktasına bağlı skaler bir işlev için varsayılan UDF tanımını almanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="febd4-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="febd4-140">PUT isteği sırasında zaten sağlanmış gibi gerçek uç noktasını belirtmiyor.</span><span class="sxs-lookup"><span data-stu-id="febd4-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="febd4-141">Akış analizi açıkça sağlanırsa istek sağlanan uç noktanın çağırır.</span><span class="sxs-lookup"><span data-stu-id="febd4-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="febd4-142">Aksi durumda ilk olarak başvurulan bir kullanır.</span><span class="sxs-lookup"><span data-stu-id="febd4-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="febd4-143">Burada tek bir dize türü tek bir çıktı parametresi (cümle) ve döndürür UDF alır bu cümleyi "düşünceleri" etiketi belirten dize.</span><span class="sxs-lookup"><span data-stu-id="febd4-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="febd4-144">Örnek istek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="febd4-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="febd4-145">Bu arama bir şey aşağıda istediğiniz bir örnek çıktı.</span><span class="sxs-lookup"><span data-stu-id="febd4-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="febd4-146">Düzeltme eki UDF yanıt</span><span class="sxs-lookup"><span data-stu-id="febd4-146">Patch UDF with the response</span></span>
<span data-ttu-id="febd4-147">Şimdi UDF önceki Yanıtla, aşağıda gösterildiği gibi düzeltme eklerinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="febd4-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="febd4-148">İstek gövdesi (RetrieveDefaultDefinition çıktısını):</span><span class="sxs-lookup"><span data-stu-id="febd4-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="febd4-149">UDF çağırmak için Stream Analytics dönüşüm uygulayın</span><span class="sxs-lookup"><span data-stu-id="febd4-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="febd4-150">Şimdi giriş her olay için (burada scoreTweet olarak adlandırılır) UDF sorgulayabilir ve bu olay için bir yanıt için bir çıktı yazma.</span><span class="sxs-lookup"><span data-stu-id="febd4-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="febd4-151">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="febd4-151">Get help</span></span>
<span data-ttu-id="febd4-152">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="febd4-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="febd4-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="febd4-153">Next steps</span></span>
* [<span data-ttu-id="febd4-154">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="febd4-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="febd4-155">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="febd4-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="febd4-156">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="febd4-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="febd4-157">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="febd4-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="febd4-158">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="febd4-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
