---
title: aaaHow tooUse Twilio ses ve SMS (Java) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. Java dilinde yazılan kod örnekleri."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Nasıl tooUse Twilio ses ve Java SMS özellikleri
Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir. Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir. Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.

## <a id="WhatIs"></a>Twilio nedir?
Twilio varolan web dilleri ve yetenekleri toobuild ses ve SMS uygulamaları kullanmanıza olanak sağlayan bir telefon web hizmeti API'dir. Twilio, (olmayan bir Azure özelliğidir ve Microsoft Ürün) bir bir üçüncü taraf hizmetidir.

**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar. **Twilio SMS** SMS iletileri almasına ve uygulamaları toomake sağlar. **Twilio istemci** uygulamalarınızın mobil bağlantıları dahil olmak üzere var olan Internet bağlantıları kullanarak tooenable sesli iletişime olanak sağlar.

## <a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler
Twilio fiyatlandırma hakkında daha fazla bilgi şu adreste [Twilio fiyatlandırma][twilio_pricing]. Azure müşterilerine alma bir [özel teklif][special_offer]: boş bir kredi 1000 metinlerinin veya 1000 dakika sayısı. Bu kaydınızı toosign sunmak veya daha fazla bilgi almak, lütfen şu adresi ziyaret [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Kavramları
Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır. İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].

Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.

### <a id="Verbs"></a>Twilio fiiller
Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.

Merhaba, Twilio fiillerin listesi verilmiştir.

* **&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.
* **&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.
* **&lt;Kapat&gt;**: bir aramasını sonlandırır.
* **&lt;Yürüt&gt;**: bir ses dosyası çalar.
* **&lt;Sıra&gt;**: Merhaba tooa arayanlar kuyruğunu ekleyin.
* **&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.
* **&lt;Kayıt&gt;**: hello arayanın sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.
* **&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.
* **&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın.
* **&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.
* **&lt;SMS&gt;**: SMS iletisi gönderir.

### <a id="TwiML"></a>TwiML
TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.

Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Merhaba Dünya!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir. Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz. Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello **TwiMLResponse** nesnesi.

Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml]. Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Twilio hesabı oluşturma
Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio]. Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.

Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız. Her ikisi de gerekli toomake Twilio API çağrıları olacaktır. tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun. Hesap Kimliğini ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio konsol][twilio_console], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.

## <a id="create_app"></a>Bir Java uygulaması oluşturma
1. Merhaba Twilio JAR almak ve Java derleme yolu ve WAR dağıtım derlemenizi tooyour ekleyin. Konumundaki [https://github.com/twilio/twilio-java][twilio_java], hello GitHub kaynakları indirmek ve kendi JAR oluşturabilir veya önceden oluşturulmuş bir JAR (veya ile bağımlılıklar olmadan) yükleyebilirsiniz.
2. JDK's olun **cacerts** anahtar deposu hello Equifax güvenli sertifika yetkilisi sertifikası MD5 parmak izi 67:CB:9 D ile içerir: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Merhaba seri numarası olan 35:DE:F4:CF ve hello SHA1 parmak izi olan D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Merhaba sertifika yetkilisi (CA) sertifikası hello için budur [https://api.twilio.com] [ twilio_api_service] Twilio API'leri kullandığınızda çağrılan hizmet. JDK's sağlama hakkında bilgi için **cacerts** anahtar deposu hello doğru CA sertifikası varsa, bkz: [sertifika toohello Java CA sertifika deposuna ekleme][add_ca_cert].

Java için hello Twilio istemci kitaplığı kullanılarak ayrıntılı yönergeler şurada bulunabilir [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir Java uygulamasında][howto_phonecall_java].

## <a id="configure_app"></a>Uygulamanızı tooUse Twilio kitaplıklarını yapılandırmak
Kodunuzu içinde ekleyebileceğiniz **alma** deyimleri Twilio paketleri veya, sınıfları hello için Kaynak dosyalarınız hello üstündeki istediğiniz uygulamanızda toouse.

Java kaynak dosyalar için:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Kaynak dosyaları Java sunucu sayfası (JSP):

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
Toouse, istediğiniz hangi Twilio paketleri ya da sınıfları bağlı olarak, **alma** deyimleri farklı olabilir.

## <a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın
Merhaba aşağıdaki giden toomake nasıl hello kullanarak Çağır gösterir **çağrısı** sınıfı. Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır. Kendi değerlerinizi hello yerine **gelen** ve **için** telefon numaraları ve hello doğruladığınızdan emin olun **gelen** Twilio hesabı önceki toorunning hello kodunuz için telefon numarası.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Toohello içinde geçirilen hello parametreler hakkında daha fazla bilgi için **Call.creator** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır. Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooProvide TwiML yanıtları Azure üzerinde bir Java uygulamasında](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin
Merhaba aşağıdakileri nasıl bir SMS iletisini kullanarak toosend hello gösterir **ileti** sınıfı. Merhaba **gelen** numarası **4155992671**, SMS iletileri toosend deneme hesapları için Twilio tarafından sağlanır. Merhaba **için** Twilio hesap önceki toorunning hello kodu için sayı doğrulandı.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

Toohello içinde geçirilen hello parametreler hakkında daha fazla bilgi için **Message.creator** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar
Olduğunda, uygulamanızın başlatır örneğin hello aracılığıyla çağrı toohello Twilio API **CallCreator.create** yöntemi, Twilio gönderecek beklenen tooreturn olduğundan isteği tooa URL'nizi TwiML yanıt. Hello yukarıdaki örnekte hello Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url]. (TwiML Web Hizmetleri tarafından kullanılmak üzere tasarlandığından, hello TwiML tarayıcınızda görüntüleyebilirsiniz. Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir  **&lt;yanıt&gt;**  öğesi; başka bir örnek olarak, 'ıtıklatın.[http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee bir  **&lt;yanıt&gt;**  içeren öğe bir  **&lt;Say &gt;**  öğesi.)

Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür kendi URL sitesi oluşturabilirsiniz. HTTP yanıt veren herhangi bir dilde hello sitesi oluşturabilirsiniz; Bu konu, bir JSP sayfasında hello URL barındırma varsayar.

JSP sayfa sonuçlarını bildiren bir TwiML yanıt aşağıdaki hello **Merhaba Dünya!** Merhaba çağrıda.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

JSP sayfa bazı metinleri bildiren TwiML yanıt sonuçlarında aşağıdaki hello birkaç duraklatır var ve hello Twilio API sürümü ve hello Azure rol adı hakkında bilgi söyler.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

Merhaba **ApiVersion** parametredir Twilio sesli istekler (SMS istek değil) kullanılabilir. toosee hello kullanılabilir İstek parametreleri Twilio ses ve SMS istekleri için bkz: <https://www.twilio.com/docs/api/twiml/twilio_request> ve <https://www.twilio.com/docs/api/twiml/sms/twilio_request >sırasıyla. Merhaba **RoleName** ortam değişkeni kullanılabilir Azure dağıtımın bir parçası olarak. (Bunlar gelen çekilmesi şekilde tooadd özel ortam değişkenleri istiyorsanız **System.getenv**, hello ortam değişkenleri kısmına bakın [çeşitli rol yapılandırma ayarları] [misc_role_config_settings].)

JSP sayfanızı tooprovide TwiML yanıtları ayarlayın olduktan sonra hello geçirilen URL hello gibi hello hello JSP sayfasının URL'sini kullanın **Call.creator** yöntemi. Örneğin, bir Web uygulaması varsa, dağıtılan MyTwiML tooan adlı Azure hizmeti, barındırılan ve hello JSP sayfasının hello adı mytwiml.jsp, hello URL çok geçirilebilir**Call.creator** hello aşağıda gösterildiği gibi:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Merhaba TwiML ile yanıt için başka bir seçenek olan **VoiceResponse** hello kullanılabilir sınıfı **com.twilio.twiml** paket.

Java ile Azure Twilio kullanma hakkında ek bilgi için bkz: [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir Java uygulamasında][howto_phonecall_java].

## <a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın
Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz. Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api_documentation].

## <a id="NextSteps"></a>Sonraki Adımlar
Merhaba Twilio hizmet hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin:

* [Twilio güvenlik yönergeleri][twilio_security_guidelines]
* [Twilio nasıl ın yapılır ve örnek kod][twilio_howtos]
* [Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]
* [Github'da Twilio][twilio_on_github]
* [Konuşma tooTwilio desteği][twilio_support]

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
