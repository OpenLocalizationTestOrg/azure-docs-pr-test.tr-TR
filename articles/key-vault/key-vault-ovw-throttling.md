---
ms.assetid: 
title: "aaaAzure anahtar kasası azaltma Kılavuzu | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="9502b-102">Azure anahtar Kasası'nı Kılavuzu azaltma</span><span class="sxs-lookup"><span data-stu-id="9502b-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="9502b-103">Azaltma eşzamanlı çağrıları toohello Azure hizmeti tooprevent aşırı kaynakların kullanımı hello sayısını sınırlayan başlatma bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="9502b-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="9502b-104">Azure anahtar kasası (AKV) tasarlanmış toohandle istekleri hacmi yüksek olur.</span><span class="sxs-lookup"><span data-stu-id="9502b-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="9502b-105">Bunaltıcı bir istek sayısı ortaya çıkarsa, istemcinin istek azaltma en iyi performansı ve güvenilirliği hello AKV hizmeti için korumaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9502b-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="9502b-106">Azaltma sınırları hello senaryo göre değişir.</span><span class="sxs-lookup"><span data-stu-id="9502b-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="9502b-107">Örneğin, büyük hacimli yazma gerçekleştiriyorsanız hello olasılığı azaltma için yalnızca okuma gerçekleştirdiğiniz varsa daha yüksek olur.</span><span class="sxs-lookup"><span data-stu-id="9502b-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="9502b-108">Anahtar kasası sınırlarına nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="9502b-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="9502b-109">Anahtar kasası hizmet sınırları tooprevent kötüye kaynakların vardır ve tüm anahtar Kasası'nın istemcileri için hizmet kalitesi emin olun.</span><span class="sxs-lookup"><span data-stu-id="9502b-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="9502b-110">Bir hizmeti eşiği aşıldığında, anahtar kasası herhangi başka bir istek Bu istemciden gelen bir süre için sınırlar.</span><span class="sxs-lookup"><span data-stu-id="9502b-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="9502b-111">Bu gerçekleştiğinde, anahtar kasası HTTP durum kodu 429 döndürür (çok sayıda istek), ve hello istekleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="9502b-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="9502b-112">Ayrıca, anahtar kasası tarafından izlenen hello azaltma sınırları doğrultusunda 429 bir sayı döndürür isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="9502b-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="9502b-113">Daha yüksek azaltma sınırları için geçerli iş durum varsa, lütfen bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="9502b-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="9502b-114">Nasıl yanıt tooservice uygulamanızda toothrottle sınırlar</span><span class="sxs-lookup"><span data-stu-id="9502b-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="9502b-115">Merhaba şunlardır **en iyi uygulamalar** uygulamanızı azaltma için:</span><span class="sxs-lookup"><span data-stu-id="9502b-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="9502b-116">İstek başına işlemleri Hello sayısını azaltın.</span><span class="sxs-lookup"><span data-stu-id="9502b-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="9502b-117">İstekleri Hello sıklığını azaltın.</span><span class="sxs-lookup"><span data-stu-id="9502b-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="9502b-118">Hemen yeniden deneme kaçının.</span><span class="sxs-lookup"><span data-stu-id="9502b-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="9502b-119">Tüm istekler, kullanım sınırları karşı tahakkuk eder.</span><span class="sxs-lookup"><span data-stu-id="9502b-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="9502b-120">Uygulamanızın hata işleme uyguladığınızda, kullanım hello HTTP hata kodunu 429 toodetect hello gerekir istemci-tarafı azaltma.</span><span class="sxs-lookup"><span data-stu-id="9502b-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="9502b-121">Merhaba isteği yeniden HTTP 429 hata koduyla başarısız olursa, bir Azure hizmeti sınırını hala karşılaşıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9502b-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="9502b-122">İstemci-tarafı azaltma yöntemi, başarılı olana dek hello isteği yeniden deneniyor toouse hello önerilen devam edin.</span><span class="sxs-lookup"><span data-stu-id="9502b-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="9502b-123">Önerilen istemci-tarafı azaltma yöntemi</span><span class="sxs-lookup"><span data-stu-id="9502b-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="9502b-124">HTTP hata kodunu 429, üstel geri alma yaklaşımı kullanarak, istemci azaltma başlayın:</span><span class="sxs-lookup"><span data-stu-id="9502b-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="9502b-125">Yeniden deneme isteği 1 saniye bekleyin</span><span class="sxs-lookup"><span data-stu-id="9502b-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="9502b-126">Hala 2 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="9502b-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="9502b-127">Hala 4 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="9502b-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="9502b-128">Hala 8 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="9502b-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="9502b-129">Hala 16 saniye bekleyin kısıtlanan, isteği yeniden deneyin</span><span class="sxs-lookup"><span data-stu-id="9502b-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="9502b-130">Bu noktada, HTTP 429 yanıt kodları alamıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="9502b-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="9502b-131">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="9502b-131">See also</span></span>

<span data-ttu-id="9502b-132">Microsoft Cloud hello üzerinde azaltma daha derin yönlendirmesi için bkz: [azaltma düzeni](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="9502b-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

