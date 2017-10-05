---
title: "Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme"
description: "Uygulamayı App Service'te ölçeklendirme, ayrıntıları hakkında bilgi edinin."
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
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="d3093-104">Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="d3093-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="d3093-105">Azure App Service içinde barındırılan uygulamalar için [yoğun ölçeği elde etmek](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="d3093-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="d3093-106">Ancak, bir uygulamayı ölçeklendirme "bir boyutu tüm uygun" Çözüm sahip olmayan bir karmaşık sorunudur.</span><span class="sxs-lookup"><span data-stu-id="d3093-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="d3093-107">Doğru Ölçekle uygulamanız var. uygulamaları başarınız katkıda bulunan 3 önemli alanlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d3093-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="d3093-108">Uygulama mimarisi ve onun zayıf anlama.</span><span class="sxs-lookup"><span data-stu-id="d3093-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="d3093-109">Uygulama durum bilgisi mi?</span><span class="sxs-lookup"><span data-stu-id="d3093-109">Is your Application Stateful?</span></span> <span data-ttu-id="d3093-110">Durum bilgisiz?</span><span class="sxs-lookup"><span data-stu-id="d3093-110">Stateless?</span></span>
   * <span data-ttu-id="d3093-111">Uygulamanızın tüm bileşenleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="d3093-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="d3093-112">Uygulamada performans sorunlarını nerede?</span><span class="sxs-lookup"><span data-stu-id="d3093-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="d3093-113">Yük uygulamanıza uygulandığında ne ilk çalışmamasına neden olur?</span><span class="sxs-lookup"><span data-stu-id="d3093-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="d3093-114">Beklenen yükü ve performans gereksinimlerini anlama.</span><span class="sxs-lookup"><span data-stu-id="d3093-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="d3093-115">Uygulama bin kullanıcılar hizmet gerekiyor mu? veya bir milyon?</span><span class="sxs-lookup"><span data-stu-id="d3093-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="d3093-116">Trafik tek bir coğrafi konumdan veya genel olarak gelir?</span><span class="sxs-lookup"><span data-stu-id="d3093-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="d3093-117">Mevsimlik Çeşitlemeler var mı? trafik yükselmeleri?</span><span class="sxs-lookup"><span data-stu-id="d3093-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="d3093-118">Uygulamanın ne kadar hızlı yanıt?</span><span class="sxs-lookup"><span data-stu-id="d3093-118">How fast should the app respond?</span></span> <span data-ttu-id="d3093-119">1 saniye?</span><span class="sxs-lookup"><span data-stu-id="d3093-119">1 second?</span></span> <span data-ttu-id="d3093-120">1 milisaniyelik?</span><span class="sxs-lookup"><span data-stu-id="d3093-120">1 millisecond?</span></span>
3. <span data-ttu-id="d3093-121">Anlama ve doğru şekilde uygulamanızı barındırma platformu yararlanın.</span><span class="sxs-lookup"><span data-stu-id="d3093-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="d3093-122">My ölçek hedeflerinize ulaşmak için hangi özelliklerin yararlanıyor?</span><span class="sxs-lookup"><span data-stu-id="d3093-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="d3093-123">Bu bölümde, tüm Etkenler ve ölçeklenebilirlik hedeflerinize ulaşmak için gerekli uygulama hizmeti özelliklerinden yararlanır bir strateji insanlara yardım anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d3093-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

