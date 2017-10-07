---
title: "Birden çok VPN ağ geçidi siteden siteye bağlantıları tooa VNet ekleyin: Azure Portal: Resource Manager | Microsoft Docs"
description: "Varolan bir bağlantıyı sahip çok siteli S2S bağlantıları tooa VPN ağ geçidi Ekle"
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
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="e8183-103">Mevcut bir VPN ağ geçidi bağlantısı olan bir siteden siteye bağlantı tooa VNet ekleme</span><span class="sxs-lookup"><span data-stu-id="e8183-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8183-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e8183-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e8183-105">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="e8183-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="e8183-106">Bu makalede, varolan bir bağlantıyı sahip hello Azure portal tooadd siteden siteye (S2S) bağlantıları tooa VPN ağ geçidi kullanılarak üzerinden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e8183-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="e8183-107">Bu tür bir bağlantı başvurulan tooas "çok siteli" yapılandırma görülür.</span><span class="sxs-lookup"><span data-stu-id="e8183-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="e8183-108">S2S bağlantısı tooa S2S bağlantısı, noktadan siteye bağlantı veya VNet-VNet bağlantısı zaten VNet ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8183-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="e8183-109">Bağlantıları eklerken, bazı sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="e8183-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="e8183-110">Merhaba denetleyin [başlamadan önce](#before) yapılandırmanıza başlamadan önce bu makale tooverify bölümünde.</span><span class="sxs-lookup"><span data-stu-id="e8183-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="e8183-111">Bu makale RouteBased VPN ağ geçidine sahip hello Resource Manager dağıtım modeli kullanılarak oluşturulan tooVNets geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e8183-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="e8183-112">Bu adımları tooExpressRoute /-siteye eşzamanlı bağlantı yapılandırmaları geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="e8183-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="e8183-113">Bkz: [ExpressRoute/S2S arada var olabilen bağlantılar](../expressroute/expressroute-howto-coexist-resource-manager.md) arada var olabilen bağlantılar hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e8183-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="e8183-114">Dağıtım modelleri ve yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e8183-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="e8183-115">Bu tabloda yeni makaleler olarak güncelleştiriyoruz ve ek araçlar bu yapılandırma için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e8183-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="e8183-116">Bir makale kullanılabilir olduğunda sizi doğrudan bu tablodan tooit bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e8183-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="e8183-117"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="e8183-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="e8183-118">Aşağıdaki öğelerindeki hello doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="e8183-118">Verify hello following items:</span></span>

* <span data-ttu-id="e8183-119">Bir ExpressRoute/S2S eşzamanlı bağlantı oluşturma değil.</span><span class="sxs-lookup"><span data-stu-id="e8183-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="e8183-120">Varolan bir bağlantı hello Resource Manager dağıtım modeli kullanılarak oluşturulmuş bir sanal ağ var.</span><span class="sxs-lookup"><span data-stu-id="e8183-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="e8183-121">Merhaba sanal ağ geçidi Vnet'inizi için RouteBased ' dir.</span><span class="sxs-lookup"><span data-stu-id="e8183-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="e8183-122">PolicyBased VPN ağ geçidi varsa, hello sanal ağ geçidini silin ve yeni bir VPN ağ geçidi RouteBased olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e8183-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="e8183-123">Herhangi bir hello bu VNet bağlandığı sanal ağlar için hello adres aralıklarını hiçbiri çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="e8183-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="e8183-124">Uyumlu VPN cihazı ve mümkün tooconfigure olan birisi sahip onu.</span><span class="sxs-lookup"><span data-stu-id="e8183-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="e8183-125">Bkz. [VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="e8183-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="e8183-126">VPN Cihazınızı yapılandırmak konusunda veya şirket içi ağ yapılandırmanızda bulunan hello IP adresi aralıklarıyla ilgili bilginiz varsa, bu detayları sizin için sağlayabilecek biriyle toocoordinate gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8183-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="e8183-127">VPN cihazınız için dışarıya dönük bir genel IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="e8183-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="e8183-128">Bu IP adresi bir NAT’nin arkasında olamaz.</span><span class="sxs-lookup"><span data-stu-id="e8183-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="e8183-129"><a name="part1"></a>Bölüm 1 - bir bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e8183-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="e8183-130">Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve gerekiyorsa Azure hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e8183-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="e8183-131">Tıklatın **tüm kaynakları** ve bulun, **sanal ağ geçidi** kaynakları hello listesinden ve tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e8183-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="e8183-132">Merhaba üzerinde **sanal ağ geçidi** dikey penceresinde tıklatın **bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="e8183-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="e8183-133">![Bağlantılar dikey penceresi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="e8183-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="e8183-134">Merhaba üzerinde **bağlantıları** dikey penceresinde tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e8183-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="e8183-135">![Add bağlantı düğmesini](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Ekle bağlantı düğmesi")</span><span class="sxs-lookup"><span data-stu-id="e8183-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="e8183-136">Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde, aşağıdaki alanları hello doldururken:</span><span class="sxs-lookup"><span data-stu-id="e8183-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="e8183-137">**Ad:** toogive toohello site hello bağlantı oluşturmakta istediğiniz hello adı.</span><span class="sxs-lookup"><span data-stu-id="e8183-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="e8183-138">**Bağlantı türü:** seçin **siteden siteye (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="e8183-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="e8183-139">![Ekle bağlantı dikey](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Ekle bağlantı dikey")</span><span class="sxs-lookup"><span data-stu-id="e8183-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="e8183-140"><a name="part2"></a>Bölüm 2 - bir yerel ağ geçidi ekleme</span><span class="sxs-lookup"><span data-stu-id="e8183-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="e8183-141">Tıklatın **yerel ağ geçidi** ***bir yerel ağ geçidi seçin***.</span><span class="sxs-lookup"><span data-stu-id="e8183-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="e8183-142">Bu hello açar **Seç yerel ağ geçidi** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8183-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="e8183-143">![Seç yerel ağ geçidi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Seç yerel ağ geçidi")</span><span class="sxs-lookup"><span data-stu-id="e8183-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="e8183-144">Tıklatın **Yeni Oluştur** tooopen hello **oluşturma yerel ağ geçidi** dikey.</span><span class="sxs-lookup"><span data-stu-id="e8183-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="e8183-145">![Create yerel ağ geçidi dikey](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "oluşturma yerel ağ geçidi")</span><span class="sxs-lookup"><span data-stu-id="e8183-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="e8183-146">Merhaba üzerinde **oluşturma yerel ağ geçidi** dikey penceresinde, aşağıdaki alanları hello doldururken:</span><span class="sxs-lookup"><span data-stu-id="e8183-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="e8183-147">**Ad:** toogive toohello yerel ağ geçidi kaynağı istediğiniz hello adı.</span><span class="sxs-lookup"><span data-stu-id="e8183-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="e8183-148">**IP adresi:** hello tooconnect için istediğiniz hello sitesinde hello VPN cihazının genel IP adresi.</span><span class="sxs-lookup"><span data-stu-id="e8183-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="e8183-149">**Adres alanı:** toobe istediğiniz hello adres alanı toohello yeni yerel ağ sitesi yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e8183-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="e8183-150">Tıklatın **Tamam** hello üzerinde **oluşturma yerel ağ geçidi** dikey toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="e8183-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="e8183-151"><a name="part3"></a>3 Kısım - hello paylaşılan anahtar ekleme ve hello bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8183-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="e8183-152">Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde hello paylaşılan anahtar bağlantınızı toouse toocreate istediğiniz ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e8183-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="e8183-153">Ya da VPN aygıtınızdan hello paylaşılan anahtar alın veya bir burada yapabilir ve VPN cihaz toouse hello yapılandırmak aynı paylaşılan anahtar.</span><span class="sxs-lookup"><span data-stu-id="e8183-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="e8183-154">Merhaba hello anahtarlarının tam olarak olduğunu şeydir önemli hello aynı.</span><span class="sxs-lookup"><span data-stu-id="e8183-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="e8183-155">![Paylaşılan anahtar](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="e8183-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="e8183-156">Merhaba dikey penceresinde Hello altındaki tıklatın **Tamam** toocreate hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e8183-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="e8183-157"><a name="part4"></a>4 Kısım - hello VPN bağlantısını doğrulama</span><span class="sxs-lookup"><span data-stu-id="e8183-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e8183-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8183-158">Next steps</span></span>

<span data-ttu-id="e8183-159">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8183-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="e8183-160">Merhaba sanal makineleri görmek [öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e8183-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
