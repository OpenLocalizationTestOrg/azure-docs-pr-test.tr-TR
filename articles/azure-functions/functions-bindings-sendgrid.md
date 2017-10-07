---
title: "aaaAzure işlevleri SendGrid bağlamaları | Microsoft Docs"
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
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Azure işlevleri SendGrid bağlamaları

Bu makalede açıklanır nasıl tooconfigure ve Azure işlevlerinde SendGrid bağlamaları ile çalışır. SendGrid Azure işlevleri toosend özelleştirilmiş e-posta programlı olarak kullanabilirsiniz.

Bu makalede, Azure işlevleri geliştiricileri için başvuru bilgilerdir. Yeni tooAzure işlevleri değilseniz, kaynakları aşağıdaki hello ile başlayın:

[İlk Azure işlevinizi oluşturma](functions-create-first-azure-function.md). 
[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), veya [düğümü](functions-reference-node.md) Geliştirici başvuruları.

## <a name="functionjson-for-sendgrid-bindings"></a>SendGrid bağlamaları için Function.JSON

Azure işlevleri için SendGrid bir çıktı bağlama sağlar. Merhaba SendGrid bağlama toocreate ve Gönder'e-posta program aracılığıyla sağlar çıktı. 

Merhaba SendGrid bağlama aşağıdaki özelliklere hello destekler:

- `name`: Gerekli - işlev kodu hello istek veya istek gövdesi için kullanılan hello değişken adı. Bu değer ```$return``` yalnızca bir dönüş değeri olduğunda. 
- `type`: Gerekli - çok ayarlanmış olmalıdır "sendGrid."
- `direction`: Gerekli - çok "out." ayarlanmış olmalıdır
- `apiKey`: Gerekli - API anahtarınıza hello işlevi uygulamanın uygulama ayarlarında depolanan kümesi toohello adı olması gerekir.
- `to`: Merhaba alıcının e-posta adresi.
- `from`: Merhaba gönderenin e-posta adresi.
- `subject`: hello e-postanın hello konu.
- `text`: Merhaba e-posta içeriği.

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

## <a name="c-example-of-hello-sendgrid-output-binding"></a>C# hello SendGrid örneği bağlama çıktı

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Bağlama SendGrid hello düğümü örnek çıkış

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

- [En iyi uygulamalar için Azure işlevleri](functions-best-practices.md) Azure işlevleri oluşturulurken bazı en iyi yöntemler toouse listeler.

- [Azure işlevleri Geliştirici Başvurusu](functions-reference.md) işlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için Programcı Başvurusu.
