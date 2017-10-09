---
title: "aaaPredict araç sistem durumu ve alışkanlık - Azure yürüten | Microsoft Docs"
description: "Yürüten alışkanlıklarınıza ve araç sistem durumunu Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler Hello özelliklerini kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Araç telemetri analizi çözüm kitabı
Bu **menü** bu playbook toohello bölümlerde bağlar. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Genel Bakış
Süper bilgisayarlar hello Laboratuvarın dışına taşınmış ve şimdi bizim Garaj yerleşmiş durumdayken! Bu modern otomobiller saniyede milyonlarca etkinliği izlemek ve hello özelliği tootrack vermiş algılayıcılar, çok sayıda içerir. 2020 tarafından bu araba çoğunu bağlı toohello Internet yapıldığını bekliyoruz. Bu bol miktarda veri tooprovide büyük güvenlik, güvenilirlik ve daha iyi yönlendirmeli deneyimi içine dokunma düşünün! Microsoft, bu gerçekte Cortana Intelligence ile düş yapmıştır.

Microsoft'un Cortana Intelligence tam olarak yönetilen bir büyük veri ve tootransform etkinleştirir analytics suite verilerinizi akıllı eyleme Gelişmiş. Toointroduce istiyoruz Cortana Intelligence araç Telemetri analizi çözüm şablonu toohello. Bu çözümün nasıl araba dealerships, otomobil üreticileri ve sigorta şirketler Cortana Intelligence toogain gerçek zamanlı hello yeteneklerini kullanabilir ve araç sistem durumu ve yürüten Tahmine dayalı Öngörüler alışkanlıklarınıza gösterir. 

Merhaba çözümü olarak gerçekleştirilen bir [lambda mimarisi deseni](https://en.wikipedia.org/wiki/Lambda_architecture) hello Cortana Intelligence platformu için tam potansiyelinin hello gösteren gerçek zamanlı ve toplu işleme. Merhaba çözüm: 

* bir araç telematik simulator sağlar
* Event Hubs Azure'da sanal araç telemetri olayları milyonlarca alma yararlanır 
* Stream Analytics toogain gerçek zamanlı Öngörüler araç sistem durumunu kullanır
* Merhaba verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder. 
* Machine Learning avantajlarından anomali algılama gerçek zamanlı yararlanır getirin ve toplu işleme toogain Tahmine dayalı Öngörüler.
* Ölçek ve Data Factory toohandle orchestration, planlama, kaynak yönetimi ve hello toplu işleme ardışık izleme Hdınsight tootransform veri yararlanır 
* Bu çözüm gerçek zamanlı veri ve Power BI kullanarak Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano sağlar

## <a name="architecture"></a>Mimari
![Çözüm mimarisi diyagramı](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Şekil 1 – araç Telemetri analizi çözüm mimarisi*

Bu çözüm hello aşağıdakileri içeren **Cortana Intelligence bileşenleri** ve bunların son tooend tümleştirme genişletilebileceğini gösterir:

* **Olay hub'ları** Azure'da araç telemetri olayları milyonlarca alma için.
* **Akış analizi** araç sistem üzerinde gerçek zamanlı Öngörüler öğrenilmesi ve bu verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.
* **Machine Learning** anomali algılama gerçek zamanlı ve toplu toogain Tahmine dayalı Öngörüler işleme.
* **Hdınsight** ölçekte çevrelerini tootransform veriler
* **Veri Fabrikası** planlama, kaynak yönetimi ve izleme hello toplu işleme ardışık orchestration işler.
* **Power BI** gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano bu çözümü sunar.

Bu çözüm iki farklı erişen **veri kaynakları**: 

* **Benzetimli araç sinyalleri ve tanılama**: tanı bilgilerini ve toohello durumunu hello araç ve düzeni, zaman içinde belirli bir anda yürüten hello karşılık gelen sinyalleri bir araç telematik simulator yayar. 
* **Araç katalog**: Toplamıdır toomodel eşleme içeren bir başvuru veri kümesi.

