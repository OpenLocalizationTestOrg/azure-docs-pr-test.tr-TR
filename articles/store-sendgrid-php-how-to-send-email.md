---
title: SendGrid e-posta hizmetine (PHP) kullanma | Microsoft Docs
description: "Bilgi nasıl Azure üzerinde SendGrid e-posta hizmeti ile e-posta gönderin. PHP ile yazılan kod örnekleri."
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
ms.openlocfilehash: 523b986f66a2e48685e9707903194856f0dcf4a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-sendgrid-email-service-from-php"></a><span data-ttu-id="f8295-104">Php'den SendGrid e-posta hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="f8295-104">How to Use the SendGrid Email Service from PHP</span></span>
<span data-ttu-id="f8295-105">Bu kılavuz, Azure üzerinde SendGrid e-posta hizmeti ile genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f8295-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="f8295-106">Örnekler, PHP ile yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f8295-106">The samples are written in PHP.</span></span>
<span data-ttu-id="f8295-107">Kapsamdaki senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, ve **eklerini ekleme**.</span><span class="sxs-lookup"><span data-stu-id="f8295-107">The scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="f8295-108">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f8295-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="f8295-109">SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="f8295-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="f8295-110">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="f8295-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="f8295-111">Ortak SendGrid kullanım senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f8295-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="f8295-112">Giriş müşterileri için otomatik olarak gönderme</span><span class="sxs-lookup"><span data-stu-id="f8295-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="f8295-113">Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler</span><span class="sxs-lookup"><span data-stu-id="f8295-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="f8295-114">Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="f8295-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="f8295-115">Eğilimleri belirlemenize yardımcı olmak için rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8295-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="f8295-116">Müşteri sorguları iletme</span><span class="sxs-lookup"><span data-stu-id="f8295-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="f8295-117">Uygulamanızdan e-posta bildirimleri</span><span class="sxs-lookup"><span data-stu-id="f8295-117">Email notifications from your application</span></span>

<span data-ttu-id="f8295-118">Daha fazla bilgi için bkz: [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="f8295-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="f8295-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8295-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="f8295-120">SendGrid PHP uygulamanızdan kullanma</span><span class="sxs-lookup"><span data-stu-id="f8295-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="f8295-121">SendGrid Azure PHP uygulamada kullanarak gerektiren hiçbir özel yapılandırma veya kodlama.</span><span class="sxs-lookup"><span data-stu-id="f8295-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="f8295-122">SendGrid bir hizmet olduğundan, bir şirket içi uygulamasından mümkün olduğunca onu tam olarak aynı şekilde bir bulut uygulamasından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="f8295-122">Because SendGrid is a service, it can be accessed in exactly the same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="f8295-123">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="f8295-123">How to: Send an Email</span></span>
<span data-ttu-id="f8295-124">SMTP ya da SendGrid tarafından sağlanan Web API kullanarak e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8295-124">You can send email using either SMTP or the Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="f8295-125">SMTP API</span><span class="sxs-lookup"><span data-stu-id="f8295-125">SMTP API</span></span>
<span data-ttu-id="f8295-126">SendGrid SMTP API kullanarak e-posta göndermek için kullanmak *Swift kullanılmasının*, PHP uygulamalarından e-postaları göndermek için bileşen tabanlı bir kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="f8295-126">To send email using the SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="f8295-127">İndirebilirsiniz *Swift kullanılmasının* kitaplığından [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (kullanmak [Oluşturucu] Swift yüklemek için Kullanılmasının).</span><span class="sxs-lookup"><span data-stu-id="f8295-127">You can download the *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] to install Swift Mailer).</span></span> <span data-ttu-id="f8295-128">E-posta kitaplığı ile gönderme içerir örneklerini oluşturmaya <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_kullanılmasının</span>, ve <span class="auto-style2">Swift\_iletisi </span> uygun özelliklerini ayarlama ve çağırma sınıfları <span class="auto-style2">Swift\_Mailer::send</span> yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f8295-128">Sending email with the library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the receiver is able to view html emails then only the html
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
     $from = array('someone@example.com' => 'Name To Appear');
     // Email recipients
     $to = array(
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

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="f8295-129">Web API</span><span class="sxs-lookup"><span data-stu-id="f8295-129">Web API</span></span>
<span data-ttu-id="f8295-130">PHP'ın kullanmak [curl işlevi] [ curl function] SendGrid Web API kullanarak e-posta göndermek için.</span><span class="sxs-lookup"><span data-stu-id="f8295-130">Use PHP's [curl function][curl function] to send email using the SendGrid Web API.</span></span>

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

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="f8295-131">Bunu gerçek anlamda bir RESTful API'si çoğu çağrıları, hem GET ve POST fiiller birbirinin yerine kullanılabilir olduğundan, olmasa da SendGrid'ın Web API'sini bir REST API için çok benzer.</span><span class="sxs-lookup"><span data-stu-id="f8295-131">SendGrid's Web API is very similar to a REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="f8295-132">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="f8295-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="f8295-133">SMTP API</span><span class="sxs-lookup"><span data-stu-id="f8295-133">SMTP API</span></span>
<span data-ttu-id="f8295-134">SMTP API kullanarak bir ek gönderirken bir ek Swift kullanılmasının içeren bir e-posta göndermek için örnek komut dosyası için kod satırı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f8295-134">Sending an attachment using the SMTP API involves one additional line of code to the example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create the body of the message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of the email
      * If the reciever is able to view html emails then only the html
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
     $from = array('someone@example.com' => 'Name To Appear');

     // Email recipients
     $to = array(
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

     // attach the body of the email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out to '.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="f8295-135">Ek kod satırı ile aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f8295-135">The additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="f8295-136">Attach yöntemi çağırır Bu kod satırı <span class="auto-style2">Swift\_ileti</span> nesne ve statik bir yöntem <span class="auto-style2">fromPath</span> üzerinde <span class="auto-style2">Swift\_ek</span> almak ve bir dosyayı iletiye sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f8295-136">This line of code calls the attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class to get and attach a file to a message.</span></span>

### <a name="web-api"></a><span data-ttu-id="f8295-137">Web API</span><span class="sxs-lookup"><span data-stu-id="f8295-137">Web API</span></span>
<span data-ttu-id="f8295-138">Web API kullanarak bir ek gönderme, Web API kullanarak bir e-posta göndermek için çok benzer.</span><span class="sxs-lookup"><span data-stu-id="f8295-138">Sending an attachment using the Web API is very similar to sending an email using the Web API.</span></span> <span data-ttu-id="f8295-139">Ancak, aşağıdaki örnekte, bu öğe parametre dizisi içermesi gerektiğini unutmayın:</span><span class="sxs-lookup"><span data-stu-id="f8295-139">However, note that in the example that follows, the parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="f8295-140">Örnek:</span><span class="sxs-lookup"><span data-stu-id="f8295-140">Example:</span></span>

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
         'html' => '<p> the HTML </p>',
         'text' => 'the plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl to use HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is the body of the POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not to return headers, but do return the response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="f8295-141">Nasıl yapılır: altbilgi, izleme ve analiz etkinleştirmek için filtreleri kullanın</span><span class="sxs-lookup"><span data-stu-id="f8295-141">How to: Use Filters to Enable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="f8295-142">SendGrid 'filtre' kullanımı ile ek e-posta işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8295-142">SendGrid provides additional email functionality through the use of 'filters'.</span></span> <span data-ttu-id="f8295-143">Bu izleme'ye tıklayın, Google analytics, izleme abonelik ve benzeri etkinleştirme gibi belirli işlevleri etkinleştirmek için e-posta iletisine eklenecek ayarlardır.</span><span class="sxs-lookup"><span data-stu-id="f8295-143">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="f8295-144">Filtreler filtreleri özelliğini kullanarak bir iletiye uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="f8295-144">Filters can be applied to a message by using the filters property.</span></span> <span data-ttu-id="f8295-145">Her filtre filtre özgü ayarları içeren bir karma tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="f8295-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="f8295-146">Aşağıdaki örnek altbilgi filtresini etkinleştirir ve e-posta iletisi sonuna eklenecek bir kısa mesaj belirtir.</span><span class="sxs-lookup"><span data-stu-id="f8295-146">The following example enables the footer filter and specifies a text message that will be appended to the bottom of the email message.</span></span>
<span data-ttu-id="f8295-147">Bu örnek için kullanacağız [sendgrid php Kitaplığı].</span><span class="sxs-lookup"><span data-stu-id="f8295-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="f8295-148">Kullanım [Oluşturucu] Kitaplığı'nı yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="f8295-148">Use [Composer] to install library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="f8295-149">Örnek:</span><span class="sxs-lookup"><span data-stu-id="f8295-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // The list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request to SendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify the names of the recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of the above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled the footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // The subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy the user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $to = 'john@contoso.com';

     # Create the body of the message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of the email
     # if the receiver is able to view html emails then only the html
     # email will be displayed

     /*
      * Note the variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment to call you at -time- EST to discuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     to call you at -time- EST to discuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach the body of the email
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

## <a name="next-steps"></a><span data-ttu-id="f8295-150">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f8295-150">Next Steps</span></span>
<span data-ttu-id="f8295-151">SendGrid e-posta hizmeti temel bilgileri öğrendiğinize göre daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f8295-151">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="f8295-152">SendGrid belgeleri: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="f8295-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="f8295-153">SendGrid PHP kitaplığı: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="f8295-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="f8295-154">SendGrid özel teklif Azure müşteriler: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="f8295-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="f8295-155">Daha fazla bilgi için Ayrıca bkz. [PHP Geliştirici Merkezi](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="f8295-155">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
<span data-ttu-id="f8295-156">[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="f8295-156">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="f8295-157">[işleme uygun e-posta teslimi]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="f8295-157">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
<span data-ttu-id="f8295-158">[sendgrid php Kitaplığı]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span><span class="sxs-lookup"><span data-stu-id="f8295-158">[sendgrid-php library]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1</span></span>
<span data-ttu-id="f8295-159">[Oluşturucu]: https://getcomposer.org/download/</span><span class="sxs-lookup"><span data-stu-id="f8295-159">[Composer]: https://getcomposer.org/download/</span></span>
