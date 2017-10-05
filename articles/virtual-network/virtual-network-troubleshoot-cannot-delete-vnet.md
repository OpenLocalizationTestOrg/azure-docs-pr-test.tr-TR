---
title: "Azure sanal ağında silemezsiniz | Microsoft Docs"
description: "Azure sanal ağında silemezsiniz sorunu gidermek öğrenin."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: 55c42a91bb1c5fad289b975ffae8ce4d6e7343dd
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="troubleshooting-failed-to-delete-a-virtual-network-in-azure"></a><span data-ttu-id="db186-103">Sorun giderme: Azure sanal ağ silinemedi</span><span class="sxs-lookup"><span data-stu-id="db186-103">Troubleshooting: Failed to delete a virtual network in Azure</span></span>

<span data-ttu-id="db186-104">Microsoft Azure sanal ağında silmeye çalıştığınızda hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db186-104">You might receive errors when you try to delete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="db186-105">Bu makalede, bu sorunu gidermenize yardımcı olmak için sorun giderme adımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="db186-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="db186-106">Sorun giderme rehberi</span><span class="sxs-lookup"><span data-stu-id="db186-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="db186-107">[Bir sanal ağ geçidi sanal ağda çalışır durumda olup olmadığını denetleyin](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="db186-107">[Check whether a virtual network gateway is running in the virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="db186-108">[Bir uygulama ağ geçidi sanal ağda çalışır durumda olup olmadığını denetleyin](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="db186-108">[Check whether an application gateway is running in the virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="db186-109">[Azure Active Directory etki alanı hizmeti sanal ağında etkinleştirilip etkinleştirilmediğini kontrol](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="db186-109">[Check whether Azure Active Directory Domain Service is enabled in the virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="db186-110">[Sanal ağ diğer kaynağa bağlı olup olmadığını denetleyin](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="db186-110">[Check whether the virtual network is connected to other resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="db186-111">[Bir sanal makinenin sanal ağda hala çalışıp çalışmadığını denetleyin](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="db186-111">[Check whether a virtual machine is still running in the virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="db186-112">[Sanal ağ içinde geçiş takıldı olup olmadığını denetleyin](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="db186-112">[Check whether the virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="db186-113">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="db186-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="db186-114">Bir sanal ağ geçidi sanal ağda çalışır durumda olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="db186-114">Check whether a virtual network gateway is running in the virtual network</span></span>

<span data-ttu-id="db186-115">Sanal ağı kaldırmak için öncelikle sanal ağ geçidi kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db186-115">To remove the virtual network, you must first remove the virtual network gateway.</span></span>

<span data-ttu-id="db186-116">Klasik sanal ağlar için Git **genel bakış** Azure portalında bir Klasik sanal ağının sayfası.</span><span class="sxs-lookup"><span data-stu-id="db186-116">For classic virtual networks, go to the **Overview** page of the classic virtual network in the Azure portal.</span></span> <span data-ttu-id="db186-117">İçinde **VPN bağlantıları** bölümünde, ağ geçidi sanal ağda çalışıyorsa, ağ geçidinin IP adresi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="db186-117">In the **VPN connections** section, if the gateway is running in the virtual network, you will see the IP address of the gateway.</span></span> 

![Ağ geçidi çalışır durumda olup olmadığını denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="db186-119">Sanal ağlar için Git **genel bakış** sanal ağın sayfası.</span><span class="sxs-lookup"><span data-stu-id="db186-119">For virtual networks, go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="db186-120">Denetleme **bağlı cihazları** sanal ağ geçidi için.</span><span class="sxs-lookup"><span data-stu-id="db186-120">Check **Connected devices** for the virtual network gateway.</span></span>

![Bağlı bir aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="db186-122">Ağ geçidi kaldırmadan önce ilk herhangi kaldırın **bağlantı** ağ geçidi nesneleri.</span><span class="sxs-lookup"><span data-stu-id="db186-122">Before you can remove the gateway, first remove any **Connection** objects in the gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-the-virtual-network"></a><span data-ttu-id="db186-123">Bir uygulama ağ geçidi sanal ağda çalışır durumda olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="db186-123">Check whether an application gateway is running in the virtual network</span></span>

<span data-ttu-id="db186-124">Git **genel bakış** sanal ağın sayfası.</span><span class="sxs-lookup"><span data-stu-id="db186-124">Go to the **Overview** page of the virtual network.</span></span> <span data-ttu-id="db186-125">Denetleme **bağlı cihazları** uygulama ağ geçidi için.</span><span class="sxs-lookup"><span data-stu-id="db186-125">Check the **Connected devices** for the application gateway.</span></span>

![Bağlı bir aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="db186-127">Bir uygulama ağ geçidi varsa, sanal ağı silmeden önce onu kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db186-127">If there is an application gateway, you must remove it before you can delete the virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network"></a><span data-ttu-id="db186-128">Azure Active Directory etki alanı hizmeti sanal ağda etkin olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="db186-128">Check whether Azure Active Directory Domain Service is enabled in the virtual network</span></span>

<span data-ttu-id="db186-129">Active Directory etki alanı hizmeti etkin ve sanal ağa bağlı değilse, bu sanal ağ silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="db186-129">If the Active Directory Domain Service is enabled and connected to the virtual network, you cannot delete this virtual network.</span></span> 

![Bağlı bir aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="db186-131">Hizmetini devre dışı bırakmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="db186-131">To disable the service, follow these steps:</span></span>

1. <span data-ttu-id="db186-132">[Klasik Azure portalı](https://manage.windowsazure.com)'na gidin.</span><span class="sxs-lookup"><span data-stu-id="db186-132">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="db186-133">Sol bölmede seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="db186-133">In the left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="db186-134">Active Directory etki alanı hizmeti etkin olan Azure Active Directory (Azure AD) dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="db186-134">Select the Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="db186-135">**Configure (Yapılandır)** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="db186-135">Select the **Configure** tab.</span></span>
5. <span data-ttu-id="db186-136">Altında **etki alanı Hizmetleri**, değiştirme **bu dizin için etki alanı Hizmetleri'ni etkinleştirme** için seçenek **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="db186-136">Under **domain services**, change the **Enable domain services for this directory** option to **No**.</span></span>  

### <a name="check-whether-the-virtual-network-is-connected-to-other-resource"></a><span data-ttu-id="db186-137">Sanal ağ diğer kaynağa bağlı olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="db186-137">Check whether the virtual network is connected to other resource</span></span>

<span data-ttu-id="db186-138">Bağlantı hattı bağlantıları, bağlantıları ve sanal ağ eşlemesi bulunabilir denetleyin.</span><span class="sxs-lookup"><span data-stu-id="db186-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="db186-139">Bunlardan herhangi bir sanal ağ silme başarısız olmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="db186-139">Any of these can cause a virtual network deletion to fail.</span></span> 

<span data-ttu-id="db186-140">Önerilen silme sipariş aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="db186-140">The recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="db186-141">Ağ Geçidi bağlantıları</span><span class="sxs-lookup"><span data-stu-id="db186-141">Gateway connections</span></span>
2. <span data-ttu-id="db186-142">Ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="db186-142">Gateways</span></span>
3. <span data-ttu-id="db186-143">IP'leri</span><span class="sxs-lookup"><span data-stu-id="db186-143">IPs</span></span>
4. <span data-ttu-id="db186-144">Sanal Ağ eşlemesi bulunabilir</span><span class="sxs-lookup"><span data-stu-id="db186-144">Virtual network peerings</span></span>
5. <span data-ttu-id="db186-145">Uygulama hizmeti ortamı (ana)</span><span class="sxs-lookup"><span data-stu-id="db186-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-the-virtual-network"></a><span data-ttu-id="db186-146">Bir sanal makinenin sanal ağda hala çalışıp çalışmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="db186-146">Check whether a virtual machine is still running in the virtual network</span></span>

<span data-ttu-id="db186-147">Hiçbir sanal makinenin sanal ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="db186-147">Make sure that no virtual machine is in the virtual network.</span></span>

### <a name="check-whether-the-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="db186-148">Sanal ağ içinde geçiş takıldı olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="db186-148">Check whether the virtual network is stuck in migration</span></span>

<span data-ttu-id="db186-149">Sanal ağı geçiş durumunda takılıyorsa silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="db186-149">If the virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="db186-150">Geçiş işlemi iptal etmek için aşağıdaki komutu çalıştırın ve sanal ağ silin.</span><span class="sxs-lookup"><span data-stu-id="db186-150">Run the following command to abort the migration, and then delete the virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="db186-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db186-151">Next steps</span></span>

- [<span data-ttu-id="db186-152">Azure Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="db186-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="db186-153">Azure Sanal Ağ hakkında sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="db186-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)