---
title: Hello Azure portal kullanarak aaaManage Nsg'ler | Microsoft Docs
description: "Bilgi nasıl hello Azure portal kullanarak Nsg'ler varolan toomanage."
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
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="8bd22-103">Nsg'ler Hello portal kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="8bd22-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bd22-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8bd22-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="8bd22-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd22-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="8bd22-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8bd22-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8bd22-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8bd22-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8bd22-108">Bu makalede, Microsoft hello Klasik dağıtım modeli yerine çoğu yeni dağıtımlar için önerir hello Resource Manager dağıtım modeli kullanılarak kapsar.</span><span class="sxs-lookup"><span data-stu-id="8bd22-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="8bd22-109">Bilgi alma</span><span class="sxs-lookup"><span data-stu-id="8bd22-109">Retrieve Information</span></span>
<span data-ttu-id="8bd22-110">Varolan Nsg'lerinizi görüntülemek için varolan bir NSG kuralları almak ve hangi kaynakların bir NSG için ilişkili olduğunu öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8bd22-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="8bd22-111">Varolan Nsg'ler görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="8bd22-111">View existing NSGs</span></span>

<span data-ttu-id="8bd22-112">tooview tüm Nsg'ler bir abonelikte, aşağıdaki adımları tam hello var:</span><span class="sxs-lookup"><span data-stu-id="8bd22-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-113">Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="8bd22-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="8bd22-114">Tıklatın **Gözat >** > **ağ güvenlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="8bd22-116">Merhaba listesinde Nsg'ler hello denetleyin **ağ güvenlik grupları** dikey.</span><span class="sxs-lookup"><span data-stu-id="8bd22-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="8bd22-118">Bir kaynak grubunda görünüm Nsg'ler</span><span class="sxs-lookup"><span data-stu-id="8bd22-118">View NSGs in a resource group</span></span>

<span data-ttu-id="8bd22-119">tooview hello listesinde Nsg'ler hello **RG NSG** kaynak grubu, şu adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-120">Tıklatın **kaynak grupları >** > **RG NSG** > **...** .</span><span class="sxs-lookup"><span data-stu-id="8bd22-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="8bd22-122">Hello gösterildiği gibi kaynak Hello listesinde hello NSG simgesini görüntüleme öğeleri arar **kaynakları** dikey penceresinde aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="8bd22-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="8bd22-124">Bir NSG için tüm kuralları listesinde</span><span class="sxs-lookup"><span data-stu-id="8bd22-124">List all rules for an NSG</span></span>

<span data-ttu-id="8bd22-125">adlı bir NSG tooview hello kuralları **NSG ön uç**tam hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8bd22-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-126">Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="8bd22-127">Merhaba, **ayarları** sekmesini tıklatın, **gelen güvenlik kuralları**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="8bd22-129">Merhaba **gelen güvenlik kuralları** dikey penceresi aşağıda gösterildiği gibi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8bd22-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="8bd22-131">Merhaba, **ayarları** sekmesini tıklatın, **giden güvenlik kurallarında** toosee hello giden kuralları.</span><span class="sxs-lookup"><span data-stu-id="8bd22-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8bd22-132">tooview varsayılan kuralları tıklatın hello **varsayılan kuralları** hello kuralları görüntüler hello dikey penceresinde hello üstündeki simgesi.</span><span class="sxs-lookup"><span data-stu-id="8bd22-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="8bd22-133">Nsg'ler ilişkilendirmelerini görüntülemek</span><span class="sxs-lookup"><span data-stu-id="8bd22-133">View NSGs associations</span></span>

<span data-ttu-id="8bd22-134">tooview hangi kaynaklara hello **NSG ön uç** NSG olan aşağıdaki adımları ile tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-135">Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="8bd22-136">Merhaba, **ayarları** sekmesini tıklatın, **alt ağlar** hangi alt ağlardır tooview toohello NSG ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="8bd22-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="8bd22-138">Merhaba, **ayarları** sekmesini tıklatın, **ağ arabirimleri** tooview ne NIC'ler ilişkili toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="8bd22-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="8bd22-139">Kuralları yönetme</span><span class="sxs-lookup"><span data-stu-id="8bd22-139">Manage rules</span></span>
<span data-ttu-id="8bd22-140">NSG varolan kuralları tooan eklemek, mevcut kuralları düzenlemek ve kuralları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8bd22-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="8bd22-141">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="8bd22-141">Add a rule</span></span>
<span data-ttu-id="8bd22-142">izin verme kuralı tooadd **gelen** trafiği tooport **443** tüm makine toohello gelen **NSG ön uç** NSG, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-143">Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="8bd22-144">Merhaba, **ayarları** sekmesini tıklatın, **gelen güvenlik kuralları**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="8bd22-145">Merhaba, **gelen güvenlik kuralları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="8bd22-146">Ardından hello **gelen Güvenlik Kuralı Ekle** dikey penceresinde, aşağıda gösterildiği gibi hello değerlerini doldurun ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="8bd22-148">Birkaç saniye sonra hello yeni hello kuralında fark **gelen güvenlik kuralları** dikey.</span><span class="sxs-lookup"><span data-stu-id="8bd22-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="8bd22-150">Bir kural değiştirme</span><span class="sxs-lookup"><span data-stu-id="8bd22-150">Change a rule</span></span>
<span data-ttu-id="8bd22-151">tooallow oluşturulan toochange hello kural hello trafiğinden gelen **Internet** aşağıdaki adımları yalnızca, tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-152">Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="8bd22-153">Merhaba, **ayarları** sekmesinde, yukarıda oluşturduğunuz hello kural'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8bd22-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="8bd22-154">Merhaba, **izin https** dikey penceresinde, değişiklik hello **kaynak** aşağıda gösterildiği gibi özelliği ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="8bd22-156">Kural silme</span><span class="sxs-lookup"><span data-stu-id="8bd22-156">Delete a rule</span></span>

<span data-ttu-id="8bd22-157">Aşağıdaki adımları toodelete hello kural yukarıda oluşturulan, tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-158">Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="8bd22-159">Merhaba, **ayarları** sekmesinde, yukarıda oluşturduğunuz hello kural'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8bd22-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="8bd22-160">Merhaba, **izin https** dikey penceresinde tıklatın **silmek**ve ardından **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="8bd22-162">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="8bd22-162">Manage associations</span></span>
<span data-ttu-id="8bd22-163">Bir NSG toosubnets ve NIC ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd22-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="8bd22-164">Bir NSG'yi ilişkili olduğu herhangi bir kaynaktan ilişkisini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8bd22-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="8bd22-165">Bir NSG tooa NIC ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="8bd22-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="8bd22-166">tooassociate hello **NSG ön uç** NSG toohello **TestNICWeb1** NIC, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-167">Merhaba gelen **ağ güvenlik grupları** dikey ya da hello **kaynakları** , yukarıda gösterilen dikey tıklayın **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="8bd22-168">Merhaba, **ayarları** sekmesini tıklatın, **ağ arabirimleri** > **ilişkilendirmek** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="8bd22-170">Bir NSG'yi bir NIC gelen ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="8bd22-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="8bd22-171">toodissociate hello **NSG ön uç** hello gelen NSG **TestNICWeb1** NIC, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-172">Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="8bd22-173">Merhaba, **TestNICWeb1** dikey penceresinde tıklatın **değiştirme güvenlik...**   >  **Hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="8bd22-175">NSG varolan bu dikey tooassociate hello NIC tooany de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd22-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="8bd22-176">Bir NSG'yi bir alt ağdan ilişkilendirmesini Kaldır</span><span class="sxs-lookup"><span data-stu-id="8bd22-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="8bd22-177">toodissociate hello **NSG ön uç** hello gelen NSG **ön uç** alt ağ, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-178">Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="8bd22-179">Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **Hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="8bd22-181">Merhaba, **ön uç** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="8bd22-183">Bir NSG tooa alt ağını ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="8bd22-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="8bd22-184">tooassociate hello **NSG ön uç** NSG toohello **FronEnd** yeniden alt ağ, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="8bd22-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="8bd22-185">Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="8bd22-186">Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="8bd22-187">Merhaba, **ön uç** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd22-188">Ayrıca, bir NSG tooa alt ağ üzerinden thh NSG's ilişkilendirebilirsiniz **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="8bd22-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="8bd22-189">Bir NSG'yi Sil</span><span class="sxs-lookup"><span data-stu-id="8bd22-189">Delete an NSG</span></span>
<span data-ttu-id="8bd22-190">Tooany kaynak ilişkili olmayan bir NSG'yi yalnızca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd22-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="8bd22-191">toodelete bir NSG, aşağıdaki adımları tam hello:.</span><span class="sxs-lookup"><span data-stu-id="8bd22-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="8bd22-192">Hello ifadesini Azure portal'ı tıklatın **kaynak grupları >** > **RG NSG** > **...**   >  **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="8bd22-193">Merhaba, **ayarları** dikey penceresinde tıklatın **ağ arabirimleri**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="8bd22-194">Listelenen NIC'ler varsa, hello NIC tıklayın ve adım 2'de izleyin [bir NSG'yi bir NIC gelen ilişkilendirmesini](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="8bd22-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="8bd22-195">3. adım her NIC için yineleyin</span><span class="sxs-lookup"><span data-stu-id="8bd22-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="8bd22-196">Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="8bd22-197">Listelenen hiçbir alt ağ yoksa, hello alt ağ'ı tıklatın ve 2 ve 3'te adımları izleyerek [bir NSG bir alt ağdan ilişkilendirmesini](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="8bd22-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="8bd22-198">Sol toohello kayar **NSG ön uç** dikey penceresinde, ardından **silmek** > **Evet**.</span><span class="sxs-lookup"><span data-stu-id="8bd22-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Azure portal - Nsg'ler](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="8bd22-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8bd22-200">Next steps</span></span>
* <span data-ttu-id="8bd22-201">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="8bd22-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
