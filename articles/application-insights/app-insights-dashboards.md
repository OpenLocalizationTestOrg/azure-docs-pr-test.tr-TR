---
title: Azure Application Insights hello gezintisi ve aaaDashboards | Microsoft Docs
description: "Anahtar APM grafikler ve sorguları görünümleri oluşturun."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Gezinti ve panolar hello Application Insights portalında
Sonra [projenizde Application Insights'ı ayarlamak](app-insights-overview.md), uygulamanızın performansı ve kullanımı hakkında telemetri verileri hello projenizin Application Insights kaynağını görünür [Azure portal](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Telemetrinizi Bul
İçinde toohello oturum [Azure portal](https://portal.azure.com) ve uygulamanız için oluşturduğunuz toohello Application Insights kaynağı gidin.

![Gözat'ı tıklatın, Application Insights ve ardından uygulamanızı seçin.](./media/app-insights-dashboards/00-start.png)

Uygulamanız için Hello genel bakış dikey penceresinde (sayfa) hello anahtar tanılama ölçümleri, uygulamanızın özetini gösterir ve bir ağ geçidi toohello hello Portalı'nın diğer özellikleri.

![Yollar tooview telemetrinizi büyük](./media/app-insights-dashboards/010-oview.png)

Tüm hello grafikleri ve kılavuzları özelleştirebilir ve tooa Pano sabitleyin. Bu şekilde, merkezi bir Panoda farklı uygulamalardan birlikte hello anahtar telemetri getirebilirsiniz.

## <a name="dashboards"></a>Panolar
içinde toohello oturumu sonra hello ilk şey gördüğünüz [Microsoft Azure portal](https://portal.azure.com) bir Pano. Burada birlikte telemetrisinden dahil olmak üzere tüm Azure kaynaklarınızı, üzerinden en önemli tooyou olan hello grafikleri getirebileceğinizden [Azure Application Insights](app-insights-overview.md).

![Özelleştirilmiş bir Pano.](./media/app-insights-dashboards/31.png)

1. **Toospecific kaynaklara gitme** uygulamanıza Application Insights gibi: kullanım hello sol çubuğu.
2. **Dönüş toohello geçerli Pano**, veya geçiş tooother son görünümleri: sol üst kullanım hello açılır menü.
3. **Geçiş panolar**: hello Pano başlık kullanım hello aşağı açılan menüsünde
4. **Oluşturma, düzenleme ve panoları paylaşmak** hello Pano araç.
5. **Merhaba Pano düzenleme**: kutucuğunun üzerine gelerek ve kendi üst kullan toomove, çubuk özelleştirebilir ya da kaldırın.

## <a name="add-tooa-dashboard"></a>Tooa Pano Ekle
Bir dikey veya özellikle ilginç grafikler kümesi bakarken toohello panonun bir kopyasını sabitleyebilirsiniz. Sonraki sefer var. dönmek görürsünüz.

![bir grafik toopin üzerine gelin ve ardından hello üstbilgisindeki "...".](./media/app-insights-dashboards/33.png)

1. Grafik toodashboard sabitleyin. Merhaba grafik bir kopyasını hello panosunda görüntülenir.
2. PIN hello tüm dikey toohello Pano - aracılığıyla tıklayabilirsiniz bir kutucuk olarak hello panosunda görünür.
3. Merhaba sol üst köşesinde tooreturn toohello geçerli panodan'ı tıklatın. Daha sonra hello açılır menü tooreturn toohello geçerli görünümü kullanabilirsiniz.

Grafikleri döşeme gruplandırılır dikkat edin: bir kutucuk birden fazla grafik içerebilir. Merhaba tüm döşeme toohello Pano sabitleyin.

Merhaba grafik hello grafiğin zaman aralığı bağımlı sıklık otomatik olarak yenilenir:

* Zaman aralığı too1 saat oluşturmak: her 5 dakikada bir Yenile
* Aralık 1-24 saat saat: 15 dakikada bir Yenile
* Zaman aralığı 24 saat yukarıda: (zaman aralığı) / 60.

### <a name="pin-any-query-in-analytics"></a>Herhangi bir sorgu analizleri sabitleyin
Ayrıca [Analytics PIN](app-insights-analytics-using.md#pin-to-dashboard) grafikleri tooa [paylaşılan](#share-dashboards-with-your-team) Pano. Bu, herhangi bir rastgele sorgu hello standart ölçümleri yanında tooadd grafiklerini sağlar. 

Sonuçları her saat otomatik olarak hesaplanır. Hemen hello grafik toorecalculate Hello Yenile simgesine tıklayın. (Tarayıcı Yenile hesaplamaz.)

## <a name="adjust-a-tile-on-hello-dashboard"></a>Başlangıç Panosu kutucuk Ayarla
Merhaba Panoda bir kutucuğu olduktan sonra ayarlayabilirsiniz.

![Üzerine gelerek sipariş tooedit grafik üzerinden bu.](./media/app-insights-dashboards/36.png)

1. Bir grafik toohello kutucuğu ekleyin.
2. Merhaba ölçüm, grup tarafından boyut ve grafiğinin stilini (tablo, grafik) ayarlayın.
3. Merhaba diyagramı toozoom sürükleyin; Merhaba geri düğmesini tooreset hello timespan tıklayın; Merhaba döşeme hello grafiklerde filtre özelliklerini ayarlayın.
4. Kutucuk başlığı ayarlayın.

Ölçüm Gezgini dikey penceresinden Sabitlenen kutucuklar bir genel bakış dikey penceresinden Sabitlenen kutucuklar'den daha fazla düzenleme seçeneğiniz vardır.

Sabitlenmiş hello özgün döşeme düzenlemeleriniz tarafından etkilenmez.

## <a name="switch-between-dashboards"></a>Panolar arasında geçiş
Birden fazla panoyu kaydedin ve bunlar arasında geçiş yapabilirsiniz. Bir grafik veya dikey pencere sabitlemek bunlar toohello geçerli Pano eklenmesi.

![Panolar arasında tooswitch Pano tıklatın ve kaydedilmiş bir Pano seçin. toocreate ve yeni bir Pano kaydetmek için yeni'yi tıklatın. toorearrange, Düzenle'yi tıklatın.](./media/app-insights-dashboards/32.png)

Örneğin, hello takım odası ve genel geliştirme için başka bir tam ekran görüntüleme için tek bir Panoda olabilir.

Merhaba Panoda bir kutucuk bir dikey pencere görünür: toogo toohello dikey tıklayın. Bir grafik özgün konumuna hello grafikte çoğaltır.

![Temsil ettiği bir kutucuğu tooopen hello dikey tıklayın](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Panoları paylaşmak
Bir Pano oluşturduğunuz zaman, diğer kullanıcılarla paylaşabilirsiniz.

![Merhaba Pano üstbilgisinde Paylaş'ı tıklatın.](./media/app-insights-dashboards/41.png)

Hakkında bilgi edinin [rolleri ve erişim denetimi](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>Uygulama gezinme
Hello genel bakış dikey penceresinde hello ağ geçidi toomore uygulamanız hakkındaki bilgilerdir.

* **Herhangi bir grafik veya döşeme** - herhangi bir kutucuğu tıklayın veya toosee ne görüntüler hakkında daha fazla ayrıntı grafik.

### <a name="overview-blade-buttons"></a>Genel Bakış dikey düğmeleri
![Genel Bakış dikey üst gezinti çubuğu](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Ölçüm Gezgini** ](app-insights-metrics-explorer.md) -performans ve kullanım kendi grafikleri oluşturun.
* [**Arama** ](app-insights-diagnostic-search.md) - olayları istekleri, özel durumlar gibi belirli örneklerini araştırmak veya oturum izlemeleri.
* [**Analytics** ](app-insights-analytics.md) -telemetrinizi üzerinden güçlü sorgular.
* **Zaman aralığı** -hello dikey penceresinde tüm hello grafikler tarafından görüntülenen hello aralığını ayarlayın.
* **Silme** -bu uygulama için hello Application Insights kaynağı silme. Ayrıca uygulama kodunuzdan hello Application Insights paketlerini kaldırın, veya hello Düzenle [izleme anahtarını](app-insights-create-new-resource.md#copy-the-instrumentation-key) uygulama toodirect telemetri tooa farklı Application Insights kaynağınıza içinde.

### <a name="essentials-tab"></a>Essentials sekmesi
* [İzleme anahtarını](app-insights-create-new-resource.md#copy-the-instrumentation-key) -bu uygulama kaynak tanımlar.
* Fiyatlandırma - özellikler kullanılabilir ve ayarlanmış birim caps olun.

### <a name="app-navigation-bar"></a>Uygulama gezinti çubuğu
![Sol gezinti çubuğu](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Genel Bakış** -dönüş toohello uygulamaya genel bakış dikey.
* **Etkinlik günlüğü** -uyarı ve Azure yönetim olayları.
* [**Erişim denetimi** ](app-insights-resources-roles-access-control.md) -erişim tooteam üyeleri ve diğerleri sağlayın.
* [**Etiketler** ](../azure-resource-manager/resource-group-using-tags.md) -kullanım uygulamanızı başkalarıyla toogroup etiketler.

ARAŞTIR

* [**Uygulama eşlemesi** ](app-insights-app-map.md) -hello bileşenleri, uygulamanızın gösteren etkin eşleme türetilmiş hello bağımlılık bilgileri.
* [**Akıllı algılama** ](app-insights-proactive-diagnostics.md) -son performans uyarıları gözden geçirin.
* [**Canlı akış** ](app-insights-live-stream.md) - sabit neredeyse anında ölçümler, yeni bir yapı dağıtırken yararlı kümesi veya hata ayıklama A.
* [**Kullanılabilirlik / Web testleri** ](app-insights-monitor-web-app-availability.md) -gönderme normal istekleri tooyour web uygulamasından hello world.* geçici
* [**Hataları, performans** ](app-insights-web-monitor-performance.md) -özel durumları, hata oranları ve yanıt süreleri uygulamanız gelen istekleri ve istekleri tooyour uygulama için çok[bağımlılıkları](app-insights-asp-net-dependencies.md).
* [**Performans** ](app-insights-web-monitor-performance.md) -yanıt süresi, bağımlılık yanıt sürelerini.
* [Sunucuları](app-insights-web-monitor-performance.md) -performans sayaçları. Kullanılabilir ise, [Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md).
* **Tarayıcı** -sayfa görünümü ve AJAX performans. Kullanılabilir ise, [web sayfalarınıza izleme](app-insights-javascript.md).
* **Kullanım** -sayfa görünümü, kullanıcı ve oturum sayısını. Kullanılabilir ise, [web sayfalarınıza izleme](app-insights-javascript.md).

YAPILANDIRMA

* **Başlarken** -satır içi öğretici.
* **Özellikler** -izleme anahtarı, abonelik ve kaynak kimliği.
* [Uyarıları](app-insights-alerts.md) -ölçüm uyarı yapılandırma.
* [Sürekli verme](app-insights-export-telemetry.md) -telemetri tooAzure depolama verilmesini yapılandırın.
* [Performans testi](app-insights-monitor-web-app-availability.md#performance-tests) -Web sitenizde yapay yük ayarlayın.
* [Kota ve fiyatlarını](app-insights-pricing.md) ve [alım örnekleme](app-insights-sampling.md).
* **API erişimini** -oluşturmak [yayın ek açıklamaları](app-insights-annotations.md) ve hello veri erişim API için.
* [**İş öğeleri** ](app-insights-diagnostic-search.md#create-work-item) -tooa iş telemetri incelenirken hatalar oluşturabilmesi için sistem izleme bağlanın.

AYARLAR

* [**Kilitler** ](../azure-resource-manager/resource-group-lock-resources.md) -Azure kaynaklarını Kilitle
* [**Otomasyon betiğini** ](app-insights-powershell.md) -hello Azure kaynak tanımını dışa şablonu bir toocreate yeni kaynağı olarak kullanın.


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Sonraki adımlar

|  |  |
| --- | --- |
| [Ölçüm Gezgini](app-insights-metrics-explorer.md)<br/>Filtre ve segment ölçümleri |![Arama örneği](./media/app-insights-dashboards/64.png) |
| [Tanılama arama](app-insights-diagnostic-search.md)<br/>Bul ve olayları, ilgili olayları inceleyin ve hatalar oluşturma |![Arama örneği](./media/app-insights-dashboards/61.png) |
| [Analizler](app-insights-analytics.md)<br/>Güçlü sorgu dili |![Arama örneği](./media/app-insights-dashboards/63.png) |
