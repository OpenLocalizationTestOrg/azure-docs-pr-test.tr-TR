---
title: "aaaScenario - tetikleyici logic apps ile Azure işlevleri ve Azure Service Bus | Microsoft Docs"
description: "Azure işlevleri ve Azure Service Bus kullanarak işlevi tootrigger mantıksal uygulama oluşturma"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="6fee9-103">Senaryo: bir mantıksal uygulama Azure işlevleri ve Azure Service Bus ile Tetikle</span><span class="sxs-lookup"><span data-stu-id="6fee9-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="6fee9-104">Bir uzun süre çalışan dinleyicisi ya da görev toodeploy gerektiğinde Azure işlevleri toocreate tetikleyici için bir mantıksal uygulama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fee9-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="6fee9-105">Örneğin, bir sıra üzerinde dinleyen bir işlev oluşturun ve hemen bir mantıksal uygulama itme tetikleyici olarak tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="6fee9-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="6fee9-106">Merhaba mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fee9-106">Build hello logic app</span></span>
<span data-ttu-id="6fee9-107">Bu örnekte, tetiklenen toobe gerektiren her mantıksal uygulama için çalışan bir işleve sahip.</span><span class="sxs-lookup"><span data-stu-id="6fee9-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="6fee9-108">İlk olarak, bir HTTP isteği tetikleyicisine sahip bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6fee9-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="6fee9-109">bir kuyruk iletisi alındığında Bu uç hello işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="6fee9-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="6fee9-110">Bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6fee9-110">Create a logic app.</span></span>
2. <span data-ttu-id="6fee9-111">Select hello **bir HTTP isteği alındığında el ile -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="6fee9-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="6fee9-112">Hello sıra iletisiyle gibi bir araç kullanarak bir JSON şeması toouse isteğe bağlı olarak, belirtebilirsiniz [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="6fee9-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="6fee9-113">Merhaba şema hello tetikleyici yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6fee9-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="6fee9-114">Şemalar hello verileri ve akış özellikleri daha kolay hello akışı aracılığıyla hello şeklini anlamanız hello Tasarımcısı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="6fee9-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="6fee9-115">Bir kuyruk iletisi alındıktan sonra toooccur istediğiniz herhangi bir ilave adımı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6fee9-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="6fee9-116">Örneğin, Office 365 aracılığıyla bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="6fee9-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="6fee9-117">Merhaba mantığı uygulama toogenerate hello geri çağırma URL'si hello tetikleyici toothis mantıksal uygulama için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6fee9-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="6fee9-118">Merhaba URL hello tetikleyici kartında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6fee9-118">hello URL appears on hello trigger card.</span></span>

![Merhaba geri çağırma URL'si hello tetikleyici kartında görüntülenir.][1]

## <a name="build-hello-function"></a><span data-ttu-id="6fee9-120">Merhaba işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fee9-120">Build hello function</span></span>
<span data-ttu-id="6fee9-121">Ardından, hello tetikleyici olarak davranır ve toohello sıra dinleyen bir işlev oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fee9-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="6fee9-122">Merhaba, [Azure işlevleri portalına](https://functions.azure.com/signin)seçin **yeni işlev**seçip hello **ServiceBusQueueTrigger - C#** şablonu.</span><span class="sxs-lookup"><span data-stu-id="6fee9-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure işlevleri portalına][2]
2. <span data-ttu-id="6fee9-124">Azure hizmet veri yolu SDK'sını kullanan hello hello bağlantı toohello Service Bus kuyruğu, yapılandırma `OnMessageReceive()` dinleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6fee9-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="6fee9-125">(Daha önce oluşturduğunuz) bir temel işlev toocall hello mantığı uygulama uç noktası tetikleyici olarak hello kuyruk iletisini kullanarak yazın.</span><span class="sxs-lookup"><span data-stu-id="6fee9-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="6fee9-126">Bir işlev tam bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6fee9-126">Here's a full example of a function.</span></span> <span data-ttu-id="6fee9-127">Merhaba örneği kullanan bir `application/json` ileti içerik türü, ancak bu tür gerektiğinde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fee9-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

<span data-ttu-id="6fee9-128">tootest, bir kuyruk iletisi gibi bir araç eklemek [hizmet veri yolu Gezgini](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="6fee9-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="6fee9-129">Merhaba mantıksal uygulamayı hemen hello işlevi hello iletisini aldıktan sonra yangın bakın.</span><span class="sxs-lookup"><span data-stu-id="6fee9-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
