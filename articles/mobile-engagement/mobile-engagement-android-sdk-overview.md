---
title: "aaaAndroid Azure Mobile Engagement SDK tümleştirmesi"
description: "Açıklar nasıl toointegrate Azure Mobile Engagement SDK'sı Android uygulamalarında"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="79289-103">Azure Mobile Engagement için Android SDK tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="79289-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79289-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="79289-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="79289-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="79289-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="79289-106">iOS</span><span class="sxs-lookup"><span data-stu-id="79289-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="79289-107">Android</span><span class="sxs-lookup"><span data-stu-id="79289-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="79289-108">Bu belgede tüm hello tümleştirme ve yapılandırma seçenekleri için Azure Mobile Engagement Android SDK açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="79289-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79289-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79289-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="79289-110">Gelişmiş Özellikler</span><span class="sxs-lookup"><span data-stu-id="79289-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="79289-111">Raporlama özellikleri</span><span class="sxs-lookup"><span data-stu-id="79289-111">Reporting Features</span></span>
<span data-ttu-id="79289-112">Bu özellikler ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79289-112">You can add these features:</span></span>

1. [<span data-ttu-id="79289-113">Gelişmiş raporlama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="79289-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="79289-114">Konum raporlama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="79289-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="79289-115">Gelişmiş yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="79289-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="79289-116">Bildirimler:</span><span class="sxs-lookup"><span data-stu-id="79289-116">Notifications:</span></span>
[<span data-ttu-id="79289-117">Nasıl Android uygulamanızda toointegrate ulaşma (bildirimleri)</span><span class="sxs-lookup"><span data-stu-id="79289-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="79289-118">Google Cloud Messaging (GCM): [nasıl tooIntegrate Mobile Engagement ile GCM](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="79289-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="79289-119">Amazon cihaz Mesajlaşma (ADM): [nasıl tooIntegrate ADM Mobile engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="79289-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="79289-120">Etiket planı uygulama:</span><span class="sxs-lookup"><span data-stu-id="79289-120">Tag plan implementation:</span></span>
[<span data-ttu-id="79289-121">Mobile Engagement Android uygulamanızda API etiketleme toouse hello nasıl Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="79289-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="79289-122">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="79289-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="79289-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="79289-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="79289-124">Çağrılırken nadiren bir kilitlenme düzeltme `EngagementAgentUtils.isInDedicatedEngagementProcess`, ayrıca hello tarafından kullanılan `EngagementApplication` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="79289-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="79289-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="79289-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="79289-126">Android 8 desteği (SDK'sı üzerinde Android 8 çalışmaz hello önceki sürümler).</span><span class="sxs-lookup"><span data-stu-id="79289-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="79289-127">Daha fazla hiçbir bağımlılık destek kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="79289-127">No more dependency on support library.</span></span>
* <span data-ttu-id="79289-128">Kaldırma `EngagementFragmentActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="79289-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="79289-129">Son çok[arka plan yürütme sınırları](https://developer.android.com/preview/features/background.html) hello kullanıcı hello aygıt ile etkileşim kadar arka planda günlükleri Android 8'de Gecikmeli, bu bir itme kampanya etkileyecek **teslim edildi** ve **Sistem bildirimi görüntülenir** hello Aygıt uyku durumunda erteleniyor istatistikleri (Merhaba bildirim görüntülenmeye devam eder, halka ve gerçek zamanlı sorun olmadan Titret).</span><span class="sxs-lookup"><span data-stu-id="79289-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="79289-130">Son çok[arka plan konum sınırları](https://developer.android.com/preview/features/background-location-limits.html), arka planda hello gerçek zamanlı konum güncelleştirilmeyecek sık üzerinde Android 8.</span><span class="sxs-lookup"><span data-stu-id="79289-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="79289-131">Tüm sürümler için bkz: Merhaba [tamamlamak sürüm notları](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="79289-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="79289-132">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="79289-132">Upgrade procedures</span></span>
<span data-ttu-id="79289-133">Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz başvurun [yükseltme yordamları](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="79289-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

