---
title: "aaaAzure olay kılavuz genel bakış"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 95dce22e9335df88e81b134143a6c14994c26b8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-event-grid"></a>Bir giriş tooAzure olay kılavuz

Azure olay kılavuz tooeasily yapı uygulamalarla olay tabanlı mimari sağlar. Hello için toosubscribe gibi ve hello olay işleyicisi veya Web kancası uç nokta toosend hello olaya vermeniz Azure kaynak seçin. Olay kılavuz depolama BLOB'ları ve kaynak grupları gibi Azure hizmetlerinden gelen olaylar için yerleşik desteğe sahiptir. Olay kılavuz özel konular ve özel Web kancalarını kullanarak uygulama ve üçüncü taraf olayları özel desteği de vardır. 

Filtreler tooroute belirli olayları toodifferent uç noktaları, çok noktaya yayın toomultiple uç noktaları kullanın ve olaylarınızı güvenilir bir şekilde teslim emin olun. Olay kılavuz, ayrıca özel ve üçüncü taraf olayları için destek oluşturdu.

Merhaba Önizleme sürümü için olay kılavuz destekleyen **westus2** ve **westcentralus** konumları. Diğer bölgeler eklenir.

Bu makalede Azure olay kılavuz genel bir bakış sağlar. Olay Kılavuzu ile çalışmaya tooget istiyorsanız, bkz: [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).

![Olay kılavuz işlevsel modeli](./media/overview/event-grid-functional-model.png)

Şu anda, Blob Storage bir yayımcı olarak genel kullanıma açık değil.

## <a name="concepts"></a>Kavramlar

Azure olay kılavuzunda yapmalarını sağlayan beş kavram vardır:

* **Olayları** -ne oldu.
* **Olay kaynakları/yayımcıları** - hello olay gerçekleşen burada.
* **Konular** -burada yayımcıları olayları göndermek endpoint hello.
* **Olay abonelikleri** -hello uç noktası veya yerleşik mekanizması tooroute olaylar, bazen toomultiple işleyicileri. Abonelikleri işleyicileri toointelligently filtre gelen olaylar tarafından da kullanılır.
* **Olay işleyicileri** - hello uygulama veya hizmet tanımlandığında toohello olay.

Bu kavramlar hakkında daha fazla bilgi için bkz: [Azure olay kılavuzunda kavramları](concepts.md).

## <a name="capabilities"></a>Özellikler

Azure olay kılavuz hello önemli özelliklerinden bazıları şunlardır:

* **Basitlik** -Azure kaynak tooany olay işleyicisi veya uç noktasına tooaim olayları.
* **Filtreleme Gelişmiş** -filtre olay türü veya olay yayımlama yolu tooensure olay işleyicileri yalnızca ilgili olayları alma.
* **Yayma** -birden çok uç noktaları toohello abone aynı olay toosend gerektiğinde bu hello olay tooas birçok yerde kopyalar.
* **Güvenilirlik** -olayları teslim edilir üstel geri alma tooensure 24 saatlik Denemeyle kullanma.
* **Olay başına ödeme** - ödeme yalnızca hello tutarı için olay kılavuzunu kullanın.
* **Yüksek verimlilik** -yapı yüksek hacimli iş yükleri üzerinde olay kılavuz saniye başına milyonlarca olayı desteği.
* **Yerleşik olayları** - hale getirmek ve hızlı bir şekilde kaynak tanımlanan yerleşik olaylar ile çalışıyor.
* **Özel olaylar** -olay kılavuz rota, filtre ve güvenilir bir şekilde teslim özel olaylar uygulamanızda kullanın.

## <a name="built-in-publisher-and-handler-integration"></a>Yerleşik yayımcı ve işleyici ile tümleştirme

Azure Yayımcılar ve işleyicileri dahil olmak üzere çok sayıda hizmetlerini kullanarak yerleşik olay destek sunar.

### <a name="publishers"></a>Yayımcılar

Şu anda hello aşağıdaki Azure hizmetlerinin yerleşik yayımcı için destek olay kılavuz vardır:

* Kaynak grupları (yönetim işlemlerini)
* Azure abonelikleri (yönetim işlemlerini)
* Event Hubs
* Özel konular

Diğer Azure hizmetleriyle bu yıl eklenir.

### <a name="handlers"></a>İşleyicileri

Şu anda hello aşağıdaki Azure hizmetlerinin yerleşik işleyicisi için destek olay kılavuz vardır: 

* Azure İşlevleri
* Logic Apps
* Azure Otomasyonu
* Web kancaları

Diğer Azure hizmetleriyle bu yıl eklenir.

## <a name="what-can-i-do-with-event-grid"></a>Olay kılavuzla ne yapabilirim?

Azure olay kılavuz birkaç çok sunucusuz artırmak özellikleri, ops otomasyon ve tümleştirme çalışma sağlar: 

### <a name="serverless-application-architectures"></a>Sunucusuz uygulama mimarileri

![Sunucusuz bir uygulama](./media/overview/serverless_web_app.png)

Event Grid, veri kaynaklarını ve olay işleyicilerini bağlar. Örneğin, olay kılavuz tooinstantly tetikleyici her zaman yeni bir fotoğraf tooa blob depolama kapsayıcısını eklenen sunucusuz işlevi toorun görüntü analiz kullanın. 

### <a name="ops-automation"></a>OPS Otomasyon

![Ops otomasyonu](./media/overview/Ops_automation.png)

Olay kılavuz toospeed Otomasyon sağlar ve ilke zorlama basitleştirin. Örneğin Event Grid, sanal makine oluşturulduğunda veya SQL Veritabanı hazırlandığında Azure Otomasyonu’na bilgi verebilir. Bu olaylar kullanılabilir tooautomatically meta veri işlemleri araçları, etiket sanal makineler ya da dosya iş öğeleri yerleştirin, hizmet yapılandırması uyumlu olduğunu denetleyin.

### <a name="application-integration"></a>Uygulama tümleştirme

![Uygulama tümleştirme](./media/overview/app_integration.png)

Event Grid, uygulamanızı diğer hizmetlerle bağlar. Örneğin, uygulamanızın olay verileri tooEvent kılavuz, bir özel konu toosend oluşturun ve yönlendirme, Gelişmiş, güvenilir teslim yararlanmak ve Azure ile tümleştirme doğrudan. Alternatif olarak, kod yazmadan herhangi bir yere, Logic Apps tooprocess verilerle olay kılavuzunu kullanabilirsiniz. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Olay kılavuz Azure tümleştirme hizmetlerinden farklı mı?

Olay kılavuz olay denetimli, geriye dönük programlama sağlayan bir olay devre kartı ' dir. Azure Hizmetleri ile son derece tümleşiktir ve üçüncü taraf hizmetleri ile tümleştirilebilir. Merhaba olay iletisi tooreact toochanges Hizmetleri ve uygulamaları gereksinim hello bilgileri içerir. Olay kılavuz veri ardışık değil ve güncelleştirildi hello gerçek nesne dağıtmaz.

Hizmet veri yolu işlemleri, sıralama, yinelenen algılama ve anlık tutarlılığı gerektiren geleneksel kurumsal uygulamalar için uygundur. Olay kılavuz hızı, Ölçek, tekliflerden için tasarlanmış ve düşük maliyetli bir reaktif modeldeki ' dir. Uygun tooserverless mimarisidir.

Olay kılavuz Logic Apps ve Event Hubs gibi diğer Azure hizmetleriyle tamamlar. Olay kılavuz tetikleyicileri, iş akışı mantığı uygulama toobegin hello. Event Hubs olay hub'ları yakalamak ve yapı veri giriş ve dönüştürme ardışık tooreact tooevents etkinleştirerek olay kılavuz ile çalışır.

## <a name="how-much-does-event-grid-cost"></a>Nasıl olay kılavuz maliyeti nedir?

Azure olay kılavuz bir olay başına ödeme fiyatlandırma modelini kullanır, bu nedenle, yalnızca, kullanım için ücret ödersiniz.

0.60 milyon işlemleri ($0.30 Önizleme sırasında) başına olay kılavuz maliyetleri ve hello ayda ilk 100.000 işlemi boş. İşlem eşleştirme, teslim girişimi ve yönetim çağrıları Gelişmiş olay giriş tanımlanır.  Merhaba hakkında daha fazla ayrıntı bulunabilir [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Sonraki adımlar

* [Oluşturun ve toocustom olayları abone](custom-event-quickstart.md) atlama sağ ve hello Azure olay kılavuz quickstart kullanarak kendi özel olaylar tooany uç noktasını göndermeye başlayın.
* [Logic Apps olay işleyici kullanarak](monitor-virtual-machine-changes-event-grid-logic-app.md) Logic Apps tooreact tooevents kullanarak bir uygulama oluşturmaya üzerinde bir öğretici olay kılavuz tarafından gönderilir.
* [Olay kılavuz REST API Başvurusu](/rest/api/eventgrid)  
  Olay Aboneliklerini yönetmek için Azure olay kılavuz hello hakkında daha fazla teknik bilgi ve bir başvuru sağlar Yönlendirme ve filtreleme.
