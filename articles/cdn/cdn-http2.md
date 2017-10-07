---
title: "Azure CDN aaaHTTP/2 desteği | Microsoft Docs"
description: "HTTP/2 ve CDN desteği hakkında bilgi edinin."
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="52e0e-103">Azure CDN HTTP/2 desteği</span><span class="sxs-lookup"><span data-stu-id="52e0e-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="52e0e-104">HTTP/2 büyük düzeltme tooHTTP/1.1\ olur.</span><span class="sxs-lookup"><span data-stu-id="52e0e-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="52e0e-105">Daha hızlı web performans, daha az yanıt süresi ve gelişmiş bir kullanıcı, hello bilinen HTTP yöntemleri, durum kodları ve semantiği korurken deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="52e0e-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="52e0e-106">HTTP/2 ile HTTP ve HTTPS tasarlanmış toowork olsa da, birçok istemci web tarayıcısı TLS yalnızca HTTP/2 destekler.</span><span class="sxs-lookup"><span data-stu-id="52e0e-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="52e0e-107">HTTP/2 avantajları</span><span class="sxs-lookup"><span data-stu-id="52e0e-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="52e0e-108">HTTP/2 Hello avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="52e0e-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="52e0e-109">**Çoğullama ve eşzamanlılık**</span><span class="sxs-lookup"><span data-stu-id="52e0e-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="52e0e-110">HTTP 1.1 kullanarak, birden çok birden çok kaynak istekleri birden fazla TCP bağlantısı gerektirir ve her bağlantı ile ilişkili performans yüke sahiptir.</span><span class="sxs-lookup"><span data-stu-id="52e0e-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="52e0e-111">HTTP/2 tek bir TCP bağlantı üzerinde istenen birden çok kaynak toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="52e0e-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="52e0e-112">**Üstbilgi sıkıştırma**</span><span class="sxs-lookup"><span data-stu-id="52e0e-112">**Header compression**</span></span>

    <span data-ttu-id="52e0e-113">Sunulacak kaynakları Hello HTTP üstbilgilerini sıkıştırarak hello kablo zamanında önemli ölçüde azalır.</span><span class="sxs-lookup"><span data-stu-id="52e0e-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="52e0e-114">**Akış bağımlılıkları**</span><span class="sxs-lookup"><span data-stu-id="52e0e-114">**Stream dependencies**</span></span>

    <span data-ttu-id="52e0e-115">Akış bağımlılıkları olan kaynakların öncelik tooindicate toohello sunucu hello istemci izin verin.</span><span class="sxs-lookup"><span data-stu-id="52e0e-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="52e0e-116">HTTP/2 tarayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="52e0e-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="52e0e-117">Tüm önde gelen tarayıcılar hello HTTP/2 desteği geçerli sürümlerine uyguladık.</span><span class="sxs-lookup"><span data-stu-id="52e0e-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="52e0e-118">Desteklenmeyen tarayıcılar otomatik olarak geri dönüş tooHTTP/1.1 olur.</span><span class="sxs-lookup"><span data-stu-id="52e0e-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="52e0e-119">Tarayıcı</span><span class="sxs-lookup"><span data-stu-id="52e0e-119">Browser</span></span>|<span data-ttu-id="52e0e-120">En düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="52e0e-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="52e0e-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="52e0e-121">Microsoft Edge</span></span>| <span data-ttu-id="52e0e-122">12</span><span class="sxs-lookup"><span data-stu-id="52e0e-122">12</span></span>|
|<span data-ttu-id="52e0e-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="52e0e-123">Google Chrome</span></span>| <span data-ttu-id="52e0e-124">43</span><span class="sxs-lookup"><span data-stu-id="52e0e-124">43</span></span>|
|<span data-ttu-id="52e0e-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="52e0e-125">Mozilla Firefox</span></span>| <span data-ttu-id="52e0e-126">38</span><span class="sxs-lookup"><span data-stu-id="52e0e-126">38</span></span>|
|<span data-ttu-id="52e0e-127">Opera</span><span class="sxs-lookup"><span data-stu-id="52e0e-127">Opera</span></span>| <span data-ttu-id="52e0e-128">32</span><span class="sxs-lookup"><span data-stu-id="52e0e-128">32</span></span>|
|<span data-ttu-id="52e0e-129">Safari</span><span class="sxs-lookup"><span data-stu-id="52e0e-129">Safari</span></span>| <span data-ttu-id="52e0e-130">9</span><span class="sxs-lookup"><span data-stu-id="52e0e-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="52e0e-131">Azure CDN HTTP/2 desteğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="52e0e-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="52e0e-132">HTTP/2 desteği şu anda etkin mi **akamai'den Azure CDN** ve **verizon'dan Azure CDN** profilleri.</span><span class="sxs-lookup"><span data-stu-id="52e0e-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="52e0e-133">Başka bir eylem müşterilerden gereklidir.</span><span class="sxs-lookup"><span data-stu-id="52e0e-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="52e0e-134">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="52e0e-134">Next Steps</span></span>

<span data-ttu-id="52e0e-135">toosee hello HTTP/2 eylem avantajlar [akamai'den bu demo](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="52e0e-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="52e0e-136">HTTP/2 hakkında daha fazla toolearn kaynakları aşağıdaki hello ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="52e0e-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="52e0e-137">HTTP/2 belirtimi giriş sayfası</span><span class="sxs-lookup"><span data-stu-id="52e0e-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="52e0e-138">Resmi HTTP/2 ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="52e0e-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="52e0e-139">Akamai HTTP/2 bilgileri</span><span class="sxs-lookup"><span data-stu-id="52e0e-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="52e0e-140">Azure CDN'ın kullanılabilir özellikler hakkında daha fazla toolearn bkz hello [Azure CDN'ye genel bakış](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="52e0e-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
