---
title: "Senaryo - tetikleyici logic apps ile Azure işlevleri ve Azure Service Bus | Microsoft Docs"
description: "Azure işlevleri ve Azure Service Bus kullanarak bir mantıksal uygulama tetiklemek için bir işlev oluşturun"
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
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="ae5f6-103">Senaryo: bir mantıksal uygulama Azure işlevleri ve Azure Service Bus ile Tetikle</span><span class="sxs-lookup"><span data-stu-id="ae5f6-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="ae5f6-104">Azure işlevleri, bir uzun süre çalışan dinleyicisi veya görev dağıtmak gerektiğinde bir mantıksal uygulama için bir tetikleyici oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="ae5f6-105">Örneğin, bir sıra üzerinde dinleyen bir işlev oluşturun ve hemen bir mantıksal uygulama itme tetikleyici olarak tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="ae5f6-106">Mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae5f6-106">Build the logic app</span></span>
<span data-ttu-id="ae5f6-107">Bu örnekte, tetiklenmesi için gereken her mantıksal uygulama için çalışan bir işleve sahip.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="ae5f6-108">İlk olarak, bir HTTP isteği tetikleyicisine sahip bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="ae5f6-109">Bir kuyruk iletisi alındığında Bu uç işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="ae5f6-110">Bir mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-110">Create a logic app.</span></span>
2. <span data-ttu-id="ae5f6-111">Seçin **bir HTTP isteği alındığında el ile -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="ae5f6-112">İsteğe bağlı olarak, gibi bir araç kullanarak sıraya ileti ile kullanmak için JSON şeması belirtebilirsiniz [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="ae5f6-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="ae5f6-113">Şema tetikleyicinin yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="ae5f6-114">Şemalar, iş akışı aracılığıyla daha kolay veri ve akış özellikleri şeklini anlamanız Tasarımcısı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="ae5f6-115">Bir kuyruk iletisi alındıktan sonra gerçekleştirilmesini istediğiniz herhangi bir ilave adımı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="ae5f6-116">Örneğin, Office 365 aracılığıyla bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="ae5f6-117">Bu mantıksal uygulama tetikleyiciye geri çağırma URL'si oluşturmak için mantıksal uygulama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="ae5f6-118">URL tetikleyici kart üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-118">The URL appears on the trigger card.</span></span>

![Geri çağırma URL'si tetikleyici kart üzerinde görüntülenir.][1]

## <a name="build-the-function"></a><span data-ttu-id="ae5f6-120">İşlev oluşturma</span><span class="sxs-lookup"><span data-stu-id="ae5f6-120">Build the function</span></span>
<span data-ttu-id="ae5f6-121">Ardından, tetikleyici olarak davranır ve sıraya dinleyen bir işlev oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="ae5f6-122">İçinde [Azure işlevleri portalına](https://functions.azure.com/signin)seçin **yeni işlev**ve ardından **ServiceBusQueueTrigger - C#** şablonu.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![Azure işlevleri portalına][2]
2. <span data-ttu-id="ae5f6-124">Azure hizmet veri yolu SDK'sını kullanan Service Bus kuyruğuna bağlantıyı yapılandırmak `OnMessageReceive()` dinleyicisi.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="ae5f6-125">Tetikleyici olarak kuyruk iletisini kullanarak (daha önce oluşturduğunuz) mantığı uygulama uç noktasını çağırmak için bir temel işlevi yazma.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="ae5f6-126">Bir işlev tam bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-126">Here's a full example of a function.</span></span> <span data-ttu-id="ae5f6-127">Örnek kullanan bir `application/json` ileti içerik türü, ancak bu tür gerektiğinde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="ae5f6-128">Test etmek için bir kuyruk iletisi gibi bir araç eklemek [hizmet veri yolu Gezgini](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="ae5f6-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="ae5f6-129">Hemen işlevi iletiyi aldıktan sonra yangın mantıksal uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="ae5f6-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
