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
# <a name="using-webjobs-in-azure-app-service"></a>Azure Uygulama Hizmeti’nde WebJobs kullanımı
Bu makalede hakkındaki toodocumentation kaynakların bağlantıları toouse Azure Web işleri ve Azure WebJobs SDK hello. Azure Web işleri sağlamak kolay bir yolu toorun komut dosyaları veya programları olarak arka plan işlemleri üzerinde [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Karşıya yükleme ve cmd gibi yürütülebilir bir dosyayı çalıştırıp .bat uzantılarını dener, exe (.NET) ps1, paylaş, php, py, js ve jar. Bu programlar bir zamanlamada (cron) veya sürekli olarak WebJobs olarak çalıştırın.

Merhaba WebJobs SDK daha kolay toouse Azure Storage kolaylaştırır. Merhaba WebJobs SDK bağlama ve Microsoft Azure Storage Bloblarında, kuyruklar ve tablolar yanı sıra ile Service Bus kuyruklarını çalışan tetikleyici sistem sahiptir.

Oluşturma, dağıtma ve yönetme WebJobs tümleşik araçları Visual Studio ile sorunsuz olarak gerçekleştirilir. Şablonlardan Web işleri oluşturmak, yayımlama ve (Çalıştır/stop/İzleyici/debug) yönetmek bunları.

Merhaba WebJobs hello Azure portal panosunda hello özelliği tooinvoke tek tek işlevlerinde Web işleri de dahil olmak üzere Web işleri, hello yürütülmesi üzerinde tam denetime güçlü yönetim yetenekleri sağlar. Merhaba Pano ayrıca işlevi çalışma zamanları ve günlük çıktısı görüntüler.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

