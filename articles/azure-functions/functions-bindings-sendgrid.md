---
title: "Azure işlevleri SendGrid bağlamaları | Microsoft Docs"
description: "Azure işlevleri SendGrid bağlamaları başvurusu"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Azure işlevleri SendGrid bağlamaları

Bu makalede, yapılandırma ve Azure işlevlerinde SendGrid bağlamaları çalışmak açıklanmaktadır. SendGrid program aracılığıyla özelleştirilmiş e-posta göndermek için Azure işlevleri kullanabilirsiniz.

Bu makalede, Azure işlevleri geliştiricileri için başvuru bilgilerdir. Azure işlevleri yeniyseniz, aşağıdaki kaynaklarla başlatın:

[İlk Azure işlevinizi oluşturma](functions-create-first-azure-function.md). 
[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), veya [düğümü](functions-reference-node.md) Geliştirici başvuruları.

## <a name="functionjson-for-sendgrid-bindings"></a>SendGrid bağlamaları için Function.JSON

Azure işlevleri için SendGrid bir çıktı bağlama sağlar. Etkinleştirir bağlama SendGrid çıktı oluşturmak ve göndermek için program aracılığıyla e-posta. 

SendGrid bağlama aşağıdaki özellikleri destekler:

- `name`: Gerekli - istek veya istek gövdesi için işlevi kod içinde kullanılan değişken adı. Bu değer ```$return``` yalnızca bir dönüş değeri olduğunda. 
- `type`: Gerekli - "sendGrid" ayarlanmış olmalıdır
- `direction`: Gerekli - out"." olarak ayarlı olması gerekir
- `apiKey`: Gerekli - API anahtarınıza işlevi uygulamanın uygulama ayarlarında depolanan adına ayarlanması gerekir.
- `to`: alıcının e-posta adresi.
- `from`: gönderenin e-posta adresi.
- `subject`: e-posta konusu.
- `text`: e-posta içeriği.

Örnek **function.json**:

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez. Bu eylem, hassas bilgilerinizi koruma sağlar.
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a>C# SendGrid örneği bağlama çıktı

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-the-sendgrid-output-binding"></a>Bağlama SendGrid düğümü örnek çıkış

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>Sonraki adımlar
Azure işlevleri için diğer bağlamalar ve tetikleyicileri hakkında bilgi için bkz 
- [Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu](functions-triggers-bindings.md)

- [En iyi uygulamalar için Azure işlevleri](functions-best-practices.md) Azure işlevleri oluşturulurken kullanılacak bazı en iyi uygulamaları listeler.

- [Azure işlevleri Geliştirici Başvurusu](functions-reference.md) işlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için Programcı Başvurusu.
