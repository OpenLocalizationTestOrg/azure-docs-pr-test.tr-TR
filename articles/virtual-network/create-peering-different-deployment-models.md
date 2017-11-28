---
title: "aaaCreate bir Azure sanal ağ eşleme - farklı dağıtım modellerini - aynı abonelik | Microsoft Docs"
description: "Nasıl hello aynı mevcut farklı Azure dağıtım modelleri arasında bir sanal ağ sanal ağlar arasında eşlemeyi toocreate oluşturulacağını öğrenin Azure aboneliği."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a><span data-ttu-id="dd8c0-103">Sanal Ağ eşlemesi bir - farklı oluşturmak dağıtım modelleri, aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="dd8c0-103">Create a virtual network peering - different deployment models, same subscription</span></span> 

<span data-ttu-id="dd8c0-104">Bu öğreticide, bir sanal ağ farklı dağıtım modeli oluşturulan sanal ağlar arasında eşleme toocreate öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="dd8c0-105">Her iki sanal ağlar hello aynı mevcut abonelik.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="dd8c0-106">Farklı sanal ağlar toocommunicate birbirleri ile olan eşleme iki sanal ağlar etkinleştirir kaynakları, aynı bant genişliği ve gecikme hello kaynakları hello gibi davranarak hello aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="dd8c0-107">Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="dd8c0-108">Merhaba adımları toocreate bir sanal ağ eşlemesi hello sanal ağlar aynı ya da farklı Merhaba, abonelikleri ve hangi yere bağlı olarak farklı [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sanal ağlar oluşturulur aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="dd8c0-109">Nasıl toocreate sanal bir ağ diğer senaryolarda aşağıdaki tablonun hello hello senaryodan tıklayarak eşliği öğrenin:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="dd8c0-110">Azure dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="dd8c0-110">Azure deployment model</span></span>  | <span data-ttu-id="dd8c0-111">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="dd8c0-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="dd8c0-112">Her iki kaynak yöneticisi</span><span class="sxs-lookup"><span data-stu-id="dd8c0-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="dd8c0-113">Aynı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-113">Same</span></span>|
|[<span data-ttu-id="dd8c0-114">Her iki kaynak yöneticisi</span><span class="sxs-lookup"><span data-stu-id="dd8c0-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="dd8c0-115">Farklı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-115">Different</span></span>|
|[<span data-ttu-id="dd8c0-116">Bir kaynak yöneticisi, bir Klasik</span><span class="sxs-lookup"><span data-stu-id="dd8c0-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="dd8c0-117">Farklı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-117">Different</span></span>|

<span data-ttu-id="dd8c0-118">Bir sanal ağ eşlemesi hello Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="dd8c0-119">Bir sanal ağ eşlemesi yalnızca aynı hello mevcut iki sanal ağ arasında oluşturulabilir Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="dd8c0-120">Her ikisi de oluşturulmuş hello Klasik dağıtım modeli aracılığıyla ya da farklı Azure bölgelerinde mevcut sanal ağlar tooconnect gerekiyorsa, Azure kullanabilirsiniz [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sanal ağlar.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="dd8c0-121">Merhaba kullanabilirsiniz [Azure portal](#portal), Azure hello [komut satırı arabirimi](#cli) (CLI) veya Azure [PowerShell](#powershell) toocreate bir sanal ağ eşlemesi.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) toocreate a virtual network peering.</span></span> <span data-ttu-id="dd8c0-122">Seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturmak için toohello adımları doğrudan hello önceki aracı bağlantılar toogo birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="dd8c0-123"><a name="cli"></a>Eşlemesi - oluşturmak portalı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-123"><a name="cli"></a>Create peering - Portal</span></span>

1. <span data-ttu-id="dd8c0-124">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dd8c0-125">Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="dd8c0-126">Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="dd8c0-127">Tıklatın **+ yeni**, tıklatın **ağ**, ardından **sanal ağ**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="dd8c0-128">Merhaba, **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="dd8c0-129">**Ad**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="dd8c0-130">**Adres alanı**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="dd8c0-131">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="dd8c0-132">**Alt ağ adres aralığı**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="dd8c0-133">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="dd8c0-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="dd8c0-134">**Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="dd8c0-135">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="dd8c0-136">Tıklatın **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-136">Click **+ New**.</span></span> <span data-ttu-id="dd8c0-137">Merhaba, **arama hello Market** kutusuna *sanal ağ*.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-137">In hello **Search hello Marketplace** box, type *Virtual network*.</span></span> <span data-ttu-id="dd8c0-138">Tıklatın **sanal ağ** hello arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-138">Click **Virtual network** when it appears in hello search results.</span></span> 
5. <span data-ttu-id="dd8c0-139">Merhaba, **sanal ağ** dikey penceresinde, select **Klasik** hello içinde **dağıtım modeli seçin** kutusuna ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-139">In hello **Virtual network** blade, select **Classic** in hello **Select a deployment model** box, and then click **Create**.</span></span>
6. <span data-ttu-id="dd8c0-140">Merhaba, **sanal ağ oluştur** dikey penceresinde girin veya hello ayarları aşağıdaki değerleri seçin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-140">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="dd8c0-141">**Ad**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-141">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="dd8c0-142">**Adres alanı**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-142">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="dd8c0-143">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-143">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="dd8c0-144">**Alt ağ adres aralığı**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-144">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="dd8c0-145">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="dd8c0-145">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="dd8c0-146">**Kaynak grubu**: seçin **var olanı kullan** seçip *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-146">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="dd8c0-147">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-147">**Location**: *East US*</span></span>
7. <span data-ttu-id="dd8c0-148">Merhaba, **arama kaynakları** kutusunu hello portalının türü hello üstünde *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-148">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="dd8c0-149">Tıklatın **myResourceGroup** hello arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-149">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="dd8c0-150">Merhaba bir dikey penceresi görünür **myresourcegroup** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-150">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="dd8c0-151">Merhaba kaynak grubu, önceki adımlarda oluşturduğunuz hello iki sanal ağ içeriyor.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-151">hello resource group contains hello two virtual networks created in previous steps.</span></span>
8. <span data-ttu-id="dd8c0-152">Tıklatın **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-152">Click **myVNet1**.</span></span>
9. <span data-ttu-id="dd8c0-153">Merhaba, **myVnet1** görünür, dikey tıklayın **eşlemeler** listesinden hello dikey yan hello dikey pencerenin sol hello seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-153">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
10. <span data-ttu-id="dd8c0-154">Merhaba, **myVnet1 - eşlemeler** görünen dikey tıklayın **+ Ekle**</span><span class="sxs-lookup"><span data-stu-id="dd8c0-154">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
11. <span data-ttu-id="dd8c0-155">Merhaba, **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri şu hello seçip'ı tıklatın **Tamam**:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-155">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="dd8c0-156">**Ad**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="dd8c0-156">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="dd8c0-157">**Sanal ağ dağıtım modeli**: seçin **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-157">**Virtual network deployment model**:  Select **Classic**.</span></span> 
     - <span data-ttu-id="dd8c0-158">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="dd8c0-158">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="dd8c0-159">**Sanal ağ**: tıklatın **sanal ağ seçin**, ardından **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-159">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="dd8c0-160">**Sanal ağ erişimine izin ver:** emin **etkin** seçilir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-160">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="dd8c0-161">Diğer bir ayarları, bu öğreticide kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-161">No other settings are used in this tutorial.</span></span> <span data-ttu-id="dd8c0-162">Tüm eşleme ayarları hakkında toolearn okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-162">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
12. <span data-ttu-id="dd8c0-163">' I tıklattıktan sonra **Tamam** hello önceki adımda hello **Ekle eşliği** dikey penceresi kapanır ve hello gördüğünüz **myVnet1 - eşlemeler** dikey penceresini yeniden.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-163">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="dd8c0-164">Birkaç saniye sonra oluşturduğunuz eşliği hello hello dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-164">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="dd8c0-165">**Bağlı** hello listelenen **EŞLİĞİ durumu** hello için sütun **myVnet1ToMyVnet2** sizin eşlemeyi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-165">**Connected** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span>

    <span data-ttu-id="dd8c0-166">Merhaba eşliği şimdi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-166">hello peering is now established.</span></span> <span data-ttu-id="dd8c0-167">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-167">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="dd8c0-168">Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-168">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="dd8c0-169">Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-169">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="dd8c0-170">Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-170">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
13. <span data-ttu-id="dd8c0-171">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-171">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
14. <span data-ttu-id="dd8c0-172">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları hello [silmek kaynakları](#delete-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-172">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="dd8c0-173"><a name="cli"></a>Eşlemesi - oluşturmak Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd8c0-173"><a name="cli"></a>Create peering - Azure CLI</span></span>

1. <span data-ttu-id="dd8c0-174">[Yükleme](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello sanal ağ (Klasik).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-174">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello virtual network (classic).</span></span>
2. <span data-ttu-id="dd8c0-175">Bir komut oturumu açın ve içinde tooAzure hello kullanarak oturum `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-175">Open a command session and log in tooAzure using hello `azure login` command.</span></span>
3. <span data-ttu-id="dd8c0-176">Merhaba girerek Hello CLI Hizmet Yönetimi modunda çalışacak `azure config mode asm` komutu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-176">Run hello CLI in Service Management mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="dd8c0-177">Toocreate hello sanal ağ (Klasik) komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-177">Enter hello following command toocreate hello virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. <span data-ttu-id="dd8c0-178">Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-178">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="dd8c0-179">Merhaba CLI 1.0 veya 2.0 kullanabilirsiniz ([yükleme](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-179">You can use either hello CLI 1.0 or 2.0 ([install](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span></span> <span data-ttu-id="dd8c0-180">Kullanılan toocreate hello eşliği 2.0 olması gerektiğinden bu öğreticide, hello CLI 2.0 kullanılan toocreate hello sanal (Resource Manager) ağdır.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-180">In this tutorial, hello CLI 2.0 is used toocreate hello virtual network (Resource Manager), since 2.0 must be used toocreate hello peering.</span></span> <span data-ttu-id="dd8c0-181">Aşağıdaki yerel makinenize hello CLI 2.0.4 ile CLI betikten bash veya sonraki bir sürümü yüklü hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-181">Execute hello following bash CLI script from your local machine with hello CLI 2.0.4 or later installed.</span></span> <span data-ttu-id="dd8c0-182">Windows istemcisi üzerinde CLI betikleri çalıştırma seçenekleri bash için bkz: [Windows hello Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-182">For options on running bash CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="dd8c0-183">Merhaba betik hello Azure bulut Kabuğu'nu kullanarak da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-183">You can also run hello script using hello Azure Cloud Shell.</span></span> <span data-ttu-id="dd8c0-184">Hello Azure bulut Kabuğu doğrudan hello Azure portal'içinde çalıştırabilirsiniz boş bir Bash kabuğunda ' dir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="dd8c0-185">Azure CLI yüklenmiş ve toouse hesabınız ile yapılandırılan hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="dd8c0-186">Merhaba tıklatın **deneyin** Azure hesabı düğmesini hello betikteki, oturumu bir bulut Kabuk çağırır aşağıdaki tooyour oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="dd8c0-187">tooexecute Merhaba komut dosyası, hello tıklatın **kopya** düğmesi ve yapıştırma, bulut Kabuğunuzu Merhaba içeriğine tuşuna `Enter`.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-187">tooexecute hello script, click hello **Copy** button and paste, hello contents into your Cloud Shell, then press `Enter`.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. <span data-ttu-id="dd8c0-188">Merhaba farklı dağıtım modelleri arasında oluşturulan hello iki sanal ağlar arasında eşleme sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-188">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="dd8c0-189">Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-189">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="dd8c0-190">Değiştir `<subscription id>` aboneliğinizle kimliği. Merhaba, abonelik kimliği bilmiyorsanız, girin `az account show` komutu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-190">Replace `<subscription id>` with your subscription Id. If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="dd8c0-191">Merhaba değeri **kimliği** hello çıktı, abonelik kimliği değil. Tooyour CLI oturumunda değiştiren hello betik yapıştırın ve tuşuna `Enter`.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-191">hello value for **id** in hello output is your subscription Id. Paste hello modified script in tooyour CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. <span data-ttu-id="dd8c0-192">Merhaba betik yürütüldükten sonra hello sanal ağ (Resource Manager) hello eşlemesi gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-192">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="dd8c0-193">Kopyalama hello aşağıdaki komutu, CLI oturumunuzda yapıştırın ve tuşuna `Enter`:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-193">Copy hello following command, paste it in your CLI session, and then press `Enter`:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="dd8c0-194">Merhaba çıktısını gösterir **bağlı** hello içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-194">hello output shows **Connected** in hello **PeeringState** column.</span></span> 

    <span data-ttu-id="dd8c0-195">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-195">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="dd8c0-196">Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-196">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="dd8c0-197">Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-197">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="dd8c0-198">Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-198">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
8. <span data-ttu-id="dd8c0-199">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-199">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
9. <span data-ttu-id="dd8c0-200">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-cli) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-200">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="dd8c0-201"><a name="powershell"></a>Eşlemesi - oluşturmak PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd8c0-201"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="dd8c0-202">Merhaba PowerShell Hello en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) ve [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modüller.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-202">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="dd8c0-203">Yeni tooAzure PowerShell değilseniz, bkz [Azure PowerShell genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-203">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="dd8c0-204">Bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-204">Start a PowerShell session.</span></span>
3. <span data-ttu-id="dd8c0-205">PowerShell'de tooAzure içinde hello girerek oturum `Add-AzureAccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-205">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="dd8c0-206">bir sanal ağ (Klasik) PowerShell ile toocreate, yeni bir, veya var olan değiştirmeniz gerekir ağ yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-206">toocreate a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="dd8c0-207">Nasıl çok öğrenin[dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-207">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="dd8c0-208">Merhaba dosya hello aşağıdakileri içermelidir **VirtualNetworkSite** öğesi Bu öğreticide kullanılan hello sanal ağ için:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-208">hello file should include hello following **VirtualNetworkSite** element for hello virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > <span data-ttu-id="dd8c0-209">Değiştirilen ağ yapılandırma dosyasını içeri değişiklikler tooexisting sanal ağlar (aboneliğinizde Klasik) neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-209">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="dd8c0-210">Yalnızca hello önceki sanal ağ ekleme ve yok değiştirdiğinizde veya var olan tüm sanal ağları aboneliğinizden kaldırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-210">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 
5. <span data-ttu-id="dd8c0-211">Merhaba girerek tooAzure toocreate hello sanal ağında (Resource Manager) oturum `login-azurermaccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-211">Log in tooAzure toocreate hello virtual network (Resource Manager) by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="dd8c0-212">Merhaba hesabı ile oturum, bir sanal ağ eşlemesi hello gerekli izinleri toocreate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-212">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="dd8c0-213">Merhaba bkz [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-213">See hello [Permissions](#permissions) section of this article for details.</span></span>
6. <span data-ttu-id="dd8c0-214">Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-214">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="dd8c0-215">Merhaba betiği kopyalayın, PowerShell içinde yapıştırın ve ardından basın `Enter`.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-215">Copy hello script, paste it into PowerShell, and then press `Enter`.</span></span>

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. <span data-ttu-id="dd8c0-216">Merhaba farklı dağıtım modelleri arasında oluşturulan hello iki sanal ağlar arasında eşleme sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-216">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="dd8c0-217">Komut dosyası tooa metin düzenleyicisi Bilgisayarınızda aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-217">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="dd8c0-218">Değiştir `<subscription id>` aboneliğinizle kimliği. Merhaba, abonelik kimliği bilmiyorsanız, girin `Get-AzureRmSubscription` komutu tooview onu.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-218">Replace `<subscription id>` with your subscription Id. If you don't know your subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="dd8c0-219">Merhaba değeri **kimliği** hello çıkış abonelik kimliğinizi döndürülür</span><span class="sxs-lookup"><span data-stu-id="dd8c0-219">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="dd8c0-220">tooexecute hello komut dosyası, kopyalama hello değiştiren komut dosyasından metin düzenleyici, PowerShell oturumunuzda sağ tıklayın ve sonra basın `Enter`.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-220">tooexecute hello script, copy hello modified script from your text editor, then right-click in your PowerShell session, and then press `Enter`.</span></span>

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. <span data-ttu-id="dd8c0-221">Merhaba betik yürütüldükten sonra hello sanal ağ (Resource Manager) hello eşlemesi gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-221">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="dd8c0-222">Kopyalama hello aşağıdaki komut, PowerShell oturumunuzda yapıştırın ve tuşuna `Enter`:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-222">Copy hello following command, paste it in your PowerShell session, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="dd8c0-223">Merhaba çıktısını gösterir **bağlı** hello içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-223">hello output shows **Connected** in hello **PeeringState** column.</span></span>

    <span data-ttu-id="dd8c0-224">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini aracılığıyla birbirleriyle mümkün toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-224">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="dd8c0-225">Varsayılan Azure ad çözümlemesi için sanal ağlar hello kullanıyorsanız hello hello sanal ağlarda değil mümkün tooresolve adları hello sanal ağlar arasında kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-225">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="dd8c0-226">Bir eşlemesindeki sanal ağlar arasında tooresolve adlarının istiyorsanız, DNS sunucunuzun oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-226">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="dd8c0-227">Bilgi nasıl yukarı tooset [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-227">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

9. <span data-ttu-id="dd8c0-228">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan de, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makine toohello diğer toovalidate bağlantı bağlanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-228">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
10. <span data-ttu-id="dd8c0-229">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz toodelete hello kaynakları, tam hello adımları [silmek kaynakları](#delete-powershell) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-229">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>
 
## <span data-ttu-id="dd8c0-230"><a name="permissions"></a>İzinleri</span><span class="sxs-lookup"><span data-stu-id="dd8c0-230"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="dd8c0-231">bir sanal ağ eşlemesi toocreate kullandığınız hello hesaplarının hello gerekli rol veya izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-231">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="dd8c0-232">Örneğin, myVnet1 ve myVnet2 adlı iki sanal ağ eşlemesi, hesabınızı en az bir rol veya her sanal ağ izinlerini aşağıdaki hello atanması gerekir:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-232">For example, if you were peering two virtual networks named myVnet1 and myVnet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="dd8c0-233">Sanal ağ</span><span class="sxs-lookup"><span data-stu-id="dd8c0-233">Virtual network</span></span>|<span data-ttu-id="dd8c0-234">Dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="dd8c0-234">Deployment model</span></span>|<span data-ttu-id="dd8c0-235">Rol</span><span class="sxs-lookup"><span data-stu-id="dd8c0-235">Role</span></span>|<span data-ttu-id="dd8c0-236">İzinler</span><span class="sxs-lookup"><span data-stu-id="dd8c0-236">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="dd8c0-237">myVnet1</span><span class="sxs-lookup"><span data-stu-id="dd8c0-237">myVnet1</span></span>|<span data-ttu-id="dd8c0-238">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd8c0-238">Resource Manager</span></span>|[<span data-ttu-id="dd8c0-239">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-239">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="dd8c0-240">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="dd8c0-240">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="dd8c0-241">Klasik</span><span class="sxs-lookup"><span data-stu-id="dd8c0-241">Classic</span></span>|[<span data-ttu-id="dd8c0-242">Klasik Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-242">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="dd8c0-243">Yok</span><span class="sxs-lookup"><span data-stu-id="dd8c0-243">N/A</span></span>|
|<span data-ttu-id="dd8c0-244">myVnet2</span><span class="sxs-lookup"><span data-stu-id="dd8c0-244">myVnet2</span></span>|<span data-ttu-id="dd8c0-245">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd8c0-245">Resource Manager</span></span>|[<span data-ttu-id="dd8c0-246">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-246">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="dd8c0-247">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="dd8c0-247">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="dd8c0-248">Klasik</span><span class="sxs-lookup"><span data-stu-id="dd8c0-248">Classic</span></span>|[<span data-ttu-id="dd8c0-249">Klasik Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-249">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="dd8c0-250">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="dd8c0-250">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="dd8c0-251">Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve özel izinleri çok atama[özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-251">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="dd8c0-252"><a name="delete"></a>Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="dd8c0-252"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="dd8c0-253">Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz hello öğreticide oluşturulan toodelete hello kaynakları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-253">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="dd8c0-254">Bir kaynak grubunu silme hello kaynak grubunda bulunan tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-254">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="dd8c0-255"><a name="delete-portal"></a>Azure portalı</span><span class="sxs-lookup"><span data-stu-id="dd8c0-255"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="dd8c0-256">Merhaba portal arama kutusuna **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-256">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="dd8c0-257">Merhaba arama sonuçlarında tıklatın **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-257">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="dd8c0-258">Merhaba üzerinde **myResourceGroup** dikey penceresinde hello tıklatın **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-258">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="dd8c0-259">Merhaba de tooconfirm hello silinmesine **türü hello kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-259">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="dd8c0-260"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dd8c0-260"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="dd8c0-261">Hello Azure CLI 2.0 toodelete hello sanal ağ (Resource Manager) komutu aşağıdaki hello ile kullanın:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-261">Use hello Azure CLI 2.0 toodelete hello virtual network (Resource Manager) with hello following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. <span data-ttu-id="dd8c0-262">Hello Azure CLI 1.0 toodelete hello sanal ağ (Klasik) ile Merhaba aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-262">Use hello Azure CLI 1.0 toodelete hello virtual network (classic) with hello following commands:</span></span>

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <span data-ttu-id="dd8c0-263"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd8c0-263"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="dd8c0-264">Toodelete hello sanal ağ (Resource Manager) komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-264">Enter hello following command toodelete hello virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. <span data-ttu-id="dd8c0-265">toodelete hello sanal ağ (Klasik) PowerShell ile varolan bir ağ yapılandırma dosyasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-265">toodelete hello virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="dd8c0-266">Nasıl çok öğrenin[dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-266">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="dd8c0-267">Bu öğreticide kullanılan hello sanal ağ için VirtualNetworkSite öğesi aşağıdaki hello kaldırın:</span><span class="sxs-lookup"><span data-stu-id="dd8c0-267">Remove hello following VirtualNetworkSite element for hello virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > <span data-ttu-id="dd8c0-268">Değiştirilen ağ yapılandırma dosyasını içeri değişiklikler tooexisting sanal ağlar (aboneliğinizde Klasik) neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-268">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="dd8c0-269">Yalnızca hello önceki sanal ağı kaldırmak ve yok değiştirdiğinizde veya diğer varolan sanal ağlara aboneliğinizden kaldırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-269">Ensure you only remove hello previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dd8c0-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd8c0-270">Next steps</span></span>

- <span data-ttu-id="dd8c0-271">Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-271">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="dd8c0-272">Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="dd8c0-272">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="dd8c0-273">Nasıl çok öğrenin[bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.</span><span class="sxs-lookup"><span data-stu-id="dd8c0-273">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
