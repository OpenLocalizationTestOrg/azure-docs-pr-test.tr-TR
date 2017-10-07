---
title: "Azure zaman serisi Öngörüler aaaOverview | Microsoft Docs"
description: "Giriş tooAzure zaman serisi Insight, zaman serisi veri analizi ve IOT çözümleri için yeni bir hizmet"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>Azure Zaman Serisi Görüşleri nedir?

Azure zaman serisi Öngörüler bir depolama, analiz ve kolay tooingest olun görselleştirme bileşenleri ile yönetilen bir bulut hizmetidir, depolama, araştırın ve olayları milyarlarca aynı anda analiz edin. Zaman Serisi Görüşleri verilerinize ilişkin genel bir görünüm sunar, gizli eğilimleri ve anormallikleri keşfetmenize ve neredeyse gerçek zamanlı olarak kök neden analizleri gerçekleştirmenize yardımcı olarak IoT Çözümlerinizi hızla doğrulamanıza ve cihazların kapalı kalma süresinden kaynaklanan maliyetleri önlemenize olanak sağlar. Zaman serisi Öngörüler olay aracıların (ör. IOT hub'ları veya olay hub'ları) zaman serisi verileri alır, hello veri dizinler ve yapılandırılabilir bekletme ilkesini temel alarak veri kaldırdıktan. Kullanıcıların hello verileri sezgisel bir UX veya REST sorgu API'leri yoluyla kullanmak.

![Zaman Serisi Görüşleri’ne Genel Bakış](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Birincil senaryolar

* IoT çözümlerini dakikalar içinde izleyin ve doğrulayın.
* IoT verilerini ölçekleyerek görselleştirin ve analiz edin.
* Kök neden analizini ve anormallik algılamayı hızlandırın.
* Çok sayıda cihazın, tesisin ve verinin genel görünümünü oluşturun.

## <a name="capabilities-and-benefits"></a>İşlevler ve avantajlar

* **Başlatılan kolay tooget**: Azure zaman serisi Öngörüler hiçbir açık veri hazırlık gerektirir ve son derece hızlı sahiptir. Azure IOT hub'ı veya olay hub'ı olayların toobillions dakika cinsinden bağlayın. Bağlantı kurulduktan sonra görselleştirin ve tooquickly doğrulamak, IOT çözümlerinizi saniye cinsinden algılayıcı verilerini ile etkileşim. Zaman serisi Öngörüler kolay toouse olur; tek satırlık bir kod yazmak zorunda kalmadan verilerinizle etkileşim kurabilirsiniz.  Yeni bir dil toolearn yoktur; Zaman serisi Öngörüler İleri düzey kullanıcılar için bir parçalı, serbest metin sorgu yüzey sağlar ve üzerine ve tüm araştırması tıklatın.

* **Yakın gerçek zamanlı Öngörüler**: zaman serisi Öngörüler alma yüz milyonlarca algılayıcı olayları, günde bir dakika gecikmeyle toochanges hızlıca tepki gösterebilmesi için. Zaman Serisi Görüşleri, eğilimleri ve anormallikleri hızla saptamanıza, karmaşık kök-neden analizleri yürütmenize ve masraflı sistem kapatma sürelerini önlemenize yardımcı olarak sensör verileriniz üzerinde derin görüşler kazanmanıza katkıda bulunur. Gerçek zamanlı ve geçmiş verileri arasında geçici bağıntı etkinleştirerek, zaman serisinin Öngörüler hello veri gizli eğilimler kilidini yardımcı olur.

* **Özel çözümler oluşturma**: Azure Zaman Serisi Öngörüleri verilerini mevcut uygulamalarınıza ekleyin ya da Zaman Serisi Öngörüleri REST API’leriyle yeni özel çözümler oluşturun. Oluşturma ve paylaşma, diğerleri için bulma tooexplore paylaşabilirsiniz görünümleri kişiselleştirilmiş.

* **Ölçeklenebilirlik**: zaman serisi Öngörüler tasarlanmış toosupport IOT ölçekte değil. Önizleme'de, dağıtabilirsiniz 31 gün varsayılan saklama ile günde milyon olayları span 1 milyon too100 giriş. Muazzam miktarlardaki geçmiş verilerine ek olarak canlı veri akışlarını da neredeyse gerçek zamanlı olarak görselleştirebilir ve analiz edebilirsiniz. İlerleyen, giriş ve saklama hızları tooaccommodate şimdiye kadar değişen bir kurumsal ölçek artmasına neden olur.

## <a name="time-series-insights-glossary"></a>Zaman Serisi Öngörüleri sözlüğü

* **Ortam**: Ortam, giriş ve depolama kapasitesi olan bir Azure kaynağıdır.  Müşteriler hello kendi gerekli kapasiteye sahip Azure Portalı aracılığıyla ortamları sağlayın.
* **Olay Kaynağı**: Olay Kaynağı, Azure Event Hubs gibi bir olay aracısından türetilir.  Zaman serisi Öngörüler tooEvent hiçbir kod yazmadan hello veri akışı alma kaynakları, doğrudan bağlanır. Şu anda Zaman Serisi Görüşleri, Azure Event Hubs'ı ve Azure IoT Hub'larını destekler.
* **Başvuru verileri**: zaman serisi Öngörüler hello özelliği toojoin zaman serisi veri başvuru verileri ile kullanıcılara sağlar.  Başvuru verileri cihazlar hakkındaki meta verileri veya görece seyrek değişen diğer statik verileri içerebilir. Zaman serisi Öngörüler kullanıcılar toovisualize izin vererek hello başvuru verileri veri akışları ile birleştirir ve bu verileri neredeyse gerçek zamanlı analiz edin.
