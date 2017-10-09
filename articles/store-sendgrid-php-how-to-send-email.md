---
title: aaaHow toouse hello SendGrid e-posta hizmetine (PHP) | Microsoft Docs
description: "Bilgi nasıl Azure'da hello SendGrid e-posta hizmeti ile e-posta gönderin. PHP ile yazılan kod örnekleri."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a>Nasıl tooUse hello php'den SendGrid e-posta hizmeti
Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri hello SendGrid tooperform e-posta gösterir. Merhaba örnekleri PHP ile yazılmıştır.
Merhaba kapsanan senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, ve **eklerini ekleme**. SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.

## <a name="what-is-hello-sendgrid-email-service"></a>Merhaba SendGrid e-posta hizmeti nedir?
SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra. Ortak SendGrid kullanım senaryoları şunları içerir:

* Otomatik olarak giriş toocustomers gönderme
* Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler
* Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama
* Toohelp eğilimleri belirlemek raporları oluşturma
* Müşteri sorguları iletme
* Uygulamanızdan e-posta bildirimleri

Daha fazla bilgi için bkz: [https://sendgrid.com][https://sendgrid.com].

## <a name="create-a-sendgrid-account"></a>SendGrid hesabı oluşturma
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a>SendGrid PHP uygulamanızdan kullanma
SendGrid Azure PHP uygulamada kullanarak gerektiren hiçbir özel yapılandırma veya kodlama. SendGrid bir hizmet olduğundan, tam olarak hello erişilebileceğini aynı şekilde, bir bulut uygulamasından bir şirket içi uygulama olabilir.

## <a name="how-to-send-an-email"></a>Nasıl yapılır: bir e-posta Gönder
SMTP ya da hello SendGrid tarafından sağlanan Web API kullanarak e-posta gönderebilirsiniz.

### <a name="smtp-api"></a>SMTP API
Merhaba SendGrid SMTP API, kullanım kullanarak toosend e-posta *Swift kullanılmasının*, PHP uygulamalarından e-postaları göndermek için bileşen tabanlı bir kitaplığı. Merhaba indirebilirsiniz *Swift kullanılmasının* kitaplığından [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (kullanmak [Oluşturucu] tooinstall SWIFT kullanılmasının). Merhaba kitaplığı ile e-posta gönderme içerir örneklerini oluşturmaya <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_kullanılmasının</span>, ve <span class="auto-style2">Swift\_iletisi </span> uygun özelliklerini ayarlama ve çağırma sınıfları <span class="auto-style2">Swift\_Mailer::send</span> yöntemi.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a>Web API
PHP'ın kullanmak [curl işlevi] [ curl function] toosend e-posta kullanarak hello SendGrid Web API.

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

Bunu gerçek anlamda bir RESTful API'si çoğu çağrıları, hem GET ve POST fiiller birbirinin yerine kullanılabilir olduğundan, olmasa da SendGrid'ın Web API çok benzer tooa REST API'dır.

## <a name="how-to-add-an-attachment"></a>Nasıl yapılır: bir eki ekleyin
### <a name="smtp-api"></a>SMTP API
Merhaba SMTP API kullanarak bir ek gönderme Swift kullanılmasının içeren bir e-posta göndermek için kod toohello örnek betik, ek bir satır içerir.

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

Merhaba ek kod satırı aşağıdaki gibidir:

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

Bu satırı kodu çağrıları Merhaba, üzerinde yöntemi ekleme <span class="auto-style2">Swift\_ileti</span> nesne ve statik bir yöntem <span class="auto-style2">fromPath</span> üzerinde <span class="auto-style2">Swift\_ek</span>sınıfı tooget ve bir dosya tooa iletisi ekleyin.

### <a name="web-api"></a>Web API
Çok benzer toosending Hello Web API kullanarak bir ek göndermeyi kullanarak bir e-posta hello Web API. Ancak, izleyen hello örnekte hello parametre dizisi bu öğe içermesi gerektiğini unutmayın:

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

Örnek:

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Nasıl yapılır: kullanım filtreleri tooEnable altbilgiler, izleme ve analizi
SendGrid 'filtrelerin' hello kullanımı aracılığıyla ek e-posta işlevselliği sağlar. İzleme'ye tıklayın, Google analytics, izleme, aboneliği etkinleştirme gibi belirli işlevleri etkinleştirmek için tooan e-posta iletisi eklenebilir ayarları bunlar ve benzeri.

Filtreler hello filtreleri özelliğini kullanarak uygulanan tooa ileti olabilir. Her filtre filtre özgü ayarları içeren bir karma tarafından belirtilir. Aşağıdaki örnek hello altbilgi filtresini etkinleştirir ve olacak bir kısa mesaj hello e-posta iletisi toohello sonuna eklenen belirtir.
Bu örnek için kullanacağız [sendgrid php Kitaplığı].
Kullanım [Oluşturucu] tooinstall kitaplığı:

    php composer.phar require sendgrid/sendgrid 2.1.1

Örnek:    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* SendGrid belgeleri: <https://sendgrid.com/docs>
* SendGrid PHP kitaplığı: <https://github.com/sendgrid/sendgrid-php>
* SendGrid özel teklif Azure müşteriler: <https://sendgrid.com/windowsazure.html>

Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/email-solutions
[işleme uygun e-posta teslimi]: https://sendgrid.com/transactional-email
[sendgrid php Kitaplığı]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[Oluşturucu]: https://getcomposer.org/download/
