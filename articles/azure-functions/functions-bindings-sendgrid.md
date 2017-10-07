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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="78379-103">Azure işlevleri SendGrid bağlamaları</span><span class="sxs-lookup"><span data-stu-id="78379-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="78379-104">Bu makalede açıklanır nasıl tooconfigure ve Azure işlevlerinde SendGrid bağlamaları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="78379-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="78379-105">SendGrid Azure işlevleri toosend özelleştirilmiş e-posta programlı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78379-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="78379-106">Bu makalede, Azure işlevleri geliştiricileri için başvuru bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="78379-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="78379-107">Yeni tooAzure işlevleri değilseniz, kaynakları aşağıdaki hello ile başlayın:</span><span class="sxs-lookup"><span data-stu-id="78379-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="78379-108">[İlk Azure işlevinizi oluşturma](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="78379-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="78379-109">[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), veya [düğümü](functions-reference-node.md) Geliştirici başvuruları.</span><span class="sxs-lookup"><span data-stu-id="78379-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="78379-110">SendGrid bağlamaları için Function.JSON</span><span class="sxs-lookup"><span data-stu-id="78379-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="78379-111">Azure işlevleri için SendGrid bir çıktı bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="78379-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="78379-112">Merhaba SendGrid bağlama toocreate ve Gönder'e-posta program aracılığıyla sağlar çıktı.</span><span class="sxs-lookup"><span data-stu-id="78379-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="78379-113">Merhaba SendGrid bağlama aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="78379-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="78379-114">`name`: Gerekli - işlev kodu hello istek veya istek gövdesi için kullanılan hello değişken adı.</span><span class="sxs-lookup"><span data-stu-id="78379-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="78379-115">Bu değer ```$return``` yalnızca bir dönüş değeri olduğunda.</span><span class="sxs-lookup"><span data-stu-id="78379-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="78379-116">`type`: Gerekli - çok ayarlanmış olmalıdır "sendGrid."</span><span class="sxs-lookup"><span data-stu-id="78379-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="78379-117">`direction`: Gerekli - çok "out." ayarlanmış olmalıdır</span><span class="sxs-lookup"><span data-stu-id="78379-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="78379-118">`apiKey`: Gerekli - API anahtarınıza hello işlevi uygulamanın uygulama ayarlarında depolanan kümesi toohello adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="78379-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="78379-119">`to`: Merhaba alıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="78379-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="78379-120">`from`: Merhaba gönderenin e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="78379-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="78379-121">`subject`: hello e-postanın hello konu.</span><span class="sxs-lookup"><span data-stu-id="78379-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="78379-122">`text`: Merhaba e-posta içeriği.</span><span class="sxs-lookup"><span data-stu-id="78379-122">`text` : hello email content.</span></span>

<span data-ttu-id="78379-123">Örnek **function.json**:</span><span class="sxs-lookup"><span data-stu-id="78379-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="78379-124">Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez.</span><span class="sxs-lookup"><span data-stu-id="78379-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="78379-125">Bu eylem, hassas bilgilerinizi koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="78379-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="78379-126">C# hello SendGrid örneği bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="78379-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="78379-127">Bağlama SendGrid hello düğümü örnek çıkış</span><span class="sxs-lookup"><span data-stu-id="78379-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="78379-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78379-128">Next steps</span></span>
<span data-ttu-id="78379-129">Azure işlevleri için diğer bağlamalar ve tetikleyicileri hakkında bilgi için bkz</span><span class="sxs-lookup"><span data-stu-id="78379-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="78379-130">Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="78379-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="78379-131">[En iyi uygulamalar için Azure işlevleri](functions-best-practices.md) Azure işlevleri oluşturulurken bazı en iyi yöntemler toouse listeler.</span><span class="sxs-lookup"><span data-stu-id="78379-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="78379-132">[Azure işlevleri Geliştirici Başvurusu](functions-reference.md) işlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için Programcı Başvurusu.</span><span class="sxs-lookup"><span data-stu-id="78379-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
