---
title: "Bir Azure sanal ağı - farklı dağıtım modellerini - eşlemesi oluşturmak aynı abonelik | Microsoft Docs"
description: "Aynı Azure aboneliğindeki mevcut farklı Azure dağıtım modelleri aracılığıyla oluşturulan sanal ağlar arasında eşleme sanal ağ oluşturmayı öğrenin."
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
ms.openlocfilehash: 7d75d85863ce4b06ef1f552e0d583dec302f7ace
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a><span data-ttu-id="1c591-103">Sanal Ağ eşlemesi bir - farklı oluşturmak dağıtım modelleri, aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="1c591-103">Create a virtual network peering - different deployment models, same subscription</span></span> 

<span data-ttu-id="1c591-104">Bu öğreticide, farklı dağıtım modeli oluşturulan sanal ağlar arasında eşleme sanal ağ oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1c591-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="1c591-105">Her iki sanal ağlar aynı abonelikte yok.</span><span class="sxs-lookup"><span data-stu-id="1c591-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="1c591-106">Kaynaklar aynı sanal ağda gibi davranarak birbirleri ile aynı bant genişliği ve gecikme süresi ile iletişim kurmak için farklı sanal ağlar iki sanal ağlar etkinleştirir kaynaklarında eşleme.</span><span class="sxs-lookup"><span data-stu-id="1c591-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="1c591-107">Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c591-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="1c591-108">Sanal ağlar aynı ya da farklı olup, abonelikleri ve hangi bağlı olarak farklı bir sanal ağ eşlemesi oluşturmak için aşağıdaki adımları [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal ağlar üzerinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1c591-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="1c591-109">Aşağıdaki tabloda senaryodan tıklayarak diğer senaryolarda eşliği bir sanal ağ oluşturmayı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="1c591-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="1c591-110">Azure dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="1c591-110">Azure deployment model</span></span>  | <span data-ttu-id="1c591-111">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="1c591-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="1c591-112">Her iki kaynak yöneticisi</span><span class="sxs-lookup"><span data-stu-id="1c591-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="1c591-113">Aynı</span><span class="sxs-lookup"><span data-stu-id="1c591-113">Same</span></span>|
|[<span data-ttu-id="1c591-114">Her iki kaynak yöneticisi</span><span class="sxs-lookup"><span data-stu-id="1c591-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="1c591-115">Farklı</span><span class="sxs-lookup"><span data-stu-id="1c591-115">Different</span></span>|
|[<span data-ttu-id="1c591-116">Bir kaynak yöneticisi, bir Klasik</span><span class="sxs-lookup"><span data-stu-id="1c591-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="1c591-117">Farklı</span><span class="sxs-lookup"><span data-stu-id="1c591-117">Different</span></span>|

<span data-ttu-id="1c591-118">Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında bir sanal ağ eşlemesi oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="1c591-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="1c591-119">Bir sanal ağ eşlemesi yalnızca aynı Azure bölgesinde mevcut iki sanal ağ arasında oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="1c591-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="1c591-120">Her ikisi de oluşturulmuş Klasik dağıtım modeli aracılığıyla ya da farklı Azure bölgelerinde mevcut sanal ağlara bağlanmak gerekiyorsa, Azure kullanabilirsiniz [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal ağlara bağlanma.</span><span class="sxs-lookup"><span data-stu-id="1c591-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="1c591-121">Kullanabileceğiniz [Azure portal](#portal), Azure [komut satırı arabirimi](#cli) (CLI) veya Azure [PowerShell](#powershell) bir sanal ağ eşlemesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1c591-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) to create a virtual network peering.</span></span> <span data-ttu-id="1c591-122">Doğrudan seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturma adımlarını gitmek için önceki aracı bağlantılardan herhangi birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1c591-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="1c591-123"><a name="cli"></a>Eşlemesi - oluşturmak portalı</span><span class="sxs-lookup"><span data-stu-id="1c591-123"><a name="cli"></a>Create peering - Portal</span></span>

1. <span data-ttu-id="1c591-124">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1c591-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1c591-125">İle oturum için kullandığınız hesabın, bir sanal ağ eşlemesi oluşturmak için gerekli izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c591-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="1c591-126">Bkz: [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="1c591-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="1c591-127">Tıklatın **+ yeni**, tıklatın **ağ**, ardından **sanal ağ**.</span><span class="sxs-lookup"><span data-stu-id="1c591-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="1c591-128">İçinde **sanal ağ oluştur** dikey penceresinde girin veya aşağıdaki ayarları için değerleri seçin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="1c591-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="1c591-129">**Ad**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="1c591-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="1c591-130">**Adres alanı**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="1c591-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="1c591-131">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="1c591-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="1c591-132">**Alt ağ adres aralığı**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="1c591-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="1c591-133">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="1c591-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="1c591-134">**Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="1c591-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="1c591-135">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="1c591-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="1c591-136">Tıklatın **+ yeni**.</span><span class="sxs-lookup"><span data-stu-id="1c591-136">Click **+ New**.</span></span> <span data-ttu-id="1c591-137">İçinde **Market arama** kutusuna *sanal ağ*.</span><span class="sxs-lookup"><span data-stu-id="1c591-137">In the **Search the Marketplace** box, type *Virtual network*.</span></span> <span data-ttu-id="1c591-138">Tıklatın **sanal ağ** arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="1c591-138">Click **Virtual network** when it appears in the search results.</span></span> 
5. <span data-ttu-id="1c591-139">İçinde **sanal ağ** dikey penceresinde, select **Klasik** içinde **dağıtım modeli seçin** kutusuna ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1c591-139">In the **Virtual network** blade, select **Classic** in the **Select a deployment model** box, and then click **Create**.</span></span>
6. <span data-ttu-id="1c591-140">İçinde **sanal ağ oluştur** dikey penceresinde girin veya aşağıdaki ayarları için değerleri seçin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="1c591-140">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="1c591-141">**Ad**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="1c591-141">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="1c591-142">**Adres alanı**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="1c591-142">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="1c591-143">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="1c591-143">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="1c591-144">**Alt ağ adres aralığı**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="1c591-144">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="1c591-145">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="1c591-145">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="1c591-146">**Kaynak grubu**: seçin **var olanı kullan** seçip *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="1c591-146">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="1c591-147">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="1c591-147">**Location**: *East US*</span></span>
7. <span data-ttu-id="1c591-148">İçinde **arama kaynakları** kutusunu türü portalı üstündeki *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1c591-148">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="1c591-149">Tıklatın **myResourceGroup** arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="1c591-149">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="1c591-150">Bir dikey pencere görünür **myresourcegroup** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1c591-150">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="1c591-151">Kaynak grubu, önceki adımlarda oluşturduğunuz iki sanal ağ içeriyor.</span><span class="sxs-lookup"><span data-stu-id="1c591-151">The resource group contains the two virtual networks created in previous steps.</span></span>
8. <span data-ttu-id="1c591-152">Tıklatın **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="1c591-152">Click **myVNet1**.</span></span>
9. <span data-ttu-id="1c591-153">İçinde **myVnet1** görünür, dikey tıklayın **eşlemeler** dikey pencerenin sol tarafındaki seçenekleri dikey listesinden.</span><span class="sxs-lookup"><span data-stu-id="1c591-153">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
10. <span data-ttu-id="1c591-154">İçinde **myVnet1 - eşlemeler** görünen dikey tıklayın **+ Ekle**</span><span class="sxs-lookup"><span data-stu-id="1c591-154">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
11. <span data-ttu-id="1c591-155">İçinde **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri belirleyin ve ardından **Tamam**:</span><span class="sxs-lookup"><span data-stu-id="1c591-155">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="1c591-156">**Ad**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="1c591-156">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="1c591-157">**Sanal ağ dağıtım modeli**: seçin **Klasik**.</span><span class="sxs-lookup"><span data-stu-id="1c591-157">**Virtual network deployment model**:  Select **Classic**.</span></span> 
     - <span data-ttu-id="1c591-158">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="1c591-158">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="1c591-159">**Sanal ağ**: tıklatın **sanal ağ seçin**, ardından **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="1c591-159">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="1c591-160">**Sanal ağ erişimine izin ver:** emin **etkin** seçilir.</span><span class="sxs-lookup"><span data-stu-id="1c591-160">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="1c591-161">Diğer bir ayarları, bu öğreticide kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c591-161">No other settings are used in this tutorial.</span></span> <span data-ttu-id="1c591-162">Tüm eşleme ayarları hakkında bilgi için okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="1c591-162">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
12. <span data-ttu-id="1c591-163">' I tıklattıktan sonra **Tamam** önceki adımda **Ekle eşliği** dikey penceresi kapanır ve gördüğünüz **myVnet1 - eşlemeler** dikey penceresini yeniden.</span><span class="sxs-lookup"><span data-stu-id="1c591-163">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="1c591-164">Birkaç saniye sonra oluşturduğunuz eşliği dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1c591-164">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="1c591-165">**Bağlı** içinde listelenen **EŞLİĞİ durumu** sütunu için **myVnet1ToMyVnet2** sizin eşlemeyi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1c591-165">**Connected** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span>

    <span data-ttu-id="1c591-166">Eşlemeyi şimdi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1c591-166">The peering is now established.</span></span> <span data-ttu-id="1c591-167">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini birbirleri ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="1c591-167">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="1c591-168">Varsayılan Azure ad çözümlemesi için sanal ağlar kullanıyorsanız, sanal ağlarda bulunan kaynaklar sanal ağlar arasında adlarını çözmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="1c591-168">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="1c591-169">Bir eşlemesindeki sanal ağlar arasında adları çözümlemek dilerseniz kendi DNS sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c591-169">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1c591-170">Nasıl ayarlanacağını öğrenin [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1c591-170">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
13. <span data-ttu-id="1c591-171">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1c591-171">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
14. <span data-ttu-id="1c591-172">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="1c591-172">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="1c591-173"><a name="cli"></a>Eşlemesi - oluşturmak Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1c591-173"><a name="cli"></a>Create peering - Azure CLI</span></span>

1. <span data-ttu-id="1c591-174">[Yükleme](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal ağ (Klasik) oluşturmak için Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1c591-174">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the Azure CLI 1.0 to create the virtual network (classic).</span></span>
2. <span data-ttu-id="1c591-175">Bir komut oturumu açın ve oturum açma Azure kullanmaya `azure login` komutu.</span><span class="sxs-lookup"><span data-stu-id="1c591-175">Open a command session and log in to Azure using the `azure login` command.</span></span>
3. <span data-ttu-id="1c591-176">CLI girerek Hizmet Yönetimi modunda çalışacak `azure config mode asm` komutu.</span><span class="sxs-lookup"><span data-stu-id="1c591-176">Run the CLI in Service Management mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="1c591-177">Sanal ağ (Klasik) oluşturmak için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="1c591-177">Enter the following command to create the virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. <span data-ttu-id="1c591-178">Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c591-178">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="1c591-179">CLI 1.0 veya 2.0 kullanabilirsiniz ([yükleme](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="1c591-179">You can use either the CLI 1.0 or 2.0 ([install](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span></span> <span data-ttu-id="1c591-180">Bu öğreticide, CLI 2.0 2.0 eşlemesi oluşturmak için kullanılması gereken bu yana (Resource Manager) sanal ağ oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1c591-180">In this tutorial, the CLI 2.0 is used to create the virtual network (Resource Manager), since 2.0 must be used to create the peering.</span></span> <span data-ttu-id="1c591-181">CLI 2.0.4 CLI ile yerel makineniz betikten veya üstü yüklü aşağıdaki bash yürütün.</span><span class="sxs-lookup"><span data-stu-id="1c591-181">Execute the following bash CLI script from your local machine with the CLI 2.0.4 or later installed.</span></span> <span data-ttu-id="1c591-182">Windows istemcisi üzerinde CLI betikleri çalıştırma seçenekleri bash için bkz: [Windows Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c591-182">For options on running bash CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="1c591-183">Azure bulut Kabuğu'nu kullanarak betik de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c591-183">You can also run the script using the Azure Cloud Shell.</span></span> <span data-ttu-id="1c591-184">Azure Cloud Shell doğrudan Azure portalının içinde çalıştırabileceğiniz ücretsiz bir Bash kabuğudur.</span><span class="sxs-lookup"><span data-stu-id="1c591-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="1c591-185">Azure CLI, kabuğa önceden yüklenmiştir ve kabuk, hesabınızla birlikte kullanılacak şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c591-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="1c591-186">Tıklatın **deneyin** , oturumu bir bulut Kabuk çağırır aşağıdaki Azure hesabınızla oturum açabildiğinizden komut düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1c591-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="1c591-187">Betik yürütmek için tıklatın **kopya** düğmesi ve yapıştırma, bulut Kabuğunuzu içeriğine tuşuna `Enter`.</span><span class="sxs-lookup"><span data-stu-id="1c591-187">To execute the script, click the **Copy** button and paste, the contents into your Cloud Shell, then press `Enter`.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create the virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. <span data-ttu-id="1c591-188">Farklı dağıtım modelleri arasında oluşturulan iki sanal ağlar arasında eşleme sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c591-188">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="1c591-189">Aşağıdaki komut dosyası, bilgisayarınızdaki bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1c591-189">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="1c591-190">Değiştir `<subscription id>` aboneliğinizle kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c591-190">Replace `<subscription id>` with your subscription Id.</span></span> <span data-ttu-id="1c591-191">Aboneliğinizi kimliği bilmiyorsanız, girin `az account show` komutu.</span><span class="sxs-lookup"><span data-stu-id="1c591-191">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="1c591-192">Değeri **kimliği** çıktıda, abonelik kimliği olan</span><span class="sxs-lookup"><span data-stu-id="1c591-192">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="1c591-193">CLI oturumunuz için değiştirilmiş betik yapıştırın ve sonra basın `Enter`.</span><span class="sxs-lookup"><span data-stu-id="1c591-193">Paste the modified script in to your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. <span data-ttu-id="1c591-194">Betiği çalıştırdıktan sonra sanal ağ (Resource Manager) için eşleme gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1c591-194">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="1c591-195">Aşağıdaki komutu kopyalayın, CLI oturumunuzda yapıştırın ve ardından basın `Enter`:</span><span class="sxs-lookup"><span data-stu-id="1c591-195">Copy the following command, paste it in your CLI session, and then press `Enter`:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="1c591-196">Çıktısında **bağlı** içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="1c591-196">The output shows **Connected** in the **PeeringState** column.</span></span> 

    <span data-ttu-id="1c591-197">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini birbirleri ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="1c591-197">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="1c591-198">Varsayılan Azure ad çözümlemesi için sanal ağlar kullanıyorsanız, sanal ağlarda bulunan kaynaklar sanal ağlar arasında adlarını çözmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="1c591-198">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="1c591-199">Bir eşlemesindeki sanal ağlar arasında adları çözümlemek dilerseniz kendi DNS sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c591-199">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1c591-200">Nasıl ayarlanacağını öğrenin [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1c591-200">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
8. <span data-ttu-id="1c591-201">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1c591-201">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
9. <span data-ttu-id="1c591-202">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete-cli) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="1c591-202">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="1c591-203"><a name="powershell"></a>Eşlemesi - oluşturmak PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c591-203"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="1c591-204">PowerShell'ın en son sürümünü yüklemek [Azure](https://www.powershellgallery.com/packages/Azure) ve [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modüller.</span><span class="sxs-lookup"><span data-stu-id="1c591-204">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="1c591-205">Azure PowerShell'i kullanmaya yeni başladıysanız [Azure PowerShell'e genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) sayfasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="1c591-205">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="1c591-206">Bir PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="1c591-206">Start a PowerShell session.</span></span>
3. <span data-ttu-id="1c591-207">PowerShell'de `Add-AzureAccount` komutunu girerek Azure oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="1c591-207">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="1c591-208">PowerShell ile bir sanal ağ (Klasik) oluşturmak için yeni bir oluşturun veya varolan, bir ağ yapılandırma dosyasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c591-208">To create a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="1c591-209">Bilgi edinmek için nasıl [dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="1c591-209">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="1c591-210">Dosya aşağıdaki içermelidir **VirtualNetworkSite** öğesi Bu öğreticide kullanılan sanal ağ için:</span><span class="sxs-lookup"><span data-stu-id="1c591-210">The file should include the following **VirtualNetworkSite** element for the virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="1c591-211">Değiştirilen ağ yapılandırma dosyasını içeri varolan sanal ağlar (aboneliğinizde Klasik) yapılan değişiklikler neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c591-211">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="1c591-212">Yalnızca önceki sanal ağ ekleyin ve verme değiştirir veya var olan tüm sanal ağları aboneliğinizden kaldırırsanız, emin olun.</span><span class="sxs-lookup"><span data-stu-id="1c591-212">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 
5. <span data-ttu-id="1c591-213">Oturum açtığınızda girerek (Resource Manager) sanal ağ oluşturmak için Azure `login-azurermaccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="1c591-213">Log in to Azure to create the virtual network (Resource Manager) by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="1c591-214">İle oturum için kullandığınız hesabın, bir sanal ağ eşlemesi oluşturmak için gerekli izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c591-214">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="1c591-215">Bkz: [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="1c591-215">See the [Permissions](#permissions) section of this article for details.</span></span>
6. <span data-ttu-id="1c591-216">Bir kaynak grubu ve sanal ağ (Resource Manager) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c591-216">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="1c591-217">Betiği kopyalayın, PowerShell içinde yapıştırın ve ardından basın `Enter`.</span><span class="sxs-lookup"><span data-stu-id="1c591-217">Copy the script, paste it into PowerShell, and then press `Enter`.</span></span>

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create the virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. <span data-ttu-id="1c591-218">Farklı dağıtım modelleri arasında oluşturulan iki sanal ağlar arasında eşleme sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1c591-218">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="1c591-219">Aşağıdaki komut dosyası, bilgisayarınızdaki bir metin düzenleyicisine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1c591-219">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="1c591-220">Değiştir `<subscription id>` aboneliğinizle kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c591-220">Replace `<subscription id>` with your subscription Id.</span></span> <span data-ttu-id="1c591-221">Aboneliğinizi kimliği bilmiyorsanız, girin `Get-AzureRmSubscription` görüntülemek için komutu.</span><span class="sxs-lookup"><span data-stu-id="1c591-221">If you don't know your subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="1c591-222">Değeri **kimliği** döndürülen çıkış, abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="1c591-222">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="1c591-223">Betik yürütmek için metin düzenleyici, sonra sağ tıklatın, PowerShell oturumunda değiştirilmiş betiği kopyalayın ve tuşuna basın `Enter`.</span><span class="sxs-lookup"><span data-stu-id="1c591-223">To execute the script, copy the modified script from your text editor, then right-click in your PowerShell session, and then press `Enter`.</span></span>

    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. <span data-ttu-id="1c591-224">Betiği çalıştırdıktan sonra sanal ağ (Resource Manager) için eşleme gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1c591-224">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="1c591-225">Aşağıdaki komutu kopyalayın, PowerShell oturumunuzda yapıştırın ve ardından basın `Enter`:</span><span class="sxs-lookup"><span data-stu-id="1c591-225">Copy the following command, paste it in your PowerShell session, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="1c591-226">Çıktısında **bağlı** içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="1c591-226">The output shows **Connected** in the **PeeringState** column.</span></span>

    <span data-ttu-id="1c591-227">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini birbirleri ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="1c591-227">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="1c591-228">Varsayılan Azure ad çözümlemesi için sanal ağlar kullanıyorsanız, sanal ağlarda bulunan kaynaklar sanal ağlar arasında adlarını çözmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="1c591-228">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="1c591-229">Bir eşlemesindeki sanal ağlar arasında adları çözümlemek dilerseniz kendi DNS sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c591-229">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1c591-230">Nasıl ayarlanacağını öğrenin [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1c591-230">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

9. <span data-ttu-id="1c591-231">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1c591-231">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
10. <span data-ttu-id="1c591-232">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete-powershell) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="1c591-232">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>
 
## <span data-ttu-id="1c591-233"><a name="permissions"></a>İzinleri</span><span class="sxs-lookup"><span data-stu-id="1c591-233"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="1c591-234">Bir sanal ağ eşlemesi oluşturmak için kullandığınız hesaplarının gerekli rol veya izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c591-234">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="1c591-235">Örneğin, myVnet1 ve myVnet2 adlı iki sanal ağ eşlemesi, hesabınızı aşağıdaki en düşük rolü veya her sanal ağ izinlerini atanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1c591-235">For example, if you were peering two virtual networks named myVnet1 and myVnet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="1c591-236">Sanal ağ</span><span class="sxs-lookup"><span data-stu-id="1c591-236">Virtual network</span></span>|<span data-ttu-id="1c591-237">Dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="1c591-237">Deployment model</span></span>|<span data-ttu-id="1c591-238">Rol</span><span class="sxs-lookup"><span data-stu-id="1c591-238">Role</span></span>|<span data-ttu-id="1c591-239">İzinler</span><span class="sxs-lookup"><span data-stu-id="1c591-239">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="1c591-240">myVnet1</span><span class="sxs-lookup"><span data-stu-id="1c591-240">myVnet1</span></span>|<span data-ttu-id="1c591-241">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1c591-241">Resource Manager</span></span>|[<span data-ttu-id="1c591-242">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="1c591-242">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="1c591-243">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="1c591-243">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="1c591-244">Klasik</span><span class="sxs-lookup"><span data-stu-id="1c591-244">Classic</span></span>|[<span data-ttu-id="1c591-245">Klasik Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="1c591-245">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="1c591-246">Yok</span><span class="sxs-lookup"><span data-stu-id="1c591-246">N/A</span></span>|
|<span data-ttu-id="1c591-247">myVnet2</span><span class="sxs-lookup"><span data-stu-id="1c591-247">myVnet2</span></span>|<span data-ttu-id="1c591-248">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1c591-248">Resource Manager</span></span>|[<span data-ttu-id="1c591-249">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="1c591-249">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="1c591-250">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="1c591-250">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="1c591-251">Klasik</span><span class="sxs-lookup"><span data-stu-id="1c591-251">Classic</span></span>|[<span data-ttu-id="1c591-252">Klasik Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="1c591-252">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="1c591-253">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="1c591-253">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="1c591-254">Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve belirli izinler atama [özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="1c591-254">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="1c591-255"><a name="delete"></a>Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="1c591-255"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="1c591-256">Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz öğreticide oluşturduğunuz kaynakları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c591-256">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="1c591-257">Bir kaynak grubunun silinmesi, kaynak grubunda bulunan tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="1c591-257">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="1c591-258"><a name="delete-portal"></a>Azure portalı</span><span class="sxs-lookup"><span data-stu-id="1c591-258"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="1c591-259">Portal arama kutusuna **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1c591-259">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="1c591-260">Arama sonuçlarında tıklatın **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1c591-260">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="1c591-261">Üzerinde **myResourceGroup** dikey penceresinde tıklatın **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="1c591-261">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="1c591-262">İçinde silmeyi onaylamak için **türü kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="1c591-262">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="1c591-263"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1c591-263"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="1c591-264">Azure CLI 2.0 aşağıdaki komutu kullanarak sanal ağ (Resource Manager) silmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c591-264">Use the Azure CLI 2.0 to delete the virtual network (Resource Manager) with the following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. <span data-ttu-id="1c591-265">Azure CLI 1.0 aşağıdaki komutlarla sanal ağ (Klasik) silmek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c591-265">Use the Azure CLI 1.0 to delete the virtual network (classic) with the following commands:</span></span>

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <span data-ttu-id="1c591-266"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c591-266"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="1c591-267">Sanal ağ (Resource Manager) silmek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="1c591-267">Enter the following command to delete the virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. <span data-ttu-id="1c591-268">Sanal ağı silmek için PowerShell ile (Klasik), mevcut bir ağ yapılandırma dosyasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c591-268">To delete the virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="1c591-269">Bilgi edinmek için nasıl [dışarı aktarma, güncelleştirme ve ağ yapılandırma dosyalarını içe](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="1c591-269">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="1c591-270">Bu öğreticide kullanılan sanal ağ için aşağıdaki VirtualNetworkSite öğeyi kaldırın:</span><span class="sxs-lookup"><span data-stu-id="1c591-270">Remove the following VirtualNetworkSite element for the virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="1c591-271">Değiştirilen ağ yapılandırma dosyasını içeri varolan sanal ağlar (aboneliğinizde Klasik) yapılan değişiklikler neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="1c591-271">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="1c591-272">Önceki sanal ağı yalnızca kaldırmak ve verme değiştirir veya diğer varolan sanal ağlara aboneliğinizden kaldırırsanız, emin olun.</span><span class="sxs-lookup"><span data-stu-id="1c591-272">Ensure you only remove the previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1c591-273">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c591-273">Next steps</span></span>

- <span data-ttu-id="1c591-274">Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c591-274">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="1c591-275">Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="1c591-275">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="1c591-276">Bilgi edinmek için nasıl [bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.</span><span class="sxs-lookup"><span data-stu-id="1c591-276">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
