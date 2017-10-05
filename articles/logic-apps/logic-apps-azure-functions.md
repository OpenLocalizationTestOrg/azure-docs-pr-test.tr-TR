---
title: "Azure Logic Apps ile Azure işlevleri için özel kod | Microsoft Docs"
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
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="e9d2d-103">Ekleme ve logic apps için özel kod aracılığıyla Azure işlevleri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e9d2d-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="e9d2d-104">C# veya node.js özel parçacıkları logic apps içinde çalıştırmak için Azure işlevleri aracılığıyla özel işlevler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="e9d2d-105">[Azure işlevleri](../azure-functions/functions-overview.md) server ücretsiz Microsoft Azure ve bu görevleri gerçekleştirmek için yararlı olan bilgi işlem sunar:</span><span class="sxs-lookup"><span data-stu-id="e9d2d-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="e9d2d-106">Gelişmiş Biçimlendirme veya logic apps alanların işlem</span><span class="sxs-lookup"><span data-stu-id="e9d2d-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="e9d2d-107">Bir iş akışında hesaplamalar.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="e9d2d-108">C# veya node.js desteklenen işlevlere sahip mantığı uygulama işlevini genişletme</span><span class="sxs-lookup"><span data-stu-id="e9d2d-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="e9d2d-109">Logic apps için özel işlevler oluştur</span><span class="sxs-lookup"><span data-stu-id="e9d2d-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="e9d2d-110">Gelen bir işlev Azure işlevleri portalındaki oluşturmanızı öneririz **Genel Web kancası - düğüm** veya **Genel Web kancası - C#** şablonları.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="e9d2d-111">Sonuç bir otomatik doldurulmuş kabul eden bir şablon oluşturur `application/json` mantığı uygulamasından.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="e9d2d-112">Bu şablondan Oluştur işlevleri otomatik olarak algılanır ve altında mantığı Uygulama Tasarımcısı'nda görünen **my bölgede Azure işlevleri.**</span><span class="sxs-lookup"><span data-stu-id="e9d2d-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="e9d2d-113">Azure portalında üzerinde **tümleştir** bölmesini işlevinizi için şablonunuzu göstermek, **modu** kümesine **Web kancası** ve **Web kancası türü** ayarlanır **genel JSON**.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="e9d2d-114">Web kancası işlevleri bir isteğini kabul edin ve yöntemiyle uygulamasına geçirmek bir `data` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="e9d2d-115">Gibi noktalı gösterim kullanılarak yükünüzü özelliklerini erişebilirsiniz `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="e9d2d-116">Örneğin, bir tarih saat değeri bir tarih dizeye dönüştürür basit bir JavaScript işlevi aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="e9d2d-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="e9d2d-117">Mantığı uygulamalardan Azure işlevlerini çağırma</span><span class="sxs-lookup"><span data-stu-id="e9d2d-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="e9d2d-118">Aboneliğinizi kapsayıcılarında listelemek ve, mantığı Uygulama Tasarımcısı'nda, aramak istediğiniz işlevi seçmek için tıklatın **Eylemler** menü ve arasından seçim **Azure işlevleri my bölgede**.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="e9d2d-119">İşlev seçtikten sonra bir giriş yükü nesne belirtmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="e9d2d-120">İleti mantıksal uygulama işlevine gönderir ve bir JSON nesnesi olmalıdır nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="e9d2d-121">Örneğin, içinde geçirmek istiyorsanız **son değişiklik** tarih Salesforce tetikleyiciden işlevi yükü bu örnekteki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e9d2d-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Son değiştirilme tarihi][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="e9d2d-123">Bir işlevden tetikleyici mantıksal uygulamalar</span><span class="sxs-lookup"><span data-stu-id="e9d2d-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="e9d2d-124">Bir işlev içinde bir mantıksal uygulama tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="e9d2d-125">Bkz: [Logic apps aranabilir uç noktalar olarak](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="e9d2d-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="e9d2d-126">El ile tetikleyicisine sahip bir mantıksal uygulama oluşturun, sonra mantıksal uygulama URL'si istediğiniz yükü ile gönderilen el ile tetikleyici için bir HTTP POST işlevinizin oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="e9d2d-127">Mantıksal Uygulama Tasarımcısı'ndan bir işlev oluşturun</span><span class="sxs-lookup"><span data-stu-id="e9d2d-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="e9d2d-128">Tasarımcısı'ndan bir node.js Web kancası işlevi de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="e9d2d-129">İlk olarak seçin **Azure işlevleri my bölgede** ve işlevinizi için bir kapsayıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="e9d2d-130">Henüz bir kapsayıcınız yoksa, birinden oluşturmanıza gerek [Azure işlevleri portalına](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="e9d2d-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="e9d2d-131">Ardından **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-131">Then select **Create New**.</span></span>  

<span data-ttu-id="e9d2d-132">İşlem yapmak istediğiniz verileri temel alan bir şablon oluşturmak için bir işlevdeki geçirmek için planlama context nesnesi belirtin.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="e9d2d-133">Bu nesne bir JSON nesnesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-133">This object must be a JSON object.</span></span> <span data-ttu-id="e9d2d-134">Örneğin, bir FTP eylemden dosya içeriğinde geçirirseniz, bağlam yükü aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="e9d2d-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Bağlam yükü][2]

> [!NOTE]
> <span data-ttu-id="e9d2d-136">Bu nesne bir dize olarak cast değildi olduğundan, içeriği doğrudan JSON yükü eklenir.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="e9d2d-137">Ancak, nesne (diğer bir deyişle, bir dize veya bir JSON nesnesi/dizi) bir JSON belirteci değilse, bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="e9d2d-138">Dize olarak nesnesi yayınlanamıyor teklifleri bu makalede ilk çizimde gösterildiği gibi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="e9d2d-139">Tasarımcı sonra satır içi oluşturabileceğiniz bir işlevi şablon oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="e9d2d-140">Değişkenleri işlevdeki geçirmek için planlama bağlam temel alınarak önceden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e9d2d-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
