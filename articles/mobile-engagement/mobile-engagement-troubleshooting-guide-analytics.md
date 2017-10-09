---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - Analytics'i"
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
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="63dbe-103">Analiz, izleme, Segment ve Pano sorunları için sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="63dbe-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="63dbe-104">Merhaba olası sorunlar aşağıda verilmiştir Azure Mobile Engagement'ın uygulamaları, cihazlar ve kullanıcılar hakkında bilgileri nasıl toplar karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63dbe-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="63dbe-105">Eksik Gecikmeli bilgi</span><span class="sxs-lookup"><span data-stu-id="63dbe-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="63dbe-106">Sorun</span><span class="sxs-lookup"><span data-stu-id="63dbe-106">Issue</span></span>
* <span data-ttu-id="63dbe-107">Bilgi Analytics, Segment veya Pano görünmesini içinde ertelendi.</span><span class="sxs-lookup"><span data-stu-id="63dbe-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="63dbe-108">İzleme bilgileri eksik.</span><span class="sxs-lookup"><span data-stu-id="63dbe-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="63dbe-109">Analytics, Segment veya pano bilgileri eksik.</span><span class="sxs-lookup"><span data-stu-id="63dbe-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="63dbe-110">Segment basarsa sınırlar.</span><span class="sxs-lookup"><span data-stu-id="63dbe-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="63dbe-111">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="63dbe-111">Causes</span></span>
* <span data-ttu-id="63dbe-112">Merhaba Analytics API, İzleyici API kullanabilirsiniz ve herhangi bir veri UI hello eksik olması durumunda kesimleri API toosee hello API'leri görülebilir.</span><span class="sxs-lookup"><span data-stu-id="63dbe-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="63dbe-113">Ardından Hello Azure Mobile Engagement SDK'sını uygulamanıza doğru tümleşik değilse hello Analytics, Segment, izleme veya panolar mümkün toosee bilgileri olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="63dbe-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="63dbe-114">Parçaları olamaz oluşturulduktan sonra kesimleri yalnızca "kopya" (kopyalanır) veya "(silinir) yok" değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="63dbe-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="63dbe-115">Segmentler yalnızca 10 ölçüt içerebilir.</span><span class="sxs-lookup"><span data-stu-id="63dbe-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="63dbe-116">İzleme bilgilerinin eksik hello en iyi şekilde tootest toosetup bir test cihazı, kaldırma ve/veya hello test aygıtta hello uygulamayı yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="63dbe-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="63dbe-117">Bilgileri Analytics, Segment veya panolar için 24 saatte bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="63dbe-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="63dbe-118">Yeni kesimleri bilgilerinde hello segment önceki bilgilere dayalı olsa bile oluşturulduktan sonra 24 saate kadar görüntülenmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="63dbe-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="63dbe-119">Analiz verilerinizi hello UI filtreleme, uygulamanızın hello sürüm ne olursa olsun bu türdeki tüm örnekler (örneğin gösterir "Adına göre filtre kilitleniyor" sürüm 1 ve sürüm 2, uygulamanızın gösterir).</span><span class="sxs-lookup"><span data-stu-id="63dbe-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="63dbe-120">Başlangıç tarihi yanlış ayarlanmış olan telefon sahip bir kullanıcı hello süre yanlış gösterilebileceği şekilde hello süre analiz için hello kullanıcıların cihaz ayarları, başlangıç tarihinden temel alır.</span><span class="sxs-lookup"><span data-stu-id="63dbe-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="63dbe-121">Merhaba düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı çok "test" iter, veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="63dbe-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="63dbe-122">Öğeleri kullanıcı Arabiriminde bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="63dbe-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="63dbe-123">Sorun</span><span class="sxs-lookup"><span data-stu-id="63dbe-123">Issue</span></span>
* <span data-ttu-id="63dbe-124">Bazı yerleşik göre kesimleri oluşturulamıyor veya özel uygulama bilgisi ölçütleri etiketi.</span><span class="sxs-lookup"><span data-stu-id="63dbe-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="63dbe-125">Bazı yerleşik bulunamıyor veya özel uygulama bilgisi ölçütleri Analytics, izleme veya panolar etiketi.</span><span class="sxs-lookup"><span data-stu-id="63dbe-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="63dbe-126">Merhaba veri analizi, izleme, Segment veya panolar yorumlayamayacağı.</span><span class="sxs-lookup"><span data-stu-id="63dbe-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="63dbe-127">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="63dbe-127">Causes</span></span>
* <span data-ttu-id="63dbe-128">Bazı öğeler yerleşik ve etiketleri yalnızca itme ölçüt olarak kullanılabilir, ancak olmayabilir uygulama bilgisi eklemişsiniz tooa segment veya Analytics, izleme veya Pano görünür.</span><span class="sxs-lookup"><span data-stu-id="63dbe-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="63dbe-129">Yerleşik öğeleri ve tooa segment olamaz etiketleri eklendi uygulama bilgileri için aynı hedefleyen bir kesiminde dayalı olarak işlevi her kampanya tooperform hello ölçütünde hedefleme toosetup listeye ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="63dbe-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="63dbe-130">Merhaba bağlam menülerini hello Analytics, izleme, Segment ve panolar bölümlerini hello Azure Mobile Engagement UI daha fazla yardım için bkz. nasıl ve ne tooinformation.</span><span class="sxs-lookup"><span data-stu-id="63dbe-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="63dbe-131">Sorun giderme kilitlenme</span><span class="sxs-lookup"><span data-stu-id="63dbe-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="63dbe-132">Sorun</span><span class="sxs-lookup"><span data-stu-id="63dbe-132">Issue</span></span>
* <span data-ttu-id="63dbe-133">Uygulama analizi, izleme veya Pano görünmesini kilitleniyor.</span><span class="sxs-lookup"><span data-stu-id="63dbe-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="63dbe-134">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="63dbe-134">Causes</span></span>
* <span data-ttu-id="63dbe-135">Analytics, izleme veya Pano görülen tootroubleshoot uygulaması kilitlenir hello SDK önceki sürümleri ile ilgili bilinen sorunlar için emin toocheck hello sürüm notları olun.</span><span class="sxs-lookup"><span data-stu-id="63dbe-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="63dbe-136">toofurther kilitlenme olaya uygulamaların yüklü olduğu bir test aygıttan gerçekleştirmek ve cihaz Kimliğinizi hello Azure Mobile Engagement UI hello "İzleyici – olayları" bölümünde aramak uygulama sorunlarını giderin.</span><span class="sxs-lookup"><span data-stu-id="63dbe-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="63dbe-137">Ardından, uygulama toocrash neden hello olay gerçekleştirin ve hello hello Azure Mobile Engagement UI "– monitör kilitlenme" bölümünü ek bilgi arayın.</span><span class="sxs-lookup"><span data-stu-id="63dbe-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

