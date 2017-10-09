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
# <a name="exploring-hockeyapp-data-in-application-insights"></a>Application Insights HockeyApp verilerde gezinme
[HockeyApp](https://azure.microsoft.com/services/hockeyapp/) hello Canlı Masaüstü ve mobil uygulamaları izlemek için platform önerilir. HockeyApp özel göndermek ve telemetri toomonitor kullanım izleme ve tanılama (verilerde ekleme toogetting kilitlenme) yardımcı olmak. Bu akış telemetri hello güçlü aracılığıyla sorgulanabilir [Analytics](app-insights-analytics.md) özelliği [Azure Application Insights](app-insights-overview.md). Buna ek olarak, şunları yapabilirsiniz [hello özel ve izleme telemetri dışarı](app-insights-export-telemetry.md). Bu özellikler, tooenable, HockeyApp özel veri tooApplication Öngörüler aktaran bir Köprüsü kurun.

## <a name="hello-hockeyapp-bridge-app"></a>Merhaba HockeyApp köprüsü uygulama
Merhaba HockeyApp köprüsü uygulama tooaccess HockeyApp özel ve Application Insights izleme telemetri hello Analytics üzerinden sağlayan hello çekirdek özelliği ve sürekli verme Özellikleri ' dir. Merhaba HockeyApp köprüsü uygulama hello oluşturulduktan sonra HockeyApp tarafından toplanan özel ve izleme olayları bu özelliklerinden erişilebilir olacaktır. Görelim nasıl tooset bu köprüsü uygulamalardan birini ayarlama.

Hesap ayarları HockeyApp içinde açmak [API belirteçleri](https://rink.hockeyapp.net/manage/auth_tokens). Yeni bir belirteç oluşturmak veya mevcut bir yeniden kullanabilirsiniz. "salt okunur" Merhaba en düşük hakları gerekir. Merhaba API kopyasını belirteci alın.

![HockeyApp API belirteci alma](./media/app-insights-hockeyapp-bridge-app/01.png)

Açık hello Microsoft Azure portal ve [bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md). Uygulama türü çok Ayarla "HockeyApp köprüsü uygulama":

![Yeni Application Insights kaynağı](./media/app-insights-hockeyapp-bridge-app/02.png)

Bir ad tooset gerekmez - bu hello HockeyApp adından otomatik olarak ayarlanır.

Merhaba HockeyApp köprüsü alanlar görünür. 

![Köprü alanları girin](./media/app-insights-hockeyapp-bridge-app/03.png)

Daha önce not ettiğiniz hello HockeyApp belirteci girin. Bu eylemin hello "HockeyApp uygulama" açılır menüsünde tüm HockeyApp uygulamaları ile doldurur. Toouse ve hello alanları tam hello kalanını istediğiniz hello birini seçin. 

Merhaba yeni kaynağı açın. 

Merhaba veri biraz uzun sürebilir Not toostart akar.

![Uygulama Insights kaynağı için veri bekleniyor](./media/app-insights-hockeyapp-bridge-app/04.png)

Bu kadar! Bu noktadan itibaren HockeyApp izlenmiş uygulamanızda toplanan özel ve izleme verileri de hello Analytics içinde kullanılabilir tooyou ve Application Insights sürekli dışarı aktarma özelliklerini sunulmuştur.

Şimdi kısaca bu özellik artık kullanılabilir tooyou inceleyin.

## <a name="analytics"></a>Analiz
Analytics verilerinizi sorgulama, toodiagnose izin vererek geçici için güçlü bir araçtır ve telemetrinizi analiz ve hızla nedenlerini ve desenler keşfedin.

![Analiz](./media/app-insights-hockeyapp-bridge-app/05.png)

* [Analytics hakkında daha fazla bilgi edinin](app-insights-analytics-tour.md)

## <a name="continuous-export"></a>Sürekli dışarı aktarma
Sürekli verme tooexport sağlayan bir Azure Blob Storage kapsayıcısı verilerinizi. Şu an Application Insights tarafından sunulan hello tutma süresinden daha uzun süre verilerinizi tookeep ihtiyacınız varsa bu oldukça yararlıdır. Blob depolama alanına hello verileri korumak, bir SQL veritabanı veya depolama çözümü, tercih edilen verilerinizi işlem.

[Sürekli dışarı aktarma hakkında daha fazla bilgi edinin](app-insights-export-telemetry.md)

## <a name="next-steps"></a>Sonraki adımlar
* [Analytics tooyour verilerini Uygula](app-insights-analytics-tour.md)

