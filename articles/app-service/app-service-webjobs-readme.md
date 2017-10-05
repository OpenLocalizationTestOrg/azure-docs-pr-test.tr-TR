---
title: "Azure App Service'te Web işleri"
description: "Arka plan testleri çalıştırmak, depolama ve hizmet veri yolu gibi hizmetlerle etkileşim ve zamanlanmış görevler oluşturmak için Web işleri oluşturmayı öğrenin."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="5c5ea-103">Azure Uygulama Hizmeti’nde WebJobs kullanımı</span><span class="sxs-lookup"><span data-stu-id="5c5ea-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="5c5ea-104">Bu belge kaynakları Azure Web işleri ve Azure WebJobs SDK nasıl kullanılacağı hakkında makale bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="5c5ea-105">Azure Web işleri komut dosyaları veya programlar arka plan işlemleri olarak çalıştırmak için kolay bir yol sağlamak [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5c5ea-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="5c5ea-106">Karşıya yükleme ve cmd gibi yürütülebilir bir dosyayı çalıştırıp .bat uzantılarını dener, exe (.NET) ps1, paylaş, php, py, js ve jar.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="5c5ea-107">Bu programlar bir zamanlamada (cron) veya sürekli olarak WebJobs olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="5c5ea-108">WebJobs SDK Azure Storage kullanmayı daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="5c5ea-109">WebJobs SDK bağlama ve Microsoft Azure Storage Bloblarında, kuyruklar ve tablolar yanı sıra ile Service Bus kuyruklarını çalışan tetikleyici sistem sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="5c5ea-110">Oluşturma, dağıtma ve yönetme WebJobs tümleşik araçları Visual Studio ile sorunsuz olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="5c5ea-111">Şablonlardan Web işleri oluşturmak, yayımlama ve (Çalıştır/stop/İzleyici/debug) yönetmek bunları.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="5c5ea-112">Web işleri Panosu'nu Azure portalında WebJobs, Web işleri içinde tek tek işlevleri çağırma yeteneği dahil olmak üzere yürütülmesi üzerinde tam denetime güçlü yönetim yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="5c5ea-113">Pano ayrıca işlevi çalışma zamanları ve günlük çıktısı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5c5ea-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

