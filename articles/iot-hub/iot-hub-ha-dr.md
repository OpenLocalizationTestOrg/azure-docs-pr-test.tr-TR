---
title: "aaaAzure IOT hub'ı yüksek kullanılabilirlik ve olağanüstü durum kurtarma | Microsoft Docs"
description: "Olağanüstü durum kurtarma özellikleri ile yüksek oranda kullanılabilir Azure IOT çözümleri toobuild yardımcı hello Azure ve IOT hub'ı özelliklerini açıklar."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>IOT hub'ı yüksek kullanılabilirlik ve olağanüstü durum kurtarma
Bir Azure hizmeti IOT hub'ı hello çözümü tarafından gerekli herhangi bir ek iş olmadan hello Azure bölgesi düzeyinde açarken kullanarak yüksek kullanılabilirlik (HA) sağlar. Merhaba Microsoft Azure platformu özellikleri toohelp olağanüstü durum kurtarma (DR) özelliklerini veya çapraz bölge kullanılabilirliği ile çözümler derleme de içerir. Tooprovide genel istiyorsanız, çapraz bölge yüksek kullanılabilirlik aygıtların veya kullanıcıların, tasarım ve tootake bu özelliklerden Azure DR çözümlerinizi hazırlayın. Merhaba makale [Azure iş sürekliliği teknik kılavuz](../resiliency/resiliency-technical-guidance.md) hello iş sürekliliği ve DR için Azure içinde yerleşik özellikler açıklanmaktadır. Merhaba [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma] [ Disaster recovery and high availability for Azure applications] kağıt üzerinde stratejileri Mimari Kılavuzu için Azure uygulamalarını tooachieve sağlar HA ve DR.

## <a name="azure-iot-hub-dr"></a>Azure IOT hub'ı DR
Ayrıca toointra bölge HA IOT hub'ı olağanüstü durum kurtarma için hiçbir hello kullanıcı müdahalesi gerekli yük devretme mekanizmaları uygular. IOT Hub DR otomatik olarak başlatılır ve bir kurtarma süresi hedefi (RTO) 2-26 saatleri ve kurtarma noktası hedefi (RPO'lar) aşağıdaki hello sahiptir.

| İşlev | RPO |
| --- | --- |
| Kayıt defteri ve iletişim işlemleri için hizmet kullanılabilirliği |CName kaybolma |
| Kimlik verilerini kimlik kayıt defterinde |0-5 dakika veri kaybı |
| Cihazdan buluta iletiler |Okunmamış iletileri kaybolur |
| İleti izleme işlemleri |Okunmamış iletileri kaybolur |
| Bulut-cihaz iletilerini |0-5 dakika veri kaybı |
| Bulut cihaz geri bildirim kuyruğu |Okunmamış iletileri kaybolur |

## <a name="regional-failover-with-iot-hub"></a>IOT Hub ile bölgesel yük devretme
Dağıtım topolojileri IOT çözümlerinde tam işlenmesi bu makalenin kapsamı dışındadır hello ' dir. Merhaba anlatılmaktadır hello *bölgesel yük devretme* dağıtım modeli için yüksek kullanılabilirlik ve olağanüstü durum kurtarma hello amacı.

Bölgesel yük devretme modelinde, çözüm arka uç çalışır bir veri merkezi konumda öncelikle hello ve bir ikincil IOT hub ve arka uç başka bir veri merkezi konumda dağıtılır. Merhaba IOT hub'hello birincil veri merkezinde hello aygıt toohello birincil bir kesinti veya hello ağ bağlantısı varsa, veri merkezi kesilir. Merhaba birincil ağ geçidi ulaşılamadığında cihazlar ikincil hizmet uç noktası kullanır. Çapraz bölge yük devretme özelliğine sahip hello çözüm kullanılabilirlik hello yüksek kullanılabilirliği tek bir bölge geliştirilebilir.

Tooimplement bölgesel yük devretme modeli IOT Hub ile yüksek bir düzeyde hello aşağıdaki gerekir:

* **İkincil bir IOT hub ve cihaz mantığı yönlendirme**: birincil bölgenizdeki hizmet kesintisi hello durumda aygıtları bağlanan tooyour ikincil bölge başlatmanız gerekir. Çoğu Hizmetleri söz konusu durumu algılayan yapısını Hello verildiğinde, çözüm Yöneticiler tootrigger hello arası bölge yük devretme işlemi için yaygın bir sorundur. Merhaba en iyi şekilde toocommunicate hello yeni uç nokta toodevices, hello işleminin denetimi korurken düzenli olarak kontrol toohave olan bir *Danışman* hello geçerli etkin uç noktası için hizmet. Merhaba Danışman hizmetinin çoğaltılır ve ulaşılabilir tutulan bir web uygulaması olabilir DNS-yeniden yönlendirme teknikleri kullanarak (örneğin, kullanarak [Azure Traffic Manager][Azure Traffic Manager]).
* **Kimlik kayıt defteri çoğaltma** -toobe kullanılabilir, hello ikincil IOT hub'ı toohello çözüm bağlanabilir tüm cihaz kimliklerini içermelidir. Hello çözüm cihaz kimliklerini coğrafi olarak çoğaltılmış yedeklerini tutmak ve hello etkin uç noktası hello aygıtlar için geçmeden önce bunları toohello ikincil IOT hub'ı karşıya gerekir. Hello aygıt kimlik verme işlevselliğini IOT Hub'ın bu bağlamda yararlı olur. Daha fazla bilgi için bkz: [IOT Hub Geliştirici Kılavuzu - kimlik kayıt defteri][IoT Hub developer guide - identity registry].
* **Mantıksal birleştirme** - zaman hello birincil bölge yeniden kullanılabilir, tüm durum hello ve hello ikincil sitede oluşturulan veri geçirilen geri toohello birincil bölge olması gerekir. Bu durum ve verileri çoğunlukla ilişkilendirilme toodevice kimlikleri ve hello birincil IOT hub'ı ve hello birincil bölgede başka bir uygulamaya özgü depoları ile birleştirilmelidir uygulama meta verileri. toosimplify bu adımı ıdempotent işlemleri kullanmanız gerekir. Idempotent işlemleri hello yan etkileri hello nihai tutarlı dağıtım olayların ve yinelemeleri ya da olayların sırası teslimini en aza indirin. Ayrıca, hello uygulama mantığını tasarlanmış tootolerate olası tutarsızlıklar veya tarih durumdan "biraz" olmalıdır. Bu durum tabanlı kurtarma noktası hedefi (RPO) üzerinde "onarma" Merhaba sistemi için çok toohello ek süresini ortaya çıkabilir.

## <a name="next-steps"></a>Sonraki adımlar
Azure IOT Hub hakkında daha fazla bu bağlantılar toolearn izleyin:

* [(Öğretici) IOT hub ile çalışmaya başlama][lnk-get-started]
* [Azure IOT Hub nedir?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
