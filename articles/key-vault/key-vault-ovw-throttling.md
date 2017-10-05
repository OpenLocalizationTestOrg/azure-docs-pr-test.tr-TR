---
ms.assetid: 
title: "Azure anahtar Kasası'nı Kılavuzu azaltma | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="bd8d0-102">Azure anahtar Kasası'nı Kılavuzu azaltma</span><span class="sxs-lookup"><span data-stu-id="bd8d0-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="bd8d0-103">Azaltma kaynakların aşırı kullanımı önlemek için Azure hizmeti eşzamanlı çağrı sayısı sınırlayan başlatma bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="bd8d0-104">Azure anahtar kasası (AKV), yüksek hacimli isteklerini işlemek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="bd8d0-105">Bunaltıcı bir istek sayısı ortaya çıkarsa, istemcinin istek azaltma en iyi performans ve güvenilirlik AKV hizmetinin korumaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="bd8d0-106">Azaltma sınırları senaryo göre değişir.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="bd8d0-107">Örneğin, büyük hacimli yazma gerçekleştiriyorsanız azaltma olanağı yalnızca okuma gerçekleştirdiğiniz varsa daha yüksek olur.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="bd8d0-108">Anahtar kasası sınırlarına nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="bd8d0-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="bd8d0-109">Kaynakların kötüye kullanımı önlemek ve tüm anahtar Kasası'nın istemcileri için hizmet kalitesi sağlamak için anahtar kasası hizmet sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="bd8d0-110">Bir hizmeti eşiği aşıldığında, anahtar kasası herhangi başka bir istek Bu istemciden gelen bir süre için sınırlar.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="bd8d0-111">Bu gerçekleştiğinde, anahtar kasası HTTP durum kodu 429 döndürür (çok sayıda istek), ve istekleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="bd8d0-112">Ayrıca, anahtar kasası tarafından izlenen azaltma sınırları doğrultusunda 429 bir sayı döndürür isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="bd8d0-113">Daha yüksek azaltma sınırları için geçerli iş durum varsa, lütfen bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="bd8d0-114">Hizmet sınırları yanıta uygulamanızda kısıtlama nasıl</span><span class="sxs-lookup"><span data-stu-id="bd8d0-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="bd8d0-115">Aşağıdakiler **en iyi uygulamalar** uygulamanızı azaltma için:</span><span class="sxs-lookup"><span data-stu-id="bd8d0-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="bd8d0-116">İstek başına işlem sayısını azaltın.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="bd8d0-117">İstekleri sıklığını azaltın.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="bd8d0-118">Hemen yeniden deneme kaçının.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="bd8d0-119">Tüm istekler, kullanım sınırları karşı tahakkuk eder.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="bd8d0-120">Uygulamanızın hata işleme uyguladığınızda, istemci-tarafı azaltma ihtiyacına algılamak için HTTP hata kodunu 429 kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="bd8d0-121">İsteği yeniden HTTP 429 hata koduyla başarısız olursa, bir Azure hizmeti sınırını hala karşılaşıyoruz.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="bd8d0-122">Önerilen yöntem azaltma, onu başarılı olana kadar istek yeniden deneniyor istemci kullanmaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="bd8d0-123">Önerilen istemci-tarafı azaltma yöntemi</span><span class="sxs-lookup"><span data-stu-id="bd8d0-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="bd8d0-124">HTTP hata kodunu 429, üstel geri alma yaklaşımı kullanarak, istemci azaltma başlayın:</span><span class="sxs-lookup"><span data-stu-id="bd8d0-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="bd8d0-125">Yeniden deneme isteği 1 saniye bekleyin</span><span class="sxs-lookup"><span data-stu-id="bd8d0-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="bd8d0-126">Hala 2 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="bd8d0-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="bd8d0-127">Hala 4 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="bd8d0-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="bd8d0-128">Hala 8 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="bd8d0-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="bd8d0-129">Hala 16 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="bd8d0-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="bd8d0-130">Bu noktada, HTTP 429 yanıt kodları alamıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="bd8d0-131">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bd8d0-131">See also</span></span>

<span data-ttu-id="bd8d0-132">Microsoft Cloud azaltma daha derin yönlendirmesi için bkz: [azaltma düzeni](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="bd8d0-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

