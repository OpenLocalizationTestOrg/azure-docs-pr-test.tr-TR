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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="53f6b-103">Azure işlevleri SendGrid bağlamaları</span><span class="sxs-lookup"><span data-stu-id="53f6b-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="53f6b-104">Bu makalede, yapılandırma ve Azure işlevlerinde SendGrid bağlamaları çalışmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="53f6b-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="53f6b-105">SendGrid program aracılığıyla özelleştirilmiş e-posta göndermek için Azure işlevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f6b-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="53f6b-106">Bu makalede, Azure işlevleri geliştiricileri için başvuru bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="53f6b-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="53f6b-107">Azure işlevleri yeniyseniz, aşağıdaki kaynaklarla başlatın:</span><span class="sxs-lookup"><span data-stu-id="53f6b-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="53f6b-108">[İlk Azure işlevinizi oluşturma](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="53f6b-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="53f6b-109">[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), veya [düğümü](functions-reference-node.md) Geliştirici başvuruları.</span><span class="sxs-lookup"><span data-stu-id="53f6b-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="53f6b-110">SendGrid bağlamaları için Function.JSON</span><span class="sxs-lookup"><span data-stu-id="53f6b-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="53f6b-111">Azure işlevleri için SendGrid bir çıktı bağlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f6b-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="53f6b-112">Etkinleştirir bağlama SendGrid çıktı oluşturmak ve göndermek için program aracılığıyla e-posta.</span><span class="sxs-lookup"><span data-stu-id="53f6b-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="53f6b-113">SendGrid bağlama aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="53f6b-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="53f6b-114">`name`: Gerekli - istek veya istek gövdesi için işlevi kod içinde kullanılan değişken adı.</span><span class="sxs-lookup"><span data-stu-id="53f6b-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="53f6b-115">Bu değer ```$return``` yalnızca bir dönüş değeri olduğunda.</span><span class="sxs-lookup"><span data-stu-id="53f6b-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="53f6b-116">`type`: Gerekli - "sendGrid" ayarlanmış olmalıdır</span><span class="sxs-lookup"><span data-stu-id="53f6b-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="53f6b-117">`direction`: Gerekli - out"." olarak ayarlı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="53f6b-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="53f6b-118">`apiKey`: Gerekli - API anahtarınıza işlevi uygulamanın uygulama ayarlarında depolanan adına ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="53f6b-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="53f6b-119">`to`: alıcının e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="53f6b-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="53f6b-120">`from`: gönderenin e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="53f6b-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="53f6b-121">`subject`: e-posta konusu.</span><span class="sxs-lookup"><span data-stu-id="53f6b-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="53f6b-122">`text`: e-posta içeriği.</span><span class="sxs-lookup"><span data-stu-id="53f6b-122">`text` : the email content.</span></span>

<span data-ttu-id="53f6b-123">Örnek **function.json**:</span><span class="sxs-lookup"><span data-stu-id="53f6b-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="53f6b-124">Azure işlevleri depolar bağlantı bilgilerini ve API anahtarlarını uygulama ayarlarda böylece kaynak denetimi deponuzun denetlenmez.</span><span class="sxs-lookup"><span data-stu-id="53f6b-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="53f6b-125">Bu eylem, hassas bilgilerinizi koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="53f6b-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="53f6b-126">C# SendGrid örneği bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="53f6b-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="53f6b-127">Bağlama SendGrid düğümü örnek çıkış</span><span class="sxs-lookup"><span data-stu-id="53f6b-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="53f6b-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53f6b-128">Next steps</span></span>
<span data-ttu-id="53f6b-129">Azure işlevleri için diğer bağlamalar ve tetikleyicileri hakkında bilgi için bkz</span><span class="sxs-lookup"><span data-stu-id="53f6b-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="53f6b-130">Azure işlevleri Tetikleyicileri ve bağlamaları Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="53f6b-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="53f6b-131">[En iyi uygulamalar için Azure işlevleri](functions-best-practices.md) Azure işlevleri oluşturulurken kullanılacak bazı en iyi uygulamaları listeler.</span><span class="sxs-lookup"><span data-stu-id="53f6b-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="53f6b-132">[Azure işlevleri Geliştirici Başvurusu](functions-reference.md) işlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için Programcı Başvurusu.</span><span class="sxs-lookup"><span data-stu-id="53f6b-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
