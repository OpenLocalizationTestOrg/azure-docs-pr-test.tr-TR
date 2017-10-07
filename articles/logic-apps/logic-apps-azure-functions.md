---
title: "Azure Logic Apps ile Azure işlevleri için aaaCustom kod | Microsoft Docs"
description: "Oluşturma ve Azure Logic Apps ile Azure işlevleri için özel kod çalıştırma"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="8e1d5-103">Ekleme ve logic apps için özel kod aracılığıyla Azure işlevleri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8e1d5-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="8e1d5-104">C# veya node.js logic apps içinde toorun özel parçacıkları, Azure işlevleri aracılığıyla özel işlevler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="8e1d5-105">[Azure işlevleri](../azure-functions/functions-overview.md) server ücretsiz Microsoft Azure ve bu görevleri gerçekleştirmek için yararlı olan bilgi işlem sunar:</span><span class="sxs-lookup"><span data-stu-id="8e1d5-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="8e1d5-106">Gelişmiş Biçimlendirme veya logic apps alanların işlem</span><span class="sxs-lookup"><span data-stu-id="8e1d5-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="8e1d5-107">Bir iş akışında hesaplamalar.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="8e1d5-108">C# veya node.js desteklenen işlevlere sahip Hello mantığı uygulama işlevini genişletme</span><span class="sxs-lookup"><span data-stu-id="8e1d5-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="8e1d5-109">Logic apps için özel işlevler oluştur</span><span class="sxs-lookup"><span data-stu-id="8e1d5-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="8e1d5-110">Bir işlev hello de hello Azure işlevleri portalından oluşturmanızı öneririz **Genel Web kancası - düğüm** veya **Genel Web kancası - C#** şablonları.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="8e1d5-111">Merhaba sonucu oluşturur otomatik doldurulan bir kabul eden bir şablonu `application/json` mantığı uygulamasından.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="8e1d5-112">Bu şablondan Oluştur işlevleri otomatik olarak algılanır ve hello mantığı Uygulama Tasarımcısı altında görünür **my bölgede Azure işlevleri.**</span><span class="sxs-lookup"><span data-stu-id="8e1d5-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="8e1d5-113">Merhaba hello üzerinde Azure portal'ın **tümleştir** bölmesini işlevinizi için şablonunuzu göstermek, **modu** çok ayarlamak**Web kancası** ve **Web kancası türü** çok ayarlanır**genel JSON**.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="8e1d5-114">Web kancası işlevleri bir isteğini kabul edin ve hello yöntemiyle uygulamasına geçirmek bir `data` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="8e1d5-115">Gibi noktalı gösterim kullanılarak yükünüzü hello özelliklerini erişebilirsiniz `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="8e1d5-116">Örneğin, bir tarih saat değeri bir tarih dizeye dönüştürür basit bir JavaScript işlevi aşağıdaki örneğine hello gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="8e1d5-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="8e1d5-117">Mantığı uygulamalardan Azure işlevlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="8e1d5-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="8e1d5-118">Aboneliğiniz ve mantığı Uygulama Tasarımcısı'nda toocall istediğinizi seçin hello işlevi toolist Merhaba kapsayıcılara tıklatın hello **Eylemler** menü ve arasından seçim **my bölgede Azure işlevleri**.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="8e1d5-119">Merhaba işlevi seçtikten sonra olduğunuz bir giriş yükü nesne toospecify istedi.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="8e1d5-120">Mantıksal uygulama gönderir toohello işlevi hello ve bir JSON nesnesi olmalıdır selamlama iletisine nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="8e1d5-121">Örneğin, hello toopass istiyorsanız **son değişiklik** tarih Salesforce tetikleyiciden hello işlevi yükü aşağıdaki örnekte olduğu gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="8e1d5-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Son değiştirilme tarihi][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="8e1d5-123">Bir işlevden tetikleyici mantıksal uygulamalar</span><span class="sxs-lookup"><span data-stu-id="8e1d5-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="8e1d5-124">Bir işlev içinde bir mantıksal uygulama tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="8e1d5-125">Bkz: [Logic apps aranabilir uç noktalar olarak](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="8e1d5-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="8e1d5-126">El ile tetikleyicisine sahip bir mantıksal uygulama oluşturun, sonra bir HTTP POST toohello el ile tetikleyici URL'si toohello mantıksal uygulama gönderilen istediğiniz hello yükü ile işlevinizin oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="8e1d5-127">Mantıksal Uygulama Tasarımcısı'ndan bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="8e1d5-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="8e1d5-128">Merhaba Tasarımcısı'ndan bir node.js Web kancası işlevi de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="8e1d5-129">İlk olarak seçin **Azure işlevleri my bölgede** ve işlevinizi için bir kapsayıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="8e1d5-130">Henüz bir kapsayıcınız yoksa, hello gelen toocreate gerek [Azure işlevleri portalına](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="8e1d5-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="8e1d5-131">Ardından **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-131">Then select **Create New**.</span></span>  

<span data-ttu-id="8e1d5-132">toogenerate toocompute, istediğiniz hello verilerine dayalı bir şablon bir işlevdeki toopass planlama hello bağlam nesnesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="8e1d5-133">Bu nesne bir JSON nesnesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-133">This object must be a JSON object.</span></span> <span data-ttu-id="8e1d5-134">Örneğin, FTP eylemin hello dosya içeriğinde geçirirseniz, hello bağlam yükü aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="8e1d5-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Bağlam yükü][2]

> [!NOTE]
> <span data-ttu-id="8e1d5-136">Bu nesne bir dize olarak cast değildi çünkü hello içerik doğrudan toohello JSON yükü eklenir.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="8e1d5-137">Ancak, Hello nesne (diğer bir deyişle, bir dize veya bir JSON nesnesi/dizi) bir JSON belirteci değilse hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="8e1d5-138">toocast hello nesnesi bir dize olarak, bu makaledeki hello ilk çizimde gösterildiği gibi teklifleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="8e1d5-139">Merhaba Tasarımcısı sonra satır içi oluşturabileceğiniz bir işlevi şablon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="8e1d5-140">Değişkenleri hello işlevdeki toopass plan hello bağlamını temel alınarak önceden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8e1d5-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
