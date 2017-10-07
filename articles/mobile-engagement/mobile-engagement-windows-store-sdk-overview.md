---
title: "aaaAzure Mobile Engagement Windows Evrensel SDK tümleştirmesi | Microsoft Docs"
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
ms.openlocfilehash: 2f88e58adb349a2a4eb43b0f182f99b3e8b8cfd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a>Azure Mobile Engagement için Windows Evrensel SDK tümleştirmesi
Bu belgede tüm hello tümleştirme ve yapılandırma seçenekleri hello Azure Mobile Engagement Windows Evrensel SDK açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce ilk tamamlamalısınız bizim [15 dakikalık Öğreticisi](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="advanced-features"></a>Gelişmiş özellikler
### <a name="reporting-features"></a>Raporlama özellikleri
Bu özellikler ekleyebilirsiniz:

1. [Gelişmiş raporlama seçenekleri](mobile-engagement-windows-store-advanced-reporting.md)
2. [Gelişmiş yapılandırma seçenekleri](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a>Bildirimler
[Nasıl Windows Evrensel uygulamanızda toointegrate ulaşma (bildirimleri)](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a>Etiket planı uygulama:
[Mobile Engagement Windows Evrensel uygulamanız API etiketleme toouse hello nasıl Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a>Sürüm notları
### <a name="341-11032016"></a>3.4.1 (11/03/2016)

* İstikrara yönelik iyileştirmeler.

Önceki sürümler için bkz: Merhaba [tamamlamak sürüm notları](mobile-engagement-windows-store-release-notes.md)

## <a name="upgrade-procedures"></a>Yükseltme yordamları
Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Merhaba SDK çeşitli sürümleri eksik, çeşitli yordamlar toofollow olabilir. Bkz: hello tam [yükseltme yordamları](mobile-engagement-windows-store-upgrade-procedure.md). 0.10.1 geçirirseniz örneğin hello izleyin toofirst sahip too0.11.0 "0.9.0'dan gelen too0.10.1" yordamı sonra hello "0.10.1 gelen too0.11.0" yordamı.

### <a name="from-330-too340"></a>3.3.0 gelen too3.4.0
#### <a name="test-logs"></a>Test günlükleri
Konsol günlükleri Hello SDK tarafından üretilen artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir. toocustomize, güncelleştirme hello özelliği `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerlerin `EngagementTestLogLevel` numaralandırma, örneğin:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a>Kaynaklar
Merhaba ulaşma katmana geliştirilmiştir. Merhaba SDK NuGet paketini kaynakları parçasıdır.

Merhaba SDK'ın yeni sürümü toohello yükseltirken tookeep istediğinizi varolan hello dosyalarınızdan kaynaklarınızın klasör veya kaplama seçebilirsiniz:

* Merhaba önceki katmana sizin yerinize çalıştığından veya hello tümleştirme `WebView` öğeleri el ile daha sonra karar, çıkma tookeep dosyaları, hala çalışmayacak.
* tooupdate toohello yeni katmana, tüm Değiştir hello `overlay` kaynaklarınızla hello SDK paketinden yeni bir hello klasöründen (UWP uygulamaları: hello yükseltmeden sonra % USERPROFILE % hello yeni katmana klasör alabilirsiniz\\.nuget\packages\ MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Merhaba yeni katmana kullanarak hello önceki sürümünde yapılan tüm özelleştirmeler üzerine yazar.
> 
> 

### <a name="upgrade-from-older-versions"></a>Eski sürümlerinden yükseltme
Bkz: [yükseltme yordamları](mobile-engagement-windows-store-upgrade-procedure.md)

