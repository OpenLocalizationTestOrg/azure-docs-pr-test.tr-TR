---
title: "Azure Resource Manager çekirdek Kotayı artırmak istekleri | Microsoft Docs"
description: "Azure Resource Manager çekirdek Kotayı artırmak istekleri"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: cb6c5b3e86f126d4110d1cd29d8c9891e356e414
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="68b77-103">Resource Manager çekirdek Kotayı artırmak istekleri</span><span class="sxs-lookup"><span data-stu-id="68b77-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="68b77-104">Resource Manager çekirdek kotalarını bölge düzeyi ve SKU ailesi düzeyinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="68b77-104">Resource Manager core quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="68b77-105">Nasıl kotaları üzerinde uygulanır hakkında daha fazla bilgi [Azure aboneliği ve hizmet sınırları](http://aka.ms/quotalimits) sayfası.</span><span class="sxs-lookup"><span data-stu-id="68b77-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="68b77-106">SKU ailesi hakkında daha fazla bilgi için maliyet ve performans üzerinde karşılaştırmak [sanal makineler fiyatlandırma](http://aka.ms/pricingcompute) sayfası.</span><span class="sxs-lookup"><span data-stu-id="68b77-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="68b77-107">Artırma isteğinde bulunmak için bir kota destek çekirdeği Azure portalında çalışmasının [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68b77-107">To request an increase, create a Quota support case for Cores in the Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="68b77-108">Bilgi edinmek için nasıl [bir destek isteği oluşturmak](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) Azure portalında</span><span class="sxs-lookup"><span data-stu-id="68b77-108">Learn how to [create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in the Azure portal</span></span>

1. <span data-ttu-id="68b77-109">Sorun türü "Kota" olarak ve kota türü "Çekirdek" olarak yeni destek isteği sayfasındaki seçin.</span><span class="sxs-lookup"><span data-stu-id="68b77-109">On the new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Kota temel bilgileri dikey penceresi](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="68b77-111">"Kaynak Yöneticisi" olarak dağıtım modeli seçin ve bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="68b77-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Kota sorun dikey penceresi](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="68b77-113">Artışı gerektiren SKU ailesi seçin.</span><span class="sxs-lookup"><span data-stu-id="68b77-113">Select the SKU Families that require an increase.</span></span>

    ![Seçili SKU serisi](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="68b77-115">İstediğiniz yeni sınırları abonelikte girin.</span><span class="sxs-lookup"><span data-stu-id="68b77-115">Enter the new limits you would like on the subscription.</span></span>

    ![SKU yeni kota isteği](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="68b77-117">Bir satırı kaldırmak için SKU SKU ailesi açılan kutusunun işaretini kaldırın veya atma "x" simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="68b77-117">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="68b77-118">Her SKU ailesi için istenen kota girdikten sonra destek isteği oluşturma işlemiyle devam etmek sorun adım sayfasında "İleri" yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="68b77-118">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>
