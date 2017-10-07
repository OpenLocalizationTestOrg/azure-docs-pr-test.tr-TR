---
title: "aaaAzure IOT hub'a genel bakış | Microsoft Docs"
description: "Hello Azure IOT Hub hizmetine genel bakış: IOT Hub, cihaz bağlantısı, nesnelerin interneti iletişim düzenleri, ağ geçitleri ve hello hizmet destekli iletişim düzeni nedir"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Hello Azure IOT Hub hizmetine genel bakış

TooAzure IOT Hub'na Hoş Geldiniz. Bu makale Azure IOT Hub genel bir bakış sağlar ve bu hizmet tooimplement bir nesnelerin interneti (IOT) çözümü neden kullanmanız gerektiğini açıklar. Azure IoT Hub, milyonlarca IoT cihazları ile bir çözüm arka ucu arasında güvenilir ve güvenli çift yönlü iletişimler sağlayan tam olarak yönetilen bir hizmettir. Azure IoT Hub:

* Tek yönlü mesajlaşma, dosya aktarımı ve request-reply metotları gibi cihazdan buluta ve buluttan cihaza iletişimi seçeneği sunar.
* Yerleşik bildirim temelli ileti yönlendirme tooother Azure hizmetleri sağlar.
* Cihaz meta verileri ve eşitlenmiş durum bilgileri için sorgulanabilir depolama sağlar.
* Cihaz başına güvenlik anahtarları veya X.509 sertifikaları kullanarak güvenli iletişim ve erişim denetimi olanağı sağlar.
* Cihaz bağlantısı ve cihaz kimlik yönetimi etkinlikleri için kapsamlı izleme sağlar.
* Merhaba en popüler diller ve platformlar için cihaz kitaplıklarını içerir.

Merhaba makale [karşılaştırma, IOT Hub ve Event Hubs] [ lnk-compare] hello bu iki hizmet arasındaki önemli farklılıkları açıklar ve IOT çözümlerinizde IOT hub'ı kullanmanın yararları hello vurgular.

IOT çözümünüzü güvenli Azure ve IOT hub'ı nasıl yardımcı daha fazla bilgi için bkz: [plan hello nesnelerin interneti güvenlikten][lnk-security-ground-up].

![Nesnelerin interneti çözümünde bulut ağ geçidi olarak Azure IoT Hub][img-architecture]

> [!NOTE]
> IOT mimarisinin ayrıntılı incelemesi için bkz: Merhaba [Microsoft Azure IOT başvuru mimarisi][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>IoT cihaz bağlantısı zorlukları

IOT Hub ve hello cihaz kitaplıkları toomeet hello zorluklar nasıl yardımcı tooreliably ve güvenli bir şekilde aygıtları toohello çözüm arka ucu bağlanın. IoT cihazları:

* İnsan olan bir operatörü bulunmayan ve genellikle katıştırılmış sistemlerdir.
* Fiziksel erişimin pahalı olduğu uzak konumlarda olabilir.
* Yalnızca hello çözüm arka ucu aracılığıyla erişilebilir.
* Sınırlı güç ve işleme kaynaklarına sahip olabilir.
* Aralıklı, yavaş veya pahalı bir ağ bağlantısına sahip olabilir.
* Toouse mülkiyete ait, özel veya sektöre özgü uygulama protokolleri gerekebilir.
* Büyük bir popüler donanım ve yazılım platformu kümesi kullanılarak oluşturulabilir.

Ayrıca yukarıdaki toohello gereksinimler, tüm IOT çözümlerinin de ölçek, güvenlik ve güvenilirlik de sunması gerekir. web kapsayıcıları ve mesajlaşma aracıları gibi geleneksel teknolojiler kullandığınızda hello elde edilen bağlantı gereksinimleri zor ve zaman alıcı tooimplement kümesidir.

## <a name="why-use-azure-iot-hub"></a>Azure IoT Hub neden kullanılır?

Tooa zengin ayrıca kümesi [cihaz bulut] [ lnk-d2c-guidance] ve [bulut cihaz] [ lnk-c2d-guidance] iletişim seçenekleri, Mesajlaşma, içeren dosya aktarımları ve istek-yanıt yöntemleri, Azure IOT Hub adresleri yolları aşağıdaki hello cihaz bağlantısı zorlukları hello:

* **Cihaz çiftleri**. [Cihaz çiftlerini][lnk-twins] kullanarak depolama, eşitleme, cihaz meta verilerini ve durum bilgisini sorgulama işlemlerini yapabiliriniz. Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir. IOT Hub cihaz çifti tooIoT Hub bağlanmak her aygıt için devam ettirir.

* **Cihaz başına kimlik doğrulaması ve güvenli bağlantı**. Her bir cihaza kendi sağlayabilirsiniz [güvenlik anahtarı] [ lnk-devguide-security] tooenable, tooconnect tooIoT Hub. Merhaba [IOT Hub kimlik kayıt defteri] [ lnk-devguide-identityregistry] cihaz kimliklerini ve anahtarlarını bir çözümün içinde depolar. Bir çözüm arka ucu tek cihazlara tooallow ekleyebilir veya listeleri tooenable tam kontrole cihaz erişimini engellemek.

* **Rota cihaz-bulut iletileri bildirim temelli kurallara göre tooAzure Hizmetleri**. IOT hub'ı yollarını burada hub'ınızın cihaz bulut iletilerini gönderir yönlendirme kuralları toocontrol üzerinde dayalı, toodefine ileti sağlar. Yönlendirme kuralları, toowrite herhangi bir kod gerektirmez ve özel sonrası alım message dağıtıcıları hello yerini alabilir.

* **Cihaz bağlantısı işlemlerini izleme**. Cihaz kimlik yönetimi işlemleri ve cihaz bağlantısı etkinlikleri hakkında ayrıntılı işlem günlükleri alabilirsiniz. Yanlış kimlik bilgileriyle tooconnect deneyin cihazları çok sık ileti göndermeye veya tüm bulut-cihaz iletilerini reddetmeye gibi IOT çözüm tooidentify bağlantı sorunları, bu izleme yeteneği sağlar.

* **Kapsamlı bir cihaz kitaplıkları kümesi**. [Azure IoT cihaz SDK'ları][lnk-device-sdks], Linux dağıtımları, Windows ve gerçek zamanlı işletim sistemlerinin çoğu için C gibi çeşitli diller ve platformlarda kullanılabilir ve desteklenir. Azure IoT cihaz SDK'ları C#, Java ve JavaScript gibi yönetilen dilleri de destekler.

* **IoT protokolleri ve genişletilebilirlik**. Çözümünüzü hello cihaz kitaplıklarını kullanamazsa IOT Hub cihazları toonatively kullanım hello MQTT v3.1.1, HTTP 1.1 veya AMQP 1.0 protokollerini etkinleştiren bir genel Protokolü kullanıma sunar. IOT hub'ı toosupport tarafından özel protokoller için aynı zamanda genişletebilirsiniz:

  * Bir alan ağ geçidi ile oluşturma [Azure IOT kenar] [ lnk-iot-edge] IOT Hub tarafından anlaşılan üç protokolden hello ', özel protokol tooone dönüştürür.
  * Özelleştirme hello [Azure IOT protokolü ağ geçidini][protocol-gateway], hello bulutta çalışan açık kaynaklı bir bileşen.

* **Ölçek**. Azure IOT Hub, eş zamanlı cihazı toomillions ve saniye başına milyonlarca olayı ölçeklendirir.

## <a name="gateways"></a>Ağ geçitleri

Bir IOT çözümündeki bir ağ geçidi genellikle ya da olduğu bir [protokol ağ geçidi] [ lnk-iotedge] hello buluta dağıtılan veya [alan ağ geçidi] [ lnk-field-gateway] diğer bir deyişle Yerel cihazlarınızı dağıtılmış. Bir protokol ağ geçidi protokol çevirisi, örneğin MQTT tooAMQP gerçekleştirir. Bir alan ağ geçidi hello kenarda analiz çalıştırmak, zamana duyarlı kararlar tooreduce gecikme, cihaz Yönetimi Hizmetleri sağlayabilecek, güvenlik ve gizlilik kısıtlamaları getirebilecek ve de protokol çevirileri gerçekleştirebilir. Her iki ağ geçidi de cihazlarınız ve IoT hub'ınız arasında aracı görevi yapar.

Bir alan ağ geçidi, çözümünüzde erişim ve bilgi akışını yönetmede genellikle etkin bir rol oynadığından, basit bir trafik yönlendirme cihazından (bir ağ adresi çeviri cihazı veya güvenlik duvarı gibi) farklıdır.

Bir çözümde hem protokol hem de alan geçitleri olabilir.

## <a name="how-does-iot-hub-work"></a>IoT Hub nasıl çalışır?

Azure IOT hub'ı uygulayan hello [hizmet destekli iletişim] [ lnk-service-assisted-pattern] aygıtlarınızın ve çözümünüzü arasındaki düzeni toomediate hello etkileşimler son yedekleme. Merhaba hizmet destekli iletişim tooestablish güvenilir, çift yönlü iletişim yolları IOT Hub ve güvenilmeyen fiziksel alanda dağıtılan özel amaçlı cihazlar gibi bir denetim sistemi arasında hedefidir. Merhaba düzeni ilkeler aşağıdaki hello oluşturur:

* Güvenlik diğer tüm işlevlerden önceliklidir.

* Cihazlar istenmemiş ağ bilgilerini kabul etmez. Bir cihaz tüm bağlantıları kurar ve yalnızca giden bağlantı şeklinde yönlendirir. Aygıt tooreceive hello çözüm arka ucu komuttan, hello aygıt düzenli olarak bağlantı toocheck tüm bekleyen komutları tooprocess için başlatması gerekir.

* Aygıtları yalnızca bağlayın tooor bunlar eşlenen, IOT Hub gibi yollar toowell bilinen hizmetleri oluşturun.

* Merhaba iletişim yolunun veya cihaz ile ağ geçidi cihazını ve hizmetini arasında hello uygulama protokol katmanında güvenli hale getirilir.

* Sistem düzeyinde yetkilendirme ve kimlik doğrulama cihaz başına kimliği temel alır. Bunlar erişim kimlik bilgilerini ve izinleri neredeyse anında iptal edilebilir hale getirir.

* Düzensiz aralıklarla hataya son toopower veya bağlantı sorunları bağlanan cihazlar için çift yönlü iletişim komutların ve cihaz bildirimlerinin bir cihazın tooreceive bağlanana kadar tutarak barındırılması bunları. IOT Hub, gönderdiği hello komutlar için cihaza özgü sıraları tutar.

* Uygulama yük verilerinin ayrı ayrı ağ geçitleri tooa belirli hizmeti aracılığıyla korumalı geçiş için güvenlik altına alınır.

Merhaba mobil sektörü hello hizmet destekli iletişim düzenini devasa ölçüde tooimplement anında iletme bildirimi Hizmetleri gibi kullandı [Windows anında bildirim Hizmetleri][lnk-wns], [Google Cloud Messaging'i][lnk-google-messaging], ve [Apple anında iletilen bildirim servisi][lnk-apple-push].

IoT Hub, ExpressRoute'un ortak eşleme yolundan desteklenmez.

## <a name="next-steps"></a>Sonraki adımlar

nasıl toosend iletileri bir aygıttan ve IOT hub'ı yanı sıra nasıl tooconfigure iletiyi yönlendirir, alma toolearn bkz [IOT Hub ile iletileri almasına ve göndermesine][lnk-send-messages].

IOT Hub, tooremotely yönetmek, yapılandırmak ve aygıtlarınızın güncelleştirmek için standartlara dayalı aygıt yönetimi sağlar nasıl toolearn bkz [cihaz yönetimine genel bakış IOT Hub ile][lnk-device-management].

çok çeşitli cihaz donanım platformları ve işletim sistemleri tooimplement istemci uygulamaları, hello Azure IOT cihaz SDK'ları kullanabilirsiniz. Merhaba cihaz SDK'ları telemetri tooan IOT hub ve alma bulut cihaza iletileri gönderme kolaylaştırmak kitaplıkları içerir. Merhaba cihaz SDK'ları kullandığınızda IOT Hub ile çeşitli ağ protokolleri toocommunicate seçebilirsiniz. toolearn daha, hello fazla [cihaz SDK'ları hakkında bilgi][lnk-device-sdks].

biraz kod yazmaya ve bazı örnekler çalıştıran başlatılan tooget bkz hello [IOT Hub ile çalışmaya başlama] [ lnk-get-started] Öğreticisi.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Hizmet Destekli İletişim, Clemens Vasters'ın blog yazısı"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
