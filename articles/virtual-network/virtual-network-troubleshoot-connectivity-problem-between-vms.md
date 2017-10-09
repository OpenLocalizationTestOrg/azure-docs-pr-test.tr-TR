---
title: "Azure VM'ler arasında aaaTroubleshooting bağlantısı sorunları | Microsoft Docs"
description: "Nasıl tooTroubleshoot hello Azure VM'ler arasında bağlantı sorunları hakkında bilgi edinin."
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
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a><span data-ttu-id="f6a04-103">Azure VM'ler arasında bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f6a04-103">Troubleshooting connectivity problems between Azure VMs</span></span>

<span data-ttu-id="f6a04-104">Azure VM'ler arasında bağlantı sorunları yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6a04-104">You might experience connectivity problems between Azure VMs.</span></span> <span data-ttu-id="f6a04-105">Bu makalede, sorun giderme adımları toohelp sağlanmaktadır. Bu sorunu çözün.</span><span class="sxs-lookup"><span data-stu-id="f6a04-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a><span data-ttu-id="f6a04-106">Belirti</span><span class="sxs-lookup"><span data-stu-id="f6a04-106">Symptom</span></span>

<span data-ttu-id="f6a04-107">Bir Azure VM tooanother Azure VM bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="f6a04-107">An Azure VM cannot connect tooanother Azure VM.</span></span>

## <a name="troubleshooting-guidance"></a><span data-ttu-id="f6a04-108">Sorun giderme rehberi</span><span class="sxs-lookup"><span data-stu-id="f6a04-108">Troubleshooting guidance</span></span> 

1. [<span data-ttu-id="f6a04-109">NIC yanlış olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-109">Check if NIC is misconfigured</span></span>](#step-1-check-if-nic-is-misconfigured)
2. [<span data-ttu-id="f6a04-110">Ağ trafiği NSG veya UDR tarafından bloke edilmiş olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-110">Check if network traffic is blocked by NSG or UDR</span></span>](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [<span data-ttu-id="f6a04-111">Ağ trafiği bir VM Güvenlik Duvarı tarafından engellenir denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-111">Check if network traffic is blocked by VM firewall</span></span>](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [<span data-ttu-id="f6a04-112">VM uygulama veya hizmet hello bağlantı noktasında dinleme olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-112">Check whether VM app or service is listening on hello port</span></span>](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [<span data-ttu-id="f6a04-113">Tarafından SNAT Hello soruna neden olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-113">Check whether hello problem is caused by SNAT</span></span>](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [<span data-ttu-id="f6a04-114">Onay trafiği için ACL'ler tarafından engellenmiş olup olmadığını hello Klasik VM</span><span class="sxs-lookup"><span data-stu-id="f6a04-114">Check whether traffic is blocked by ACLs for hello classic VM</span></span>](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [<span data-ttu-id="f6a04-115">Onay hello uç noktası için oluşturulup oluşturulmadığını hello Klasik VM</span><span class="sxs-lookup"><span data-stu-id="f6a04-115">Check whether hello endpoint is created for hello classic VM</span></span>](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [<span data-ttu-id="f6a04-116">%S tooconnect tooa VM ağ paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f6a04-116">Unable tooconnect tooa VM network share</span></span>](#step-8-unable-to-connect-to-a-vm-network-share)
9. [<span data-ttu-id="f6a04-117">Ağlar arası Vnet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="f6a04-117">Inter-Vnet connectivity</span></span>](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a><span data-ttu-id="f6a04-118">Sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="f6a04-118">Troubleshooting steps</span></span>

<span data-ttu-id="f6a04-119">Bu adımları tootroubleshoot hello sorunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a04-119">Follow these steps tootroubleshoot hello problem.</span></span> <span data-ttu-id="f6a04-120">Her adımdan sonra Hello sorunun giderilmiş olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a04-120">Check whether hello problem is resolved after each step.</span></span> 

### <a name="step-1-check-if-nic-is-misconfigured"></a><span data-ttu-id="f6a04-121">1. adım: NIC yanlış olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-121">Step 1: Check if NIC is misconfigured</span></span>

<span data-ttu-id="f6a04-122">İzleyin [nasıl tooreset ağ arabirimi için Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span><span class="sxs-lookup"><span data-stu-id="f6a04-122">Follow [How tooreset network interface for Azure Windows VM](../virtual-machines/windows/reset-network-interface.md).</span></span> 

<span data-ttu-id="f6a04-123">Merhaba ağ arabirimi (NIC) değiştirdikten sonra hello sorun oluşursa, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f6a04-123">If hello problem occurs after you modify hello network interface (NIC), follow these steps:</span></span>

<span data-ttu-id="f6a04-124">**Mulit-NIC VM**</span><span class="sxs-lookup"><span data-stu-id="f6a04-124">**Mulit-NIC VMs**</span></span>

1. <span data-ttu-id="f6a04-125">Bir NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="f6a04-125">Add a NIC.</span></span>
2. <span data-ttu-id="f6a04-126">Merhaba hatalı NIC veya kaldırma hatalı NIC Hello sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="f6a04-126">Fix hello problems in hello bad NIC or remove bad NIC.</span></span>  <span data-ttu-id="f6a04-127">Merhaba NIC readd</span><span class="sxs-lookup"><span data-stu-id="f6a04-127">Then readd hello NIC.</span></span>

<span data-ttu-id="f6a04-128">Daha fazla bilgi için bkz: [Ekle ağ arabirimleri tooor sanal makinelerden kaldırmak](virtual-network-network-interface-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f6a04-128">For more information, see [Add network interfaces tooor remove from virtual machines](virtual-network-network-interface-vm.md).</span></span>

<span data-ttu-id="f6a04-129">**Tek NIC VM**</span><span class="sxs-lookup"><span data-stu-id="f6a04-129">**Single-NIC VM**</span></span> 

- [<span data-ttu-id="f6a04-130">Windows VM yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="f6a04-130">Redeploy Windows VM</span></span>](../virtual-machines/windows/redeploy-to-new-node.md)
- [<span data-ttu-id="f6a04-131">Linux VM yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="f6a04-131">Redeploy Linux VM</span></span>](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a><span data-ttu-id="f6a04-132">2. adım: ağ trafiği NSG veya UDR tarafından bloke edilmiş olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-132">Step 2: Check if network traffic is blocked by NSG or UDR</span></span>

<span data-ttu-id="f6a04-133">Kullanan [Ağ İzleyicisi IP akış doğrulayın](../network-watcher/network-watcher-ip-flow-verify-overview.md) ve [NSG akış günlüğü](../network-watcher/network-watcher-nsg-flow-logging-overview.md) bir ağ güvenlik grubu veya kullanıcı tanımlı yol, trafik akışı ile engellemesini ise tooidentify.</span><span class="sxs-lookup"><span data-stu-id="f6a04-133">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span>

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a><span data-ttu-id="f6a04-134">3. adım: ağ trafiği bir VM Güvenlik Duvarı tarafından engellenir denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-134">Step 3: Check if network traffic is blocked by VM firewall</span></span>

<span data-ttu-id="f6a04-135">Hello Güvenlik Duvarı'nı devre dışı bırakın ve ardından hello sonucunu sınayın.</span><span class="sxs-lookup"><span data-stu-id="f6a04-135">Disable hello firewall, and then test hello result.</span></span> <span data-ttu-id="f6a04-136">Merhaba sorunun giderilip giderilmediğini hello Güvenlik Duvarı'nda hello ayarlarını doğrulayın ve yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f6a04-136">If hello problem is resolved, validate hello settings in hello firewall and re-enable.</span></span>

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a><span data-ttu-id="f6a04-137">4. adım: VM uygulama veya hizmet hello bağlantı noktasında dinleme olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-137">Step 4: Check whether VM app or service is listening on hello port</span></span>

<span data-ttu-id="f6a04-138">VM uygulama veya hizmet hello bağlantı noktasında dinleme olup olmadığını yöntemleri toocheck aşağıdaki hello birini kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f6a04-138">You can use one of hello following methods toocheck whether VM Application or Service is listening on hello port</span></span>

- <span data-ttu-id="f6a04-139">Merhaba sunucu bu bağlantı noktasında dinleme olup olmadığını komutları toocheck aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f6a04-139">Run hello following commands toocheck whether hello server is listening on that port.</span></span>

<span data-ttu-id="f6a04-140">**Windows VM**</span><span class="sxs-lookup"><span data-stu-id="f6a04-140">**Windows VM**</span></span>

    netstat –ano

<span data-ttu-id="f6a04-141">**Linux VM**</span><span class="sxs-lookup"><span data-stu-id="f6a04-141">**Linux VM**</span></span>

    netstat -l

- <span data-ttu-id="f6a04-142">Merhaba çalıştırmak **Telnet** hello VM tooitself tootest hello bağlantı noktası üzerinde komutu.</span><span class="sxs-lookup"><span data-stu-id="f6a04-142">Run hello **Telnet** command on hello VM tooitself tootest hello port.</span></span> <span data-ttu-id="f6a04-143">Merhaba testi başarısız olursa, uygulama veya hizmet hello bağlantı noktasında yapılandırılmış toolisten değil.</span><span class="sxs-lookup"><span data-stu-id="f6a04-143">If hello test fails, application or service is not configured toolisten on hello port.</span></span>

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a><span data-ttu-id="f6a04-144">5. adım: SNAT tarafından hello soruna neden olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="f6a04-144">Step 5: Check whether hello problem is caused by SNAT</span></span>

<span data-ttu-id="f6a04-145">Bazı senaryolarda hello VM kaynakların Azure dışında bir bağımlılığa sahip bir yük dengeleme çözümü arkasında yer alır.</span><span class="sxs-lookup"><span data-stu-id="f6a04-145">In some scenarios, hello VM is placed behind a Load balance solution that has a dependency on resources outside of Azure.</span></span> <span data-ttu-id="f6a04-146">Aralıklı bağlantısı sorunlar yaşıyorsanız bu senaryolarda, hello sorunun nedeni olabilir [SNAT bağlantı noktası Tükenme](../load-balancer/load-balancer-outbound-connections.md).</span><span class="sxs-lookup"><span data-stu-id="f6a04-146">In these scenarios, if you experience intermittent connection problems, hello problem may be caused by [SNAT port exhaustion](../load-balancer/load-balancer-outbound-connections.md).</span></span> <span data-ttu-id="f6a04-147">tooresolve hello sorun hello yük dengeleyicinin arkasına olan her bir VM için bir VIP (veya Klasik ILPIP) oluşturun ve NSG veya ACL ile güvenli.</span><span class="sxs-lookup"><span data-stu-id="f6a04-147">tooresolve hello issue, create a VIP (or ILPIP for classic) for each VM that is behind hello Load balancer and secure with NSG or ACL.</span></span> 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a><span data-ttu-id="f6a04-148">6. adım: Onay trafiği için ACL'ler tarafından engellenmiş olup olmadığını hello Klasik VM</span><span class="sxs-lookup"><span data-stu-id="f6a04-148">Step 6: Check whether traffic is blocked by ACLs for hello classic VM</span></span>

<span data-ttu-id="f6a04-149">Bir ACL veya bir sanal makine uç noktası için trafiği reddetmeye hello özelliği tooselectively izin sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6a04-149">An ACL provides hello ability tooselectively permit or deny traffic for a virtual machine endpoint.</span></span> <span data-ttu-id="f6a04-150">Daha fazla bilgi için bkz: [uç noktada Yönet hello ACL](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span><span class="sxs-lookup"><span data-stu-id="f6a04-150">For more information, see [Manage hello ACL on an endpoint](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).</span></span>

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a><span data-ttu-id="f6a04-151">7. adım: Onay hello uç noktası için oluşturulup oluşturulmadığını hello Klasik VM</span><span class="sxs-lookup"><span data-stu-id="f6a04-151">Step 7: Check whether hello endpoint is created for hello classic VM</span></span>

<span data-ttu-id="f6a04-152">Azure'da hello Klasik dağıtım modeli kullanarak oluşturduğunuz tüm sanal makineleri otomatik olarak hello içindeki diğer sanal makinelerle özel ağ kanalı üzerinden aynı hizmet veya sanal ağ bulut iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="f6a04-152">All VMs that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="f6a04-153">Ancak, diğer sanal ağlardaki bilgisayarlara uç noktaları toodirect hello gelen ağ trafiğini tooa sanal makine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f6a04-153">However, computers on other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="f6a04-154">Daha fazla bilgi için bkz: [nasıl tooset uç noktaları yukarı](../virtual-machines/windows/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="f6a04-154">For more information, see [How tooset up endpoints](../virtual-machines/windows/classic/setup-endpoints.md).</span></span>

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a><span data-ttu-id="f6a04-155">8. adım: Oluşturulamıyor tooconnect tooa VM ağ paylaşımı</span><span class="sxs-lookup"><span data-stu-id="f6a04-155">Step 8: Unable tooconnect tooa VM network share</span></span>

<span data-ttu-id="f6a04-156">%S tooconnect tooa VM ağ paylaşımı varsa, hello VM içinde kullanılamaz NIC tarafından hello sorunu neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f6a04-156">If you are unable tooconnect tooa VM network share, hello problem can be caused by unavailable NICs in hello VM.</span></span> <span data-ttu-id="f6a04-157">toodelete kullanılamayan NICs Merhaba, bkz: [nasıl toodelete hello kullanılamaz NIC](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span><span class="sxs-lookup"><span data-stu-id="f6a04-157">toodelete hello unavailable NICs, see [How toodelete hello unavailable NICs](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)</span></span>

### <a name="step-9-inter-vnet-connectivity"></a><span data-ttu-id="f6a04-158">9. adım: Arası Vnet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="f6a04-158">Step 9: Inter-Vnet connectivity</span></span>

<span data-ttu-id="f6a04-159">Kullanan [Ağ İzleyicisi IP akış doğrulayın](../network-watcher/network-watcher-ip-flow-verify-overview.md) ve [NSG akış günlüğü](../network-watcher/network-watcher-nsg-flow-logging-overview.md) bir ağ güvenlik grubu veya kullanıcı tanımlı yol, trafik akışı ile engellemesini ise tooidentify.</span><span class="sxs-lookup"><span data-stu-id="f6a04-159">Utilize [Network Watcher IP Flow Verify](../network-watcher/network-watcher-ip-flow-verify-overview.md) and [NSG Flow Logging](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify if there is a Network Security Group or User-Defined Route that is interfering with traffic flow.</span></span> <span data-ttu-id="f6a04-160">Inter-Vnet yapılandırmasını doğrulamak için [burada](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span><span class="sxs-lookup"><span data-stu-id="f6a04-160">You can also validate your Inter-Vnet configuration [here](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).</span></span>

### <a name="need-help-contact-support"></a><span data-ttu-id="f6a04-161">Yardım mı gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="f6a04-161">Need help?</span></span> <span data-ttu-id="f6a04-162">Desteğe başvurun.</span><span class="sxs-lookup"><span data-stu-id="f6a04-162">Contact support.</span></span>
<span data-ttu-id="f6a04-163">Hala yardıma gereksiniminiz varsa [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) sorunu Çözümlendi hızla tooget.</span><span class="sxs-lookup"><span data-stu-id="f6a04-163">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
