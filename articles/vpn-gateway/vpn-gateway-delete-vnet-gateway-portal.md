---
title: "Bir sanal ağ geçidini silmek: Azure portal: Resource Manager | Microsoft Docs"
description: "Resource Manager dağıtım modelinde Azure portalını kullanarak bir sanal ağ geçidini silin."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="14bcf-103">Portalı kullanarak bir sanal ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="14bcf-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="14bcf-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="14bcf-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="14bcf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14bcf-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="14bcf-106">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="14bcf-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="14bcf-107">Birkaç VPN ağ geçidi yapılandırması için bir sanal ağ geçidi silmek istediğinizde uygulayabileceğiniz çeşitli yaklaşımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="14bcf-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="14bcf-108">Her şeyi silin ve üzerinde bir test ortamı durumda olduğu gibi başlatmak istiyorsanız, kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14bcf-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="14bcf-109">Bir kaynak grubunu silmek gruptaki tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="14bcf-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="14bcf-110">Bu yöntem olduğundan tüm kaynakların kaynak grubunda saklamak istemiyorsanız yalnızca önerilir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="14bcf-111">Bu yaklaşımı kullanarak yalnızca birkaç kaynakları seçmeli olarak silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="14bcf-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="14bcf-112">Bazı kaynakların kaynak grubunda tutmak istiyorsanız, bir sanal ağ geçidi silinmesi biraz daha karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="14bcf-113">Sanal ağ geçidi silmeden önce ağ geçidinde bağımlı herhangi bir kaynağa silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="14bcf-114">İzleyeceğiniz adımlar oluşturduğunuz bağlantı türünü ve her bağlantı için bağımlı kaynakları bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="14bcf-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="14bcf-115">VPN ağ geçidi silme</span><span class="sxs-lookup"><span data-stu-id="14bcf-115">Delete a VPN gateway</span></span>

<span data-ttu-id="14bcf-116">Bir sanal ağ geçidi silmek için önce sanal ağ geçidi için ilgili her bir kaynağın silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="14bcf-117">Belirli bir sırada bağımlılıkları nedeniyle kaynakları silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="14bcf-118">Bu noktada, sanal ağ geçidi silinir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="14bcf-119">Sonraki adımlar artık kullanılmakta olan tüm kaynakları silmesini yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="14bcf-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="14bcf-120">Yerel ağ geçidi silmek için</span><span class="sxs-lookup"><span data-stu-id="14bcf-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="14bcf-121">İçinde **tüm kaynakları**, her bağlantı ile ilişkili yerel ağ geçitleri bulun.</span><span class="sxs-lookup"><span data-stu-id="14bcf-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="14bcf-122">Üzerinde **genel bakış** yerel ağ geçidi için dikey tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="14bcf-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="14bcf-123">Ağ geçidi için genel IP adresi kaynağı silmek için</span><span class="sxs-lookup"><span data-stu-id="14bcf-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="14bcf-124">İçinde **tüm kaynakları**, ağ geçidi için ilişkili ortak IP adresi kaynağı bulun.</span><span class="sxs-lookup"><span data-stu-id="14bcf-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="14bcf-125">Sanal ağ geçidi etkin-etkin iki genel IP adresleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="14bcf-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="14bcf-126">Üzerinde **genel bakış** sayfasında için genel IP adresi, **silmek**, ardından **Evet** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="14bcf-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="14bcf-127">Ağ geçidi alt ağını silmek için</span><span class="sxs-lookup"><span data-stu-id="14bcf-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="14bcf-128">İçinde **tüm kaynakları**, sanal ağ bulun.</span><span class="sxs-lookup"><span data-stu-id="14bcf-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="14bcf-129">Üzerinde **alt ağlar** dikey penceresinde tıklatın **GatewaySubnet**, ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="14bcf-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="14bcf-130">Tıklatın **Evet** ağ geçidi alt ağı silmek istediğinizi onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="14bcf-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="14bcf-131"><a name="deleterg"></a>Kaynak grubunu silerek bir VPN ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="14bcf-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="14bcf-132">Kaynak grubunda kaynaklarınızın hiçbirini saklanması ilgili değildir ve baştan başlamak istiyorsanız, tüm kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14bcf-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="14bcf-133">Bu, her şeyi kaldırmak için hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="14bcf-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="14bcf-134">Aşağıdaki adımlar yalnızca Resource Manager dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="14bcf-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="14bcf-135">İçinde **tüm kaynakları**, kaynak grubunu bulun ve dikey penceresini açmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="14bcf-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="14bcf-136">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="14bcf-136">Click **Delete**.</span></span> <span data-ttu-id="14bcf-137">Delete dikey penceresinde, etkilenen kaynakları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="14bcf-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="14bcf-138">Tüm bu kaynaklar silmek istediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="14bcf-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="14bcf-139">Aksi takdirde, içindeki adımları kullanın [bir VPN ağ geçidi silmek](#deletegw) bu makalenin üst.</span><span class="sxs-lookup"><span data-stu-id="14bcf-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="14bcf-140">Devam etmek için silin ve ardından istediğiniz kaynak grubunun adını yazın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="14bcf-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>