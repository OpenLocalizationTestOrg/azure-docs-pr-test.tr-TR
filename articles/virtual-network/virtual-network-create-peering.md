---
title: "Azure sanal ağ eşlemesi bir - aaaCreate Resource Manager - aynı abonelik | Microsoft Docs"
description: "Nasıl Resource Manager aracılığıyla aynı hello mevcut bir sanal ağ sanal ağlar arasında eşlemeyi toocreate oluşturulacağını öğrenin Azure aboneliği."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="cc2e1-103">Bir sanal ağ eşlemesi - oluşturmak Resource Manager, aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="cc2e1-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="cc2e1-104">Bu öğreticide, bir sanal ağ Resource Manager aracılığıyla oluşturulan sanal ağlar arasında eşleme toocreate öğrenin.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="cc2e1-105">Her iki sanal ağlar hello aynı mevcut abonelik.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="cc2e1-106">Farklı sanal ağlar toocommunicate birbirleri ile olan eşleme iki sanal ağlar etkinleştirir kaynakları, aynı bant genişliği ve gecikme hello kaynakları hello gibi davranarak hello aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="cc2e1-107">Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="cc2e1-108">Merhaba adımları toocreate bir sanal ağ eşlemesi hello sanal ağlar aynı ya da farklı Merhaba, abonelikleri ve hangi yere bağlı olarak farklı [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar oluşturulur aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="cc2e1-109">Nasıl toocreate sanal bir ağ diğer senaryolarda aşağıdaki tablonun hello hello senaryodan tıklayarak eşliği öğrenin:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="cc2e1-110">Azure dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="cc2e1-110">Azure deployment model</span></span>  | <span data-ttu-id="cc2e1-111">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="cc2e1-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="cc2e1-112">Her iki kaynak yöneticisi</span><span class="sxs-lookup"><span data-stu-id="cc2e1-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="cc2e1-113">Farklı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-113">Different</span></span>|
|[<span data-ttu-id="cc2e1-114">Bir kaynak yöneticisi, bir Klasik</span><span class="sxs-lookup"><span data-stu-id="cc2e1-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="cc2e1-115">Aynı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-115">Same</span></span>|
|[<span data-ttu-id="cc2e1-116">Bir kaynak yöneticisi, bir Klasik</span><span class="sxs-lookup"><span data-stu-id="cc2e1-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="cc2e1-117">Farklı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-117">Different</span></span>|

<span data-ttu-id="cc2e1-118">Bir sanal ağ eşlemesi hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="cc2e1-119">Bir sanal ağ eşlemesi yalnızca aynı hello mevcut iki sanal ağ arasında oluşturulabilir Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="cc2e1-120">Her ikisi de oluşturulmuş hello Klasik dağıtım modeli aracılığıyla ya da farklı Azure bölgelerinde mevcut sanal ağlar tooconnect gerekiyorsa, Azure kullanabilirsiniz [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sanal ağlar.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="cc2e1-121">Merhaba kullanabilirsiniz [Azure portal](#portal), Azure hello [komut satırı arabirimi](#cli) (CLI) Azure [PowerShell](#powershell), veya bir [Azure Resource Manager şablonu](#template) toocreate bir sanal ağ eşlemesi.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="cc2e1-122">Seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturmak için toohello adımları doğrudan hello önceki aracı bağlantılar toogo birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="cc2e1-123"><a name="portal"></a>Eşlemesi - oluşturmak Azure portalı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="cc2e1-124">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="cc2e1-125">Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="cc2e1-126">Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="cc2e1-127">Tıklatın **+ yeni**, tıklatın **ağ**, ardından **sanal ağ**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="cc2e1-128">Merhaba, **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="cc2e1-129">**Ad**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="cc2e1-130">**Adres alanı**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="cc2e1-131">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="cc2e1-132">**Alt ağ adres aralığı**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="cc2e1-133">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="cc2e1-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="cc2e1-134">**Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="cc2e1-135">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="cc2e1-136">Adım 2-3 yeniden değerleri adım 3'te aşağıdaki hello belirtme tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="cc2e1-137">**Ad**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="cc2e1-138">**Adres alanı**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="cc2e1-139">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="cc2e1-140">**Alt ağ adres aralığı**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="cc2e1-141">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="cc2e1-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="cc2e1-142">**Kaynak grubu**: seçin **var olanı kullan** seçip *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="cc2e1-143">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="cc2e1-144">Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="cc2e1-145">Tıklatın **myResourceGroup** hello arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="cc2e1-146">Merhaba bir dikey penceresi görünür **myresourcegroup** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="cc2e1-147">Merhaba kaynak grubu, önceki adımlarda oluşturduğunuz hello iki sanal ağ içeriyor.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="cc2e1-148">Tıklatın **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="cc2e1-149">Merhaba, **myVnet1** görünür, dikey tıklayın **eşlemeler** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="cc2e1-150">Merhaba, **myVnet1 - eşlemeler** görünen dikey tıklayın **+ Ekle**</span><span class="sxs-lookup"><span data-stu-id="cc2e1-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="cc2e1-151">Merhaba, **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri şu hello seçip'ı tıklatın **Tamam**:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="cc2e1-152">**Ad**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="cc2e1-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="cc2e1-153">**Sanal ağ dağıtım modeli**: seçin **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="cc2e1-154">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="cc2e1-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="cc2e1-155">**Sanal ağ**: tıklatın **sanal ağ seçin**, ardından **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="cc2e1-156">**Sanal ağ erişimine izin ver:** emin **etkin** seçilir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="cc2e1-157">Diğer bir ayarları, bu öğreticide kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="cc2e1-158">Tüm eşleme ayarları hakkında toolearn okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="cc2e1-159">' I tıklattıktan sonra **Tamam** hello önceki adımda hello **Ekle eşliği** dikey penceresi kapanır ve hello gördüğünüz **myVnet1 - eşlemeler** dikey penceresini yeniden.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="cc2e1-160">Birkaç saniye sonra oluşturduğunuz eşliği hello hello dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="cc2e1-161">**Başlatılan** hello listelenen **EŞLİĞİ durumu** hello için sütun **myVnet1ToMyVnet2** sizin eşlemeyi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="cc2e1-162">Vnet1 tooVnet2 eşlenen, ancak şimdi myVnet2 toomyVnet1 eş gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="cc2e1-163">Merhaba eşliği her iki yönde de hello sanal ağlar toocommunicate tooenable kaynaklarında birbirleri ile oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="cc2e1-164">Yeniden myVnet2 için 5-10 adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="cc2e1-165">Merhaba ad eşlemesi *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="cc2e1-166">' I tıklattıktan sonra birkaç saniye **Tamam** toocreate hello MyVnet2 için hello eşliği **myVnet2ToMyVnet1** , yeni oluşturduğunuz eşliği ile listelendiğini **bağlı** hello içinde **Eşleme durumu** sütun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="cc2e1-167">Adım 5-7 MyVnet1 için yeniden tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="cc2e1-168">Merhaba **EŞLİĞİ durumu** hello için **myVnet1ToVNet2** eşliği olan şimdi de **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="cc2e1-169">Merhaba eşliği başarıyla kuruldu gördükten sonra **bağlı** hello içinde **EŞLİĞİ durum** hello eşlemesindeki her iki sanal ağlar için sütun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="cc2e1-170">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="cc2e1-171">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="cc2e1-172">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="cc2e1-173">Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="cc2e1-174">Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="cc2e1-175">Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="cc2e1-176"><a name="cli"></a>Eşlemesi - oluşturmak Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cc2e1-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="cc2e1-177">komut dosyası izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-177">hello following script:</span></span>

- <span data-ttu-id="cc2e1-178">Hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cc2e1-179">Merhaba çalıştırmak toofind hello sürüm `az --version` komutu.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="cc2e1-180">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="cc2e1-181">Bir Bash kabuğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-181">Works in a Bash shell.</span></span> <span data-ttu-id="cc2e1-182">Windows istemcisi üzerinde Azure CLI betikleri çalıştırma seçenekleri için bkz [Windows hello Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="cc2e1-183">Merhaba CLI ve bağımlılıklarını yüklemek yerine, hello Azure bulut Kabuk kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="cc2e1-184">Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="cc2e1-185">Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="cc2e1-186">Merhaba tıklatın **deneyin** Azure hesabı düğmesini hello betikteki, oturumu bir bulut Kabuk çağırır aşağıdaki tooyour oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="cc2e1-187">tooexecute Merhaba komut dosyası, hello tıklatın **kopyalama** düğmesine tıklayın ve bulut kabuğundan hello içeriğini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="cc2e1-188">Bir kaynak grubu ve iki sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="cc2e1-189">Merhaba iki sanal ağlar arasında eşlemeyi bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="cc2e1-190">Merhaba betiği çalıştırdıktan sonra her bir sanal ağ hello eşlemeleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="cc2e1-191">Değiştirme Hello önceki komutu yeniden çalıştırın *myVnet1* ile *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="cc2e1-192">her ikisi de Hello çıktısını gösterir komutları **bağlı** hello içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="cc2e1-193">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="cc2e1-194">Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="cc2e1-195">Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="cc2e1-196">Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="cc2e1-197">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="cc2e1-198">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="cc2e1-199"><a name="powershell"></a>Eşlemesi - oluşturmak PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc2e1-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="cc2e1-200">Merhaba PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="cc2e1-201">Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="cc2e1-202">bir PowerShell oturumu toostart Git çok**Başlat**, girin **powershell**ve ardından **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="cc2e1-203">PowerShell'de tooAzure içinde hello girerek oturum `login-azurermaccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="cc2e1-204">Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="cc2e1-205">Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="cc2e1-206">Bir kaynak grubu ve iki sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="cc2e1-207">tooexecute hello komut dosyası, kopyalama hello aşağıdaki komut, PowerShell içinde yapıştırın ve tuşuna basarak `Enter` hello son satırında Merhaba ekranında göründükten sonra:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="cc2e1-208">Merhaba iki sanal ağlar arasında eşlemeyi bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="cc2e1-209">Kopya hello aşağıdaki komut, tooPowerShell içinde yapıştırın ve tuşuna basarak `Enter` hello son satırında Merhaba ekranında göründükten sonra:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="cc2e1-210">tooreview hello hello sanal ağ alt ağları, kopyalama hello aşağıdaki komutu, içinde tooPowerShell yapıştırın ve tuşuna basın `Enter`:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="cc2e1-211">Değiştirme Hello önceki komutu yeniden çalıştırın *myVnet1* ile *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="cc2e1-212">her ikisi de Hello çıktısını gösterir komutları **bağlı** hello içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="cc2e1-213">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="cc2e1-214">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="cc2e1-215">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="cc2e1-216">Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="cc2e1-217">Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="cc2e1-218">Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="cc2e1-219"><a name="template"></a>Eşlemesi - oluşturmak Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="cc2e1-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="cc2e1-220">Başvuru [bir sanal ağ eşlemesi oluşturma](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="cc2e1-221">Merhaba şablonu dağıtmak için hello şablonuyla kullanarak hello Azure portal, PowerShell veya Azure CLI hello yönergeler sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="cc2e1-222">Günlük toodeploy hello şablonla, sahip bir hesap kullanarak seçtiğiniz toowhichever aracında bir sanal ağ eşlemesi gerekli izinleri toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="cc2e1-223">Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="cc2e1-224">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="cc2e1-225">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete) kullanarak, bu makalenin bölümüne hello Azure portal, PowerShell veya Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="cc2e1-226"><a name="permissions"></a>İzinleri</span><span class="sxs-lookup"><span data-stu-id="cc2e1-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="cc2e1-227">bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="cc2e1-228">Örneğin, VNet1 ve VNet2 adlı iki sanal ağ eşlemesi, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="cc2e1-229">Sanal ağ</span><span class="sxs-lookup"><span data-stu-id="cc2e1-229">Virtual network</span></span>|<span data-ttu-id="cc2e1-230">Rol</span><span class="sxs-lookup"><span data-stu-id="cc2e1-230">Role</span></span>|<span data-ttu-id="cc2e1-231">İzinler</span><span class="sxs-lookup"><span data-stu-id="cc2e1-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="cc2e1-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="cc2e1-232">VNet1</span></span>|[<span data-ttu-id="cc2e1-233">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="cc2e1-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="cc2e1-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="cc2e1-235">Vnet2'ye</span><span class="sxs-lookup"><span data-stu-id="cc2e1-235">VNet2</span></span>|[<span data-ttu-id="cc2e1-236">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="cc2e1-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="cc2e1-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="cc2e1-238">Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="cc2e1-239"><a name="delete"></a>Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="cc2e1-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="cc2e1-240">Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz hello öğreticide oluşturulan toodelete hello kaynakları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="cc2e1-241">Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="cc2e1-242"><a name="delete-portal"></a>Azure portalı</span><span class="sxs-lookup"><span data-stu-id="cc2e1-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="cc2e1-243">Merhaba portal arama kutusuna **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="cc2e1-244">Merhaba arama sonuçlarında tıklatın **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="cc2e1-245">Merhaba üzerinde **myResourceGroup** dikey penceresinde hello tıklatın **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="cc2e1-246">Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="cc2e1-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cc2e1-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="cc2e1-248">Merhaba aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="cc2e1-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc2e1-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="cc2e1-250">Merhaba aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="cc2e1-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="cc2e1-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc2e1-251">Next steps</span></span>

- <span data-ttu-id="cc2e1-252">Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="cc2e1-253">Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="cc2e1-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="cc2e1-254">Nasıl çok öğrenin[bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.</span><span class="sxs-lookup"><span data-stu-id="cc2e1-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
