---
title: "Olay izleme ile sorunlarını giderme | Microsoft Docs"
description: "Microsoft Azure Service Fabric Services'de dağıtırken karşılaşılan en yaygın sorunları."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Azure Service Fabric Services'de dağıttığınızda sık rastlanan sorunları giderme
Geliştirici bilgisayarınızda Hizmetleri çalıştırırken, kullanımı kolay [hata ayıklama Visual Studio Araçları](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Uzak kümeleri için [sistem durumu raporlarının](service-fabric-view-entities-aggregated-health.md) her zaman başlatmak için iyi bir yerdir. Bu raporlara erişmek için en kolay yollarından PowerShell aracılığıyla olan veya [SFX](service-fabric-visualizing-your-cluster.md). Bu makalede, uzak bir küme hata ayıklama ve bu araçlardan birini kullanımıyla ilgili temel bilgilere sahipsiniz varsayar.

## <a name="application-crash"></a>Uygulama kilitlenme
"Bölüm aşağıdadır hedef çoğaltma veya örnek sayısının" rapordur hizmetinizi kilitlenen bir göstergesidir. Bulmanın nerede hizmetinizi kilitlenen biraz daha fazla araştırma alır. Hizmetinizi ölçekte çalışırken en iyi arkadaşınızın iyi planlanmış genişletme izlemeleri kümesi olur.  Denemeden önerin [Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) bu izlemeleri toplamak ve bir çözüm gibi kullanılarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) görüntüleme ve izlemeleri arama için.

![SFX bölüm sistem durumu](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Hizmet veya aktör başlatma sırasında
Hizmet türü başlatılmadan önce tüm özel durumlar işleminin çökmesine neden olur. Bu kilitlenme türleri için uygulama olay günlüğüne hizmetinizden hata gösterir.
Bu hizmet başlatılmadan önce görmek için en yaygın durumlardır.

***System.IO.FileNotFoundException***

Bu hata genellikle derleme bağımlılıkları nedeniyle eksik. Visual Studio ya da düğümü için Genel Derleme Önbelleği CopyLocal özelliğini denetleyin.

***System.Runtime.InteropServices.COMException*** *adresindeki System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Bu, kayıtlı hizmet türü adı hizmet bildirimi eşleşmediğini gösterir.

[Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) tüm düğümler için uygulama olay günlüğünü otomatik olarak karşıya yüklemek için yapılandırılabilir.

### <a name="runasync-or-onactivateasync"></a>RunAsync() veya OnActivateAsync()
Kilitlenme başlatma veya kayıtlı hizmet türü veya aktör çalıştırılması sırasında oluşursa, Azure Service Fabric tarafından özel durum yakalandı. Bu "Sonraki adımlar" bölümünde ayrıntılı EventSource sağlayıcılardan görüntüleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric tarafından sağlanan mevcut Tanılama hakkında daha fazla bilgi edinin:

* [Güvenilir aktörler tanılama](service-fabric-reliable-actors-diagnostics.md)
* [Güvenilir hizmetler tanılama](service-fabric-reliable-services-diagnostics.md)

