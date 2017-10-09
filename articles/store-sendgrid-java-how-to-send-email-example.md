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
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Nasıl tooSend e-posta kullanarak SendGrid Azure dağıtımında Java'dan
Merhaba aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından SendGrid toosend e-postaları nasıl kullanabileceğinizi gösterir. Merhaba sonuç uygulaması hello kullanıcı e-posta değerleri için hello aşağıdaki ekran görüntüsü gösterildiği gibi ister.

![E-posta formu][emailform]

e-posta kaynaklanan hello ekran görüntüsü aşağıdaki benzer toohello arar.

![E-posta iletisi][emailsent]

Toodo hello aşağıdakilere ihtiyacınız olacak toouse hello kod bu konuda:

1. Elde javax.mail Kavanoz, örneğin gelen hello <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Java derleme yolu hello Kavanoz tooyour ekleyin.
3. Bu Java uygulaması Eclipse toocreate kullanıyorsanız, hello SendGrid kitaplıkları Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerebilir. Bu Java uygulaması Eclipse toocreate kullanmıyorsanız hello kitaplıkları hello içinde bulunan emin olun, Java uygulama ve eklenen toohello sınıf yolu uygulamanızın olarak aynı Azure rol.

Oluşturmuş olmanız da gerekir, kendi SendGrid kullanıcı adı ve parola, toobe mümkün toosend hello e-posta. SendGrid başlatılan tooget bkz [toosend e-posta nasıl SendGrid Java kullanarak](store-sendgrid-java-how-to-send-email.md).

Merhaba bilgilerine ek olarak, bir aşina [Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944), veya Eclipse kullanıyorsanız azure'da Java uygulamaları barındırmak için başka teknikler ile önemle önerilir.

## <a name="create-a-web-form-for-sending-email"></a>E-posta göndermek için web formu oluşturma
koddan hello nasıl toocreate web form e-posta göndermek için tooretrieve kullanıcı verileri gösterir. Bu içerik amaçları doğrultusunda hello JSP dosyası adlı **emailform.jsp**.

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

## <a name="create-hello-code-toosend-hello-email"></a>Merhaba kod toosend hello e-posta oluşturma
Merhaba emailform.jsp hello formunda tamamladığınızda olarak adlandırılır, aşağıdaki kod, hello e-posta iletisi oluşturur ve gönderir. Bu içerik amaçları doğrultusunda hello JSP dosyası adlı **sendemail.jsp**.

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

Ayrıca toosending hello e-posta emailform.jsp hello kullanıcı için bir sonuç sağlar; Aşağıdaki ekran görüntüsü hello buna bir örnektir:

![Posta sonucunu gönderin][emailresult]

## <a name="next-steps"></a>Sonraki adımlar
Uygulama toohello işlem öykünücüsü dağıtmak ve emailform.jsp çalıştırmak bir tarayıcı değerleri hello biçiminde girin, tıklatın **bu e-posta Gönder**ve ardından sendemail.jsp sonuçlarında görebilirsiniz.

Bu kod tooshow sağlanan, nasıl toouse SendGrid azure'da Java. TooAzure üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler tooadd isteyebilirsiniz. Örneğin: 

* Bir web formu kullanmak yerine Azure storage bloblarında veya SQL veritabanı toostore e-posta adresleri ve e-posta iletilerini kullanabilirsiniz. Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse hello Java'dan Blob Depolama hizmetinin](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` tooretrieve hello SendGrid kullanıcı adı ve parola kullanmak yerine, dağıtımınızın yapılandırma ayarları, bu değerler web formu tooretrieve hello. Merhaba hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [kullanma hello Azure hizmeti Çalışma Zamanı Kitaplığı'nda JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) ve hello Azure hizmeti çalışma zamanı paketi belgelerine <http://dl.windowsazure.com/javadoc>.
* SendGrid Java kullanma hakkında daha fazla bilgi için bkz: [toosend e-posta nasıl SendGrid Java kullanarak](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
