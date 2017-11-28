---
title: "aaaAzure Resource Manager çekirdek Kotayı artırmak istekleri | Microsoft Docs"
description: "Azure Resource Manager çekirdek Kotayı artırmak istekleri"
author: ganganarayanan
ms.author: gangan
ms.date: 1/18/2017
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: b158b9f0e0338eb239da9253c2146ea93c02e316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-core-quota-increase-requests"></a><span data-ttu-id="d9324-103">Resource Manager çekirdek Kotayı artırmak istekleri</span><span class="sxs-lookup"><span data-stu-id="d9324-103">Resource Manager core quota increase requests</span></span>

<span data-ttu-id="d9324-104">Resource Manager çekirdek kotalarını hello bölge düzeyinde ve SKU ailesi düzeyinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d9324-104">Resource Manager core quotas are enforced at hello region level and SKU family level.</span></span>
<span data-ttu-id="d9324-105">Kotalar hello üzerinde nasıl zorlanır hakkında daha fazla bilgi [Azure aboneliği ve hizmet sınırları](http://aka.ms/quotalimits) sayfası.</span><span class="sxs-lookup"><span data-stu-id="d9324-105">Learn more about how quotas are enforced on hello [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="d9324-106">SKU ailesi hakkında daha fazla toolearn, karşılaştırmanızı maliyet ve performansı hello üzerinde [sanal makineler fiyatlandırma](http://aka.ms/pricingcompute) sayfası.</span><span class="sxs-lookup"><span data-stu-id="d9324-106">toolearn more about SKU Families, you may compare cost and performance on hello [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="d9324-107">toorequest artış, bir hello Azure portal için çekirdek kota destek servis talebi oluşturma [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d9324-107">toorequest an increase, create a Quota support case for Cores in hello Azure portal, [https://portal.azure.com](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="d9324-108">Nasıl çok öğrenin[bir destek isteği oluşturmak](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) hello Azure portal'ın</span><span class="sxs-lookup"><span data-stu-id="d9324-108">Learn how too[create a support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) in hello Azure portal</span></span>

1. <span data-ttu-id="d9324-109">Merhaba yeni destek isteği sayfasında, sorunu türü "Kota" olarak ve "Çekirdek" olarak kota türü seçin.</span><span class="sxs-lookup"><span data-stu-id="d9324-109">On hello new support request page, select Issue type as "Quota" and Quota type as "Cores".</span></span>

    ![Kota temel bilgileri dikey penceresi](./media/resource-manager-core-quotas-request/Basics-blade.png)

2. <span data-ttu-id="d9324-111">"Kaynak Yöneticisi" olarak dağıtım modeli seçin ve bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="d9324-111">Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Kota sorun dikey penceresi](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="d9324-113">Artışı gerektiren Hello SKU ailesi seçin.</span><span class="sxs-lookup"><span data-stu-id="d9324-113">Select hello SKU Families that require an increase.</span></span>

    ![Seçili SKU serisi](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="d9324-115">Merhaba yeni sınırları hello abonelikte istediğiniz girin.</span><span class="sxs-lookup"><span data-stu-id="d9324-115">Enter hello new limits you would like on hello subscription.</span></span>

    ![SKU yeni kota isteği](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="d9324-117">tooremove bir satır hello SKU simgesinden hello SKU ailesi tıklayın veya açılır hello atma "x" seçeneğinin işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d9324-117">tooremove a line, uncheck hello SKU from hello SKU family dropdown or click hello discard "x" icon.</span></span>
<span data-ttu-id="d9324-118">Merhaba istenen kota her SKU ailesi için girdikten sonra "İleri" Merhaba üzerinde sorun adım sayfa toocontinue hello destek isteği oluşturma ile tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9324-118">After entering hello desired quota for each SKU family, click "Next" on hello Problem step page toocontinue with hello support request creation.</span></span>
