---
title: "Azure tanılama aaaOverview | Microsoft Docs"
description: "Hata ayıklama, izleme, bulut Hizmetleri, sanal makineler ve hizmet doku trafiği çözümleme performansını ölçmek için Azure Tanılama'yı kullanın"
services: multiple
documentationcenter: .net
author: rboucher
manager: 
editor: 
ms.assetid: baad40d8-c915-4f93-b486-8b160bf33463
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/18/2017
ms.author: robb
ms.openlocfilehash: 2a03a96a37091894d7ab16120c125116e4bf462a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-diagnostics"></a>Azure tanılama nedir
Azure Tanılama, dağıtılan bir uygulama tanılama verilerini hello koleksiyonunu sağlayan Azure içinde hello yetenektir. Bir dizi farklı kaynaktan hello tanılama uzantısını kullanabilirsiniz. Şu anda Azure bulut hizmeti Web ve çalışan rolleri, Microsoft Windows ve Service Fabric çalışan Azure sanal makineler desteklenir. Diğer Azure hizmetleriyle kendi ayrı tanılama vardır.

## <a name="data-you-can-collect"></a>Verileri toplamak
Azure tanılama veri türleri aşağıdaki hello toplayabilirsiniz:

| Veri kaynağı | Açıklama |
| --- | --- |
| Performans sayaçları |İşletim sistemi ve özel performans sayaçları |
| Uygulama günlükleri |Uygulamanız tarafından yazılan iletilerin izleme |
| Windows olay günlükleri |Toohello Windows olay günlüğü sistem gönderilen bilgiler |
| .NET olay kaynağı |Merhaba .NET kullanarak olayları yazma kodu [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) sınıfı |
| IIS günlükleri |IIS web siteleri hakkında bilgi |
| Temel ETW bildirimi |Herhangi bir işlem tarafından oluşturulan olay Windows için izleme olayları |
| Kilitlenme bilgi dökümleri |Bir uygulama kilitlenme hello olay hello işleminde hello durumuyla ilgili bilgileri |
| Özel hata günlükleri |Uygulama veya hizmet tarafından oluşturulan günlükleri |
| Azure tanılama altyapı günlükleri |Tanılama kendisi hakkında bilgi |

Hello Azure tanılama uzantısını bu verileri tooan Azure depolama hesabı aktarma veya tooservices gibi Gönder [Application Insights](../application-insights/app-insights-cloudservices.md). Merhaba veri, hata ayıklama ve sorun giderme performansını ölçmek, kaynak kullanımı, trafik analizi ve kapasite planlaması izleme ve denetim için kullanabilirsiniz.

## <a name="versioning"></a>Sürüm oluşturma
Bkz: [Azure tanılama sürüm geçmişi](azure-diagnostics-versioning-history.md).

## <a name="next-steps"></a>Sonraki adımlar
Hangi hizmet toocollect tanılama çalıştığınız seçin ve çalışmaya makaleleri tooget aşağıdaki hello kullanın. Belirli görevleri başvurusu için Hello genel Azure tanılama bağlantıları kullanın.

## <a name="web-apps"></a>Web Apps
Web uygulamaları Azure tanılama kullanmayın unutmayın. Merhaba eşdeğer bilgilerini bulmak [Web uygulamaları](../app-service-web/web-sites-enable-diagnostic-log.md)

## <a name="cloud-services-using-azure-diagnostics"></a>Azure Tanılama'yı kullanarak bulut Hizmetleri
* Visual Studio kullanıyorsanız, bkz: [Visual Studio'yu kullanın tootrace bir bulut Hizmetleri uygulaması](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget başlatıldı. Aksi takdirde bkz:
* [Azure Tanılama'yı kullanarak nasıl toomonitor bulut Hizmetleri](../cloud-services/cloud-services-how-to-monitor.md)
* [Bulut Hizmetleri uygulamada Azure tanılama ayarlama](../cloud-services/cloud-services-dotnet-diagnostics.md)

Daha gelişmiş konular için bkz:

* [Bulut Hizmetleri için Application Insights'a Azure tanılama kullanma](../application-insights/app-insights-cloudservices.md)
* [Bulut Hizmetleri uygulaması Azure Tanılama ile Merhaba akışını izleme](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)
* [Bulut Hizmetleri PowerShell tooset tanılama yukarı kullanın](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="virtual-machines-using-azure-diagnostics"></a>Azure tanılama kullanarak sanal makineler
* Visual Studio kullanıyorsanız, bkz: [Visual Studio'yu kullanın tootrace Azure sanal makineleri](../vs-azure-tools-debug-cloud-services-virtual-machines.md) tooget başlatıldı. Aksi takdirde bkz:
* [Azure tanılama üzerinde bir Azure sanal makine ayarlama](../virtual-machines-dotnet-diagnostics.md)

Daha gelişmiş konular için bkz:

* [Azure sanal makinelerde tanılama yukarı PowerShell tooset kullanın](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [İzleme ve tanılama Azure Resource Manager şablonu kullanarak bir Windows sanal makine oluşturma](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="service-fabric-using-azure-diagnostics"></a>Service Fabric Azure Tanılama'yı kullanarak
Konumundaki başlamak [Service Fabric uygulaması izleme](../service-fabric/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Diğer birçok Service Fabric tanılama makale hello Gezinti ağacında toothis makale aldıktan sonra sol hello üzerinde kullanılabilir.

## <a name="general-azure-diagnostics-articles"></a>Genel Azure tanılama makaleleri
* [Azure tanılama şema yapılandırma](https://msdn.microsoft.com/library/azure/mt634524.aspx) – nasıl toochange hello şema dosyası toocollect öğrenin ve rota Tanılama verileri. Visual Studio toochange hello şema dosyasını da kullanabileceğinizi unutmayın.
* [Azure Tanılama verileri Azure depolama alanında nasıl depolandığını](../cloud-services/cloud-services-dotnet-diagnostics-storage.md) -hello tabloları ve blobları hello tanılama veri yazıldığı hello adlarını bilme.
* Çok öğrenin[performans sayaçları Azure Tanılama'kullanma](../cloud-services/cloud-services-dotnet-diagnostics-performance-counters.md).
* Çok öğrenin[rota Azure tanılama bilgileri tooApplication Öngörüler](azure-diagnostics-configure-application-insights.md)
* Tanılama başlatılıyor ile sorun varsa veya verileriniz Azure Storage tablolarda bkz [Azure tanılama sorunlarını giderme](azure-diagnostics-troubleshooting.md)
