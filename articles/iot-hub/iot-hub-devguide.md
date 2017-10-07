---
title: "Azure IOT Hub için aaaDeveloper Kılavuzu | Microsoft Docs"
description: "Hello Azure IOT Hub Geliştirici Kılavuzu uç noktaları, güvenlik, hello kimlik kayıt defteri, cihaz yönetimi, doğrudan yöntemleri, cihaz çiftlerini, dosya yüklemeleri, işleri, hello IOT hub'ı sorgu dili ve mesajlaşma tartışmalarını içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Azure IOT Hub Geliştirici Kılavuzu

Azure IOT Hub, milyonlarca cihaza arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen hizmet etkinleştirin ve bir çözüm arka ucu ' dir.

Azure IOT Hub ile sağlar:

* Cihaz başına güvenlik kimlik bilgileri kullanılarak güvenli iletişim ve erişim denetimi.
* Birden çok cihaz Bulut ve bulut-cihaz hiper ölçekli iletişim seçenekleri.
* Sorgulanabilir depolama aygıt başına durum bilgilerini ve meta verileri.
* Merhaba en popüler diller ve platformlar için cihaz kitaplıklarını ile kolay cihaz bağlantısı.

Bu IOT Hub geliştirici kılavuzu makaleleri aşağıdaki hello içerir:

* [Cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] cihaz bulut iletilerini, cihaz çifti'nın bildirilen özellikleri ve karşıya dosya yükleme arasında seçtiğiniz yardımcı olur.
* [Bulut-cihaz iletişimi Kılavuzu] [ lnk-c2d-guidance] doğrudan yöntemleri, cihaz çifti'nın istenen özellikleri ve bulut-cihaz iletilerini arasında seçtiğiniz yardımcı olur.
* [Cihaz Bulut ve bulut cihaz IOT Hub ile Mesajlaşma] [ devguide-messaging] IOT hub'ı gösteren hello Mesajlaşma özellikleri (cihaz Bulut ve bulut-cihaz) açıklar.
  * [Cihaz bulut iletilerini tooIoT Hub Gönder][devguide-messages-d2c].
  * [Merhaba yerleşik uç noktasından cihaz bulut iletilerini okumanızı][devguide-builtin].
  * [Özel uç noktaları ve yönlendirme kuralları için cihaz bulut iletilerini kullanmak][devguide-custom].
  * [IOT Hub'ından bulut-cihaz iletilerini göndermek][devguide-messages-c2d].
  * [Oluşturun ve IOT hub'ı iletileri okumak][devguide-format].
* [Bir CİHAZDAN dosyaları karşıya yükleme] [ devguide-upload] aygıttan dosyaları karşıya nasıl yükleneceğini açıklar. Merhaba makale ayrıca bildirimleri hello karşıya yükleme işlemi gönderebilir hello gibi konular hakkında bilgi içerir.
* [IOT Hub cihaz kimliklerini yönetmek] [ devguide-identities] hangi bilgilerin açıklar her IOT hub'ın kimlik kayıt defteri depolarına ve nasıl erişmek ve değiştirebilirsiniz.
* [Erişim tooIoT Hub kontrol] [ devguide-security] hello güvenlik modeli kullanılan toogrant erişim tooIoT Hub işlevselliği cihazlar ve bulut bileşenleri için açıklar. Merhaba makale belirteçleri ve X.509 sertifikalarını ve erişim izni verebilir hello izinleri ayrıntılarını kullanma hakkında bilgi içerir.
* [Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanma] [ devguide-device-twins] hello açıklar *cihaz çifti* kullanıma sunan bir aygıt, aygıtla eşitleme gibi kavram ve hello işlevi çifti. Merhaba makale bir cihaz çiftine depolanır hello verileri hakkında bilgiler içerir.
* [Bir cihazda doğrudan bir yöntem çağırma] [ devguide-directmethods] hello yaşam döngüsünü nasıl tooinvoke yöntemleri arka uç uygulama ve tanıtıcı hello cihaza yöntemi aygıtınızda doğrudan hakkında bilgi doğrudan bir yöntem açıklar.
* [Zamanlama işlerini birden çok aygıta] [ devguide-jobs] işleri birden çok aygıta nasıl zamanlayabilirsiniz açıklar. Merhaba nasıl toosubmit işlerin makalede cihaz çifti kullanarak bir cihazı güncelleştirme doğrudan bir yöntem yürütülen görevleri gerçekleştirin. Ayrıca, nasıl tooquery hello işin durumunu açıklar.
* [Başvuru - iletişim protokolü seçin] [ devguide-protocol] IOT Hub cihaz iletişimi için destekler ve listeleri hello açık olması gereken bağlantı noktalarını hello iletişim protokolleri açıklar.
* [Başvuru - IOT Hub uç noktaları] [ devguide-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello. Merhaba ayrıca makalede IOT hub'ınıza ek uç noktaları oluşturabilirsiniz nasıl ve nasıl toouse bir alan ağ geçidi tooenable aygıtları bağlantı tooyour IOT Hub uç noktaları standart senaryolarda.
* [Başvuru - cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgu dili] [ devguide-query] hub'ınızın cihaz çiftlerini ve işleri hakkında tooretrieve bilgileri sağlayan bu IOT hub'ı sorgu dili açıklar.
* [Başvuru - kotalar ve azaltma] [ devguide-quotas] hello IOT Hub hizmeti ve davranış almanız olasıdır toosee kota aştıklarında azaltma hello ayarlamak hello kotaları özetler.
* [Başvuru - fiyatlandırma] [ devguide-pricing] farklı SKU'ları ve IOT hub'ı ve IOT Hub tarafından nasıl çeşitli IOT hub'ı işlevler olarak ölçülen hello iletileri ile ilgili ayrıntılar için fiyatlandırma hakkında genel bilgiler sağlar.
* [Başvuru - cihazını ve hizmetini SDK'ları] [ devguide-sdks] listeleri hello Azure IOT SDK'ları toodevelop kullanabilirsiniz, IOT hub ile etkileşim hem cihaz hem de hizmet uygulamaları. Merhaba makale bağlantılar tooonline API belgelerine içerir.
* [Başvuru - IOT Hub MQTT Destek] [ devguide-mqtt] hello MQTT Protokolü IOT hub'ı nasıl desteklediği hakkında ayrıntılı bilgiler sağlar. Merhaba makale hello MQTT Protokolü yerleşik toohello Azure IOT SDK'ları hello desteğini açıklar ve hello MQTT protokolü kullanarak doğrudan hakkında bilgi sağlar.
* [Sözlük] [ devguide-glossary] ortak IOT Hub ile ilgili terimlerin bir listesi.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
