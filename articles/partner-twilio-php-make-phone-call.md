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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="2d40d-104">Nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir PHP uygulamasının içinde</span><span class="sxs-lookup"><span data-stu-id="2d40d-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="2d40d-105">Merhaba aşağıdaki örnek, bir PHP web sayfasından Azure üzerinde barındırılan bir çağrı Twilio toomake nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="2d40d-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="2d40d-106">Merhaba sonuç uygulaması hello aşağıdaki ekran görüntüsü gösterildiği gibi hello kullanıcıdan telefon araması değerlerini ister.</span><span class="sxs-lookup"><span data-stu-id="2d40d-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Twilio ve PHP kullanarak azure çağrı formu][twilio_php]

<span data-ttu-id="2d40d-108">Toodo hello aşağıdakilere ihtiyacınız olacak toouse hello kod bu konuda:</span><span class="sxs-lookup"><span data-stu-id="2d40d-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="2d40d-109">Twilio hesabı ve kimlik doğrulaması almak belirtecine, [Twilio konsol][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="2d40d-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="2d40d-110">tooget Twilio ile kullanmaya değerlendirmek, fiyatlandırma [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="2d40d-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="2d40d-111">Bir deneme hesabı için kaydolabilirsiniz [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="2d40d-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="2d40d-112">Merhaba elde [Twilio kitaplığı için PHP](https://github.com/twilio/twilio-php) veya ARMUTLU paket olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2d40d-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="2d40d-113">Daha fazla bilgi için bkz: Merhaba [Benioku dosyasını](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="2d40d-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="2d40d-114">PHP için Hello Azure SDK'sını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2d40d-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="2d40d-115">Merhaba SDK ve yükleme yönergeleri genel bakış için bkz: [PHP için Azure SDK'sı hello ayarlayın](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="2d40d-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="2d40d-116">Arama yapmak için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2d40d-116">Create a web form for making a call</span></span>
<span data-ttu-id="2d40d-117">HTML aşağıdaki hello kod gösterir nasıl toobuild bir web sayfası (**callform.html**) arama yapmak için kullanıcı verilerini alır:</span><span class="sxs-lookup"><span data-stu-id="2d40d-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

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

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="2d40d-118">Merhaba kod toomake hello çağrı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2d40d-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="2d40d-119">kodun gösterdiği nasıl aşağıdaki hello toobuild **makecall.php**, hello kullanıcı tarafından görüntülenen hello formu gönderdiğinde adlandırılan **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="2d40d-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="2d40d-120">Aşağıda gösterilen hello kod hello çağrı iletisi oluşturur ve hello çağrı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2d40d-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="2d40d-121">Twilio hesabı ve kimlik doğrulama belirteci hello emin toouse de [Twilio konsol] [ twilio_console] çok atanan hello yer tutucu değerlerini yerine**$sid** ve **$token** aşağıdaki hello kodda.</span><span class="sxs-lookup"><span data-stu-id="2d40d-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

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

<span data-ttu-id="2d40d-122">Ayrıca toomaking hello çağrısı **makecall.php** hello resimde gösterildiği gibi bazı çağrı meta verilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d40d-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="2d40d-123">Çağrı meta veriler hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="2d40d-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Twilio ve PHP kullanarak azure çağrı yanıtı][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="2d40d-125">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2d40d-125">Run hello application</span></span>
<span data-ttu-id="2d40d-126">Merhaba sonraki adım, uygulama tooAzure Web siteleri toodeploy olduğu.</span><span class="sxs-lookup"><span data-stu-id="2d40d-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="2d40d-127">Merhaba aşağıdaki makaleleri bir Web sitesi oluşturma ve Git, FTP veya WebMatrix ile kodunuzu (her makaledeki tüm bilgiler ilgili olmasına rağmen) dağıtma hello bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="2d40d-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="2d40d-128">Bir PHP MySQL Azure Web sitesi oluşturma ve Git kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="2d40d-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="2d40d-129">Bir PHP MySQL Azure Web sitesi oluşturun ve FTP kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="2d40d-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="2d40d-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2d40d-130">Next steps</span></span>
<span data-ttu-id="2d40d-131">Bu kod tooshow sağlanan Twilio azure'da PHP kullanma, temel işlevleri.</span><span class="sxs-lookup"><span data-stu-id="2d40d-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="2d40d-132">TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d40d-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="2d40d-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2d40d-133">For example:</span></span>

* <span data-ttu-id="2d40d-134">Bir web formu kullanmak yerine, Azure storage bloblarında veya SQL veritabanı toostore telefon numaralarını kullanın ve metin arama.</span><span class="sxs-lookup"><span data-stu-id="2d40d-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="2d40d-135">Azure storage bloblarında PHP ile kullanma hakkında daha fazla bilgi için bkz: [PHP uygulamaları kullanarak Azure depolamaya][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="2d40d-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="2d40d-136">SQL veritabanı PHP ile kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanıyla kullanarak PHP uygulamaları][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="2d40d-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="2d40d-137">Merhaba **makecall.php** kod Twilio tarafından sağlanan URL kullanır ([http://twimlets.com/message][twimlet_message_url]) tooprovide Twilio nasıl bildiren bir Twilio biçimlendirme dili (TwiML) yanıt Merhaba çağrıyla tooproceed.</span><span class="sxs-lookup"><span data-stu-id="2d40d-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="2d40d-138">Örneğin, hello döndürülen TwiML içerebilir bir `<Say>` konuşulan toohello çağrı alıcı olan metinde sonuçları fiil.</span><span class="sxs-lookup"><span data-stu-id="2d40d-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="2d40d-139">Merhaba Twilio tarafından sağlanan URL kullanmak yerine, kendi hizmet toorespond tooTwilio's isteği oluşturabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooUse ses ve PHP SMS özelliklerini için Twilio][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="2d40d-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="2d40d-140">TwiML hakkında daha fazla bilgi bulunabilir [http://www.twilio.com/docs/api/twiml][twiml]ve hakkında daha fazla bilgi `<Say>` ve diğer Twilio fiiller bulunabilir [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="2d40d-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="2d40d-141">Merhaba Twilio güvenlik yönergeleri okuyun [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="2d40d-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="2d40d-142">Twilio hakkında ek bilgi için bkz: [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="2d40d-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="2d40d-143">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="2d40d-143">See Also</span></span>
* [<span data-ttu-id="2d40d-144">Nasıl tooUse Twilio ses ve PHP SMS özellikleri</span><span class="sxs-lookup"><span data-stu-id="2d40d-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

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
