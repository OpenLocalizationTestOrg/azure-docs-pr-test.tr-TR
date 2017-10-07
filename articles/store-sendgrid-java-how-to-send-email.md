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
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Nasıl tooSend e-posta kullanarak SendGrid Java'dan
Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri SendGrid tooperform e-posta gösterir. Merhaba örnekleri Java'da yazılmış. Merhaba kapsanan senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, **eklerini ekleme**, **filtreleri kullanarak**ve **özelliklerini güncelleştirme**. SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.

## <a name="what-is-hello-sendgrid-email-service"></a>Merhaba SendGrid e-posta hizmeti nedir?
SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra. Ortak SendGrid kullanım senaryoları şunları içerir:

* Otomatik olarak giriş toocustomers gönderme
* Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler
* Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama
* Toohelp eğilimleri belirlemek raporları oluşturma
* Müşteri sorguları iletme
* Uygulamanızdan e-posta bildirimleri

Daha fazla bilgi için bkz: <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>SendGrid hesabı oluşturma
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Nasıl yapılır: Merhaba javax.mail kitaplıkları kullanma
Merhaba javax.mail kitaplıkları, örneğin almak <http://www.oracle.com/technetwork/java/javamail> ve bunları kodunuza içeri aktarın. Bir üst düzey, hello SMTP aracılığıyla hello javax.mail kitaplığı toosend e-posta kullanma işlemini toodo hello aşağıda verilmiştir:

1. SendGrid için smtp.sendgrid.net hello SMTP sunucu dahil hello SMTP değerlerini belirtin.

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

1. Merhaba genişletmek *javax.mail.Authenticator* sınıfı ve uygulamanızda *getPasswordAuthentication* yöntemi, SendGrid kullanıcı adı ve parola döndürür.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Kimliği doğrulanmış e-posta oturumu aracılığıyla oluşturma bir *javax.mail.Session* nesnesi.  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. İletinizi oluşturun ve Ata **için**, **gelen**, **konu** ve içerik değerleri. Bu hello gösterilir [nasıl yapılır: bir e-posta oluşturma](#how-to-create-an-email) bölümü.
4. Merhaba iletisi göndermesi bir *javax.mail.Transport* nesnesi. Bu hello gösterilir [nasıl yapılır: bir e-posta Gönder] [nasıl yapılır: bir e-posta Gönder] bölümü.

## <a name="how-to-create-an-email"></a>Nasıl yapılır: bir e-posta oluşturma
Merhaba aşağıdaki nasıl toospecify için bir e-posta değerleri gösterir.

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

## <a name="how-to-send-an-email"></a>Nasıl yapılır: bir e-posta Gönder
gösterir nasıl aşağıdaki hello toosend bir e-posta.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Nasıl yapılır: bir eki ekleyin
Merhaba aşağıdaki kod, nasıl gösterir tooadd eki.

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Nasıl yapılır: kullanım filtreler tooenable altbilgiler, izleme ve analizi
SendGrid hello kullanımı aracılığıyla ek e-posta işlevselliği sağlayan *filtreleri*. İzleme'ye tıklayın, Google analytics, izleme, aboneliği etkinleştirme gibi belirli işlevleri etkinleştirmek için tooan e-posta iletisi eklenebilir ayarları bunlar ve benzeri. Filtrelerin tam bir listesi için bkz: [filtresi ayarlarını][Filter Settings].

* Merhaba aşağıdaki nasıl tooinsert altbilgi filtre hello e-posta gönderilmesini hello alt kısmında görünen HTML metin bu sonuçları gösterir.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Filtre başka bir örneği izleme tıklayın. Diyelim ki e-posta metninizi köprü içeren, tootrack hello hello aşağıdakileri yazın ve istediğiniz gibi oranı'ı tıklatın:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* tooenable hello tıklatın izleme, kod aşağıdaki kullanım hello:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Nasıl yapılır: güncelleştirme e-posta özellikleri
Bazı e-posta özellikleri kullanılarak üzerine yazılabilir  **ayarlamak*özelliği*** veya kullanarak eklenmiş  **ekleme*özelliği***.

Örneğin, toospecify **ReplyTo** adresleri hello aşağıdakileri kullanın:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd bir **Cc** alıcı, kullanım hello aşağıdaki:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Nasıl yapılır: ek SendGrid Hizmetleri kullanın
SendGrid sunan web tabanlı API'ler Azure uygulamanızı tooleverage işlevsellikler SendGrid kullanabilirsiniz. Tüm Ayrıntılar için bkz: hello [SendGrid API belgelerine][SendGrid API documentation].

## <a name="next-steps"></a>Sonraki adımlar
Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* Bir Azure dağıtımında SendGrid kullanarak oluşturulduğunu gösteren örnek: [toosend e-posta nasıl SendGrid Java'dan bir Azure dağıtımında kullanılması](store-sendgrid-java-how-to-send-email-example.md)
* SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html>
* SendGrid API belgelerine: <https://sendgrid.com/docs/API_Reference/index.html>
* SendGrid özel teklif Azure müşteriler: <https://sendgrid.com/windowsazure.html>

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
