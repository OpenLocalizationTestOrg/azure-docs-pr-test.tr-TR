---
title: "aaaManage DNS bölgeleri Azure DNS - Azure portalı | Microsoft Docs"
description: "DNS bölgelerini hello Azure portal kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma"
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="03af3-104">Azure portal toomanage DNS bölgelerini nasıl hello</span><span class="sxs-lookup"><span data-stu-id="03af3-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="03af3-105">Portal</span><span class="sxs-lookup"><span data-stu-id="03af3-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="03af3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03af3-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="03af3-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="03af3-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="03af3-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="03af3-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="03af3-109">Bu makale size nasıl toomanage hello Azure portal kullanarak DNS bölgeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="03af3-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="03af3-110">DNS bölgelerini hello platformlar arası kullanarak da yönetebilirsiniz [Azure CLI](dns-operations-dnszones-cli.md) veya Azure hello [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="03af3-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="03af3-111">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="03af3-111">Create a DNS zone</span></span>

1. <span data-ttu-id="03af3-112">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="03af3-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="03af3-113">Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.</span><span class="sxs-lookup"><span data-stu-id="03af3-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS bölgesi](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="03af3-115">Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="03af3-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="03af3-116">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="03af3-116">**Setting**</span></span> | <span data-ttu-id="03af3-117">**Değer**</span><span class="sxs-lookup"><span data-stu-id="03af3-117">**Value**</span></span> | <span data-ttu-id="03af3-118">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="03af3-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="03af3-119">**Ad**</span><span class="sxs-lookup"><span data-stu-id="03af3-119">**Name**</span></span>|<span data-ttu-id="03af3-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="03af3-120">contoso.com</span></span>|<span data-ttu-id="03af3-121">Merhaba DNS bölgesinin Hello adı</span><span class="sxs-lookup"><span data-stu-id="03af3-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="03af3-122">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="03af3-122">**Subscription**</span></span>|<span data-ttu-id="03af3-123">[Aboneliğiniz]</span><span class="sxs-lookup"><span data-stu-id="03af3-123">[Your subscription]</span></span>|<span data-ttu-id="03af3-124">Bir abonelik toocreate hello DNS bölgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="03af3-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="03af3-125">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="03af3-125">**Resource group**</span></span>|<span data-ttu-id="03af3-126">**Yeni oluştur:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="03af3-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="03af3-127">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03af3-127">Create a resource group.</span></span> <span data-ttu-id="03af3-128">Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="03af3-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="03af3-129">Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.</span><span class="sxs-lookup"><span data-stu-id="03af3-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="03af3-130">**Konum**</span><span class="sxs-lookup"><span data-stu-id="03af3-130">**Location**</span></span>|<span data-ttu-id="03af3-131">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="03af3-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="03af3-132">Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="03af3-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="03af3-133">Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="03af3-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="03af3-134">Liste DNS bölgeleri</span><span class="sxs-lookup"><span data-stu-id="03af3-134">List DNS zones</span></span>

<span data-ttu-id="03af3-135">İçinde Azure portal Merhaba, çok gidin**daha fazla hizmet** > **ağ** > **DNS bölgeleri**.</span><span class="sxs-lookup"><span data-stu-id="03af3-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="03af3-136">Her DNS bölgesinin kendi kaynağı, kayıt kümesi sayısı gibi bilgiler ve ad sunucuları bu görünümden görüntülenebilir ' dir.</span><span class="sxs-lookup"><span data-stu-id="03af3-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="03af3-137">Merhaba sütun **ad sunucuları** hello varsayılan görünüm tooadd tıklatın erişilebilir **sütunları**seçin **ad sunucuları** tıklatıp **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="03af3-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![DNS bölgelerini listeleme](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="03af3-139">Bir DNS bölgesi Sil</span><span class="sxs-lookup"><span data-stu-id="03af3-139">Delete a DNS zone</span></span>

<span data-ttu-id="03af3-140">Merhaba portal tooa DNS bölgesinde gidin.</span><span class="sxs-lookup"><span data-stu-id="03af3-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="03af3-141">Merhaba üzerinde **DNS bölgesi** dikey penceresinde tıklatın **bölgeyi Sil**.</span><span class="sxs-lookup"><span data-stu-id="03af3-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="03af3-142">İstendiğinde tooconfirm toodelete hello DNS bölgesi isteyen var.</span><span class="sxs-lookup"><span data-stu-id="03af3-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="03af3-143">Bir DNS bölgesi silme hello bölgede bulunan tüm hello kayıtlarını siler.</span><span class="sxs-lookup"><span data-stu-id="03af3-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03af3-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03af3-144">Next steps</span></span>

<span data-ttu-id="03af3-145">Bilgi nasıl DNS bölgesi ve kayıtları şu adresi ziyaret ederek toowork [Azure hello Azure portal kullanarak DNS ile çalışmaya başlama](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="03af3-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
