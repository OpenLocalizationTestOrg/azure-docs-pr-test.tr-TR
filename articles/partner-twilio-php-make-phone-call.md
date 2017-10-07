---
title: "aaaHow toomake bir telefon araması gelen Twilio (PHP) | Microsoft Docs"
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. PHP uygulaması için örneklerdir."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir PHP uygulamasının içinde
Merhaba aşağıdaki örnek, bir PHP web sayfasından Azure üzerinde barındırılan bir çağrı Twilio toomake nasıl kullanabileceğinizi gösterir. Merhaba sonuç uygulaması hello aşağıdaki ekran görüntüsü gösterildiği gibi hello kullanıcıdan telefon araması değerlerini ister.

![Twilio ve PHP kullanarak azure çağrı formu][twilio_php]

Toodo hello aşağıdakilere ihtiyacınız olacak toouse hello kod bu konuda:

1. Twilio hesabı ve kimlik doğrulaması almak belirtecine, [Twilio konsol][twilio_console]. tooget Twilio ile kullanmaya değerlendirmek, fiyatlandırma [http://www.twilio.com/pricing][twilio_pricing]. Bir deneme hesabı için kaydolabilirsiniz [https://www.twilio.com/try-twilio][try_twilio].
2. Merhaba elde [Twilio kitaplığı için PHP](https://github.com/twilio/twilio-php) veya ARMUTLU paket olarak yükleyin. Daha fazla bilgi için bkz: Merhaba [Benioku dosyasını](https://github.com/twilio/twilio-php/blob/master/README.md).
3. PHP için Hello Azure SDK'sını yükleyin. Merhaba SDK ve yükleme yönergeleri genel bakış için bkz: [PHP için Azure SDK'sı hello ayarlayın](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Arama yapmak için web formu oluşturma
HTML aşağıdaki hello kod gösterir nasıl toobuild bir web sayfası (**callform.html**) arama yapmak için kullanıcı verilerini alır:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a>Merhaba kod toomake hello çağrı oluşturma
kodun gösterdiği nasıl aşağıdaki hello toobuild **makecall.php**, hello kullanıcı tarafından görüntülenen hello formu gönderdiğinde adlandırılan **callform.html**. Aşağıda gösterilen hello kod hello çağrı iletisi oluşturur ve hello çağrı oluşturur. Twilio hesabı ve kimlik doğrulama belirteci hello emin toouse de [Twilio konsol] [ twilio_console] çok atanan hello yer tutucu değerlerini yerine**$sid** ve **$token** aşağıdaki hello kodda.

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

Ayrıca toomaking hello çağrısı **makecall.php** hello resimde gösterildiği gibi bazı çağrı meta verilerini görüntüler. Çağrı meta veriler hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Twilio ve PHP kullanarak azure çağrı yanıtı][twilio_php_response]

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın
Merhaba sonraki adım, uygulama tooAzure Web siteleri toodeploy olduğu. Merhaba aşağıdaki makaleleri bir Web sitesi oluşturma ve Git, FTP veya WebMatrix ile kodunuzu (her makaledeki tüm bilgiler ilgili olmasına rağmen) dağıtma hello bilgileri içerir:

* [Bir PHP MySQL Azure Web sitesi oluşturma ve Git kullanarak dağıtma](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Bir PHP MySQL Azure Web sitesi oluşturun ve FTP kullanarak dağıtma](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Sonraki adımlar
Bu kod tooshow sağlanan Twilio azure'da PHP kullanma, temel işlevleri. TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz. Örneğin:

* Bir web formu kullanmak yerine, Azure storage bloblarında veya SQL veritabanı toostore telefon numaralarını kullanın ve metin arama. Azure storage bloblarında PHP ile kullanma hakkında daha fazla bilgi için bkz: [PHP uygulamaları kullanarak Azure depolamaya][howto_blob_storage_php]. SQL veritabanı PHP ile kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanıyla kullanarak PHP uygulamaları][howto_sql_azure_php].
* Merhaba **makecall.php** kod Twilio tarafından sağlanan URL kullanır ([http://twimlets.com/message][twimlet_message_url]) tooprovide Twilio nasıl bildiren bir Twilio biçimlendirme dili (TwiML) yanıt Merhaba çağrıyla tooproceed. Örneğin, hello döndürülen TwiML içerebilir bir `<Say>` konuşulan toohello çağrı alıcı olan metinde sonuçları fiil. Merhaba Twilio tarafından sağlanan URL kullanmak yerine, kendi hizmet toorespond tooTwilio's isteği oluşturabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooUse ses ve PHP SMS özelliklerini için Twilio][howto_twilio_voice_sms_php]. TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml]ve hakkında daha fazla bilgi `<Say>` ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].
* Merhaba Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].

Twilio hakkında ek bilgi için bkz: [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Ayrıca Bkz.
* [Nasıl tooUse Twilio ses ve PHP SMS özellikleri](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
