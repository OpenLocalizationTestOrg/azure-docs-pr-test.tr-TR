---
title: "Birden çok VPN ağ geçidi siteden siteye bağlantıları bir Vnet'e eklenecek: Azure Portal: Resource Manager | Microsoft Docs"
description: "Çok siteli S2S bağlantılarının varolan bir bağlantıyı içeren bir VPN ağ geçidi eklemek"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: 7ec57789ee76f4ec54e4f7b68ea75c19522f3d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="a865f-103">Mevcut bir VPN ağ geçidi bağlantısı olan bir sanal ağa bir siteden siteye bağlantı Ekle</span><span class="sxs-lookup"><span data-stu-id="a865f-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a865f-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a865f-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="a865f-105">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="a865f-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="a865f-106">Bu makalede, siteden siteye (S2S) bağlantıları varolan bir bağlantıyı sahip bir VPN ağ geçidi eklemek için Azure portal'ı kullanma aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a865f-106">This article walks you through using the Azure portal to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="a865f-107">Bu bağlantı türü genellikle "çok siteli" yapılandırma olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="a865f-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="a865f-108">S2S bağlantısı, noktadan siteye bağlantı veya VNet-VNet bağlantı zaten bir sanal ağa S2S bağlantısı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a865f-108">You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="a865f-109">Bağlantıları eklerken, bazı sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="a865f-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="a865f-110">Denetleme [başlamadan önce](#before) yapılandırmanıza başlamadan önce doğrulamak için bu makaledeki bölümü.</span><span class="sxs-lookup"><span data-stu-id="a865f-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span></span> 

<span data-ttu-id="a865f-111">Bu makale RouteBased VPN ağ geçidine sahip Resource Manager dağıtım modeli kullanılarak oluşturulan sanal ağlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a865f-111">This article applies to VNets created using the Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="a865f-112">Bu adımları ExpressRoute /-siteye eşzamanlı bağlantı yapılandırmaları için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="a865f-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="a865f-113">Bkz: [ExpressRoute/S2S arada var olabilen bağlantılar](../expressroute/expressroute-howto-coexist-resource-manager.md) arada var olabilen bağlantılar hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a865f-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="a865f-114">Dağıtım modelleri ve yöntemleri</span><span class="sxs-lookup"><span data-stu-id="a865f-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="a865f-115">Bu tabloda yeni makaleler olarak güncelleştiriyoruz ve ek araçlar bu yapılandırma için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="a865f-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="a865f-116">Bir makale kullanılabilir olduğunda sizi doğrudan bu tablodan bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a865f-116">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="a865f-117"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a865f-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="a865f-118">Aşağıdaki öğeleri doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="a865f-118">Verify the following items:</span></span>

* <span data-ttu-id="a865f-119">Bir ExpressRoute/S2S eşzamanlı bağlantı oluşturma değil.</span><span class="sxs-lookup"><span data-stu-id="a865f-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="a865f-120">Varolan bir bağlantı Resource Manager dağıtım modeli kullanılarak oluşturulmuş bir sanal ağ var.</span><span class="sxs-lookup"><span data-stu-id="a865f-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="a865f-121">RouteBased Vnet'inizi için sanal ağ geçididir.</span><span class="sxs-lookup"><span data-stu-id="a865f-121">The virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="a865f-122">PolicyBased VPN ağ geçidi varsa, sanal ağ geçidini silin ve yeni bir VPN ağ geçidi RouteBased olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a865f-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="a865f-123">Bu VNet bağlandığı sanal ağlar hiçbirini için adres aralıklarını hiçbiri çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="a865f-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="a865f-124">Uyumlu bir VPN cihazı ve onu yapılandırmanız mümkün olan birisi vardır.</span><span class="sxs-lookup"><span data-stu-id="a865f-124">You have compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="a865f-125">Bkz. [VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="a865f-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="a865f-126">VPN cihazınızı yapılandırma konusuyla veya şirket içi ağ yapılandırmanızdaki IP adresi aralıklarıyla ilgili fazla bilginiz yoksa size bu ayrıntıları sağlayabilecek biriyle çalışmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a865f-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="a865f-127">VPN cihazınız için dışarıya dönük bir genel IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="a865f-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="a865f-128">Bu IP adresi bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="a865f-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="a865f-129"><a name="part1"></a>Bölüm 1 - bir bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a865f-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="a865f-130">Tarayıcıdan [Azure portalına](http://portal.azure.com) gidin ve gerekiyorsa Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a865f-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="a865f-131">Tıklatın **tüm kaynakları** ve bulun, **sanal ağ geçidi** kaynakları listesinden ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a865f-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span></span>
3. <span data-ttu-id="a865f-132">Üzerinde **sanal ağ geçidi** dikey penceresinde tıklatın **bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="a865f-132">On the **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="a865f-133">![Bağlantıları dikey penceresi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="a865f-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="a865f-134">Üzerinde **bağlantıları** dikey penceresinde tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a865f-134">On the **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="a865f-135">![Bağlantı düğme ekleme](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span><span class="sxs-lookup"><span data-stu-id="a865f-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="a865f-136">Üzerinde **Bağlantı Ekle** dikey penceresinde, aşağıdaki alanlar doldururken:</span><span class="sxs-lookup"><span data-stu-id="a865f-136">On the **Add connection** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="a865f-137">**Ad:** bağlantısı oluşturmakta siteye vermek istediğiniz adı.</span><span class="sxs-lookup"><span data-stu-id="a865f-137">**Name:** The name you want to give to the site you are creating the connection to.</span></span>
   * <span data-ttu-id="a865f-138">**Bağlantı türü:** seçin **siteden siteye (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="a865f-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="a865f-139">![Bağlantı dikey ekleme](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span><span class="sxs-lookup"><span data-stu-id="a865f-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="a865f-140"><a name="part2"></a>Bölüm 2 - bir yerel ağ geçidi ekleme</span><span class="sxs-lookup"><span data-stu-id="a865f-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="a865f-141">Tıklatın **yerel ağ geçidi** ***bir yerel ağ geçidi seçin***.</span><span class="sxs-lookup"><span data-stu-id="a865f-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="a865f-142">Bu açılır **Seç yerel ağ geçidi** dikey.</span><span class="sxs-lookup"><span data-stu-id="a865f-142">This will open the **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="a865f-143">![Yerel ağ geçidi seçin](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span><span class="sxs-lookup"><span data-stu-id="a865f-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="a865f-144">Tıklatın **Yeni Oluştur** açmak için **oluşturma yerel ağ geçidi** dikey.</span><span class="sxs-lookup"><span data-stu-id="a865f-144">Click **Create new** to open the **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="a865f-145">![Yerel ağ geçidi Oluştur dikey penceresi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span><span class="sxs-lookup"><span data-stu-id="a865f-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="a865f-146">Üzerinde **oluşturma yerel ağ geçidi** dikey penceresinde, aşağıdaki alanlar doldururken:</span><span class="sxs-lookup"><span data-stu-id="a865f-146">On the **Create local network gateway** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="a865f-147">**Ad:** yerel ağ geçidi kaynağına vermek istediğiniz adı.</span><span class="sxs-lookup"><span data-stu-id="a865f-147">**Name:** The name you want to give to the local network gateway resource.</span></span>
   * <span data-ttu-id="a865f-148">**IP adresi:** bağlanmak istediğiniz siteye VPN cihazının genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="a865f-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span></span>
   * <span data-ttu-id="a865f-149">**Adres alanı:** yeni yerel ağ sitesine yönlendirilmesini istediğiniz adres alanı.</span><span class="sxs-lookup"><span data-stu-id="a865f-149">**Address space:** The address space that you want to be routed to the new local network site.</span></span>
4. <span data-ttu-id="a865f-150">Tıklatın **Tamam** üzerinde **oluşturma yerel ağ geçidi** değişiklikleri kaydetmek için dikey.</span><span class="sxs-lookup"><span data-stu-id="a865f-150">Click **OK** on the **Create local network gateway** blade to save the changes.</span></span>

## <span data-ttu-id="a865f-151"><a name="part3"></a>Bölüm 3 - paylaşılan anahtar ekleme ve bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a865f-151"><a name="part3"></a>Part 3 - Add the shared key and create the connection</span></span>
1. <span data-ttu-id="a865f-152">Üzerinde **Bağlantı Ekle** dikey penceresinde, bağlantı oluşturmak için kullanmak istediğiniz paylaşılan anahtar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a865f-152">On the **Add connection** blade, add the shared key that you want to use to create your connection.</span></span> <span data-ttu-id="a865f-153">VPN cihazınızın paylaşılan anahtarı alma veya bir burada olun ve aynı paylaşılan anahtarı kullanmak üzere VPN Cihazınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a865f-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span></span> <span data-ttu-id="a865f-154">Önemli şey anahtarları tam olarak aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="a865f-154">The important thing is that the keys are exactly the same.</span></span>
   
    <span data-ttu-id="a865f-155">![Paylaşılan anahtar](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="a865f-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="a865f-156">Dikey pencerenin alt kısmındaki tıklatın **Tamam** bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a865f-156">At the bottom of the blade, click **OK** to create the connection.</span></span>

## <span data-ttu-id="a865f-157"><a name="part4"></a>4 bölüm - VPN bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="a865f-157"><a name="part4"></a>Part 4 - Verify the VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a865f-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a865f-158">Next steps</span></span>

<span data-ttu-id="a865f-159">Bağlantınız tamamlandıktan sonra sanal ağlarınıza sanal makineler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a865f-159">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="a865f-160">Daha fazla bilgi için bkz. sanal makineleri [öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="a865f-160">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
