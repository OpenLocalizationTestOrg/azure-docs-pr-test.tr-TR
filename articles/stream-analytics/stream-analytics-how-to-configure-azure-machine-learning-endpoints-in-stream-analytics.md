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
# <a name="machine-learning-integration-in-stream-analytics"></a>Stream Analytics öğrenme tümleştirmesine makine
Akış analizi, tooAzure Machine Learning uç noktaları arama kullanıcı tanımlı işlevler destekler. Bu özellik için REST API desteği hello ayrıntılı [Stream Analytics REST API Kitaplığı](https://msdn.microsoft.com/library/azure/dn835031.aspx). Bu makalede bu özelliği Stream Analytics de başarılı uygulama için gerekli ek bilgiler sağlar. Öğreticinin Ayrıca gönderilen ve kullanılabilir [burada](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Genel Bakış: Azure Machine Learning terminolojisi
Microsoft Azure Machine Learning sağlar kullanabileceğiniz bir işbirliğine dayalı, sürükle ve bırak aracı toobuild, test ve verilerinizi Tahmine dayalı analiz çözümlerini dağıtma. Bu aracı hello adlı *Azure Machine Learning Studio*. Merhaba studio hello ile kullanılan toointeract olan Machine Learning kaynakları ve kolayca oluşturmanıza, test ve üzerinde tasarımınızı yinelemek. Bu kaynaklar ve tanımları aşağıda verilmiştir.

* **Çalışma alanı**: Merhaba *çalışma* tüm diğer Machine Learning kaynakları birlikte yönetim ve denetimi için bir kapsayıcı tutan bir kapsayıcıdır.
* **Deneme**: *denemeler* machine learning modelini eğitmek ve veri bilimcilerine tooutilize veri kümeleri tarafından oluşturulur.
* **Uç nokta**: *uç noktaları* kullanılan nesnesi tootake özellikleri Azure Machine Learning'e giriş olarak Merhaba, belirtilen machine learning modelini uygulamak ve puanlanmış çıktı döndürür.
* **Web hizmeti Puanlama**: A *webservice Puanlama* uç noktaları yukarıda belirtildiği gibi koleksiyonudur.

Her uç nokta toplu iş yürütme ve zaman uyumlu yürütme için API'lere sahiptir. Akış analizi, zaman uyumlu yürütme kullanır. Merhaba belirli hizmet adlandırılan bir [istek/yanıt hizmet](../machine-learning/machine-learning-consume-web-services.md) AzureML Studio'da.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Machine Learning akış analizi işleri için gerekli kaynakları
Hello amaçları doğrultusunda Stream Analytics işi, bir istek/yanıt uç noktası işleme bir [apikey ile yapılan](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), ve bir swagger tanımı başarılı yürütme için tüm gerekli. Akış analizi swagger uç nokta için hello URL'si oluşturur, hello arabirimi arar ve varsayılan bir UDF tanımı toohello kullanıcı döndüren ek bir uç nokta vardır.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Bir akış analizi ve makine öğrenimi UDF REST API aracılığıyla yapılandırın
REST API'lerini kullanarak iş toocall Azure makine dili işlevlerinizi yapılandırabilirsiniz. Merhaba adımlar aşağıdaki gibidir:

1. Akış Analizi işi oluşturma
2. Bir giriş tanımlayın
3. Bir çıkış tanımlayın
4. Kullanıcı tanımlı bir işlev (UDF) oluşturun
5. Stream Analytics dönüştürme çağrıları UDF hello yazma
6. Merhaba işi Başlat

## <a name="creating-a-udf-with-basic-properties"></a>Bir UDF temel özellikleri ile oluşturma
Örnek olarak, aşağıdaki örnek kod hello adlı bir skaler UDF oluşturur *newudf* tooan Azure Machine Learning uç noktası bağlar. Bu hello Not *endpoint* (hizmet URI'si), hizmet ve hello seçilen hello hello API Yardım sayfasında bulunabilir *apikey ile yapılan* hello Services ana sayfasında bulunabilir.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Örnek istek gövdesi:  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>RetrieveDefaultDefinition uç noktası için varsayılan UDF çağırın
Bir kez UDF hello tam UDF gerekli hello tanımını oluşturulan çatıyı hello. Merhaba RetreiveDefaultDefinition endpoint hello varsayılan tanımı ilişkili tooan Azure Machine Learning uç noktası skaler bir işlev için size yardımcı olur. Merhaba yükü aşağıdaki ilişkili tooan Azure Machine Learning uç noktası olan skaler bir işlev için tooget hello varsayılan UDF tanımı gerektirir. PUT isteği sırasında zaten sağlanmış gibi hello gerçek uç noktasını belirtmiyor. Akış analizi açıkça sağlanırsa hello isteğinde sağlanan hello endpoint çağırır. Aksi durumda hello bir ilk olarak başvurulan kullanır. Tek bir dize parametresi (cümle) ve döndürür bu cümleyi hello "düşünceleri" etiketini gösteren dize türünde tek bir çıktı UDF alır hello.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Örnek istek gövdesi:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Bu arama bir şey aşağıda istediğiniz bir örnek çıktı.  

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

## <a name="patch-udf-with-hello-response"></a>Düzeltme eki UDF hello yanıt
Şimdi hello UDF hello önceki yanıtıyla aşağıda gösterildiği gibi düzeltme eklerinin gerekir.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

İstek gövdesi (RetrieveDefaultDefinition çıktısını):

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Stream Analytics dönüştürme toocall hello UDF uygulama
Şimdi hello (burada scoreTweet olarak adlandırılır) UDF giriş her olay için sorgu ve bu olay tooan çıkış için bir yanıt yazma.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Yardım alın
Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Giriş tooAzure akış analizi](stream-analytics-introduction.md)
* [Azure Akış Analizi'ni kullanmaya başlama](stream-analytics-real-time-fraud-detection.md)
* [Azure Akış Analizi işlerini ölçeklendirme](stream-analytics-scale-jobs.md)
* [Azure Akış Analizi Sorgu Dili Başvurusu](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Akış Analizi Yönetimi REST API'si Başvurusu](https://msdn.microsoft.com/library/azure/dn835031.aspx)
