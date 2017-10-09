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
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Nasıl tooSend e-posta kullanarak SendGrid node.js'den
Bu kılavuz, nasıl Azure hizmetine genel programlama görevleri SendGrid tooperform e-posta gösterir. Merhaba örnekleri hello Node.js API kullanılarak yazılır. Merhaba kapsanan senaryolar dahil **e-posta oluşturma**, **e-posta gönderme**, **eklerini ekleme**, **filtreleri kullanarak**ve **özelliklerini güncelleştirme**. SendGrid ve e-posta gönderme hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.

## <a name="what-is-hello-sendgrid-email-service"></a>Merhaba SendGrid e-posta hizmeti nedir?
SendGrid olan bir [bulut tabanlı e-posta hizmeti] güvenilir sağlayan [işleme uygun e-posta teslimi], ölçeklenebilirlik ve gerçek zamanlı analiz özel tümleştirme kolaylaştırmak esnek API'leri yanı sıra. Ortak SendGrid kullanım senaryoları şunları içerir:

* Otomatik olarak giriş toocustomers gönderme
* Aylık e ilanları ve özel teklifler müşteriler göndermek için dağıtım yönetme listeler
* Engellenen e-posta ve müşteri yanıtlama gibi için gerçek zamanlı ölçümleri toplama
* Toohelp eğilimleri belirlemek raporları oluşturma
* Müşteri sorguları iletme
* Uygulamanızdan e-posta bildirimleri

Daha fazla bilgi için bkz: [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>SendGrid hesabı oluşturma
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Başvuru hello SendGrid Node.js Modülü
Merhaba SendGrid modül Node.js için komutu aşağıdaki hello kullanarak hello düğüm paketi Yöneticisi (npm) yüklenebilir:

    npm install sendgrid

Yükleme sonrasında, koddan hello kullanarak uygulamanızda hello modülü gerektirebilir:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

Merhaba SendGrid modülü aktarır hello **SendGrid** ve **e-posta** işlevleri.
**SendGrid** Web API aracılığıyla e-posta göndermekten sorumludur sırada **e-posta** bir e-posta iletisi yalıtır.

## <a name="how-to-create-an-email"></a>Nasıl yapılır: bir e-posta oluşturma
Merhaba SendGrid modülü kullanılarak bir e-posta iletisi oluşturma e-posta iletisine hello e-posta işlevi kullanılarak ve sonra hello SendGrid işlevini kullanarak göndermeden önce oluşturma içerir. Merhaba, hello e-posta işlevi kullanarak yeni bir ileti oluşturma örneği aşağıdadır:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

Merhaba html özelliği ayarlanarak destek istemciler için bir HTML iletisi de belirtebilirsiniz. Örneğin:

    html: This is a sample <b>HTML<b> email message.

Her iki hello metin ve html özellikleri ayarlama normal geri dönüş metin içeriği için HTML iletilerini destekleyemez istemcileri için sağlar.

E-posta işlevi hello tarafından desteklenen tüm özellikleri hakkında daha fazla bilgi için bkz: [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Nasıl yapılır: bir e-posta Gönder
Merhaba e-posta işlevi kullanarak e-posta iletisi oluşturduktan sonra hello SendGrid tarafından sağlanan Web API kullanarak gönderebilirsiniz. 

### <a name="web-api"></a>Web API
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Merhaba örnekleri yukarıda gösterirken geçirme bir e-posta nesne ve geri çağırma işlevi, doğrudan e-posta özelliklerini belirterek hello gönderme işlevi doğrudan da çağırabilirsiniz. Örneğin:  
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

## <a name="how-to-add-an-attachment"></a>Nasıl yapılır: bir eki ekleyin
Ekleri eklenebilir tooa ileti hello hello dosya adlarını ve yollarını belirterek **dosyaları** özelliği. Aşağıdaki örnek hello eki gönderme gösterir:

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
> Merhaba kullanırken **dosyaları** özelliği, hello dosya olmalıdır üzerinden erişilebilir [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Tooattach istediğiniz hello dosya olarak Azure Storage'da bir Blob kapsayıcısını olduğu gibi barındırılıyorsa hello kullanarak ek olarak gönderilmeden önce ilk hello dosya toolocal depolama veya tooan Azure sürücüsü kopyalamanız gerekir **dosyaları** özelliği.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Nasıl yapılır: kullanım filtreleri tooEnable altbilgiler ve izleme
SendGrid filtrelerin hello kullanımı aracılığıyla ek e-posta işlevselliği sağlar. İzleme'ye tıklayın, Google analytics, izleme, aboneliği etkinleştirme gibi belirli işlevleri etkinleştirmek için tooan e-posta iletisi eklenebilir ayarları bunlar ve benzeri. Filtrelerin tam bir listesi için bkz: [filtresi ayarlarını][Filter Settings].

Filtreler hello kullanarak uygulanan tooa ileti olabilir **filtreleri** özelliği.
Her filtre filtre özgü ayarları içeren bir karma tarafından belirtilir.
Merhaba aşağıdaki örneklerde hello altbilgi göstermek ve filtreleri İzleme'yi tıklatın:

### <a name="footer"></a>Altbilgi
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

### <a name="click-tracking"></a>İzleme'yi tıklatın
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

## <a name="how-to-update-email-properties"></a>Nasıl yapılır: güncelleştirme e-posta özellikleri
Bazı e-posta özellikleri kullanılarak üzerine yazılabilir  **ayarlamak*özelliği*** veya kullanarak eklenmiş  **ekleme*özelliği***. Örneğin, kullanarak ek alıcılar ekleyebilirsiniz.

    email.addTo('jeff@contoso.com');

veya bir filtre kullanarak ayarlayın

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Daha fazla bilgi için bkz: [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Nasıl yapılır: ek SendGrid Hizmetleri kullanın
SendGrid sunan web tabanlı API'ler Azure uygulamanızı tooleverage işlevsellikler SendGrid kullanabilirsiniz. Tüm Ayrıntılar için bkz: hello [SendGrid API belgelerine][SendGrid API documentation].

## <a name="next-steps"></a>Sonraki Adımlar
Merhaba SendGrid e-posta hizmeti hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* SendGrid Node.js modülü deposu: [sendgrid nodejs][sendgrid-nodejs]
* SendGrid API belgelerine: <https://sendgrid.com/docs>
* SendGrid özel teklif Azure müşteriler: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[bulut tabanlı e-posta hizmeti]: https://sendgrid.com/email-solutions
[işleme uygun e-posta teslimi]: https://sendgrid.com/transactional-email
