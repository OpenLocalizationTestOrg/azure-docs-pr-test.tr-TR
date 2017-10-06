---
title: "aaaMove Web uygulama kaynakları tooanother kaynak grubu"
description: "Burada, Web uygulamaları ve uygulama hizmetleri bir kaynak grubu tooanother taşıyabilirsiniz hello senaryoları açıklanmıştır."
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
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a><span data-ttu-id="0451f-103">Desteklenen taşıma yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="0451f-103">Supported Move Configurations</span></span>
<span data-ttu-id="0451f-104">Hello kullanarak Azure Web uygulaması kaynaklarına taşıyabilirsiniz [Kaynak Yöneticisi taşıma kaynakları API](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0451f-104">You can move Azure Web App resources using hello [Resource Manager Move Resources API](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="0451f-105">Azure Web uygulamaları, şu anda hello aşağıdaki taşıma senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="0451f-105">Azure Web Apps currently supports hello following move scenarios:</span></span>

* <span data-ttu-id="0451f-106">Bir kaynak grubu (web uygulamaları, uygulama hizmeti planları ve sertifikaları) tüm içeriğini Hello taşıma tooanother kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="0451f-106">Move hello entire contents of a resource group (web apps, app service plans, and certificates) tooanother resource group.</span></span> 
   > [!Note]
   > <span data-ttu-id="0451f-107">Merhaba hedef kaynak grubu, bu senaryoda tüm Microsoft.Web kaynakları içeremez.</span><span class="sxs-lookup"><span data-stu-id="0451f-107">hello destination resource group can not contain any Microsoft.Web resources in this scenario.</span></span>

* <span data-ttu-id="0451f-108">Tek tek web uygulamaları tooa farklı bir kaynak grubu, hala bunları kendi geçerli bir uygulama hizmeti planında (Merhaba app service planı kalır hello eski kaynak grubunda) barındırma sırasında taşıyın.</span><span class="sxs-lookup"><span data-stu-id="0451f-108">Move individual web apps tooa different resource group, while still hosting them in their current app service plan (hello app service plan stays in hello old resource group).</span></span>


