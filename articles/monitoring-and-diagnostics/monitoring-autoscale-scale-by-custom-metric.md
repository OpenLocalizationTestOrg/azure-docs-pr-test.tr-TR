---
title: "aaaGet otomatik ölçek ile özel bir ölçü Azure tarafından başlatılan | Microsoft Docs"
description: "Bilgi nasıl tooscale kaynağınız özel ölçüm Azure tarafından."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Otomatik ölçek ile özel bir ölçü Azure tarafından kullanmaya başlama
Bu makalede nasıl tooscale kaynağınız Azure portal'ın özel bir ölçü tarafından.

Azure İzleyici otomatik ölçek tooVirtual makine ölçek kümeleri (VMSS), bulut Hizmetleri, uygulama hizmeti planları ve uygulama hizmeti ortamları yalnızca geçerlidir. 

# <a name="lets-get-started"></a>Sağlar kullanmaya başlama
Bu makalede, application ınsights ile yapılandırılmış bir web uygulaması olduğunu varsayar. Zaten yoksa, şunları yapabilirsiniz [ASP.NET Web siteniz için Application Insights'ı ayarlama][1]

- Açık [Azure portalı][2]
- Merhaba sol gezinti bölmesindeki Azure İzleyici simgeyi tıklatın.
  ![Azure izleyicisini Başlat][3]
- Otomatik ölçeklendirme için Otomatik ölçek geçerli otomatik ölçeklendirme durumunun yanı sıra uygulanabilir tüm hello kaynaklarını tooview ayarı tıklatıldığında ![Azure İzleyicisi'nde otomatik ölçek Bul][4]
- Azure İzleyicisi'nde 'Otomatik ölçeklendirme' dikey penceresini açın ve tooscale istediğiniz bir kaynak seçin
> Not: app ınsights yapılandırılmış olan bir web uygulaması ile ilişkili bir uygulama hizmeti planı hello adımları kullanın.
- Merhaba ölçek ayarı dikey penceresinde hello kaynağın hello geçerli örnek sayısı 1 olduğuna dikkat edin. 'Etkinleştir otomatik 'ölçeklendirme'yi tıklatın.
  ![Yeni web uygulaması için ölçek ayarı][5]
- Merhaba ölçek ayarlama ve hello tıklayın için "Kural Ekle" bir ad sağlayın. Bir bağlam hello sağ taraftaki bölmede olarak açılır hello ölçek kuralı seçeneklerini dikkat edin. Varsayılan olarak, örneğinizi sayısı 1 ile Merhaba CPU percetage hello kaynağının % 70 aşarsa hello seçeneği tooscale ayarlar. Merhaba ölçüm Kaynağı Değiştir hello üstünde çok "Application Insights", select app ınsights kaynağı hello 'Resource' açılır ve temel seçip hello özel ölçüm tooscale istediğiniz hello.
  ![Özel bir ölçü ölçeklendirin][6]
- Yukarıdaki benzer toohello adımı içinde ölçeklendirmek ve hello özel ölçüm eşiğin altına ise hello ölçek sayısı 1 ile azaltmak ölçek kuralı ekleyin.
  ![CPU üzerinde göre ölçeklendirin][7]
- Merhaba sınırları örneği ayarlayın. Merhaba özel ölçüm dalgalanmaları bağlı olarak 2-5 örnekleri arasında tooscale isterseniz, örneğin, 'minimum' çok '2', 'en fazla' çok ayarlayın '5' ve 'default' çok '2'
> Not: hello kaynak ölçümleri okunurken bir sorun oluştu ve hello geçerli kapasitesi hello varsayılan kapasitenin altında olduğunda durumunda, ardından tooensure hello hello kaynak kullanılabilirliğini otomatik ölçeklendirme toohello varsayılan değerini ölçeklendirir. Merhaba geçerli kapasite zaten varsayılan kapasitesinden yüksek ise, otomatik ölçeklendirme, ölçekleme sağlamaz.
- 'Kaydet' tıklayın

Tebrikler. Şimdi başarıyla ölçek ayarı tooauto oluşturulan artık web uygulamanız özel bir ölçü ölçekleme.

> Not: hello aynı VMSS veya Bulut hizmet rolü ile başlatılan geçerli tooget adımlardır.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
