---
title: "6. adım: Machine Learning Web hizmetine erişim | Microsoft Docs"
description: "6. adımını geliştirme Tahmine dayalı bir çözüm izlenecek yol: etkin bir Azure Machine Learning Web hizmetine erişim."
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
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="ea356-103">Kılavuz Adımı 6: Azure Machine Learning web hizmetine erişim</span><span class="sxs-lookup"><span data-stu-id="ea356-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="ea356-104">Bu izlenecek yol son adımdır [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="ea356-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="ea356-105">Bir Machine Learning çalışma alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea356-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="ea356-106">Mevcut verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="ea356-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="ea356-107">Yeni bir deneme oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea356-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="ea356-108">Modelleri eğitme ve değerlendirme</span><span class="sxs-lookup"><span data-stu-id="ea356-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="ea356-109">Web hizmetini dağıtma</span><span class="sxs-lookup"><span data-stu-id="ea356-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="ea356-110">**Web hizmetine erişim**</span><span class="sxs-lookup"><span data-stu-id="ea356-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="ea356-111">Bu kılavuzda önceki adımda bizim kredi riskini tahmin modelini kullanan bir web hizmeti dağıttığımız.</span><span class="sxs-lookup"><span data-stu-id="ea356-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="ea356-112">Artık kullanıcıların veri göndermek ve sonuçları almak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea356-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="ea356-113">Web hizmetini alabilen ve dönüş verileri iki yoldan biriyle REST API'lerini kullanarak bir Azure web hizmetidir:</span><span class="sxs-lookup"><span data-stu-id="ea356-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="ea356-114">**İstek/yanıt** - kullanıcı, bir HTTP protokolünü kullanarak hizmete kredi veri bir veya daha fazla satırı gönderir ve hizmeti bir veya daha fazla sonuç kümeleri yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="ea356-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="ea356-115">**Toplu yürütme** - kullanıcı depolar veya daha fazla satır kredi Azure blob ve blob konumu hizmetine gönderir.</span><span class="sxs-lookup"><span data-stu-id="ea356-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="ea356-116">Hizmet giriş blob veri tüm satırları puanlar, başka bir blob'a sonuçları depolar ve bu kapsayıcı URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="ea356-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="ea356-117">Klasik web hizmetine erişmek için hızlı ve kolay yolunu [Azure ML istek-yanıt hizmeti Web uygulaması](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) veya [Azure ML toplu iş yürütme hizmeti Web uygulaması şablonu](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="ea356-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="ea356-118">Bu web uygulaması şablonlar web hizmetinizin giriş verilerini ve ne döndürülecek bilir bir özel web uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea356-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="ea356-119">Yapmanız gereken tek şey web hizmeti ve veri erişim sağlar ve geri kalan şablon yapar.</span><span class="sxs-lookup"><span data-stu-id="ea356-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="ea356-120">Web uygulama şablonları kullanma hakkında daha fazla bilgi için bkz: [bir Azure Machine Learning Web hizmeti bir web uygulaması şablonu kullanmak](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="ea356-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="ea356-121">Ayrıca sizin için R, C# ve Python programlama dili sağlanan Başlatıcı kodu kullanarak web hizmetine erişmek için özel bir uygulama geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea356-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="ea356-122">Tam ayrıntıları bulabilirsiniz [bir Azure Machine Learning Web hizmeti kullanmak nasıl](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="ea356-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

