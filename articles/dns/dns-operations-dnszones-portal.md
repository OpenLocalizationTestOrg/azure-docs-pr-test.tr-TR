---
title: "Azure DNS'de - Azure portalında DNS bölgelerini yönetme | Microsoft Docs"
description: "DNS bölgelerini Azure portalını kullanarak yönetebilirsiniz. Bu makalede, güncelleştirme, silme ve DNS bölgelerini Azure DNS üzerinde oluşturmak açıklar"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="9e514-104">Azure portalında DNS bölgelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="9e514-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e514-105">Portal</span><span class="sxs-lookup"><span data-stu-id="9e514-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="9e514-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e514-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="9e514-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9e514-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="9e514-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9e514-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="9e514-109">Bu makalede Azure portalını kullanarak DNS bölgelerini yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e514-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="9e514-110">Platformlar arası kullanarak DNS bölgelerini yönetebilmeniz için [Azure CLI](dns-operations-dnszones-cli.md) veya Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="9e514-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="9e514-111">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e514-111">Create a DNS zone</span></span>

1. <span data-ttu-id="9e514-112">Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="9e514-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="9e514-113">Hub menüsünde **Yeni > Ağ >** ve ardından **DNS bölgesi**’ne tıklayarak DNS bölgesi oluştur dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="9e514-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS bölgesi](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="9e514-115">**DNS bölgesi oluştur** dikey penceresinde aşağıdaki değerleri girin ve **Oluştur**’a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="9e514-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="9e514-116">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="9e514-116">**Setting**</span></span> | <span data-ttu-id="9e514-117">**Değer**</span><span class="sxs-lookup"><span data-stu-id="9e514-117">**Value**</span></span> | <span data-ttu-id="9e514-118">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="9e514-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="9e514-119">**Ad**</span><span class="sxs-lookup"><span data-stu-id="9e514-119">**Name**</span></span>|<span data-ttu-id="9e514-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="9e514-120">contoso.com</span></span>|<span data-ttu-id="9e514-121">DNS bölgesinin adı</span><span class="sxs-lookup"><span data-stu-id="9e514-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="9e514-122">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="9e514-122">**Subscription**</span></span>|<span data-ttu-id="9e514-123">[Aboneliğiniz]</span><span class="sxs-lookup"><span data-stu-id="9e514-123">[Your subscription]</span></span>|<span data-ttu-id="9e514-124">DNS bölgesini oluşturmak için bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="9e514-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="9e514-125">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="9e514-125">**Resource group**</span></span>|<span data-ttu-id="9e514-126">**Yeni oluştur:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="9e514-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="9e514-127">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e514-127">Create a resource group.</span></span> <span data-ttu-id="9e514-128">Kaynak grubu adı, seçili abonelik içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9e514-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="9e514-129">Kaynak grupları hakkında daha fazla bilgi için, [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)’a genel bakış makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="9e514-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="9e514-130">**Konum**</span><span class="sxs-lookup"><span data-stu-id="9e514-130">**Location**</span></span>|<span data-ttu-id="9e514-131">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="9e514-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="9e514-132">Kaynak grubu, kaynak grubunun konumunu ifade eder ve DNS bölgesini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="9e514-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="9e514-133">DNS bölgesinin konumu her zaman "genel" şeklindedir ve gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="9e514-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="9e514-134">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="9e514-134">List DNS zones</span></span>

<span data-ttu-id="9e514-135">Azure portalında gidin **daha fazla hizmet** > **ağ** > **DNS bölgeleri**.</span><span class="sxs-lookup"><span data-stu-id="9e514-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="9e514-136">Her DNS bölgesinin kendi kaynağı, kayıt kümesi sayısı gibi bilgiler ve ad sunucuları bu görünümden görüntülenebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e514-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="9e514-137">Sütun **ad sunucuları** tıklatın eklemek için varsayılan görünümünde değil **sütunları**seçin **ad sunucuları** tıklatıp **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="9e514-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![DNS bölgelerini listeleme](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="9e514-139">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="9e514-139">Delete a DNS zone</span></span>

<span data-ttu-id="9e514-140">Bir DNS bölgesi portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="9e514-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="9e514-141">Üzerinde **DNS bölgesi** dikey penceresinde tıklatın **bölgeyi Sil**.</span><span class="sxs-lookup"><span data-stu-id="9e514-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="9e514-142">DNS bölgesini silmek isteyen onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="9e514-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="9e514-143">Bir DNS bölgesi silme bölgede bulunan tüm kayıtları siler.</span><span class="sxs-lookup"><span data-stu-id="9e514-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e514-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e514-144">Next steps</span></span>

<span data-ttu-id="9e514-145">DNS bölgesi ve kayıtları ile ziyaret ederek çalışmayı öğrenin [Azure Azure portalını kullanarak DNS ile çalışmaya başlama](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9e514-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>