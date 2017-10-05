---
title: "Web uygulama kaynakları başka bir kaynak grubuna taşıma"
description: "Burada, Web uygulamaları ve uygulama hizmetleri bir kaynak grubundan diğerine taşıyabilirsiniz senaryoları açıklanmıştır."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 1b5059dc052005b6079f70ecf6771a3771df8d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="68d67-103">Desteklenen taşıma yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="68d67-103">Supported Move Configurations</span></span>
<span data-ttu-id="68d67-104">Azure Web uygulaması kaynakları kullanarak taşıyabilirsiniz [Kaynak Yöneticisi taşıma kaynakları API](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="68d67-104">You can move Azure Web App resources using the [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="68d67-105">Azure Web uygulamaları, şu anda aşağıdaki taşıma senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="68d67-105">Azure Web Apps currently supports the following move scenarios:</span></span>

* <span data-ttu-id="68d67-106">Bir kaynak grubu (web uygulamaları, uygulama hizmeti planları ve sertifikaları) tüm içeriğini başka bir kaynak grubuna taşınır.</span><span class="sxs-lookup"><span data-stu-id="68d67-106">Move the entire contents of a resource group (web apps, app service plans, and certificates) to another resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="68d67-107">Hedef kaynak grubu, bu senaryoda tüm Microsoft.Web kaynakları içeremez.</span><span class="sxs-lookup"><span data-stu-id="68d67-107">The destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="68d67-108">Tek tek web uygulamaları, hala bunları (uygulama hizmeti planı eski kaynak grubunda kalır), geçerli uygulama hizmeti planında barındırma sırasında farklı bir kaynak grubuna taşıyın.</span><span class="sxs-lookup"><span data-stu-id="68d67-108">Move individual web apps to a different resource group, while still hosting them in their current app service plan (the app service plan stays in the old resource group).</span></span>


