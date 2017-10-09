---
title: Azure Application Insights HockeyApp verileri aaaExploring | Microsoft Docs
description: "Kullanım ve Application Insights ile Azure, uygulamanızın performansını analiz edin."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 97783cc6-67d6-465f-9926-cb9821f4176e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: bwren
ms.openlocfilehash: ed7cf99b48f5ec78d6b401bb954cfcd014b9d1f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-hockeyapp-data-in-application-insights"></a><span data-ttu-id="013d9-103">Application Insights HockeyApp verilerde gezinme</span><span class="sxs-lookup"><span data-stu-id="013d9-103">Exploring HockeyApp data in Application Insights</span></span>
<span data-ttu-id="013d9-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello Canlı Masaüstü ve mobil uygulamaları izlemek için platform önerilir.</span><span class="sxs-lookup"><span data-stu-id="013d9-104">[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) is hello recommended platform for monitoring live desktop and mobile apps.</span></span> <span data-ttu-id="013d9-105">HockeyApp özel göndermek ve telemetri toomonitor kullanım izleme ve tanılama (verilerde ekleme toogetting kilitlenme) yardımcı olmak.</span><span class="sxs-lookup"><span data-stu-id="013d9-105">From HockeyApp, you can send custom and trace telemetry toomonitor usage and assist in diagnosis (in addition toogetting crash data).</span></span> <span data-ttu-id="013d9-106">Bu akış telemetri hello güçlü aracılığıyla sorgulanabilir [Analytics](app-insights-analytics.md) özelliği [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="013d9-106">This stream of telemetry can be queried using hello powerful [Analytics](app-insights-analytics.md) feature of [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="013d9-107">Buna ek olarak, şunları yapabilirsiniz [hello özel ve izleme telemetri dışarı](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="013d9-107">In addition, you can [export hello custom and trace telemetry](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="013d9-108">Bu özellikler, tooenable, HockeyApp özel veri tooApplication Öngörüler aktaran bir Köprüsü kurun.</span><span class="sxs-lookup"><span data-stu-id="013d9-108">tooenable these features, you set up a bridge that relays HockeyApp custom data tooApplication Insights.</span></span>

## <a name="hello-hockeyapp-bridge-app"></a><span data-ttu-id="013d9-109">Merhaba HockeyApp köprüsü uygulama</span><span class="sxs-lookup"><span data-stu-id="013d9-109">hello HockeyApp Bridge app</span></span>
<span data-ttu-id="013d9-110">Merhaba HockeyApp köprüsü uygulama tooaccess HockeyApp özel ve Application Insights izleme telemetri hello Analytics üzerinden sağlayan hello çekirdek özelliği ve sürekli verme Özellikleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="013d9-110">hello HockeyApp Bridge App is hello core feature that enables you tooaccess your HockeyApp custom and trace telemetry in Application Insights through hello Analytics and Continuous Export features.</span></span> <span data-ttu-id="013d9-111">Merhaba HockeyApp köprüsü uygulama hello oluşturulduktan sonra HockeyApp tarafından toplanan özel ve izleme olayları bu özelliklerinden erişilebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="013d9-111">Custom and trace events collected by HockeyApp after hello creation of hello HockeyApp Bridge App will be accessible from these features.</span></span> <span data-ttu-id="013d9-112">Görelim nasıl tooset bu köprüsü uygulamalardan birini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="013d9-112">Let’s see how tooset up one of these Bridge Apps.</span></span>

<span data-ttu-id="013d9-113">Hesap ayarları HockeyApp içinde açmak [API belirteçleri](https://rink.hockeyapp.net/manage/auth_tokens).</span><span class="sxs-lookup"><span data-stu-id="013d9-113">In HockeyApp, open Account Settings, [API Tokens](https://rink.hockeyapp.net/manage/auth_tokens).</span></span> <span data-ttu-id="013d9-114">Yeni bir belirteç oluşturmak veya mevcut bir yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="013d9-114">Either create a new token or reuse an existing one.</span></span> <span data-ttu-id="013d9-115">"salt okunur" Merhaba en düşük hakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="013d9-115">hello minimum rights required are "read only".</span></span> <span data-ttu-id="013d9-116">Merhaba API kopyasını belirteci alın.</span><span class="sxs-lookup"><span data-stu-id="013d9-116">Take a copy of hello API token.</span></span>

![HockeyApp API belirteci alma](./media/app-insights-hockeyapp-bridge-app/01.png)

<span data-ttu-id="013d9-118">Açık hello Microsoft Azure portal ve [bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="013d9-118">Open hello Microsoft Azure portal and [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="013d9-119">Uygulama türü çok Ayarla "HockeyApp köprüsü uygulama":</span><span class="sxs-lookup"><span data-stu-id="013d9-119">Set Application Type too“HockeyApp bridge application”:</span></span>

![Yeni Application Insights kaynağı](./media/app-insights-hockeyapp-bridge-app/02.png)

<span data-ttu-id="013d9-121">Bir ad tooset gerekmez - bu hello HockeyApp adından otomatik olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="013d9-121">You don't need tooset a name - this will automatically be set from hello HockeyApp name.</span></span>

<span data-ttu-id="013d9-122">Merhaba HockeyApp köprüsü alanlar görünür.</span><span class="sxs-lookup"><span data-stu-id="013d9-122">hello HockeyApp bridge fields appear.</span></span> 

![Köprü alanları girin](./media/app-insights-hockeyapp-bridge-app/03.png)

<span data-ttu-id="013d9-124">Daha önce not ettiğiniz hello HockeyApp belirteci girin.</span><span class="sxs-lookup"><span data-stu-id="013d9-124">Enter hello HockeyApp token you noted earlier.</span></span> <span data-ttu-id="013d9-125">Bu eylemin hello "HockeyApp uygulama" açılır menüsünde tüm HockeyApp uygulamaları ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="013d9-125">This action populates hello “HockeyApp Application” dropdown menu with all your HockeyApp applications.</span></span> <span data-ttu-id="013d9-126">Toouse ve hello alanları tam hello kalanını istediğiniz hello birini seçin.</span><span class="sxs-lookup"><span data-stu-id="013d9-126">Select hello one you want toouse, and complete hello remainder of hello fields.</span></span> 

<span data-ttu-id="013d9-127">Merhaba yeni kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="013d9-127">Open hello new resource.</span></span> 

<span data-ttu-id="013d9-128">Merhaba veri biraz uzun sürebilir Not toostart akar.</span><span class="sxs-lookup"><span data-stu-id="013d9-128">Note that hello data takes a while toostart flowing.</span></span>

![Uygulama Insights kaynağı için veri bekleniyor](./media/app-insights-hockeyapp-bridge-app/04.png)

<span data-ttu-id="013d9-130">Bu kadar!</span><span class="sxs-lookup"><span data-stu-id="013d9-130">That’s it!</span></span> <span data-ttu-id="013d9-131">Bu noktadan itibaren HockeyApp izlenmiş uygulamanızda toplanan özel ve izleme verileri de hello Analytics içinde kullanılabilir tooyou ve Application Insights sürekli dışarı aktarma özelliklerini sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="013d9-131">Custom and trace data collected in your HockeyApp-instrumented app from this point forward is now also available tooyou in hello Analytics and Continuous Export features of Application Insights.</span></span>

<span data-ttu-id="013d9-132">Şimdi kısaca bu özellik artık kullanılabilir tooyou inceleyin.</span><span class="sxs-lookup"><span data-stu-id="013d9-132">Let’s briefly review each of these features now available tooyou.</span></span>

## <a name="analytics"></a><span data-ttu-id="013d9-133">Analiz</span><span class="sxs-lookup"><span data-stu-id="013d9-133">Analytics</span></span>
<span data-ttu-id="013d9-134">Analytics verilerinizi sorgulama, toodiagnose izin vererek geçici için güçlü bir araçtır ve telemetrinizi analiz ve hızla nedenlerini ve desenler keşfedin.</span><span class="sxs-lookup"><span data-stu-id="013d9-134">Analytics is a powerful tool for ad-hoc querying of your data, allowing you toodiagnose and analyze your telemetry and quickly discover root causes and patterns.</span></span>

![Analiz](./media/app-insights-hockeyapp-bridge-app/05.png)

* [<span data-ttu-id="013d9-136">Analytics hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="013d9-136">Learn more about Analytics</span></span>](app-insights-analytics-tour.md)

## <a name="continuous-export"></a><span data-ttu-id="013d9-137">Sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="013d9-137">Continuous export</span></span>
<span data-ttu-id="013d9-138">Sürekli verme tooexport sağlayan bir Azure Blob Storage kapsayıcısı verilerinizi.</span><span class="sxs-lookup"><span data-stu-id="013d9-138">Continuous Export allows you tooexport your data into an Azure Blob Storage container.</span></span> <span data-ttu-id="013d9-139">Şu an Application Insights tarafından sunulan hello tutma süresinden daha uzun süre verilerinizi tookeep ihtiyacınız varsa bu oldukça yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="013d9-139">This is very useful if you need tookeep your data for longer than hello retention period currently offered by Application Insights.</span></span> <span data-ttu-id="013d9-140">Blob depolama alanına hello verileri korumak, bir SQL veritabanı veya depolama çözümü, tercih edilen verilerinizi işlem.</span><span class="sxs-lookup"><span data-stu-id="013d9-140">You can keep hello data in blob storage, process it into a SQL Database, or your preferred data warehousing solution.</span></span>

[<span data-ttu-id="013d9-141">Sürekli dışarı aktarma hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="013d9-141">Learn more about Continuous Export</span></span>](app-insights-export-telemetry.md)

## <a name="next-steps"></a><span data-ttu-id="013d9-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="013d9-142">Next steps</span></span>
* [<span data-ttu-id="013d9-143">Analytics tooyour verilerini Uygula</span><span class="sxs-lookup"><span data-stu-id="013d9-143">Apply Analytics tooyour data</span></span>](app-insights-analytics-tour.md)

