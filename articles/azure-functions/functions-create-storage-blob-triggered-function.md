---
title: "Azure'da Blob depolama tarafından tetiklenen bir işlev oluşturma | Microsoft Docs"
description: "Azure Blob depolamaya eklenen öğeler tarafından çağrılan sunucusuz bir işlev oluşturmak için Azure İşlevlerini kullanın."
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
ms.openlocfilehash: 1ddd056903b1a2f973a58bd7054ea2b8281607c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="e33d3-103">Azure Blob depolama ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="e33d3-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="e33d3-104">Azure Blob depolamada dosyalar karşıya yüklendiğinde veya güncelleştirildiğinde tetiklenen bir işlev oluşturma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="e33d3-104">Learn how to create a function triggered when files are uploaded to or updated in Azure Blob storage.</span></span>

![Günlüklerde iletiyi görüntüleyin.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="e33d3-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e33d3-106">Prerequisites</span></span>

+ <span data-ttu-id="e33d3-107">[Microsoft Azure Depolama Gezgini](http://storageexplorer.com/)'ni indirip yükleme.</span><span class="sxs-lookup"><span data-stu-id="e33d3-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="e33d3-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="e33d3-108">An Azure subscription.</span></span> <span data-ttu-id="e33d3-109">Aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e33d3-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="e33d3-110">Azure İşlev uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e33d3-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![İşlev uygulaması başarıyla oluşturuldu.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="e33d3-112">Ardından, yeni işlev uygulamasında bir işlev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e33d3-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="e33d3-113">Blob depolama ile tetiklenen bir işlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="e33d3-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="e33d3-114">İşlev uygulamanızı genişletin ve **İşlevler**'in yanındaki **+** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="e33d3-115">Bu, işlev uygulamanızdaki ilk işlevse **Özel işlev**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="e33d3-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="e33d3-116">Böylece işlev şablonlarının tamamı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e33d3-116">This displays the complete set of function templates.</span></span>

    ![Azure portalındaki İşlevler hızlı başlangıç sayfası](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="e33d3-118">İstediğiniz dil için **BlobTrigger** şablonunu seçin ve tabloda belirtilen ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-118">Select the **BlobTrigger** template for your desired language, and use the settings as specified in the table.</span></span>

    ![Blob depolama ile tetiklenen bir işlev oluşturun.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="e33d3-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="e33d3-120">Setting</span></span> | <span data-ttu-id="e33d3-121">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="e33d3-121">Suggested value</span></span> | <span data-ttu-id="e33d3-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e33d3-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="e33d3-123">**Path**</span><span class="sxs-lookup"><span data-stu-id="e33d3-123">**Path**</span></span>   | <span data-ttu-id="e33d3-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="e33d3-124">mycontainer/{name}</span></span>    | <span data-ttu-id="e33d3-125">İzlenmekte olan Blob depolamanın konumu.</span><span class="sxs-lookup"><span data-stu-id="e33d3-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="e33d3-126">Blob’un dosya adı bağlamaya _name_ parametresi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="e33d3-126">The file name of the blob is passed in the binding as the _name_ parameter.</span></span>  |
    | <span data-ttu-id="e33d3-127">**Depolama hesabı bağlantısı**</span><span class="sxs-lookup"><span data-stu-id="e33d3-127">**Storage account connection**</span></span> | <span data-ttu-id="e33d3-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="e33d3-128">AzureWebJobStorage</span></span> | <span data-ttu-id="e33d3-129">İşlev uygulamanız tarafından kullanılmakta olan depolama hesabı bağlantısını kullanabilir veya yeni bir bağlantı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e33d3-129">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="e33d3-130">**İşlevinizi adlandırın**</span><span class="sxs-lookup"><span data-stu-id="e33d3-130">**Name your function**</span></span> | <span data-ttu-id="e33d3-131">İşlev uygulamanızda benzersiz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="e33d3-131">Unique in your function app</span></span> | <span data-ttu-id="e33d3-132">Blob ile tetiklenen bu işlevin adı.</span><span class="sxs-lookup"><span data-stu-id="e33d3-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="e33d3-133">İşlevinizi oluşturmak için **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-133">Click **Create** to create your function.</span></span>

<span data-ttu-id="e33d3-134">Ardından Azure Depolama hesabınıza bağlanıp **mycontainer** kapsayıcısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e33d3-134">Next, you connect to your Azure Storage account and create the **mycontainer** container.</span></span>

## <a name="create-the-container"></a><span data-ttu-id="e33d3-135">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e33d3-135">Create the container</span></span>

1. <span data-ttu-id="e33d3-136">İşlevinizde **Tümleştir**'e tıklayın, **Belgeler**'i genişletin ve hem **Hesap adı** hem de **Hesap anahtarı** değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="e33d3-137">Depolama hesabına bağlanmak için bu kimlik bilgilerini kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e33d3-137">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="e33d3-138">Depolama hesabınıza önceden bağlandıysanız 4. adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="e33d3-138">If you have already connected your storage account, skip to step 4.</span></span>

    ![Depolama hesabı bağlantısı için kimlik bilgilerini alın.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="e33d3-140">[Microsoft Azure Depolama Gezgini](http://storageexplorer.com/) aracını çalıştırın, sol taraftaki bağlan simgesine tıklayın, **Depolama hesabı adı ve anahtarı kullan**'ı seçin ve **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Depolama Hesabı Gezgini aracını çalıştırın.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="e33d3-142">1 Adımda kopyaladığınız **Hesap adı** ve **Hesap anahtarı** değerlerini girin, **İleri**'ye ve ardından **Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Depolama kimlik bilgilerini girin ve bağlanın.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="e33d3-144">Bağlı depolama hesabını genişletin, **Blob kapsayıcılar**’a sağ tıklayın, **Blob kapsayıcı oluştur**’a tıklayın, `mycontainer` yazın ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-144">Expand the attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Depolama kuyruğu oluşturun.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="e33d3-146">Artık bir blob kapsayıcısına sahip olduğunuza göre, kapsayıcıya bir dosya yükleyerek işlevi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e33d3-146">Now that you have a blob container, you can test the function by uploading a file to the container.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="e33d3-147">İşlevi test etme</span><span class="sxs-lookup"><span data-stu-id="e33d3-147">Test the function</span></span>

1. <span data-ttu-id="e33d3-148">Azure portalına dönün, işlevinizi bulun, sayfanın en altındaki **Günlükler** bölümünü genişletin ve günlük akışının duraklatılmış olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e33d3-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="e33d3-149">Depolama Gezgini’nde depolama hesabınızı genişletin, **Blob kapsayıcıları** ve **mycontainer** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="e33d3-150">**Karşıya Yükle**’ye ve ardından **Dosyaları yükle...** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Dosyayı blob kapsayıcısına yükleyin.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="e33d3-152">**Dosyaları karşıya yükle** iletişim kutusunda **Dosyalar** alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-152">In the **Upload files** dialog box, click the **Files** field.</span></span> <span data-ttu-id="e33d3-153">Yerel bilgisayarınızda görüntü dosyası gibi bir dosyaya gidin, seçin, **Aç**’ı ve ardından **Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e33d3-153">Browse to a file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="e33d3-154">İşlev günlüklerinize geri dönün ve blob’un okunduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e33d3-154">Go back to your function logs and verify that the blob has been read.</span></span>

   ![Günlüklerde iletiyi görüntüleyin.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="e33d3-156">İşlev uygulamanız varsayılan Tüketim planında çalıştığında, blob’un eklenmesi veya güncelleştirilmesi ile işlevin tetiklenmesi arasında birkaç dakika gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="e33d3-156">When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered.</span></span> <span data-ttu-id="e33d3-157">Blob ile tetiklenen işlevlerde düşük gecikme süresi gerekiyorsa, işlev uygulamanızı bir App Service planında çalıştırmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="e33d3-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="e33d3-158">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="e33d3-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="e33d3-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e33d3-159">Next steps</span></span>

<span data-ttu-id="e33d3-160">Blob depolamaya bir blob eklendiğinde çalışacak bir işlev oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e33d3-160">You have created a function that runs when a blob is added to or updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="e33d3-161">Blob depolama tetikleyicileri hakkında daha fazla bilgi için bkz. [Azure İşlevleri Blob depolama bağlamaları](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="e33d3-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
