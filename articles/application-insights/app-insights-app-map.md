---
title: "Azure Application Insights eşlemesinde aaaApplication | Microsoft Docs"
description: "Uygulama bileşenleri arasında hello bağımlılıkları görsel sunumu KPI'ları ve uyarılarla etiketli."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a>Application ınsights'ta uygulama eşlemesi
İçinde [Azure Application Insights](app-insights-overview.md), uygulama eşlemesi olan uygulama bileşenlerinizin hello bağımlılık ilişkilerini visual düzeni. Her bileşen KPI'ları bir performans sorunu veya hatası neden herhangi bir bileşeni Bul gibi yük, performans, hataları ve Uyarıları, toohelp gösterir. Hiçbir bileşen toomore aracılığıyla tıklatabilirsiniz ayrıntılı tanılama, Application Insights olaylarını gibi. Uygulamanızı Azure hizmetlerini kullanıyorsa, SQL veritabanı Danışmanı önerileri gibi tooAzure tanılama aracılığıyla tıklatabilirsiniz.

Diğer grafikler gibi bir uygulama eşlemesi toohello tam olarak işlevsel olduğu Azure Pano sabitleyebilirsiniz. 

## <a name="open-hello-application-map"></a>Açık hello uygulama eşlemesi
Uygulamanız için hello genel bakış dikey penceresinden açık hello eşleyin:

![Uygulama Eşlem'i açın](./media/app-insights-app-map/01.png)

![Uygulama eşleme](./media/app-insights-app-map/02.png)

Merhaba eşlemesini gösterir:

* Kullanılabilirlik testleri
* İstemci tarafı bileşen (Merhaba JavaScript SDK'sı ile izlenen)
* Sunucu tarafı bileşeni
* Merhaba istemci ve sunucu bileşenleri bağımlılıkları

Genişletme ve bağımlılık bağlantı gruplarına daraltma:

![Daralt](./media/app-insights-app-map/03.png)

Bir tür (SQL, HTTP vb.) pek çok bağımlılık varsa, bunlar gruplandırılmış görünebilir. 

![Gruplandırılmış bağımlılıkları](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a>Nokta sorunları
Her düğüm bu bileşen için hello yük, performans ve hata hızlarını gibi ilgili performans göstergelerini içerir. 

Uyarı simgeleri olası sorunlar vurgulayın. Turuncu bir uyarı isteklerinde sayfa görünümleri veya bağımlılık çağrıları hataları olduğu anlamına gelir. Kırmızı bir hata oranı %5 yukarıda anlamına gelir. Bu eşikler tooadjust istiyorsanız Seçenekleri'ni açın.

![hata simgeleri](./media/app-insights-app-map/04.png)

Etkin Göster yukarı da uyarır: 

![Etkin uyarılar](./media/app-insights-app-map/05.png)

SQL Azure kullanırsanız, ne zaman gösteren bir simge yoktur nasıl performansını iyileştirebilir ilişkin öneriler vardır. 

![Azure önerisi](./media/app-insights-app-map/06.png)

Tüm simge tooget daha fazla ayrıntı tıklatın:

![Azure önerisi](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a>Tanılama geçişli tıklatma
Merhaba haritaya hello düğümlerinin her biri için tanılama aracılığıyla hedeflenen tıklatın sunar. Merhaba seçenekler hello düğümü hello türüne bağlı olarak değişir.

![Sunucu seçenekleri](./media/app-insights-app-map/09.png)

Azure üzerinde barındırılan bileşenleri için doğrudan bağlantılar toothem hello seçenekleri içerir.

## <a name="filters-and-time-range"></a>Filtreler ve zaman aralığı
Varsayılan olarak, zaman aralığı seçilen hello için kullanılabilir tüm hello veri hello harita özetler. Ancak tooinclude yalnızca belirli işlem adları veya bağımlılıkları filtreleyebilirsiniz.

* İşlem adı: Bu sayfa görünümleri ve sunucu tarafı istek türleri içerir. Bu seçenek ile yalnızca seçili hello işlemleri için hello istemci/sunucu-tarafı düğümde KPI hello harita gösterir hello. Bu belirli işlemler hello bağlamında adlı hello bağımlılıkları gösterir.
* Bağımlılık temel name: Bu hello AJAX tarayıcı ve sunucu tarafı iç bağımlılıkları içerir. Özel bağımlılık telemetri hello TrackDependency API ile rapor ise, bunlar ayrıca burada görünür. Merhaba bağımlılıkları tooshow hello haritaya seçebilirsiniz. Şu anda bu seçimi hello sunucu tarafı istekleri ya da hello istemci-tarafı sayfa görünümleri filtre uygulamaz.

![Filtrelerini ayarlama](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a>Filtreleri Kaydet
uyguladığınız toosave hello filtreleri PIN hello filtrelenmiş görünüm üzerine bir [Pano](app-insights-dashboards.md).

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a>Hata bölmesi
Merhaba eşlemesindeki bir düğümüne tıkladığınızda bir hata bölmesi hataları bu düğüm için özetleme hello sağ tarafında görüntülenir. Hataları ilk işlem Kimliğine göre gruplandırılmış ve sorun kimliğine göre gruplandırılmış

![Hata bölmesi](./media/app-insights-app-map/error-pane.png)

Bir arıza tıklamak bu hatanın en son örnek toohello götürür.

## <a name="resource-health"></a>Kaynak durumu
Bazı kaynak türleri için kaynak durumu hello hello hata bölmesinin üst kısmında görüntülenir. Örneğin, bir SQL düğümü tıklatarak hello veritabanı sistem durumu ve puanlı herhangi bir uyarı gösterir.

![Kaynak durumu](./media/app-insights-app-map/resource-health.png)

Bu kaynak için hello kaynak adı tooview standart genel bakış ölçümleri tıklatabilirsiniz.

## <a name="end-to-end-system-app-maps"></a>Uçtan uca sistem uygulama eşlemeleri

*SDK'sı sürüm 2.3 veya üstü gerektirir*

Çeşitli bileşenleri - uygulamanız varsa, örneğin, bir arka uç Hizmeti ayrıca toohello web uygulaması - sonra gösterebilir bir tümleşik uygulama harita üzerinde tüm bunları.

![Filtrelerini ayarlama](./media/app-insights-app-map/multi-component-app-map.png)

Merhaba uygulama harita hello Application Insights SDK'sı yüklü olan sunucuları arasında yapılan tüm HTTP bağımlılık çağrıları izleyerek sunucu düğümleri bulur. Her bir Application Insights kaynağı toocontain bir sunucu olduğu varsayılır.

### <a name="multi-role-app-map-preview"></a>Birden çok rol uygulama eşleme (Önizleme)

Merhaba Önizleme birden çok rol uygulama eşleme özelliğini sağlar toouse hello uygulama harita veri toohello gönderme birden çok sunucu ile aynı Application Insights kaynağı / izleme anahtarı. Hello eşlemesindeki sunucuları, telemetri öğeler üzerinde hello cloud_RoleName özelliği tarafından ayrılmış. Ayarlama *birden çok rol uygulama eşlemesi* çok*üzerinde* gelen önizlemeleri dikey tooenable bu yapılandırma hello.

Bu yaklaşım, bir mikro hizmetler uygulamasındaki ya da tek bir Application Insights kaynağı içinde birden çok sunucu boyunca toocorrelate olayları istediğiniz diğer senaryolarda istenebilir.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a>Geri Bildirim
Lütfen hello portal geri bildirimi seçeneği aracılığıyla geri bildirim sağlayın.

![MapLink-1 görüntüsü](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a>Sonraki adımlar

* [Azure portal](https://portal.azure.com)
