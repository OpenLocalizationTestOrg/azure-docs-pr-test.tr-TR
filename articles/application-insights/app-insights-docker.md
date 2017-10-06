---
title: "Azure Application Insights aaaMonitor Docker uygulamalarında | Microsoft Docs"
description: "Docker performans sayaçları, olaylar ve özel durumları Application Insights üzerinde hello telemetri kapsayıcılı hello uygulamalardan birlikte görüntülenebilir."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Application ınsights'ta Docker uygulama izleme
Yaşam döngüsü olayları ve performans sayaçları [Docker](https://www.docker.com/) kapsayıcıları Application Insights grafiğinin. Merhaba yüklemek [Application Insights](app-insights-overview.md) ana bilgisayarınız ve kapsayıcısında görüntü olarak için diğer görüntüleri hello gibi hello ana performans sayaçlarını görüntüler.

Docker ile uygulamalarınızı basit kapsayıcılarında tüm bağımlılıkları ile tam dağıtın. Bunlar, Docker altyapısına çalıştıran herhangi bir ana makinede çalıştıracaksınız.

Merhaba çalıştırdığınızda [Application Insights görüntü](https://hub.docker.com/r/microsoft/applicationinsights/) , Docker ana bilgisayarda bu avantajlarını elde edersiniz:

* Yaşam döngüsü telemetri çalıştıran tüm Merhaba kapsayıcılara hakkında hello konakta - başlatmak, durdurmak ve benzeri.
* Tüm Merhaba kapsayıcılara için performans sayaçları. CPU, bellek, ağ kullanımını ve daha fazlası.
* Varsa, [Java için Application Insights SDK'sı yüklü](app-insights-java-live.md) Merhaba kapsayıcılara çalıştıran hello uygulamalarında, bu uygulamaların tüm hello telemetri hello kapsayıcı ve ana bilgisayar makinesi tanımlama ek özellikleri sahip olur. Dolayısıyla örneğin bir uygulama içinde birden fazla ana çalışan örneklerini varsa, ana bilgisayar tarafından uygulama telemetrinizi kolayca filtreleyebilirsiniz.

![Örnek](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Application Insights kaynağı ayarladıysanız
1. Oturum [Microsoft Azure portal](https://azure.com) ve açın; uygulamanız için hello Application Insights kaynağı veya [yeni bir tane oluşturun](app-insights-create-new-resource.md). 
   
    *Hangi kaynak kullanmalıyım?* Konağınız üzerinde çalışan hello uygulamaları başka birisi tarafından geliştirilmiştir sonra çok ihtiyacınız[yeni bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md). Burada görüntüleyebilir ve hello telemetriyi Çözümle budur. ('Genel' hello uygulama türü için seçin.)
   
    Ancak hello uygulamaların hello Geliştirici değilseniz, daha sonra umuyoruz [Application Insights SDK'sı eklenen](app-insights-java-live.md) bunların tooeach. Gerçekten'ın tüm bileşenleri tek bir iş uygulaması değilseniz, ardından bunların tümünün toosend telemetri tooone kaynak yapılandırın ve bu aynı kaynak toodisplay hello Docker yaşam döngüsü ve performans verileri kullanacaksınız. 
   
    Üçüncü senaryo hello uygulamaların çoğu geliştirilmiş, ancak bunların telemetri ayrı kaynaklar toodisplay kullanıyorsanız ' dir. Bu durumda, büyük olasılıkla da istediğiniz toocreate hello Docker verileri için ayrı bir kaynak. 
2. Ekle hello Docker döşeme: seçin **eklemek döşeme**hello Docker döşeme hello Galerisi'nden sürükleyin ve ardından **Bitti**. 
   
    ![Örnek](./media/app-insights-docker/03.png)
3. Merhaba tıklatın **Essentials** açılır ve hello izleme anahtarını kopyalayın. Bu tootell hello SDK kullandığınız nerede toosend kendi telemetri.

    ![Örnek](./media/app-insights-docker/02-props.png)

Tooit en kısa sürede geri dönerseniz şekilde bu tarayıcı penceresini elinizin altında toolook, telemetrisini tutun.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>Ana bilgisayarda Hello Application Insights izleyicisini Çalıştır
Herhangi bir yerde toodisplay hello telemetri olduğuna göre toplamak ve göndermeden hello kapsayıcılı uygulaması ayarlayabilirsiniz.

1. Tooyour Docker ana bağlayın. 
2. Bu komutta, izleme anahtarını düzenleyin ve ardından çalıştırın:
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Docker ana bilgisayar başına yalnızca bir Application Insights görüntü gereklidir. Uygulamanız birden çok Docker ana bilgisayarda dağıtılırsa, her ana bilgisayarda hello komutu yineleyin.

## <a name="update-your-app"></a>Uygulamanızı güncelleştirme
Uygulamanız ile Merhaba izlenmiş olan varsa [Java için Application Insights SDK](app-insights-java-get-started.md), satır hello altında projenizdeki hello Applicationınsights.xml dosyasına aşağıdaki hello eklemek `<TelemetryInitializers>` öğe:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

Bu, uygulamanızdan gönderilen kapsayıcı ve ana bilgisayar kimliği tooevery telemetri öğesi gibi Docker bilgileri ekler.

## <a name="view-your-telemetry"></a>Telemetrinizi görüntüleme
Tooyour Application Insights kaynağını hello Azure portalına geri dönün.

Hello Docker kutucuğa tıklayın.

Özellikle, Docker altyapısı üzerinde çalışan diğer kapsayıcılar varsa, kısa süre içinde hello Docker uygulamadan gelen veri görürsünüz.

Hello görünümleri alabileceğiniz bazıları aşağıda verilmiştir.

### <a name="perf-counters-by-host-activity-by-image"></a>Ana bilgisayar, görüntü göre etkinlik tarafından performans sayaçları
![Örnek](./media/app-insights-docker/10.png)

![Örnek](./media/app-insights-docker/11.png)

Herhangi bir ana bilgisayar veya görüntü adıyla daha fazla ayrıntı için'ı tıklatın.

toocustomize hello görünümü, herhangi bir grafik, başlık hello kılavuz'a tıklayın veya ekleme grafik kullanın. 

[Ölçüm Gezgini hakkında daha fazla bilgi](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Docker kapsayıcısı olayları
![Örnek](./media/app-insights-docker/13.png)

olayları tek tek tooinvestigate, tıklatın [arama](app-insights-diagnostic-search.md). İstediğiniz arama ve filtreleme toofind hello olaylar. Tüm olay tooget daha fazla ayrıntı'ı tıklatın.

### <a name="exceptions-by-container-name"></a>Kapsayıcı adı tarafından özel durumlar
![Örnek](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Docker bağlamı tooapp telemetri eklendi
AI Docker bağlamla zenginleştirilmiş SDK'sı, izlenmiş hello uygulamasından gönderilen telemetri isteği:

![Örnek](./media/app-insights-docker/16.png)

İşlemci zamanı ve kullanılabilir bellek performans sayaçları, zenginleştirilmiş ve Docker kapsayıcısı adına göre gruplandırılır:

![Örnek](./media/app-insights-docker/15.png)

## <a name="q--a"></a>Soru-Cevap
*Ne Application Insights Docker elde edilemiyor bana veriyor?*

* Performans sayaçları kapsayıcı ve görüntü tarafından ayrıntılı dökümü.
* Kapsayıcı ve uygulama verilerini tek bir Panoda tümleştirin.
* [Telemetri verme](app-insights-export-telemetry.md) daha fazla analiz tooa veritabanı, Power BI veya diğer Pano için.

*Merhaba uygulamadan kendisini telemetri nasıl sağlarım?*

* Merhaba Application Insights SDK'sı hello uygulamada yükleyin. Bilgi edinmek için nasıl: [Java web uygulamaları](app-insights-java-get-started.md), [Windows web uygulamaları](app-insights-asp-net.md).

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Sonraki adımlar

* [Java için Application Insights](app-insights-java-get-started.md)
* [Node.js için Application Insights](app-insights-nodejs.md)
* [ASP.NET için Application Insights](app-insights-asp-net.md)
