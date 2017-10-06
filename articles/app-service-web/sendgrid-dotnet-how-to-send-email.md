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
# <a name="how-toosend-email-using-sendgrid-with-azure"></a><span data-ttu-id="943f1-104">Nasıl tooSend e-posta kullanarak SendGrid Azure ile</span><span class="sxs-lookup"><span data-stu-id="943f1-104">How tooSend Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="943f1-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="943f1-105">Overview</span></span>
<span data-ttu-id="943f1-106">Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri SendGrid tooperform e-posta gösterir.</span><span class="sxs-lookup"><span data-stu-id="943f1-106">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="943f1-107">Merhaba örnekleri C'de yazılmış\# ve .NET standart 1.3 destekler.</span><span class="sxs-lookup"><span data-stu-id="943f1-107">hello samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="943f1-108">Kapsanan hello senaryolar, e-posta oluşturma, e-posta gönderen, ekleri ekleme ve çeşitli posta etkinleştirme ve izleme ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="943f1-108">hello scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="943f1-109">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar] [ Next steps] bölümü.</span><span class="sxs-lookup"><span data-stu-id="943f1-109">For more information on SendGrid and sending email, see hello [Next steps][Next steps] section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="943f1-110">Merhaba SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="943f1-110">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="943f1-111">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="943f1-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="943f1-112">Ortak SendGrid kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="943f1-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="943f1-113">Otomatik olarak giriş veya satın alma onayı toocustomers gönderme.</span><span class="sxs-lookup"><span data-stu-id="943f1-113">Automatically sending receipts or purchase confirmations toocustomers.</span></span>
* <span data-ttu-id="943f1-114">Dağıtım yönetme aylık ilanları ve promosyonlar müşteriler göndermek için listeler.</span><span class="sxs-lookup"><span data-stu-id="943f1-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="943f1-115">Engellenen e-posta ve müşteri katılım gibi için gerçek zamanlı ölçümleri toplama.</span><span class="sxs-lookup"><span data-stu-id="943f1-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="943f1-116">İletme müşteri sorgular.</span><span class="sxs-lookup"><span data-stu-id="943f1-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="943f1-117">Gelen e-postaları işleniyor.</span><span class="sxs-lookup"><span data-stu-id="943f1-117">Processing incoming emails.</span></span>

<span data-ttu-id="943f1-118">Daha fazla bilgi için ziyaret [https://sendgrid.com](https://sendgrid.com) veya SendGrid'ın [C# Kitaplığı] [ sendgrid-csharp] GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="943f1-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="943f1-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="943f1-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-net-class-library"></a><span data-ttu-id="943f1-120">Merhaba SendGrid .NET sınıf kitaplığı başvurusu</span><span class="sxs-lookup"><span data-stu-id="943f1-120">Reference hello SendGrid .NET Class Library</span></span>
<span data-ttu-id="943f1-121">Merhaba [SendGrid NuGet paketi](https://www.nuget.org/packages/Sendgrid) hello en kolay yolu tooget hello SendGrid API tooconfigure tüm bağımlılıkları uygulamanızla ise.</span><span class="sxs-lookup"><span data-stu-id="943f1-121">hello [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is hello easiest way tooget hello SendGrid API and tooconfigure your application with all dependencies.</span></span> <span data-ttu-id="943f1-122">NuGet ve üstü, Microsoft Visual Studio 2015 ile dahil uzantısı kolay tooinstall ve güncelleştirme kitaplıklar ve Araçlar kolaylaştırır bir Visual Studio ' dir.</span><span class="sxs-lookup"><span data-stu-id="943f1-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy tooinstall and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="943f1-123">tooinstall NuGet Visual Studio Visual Studio 2015'ten önceki bir sürümünü çalıştırıyorsanız, ziyaret [http://www.nuget.org](http://www.nuget.org), hello tıklatıp **Nuget'i Yükle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="943f1-123">tooinstall NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click hello **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="943f1-124">tooinstall hello SendGrid NuGet paketi, uygulamanızda hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="943f1-124">tooinstall hello SendGrid NuGet package in your application, do hello following:</span></span>

1. <span data-ttu-id="943f1-125">Tıklayın **yeni proje** seçip bir **şablon**.</span><span class="sxs-lookup"><span data-stu-id="943f1-125">Click on **New Project** and select a **Template**.</span></span>

   ![Yeni bir proje oluşturma][create-new-project]
2. <span data-ttu-id="943f1-127">İçinde **Çözüm Gezgini**, sağ **başvuruları**, ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="943f1-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet paketi][SendGrid-NuGet-package]
3. <span data-ttu-id="943f1-129">Arama **SendGrid** ve select hello **SendGrid** sonuçlar listesinde öğesi.</span><span class="sxs-lookup"><span data-stu-id="943f1-129">Search for **SendGrid** and select hello **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="943f1-130">Merhaba sürümü açılır toobe mümkün toowork hello nesne modeli ve bu makalede gösterilen API'leri ile Merhaba en son kararlı sürümü hello Nuget paketi seçin.</span><span class="sxs-lookup"><span data-stu-id="943f1-130">Select hello latest stable version of hello Nuget package from hello version dropdown toobe able toowork with hello object model and APIs demonstrated in this article.</span></span>

   ![SendGrid paketi][sendgrid-package]
5. <span data-ttu-id="943f1-132">Tıklatın **yükleme** toocomplete hello yükleme ve bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="943f1-132">Click **Install** toocomplete hello installation, and then close this dialog.</span></span>

<span data-ttu-id="943f1-133">SendGrid'ın .NET sınıf kitaplığı çağrılır **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="943f1-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="943f1-134">Ad alanları aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="943f1-134">It contains hello following namespaces:</span></span>

* <span data-ttu-id="943f1-135">**SendGrid** SendGrid'ın API'si ile iletişim kurmak için.</span><span class="sxs-lookup"><span data-stu-id="943f1-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="943f1-136">**SendGrid.Helpers.Mail** için yardımcı yöntemleri tooeasily nasıl toosend e-postalar belirtin SendGridMessage nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="943f1-136">**SendGrid.Helpers.Mail** for helper methods tooeasily create SendGridMessage objects that specify how toosend emails.</span></span>

<span data-ttu-id="943f1-137">Aşağıdaki kodu ad alanı bildirimleri toohello üst tooprogrammatically erişim hello SendGrid e-posta hizmeti istediğiniz tüm C# dosyanın hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="943f1-137">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access hello SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="943f1-138">Nasıl yapılır: bir e-posta oluşturma</span><span class="sxs-lookup"><span data-stu-id="943f1-138">How to: Create an Email</span></span>
<span data-ttu-id="943f1-139">Kullanım hello **SendGridMessage** toocreate bir e-posta iletisi nesne.</span><span class="sxs-lookup"><span data-stu-id="943f1-139">Use hello **SendGridMessage** object toocreate an email message.</span></span> <span data-ttu-id="943f1-140">Merhaba ileti nesnesi oluşturulduktan sonra özellikleri ve yöntemleri hello e-posta gönderen, hello e-posta alıcısının ve hello konu ve hello e-posta gövdesi dahil olmak üzere, ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="943f1-140">Once hello message object is created, you can set properties and methods, including hello email sender, hello email recipient, and hello subject and body of hello email.</span></span>

<span data-ttu-id="943f1-141">Merhaba aşağıdaki örnekte gösterilmiştir nasıl toocreate tam olarak doldurulan bir e-posta nesnesi:</span><span class="sxs-lookup"><span data-stu-id="943f1-141">hello following example demonstrates how toocreate a fully populated email object:</span></span>

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

<span data-ttu-id="943f1-142">Tüm özellikleri ve yöntemleri tarafından desteklenen hakkında daha fazla bilgi için **SendGrid** yazın, bkz: [sendgrid csharp] [ sendgrid-csharp] github'da.</span><span class="sxs-lookup"><span data-stu-id="943f1-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="943f1-143">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="943f1-143">How to: Send an Email</span></span>
<span data-ttu-id="943f1-144">Bir e-posta iletisi oluşturduktan sonra SendGrid'ın API kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="943f1-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="943f1-145">Alternatif olarak, kullanabilir [. NET'in yerleşik Kitaplığı'nda][NET-library].</span><span class="sxs-lookup"><span data-stu-id="943f1-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="943f1-146">E-posta gönderilmesi SendGrid API anahtarınızı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="943f1-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="943f1-147">Hakkında ayrıntılı bilgi gerekirse tooconfigure API anahtarları, lütfen şu adresi ziyaret SendGrid'ın API anahtarları [belgelerine][documentation].</span><span class="sxs-lookup"><span data-stu-id="943f1-147">If you need details about how tooconfigure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="943f1-148">Bu kimlik bilgileri, Azure Portal tıklatarak uygulama ayarları ve uygulama ayarları altından ekleme hello anahtar/değer çiftleri tarafından aracılığıyla depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="943f1-148">You may store these credentials via your Azure Portal by clicking Application settings and adding hello key/value pairs under App settings.</span></span>

 ![Azure uygulama ayarları][azure_app_settings]

 <span data-ttu-id="943f1-150">Daha sonra bunları aşağıdaki gibi erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="943f1-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="943f1-151">Örnek hello nasıl bir iletiyi kullanarak toosend hello Web API gösterir.</span><span class="sxs-lookup"><span data-stu-id="943f1-151">hello following examples show how toosend a message using hello Web API.</span></span>

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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="943f1-152">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="943f1-152">How to: Add an attachment</span></span>
<span data-ttu-id="943f1-153">Ekleri eklenebilir tooa ileti ile arama hello **AddAttachment** yöntemi ve en düşük düzeyde hello dosya adı ve Base64 ile kodlanmış içeriği belirten tooattach istiyor.</span><span class="sxs-lookup"><span data-stu-id="943f1-153">Attachments can be added tooa message by calling hello **AddAttachment** method and minimally specifying hello file name and Base64 encoded content you want tooattach.</span></span> <span data-ttu-id="943f1-154">Her dosya için istediğiniz tooattach sonra bu yöntemi çağırmadan veya hello kullanarak birden çok eki içerebilir **AddAttachments** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="943f1-154">You can include multiple attachments by calling this method once for each file you wish tooattach or by using hello **AddAttachments** method.</span></span> <span data-ttu-id="943f1-155">Aşağıdaki örneğine hello ek tooa iletisine ekleme gösterir:</span><span class="sxs-lookup"><span data-stu-id="943f1-155">hello following example demonstrates adding an attachment tooa message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="943f1-156">Nasıl yapılır: posta ayarları tooenable altbilgiler, izleme ve analiz kullanma</span><span class="sxs-lookup"><span data-stu-id="943f1-156">How to: Use mail settings tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="943f1-157">SendGrid posta ve izleme ayarlarını hello kullanımı aracılığıyla ek e-posta işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="943f1-157">SendGrid provides additional email functionality through hello use of mail settings and tracking settings.</span></span> <span data-ttu-id="943f1-158">Bu ayarları tooan e-posta iletisi tooenable belirli işlevleri İzleme'ye tıklayın, Google analytics, izleme abonelik vb. gibi eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="943f1-158">These settings can be added tooan email message tooenable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="943f1-159">Merhaba uygulamaların tam listesi için bkz: [ayarları belgelerine][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="943f1-159">For a full list of apps, see hello [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="943f1-160">Uygulamalar çok uygulanabilir**SendGrid** e-posta iletileri hello bir parçası olarak uygulanan yöntemleri kullanarak **SendGridMessage** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="943f1-160">Apps can be applied too**SendGrid** email messages using methods implemented as part of hello **SendGridMessage** class.</span></span> <span data-ttu-id="943f1-161">Merhaba aşağıdaki örneklerde hello altbilgi göstermek ve filtreleri İzleme'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="943f1-161">hello following examples demonstrate hello footer and click tracking filters:</span></span>

<span data-ttu-id="943f1-162">Merhaba aşağıdaki örneklerde hello altbilgi göstermek ve filtreleri İzleme'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="943f1-162">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="943f1-163">Altbilgi ayarları</span><span class="sxs-lookup"><span data-stu-id="943f1-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="943f1-164">İzleme'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="943f1-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="943f1-165">Nasıl yapılır: ek SendGrid Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="943f1-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="943f1-166">SendGrid çeşitli API'ler ve Azure uygulamanızdaki tooleverage ek işlevsellik kullanabileceğiniz Web kancalarını sunar.</span><span class="sxs-lookup"><span data-stu-id="943f1-166">SendGrid offers several APIs and webhooks that you can use tooleverage additional functionality within your Azure application.</span></span> <span data-ttu-id="943f1-167">Daha fazla ayrıntı için bkz: Merhaba [SendGrid API Başvurusu][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="943f1-167">For more details, see hello [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="943f1-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="943f1-168">Next steps</span></span>
<span data-ttu-id="943f1-169">Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="943f1-169">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="943f1-170">SendGrid C\# kitaplığı deposu: [sendgrid csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="943f1-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="943f1-171">SendGrid API belgelerine: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="943f1-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

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

