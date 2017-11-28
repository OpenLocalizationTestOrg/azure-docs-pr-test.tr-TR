---
title: "Sorun giderme kılavuzu - Analytics'i azure Mobile Engagement"
description: "Azure Mobile Engagement Analytics, izleme, Segment ve Pano sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="cadc1-103">Analiz, izleme, Segment ve Pano sorunları için sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="cadc1-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="cadc1-104">Olası sorunlar aşağıda verilmiştir Azure Mobile Engagement'ın uygulamaları, cihazlar ve kullanıcılar hakkında bilgileri nasıl toplar karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cadc1-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="cadc1-105">Eksik Gecikmeli bilgi</span><span class="sxs-lookup"><span data-stu-id="cadc1-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="cadc1-106">Sorun</span><span class="sxs-lookup"><span data-stu-id="cadc1-106">Issue</span></span>
* <span data-ttu-id="cadc1-107">Bilgi Analytics, Segment veya Pano görünmesini içinde ertelendi.</span><span class="sxs-lookup"><span data-stu-id="cadc1-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="cadc1-108">İzleme bilgileri eksik.</span><span class="sxs-lookup"><span data-stu-id="cadc1-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="cadc1-109">Analytics, Segment veya pano bilgileri eksik.</span><span class="sxs-lookup"><span data-stu-id="cadc1-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="cadc1-110">Segment basarsa sınırlar.</span><span class="sxs-lookup"><span data-stu-id="cadc1-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="cadc1-111">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="cadc1-111">Causes</span></span>
* <span data-ttu-id="cadc1-112">Analytics bir API İzleyici API'si kullanabilir ve kesimleri herhangi bir veri, kullanıcı Arabiriminden eksik olup olmadığını görmek için API API'leri aracılığıyla görülebilir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="cadc1-113">Ardından Azure Mobile Engagement SDK'sını uygulamanıza doğru tümleşik değilse Analytics, Segment, izleme veya panolar bilgileri görmeye olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="cadc1-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="cadc1-114">Parçaları olamaz oluşturulduktan sonra kesimleri yalnızca "kopya" (kopyalanır) veya "(silinir) yok" değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="cadc1-115">Segmentler yalnızca 10 ölçüt içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="cadc1-116">İzleme eksik bilgilerinin test etmek için en iyi yolu bir test cihazı Kurulum, kaldırma ve/veya uygulama test aygıtta yeniden yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="cadc1-117">Bilgileri Analytics, Segment veya panolar için 24 saatte bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="cadc1-118">Segment önceki bilgilere dayalı olsa bile oluşturulduktan sonra 24 saate kadar yeni kesimleri bilgilerinde görüntülenmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="cadc1-119">Kullanıcı arabiriminde analiz verilerinizi filtrelemeyi uygulamanızı sürümünden bağımsız olarak bu türdeki tüm örnekler (örneğin gösterir "Adına göre filtre kilitleniyor" sürüm 1 ve sürüm 2, uygulamanızın gösterir).</span><span class="sxs-lookup"><span data-stu-id="cadc1-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="cadc1-120">Yanlış ayarlanmış tarih, telefon sahip bir kullanıcı yanlış bir zaman diliminde gösterebilirsiniz şekilde süre analiz için kullanıcıların cihaz ayarlarını tarihinden temel alır.</span><span class="sxs-lookup"><span data-stu-id="cadc1-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="cadc1-121">"Test etmek için" düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı iter, veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="cadc1-122">Öğeleri kullanıcı Arabiriminde bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="cadc1-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="cadc1-123">Sorun</span><span class="sxs-lookup"><span data-stu-id="cadc1-123">Issue</span></span>
* <span data-ttu-id="cadc1-124">Bazı yerleşik göre kesimleri oluşturulamıyor veya özel uygulama bilgisi ölçütleri etiketi.</span><span class="sxs-lookup"><span data-stu-id="cadc1-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="cadc1-125">Bazı yerleşik bulunamıyor veya özel uygulama bilgisi ölçütleri Analytics, izleme veya panolar etiketi.</span><span class="sxs-lookup"><span data-stu-id="cadc1-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="cadc1-126">Veri analizi, izleme, Segment veya panolar yorumlayamayacağı.</span><span class="sxs-lookup"><span data-stu-id="cadc1-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="cadc1-127">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="cadc1-127">Causes</span></span>
* <span data-ttu-id="cadc1-128">Bazı öğeler oluşturulur ve uygulama bilgisi etiketleri yalnızca itme ölçüt olarak kullanılabilir, ancak Analytics, izleme veya Pano kesimi eklenebilir ya da görünür olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="cadc1-129">Yerleşik öğeleri ve bir kesimine eklenemez uygulama bilgisi etiketler, bir kesiminde dayalı hedefleme olarak aynı işlevi gerçekleştirmek için her kampanya ölçütünde hedefleme Kurulum listesine gerekir.</span><span class="sxs-lookup"><span data-stu-id="cadc1-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="cadc1-130">Daha fazla yardım için Azure Mobile Engagement UI Analytics, izleme, Segment ve panolar bölümlerindeki bağlam menülerini bakın ve bilgileri nasıl.</span><span class="sxs-lookup"><span data-stu-id="cadc1-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="cadc1-131">Sorun giderme kilitlenme</span><span class="sxs-lookup"><span data-stu-id="cadc1-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="cadc1-132">Sorun</span><span class="sxs-lookup"><span data-stu-id="cadc1-132">Issue</span></span>
* <span data-ttu-id="cadc1-133">Uygulama analizi, izleme veya Pano görünmesini kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="cadc1-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="cadc1-134">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="cadc1-134">Causes</span></span>
* <span data-ttu-id="cadc1-135">Sorun giderme için uygulama analizi, izleme veya Pano görülen çöküyor SDK'ın önceki sürümleri ile ilgili bilinen sorunlar için sürüm notları denetlemek emin olun.</span><span class="sxs-lookup"><span data-stu-id="cadc1-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="cadc1-136">Daha fazla sorun giderme için bir test cihazı uygulamaların yüklü olduğu ve cihaz Kimliğinizi Azure Mobile Engagement UI "İzleyici – olayları" bölümündeki Ara olay uygulama kilitlenmelerine gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cadc1-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="cadc1-137">Sonra uygulamanızın kilitlenme ve Azure Mobile Engagement UI "İzleyici – kilitlenme" bölümünde ek bilgileri aramak neden olan olay gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cadc1-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

