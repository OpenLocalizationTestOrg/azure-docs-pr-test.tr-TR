---
title: "aaaUnderstand Azure IOT Hub ileti biçimi | Microsoft Docs"
description: "Geliştirici Kılavuzu - descibes hello biçimi ve IOT hub'ı iletilerinin beklenen içerik."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Oluşturun ve IOT hub'ı iletileri okur

toosupport sorunsuz birlikte çalışabilirlik protokolleri üzerinden, IOT hub'ı tüm aygıt dönük protokoller için ortak bir ileti biçimi tanımlar. Bu ileti biçimi her ikisi için kullanılan [cihaz bulut] [ lnk-d2c] ve [bulut cihaz] [ lnk-c2d] iletileri. Bir [IOT hub'ı ileti] [ lnk-messaging] oluşur:

* Bir dizi *Sistem Özellikleri*. IOT hub'ı yorumlar veya ayarlayan özellikleri. Bu önceden belirlenmiş kümesidir.
* Bir dizi *uygulama özellikleri*. Uygulama hello dize özellikleri sözlüğü tanımlayabilir ve erişim, toodeserialize hello ileti gövdesi gerek kalmadan. IOT hub'ı hiçbir zaman bu özellikleri değiştirir.
* Donuk bir ikili gövdesi.

Özellik adları ve değerleri yalnızca ASCII alfasayısal karakterler içerebilirler, artı ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` olduğunda:

* Merhaba HTTP protokolünü kullanarak cihaz-bulut iletileri gönderir.
* Bulut cihaz iletileri gönderir.

Hakkında daha fazla bilgi için tooencode ve farklı protokoller kullanılarak gönderilen iletileri kod çözme bkz [Azure IOT SDK'ları][lnk-sdks].

Aşağıdaki tablonun hello hello kümesi IOT hub'ı iletileri Sistem özelliklerinde listelenir.

| Özellik | Açıklama |
| --- | --- |
| MessageID |İstek-yanıt desenler için kullanılan hello ileti için kullanıcı ayarlanabilir bir tanımlayıcı. Biçimi: Bir büyük küçük harf duyarlı dize (too128 karakter uzunluğunda) ASCII 7 bit alfasayısal karakter + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Sıra numarası |IOT hub'ı tooeach bulut aygıt iletisi tarafından atanan bir sayı (aygıt sırası benzersiz). |
| çok|Belirtilen bir hedef [bulut cihaz] [ lnk-c2d] iletileri. |
| ExpiryTimeUtc |Tarih ve saat iletisi süre sonu. |
| EnqueuedTime |Tarih ve saat hello [bulut cihaz] [ lnk-c2d] ileti IOT Hub tarafından alındı. |
| CorrelationId |Bir dize özelliği genellikle hello MessageID hello isteğinin, istek-yanıt desenleri içeren bir yanıt iletisi. |
| Kullanıcı Kimliği |Bir kimliği toospecify hello iletileri kökeni kullanılır. IOT Hub tarafından iletileri oluşturulduğunda, çok ayarlanır`{iot hub name}`. |
| ACK |Geri bildirim iletisi üreteci. Bu özellik selamlama iletisine hello tüketimini sonucunda bulut-cihaz iletilerini toorequest IOT hub'ı toogenerate geri bildirim iletileri hello aygıt tarafından kullanılıyor. Olası değerler: **hiçbiri** (varsayılan): hiçbir geri bildirim iletisi oluşturulur, **pozitif**: Selamlama iletisine tamamlanmışsa bir geri bildirim iletisi **negatif**: alma bir Selamlama iletisine süresi (veya en yüksek teslimat sayısı ulaşıldı varsa) hello aygıt tarafından tamamlandığı olmadan geri bildirim iletisi veya **tam**: pozitif ve negatif. Daha fazla bilgi için bkz: [ileti geri bildirim][lnk-feedback]. |
| ConnectionDeviceId |IOT Hub tarafından cihaz bulut iletilerini üzerinde ayarlanmış bir kimliği. Merhaba içerdiği **DeviceID** selamlama iletisine gönderilen hello cihazın. |
| ConnectionDeviceGenerationId |IOT Hub tarafından cihaz bulut iletilerini üzerinde ayarlanmış bir kimliği. Merhaba içerdiği **Generationıd** (göre [aygıt kimlik özellikleri][lnk-device-properties]) selamlama iletisine gönderilen hello cihazın. |
| ConnectionAuthMethod |IOT Hub tarafından cihaz bulut iletilerini üzerinde ayarlanmış bir kimlik doğrulama yöntemi. Bu özellik hello kimlik doğrulaması kullanılan yöntemi tooauthenticate hello cihaz hello ileti gönderme hakkında bilgi içerir. Daha fazla bilgi için bkz: [aygıt toocloud yanıltma][lnk-antispoofing]. |

## <a name="message-size"></a>İleti boyutu

IOT hub'ı yalnızca hello gerçek yükü dikkate Protokolü belirsiz şekilde, ileti boyutu ölçer. Merhaba boyutunu bayt cinsinden hello aşağıdaki hello toplamı olarak hesaplanır:

* bayt Hello Gövde boyutu.
* Merhaba ileti sistemi özelliklerini tüm hello değerlerinin bayt Hello boyutu.
* Merhaba boyutunu bayt cinsinden tüm kullanıcı özellik adları ve değerleri.

Dolayısıyla hello dizeleri Hello uzunluğu hello boyutunu bayt cinsinden eşittir özellik adları ve değerleri sınırlı tooASCII karakterler olur.

## <a name="next-steps"></a>Sonraki adımlar

IOT Hub'ındaki ileti boyutu sınırları hakkında daha fazla bilgi için bkz: [IOT hub'ı kotalar ve azaltma][lnk-quotas].

toolearn nasıl toocreate ve okuma IOT hub'ı iletileri çeşitli programlama dillerinde, bkz: Merhaba [başlama] [ lnk-get-started] öğreticileri.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
