---
title: "Galeri aaaRelated ve hello bağlı kaynaklar döşeme"
description: "Merhaba döşeme Galerisi'nde hello Azure Önizleme portalının görüntüleneceğini ilgili ve bağlı kaynaklar hakkında bilgi edinin."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a><span data-ttu-id="3ff11-103">Merhaba döşeme galerisinde ilgili ve bağlantılı kaynakları</span><span class="sxs-lookup"><span data-stu-id="3ff11-103">Related and linked resources in hello tile gallery</span></span>
<span data-ttu-id="3ff11-104">Merhaba döşeme galeri toofind döşeme belirli bir kaynak için etkinleştirir ve geçerli dikey pencerenizin sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="3ff11-104">hello tile gallery enables you toofind tiles for a particular resource and drag them onto your current blade.</span></span> <span data-ttu-id="3ff11-105">Merhaba döşeme Galerisi kullanarak, kaynakları span Yönetimi görünümlerini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ff11-105">Using hello tile gallery, you can create management views that span resources.</span></span> <span data-ttu-id="3ff11-106">Belirtilen herhangi bir kaynağa için kaynakları, kaynak grubu ve hello kaynaktan tooor bağlantı herhangi bir kaynağa tüm hello kaynaklar dahil hello ilgili.</span><span class="sxs-lookup"><span data-stu-id="3ff11-106">For any specified resource, hello related resources include all hello resources in its resource group, and any resources that link tooor from hello resource.</span></span>

## <a name="linked-resources-in-resource-manager"></a><span data-ttu-id="3ff11-107">Bağlı kaynaklar Kaynak Yöneticisi'nde</span><span class="sxs-lookup"><span data-stu-id="3ff11-107">Linked resources in Resource Manager</span></span>
<span data-ttu-id="3ff11-108">Bağlama hello Resource Manager özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="3ff11-108">Linking is a feature of hello Resource Manager.</span></span>  <span data-ttu-id="3ff11-109">Hello aynı bulundukları değil olsa bile kaynaklar arasındaki toodeclare ilişkilerini sağlar kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="3ff11-109">It enables you toodeclare relationships between resources even if they do not reside in hello same resource group.</span></span> <span data-ttu-id="3ff11-110">Bağlama hello çalışma zamanı kaynaklarınızı, fatura üzerinde hiçbir etkisi ve rol tabanlı erişim üzerinde hiçbir etkisi üzerinde etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="3ff11-110">Linking has no impact on hello runtime of your resources, no impact on billing, and no impact on role-based access.</span></span>  <span data-ttu-id="3ff11-111">Bu toorepresent ilişkileri hello döşeme galeri zengin yönetim sağlayabilir gibi araçlar deneyimi kullanabilirsiniz yalnızca bir mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="3ff11-111">It's simply a mechanism you can use toorepresent relationships so that tools like hello tile gallery can provide a rich management experience.</span></span>  <span data-ttu-id="3ff11-112">Araçlarınızı hello bağlantıları API kullanarak hello bağlantıları inceleyin ve de özel İlişkileri Yönetimi deneyimleri sunar.</span><span class="sxs-lookup"><span data-stu-id="3ff11-112">Your tools can inspect hello links using hello links API and provide custom relationship management experiences as well.</span></span> 

## <a name="how-do-i-link-my-resources"></a><span data-ttu-id="3ff11-113">Kaynaklarım nasıl bağlanır?</span><span class="sxs-lookup"><span data-stu-id="3ff11-113">How do I link my resources?</span></span>
<span data-ttu-id="3ff11-114">Merhaba portalı üzerinden veya bir şablonu Azure PowerShell veya Azure CLI aracılığıyla dağıtarak kaynakları oluşturduğunuzda, bağlantılar için bazı bağımlı kaynakları otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3ff11-114">When you create resources through hello portal or by deploying a template through Azure PowerShell or Azure CLI, links are automatically created for some dependent resources.</span></span> <span data-ttu-id="3ff11-115">Hello kullanarak program aracılığıyla da kaynaklara bağlayabilirsiniz [bağlı kaynakları REST API](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="3ff11-115">You can also programmatically link resources by using hello [Linked Resources REST API](/rest/api/resources/resourcelinks).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ff11-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ff11-116">Next steps</span></span>
* <span data-ttu-id="3ff11-117">Bir giriş toowriting Resource Manager şablonları gerekirse bkz [şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3ff11-117">If you need an introduction toowriting Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3ff11-118">Merhaba portal üzerinden kaynak gruplarıyla çalışma hakkında daha fazla toounderstand bkz [kullanarak Azure kaynaklarınızı Azure portal toomanage hello](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ff11-118">toounderstand more about working with resource groups through hello portal, see [Using hello Azure portal toomanage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>

