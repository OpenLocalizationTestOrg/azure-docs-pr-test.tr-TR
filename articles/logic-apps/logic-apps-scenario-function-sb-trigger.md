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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Senaryo: bir mantıksal uygulama Azure işlevleri ve Azure Service Bus ile Tetikle

Bir uzun süre çalışan dinleyicisi ya da görev toodeploy gerektiğinde Azure işlevleri toocreate tetikleyici için bir mantıksal uygulama kullanabilirsiniz. Örneğin, bir sıra üzerinde dinleyen bir işlev oluşturun ve hemen bir mantıksal uygulama itme tetikleyici olarak tetiklenecek.

## <a name="build-hello-logic-app"></a>Merhaba mantıksal uygulama oluşturma
Bu örnekte, tetiklenen toobe gerektiren her mantıksal uygulama için çalışan bir işleve sahip. İlk olarak, bir HTTP isteği tetikleyicisine sahip bir mantıksal uygulama oluşturun. bir kuyruk iletisi alındığında Bu uç hello işlevi çağırır.  

1. Bir mantıksal uygulama oluşturun.
2. Select hello **bir HTTP isteği alındığında el ile -** tetikleyici.
   Hello sıra iletisiyle gibi bir araç kullanarak bir JSON şeması toouse isteğe bağlı olarak, belirtebilirsiniz [jsonschema.net](http://jsonschema.net). Merhaba şema hello tetikleyici yapıştırın. Şemalar hello verileri ve akış özellikleri daha kolay hello akışı aracılığıyla hello şeklini anlamanız hello Tasarımcısı yardımcı olur.
2. Bir kuyruk iletisi alındıktan sonra toooccur istediğiniz herhangi bir ilave adımı ekleyin. Örneğin, Office 365 aracılığıyla bir e-posta gönderin.  
3. Merhaba mantığı uygulama toogenerate hello geri çağırma URL'si hello tetikleyici toothis mantıksal uygulama için kaydedin. Merhaba URL hello tetikleyici kartında görüntülenir.

![Merhaba geri çağırma URL'si hello tetikleyici kartında görüntülenir.][1]

## <a name="build-hello-function"></a>Merhaba işlevi oluşturma
Ardından, hello tetikleyici olarak davranır ve toohello sıra dinleyen bir işlev oluşturmanız gerekir.

1. Merhaba, [Azure işlevleri portalına](https://functions.azure.com/signin)seçin **yeni işlev**seçip hello **ServiceBusQueueTrigger - C#** şablonu.
   
    ![Azure işlevleri portalına][2]
2. Azure hizmet veri yolu SDK'sını kullanan hello hello bağlantı toohello Service Bus kuyruğu, yapılandırma `OnMessageReceive()` dinleyicisi.
3. (Daha önce oluşturduğunuz) bir temel işlev toocall hello mantığı uygulama uç noktası tetikleyici olarak hello kuyruk iletisini kullanarak yazın. Bir işlev tam bir örneği burada verilmiştir. Merhaba örneği kullanan bir `application/json` ileti içerik türü, ancak bu tür gerektiğinde değiştirebilirsiniz.
   
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

tootest, bir kuyruk iletisi gibi bir araç eklemek [hizmet veri yolu Gezgini](https://github.com/paolosalvatori/ServiceBusExplorer). Merhaba mantıksal uygulamayı hemen hello işlevi hello iletisini aldıktan sonra yangın bakın.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
