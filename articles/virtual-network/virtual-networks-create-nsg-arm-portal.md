---
title: "aaaManage ağ güvenlik grupları - Azure portalı | Microsoft Docs"
description: "Azure portal kullanarak toomanage ağ güvenlik grupları nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="c9c07-103">Ağ güvenlik grupları Hello Azure portal kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="c9c07-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c9c07-104">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c9c07-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="c9c07-105">Ayrıca [hello Klasik dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c9c07-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="c9c07-106">Merhaba örnek PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz senaryosunda hello yukarıdaki temel.</span><span class="sxs-lookup"><span data-stu-id="c9c07-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="c9c07-107">Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.</span><span class="sxs-lookup"><span data-stu-id="c9c07-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="c9c07-108">Merhaba adımlar kullanım **RG NSG** hello hello kaynak grubu hello şablonunun adını dağıtılmış olan gibi.</span><span class="sxs-lookup"><span data-stu-id="c9c07-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="c9c07-109">Merhaba NSG ön uç NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9c07-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="c9c07-110">toocreate hello **NSG ön uç** NSG hello senaryoda yukarıdaki gösterildiği gibi hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c9c07-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="c9c07-111">Tarayıcıdan toohttp://portal.azure.com gidin ve gerekiyorsa Azure hesabınıza.</span><span class="sxs-lookup"><span data-stu-id="c9c07-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c9c07-112">Tıklatın **Gözat >** > **ağ güvenlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Azure portal - Nsg'ler](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="c9c07-114">Merhaba, **ağ güvenlik grupları** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Azure portal - Nsg'ler](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="c9c07-116">Merhaba, **oluşturma ağ güvenlik grubu** dikey penceresinde adlı bir NSG oluşturma *NSG ön uç* hello içinde *RG NSG* kaynak grubu ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Azure portal - Nsg'ler](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="c9c07-118">Mevcut bir NSG’de kurallar oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9c07-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="c9c07-119">Varolan bir NSG hello Azure Portalı'ndan toocreate kurallarında hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c9c07-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="c9c07-120">Tıklatın **Gözat >** > **ağ güvenlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="c9c07-121">Nsg'ler Hello listesinde tıklayın **NSG ön uç** > **gelen güvenlik kuralları**</span><span class="sxs-lookup"><span data-stu-id="c9c07-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Azure portal - NSG ön uç](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="c9c07-123">Merhaba listesinde **gelen güvenlik kuralları**, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Azure portal - Kuralı Ekle](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="c9c07-125">Merhaba, **gelen Güvenlik Kuralı Ekle** dikey penceresinde adlı bir kural oluşturmak *web kuralı* önceliğini ile *200* aracılığıyla erişime izin verme *TCP* tooport *80* tooany VM herhangi kaynağı ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="c9c07-126">Bu ayarların çoğu varsayılan değerleri zaten olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c9c07-126">Notice that most of these settings are default values already.</span></span>
   
    ![Azure portal - kural ayarları](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="c9c07-128">Birkaç saniye sonra hello yeni hello NSG kuralında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c9c07-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Azure portalı - yeni kural](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="c9c07-130">Arasındaki adımları yineleyin too6 toocreate adlı bir gelen kuralı *rdp kural* önceliği *250* aracılığıyla erişime izin verme *TCP* tooport *3389* tooany herhangi bir kaynaktan VM.</span><span class="sxs-lookup"><span data-stu-id="c9c07-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="c9c07-131">Merhaba NSG toohello ön uç alt ağını ilişkilendirin</span><span class="sxs-lookup"><span data-stu-id="c9c07-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="c9c07-132">Tıklatın **Gözat >** > **kaynak grupları** > **RG NSG**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="c9c07-133">Merhaba, **RG NSG** dikey penceresinde tıklatın **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Azure portal - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="c9c07-135">Merhaba, **ayarları** dikey penceresinde tıklatın **alt ağlar** > **ön uç** > **ağ güvenlik grubu**  >  **NSG ön uç**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Azure portal - alt ağ ayarları](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="c9c07-137">Merhaba, **ön uç** dikey penceresinde tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c9c07-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Azure portal - alt ağ ayarları](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="c9c07-139">Merhaba NSG arka uç NSG oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9c07-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="c9c07-140">toocreate hello **NSG arka uç** NSG ve toohello ilişkilendirmek **arka uç** alt ağ, aşağıdaki hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c9c07-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="c9c07-141">Yineleme başlangıç adımları [oluşturma hello NSG ön uç NSG](#Create-the-NSG-FrontEnd-NSG) toocreate adlı bir NSG *NSG arka uç*</span><span class="sxs-lookup"><span data-stu-id="c9c07-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="c9c07-142">Yineleme başlangıç adımları [içinde varolan bir NSG kuralları oluşturma](#Create-rules-in-an-existing-NSG) toocreate hello **gelen** hello tabloda kurallarında.</span><span class="sxs-lookup"><span data-stu-id="c9c07-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="c9c07-143">Gelen kuralı</span><span class="sxs-lookup"><span data-stu-id="c9c07-143">Inbound rule</span></span> | <span data-ttu-id="c9c07-144">Giden kuralı</span><span class="sxs-lookup"><span data-stu-id="c9c07-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Azure portal - gelen kuralı](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Azure portal - giden kuralı](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="c9c07-147">Yineleme başlangıç adımları [hello NSG toohello ön uç alt ağını ilişkilendirin](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG arka uç** NSG toohello **arka uç** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="c9c07-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c07-148">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c9c07-148">Next Steps</span></span>
* <span data-ttu-id="c9c07-149">Nasıl çok öğrenin[varolan Nsg'ler yönetme](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c9c07-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="c9c07-150">[Günlük kaydını etkinleştir](virtual-network-nsg-manage-log.md) Nsg'ler için.</span><span class="sxs-lookup"><span data-stu-id="c9c07-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

