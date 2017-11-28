---
title: Azure App Service'te aaaWebJobs
description: "Zamanlanmış Görevler oluşturun ve depolama ve hizmet veri yolu gibi hizmetlerle etkileşimde veya nasıl toobuild WebJobs toorun arka plan testleri öğrenin."
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
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="bbc3f-103">Azure Uygulama Hizmeti’nde WebJobs kullanımı</span><span class="sxs-lookup"><span data-stu-id="bbc3f-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="bbc3f-104">Bu makalede hakkındaki toodocumentation kaynakların bağlantıları toouse Azure Web işleri ve Azure WebJobs SDK hello.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="bbc3f-105">Azure Web işleri sağlamak kolay bir yolu toorun komut dosyaları veya programları olarak arka plan işlemleri üzerinde [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="bbc3f-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="bbc3f-106">Karşıya yükleme ve cmd gibi yürütülebilir bir dosyayı çalıştırıp .bat uzantılarını dener, exe (.NET) ps1, paylaş, php, py, js ve jar.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="bbc3f-107">Bu programlar bir zamanlamada (cron) veya sürekli olarak WebJobs olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="bbc3f-108">Merhaba WebJobs SDK daha kolay toouse Azure Storage kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="bbc3f-109">Merhaba WebJobs SDK bağlama ve Microsoft Azure Storage Bloblarında, kuyruklar ve tablolar yanı sıra ile Service Bus kuyruklarını çalışan tetikleyici sistem sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="bbc3f-110">Oluşturma, dağıtma ve yönetme WebJobs tümleşik araçları Visual Studio ile sorunsuz olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="bbc3f-111">Şablonlardan Web işleri oluşturmak, yayımlama ve (Çalıştır/stop/İzleyici/debug) yönetmek bunları.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="bbc3f-112">Merhaba WebJobs hello Azure portal panosunda hello özelliği tooinvoke tek tek işlevlerinde Web işleri de dahil olmak üzere Web işleri, hello yürütülmesi üzerinde tam denetime güçlü yönetim yetenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="bbc3f-113">Merhaba Pano ayrıca işlevi çalışma zamanları ve günlük çıktısı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bbc3f-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

