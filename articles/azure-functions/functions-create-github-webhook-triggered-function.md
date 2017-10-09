---
title: "aaaCreate GitHub Web kancası tarafından tetiklenen Azure işlevinde | Microsoft Docs"
description: "Azure işlevleri toocreate GitHub Web kancası tarafından çağrılan sunucusuz bir işlevini kullanın."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="79b63-103">GitHub web kancası tarafından tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b63-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="79b63-104">Bilgi nasıl toocreate HTTP Web kancası isteğiyle bir GitHub özgü yükü tarafından tetiklenen bir işlev.</span><span class="sxs-lookup"><span data-stu-id="79b63-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Github Web kancası hello Azure portal işlevinde tetiklendi](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="79b63-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79b63-106">Prerequisites</span></span>

+ <span data-ttu-id="79b63-107">En az bir proje içeren bir GitHub hesabı.</span><span class="sxs-lookup"><span data-stu-id="79b63-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="79b63-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="79b63-108">An Azure subscription.</span></span> <span data-ttu-id="79b63-109">Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="79b63-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="79b63-110">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b63-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="79b63-112">Ardından, hello yeni işlev uygulamada bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="79b63-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="79b63-113">GitHub web kancası ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="79b63-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="79b63-114">Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**.</span><span class="sxs-lookup"><span data-stu-id="79b63-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="79b63-115">Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**.</span><span class="sxs-lookup"><span data-stu-id="79b63-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="79b63-116">Merhaba eksiksiz işlev şablonları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="79b63-116">This displays hello complete set of function templates.</span></span>

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="79b63-118">Select hello **GitHub Web kancası** istediğiniz dili için şablon.</span><span class="sxs-lookup"><span data-stu-id="79b63-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="79b63-119">**İşlevinizi adlandırın** ve ardından **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b63-119">**Name your function**, then select **Create**.</span></span>

     ![GitHub Web kancası tetiklenen işlevi hello Azure portal oluşturma](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="79b63-121">Yeni işlevinizi tıklatın **<> / Get işlevi URL**, daha sonra kopyalayın ve başlangıç değerleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="79b63-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="79b63-122">Aynı şeyi hello **<> / alma GitHub gizli**.</span><span class="sxs-lookup"><span data-stu-id="79b63-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="79b63-123">Bu değerleri tooconfigure hello Web kancası Github'da kullanın.</span><span class="sxs-lookup"><span data-stu-id="79b63-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Merhaba işlevi kod gözden geçirme](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="79b63-125">Ardından, GitHub deponuzda web kancasını oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="79b63-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="79b63-126">Merhaba Web kancası yapılandırın</span><span class="sxs-lookup"><span data-stu-id="79b63-126">Configure hello webhook</span></span>

1. <span data-ttu-id="79b63-127">Github'da, sahip olduğunuz tooa depo gidin.</span><span class="sxs-lookup"><span data-stu-id="79b63-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="79b63-128">Varsa çatallandırdığınız depoları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79b63-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="79b63-129">Toofork depo gerekiyorsa kullanın <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="79b63-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="79b63-130">**Ayarlar**’a tıklayın, sonra da **Web Kancaları**’na ve **Web kancası ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="79b63-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![GitHub web kancası ekleme](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="79b63-132">Merhaba tabloda belirtildiği gibi ayarları kullanın ve ardından **Web kancası eklemek**.</span><span class="sxs-lookup"><span data-stu-id="79b63-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Merhaba Web kancası URL'si ve parolasını ayarlayın](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="79b63-134">Ayar</span><span class="sxs-lookup"><span data-stu-id="79b63-134">Setting</span></span> | <span data-ttu-id="79b63-135">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="79b63-135">Suggested value</span></span> | <span data-ttu-id="79b63-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79b63-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="79b63-137">**Yük URL'si**</span><span class="sxs-lookup"><span data-stu-id="79b63-137">**Payload URL**</span></span> | <span data-ttu-id="79b63-138">Kopyalanan değer</span><span class="sxs-lookup"><span data-stu-id="79b63-138">Copied value</span></span> | <span data-ttu-id="79b63-139">Tarafından döndürülen hello değeri kullanmak **<> / Get işlevi URL**.</span><span class="sxs-lookup"><span data-stu-id="79b63-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="79b63-140">**Gizli dizi**</span><span class="sxs-lookup"><span data-stu-id="79b63-140">**Secret**</span></span>   | <span data-ttu-id="79b63-141">Kopyalanan değer</span><span class="sxs-lookup"><span data-stu-id="79b63-141">Copied value</span></span> | <span data-ttu-id="79b63-142">Tarafından döndürülen hello değeri kullanmak **<> / alma GitHub gizli**.</span><span class="sxs-lookup"><span data-stu-id="79b63-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="79b63-143">**İçerik türü**</span><span class="sxs-lookup"><span data-stu-id="79b63-143">**Content type**</span></span> | <span data-ttu-id="79b63-144">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="79b63-144">application/json</span></span> | <span data-ttu-id="79b63-145">Merhaba işlevi bir JSON yükü bekliyor.</span><span class="sxs-lookup"><span data-stu-id="79b63-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="79b63-146">Olay tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="79b63-146">Event triggers</span></span> | <span data-ttu-id="79b63-147">Olayları ayrı ayrı seçmeme izin ver</span><span class="sxs-lookup"><span data-stu-id="79b63-147">Let me select individual events</span></span> | <span data-ttu-id="79b63-148">Yalnızca tootrigger sorunu açıklama olaylarına istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="79b63-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="79b63-149">Sorun açıklaması</span><span class="sxs-lookup"><span data-stu-id="79b63-149">Issue comment</span></span> |  |

<span data-ttu-id="79b63-150">Şimdi, Web kancası hello yeni bir sorun açıklama eklendiğinde yapılandırılmış tootrigger işlevinizi olur.</span><span class="sxs-lookup"><span data-stu-id="79b63-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="79b63-151">Test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="79b63-151">Test hello function</span></span>

1. <span data-ttu-id="79b63-152">Merhaba, GitHub deposunda açmak **sorunları** yeni bir tarayıcı penceresi sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="79b63-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="79b63-153">Merhaba yeni penceresinde **yeni sorun**bir başlık yazın ve ardından **yeni sorun gönderme**.</span><span class="sxs-lookup"><span data-stu-id="79b63-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="79b63-154">Merhaba sayısındaki bir yorum yazın ve'ı tıklatın **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="79b63-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![GitHub sorun açıklaması ekleyin.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="79b63-156">Toohello portalına geri dönün ve hello günlüklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="79b63-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="79b63-157">Merhaba yeni açıklama metni içeren bir izleme girişi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79b63-157">You should see a trace entry with hello new comment text.</span></span>

     ![Merhaba açıklama metni hello günlüklerinde görüntüleyin.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="79b63-159">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="79b63-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="79b63-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79b63-160">Next steps</span></span>

<span data-ttu-id="79b63-161">GitHub web kancasından istek alındığında çalıştırılan bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="79b63-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="79b63-162">Web kancası bağlamaları hakkında daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="79b63-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
