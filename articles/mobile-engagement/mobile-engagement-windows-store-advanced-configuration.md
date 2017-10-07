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
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Gelişmiş Windows Evrensel uygulamaları Engagement SDK'sı için yapılandırma
> [!div class="op_single_selector"]
> * [Evrensel Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Bu yordam açıklar nasıl tooconfigure Azure Mobile Engagement Android uygulamaları için çeşitli yapılandırma seçenekleri.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Gelişmiş yapılandırma
### <a name="disable-automatic-crash-reporting"></a>Otomatik Kilitlenme bildirimini devre dışı bırak
Merhaba otomatik kilitlenme raporlama katılım özelliği devre dışı bırakabilirsiniz. Ardından, işlenmeyen bir özel durum oluştuğunda katılım hiçbir şey yapmaz.

> [!WARNING]
> Bu özelliği devre dışı sonra uygulamanızda işlenmeyen bir kilitlenme ortaya çıktığında, katılım hello kilitlenme göndermez **ve** hello oturum ve işleri kapatmaz.
> 
> 

Raporlama toodisable otomatik kilitlenme yapılandırmanıza bağlı olarak, bildirilen hello şekilde Özelleştir:

#### <a name="from-engagementconfigurationxml-file"></a>Gelen `EngagementConfiguration.xml` dosyası
Raporu çökme çok Ayarla`false` arasında `<reportCrash>` ve `</reportCrash>` etiketler.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Gelen `EngagementConfiguration` çalışma zamanında nesne
EngagementConfiguration nesnesini kullanarak rapor kilitlenme toofalse ayarlayın.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Gerçek zamanlı raporlama devre dışı bırak
Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder. Uygulamanızı günlükleri sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları aynı anda normal zaman temelinde. Bu, "veri bloğu modu" adı verilir.

toodo, bu nedenle, hello yöntemi çağırın:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Merhaba bağımsız değişkeni olarak bir değerdir **milisaniye**. Tooreactivate hello gerçek zamanlı günlük tutma istediğinizde, hello 0 değerine sahip veya herhangi bir parametre olmadan hello yöntemi çağırın.

Veri bloğu modu biraz hello pil ömrünün artırır ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olan. Bir veri bloğu eşikten artık 30000 (30s) kullanmanızı öneririz. Kaydedilen günlükler sınırlı too300 öğelerdir. Gönderme çok uzunsa, bazı günlükleri kaybedebilir.

> [!WARNING]
> Merhaba veri bloğu eşiği ikinci bir'den küçük yapılandırılmış tooa nokta olamaz. Bunu yaparsanız, hello SDK izleme hello hatasıyla gösterir ve otomatik olarak toohello varsayılan değeri, sıfır saniye sıfırlar. Bu tetikleyicileri hello SDK tooreport hello gerçek zamanlı oturumunu açar.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
