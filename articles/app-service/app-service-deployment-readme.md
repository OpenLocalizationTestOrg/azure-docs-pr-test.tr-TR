---
title: "Azure uygulama hizmeti uygulamalarını dağıtma"
description: "Bilgi uygulama hizmeti iş uygulamaları dağıtma hakkında"
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
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="0e9a9-104">Azure uygulama hizmeti dağıtımına genel bakış</span><span class="sxs-lookup"><span data-stu-id="0e9a9-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="0e9a9-105">Azure uygulama hizmeti güçlü ve esnek dağıtım iş akışları oluşturma desteklemek için ayarlanmış bir zengin ve tümleşik özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="0e9a9-106">Uygulama dağıtımı, WebDeploy ve FTP sürekli tümleştirme veya yerel kaynak denetimi yayımlamayı dahil seçenekleri yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="0e9a9-107">Önerilen üretim uygulama dağıtımı için dağıtım yuvası takas yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="0e9a9-108">Dağıtım yuvaları, üretim uygulamalarla ilişkili hazırlama ve tümleştirme ortamları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="0e9a9-109">Dağıtım yuvaları yapılandırıldığında ve doğrulama için web trafiği ile hedef ve trafik dağıtımı üretime aşağı zaman ile isteğe bağlı takas ve Isınma otomatik.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="0e9a9-110">Visual Studio yayın yönetimi gibi yayın yönetim ürünleri aracılığıyla bir dağıtım iş akışı adımları kolayca otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="0e9a9-111">Bu çözüm kaynaklar birlikte için yararlıdır (örn. veri deposu) yinelenme ve birden çok birimi arasında bir çoğaltma dağıtım.</span><span class="sxs-lookup"><span data-stu-id="0e9a9-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

