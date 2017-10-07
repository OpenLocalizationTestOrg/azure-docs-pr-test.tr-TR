---
title: "aaaSecure nesnelerin interneti dağıtımınızı | Microsoft Docs"
description: "Bu makale ayrıntıları nasıl toosecure IOT dağıtımınızı"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 95c23341-16b0-4954-b3f2-d2e82ab7b367
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: befba8f2009279c2217dcd3496d529139134ec01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-iot-deployment"></a>IoT dağıtımınızın güvenliğini sağlama
Bu makalede, hello Azure IOT tabanlı nesnelerin interneti (IOT) altyapısı güvenliğini sağlamak için hello sonraki ayrıntı düzeyini sağlar. Yapılandırma ve her bileşenin dağıtma tooimplementation düzey ayrıntıların bağlar. Karşılaştırmaları ve çeşitli rakip yöntemleri arasında seçenekleri de sağlar.

Hello Azure IOT dağıtımının güvenliğini sağlama üç güvenlik alanları aşağıdaki hello ayrılabilir:

* **Cihaz güvenliği**: hello joker dağıtılırken güvenliğini sağlama hello IOT cihaz.
* **Bağlantı güvenliği**: gizli ve yetkisiz değiştirmeye karşı kanıt hello IOT cihaz ve IOT hub'ı arasında aktarılan tüm verileri sağlama.
* **Bulut güvenlik**: aracılığıyla taşır ve hello bulutta depolanan toosecure verileri bir yol sağlayan.

![Üç güvenlik alanları][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Güvenli aygıt sağlama ve kimlik doğrulama
Hello Azure IOT paketi IOT cihazları iki yöntemden aşağıdaki hello tarafından güvenliğini sağlar:

* Merhaba IOT Hub ile Merhaba aygıt toocommunicate kullandığı her cihaz için benzersiz kimlik anahtarı (güvenlik belirteçleri) sağlayarak.
* Bir aygıt kullanarak [X.509 sertifikası] [ lnk-x509] ve anlamına gelir tooauthenticate hello aygıt toohello IOT hub'ı olarak özel anahtar. Bu kimlik doğrulama yöntemini bu hello sağlar hello cihazda özel anahtar olmayan bilinen hello cihaz dışında herhangi bir zamanda daha yüksek düzeyde güvenlik sağlar.

Merhaba güvenlik belirteci yöntemi hello simetrik anahtar tooeach çağrısı ilişkilendirerek hello aygıt tooIoT Hub tarafından yapılan her çağrı için kimlik doğrulaması sağlar. X.509 tabanlı kimlik doğrulama IOT cihaz hello TLS bağlantı kurulurken bir parçası olarak hello fiziksel katmanında olanak sağlar. Merhaba belirteç tabanlı güvenlik yöntemi, daha az güvenli bir desen hello X.509 olmadan kimlik doğrulaması kullanılabilir. Merhaba hello iki yöntemleri arasında seçim öncelikle toobe ve güvenli depolama hello aygıtta kullanılabilirliğini tarafından nasıl güvenli hello cihaz kimlik doğrulaması gerekiyor dikte edilir (toostore hello özel anahtarı güvenli bir şekilde).

## <a name="iot-hub-security-tokens"></a>IoT Hub güvenlik belirteçleri
IOT hub'ı anahtarları hello ağda gönderme güvenlik belirteçleri tooauthenticate aygıtlarını ve hizmetlerini tooavoid kullanır. Ayrıca, güvenlik belirteçlerini geçerlilik tarihi ve kapsam sınırlıdır. Azure IOT SDK'ları otomatik olarak özel bir yapılandırma gerektirmeden belirteçleri oluşturur. Bazı senaryolar ancak hello kullanıcı toogenerate gerektirir ve güvenlik belirteçlerini doğrudan kullanır. Bunlar, hello doğrudan hello MQTT, AMQP veya HTTP yüzeyleri kullanımını ya da hello uygulanmasını hello belirteci hizmeti deseninin içerir.

Aşağıdaki makaleleri hello hello yapısını hello güvenlik belirteci ve kullanım hakkında daha fazla ayrıntı bulunabilir:

* [Güvenlik belirteci yapısı][lnk-security-tokens]
* [SAS belirteci bir aygıt olarak kullanma][lnk-sas-tokens]

Her IOT hub'ı olan bir [kimlik kayıt defteri] [ lnk-identity-registry] kullanılan toocreate aygıt başına yürütülen bulut-cihaz iletilerini ve tooallow erişim toohello içeren bir kuyruk gibi hello hizmet kaynaklarında olabilir Aygıt'e yönelik uç noktalar. Merhaba IOT Hub kimlik kayıt defteri cihaz kimliklerini ve güvenlik anahtarları bir çözüm için güvenli depolama sağlar. Tek tek veya grup cihaz kimlikleri eklenebilir tooan izin listesi veya aygıt erişimi üzerinde tam denetimi etkinleştirme bir Engellenenler listesi. Merhaba Aşağıdaki makaleler daha fazla ayrıntı hello kimlik kayıt defteri ve desteklenen işlemler hello yapısını sağlar.

[IOT hub'ı destekleyen MQTT, AMQP ve HTTP gibi protokoller][lnk-protocols]. Bu protokollerin her kullanın hello IOT cihaz tooIoT Hub gelen güvenlik belirteçleri farklı:

* AMQP: SASL DÜZ ve AMQP talep tabanlı güvenlik ({policyName}@sas.root. { iothubName} hello durumda IOT hub düzeyindeki belirteçlerin; {DeviceID} belirteçleri aygıt kapsamlı durumunda).
* MQTT: Paket kullanır {DeviceID} hello {ClientID}, {IoThubhostname} BAĞLANMAK / {DeviceID} hello içinde **kullanıcıadı** alanı ve SAS belirteci hello **parola** alan.
* HTTP: Hello yetkilendirme istek üstbilgisinde geçerli belirtecidir.

IOT Hub kimlik kayıt defteri kullanılan tooconfigure cihaz başına güvenlik kimlik bilgileri olması ve erişim denetimi. Ancak, bir IOT Çözüm zaten önemli yatırımınız varsa bir [özel cihaz kimlik kayıt defteri ve/veya kimlik doğrulama düzeni][lnk-custom-auth], IOT Hub ile varolan altyapısıyla tümleştirilebilir bir belirteci hizmeti oluşturarak.

### <a name="x509-certificate-based-device-authentication"></a>X.509 cihaz sertifika tabanlı kimlik doğrulaması
Merhaba kullanımını bir [aygıt tabanlı X.509 sertifikası] [ lnk-protocols] ve ilişkili özel ve ortak anahtar çiftini hello fiziksel katmanında ek kimlik doğrulaması sağlar. Merhaba özel anahtarı hello aygıtı güvenli bir şekilde depolanır ve hello cihaz dışında bulunabilirlik değil. Merhaba X.509 sertifikası cihaz kimliği gibi hello aygıt hakkındaki bilgileri ve diğer kuruluş ayrıntıları içerir. Merhaba sertifikanın imzasını hello özel anahtarı kullanılarak oluşturulur.

Üst düzey cihaz sağlama akışı:

* Bir tanımlayıcı tooa fiziksel aygıt – cihaz kimliği ve/veya üretim veya commissioning aygıt sırasında X.509 sertifikası ilişkili toohello aygıt ilişkilendirin.
* IOT hub – cihaz kimliği ve ilişkili aygıt bilgileri hello IOT Hub kimlik kayıt defteri karşılık gelen bir kimlik giriş oluşturun.
* X.509 sertifika parmak izi IOT Hub kimlik kayıt defterinde kaybedilebilir.

### <a name="root-certificate-on-device"></a>Cihaz üzerinde kök sertifikası
IOT Hub ile güvenli TLS bağlantı kurulurken hello IOT cihaz IOT Hub'ın hello cihaz SDK'sı parçası olan bir kök sertifikayı kullanarak doğrular. Merhaba C istemci SDK hello sertifika hello klasörü altında bulunan "\\c\\sertifikaları" Merhaba hello depo kökündeki altında. Bu kök sertifikaları uzun süreli olmakla birlikte, bunlar hala dolabilir veya iptal edilebilir. Varsa hello sertifika hello aygıtta hello güncelleştirme hiçbir şekilde aygıt mümkün olmayabilir toosubsequently toohello IOT hub'ı (veya diğer herhangi bir bulut hizmeti) bağlayın. Merhaba IOT cihaz dağıtıldıktan sonra anlamına gelir tooupdate hello kök sertifikaya sahip etkili bir şekilde Bu riskin azaltılmasına.

## <a name="securing-hello-connection"></a>Merhaba bağlantı güvenliğini sağlama
Internet bağlantısı hello IOT cihaz IOT hub'ı arasındaki hello Aktarım Katmanı Güvenliği (TLS) standardını kullanarak güvenlik altına alınır. Azure IOT destekler [TLS 1.2][lnk-tls12], TLS 1.1 ve TLS 1.0, bu sırada. TLS 1.0 desteği yalnızca geriye dönük uyumluluk için sağlanır. Merhaba en yüksek güvenliği sağlar gerektiğinden toouse TLS 1.2 önerilir.

Azure IOT paketi şifre paketleri, bu sırada aşağıdaki hello destekler.

| Şifre paketi | uzunluğu |
| --- | --- |
| TLS\_ECDHE\_RSA\_ile\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. 7680 bit RSA) FS |256 |
| TLS\_ECDHE\_RSA\_ile\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. 3072 bit RSA) FS |128 |
| TLS\_ECDHE\_RSA\_ile\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. 7680 bit RSA) FS |256 |
| TLS\_ECDHE\_RSA\_ile\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. 3072 bit RSA) FS |128 |
| TLS\_RSA\_ile\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_ile\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_ile\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_ile\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_ile\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_ile\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Merhaba bulut güvenliğini sağlama
Azure IOT Hub verir tanımını [erişim denetimi ilkeleri] [ lnk-protocols] her güvenlik anahtarı için. İzinleri toogrant erişim tooeach IOT Hub'ın uç noktalar kümesi aşağıdaki hello kullanır. İzinleri IOT hub'ı işlevselliğine bağlı hello erişim tooan sınırlayın.

* **RegistryRead**. Okuma erişimi toohello kimlik kayıt defteri verir. Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry].
* **RegistryReadWrite**. Verir okuma ve yazma erişimi toohello kimlik kayıt defteri. Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry].
* **ServiceConnect**. Verir toocloud hizmet dönük iletişim ve uç nokta izleme erişin. Örneğin, izin tooback uç bulut Hizmetleri tooreceive cihaz bulut iletilerini, bulut cihaza iletileri gönderme ve alma hello teslim alındı bildirimleri karşılık gelen verir.
* **DeviceConnect**. Verir toodevice'te Uç noktalara erişebilirsiniz. Örneğin, toosend cihaz bulut iletilerini izin verir ve bulut-cihaz iletilerini. Bu izin, cihazlar tarafından kullanılır.

İki yolu tooobtain vardır **DeviceConnect** IOT Hub ile izinlerle [güvenlik belirteçleri][lnk-sas-tokens]: cihaz kimliği anahtar veya bir paylaşılan erişim anahtarı kullanarak. Ayrıca, önemli toonote olan tüm işlevlere aygıtlardan erişilebilir uç öneki ile tasarım tarafından sunulan `/devices/{deviceId}`.

[Hizmet bileşenleri yalnızca güvenlik belirteçleri oluşturmak] [ lnk-service-tokens] paylaşılan erişim ilkeleri hello uygun izinleri verme kullanma.

Azure IOT Hub ve hello çözümün parçası olabilecek diğer hizmetler hello Azure Active Directory kullanarak kullanıcı yönetimi izin verir.

Azure IOT Hub tarafından alınan verilerin çeşitli Azure akış analizi ve Azure blob depolama gibi hizmetler tarafından kullanılabilecek. Bu hizmetler yönetim erişimi sağlar. Bu hizmetleri ve aşağıdaki kullanılabilir seçenekler hakkında daha fazlasını okuyun:

* [Azure Cosmos DB][lnk-docdb]: hello cihazlar için meta verileri yönetir yarı yapılandırılmış veriler için ölçeklenebilir, tam olarak dizine veritabanı hizmeti, öznitelikler, yapılandırma ve güvenlik özellikleri gibi sağlamanız. Cosmos DB yüksek performanslı ve yüksek verimlilik işleme, veri ve zengin bir SQL sorgu arabirimi şema belirsiz dizin sunar.
* [Azure Stream Analytics][lnk-asa]: Gerçek Zamanlı Akış, toorapidly sağlayan hello bulutta işleme geliştirmek ve düşük maliyetli analytics bir çözüm toouncover gerçek zamanlı Öngörüler cihazlar, algılayıcılar, üzerinden dağıtma Altyapı ve uygulamaları. Bu tam olarak yönetilen hizmet Hello verileri, yüksek performans, düşük gecikme süresi ve dayanıklılık hala elde ederken tooany birim ölçeklendirebilirsiniz.
* [Azure uygulama hizmetleri][lnk-appservices]: bir bulut platformu toobuild güçlü web ve herhangi bir yere; toodata bağlanan mobil uygulamalar hello Bulut veya şirket içi. iOS, Android ve Windows için ilgi çekici mobil uygulamalar oluşturun. Yazılımınızda hizmet (SaaS) ve kurumsal bulut tabanlı hizmetlerin Giden kutusu bağlantı toodozens ile uygulamaları ve kurumsal uygulamaları tümleştirin. Sık kullanılan dil ve IDE kodda (.NET, Node.js, PHP, Python veya Java) toobuild web uygulamaları ve API'ları zamankinden daha hızlı.
* [Logic Apps][lnk-logicapps]: Azure App Service Logic Apps özelliğini hello IOT çözüm tooyour mevcut iş kolu satır sistemlerinizi tümleştirmek ve iş akışı işlemlerini otomatikleştirmek yardımcı olur. Logic Apps sağlar; bir tetikleyiciyle başlayan ve bir dizi adımı yürütürken geliştiriciler toodesign iş akışları — kurallar ve Eylemler ile İş süreçlerinizi güçlü bağlayıcılar toointegrate kullanın. Logic Apps Giden kutusu bağlantı tooa büyük ekosistemi SaaS, bulut tabanlı sunar ve şirket içi uygulamalar.
* [Azure blob depolama][lnk-blob]: hello verileri aygıtlarınızı toohello bulut göndermek için güvenilir ve ekonomik bulut depolama.

## <a name="conclusion"></a>Sonuç
Bu makalede tasarlama ve Azure IOT kullanarak bir IOT altyapı dağıtma için düzeyi Ayrıntılar uygulama genel bakış sağlar. Her bileşen toobe güvenli yapılandırma olan korumak anahtar hello genel IOT altyapı. Azure IOT kullanılabilir Hello tasarım seçenekleri esneklik ve tercih bazı düzeyi sağlamak; Bununla birlikte, her seçenek güvenlik etkileri olabilir. Bu seçenek her risk/maliyeti değerlendirmesi değerlendirilmesi önerilir.

## <a name="see-also"></a>Ayrıca bkz.
Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:

* [Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]
* [IoT Paketi için sık sorulan sorular][lnk-faq]

IOT hub'ı güvenlik konusunda okuyabilirsiniz [Denetim erişim tooIoT Hub] [ lnk-devguide-security] hello IOT Hub Geliştirici Kılavuzu'nda.


[img-overview]: media/iot-suite-security-deployment/overview.png

[lnk-security-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
