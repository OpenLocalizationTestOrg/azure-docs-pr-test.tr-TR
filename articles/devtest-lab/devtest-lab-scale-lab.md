---
title: "Ölçeklendirme kotalar ve sınırlar laboratuvarınızda Azure DevTest Labs | Microsoft Docs"
description: "Azure DevTest Labs'de Laboratuvar ölçeklendirmek öğrenin"
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
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="881dd-103">Kotalar ve sınırlar DevTest Labs'de ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="881dd-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="881dd-104">DevTest Labs'de çalışırken DevTest Labs hizmet etkileyebilecek bazı Azure kaynakları için belirli varsayılan sınırları olduğunu fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881dd-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="881dd-105">Bu sınırlar denir **kotaları**.</span><span class="sxs-lookup"><span data-stu-id="881dd-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="881dd-106">DevTest Labs hizmet hiçbir kota zorunlu tuttukları değil.</span><span class="sxs-lookup"><span data-stu-id="881dd-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="881dd-107">Karşılaşabileceğiniz kotaları varsayılan genel Azure aboneliğinin sınırlamalardır.</span><span class="sxs-lookup"><span data-stu-id="881dd-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="881dd-108">Kotasına ulaşana kadar her Azure kaynak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881dd-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="881dd-109">Her abonelik ayrı kotaları sahiptir ve abonelik başına kullanım izlenir.</span><span class="sxs-lookup"><span data-stu-id="881dd-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="881dd-110">Örneğin, her abonelik varsayılan kota 20 olarak belirlenen çekirdek sahiptir.</span><span class="sxs-lookup"><span data-stu-id="881dd-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="881dd-111">Dört çekirdek ile laboratuvarınızda VM'ler oluşturuyorsanız, bu nedenle, daha sonra yalnızca beş VM'ler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="881dd-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="881dd-112">[Azure aboneliği ve hizmet sınırları](https://docs.microsoft.com/azure/azure-subscription-service-limits) bazı Azure kaynakları için en yaygın kotaları yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="881dd-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="881dd-113">Kaynakları bir laboratuar ortamında en yaygın olarak kullanılan ve hangi karşılaşabileceğiniz için kotaları içerir VM çekirdek, genel IP adresleri, ağ arabirimi, yönetilen diskleri, RBAC rol ataması ve ExpressRoute bağlantı hatları.</span><span class="sxs-lookup"><span data-stu-id="881dd-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="881dd-114">Kotalar ve kullanım görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="881dd-114">View your usage and quotas</span></span>
<span data-ttu-id="881dd-115">Bu adımlar nasıl aboneliğinizde belirli Azure kaynakları için geçerli kotalar görüntülemek ve her kota yüzdesini kullanıldığını görmek için gösterir.</span><span class="sxs-lookup"><span data-stu-id="881dd-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="881dd-116">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="881dd-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="881dd-117">Seçin **daha Hizmetleri**ve ardından **faturalama** listeden.</span><span class="sxs-lookup"><span data-stu-id="881dd-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="881dd-118">Faturalama dikey penceresinde bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="881dd-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="881dd-119">Seçin **kullanım + kotaları**.</span><span class="sxs-lookup"><span data-stu-id="881dd-119">Select **Usage + quotas**.</span></span>

   ![Kullanım ve kotaları düğmesi](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="881dd-121">Kullanım + kotaları dikey penceresi görünür, listeyi farklı kaynaklar bu abonelikte ve kaynak başına kullanılan kota yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="881dd-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Kotalar ve kullanım](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="881dd-123">Daha fazla kaynak aboneliğinizde isteme</span><span class="sxs-lookup"><span data-stu-id="881dd-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="881dd-124">Bir kota cap ulaştıysanız, bir kaynağın bir abonelik varsayılan sınır sınırına kadar açıklandığı gibi artırılabilir [Azure aboneliği ve hizmet sınırları](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="881dd-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="881dd-125">Bu adımları aracılığıyla kota artışı isteği göndermek üzere nasıl Göster [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="881dd-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="881dd-126">Seçin **daha Hizmetleri**seçin **faturalama**ve ardından **kullanım + kotaları**.</span><span class="sxs-lookup"><span data-stu-id="881dd-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="881dd-127">Kullanım + kotaları dikey penceresinde, select **isteği artırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="881dd-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![İstek artış düğmesi](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="881dd-129">Tamamlayıp isteği göndermek için gerekli bilgiler tüm üç sekmelerde doldurmak **yeni destek isteği** formu.</span><span class="sxs-lookup"><span data-stu-id="881dd-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![İstek artış formu](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="881dd-131">[Anlama Azure sınırları ve artar](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) kota artışı isteği göndermek üzere Azure desteğine başvurarak hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="881dd-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="881dd-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="881dd-132">Next steps</span></span>
* <span data-ttu-id="881dd-133">Araştır [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="881dd-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
