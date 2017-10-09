---
title: Olay izleme ile aaaTroubleshooting | Microsoft Docs
description: "Microsoft Azure Service Fabric Services'de dağıtırken karşılaşılan en yaygın sorunları hello."
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
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Azure Service Fabric Services'de dağıttığınızda sık rastlanan sorunları giderme
Geliştirici bilgisayarınızda Hizmetleri çalıştırırken kolay toouse olan [hata ayıklama Visual Studio Araçları](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Uzak kümeleri için [sistem durumu raporlarının](service-fabric-view-entities-aggregated-health.md) her zaman iyi toostart olur. Bu raporlar içindir PowerShell aracılığıyla en kolay yolu tooaccess hello veya [SFX](service-fabric-visualizing-your-cluster.md). Bu makalede, uzak bir küme hata ayıklama ve nasıl ilgili temel bilgilere sahipsiniz varsayar bunlardan araçları toouse.

## <a name="application-crash"></a>Uygulama kilitlenme
Merhaba "bölümdür aşağıda hedef çoğaltma veya örnek sayısının" rapordur hizmetinizi kilitlenen bir göstergesidir. Burada hizmetinizi kilitlenen çıkışı toofind biraz daha fazla araştırma alır. Hizmetinizi ölçekte çalışırken en iyi arkadaşınızın iyi planlanmış genişletme izlemeleri kümesi olur.  Denemeden önerin [Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) bu izlemeleri toplamak ve bir çözüm gibi kullanılarak [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) görüntüleme ve arama hello izlemeleri için.

![SFX bölüm sistem durumu](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Hizmet veya aktör başlatma sırasında
Merhaba hizmet türü başlatılmadan önce tüm özel durumlar hello işlem toocrash neden olur. Bu kilitlenme türlerinde hello uygulama olay günlüğü hizmetinizden hello hata gösterir.
Merhaba hizmet başlatılmadan önce hello en yaygın özel durumları toosee bunlar.

***System.IO.FileNotFoundException***

Bu hata genellikle toomissing derleme bağımlılıkları olur. Visual Studio veya hello Genel Derleme Önbelleği hello düğüm için Hello CopyLocal özelliği denetleyin.

***System.Runtime.InteropServices.COMException*** *adresindeki System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Bu, hello kayıtlı hizmet türü adının hello hizmet bildirimi eşleşmiyor gösterir.

[Azure tanılama](service-fabric-diagnostics-how-to-setup-wad.md) yapılandırılmış tooupload hello uygulama olay günlüğü, tüm düğümler için otomatik olarak olabilir.

### <a name="runasync-or-onactivateasync"></a>RunAsync() veya OnActivateAsync()
Merhaba kilitlenme hello başlatma veya kayıtlı hizmet türü veya aktör çalıştırılması sırasında oluşursa, Azure Service Fabric tarafından hello özel durum yakalandı. Bunlar hello "Sonraki adımlar" bölümüne ayrıntılı hello EventSource sağlayıcılardan görüntüleyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric tarafından sağlanan mevcut Tanılama hakkında daha fazla bilgi edinin:

* [Güvenilir aktörler tanılama](service-fabric-reliable-actors-diagnostics.md)
* [Güvenilir hizmetler tanılama](service-fabric-reliable-services-diagnostics.md)

