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
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-java-in-an-azure-deployment"></a><span data-ttu-id="29b0b-103">Bir Azure dağıtımında SendGrid Java kullanarak e-posta gönderme</span><span class="sxs-lookup"><span data-stu-id="29b0b-103">How to Send Email Using SendGrid from Java in an Azure Deployment</span></span>
<span data-ttu-id="29b0b-104">Aşağıdaki örnek, Azure üzerinde barındırılan bir web sayfasından e-postalar gönderme SendGrid nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="29b0b-104">The following example shows you how you can use SendGrid to send emails from a web page hosted in Azure.</span></span> <span data-ttu-id="29b0b-105">Sonuçta elde edilen uygulama kullanıcı e-posta değerleri için aşağıdaki ekran görüntüsünde gösterildiği gibi isteyecektir.</span><span class="sxs-lookup"><span data-stu-id="29b0b-105">The resulting application will prompt the user for email values, as shown in the following screen shot.</span></span>

![E-posta formu][emailform]

<span data-ttu-id="29b0b-107">Sonuçta elde edilen e-posta aşağıdaki ekran görüntüsüne benzer görünür.</span><span class="sxs-lookup"><span data-stu-id="29b0b-107">The resulting email will look similar to the following screen shot.</span></span>

![E-posta iletisi][emailsent]

<span data-ttu-id="29b0b-109">Bu konudaki kodu kullanmak için aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="29b0b-109">You'll need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="29b0b-110">Javax.mail Kavanoz örneğin almak <http://www.oracle.com/technetwork/java/javamail/index.html>.</span><span class="sxs-lookup"><span data-stu-id="29b0b-110">Obtain the javax.mail JARs, for example from <http://www.oracle.com/technetwork/java/javamail/index.html>.</span></span>
2. <span data-ttu-id="29b0b-111">Kavanoz, Java derleme yolu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="29b0b-111">Add the JARs to your Java build path.</span></span>
3. <span data-ttu-id="29b0b-112">Bu Java uygulaması oluşturmak için Eclipse kullanıyorsanız, SendGrid kitaplıkları Eclipse'nın dağıtım derleme özelliğini kullanarak, uygulama dağıtım dosyanızda (WAR) içerebilir.</span><span class="sxs-lookup"><span data-stu-id="29b0b-112">If you are using Eclipse to create this Java application, you can include the SendGrid libraries in your application deployment file (WAR) using Eclipse's deployment assembly feature.</span></span> <span data-ttu-id="29b0b-113">Bu Java uygulaması oluşturmak için Eclipse kullanmıyorsanız kitaplıkları Java uygulamanız aynı Azure rolünü içerdiği ve uygulamanızı sınıfı yoluna eklenen emin olun.</span><span class="sxs-lookup"><span data-stu-id="29b0b-113">If you are not using Eclipse to create this Java application, ensure the libraries are included within the same Azure role as your Java application, and added to the class path of your application.</span></span>

<span data-ttu-id="29b0b-114">SendGrid kullanıcı adınızı ve e-posta gönderebilmesi için parola, ayrıca sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="29b0b-114">You must also have your own SendGrid username and password, to be able to send the email.</span></span> <span data-ttu-id="29b0b-115">SendGrid başlamak için bkz: [SendGrid Java kullanarak e-posta göndermek nasıl](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="29b0b-115">To get started with SendGrid, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

<span data-ttu-id="29b0b-116">Ayrıca, bilgileri aşina [bir Hello World uygulamasının Azure için Eclipse'te oluşturma](http://msdn.microsoft.com/library/windowsazure/hh690944), veya Eclipse kullanıyorsanız azure'da Java uygulamaları barındırmak için başka teknikler ile önemle önerilir.</span><span class="sxs-lookup"><span data-stu-id="29b0b-116">Additionally, familiarity with the information at [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), or with other techniques for hosting Java applications in Azure if you are not using Eclipse, is highly recommended.</span></span>

## <a name="create-a-web-form-for-sending-email"></a><span data-ttu-id="29b0b-117">E-posta göndermek için web formu oluşturma</span><span class="sxs-lookup"><span data-stu-id="29b0b-117">Create a web form for sending email</span></span>
<span data-ttu-id="29b0b-118">Aşağıdaki kod, e-posta göndermek için kullanıcı verilerini almak için web formu oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="29b0b-118">The following code shows how to create a web form to retrieve user data for sending email.</span></span> <span data-ttu-id="29b0b-119">Bu içerik amaçları doğrultusunda JSP dosyası adlı **emailform.jsp**.</span><span class="sxs-lookup"><span data-stu-id="29b0b-119">For purposes of this content, the JSP file is named **emailform.jsp**.</span></span>

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

## <a name="create-the-code-to-send-the-email"></a><span data-ttu-id="29b0b-120">E-posta göndermek için kod oluşturma</span><span class="sxs-lookup"><span data-stu-id="29b0b-120">Create the code to send the email</span></span>
<span data-ttu-id="29b0b-121">Emailform.jsp biçiminde tamamladığınızda olarak adlandırılır, aşağıdaki kod, e-posta iletisi oluşturur ve bunu gönderir.</span><span class="sxs-lookup"><span data-stu-id="29b0b-121">The following code, which is called when you complete the form in emailform.jsp, creates the email message and sends it.</span></span> <span data-ttu-id="29b0b-122">Bu içerik amaçları doğrultusunda JSP dosyası adlı **sendemail.jsp**.</span><span class="sxs-lookup"><span data-stu-id="29b0b-122">For purposes of this content, the JSP file is named **sendemail.jsp**.</span></span>

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

<span data-ttu-id="29b0b-123">E-posta gönderme yanı sıra emailform.jsp kullanıcı için bir sonuç sağlar; Aşağıdaki ekran örneğidir:</span><span class="sxs-lookup"><span data-stu-id="29b0b-123">In addition to sending the email, emailform.jsp provides a result for the user; an example is the following screen shot:</span></span>

![Posta sonucunu gönderin][emailresult]

## <a name="next-steps"></a><span data-ttu-id="29b0b-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="29b0b-125">Next steps</span></span>
<span data-ttu-id="29b0b-126">İşlem öykünücüsü uygulamanızı dağıtmak ve bir tarayıcıdan emailform.jsp çalıştırmak, değerleri girin, tıklatın **bu e-posta Gönder**ve ardından sendemail.jsp sonuçlarında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29b0b-126">Deploy your application to the compute emulator and within a browser run emailform.jsp, enter values in the form, click **Send this email**, and then see results in sendemail.jsp.</span></span>

<span data-ttu-id="29b0b-127">Bu kod, Azure üzerinde Java SendGrid kullanmayı göstermek için sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="29b0b-127">This code was provided to show you how to use SendGrid in Java on Azure.</span></span> <span data-ttu-id="29b0b-128">Azure'a üretimde dağıtmadan önce daha fazla hata işleme veya diğer özellikler eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29b0b-128">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="29b0b-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="29b0b-129">For example:</span></span> 

* <span data-ttu-id="29b0b-130">E-posta adreslerini ve bir web formu kullanmak yerine, e-posta iletileri depolamak için Azure storage bloblarında veya SQL veritabanı'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29b0b-130">You could use Azure storage blobs or SQL Database to store email addresses and email messages, instead of using a web form.</span></span> <span data-ttu-id="29b0b-131">Azure storage bloblarında Java kullanma hakkında daha fazla bilgi için bkz: [Java'dan Blob Depolama hizmetini kullanmayı](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span><span class="sxs-lookup"><span data-stu-id="29b0b-131">For information about using Azure storage blobs in Java, see [How to Use the Blob Storage Service from Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/).</span></span> <span data-ttu-id="29b0b-132">SQL veritabanı Java kullanma hakkında daha fazla bilgi için bkz: [SQL veritabanında kullanarak Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span><span class="sxs-lookup"><span data-stu-id="29b0b-132">For information about using SQL Database in Java, see [Using SQL Database in Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).</span></span>
* <span data-ttu-id="29b0b-133">Kullanabileceğinizi `RoleEnvironment.getConfigurationSettings` bu değerleri almak için web formu kullanmak yerine dağıtımınızın yapılandırma ayarlarını SendGrid kullanıcı adı ve parola almalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="29b0b-133">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the SendGrid username and password from your deployment's configuration settings, instead of using the web form to retrieve those values.</span></span> <span data-ttu-id="29b0b-134">Hakkında bilgi için `RoleEnvironment` sınıfı için bkz: [JSP biçiminde Azure hizmeti çalışma zamanı kitaplığını kullanarak](http://msdn.microsoft.com/library/windowsazure/hh690948) ve Azure hizmet çalışma zamanı paketi belgelerine <http://dl.windowsazure.com/javadoc>.</span><span class="sxs-lookup"><span data-stu-id="29b0b-134">For information about the `RoleEnvironment` class, see [Using the Azure Service Runtime Library in JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) and the Azure Service Runtime package documentation at <http://dl.windowsazure.com/javadoc>.</span></span>
* <span data-ttu-id="29b0b-135">SendGrid Java kullanma hakkında daha fazla bilgi için bkz: [SendGrid Java kullanarak e-posta göndermek nasıl](store-sendgrid-java-how-to-send-email.md).</span><span class="sxs-lookup"><span data-stu-id="29b0b-135">For more information about using SendGrid in Java, see [How to send email using SendGrid from Java](store-sendgrid-java-how-to-send-email.md).</span></span>

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
