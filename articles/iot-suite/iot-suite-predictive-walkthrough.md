---
title: "aaaPredictive bakımda gezinme | Microsoft Docs"
description: "İzlenecek yol hello Azure IOT Tahmine dayalı bakım çözümü önceden yapılandırılmış."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Önceden yapılandırılmış tahmine dayalı bakım çözümünde gezinme

Merhaba önceden yapılandırılmış Tahmine dayalı bakım çözümü, bir hata olasılıkla toooccur olduğu hello noktayı tahmin eden iş senaryosu için uçtan uca çözümüdür. Bu önceden yapılandırılmış çözümü, bakım iyileştirmesi gibi etkinlikler için proaktif olarak kullanabilirsiniz. Merhaba çözüm IOT Hub, akış analizi gibi önemli Azure IOT paketi hizmetlerini birleştirir ve bir [Azure Machine Learning] [ lnk-machine-learning] çalışma. Bu çalışma alanı, ortak örnek veri kümesi, toopredict hello uçak motorunun kalan kullanım ömrü (RUL) dayalı bir modeli içerir. Merhaba çözüm tam, tooplan için bir başlangıç noktası olarak hello IOT iş senaryosu uygular ve belirli iş gereksinimlerinizi karşılayan bir çözüm uygulayabilirsiniz.

## <a name="logical-architecture"></a>Mantıksal mimari

Diyagram aşağıdaki hello hello hello önceden yapılandırılmış çözümün mantıksal bileşenlerinin ana hatların vermektedir:

![][img-architecture]

Merhaba önceden yapılandırılmış çözüm dağıtıldığı hello bölgede sağlanan Azure Hizmetleri mavi Hello öğelerdir. Merhaba önceden yapılandırılmış çözüm dağıtabileceğiniz bölgeler Hello listesini görüntüler üzerinde hello [sağlama sayfası][lnk-azureiotsuite].

Merhaba yeşil öğe uçak motorunu temsil eden sanal cihazdır. Bu sanal cihazlar bölümden hello içinde hakkında daha fazla bilgi edinebilirsiniz.

Merhaba gri öğeler uygulayan bileşenleri temsil eden *Aygıt Yönetimi* özellikleri. Merhaba sürümü geçerli hello önceden yapılandırılmış Tahmine dayalı bakım çözümü bu kaynakları sağlamak değil. Aygıt Yönetimi hakkında daha fazla toolearn başvuran toohello [Uzaktan izleme önceden yapılandırılmış çözümü][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Sanal cihazlar

Merhaba önceden yapılandırılmış çözümde sanal cihaz uçak motorunu temsil eder. Merhaba çözüm tooa tek uçakla eşlenen iki alt yapısıyla sağlanır. Her motor dört tür telemetri yayar: algılayıcı 9, algılayıcı 11, algılayıcı 14 ve algılayıcı 15 hello Machine Learning modeli toocalculate hello RUL hello altyapısı için gereken hello verileri sağlar. Her sanal cihaz telemetri iletilerini tooIoT Hub aşağıdaki hello gönderir:

*Döngü sayısı*. Bir döngü, iki ile on saat arasındaki bir süreyle tamamlanmış uçuşu temsil eder. Merhaba uçuş sırasında telemetri verilerini yarım saatte yakalanır.

*Telemetri*. Motor özniteliklerini temsil eden dört algılayıcı vardır. Merhaba algılayıcılar genel olarak algılayıcı 9, algılayıcı 11, algılayıcı 14 ve algılayıcı 15 olarak etiketlenir. Bu dört algılayıcılar hello RUL modelinden yararlı sonuçlar yeterli tooobtain telemetri temsil eder. Merhaba önceden yapılandırılmış çözümde kullanılan hello model, gerçek motor algılayıcı verilerinin bulunduğu ortak bir veri kümesi oluşturulur. Merhaba hello model hello özgün veri kümesinden nasıl oluşturulduğu hakkında daha fazla bilgi için bkz: [Cortana Intelligence Gallery Tahmine dayalı bakım şablonu][lnk-cortana-analytics].

Benzetimli hello cihazlar hello çözümde hello IOT hub'dan gönderilen komutları aşağıdaki hello işleyebilir:

| Komut | Açıklama |
| --- | --- |
| StartTelemetry |Denetimleri hello benzetim durumunu hello.<br/>Telemetri göndermesini başlatır hello cihaz |
| StopTelemetry |Denetimleri hello benzetim durumunu hello.<br/>Cihazın telemetri göndermesini durdurur hello |

IoT hub'ı cihaz komut bildirim sağlar.

## <a name="azure-stream-analytics-job"></a>Azure Stream Analytics işi

**İş: Telemetri** iki durumu kullanarak hello gelen cihaz telemetrisi akışını çalışır:

* Merhaba ilk hello cihazlardan tüm telemetriyi seçer ve bu verileri tooblob depolama gönderir. Buradan, hello web uygulamasında görselleştirilen.
* Merhaba ikinci hesaplar ortalama algılayıcı değerlerini iki dakikalık kayan pencere üzerinde ve hello olay hub'ı tooan aracılığıyla bu verileri gönderir **olay işlemcisi**.

## <a name="event-processor"></a>Olay işlemcisi
Merhaba **olay işleyicisi konağı** bir Azure Web işi çalıştırır. Merhaba **olay işlemcisi** tamamlanmış döngünün hello ortalama algılayıcı değerlerini alır. Ardından, bu değerleri tooan motor için RUL eğitilen model toocalculate hello sunan API geçirir. Merhaba API hello çözümün bir parçası sağlanan bir Machine Learning çalışma alanı tarafından sunulur.

## <a name="machine-learning"></a>Machine Learning
Merhaba Machine Learning bileşen gerçek uçak motorlarından toplanan verileri türetilmiş bir modeli kullanır. Hello hello kutucuğu toohello Machine Learning çalışma alanına gidin [azureiotsuite.com] [ lnk-azureiotsuite] sağlanan çözümünüz için sayfa. Merhaba çözüm hello olduğunda hello döşeme kullanılabilir **hazır** durumu.


## <a name="next-steps"></a>Sonraki adımlar
Merhaba anahtar hello önceden yapılandırılmış Tahmine dayalı bakım çözümü bileşenlerinin gördüğünüze göre toocustomize isteyebilirsiniz. Bkz. [Önceden yapılandırılmış çözümleri özelleştirme kılavuzu][lnk-customize].

Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [IoT Paketi için sık sorulan sorular][lnk-faq]
* [Merhaba IOT güvenlikten plan][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/