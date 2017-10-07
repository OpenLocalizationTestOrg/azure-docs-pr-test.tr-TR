---
title: "aaaMicrosoft Azure IOT Paketi'ne Genel Bakış | Microsoft Docs"
description: "Azure IOT paketi önceden yapılandırılmış çözümler toocollect şey, Internet nasıl sunar genel bakış çözümleme, verileri depolamak, görselleştirmeler sağlamak ve diğer sistemlerle tümleştirmek."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Azure IoT Paketi’ne Genel Bakış

Hello Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar. Bu kurumsal sınıf hizmetler şunları yapmanızı sağlar:

* Cihazlardan veri toplama
* Hareket halinde veri akışı çözümleme
* Büyük veri gruplarını depolama ve sorgulama
* Gerçek zamanlı ve geçmiş verileri görselleştirme
* Arka ofis sistemleriyle tümleştirme
* Cihazlarınızı yönetme

toodeliver bu özellikler, Azure IOT paketi paketleri birlikte birden çok Azure hizmetini özel uzantılarla *önceden yapılandırılmış çözümleri*. Bu önceden yapılandırılmış çözümler, IOT çözümlerinizi toodeliver ele tooreduce hello zaman yardımcı genel IOT çözümü düzenlerinin temel uygulamalarıdır. Hello kullanarak [IOT yazılım geliştirme setleri][lnk-sdks], özelleştirebilir ve bu çözümler toomeet kendi gereksinimlerinizi genişletir. Ayrıca bu çözümleri, yeni IoT çözümleri geliştirirken örnekler ya da şablonlar olarak da kullanabilirsiniz.

Merhaba aşağıdaki video giriş tooAzure IOT paketi sağlar:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Azure IoT Paketindeki Azure IoT Hizmetleri
Merhaba önceden yapılandırılmış çözümler genellikle aşağıdaki hizmetleri hello kullanın:

* Çekirdek tooAzure IOT paketi olan hello [Azure IOT Hub] [ lnk-iot-hub] hizmet. Bu hizmet hello cihaz-bulut sağlar ve bulut-cihaz Mesajlaşma işlevlerini ve ağ geçidi toohello hello gibi davranır Bulut ve diğer önemli IOT paketi hizmetlerini hello. Merhaba hizmet cihazınızdan ölçekte tooreceive iletilerden sağlar ve komutları tooyour aygıtları gönderin. Merhaba hizmeti de sağlar, çok[cihazlarınızı yönetmek][lnk-device-management]. Örneğin, yapılandırma, yeniden başlatma veya bir veya daha fazla aygıtları bağlı toohello hub bir Fabrika gerçekleştirin.
* [Azure Stream Analytics][lnk-asa] hareket halinde veri çözümleme sağlar. Bu hizmet tooprocess gelen telemetri IOT paketi kullanır, toplama gerçekleştirmek ve olayları algılamak. Merhaba önceden yapılandırılmış çözümleri ayrıca aygıtlardan meta veri ya da komut yanıtları gibi verileri içeren stream analytics tooprocess bilgilendirici iletileri kullanır. Hello çözümler cihazlarınızdan gelen akış analizi tooprocess hello iletileri kullanın ve bu iletileri tooother Hizmetleri sunmak.
* [Azure depolama] [ lnk-azure-storage] ve [Azure Cosmos DB] [ lnk-document-db] hello veri depolama özellikleri sağlar. Merhaba önceden yapılandırılmış çözümler blob depolama toostore telemetri ve toomake kullanır, çözümleme için kullanılabilir. Merhaba çözümleri hello çözümlerinin hello cihaz Yönetimi işlevlerini etkinleştirmek ve Cosmos DB toostore cihaz meta verilerini kullanın.
* [Azure Web Apps] [ lnk-web-apps] ve [Microsoft Power BI] [ lnk-power-bi] hello veri görselleştirme özellikleri sağlar. Power BI Hello esnekliğini sağlar tooquickly IOT paketi verilerini kullanan kendi etkileşimli panolar oluşturun.

Tipik bir IOT çözüm mimarisini hello genel bakış için bkz: [Microsoft Azure ve nesnelerin interneti (IOT) hello][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>Önceden yapılandırılmış çözümler

IOT paketi önceden yapılandırılmış çözümler içerir, etkinleştirme, tooquickly ile çalışmaya başlama ve tooexplore gibi yaygın IOT senaryolarını hello:

* Uzaktan izleme
* Tahmine dayalı bakım
* Bağlı fabrika

Bu çözümleri tooyour Azure aboneliği dağıtın ve ardından tam, uçtan uca bir IOT senaryosu çalıştırabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar

IOT paketi yapabileceklerine ve temel bileşenlerine nelerdir genel bakış sahip olduğunuza göre IOT paketi önceden yapılandırılmış hello çözümleri hakkında daha fazla bilgi edinebilirsiniz. Daha fazla bilgi için bkz: [ne hello Azure IOT önceden yapılandırılmış çözümleri?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
