---
title: "aaaDeploying uygulamaları tooAzure uygulama hizmeti"
description: "TooDeploy uygulamaları tooApp hizmeti nasıl çalıştığını öğrenin"
keywords: "dağıtımı, dağıtım, app service, azure uygulama hizmeti"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="d1b85-104">Azure uygulama hizmeti dağıtımına genel bakış</span><span class="sxs-lookup"><span data-stu-id="d1b85-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="d1b85-105">Azure uygulama hizmeti bir zengin sağlar ve güçlü ve esnek dağıtım iş akışları oluşturma toosupport tümleşik özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d1b85-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="d1b85-106">Uygulama dağıtımı, WebDeploy ve FTP sürekli tümleştirme veya yerel kaynak denetimi yayımlamayı dahil seçenekleri yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1b85-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="d1b85-107">Merhaba yöntemi üretim uygulama dağıtımı için dağıtım yuvası takas önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1b85-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="d1b85-108">Dağıtım yuvaları, üretim uygulamalarla ilişkili hazırlama ve tümleştirme ortamları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d1b85-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="d1b85-109">Dağıtım yuvaları yapılandırıldığında ve doğrulama için web trafiği ile hedef ve trafik dağıtım tooproduction aşağı zaman ile isteğe bağlı takas ve Isınma otomatik.</span><span class="sxs-lookup"><span data-stu-id="d1b85-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="d1b85-110">Visual Studio yayın yönetimi gibi yayın yönetim ürünleri aracılığıyla bir dağıtım iş akışı Hello adımlardan kolayca otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="d1b85-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="d1b85-111">Bu çözüm kaynaklar birlikte için yararlıdır (örn. veri deposu) yinelenme ve birden çok birimi arasında bir çoğaltma dağıtım.</span><span class="sxs-lookup"><span data-stu-id="d1b85-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

