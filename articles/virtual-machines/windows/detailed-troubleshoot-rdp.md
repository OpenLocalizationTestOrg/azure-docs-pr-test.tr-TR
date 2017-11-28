---
title: "Azure'da sorun giderme aaaDetailed Uzak Masaüstü | Microsoft Docs"
description: "Burada tooa Windows Azure sanal makinelerde yapamazsınız Uzak Masaüstü hataları için ayrıntılı sorun giderme adımlarını gözden geçirin"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "gönderilemiyor tooremote Masaüstü Bağlantısı, Uzak Masaüstü, sorun giderme Uzak Masaüstü bağlantı kuramıyor, Uzak Masaüstü hataları, Uzak Masaüstü sorunlarını giderme, Uzak Masaüstü sorunları"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a><span data-ttu-id="f97d5-104">Uzak Masaüstü bağlantısı için ayrıntılı sorun giderme adımları sorunları tooWindows azure'da VM</span><span class="sxs-lookup"><span data-stu-id="f97d5-104">Detailed troubleshooting steps for remote desktop connection issues tooWindows VMs in Azure</span></span>
<span data-ttu-id="f97d5-105">Bu makale, Windows tabanlı Azure sanal makineler için toodiagnose ve düzeltme karmaşık Uzak Masaüstü hatalarını ayrıntılı sorun giderme adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f97d5-105">This article provides detailed troubleshooting steps toodiagnose and fix complex Remote Desktop errors for Windows-based Azure virtual machines.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f97d5-106">tooeliminate hello daha yaygın Uzak Masaüstü hataları, yapma emin tooread [hello temel sorun giderme makalesi, Uzak Masaüstü için](troubleshoot-rdp-connection.md) devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="f97d5-106">tooeliminate hello more common Remote Desktop errors, make sure tooread [hello basic troubleshooting article for Remote Desktop](troubleshoot-rdp-connection.md) before proceeding.</span></span>

<span data-ttu-id="f97d5-107">Uzak Masaüstü hello belirli hata iletilerinden birini benzemez hata iletisi ele karşılaşabileceğiniz [sorun giderme kılavuzu temel Uzak Masaüstü hello](troubleshoot-rdp-connection.md).</span><span class="sxs-lookup"><span data-stu-id="f97d5-107">You may encounter a Remote Desktop error message that does not resemble any of hello specific error messages covered in [hello basic Remote Desktop troubleshooting guide](troubleshoot-rdp-connection.md).</span></span> <span data-ttu-id="f97d5-108">Bu adımları toodetermine neden hello Uzak Masaüstü (RDP) istemci oluşturulamıyor tooconnect toohello RDP hello Azure VM üzerinde hizmetidir izleyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-108">Follow these steps toodetermine why hello Remote Desktop (RDP) client is unable tooconnect toohello RDP service on hello Azure VM.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f97d5-109">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f97d5-109">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="f97d5-110">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="f97d5-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="f97d5-111">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) tıklatıp **destek alın**.</span><span class="sxs-lookup"><span data-stu-id="f97d5-111">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span> <span data-ttu-id="f97d5-112">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="f97d5-112">For information about using Azure Support, read hello [Microsoft Azure Support FAQ](https://azure.microsoft.com/support/faq/).</span></span>

## <a name="components-of-a-remote-desktop-connection"></a><span data-ttu-id="f97d5-113">Uzak Masaüstü bağlantısının bileşenleri</span><span class="sxs-lookup"><span data-stu-id="f97d5-113">Components of a Remote Desktop connection</span></span>
<span data-ttu-id="f97d5-114">Aşağıdaki bileşenler hello bir RDP bağlantısının oynayan:</span><span class="sxs-lookup"><span data-stu-id="f97d5-114">hello following components are involved in an RDP connection:</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

<span data-ttu-id="f97d5-115">Devam etmeden önce nelerin hello son başarılı Uzak Masaüstü Bağlantısı toohello itibaren VM değiştiğini gözden toomentally yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f97d5-115">Before proceeding, it might help toomentally review what has changed since hello last successful Remote Desktop connection toohello VM.</span></span> <span data-ttu-id="f97d5-116">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f97d5-116">For example:</span></span>

* <span data-ttu-id="f97d5-117">Merhaba hello VM içeren hello VM veya hello bulut hizmetinin genel IP adresi (Merhaba sanal IP adresi olarak da bilinir [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) değişti.</span><span class="sxs-lookup"><span data-stu-id="f97d5-117">hello public IP address of hello VM or hello cloud service containing hello VM (also called hello virtual IP address [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) has changed.</span></span> <span data-ttu-id="f97d5-118">DNS istemci önbelleği hala hello olduğundan Hello RDP hatası olabilir *eski IP adresi* hello DNS adı için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="f97d5-118">hello RDP failure could be because your DNS client cache still has hello *old IP address* registered for hello DNS name.</span></span> <span data-ttu-id="f97d5-119">DNS istemci önbelleğini temizlemek ve hello VM yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-119">Flush your DNS client cache and try connecting hello VM again.</span></span> <span data-ttu-id="f97d5-120">Veya doğrudan hello yeni VIP ile bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-120">Or try connecting directly with hello new VIP.</span></span>
* <span data-ttu-id="f97d5-121">Bir üçüncü taraf uygulama toomanage hello Azure portal tarafından oluşturulan hello bağlantısı kullanmak yerine, Uzak Masaüstü bağlantıları kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="f97d5-121">You are using a third-party application toomanage your Remote Desktop connections instead of using hello connection generated by hello Azure portal.</span></span> <span data-ttu-id="f97d5-122">Merhaba doğru TCP bağlantı noktası hello Uzak Masaüstü trafiği için bu hello uygulama yapılandırması içerir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-122">Verify that hello application configuration includes hello correct TCP port for hello Remote Desktop traffic.</span></span> <span data-ttu-id="f97d5-123">Bu bağlantı noktası hello klasik bir sanal makine için kontrol edebilirsiniz [Azure portal](https://portal.azure.com), hello VM'in ayarları tıklayarak > uç noktaları.</span><span class="sxs-lookup"><span data-stu-id="f97d5-123">You can check this port for a classic virtual machine in hello [Azure portal](https://portal.azure.com), by clicking hello VM's Settings > Endpoints.</span></span>

## <a name="preliminary-steps"></a><span data-ttu-id="f97d5-124">Başlangıç adımları</span><span class="sxs-lookup"><span data-stu-id="f97d5-124">Preliminary steps</span></span>
<span data-ttu-id="f97d5-125">Devam etmeden önce toohello ayrıntılı sorun giderme,</span><span class="sxs-lookup"><span data-stu-id="f97d5-125">Before proceeding toohello detailed troubleshooting,</span></span>

* <span data-ttu-id="f97d5-126">Merhaba hello belirgin sorunları için Azure portalı hello sanal makinenin durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-126">Check hello status of hello virtual machine in hello Azure portal for any obvious issues.</span></span>
* <span data-ttu-id="f97d5-127">Merhaba izleyin [hızlı düzeltme adımları hello temel sorun gidermeyi ortak RDP hataları için kılavuzluk](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="f97d5-127">Follow hello [quick fix steps for common RDP errors in hello basic troubleshooting guide](troubleshoot-rdp-connection.md#quick-troubleshooting-steps).</span></span>

<span data-ttu-id="f97d5-128">Uzak Masaüstü VM toohello adımları sonra yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-128">Try reconnecting toohello VM via Remote Desktop after these steps.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="f97d5-129">Ayrıntılı sorun giderme adımları</span><span class="sxs-lookup"><span data-stu-id="f97d5-129">Detailed troubleshooting steps</span></span>
<span data-ttu-id="f97d5-130">Merhaba uzak masaüstü istemcisini kullanabilirsiniz tooreach hello Uzak Masaüstü hizmetini hello Azure VM olmayabilir aşağıdaki kaynaklar hello en son tooissues:</span><span class="sxs-lookup"><span data-stu-id="f97d5-130">hello Remote Desktop client may not be able tooreach hello Remote Desktop service on hello Azure VM due tooissues at hello following sources:</span></span>

* [<span data-ttu-id="f97d5-131">Uzak Masaüstü istemcisi bilgisayar</span><span class="sxs-lookup"><span data-stu-id="f97d5-131">Remote Desktop client computer</span></span>](#source-1-remote-desktop-client-computer)
* [<span data-ttu-id="f97d5-132">Kuruluş intranet sınır cihazı</span><span class="sxs-lookup"><span data-stu-id="f97d5-132">Organization intranet edge device</span></span>](#source-2-organization-intranet-edge-device)
* [<span data-ttu-id="f97d5-133">Bulut Hizmeti uç noktası ve erişim denetimi listesi (ACL)</span><span class="sxs-lookup"><span data-stu-id="f97d5-133">Cloud service endpoint and access control list (ACL)</span></span>](#source-3-cloud-service-endpoint-and-acl)
* [<span data-ttu-id="f97d5-134">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="f97d5-134">Network security groups</span></span>](#source-4-network-security-groups)
* [<span data-ttu-id="f97d5-135">Windows tabanlı Azure VM</span><span class="sxs-lookup"><span data-stu-id="f97d5-135">Windows-based Azure VM</span></span>](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a><span data-ttu-id="f97d5-136">Kaynak 1: Uzak Masaüstü istemcisi bilgisayar</span><span class="sxs-lookup"><span data-stu-id="f97d5-136">Source 1: Remote Desktop client computer</span></span>
<span data-ttu-id="f97d5-137">Bilgisayarınızı Uzak Masaüstü yapabilirsiniz doğrulayın içi tooanother bağlantıları, Windows tabanlı bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="f97d5-137">Verify that your computer can make Remote Desktop connections tooanother on-premises, Windows-based computer.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

<span data-ttu-id="f97d5-138">Şunları yapamazsınız ayarları bilgisayarınızda aşağıdaki hello için kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="f97d5-138">If you cannot, check for hello following settings on your computer:</span></span>

* <span data-ttu-id="f97d5-139">Uzak Masaüstü trafiği engelleyen bir yerel güvenlik duvarı ayarı.</span><span class="sxs-lookup"><span data-stu-id="f97d5-139">A local firewall setting that is blocking Remote Desktop traffic.</span></span>
* <span data-ttu-id="f97d5-140">Yerel olarak Uzak Masaüstü bağlantıları engelliyor istemci ara yazılımı yüklü.</span><span class="sxs-lookup"><span data-stu-id="f97d5-140">Locally installed client proxy software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="f97d5-141">Yerel ağ Uzak Masaüstü bağlantıları engelliyor yazılım izleme yüklü.</span><span class="sxs-lookup"><span data-stu-id="f97d5-141">Locally installed network monitoring software that is preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="f97d5-142">Trafiği izlemek ya da belirli Uzak Masaüstü bağlantıları engelliyor trafik türlerine izin ver/engellemek diğer güvenlik yazılım türleri.</span><span class="sxs-lookup"><span data-stu-id="f97d5-142">Other types of security software that either monitor traffic or allow/disallow specific types of traffic that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="f97d5-143">Tüm bu durumlarda, geçici olarak hello yazılımını devre dışı bırakma ve Uzak Masaüstü üzerinden tooconnect tooan şirket içi bilgisayara deneyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-143">In all these cases, temporarily disable hello software and try tooconnect tooan on-premises computer via Remote Desktop.</span></span> <span data-ttu-id="f97d5-144">Bu şekilde hello gerçek nedenini bulabilirsiniz, ağ yöneticisi toocorrect hello yazılım ayarları tooallow Uzak Masaüstü bağlantıları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f97d5-144">If you can find out hello actual cause this way, work with your network administrator toocorrect hello software settings tooallow Remote Desktop connections.</span></span>

## <a name="source-2-organization-intranet-edge-device"></a><span data-ttu-id="f97d5-145">2. kaynak: Kuruluş intranet sınır cihazı</span><span class="sxs-lookup"><span data-stu-id="f97d5-145">Source 2: Organization intranet edge device</span></span>
<span data-ttu-id="f97d5-146">Bir bilgisayarın Uzak Masaüstü bağlantıları tooyour Azure sanal makinesi Internet yapabilirsiniz toohello doğrudan bağlı emin olun.</span><span class="sxs-lookup"><span data-stu-id="f97d5-146">Verify that a computer directly connected toohello Internet can make Remote Desktop connections tooyour Azure virtual machine.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

<span data-ttu-id="f97d5-147">Doğrudan bağlı bir bilgisayarda yoksa toohello Internet oluşturun ve yeni bir Azure sanal makine bir kaynak grubu veya Bulut hizmetinde sınayın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-147">If you do not have a computer that is directly connected toohello Internet, create and test with a new Azure virtual machine in a resource group or cloud service.</span></span> <span data-ttu-id="f97d5-148">Daha fazla bilgi için bkz: [Windows Azure üzerinde çalışan bir sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f97d5-148">For more information, see [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="f97d5-149">Merhaba test ettikten sonra hello sanal makine ve hello kaynak grubu ya da hello bulut hizmeti silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f97d5-149">You can delete hello virtual machine and hello resource group or hello cloud service, after hello test.</span></span>

<span data-ttu-id="f97d5-150">Doğrudan bağlı bilgisayar toohello Internet ile bir Uzak Masaüstü bağlantısı oluşturabilirsiniz kuruluş intranet kenar cihazınız için kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="f97d5-150">If you can create a Remote Desktop connection with a computer directly attached toohello Internet, check your organization intranet edge device for:</span></span>

* <span data-ttu-id="f97d5-151">HTTPS bağlantıları toohello Internet engelleyen bir iç güvenlik duvarı.</span><span class="sxs-lookup"><span data-stu-id="f97d5-151">An internal firewall blocking HTTPS connections toohello Internet.</span></span>
* <span data-ttu-id="f97d5-152">Uzak Masaüstü bağlantıları engelleyen bir proxy sunucu.</span><span class="sxs-lookup"><span data-stu-id="f97d5-152">A proxy server preventing Remote Desktop connections.</span></span>
* <span data-ttu-id="f97d5-153">Yetkisiz erişim algılama veya ağ kenar ağınızdaki Uzak Masaüstü bağlantıları engelliyor cihazlarda çalışan yazılım izleme.</span><span class="sxs-lookup"><span data-stu-id="f97d5-153">Intrusion detection or network monitoring software running on devices in your edge network that is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="f97d5-154">Ağ Yöneticisi toocorrect hello ayarlarının, kuruluş intranet kenar aygıt tooallow HTTPS tabanlı Uzak Masaüstü bağlantıları toohello Internet ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f97d5-154">Work with your network administrator toocorrect hello settings of your organization intranet edge device tooallow HTTPS-based Remote Desktop connections toohello Internet.</span></span>

## <a name="source-3-cloud-service-endpoint-and-acl"></a><span data-ttu-id="f97d5-155">3. kaynak: Bulut Hizmeti uç noktası ve ACL</span><span class="sxs-lookup"><span data-stu-id="f97d5-155">Source 3: Cloud service endpoint and ACL</span></span>
<span data-ttu-id="f97d5-156">Oluşturulan VM'ler hello Klasik dağıtım modeli kullanılarak başka bir Azure VM, olduğunu doğrulamak için hello aynı bulut hizmeti veya Uzak Masaüstü bağlantıları tooyour Azure VM sanal ağ yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f97d5-156">For VMs created using hello Classic deployment model, verify that another Azure VM that is in hello same cloud service or virtual network can make Remote Desktop connections tooyour Azure VM.</span></span>

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> <span data-ttu-id="f97d5-157">Kaynak Yöneticisi'nde oluşturulan sanal makineler için çok atla[kaynak 4: ağ güvenlik grupları](#source-4-network-security-groups).</span><span class="sxs-lookup"><span data-stu-id="f97d5-157">For virtual machines created in Resource Manager, skip too[Source 4: Network Security Groups](#source-4-network-security-groups).</span></span>

<span data-ttu-id="f97d5-158">Başka bir sanal aynı bulut hizmeti ya da sanal ağ Merhaba, bir tane oluşturun makine yoksa.</span><span class="sxs-lookup"><span data-stu-id="f97d5-158">If you do not have another virtual machine in hello same cloud service or virtual network, create one.</span></span> <span data-ttu-id="f97d5-159">Merhaba adımları [Windows Azure üzerinde çalışan bir sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f97d5-159">Follow hello steps in [Create a virtual machine running Windows in Azure](../virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="f97d5-160">Merhaba test tamamlandıktan sonra hello test sanal makinesi silin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-160">Delete hello test virtual machine after hello test is completed.</span></span>

<span data-ttu-id="f97d5-161">Merhaba tooa sanal makinede Uzak Masaüstü aracılığıyla bağlanabiliyorsa aynı hizmet veya sanal ağ, bulut için bu ayarları kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="f97d5-161">If you can connect via Remote Desktop tooa virtual machine in hello same cloud service or virtual network, check for these settings:</span></span>

* <span data-ttu-id="f97d5-162">Uzak Masaüstü trafiğini hello hedef VM Hello uç nokta yapılandırması: hello özel TCP bağlantı noktası hello uç noktasının hangi hello üzerinde VM'ın Uzak Masaüstü hizmetini dinliyor hello TCP bağlantı noktası eşleşmesi gerekir (varsayılan olarak 3389).</span><span class="sxs-lookup"><span data-stu-id="f97d5-162">hello endpoint configuration for Remote Desktop traffic on hello target VM: hello private TCP port of hello endpoint must match hello TCP port on which hello VM's Remote Desktop service is listening (default is 3389).</span></span>
* <span data-ttu-id="f97d5-163">VM hello hedefte hello Uzak Masaüstü trafiği uç noktası için ACL Hello: ACL'leri izin verilen veya Internet tabanlı kaynak IP adresine hello öğesinden gelen trafiği reddedilen toospecify tanır.</span><span class="sxs-lookup"><span data-stu-id="f97d5-163">hello ACL for hello Remote Desktop traffic endpoint on hello target VM: ACLs allow you toospecify allowed or denied incoming traffic from hello Internet based on its source IP address.</span></span> <span data-ttu-id="f97d5-164">Yanlış yapılandırılmış ACL'ler gelen Uzak Masaüstü trafiği toohello endpoint engelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="f97d5-164">Misconfigured ACLs can prevent incoming Remote Desktop traffic toohello endpoint.</span></span> <span data-ttu-id="f97d5-165">Proxy ya da diğer uç sunucu, ortak IP adreslerinden gelen trafiğe izin verilir, ACL'ler tooensure denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-165">Check your ACLs tooensure that incoming traffic from your public IP addresses of your proxy or other edge server is allowed.</span></span> <span data-ttu-id="f97d5-166">Daha fazla bilgi için bkz: [bir ağ erişim denetimi listesi (ACL) nedir?](../../virtual-network/virtual-networks-acl.md)</span><span class="sxs-lookup"><span data-stu-id="f97d5-166">For more information, see [What is a Network Access Control List (ACL)?](../../virtual-network/virtual-networks-acl.md)</span></span>

<span data-ttu-id="f97d5-167">toocheck hello endpoint hello kaynağı hello sorununun ise hello geçerli uç nokta kaldırın ve hello aralığı 49152 – 65535 hello harici bağlantı noktası numarası için de bir rastgele bağlantı noktası seçerek yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f97d5-167">toocheck if hello endpoint is hello source of hello problem, remove hello current endpoint and create a new one, choosing a random port in hello range 49152–65535 for hello external port number.</span></span> <span data-ttu-id="f97d5-168">Daha fazla bilgi için bkz: [nasıl tooset uç noktaları tooa sanal makineyi](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f97d5-168">For more information, see [How tooset up endpoints tooa virtual machine](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="source-4-network-security-groups"></a><span data-ttu-id="f97d5-169">4. kaynak: Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="f97d5-169">Source 4: Network Security Groups</span></span>
<span data-ttu-id="f97d5-170">Ağ güvenlik grupları, izin verilen gelen ve giden trafik daha ayrıntılı denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="f97d5-170">Network Security Groups allow more granular control of allowed inbound and outbound traffic.</span></span> <span data-ttu-id="f97d5-171">Alt ağlar kapsayıcı kurallar oluşturabilir ve bir Azure sanal ağı Hizmetleri'nde bulut.</span><span class="sxs-lookup"><span data-stu-id="f97d5-171">You can create rules spanning subnets and cloud services in an Azure virtual network.</span></span>

<span data-ttu-id="f97d5-172">Kullanım [IP akış doğrulayın](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) trafiği tooor bir sanal makineden bir ağ güvenlik grubu kural engelliyorsa tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="f97d5-172">Use [IP flow verify](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm if a rule in a Network Security Group is blocking traffic tooor from a virtual machine.</span></span> <span data-ttu-id="f97d5-173">Ayrıca, etkin güvenlik grubu kuralları tooensure gelen "NSG izin ver" kuralı var ve RDP bağlantı noktası (varsayılan 3389) öncelik gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f97d5-173">You can also review effective security group rules tooensure inbound "Allow" NSG rule exists and is prioritized for RDP port(default 3389).</span></span> <span data-ttu-id="f97d5-174">Daha fazla bilgi için bkz: [kullanarak etkili güvenlik kuralları tootroubleshoot VM trafiğinin akmasını](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span><span class="sxs-lookup"><span data-stu-id="f97d5-174">For more information, see [Using Effective Security Rules tootroubleshoot VM traffic flow](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).</span></span>

## <a name="source-5-windows-based-azure-vm"></a><span data-ttu-id="f97d5-175">Kaynak 5: Windows tabanlı Azure VM</span><span class="sxs-lookup"><span data-stu-id="f97d5-175">Source 5: Windows-based Azure VM</span></span>
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

<span data-ttu-id="f97d5-176">Merhaba yönergeleri izleyin [bu makalede](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="f97d5-176">Follow hello instructions in [this article](reset-rdp.md).</span></span> <span data-ttu-id="f97d5-177">Bu makalede hello Uzak Masaüstü hizmetini hello sanal makineye sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="f97d5-177">This article resets hello Remote Desktop service on hello virtual machine:</span></span>

* <span data-ttu-id="f97d5-178">Merhaba "Uzak Masaüstü" Windows Güvenlik Duvarı varsayılan kuralı (TCP bağlantı noktası 3389) etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-178">Enable hello "Remote Desktop" Windows Firewall default rule (TCP port 3389).</span></span>
* <span data-ttu-id="f97d5-179">Uzak Masaüstü bağlantıları hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections kayıt defteri değeri too0 ayarlayarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-179">Enable Remote Desktop connections by setting hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections registry value too0.</span></span>

<span data-ttu-id="f97d5-180">Merhaba bağlantıyı bilgisayarınızdan yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-180">Try hello connection from your computer again.</span></span> <span data-ttu-id="f97d5-181">Uzak Masaüstü hala erişilemiyor tooconnect varsa, aşağıdaki olası sorunları Merhaba denetleyin:</span><span class="sxs-lookup"><span data-stu-id="f97d5-181">If you are still not able tooconnect via Remote Desktop, check for hello following possible problems:</span></span>

* <span data-ttu-id="f97d5-182">Merhaba Uzak Masaüstü hizmetini hello hedef VM üzerinde çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="f97d5-182">hello Remote Desktop service is not running on hello target VM.</span></span>
* <span data-ttu-id="f97d5-183">Uzak Masaüstü hizmetini Hello TCP bağlantı noktası 3389 dinlemiyor.</span><span class="sxs-lookup"><span data-stu-id="f97d5-183">hello Remote Desktop service is not listening on TCP port 3389.</span></span>
* <span data-ttu-id="f97d5-184">Windows Güvenlik Duvarı veya başka bir yerel güvenlik duvarı Uzak Masaüstü trafiği engelleyen bir giden kuralı vardır.</span><span class="sxs-lookup"><span data-stu-id="f97d5-184">Windows Firewall or another local firewall has an outbound rule that is preventing Remote Desktop traffic.</span></span>
* <span data-ttu-id="f97d5-185">Yetkisiz erişim algılama veya ağ hello Azure sanal makine üzerinde çalışan yazılımı izleme Uzak Masaüstü bağlantıları engelliyor.</span><span class="sxs-lookup"><span data-stu-id="f97d5-185">Intrusion detection or network monitoring software running on hello Azure virtual machine is preventing Remote Desktop connections.</span></span>

<span data-ttu-id="f97d5-186">Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler için uzak bir Azure PowerShell oturumu toohello Azure sanal makinesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f97d5-186">For VMs created using hello classic deployment model, you can use a remote Azure PowerShell session toohello Azure virtual machine.</span></span> <span data-ttu-id="f97d5-187">İlk olarak, hello sanal makinenin barındırma bulut hizmeti için tooinstall bir sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97d5-187">First, you need tooinstall a certificate for hello virtual machine's hosting cloud service.</span></span> <span data-ttu-id="f97d5-188">Çok Git[güvenli uzaktan PowerShell erişimi Yapılandır tooAzure sanal makineleri](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) ve hello indirme **InstallWinRMCertAzureVM.ps1** komut dosyası tooyour yerel bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="f97d5-188">Go too[Configure Secure Remote PowerShell Access tooAzure Virtual Machines](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe) and download hello **InstallWinRMCertAzureVM.ps1** script file tooyour local computer.</span></span>

<span data-ttu-id="f97d5-189">Ardından, henüz yapmadıysanız Azure PowerShell'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-189">Next, install Azure PowerShell if you haven't already.</span></span> <span data-ttu-id="f97d5-190">Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f97d5-190">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="f97d5-191">Ardından, bir Azure PowerShell komut istemi açın ve hello geçerli klasör toohello konumunu hello değiştirmek **InstallWinRMCertAzureVM.ps1** komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="f97d5-191">Next, open an Azure PowerShell command prompt and change hello current folder toohello location of hello **InstallWinRMCertAzureVM.ps1** script file.</span></span> <span data-ttu-id="f97d5-192">bir Azure PowerShell Betiği toorun hello doğru yürütme ilkesini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f97d5-192">toorun an Azure PowerShell script, you must set hello correct execution policy.</span></span> <span data-ttu-id="f97d5-193">Merhaba çalıştırmak **Get-ExecutionPolicy** toodetermine geçerli ilke düzeyinizi komutu.</span><span class="sxs-lookup"><span data-stu-id="f97d5-193">Run hello **Get-ExecutionPolicy** command toodetermine your current policy level.</span></span> <span data-ttu-id="f97d5-194">Merhaba uygun düzeyini ayarlama hakkında daha fazla bilgi için bkz: [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).</span><span class="sxs-lookup"><span data-stu-id="f97d5-194">For information about setting hello appropriate level, see [Set-ExecutionPolicy](https://technet.microsoft.com/library/hh849812.aspx).</span></span>

<span data-ttu-id="f97d5-195">Ardından, Azure aboneliği adınızı, hello bulut hizmeti adı ve (merhaba < ve > karakterleri kaldırma), sanal makine adı doldurun ve ardından aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-195">Next, fill in your Azure subscription name, hello cloud service name, and your virtual machine name (removing hello < and > characters), and then run these commands.</span></span>

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

<span data-ttu-id="f97d5-196">Hello hello doğru abonelik adı alabilirsiniz *varlığıyla SubscriptionName* hello hello görüntüsünü özelliğinin **Get-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="f97d5-196">You can get hello correct subscription name from hello *SubscriptionName* property of hello display of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="f97d5-197">Merhaba bulut hizmeti adı hello sanal makine için hello alabilirsiniz *ServiceName* hello hello görüntüsünü sütununda **Get-AzureVM** komutu.</span><span class="sxs-lookup"><span data-stu-id="f97d5-197">You can get hello cloud service name for hello virtual machine from hello *ServiceName* column in hello display of hello **Get-AzureVM** command.</span></span>

<span data-ttu-id="f97d5-198">Merhaba yeni bir sertifika olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-198">Check if you have hello new certificate.</span></span> <span data-ttu-id="f97d5-199">Merhaba geçerli kullanıcı ile bir sertifika ek bileşenini açın ve hello arayın **güvenilen kök sertifika Authorities\Certificates** klasör.</span><span class="sxs-lookup"><span data-stu-id="f97d5-199">Open a Certificates snap-in for hello current user and look in hello **Trusted Root Certification Authorities\Certificates** folder.</span></span> <span data-ttu-id="f97d5-200">Bulut hizmetinizi hello verilen toocolumn hello DNS adına sahip bir sertifika görmeniz gerekir (örnek: cloudservice4testing.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="f97d5-200">You should see a certificate with hello DNS name of your cloud service in hello Issued toocolumn (example: cloudservice4testing.cloudapp.net).</span></span>

<span data-ttu-id="f97d5-201">Ardından, bu komutları kullanarak uzak bir Azure PowerShell oturumu başlatın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-201">Next, initiate a remote Azure PowerShell session by using these commands.</span></span>

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

<span data-ttu-id="f97d5-202">Geçerli yönetici kimlik bilgileri girdikten sonra Azure PowerShell komut isteminde aşağıdaki benzeri toohello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f97d5-202">After entering valid administrator credentials, you should see something similar toohello following Azure PowerShell prompt:</span></span>

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

<span data-ttu-id="f97d5-203">Merhaba ilk bu istemi hello hedef VM, "cloudservice4testing.cloudapp.net" farklı olabilir içeren bulut hizmeti adınızı parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f97d5-203">hello first part of this prompt is your cloud service name that contains hello target VM, which could be different from "cloudservice4testing.cloudapp.net".</span></span> <span data-ttu-id="f97d5-204">Şimdi, belirtilen hizmet tooinvestigate hello sorunlarına bu bulut için Azure PowerShell komutlarını verin ve hello yapılandırmasını düzeltin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-204">You can now issue Azure PowerShell commands for this cloud service tooinvestigate hello problems mentioned and correct hello configuration.</span></span>

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a><span data-ttu-id="f97d5-205">toomanually doğru hello Uzak Masaüstü Hizmetleri dinleme TCP bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="f97d5-205">toomanually correct hello Remote Desktop Services listening TCP port</span></span>
<span data-ttu-id="f97d5-206">Merhaba uzaktan Azure PowerShell oturumu isteminde bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-206">At hello remote Azure PowerShell session prompt, run this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="f97d5-207">Merhaba PortNumber özelliği hello geçerli bağlantı noktası numarasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f97d5-207">hello PortNumber property shows hello current port number.</span></span> <span data-ttu-id="f97d5-208">Gerekirse, hello Uzak Masaüstü bağlantı noktası numarası geri tooits varsayılan değeri (3389'dur) Bu komutu kullanarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-208">If needed, change hello Remote Desktop port number back tooits default value (3389) by using this command.</span></span>

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

<span data-ttu-id="f97d5-209">Bu komutu kullanarak Hello bağlantı noktası değiştirilen too3389 etkinleştirilmiş olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-209">Verify that hello port has been changed too3389 by using this command.</span></span>

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

<span data-ttu-id="f97d5-210">Merhaba uzaktan Azure PowerShell oturumunda bu komutu kullanarak çıkın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-210">Exit hello remote Azure PowerShell session by using this command.</span></span>

```powershell
Exit-PSSession
```

<span data-ttu-id="f97d5-211">Bu hello Uzak Masaüstü uç noktası hello Azure VM için de kendi iç bağlantı noktası olarak TCP bağlantı noktası 3398 kullanıyor doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f97d5-211">Verify that hello Remote Desktop endpoint for hello Azure VM is also using TCP port 3398 as its internal port.</span></span> <span data-ttu-id="f97d5-212">Hello Azure VM yeniden başlatın ve hello Uzak Masaüstü bağlantısı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="f97d5-212">Restart hello Azure VM and try hello Remote Desktop connection again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f97d5-213">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f97d5-213">Additional resources</span></span>
[<span data-ttu-id="f97d5-214">Nasıl tooreset bir parola veya hello Uzak Masaüstü hizmet için Windows sanal makineler</span><span class="sxs-lookup"><span data-stu-id="f97d5-214">How tooreset a password or hello Remote Desktop service for Windows virtual machines</span></span>](reset-rdp.md)

[<span data-ttu-id="f97d5-215">Nasıl tooinstall Azure PowerShell'i ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f97d5-215">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

[<span data-ttu-id="f97d5-216">Güvenli Kabuk (SSH) bağlantı tooa Linux tabanlı Azure sanal makine sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f97d5-216">Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine</span></span>](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="f97d5-217">Bir Azure sanal makine üzerinde çalışan erişim tooan uygulama sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f97d5-217">Troubleshoot access tooan application running on an Azure virtual machine</span></span>](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

