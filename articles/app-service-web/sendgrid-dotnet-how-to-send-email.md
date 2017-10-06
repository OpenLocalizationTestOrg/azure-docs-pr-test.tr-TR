---
title: aaaHow toouse hello SendGrid e-posta hizmetine (.NET) | Microsoft Docs
description: "Bilgi nasıl Azure'da hello SendGrid e-posta hizmeti ile e-posta gönderin. C# ve kullanım hello .NET API yazılan kod örnekleri."
services: app-service-web
documentationcenter: .net
author: thinkingserious
manager: erikre
editor: 
ms.assetid: 21bf4028-9046-476b-9799-3d3082a0f84c
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/15/2017
ms.author: dx@sendgrid.com
ms.openlocfilehash: b3d77bb67898b991c7293e6b9086b263f6bcb755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-with-azure"></a>Nasıl tooSend e-posta kullanarak SendGrid Azure ile
## <a name="overview"></a>Genel Bakış
Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri SendGrid tooperform e-posta gösterir. Merhaba örnekleri C'de yazılmış\# ve .NET standart 1.3 destekler. Kapsanan hello senaryolar, e-posta oluşturma, e-posta gönderen, ekleri ekleme ve çeşitli posta etkinleştirme ve izleme ayarları içerir. SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar] [ Next steps] bölümü.

## <a name="what-is-hello-sendgrid-email-service"></a>Merhaba SendGrid e-posta hizmeti nedir?
SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra. Ortak SendGrid kullanım örnekleri şunlardır:

* Otomatik olarak giriş veya satın alma onayı toocustomers gönderme.
* Dağıtım yönetme aylık ilanları ve promosyonlar müşteriler göndermek için listeler.
* Engellenen e-posta ve müşteri katılım gibi için gerçek zamanlı ölçümleri toplama.
* İletme müşteri sorgular.
* Gelen e-postaları işleniyor.

Daha fazla bilgi için ziyaret [https://sendgrid.com](https://sendgrid.com) veya SendGrid'ın [C# Kitaplığı] [ sendgrid-csharp] GitHub depo.

## <a name="create-a-sendgrid-account"></a>SendGrid hesabı oluşturma
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a>Merhaba SendGrid .NET sınıf kitaplığı başvurusu
Merhaba [SendGrid NuGet paketi](https://www.nuget.org/packages/Sendgrid) hello en kolay yolu tooget hello SendGrid API tooconfigure tüm bağımlılıkları uygulamanızla ise. NuGet ve üstü, Microsoft Visual Studio 2015 ile dahil uzantısı kolay tooinstall ve güncelleştirme kitaplıklar ve Araçlar kolaylaştırır bir Visual Studio ' dir.

> [!NOTE]
> tooinstall NuGet Visual Studio Visual Studio 2015'ten önceki bir sürümünü çalıştırıyorsanız, ziyaret [http://www.nuget.org](http://www.nuget.org), hello tıklatıp **Nuget'i Yükle** düğmesi.
>
>

tooinstall hello SendGrid NuGet paketi, uygulamanızda hello aşağıdaki:

1. Tıklayın **yeni proje** seçip bir **şablon**.

   ![Yeni bir proje oluşturma][create-new-project]
2. İçinde **Çözüm Gezgini**, sağ **başvuruları**, ardından **NuGet paketlerini Yönet**.

   ![SendGrid NuGet paketi][SendGrid-NuGet-package]
3. Arama **SendGrid** ve select hello **SendGrid** sonuçlar listesinde öğesi.
4. Merhaba sürümü açılır toobe mümkün toowork hello nesne modeli ve bu makalede gösterilen API'leri ile Merhaba en son kararlı sürümü hello Nuget paketi seçin.

   ![SendGrid paketi][sendgrid-package]
5. Tıklatın **yükleme** toocomplete hello yükleme ve bu iletişim kutusunu kapatın.

SendGrid'ın .NET sınıf kitaplığı çağrılır **SendGrid**. Ad alanları aşağıdaki hello içerir:

* **SendGrid** SendGrid'ın API'si ile iletişim kurmak için.
* **SendGrid.Helpers.Mail** için yardımcı yöntemleri tooeasily nasıl toosend e-postalar belirtin SendGridMessage nesne oluşturun.

Aşağıdaki kodu ad alanı bildirimleri toohello üst tooprogrammatically erişim hello SendGrid e-posta hizmeti istediğiniz tüm C# dosyanın hello ekleyin.

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a>Nasıl yapılır: bir e-posta oluşturma
Kullanım hello **SendGridMessage** toocreate bir e-posta iletisi nesne. Merhaba ileti nesnesi oluşturulduktan sonra özellikleri ve yöntemleri hello e-posta gönderen, hello e-posta alıcısının ve hello konu ve hello e-posta gövdesi dahil olmak üzere, ayarlayabilirsiniz.

Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate tam olarak doldurulan bir e-posta nesnesi:

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing hello SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

Tüm özellikleri ve yöntemleri tarafından desteklenen hakkında daha fazla bilgi için **SendGrid** yazın, bkz: [sendgrid csharp] [ sendgrid-csharp] github'da.

## <a name="how-to-send-an-email"></a>Nasıl yapılır: bir e-posta Gönder
Bir e-posta iletisi oluşturduktan sonra SendGrid'ın API kullanarak gönderebilirsiniz. Alternatif olarak, kullanabilir [. NET'in yerleşik Kitaplığı'nda][NET-library].

E-posta gönderilmesi SendGrid API anahtarınızı sağlamanız gerekir. Hakkında ayrıntılı bilgi gerekirse tooconfigure API anahtarları, lütfen şu adresi ziyaret SendGrid'ın API anahtarları [belgelerine][documentation].

Bu kimlik bilgileri, Azure Portal tıklatarak uygulama ayarları ve uygulama ayarları altından ekleme hello anahtar/değer çiftleri tarafından aracılığıyla depolayabilir.

 ![Azure uygulama ayarları][azure_app_settings]

 Daha sonra bunları aşağıdaki gibi erişebilirsiniz:

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

Örnek hello nasıl bir iletiyi kullanarak toosend hello Web API gösterir.

    using System;
    using System.Threading.Tasks;
    using SendGrid;
    using SendGrid.Helpers.Mail;

    namespace Example
    {
        internal class Example
        {
            private static void Main()
            {
                Execute().Wait();
            }

            static async Task Execute()
            {
                var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
                var client = new SendGridClient(apiKey);
                var msg = new SendGridMessage()
                {
                    From = new EmailAddress("test@example.com", "DX Team"),
                    Subject = "Hello World from hello SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a>Nasıl yapılır: bir eki ekleyin
Ekleri eklenebilir tooa ileti ile arama hello **AddAttachment** yöntemi ve en düşük düzeyde hello dosya adı ve Base64 ile kodlanmış içeriği belirten tooattach istiyor. Her dosya için istediğiniz tooattach sonra bu yöntemi çağırmadan veya hello kullanarak birden çok eki içerebilir **AddAttachments** yöntemi. Aşağıdaki örneğine hello ek tooa iletisine ekleme gösterir:

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a>Nasıl yapılır: posta ayarları tooenable altbilgiler, izleme ve analiz kullanma
SendGrid posta ve izleme ayarlarını hello kullanımı aracılığıyla ek e-posta işlevselliği sağlar. Bu ayarları tooan e-posta iletisi tooenable belirli işlevleri İzleme'ye tıklayın, Google analytics, izleme abonelik vb. gibi eklenebilir. Merhaba uygulamaların tam listesi için bkz: [ayarları belgelerine][settings-documentation].

Uygulamalar çok uygulanabilir**SendGrid** e-posta iletileri hello bir parçası olarak uygulanan yöntemleri kullanarak **SendGridMessage** sınıfı. Merhaba aşağıdaki örneklerde hello altbilgi göstermek ve filtreleri İzleme'yi tıklatın:

Merhaba aşağıdaki örneklerde hello altbilgi göstermek ve filtreleri İzleme'yi tıklatın:

### <a name="footer-settings"></a>Altbilgi ayarları
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a>İzleme'yi tıklatın
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a>Nasıl yapılır: ek SendGrid Hizmetleri kullanın
SendGrid çeşitli API'ler ve Azure uygulamanızdaki tooleverage ek işlevsellik kullanabileceğiniz Web kancalarını sunar. Daha fazla ayrıntı için bkz: Merhaba [SendGrid API Başvurusu][SendGrid API documentation].

## <a name="next-steps"></a>Sonraki adımlar
Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* SendGrid C\# kitaplığı deposu: [sendgrid csharp][sendgrid-csharp]
* SendGrid API belgelerine: <https://sendgrid.com/docs>

[Next steps]: #next-steps
[What is hello SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference hello SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters tooEnable Footers, Tracking, and Analytics]: #usefilters
[How to: Use Additional SendGrid Services]: #useservices

[create-new-project]: ./media/sendgrid-dotnet-how-to-send-email/new-project.png
[SendGrid-NuGet-package]: ./media/sendgrid-dotnet-how-to-send-email/reference.png
[sendgrid-package]: ./media/sendgrid-dotnet-how-to-send-email/sendgrid-package.png
[azure_app_settings]: ./media/sendgrid-dotnet-how-to-send-email/azure-app-settings.png
[sendgrid-csharp]: https://github.com/sendgrid/sendgrid-csharp
[SMTP vs. Web API]: https://sendgrid.com/docs/Integrate/index.html
[App Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/api_v3.html
[NET-library]: https://sendgrid.com/docs/Integrate/Code_Examples/v2_Mail/csharp.html#-Using-NETs-Builtin-SMTP-Library
[documentation]: https://sendgrid.com/docs/Classroom/Send/api_keys.html
[settings-documentation]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html

[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/solutions
[işleme uygun e-posta teslimi]: https://sendgrid.com/use-cases/transactional-email

