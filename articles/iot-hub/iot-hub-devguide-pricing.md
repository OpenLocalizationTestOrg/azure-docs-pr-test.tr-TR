---
title: "Azure IOT Hub aaaUnderstand fiyatlandırma | Microsoft Docs"
description: "Geliştirici Kılavuzu - ölçüm ve de dahil olmak üzere IOT Hub ile works fiyatlandırma örnekler nasıl çalıştığı hakkında bilgi."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Azure IOT Hub ile fiyatlandırma bilgileri

[Azure IOT Hub ile fiyatlandırma] [ lnk-pricing] farklı SKU'ları ve IOT Hub için fiyatlandırma hello genel bilgiler sağlar. Bu makale, çeşitli IOT hub'ı işlevler olarak ölçülen hello IOT Hub tarafından nasıl iletileri hakkında ek bilgi içerir.

## <a name="charges-per-operation"></a>İşlem başına ücret

| İşlem | Faturalama bilgileri | 
| --------- | ------------------- |
| Kimlik kayıt defteri işlemleri <br/> (oluşturma, alma, liste, Güncelleştir, Sil) | Ücret işlenmedi. |
| Cihazdan buluta iletiler | Başarıyla gönderilen iletileri 4 KB öbekler giriş üzerinde IOT Hub'ına örneğin 6-KB ileti 2 mesaj doludur sizden ücret kesilir. |
| Bulut-cihaz iletilerini | Başarıyla gönderilen iletileri 4 KB öbekler ücretlendirilen, 6-KB ileti 2 mesaj örneğin doludur. |
| Dosya yüklemeleri | Dosya aktarımı tooAzure depolama IOT Hub tarafından ölçülen değil. Dosya aktarımı başlatma ve tamamlanma iletilerini 4 KB artımlarla ölçülen messaged gibi ücretlendirilirsiniz. Örneğin, 10 MB'lık dosyası aktarma toplama toohello maliyeti Azure depolama iki iletilerinde ücret kesilir. |
| Doğrudan yöntemler | Başarılı yöntem isteği 4 KB öbekler ücretlendirilen, boş olmayan gövdeleri yanıtları 4 KB ek iletiler sizden ücret kesilir. İstekleri toodisconnected aygıtları 4 KB öbekler iletilerinde olarak ücretlendirilirsiniz. Örneği için hiçbir gövde ile bir yanıt hello aygıttan sonuçlanan 6-KB gövde yöntemiyle seçili iki ileti; bir 1 KB yanıt hello aygıttan sonuçlanan 6-KB gövde yöntemiyle hello istek için iki ileti artı hello yanıtı için başka bir ileti olarak ücretlendirilir. |
| Cihaz ikizi okumaları | Cihaz çifti hello cihaz ve hello çözüm arka uç 512 baytlık öbekleri iletilerinde olarak ücretlendirilirsiniz okur. Örneğin, 6-KB cihaz çifti okuma 12 iletileri ücret kesilir. |
| Cihaz çifti güncelleştirmeleri (etiketleri ve özellikleri) | Cihaz çifti güncelleştirmeleri hello cihaz ve hello aygıttan 512 baytlık öbekleri iletilerinde olarak ücretlendirilirsiniz. Örneğin, 6-KB cihaz çifti okuma 12 iletileri ücret kesilir. |
| Cihaz çifti sorguları | Sorguları iletileri Merhaba sonuç boyutunu 512 baytlık parçalar bağlı olarak sizden ücret kesilir. |
| İş işlemleri <br/> (oluşturma, güncelleştirme, listeleme, silme) | Ücret işlenmedi. |
| İşlerini aygıt başına işlem | İşlerini işlemleri (örneğin, cihaz çifti güncelleştirmeleri ve yöntemleri) normal olarak sizden ücret kesilir. Örneğin, 1 KB isteklerini ve yanıtlarını gövdesi boş olan 1000 yöntem çağrılarını sonuçta bir işi 1000 iletileri ücretlendirilir. |

> [!NOTE]
> Tüm boyutları hello yükü boyutu (Protokolü çerçeveleme göz ardı edilir) bayt dikkate hesaplanır. (Olan özellikleri ve gövde) iletileri durumunda hello boyutu bir protokol belirsiz şekilde hello açıklandığı gibi hesaplanır [IOT Hub Geliştirici Kılavuzu Mesajlaşma][lnk-message-size].

## <a name="example-1"></a>Örnek #1

Bir aygıt dakika tooIoT sonra Azure akış analizi tarafından okunur Hub başına tek bir 1 KB cihaz bulut ileti gönderir. Merhaba çözüm arka ucu bir yöntemle (512 baytlık yükü) hello aygıtta her on dakika tootrigger belirli bir eylemi çağırır. Merhaba aygıt 200 bayt sonucunu toohello yöntemiyle yanıt verir.

Merhaba aygıt tüketir 1 ileti * 60 dakika * 24 saat = 1440 iletileri hello cihaz bulut iletilerini ve 2 istek ve yanıt için günlük * 6 kereye saat başına * 24 saat = 288 iletileri 1728 iletileri gün başına toplam hello yöntemleri için.

## <a name="example-2"></a>Örnek #2

Bir aygıt her saat bir 100 KB cihaz bulut iletisi gönderir. Ayrıca, cihaz çifti 4 saatte bir 1 KB yükü ile güncelleştirir. Merhaba çözüm arka son, günde bir kez, okumalar hello 14-KB cihaz çifti ve 512 baytlık yüklerini toochange yapılandırmaları ile güncelleştirir.

Merhaba aygıt tüketir 25 (100KB / 4KB) iletileri * cihaz bulut iletilerini artı 1 ileti 24 saat * 6 kereye günde cihaz çifti güncelleştirmeleri için günde 156 iletilerin toplam.
Merhaba çözüm arka ucu 28 iletileri (14 KB/0,5 KB) tooread hello cihaz çifti artı 1 ileti tooupdate kullanır, 29 iletilerin toplam.

Toplam, hello cihaz ve hello çözüm arka ucu günde 185 iletileri kullanabilir.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
