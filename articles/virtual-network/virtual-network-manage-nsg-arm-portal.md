---
title: "Azure portalını kullanarak Nsg'ler yönetme | Microsoft Docs"
description: "Azure Portalı'nı kullanarak var olan Nsg'ler yönetmeyi öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="d8ee2-103">Nsg'ler Portalı'nı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8ee2-104">Portal</span><span class="sxs-lookup"><span data-stu-id="d8ee2-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="d8ee2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8ee2-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="d8ee2-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d8ee2-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d8ee2-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d8ee2-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d8ee2-108">Bu makalede, Klasik dağıtım modeli yerine en yeni dağıtımlar için Microsoft önerir Resource Manager dağıtım modelini kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="d8ee2-109">Bilgi alma</span><span class="sxs-lookup"><span data-stu-id="d8ee2-109">Retrieve Information</span></span>
<span data-ttu-id="d8ee2-110">Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="d8ee2-111">Varolan Nsg'ler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="d8ee2-111">View existing NSGs</span></span>

<span data-ttu-id="d8ee2-112">Bir Abonelikteki tüm mevcut Nsg'ler görüntülemek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-113">Tarayıcıdan http://portal.azure.com adresine gidin ve gerekiyorsa Azure hesabınıza giriş yapın.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="d8ee2-114">Tıklatın **Gözat >** > **ağ güvenlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="d8ee2-116">Nsg'ler içinde listesini kontrol edin **ağ güvenlik grupları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="d8ee2-118">Bir kaynak grubunda görünüm Nsg'ler</span><span class="sxs-lookup"><span data-stu-id="d8ee2-118">View NSGs in a resource group</span></span>

<span data-ttu-id="d8ee2-119">Nsg'ler içinde listesini görüntülemek için **RG NSG** kaynak grubunda, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-120">Tıklatın **kaynak grupları >** > **RG NSG** > **...** .</span><span class="sxs-lookup"><span data-stu-id="d8ee2-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="d8ee2-122">Gösterildiği gibi kaynak listesinde NSG simgesini görüntüleme öğeleri arar **kaynakları** dikey penceresinde aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="d8ee2-124">Bir NSG için tüm kuralları listesinde</span><span class="sxs-lookup"><span data-stu-id="d8ee2-124">List all rules for an NSG</span></span>

<span data-ttu-id="d8ee2-125">Adlı bir NSG kurallarını görüntülemek için **NSG ön uç**, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-126">Gelen **ağ güvenlik grupları** dikey penceresinde veya **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="d8ee2-127">İçinde **ayarları** sekmesini tıklatın, **gelen güvenlik kuralları**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="d8ee2-129">**Gelen güvenlik kuralları** dikey penceresi aşağıda gösterildiği gibi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="d8ee2-131">İçinde **ayarları** sekmesini tıklatın, **giden güvenlik kurallarında** Giden kurallarını görmek için.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8ee2-132">Varsayılan kuralları görüntülemek için **varsayılan kuralları** kuralları görüntüler dikey simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="d8ee2-133">Nsg'ler ilişkilendirmelerini görüntülemek</span><span class="sxs-lookup"><span data-stu-id="d8ee2-133">View NSGs associations</span></span>

<span data-ttu-id="d8ee2-134">Hangi kaynakları görüntülemek için **NSG ön uç** NSG ilişkilendirmek, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-135">Gelen **ağ güvenlik grupları** dikey penceresinde veya **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="d8ee2-136">İçinde **ayarları** sekmesini tıklatın, **alt ağlar** hangi alt ağların NSG'yi ilişkili görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="d8ee2-138">İçinde **ayarları** sekmesini tıklatın, **ağ arabirimleri** NIC'ler NSG'yi ilişkili nelerdir görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="d8ee2-139">Kuralları yönetme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-139">Manage rules</span></span>
<span data-ttu-id="d8ee2-140">Varolan bir NSG kuralları ekleme, mevcut kuralları düzenlemek ve kuralları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="d8ee2-141">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-141">Add a rule</span></span>
<span data-ttu-id="d8ee2-142">İzin verme kuralı eklemek için **gelen** bağlantı noktası trafiği **443** için herhangi bir makineden **NSG ön uç** NSG, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-143">Gelen **ağ güvenlik grupları** dikey penceresinde veya **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="d8ee2-144">İçinde **ayarları** sekmesini tıklatın, **gelen güvenlik kuralları**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="d8ee2-145">İçinde **gelen güvenlik kuralları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="d8ee2-146">Ardından **gelen Güvenlik Kuralı Ekle** dikey penceresinde, aşağıda gösterildiği gibi değerlerini doldurun ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="d8ee2-148">Birkaç saniye sonra yeni kuralında fark **gelen güvenlik kuralları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="d8ee2-150">Bir kural değiştirme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-150">Change a rule</span></span>
<span data-ttu-id="d8ee2-151">Öğesinden gelen trafiğe izin vermek için yukarıda oluşturduğunuz kural değiştirmek için **Internet** yalnızca, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-152">Gelen **ağ güvenlik grupları** dikey penceresinde veya **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="d8ee2-153">İçinde **ayarları** sekmesinde, yukarıda oluşturduğunuz kural'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="d8ee2-154">İçinde **izin https** dikey penceresinde, değişiklik **kaynak** aşağıda gösterildiği gibi özelliği ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="d8ee2-156">Kural silme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-156">Delete a rule</span></span>

<span data-ttu-id="d8ee2-157">Yukarıda oluşturduğunuz kural silmek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-158">Gelen **ağ güvenlik grupları** dikey penceresinde veya **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="d8ee2-159">İçinde **ayarları** sekmesinde, yukarıda oluşturduğunuz kural'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="d8ee2-160">İçinde **izin https** dikey penceresinde tıklatın **silmek**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="d8ee2-162">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-162">Manage associations</span></span>
<span data-ttu-id="d8ee2-163">Bir NSG'yi alt ağlara ve NIC ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="d8ee2-164">Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="d8ee2-165">Bir NSG'yi bir NIC ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="d8ee2-166">İlişkilendirilecek **NSG ön uç** NSG'yi **TestNICWeb1** NIC, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-167">Gelen **ağ güvenlik grupları** dikey penceresinde veya **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="d8ee2-168">İçinde **ayarları** sekmesini tıklatın, **ağ arabirimleri** > **ilişkilendirmek** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="d8ee2-170">Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="d8ee2-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="d8ee2-171">İlişkilendirmesini kaldırmak **NSG ön uç** NSG gelen **TestNICWeb1** NIC, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-172">Azure portalından tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="d8ee2-173">İçinde **TestNICWeb1** dikey penceresinde tıklatın **değiştirme güvenlik...**   >  **Hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="d8ee2-175">Bu dikey pencere, varolan bir NSG NIC'ye ilişkilendirmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="d8ee2-176">Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="d8ee2-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="d8ee2-177">İlişkilendirmesini kaldırmak **NSG ön uç** NSG gelen **ön uç** alt ağ, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-178">Azure portalından tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="d8ee2-179">İçinde **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **Hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="d8ee2-181">İçinde **ön uç** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="d8ee2-183">Bir NSG'yi bir alt ağ ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="d8ee2-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="d8ee2-184">İlişkilendirilecek **NSG ön uç** NSG'yi **FronEnd** alt yeniden, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="d8ee2-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="d8ee2-185">Azure portalından tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="d8ee2-186">İçinde **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu** > **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="d8ee2-187">İçinde **ön uç** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8ee2-188">Ayrıca bir NSG bir alt ağa thh NSG's ilişkilendirebilirsiniz **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="d8ee2-189">Bir NSG'yi Sil</span><span class="sxs-lookup"><span data-stu-id="d8ee2-189">Delete an NSG</span></span>
<span data-ttu-id="d8ee2-190">Herhangi bir kaynağa ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="d8ee2-191">Bir NSG'yi silmek için aşağıdaki adımları tamamlayın:.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="d8ee2-192">Azure portalından tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="d8ee2-193">İçinde **ayarları** dikey penceresinde tıklatın **ağ arabirimleri**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="d8ee2-194">Listelenen NIC'ler varsa, NIC tıklayın ve adım 2'de izleyin [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="d8ee2-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="d8ee2-195">3. adım her NIC için yineleyin</span><span class="sxs-lookup"><span data-stu-id="d8ee2-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="d8ee2-196">İçinde **ayarları** dikey penceresinde tıklatın **alt ağlar**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="d8ee2-197">Listelenen alt ağı varsa, alt ağ'ı tıklatın ve 2 ve 3'te adımları izleyerek [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="d8ee2-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="d8ee2-198">Sola kaydırır **NSG ön uç** dikey penceresinde, ardından **silmek** > **Evet**.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="d8ee2-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8ee2-200">Next steps</span></span>
* <span data-ttu-id="d8ee2-201">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="d8ee2-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
