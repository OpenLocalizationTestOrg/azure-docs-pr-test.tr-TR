---
title: aaastore-sendgrid-Java-How-To-Send-EMail-example
description: "Toosend e-posta nasıl bir Azure dağıtımında Java'dan SendGrid kullanma"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="652de-103">Nasıl tooSend e-posta kullanarak SendGrid Azure dağıtımında Java'dan</span><span class="sxs-lookup"><span data-stu-id="652de-103">How tooSend Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="652de-104">Merhaba aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından SendGrid toosend e-postaları nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="652de-104">hello following example shows you how you can use SendGrid toosend emails from a web page hosted in Azure.</span></span> <span data-ttu-id="652de-105">Merhaba sonuç uygulaması hello kullanıcı e-posta değerleri için hello aşağıdaki ekran görüntüsü gösterildiği gibi ister.</span><span class="sxs-lookup"><span data-stu-id="652de-105">hello resulting application will prompt hello user for email values, as shown in hello following screen shot.</span></span>

![E-posta formu][emailform]

<span data-ttu-id="652de-107">e-posta kaynaklanan hello ekran görüntüsü aşağıdaki benzer toohello arar.</span><span class="sxs-lookup"><span data-stu-id="652de-107">hello resulting email will look similar toohello following screen shot.</span></span>

![E-posta iletisi][emailsent]

<span data-ttu-id="652de-109">Toodo hello aşağıdakilere ihtiyacınız olacak toouse hello kod bu konuda:</span><span class="sxs-lookup"><span data-stu-id="652de-109">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="652de-110">Elde javax.mail Kavanoz, örneğin gelen hello <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="652de-110">Obtain hello javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="652de-111">Java derleme yolu hello Kavanoz tooyour ekleyin.</span><span class="sxs-lookup"><span data-stu-id="652de-111">Add hello JARs tooyour Java build path.</span></span>
3. <span data-ttu-id="652de-112">Bu Java uygulaması Eclipse toocreate kullanıyorsanız, hello SendGrid kitaplıkları Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="652de-112">If you are using Eclipse toocreate this Java application, you can include hello SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="652de-113">Bu Java uygulaması Eclipse toocreate kullanmıyorsanız hello kitaplıkları hello içinde bulunan emin olun, Java uygulama ve eklenen toohello sınıf yolu uygulamanızın olarak aynı Azure rol.</span><span class="sxs-lookup"><span data-stu-id="652de-113">If you are not using Eclipse toocreate this Java application, ensure hello libraries are included within hello same Azure role as your Java application, and added toohello class path of your application.</span></span>

<span data-ttu-id="652de-114">Oluşturmuş olmanız da gerekir, kendi SendGrid kullanıcı adı ve parola, toobe mümkün toosend hello e-posta.</span><span class="sxs-lookup"><span data-stu-id="652de-114">You must also have your own SendGrid username and password, toobe able toosend hello email.</span></span> <span data-ttu-id="652de-115">SendGrid başlatılan tooget bkz [toosend e-posta nasıl SendGrid Java kullanarak](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="652de-115">tooget started with SendGrid, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="652de-116">Merhaba bilgilerine ek olarak, bir aşina [Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944), veya Eclipse kullanıyorsanız azure'da Java uygulamaları barındırmak için başka teknikler ile önemle önerilir.</span><span class="sxs-lookup"><span data-stu-id="652de-116">Additionally, familiarity with hello information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="652de-117">E-posta göndermek için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="652de-117">Create a web form for sending email</span></span>
<span data-ttu-id="652de-118">koddan hello nasıl toocreate web form e-posta göndermek için tooretrieve kullanıcı verileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="652de-118">hello following code shows how toocreate a web form tooretrieve user data for sending email.</span></span> <span data-ttu-id="652de-119">Bu içerik amaçları doğrultusunda hello JSP dosyası adlı **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="652de-119">For purposes of this content, hello JSP file is named **emailform.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a><span data-ttu-id="652de-120">Merhaba kod toosend hello e-posta oluşturma</span><span class="sxs-lookup"><span data-stu-id="652de-120">Create hello code toosend hello email</span></span>
<span data-ttu-id="652de-121">Merhaba emailform.jsp hello formunda tamamladığınızda olarak adlandırılır, aşağıdaki kod, hello e-posta iletisi oluşturur ve gönderir.</span><span class="sxs-lookup"><span data-stu-id="652de-121">hello following code, which is called when you complete hello form in emailform.jsp, creates hello email message and sends it.</span></span> <span data-ttu-id="652de-122">Bu içerik amaçları doğrultusunda hello JSP dosyası adlı **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="652de-122">For purposes of this content, hello JSP file is named **sendemail.jsp**.</span></span>

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

<span data-ttu-id="652de-123">Ayrıca toosending hello e-posta emailform.jsp hello kullanıcı için bir sonuç sağlar; Aşağıdaki ekran görüntüsü hello buna bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="652de-123">In addition toosending hello email, emailform.jsp provides a result for hello user; an example is hello following screen shot:</span></span>

![Posta sonucunu gönderin][emailresult]

## <a name="next-steps"></a><span data-ttu-id="652de-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="652de-125">Next steps</span></span>
<span data-ttu-id="652de-126">Uygulama toohello işlem öykünücüsü dağıtmak ve emailform.jsp çalıştırmak bir tarayıcı değerleri hello biçiminde girin, tıklatın **bu e-posta Gönder**ve ardından sendemail.jsp sonuçlarında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="652de-126">Deploy your application toohello compute emulator and within a browser run emailform.jsp, enter values in hello form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="652de-127">Bu kod tooshow sağlanan, nasıl toouse SendGrid azure'da Java.</span><span class="sxs-lookup"><span data-stu-id="652de-127">This code was provided tooshow you how toouse SendGrid in Java on Azure.</span></span> <span data-ttu-id="652de-128">TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="652de-128">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="652de-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="652de-129">For example:</span></span> 

* <span data-ttu-id="652de-130">Bir web formu kullanmak yerine Azure storage bloblarında veya SQL veritabanı toostore e-posta adresleri ve e-posta iletilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="652de-130">You could use Azure storage blobs or SQL Database toostore email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="652de-131">Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse hello Java'dan Blob Depolama hizmetinin](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="652de-131">For information about using Azure storage blobs in Java, see [How tooUse hello Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="652de-132">SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="652de-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="652de-133">Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid kullanıcı adı ve parola kullanmak yerine, dağıtımınızın yapılandırma ayarları, bu değerler web formu tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="652de-133">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid username and password from your deployment's configuration settings, instead of using hello web form tooretrieve those values.</span></span> <span data-ttu-id="652de-134">Merhaba hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [kullanma hello Azure hizmeti Çalışma Zamanı Kitaplığı'nda JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) ve hello Azure hizmeti çalışma zamanı paketi belgelerine <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="652de-134">For information about hello `RoleEnvironment` class, see [Using hello Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and hello Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="652de-135">SendGrid Java kullanma hakkında daha fazla bilgi için bkz: [toosend e-posta nasıl SendGrid Java kullanarak](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="652de-135">For more information about using SendGrid in Java, see [How toosend email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
