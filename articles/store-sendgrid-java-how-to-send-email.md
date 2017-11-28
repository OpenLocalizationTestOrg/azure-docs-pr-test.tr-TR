---
title: aaaHow toouse hello SendGrid e-posta hizmetine (Java) | Microsoft Docs
description: "Bilgi nasıl Azure'da hello SendGrid e-posta hizmeti ile e-posta gönderin. Java dilinde yazılan kod örnekleri."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="72d4f-104">Nasıl tooSend e-posta kullanarak SendGrid Java'dan</span><span class="sxs-lookup"><span data-stu-id="72d4f-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="72d4f-105">Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri SendGrid tooperform e-posta gösterir.</span><span class="sxs-lookup"><span data-stu-id="72d4f-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="72d4f-106">Merhaba örnekleri Java'da yazılmış.</span><span class="sxs-lookup"><span data-stu-id="72d4f-106">hello samples are written in Java.</span></span> <span data-ttu-id="72d4f-107">Merhaba kapsanan senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, **eklerini ekleme**, **filtreleri kullanarak**ve **özelliklerini güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="72d4f-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="72d4f-108">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="72d4f-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="72d4f-109">Merhaba SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="72d4f-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="72d4f-110">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="72d4f-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="72d4f-111">Ortak SendGrid kullanım senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="72d4f-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="72d4f-112">Otomatik olarak giriş toocustomers gönderme</span><span class="sxs-lookup"><span data-stu-id="72d4f-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="72d4f-113">Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler</span><span class="sxs-lookup"><span data-stu-id="72d4f-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="72d4f-114">Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="72d4f-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="72d4f-115">Toohelp eğilimleri belirlemek raporları oluşturma</span><span class="sxs-lookup"><span data-stu-id="72d4f-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="72d4f-116">Müşteri sorguları iletme</span><span class="sxs-lookup"><span data-stu-id="72d4f-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="72d4f-117">Uygulamanızdan e-posta bildirimleri</span><span class="sxs-lookup"><span data-stu-id="72d4f-117">Email notifications from your application</span></span>

<span data-ttu-id="72d4f-118">Daha fazla bilgi için bkz: <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="72d4f-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="72d4f-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="72d4f-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="72d4f-120">Nasıl yapılır: Merhaba javax.mail kitaplıkları kullanma</span><span class="sxs-lookup"><span data-stu-id="72d4f-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="72d4f-121">Merhaba javax.mail kitaplıkları, örneğin almak <http://www.oracle.com/technetwork/java/javamail> ve bunları kodunuza içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="72d4f-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="72d4f-122">Bir üst düzey, hello SMTP aracılığıyla hello javax.mail kitaplığı toosend e-posta kullanma işlemini toodo hello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="72d4f-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="72d4f-123">SendGrid için smtp.sendgrid.net hello SMTP sunucu dahil hello SMTP değerlerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="72d4f-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. <span data-ttu-id="72d4f-124">Merhaba genişletmek *javax.mail.Authenticator* sınıfı ve uygulamanızda *getPasswordAuthentication* yöntemi, SendGrid kullanıcı adı ve parola döndürür.</span><span class="sxs-lookup"><span data-stu-id="72d4f-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="72d4f-125">Kimliği doğrulanmış e-posta oturumu aracılığıyla oluşturma bir *javax.mail.Session* nesnesi.</span><span class="sxs-lookup"><span data-stu-id="72d4f-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="72d4f-126">İletinizi oluşturun ve Ata **için**, **gelen**, **konu** ve içerik değerleri.</span><span class="sxs-lookup"><span data-stu-id="72d4f-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="72d4f-127">Bu hello gösterilir [nasıl yapılır: bir e-posta oluşturma](#how-to-create-an-email) bölümü.</span><span class="sxs-lookup"><span data-stu-id="72d4f-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="72d4f-128">Merhaba iletisi göndermesi bir *javax.mail.Transport* nesnesi.</span><span class="sxs-lookup"><span data-stu-id="72d4f-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="72d4f-129">Bu hello gösterilir [nasıl yapılır: bir e-posta Gönder] [nasıl yapılır: bir e-posta Gönder] bölümü.</span><span class="sxs-lookup"><span data-stu-id="72d4f-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="72d4f-130">Nasıl yapılır: bir e-posta oluşturma</span><span class="sxs-lookup"><span data-stu-id="72d4f-130">How to: Create an email</span></span>
<span data-ttu-id="72d4f-131">Merhaba aşağıdaki nasıl toospecify için bir e-posta değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="72d4f-131">hello following shows how toospecify values for an email.</span></span>

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a><span data-ttu-id="72d4f-132">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="72d4f-132">How to: Send an email</span></span>
<span data-ttu-id="72d4f-133">gösterir nasıl aşağıdaki hello toosend bir e-posta.</span><span class="sxs-lookup"><span data-stu-id="72d4f-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="72d4f-134">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="72d4f-134">How to: Add an attachment</span></span>
<span data-ttu-id="72d4f-135">Merhaba aşağıdaki kod, nasıl gösterir tooadd eki.</span><span class="sxs-lookup"><span data-stu-id="72d4f-135">hello following code shows you how tooadd an attachment.</span></span>

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="72d4f-136">Nasıl yapılır: kullanım filtreler tooenable altbilgiler, izleme ve analizi</span><span class="sxs-lookup"><span data-stu-id="72d4f-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="72d4f-137">SendGrid hello kullanımı aracılığıyla ek e-posta işlevselliği sağlayan *filtreleri*.</span><span class="sxs-lookup"><span data-stu-id="72d4f-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="72d4f-138">İzleme'ye tıklayın, Google analytics, izleme, aboneliği etkinleştirme gibi belirli işlevleri etkinleştirmek için tooan e-posta iletisi eklenebilir ayarları bunlar ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="72d4f-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="72d4f-139">Filtrelerin tam bir listesi için bkz: [filtresi ayarlarını][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="72d4f-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="72d4f-140">Merhaba aşağıdaki nasıl tooinsert altbilgi filtre hello e-posta gönderilmesini hello alt kısmında görünen HTML metin bu sonuçları gösterir.</span><span class="sxs-lookup"><span data-stu-id="72d4f-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="72d4f-141">Filtre başka bir örneği izleme tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72d4f-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="72d4f-142">Diyelim ki e-posta metninizi köprü içeren, tootrack hello hello aşağıdakileri yazın ve istediğiniz gibi oranı'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="72d4f-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="72d4f-143">tooenable hello tıklatın izleme, kod aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="72d4f-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="72d4f-144">Nasıl yapılır: güncelleştirme e-posta özellikleri</span><span class="sxs-lookup"><span data-stu-id="72d4f-144">How to: Update email properties</span></span>
<span data-ttu-id="72d4f-145">Bazı e-posta özellikleri kullanılarak üzerine yazılabilir  **ayarlamak*özelliği*** veya kullanarak eklenmiş  **ekleme*özelliği***.</span><span class="sxs-lookup"><span data-stu-id="72d4f-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="72d4f-146">Örneğin, toospecify **ReplyTo** adresleri hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="72d4f-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="72d4f-147">tooadd bir **Cc** alıcı, kullanım hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="72d4f-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="72d4f-148">Nasıl yapılır: ek SendGrid Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="72d4f-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="72d4f-149">SendGrid sunan web tabanlı API'ler Azure uygulamanızı tooleverage işlevsellikler SendGrid kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72d4f-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="72d4f-150">Tüm Ayrıntılar için bkz: hello [SendGrid API belgelerine][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="72d4f-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="72d4f-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72d4f-151">Next steps</span></span>
<span data-ttu-id="72d4f-152">Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="72d4f-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="72d4f-153">Bir Azure dağıtımında SendGrid kullanarak oluşturulduğunu gösteren örnek: [toosend e-posta nasıl SendGrid Java'dan bir Azure dağıtımında kullanılması](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="72d4f-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="72d4f-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="72d4f-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="72d4f-155">SendGrid API belgelerine: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="72d4f-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="72d4f-156">SendGrid özel teklif Azure müşteriler: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="72d4f-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/email-solutions
[işleme uygun e-posta teslimi]: https://sendgrid.com/transactional-email
