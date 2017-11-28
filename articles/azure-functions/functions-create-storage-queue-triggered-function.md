---
title: "Azure kuyruk iletileri tarafından tetiklenen bir işlev aaaCreate | Microsoft Docs"
description: "Kullanım Azure işlevleri toocreate iletileri tarafından çağrılan sunucusuz bir işlev tooan Azure depolama kuyruğu gönderildi."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="54839-103">Azure Kuyruk Depolama tarafından tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="54839-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="54839-104">Nasıl toocreate iletileri olduğunda tetiklenen bir işlev tooan Azure Storage kuyruğuna gönderilen bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="54839-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="54839-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="54839-106">Prerequisites</span></span>

- <span data-ttu-id="54839-107">Merhaba yükleyip [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="54839-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="54839-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="54839-108">An Azure subscription.</span></span> <span data-ttu-id="54839-109">Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54839-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="54839-110">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="54839-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="54839-112">Ardından, hello yeni işlev uygulamada bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54839-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="54839-113">Kuyruk ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="54839-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="54839-114">Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**.</span><span class="sxs-lookup"><span data-stu-id="54839-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="54839-115">Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**.</span><span class="sxs-lookup"><span data-stu-id="54839-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="54839-116">Merhaba eksiksiz işlev şablonları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="54839-116">This displays hello complete set of function templates.</span></span>

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="54839-118">Select hello **QueueTrigger** şablonu istediğiniz dili ve hello tabloda belirtildiği gibi hello ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="54839-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Merhaba depolama kuyruğu tetiklenen bir işlev oluşturun.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="54839-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="54839-120">Setting</span></span> | <span data-ttu-id="54839-121">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="54839-121">Suggested value</span></span> | <span data-ttu-id="54839-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="54839-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="54839-123">**Kuyruk adı**</span><span class="sxs-lookup"><span data-stu-id="54839-123">**Queue name**</span></span>   | <span data-ttu-id="54839-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="54839-124">myqueue-items</span></span>    | <span data-ttu-id="54839-125">Merhaba adını, depolama hesabınız tooconnect tooin sırası.</span><span class="sxs-lookup"><span data-stu-id="54839-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="54839-126">**Depolama hesabı bağlantısı**</span><span class="sxs-lookup"><span data-stu-id="54839-126">**Storage account connection**</span></span> | <span data-ttu-id="54839-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="54839-127">AzureWebJobStorage</span></span> | <span data-ttu-id="54839-128">Merhaba depolama hesabı bağlantısı işlevi uygulamanız tarafından zaten kullanılmakta kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54839-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="54839-129">**İşlevinizi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="54839-129">**Name your function**</span></span> | <span data-ttu-id="54839-130">İşlev uygulamanızda benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="54839-130">Unique in your function app</span></span> | <span data-ttu-id="54839-131">Kuyruk tarafından tetiklenen bu işlevin adı.</span><span class="sxs-lookup"><span data-stu-id="54839-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="54839-132">Tıklatın **oluşturma** toocreate işlevinizi.</span><span class="sxs-lookup"><span data-stu-id="54839-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="54839-133">Ardından, tooyour Azure depolama hesabı bağlanmak ve hello oluşturmak **Sıram öğeleri** depolama kuyruğu.</span><span class="sxs-lookup"><span data-stu-id="54839-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="54839-134">Merhaba kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="54839-134">Create hello queue</span></span>

1. <span data-ttu-id="54839-135">İşlevinizde **Tümleştir**'e tıklayın, **Belgeler**'i genişletin ve hem **Hesap adı** hem de **Hesap anahtarı** değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="54839-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="54839-136">Bu kimlik bilgileri tooconnect toohello depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="54839-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="54839-137">Depolama hesabınız zaten bağlanmış olduğunuz toostep 4 atlayın.</span><span class="sxs-lookup"><span data-stu-id="54839-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Merhaba depolama hesabı bağlantısı kimlik bilgilerini edinin.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="54839-139">v</span><span class="sxs-lookup"><span data-stu-id="54839-139">v</span></span>

1. <span data-ttu-id="54839-140">Merhaba çalıştırmak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/) aracı, hello tıklatın Bağlan simgesi hello sol tarafta, seçin **bir depolama hesabı adı ve anahtar kullanmak**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="54839-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Merhaba depolama hesabı Gezgini aracını çalıştırın.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="54839-142">Merhaba girin **hesap adı** ve **hesap anahtarı** 1. adımdaki tıklatın **sonraki** ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="54839-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Merhaba depolama kimlik bilgilerini girin ve bağlanın.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="54839-144">Merhaba bağlı depolama hesabı'nı genişletin, sağ tıklatın **sıraları**, tıklatın **Oluşturma sırası**, türü `myqueue-items`, ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="54839-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Depolama kuyruğu oluşturun.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="54839-146">Bir depolama kuyruğu sahip olduğunuza göre bir ileti toohello sırası ekleyerek hello işlevi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54839-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="54839-147">Test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="54839-147">Test hello function</span></span>

1. <span data-ttu-id="54839-148">Geri Azure portal hello, Gözat tooyour işlevi genişletin hello **günlükleri** hello sonunda hello sayfası ve emin olun, bu günlük akış duraklatıldı değil.</span><span class="sxs-lookup"><span data-stu-id="54839-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="54839-149">Depolama Gezgini'nde depolama hesabınızı genişletin, **Kuyruklar**'ı ve **myqueue-items** öğesini seçip **İleti ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="54839-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Bir ileti toohello sırası ekleyin.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="54839-151">"Hello World!" iletinizi</span><span class="sxs-lookup"><span data-stu-id="54839-151">Type your "Hello World!"</span></span> <span data-ttu-id="54839-152">**İleti metni** alanına yazın ve **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="54839-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="54839-153">Birkaç saniye bekleyin, sonra tooyour işlev günlükleri geri dönün ve hello yeni ileti hello sırasından okuma doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="54839-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="54839-155">Depolama Gezgini içinde geri tıklayın **yenileme** ve hello ileti işlendikten ve artık hello sırada olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="54839-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="54839-156">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="54839-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="54839-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54839-157">Next steps</span></span>

<span data-ttu-id="54839-158">Bir ileti tooa depolama kuyruğu eklendiğinde çalıştırılan bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="54839-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="54839-159">Kuyruk depolama tetikleyicileri hakkında daha fazla bilgi için bkz. [Azure İşlevleri Kuyruk depolama bağlamaları](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="54839-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>