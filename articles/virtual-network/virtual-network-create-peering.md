---
title: "Bir Azure sanal ağı - Resource Manager - eşlemesi oluşturmak aynı abonelik | Microsoft Docs"
description: "Aynı Azure aboneliğindeki mevcut Resource Manager aracılığıyla oluşturulan sanal ağlar arasında eşleme sanal ağ oluşturmayı öğrenin."
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
ms.openlocfilehash: a32a6b33e04c603325ab3612f61e5852682eac7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="98ba0-103">Bir sanal ağ eşlemesi - oluşturmak Resource Manager, aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="98ba0-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="98ba0-104">Bu öğreticide, Resource Manager aracılığıyla oluşturulan sanal ağlar arasında eşleme sanal ağ oluşturmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="98ba0-105">Her iki sanal ağlar aynı abonelikte yok.</span><span class="sxs-lookup"><span data-stu-id="98ba0-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="98ba0-106">Kaynaklar aynı sanal ağda gibi davranarak birbirleri ile aynı bant genişliği ve gecikme süresi ile iletişim kurmak için farklı sanal ağlar iki sanal ağlar etkinleştirir kaynaklarında eşleme.</span><span class="sxs-lookup"><span data-stu-id="98ba0-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="98ba0-107">Daha fazla bilgi edinmek [sanal ağ eşlemesi](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98ba0-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="98ba0-108">Sanal ağlar aynı ya da farklı olup, abonelikleri ve hangi bağlı olarak farklı bir sanal ağ eşlemesi oluşturmak için aşağıdaki adımları [Azure dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal ağlar üzerinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="98ba0-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="98ba0-109">Aşağıdaki tabloda senaryodan tıklayarak diğer senaryolarda eşliği bir sanal ağ oluşturmayı öğrenin:</span><span class="sxs-lookup"><span data-stu-id="98ba0-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="98ba0-110">Azure dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="98ba0-110">Azure deployment model</span></span>  | <span data-ttu-id="98ba0-111">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="98ba0-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="98ba0-112">Her iki kaynak yöneticisi</span><span class="sxs-lookup"><span data-stu-id="98ba0-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="98ba0-113">Farklı</span><span class="sxs-lookup"><span data-stu-id="98ba0-113">Different</span></span>|
|[<span data-ttu-id="98ba0-114">Bir kaynak yöneticisi, bir Klasik</span><span class="sxs-lookup"><span data-stu-id="98ba0-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="98ba0-115">Aynı</span><span class="sxs-lookup"><span data-stu-id="98ba0-115">Same</span></span>|
|[<span data-ttu-id="98ba0-116">Bir kaynak yöneticisi, bir Klasik</span><span class="sxs-lookup"><span data-stu-id="98ba0-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="98ba0-117">Farklı</span><span class="sxs-lookup"><span data-stu-id="98ba0-117">Different</span></span>|

<span data-ttu-id="98ba0-118">Klasik dağıtım modeli aracılığıyla dağıtılan iki sanal ağ arasında bir sanal ağ eşlemesi oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="98ba0-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="98ba0-119">Bir sanal ağ eşlemesi yalnızca aynı Azure bölgesinde mevcut iki sanal ağ arasında oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="98ba0-120">Her ikisi de oluşturulmuş Klasik dağıtım modeli aracılığıyla ya da farklı Azure bölgelerinde mevcut sanal ağlara bağlanmak gerekiyorsa, Azure kullanabilirsiniz [VPN ağ geçidi](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) sanal ağlara bağlanma.</span><span class="sxs-lookup"><span data-stu-id="98ba0-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="98ba0-121">Kullanabileceğiniz [Azure portal](#portal), Azure [komut satırı arabirimi](#cli) (CLI) Azure [PowerShell](#powershell), veya bir [Azure Resource Manager şablonu](#template)bir sanal ağ eşlemesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="98ba0-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) to create a virtual network peering.</span></span> <span data-ttu-id="98ba0-122">Doğrudan seçeceğiniz araç kullanarak bir sanal ağ eşlemesi oluşturma adımlarını gitmek için önceki aracı bağlantılardan herhangi birine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="98ba0-123"><a name="portal"></a>Eşlemesi - oluşturmak Azure portalı</span><span class="sxs-lookup"><span data-stu-id="98ba0-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="98ba0-124">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="98ba0-125">İle oturum için kullandığınız hesabın, bir sanal ağ eşlemesi oluşturmak için gerekli izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="98ba0-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="98ba0-126">Bkz: [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="98ba0-127">Tıklatın **+ yeni**, tıklatın **ağ**, ardından **sanal ağ**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="98ba0-128">İçinde **sanal ağ oluştur** dikey penceresinde girin veya aşağıdaki ayarları için değerleri seçin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="98ba0-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="98ba0-129">**Ad**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="98ba0-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="98ba0-130">**Adres alanı**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="98ba0-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="98ba0-131">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="98ba0-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="98ba0-132">**Alt ağ adres aralığı**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="98ba0-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="98ba0-133">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="98ba0-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="98ba0-134">**Kaynak grubu**: seçin **Yeni Oluştur** ve girin *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="98ba0-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="98ba0-135">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="98ba0-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="98ba0-136">Adım 3'te yeniden aşağıdaki değerleri belirtme 2-3 adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="98ba0-136">Complete steps 2-3 again specifying the following values in step 3:</span></span>
    - <span data-ttu-id="98ba0-137">**Ad**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="98ba0-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="98ba0-138">**Adres alanı**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="98ba0-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="98ba0-139">**Alt ağ adı**: *varsayılan*</span><span class="sxs-lookup"><span data-stu-id="98ba0-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="98ba0-140">**Alt ağ adres aralığı**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="98ba0-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="98ba0-141">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="98ba0-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="98ba0-142">**Kaynak grubu**: seçin **var olanı kullan** seçip *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="98ba0-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="98ba0-143">**Konum**: *Doğu ABD*</span><span class="sxs-lookup"><span data-stu-id="98ba0-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="98ba0-144">İçinde **arama kaynakları** kutusunu türü portalı üstündeki *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="98ba0-144">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="98ba0-145">Tıklatın **myResourceGroup** arama sonuçlarında görüntülendiğinde.</span><span class="sxs-lookup"><span data-stu-id="98ba0-145">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="98ba0-146">Bir dikey pencere görünür **myresourcegroup** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="98ba0-146">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="98ba0-147">Kaynak grubu, önceki adımlarda oluşturduğunuz iki sanal ağ içeriyor.</span><span class="sxs-lookup"><span data-stu-id="98ba0-147">The resource group contains the two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="98ba0-148">Tıklatın **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="98ba0-149">İçinde **myVnet1** görünür, dikey tıklayın **eşlemeler** dikey pencerenin sol tarafındaki seçenekleri dikey listesinden.</span><span class="sxs-lookup"><span data-stu-id="98ba0-149">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
8. <span data-ttu-id="98ba0-150">İçinde **myVnet1 - eşlemeler** görünen dikey tıklayın **+ Ekle**</span><span class="sxs-lookup"><span data-stu-id="98ba0-150">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="98ba0-151">İçinde **Ekle eşliği** görünür, dikey girin veya aşağıdaki seçenekleri belirleyin ve ardından **Tamam**:</span><span class="sxs-lookup"><span data-stu-id="98ba0-151">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="98ba0-152">**Ad**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="98ba0-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="98ba0-153">**Sanal ağ dağıtım modeli**: seçin **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="98ba0-154">**Abonelik**: aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="98ba0-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="98ba0-155">**Sanal ağ**: tıklatın **sanal ağ seçin**, ardından **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="98ba0-156">**Sanal ağ erişimine izin ver:** emin **etkin** seçilir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="98ba0-157">Diğer bir ayarları, bu öğreticide kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98ba0-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="98ba0-158">Tüm eşleme ayarları hakkında bilgi için okuma [sanal ağ eşlemeleri yönetme](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="98ba0-158">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="98ba0-159">' I tıklattıktan sonra **Tamam** önceki adımda **Ekle eşliği** dikey penceresi kapanır ve gördüğünüz **myVnet1 - eşlemeler** dikey penceresini yeniden.</span><span class="sxs-lookup"><span data-stu-id="98ba0-159">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="98ba0-160">Birkaç saniye sonra oluşturduğunuz eşliği dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-160">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="98ba0-161">**Başlatılan** içinde listelenen **EŞLİĞİ durumu** sütunu için **myVnet1ToMyVnet2** sizin eşlemeyi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="98ba0-161">**Initiated** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="98ba0-162">Vnet1'den vnet2'ye eşlenen, ancak şimdi myVnet1 myVnet2 eş gerekir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-162">You've peered Vnet1 to Vnet2, but now you must peer myVnet2 to myVnet1.</span></span> <span data-ttu-id="98ba0-163">Eşlemeyi birbirleri ile iletişim kurmak üzere sanal ağ kaynaklarında etkinleştirmek için her iki yönde oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="98ba0-163">The peering must be created in both directions to enable resources in the virtual networks to communicate with each other.</span></span>
11. <span data-ttu-id="98ba0-164">Yeniden myVnet2 için 5-10 adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="98ba0-165">Eşlemeyi ad *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="98ba0-165">Name the peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="98ba0-166">' I tıklattıktan sonra birkaç saniye **Tamam** MyVnet2 için eşlemesi oluşturmak için **myVnet2ToMyVnet1** , yeni oluşturduğunuz eşliği ile listelendiğini **bağlı** içinde  **Eşleme durumu** sütun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-166">A few seconds after clicking **OK** to create the peering for MyVnet2, the **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in the **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="98ba0-167">Adım 5-7 MyVnet1 için yeniden tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="98ba0-168">**EŞLİĞİ durumu** için **myVnet1ToVNet2** eşliği olan şimdi de **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-168">The **PEERING STATUS** for the **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="98ba0-169">Gördükten sonra Eşleme başarıyla kurulduktan **bağlı** içinde **EŞLİĞİ durum** sütun eşlemesi içindeki iki sanal ağlar için.</span><span class="sxs-lookup"><span data-stu-id="98ba0-169">The peering is successfully established after you see **Connected** in the **PEERING STATUS** column for both virtual networks in the peering.</span></span>
14. <span data-ttu-id="98ba0-170">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
15. <span data-ttu-id="98ba0-171">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-171">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="98ba0-172">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini birbirleri ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="98ba0-172">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="98ba0-173">Varsayılan Azure ad çözümlemesi için sanal ağlar kullanıyorsanız, sanal ağlarda bulunan kaynaklar sanal ağlar arasında adlarını çözmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-173">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="98ba0-174">Bir eşlemesindeki sanal ağlar arasında adları çözümlemek dilerseniz kendi DNS sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-174">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="98ba0-175">Nasıl ayarlanacağını öğrenin [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="98ba0-175">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="98ba0-176"><a name="cli"></a>Eşlemesi - oluşturmak Azure CLI</span><span class="sxs-lookup"><span data-stu-id="98ba0-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="98ba0-177">Aşağıdaki komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="98ba0-177">The following script:</span></span>

- <span data-ttu-id="98ba0-178">Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="98ba0-178">Requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="98ba0-179">Sürüm bulmak için Çalıştır `az --version` komutu.</span><span class="sxs-lookup"><span data-stu-id="98ba0-179">To find the version, run the `az --version` command.</span></span> <span data-ttu-id="98ba0-180">Yükseltme gerekiyorsa, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98ba0-180">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="98ba0-181">Bir Bash kabuğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="98ba0-181">Works in a Bash shell.</span></span> <span data-ttu-id="98ba0-182">Windows istemcisi üzerinde Azure CLI betikleri çalıştırma seçenekleri için bkz [Windows Azure CLI çalıştıran](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98ba0-182">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="98ba0-183">CLI ve bağımlılıklarını yüklemek yerine, Azure bulut Kabuğu'nu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98ba0-183">Instead of installing the CLI and its dependencies, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="98ba0-184">Azure Cloud Shell doğrudan Azure portalının içinde çalıştırabileceğiniz ücretsiz bir Bash kabuğudur.</span><span class="sxs-lookup"><span data-stu-id="98ba0-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="98ba0-185">Azure CLI, kabuğa önceden yüklenmiştir ve kabuk, hesabınızla birlikte kullanılacak şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="98ba0-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="98ba0-186">Tıklatın **deneyin** , oturumu bir bulut Kabuk çağırır aşağıdaki Azure hesabınızla oturum açabildiğinizden komut düğmesi.</span><span class="sxs-lookup"><span data-stu-id="98ba0-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="98ba0-187">Betik yürütmek için tıklatın **kopyalama** düğmesine tıklayın ve bulut kabuğundan içeriğini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-187">To execute the script, click the **Copy** button and paste the contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="98ba0-188">Bir kaynak grubu ve iki sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
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

2. <span data-ttu-id="98ba0-189">İki sanal ağlar arasında eşlemeyi bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-189">Create a virtual network peering between the two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get the id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 to VNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="98ba0-190">Betiği çalıştırdıktan sonra her bir sanal ağ eşlemeleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-190">After the script executes, review the peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="98ba0-191">Değiştirme önceki komutu yeniden çalıştırın *myVnet1* ile *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="98ba0-191">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="98ba0-192">Her ikisi de çıktısını gösterir komutları **bağlı** içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-192">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>

     <span data-ttu-id="98ba0-193">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini birbirleri ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="98ba0-193">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="98ba0-194">Varsayılan Azure ad çözümlemesi için sanal ağlar kullanıyorsanız, sanal ağlarda bulunan kaynaklar sanal ağlar arasında adlarını çözmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-194">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="98ba0-195">Bir eşlemesindeki sanal ağlar arasında adları çözümlemek dilerseniz kendi DNS sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-195">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="98ba0-196">Nasıl ayarlanacağını öğrenin [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="98ba0-196">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="98ba0-197">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
5. <span data-ttu-id="98ba0-198">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete-cli) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="98ba0-198">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="98ba0-199"><a name="powershell"></a>Eşlemesi - oluşturmak PowerShell</span><span class="sxs-lookup"><span data-stu-id="98ba0-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="98ba0-200">PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülünün en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-200">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="98ba0-201">Azure PowerShell'i kullanmaya yeni başladıysanız [Azure PowerShell'e genel bakış](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json) sayfasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-201">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="98ba0-202">Bir PowerShell oturumu başlatmak için **Başlat**'a gidin, **powershell** yazın ve **PowerShell**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-202">To start a PowerShell session, go to **Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="98ba0-203">PowerShell'de `login-azurermaccount` komutunu girerek Azure oturumu açın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-203">In PowerShell, log in to Azure by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="98ba0-204">İle oturum için kullandığınız hesabın, bir sanal ağ eşlemesi oluşturmak için gerekli izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="98ba0-204">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="98ba0-205">Bkz: [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-205">See the [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="98ba0-206">Bir kaynak grubu ve iki sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="98ba0-207">Betik yürütmek için aşağıdaki komutu kopyalayın, PowerShell içinde yapıştırın ve ardından basın `Enter` son satırında ekranda göründükten sonra:</span><span class="sxs-lookup"><span data-stu-id="98ba0-207">To execute the script, copy the following script, paste it into PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>

    ```powershell
    # Variables for common values used throughout the script.
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

5. <span data-ttu-id="98ba0-208">İki sanal ağlar arasında eşlemeyi bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-208">Create a virtual network peering between the two virtual networks.</span></span> <span data-ttu-id="98ba0-209">Aşağıdaki komutu kopyalayın, PowerShell yapıştırın ve ardından basın `Enter` son satırında ekranda göründükten sonra:</span><span class="sxs-lookup"><span data-stu-id="98ba0-209">Copy the following script, paste in to PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>
    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 to VNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="98ba0-210">Sanal ağ alt ağlarını gözden geçirmek için aşağıdaki komutu kopyalayın, PowerShell yapıştırın ve ardından basın `Enter`:</span><span class="sxs-lookup"><span data-stu-id="98ba0-210">To review the subnets for the virtual network, copy the following command, paste in to PowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="98ba0-211">Değiştirme önceki komutu yeniden çalıştırın *myVnet1* ile *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="98ba0-211">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="98ba0-212">Her ikisi de çıktısını gösterir komutları **bağlı** içinde **PeeringState** sütun.</span><span class="sxs-lookup"><span data-stu-id="98ba0-212">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>
7. <span data-ttu-id="98ba0-213">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
8. <span data-ttu-id="98ba0-214">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete-powershell) bu makalede.</span><span class="sxs-lookup"><span data-stu-id="98ba0-214">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="98ba0-215">Ya da sanal ağ içinde oluşturduğunuz Azure kaynaklarını IP adreslerini birbirleri ile iletişim kuramıyor.</span><span class="sxs-lookup"><span data-stu-id="98ba0-215">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="98ba0-216">Varsayılan Azure ad çözümlemesi için sanal ağlar kullanıyorsanız, sanal ağlarda bulunan kaynaklar sanal ağlar arasında adlarını çözmek mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-216">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="98ba0-217">Bir eşlemesindeki sanal ağlar arasında adları çözümlemek dilerseniz kendi DNS sunucusu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-217">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="98ba0-218">Nasıl ayarlanacağını öğrenin [kendi DNS sunucu kullanılarak ad çözümleme](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="98ba0-218">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="98ba0-219"><a name="template"></a>Eşlemesi - oluşturmak Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="98ba0-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="98ba0-220">Başvuru [bir sanal ağ eşlemesi oluşturma](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="98ba0-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="98ba0-221">Şablonla birlikte verilen talimatları kullanarak şablonu Azure portalı, PowerShell veya Azure CLI aracılığıyla dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98ba0-221">Instructions are provided with the template for deploying the template using the Azure portal, PowerShell, or the Azure CLI.</span></span> <span data-ttu-id="98ba0-222">Bir sanal ağ eşlemesi oluşturmak için gerekli izinlere sahip bir hesap kullanarak şablonu dağıtmak hangisi aracı için oturum açma seçin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-222">Log in to whichever tool you choose to deploy the template with using an account that has the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="98ba0-223">Bkz: [izinleri](#permissions) Ayrıntılar için bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="98ba0-223">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="98ba0-224">**İsteğe bağlı**: sanal makineler oluştururken bu öğreticide kapsanmayan olsa, her sanal ağ içinde bir sanal makine oluşturun ve bir sanal makineden diğerine, bağlanabilirliği doğrulamak için bağlanın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
3. <span data-ttu-id="98ba0-225">**İsteğe bağlı**: Bu öğreticide oluşturduğunuz kaynaklarını silmek için adımları tamamlamanız [silmek kaynakları](#delete) Azure portalı, PowerShell veya Azure CLI kullanarak, bu makalenin bölümüne.</span><span class="sxs-lookup"><span data-stu-id="98ba0-225">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete) section of this article, using either the Azure portal, PowerShell, or the Azure CLI.</span></span>

## <span data-ttu-id="98ba0-226"><a name="permissions"></a>İzinleri</span><span class="sxs-lookup"><span data-stu-id="98ba0-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="98ba0-227">Bir sanal ağ eşlemesi oluşturmak için kullandığınız hesaplarının gerekli rol veya izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="98ba0-227">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="98ba0-228">Örneğin, VNet1 ve VNet2 adlı iki sanal ağ eşlemesi, hesabınızı aşağıdaki en düşük rolü veya her sanal ağ izinlerini atanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="98ba0-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="98ba0-229">Sanal ağ</span><span class="sxs-lookup"><span data-stu-id="98ba0-229">Virtual network</span></span>|<span data-ttu-id="98ba0-230">Rol</span><span class="sxs-lookup"><span data-stu-id="98ba0-230">Role</span></span>|<span data-ttu-id="98ba0-231">İzinler</span><span class="sxs-lookup"><span data-stu-id="98ba0-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="98ba0-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="98ba0-232">VNet1</span></span>|[<span data-ttu-id="98ba0-233">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="98ba0-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="98ba0-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="98ba0-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="98ba0-235">Vnet2'ye</span><span class="sxs-lookup"><span data-stu-id="98ba0-235">VNet2</span></span>|[<span data-ttu-id="98ba0-236">Ağ Katılımcısı</span><span class="sxs-lookup"><span data-stu-id="98ba0-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="98ba0-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="98ba0-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="98ba0-238">Daha fazla bilgi edinmek [yerleşik roller](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) ve belirli izinler atama [özel roller](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (yalnızca Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="98ba0-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="98ba0-239"><a name="delete"></a>Kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="98ba0-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="98ba0-240">Bu öğreticiyi tamamladığınızda, kullanım ücret ödememeniz öğreticide oluşturduğunuz kaynakları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98ba0-240">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="98ba0-241">Bir kaynak grubunun silinmesi, kaynak grubunda bulunan tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="98ba0-241">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="98ba0-242"><a name="delete-portal"></a>Azure portalı</span><span class="sxs-lookup"><span data-stu-id="98ba0-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="98ba0-243">Portal arama kutusuna **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-243">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="98ba0-244">Arama sonuçlarında tıklatın **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-244">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="98ba0-245">Üzerinde **myResourceGroup** dikey penceresinde tıklatın **silmek** simgesi.</span><span class="sxs-lookup"><span data-stu-id="98ba0-245">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="98ba0-246">İçinde silmeyi onaylamak için **türü kaynak grubu adı** kutusuna **myResourceGroup**ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="98ba0-246">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="98ba0-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="98ba0-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="98ba0-248">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="98ba0-248">Enter the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="98ba0-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="98ba0-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="98ba0-250">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="98ba0-250">Enter the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="98ba0-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98ba0-251">Next steps</span></span>

- <span data-ttu-id="98ba0-252">Baştan sona ile önemli öğrenmeniz [sanal ağ eşleme kısıtlamaları ve davranışları](virtual-network-manage-peering.md#requirements-and-constraints) için üretim eşleme sanal ağ oluşturmadan önce kullanın.</span><span class="sxs-lookup"><span data-stu-id="98ba0-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="98ba0-253">Tüm hakkında bilgi edinin [sanal ağ eşleme ayarları](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="98ba0-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="98ba0-254">Bilgi edinmek için nasıl [bir hub oluşturmak ve ağ topolojisine bağlı bileşen](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) sanal ağ eşlemesi ile.</span><span class="sxs-lookup"><span data-stu-id="98ba0-254">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
