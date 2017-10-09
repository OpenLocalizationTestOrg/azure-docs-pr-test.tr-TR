---
title: "aaaAzure olay hub'ları yakalama portal üzerinden etkinleştirme | Microsoft Docs"
description: "Hello Azure portal kullanarak hello olay hub'ları yakalama özelliğini etkinleştirin."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="55ce4-103">Olay hub'ları hello Azure portal kullanarak yakalama etkinleştir</span><span class="sxs-lookup"><span data-stu-id="55ce4-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="55ce4-104">Yakalama hello kullanarak hello olay hub'ı oluşturma zamanında yapılandırabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55ce4-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="55ce4-105">Her iki yakalama hello veri tooan Azure yapabilecekleriniz [Blob storage](https://azure.microsoft.com/services/storage/blobs/) kapsayıcı ya da tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="55ce4-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="55ce4-106">Yakalama veri tooan Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="55ce4-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="55ce4-107">Bir olay hub'ı oluşturduğunuzda hello tıklatarak yakalama etkinleştirebilirsiniz **üzerinde** hello düğmesini **Event Hub'ı oluşturma** portal dikey.</span><span class="sxs-lookup"><span data-stu-id="55ce4-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="55ce4-108">Ardından bir depolama hesabı ve kapsayıcı tıklayarak belirttiğiniz **Azure Storage** hello içinde **yakalama sağlayıcısı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="55ce4-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="55ce4-109">Olay hub'ları yakalama hizmeti için kimlik doğrulaması ile depolama kullandığından, toospecify bir depolama bağlantı dizesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="55ce4-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="55ce4-110">Merhaba kaynak seçici hello kaynak URI'si depolama hesabınız için otomatik olarak seçer.</span><span class="sxs-lookup"><span data-stu-id="55ce4-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="55ce4-111">Azure Resource Manager kullanıyorsanız bu URI'yi dize olarak açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="55ce4-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="55ce4-112">Merhaba varsayılan zaman penceresi 5 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="55ce4-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="55ce4-113">Hello en düşük değer 1, en fazla 15 hello olur.</span><span class="sxs-lookup"><span data-stu-id="55ce4-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="55ce4-114">Merhaba **boyutu** penceresine sahip bir dizi 10-500 MB.</span><span class="sxs-lookup"><span data-stu-id="55ce4-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="55ce4-115">Veri tooan Azure Data Lake Store hesabı yakalama</span><span class="sxs-lookup"><span data-stu-id="55ce4-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="55ce4-116">toocapture veri tooAzure Data Lake Store, bir Data Lake Store hesabı ve bir olay hub'ı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="55ce4-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="55ce4-117">Azure Data Lake Store hesabı ve klasörleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="55ce4-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="55ce4-118">Merhaba yönergeleri izleyerek bir Data Lake Store hesabı oluşturma [Azure Data Lake hello Azure portal kullanarak Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="55ce4-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="55ce4-119">Merhaba hello yönergeleri izleyerek bu hesap altında bir klasör oluşturun [Azure Data Lake Store hesabında klasör oluşturma](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) bölümü.</span><span class="sxs-lookup"><span data-stu-id="55ce4-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="55ce4-120">Merhaba Data Lake Store hesabı dikey penceresinde tıklayın **Veri Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="55ce4-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="55ce4-121">**Erişim**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ce4-121">Click **Access**.</span></span>
5. <span data-ttu-id="55ce4-122">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ce4-122">Click **Add**.</span></span>
6. <span data-ttu-id="55ce4-123">Merhaba, **arama adına veya e-posta** kutusuna **Microsoft.EventHubs** ve bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="55ce4-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="55ce4-124">Merhaba **izinleri** sekmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="55ce4-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="55ce4-125">Merhaba izinleri hello aşağıdaki şekilde gösterildiği gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="55ce4-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="55ce4-126">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ce4-126">Click **OK**.</span></span>
9. <span data-ttu-id="55ce4-127">Şimdi, toohello hedef klasör gözatma ve hello klasör adını tıklatarak hello kök klasöründe bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="55ce4-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="55ce4-128">**Erişim**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ce4-128">Click **Access**.</span></span>
11. <span data-ttu-id="55ce4-129">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55ce4-129">Click **Add**.</span></span>
12. <span data-ttu-id="55ce4-130">Merhaba, **arama adına veya e-posta** kutusuna **Microsoft.EventHubs** ve bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="55ce4-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="55ce4-131">Merhaba **izinleri** yeniden sekmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="55ce4-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="55ce4-132">Merhaba izinleri hello aşağıdaki şekilde gösterildiği gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="55ce4-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="55ce4-133">Olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="55ce4-133">Create an event hub</span></span>

1. <span data-ttu-id="55ce4-134">Bu hello olay hub'ın hello olmalıdır Not hello Azure Data Lake Store, yeni oluşturduğunuz aynı Azure abonelik.</span><span class="sxs-lookup"><span data-stu-id="55ce4-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="55ce4-135">Merhaba tıklatarak oluşturma hello olay hub'ı **üzerinde** altında düğmesini **yakalama** hello içinde **Event Hub'ı oluşturma** portal dikey.</span><span class="sxs-lookup"><span data-stu-id="55ce4-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="55ce4-136">Merhaba, **Event Hub'ı oluşturma** portal dikey penceresinde, seçin **Azure Data Lake Store** hello gelen **yakalama sağlayıcısı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="55ce4-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="55ce4-137">İçinde **seçin Data Lake Store**, hello önceden ve hello oluşturduğunuz Data Lake Store hesabı belirtin **Data Lake yolu** alanında, oluşturduğunuz hello yolu toohello veri klasörü girin.</span><span class="sxs-lookup"><span data-stu-id="55ce4-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="55ce4-138">Mevcut bir olay hub'ında Yakalama özelliğini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="55ce4-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="55ce4-139">Event Hubs ad alanlarında mevcut olan olay hub'ları üzerinde Yakalama özelliğini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ce4-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="55ce4-140">tooenable bir var olan olay hub'ı veya toochange yakalama ayarlarınızı yakalama, hello ad alanı tooload hello tıklatın **Essentials** dikey penceresinde, kendisi için tooenable istediğiniz veya hello yakalama ayarını hello olay hub'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="55ce4-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="55ce4-141">Son olarak, hello tıklatın **özellikleri** hello bölümünü dikey penceresini açın ve ardından hello rakamları aşağıdaki gösterildiği gibi hello yakalama ayarları düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="55ce4-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="55ce4-142">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="55ce4-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="55ce4-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="55ce4-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="55ce4-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55ce4-144">Next steps</span></span>

<span data-ttu-id="55ce4-145">Dilerseniz Azure Resource Manager şablonlarını kullanarak da Event Hubs Yakalama özelliğini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55ce4-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="55ce4-146">Daha fazla bilgi için bkz. [Azure Resource Manager şablonu kullanarak Yakalama özelliğini etkinleştirme](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="55ce4-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
