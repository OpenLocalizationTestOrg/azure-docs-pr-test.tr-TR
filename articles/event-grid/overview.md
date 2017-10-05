---
title: "Azure olay kılavuz genel bakış"
description: "Azure olay kılavuz ve onun kavramlarını açıklar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/18/2017
ms.author: babanisa
ms.openlocfilehash: 59a834f32793e349d5639baf3c80dbcba274dfa8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="an-introduction-to-azure-event-grid"></a>Azure olay kılavuzuna giriş

Azure olay kılavuz, olay tabanlı mimari ile uygulamaları kolayca oluşturmanıza olanak sağlar. Abone olma ve olay işleyicisi veya olayı göndermek için Web kancası uç noktası vermek istediğiniz Azure kaynağı seçin. Olay kılavuz depolama BLOB'ları ve kaynak grupları gibi Azure hizmetlerinden gelen olaylar için yerleşik desteğe sahiptir. Olay kılavuz özel konular ve özel Web kancalarını kullanarak uygulama ve üçüncü taraf olayları özel desteği de vardır. 

Belirli olayları farklı uç noktalar, birden çok uç nokta için çok noktaya yayın yönlendirmek ve olaylarınızı güvenilir bir şekilde teslim emin olmak için filtreleri kullanabilirsiniz. Olay kılavuz, ayrıca özel ve üçüncü taraf olayları için destek oluşturdu.

Önizleme sürümü için Event Grid tarafından **westus2** ve **westcentralus** konumları desteklenir. Diğer bölgeler eklenir.

Bu makalede Azure olay kılavuz genel bir bakış sağlar. Olay kılavuzla başlamak istiyorsanız, bkz: [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).

![Olay kılavuz işlevsel modeli](./media/overview/event-grid-functional-model.png)

Şu anda, Blob Storage bir yayımcı olarak genel kullanıma açık değil.

## <a name="concepts"></a>Kavramlar

Azure olay kılavuzunda yapmalarını sağlayan beş kavram vardır:

* **Olayları** -ne oldu.
* **Olay kaynakları/yayımcıları** - burada olay gerçekleşen.
* **Konular** -burada yayımcıları olayları göndereceği.
* **Olay abonelikleri** -rota olayları, bazen birden çok işleyici için uç nokta veya yerleşik mekanizması. Abonelikleri akıllıca gelen olayları filtrelemek için işleyiciler tarafından da kullanılır.
* **Olay işleyicileri** -uygulama veya hizmet olaya tepki verme.

Bu kavramlar hakkında daha fazla bilgi için bkz: [Azure olay kılavuzunda kavramları](concepts.md).

## <a name="capabilities"></a>Özellikler

Azure olay kılavuz önemli özelliklerinden bazıları şunlardır:

* **Basitlik** -Point'ye tıklayın, Azure kaynak olaylarından herhangi bir olay işleyicisi veya uç nokta hedeflenir.
* **Filtreleme Gelişmiş** -filtre olay türü veya olay olay işleyicileri yalnızca ilgili olayları aldığınızdan emin olmak için yol yayımlayın.
* **Yayma** -birden çok uç nokta gerektiğinde sayıda basamağa olay kopyalarını göndermesini aynı olaya abone olun.
* **Güvenilirlik** -olayları teslim edilir emin olmak için üstel geri alma 24 saatlik Denemeyle kullanma.
* **Olay başına ödeme** - ödeme tutarını yalnızca olay kılavuzunu kullanın.
* **Yüksek verimlilik** -yapı yüksek hacimli iş yükleri üzerinde olay kılavuz saniye başına milyonlarca olayı desteği.
* **Yerleşik olayları** - hale getirmek ve hızlı bir şekilde kaynak tanımlanan yerleşik olaylar ile çalışıyor.
* **Özel olaylar** -olay kılavuz rota, filtre ve güvenilir bir şekilde teslim özel olaylar uygulamanızda kullanın.

## <a name="built-in-publisher-and-handler-integration"></a>Yerleşik yayımcı ve işleyici ile tümleştirme

Azure Yayımcılar ve işleyicileri dahil olmak üzere çok sayıda hizmetlerini kullanarak yerleşik olay destek sunar.

### <a name="publishers"></a>Yayımcılar

Şu anda aşağıdaki Azure hizmetlerini olay kılavuz için yerleşik yayımcı desteğine sahiptir:

* Kaynak grupları (yönetim işlemlerini)
* Azure abonelikleri (yönetim işlemlerini)
* Event Hubs
* Özel konular

Diğer Azure hizmetleriyle bu yıl eklenir.

### <a name="handlers"></a>İşleyicileri

Şu anda aşağıdaki Azure hizmetlerini olay kılavuz yerleşik işleyici desteği vardır: 

* Azure İşlevleri
* Logic Apps
* Azure Otomasyonu
* Web kancaları

Diğer Azure hizmetleriyle bu yıl eklenir.

## <a name="what-can-i-do-with-event-grid"></a>Olay kılavuzla ne yapabilirim?

Azure olay kılavuz birkaç çok sunucusuz artırmak özellikleri, ops otomasyon ve tümleştirme çalışma sağlar: 

### <a name="serverless-application-architectures"></a>Sunucusuz uygulama mimarileri

![Sunucusuz bir uygulama](./media/overview/serverless_web_app.png)

Event Grid, veri kaynaklarını ve olay işleyicilerini bağlar. Event Grid’i örneğin bir blob depolama kapsayıcısına eklenen her yeni fotoğrafta görüntü analizini çalıştıracak sunucusuz bir işlev tetiklemek için kullanabilirsiniz. 

### <a name="ops-automation"></a>OPS Otomasyon

![Ops otomasyonu](./media/overview/Ops_automation.png)

Event Grid, otomasyonu hızlandırmanızı ve ilke uygulamayı basitleştirmenizi sağlar. Örneğin Event Grid, sanal makine oluşturulduğunda veya SQL Veritabanı hazırlandığında Azure Otomasyonu’na bilgi verebilir. Bu olaylar hizmet yapılandırmalarının uyumlu olup olmadığını otomatik olarak denetlemek, operasyon araçlarına meta verileri eklemek, sanal makineleri etiketlemek ve iş öğelerini dosyalamak için kullanılabilir.

### <a name="application-integration"></a>Uygulama tümleştirme

![Uygulama tümleştirme](./media/overview/app_integration.png)

Event Grid, uygulamanızı diğer hizmetlerle bağlar. Örneğin, olay kılavuza uygulamanızın olay verileri göndermek ve yönlendirme, Gelişmiş, güvenilir teslim yararlanmak için özel bir konu oluşturun ve Azure ile tümleştirme doğrudan. Ayrıca Event Grid’i Logic Apps ile birlikte kullanarak kod yazmadan her yerden veri işleyebilirsiniz. 

## <a name="how-is-event-grid-different-from-other-azure-integration-services"></a>Olay kılavuz Azure tümleştirme hizmetlerinden farklı mı?

Olay kılavuz olay denetimli, geriye dönük programlama sağlayan bir olay devre kartı ' dir. Azure Hizmetleri ile son derece tümleşiktir ve üçüncü taraf hizmetleri ile tümleştirilebilir. Olay iletisi hizmetler ve uygulamalar değişikliklere tepki vermek için gereken bilgileri içerir. Olay kılavuz veri ardışık değil ve güncelleştirildi gerçek nesne dağıtmaz.

Hizmet veri yolu işlemleri, sıralama, yinelenen algılama ve anlık tutarlılığı gerektiren geleneksel kurumsal uygulamalar için uygundur. Olay kılavuz hızı, Ölçek, tekliflerden için tasarlanmış ve düşük maliyetli bir reaktif modeldeki ' dir. Bunu sunucusuz mimarisi için uygundur.

Olay kılavuz Logic Apps ve Event Hubs gibi diğer Azure hizmetleriyle tamamlar. Olay kılavuz kendi iş akışını başlatmak için mantıksal uygulama tetikler. Olay hub'ları, hub olayı yakalamak olaylarına tepki vermek ve veri giriş ve dönüşüm işlem hatlarını oluşturmak etkinleştirerek olay kılavuzla çalışır.

## <a name="how-much-does-event-grid-cost"></a>Nasıl olay kılavuz maliyeti nedir?

Azure olay kılavuz bir olay başına ödeme fiyatlandırma modelini kullanır, bu nedenle, yalnızca, kullanım için ücret ödersiniz.

0.60 milyon işlemleri ($0.30 Önizleme sırasında) başına olay kılavuz maliyetleri ve ilk 100.000 işlemi her ay ücretsiz. İşlem eşleştirme, teslim girişimi ve yönetim çağrıları Gelişmiş olay giriş tanımlanır.  Daha fazla ayrıntı bulunabilir [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/event-grid/).

## <a name="next-steps"></a>Sonraki adımlar

* [Oluşturma ve özel olaylarına abone olma](custom-event-quickstart.md) atlama sağ taraf ve özel olaylarınızı Azure olay kılavuz hızlı başlangıç kullanarak herhangi bir uç nokta için göndermeye başlayın.
* [Logic Apps olay işleyici kullanarak](monitor-virtual-machine-changes-event-grid-logic-app.md) olaylarına tepki vermek için Logic Apps kullanarak bir uygulama oluşturmaya üzerinde bir öğretici olay kılavuz tarafından gönderilir.
* [Olay kılavuz REST API Başvurusu](/rest/api/eventgrid)  
  Olay Aboneliklerini yönetmek için Azure olay kılavuz ve başvurusu hakkında daha fazla teknik bilgi sağlayan Yönlendirme ve filtreleme.