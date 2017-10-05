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
# <a name="using-webjobs-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde WebJobs kullanımı
Bu belge kaynakları Azure Web işleri ve Azure WebJobs SDK nasıl kullanılacağı hakkında makale bağlanır. Azure Web işleri komut dosyaları veya programlar arka plan işlemleri olarak çalıştırmak için kolay bir yol sağlamak [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Karşıya yükleme ve cmd gibi yürütülebilir bir dosyayı çalıştırıp .bat uzantılarını dener, exe (.NET) ps1, paylaş, php, py, js ve jar. Bu programlar bir zamanlamada (cron) veya sürekli olarak WebJobs olarak çalıştırın.

WebJobs SDK Azure Storage kullanmayı daha kolay hale getirir. WebJobs SDK bağlama ve Microsoft Azure Storage Bloblarında, kuyruklar ve tablolar yanı sıra ile Service Bus kuyruklarını çalışan tetikleyici sistem sahiptir.

Oluşturma, dağıtma ve yönetme WebJobs tümleşik araçları Visual Studio ile sorunsuz olarak gerçekleştirilir. Şablonlardan Web işleri oluşturmak, yayımlama ve (Çalıştır/stop/İzleyici/debug) yönetmek bunları.

Web işleri Panosu'nu Azure portalında WebJobs, Web işleri içinde tek tek işlevleri çağırma yeteneği dahil olmak üzere yürütülmesi üzerinde tam denetime güçlü yönetim yetenekleri sağlar. Pano ayrıca işlevi çalışma zamanları ve günlük çıktısı görüntüler.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

