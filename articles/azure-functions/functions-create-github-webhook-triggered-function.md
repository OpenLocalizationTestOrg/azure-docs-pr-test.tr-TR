---
title: "Azure’da GitHub web kancası tarafından tetiklenen bir işlev oluşturma | Microsoft Docs"
description: "GitHub web kancası ile çağrılan sunucusuz işlev oluşturmak için Azure İşlevlerini kullanın."
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
ms.openlocfilehash: 038bb4cf0a9278416261c05ddaa0ee97d83b63c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="7b151-103">GitHub web kancası tarafından tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b151-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="7b151-104">GitHub’a özel bir yük kullanarak, HTTP web kancası isteğiyle tetiklenmiş bir işlev oluşturma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7b151-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Azure portalında GitHub Web Kancası ile tetiklenen işlev](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="7b151-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7b151-106">Prerequisites</span></span>

+ <span data-ttu-id="7b151-107">En az bir proje içeren bir GitHub hesabı.</span><span class="sxs-lookup"><span data-stu-id="7b151-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="7b151-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="7b151-108">An Azure subscription.</span></span> <span data-ttu-id="7b151-109">Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b151-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7b151-110">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b151-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="7b151-112">Ardından, yeni işlev uygulamasında bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b151-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="7b151-113">GitHub web kancası ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b151-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="7b151-114">İşlev uygulamanızı genişletin ve **İşlevler**'in yanındaki **+** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b151-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="7b151-115">Bu, işlev uygulamanızdaki ilk işlevse **Özel işlev**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="7b151-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="7b151-116">Böylece işlev şablonlarının tamamı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7b151-116">This displays the complete set of function templates.</span></span>

    ![Azure portalındaki İşlevler hızlı başlangıç sayfası](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="7b151-118">Seçin **GitHub Web kancası** istediğiniz dili için şablon.</span><span class="sxs-lookup"><span data-stu-id="7b151-118">Select the **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="7b151-119">**İşlevinizi adlandırın** ve ardından **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b151-119">**Name your function**, then select **Create**.</span></span>

     ![Azure portalında GitHub web kancası ile tetiklenen bir işlev oluşturma](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="7b151-121">Yeni işlevinizde, **</> İşlev URL’sini al**’a tıklayın, sonra da değerleri kopyalayın ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7b151-121">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="7b151-122">**</> GitHub parolasını al** için de aynı işlemi yapın.</span><span class="sxs-lookup"><span data-stu-id="7b151-122">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="7b151-123">GitHub’da web kancasını yapılandırırken bu değerleri kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7b151-123">You use these values to configure the webhook in GitHub.</span></span>

    ![İşlev kodunu gözden geçirme](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="7b151-125">Ardından, GitHub deponuzda web kancasını oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7b151-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="7b151-126">Web kancası yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b151-126">Configure the webhook</span></span>

1. <span data-ttu-id="7b151-127">GitHub’da sahip olduğunuz bir depoya gidin.</span><span class="sxs-lookup"><span data-stu-id="7b151-127">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="7b151-128">Varsa çatallandırdığınız depoları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b151-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="7b151-129">Bir depoyu çatallaştırmanız gerekirse, <https://github.com/Azure-Samples/functions-quickstart> sayfasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b151-129">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="7b151-130">**Ayarlar**’a tıklayın, sonra da **Web Kancaları**’na ve **Web kancası ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b151-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![GitHub web kancası ekleme](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="7b151-132">Tabloda belirtilen ayarları kullanın, ardından **Web kancası ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b151-132">Use settings as specified in the table, then click **Add webhook**.</span></span>

    ![Web kancası URL'sini ve parolasını ayarlama](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="7b151-134">Ayar</span><span class="sxs-lookup"><span data-stu-id="7b151-134">Setting</span></span> | <span data-ttu-id="7b151-135">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="7b151-135">Suggested value</span></span> | <span data-ttu-id="7b151-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7b151-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="7b151-137">**Yük URL'si**</span><span class="sxs-lookup"><span data-stu-id="7b151-137">**Payload URL**</span></span> | <span data-ttu-id="7b151-138">Kopyalanan değer</span><span class="sxs-lookup"><span data-stu-id="7b151-138">Copied value</span></span> | <span data-ttu-id="7b151-139">**</> İşlev URL’sini Al** tarafından döndürülen değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b151-139">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="7b151-140">**Gizli dizi**</span><span class="sxs-lookup"><span data-stu-id="7b151-140">**Secret**</span></span>   | <span data-ttu-id="7b151-141">Kopyalanan değer</span><span class="sxs-lookup"><span data-stu-id="7b151-141">Copied value</span></span> | <span data-ttu-id="7b151-142">**</> GitHub gizli dizisini al** tarafından döndürülen değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b151-142">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="7b151-143">**İçerik türü**</span><span class="sxs-lookup"><span data-stu-id="7b151-143">**Content type**</span></span> | <span data-ttu-id="7b151-144">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="7b151-144">application/json</span></span> | <span data-ttu-id="7b151-145">İşlev bir JSON yükü bekler.</span><span class="sxs-lookup"><span data-stu-id="7b151-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="7b151-146">Olay tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="7b151-146">Event triggers</span></span> | <span data-ttu-id="7b151-147">Olayları ayrı ayrı seçmeme izin ver</span><span class="sxs-lookup"><span data-stu-id="7b151-147">Let me select individual events</span></span> | <span data-ttu-id="7b151-148">Yalnızca sorun yorum olaylarını tetiklemek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="7b151-148">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="7b151-149">Sorun açıklaması</span><span class="sxs-lookup"><span data-stu-id="7b151-149">Issue comment</span></span> |  |

<span data-ttu-id="7b151-150">Şimdi, web kancası yeni bir sorun açıklaması eklendiğinde işlevinizi tetikleyecek şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="7b151-150">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="7b151-151">İşlevi test etme</span><span class="sxs-lookup"><span data-stu-id="7b151-151">Test the function</span></span>

1. <span data-ttu-id="7b151-152">GitHub deposunda **Sorunlar** sekmesini yeni bir tarayıcı penceresinde açın.</span><span class="sxs-lookup"><span data-stu-id="7b151-152">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="7b151-153">Yeni pencerede **Yeni Sorun**’a tıklayın, bir başlık yazın ve ardından **Yeni sorunu gönder**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b151-153">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="7b151-154">Sorunda bir açıklama yazın ve **Açıklama**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7b151-154">In the issue, type a comment and click **Comment**.</span></span>

    ![GitHub sorun açıklaması ekleyin.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="7b151-156">Portala geri dönün ve günlükleri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7b151-156">Go back to the portal and view the logs.</span></span> <span data-ttu-id="7b151-157">Yeni açıklama metnini içeren bir izleme girişi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b151-157">You should see a trace entry with the new comment text.</span></span>

     ![Günlüklerde açıklama metnini görüntüleyin.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="7b151-159">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="7b151-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="7b151-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b151-160">Next steps</span></span>

<span data-ttu-id="7b151-161">GitHub web kancasından istek alındığında çalıştırılan bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7b151-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7b151-162">Web kancası bağlamaları hakkında daha fazla bilgi için bkz. [Azure İşlevleri HTTP ve web kancası bağlamaları](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="7b151-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
