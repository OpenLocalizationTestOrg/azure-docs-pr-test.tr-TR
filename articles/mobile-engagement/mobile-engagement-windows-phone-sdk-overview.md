---
title: "aaaAzure Mobile Engagement Windows Phone Silverlight SDK genel bakış | Microsoft Docs"
description: "Hello Azure Mobile Engagement için Windows Phone Silverlight SDK genel bakış"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Windows Phone Silverlight SDK'sına genel bakış için Azure Mobile Engagement
Tooget hello ayrıntılar hakkında buradan başlayın toointegrate Azure Mobile Engagement Windows Phone Silverlight uygulaması içinde. Toogive isterseniz, bir try ilk olarak, emin olun, tamamlamak bizim [15 dakika Öğreticisi](mobile-engagement-windows-phone-get-started.md).

Toosee hello tıklatın [SDK içerik](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Tümleştirme yordamları
1. Buradan başlayın: [nasıl toointegrate Mobile Engagement Windows Phone Silverlight uygulamanızda](mobile-engagement-windows-phone-integrate-engagement.md)
2. Bildirimlerinin: [nasıl toointegrate ulaşma (bildirimleri), Windows Phone Silverlight uygulamanızda](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Etiket planı uygulama: [nasıl toouse hello Mobile Engagement Windows Phone Silverlight uygulamanızda API etiketleme Gelişmiş](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Sürüm notları
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Merhaba parçası *MicrosoftAzure.MobileEngagement* Nuget paketi **v3.4.1**

* İstikrara yönelik iyileştirmeler.

Önceki sürümü için lütfen bkz hello [tamamlamak sürüm notları](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Yükseltme yordamları
Uygulamanıza bizim SDK daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir. Bkz: hello tam [yükseltme yordamları](mobile-engagement-windows-phone-upgrade-procedure.md). 0.10.1 geçirirseniz örneğin hello izleyin toofirst sahip too0.11.0 "0.9.0'dan gelen too0.10.1" yordamı sonra hello "0.10.1 gelen too0.11.0" yordamı.

### <a name="from-200-too330"></a>2.0.0 gelen too3.3.0
#### <a name="test-logs"></a>Test günlükleri
Konsol günlükleri Hello SDK tarafından üretilen artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir. toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Eski sürümlerinden yükseltme
Bkz: [yükseltme yordamları](mobile-engagement-windows-phone-upgrade-procedure.md)

