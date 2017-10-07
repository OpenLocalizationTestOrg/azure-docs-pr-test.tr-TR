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
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Azure Mobile Engagement için Android SDK tümleştirmesi
> [!div class="op_single_selector"]
> * [Evrensel Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

Bu belgede tüm hello tümleştirme ve yapılandırma seçenekleri için Azure Mobile Engagement Android SDK açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Gelişmiş Özellikler
### <a name="reporting-features"></a>Raporlama özellikleri
Bu özellikler ekleyebilirsiniz:

1. [Gelişmiş raporlama seçenekleri](mobile-engagement-android-advanced-reporting.md)
2. [Konum raporlama seçenekleri](mobile-engagement-android-location-reporting.md)
3. [Gelişmiş yapılandırma seçenekleri](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Bildirimler:
[Nasıl Android uygulamanızda toointegrate ulaşma (bildirimleri)](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM): [nasıl tooIntegrate Mobile Engagement ile GCM](mobile-engagement-android-gcm-integrate.md)
2. Amazon cihaz Mesajlaşma (ADM): [nasıl tooIntegrate ADM Mobile engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Etiket planı uygulama:
[Mobile Engagement Android uygulamanızda API etiketleme toouse hello nasıl Gelişmiş](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Sürüm notları

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Çağrılırken nadiren bir kilitlenme düzeltme `EngagementAgentUtils.isInDedicatedEngagementProcess`, ayrıca hello tarafından kullanılan `EngagementApplication` sınıfı.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 desteği (SDK'sı üzerinde Android 8 çalışmaz hello önceki sürümler).
* Daha fazla hiçbir bağımlılık destek kitaplığı.
* Kaldırma `EngagementFragmentActivity` sınıfı.
* Son çok[arka plan yürütme sınırları](https://developer.android.com/preview/features/background.html) hello kullanıcı hello aygıt ile etkileşim kadar arka planda günlükleri Android 8'de Gecikmeli, bu bir itme kampanya etkileyecek **teslim edildi** ve **Sistem bildirimi görüntülenir** hello Aygıt uyku durumunda erteleniyor istatistikleri (Merhaba bildirim görüntülenmeye devam eder, halka ve gerçek zamanlı sorun olmadan Titret).
* Son çok[arka plan konum sınırları](https://developer.android.com/preview/features/background-location-limits.html), arka planda hello gerçek zamanlı konum güncelleştirilmeyecek sık üzerinde Android 8.

Tüm sürümler için bkz: Merhaba [tamamlamak sürüm notları](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Yükseltme yordamları
Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz başvurun [yükseltme yordamları](mobile-engagement-android-upgrade-procedure.md).

