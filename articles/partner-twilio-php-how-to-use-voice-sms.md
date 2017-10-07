---
title: aaaHow tooUse Twilio ses ve SMS (PHP) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. PHP ile yazılan kod örnekleri."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Nasıl tooUse Twilio ses ve PHP SMS özellikleri
Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir. Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir. Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.

## <a id="WhatIs"></a>Twilio nedir?
Twilio iş iletişimleri hello geleceği destekleyen, geliştiricilerin tooembed ses, VoIP, etkinleştirme ve uygulamalara Mesajlaşma. Bunlar hello Twilio iletişimleri API platformu ile gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın. Uygulamalardır basit toobuild ve ölçeklendirilebilir. Sizinle ödeme-olarak esnekliğinin fiyatlandırma gidin ve bulut güvenilirlik ' yararlanır.

**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar. **Twilio SMS** metin iletileri almasına ve uygulama toosend sağlar. **Twilio istemci** toomake VoIP çağrılarından herhangi telefon, tablet veya tarayıcı sağlar ve WebRTC destekler.

## <a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler
Azure müşterilerin alacak bir [özel teklif](http://www.twilio.com/azure): 10 ücretsiz Twilio Twilio hesabınızı yükseltirken kredisi. Bu Twilio kredi uygulanan tooany Twilio kullanım (1. 000'kadar SMS iletileri veya too1000 yukarı alma gelen telefon numarasını ve ileti veya çağrı hedef hello konumuna bağlı olarak sesli dakika başına 10 kredi eşdeğer toosending) olabilir. Bu Twilio iade almak ve adresindeki kullanmaya başlama: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio Kullandıkça Ödeme tabanlı bir hizmettir. Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz. Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma][twilio_pricing].

## <a id="Concepts"></a>Kavramları
Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır. İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].

Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.

### <a id="Verbs"></a>Twilio fiiller
Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.

Merhaba, Twilio fiillerin listesi verilmiştir. Bilgi hakkında hello diğer fiilleri ve yetenekleri aracılığıyla [Twilio biçimlendirme dili belgeleri](http://www.twilio.com/docs/api/twiml).

* **&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.
* **&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.
* **&lt;Kapat&gt;**: bir aramasını sonlandırır.
* **&lt;Yürüt&gt;**: bir ses dosyası çalar.
* **&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.
* **&lt;Kayıt&gt;**: hello arayanın sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.
* **&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.
* **&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın
* **&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.
* **&lt;SMS&gt;**: SMS iletisi gönderir.

### <a id="TwiML"></a>TwiML
TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.

Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir. Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz. Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello **TwiMLResponse** nesnesi.

Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml]. Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Twilio hesabı oluşturma
Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio]. Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.

Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız. Her ikisi de gerekli toomake Twilio API çağrıları olacaktır. tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun. Hesap Kimliğini ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio hesap sayfası][twilio_account], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.

## <a id="create_app"></a>PHP uygulaması oluşturma
Merhaba Twilio hizmeti kullanır ve Azure üzerinde çalışan bir PHP uygulamasının hello Twilio hizmetini kullanan tüm diğer PHP uygulaması farklı değildir. Twilio Hizmetleri REST tabanlı ve PHP'nin çeşitli yollarla çağrılabilir olsa da, bu makalede toouse Twilio ile hizmetleri nasıl üzerine odaklanacaktır [GitHub PHP'nin Twilio kitaplığının][twilio_php]. PHP için hello Twilio kitaplığını kullanma hakkında daha fazla bilgi için bkz: [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Oluşturma ve Twilio/PHP uygulama tooAzure dağıtma hakkında ayrıntılı yönergeler şurada bulunabilir [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir PHP uygulamasının içinde][howto_phonecall_php].

## <a id="configure_app"></a>Uygulamanızı tooUse Twilio kitaplıklarını yapılandırmak
PHP için uygulama toouse hello Twilio kitaplığınızın iki yolla yapılandırabilirsiniz:

1. Merhaba Twilio kitaplığı PHP github'dan indirin ([https://github.com/twilio/twilio-php][twilio_php]) ve hello ekleyin **Hizmetleri** directory tooyour uygulama.
   
    -VEYA-
2. Merhaba Twilio kitaplığı için PHP ARMUTLU paket olarak yükleyin. Aşağıdaki komutları hello ile yüklenebilir:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

PHP için hello Twilio kitaplığı yükledikten sonra daha sonra ekleyebilirsiniz bir **require_once** deyimi, PHP hello üstündeki dosyaları tooreference hello kitaplığı:

        require_once 'Services/Twilio.php';

Daha fazla bilgi için bkz: [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın
Merhaba aşağıdaki giden toomake nasıl hello kullanarak Çağır gösterir **Services_Twilio** sınıfı. Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır. Kendi değerlerinizi hello yerine **gelen** ve **için** telefon numaraları ve hello doğruladığınızdan emin olun **gelen** Twilio hesabı önceki toorunning hello kodunuz için telefon numarası.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır. Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooProvide TwiML yanıtları bilgisayarınızı kendi Web sitesinden](#howto_provide_twiml_responses).

* **Not**: tootroubleshoot SSL sertifika doğrulama hataları, bkz: [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin
Merhaba aşağıdakileri nasıl bir SMS iletisini kullanarak toosend hello gösterir **Services_Twilio** sınıfı. Merhaba **gelen** SMS iletileri toosend deneme hesapları için numarası Twilio tarafından sağlanır. Merhaba **için** Twilio hesap önceki toorunning hello kodu için sayı doğrulandı.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar
Uygulamanızı bir çağrı toohello Twilio API başlattığında Twilio olduğundan isteği tooa URL'nizi tooreturn TwiML yanıt beklenen gönderir. Hello yukarıdaki örnekte hello Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url]. (TwiML Twilio tarafından kullanılmak üzere tasarlandığından, görüntüleyebileceğiniz tarayıcınızda hello. Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir `<Response>` öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message? İleti % 5B0 %5 D Hello % 20World =] [ twimlet_message_url_hello_world] toosee bir `<Response>` içeren öğe bir `<Say>` öğesi.)

Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür, kendi site oluşturabilirsiniz. XML yanıtlarını döndürür herhangi bir dilde hello sitesi oluşturabilirsiniz; Bu konu, PHP toocreate hello TwiML kullanan varsaymaktadır.

PHP sayfa sonuçlarını bildiren bir TwiML yanıt aşağıdaki hello **Hello World** hello çağrıda.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Yukarıdaki hello örnekte görebildiğiniz gibi hello TwiML yanıt basitçe bir XML dosyasıdır. PHP için Hello Twilio kitaplığı TwiML oluşturacaktır sınıfları içerir. Aşağıdaki Hello örnek yukarıda gösterildiği gibi hello eşdeğer yanıt oluşturur, ancak kullanır hello **Hizmetleri\_Twilio\_Twiml** sınıfı PHP hello Twilio Kitaplığı'nda:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Tooprovide TwiML yanıtları ayarlayın, PHP sayfanızı oluşturduktan sonra hello geçirilen URL hello gibi hello hello PHP sayfanın URL'sini kullanın `Services_Twilio->account->calls->create` yöntemi. Adlı bir Web uygulaması varsa, örneğin, **MyTwiML** dağıtılan tooan Azure barındırılan hizmeti ve hello PHP sayfa hello adıdır **mytwiml.php**, URL çok geçirilebilir hello **Services_ Twilio -> Hesap çağrıları -> -> oluşturma** hello aşağıdaki örnekte gösterildiği gibi:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

PHP ile azure'da Twilio kullanma hakkında ek bilgi için bkz: [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir PHP uygulamasının içinde][howto_phonecall_php].

## <a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın
Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz. Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api_documentation].

## <a id="NextSteps"></a>Sonraki Adımlar
Merhaba Twilio hizmet hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin:

* [Twilio güvenlik yönergeleri][twilio_security_guidelines]
* [Twilio nasıl ın yapılır ve örnek kod][twilio_howtos]
* [Twilio hızlı başlangıç öğreticileri][twilio_quickstarts] 
* [Github'da Twilio][twilio_on_github]
* [Konuşma tooTwilio desteği][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
