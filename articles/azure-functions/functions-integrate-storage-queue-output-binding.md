---
title: "Azure kuyruk iletileri tarafından tetiklenen bir işlev aaaCreate | Microsoft Docs"
description: "Kullanım Azure işlevleri toocreate iletileri tarafından çağrılan sunucusuz bir işlev tooan Azure depolama kuyruğu gönderildi."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a><span data-ttu-id="f065b-103">İşlevler kullanılarak iletileri tooan Azure depolama kuyruğu ekleme</span><span class="sxs-lookup"><span data-stu-id="f065b-103">Add messages tooan Azure Storage queue using Functions</span></span>

<span data-ttu-id="f065b-104">Azure işlevleri, giriş ve çıkış bağlama işlevinizde bir bildirim temelli yolu tooconnect tooexternal hizmet verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="f065b-104">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="f065b-105">Bu konuda, nasıl tooupdate bağlaması bir çıktı ekleyerek varolan bir işlev tooAzure kuyruk depolama iletileri gönderir öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f065b-105">In this topic, learn how tooupdate an existing function by adding an output binding that sends messages tooAzure Queue storage.</span></span>  

![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="f065b-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f065b-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="f065b-108">Merhaba yüklemek [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f065b-108">Install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="f065b-109"><a name="add-binding"></a>Çıkış bağlaması ekleme</span><span class="sxs-lookup"><span data-stu-id="f065b-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="f065b-110">İşlev uygulamanızı ve işlevinizi genişletin.</span><span class="sxs-lookup"><span data-stu-id="f065b-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="f065b-111">Seçin **tümleştir** ve **+ yeni çıktı**, ardından **Azure kuyruk depolama** ve **seçin**.</span><span class="sxs-lookup"><span data-stu-id="f065b-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![Bir sıranın depolama çıkış bağlama tooa işlevi hello Azure portal ekleyin.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="f065b-113">Merhaba tabloda belirtildiği gibi Hello ayarları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f065b-113">Use hello settings as specified in hello table:</span></span> 

    ![Bir sıranın depolama çıkış bağlama tooa işlevi hello Azure portal ekleyin.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="f065b-115">Ayar</span><span class="sxs-lookup"><span data-stu-id="f065b-115">Setting</span></span>      |  <span data-ttu-id="f065b-116">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="f065b-116">Suggested value</span></span>   | <span data-ttu-id="f065b-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f065b-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="f065b-118">**Kuyruk adı**</span><span class="sxs-lookup"><span data-stu-id="f065b-118">**Queue name**</span></span>   | <span data-ttu-id="f065b-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="f065b-119">myqueue-items</span></span>    | <span data-ttu-id="f065b-120">Merhaba Hello adını, depolama hesabınız tooconnect tooin sırası.</span><span class="sxs-lookup"><span data-stu-id="f065b-120">hello name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="f065b-121">**Depolama hesabı bağlantısı**</span><span class="sxs-lookup"><span data-stu-id="f065b-121">**Storage account connection**</span></span> | <span data-ttu-id="f065b-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="f065b-122">AzureWebJobStorage</span></span> | <span data-ttu-id="f065b-123">Merhaba depolama hesabı bağlantısı işlevi uygulamanız tarafından zaten kullanılmakta kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f065b-123">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="f065b-124">**İleti parametre adı**</span><span class="sxs-lookup"><span data-stu-id="f065b-124">**Message parameter name**</span></span> | <span data-ttu-id="f065b-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="f065b-125">outputQueueItem</span></span> | <span data-ttu-id="f065b-126">Merhaba çıkış bağlama parametresinin Hello adı.</span><span class="sxs-lookup"><span data-stu-id="f065b-126">hello name of hello output binding parameter.</span></span> | 

4. <span data-ttu-id="f065b-127">Tıklatın **kaydetmek** tooadd hello bağlama.</span><span class="sxs-lookup"><span data-stu-id="f065b-127">Click **Save** tooadd hello binding.</span></span>
 
<span data-ttu-id="f065b-128">Tanımlanan bir çıktı bağlama sahip olduğunuza göre tooupdate hello kod toouse hello bağlama tooadd iletileri tooa sırası gerekir.</span><span class="sxs-lookup"><span data-stu-id="f065b-128">Now that you have an output binding defined, you need tooupdate hello code toouse hello binding tooadd messages tooa queue.</span></span>  

## <a name="update-hello-function-code"></a><span data-ttu-id="f065b-129">Merhaba işlev kodunu güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="f065b-129">Update hello function code</span></span>

1. <span data-ttu-id="f065b-130">İşlev toodisplay hello işlevi kodunuzu hello Düzenleyicisi'nde seçin.</span><span class="sxs-lookup"><span data-stu-id="f065b-130">Select your function toodisplay hello function code in hello editor.</span></span> 

2. <span data-ttu-id="f065b-131">C#, bir işlev için tooadd hello aşağıdaki gibi işlev tanımının güncelleştirme **outputQueueItem** depolama bağlama parametresi.</span><span class="sxs-lookup"><span data-stu-id="f065b-131">For a C# function, update your function definition as follows tooadd hello **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="f065b-132">JavaScript işlevi için bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="f065b-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="f065b-133">Kod toohello işlevi yalnızca hello yöntemi döndürmeden önce aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f065b-133">Add hello following code toohello function just before hello method returns.</span></span> <span data-ttu-id="f065b-134">Merhaba uygun parçacığı işlevinizi hello dili için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f065b-134">Use hello appropriate snippet for hello language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. <span data-ttu-id="f065b-135">Seçin **kaydetmek** toosave değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="f065b-135">Select **Save** toosave changes.</span></span>

<span data-ttu-id="f065b-136">toohello HTTP tetikleyicisini geçirilen hello değeri bir ileti eklenen toohello sırada dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="f065b-136">hello value passed toohello HTTP trigger is included in a message added toohello queue.</span></span>
 
## <a name="test-hello-function"></a><span data-ttu-id="f065b-137">Test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="f065b-137">Test hello function</span></span> 

1. <span data-ttu-id="f065b-138">Merhaba kod değişiklikler kaydedildikten sonra seçin **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="f065b-138">After hello code changes are saved, select **Run**.</span></span> 

    ![Bir sıranın depolama çıkış bağlama tooa işlevi hello Azure portal ekleyin.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="f065b-140">Merhaba günlükleri toomake hello işlevi başarılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f065b-140">Check hello logs toomake sure that hello function succeeded.</span></span> <span data-ttu-id="f065b-141">Adlı yeni bir sıra **outqueue** depolama hesabınıza bağlama hello çıktısını alırken işlevleri çalışma zamanı ilk kullanılan hello tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f065b-141">A new queue named **outqueue** is created in your Storage account by hello Functions runtime when hello output binding is first used.</span></span>

<span data-ttu-id="f065b-142">Ardından, tooyour depolama hesabı tooverify hello yeni kuyruk ve tooit eklenen selamlama iletisine bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f065b-142">Next, you can connect tooyour storage account tooverify hello new queue and hello message you added tooit.</span></span> 

## <a name="connect-toohello-queue"></a><span data-ttu-id="f065b-143">Toohello sıra Bağlan</span><span class="sxs-lookup"><span data-stu-id="f065b-143">Connect toohello queue</span></span>

<span data-ttu-id="f065b-144">Zaten Depolama Gezgini yüklediyseniz ve tooyour depolama hesabı bağlı Atla hello ilk üç adımı.</span><span class="sxs-lookup"><span data-stu-id="f065b-144">Skip hello first three steps if you have already installed Storage Explorer and connected it tooyour storage account.</span></span>    

1. <span data-ttu-id="f065b-145">İşlevinde seçin **tümleştir** ve hello yeni **Azure kuyruk depolama** bağlama çıktı sonra genişletin **belgelerine**.</span><span class="sxs-lookup"><span data-stu-id="f065b-145">In your function, choose **Integrate** and hello new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="f065b-146">Hem **Hesap adı** hem de **Hesap anahtarı** değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f065b-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="f065b-147">Bu kimlik bilgileri tooconnect toohello depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f065b-147">You use these credentials tooconnect toohello storage account.</span></span>
 
    ![Merhaba depolama hesabı bağlantısı kimlik bilgilerini edinin.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="f065b-149">Hello çalıştırmak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/) aracı, select hello Bağlan simgesi hello sol tarafta, seçin **bir depolama hesabı adı ve anahtar kullanmak**seçip **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="f065b-149">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select hello connect icon on hello left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![Merhaba depolama hesabı Gezgini aracını çalıştırın.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="f065b-151">Yapıştır hello **hesap adı** ve **hesap anahtarı** bunların karşılık gelen alanlara adım 1 öğesinden sonra seçin **sonraki**, ve **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="f065b-151">Paste hello **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![Merhaba depolama kimlik yapıştırın ve bağlanın.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="f065b-153">Merhaba bağlı depolama hesabı genişletin, **sıraları** ve bir sıraya adlı doğrulayın **Sıram öğeleri** bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f065b-153">Expand hello attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="f065b-154">Ayrıca bir iletiyi zaten hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f065b-154">You should also see a message already in hello queue.</span></span>  
 
    ![Depolama kuyruğu oluşturun.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="f065b-156">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="f065b-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="f065b-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f065b-157">Next steps</span></span>

<span data-ttu-id="f065b-158">Bir çıkış bağlama tooan varolan işlevi eklediniz.</span><span class="sxs-lookup"><span data-stu-id="f065b-158">You have added an output binding tooan existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="f065b-159">Bağlama tooQueue depolama hakkında daha fazla bilgi için bkz: [Azure işlevleri depolama kuyruğu bağlamaları](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="f065b-159">For more information about binding tooQueue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



