---
title: "aaaAzure İzleyiciye Genel Bakış | Microsoft Docs"
description: "Azure İzleyici uyarıları, Web kancalarını, otomatik ölçeklendirme ve Otomasyon kullanımda istatistikleri toplar. Makale ayrıca diğer Microsoft izleme seçenekleri listeleyin."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Azure İzleyicisi'ne genel bakış
Bu makalede hello Azure Monitor Hizmeti Microsoft Azure genel bir bakış sağlar. Hangi Azure İzleyici yapar ve işaretçileri tooadditional ilgili bilgiler verilmektedir anlatılmaktadır toouse Azure İzleyicisi.  Bir tanıtım tercih ederseniz, bu makalenin hello altındaki sonraki adımları bağlantılara bakın. 

## <a name="why-monitor-your-application-or-system"></a>Neden uygulama veya sistem izleme
Bulut uygulamalarını birçok taşıma bölümleriyle karmaşıktır. İzleme, uygulamanızı kurma kalır veri tooensure ve sistem durumu iyi çalışan sağlar. Olası sorunlar kapalı veya olanları sorun giderme, toostave yardımcı olur. Ayrıca, uygulamanız hakkında izleme verileri toogain ayrıntılı Öngörüler kullanabilirsiniz. Bu bilgi tooimprove uygulama performansı veya bakım yardımcı veya aksi halde el ile müdahale gerektiren Eylemler otomatik hale getirme.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure İzleyicisi'ni ve Microsoft kullanıcının diğer izleme ürünleri
Azure İzleyicisi, çoğu Microsoft Azure hizmetlerini taban düzeyi altyapı ölçümleri ve günlükleri sağlar. Henüz verilerini Azure izleyicisine koymayın azure Hizmetleri var. Bunun yerine gelecekteki hello koyacaktır.

Microsoft, geliştiriciler, DevOps veya şirket içi yüklemeleri de BT Ops için ek izleme olanakları sağlayan ek ürün ve hizmetlerin birlikte gönderilir. Bir genel bakış ve bu farklı ürün ve hizmetlerin birlikte nasıl çalıştığını anlamak için bkz: [Microsoft Azure'da izleme](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>İşlem kaynakları - izleme

![İzleme ve tanılama işlem dışı kaynakları modeli](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

Merhaba işlem hizmetleri içerir 
- Cloud Services 
- Virtual Machines 
- Sanal makine ölçekleme kümeleri 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Uygulama - tanılama günlükleri, uygulama günlüklerini ve ölçümleri
Uygulamaları hello işlem modeli hello konuk işletim sistemi üzerinde çalıştırılabilir. Bunlar, kullanıcıların kendi günlüklerini ve ölçümleri kümesini yayma. Azure İzleyicisi Merhaba Azure tanılama uzantısını (Windows veya Linux) toocollect üzerinde çoğu uygulama düzeyindeki ölçümlerini ve günlükleri kullanır. Merhaba türler

* Performans sayaçları
* Uygulama günlükleri
* Windows olay günlükleri
* .NET olay kaynağı
* IIS günlükleri
* Temel ETW bildirimi
* Kilitlenme bilgi dökümleri
* Müşteri hata günlükleri

Merhaba tanılama uzantısını, yalnızca birkaç ölçümleri CPU kullanımı gibi kullanılabilir. 

### <a name="host-and-guest-vm-metrics"></a>Ana bilgisayar ve Konuk VM ölçümleri
Merhaba daha önce listelenen işlem kaynakları ayrılmış bir ana bilgisayar VM ve konuk işletim sistemi ile etkileşim vardır. Merhaba konak VM ve konuk işletim sistemi kök VM hello denk ve Konuk VM hello Hyper-V hiper yönetici modelinde kümesidir. Ölçümleri hem de toplayabilir. Ayrıca, hello konuk işletim sistemi tanılama günlüklerini toplayabilir.   

### <a name="activity-log"></a>Etkinlik Günlüğü
Hello Azure altyapısı tarafından görülen, kaynak hakkında bilgi için hello etkinlik günlüğü (daha önce işlemsel veya denetim günlüklerini denir) arayabilirsiniz. Merhaba günlük kez kaynakları zaman oluşturulan veya yok gibi bilgileri içerir.  Daha fazla bilgi için bkz: [etkinlik günlüğü'ne genel bakış](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>İzleme kaynakları - şey

![İzleme ve tanılama işlem kaynakları için modeli](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Kaynak - ölçümleri ve tanılama günlükleri
Toplanabilir ölçümleri ve tanılama günlüklerini hello kaynak türüne göre farklılık gösterir. Örneğin, Web uygulamaları hello Disk GÇ ve yüzde CPU istatistikler sağlar. Bu ölçümleri yerine kuyruk boyutu ve ileti işleme gibi ölçümleri sağlar Service Bus kuyruğuna için mevcut değil. Her kaynak için toplanabilir ölçümleri listesi kullanılabilir [ölçümleri desteklenen](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Ana bilgisayar ve Konuk VM ölçümleri
Olmadığından değil mutlaka kaynağınız ve belirli ana bilgisayar veya konuk VM 1:1 eşlemesini ölçümleri kullanılabilir değil.

### <a name="activity-log"></a>Etkinlik Günlüğü
Merhaba etkinlik günlüğü olduğu hello aynı işlem kaynakları.  

## <a name="uses-for-monitoring-data"></a>Veri izleme kullanır
Veri toplama sonra yapabilirsiniz ile Azure İzleyicisi'nde aşağıdaki hello

### <a name="route"></a>Yol
Gerçek zamanlı izleme verileri tooother konumlarda akışını sağlayabilirsiniz.

Örneklere şunlar dahildir:

- Daha zengin Görselleştirme ve çözümleme araçları kullanabilmeniz için tooApplication Öngörüler gönderin.
- Toothird taraf Araçlar yönlendirmek için tooEvent hub gönderin. 

### <a name="store-and-archive"></a>Depolama ve Arşiv
Bazı izleme verilerini bir kümesi süre boyunca depolanan ve Azure İzleyicisi'nde kullanılabilir zaten var. 
- Ölçümleri 30 gün süreyle depolanır. 
- Etkinlik günlüğü girişleri 90 gün süreyle depolanır. 
- Tanılama günlüklerini hiç depolanmaz. 

Yukarıda listelenen dönemleri toostore verilerin hello uzun istiyorsanız, Azure depolamayı kullanabilirsiniz. İzleme verilerini ayarladığınız bir bekletme ilkesi temel alınarak, depolama hesabı tutulur. Azure depolama alanında veri işgal hello alanı hello toopay sahip. 

Birkaç yolu toouse bu veriler:

- Yazıldıktan sonra onu okuyun ve işleme diğer araçları içinde veya Azure dışında olabilir.
- Uzun süre için bekletme ilkenizde hello bulut tookeep veri değiştirmek veya hello verilerini yerel olarak yerel bir arşiv indirilir.  
- Arşiv amacıyla süresiz olarak Azure depolama alanında hello veri bırakın. 

### <a name="query"></a>Sorgu
Hello Azure İzleyici REST API'si, platformlar arası komut satırı arabirimi (CLI) komutları, PowerShell cmdlet'lerini kullanabilirsiniz ya da hello sistem veya Azure storage veri hello .NET SDK'sı tooaccess hello

Örneklere şunlar dahildir:

* Yazdığınız özel bir izleme uygulama için veri alma
* Özel sorgular oluşturma ve bu verileri tooa üçüncü taraf uygulaması gönderme.

### <a name="visualize"></a>Görselleştirme
Grafikleri izleme verilerinizi görselleştirme eğilimleri hello verilerine kendisini arayan hızlıdır bulmanıza yardımcı olur.  

Birkaç görselleştirme yöntemler şunlardır:

* Hello Azure portalını kullanın
* Rota veri tooAzure Application Insights
* Rota veri tooMicrosoft Powerbı
* Rota hello veri tooa üçüncü taraf görselleştirme aracını kullanarak ya da canlı akış veya sağlayarak hello aracı Azure depolama alanında bir arşiv okuma


### <a name="automate"></a>Otomatikleştirme
İzleme veri tootrigger uyarıları kullanın veya hatta tüm işlemler. Örneklere şunlar dahildir:

* Veri tooautoscale işlem örneklerini uygulama yüküne göre yukarı veya aşağı kullanın.
* Ölçüm önceden belirlenmiş bir eşik kestiği olduğunda e-postalar gönderin.
* Web URL (Web kancası) tooexecute Azure dışında bir sistemde bir eylem çağrısı
* Bir runbook'un Azure Otomasyon tooperform herhangi çeşitli görevleri Başlat

## <a name="methods-of-accessing-azure-monitor"></a>Azure İzleyicisi'ne erişim yöntemleri
Genel olarak, veri izleme, Yönlendirme ve alma yöntemleri aşağıdaki hello birini kullanarak yönetebilirsiniz. Tüm yöntemler, tüm eylemler veya veri türleri için kullanılabilir.

* [Azure portal](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Platformlar arası komut satırı arabirimi (CLI)](insights-cli-samples.md)
* [REST API](https://docs.microsoft.com/rest/api/monitor/)
* [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinin
- Videosu yalnızca Azure İzleyicisi'ni şu adresten edinilebilir  
[Azure İzleyicisi ile çalışmaya başlama](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Burada kullanabileceğiniz Azure monitör bir senaryoda açıklayan ek bir video için bkz. [Microsoft Azure keşfedin izleme ve tanılama](https://channel9.msdn.com/events/Ignite/2016/BRK2234) ve [Ignite 2016'den video Azure izleyicisinde](https://myignite.microsoft.com/videos/4977)
- Hello Azure İzleyicisi arabirimi aracılığıyla çalıştırmak [Azure İzleyicisi ile çalışmaya başlama](monitoring-get-started.md)
- Merhaba ayarlamak [Azure tanılama uzantıları](../azure-diagnostics.md) sanal makine, bulut hizmetinde toodiagnose sorunları çalışıyorsanız sanal makine ölçekleme kümeleri veya Service Fabric uygulaması.
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) App Service Web uygulamanızda toodiagnostic sorunları çalışıyorsanız.
- [Azure Storage sorunlarını giderme](../storage/common/storage-e2e-troubleshooting.md) depolama BLOB'ları, tabloların veya kuyrukların kullanırken
- [Günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics/) ve hello [Operations Management Suite](https://www.microsoft.com/oms/)
