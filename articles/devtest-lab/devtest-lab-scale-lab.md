---
title: "aaaScale kotalar ve sınırlar laboratuvarınızda Azure DevTest Labs | Microsoft Docs"
description: "Bilgi nasıl tooscale Azure DevTest Labs laboratuvarda"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="2aa40-103">Kotalar ve sınırlar DevTest Labs'de ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="2aa40-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="2aa40-104">DevTest Labs'de çalışırken hello DevTest Labs hizmet etkileyebilir Azure kaynaklarını belirli varsayılan sınırları toosome olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2aa40-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="2aa40-105">Başvurulan tooas bu kısıtlamalardır **kotaları**.</span><span class="sxs-lookup"><span data-stu-id="2aa40-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="2aa40-106">Merhaba DevTest Labs hizmet hiçbir kota zorunlu tuttukları değil.</span><span class="sxs-lookup"><span data-stu-id="2aa40-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="2aa40-107">Karşılaşabileceğiniz kotaları hello genel Azure aboneliği varsayılan kısıtlamaları ' dir.</span><span class="sxs-lookup"><span data-stu-id="2aa40-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="2aa40-108">Kotasına ulaşana kadar her Azure kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2aa40-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="2aa40-109">Her abonelik ayrı kotaları sahiptir ve abonelik başına kullanım izlenir.</span><span class="sxs-lookup"><span data-stu-id="2aa40-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="2aa40-110">Örneğin, her abonelik varsayılan kota 20 olarak belirlenen çekirdek sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2aa40-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="2aa40-111">Dört çekirdek ile laboratuvarınızda VM'ler oluşturuyorsanız, bu nedenle, daha sonra yalnızca beş VM'ler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2aa40-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="2aa40-112">[Azure aboneliği ve hizmet sınırları](https://docs.microsoft.com/azure/azure-subscription-service-limits) bazı Azure kaynakları için en yaygın kotaları hello yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="2aa40-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="2aa40-113">en yaygın olarak kullanılan bir laboratuar ortamında kaynakları hello ve hangi karşılaşabileceğiniz için kotaları dahil VM çekirdek, genel IP adresleri, ağ arabirimi, yönetilen diskleri, RBAC rol ataması ve ExpressRoute bağlantı hatları.</span><span class="sxs-lookup"><span data-stu-id="2aa40-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="2aa40-114">Kotalar ve kullanım görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="2aa40-114">View your usage and quotas</span></span>
<span data-ttu-id="2aa40-115">Bu adımlar nasıl tooview hello geçerli kotalar aboneliğinizde belirli Azure kaynaklarını ve toosee için kullandığınız her kota yüzdesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2aa40-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="2aa40-116">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2aa40-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="2aa40-117">Seçin **daha Hizmetleri**ve ardından **faturalama** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="2aa40-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="2aa40-118">Merhaba faturalama dikey penceresinde bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="2aa40-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="2aa40-119">Seçin **kullanım + kotaları**.</span><span class="sxs-lookup"><span data-stu-id="2aa40-119">Select **Usage + quotas**.</span></span>

   ![Kullanım ve kotaları düğmesi](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="2aa40-121">Merhaba kullanım + kotaları dikey penceresi görünür, farklı kaynaklar Bu abonelik ve hello yüzdesi kaynak başına kullanılan hello kota olarak listeleniyor.</span><span class="sxs-lookup"><span data-stu-id="2aa40-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Kotalar ve kullanım](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="2aa40-123">Daha fazla kaynak aboneliğinizde isteme</span><span class="sxs-lookup"><span data-stu-id="2aa40-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="2aa40-124">Bir kota cap ulaştıysanız, bir kaynağın bir abonelik hello varsayılan sınır tooa sınırını, açıklandığı gibi artırılabilir [Azure aboneliği ve hizmet sınırları](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="2aa40-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="2aa40-125">Bu adımları nasıl toorequest kota artırma hello Göster [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2aa40-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="2aa40-126">Seçin **daha Hizmetleri**seçin **faturalama**ve ardından **kullanım + kotaları**.</span><span class="sxs-lookup"><span data-stu-id="2aa40-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="2aa40-127">Merhaba kullanım + kotaları dikey biçiminde hello seçin **isteği artırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2aa40-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![İstek artış düğmesi](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="2aa40-129">toocomplete ve hello isteği göndermek, gerekli hello bilgileri Merhaba, tüm üç sekmelerde doldurun **yeni destek isteği** formu.</span><span class="sxs-lookup"><span data-stu-id="2aa40-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![İstek artış formu](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="2aa40-131">[Anlama Azure sınırları ve artar](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) Azure destek toorequest bağlantı kurma hakkında daha fazla bilgi sağlayan bir kota artırma.</span><span class="sxs-lookup"><span data-stu-id="2aa40-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="2aa40-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2aa40-132">Next steps</span></span>
* <span data-ttu-id="2aa40-133">Merhaba keşfedin [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="2aa40-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
