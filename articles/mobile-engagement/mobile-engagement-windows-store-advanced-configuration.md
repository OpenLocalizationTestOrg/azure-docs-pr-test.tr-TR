---
title: "aaaAdvanced yapılandırma için Windows Evrensel uygulamaları Engagement SDK'sı"
description: "Gelişmiş yapılandırma seçenekleri için Azure Mobile Engagement Windows Evrensel uygulamaları ile"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="ceaaa-103">Gelişmiş Windows Evrensel uygulamaları Engagement SDK'sı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ceaaa-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ceaaa-104">Evrensel Windows</span><span class="sxs-lookup"><span data-stu-id="ceaaa-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="ceaaa-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ceaaa-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="ceaaa-106">iOS</span><span class="sxs-lookup"><span data-stu-id="ceaaa-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="ceaaa-107">Android</span><span class="sxs-lookup"><span data-stu-id="ceaaa-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="ceaaa-108">Bu yordam açıklar nasıl tooconfigure Azure Mobile Engagement Android uygulamaları için çeşitli yapılandırma seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ceaaa-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ceaaa-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="ceaaa-110">Gelişmiş yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ceaaa-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="ceaaa-111">Otomatik Kilitlenme bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ceaaa-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="ceaaa-112">Merhaba otomatik kilitlenme raporlama katılım özelliği devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="ceaaa-113">Ardından, işlenmeyen bir özel durum oluştuğunda katılım hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="ceaaa-114">Bu özelliği devre dışı sonra uygulamanızda işlenmeyen bir kilitlenme ortaya çıktığında, katılım hello kilitlenme göndermez **ve** hello oturum ve işleri kapatmaz.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="ceaaa-115">Raporlama toodisable otomatik kilitlenme yapılandırmanıza bağlı olarak, bildirilen hello şekilde Özelleştir:</span><span class="sxs-lookup"><span data-stu-id="ceaaa-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="ceaaa-116">Gelen `EngagementConfiguration.xml` dosyası</span><span class="sxs-lookup"><span data-stu-id="ceaaa-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="ceaaa-117">Raporu çökme çok Ayarla`false` arasında `<reportCrash>` ve `</reportCrash>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="ceaaa-118">Gelen `EngagementConfiguration` çalışma zamanında nesne</span><span class="sxs-lookup"><span data-stu-id="ceaaa-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="ceaaa-119">EngagementConfiguration nesnesini kullanarak rapor kilitlenme toofalse ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="ceaaa-120">Gerçek zamanlı raporlama devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ceaaa-120">Disable real time reporting</span></span>
<span data-ttu-id="ceaaa-121">Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="ceaaa-122">Uygulamanızı günlükleri sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları aynı anda normal zaman temelinde.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="ceaaa-123">Bu, "veri bloğu modu" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-123">This is called “burst mode”.</span></span>

<span data-ttu-id="ceaaa-124">toodo, bu nedenle, hello yöntemi çağırın:</span><span class="sxs-lookup"><span data-stu-id="ceaaa-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="ceaaa-125">Merhaba bağımsız değişkeni olarak bir değerdir **milisaniye**.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="ceaaa-126">Tooreactivate hello gerçek zamanlı günlük tutma istediğinizde, hello 0 değerine sahip veya herhangi bir parametre olmadan hello yöntemi çağırın.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="ceaaa-127">Veri bloğu modu biraz hello pil ömrünün artırır ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olan.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="ceaaa-128">Bir veri bloğu eşikten artık 30000 (30s) kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="ceaaa-129">Kaydedilen günlükler sınırlı too300 öğelerdir.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="ceaaa-130">Gönderme çok uzunsa, bazı günlükleri kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="ceaaa-131">Merhaba veri bloğu eşiği ikinci bir'den küçük yapılandırılmış tooa nokta olamaz.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="ceaaa-132">Bunu yaparsanız, hello SDK izleme hello hatasıyla gösterir ve otomatik olarak toohello varsayılan değeri, sıfır saniye sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="ceaaa-133">Bu tetikleyicileri hello SDK tooreport hello gerçek zamanlı oturumunu açar.</span><span class="sxs-lookup"><span data-stu-id="ceaaa-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
