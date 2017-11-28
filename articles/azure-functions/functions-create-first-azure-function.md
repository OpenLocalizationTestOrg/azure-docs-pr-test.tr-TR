---
title: "ilk işlev hello Azure Portalı ' aaaCreate | Microsoft Docs"
description: "Bilgi nasıl ilk Azure işlev kullanılarak sunucusuz yürütme için toocreate hello Azure portalı."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="8205d-103">Hello Azure portalını ilk işlevinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8205d-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="8205d-104">Azure işlevleri sağlayan bir VM oluşturun veya bir web uygulaması yayımlama toofirst gerek kalmadan sunucusuz bir ortamda kodunuzu yürütün.</span><span class="sxs-lookup"><span data-stu-id="8205d-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="8205d-105">Bu konuda, toouse toocreate hello Azure portalı "hello world" işlevinde nasıl çalıştığını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8205d-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Hello Azure portal işlev uygulaması oluşturma](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="8205d-107">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="8205d-107">Log in tooAzure</span></span>

<span data-ttu-id="8205d-108">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8205d-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="8205d-109">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8205d-109">Create a function app</span></span>

<span data-ttu-id="8205d-110">Bir işlev uygulaması toohost hello işlevlerinizin yürütülmesini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8205d-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="8205d-111">İşlev uygulaması, kaynakların daha kolay yönetilmesi, dağıtılması ve paylaşılması için işlevleri bir mantıksal birim olarak gruplandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8205d-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="8205d-112">Ardından, hello yeni işlev uygulamada bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8205d-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="8205d-113"><a name="create-function"></a>HTTP ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="8205d-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="8205d-114">Yeni işlev uygulamanız genişletin ve ardından hello  **+**  sonraki çok düğmesini**işlevler**.</span><span class="sxs-lookup"><span data-stu-id="8205d-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="8205d-115">Merhaba, **hızlı şekilde kullanmaya** sayfasında, **Web kancası + API**, **bir dil seçin** işlevi ve tıklatın **bu işlev oluşturma** .</span><span class="sxs-lookup"><span data-stu-id="8205d-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Hello Azure portal işlevleri hızlı başlangıcı.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="8205d-117">Bir işlev hello şablonu için bir HTTP tetiklenen işlevi kullanarak seçmiş olduğunuz dili oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8205d-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="8205d-118">Bir HTTP isteği göndererek hello yeni işlev çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8205d-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="8205d-119">Test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="8205d-119">Test hello function</span></span>

1. <span data-ttu-id="8205d-120">Yeni işlevinizde **</> İşlev URL'sini al**'a tıklayın, **varsayılan (İşlev anahtarı)** seçeneğini belirleyin ve ardından **Kopyala**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8205d-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Azure portal hello Hello işlevi URL'sini Kopyala](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="8205d-122">Merhaba işlevi URL'sini tarayıcınızın adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8205d-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="8205d-123">Merhaba sorgu dizesi eklemek `&name=<yourname>` toothis URL ve tuşuna hello `Enter` klavye tooexecute hello isteğiniz üzerinde anahtar.</span><span class="sxs-lookup"><span data-stu-id="8205d-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="8205d-124">Merhaba, hello Edge tarayıcısında hello işlevi tarafından döndürülen hello yanıt örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8205d-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Merhaba tarayıcıda işlev yanıtı.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="8205d-126">Merhaba istek URL'sini içerir, varsayılan olarak, tooaccess gerekli bir anahtarı işlevinizi HTTP üzerinden.</span><span class="sxs-lookup"><span data-stu-id="8205d-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="8205d-127">İşlevinizi çalıştığında, izleme bilgilerini toohello günlüklerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="8205d-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="8205d-128">Merhaba önceki yürütme toosee hello izleme çıktısını hello Portalı'nda tooyour işlevi dönün ve yukarı ok Merhaba ekranında tooexpand hello sonundaki hello **günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="8205d-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![İşlevler Görüntüleyicisi hello Azure portalında oturum açın.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="8205d-130">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="8205d-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="8205d-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8205d-131">Next steps</span></span>

<span data-ttu-id="8205d-132">HTTP ile tetiklenen basit bir işlevi kullanarak işlev uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="8205d-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="8205d-133">Daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="8205d-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



