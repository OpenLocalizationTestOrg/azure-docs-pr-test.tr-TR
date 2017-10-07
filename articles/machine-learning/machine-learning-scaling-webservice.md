---
title: "bir Azure Machine Learning web hizmetini aaaHow tooincrease eşzamanlılığı | Microsoft Docs"
description: "Nasıl tooincrease eşzamanlılığı bir Azure Machine Learning web hizmeti ek uç noktaları ekleyerek öğrenin."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "azure machine Learning web hizmetlerini ölçeklendirme, uç nokta, eşzamanlılık operationalization"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="b2e45-104">Ek uç noktaları ekleyerek bir Azure Machine Learning web hizmetini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b2e45-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="b2e45-105">Bu konu, geçerli tooa teknikleri açıklar **Klasik** Machine Learning Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b2e45-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="b2e45-106">Varsayılan olarak, her yayımlanan Web hizmeti yapılandırılmış toosupport 20 eş zamanlı istekler ve 200 eş zamanlı istekleri olarak yüksek olabilir.</span><span class="sxs-lookup"><span data-stu-id="b2e45-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="b2e45-107">Hello Klasik Azure portalı bu değer bir şekilde tooset sağlarken, Azure Machine Learning otomatik olarak hello ayarı tooprovide hello en iyi performansı web hizmetiniz için en iyi duruma getirir ve hello portal değeri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="b2e45-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="b2e45-108">Toocall hello API 200 en fazla eşzamanlı çağrıları değeri destekleyecek daha yüksek bir yük ile planlıyorsanız, birden çok uç nokta üzerinde hello oluşturmalısınız aynı Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b2e45-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="b2e45-109">Ardından rastgele yük bunların tümünün arasında dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e45-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="b2e45-110">bir Web hizmeti Hello ölçeklendirme ortak bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="b2e45-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="b2e45-111">Bazı nedenlerden tooscale olan 200 eş zamanlı istekleri birden çok toosupport, birden fazla uç noktası aracılığıyla kullanılabilirliğini artırmak veya hello web hizmeti için ayrı uç noktaları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b2e45-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="b2e45-112">Hello için ek uç noktaları ekleyerek hello ölçek artırabilir aynı Web hizmeti aracılığıyla [Klasik Azure portalı](https://manage.windowsazure.com/) veya hello [Azure Machine Learning Web hizmeti](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="b2e45-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="b2e45-113">Yeni uç nokta ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="b2e45-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="b2e45-114">Bir yüksek eşzamanlılık sayısı kullanarak hello API gelenlere yüksek oranda ile arıyoruz değil, detrimental göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b2e45-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="b2e45-115">Yüksek yük için yapılandırılmış bir API nispeten düşük yük yerleştirirseniz hello gecikme ara sıra zaman aşımları ve/veya ani görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e45-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="b2e45-116">Merhaba, zaman uyumlu API'leri, tipik olarak düşük gecikme süresi burada istenen durumlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2e45-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="b2e45-117">Burada gecikme gelir başlangıç saati hello API toocomplete bir istek için alır ve tüm ağ gecikme hesabı değil.</span><span class="sxs-lookup"><span data-stu-id="b2e45-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="b2e45-118">50-ms gecikme süresi ile bir API sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b2e45-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="b2e45-119">toofully tüketen hello kullanılabilir kapasiteye sahip azaltma düzeyi yüksek ve en fazla eşzamanlı çağrıları = 20, bu API 20 * 1000 toocall ihtiyacınız / saniye başına 50 = 400 zaman.</span><span class="sxs-lookup"><span data-stu-id="b2e45-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="b2e45-120">Bu daha fazla genişletme, en fazla eşzamanlı çağrıları 200, toocall hello API 4000 saniye başına alınabildiği 50-ms gecikme varsayarak, sağlar.</span><span class="sxs-lookup"><span data-stu-id="b2e45-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
