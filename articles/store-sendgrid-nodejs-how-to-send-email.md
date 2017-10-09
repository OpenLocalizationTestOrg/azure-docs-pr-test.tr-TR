---
title: aaaHow toouse hello SendGrid e-posta hizmetine (Node.js) | Microsoft Docs
description: "Bilgi nasıl Azure'da hello SendGrid e-posta hizmeti ile e-posta gönderin. Merhaba Node.js API kullanılarak yazılan kod örnekleri."
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
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a><span data-ttu-id="bdd8e-104">Nasıl tooSend e-posta kullanarak SendGrid node.js'den</span><span class="sxs-lookup"><span data-stu-id="bdd8e-104">How tooSend Email Using SendGrid from Node.js</span></span>
<span data-ttu-id="bdd8e-105">Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri SendGrid tooperform e-posta gösterir.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="bdd8e-106">Merhaba örnekleri hello Node.js API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-106">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="bdd8e-107">Merhaba kapsanan senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, **eklerini ekleme**, **filtreleri kullanarak**ve **özelliklerini güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="bdd8e-108">SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="bdd8e-109">Merhaba SendGrid e-posta hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="bdd8e-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="bdd8e-110">SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="bdd8e-111">Ortak SendGrid kullanım senaryoları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="bdd8e-112">Otomatik olarak giriş toocustomers gönderme</span><span class="sxs-lookup"><span data-stu-id="bdd8e-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="bdd8e-113">Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler</span><span class="sxs-lookup"><span data-stu-id="bdd8e-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="bdd8e-114">Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="bdd8e-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="bdd8e-115">Toohelp eğilimleri belirlemek raporları oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdd8e-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="bdd8e-116">Müşteri sorguları iletme</span><span class="sxs-lookup"><span data-stu-id="bdd8e-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="bdd8e-117">Uygulamanızdan e-posta bildirimleri</span><span class="sxs-lookup"><span data-stu-id="bdd8e-117">Email notifications from your application</span></span>

<span data-ttu-id="bdd8e-118">Daha fazla bilgi için bkz: [https://sendgrid.com](https://sendgrid.com).</span><span class="sxs-lookup"><span data-stu-id="bdd8e-118">For more information, see [https://sendgrid.com](https://sendgrid.com).</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="bdd8e-119">SendGrid hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdd8e-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a><span data-ttu-id="bdd8e-120">Başvuru hello SendGrid Node.js Modülü</span><span class="sxs-lookup"><span data-stu-id="bdd8e-120">Reference hello SendGrid Node.js Module</span></span>
<span data-ttu-id="bdd8e-121">Merhaba SendGrid modül Node.js için komutu aşağıdaki hello kullanarak hello düğüm paketi Yöneticisi (npm) yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-121">hello SendGrid module for Node.js can be installed through hello node package manager (npm) by using hello following command:</span></span>

    npm install sendgrid

<span data-ttu-id="bdd8e-122">Yükleme sonrasında, koddan hello kullanarak uygulamanızda hello modülü gerektirebilir:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-122">After installation, you can require hello module in your application by using hello following code:</span></span>

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

<span data-ttu-id="bdd8e-123">Merhaba SendGrid modülü aktarır hello **SendGrid** ve **e-posta** işlevleri.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-123">hello SendGrid module exports hello **SendGrid** and **Email** functions.</span></span>
<span data-ttu-id="bdd8e-124">**SendGrid** Web API aracılığıyla e-posta göndermekten sorumludur sırada **e-posta** bir e-posta iletisi yalıtır.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-124">**SendGrid** is responsible for sending email through Web API, while **Email** encapsulates an email message.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="bdd8e-125">Nasıl yapılır: bir e-posta oluşturma</span><span class="sxs-lookup"><span data-stu-id="bdd8e-125">How to: Create an Email</span></span>
<span data-ttu-id="bdd8e-126">Merhaba SendGrid modülü kullanılarak bir e-posta iletisi oluşturma e-posta iletisine hello e-posta işlevi kullanılarak ve sonra hello SendGrid işlevini kullanarak göndermeden önce oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-126">Creating an email message using hello SendGrid module involves first creating an email message using hello Email function, and then sending it using hello SendGrid function.</span></span> <span data-ttu-id="bdd8e-127">Merhaba, hello e-posta işlevi kullanarak yeni bir ileti oluşturma örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-127">hello following is an example of creating a new message using hello Email function:</span></span>

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

<span data-ttu-id="bdd8e-128">Merhaba html özelliği ayarlanarak destek istemciler için bir HTML iletisi de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-128">You can also specify an HTML message for clients that support it by setting hello html property.</span></span> <span data-ttu-id="bdd8e-129">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-129">For example:</span></span>

    html: This is a sample <b>HTML<b> email message.

<span data-ttu-id="bdd8e-130">Her iki hello metin ve html özellikleri ayarlama normal geri dönüş metin içeriği için HTML iletilerini destekleyemez istemcileri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-130">Setting both hello text and html properties provides graceful fallback to text content for clients that cannot support HTML messages.</span></span>

<span data-ttu-id="bdd8e-131">E-posta işlevi hello tarafından desteklenen tüm özellikleri hakkında daha fazla bilgi için bkz: [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="bdd8e-131">For more information on all properties supported by hello Email function, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="bdd8e-132">Nasıl yapılır: bir e-posta Gönder</span><span class="sxs-lookup"><span data-stu-id="bdd8e-132">How to: Send an Email</span></span>
<span data-ttu-id="bdd8e-133">Merhaba e-posta işlevi kullanarak e-posta iletisi oluşturduktan sonra hello SendGrid tarafından sağlanan Web API kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-133">After creating an email message using hello Email function, you can send it using hello Web API provided by SendGrid.</span></span> 

### <a name="web-api"></a><span data-ttu-id="bdd8e-134">Web API</span><span class="sxs-lookup"><span data-stu-id="bdd8e-134">Web API</span></span>
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> <span data-ttu-id="bdd8e-135">Merhaba örnekleri yukarıda gösterirken geçirme bir e-posta nesne ve geri çağırma işlevi, doğrudan e-posta özelliklerini belirterek hello gönderme işlevi doğrudan da çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-135">While hello above examples show passing in an email object and callback function, you can also directly invoke hello send function by directly specifying email properties.</span></span> <span data-ttu-id="bdd8e-136">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-136">For example:</span></span>  
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

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="bdd8e-137">Nasıl yapılır: bir eki ekleyin</span><span class="sxs-lookup"><span data-stu-id="bdd8e-137">How to: Add an Attachment</span></span>
<span data-ttu-id="bdd8e-138">Ekleri eklenebilir tooa ileti hello hello dosya adlarını ve yollarını belirterek **dosyaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-138">Attachments can be added tooa message by specifying hello file name(s) and path(s) in hello **files** property.</span></span> <span data-ttu-id="bdd8e-139">Aşağıdaki örnek hello eki gönderme gösterir:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-139">hello following example demonstrates sending an attachment:</span></span>

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> <span data-ttu-id="bdd8e-140">Merhaba kullanırken **dosyaları** özelliği, hello dosya olmalıdır üzerinden erişilebilir [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span><span class="sxs-lookup"><span data-stu-id="bdd8e-140">When using hello **files** property, hello file must be accessible through [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile).</span></span> <span data-ttu-id="bdd8e-141">Tooattach istediğiniz hello dosya olarak Azure Storage'da bir Blob kapsayıcısını olduğu gibi barındırılıyorsa hello kullanarak ek olarak gönderilmeden önce ilk hello dosya toolocal depolama veya tooan Azure sürücüsü kopyalamanız gerekir **dosyaları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-141">If hello file you wish tooattach is hosted in Azure Storage, such as in a Blob container, you must first copy hello file toolocal storage or tooan Azure drive before it can be sent as an attachment using hello **files** property.</span></span>
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a><span data-ttu-id="bdd8e-142">Nasıl yapılır: kullanım filtreleri tooEnable altbilgiler ve izleme</span><span class="sxs-lookup"><span data-stu-id="bdd8e-142">How to: Use Filters tooEnable Footers and Tracking</span></span>
<span data-ttu-id="bdd8e-143">SendGrid filtrelerin hello kullanımı aracılığıyla ek e-posta işlevselliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-143">SendGrid provides additional email functionality through hello use of filters.</span></span> <span data-ttu-id="bdd8e-144">İzleme'ye tıklayın, Google analytics, izleme, aboneliği etkinleştirme gibi belirli işlevleri etkinleştirmek için tooan e-posta iletisi eklenebilir ayarları bunlar ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-144">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="bdd8e-145">Filtrelerin tam bir listesi için bkz: [filtresi ayarlarını][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="bdd8e-145">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

<span data-ttu-id="bdd8e-146">Filtreler hello kullanarak uygulanan tooa ileti olabilir **filtreleri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-146">Filters can be applied tooa message by using hello **filters** property.</span></span>
<span data-ttu-id="bdd8e-147">Her filtre filtre özgü ayarları içeren bir karma tarafından belirtilir.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-147">Each filter is specified by a hash containing filter-specific settings.</span></span>
<span data-ttu-id="bdd8e-148">Merhaba aşağıdaki örneklerde hello altbilgi göstermek ve filtreleri İzleme'yi tıklatın:</span><span class="sxs-lookup"><span data-stu-id="bdd8e-148">hello following examples demonstrate hello footer and click tracking filters:</span></span>

### <a name="footer"></a><span data-ttu-id="bdd8e-149">Altbilgi</span><span class="sxs-lookup"><span data-stu-id="bdd8e-149">Footer</span></span>
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

### <a name="click-tracking"></a><span data-ttu-id="bdd8e-150">İzleme'yi tıklatın</span><span class="sxs-lookup"><span data-stu-id="bdd8e-150">Click Tracking</span></span>
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

## <a name="how-to-update-email-properties"></a><span data-ttu-id="bdd8e-151">Nasıl yapılır: güncelleştirme e-posta özellikleri</span><span class="sxs-lookup"><span data-stu-id="bdd8e-151">How to: Update Email Properties</span></span>
<span data-ttu-id="bdd8e-152">Bazı e-posta özellikleri kullanılarak üzerine yazılabilir  **ayarlamak*özelliği*** veya kullanarak eklenmiş  **ekleme*özelliği***.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-152">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span> <span data-ttu-id="bdd8e-153">Örneğin, kullanarak ek alıcılar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-153">For example, you can add additional recipients by using</span></span>

    email.addTo('jeff@contoso.com');

<span data-ttu-id="bdd8e-154">veya bir filtre kullanarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="bdd8e-154">or set a filter by using</span></span>

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

<span data-ttu-id="bdd8e-155">Daha fazla bilgi için bkz: [sendgrid nodejs][sendgrid-nodejs].</span><span class="sxs-lookup"><span data-stu-id="bdd8e-155">For more information, see [sendgrid-nodejs][sendgrid-nodejs].</span></span>

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="bdd8e-156">Nasıl yapılır: ek SendGrid Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="bdd8e-156">How to: Use Additional SendGrid Services</span></span>
<span data-ttu-id="bdd8e-157">SendGrid sunan web tabanlı API'ler Azure uygulamanızı tooleverage işlevsellikler SendGrid kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-157">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="bdd8e-158">Tüm Ayrıntılar için bkz: hello [SendGrid API belgelerine][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="bdd8e-158">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdd8e-159">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="bdd8e-159">Next Steps</span></span>
<span data-ttu-id="bdd8e-160">Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="bdd8e-160">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="bdd8e-161">SendGrid Node.js modülü deposu: [sendgrid nodejs][sendgrid-nodejs]</span><span class="sxs-lookup"><span data-stu-id="bdd8e-161">SendGrid Node.js module repository: [sendgrid-nodejs][sendgrid-nodejs]</span></span>
* <span data-ttu-id="bdd8e-162">SendGrid API belgelerine: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="bdd8e-162">SendGrid API documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="bdd8e-163">SendGrid özel teklif Azure müşteriler: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span><span class="sxs-lookup"><span data-stu-id="bdd8e-163">SendGrid special offer for Azure customers: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)</span></span>

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/email-solutions
[işleme uygun e-posta teslimi]: https://sendgrid.com/transactional-email
