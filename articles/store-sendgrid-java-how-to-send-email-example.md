---
title: Store-sendgrid-Java-How-To-Send-EMail-example
description: "Bir Azure dağıtımında SendGrid Java kullanarak e-posta gönderme"
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
ms.openlocfilehash: d80d7d9c54bad12a4d26d8623eeccdf9bc2a743a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Bir Azure dağıtımında SendGrid Java kullanarak e-posta gönderme
Aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından e-postalar gönderme SendGrid nasıl kullanabileceğinizi gösterir. Sonuçta elde edilen uygulama kullanıcı e-posta değerleri için aşağıdaki ekran görüntüsünde gösterildiği gibi isteyecektir.

![E-posta formu][emailform]

Sonuçta elde edilen e-posta aşağıdaki ekran görüntüsüne benzer görünür.

![E-posta iletisi][emailsent]

Bu konudaki kodu kullanmak için aşağıdakileri yapmanız gerekir:

1. Javax.mail Kavanoz örneğin almak <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Kavanoz, Java derleme yolu ekleyin.
3. Bu Java uygulaması oluşturmak için Eclipse kullanıyorsanız, SendGrid kitaplıkları Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerebilir. Bu Java uygulaması oluşturmak için Eclipse kullanmıyorsanız kitaplıkları Java uygulamanız aynı Azure rolünü içerdiği ve uygulamanızı sınıfı yoluna eklenen emin olun.

SendGrid kullanıcı adınızı ve e-posta gönderebilmesi için parola, ayrıca sahip olmalıdır. SendGrid başlamak için bkz: [SendGrid Java kullanarak e-posta göndermek nasıl](store-sendgrid-java-how-to-send-email.md).

Ayrıca, bilgileri aşina [bir Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944), veya Eclipse kullanıyorsanız azure'da Java uygulamaları barındırmak için başka teknikler ile önemle önerilir.

## <a name="create-a-web-form-for-sending-email"></a>E-posta göndermek için web formu oluşturma
Aşağıdaki kod, e-posta göndermek için kullanıcı verilerini almak için web formu oluşturulacağını gösterir. Bu içerik amaçları doğrultusunda JSP dosyası adlı **emailform.jsp**.

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

## <a name="create-the-code-to-send-the-email"></a>E-posta göndermek için kod oluşturma
Emailform.jsp biçiminde tamamladığınızda olarak adlandırılır, aşağıdaki kod, e-posta iletisi oluşturur ve bunu gönderir. Bu içerik amaçları doğrultusunda JSP dosyası adlı **sendemail.jsp**.

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

         // The SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display the email fields entered by the user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create the authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create the mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information to stdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create the message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify the email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment the following if you want to add a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment the following if you want to enable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect the transport object.
         transport.connect();
         // Send the message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close the connection.
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

E-posta gönderme yanı sıra emailform.jsp kullanıcı için bir sonuç sağlar; Aşağıdaki ekran örneğidir:

![Posta sonucunu gönderin][emailresult]

## <a name="next-steps"></a>Sonraki adımlar
İşlem öykünücüsü uygulamanızı dağıtmak ve bir tarayıcıdan emailform.jsp çalıştırmak, değerleri girin, tıklatın **bu e-posta Gönder**ve ardından sendemail.jsp sonuçlarında görebilirsiniz.

Bu kod, Azure üzerinde Java SendGrid kullanmayı göstermek için sağlanmıştır. Azure'a üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler eklemek isteyebilirsiniz. Örneğin: 

* E-posta adreslerini ve bir web formu kullanmak yerine, e-posta iletileri depolamak için Azure storage bloblarında veya SQL veritabanı'nı kullanabilirsiniz. Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [Java'dan Blob Depolama hizmetini kullanmayı](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` bu değerleri almak için web formu kullanmak yerine dağıtımınızın yapılandırma ayarlarını SendGrid kullanıcı adı ve parola almalarını sağlar. Hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [JSP biçiminde Azure hizmeti çalışma zamanı kitaplığını kullanarak](http://msdn.microsoft.com/library/windowsazure/hh690948) ve Azure hizmet çalışma zamanı paketi belgelerine <http://dl.windowsazure.com/javadoc>.
* SendGrid Java kullanma hakkında daha fazla bilgi için bkz: [SendGrid Java kullanarak e-posta göndermek nasıl](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
