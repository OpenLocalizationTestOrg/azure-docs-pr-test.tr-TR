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
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="82207-104">Nasıl tooUse hello php'den SendGrid e-posta hizmeti</span><span class="sxs-lookup"><span data-stu-id="82207-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="82207-105">Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri hello SendGrid tooperform e-posta gösterir.</span><span class="sxs-lookup"><span data-stu-id="82207-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="82207-106">Merhaba örnekleri PHP ile yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="82207-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="82207-107">Merhaba kapsanan senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, ve **eklerini ekleme**.</span><span class="sxs-lookup"><span data-stu-id="82207-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="82207-108">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="82207-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="82207-109">Merhaba SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="82207-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="82207-110">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="82207-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="82207-111">Ortak SendGrid kullanım senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="82207-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="82207-112">Otomatik olarak giriş toocustomers gönderme</span><span class="sxs-lookup"><span data-stu-id="82207-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="82207-113">Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler</span><span class="sxs-lookup"><span data-stu-id="82207-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="82207-114">Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="82207-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="82207-115">Toohelp eğilimleri belirlemek raporları oluşturma</span><span class="sxs-lookup"><span data-stu-id="82207-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="82207-116">Müşteri sorguları iletme</span><span class="sxs-lookup"><span data-stu-id="82207-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="82207-117">Uygulamanızdan e-posta bildirimleri</span><span class="sxs-lookup"><span data-stu-id="82207-117">Email notifications from your application</span></span>

<span data-ttu-id="82207-118">Daha fazla bilgi için bkz: [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="82207-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="82207-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="82207-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="82207-120">SendGrid PHP uygulamanızdan kullanma</span><span class="sxs-lookup"><span data-stu-id="82207-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="82207-121">SendGrid Azure PHP uygulamada kullanarak gerektiren hiçbir özel yapılandırma veya kodlama.</span><span class="sxs-lookup"><span data-stu-id="82207-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="82207-122">SendGrid bir hizmet olduğundan, tam olarak hello erişilebileceğini aynı şekilde, bir bulut uygulamasından bir şirket içi uygulama olabilir.</span><span class="sxs-lookup"><span data-stu-id="82207-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="82207-123">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="82207-123">How to: Send an Email</span></span>
<span data-ttu-id="82207-124">SMTP ya da hello SendGrid tarafından sağlanan Web API kullanarak e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82207-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="82207-125">SMTP API</span><span class="sxs-lookup"><span data-stu-id="82207-125">SMTP API</span></span>
<span data-ttu-id="82207-126">Merhaba SendGrid SMTP API, kullanım kullanarak toosend e-posta *Swift kullanılmasının*, PHP uygulamalarından e-postaları göndermek için bileşen tabanlı bir kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="82207-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="82207-127">Merhaba indirebilirsiniz *Swift kullanılmasının* kitaplığından [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (kullanmak [Oluşturucu] tooinstall SWIFT kullanılmasının).</span><span class="sxs-lookup"><span data-stu-id="82207-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="82207-128">Merhaba kitaplığı ile e-posta gönderme içerir örneklerini oluşturmaya <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_kullanılmasının</span>, ve <span class="auto-style2">Swift\_iletisi </span> uygun özelliklerini ayarlama ve çağırma sınıfları <span class="auto-style2">Swift\_Mailer::send</span> yöntemi.</span><span class="sxs-lookup"><span data-stu-id="82207-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

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

### <a name="web-api"></a><span data-ttu-id="82207-129">Web API</span><span class="sxs-lookup"><span data-stu-id="82207-129">Web API</span></span>
<span data-ttu-id="82207-130">PHP'ın kullanmak [curl işlevi] [ curl function] toosend e-posta kullanarak hello SendGrid Web API.</span><span class="sxs-lookup"><span data-stu-id="82207-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

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

<span data-ttu-id="82207-131">Bunu gerçek anlamda bir RESTful API'si çoğu çağrıları, hem GET ve POST fiiller birbirinin yerine kullanılabilir olduğundan, olmasa da SendGrid'ın Web API çok benzer tooa REST API'dır.</span><span class="sxs-lookup"><span data-stu-id="82207-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="82207-132">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="82207-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="82207-133">SMTP API</span><span class="sxs-lookup"><span data-stu-id="82207-133">SMTP API</span></span>
<span data-ttu-id="82207-134">Merhaba SMTP API kullanarak bir ek gönderme Swift kullanılmasının içeren bir e-posta göndermek için kod toohello örnek betik, ek bir satır içerir.</span><span class="sxs-lookup"><span data-stu-id="82207-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

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

<span data-ttu-id="82207-135">Merhaba ek kod satırı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="82207-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="82207-136">Bu satırı kodu çağrıları Merhaba, üzerinde yöntemi ekleme <span class="auto-style2">Swift\_ileti</span> nesne ve statik bir yöntem <span class="auto-style2">fromPath</span> üzerinde <span class="auto-style2">Swift\_ek</span>sınıfı tooget ve bir dosya tooa iletisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="82207-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="82207-137">Web API</span><span class="sxs-lookup"><span data-stu-id="82207-137">Web API</span></span>
<span data-ttu-id="82207-138">Çok benzer toosending Hello Web API kullanarak bir ek göndermeyi kullanarak bir e-posta hello Web API.</span><span class="sxs-lookup"><span data-stu-id="82207-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="82207-139">Ancak, izleyen hello örnekte hello parametre dizisi bu öğe içermesi gerektiğini unutmayın:</span><span class="sxs-lookup"><span data-stu-id="82207-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="82207-140">Örnek:</span><span class="sxs-lookup"><span data-stu-id="82207-140">Example:</span></span>

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="82207-141">Nasıl yapılır: kullanım filtreleri tooEnable altbilgiler, izleme ve analizi</span><span class="sxs-lookup"><span data-stu-id="82207-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="82207-142">SendGrid 'filtrelerin' hello kullanımı aracılığıyla ek e-posta işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="82207-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="82207-143">İzleme'ye tıklayın, Google analytics, izleme, aboneliği etkinleştirme gibi belirli işlevleri etkinleştirmek için tooan e-posta iletisi eklenebilir ayarları bunlar ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="82207-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="82207-144">Filtreler hello filtreleri özelliğini kullanarak uygulanan tooa ileti olabilir.</span><span class="sxs-lookup"><span data-stu-id="82207-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="82207-145">Her filtre filtre özgü ayarları içeren bir karma tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="82207-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="82207-146">Aşağıdaki örnek hello altbilgi filtresini etkinleştirir ve olacak bir kısa mesaj hello e-posta iletisi toohello sonuna eklenen belirtir.</span><span class="sxs-lookup"><span data-stu-id="82207-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="82207-147">Bu örnek için kullanacağız [sendgrid php Kitaplığı].</span><span class="sxs-lookup"><span data-stu-id="82207-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="82207-148">Kullanım [Oluşturucu] tooinstall kitaplığı:</span><span class="sxs-lookup"><span data-stu-id="82207-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="82207-149">Örnek:</span><span class="sxs-lookup"><span data-stu-id="82207-149">Example:</span></span>    

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

## <a name="next-steps"></a><span data-ttu-id="82207-150">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="82207-150">Next Steps</span></span>
<span data-ttu-id="82207-151">Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="82207-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="82207-152">SendGrid belgeleri: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="82207-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="82207-153">SendGrid PHP kitaplığı: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="82207-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="82207-154">SendGrid özel teklif Azure müşteriler: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="82207-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="82207-155">Daha fazla bilgi için hello Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="82207-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

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
