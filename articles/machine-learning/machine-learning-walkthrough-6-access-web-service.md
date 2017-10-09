---
title: "6. adım: Hello Machine Learning Web hizmetine erişim | Microsoft Docs"
description: "6. adımını hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: etkin bir Azure Machine Learning Web hizmetine erişim."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="40f8d-103">Gözden geçirme adım 6: hello Azure Machine Learning web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="40f8d-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="40f8d-104">Merhaba kılavuzun hello son adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="40f8d-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="40f8d-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="40f8d-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="40f8d-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="40f8d-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="40f8d-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="40f8d-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="40f8d-108">Eğitmek ve hello modelleri değerlendir</span><span class="sxs-lookup"><span data-stu-id="40f8d-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="40f8d-109">Merhaba Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="40f8d-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="40f8d-110">**Merhaba Web hizmetine erişim**</span><span class="sxs-lookup"><span data-stu-id="40f8d-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="40f8d-111">Bu kılavuzda hello önceki adımda bizim kredi riskini tahmin modelini kullanan bir web hizmeti dağıttığımız.</span><span class="sxs-lookup"><span data-stu-id="40f8d-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="40f8d-112">Artık kullanıcılar mümkün toosend veri tooit ve sonuçları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="40f8d-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="40f8d-113">Merhaba Web hizmetini alabilen ve iki yoldan biriyle REST API'lerini kullanarak verileri döndürmek bir Azure web hizmetidir:</span><span class="sxs-lookup"><span data-stu-id="40f8d-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="40f8d-114">**İstek/yanıt** - hello kullanıcı bir gönderir veya kredi veri toohello daha fazla satır hizmeti bir HTTP protokolünü kullanarak ve hello sonuçlarının bir veya daha fazla kümeleriyle hizmet yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="40f8d-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="40f8d-115">**Toplu yürütme** - hello kullanıcı depolayan bir veya daha fazla satır kredi Azure blob ve hello blob konumu toohello hizmetine gönderir.</span><span class="sxs-lookup"><span data-stu-id="40f8d-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="40f8d-116">Giriş blob tüm satır hello hello hizmet puanları Merhaba, bu kapsayıcı URL'sini hello başka bir blob'a sonuçlanır ve döndürür depolarını hello.</span><span class="sxs-lookup"><span data-stu-id="40f8d-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="40f8d-117">Klasik web hizmeti hello olan hızlı ve kolay bir yol tooaccess hello [Azure ML istek-yanıt hizmeti Web uygulaması](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) veya [Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="40f8d-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="40f8d-118">Bu web uygulaması şablonlar web hizmetinizin giriş verilerini ve ne döndürülecek bilir bir özel web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40f8d-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="40f8d-119">Tek toodo ihtiyacınız olan erişim tooyour web hizmeti ve verileri sağlar ve hello şablon rest hello.</span><span class="sxs-lookup"><span data-stu-id="40f8d-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="40f8d-120">Merhaba web uygulama şablonları kullanma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning Web hizmeti bir web uygulaması şablonu kullanmak](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="40f8d-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="40f8d-121">R, C# ve Python programlama dilleri, için sağlanan starter kod kullanarak bir özel uygulama tooaccess hello web hizmeti de geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40f8d-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="40f8d-122">Tam ayrıntıları bulabilirsiniz [nasıl tooconsume bir Azure Machine Learning Web hizmeti](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="40f8d-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

