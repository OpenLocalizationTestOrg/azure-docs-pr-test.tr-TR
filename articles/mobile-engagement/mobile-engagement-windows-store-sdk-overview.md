---
title: "Azure Mobile Engagement Windows Evrensel SDK tümleştirmesi | Microsoft Docs"
description: "Azure Mobile Engagement SDK'sı tümleştirmesi Evrensel Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: d616ad58156a19e89b3e106639a38df67cbd0abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="50b0f-103">Azure Mobile Engagement için Windows Evrensel SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="50b0f-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="50b0f-104">Bu belgede, tümleştirme ve yapılandırma için tüm seçenekleri kullanılabilir Azure Mobile Engagement Windows Evrensel SDK açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="50b0f-104">This document describes all the integration and configuration options available for the Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50b0f-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="50b0f-105">Prerequisites</span></span>
<span data-ttu-id="50b0f-106">Bu öğreticiye başlamadan önce ilk tamamlamalısınız bizim [15 dakikalık Öğreticisi](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="50b0f-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="50b0f-107">Gelişmiş özellikler</span><span class="sxs-lookup"><span data-stu-id="50b0f-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="50b0f-108">Raporlama özellikleri</span><span class="sxs-lookup"><span data-stu-id="50b0f-108">Reporting features</span></span>
<span data-ttu-id="50b0f-109">Bu özellikler ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="50b0f-109">You can add these features:</span></span>

1. [<span data-ttu-id="50b0f-110">Gelişmiş raporlama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="50b0f-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="50b0f-111">Gelişmiş yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="50b0f-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="50b0f-112">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="50b0f-112">Notifications</span></span>
[<span data-ttu-id="50b0f-113">Windows Evrensel uygulamanız ulaşma (bildirimler) tümleştirme</span><span class="sxs-lookup"><span data-stu-id="50b0f-113">How to integrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="50b0f-114">Etiket planı uygulama:</span><span class="sxs-lookup"><span data-stu-id="50b0f-114">Tag plan implementation:</span></span>
[<span data-ttu-id="50b0f-115">Gelişmiş Mobile Engagement Windows Evrensel uygulamanız API etiketleme kullanma</span><span class="sxs-lookup"><span data-stu-id="50b0f-115">How to use the advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="50b0f-116">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="50b0f-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="50b0f-117">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="50b0f-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="50b0f-118">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="50b0f-118">Stability improvements.</span></span>

<span data-ttu-id="50b0f-119">Önceki sürümler için bkz: [tamamlamak sürüm notları](mobile-engagement-windows-store-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="50b0f-119">For earlier versions, see the [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="50b0f-120">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="50b0f-120">Upgrade procedures</span></span>
<span data-ttu-id="50b0f-121">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz, SDK'yı yükseltirken aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="50b0f-121">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="50b0f-122">SDK çeşitli sürümleri eksik, birkaç yordamları izleyin olabilir.</span><span class="sxs-lookup"><span data-stu-id="50b0f-122">If you missed several versions of the SDK, you may have to follow several procedures.</span></span> <span data-ttu-id="50b0f-123">Tam bkz [yükseltme yordamları](mobile-engagement-windows-store-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="50b0f-123">See the complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="50b0f-124">Örneğin, 0.10.1 önce "Kimden 0.9.0'dan 0.10.1 için" yordamını takip etmek için sahip 0.11.0 sonra "Kimden 0.10.1 0.11.0 için" yordamı geçiş ise.</span><span class="sxs-lookup"><span data-stu-id="50b0f-124">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

### <a name="from-330-to-340"></a><span data-ttu-id="50b0f-125">3.3.0 3.4.0 için</span><span class="sxs-lookup"><span data-stu-id="50b0f-125">From 3.3.0 to 3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="50b0f-126">Test günlükleri</span><span class="sxs-lookup"><span data-stu-id="50b0f-126">Test logs</span></span>
<span data-ttu-id="50b0f-127">SDK'sı tarafından üretilen konsol günlükleri artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="50b0f-127">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="50b0f-128">Özelleştirmek için özelliğini güncelleştirme `EngagementAgent.Instance.TestLogEnabled` kullanılabilir değerlerden birine `EngagementTestLogLevel` numaralandırma, örneğin:</span><span class="sxs-lookup"><span data-stu-id="50b0f-128">To customize, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the values available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="50b0f-129">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="50b0f-129">Resources</span></span>
<span data-ttu-id="50b0f-130">Reach katmana geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="50b0f-130">The Reach overlay has been improved.</span></span> <span data-ttu-id="50b0f-131">SDK'sı NuGet paketi kaynakları parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="50b0f-131">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="50b0f-132">SDK'ın yeni sürümüne yükseltirken, varolan dosyalarınızı kaynaklarınızı katmana klasöründen veya tutmak isteyip istemediğinizi seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="50b0f-132">While upgrading to the new version of the SDK, you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="50b0f-133">Önceki katmana sizin yerinize çalıştığından veya tümleştirme `WebView` öğeleri el ile daha sonra karar, çıkma tutmak dosyaları, bunu hala çalışır.</span><span class="sxs-lookup"><span data-stu-id="50b0f-133">If the previous overlay is working for you, or you are integrating the `WebView` elements manually, then you can decide to keep your exiting files, it will still work.</span></span>
* <span data-ttu-id="50b0f-134">Yeni katmana güncelleştirmek için tüm Değiştir `overlay` kaynaklarınızı klasöründen SDK paketinden yeni bir (UWP uygulamaları: yükseltmeden sonra yeni katmana klasör % USERPROFILE % alabilirsiniz\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="50b0f-134">To update to the new overlay, replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="50b0f-135">Yeni katmana kullanarak önceki bir sürümünde yapılan tüm özelleştirmeler üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="50b0f-135">Using the new overlay overwrites any customizations made on the previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="50b0f-136">Eski sürümlerinden yükseltme</span><span class="sxs-lookup"><span data-stu-id="50b0f-136">Upgrade from older versions</span></span>
<span data-ttu-id="50b0f-137">Bkz: [yükseltme yordamları](mobile-engagement-windows-store-upgrade-procedure.md)</span><span class="sxs-lookup"><span data-stu-id="50b0f-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

