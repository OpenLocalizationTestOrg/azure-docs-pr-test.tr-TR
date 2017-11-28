---
title: "Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme"
description: "Merhaba, uygulamayı App Service'te ölçeklendirme ayrıntıları hakkında bilgi edinin."
keywords: "app service, azure app service, ölçek, ölçeklenebilir, app service planı, app service maliyeti"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="5b8c9-104">Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="5b8c9-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="5b8c9-105">Azure App Service içinde barındırılan uygulamalar için [yoğun ölçeği elde etmek](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="5b8c9-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="5b8c9-106">Ancak, bir uygulamayı ölçeklendirme "bir boyutu tüm uygun" Çözüm sahip olmayan bir karmaşık sorunudur.</span><span class="sxs-lookup"><span data-stu-id="5b8c9-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="5b8c9-107">toocorrectly uygulamanız ölçeği tooyour uygulamaları başarı katkıda bulunan 3 önemli konu vardır:</span><span class="sxs-lookup"><span data-stu-id="5b8c9-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="5b8c9-108">Uygulama mimarisi ve onun zayıf anlama.</span><span class="sxs-lookup"><span data-stu-id="5b8c9-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="5b8c9-109">Uygulama durum bilgisi mi?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-109">Is your Application Stateful?</span></span> <span data-ttu-id="5b8c9-110">Durum bilgisiz?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-110">Stateless?</span></span>
   * <span data-ttu-id="5b8c9-111">Merhaba, uygulama bileşenlerinin tümünü nelerdir?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="5b8c9-112">Merhaba uygulaması hello darboğazları nerede?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="5b8c9-113">Yük uygulanan tooyour uygulama olduğunda hangi ilk çalışmamasına neden olur?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="5b8c9-114">Yük ve performans gereksinimlerini anlama hello bekleniyordu.</span><span class="sxs-lookup"><span data-stu-id="5b8c9-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="5b8c9-115">Merhaba uygulaması tooserve bin kullanıcılar gerekiyor mu? veya bir milyon?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="5b8c9-116">Trafik tek bir coğrafi konumdan veya genel olarak gelir?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="5b8c9-117">Mevsimlik Çeşitlemeler var mı? trafik yükselmeleri?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="5b8c9-118">Merhaba uygulama ne kadar hızlı yanıt?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-118">How fast should hello app respond?</span></span> <span data-ttu-id="5b8c9-119">1 saniye?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-119">1 second?</span></span> <span data-ttu-id="5b8c9-120">1 milisaniyelik?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-120">1 millisecond?</span></span>
3. <span data-ttu-id="5b8c9-121">Anlama ve doğru şekilde uygulamanızı barındırma Dengeleme hello platformu.</span><span class="sxs-lookup"><span data-stu-id="5b8c9-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="5b8c9-122">Hangi özelliklerin gerektiğini ı tooachieve my ölçek hedefleri yararlanır?</span><span class="sxs-lookup"><span data-stu-id="5b8c9-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="5b8c9-123">Bu bölümde, tüm hello Etkenler ve ölçeklenebilirlik hedeflerinizi hello gerekli uygulama hizmeti özellikleri tooachieve yararlanan bir strateji insanlara yardım anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5b8c9-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

