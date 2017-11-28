---
title: "aaaHow toouse SendGrid Azure işlevlerinde | Microsoft Docs"
description: "Gösterir nasıl toouse Azure işlevlerinde SendGrid"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="034a6-103">Nasıl toouse Azure işlevlerinde SendGrid</span><span class="sxs-lookup"><span data-stu-id="034a6-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="034a6-104">SendGrid genel bakış</span><span class="sxs-lookup"><span data-stu-id="034a6-104">SendGrid Overview</span></span>

<span data-ttu-id="034a6-105">Azure işlevleri destekler SendGrid bağlamaları tooenable birkaç satır kod ve SendGrid hesabı, işlevleri toosend e-posta iletileriyle çıktı.</span><span class="sxs-lookup"><span data-stu-id="034a6-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="034a6-106">toouse hello SendGrid API bir Azure işlevi'olmalıdır bir [SendGrid hesap](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="034a6-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="034a6-107">Ayrıca, bir SendGrid API anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="034a6-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="034a6-108">Tooyour SendGrid hesap açın ve tıklayın **ayarları** sonra **API anahtarı** toogenerate bir API anahtarı.</span><span class="sxs-lookup"><span data-stu-id="034a6-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="034a6-109">Yaklaşan bir adımda kullanırken kullanılabilir bu anahtarı tutun.</span><span class="sxs-lookup"><span data-stu-id="034a6-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="034a6-110">Hazır toocreate bir Azure işlevi uygulama sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="034a6-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="034a6-111">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="034a6-111">Create an Azure Function app</span></span> 

<span data-ttu-id="034a6-112">Azure işlevi uygulamaları bir veya daha fazla Azure işlevleri için kapsayıcı görevi görür.</span><span class="sxs-lookup"><span data-stu-id="034a6-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="034a6-113">Azure işlevleri yalnızca - bir işlevi olan.</span><span class="sxs-lookup"><span data-stu-id="034a6-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="034a6-114">Merhaba işlevi toorun neden olan bir olay bağlı tooone tetikleyici her Azure işlevdir.</span><span class="sxs-lookup"><span data-stu-id="034a6-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="034a6-115">Her işlevi, giriş herhangi bir sayıda içermiyor ya da bağlamaları çıktı.</span><span class="sxs-lookup"><span data-stu-id="034a6-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="034a6-116">Bağlamaları bir işlevde kullanabileceğiniz hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="034a6-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="034a6-117">SendGrid, bağlama çıktı toosend e-postanızı kullanabileceğiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="034a6-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="034a6-118">Toohello Azure portalında oturum ve [Azure işlev uygulaması oluşturma](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) veya varolan bir işlev uygulaması açın.</span><span class="sxs-lookup"><span data-stu-id="034a6-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="034a6-119">Azure bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="034a6-119">Create an Azure function.</span></span> <span data-ttu-id="034a6-120">tookeep basit, onu seçin bir el ile tetikleyici ve C#.</span><span class="sxs-lookup"><span data-stu-id="034a6-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Bir Azure işlevi oluşturma](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="034a6-122">SendGrid bir Azure işlevi uygulamada kullanmak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="034a6-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="034a6-123">Bir uygulama ayarı toouse SendGrid API anahtarınıza depolamanız gerekir, bir işlev.</span><span class="sxs-lookup"><span data-stu-id="034a6-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="034a6-124">Merhaba apikey ile yapılan alan gerçek SendGrid API anahtarınıza değildir, ancak bir uygulama ayarı gerçek API anahtarınıza temsil eden tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="034a6-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="034a6-125">Herhangi bir kod veya kaynak kod denetimine iade dosyalarını ayrı olduğundan bu şekilde anahtarınızın depolanması güvenlik için kalır.</span><span class="sxs-lookup"><span data-stu-id="034a6-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="034a6-126">Oluşturma bir **AppSettings** işlevi uygulamanızın anahtar **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="034a6-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Bir Azure işlevi oluşturma](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="034a6-128">SendGrid çıkış bağlamaları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="034a6-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="034a6-129">SendGrid Azure kullanılabilir işlevi çıktı bağlama.</span><span class="sxs-lookup"><span data-stu-id="034a6-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="034a6-130">toocreate bir SendGrid bağlama çıktı:</span><span class="sxs-lookup"><span data-stu-id="034a6-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="034a6-131">Toohello Git **tümleştir** hello Azure portal hello işlevinde sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="034a6-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="034a6-132">Tıklatın **yeni çıktı** toocreate bir SendGrid çıkış bağlama.</span><span class="sxs-lookup"><span data-stu-id="034a6-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="034a6-133">Hello dolgu **API anahtarı** ve **ileti parametre adı** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="034a6-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="034a6-134">İsterseniz, girebilirsiniz diğer özellikleri artık hello veya bunun yerine kod.</span><span class="sxs-lookup"><span data-stu-id="034a6-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="034a6-135">Bu ayarlar varsayılan olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="034a6-135">These settings can be used as defaults.</span></span>

 ![SendGrid çıkış bağlamaları yapılandırma](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="034a6-137">Adlı bir dosya oluşturur bağlama tooa işlevi ekleme **function.json** , işlevin klasöründeki.</span><span class="sxs-lookup"><span data-stu-id="034a6-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="034a6-138">Tüm bu dosyayı içeren hello Azure işlevin hello bkz aynı bilgileri **tümleştir** sekmesinde ancak Json biçiminde.</span><span class="sxs-lookup"><span data-stu-id="034a6-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="034a6-139">Ayar hello **apikey ile yapılan**, **ileti**, ve **gelen** alanları oluşturmak hello girdiler aşağıdaki hello **function.json** dosyası:</span><span class="sxs-lookup"><span data-stu-id="034a6-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="034a6-140">Tercih ederseniz, bu değiştirebilen kendiniz dosyasını doğrudan.</span><span class="sxs-lookup"><span data-stu-id="034a6-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="034a6-141">Oluşturulan ve hello işlev uygulaması ve işlevi yapılandırılmış göre bir e-posta hello kod toosend yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="034a6-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="034a6-142">Oluşturur ve e-posta gönderir. kod yazma</span><span class="sxs-lookup"><span data-stu-id="034a6-142">Write code that creates and sends email</span></span>

<span data-ttu-id="034a6-143">Merhaba SendGrid API içeren tüm hello komutları toocreate gerekir ve bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="034a6-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="034a6-144">Merhaba işlevi Hello kodda koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="034a6-144">Replace hello code in hello function with hello following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="034a6-145">Bildirim hello ilk satırında hello ```#r``` hello SendGrid derlemeye başvuran yönergesi.</span><span class="sxs-lookup"><span data-stu-id="034a6-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="034a6-146">Bundan sonra kullanabileceğiniz bir ```using``` deyimi toomore hello nesneleri bu ad alanındaki kolayca erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="034a6-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="034a6-147">Merhaba kodda örneklerini oluşturmak ```Mail```, ```Personalization```, ve ```Content``` hello e-posta oluştur hello SendGrid API nesnelerden.</span><span class="sxs-lookup"><span data-stu-id="034a6-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="034a6-148">SendGrid selamlama iletisine döndüğünüzde sağlar.</span><span class="sxs-lookup"><span data-stu-id="034a6-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="034a6-149">Merhaba işlevin imza ayrıca fazladan çıkış parametresi türü içeren ```Mail``` adlı ```message```.</span><span class="sxs-lookup"><span data-stu-id="034a6-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="034a6-150">Her ikisi de giriş ve bağlamaları express kendilerini kod işlevi parametre olarak çıkış.</span><span class="sxs-lookup"><span data-stu-id="034a6-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="034a6-151">Kodunuzu tıklayarak test **Test** ve bir ileti hello girerek **istek gövdesinde** alan sonra hello tıklatarak **çalıştırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="034a6-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Kodunuzu test](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="034a6-153">SendGrid hello e-posta gönderilen e-posta tooverify denetleyin.</span><span class="sxs-lookup"><span data-stu-id="034a6-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="034a6-154">Adım 1'den toohello adresi hello kodda gidin ve hello hello iletiden içeren **istek gövdesinde**.</span><span class="sxs-lookup"><span data-stu-id="034a6-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="034a6-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="034a6-155">Next steps</span></span>
<span data-ttu-id="034a6-156">Bu makalede, nasıl toouse SendGrid hizmet toocreate hello ve e-posta Gönder gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="034a6-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="034a6-157">Uygulamalarınızda, Azure işlevlerini kullanma hakkında daha fazla toolearn aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="034a6-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="034a6-158">[En iyi uygulamalar için Azure işlevleri](functions-best-practices.md) Azure işlevleri oluşturulurken bazı en iyi yöntemler toouse listeler.</span><span class="sxs-lookup"><span data-stu-id="034a6-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="034a6-159">[Azure işlevleri Geliştirici Başvurusu](functions-reference.md) işlevleri kodlamak ve tetikleyicileri ve bağlamaları tanımlamak için Programcı Başvurusu.</span><span class="sxs-lookup"><span data-stu-id="034a6-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="034a6-160">[Azure işlevlerini test etme](functions-test-a-function.md) çeşitli araçları ve teknikleri işlevlerinizi test etmek için açıklar.</span><span class="sxs-lookup"><span data-stu-id="034a6-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>