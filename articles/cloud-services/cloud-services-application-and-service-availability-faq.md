---
title: "Microsoft Azure bulut Hizmetleri ile ilgili SSS aaaApplication ve hizmet kullanılabilirliği sorunlarını | Microsoft Docs"
description: "Bu makalede sık sorulan Microsoft Azure bulut Hizmetleri için uygulama ve hizmet kullanılabilirliği hakkında sorular hello listelenmektedir."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="35042-103">Uygulama ve hizmet kullanılabilirliği sorunlarını Azure Cloud Services: sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="35042-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="35042-104">Bu makale, uygulama ve hizmet kullanılabilirliği sorunlarını hakkında sık sorulan sorular içermektedir [Microsoft Azure bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services).</span><span class="sxs-lookup"><span data-stu-id="35042-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="35042-105">Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.</span><span class="sxs-lookup"><span data-stu-id="35042-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="35042-106">My rol geri aldı.</span><span class="sxs-lookup"><span data-stu-id="35042-106">My role got recycled.</span></span> <span data-ttu-id="35042-107">My bulut hizmeti için toplu herhangi bir güncelleştirme oluştu?</span><span class="sxs-lookup"><span data-stu-id="35042-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="35042-108">Kabaca ayda bir kez Microsoft yeni bir konuk işletim sistemi sürümü Windows Azure PaaS VM'ler için serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="35042-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="35042-109"> Konuk işletim sistemi yalnızca bir tür hello ardışık düzeninde güncelleştirmesidir.</span><span class="sxs-lookup"><span data-stu-id="35042-109"> The Guest OS is only one such update in hello pipeline.</span></span> <span data-ttu-id="35042-110">Bir yayın birçok diğer faktörler tarafından etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="35042-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="35042-111">Ayrıca, Azure yüz binlerce makineler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="35042-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="35042-112">Bu nedenle imkansız toopredict hello tam tarihi ve saati rollerinizi ne zaman yeniden olur.</span><span class="sxs-lookup"><span data-stu-id="35042-112">Therefore, it's impossible toopredict hello exact date and time when your roles will reboot.</span></span> <span data-ttu-id="35042-113">Biz sahip hello en son bilgilerle hello konuk işletim sistemi güncelleştirme RSS akışı güncelleştiriyoruz ancak zaman toobe yaklaşık bir değer bildirilen göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35042-113">We update hello Guest OS Update RSS Feed with hello latest information that we have, but you should consider that reported time toobe an approximate value.</span></span> <span data-ttu-id="35042-114">Biz bu müşteriler için sorunlu olduğunu farkında olduğundan ve bir plan toolimit veya tam olarak zaman yeniden başlatmalar çalışma.</span><span class="sxs-lookup"><span data-stu-id="35042-114">We are aware that this is problematic for customers and are working on a plan toolimit or precisely time reboots.</span></span>

<span data-ttu-id="35042-115">Yeni konuk işletim sistemi güncelleştirmeleri hakkında tam Ayrıntılar için bkz: [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="35042-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="35042-116">Merhaba MSDN blog gönderisi Konuk ve ana bilgisayar işletim sistemi güncelleştirmelerinin yeniden başlatılır ve işaretçileri tootechnical ayrıntıları yararlı bilgi için bkz [rol örneği yeniden son tooOS yükseltmeler](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span><span class="sxs-lookup"><span data-stu-id="35042-116">For helpful information on restarts and pointers tootechnical details of Guest and Host OS updates, see hello MSDN blog post [Role Instance Restarts Due tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="35042-117">Merhaba hizmet biraz zaman boşta kaldıktan sonra hello ilk istek toomy bulut hizmeti neden normalden daha uzun sürer?</span><span class="sxs-lookup"><span data-stu-id="35042-117">Why does hello first request toomy cloud service after hello service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="35042-118">Merhaba Web sunucusu hello ilk isteği aldığında, önce hello kodu yeniden derler ve hello isteğini işler.</span><span class="sxs-lookup"><span data-stu-id="35042-118">When hello Web Server receives hello first request, it first recompiles hello code and then processes hello request.</span></span> <span data-ttu-id="35042-119">Bu neden hello uzun ilk isteği alır başkalarının hello olduğu.</span><span class="sxs-lookup"><span data-stu-id="35042-119">That's why hello first request takes longer than hello others.</span></span> <span data-ttu-id="35042-120">Varsayılan olarak, hello uygulama havuzu kullanıcı etkinlik durumlarda kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="35042-120">By default, hello app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="35042-121">Merhaba uygulama havuzu da varsayılan olarak 1,740 dakikada (29 saat) geri.</span><span class="sxs-lookup"><span data-stu-id="35042-121">hello app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="35042-122">Internet Information Services (IIS) uygulama havuzları tooapplication çökme (Crash), askıda veya bellek sızıntıları açabilir düzenli aralıklarla geri dönüştürüldüğünde tooavoid kararsız durumlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="35042-122">Internet Information Services (IIS) application pools can be periodically recycled tooavoid unstable states that can lead tooapplication crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="35042-123">Aşağıdaki belgeler hello anlamanıza ve bu sorunu azaltmak yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="35042-123">hello following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="35042-124">IIS için yavaş ilk yük çözme</span><span class="sxs-lookup"><span data-stu-id="35042-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="35042-125">Uygulama havuzu geri dönüşümü çok yavaş sonra IIS 7.5 web uygulaması ilk istek</span><span class="sxs-lookup"><span data-stu-id="35042-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="35042-126">IIS toochange hello varsayılan davranışını isterseniz, değişiklikleri toohello Web rolü örneklerini elle uygularsanız, hello değişiklikleri sonunda kaybolacağı için toouse başlangıç görevleri, gerekir.</span><span class="sxs-lookup"><span data-stu-id="35042-126">If you want toochange hello default behavior of IIS, you will need toouse startup tasks, because if you manually apply changes toohello Web Role instances, hello changes will eventually be lost.</span></span>

<span data-ttu-id="35042-127">Daha fazla bilgi için bkz: [nasıl tooconfigure ve çalıştırma başlangıç için bir bulut hizmeti görevleri](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="35042-127">For more information, see [How tooconfigure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
