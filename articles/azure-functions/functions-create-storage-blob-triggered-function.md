---
title: "Azure Blob Depolama Birimi tarafından tetiklenen bir işlev aaaCreate | Microsoft Docs"
description: "Kullanım Azure işlevleri toocreate öğeleri tarafından çağrılan sunucusuz bir işlev tooAzure Blob Depolama eklendi."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="2ea5b-103">Azure Blob depolama ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ea5b-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="2ea5b-104">Toocreate dosyaları olduğunda tetiklenen bir işlev Azure Blob depolama alanına güncelleştirilmiş tooor nasıl karşıya öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="2ea5b-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ea5b-106">Prerequisites</span></span>

+ <span data-ttu-id="2ea5b-107">Merhaba yükleyip [Microsoft Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="2ea5b-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="2ea5b-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-108">An Azure subscription.</span></span> <span data-ttu-id="2ea5b-109">Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="2ea5b-110">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ea5b-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="2ea5b-112">Ardından, hello yeni işlev uygulamada bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="2ea5b-113">Blob depolama ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ea5b-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="2ea5b-114">Merhaba, işlev uygulaması'nı genişletin ve  **+**  sonraki çok düğmesini**işlevler**.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="2ea5b-115">Bu işlev uygulamanızda hello ilk işlevi ise seçin **özel işlevi**.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="2ea5b-116">Merhaba eksiksiz işlev şablonları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-116">This displays hello complete set of function templates.</span></span>

    ![Hello Azure portalı hızlı başlangıç sayfasında işlevleri](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="2ea5b-118">Select hello **BlobTrigger** şablonu istediğiniz dili ve hello tabloda belirtildiği gibi hello ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Merhaba Blob Depolama tetiklenen bir işlev oluşturun.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="2ea5b-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="2ea5b-120">Setting</span></span> | <span data-ttu-id="2ea5b-121">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="2ea5b-121">Suggested value</span></span> | <span data-ttu-id="2ea5b-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ea5b-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="2ea5b-123">**Path**</span><span class="sxs-lookup"><span data-stu-id="2ea5b-123">**Path**</span></span>   | <span data-ttu-id="2ea5b-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="2ea5b-124">mycontainer/{name}</span></span>    | <span data-ttu-id="2ea5b-125">İzlenmekte olan Blob depolamanın konumu.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="2ea5b-126">Merhaba dosya adı hello BLOB hello bağlama hello olarak geçirilir _adı_ parametresi.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="2ea5b-127">**Depolama hesabı bağlantısı**</span><span class="sxs-lookup"><span data-stu-id="2ea5b-127">**Storage account connection**</span></span> | <span data-ttu-id="2ea5b-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="2ea5b-128">AzureWebJobStorage</span></span> | <span data-ttu-id="2ea5b-129">Merhaba depolama hesabı bağlantısı işlevi uygulamanız tarafından zaten kullanılmakta kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="2ea5b-130">**İşlevinizi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="2ea5b-130">**Name your function**</span></span> | <span data-ttu-id="2ea5b-131">İşlev uygulamanızda benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="2ea5b-131">Unique in your function app</span></span> | <span data-ttu-id="2ea5b-132">Blob ile tetiklenen bu işlevin adı.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="2ea5b-133">Tıklatın **oluşturma** toocreate işlevinizi.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="2ea5b-134">Ardından, tooyour Azure depolama hesabı bağlanmak ve hello oluşturmak **mycontainer** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="2ea5b-135">Merhaba kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ea5b-135">Create hello container</span></span>

1. <span data-ttu-id="2ea5b-136">İşlevinizde **Tümleştir**'e tıklayın, **Belgeler**'i genişletin ve hem **Hesap adı** hem de **Hesap anahtarı** değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="2ea5b-137">Bu kimlik bilgileri tooconnect toohello depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="2ea5b-138">Depolama hesabınız zaten bağlanmış olduğunuz toostep 4 atlayın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Merhaba depolama hesabı bağlantısı kimlik bilgilerini edinin.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="2ea5b-140">Merhaba çalıştırmak [Microsoft Azure Storage Gezgini](http://storageexplorer.com/) aracı, hello tıklatın Bağlan simgesi hello sol tarafta, seçin **bir depolama hesabı adı ve anahtar kullanmak**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Merhaba depolama hesabı Gezgini aracını çalıştırın.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="2ea5b-142">Merhaba girin **hesap adı** ve **hesap anahtarı** 1. adımdaki tıklatın **sonraki** ve ardından **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Merhaba depolama kimlik bilgilerini girin ve bağlanın.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="2ea5b-144">Merhaba bağlı depolama hesabı'nı genişletin, sağ tıklatın **Blob kapsayıcıları**, tıklatın **oluşturma blob kapsayıcısı**, türü `mycontainer`, ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Depolama kuyruğu oluşturun.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="2ea5b-146">Bir blob kapsayıcısını sahip olduğunuza göre bir dosya toohello kapsayıcısı yükleyerek hello işlevi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="2ea5b-147">Test hello işlevi</span><span class="sxs-lookup"><span data-stu-id="2ea5b-147">Test hello function</span></span>

1. <span data-ttu-id="2ea5b-148">Geri Azure portal hello, Gözat tooyour işlevi genişletin hello **günlükleri** hello sonunda hello sayfası ve emin olun, bu günlük akış duraklatıldı değil.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="2ea5b-149">Depolama Gezgini’nde depolama hesabınızı genişletin, **Blob kapsayıcıları** ve **mycontainer** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="2ea5b-150">**Karşıya Yükle**’ye ve ardından **Dosyaları yükle...** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Bir dosya toohello blob kapsayıcısı karşıya yükleyin.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="2ea5b-152">Merhaba, **dosyaları karşıya yükleme** iletişim kutusunda, hello **dosyaları** alan.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="2ea5b-153">Bir görüntü dosyası gibi yerel bilgisayarınızda tooa dosyasını bulun, seçin ve **açık** ve ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="2ea5b-154">Tooyour işlev günlükleri gidip bu hello blobu okuma emin olun.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Merhaba günlüklerine iletiyi görüntüle.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="2ea5b-156">İşlevi uygulamanızı hello varsayılan tüketim planında çalıştığında, olabilir bir gecikme dakika arasında hello eklenen veya güncelleştirilen blob ile Merhaba tooseveral yukarı işlev tetiklenen.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="2ea5b-157">Blob ile tetiklenen işlevlerde düşük gecikme süresi gerekiyorsa, işlev uygulamanızı bir App Service planında çalıştırmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2ea5b-158">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="2ea5b-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="2ea5b-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ea5b-159">Next steps</span></span>

<span data-ttu-id="2ea5b-160">Güncelleştirilmiş tooor Blob storage'da bir blob eklendiğinde çalıştırılan bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="2ea5b-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="2ea5b-161">Blob depolama tetikleyicileri hakkında daha fazla bilgi için bkz. [Azure İşlevleri Blob depolama bağlamaları](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="2ea5b-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
