---
title: "aaaCannot Sil Azure sanal ağında | Microsoft Docs"
description: "Nasıl tootroubleshoot hello Azure sanal ağında silemezsiniz sorun hakkında bilgi edinin."
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
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a><span data-ttu-id="86dc0-103">Sorun giderme: toodelete Azure sanal ağında başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="86dc0-103">Troubleshooting: Failed toodelete a virtual network in Azure</span></span>

<span data-ttu-id="86dc0-104">Microsoft Azure sanal ağında toodelete çalıştığınızda hata alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86dc0-104">You might receive errors when you try toodelete a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="86dc0-105">Bu makalede, sorun giderme adımları toohelp sağlanmaktadır. Bu sorunu çözün.</span><span class="sxs-lookup"><span data-stu-id="86dc0-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a><span data-ttu-id="86dc0-106">Sorun giderme rehberi</span><span class="sxs-lookup"><span data-stu-id="86dc0-106">Troubleshooting guidance</span></span> 

1. <span data-ttu-id="86dc0-107">[Bir sanal ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="86dc0-107">[Check whether a virtual network gateway is running in hello virtual network](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).</span></span>
2. <span data-ttu-id="86dc0-108">[Bir uygulama ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="86dc0-108">[Check whether an application gateway is running in hello virtual network](#check-whether-an-application-gateway-is-running-in-the-virtual-network).</span></span>
3. <span data-ttu-id="86dc0-109">[Azure Active Directory etki alanı hizmeti hello sanal ağında etkinleştirilip etkinleştirilmediğini kontrol](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="86dc0-109">[Check whether Azure Active Directory Domain Service is enabled in hello virtual network](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).</span></span>
4. <span data-ttu-id="86dc0-110">[Merhaba sanal ağ bağlantılı tooother kaynak olup olmadığını denetleyin](#check-whether-the-virtual-network-is-connected-to-other-resource).</span><span class="sxs-lookup"><span data-stu-id="86dc0-110">[Check whether hello virtual network is connected tooother resource](#check-whether-the-virtual-network-is-connected-to-other-resource).</span></span>
5. <span data-ttu-id="86dc0-111">[Bir sanal makine hello sanal ağında hala çalışıp çalışmadığını denetleyin](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="86dc0-111">[Check whether a virtual machine is still running in hello virtual network](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).</span></span>
6. <span data-ttu-id="86dc0-112">[Merhaba sanal ağ içinde geçiş takıldı olup olmadığını denetleyin](#check-whether-the-virtual-network-is-stuck-in-migration).</span><span class="sxs-lookup"><span data-stu-id="86dc0-112">[Check whether hello virtual network is stuck in migration](#check-whether-the-virtual-network-is-stuck-in-migration).</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="86dc0-113">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="86dc0-113">Troubleshooting steps</span></span>

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="86dc0-114">Bir sanal ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="86dc0-114">Check whether a virtual network gateway is running in hello virtual network</span></span>

<span data-ttu-id="86dc0-115">tooremove hello sanal ağ, hello sanal ağ geçidi önce kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86dc0-115">tooremove hello virtual network, you must first remove hello virtual network gateway.</span></span>

<span data-ttu-id="86dc0-116">Klasik sanal ağlar için toohello Git **genel bakış** sayfa hello Azure Portalı'nda hello Klasik sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="86dc0-116">For classic virtual networks, go toohello **Overview** page of hello classic virtual network in hello Azure portal.</span></span> <span data-ttu-id="86dc0-117">Merhaba, **VPN bağlantıları** bölümünde, hello ağ geçidi hello sanal ağda çalışıyorsa, hello IP görürsünüz hello ağ geçidi adresi.</span><span class="sxs-lookup"><span data-stu-id="86dc0-117">In hello **VPN connections** section, if hello gateway is running in hello virtual network, you will see hello IP address of hello gateway.</span></span> 

![Ağ geçidi çalışır durumda olup olmadığını denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

<span data-ttu-id="86dc0-119">Sanal ağlar için toohello Git **genel bakış** hello sanal ağ sayfası.</span><span class="sxs-lookup"><span data-stu-id="86dc0-119">For virtual networks, go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="86dc0-120">Denetleme **bağlı cihazları** hello sanal ağ geçidi için.</span><span class="sxs-lookup"><span data-stu-id="86dc0-120">Check **Connected devices** for hello virtual network gateway.</span></span>

![Merhaba bağlı aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

<span data-ttu-id="86dc0-122">Hello ağ geçidi kaldırmadan önce ilk herhangi kaldırın **bağlantı** hello ağ geçidi nesneleri.</span><span class="sxs-lookup"><span data-stu-id="86dc0-122">Before you can remove hello gateway, first remove any **Connection** objects in hello gateway.</span></span> 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a><span data-ttu-id="86dc0-123">Bir uygulama ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="86dc0-123">Check whether an application gateway is running in hello virtual network</span></span>

<span data-ttu-id="86dc0-124">Toohello Git **genel bakış** hello sanal ağ sayfası.</span><span class="sxs-lookup"><span data-stu-id="86dc0-124">Go toohello **Overview** page of hello virtual network.</span></span> <span data-ttu-id="86dc0-125">Merhaba denetleyin **bağlı cihazları** hello uygulama ağ geçidi için.</span><span class="sxs-lookup"><span data-stu-id="86dc0-125">Check hello **Connected devices** for hello application gateway.</span></span>

![Merhaba bağlı aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

<span data-ttu-id="86dc0-127">Bir uygulama ağ geçidi ise hello sanal ağı silmeden önce onu kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="86dc0-127">If there is an application gateway, you must remove it before you can delete hello virtual network.</span></span>

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a><span data-ttu-id="86dc0-128">Azure Active Directory etki alanı hizmeti hello sanal ağda etkin olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="86dc0-128">Check whether Azure Active Directory Domain Service is enabled in hello virtual network</span></span>

<span data-ttu-id="86dc0-129">Merhaba Active Directory etki alanı hizmeti etkin ve bağlı toohello sanal ağ ise, bu sanal ağ silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="86dc0-129">If hello Active Directory Domain Service is enabled and connected toohello virtual network, you cannot delete this virtual network.</span></span> 

![Merhaba bağlı aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

<span data-ttu-id="86dc0-131">toodisable Merhaba hizmeti, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="86dc0-131">toodisable hello service, follow these steps:</span></span>

1. <span data-ttu-id="86dc0-132">Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="86dc0-132">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="86dc0-133">Merhaba sol bölmesinde seçin **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="86dc0-133">In hello left pane, select  **Active Directory**.</span></span>
3. <span data-ttu-id="86dc0-134">Active Directory etki alanı hizmeti etkin olan hello Azure Active Directory (Azure AD) dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="86dc0-134">Select hello Azure Active Directory (Azure AD) directory that has Active Directory Domain Service enabled.</span></span>
4. <span data-ttu-id="86dc0-135">Select hello **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="86dc0-135">Select hello **Configure** tab.</span></span>
5. <span data-ttu-id="86dc0-136">Altında **etki alanı Hizmetleri**, hello değiştirme **bu dizin için etki alanı Hizmetleri'ni etkinleştirme** çok seçenek**Hayır**.</span><span class="sxs-lookup"><span data-stu-id="86dc0-136">Under **domain services**, change hello **Enable domain services for this directory** option too**No**.</span></span>  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a><span data-ttu-id="86dc0-137">Merhaba sanal ağ bağlantılı tooother kaynak olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="86dc0-137">Check whether hello virtual network is connected tooother resource</span></span>

<span data-ttu-id="86dc0-138">Bağlantı hattı bağlantıları, bağlantıları ve sanal ağ eşlemesi bulunabilir denetleyin.</span><span class="sxs-lookup"><span data-stu-id="86dc0-138">Check for Circuit Links, connections, and virtual network peerings.</span></span> <span data-ttu-id="86dc0-139">Bunlardan herhangi bir sanal ağ silme toofail neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="86dc0-139">Any of these can cause a virtual network deletion toofail.</span></span> 

<span data-ttu-id="86dc0-140">Merhaba önerilen silme sipariş şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="86dc0-140">hello recommended deletion order is as follows:</span></span>

1. <span data-ttu-id="86dc0-141">Ağ Geçidi bağlantıları</span><span class="sxs-lookup"><span data-stu-id="86dc0-141">Gateway connections</span></span>
2. <span data-ttu-id="86dc0-142">Ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="86dc0-142">Gateways</span></span>
3. <span data-ttu-id="86dc0-143">IP'leri</span><span class="sxs-lookup"><span data-stu-id="86dc0-143">IPs</span></span>
4. <span data-ttu-id="86dc0-144">Sanal Ağ eşlemesi bulunabilir</span><span class="sxs-lookup"><span data-stu-id="86dc0-144">Virtual network peerings</span></span>
5. <span data-ttu-id="86dc0-145">Uygulama hizmeti ortamı (ana)</span><span class="sxs-lookup"><span data-stu-id="86dc0-145">App Service Environment (ASE)</span></span>

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a><span data-ttu-id="86dc0-146">Bir sanal makine hello sanal ağında hala çalışıp çalışmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="86dc0-146">Check whether a virtual machine is still running in hello virtual network</span></span>

<span data-ttu-id="86dc0-147">Hiçbir sanal makine hello sanal ağda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="86dc0-147">Make sure that no virtual machine is in hello virtual network.</span></span>

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a><span data-ttu-id="86dc0-148">Merhaba sanal ağ içinde geçiş takıldı olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="86dc0-148">Check whether hello virtual network is stuck in migration</span></span>

<span data-ttu-id="86dc0-149">Merhaba sanal ağ bir geçiş durumunda takılıyorsa silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="86dc0-149">If hello virtual network is stuck in a migration state, it cannot be deleted.</span></span> <span data-ttu-id="86dc0-150">Komut tooabort hello geçiş aşağıdaki hello çalıştırın ve hello sanal ağ silin.</span><span class="sxs-lookup"><span data-stu-id="86dc0-150">Run hello following command tooabort hello migration, and then delete hello virtual network.</span></span>

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a><span data-ttu-id="86dc0-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86dc0-151">Next steps</span></span>

- [<span data-ttu-id="86dc0-152">Azure Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="86dc0-152">Azure Virtual Network</span></span>](virtual-networks-overview.md)
- [<span data-ttu-id="86dc0-153">Azure Sanal Ağ hakkında sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="86dc0-153">Azure Virtual Network frequently asked questions (FAQ)</span></span>](virtual-networks-faq.md)