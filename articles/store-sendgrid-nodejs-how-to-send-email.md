---
title: SendGrid e-posta hizmetine (Node.js) kullanma | Microsoft Docs
description: "Bilgi nasıl Azure üzerinde SendGrid e-posta hizmeti ile e-posta gönderin. Node.js API kullanılarak yazılan kod örnekleri."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: 327cea3a24cc47a9cc463b37cc2346ebc475ef7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="ddf74-104">SendGrid node.js'den kullanarak e-posta gönderme</span><span class="sxs-lookup"><span data-stu-id="ddf74-104">How to Send Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="ddf74-105">Bu kılavuz, Azure üzerinde SendGrid e-posta hizmeti ile genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ddf74-105">This guide demonstrates how to perform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="ddf74-106">Örnekler, Node.js API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="ddf74-106">The samples are written using the Node.js API.</span></span> <span data-ttu-id="ddf74-107">Kapsamdaki senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, **eklerini ekleme**, **filtreleri kullanarak**, ve **özelliklerini güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="ddf74-107">The scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="ddf74-108">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ddf74-108">For more information on SendGrid and sending email, see the [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-the-sendgrid-email-service"></a><span data-ttu-id="ddf74-109">SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="ddf74-109">What is the SendGrid Email Service?</span></span>
<span data-ttu-id="ddf74-110">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="ddf74-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="ddf74-111">Ortak SendGrid kullanım senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ddf74-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="ddf74-112">Giriş müşterileri için otomatik olarak gönderme</span><span class="sxs-lookup"><span data-stu-id="ddf74-112">Automatically sending receipts to customers</span></span>
* <span data-ttu-id="ddf74-113">Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler</span><span class="sxs-lookup"><span data-stu-id="ddf74-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="ddf74-114">Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="ddf74-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="ddf74-115">Eğilimleri belirlemenize yardımcı olmak için rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddf74-115">Generating reports to help identify trends</span></span>
* <span data-ttu-id="ddf74-116">Müşteri sorguları iletme</span><span class="sxs-lookup"><span data-stu-id="ddf74-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="ddf74-117">Uygulamanızdan e-posta bildirimleri</span><span class="sxs-lookup"><span data-stu-id="ddf74-117">Email notifications from your application</span></span>

<span data-ttu-id="ddf74-118">Daha fazla bilgi için bkz: [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="ddf74-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="ddf74-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddf74-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-the-sendgrid-nodejs-module"></a><span data-ttu-id="ddf74-120">SendGrid Node.js modülü başvurusu</span><span class="sxs-lookup"><span data-stu-id="ddf74-120">Reference the SendGrid Node.js Module</span></span>
<span data-ttu-id="ddf74-121">SendGrid modül Node.js için aşağıdaki komutu kullanarak (npm) düğüm paketi Yöneticisi yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="ddf74-121">The SendGrid module for Node.js can be installed through the node package manager (npm) by using the following command:</span></span>

    npm install sendgrid

<span data-ttu-id="ddf74-122">Yükleme tamamlandıktan sonra aşağıdaki kodu kullanarak uygulamanızda modülü gerektirebilir:</span><span class="sxs-lookup"><span data-stu-id="ddf74-122">After installation, you can require the module in your application by using the following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="ddf74-123">SendGrid modülü aktarır **SendGrid** ve **e-posta** işlevleri.</span><span class="sxs-lookup"><span data-stu-id="ddf74-123">The SendGrid module exports the **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="ddf74-124">**SendGrid** Web API aracılığıyla e-posta göndermekten sorumludur sırada **e-posta** bir e-posta iletisi yalıtır.</span><span class="sxs-lookup"><span data-stu-id="ddf74-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="ddf74-125">Nasıl yapılır: bir e-posta oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddf74-125">How to: Create an Email</span></span>
<span data-ttu-id="ddf74-126">SendGrid modülü kullanılarak bir e-posta iletisi oluşturmak önce e-posta işlevini kullanarak ve SendGrid işlevi kullanarak gönderme bir e-posta iletisi oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="ddf74-126">Creating an email message using the SendGrid module involves first creating an email message using the Email function, and then sending it using the SendGrid function.</span></span> <span data-ttu-id="ddf74-127">E-posta işlevi kullanarak yeni bir ileti oluşturma bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ddf74-127">The following is an example of creating a new message using the Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="ddf74-128">Html özelliği ayarlanarak destek istemciler için bir HTML iletisi de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddf74-128">You can also specify an HTML message for clients that support it by setting the html property.</span></span> <span data-ttu-id="ddf74-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ddf74-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="ddf74-130">Metin ve html özellikleri ayarlama normal geri dönüş metin içeriği için HTML iletilerini destekleyemez istemcileri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddf74-130">Setting both the text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="ddf74-131">E-posta işlevi tarafından desteklenen tüm özellikleri hakkında daha fazla bilgi için bkz: [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="ddf74-131">For more information on all properties supported by the Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="ddf74-132">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="ddf74-132">How to: Send an Email</span></span>
<span data-ttu-id="ddf74-133">E-posta işlevini kullanarak bir e-posta iletisi oluşturduktan sonra SendGrid tarafından sağlanan Web API kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddf74-133">After creating an email message using the Email function, you can send it using the Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="ddf74-134">Web API</span><span class="sxs-lookup"><span data-stu-id="ddf74-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="ddf74-135">Yukarıdaki örneklerde bir e-posta nesne ve geri çağırma işlevi geçirme gösterirken, doğrudan e-posta özelliklerini belirterek gönderme işlevi doğrudan da çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddf74-135">While the above examples show passing in an email object and callback function, you can also directly invoke the send function by directly specifying email properties.</span></span> <span data-ttu-id="ddf74-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ddf74-136">For example:</span></span>  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="ddf74-137">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="ddf74-137">How to: Add an Attachment</span></span>
<span data-ttu-id="ddf74-138">Ekleri eklenebilir bir iletiye yollarda ve dosya adları belirterek **dosyaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ddf74-138">Attachments can be added to a message by specifying the file name(s) and path(s) in the **files** property.</span></span> <span data-ttu-id="ddf74-139">Aşağıdaki örnek, bir ek gönderme gösterir:</span><span class="sxs-lookup"><span data-stu-id="ddf74-139">The following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used to specify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="ddf74-140">Kullanırken **dosyaları** özelliği, dosya olmalıdır üzerinden erişilebilir [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="ddf74-140">When using the **files** property, the file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="ddf74-141">Eklemek istediğiniz dosya olarak Azure Storage'da bir Blob kapsayıcısını olduğu gibi barındırılıyorsa kullanarak ek olarak gönderilmeden önce ilk dosyasını yerel depolama veya Azure sürücüye kopyalamanız gerekir **dosyaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ddf74-141">If the file you wish to attach is hosted in Azure Storage, such as in a Blob container, you must first copy the file to local storage or to an Azure drive before it can be sent as an attachment using the **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-to-enable-footers-and-tracking"></a><span data-ttu-id="ddf74-142">Nasıl yapılır: etkinleştir altbilgiler ve izleme için filtreleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ddf74-142">How to: Use Filters to Enable Footers and Tracking</span></span>
<span data-ttu-id="ddf74-143">SendGrid filtreleri kullanarak ek e-posta işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="ddf74-143">SendGrid provides additional email functionality through the use of filters.</span></span> <span data-ttu-id="ddf74-144">Bu izleme'ye tıklayın, Google analytics, izleme abonelik ve benzeri etkinleştirme gibi belirli işlevleri etkinleştirmek için e-posta iletisine eklenecek ayarlardır.</span><span class="sxs-lookup"><span data-stu-id="ddf74-144">These are settings that can be added to an email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="ddf74-145">Filtrelerin tam bir listesi için bkz: [filtresi ayarlarını][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="ddf74-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="ddf74-146">Filtreler uygulanabilir bir iletiyi kullanarak **filtreleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ddf74-146">Filters can be applied to a message by using the **filters** property.</span></span>
<span data-ttu-id="ddf74-147">Her filtre filtre özgü ayarları içeren bir karma tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ddf74-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="ddf74-148">Aşağıdaki örnekler altbilgi göstermek ve filtreleri İzleme'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="ddf74-148">The following examples demonstrate the footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="ddf74-149">Altbilgi</span><span class="sxs-lookup"><span data-stu-id="ddf74-149">Footer</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a><span data-ttu-id="ddf74-150">İzleme'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="ddf74-150">Click Tracking</span></span>
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a><span data-ttu-id="ddf74-151">Nasıl yapılır: güncelleştirme e-posta özellikleri</span><span class="sxs-lookup"><span data-stu-id="ddf74-151">How to: Update Email Properties</span></span>
<span data-ttu-id="ddf74-152">Bazı e-posta özellikleri kullanılarak üzerine yazılabilir  **ayarlamak*özelliği*** veya kullanarak eklenmiş  **ekleme*özelliği***.</span><span class="sxs-lookup"><span data-stu-id="ddf74-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="ddf74-153">Örneğin, kullanarak ek alıcılar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddf74-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="ddf74-154">veya bir filtre kullanarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ddf74-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="ddf74-155">Daha fazla bilgi için bkz: [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="ddf74-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="ddf74-156">Nasıl yapılır: ek SendGrid Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ddf74-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="ddf74-157">SendGrid Azure uygulamanızı ek SendGrid işlevinden yararlanmak için kullanabileceğiniz web tabanlı API'ler sunar.</span><span class="sxs-lookup"><span data-stu-id="ddf74-157">SendGrid offers web-based APIs that you can use to leverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="ddf74-158">Ayrıntılar için bkz: [SendGrid API belgelerine][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="ddf74-158">For full details, see the [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddf74-159">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ddf74-159">Next Steps</span></span>
<span data-ttu-id="ddf74-160">SendGrid e-posta hizmeti temel bilgileri öğrendiğinize göre daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ddf74-160">Now that you've learned the basics of the SendGrid Email service, follow these links to learn more.</span></span>

* <span data-ttu-id="ddf74-161">SendGrid Node.js modülü deposu: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="ddf74-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="ddf74-162">SendGrid API belgelerine: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="ddf74-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="ddf74-163">SendGrid özel teklif Azure müşteriler: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="ddf74-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
<span data-ttu-id="ddf74-164">[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/email-solutions</span><span class="sxs-lookup"><span data-stu-id="ddf74-164">[cloud-based email service]: https://sendgrid.com/email-solutions</span></span>
<span data-ttu-id="ddf74-165">[işleme uygun e-posta teslimi]: https://sendgrid.com/transactional-email</span><span class="sxs-lookup"><span data-stu-id="ddf74-165">[transactional email delivery]: https://sendgrid.com/transactional-email</span></span>
