---
title: Azure Web Apps analitik veri aaaView | Microsoft Docs
description: "Tüm Azure Web uygulaması kaynaklar arasında farklı ölçümleri toplayarak, Azure Web Apps hakkında hello Azure Web Apps Analytics çözüm toogain Öngörüler kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 20ff337f-b1a3-4696-9b5a-d39727a94220
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: banders
ms.openlocfilehash: 7e9725f95c9faf01da89184975ad5444dd19ff95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-analytic-data-for-metrics-across-all-your-azure-web-app-resources"></a>Tüm Azure Web uygulaması kaynaklarına arasında ölçümleri ilişkin analitik verileri görüntüle

![Web uygulamaları simgesi](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-symbol.png)  
Hello Azure Web Apps analiz (Önizleme) çözümü fikir sağlar, [Azure Web Apps](../app-service-web/app-service-web-overview.md) tüm Azure Web uygulaması kaynaklar arasında farklı ölçümleri toplayarak. Hello çözümüyle çözümlemek ve web uygulaması kaynak ölçüm verileri arayabilirsiniz.

Merhaba çözümünü kullanarak, görüntüleyebilirsiniz:

- Merhaba yüksek yanıt süresiyle üst Web uygulamaları
- Başarılı ve başarısız istekleri dahil olmak üzere, Web uygulamalarında istek sayısı
- En yüksek gelen ve giden trafiği ile üst Web uygulamaları
- Yüksek CPU ve bellek kullanımı ile üst hizmet planları
- Azure Web Apps etkinlik günlük işlemleri

## <a name="connected-sources"></a>Bağlı kaynaklar

Çoğu diğer günlük analizi çözümlerden farklı Azure Web uygulamaları için aracıları tarafından toplanan veriler değil. Merhaba çözümü tarafından kullanılan tüm verileri doğrudan Azure'dan gelir.

| Bağlı Kaynak | Destekleniyor | Açıklama |
| --- | --- | --- |
| [Windows aracıları](log-analytics-windows-agents.md) | Hayır | Merhaba çözüm Windows aracılardan bilgi toplamaz. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır | Merhaba çözüm Linux aracılarını bilgi toplamaz. |
| [SCOM yönetim grubu](log-analytics-om-agents.md) | Hayır | Merhaba çözüm bağlı SCOM yönetim grubunda aracılardan gelen bilgiler toplamaz. |
| [Azure depolama hesabı](log-analytics-azure-storage.md) | Hayır | Merhaba çözüm koleksiyonu bilgileri Azure depolama biriminden değil yapar. |

## <a name="prerequisites"></a>Ön koşullar

- tooaccess Azure Web uygulaması kaynak ölçüm bilgileri, bir Azure aboneliğinizin olması gerekir.

## <a name="configuration"></a>Yapılandırma

Aşağıdaki adımları tooconfigure hello Azure Web Apps analiz çözümü alanlarınızı için hello gerçekleştirin.

1. Hello Azure Web Apps Analytics çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. [PowerShell kullanarak Azure kaynak ölçümleri günlük tooOMS etkinleştirmek](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

Hello Azure Web Apps analiz çözümü Azure'dan iki kümesi ölçümleri toplar:

- Azure Web Apps ölçümleri
  - Ortalama bellek çalışma kümesi
  - Ortalama yanıt süresi
  - Bayt alınan/gönderilen
  - CPU süresi
  - İstekler
  - Bellek çalışma kümesi
  - Httpxxx
- Uygulama hizmeti planı ölçümleri
  - Bayt alınan/gönderilen
  - CPU Yüzdesi
  - Disk Sırası Uzunluğu
  - HTTP sırası uzunluğu
  - Bellek yüzdesi

Ayrılmış hizmet planı kullanıyorsanız, uygulama hizmeti planı ölçümleri yalnızca toplanır. Bu toofree uygulanmaz veya paylaşılan uygulama hizmeti planları.

Merhaba OMS portalı kullanarak hello çözüm eklerseniz, döşeme hello aşağıdaki görürsünüz. Çok ihtiyacınız[PowerShell kullanarak Azure kaynak ölçümleri günlük tooOMS etkinleştirmek](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell).

![Değerlendirme bildirim gerçekleştirme](./media/log-analytics-azure-web-apps-analytics/performing-assessment.png)

Merhaba çözüm yapılandırdıktan sonra veri akışının başlamalıdır 15 dakika içinde tooyour çalışma.

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

Hello Azure Web uygulamaları analizi çözüm tooyour çalışma alanı eklediğinizde, hello **Azure Web Apps Analytics** döşeme tooyour genel bakış Panosu'na eklenir. Bu kutucuğu, Azure Web Apps hello çözüm erişim tooin Azure aboneliğinizin bulunduğu hello sayısı sayısını görüntüler.

![Azure Web Apps Analytics döşeme](./media/log-analytics-azure-web-apps-analytics/azure-web-apps-analytics-tile.png)

### <a name="view-azure-web-apps-analytics-information"></a>Azure Web uygulamaları analizi bilgilerini görüntüleme

Merhaba tıklatın **Azure Web Apps Analytics** döşeme tooopen hello **Azure Web Apps Analytics** Pano. Merhaba Pano aşağıdaki tablonun hello hello Kanatlar içerir. Her dikey penceresinde hello dikey'nın ölçütlerine kapsam ve zaman aralığını belirtilen eşleşen tooten öğeleri listeler. Tıklayarak tüm kayıtları döndüren bir günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello dikey veya hello dikey penceresi Başlığı tıklatarak.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| Sütun | Açıklama |
| --- | --- |
| Azure Webapps |   |
| Web uygulamaları istek eğilimleri | Merhaba, seçtiğiniz hello tarih aralığı için Web uygulamaları İstek Eğilimi bir çizgi grafiğini gösterir ve hello üst on web isteklerinin listesini gösterir. Merhaba çizgi grafiği toorun günlük arama için tıklatın<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* (MetricName=Requests OR MetricName=Http*) &#124; measure avg(Average) by MetricName interval 1HOUR</code> <br>Web isteği öğesi toorun isteyen hello web isteği ölçüm eğilimi için bir günlük Ara'yı tıklatın. |
| Web uygulamaları yanıt süresi | Merhaba Web Apps yanıt süresi, seçtiğiniz hello tarih aralığı için bir çizgi grafiğini gösterir. Ayrıca bir listesini hello listesini gösterir üst on Web Apps yanıt süreleri. Merhaba grafik toorun günlük arama için tıklatın<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"* MetricName="AverageResponseTime" &#124; measure avg(Average) by Resource interval 1HOUR</code><br> Bir Web uygulaması toorun hello Web uygulaması için yanıt sürelerini döndüren bir günlük Ara'yı tıklatın. |
| Web uygulamaları trafiği | MB cinsinden Web Apps trafiği için bir çizgi grafiği gösterir ve hello üst Web Apps trafiği listeler. Merhaba grafik toorun günlük arama için tıklatın<code>Type:AzureMetrics ResourceId=*"/MICROSOFT.WEB/SITES/"*  MetricName=BytesSent OR BytesReceived &#124; measure sum(Average) by Resource interval 1HOUR</code><br> Bu trafiği ile tüm Web uygulamaları için hello son dakika gösterir. Bayt gösteren bir günlük arama alınan ve Web uygulaması hello için gönderilen bir Web uygulaması toorun'ı tıklatın. |
| Azure uygulama hizmeti planları |   |
| Uygulama hizmeti planları CPU kullanımı ile &gt; % 80 | Merhaba sayısı toplam CPU kullanımını en iyi 10 App Service planları CPU kullanımı % 80 ve listeleri hello büyük sahip App Service planları gösterir. Merhaba toplam alan toorun günlük arama için tıklatın<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=CpuPercentage &#124; measure Avg(Average) by Resource</code><br> App Service planları ve ortalama CPU kullanımlarını listesini gösterir. Bir uygulama hizmeti planı toorun, ortalama CPU kullanımını gösteren bir günlük Ara'yı tıklatın. |
| Uygulama hizmeti planları bellek kullanımı ile &gt; % 80 | Merhaba toplam sayısını bellek kullanımı % 80 ve listeleri tarafından bellek kullanımı en iyi 10 App Service planları hello büyük sahip App Service planları gösterir. Merhaba toplam alan toorun günlük arama için tıklatın<code>Type=AzureMetrics ResourceId=*"/MICROSOFT.WEB/SERVERFARMS/"* MetricName=MemoryPercentage &#124; measure Avg(Average) by Resource</code><br> App Service planları ve bunların ortalama bellek kullanımı listesini gösterir. Bir uygulama hizmeti planı toorun ortalama bellek kullanımı gösteren bir günlük Ara'yı tıklatın. |
| Azure Web Apps etkinlik günlükleri |   |
| Azure Web Apps etkinlik denetim | Gösterir hello toplam sayısı ile Web uygulamaları [etkinlik günlükleri](log-analytics-activity.md) ve listeleri hello ilk 10 etkinlik günlüğü işlemleri. Merhaba toplam alan toorun günlük arama için tıklatın<code>Type=AzureActivity ResourceProvider= "Azure Web Sites" &#124; measure count() by OperationName</code><br> Bu etkinlik günlüğü işlemlerini hello listesini gösterir. Bir etkinlik günlüğü işlemi toorun hello kayıtlarını hello işlemi için listeler günlük arama tıklayın. |



### <a name="azure-web-apps"></a>Azure Web Apps

Merhaba panosunda, Web uygulamaları ölçümlerinizi konusunda daha fazla bilgi tooget inebilir. Dikey pencere ilk bu kümesi zamanla hello Web Apps istekler, hatalar (örneğin, HTTP404), trafik ve ortalama yanıt süresi sayısı hello eğilimi gösterir. Ayrıca farklı Web uygulamaları için bu ölçümleri dökümünü gösterir.

![Azure Webapps dikey penceresi](./media/log-analytics-azure-web-apps-analytics/web-apps-dash01.png)

Bu verileri gösteren bir temel nedeni, böylelikle yüksek yanıt süresi ile bir Web uygulaması tanımlamak ve toofind hello kök nedeni araştırın. Bir eşiği de daha kolay tanımanıza olanları sorunları hello uygulanan toohelp sınırıdır.

- Web uygulamaları kırmızı ile gösterilen yanıt süresi 1 saniyeden daha yüksek olması.
- Web uygulamaları turuncu içinde gösterilen 0.7 ikinci ve 1 saniyeden az maliyetinden daha yüksek bir yanıt süresi vardır.
- Web uygulamaları yeşil renkte gösterilir 0,7'den küçük bir yanıt süresi ikinci gerekir.

Günlük arama örnek resmi aşağıdaki hello bu hello görebilirsiniz *anugup3* web uygulaması diğer web uygulamaları hello daha çok daha yüksek bir yanıt süresi vardı.

![Günlük arama örneği](./media/log-analytics-azure-web-apps-analytics/web-app-search-example.png)

### <a name="app-service-plans"></a>App Service Planları

Ayrılmış hizmet planları kullanıyorsanız, App Service planları için ölçümleri de toplayabilir. Bu görünümde, App Service planları yüksek CPU veya bellek kullanımı ile bakın (&gt; % 80). Ayrıca, gösterir yüksek bellek veya CPU kullanımı ile üst uygulama hizmetleri hello. Benzer şekilde, bir eşik sınırını olanları sorunları daha kolay tanımanıza hello uygulanan toohelp ' dir.

- Kırmızı ile gösterilen App Service planları CPU/bellek kullanımı % 80 ' daha yüksek olması.
- Uygulama hizmeti planları turuncu içinde gösterilen bir CPU/bellek kullanımı % 60 daha yüksek ve % 80'den daha düşük sahip.
- Yeşil renkte gösterilir App Service planları CPU/bellek kullanımı % 60 ' daha düşük sahip.

![Azure App Service planları dikey penceresi](./media/log-analytics-azure-web-apps-analytics/web-apps-dash02.png)

## <a name="azure-web-apps-log-searches"></a>Azure Web Apps Günlük aramalar

Merhaba **listesi, popüler Azure Web Apps arama sorguları** tüm hello gösterir ilgili etkinlik günlükleri, Web uygulamaları kaynaklarınızı gerçekleştirilen hello işlemlerinin Öngörüler sağlayan Web uygulamaları için. Ayrıca tüm listeler hello ilgili işlemler ve hello kaç kez oluştu.

Merhaba günlük arama sorguları herhangi bir başlangıç noktası olarak kullanarak, bir uyarı kolayca oluşturabilirsiniz. Örneğin, bir ölçüm 's ortalama yanıt süresi 1 saniyede büyük olduğunda bir uyarı toocreate isteyebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

- Oluşturma bir [uyarı](log-analytics-alerts-creating.md) belirli bir ölçüm için.
- Kullanım [günlük arama](log-analytics-log-searches.md) tooview ayrıntılı bilgileri, etkinlik günlükleri.
