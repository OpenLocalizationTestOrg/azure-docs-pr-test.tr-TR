---
title: "Azure IOT Hub güvenlik aaaUnderstand | Microsoft Docs"
description: "Geliştirici Kılavuzu - nasıl toocontrol erişim tooIoT Hub cihaz uygulamaları ve arka uç uygulamalar için. Güvenlik belirteçleri ve X.509 sertifikalarını desteği hakkında bilgiler içerir."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Denetim erişim tooIoT Hub

Bu makalede, IOT hub'ınızı güvenliğini sağlamaya yönelik hello seçenekleri açıklanmaktadır. IOT hub'ı kullanan *izinleri* toogrant erişim tooeach IOT hub uç. İzinleri hello erişim tooan IOT hub işlevselliğine bağlı sınırlayın.

Bu makalede açıklanır:

* Merhaba farklı izinler IOT hub'ınızı tooa aygıt veya arka uç uygulama tooaccess verebilirsiniz.
* tooverify izinleri kullanan kimlik doğrulama işlemi ve hello belirteçleri hello.
* Nasıl tooscope toolimit toospecific kaynaklarına erişim kimlik bilgileri.
* X.509 sertifikaları IOT hub'ı destekler.
* Var olan cihaz kimlik kayıt defterleri veya kimlik doğrulama şemasını kullanan özel cihaz kimlik doğrulama mekanizmaları.

### <a name="when-toouse"></a>Zaman toouse

Uygun izinleri tooaccess hello IOT Hub uç noktaları hiçbirini olması gerekir. Örneğin, bir aygıt tooIoT Hub, gönderdiği her ileti yanı sıra güvenlik kimlik bilgileri içeren bir belirteç eklemeniz gerekir.

## <a name="access-control-and-permissions"></a>Erişim denetimi ve izinleri

Erişim izni verebilir [izinleri](#iot-hub-permissions) yolları aşağıdaki hello içinde:

* **IOT hub düzeyi paylaşılan erişim ilkeleri**. Paylaşılan erişim ilkeleri, herhangi bir birleşimini vermek [izinleri](#iot-hub-permissions). Hello ilkeleri tanımlayabilirsiniz [Azure portal][lnk-management-portal], hello kullanarak program aracılığıyla veya [IOT hub'ı kaynak sağlayıcısı REST API'leri][lnk-resource-provider-apis]. Yeni oluşturulan bir IOT hub aşağıdaki varsayılan ilkeler hello sahiptir:

  * **iothubowner**: tüm izinleri ilkesiyle.
  * **Hizmet**: ilke ile **ServiceConnect** izni.
  * **Aygıt**: ilke ile **DeviceConnect** izni.
  * **registryRead**: ilke ile **RegistryRead** izni.
  * **registryReadWrite**: ilke ile **RegistryRead** ve RegistryWrite izinleri.
  * **Cihaz başına güvenlik kimlik bilgileri**. Her IOT hub'ı içeren bir [kimlik kayıt defteri][lnk-identity-registry]. Bu kimlik kayıt defterinde her cihaz için vermek güvenlik kimlik bilgileri yapılandırabilirsiniz **DeviceConnect** izinleri kapsamlı toohello karşılık gelen cihaz uç noktaları.

Örneğin, tipik bir IOT çözüm içinde:

* Merhaba aygıt yönetimi bileşeni kullanır hello *registryReadWrite* ilkesi.
* Merhaba olay işlemci bileşeninin kullandığı hello *hizmet* ilkesi.
* Merhaba çalışma zamanı aygıt iş mantığı bileşeni kullanır hello *hizmet* ilkesi.
* Tek bir cihazı hello IOT hub'ın kimlik kayıt defterinde depolanan kimlik bilgilerini kullanarak bağlanın.

> [!NOTE]
> Bkz: [izinleri](#iot-hub-permissions) ayrıntılı bilgi için.

## <a name="authentication"></a>Kimlik Doğrulaması

Azure IOT Hub, bir belirteç hello paylaşılan erişim ilkeleri ve kayıt defteri güvenlik kimlik karşı doğrulayarak erişim tooendpoints verir.

Simetrik anahtarlar gibi güvenlik kimlik bilgileri hiçbir zaman hello kablo üzerinden gönderilir.

> [!NOTE]
> Merhaba tüm sağlayıcıları gibi hello Azure IOT Hub kaynak sağlayıcısı Azure aboneliğiniz ile korunuyor [Azure Resource Manager][lnk-azure-resource-manager].

Hakkında daha fazla bilgi için güvenlik belirteçleri tooconstruct ve kullanım bkz [IOT hub'ı güvenlik belirteçleri][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Protokol özellikleri

Desteklenen her protokolü, MQTT, AMQP ve HTTP gibi farklı yollarla belirteçleri taşımaları.

MQTT kullanırken hello BAĞLAN paket hello DeviceID ClientID, {iothubhostname} hello sahiptir / {DeviceID} hello Username alanı ve SAS belirteci hello parolası alanında. {iothubhostname} olması hello tam CName hello IOT hub (örneğin, contoso.azure-devices.net).

Kullanırken [AMQP][lnk-amqp], IOT hub'ı destekleyen [SASL DÜZ] [ lnk-sasl-plain] ve [AMQP talep tabanlı-güvenlik] [ lnk-cbs].

AMQP talep tabanlı-güvenlik kullanırsanız, standart hello belirtir nasıl tootransmit bu belirteçleri.

SASL DÜZ için hello **kullanıcıadı** olabilir:

* `{policyName}@sas.root.{iothubName}`IOT hub düzeyindeki belirteçleri kullanıyorsanız.
* `{deviceId}@sas.{iothubname}`cihaz kapsamlı belirteçleri kullanıyorsanız.

Her iki durumda da açıklandığı gibi hello parola alanı hello belirtecini içeren [IOT hub'ı güvenlik belirteçleri][lnk-sas-tokens].

HTTP kimlik doğrulaması geçerli bir belirteci hello dahil ederek uygulayan **yetkilendirme** istek üstbilgisi.

#### <a name="example"></a>Örnek

Kullanıcı adı (DeviceID büyük küçük harfe duyarlı):`iothubname.azure-devices.net/DeviceId`

Parola (oluşturmak SAS belirteci hello ile [aygıt explorer] [ lnk-device-explorer] aracı):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Merhaba [Azure IOT SDK'ları] [ lnk-sdks] toohello hizmet bağlanırken belirteçleri otomatik olarak oluşturmak. Bazı durumlarda, hello Azure IOT SDK'ları desteklemez tüm hello protokolleri ya da tüm hello kimlik doğrulama yöntemleri.

### <a name="special-considerations-for-sasl-plain"></a>SASL DÜZ için özel hususlar

SASL DÜZ AMQP ile kullanırken, tooan IOT hub'a bağlanan bir istemci her TCP bağlantısı için tek bir belirteci kullanabilirsiniz. Merhaba belirtecinin süresi dolduğunda, hello TCP bağlantısı hello hizmet bağlantısını keser ve bir reconnect tetikler. Bu davranış değil sorunlu sırada bir arka uç uygulaması için nedenleri aşağıdaki hello için cihaz uygulaması için zarar:

* Ağ geçidi genellikle birçok aygıtlar adına bağlayın. SASL DÜZ kullanırken, tooan IOT hub'a bağlanan her aygıt için ayrı bir TCP bağlantı toocreate sahip. Bu senaryoda önemli ölçüde hello tüketimi, güç ve ağ kaynaklarını artırır ve her cihaz bağlantısı hello gecikme artar.
* Kaynak kısıtlı cihazları olumsuz her belirteç süresi dolduktan sonra artan hello kaynakları tooreconnect kullanımıyla etkilenir.

## <a name="scope-iot-hub-level-credentials"></a>Kapsam IOT hub düzeyindeki kimlik bilgileri

Sınırlı kaynak URI'si ile belirteçleri oluşturarak IOT hub'ı düzeyinde güvenlik ilkelerinin kapsamını belirleyebilirsiniz. Örneğin, hello uç nokta toosend cihaz bulut iletilerini aygıttan **/devices/ {DeviceID} / iletileri/olayları**. Bir IOT hub düzeyindeki paylaşılan erişim ilkesi ile de kullanabileceğiniz **DeviceConnect** izinleri toosign, resourceURI olan bir belirteç **/devices/ {DeviceID}**. Bu yaklaşım, yalnızca cihaz adına kullanılabilir toosend iletileri bir belirteç oluşturur **DeviceID**.

Bu bir mekanizmadır benzer toohello [olay hub'ları Yayımcı ilkesi][lnk-event-hubs-publisher-policy]ve tooimplement özel kimlik doğrulama yöntemleri sağlar.

## <a name="security-tokens"></a>Güvenlik belirteçleri

IOT hub'ı kullanan güvenlik tooauthenticate aygıtları belirteçleri ve anahtarları hello kablo gönderme tooavoid Hizmetleri. Ayrıca, güvenlik belirteçlerini geçerlilik tarihi ve kapsam sınırlıdır. [Azure IOT SDK'ları] [ lnk-sdks] otomatik olarak özel bir yapılandırma gerektirmeden belirteçleri oluşturur. Bazı senaryolar toogenerate gerektirir ve güvenlik belirteçlerini doğrudan kullanır. Bu tür senaryoları şunları içerir:

* Merhaba doğrudan hello MQTT, AMQP veya HTTP yüzeyleri kullanımı.
* Merhaba belirteci hizmeti düzeni uyarlamasını açıklandığı gibi hello [özel cihaz kimlik doğrulamasını][lnk-custom-auth].

IOT Hub ayrıca sağlar aygıtları tooauthenticate IOT Hub ile kullanarak [X.509 sertifikalarını][lnk-x509].

### <a name="security-token-structure"></a>Güvenlik belirteci yapısı

IOT Hub ' güvenlik belirteçleri toogrant zaman sınırlı erişim toodevices ve Hizmetleri toospecific işlevini kullanın. paylaşılan erişim veya simetrik anahtarı ile imzalanmış güvenlik belirteçleri tooget yetkilendirme tooconnect tooIoT Hub, cihazları ve Hizmetleri göndermeniz gerekir. Bu anahtarları hello kimlik kayıt defterinde bir cihaz kimliği ile depolanır.

Merhaba paylaşılan erişim ilkesi izinleri ile ilişkili bir paylaşılan erişim anahtarı verir erişim tooall hello işlevselliğe sahip bir belirteci imzalayan. Bir belirteci imzalayan aygıt kimliğin simetrik anahtar yalnızca verir hello ile **DeviceConnect** hello izinlerini ilişkili cihaz kimliği.

Merhaba güvenlik belirteci biçimi aşağıdaki hello sahiptir:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Merhaba beklenen değerler şunlardır:

| Değer | Açıklama |
| --- | --- |
| {İmza} |HMAC SHA256 imza dizisi hello formunun: `{URL-encoded-resourceURI} + "\n" + expiry`. **Önemli**: hello anahtar base64 kodlaması kodunu çözdü ve anahtar tooperform hello HMAC SHA256 hesaplama kullanılır. |
| {resourceURI} |Merhaba IOT hub'ı (Protokol) ana bilgisayar adı ile başlayarak, bu belirteci ile erişilen hello uç noktalar için URI öneki (tarafından kesim). Örneğin, `myHub.azure-devices.net/devices/device1` |
| {süre sonu} |UTF8 dizeleri hello dönemi: 00:00:00 UTC üzerinde 1 Ocak 1970'ten beri geçen saniye sayısı. |
| {URL-kodlanmış-resourceURI} |Düşük hello küçük kaynak URI'si için URL kodlaması durumda |
| {policyName} |Bu belirteç başvuruyor hello paylaşılan erişim ilkesi toowhich Hello adı. Yüklenmesinden hello belirteci toodevice kayıt defteri kimlik bilgilerini ifade eder. |

**Not önek üzerinde**: hello URI öneki segmente göre ve karakter tarafından hesaplanır. Örneğin `/a/b` için bir önek `/a/b/c` ancak için `/a/bc`.

Merhaba aşağıdaki Node.js parçacığını gösterir adlı bir işlev **generateSasToken** hesaplar hello girişleri belirtecinden hello `resourceUri, signingKey, policyName, expiresInMins`. Merhaba sonraki bölümlerde nasıl tooinitialize hello farklı girişleri hello farklı belirteci için kullanım ayrıntılarını gösterir.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

Bir karşılaştırma bir güvenlik belirteci eşdeğer Python kodu toogenerate hello:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Hello zaman hello belirtecin geçerliliğini IOT hub'ı makinelerde doğrulanır olduğundan, başlangıç saati hello belirteci oluşturur hello makinenin hello kayması en az olmalıdır.

### <a name="use-sas-tokens-in-a-device-app"></a>SAS belirteci bir aygıt uygulamasında kullanma

İki yolu tooobtain vardır **DeviceConnect** güvenlik belirteçleri IOT Hub ile izinlerle: kullanmak bir [simetrik aygıt hello kimlik kayıt defteri anahtarından](#use-a-symmetric-key-in-the-identity-registry), veya bir [paylaşılan erişim anahtarı](#use-a-shared-access-policy).

Tüm işlevlere aygıtlardan erişilebilir önekiyle uç noktalarda tasarıma göre sunulur unutmayın `/devices/{deviceId}`.

> [!IMPORTANT]
> IOT hub'ı belirli bir aygıt doğrulayacağını hello tek yolu hello aygıt kimlik simetrik anahtar kullanıyor. Paylaşılan Erişim İlkesi kullanılan tooaccess cihazın işlevselliğini olduğunda durumlarda hello güvenlik belirteci güvenilir bir alt bileşen olarak veren hello bileşen hello çözüm dikkate almanız gerekir.

Merhaba aygıt'e yönelik uç noktalar (yedeklemiş hello Protokolü) şunlardır:

| Uç Nokta | İşlev |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Cihaz-bulut iletileri gönderir. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Bulut-cihaz iletilerini alır. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Simetrik anahtar hello kimlik kayıt defterinde kullanma

Bir aygıt kimliğin simetrik anahtar toogenerate bir belirteç kullanırken policyName hello (`skn`) öğesi hello belirtecinin atlanmış.

Örneğin, bir belirteç tüm cihazın işlevselliğini sahip hello şu parametreler tooaccess oluşturuldu:

* Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* imzalama anahtarı: herhangi bir simetrik anahtar hello için `{device id}` kimliği
* hiçbir ilke adı
* Tüm süre sonu zamanı.

Node.js işlevi önceki hello kullanarak bir örnek olabilir:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

erişim tooall işlevselliği device1 için verir, hello sonuç olacaktır:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Bu olası toogenerate hello .NET kullanarak bir SAS belirteci olan [aygıt explorer] [ lnk-device-explorer] aracı veya platformlar arası, düğüm tabanlı hello [iothub-explorer] [ lnk-iothub-explorer] komut satırı yardımcı programı.

### <a name="use-a-shared-access-policy"></a>Bir paylaşılan erişim ilkesi kullanın

Paylaşılan Erişim İlkesi tarafından bir belirteç oluşturduğunuzda, hello ayarlamak `skn` hello İlkesi alan toohello adı. Bu ilke hello vermelidir **DeviceConnect** izni.

paylaşılan erişim ilkeleri tooaccess cihazın işlevselliğini kullanma hello iki ana senaryo şunlardır:

* [protokol ağ geçidi bulut][lnk-endpoints],
* [simge Hizmetleri] [ lnk-custom-auth] tooimplement özel kimlik doğrulama şemasını kullanılır.

Bu yana Hello paylaşılan erişim ilkesi potansiyel olarak erişim tooconnect herhangi bir aygıtı güvenlik belirteçleri oluşturulurken önemli toouse hello doğru kaynak URI'si olduğundan verebilirsiniz. Bu ayar tooscope hello belirteci tooa belirli cihazda hello kaynak URI'si kullanarak belirteci Hizmetleri için özellikle önemlidir. Bu zaten tüm aygıtlar için trafiği eşlemlerse protokolü ağ geçitleri için daha az ilgili noktasıdır.

Örnek olarak, önceden oluşturulan hello kullanarak bir belirteç hizmet adlı erişim ilkesi paylaşılan **aygıt** bir belirteç ile şu parametreler hello oluşturacak:

* Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* imzalama anahtarı: hello hello anahtarları birini `device` İlkesi
* İlke adı: `device`,
* Tüm süre sonu zamanı.

Node.js işlevi önceki hello kullanarak bir örnek olabilir:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

erişim tooall işlevselliği device1 için verir, hello sonuç olacaktır:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Bir protokol ağ geçidi aynı belirteci yalnızca ayarı tüm cihazlar kaynak URI'si çok hello için hello kullanabilirsiniz`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Hizmet bileşenleri gelen güvenlik belirteçleri kullanın

Hizmet bileşenleri, yalnızca daha önce açıklandığı gibi hello uygun izinleri verme paylaşılan erişim ilkeleri kullanan güvenlik belirteçleri üretebilir.

Merhaba bitiş noktasında kullanıma sunulan hello hizmeti işlevleri şöyledir:

| Uç Nokta | İşlev |
| --- | --- |
| `{iot hub host name}/devices` |Oluştur, Güncelleştir, alabilir ve cihaz kimliklerini silebilir. |
| `{iot hub host name}/messages/events` |Cihaz bulut iletilerini alır. |
| `{iot hub host name}/servicebound/feedback` |Bulut-cihaz iletilerini için bildirim alırsınız. |
| `{iot hub host name}/devicebound` |Bulut cihaz iletileri gönderir. |

Örnek olarak, önceden oluşturulan hello kullanma oluşturma hizmeti adlı erişim ilkesi paylaşılan **registryRead** bir belirteç ile şu parametreler hello oluşturacak:

* Kaynak URI'si: `{IoT hub name}.azure-devices.net/devices`,
* imzalama anahtarı: hello hello anahtarları birini `registryRead` İlkesi
* İlke adı: `registryRead`,
* Tüm süre sonu zamanı.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

erişim tooread tüm cihaz kimliklerini vermeniz, hello sonuç olacaktır:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Desteklenen X.509 sertifikaları

Bir X.509 sertifikası tooauthenticate bir cihaz IOT Hub ile kullanabilirsiniz. Sertifikaları dahil et:

* **Varolan bir X.509 sertifikası**. Bir aygıt zaten kendisiyle ilişkilendirilmiş bir X.509 sertifikası olabilir. Bu sertifika tooauthenticate Hello cihaz IOT Hub ile kullanabilirsiniz.
* **A otomatik olarak oluşturulan ve X-509 Sertifika'otomatik olarak imzalanan**. Bir aygıt üreticisi veya şirket içi dağıtıcı, bu sertifikalar oluşturmak ve hello karşılık gelen özel anahtar (ve sertifika) hello aygıtta depolamak. Araçları gibi kullanabilir [OpenSSL] [ lnk-openssl] ve [Windows SelfSignedCertificate] [ lnk-selfsigned] bu amaç için yardımcı programı.
* **X.509 sertifikası CA tarafından imzalanmış**. bir aygıt tooidentify ve IOT Hub ile kimlik doğrulaması, oluşturulur ve bir sertifika yetkilisi (CA) tarafından imzalanmış bir X.509 sertifikası kullanabilirsiniz. IOT hub'ı yalnızca sunulan bu hello parmak izi doğrular hello yapılandırılmış parmak izi ile eşleşir. Iothub hello sertifika zinciri doğrulamaz.

Bir aygıt ya da bir X.509 sertifikası veya bir güvenlik belirteci kimlik doğrulaması, ancak ikisini için kullanabilir.

### <a name="register-an-x509-certificate-for-a-device"></a>Bir aygıt bir X.509 sertifikası Kaydet

Merhaba [Azure IOT hizmeti SDK'sı için C#] [ lnk-service-sdk] (sürüm 1.0.8+) destekleyen bir X.509 sertifikası için kimlik doğrulaması kullanan bir cihazı kaydetme. İçeri/dışarı aktarma aygıtların gibi diğer API'leri X.509 sertifikalarını da destekler.

### <a name="c-support"></a>C\# desteği

Merhaba **RegistryManager** sınıfı, bir cihaz programlı şekilde tooregister sağlar. Özellikle, hello **AddDeviceAsync** ve **UpdateDeviceAsync** yöntemleri tooregister etkinleştirmek ve bir aygıtı hello IOT Hub kimlik kayıt defteri güncelleştirin. Bu iki yöntem ele bir **aygıt** örnek giriş olarak. Hello **aygıt** sınıfı içeren bir **kimlik doğrulaması** toospecify birincil ve ikincil X.509 sertifika parmak izlerini veren özelliği. Merhaba parmak izi SHA-1 karma hello X.509 sertifikası (DER ikili kodlama kullanılarak depolanır) değerini temsil eder. Merhaba birincil bir parmak izi veya ikincil bir parmak izi veya her ikisini belirtme seçeneğiniz vardır. Birincil ve ikincil parmak izleri desteklenen toohandle sertifika aktarma senaryolar verilmiştir.

> [!NOTE]
> IOT hub'ı gerektirmez veya hello tüm X.509 sertifikası, parmak izi hello depolar.

Örnek C işte\# parçacığı tooregister bir X.509 sertifikası kullanarak bir cihazı kod:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Çalıştırma işlemleri sırasında bir X.509 sertifikası kullanın

Merhaba [.NET için Azure IOT cihaz SDK'sı] [ lnk-client-sdk] (sürüm 1.0.11+) X.509 sertifikalarını hello kullanımını destekler.

### <a name="c-support"></a>C\# desteği

Merhaba sınıfı **DeviceAuthenticationWithX509Certificate** destekler hello oluşturulmasını **DeviceClient** X.509 sertifikası kullanarak örnekleri. Merhaba X.509 sertifikası hello özel anahtarı içeren hello (PKCS #12 olarak da bilinir) PFX biçiminde olması gerekir.

Örnek kod parçacığı aşağıda verilmiştir:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Özel cihaz kimlik doğrulaması

Merhaba IOT hub'ı kullanabilirsiniz [kimlik kayıt defteri] [ lnk-identity-registry] tooconfigure cihaz başına güvenlik kimlik ve erişim denetimi kullanarak [belirteçleri] [ lnk-sas-tokens] . Bir IOT çözümündeki bir özel kimlik kayıt defteri ve/veya kimlik doğrulama düzeni zaten varsa, oluşturmayı göz önünde bulundurun bir *belirteç hizmeti* toointegrate IOT Hub ile bu altyapı. Bu şekilde, çözümünüz içinde diğer IOT özelliklerini kullanabilirsiniz.

Bir belirteci hizmeti bir özel bulut hizmetidir. IOT hub'ı kullanan *paylaşılan erişim ilkesi* ile **DeviceConnect** izinleri toocreate *aygıt kapsamlı* belirteçleri. Bu belirteçler bir aygıt tooconnect tooyour IOT hub'ı etkinleştirin.

![Merhaba belirteci hizmeti deseninin adımları][img-tokenservice]

Merhaba belirteci hizmeti deseninin hello ana adımlar şunlardır:

1. IOT Hub'ı paylaşılan erişim ilkesi ile oluşturma **DeviceConnect** IOT hub'ınız için izinleri. Bu ilke hello oluşturabilirsiniz [Azure portal] [ lnk-management-portal] veya program aracılığıyla. Merhaba belirteci hizmeti oluşturduğu Bu ilke toosign hello belirteçlerini kullanır.
1. Bir cihaz IOT hub'ınızı tooaccess gerektiğinde, imzalı bir belirteç belirteci Hizmeti'nden ister. Merhaba aygıt hello belirteci hizmeti toocreate hello belirtecini kullanır, özel kimlik kayıt defteri/kimlik doğrulama düzeni toodetermine hello cihaz kimliği ile kimlik doğrulaması yapabilir.
1. Merhaba belirteci hizmeti bir belirteci döndürür. Merhaba belirteci kullanılarak oluşturulan `/devices/{deviceId}` olarak `resourceURI`, ile `deviceId` kimlik doğrulaması gerçekleştirilen hello aygıt olarak. Merhaba belirteç hizmeti hello paylaşılan erişim ilkesi tooconstruct hello belirteci kullanır.
1. Merhaba cihaz doğrudan hello IOT hub ile Merhaba belirtecini kullanır.

> [!NOTE]
> Merhaba .NET sınıfını kullanabilirsiniz [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] veya Java sınıfı hello [IotHubServiceSasToken] [ lnk-java-sas] toocreate bir belirteç belirteci hizmetinizi.

Merhaba belirteci hizmeti hello belirteci süre sonu istendiği gibi ayarlayabilirsiniz. Merhaba belirtecinin süresi dolduğunda, hello IOT hub'ı hello cihaz bağlantısı sunucularının. Ardından, hello aygıt hello belirteci Hizmeti'nden yeni bir belirteç istemeniz gerekir. Kısa süre sonu zamanı hello cihaz ve hello belirteci hizmeti hello yükü artırır.

Aygıt tooconnect tooyour hub için hala toohello IOT Hub kimlik kayıt defteri eklemelisiniz — hello aygıt bir belirteç ve olmayan bir aygıt anahtar tooconnect kullanıyor olsa da. Bu nedenle, etkinleştirme veya hello cihaz kimliklerini devre dışı bırakarak toouse aygıt başına erişim denetimi devam edebilirsiniz [kimlik kayıt defteri][lnk-identity-registry]. Bu yaklaşım, uzun süre sonu zamanlarında belirteçleri kullanarak hello riskleri azaltır.

### <a name="comparison-with-a-custom-gateway"></a>Özel bir ağ geçidi ile karşılaştırma

Merhaba belirteci hizmeti düzeni hello yolu tooimplement IOT hub'ı içeren bir özel kimlik kayıt defteri/kimlik doğrulaması şeması önerilen ' dir. IOT hub'ı toohandle devam ettiğinden bu deseni önerilir hello çözüm trafiğin çoğu. Ancak, hello özel kimlik doğrulama düzeni şekilde hello protokolüyle birbirine, gerektirebilecek bir *özel ağ geçidi* tooprocess tüm trafiği hello. Böyle bir senaryo örneği kullanarak[Aktarım Katmanı Güvenliği (TLS) ve önceden paylaşılan anahtarı (PSKs)][lnk-tls-psk]. Daha fazla bilgi için bkz: Merhaba [protokol ağ geçidi] [ lnk-protocols] konu.

## <a name="reference-topics"></a>Başvuru konuları:

Merhaba aşağıdaki başvuru konuları denetleme erişim tooyour IOT hub'ı hakkında daha fazla bilgi sağlar.

## <a name="iot-hub-permissions"></a>IOT hub'ı izinleri

Merhaba aşağıdaki tabloda toocontrol erişim tooyour IOT hub'ı kullanabilirsiniz hello izinleri listeler.

| İzin | Notlar |
| --- | --- |
| **RegistryRead** |Okuma erişimi toohello kimlik kayıt defteri verir. Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry]. <br/>Bu izin, arka uç bulut Hizmetleri tarafından kullanılır. |
| **RegistryReadWrite** |Verir okuma ve yazma erişimi toohello kimlik kayıt defteri. Daha fazla bilgi için bkz: [kimlik kayıt defteri][lnk-identity-registry]. <br/>Bu izin, arka uç bulut Hizmetleri tarafından kullanılır. |
| **ServiceConnect** |Verir toocloud hizmet dönük iletişim ve uç nokta izleme erişin. <br/>Verir izni tooreceive cihaz bulut iletilerini, bulut-cihaz iletilerini ve teslim alındı bildirimleri karşılık gelen alma hello gönderin. <br/>Dosya için verir izni tooretrieve teslim onay yükler. <br/>Verir izni tooaccess cihaz çiftlerini tooupdate etiketleri ve istenen özellikleri bildirilen özelliklerini almak ve sorgular çalıştırın. <br/>Bu izin, arka uç bulut Hizmetleri tarafından kullanılır. |
| **DeviceConnect** |Verir toodevice'te Uç noktalara erişebilirsiniz. <br/>Verir izni toosend cihaz-bulut iletileri ve bulut-cihaz iletilerini. <br/>Verir izni tooperform karşıya dosya yükleme aygıttan. <br/>Verir izin tooreceive cihaz çifti istenen özelliği bildirimleri ve bildirilen özellikleri twin güncelleştirme aygıt. <br/>Verir izni tooperform dosyayı yükler. <br/>Bu izin, cihazlar tarafından kullanılır. |

## <a name="additional-reference-material"></a>Ek başvuru bilgileri

Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.
* [Azaltma ve kotaları] [ lnk-quotas] hello kotaları açıklar ve IOT Hub hizmeti toohello uygulamak davranışları azaltma.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.
* [IOT hub'ı sorgu dili] [ lnk-query] tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz hello sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl toocontrol erişim IOT hub'ı öğrendiniz artık IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenen olabilir:

* [Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanacak][lnk-devguide-device-twins]
* [Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]
* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticileri aşağıdaki hello ilgilenen olabilir:

* [Azure IOT Hub ile çalışmaya başlama][lnk-getstarted-tutorial]
* [Toosend bulut-cihaz IOT Hub ile nasıl iletileri][lnk-c2d-tutorial]
* [Nasıl tooprocess IOT hub'a cihaz-bulut iletileri][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
