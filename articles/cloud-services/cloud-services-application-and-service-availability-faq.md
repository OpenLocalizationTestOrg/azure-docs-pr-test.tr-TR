---
title: "Uygulama ve hizmet kullanılabilirliği sorunlarını için Microsoft Azure bulut Hizmetleri ile ilgili SSS | Microsoft Docs"
description: "Bu makalede, Microsoft Azure bulut Hizmetleri için uygulama ve hizmet kullanılabilirliği hakkında sık sorulan sorular listelenmektedir."
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
ms.openlocfilehash: a893a6d009dd018ad440964419e0a5a1963084b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="28add-103">Uygulama ve hizmet kullanılabilirliği sorunlarını Azure Cloud Services: sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="28add-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="28add-104">Bu makale, uygulama ve hizmet kullanılabilirliği sorunlarını hakkında sık sorulan sorular içermektedir [Microsoft Azure bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services).</span><span class="sxs-lookup"><span data-stu-id="28add-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="28add-105">Ayrıca başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.</span><span class="sxs-lookup"><span data-stu-id="28add-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="28add-106">My rol geri aldı.</span><span class="sxs-lookup"><span data-stu-id="28add-106">My role got recycled.</span></span> <span data-ttu-id="28add-107">My bulut hizmeti için toplu herhangi bir güncelleştirme oluştu?</span><span class="sxs-lookup"><span data-stu-id="28add-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="28add-108">Kabaca ayda bir kez Microsoft yeni bir konuk işletim sistemi sürümü Windows Azure PaaS VM'ler için serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="28add-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="28add-109"> Konuk işletim sistemi yalnızca bir tür ardışık düzeninde güncelleştirmesidir.</span><span class="sxs-lookup"><span data-stu-id="28add-109"> The Guest OS is only one such update in the pipeline.</span></span> <span data-ttu-id="28add-110">Bir yayın birçok diğer faktörler tarafından etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="28add-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="28add-111">Ayrıca, Azure yüz binlerce makineler üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="28add-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="28add-112">Bu nedenle, tam tarihi ve saati rollerinizi ne zaman yeniden tahmin etmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="28add-112">Therefore, it's impossible to predict the exact date and time when your roles will reboot.</span></span> <span data-ttu-id="28add-113">Konuk işletim sistemi güncelleştirme RSS akışı sahibiz en son bilgilerle güncelleştiriyoruz ancak yaklaşık bir değer süreyi bildirilen göz önünde bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="28add-113">We update the Guest OS Update RSS Feed with the latest information that we have, but you should consider that reported time to be an approximate value.</span></span> <span data-ttu-id="28add-114">Biz bu müşteriler için sorunlu olduğunu farkında olduğundan ve sınırı veya tam olarak zaman yeniden başlatma için bir plan üzerinde çalışma.</span><span class="sxs-lookup"><span data-stu-id="28add-114">We are aware that this is problematic for customers and are working on a plan to limit or precisely time reboots.</span></span>

<span data-ttu-id="28add-115">Yeni konuk işletim sistemi güncelleştirmeleri hakkında tam Ayrıntılar için bkz: [Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="28add-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="28add-116">Yeniden başlatılır ve Konuk ve ana bilgisayar işletim sistemi güncelleştirmelerinin teknik ayrıntılar işaretçiler hakkında yararlı bilgi için MSDN blog gönderisine bakın [rol örneği yeniden son işletim sistemi yükseltmeleri için](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span><span class="sxs-lookup"><span data-stu-id="28add-116">For helpful information on restarts and pointers to technical details of Guest and Host OS updates, see the MSDN blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-the-first-request-to-my-cloud-service-after-the-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="28add-117">Hizmet için biraz zaman boşta kaldıktan sonra bulut Hizmetim ilk isteği neden normalden daha uzun sürer?</span><span class="sxs-lookup"><span data-stu-id="28add-117">Why does the first request to my cloud service after the service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="28add-118">Web sunucusuna yapılan ilk istek aldığında, ilk kod yeniden derler ve isteği işler.</span><span class="sxs-lookup"><span data-stu-id="28add-118">When the Web Server receives the first request, it first recompiles the code and then processes the request.</span></span> <span data-ttu-id="28add-119">İşte bu nedenle ilk istek diğerlerinden daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="28add-119">That's why the first request takes longer than the others.</span></span> <span data-ttu-id="28add-120">Varsayılan olarak, uygulama havuzu kullanıcı etkinlik durumlarda kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="28add-120">By default, the app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="28add-121">Uygulama havuzu da varsayılan olarak 1,740 dakikada (29 saat) geri.</span><span class="sxs-lookup"><span data-stu-id="28add-121">The app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="28add-122">Internet Information Services (IIS) uygulama havuzları uygulamaya açabilir kararsız durumları önlemek için düzenli aralıklarla dönüştürülebilir, askıda, kilitlenmesine veya bellek sızıntıları.</span><span class="sxs-lookup"><span data-stu-id="28add-122">Internet Information Services (IIS) application pools can be periodically recycled to avoid unstable states that can lead to application crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="28add-123">Aşağıdaki belgeler anlamanıza ve bu sorunu azaltılmasına yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="28add-123">The following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="28add-124">IIS için yavaş ilk yük çözme</span><span class="sxs-lookup"><span data-stu-id="28add-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="28add-125">Uygulama havuzu geri dönüşümü çok yavaş sonra IIS 7.5 web uygulaması ilk istek</span><span class="sxs-lookup"><span data-stu-id="28add-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="28add-126">IIS varsayılan davranışını değiştirmek istiyorsanız, Web rolü örneklerine el ile değişiklik uygularsanız, değişiklikleri sonunda kaybolacağı için başlangıç görevleri kullanmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="28add-126">If you want to change the default behavior of IIS, you will need to use startup tasks, because if you manually apply changes to the Web Role instances, the changes will eventually be lost.</span></span>

<span data-ttu-id="28add-127">Daha fazla bilgi için bkz: [nasıl yapılandırılacağı ve bir bulut hizmeti için başlangıç görevleri çalıştırmak](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="28add-127">For more information, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
