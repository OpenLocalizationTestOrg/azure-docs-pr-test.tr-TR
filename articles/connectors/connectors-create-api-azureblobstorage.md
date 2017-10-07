---
title: "aaaAdd hello Azure blob depolama Logic Apps bağlayıcı | Microsoft Docs"
description: "Başlama ve bir mantıksal uygulama hello Azure blob depolama bağlayıcısını yapılandırma"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="4f6a4-103">Bir mantıksal uygulama Hello Azure blob depolama Bağlayıcısı kullanma</span><span class="sxs-lookup"><span data-stu-id="4f6a4-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="4f6a4-104">Kullanım hello Azure Blob Depolama bağlayıcı tooupload, güncelleştirme, almak ve depolama hesabınızda, tüm mantıksal uygulama içinde BLOB'ları silme.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="4f6a4-105">Azure blob storage ile:</span><span class="sxs-lookup"><span data-stu-id="4f6a4-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="4f6a4-106">İş akışınızı yeni projeler karşıya yükleme veya en son güncelleştirilen dosyaları alma oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="4f6a4-107">Eylemler tooget dosya meta verileri kullanmak, bir dosya, dosyaları kopyala ve daha fazlasını silin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="4f6a4-108">Örneğin, bir aracı bir Azure web sitesinde (bir tetikleyici) güncelleştirildiğinde, ardından bir blob depolama (bir eylem) dosyasında güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="4f6a4-109">Bu konu nasıl toouse hello blob depolama bağlayıcı bir mantıksal uygulama içinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="4f6a4-110">Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a4-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="4f6a4-111">Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a4-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="4f6a4-112">TooAzure blob depolama birimini bağlayın</span><span class="sxs-lookup"><span data-stu-id="4f6a4-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="4f6a4-113">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="4f6a4-114">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="4f6a4-115">Örneğin, tooconnect tooa depolama hesabı, önce bir blob depolama oluşturmanız *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="4f6a4-116">toocreate bir bağlantı, bağlandığınız tooaccess hello hizmet normalde kullandığınız hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="4f6a4-117">Bu nedenle Azure storage ile Merhaba kimlik bilgilerini tooyour depolama hesabı toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="4f6a4-118">Merhaba bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f6a4-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="4f6a4-119">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="4f6a4-119">Use a trigger</span></span>
<span data-ttu-id="4f6a4-120">Bu bağlayıcı hiçbir tetikleyici yok.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-120">This connector does not have any triggers.</span></span> <span data-ttu-id="4f6a4-121">Diğer Tetikleyicileri toostart hello mantıksal uygulama, bir yineleme tetikleyici, bir HTTP Web kancası tetikleyici, tetikleyici diğer bağlayıcıları ve daha fazla ile kullanılabilir gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="4f6a4-122">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md) bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="4f6a4-123">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="4f6a4-123">Use an action</span></span>
<span data-ttu-id="4f6a4-124">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="4f6a4-125">Merhaba artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-125">Select hello plus sign.</span></span> <span data-ttu-id="4f6a4-126">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="4f6a4-127">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="4f6a4-128">"Tooget tüm hello kullanılabilir eylemlerin bir listesini blob" Merhaba metin kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="4f6a4-129">Bizim örneğimizde seçin **AzureBlob - Get dosya meta veri yolu kullanarak**.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="4f6a4-130">Bir bağlantı zaten varsa, hello seçin **...** (Göster Seçici) düğmesini tooselect bir dosya.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="4f6a4-131">Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="4f6a4-132">[Merhaba bağlantı oluşturmak](connectors-create-api-azureblobstorage.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4f6a4-133">Bu örnekte, bir dosyanın hello meta verileri alın.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="4f6a4-134">toosee meta verileri Merhaba, başka bir bağlayıcı kullanarak yeni bir dosya oluşturur başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="4f6a4-135">Örneğin, hello meta verileri temel alarak yeni bir "test" dosyası oluşturur OneDrive eylemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="4f6a4-136">**Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç).</span><span class="sxs-lookup"><span data-stu-id="4f6a4-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="4f6a4-137">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="4f6a4-138">[Depolama Gezgini](http://storageexplorer.com/) harika bir aracı birden çok depolama hesabı çok yönettiği yerdir.</span><span class="sxs-lookup"><span data-stu-id="4f6a4-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="4f6a4-139">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4f6a4-139">Connector-specific details</span></span>

<span data-ttu-id="4f6a4-140">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/azureblobconnector/).</span><span class="sxs-lookup"><span data-stu-id="4f6a4-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4f6a4-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f6a4-141">Next steps</span></span>
<span data-ttu-id="4f6a4-142">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a4-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4f6a4-143">Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4f6a4-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

