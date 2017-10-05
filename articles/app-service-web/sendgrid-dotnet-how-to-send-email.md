---
title: SendGrid e-posta hizmetine (.NET) kullanma | Microsoft Docs
description: "Bilgi nasıl Azure üzerinde SendGrid e-posta hizmeti ile e-posta gönderin. C# dilinde yazılan kod örnekleri ve .NET API kullanır."
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
ms.openlocfilehash: b3a48b3c838763b022a18e55817ec7455fe94c85
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-send-email-using-sendgrid-with-azure"></a><span data-ttu-id="ba3fa-104">Azure ile SendGrid kullanarak e-posta gönderme</span><span class="sxs-lookup"><span data-stu-id="ba3fa-104">How to Send Email Using SendGrid with Azure</span></span>
## <a name="overview"></a><span data-ttu-id="ba3fa-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ba3fa-105">Overview</span></span>
<span data-ttu-id="ba3fa-106">Bu kılavuz, Azure üzerinde SendGrid e-posta hizmeti ile genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-106">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="ba3fa-107">Örnekler C yazılır\# ve .NET standart 1.3 destekler.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-107">The samples are written in C\# and supports .NET Standard 1.3.</span></span> <span data-ttu-id="ba3fa-108">Kapsamdaki senaryolar, e-posta oluşturma, e-posta gönderen, ekleri ekleme ve çeşitli posta etkinleştirme ve izleme ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-108">The scenarios covered include constructing email, sending email, adding attachments, and enabling various mail and tracking settings.</span></span> <span data-ttu-id="ba3fa-109">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: [sonraki adımlar] [ Next steps] bölümü.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-109">For more information on SendGrid and sending email, see the [Next steps][Next steps] section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="ba3fa-110">SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="ba3fa-110">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="ba3fa-111">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-111">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="ba3fa-112">Ortak SendGrid kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-112">Common SendGrid use cases include:</span></span>

* <span data-ttu-id="ba3fa-113">Otomatik olarak giriş veya satın alma onayı müşterilere gönderme.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-113">Automatically sending receipts or purchase confirmations to customers.</span></span>
* <span data-ttu-id="ba3fa-114">Dağıtım yönetme aylık ilanları ve promosyonlar müşteriler göndermek için listeler.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-114">Administering distribution lists for sending customers monthly fliers and promotions.</span></span>
* <span data-ttu-id="ba3fa-115">Engellenen e-posta ve müşteri katılım gibi için gerçek zamanlı ölçümleri toplama.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-115">Collecting real-time metrics for things like blocked email and customer engagement.</span></span>
* <span data-ttu-id="ba3fa-116">İletme müşteri sorgular.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-116">Forwarding customer inquiries.</span></span>
* <span data-ttu-id="ba3fa-117">Gelen e-postaları işleniyor.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-117">Processing incoming emails.</span></span>

<span data-ttu-id="ba3fa-118">Daha fazla bilgi için ziyaret [https://sendgrid.com](https://sendgrid.com) veya SendGrid'ın [C# Kitaplığı] [ sendgrid-csharp] GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-118">For more information, visit [https://sendgrid.com](https://sendgrid.com) or SendGrid's [C# library][sendgrid-csharp] GitHub repo.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="ba3fa-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba3fa-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-net-class-library"></a><span data-ttu-id="ba3fa-120">SendGrid .NET sınıf kitaplığı başvurusu</span><span class="sxs-lookup"><span data-stu-id="ba3fa-120">Reference the SendGrid .NET Class Library</span></span>
<span data-ttu-id="ba3fa-121">[SendGrid NuGet paketi](https://www.nuget.org/packages/Sendgrid) SendGrid API'sini almanın ve uygulamanızı tüm bağımlılıkları ile yapılandırmak için çok kolay yoludur.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-121">The [SendGrid NuGet package](https://www.nuget.org/packages/Sendgrid) is the easiest way to get the SendGrid API and to configure your application with all dependencies.</span></span> <span data-ttu-id="ba3fa-122">NuGet Microsoft Visual Studio 2015 ile birlikte bulunan bir Visual Studio uzantısı gerekir ve bu düzeyin yüklemek ve kitaplıklar ve Araçlar güncelleştirmek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-122">NuGet is a Visual Studio extension included with Microsoft Visual Studio 2015 and above that makes it easy to install and update libraries and tools.</span></span>

> [!NOTE]
> <span data-ttu-id="ba3fa-123">Visual Studio Visual Studio 2015'ten önceki bir sürümünü çalıştırıyorsanız, NuGet yüklemek için ziyaret edin [http://www.nuget.org](http://www.nuget.org), tıklatıp **Nuget'i Yükle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-123">To install NuGet if you are running a version of Visual Studio earlier than Visual Studio 2015, visit [http://www.nuget.org](http://www.nuget.org), and click the **Install NuGet** button.</span></span>
>
>

<span data-ttu-id="ba3fa-124">Uygulamanızda SendGrid NuGet paketini yüklemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-124">To install the SendGrid NuGet package in your application, do the following:</span></span>

1. <span data-ttu-id="ba3fa-125">Tıklayın **yeni proje** seçip bir **şablon**.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-125">Click on **New Project** and select a **Template**.</span></span>

   ![Yeni bir proje oluşturma][create-new-project]
2. <span data-ttu-id="ba3fa-127">İçinde **Çözüm Gezgini**, sağ **başvuruları**, ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-127">In **Solution Explorer**, right-click **References**, then click **Manage NuGet Packages**.</span></span>

   ![SendGrid NuGet paketi][SendGrid-NuGet-package]
3. <span data-ttu-id="ba3fa-129">Arama **SendGrid** seçip **SendGrid** sonuçlar listesinde öğesi.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-129">Search for **SendGrid** and select the **SendGrid** item in the results list.</span></span>
4. <span data-ttu-id="ba3fa-130">Nesne modeli ile çalışmak için sürüm açılır Nuget paketi en son kararlı sürümü seçin ve bu makalede API'leri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-130">Select the latest stable version of the Nuget package from the version dropdown to be able to work with the object model and APIs demonstrated in this article.</span></span>

   ![SendGrid paketi][sendgrid-package]
5. <span data-ttu-id="ba3fa-132">Tıklatın **yükleme** yüklemeyi tamamlamak ve sonra bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-132">Click **Install** to complete the installation, and then close this dialog.</span></span>

<span data-ttu-id="ba3fa-133">SendGrid'ın .NET sınıf kitaplığı çağrılır **SendGrid**.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-133">SendGrid's .NET class library is called **SendGrid**.</span></span> <span data-ttu-id="ba3fa-134">Şu ad alanlarından içerir:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-134">It contains the following namespaces:</span></span>

* <span data-ttu-id="ba3fa-135">**SendGrid** SendGrid'ın API'si ile iletişim kurmak için.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-135">**SendGrid** for communicating with SendGrid’s API.</span></span>
* <span data-ttu-id="ba3fa-136">**SendGrid.Helpers.Mail** kolayca e-postalar gönderme belirtin SendGridMessage nesneleri oluşturmak yardımcı yöntemler için.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-136">**SendGrid.Helpers.Mail** for helper methods to easily create SendGridMessage objects that specify how to send emails.</span></span>

<span data-ttu-id="ba3fa-137">Aşağıdaki kod ad alanı bildirimleri SendGrid e-posta hizmeti programlı olarak erişmek istediğiniz tüm C# dosyasının üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-137">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access the SendGrid email service.</span></span>

    using SendGrid;
    using SendGrid.Helpers.Mail;

## <a name="how-to-create-an-email"></a><span data-ttu-id="ba3fa-138">Nasıl yapılır: bir e-posta oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba3fa-138">How to: Create an Email</span></span>
<span data-ttu-id="ba3fa-139">Kullanım **SendGridMessage** bir e-posta iletisi oluşturmak için nesne.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-139">Use the **SendGridMessage** object to create an email message.</span></span> <span data-ttu-id="ba3fa-140">İleti nesnesi oluşturulduktan sonra özellikleri ve yöntemleri, e-posta gönderen, e-posta alıcısının ve konu ve gövde e-posta dahil olmak üzere ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-140">Once the message object is created, you can set properties and methods, including the email sender, the email recipient, and the subject and body of the email.</span></span>

<span data-ttu-id="ba3fa-141">Aşağıdaki örnek, bir tam olarak doldurulan bir e-posta nesnesinin nasıl oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-141">The following example demonstrates how to create a fully populated email object:</span></span>

    var msg = new SendGridMessage();

    msg.SetFrom(new EmailAddress("dx@example.com", "SendGrid DX Team"));

    var recipients = new List<EmailAddress>
    {
        new EmailAddress("jeff@example.com", "Jeff Smith"),
        new EmailAddress("anna@example.com", "Anna Lidman"),
        new EmailAddress("peter@example.com", "Peter Saddow")
    };
    msg.AddTos(recipients);

    msg.SetSubject("Testing the SendGrid C# Library");

    msg.AddContent(MimeType.Text, "Hello World plain text!");
    msg.AddContent(MimeType.Html, "<p>Hello World!</p>");

<span data-ttu-id="ba3fa-142">Tüm özellikleri ve yöntemleri tarafından desteklenen hakkında daha fazla bilgi için **SendGrid** yazın, bkz: [sendgrid csharp] [ sendgrid-csharp] github'da.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-142">For more information on all properties and methods supported by the **SendGrid** type, see [sendgrid-csharp][sendgrid-csharp] on GitHub.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="ba3fa-143">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="ba3fa-143">How to: Send an Email</span></span>
<span data-ttu-id="ba3fa-144">Bir e-posta iletisi oluşturduktan sonra SendGrid'ın API kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-144">After creating an email message, you can send it using SendGrid's API.</span></span> <span data-ttu-id="ba3fa-145">Alternatif olarak, kullanabilir [. NET'in yerleşik Kitaplığı'nda][NET-library].</span><span class="sxs-lookup"><span data-stu-id="ba3fa-145">Alternatively, you may use [.NET's built in library][NET-library].</span></span>

<span data-ttu-id="ba3fa-146">E-posta gönderilmesi SendGrid API anahtarınızı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-146">Sending email requires that you supply your SendGrid API Key.</span></span> <span data-ttu-id="ba3fa-147">API anahtarları yapılandırma hakkında ayrıntılar gerekiyorsa, lütfen SendGrid'ın API anahtarları adresini ziyaret edin [belgelerine][documentation].</span><span class="sxs-lookup"><span data-stu-id="ba3fa-147">If you need details about how to configure API Keys, please visit SendGrid's API Keys [documentation][documentation].</span></span>

<span data-ttu-id="ba3fa-148">Uygulama Ayarları'nı ve uygulama ayarları altından anahtar/değer çiftleri ekleyerek, Azure Portal bu kimlik bilgileri depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-148">You may store these credentials via your Azure Portal by clicking Application settings and adding the key/value pairs under App settings.</span></span>

 ![Azure uygulama ayarları][azure_app_settings]

 <span data-ttu-id="ba3fa-150">Daha sonra bunları aşağıdaki gibi erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-150">Then, you may access them as follows:</span></span>

    var apiKey = System.Environment.GetEnvironmentVariable("SENDGRID_APIKEY");
    var client = new SendGridClient(apiKey);

<span data-ttu-id="ba3fa-151">Aşağıdaki örnekler, Web API kullanarak ileti göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-151">The following examples show how to send a message using the Web API.</span></span>

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
                    Subject = "Hello World from the SendGrid CSharp SDK!",
                    PlainTextContent = "Hello, Email!",
                    HtmlContent = "<strong>Hello, Email!</strong>"
                };
                msg.AddTo(new EmailAddress("test@example.com", "Test User"));
                var response = await client.SendEmailAsync(msg);
            }
        }
    }

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="ba3fa-152">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="ba3fa-152">How to: Add an attachment</span></span>
<span data-ttu-id="ba3fa-153">Ekleri eklenebilir bir iletiye çağırarak **AddAttachment** yöntemi ve dosya adını ve Base64 ile kodlanmış içeriği en düşük düzeyde belirten eklemek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-153">Attachments can be added to a message by calling the **AddAttachment** method and minimally specifying the file name and Base64 encoded content you want to attach.</span></span> <span data-ttu-id="ba3fa-154">Eklemek istediğiniz her dosya için bir kez bu yöntemi çağırmadan veya kullanarak birden çok eki içerebilir **AddAttachments** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-154">You can include multiple attachments by calling this method once for each file you wish to attach or by using the **AddAttachments** method.</span></span> <span data-ttu-id="ba3fa-155">Aşağıdaki örnek, bir iletinin eki ekleme gösterir:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-155">The following example demonstrates adding an attachment to a message:</span></span>

    var banner2 = new Attachment()
    {
        Content = Convert.ToBase64String(raw_content),
        Type = "image/png",
        Filename = "banner2.png",
        Disposition = "inline",
        ContentId = "Banner 2"
    };
    msg.AddAttachment(banner2);

## <a name="how-to-use-mail-settings-to-enable-footers-tracking-and-analytics"></a><span data-ttu-id="ba3fa-156">Nasıl yapılır: altbilgi, izleme ve analiz etkinleştirmek için posta ayarları kullanın</span><span class="sxs-lookup"><span data-stu-id="ba3fa-156">How to: Use mail settings to enable footers, tracking, and analytics</span></span>
<span data-ttu-id="ba3fa-157">SendGrid posta ve izleme ayarlarını kullanarak ek e-posta işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-157">SendGrid provides additional email functionality through the use of mail settings and tracking settings.</span></span> <span data-ttu-id="ba3fa-158">Bu ayarlar, izleme'ye tıklayın, Google analytics, izleme abonelik vb. gibi belirli işlevleri etkinleştirmek için bir e-posta iletisine eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-158">These settings can be added to an email message to enable specific functionality such as click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="ba3fa-159">Uygulamaların tam listesi için bkz: [ayarları belgelerine][settings-documentation].</span><span class="sxs-lookup"><span data-stu-id="ba3fa-159">For a full list of apps, see the [Settings Documentation][settings-documentation].</span></span>

<span data-ttu-id="ba3fa-160">Uygulamalar uygulanabilir **SendGrid** e-posta iletileri bir parçası olarak uygulanan yöntemleri kullanarak **SendGridMessage** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-160">Apps can be applied to **SendGrid** email messages using methods implemented as part of the **SendGridMessage** class.</span></span> <span data-ttu-id="ba3fa-161">Aşağıdaki örnekler altbilgi göstermek ve filtreleri İzleme'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-161">The following examples demonstrate the footer and click tracking filters:</span></span>

<span data-ttu-id="ba3fa-162">Aşağıdaki örnekler altbilgi göstermek ve filtreleri İzleme'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="ba3fa-162">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer-settings"></a><span data-ttu-id="ba3fa-163">Altbilgi ayarları</span><span class="sxs-lookup"><span data-stu-id="ba3fa-163">Footer settings</span></span>
    msg.SetFooterSetting(
                         true,
                         "Some Footer HTML",
                         "<strong>Some Footer Text</strong>");

### <a name="click-tracking"></a><span data-ttu-id="ba3fa-164">İzleme'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="ba3fa-164">Click tracking</span></span>
    msg.SetClickTracking(true);

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="ba3fa-165">Nasıl yapılır: ek SendGrid Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ba3fa-165">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="ba3fa-166">SendGrid çeşitli API'ler ve Azure uygulamanız içinde ek işlevsellik yararlanmak için kullanabileceğiniz Web kancalarını sunar.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-166">SendGrid offers several APIs and webhooks that you can use to leverage additional functionality within your Azure application.</span></span> <span data-ttu-id="ba3fa-167">Daha fazla ayrıntı için bkz: [SendGrid API Başvurusu][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="ba3fa-167">For more details, see the [SendGrid API Reference][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba3fa-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba3fa-168">Next steps</span></span>
<span data-ttu-id="ba3fa-169">SendGrid e-posta hizmeti temel bilgileri öğrendiğinize göre daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ba3fa-169">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="ba3fa-170">SendGrid C\# kitaplığı deposu: [sendgrid csharp][sendgrid-csharp]</span><span class="sxs-lookup"><span data-stu-id="ba3fa-170">SendGrid C\# library repo: [sendgrid-csharp][sendgrid-csharp]</span></span>
* <span data-ttu-id="ba3fa-171">SendGrid API belgelerine: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="ba3fa-171">SendGrid API documentation: <https://sendgrid.com/docs></span></span>

[Next steps]: #next-steps
[What is the SendGrid Email Service?]: #whatis
[Create a SendGrid Account]: #createaccount
[Reference the SendGrid .NET Class Library]: #reference
[How to: Create an Email]: #createemail
[How to: Send an Email]: #sendemail
[How to: Add an Attachment]: #addattachment
[How to: Use Filters to Enable Footers, Tracking, and Analytics]: #usefilters
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

<span data-ttu-id="ba3fa-172">[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/solutions</span><span class="sxs-lookup"><span data-stu-id="ba3fa-172">[cloud-based email service]: https://sendgrid.com/solutions</span></span>
<span data-ttu-id="ba3fa-173">[işleme uygun e-posta teslimi]: https://sendgrid.com/use-cases/transactional-email</span><span class="sxs-lookup"><span data-stu-id="ba3fa-173">[transactional email delivery]: https://sendgrid.com/use-cases/transactional-email</span></span>

