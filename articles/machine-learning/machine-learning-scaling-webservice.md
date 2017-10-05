---
title: "Bir Azure Machine Learning web hizmetini eşzamanlılığı artırmak nasıl | Microsoft Docs"
description: "Ek uç noktaları ekleyerek bir Azure Machine Learning web hizmetini eşzamanlılığı artırmak öğrenin."
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
ms.openlocfilehash: 013354515d841003c912ac0338690dd975a79ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="a1cdc-104">Ek uç noktaları ekleyerek bir Azure Machine Learning web hizmetini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="a1cdc-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="a1cdc-105">Bu konu, uygulanabilir teknikleri açıklar bir **Klasik** Machine Learning Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-105">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="a1cdc-106">Varsayılan olarak, yayımlanan her Web hizmeti 20 eş zamanlı istekleri desteklemek üzere yapılandırılmış ve 200 eş zamanlı istekleri olarak yüksek olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-106">By default, each published Web service is configured to support 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="a1cdc-107">Klasik Azure portalı bu değeri ayarlamak için bir yol sağlar, ancak Azure Machine Learning web hizmeti için en iyi performansı sağlamak için bu ayarı otomatik olarak iyileştirir ve portal değeri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-107">While the Azure classic portal provides a way to set this value, Azure Machine Learning automatically optimizes the setting to provide the best performance for your web service and the portal value is ignored.</span></span> 

<span data-ttu-id="a1cdc-108">API 200 en fazla eşzamanlı çağrıları değerden daha yüksek bir yük ile çağırmak için plan destekleyecekse aynı Web hizmetinde birden fazla uç noktası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-108">If you plan to call the API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on the same Web service.</span></span> <span data-ttu-id="a1cdc-109">Ardından rastgele yük bunların tümünün arasında dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="a1cdc-110">Bir Web hizmeti ölçeklendirme ortak bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-110">The scaling of a Web service is a common task.</span></span> <span data-ttu-id="a1cdc-111">200'den fazla eşzamanlı isteği destekler, birden fazla uç noktası aracılığıyla kullanılabilirliğini artırmak veya web hizmeti için ayrı uç noktaları sağlamak için ölçeklendirmek için bazı nedenler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-111">Some reasons to scale are to support more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for the web service.</span></span> <span data-ttu-id="a1cdc-112">Ek uç noktalar aynı Web hizmeti ekleyerek ölçeği artırabilir [Klasik Azure portalı](https://manage.windowsazure.com/) veya [Azure Machine Learning Web hizmeti](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-112">You can increase the scale by adding additional endpoints for the same Web service through [Azure classic portal](https://manage.windowsazure.com/) or the [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="a1cdc-113">Yeni uç nokta ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="a1cdc-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="a1cdc-114">Bir yüksek eşzamanlılık sayısı kullanarak API gelenlere yüksek oranda ile arıyoruz değil, detrimental göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling the API with a correspondingly high rate.</span></span> <span data-ttu-id="a1cdc-115">Yüksek yük için yapılandırılmış bir API nispeten düşük yük yerleştirirseniz gecikme ara sıra zaman aşımları ve/veya ani görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-115">You might see sporadic timeouts and/or spikes in the latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="a1cdc-116">Zaman uyumlu API'leri genellikle düşük gecikme süresi burada istenen durumlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-116">The synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="a1cdc-117">Burada gecikme API bir isteği tamamlamak alır ve tüm ağ gecikme hesabı olmayan zaman anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-117">Latency here implies the time it takes for the API to complete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="a1cdc-118">50-ms gecikme süresi ile bir API sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="a1cdc-119">Kullanılabilir kapasiteye sahip azaltma düzeyi yüksek ve en fazla eşzamanlı çağrıları tam olarak kullanmak üzere = 20, bu API 20 * 1000 çağırmanız gerekir / saniye başına 50 = 400 zaman.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-119">To fully consume the available capacity with throttle level High and Max Concurrent Calls = 20, you need to call this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="a1cdc-120">Bu daha fazla genişletme, en fazla eşzamanlı çağrıları 200, 50-ms gecikme varsayılarak saniyede API 4000 kez çağrılması olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1cdc-120">Extending this further, a Max Concurrent Calls of 200 allows you to call the API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
