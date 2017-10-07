---
title: "Azure işlevleri için aaaBest uygulamaları | Microsoft Docs"
description: "Azure işlevleri için en iyi yöntemler ve yaklaşımlar öğrenin."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, desenleri, en iyi uygulama, işlemler ve olay işleme, Web kancalarını, dinamik işlem, sunucusuz mimarisi"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="6a785-104">Merhaba performansı ve güvenilirliği Azure işlevleri için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="6a785-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="6a785-105">Bu makalede Kılavuzu tooimprove hello performansı ve güvenilirliği işlevi uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a785-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="6a785-106">İşlevler uzun süre çalışan kaçının</span><span class="sxs-lookup"><span data-stu-id="6a785-106">Avoid long running functions</span></span>

<span data-ttu-id="6a785-107">Büyük, uzun süre çalışan işlevler beklenmeyen zaman aşımı sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="6a785-108">Bir işlev toomany Node.js bağımlılıkları büyüyebilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="6a785-109">Bağımlılıklar alma beklenmeyen zaman aşımlarına neden artan yükleme süreleri de neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="6a785-110">Bağımlılıklar her ikisi de açıkça ve örtülü olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="6a785-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="6a785-111">Kodunuz tarafından yüklenen tek bir modül ek modülleri yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="6a785-112">Mümkün olduğunda, daha küçük işlevine düzenleme büyük işlevlerin o iş birlikte ayarlar ve yanıtları hızlı döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a785-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="6a785-113">Örneğin, bir Web kancası veya HTTP tetikleyicisi işlevi belirli bir süre içinde bir bildirim yanıt gerektirebilir; Web kancası toorequire hemen yanıt verilmesi için yaygın bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="6a785-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="6a785-114">Bir kuyruk tetikleyici işlev tarafından işlenen bir sıra toobe içine hello HTTP tetikleyicisi yükü geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a785-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="6a785-115">Bu yaklaşım toodefer hello gerçek iş sağlar ve hemen bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="6a785-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="6a785-116">İşlev iletişimi arası</span><span class="sxs-lookup"><span data-stu-id="6a785-116">Cross function communication</span></span>

<span data-ttu-id="6a785-117">Birden çok işlevleri tümleştirdiğinizde, genellikle bir en iyi yöntem toouse depolama kuyruklarında işlevi iletişim çapraz içindir.</span><span class="sxs-lookup"><span data-stu-id="6a785-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="6a785-118">Merhaba ana nedeni olan depolama kuyrukları ucuz ve çok daha kolay tooprovision.</span><span class="sxs-lookup"><span data-stu-id="6a785-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="6a785-119">Bir depolama kuyruğu tek bir ileti boyutu too64 sınırlı KB.</span><span class="sxs-lookup"><span data-stu-id="6a785-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="6a785-120">İşlevler arasında daha büyük ileti toopass gerekiyorsa, bir Azure hizmet veri yolu kuyruğu kullanılan toosupport ileti boyutları too256 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="6a785-121">Service Bus konu başlıklarını ileti işleme önce filtreleme gerektiriyorsa yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="6a785-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="6a785-122">Olay hub'ları yararlı toosupport yüksek hacimli iletişimleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a785-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="6a785-123">Durum bilgisiz işlevleri toobe yazma</span><span class="sxs-lookup"><span data-stu-id="6a785-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="6a785-124">İşlevler durum bilgisiz ve mümkünse ıdempotent.</span><span class="sxs-lookup"><span data-stu-id="6a785-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="6a785-125">Tüm gerekli durum bilgilerini verilerinizle ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="6a785-125">Associate any required state information with your data.</span></span> <span data-ttu-id="6a785-126">Örneğin, işlenmekte olan büyük olasılıkla sahip olabilir ilişkili bir sipariş `state` üyesi.</span><span class="sxs-lookup"><span data-stu-id="6a785-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="6a785-127">Bir işlev hello işlevi kendisini durum bilgisiz devam ederken bu durumuna bağlı bir sipariş işlem gerçekleştirilemedi.</span><span class="sxs-lookup"><span data-stu-id="6a785-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="6a785-128">Idempotent işlevleri ile Zamanlayıcı Tetikleyicileri özellikle önerilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="6a785-129">Kesinlikle günde bir kez çalıştırmanız gereken bir şey varsa, onu hello gün sırasında her zaman aynı sonuçları hello ile çalıştırabilmeniz için örneğin, okuma ve yazma.</span><span class="sxs-lookup"><span data-stu-id="6a785-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="6a785-130">belirli bir gün için hiçbir iş olduğunda hello işlevi çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a785-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="6a785-131">Ayrıca bir önceki çalıştırma toocomplete başarısız olursa, sonraki çalıştırma hello kaldığı yerden yukarı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a785-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="6a785-132">Savunma işlevler yazma</span><span class="sxs-lookup"><span data-stu-id="6a785-132">Write defensive functions</span></span>

<span data-ttu-id="6a785-133">İşlevinizi dilediğiniz zaman bir özel durum karşılaşabileceği varsayalım.</span><span class="sxs-lookup"><span data-stu-id="6a785-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="6a785-134">İşlevlerinizi hello özelliği toocontinue bir önceki başarısız noktasından ile Merhaba sonraki yürütme sırasında tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="6a785-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="6a785-135">Aşağıdaki eylemler hello gerektiren bir senaryo düşünün:</span><span class="sxs-lookup"><span data-stu-id="6a785-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="6a785-136">Bir db 10.000 satır için sorgu.</span><span class="sxs-lookup"><span data-stu-id="6a785-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="6a785-137">Bu satırlar tooprocess daha fazla hello satır aşağı her bir kuyruk iletisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6a785-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="6a785-138">Nasıl karmaşık sisteminize bağlı olarak, size sahip olabilir: hatalı davranmakta söz konusu aşağı akış hizmetleriyle ağ kesintileri veya kota sınırları ulaşıldığında, vb.. Tüm bunların herhangi bir zamanda işlevinizi etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="6a785-139">Bunun için hazırlanmış, işlevleri toobe toodesign gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a785-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="6a785-140">İşleme kuyruğuna bu öğelerinin 5.000 ekledikten sonra bir hata oluşursa, kodunuzu nasıl tepki vermez?</span><span class="sxs-lookup"><span data-stu-id="6a785-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="6a785-141">Öğeleri, tamamladığınız kümesindeki izler.</span><span class="sxs-lookup"><span data-stu-id="6a785-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="6a785-142">Aksi takdirde, bunları yeniden başlattığınızda ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a785-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="6a785-143">Bu, iş akışınızı üzerinde ciddi bir etkisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="6a785-144">Bir kuyruk öğesi zaten işlenmiş ise işlevi toobe Hayır op izin verir.</span><span class="sxs-lookup"><span data-stu-id="6a785-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="6a785-145">Hello Azure işlevleri platformunda kullandığınız bileşenleri için zaten sağlanan savunma önlemleri yararlanın.</span><span class="sxs-lookup"><span data-stu-id="6a785-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="6a785-146">Örneğin, **zarar iletileri işleme** hello belgelerinde [Azure depolama kuyruğu tetikler](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="6a785-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="6a785-147">Karışımı test ve üretim hello aynı kod olmayan işlev uygulaması</span><span class="sxs-lookup"><span data-stu-id="6a785-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="6a785-148">Bir işlev uygulaması işlevlerinde kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="6a785-148">Functions within a function app share resources.</span></span> <span data-ttu-id="6a785-149">Örneğin, bellek paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="6a785-149">For example, memory is shared.</span></span> <span data-ttu-id="6a785-150">Bir işlev uygulaması üretimde kullanıyorsanız, test ilgili işlevleri ve kaynakları tooit eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="6a785-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="6a785-151">Üretim kodu yürütme sırasında beklenmeyen yükünü neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="6a785-152">Üretim işlevi uygulamalarınızda yük dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="6a785-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="6a785-153">Bellek hello uygulamasında her işlev üzerinden ortalaması alınır.</span><span class="sxs-lookup"><span data-stu-id="6a785-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="6a785-154">Birden çok .net işlevlerde başvurulan paylaşılan bir derleme varsa, ortak bir paylaşılan klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="6a785-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="6a785-155">Örneğin aşağıdaki deyim benzer toohello hello derleme başvurusu:</span><span class="sxs-lookup"><span data-stu-id="6a785-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="6a785-156">Aksi takdirde, kolay tooaccidentally birden çok test sürümleri arasında farklı şekilde davranan aynı ikili işlevleri hello dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6a785-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="6a785-157">Ayrıntılı günlük üretim kodunda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="6a785-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="6a785-158">Olumsuz bir etkisi vardır.</span><span class="sxs-lookup"><span data-stu-id="6a785-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="6a785-159">Zaman uyumsuz kod kullanır ancak çağrıları engelleme kaçının</span><span class="sxs-lookup"><span data-stu-id="6a785-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="6a785-160">Zaman uyumsuz programlama önerilen en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="6a785-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="6a785-161">Bununla birlikte, her zaman hello başvuran kaçının `Result` özelliği veya arama `Wait` yöntemi bir `Task` örneği.</span><span class="sxs-lookup"><span data-stu-id="6a785-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="6a785-162">Bu yaklaşım toothread Tükenme yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="6a785-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="6a785-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a785-163">Next steps</span></span>
<span data-ttu-id="6a785-164">Daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="6a785-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="6a785-165">Azure işlevleri Azure App Service kullandığından, ayrıca uygulama hizmeti yönergelerini farkında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6a785-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="6a785-166">Patterns and Practices HTTP performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="6a785-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

