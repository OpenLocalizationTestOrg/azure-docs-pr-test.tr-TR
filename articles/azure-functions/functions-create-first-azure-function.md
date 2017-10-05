---
title: "Azure portalında ilk işlevinizi oluşturma | Microsoft Docs"
description: "Azure portalını kullanarak sunucusuz yürütme için ilk Azure İşlevinizi oluşturma hakkında bilgi edinin."
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
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="ff01d-103">Azure portalında ilk işlevinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff01d-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="ff01d-104">Azure İşlevleri, öncelikle bir VM oluşturmak veya bir web uygulaması yayımlamak zorunda kalmadan kodunuzu sunucusuz bir ortamda yürütmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ff01d-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="ff01d-105">Bu konu başlığında, Azure portalında İşlevler’i kullanarak bir "hello world" işlevi oluşturmayı öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff01d-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Azure portalında işlev uygulaması oluşturma](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="ff01d-107">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="ff01d-107">Log in to Azure</span></span>

<span data-ttu-id="ff01d-108">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ff01d-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="ff01d-109">İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff01d-109">Create a function app</span></span>

<span data-ttu-id="ff01d-110">İşlevlerinizin yürütülmesini barındıran bir işlev uygulamasına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff01d-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="ff01d-111">İşlev uygulaması, kaynakların daha kolay yönetilmesi, dağıtılması ve paylaşılması için işlevleri bir mantıksal birim olarak gruplandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ff01d-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="ff01d-112">Ardından, yeni işlev uygulamasında bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff01d-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="ff01d-113"><a name="create-function"></a>HTTP ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff01d-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="ff01d-114">Yeni işlev uygulamanızı genişletin, ardından **İşlevler**’in yanındaki **+** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff01d-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="ff01d-115">**Hemen kullanmaya başlayın** sayfasında **Web Kancası + API**'ye tıklayın, **işleviniz için bir dil seçin** ve **Bu işlevi oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff01d-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Azure portalındaki İşlevler hızlı başlangıcı.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="ff01d-117">HTTP ile tetiklenen işlevin şablonu kullanılarak, seçtiğiniz dilde bir işlev oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ff01d-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="ff01d-118">Bir HTTP isteği göndererek yeni işlevi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff01d-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="ff01d-119">İşlevi test etme</span><span class="sxs-lookup"><span data-stu-id="ff01d-119">Test the function</span></span>

1. <span data-ttu-id="ff01d-120">Yeni işlevinizde **</> İşlev URL'sini al**'a tıklayın, **varsayılan (İşlev anahtarı)** seçeneğini belirleyin ve ardından **Kopyala**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff01d-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Azure portalından işlev URL’sini kopyalama](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="ff01d-122">İşlev URL'sini tarayıcınızın adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff01d-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="ff01d-123">Bu URL’ye `&name=<yourname>` sorgu dizesini ekleyin ve isteği yürütmek için klavyenizdeki `Enter` tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="ff01d-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="ff01d-124">Aşağıda, isteğin Edge tarayıcısında döndürülen bir yanıt örneğini gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ff01d-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Tarayıcıdaki işlev yanıtı.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="ff01d-126">İstek URL’si, işlevinize HTTP üzerinden erişmek için varsayılan olarak gerekli olan bir anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="ff01d-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="ff01d-127">İşleviniz çalıştığında, izleme bilgileri günlüklere yazılır.</span><span class="sxs-lookup"><span data-stu-id="ff01d-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="ff01d-128">Önceki yürütme işleminden alınan izleme çıktısını görmek için, portalda işlevinize geri dönün ve ekranın altındaki yukarı okuna tıklayarak **Günlükler**’i genişletin.</span><span class="sxs-lookup"><span data-stu-id="ff01d-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Azure portalında İşlevler günlük görüntüleyicisi.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ff01d-130">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="ff01d-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="ff01d-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff01d-131">Next steps</span></span>

<span data-ttu-id="ff01d-132">HTTP ile tetiklenen basit bir işlevi kullanarak işlev uygulaması oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ff01d-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="ff01d-133">Daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="ff01d-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



