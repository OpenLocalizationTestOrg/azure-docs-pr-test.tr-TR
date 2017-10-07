---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: Azure portal | Microsoft Docs"
description: "Bu belge nasıl (Vnet'ler) tooExpressRoute devreler toolink sanal ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="20f59-103">Sanal ağ tooan expressroute bağlantı hattı Bağlan</span><span class="sxs-lookup"><span data-stu-id="20f59-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20f59-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="20f59-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="20f59-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20f59-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="20f59-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="20f59-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="20f59-107">Video - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="20f59-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="20f59-108">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="20f59-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="20f59-109">Bu makalede hello Resource Manager dağıtım modeli kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute bağlantı hatları bağlama ve Azure portal hello yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="20f59-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="20f59-110">Sanal ağlar olabilir ya da hello aynı abonelik veya başka bir abonelik parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="20f59-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="20f59-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="20f59-111">Before you begin</span></span>
* <span data-ttu-id="20f59-112">Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="20f59-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="20f59-113">Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20f59-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="20f59-114">Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve bağlantı sağlayıcınız tarafından etkinleştirilmiş hello hattı sahip.</span><span class="sxs-lookup"><span data-stu-id="20f59-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="20f59-115">Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20f59-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="20f59-116">Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-portal-resource-manager.md) yönlendirme yönergeleri için makalenin.</span><span class="sxs-lookup"><span data-stu-id="20f59-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="20f59-117">Azure özel eşleme yapılandırılır ve uçtan uca bağlantı etkinleştirebilmeniz için ağınız ve Microsoft arasında hello BGP eşliği yukarı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20f59-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="20f59-118">Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20f59-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="20f59-119">Çok olarak Hello yönergeleri[ExpressRoute için bir sanal ağ geçidi oluşturmak](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="20f59-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="20f59-120">ExpressRoute için bir sanal ağ geçidi hello GatewayType 'ExpressRoute' değil VPN kullanır.</span><span class="sxs-lookup"><span data-stu-id="20f59-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="20f59-121">Too10 sanal ağlar tooa standart expressroute bağlantı hattı bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="20f59-122">Tüm sanal ağları hello olmalıdır standart bir expressroute bağlantı hattını kullanırken aynı coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="20f59-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="20f59-123">Bir sanal ağ dışında hello coğrafi bölge hello expressroute bağlantı hattı, bağlantı veya çok sayıda sanal ağlar tooyour expressroute bağlantı hattı hello ExpressRoute premium eklentisi etkinse bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="20f59-124">Merhaba denetleyin [SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="20f59-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="20f59-125">Yapabilecekleriniz [bir video izlemek](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) başına toobetter anlamak önce hello adımları.</span><span class="sxs-lookup"><span data-stu-id="20f59-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="20f59-126">Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı</span><span class="sxs-lookup"><span data-stu-id="20f59-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="20f59-127">toocreate bağlantı</span><span class="sxs-lookup"><span data-stu-id="20f59-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="20f59-128">BGP yapılandırma bilgilerini hello Katman 3 sağlayıcısı, eşlemeler yapılandırılıp yapılandırılmadığını gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="20f59-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="20f59-129">Bağlantı hattınız sağlanan durumdaysa mümkün toocreate bağlantıları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20f59-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="20f59-130">Expressroute bağlantı hattı ve Azure özel eşleme başarılı bir şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="20f59-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="20f59-131">Merhaba yönergeleri izleyin [bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="20f59-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="20f59-132">Expressroute bağlantı hattı hello görüntü aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="20f59-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![ExpressRoute bağlantı hattı ekran görüntüsü](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="20f59-134">Sanal ağ geçidi tooyour expressroute bağlantı hattı bağlantı toolink sağlama şimdi başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="20f59-135">Tıklatın **bağlantı** > **Ekle** tooopen hello **Bağlantı Ekle** dikey penceresinde ve başlangıç değerleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="20f59-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Bağlantı ekran Ekle](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="20f59-137">Bağlantınızı başarıyla yapılandırıldıktan sonra bağlantı nesnesi hello bağlantısı için hello bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="20f59-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Bağlantı nesnesi ekran görüntüsü](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="20f59-139">toodelete bağlantı</span><span class="sxs-lookup"><span data-stu-id="20f59-139">toodelete a connection</span></span>
<span data-ttu-id="20f59-140">Bir bağlantı hello seçerek silebilirsiniz **silmek** hello dikey bağlantınız için simge.</span><span class="sxs-lookup"><span data-stu-id="20f59-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="20f59-141">Farklı bir abonelik tooa hattı sanal bir ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="20f59-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="20f59-142">Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="20f59-143">Aşağıdaki Hello şekilde birden çok abonelik arasında basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="20f59-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="20f59-145">Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir.</span><span class="sxs-lookup"><span data-stu-id="20f59-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="20f59-146">Hizmetlerini dağıtmak için her hello kuruluşunuz içinde hello bölümlerin kendi abonelik kullanabilirsiniz, ancak tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="20f59-147">Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="20f59-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="20f59-148">Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="20f59-149">Bağlantı ve bant genişliği ücretleri ayrılmış hello hattı için uygulanan toohello ExpressRoute bağlantı hattı sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="20f59-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="20f59-150">Tüm sanal ağları hello paylaşmak aynı bant genişliği.</span><span class="sxs-lookup"><span data-stu-id="20f59-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="20f59-151">Yönetim - hattı sahipleri ve hattı kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="20f59-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="20f59-152">Merhaba 'devre sahibinden' hello ExpressRoute bağlantı hattı kaynak yetkili bir güç kullanıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="20f59-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="20f59-153">Merhaba devre sahibinden 'hattı kullanıcılar tarafından kullanılan yetkilerini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="20f59-154">Bağlantı hattı kullanıcılardır sahipleri sanal ağ içinde olmayan ağ geçitleri, expressroute bağlantı hattı hello gibi aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="20f59-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="20f59-155">Bağlantı hattı kullanıcıların yetkilerini (sanal ağ başına bir yetkilendirme) kullanmak.</span><span class="sxs-lookup"><span data-stu-id="20f59-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="20f59-156">Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir.</span><span class="sxs-lookup"><span data-stu-id="20f59-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="20f59-157">Bir yetkilendirme sonuçlarına tüm bağlantı erişimini iptal edildi hello abonelikten silinmesini iptal ediliyor.</span><span class="sxs-lookup"><span data-stu-id="20f59-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="20f59-158">Bağlantı hattı sahibi işlemleri</span><span class="sxs-lookup"><span data-stu-id="20f59-158">Circuit owner operations</span></span>

<span data-ttu-id="20f59-159">**toocreate Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="20f59-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="20f59-160">Merhaba devre sahibinden bir yetkilendirme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="20f59-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="20f59-161">Bu olabilir bir yetkilendirme anahtarı hello oluşturulmasında sonuçları kendi sanal ağ ağ geçitleri toohello expressroute bağlantı hattı kullanıcı tooconnect tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="20f59-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="20f59-162">Bir yetkilendirme yalnızca bir bağlantı için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="20f59-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="20f59-163">Merhaba ExpressRoute dikey penceresinde tıklayın **yetkilerini** ve ardından bir **adı** hello yetkilendirme ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="20f59-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Yetkileri değiştirme](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="20f59-165">Merhaba Hello yapılandırma kaydedildikten sonra kopyalama **kaynak kimliği** ve hello **yetkilendirme anahtarının**.</span><span class="sxs-lookup"><span data-stu-id="20f59-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Yetkilendirme anahtarı](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="20f59-167">**toodelete Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="20f59-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="20f59-168">Bir bağlantı hello seçerek silebilirsiniz **silmek** hello dikey bağlantınız için simge.</span><span class="sxs-lookup"><span data-stu-id="20f59-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="20f59-169">Bağlantı hattı kullanıcı işlemleri</span><span class="sxs-lookup"><span data-stu-id="20f59-169">Circuit user operations</span></span>

<span data-ttu-id="20f59-170">Merhaba hattı kullanıcı hello kaynak kimliği ile Merhaba devre sahibinden yetkilendirme anahtarından gerekir.</span><span class="sxs-lookup"><span data-stu-id="20f59-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="20f59-171">**tooredeem Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="20f59-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="20f59-172">Merhaba tıklatın **+ yeni** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="20f59-172">Click hello **+New** button.</span></span>

    ![Yeni'yi tıklatın](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="20f59-174">Arama **"Bağlantı"** hello Market, seçin ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20f59-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Bağlantı için arama](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="20f59-176">Merhaba emin olun **bağlantı türü** çok Ayarla "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="20f59-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="20f59-177">Merhaba ayrıntıları doldurun ve ardından **Tamam** hello temel bilgileri dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="20f59-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Temel Bilgiler dikey penceresi](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="20f59-179">Merhaba, **ayarları** dikey penceresinde, Select hello **sanal ağ geçidi** ve hello denetleyin **yetkilendirme kullanmak** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="20f59-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="20f59-180">Merhaba girin **yetkilendirme anahtar** ve hello **hattı URI eş** ve hello bağlantı bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="20f59-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="20f59-181">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20f59-181">Click **OK**.</span></span>

    ![Ayarlar dikey penceresi](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="20f59-183">Merhaba hello bilgileri gözden **Özet** tıklayın ve dikey **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="20f59-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="20f59-184">**toorelease Bağlantı Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="20f59-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="20f59-185">Bir yetkilendirme hello ExpressRoute bağlantı hattı toohello sanal ağ bağlantıları hello bağlantı silerek serbest bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20f59-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20f59-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20f59-186">Next steps</span></span>
<span data-ttu-id="20f59-187">ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="20f59-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
