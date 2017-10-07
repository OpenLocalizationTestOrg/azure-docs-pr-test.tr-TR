---
title: "bir Azure sanal makinesi hızlandırılmış ağ aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate hızlandırılmış ağ sahip bir sanal makine."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="07152-103">Hızlandırılmış ağ ile bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="07152-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="07152-104">Bu öğreticide, bilgi nasıl toocreate hızlandırılmış ağ ile bir Azure sanal makine (VM).</span><span class="sxs-lookup"><span data-stu-id="07152-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="07152-105">Windows için ve belirli Linux dağıtımları için genel Önizleme GA hızlandırılmış ağdır.</span><span class="sxs-lookup"><span data-stu-id="07152-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="07152-106">Hızlandırılmış ağ tek köklü g/ç Sanallaştırması (SR-IOV) tooa VM, ağ performansını önemli ölçüde geliştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="07152-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="07152-107">Bu yüksek performanslı yolu gecikme, değişim ve hello zorlu ağ iş yükleri desteklenen VM türler ile kullanmak için CPU kullanımını azaltma hello datapath hello konaktan atlar.</span><span class="sxs-lookup"><span data-stu-id="07152-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="07152-108">Resim gösterir iletişimi ile ve hızlandırılmış ağ olmadan iki sanal makine (VM) arasında aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="07152-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Karşılaştırma](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="07152-110">Hızlandırılmış ağ olmadan hello VM ve dışındaki tüm ağ trafiğini hello konak ve sanal anahtar hello çapraz geçiş gerekir.</span><span class="sxs-lookup"><span data-stu-id="07152-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="07152-111">Hello sanal anahtarı tüm ilke zorunluluğu sağlar, örneğin ağ güvenlik grubu olarak denetim listeleri, yalıtım ve diğer ağ sanallaştırılmış Hizmetleri toonetwork trafiğinin erişim.</span><span class="sxs-lookup"><span data-stu-id="07152-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="07152-112">Merhaba okuma sanal anahtarları hakkında daha fazla toolearn [Hyper-V ağ sanallaştırma ve sanal anahtar](https://technet.microsoft.com/library/jj945275.aspx) makalesi.</span><span class="sxs-lookup"><span data-stu-id="07152-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="07152-113">Hızlandırılmış ağ ile ağ trafiğini hello VM'in ağ arabiriminin (NIC) ulaştığında ve ardından toohello VM iletilir.</span><span class="sxs-lookup"><span data-stu-id="07152-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="07152-114">Sanal anahtar hello tüm ağ ilkeleri hızlandırılmış ağ Boşaltılan ve donanım uygulanan olmadan uygular.</span><span class="sxs-lookup"><span data-stu-id="07152-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="07152-115">Donanım etkinleştirir hello NIC tooforward ilkesinde uygulama ağ trafiği doğrudan toohello hello ana uygulanan tüm hello İlkesi korurken hello konak ve sanal anahtar hello atlayarak VM.</span><span class="sxs-lookup"><span data-stu-id="07152-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="07152-116">Merhaba hızlandırılmış ağ yararları yalnızca toohello üzerinde etkin VM geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="07152-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="07152-117">İsteğe bağlı olarak Hello en iyi sonuçlar için ideal tooenable olan en az iki VM bu özelliğe bağlı toohello aynı Azure sanal ağ (VNet).</span><span class="sxs-lookup"><span data-stu-id="07152-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="07152-118">Sanal ağlar veya içi bağlantı üzerinden iletişim kurarken, bu özellik en az etki toooverall gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="07152-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="07152-119">Genel Önizleme kullanılabilirliği ve güvenilirliği gibi özelliklere aynı düzeyde olan hello olmayabilir bu Linux genel kullanılabilirlik sürümü.</span><span class="sxs-lookup"><span data-stu-id="07152-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="07152-120">Merhaba özelliği desteklenmiyor, yetenekleri kısıtlı ve tüm Azure konumlarda kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="07152-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="07152-121">Merhaba en güncel bildirimleri için kullanılabilirlik ve bu özellik durumunu hello Azure Virtual Network güncelleştirmeleri sayfasında denetleyin.</span><span class="sxs-lookup"><span data-stu-id="07152-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="07152-122">Avantajlar</span><span class="sxs-lookup"><span data-stu-id="07152-122">Benefits</span></span>
* <span data-ttu-id="07152-123">**Düşük gecikme / saniye başına daha yüksek paket (pps):** kaldırma hello sanal anahtardan hello datapath hello ana bilgisayar ilke işleme için paketler harcadığınız hello zamanı kaldırır ve artar hello hello VM içinde işlenen paket sayısı.</span><span class="sxs-lookup"><span data-stu-id="07152-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="07152-124">**Değişim azaltılmış:** sanal anahtar hello uygulanan toobe gereken ilke miktarını ve hello işlem yaptığını hello iş yükü hello CPU, üzerinde işlem bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="07152-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="07152-125">Hello ilkesi zorlama toohello donanım yük boşaltma, paketleri toohello hello konak tooVM iletişim ve tüm yazılım kesmelerini ve bağlam kaldırma VM anahtarları doğrudan sunarak bu değişkenlik kaldırır.</span><span class="sxs-lookup"><span data-stu-id="07152-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="07152-126">**Düşük CPU kullanımı:** Bypassing hello sanal anahtarda hello ana ağ trafiğini işlemek için CPU kullanımı tooless yol açar.</span><span class="sxs-lookup"><span data-stu-id="07152-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="07152-127"><a name="Limitations"></a>Sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="07152-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="07152-128">Bu özelliği kullanırken aşağıdaki sınırlamalar hello mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="07152-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="07152-129">**Ağ arabirimi oluşturma:** hızlandırılmış ağ yalnızca yeni bir NIC için etkinleştirilmesi</span><span class="sxs-lookup"><span data-stu-id="07152-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="07152-130">Varolan bir NIC için etkinleştirilemez</span><span class="sxs-lookup"><span data-stu-id="07152-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="07152-131">**VM oluşturma:** etkin hızlandırılmış ağ ile bir NIC yalnızca VM oluşturulan hello zaman ekli tooa VM olması olabilir.</span><span class="sxs-lookup"><span data-stu-id="07152-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="07152-132">Merhaba NIC VM varolan ekli tooan olamaz.</span><span class="sxs-lookup"><span data-stu-id="07152-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="07152-133">**Bölgeler:** Windows VM hızlandırılmış ağ iletişimi ile birlikte, çoğu Azure bölgelerde sunulur.</span><span class="sxs-lookup"><span data-stu-id="07152-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="07152-134">Linux VM'ler hızlandırılmış ağ ile birden çok bölgede sunulur.</span><span class="sxs-lookup"><span data-stu-id="07152-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="07152-135">Bu özellik kullanılabilir hello bölgeleri genişletme.</span><span class="sxs-lookup"><span data-stu-id="07152-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="07152-136">Aşağıda hello Azure sanal ağı güncelleştirmeleri blog hello en son bilgiler için bkz.</span><span class="sxs-lookup"><span data-stu-id="07152-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="07152-137">**Desteklenen işletim sistemleri:** Windows: Microsoft Windows Server 2012 R2 Datacenter ve Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="07152-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="07152-138">Linux: Ubuntu Server 16.04 LTS çekirdek 4.4.0-77 veya sonrası, SLES 12 SP2, RHEL 7.3 ve CentOS 7.3 (yayımlanmış "Standart dışı Wave yazılım").</span><span class="sxs-lookup"><span data-stu-id="07152-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="07152-139">**VM boyutu:** genel amaçlı ve en az sekiz çekirdeği ile işlem iyileştirilmiş örnek boyutları.</span><span class="sxs-lookup"><span data-stu-id="07152-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="07152-140">Daha fazla bilgi için bkz: Merhaba [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ve [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM boyutları makaleleri.</span><span class="sxs-lookup"><span data-stu-id="07152-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="07152-141">Merhaba desteklenen VM örneği boyutlarının kümesi hello gelecekteki genişletilir.</span><span class="sxs-lookup"><span data-stu-id="07152-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="07152-142">**Dağıtım Azure Resource Manager (ARM) aracılığıyla yalnızca:** hızlandırılmış ağ ASM/RDFE aracılığıyla dağıtımı için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="07152-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="07152-143">Değişiklikleri toothese sınırlamalar hello duyurdu [Azure sanal ağı güncelleştirir](https://azure.microsoft.com/updates/accelerated-networking-in-preview) sayfası.</span><span class="sxs-lookup"><span data-stu-id="07152-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="07152-144">Windows VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="07152-144">Create a Windows VM</span></span>
<span data-ttu-id="07152-145">Hello Azure portalında veya Azure kullanabilirsiniz [PowerShell](#windows-powershell) toocreate hello VM.</span><span class="sxs-lookup"><span data-stu-id="07152-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="07152-146"><a name="windows-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="07152-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="07152-147">Bir Internet tarayıcısından hello Azure açın [portal](https://portal.azure.com) ve Azure ile oturum [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="07152-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="07152-148">Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="07152-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="07152-149">Merhaba Portalı'nda tıklatın **+ yeni** > **işlem** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="07152-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="07152-150">Merhaba, **Windows Server 2016 Datacenter** görünür, dikey bırakın *Resource Manager* altında seçilen **dağıtım modeli seçin**, tıklatıp **oluştur** .</span><span class="sxs-lookup"><span data-stu-id="07152-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="07152-151">Merhaba, **Temelleri** görünür, dikey hello aşağıdaki değerleri girin, varsayılan seçenekleri kalan hello bırakın veya seçin ya da kendi değerlerinizi girin ve hello'ı tıklatın **Tamam** düğmesi:</span><span class="sxs-lookup"><span data-stu-id="07152-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="07152-152">Ayar</span><span class="sxs-lookup"><span data-stu-id="07152-152">Setting</span></span>|<span data-ttu-id="07152-153">Değer</span><span class="sxs-lookup"><span data-stu-id="07152-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="07152-154">Ad</span><span class="sxs-lookup"><span data-stu-id="07152-154">Name</span></span>|<span data-ttu-id="07152-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="07152-155">MyVm</span></span>|
    |<span data-ttu-id="07152-156">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="07152-156">Resource group</span></span>|<span data-ttu-id="07152-157">Bırakın **Yeni Oluştur** seçili ve girin *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="07152-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="07152-158">Konum</span><span class="sxs-lookup"><span data-stu-id="07152-158">Location</span></span>|<span data-ttu-id="07152-159">Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="07152-159">West US 2</span></span>|

    <span data-ttu-id="07152-160">Yeni tooAzure değilseniz, hakkında daha fazla bilgi [kaynak grupları](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonelikleri](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), ve [konumları](https://azure.microsoft.com/regions) (tooas bölgeler adlandırılır da olduğu).</span><span class="sxs-lookup"><span data-stu-id="07152-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="07152-161">Merhaba, **bir boyutu seçin** görünür, dikey girin *8* hello içinde **Minimum çekirdek** kutusuna ve ardından **tümünü görüntülemek**.</span><span class="sxs-lookup"><span data-stu-id="07152-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="07152-162">Tıklatın **DS4_V2 standart**, veya desteklenen herhangi bir VM, hello ardından **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="07152-163">Merhaba, **ayarları** görünür, dikey olarak tüm ayarları bırakın-dışında tıklatın ise **etkin** altında **ağ hızlandırılmış**, hello'ye tıklayın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="07152-164">**Not:** önceki adımlarda hello listelenmeyen değerleri VM boyutu, işletim sistemi veya konumu için seçtiğiniz, [sınırlamalar](#Limitations) bu makalenin bölümüne **hızlandırılmış ağ**görünür değil.</span><span class="sxs-lookup"><span data-stu-id="07152-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="07152-165">Merhaba, **Özet** görünür, dikey tıklayın hello **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="07152-166">Azure hello VM oluşturma başlatır.</span><span class="sxs-lookup"><span data-stu-id="07152-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="07152-167">VM oluşturmak birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="07152-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="07152-168">tooinstall hello için Windows ağ sürücüsü hızlandırılmış, tam hello adımları hello [Windows'u yapılandırma](#configure-windows) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="07152-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="07152-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="07152-170">Hello Azure PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü.</span><span class="sxs-lookup"><span data-stu-id="07152-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="07152-171">Yeni tooAzure PowerShell değilseniz, hello okuma [Azure PowerShell genel bakış](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.</span><span class="sxs-lookup"><span data-stu-id="07152-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="07152-172">Windows Başlat hello düğmesini tıklatarak bir PowerShell oturumu Başlat yazarak **powershell**, ardından **PowerShell** hello Arama sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="07152-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="07152-173">Merhaba, PowerShell penceresinde girin `login-azurermaccount` Azure oturum komutu toosign [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="07152-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="07152-174">Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="07152-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="07152-175">Tarayıcınızda komut dosyası izleyen hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="07152-175">In your browser, copy hello following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="07152-176">PowerShell pencerenize toopaste hello komut dosyasını sağ tıklatın ve, yürütülmekte başlatın.</span><span class="sxs-lookup"><span data-stu-id="07152-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="07152-177">Bir kullanıcı adı ve parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="07152-177">You are prompted for a username and password.</span></span> <span data-ttu-id="07152-178">Bu kimlik bilgileri toolog toohello VM hello sonraki adımda tooit bağlanırken kullanın.</span><span class="sxs-lookup"><span data-stu-id="07152-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="07152-179">Merhaba komut başarısız olursa ve değerleri hello komut yürütülmeden önce değiştirilen VM boyutu, işletim sistemi için kullanılan hello değerlerini onaylayın ve konum hello listelenen [sınırlamalar](#Limitations) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="07152-180">tooinstall hello için Windows ağ sürücüsü hızlandırılmış, tam hello adımları hello [Windows'u yapılandırma](#configure-windows) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="07152-181"><a name="configure-windows"></a>Windows yapılandırma</span><span class="sxs-lookup"><span data-stu-id="07152-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="07152-182">Azure'da hello VM oluşturduktan sonra Windows hello hızlandırılmış ağ sürücüsü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="07152-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="07152-183">Aşağıdaki adımları hello tamamlamadan önce bir Windows VM ile hızlandırılmış ağ ya da hello kullanarak oluşturduğunuz gerekir [portal](#windows-portal) veya [PowerShell](#windows-powershell) bu makaledeki adımları.</span><span class="sxs-lookup"><span data-stu-id="07152-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="07152-184">Bir Internet tarayıcısından hello Azure açın [portal](https://portal.azure.com) ve Azure ile oturum [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="07152-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="07152-185">Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="07152-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="07152-186">Merhaba metni içeren hello kutusunda *arama kaynakları* hello Azure portal hello üstünde yazın *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="07152-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="07152-187">Zaman **MyVm** görünür hello arama sonuçlarında tıklatın.</span><span class="sxs-lookup"><span data-stu-id="07152-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="07152-188">Merhaba, **MyVm** görünür, dikey tıklayın hello **Bağlan** hello sol üst köşesindeki hello dikey düğmesini.</span><span class="sxs-lookup"><span data-stu-id="07152-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="07152-189">**Not:** varsa **oluşturma** hello altında görülebilir **Bağlan** düğmesi, Azure henüz tamamlanmadı hello VM oluşturma.</span><span class="sxs-lookup"><span data-stu-id="07152-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="07152-190">Tıklatın **Bağlan** yalnızca artık gördükten sonra **oluşturma** hello altında **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="07152-191">Tarayıcı toodownload hello izin **MyVm.rdp** dosya.</span><span class="sxs-lookup"><span data-stu-id="07152-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="07152-192">Yüklendikten sonra hello dosya tooopen'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="07152-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="07152-193">Merhaba tıklatın **Bağlan** hello düğmesini **Uzak Masaüstü Bağlantısı** görünür, o hello hello uzak bağlantının yayımcısının belirlenemedi bildiren kutusu.</span><span class="sxs-lookup"><span data-stu-id="07152-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="07152-194">Hello içinde **Windows Güvenlik** görünen kutusu **daha fazla seçenek**, ardından **farklı bir hesap kullanın**.</span><span class="sxs-lookup"><span data-stu-id="07152-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="07152-195">Merhaba kullanıcı adı ve 4. adımda girdiğiniz parola girin ve ardından hello **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="07152-196">Merhaba tıklatın **Evet** görünür, hello hello uzak bilgisayarın kimliği doğrulanamıyor bildiren hello Uzak Masaüstü Bağlantısı kutusundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="07152-197">Merhaba Windows Başlat düğmesine sağ tıklatın ve **Aygıt Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="07152-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="07152-198">Merhaba genişletin **ağ bağdaştırıcıları** düğümü.</span><span class="sxs-lookup"><span data-stu-id="07152-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="07152-199">Bu hello onaylayın **Mellanox ConnectX-3 sanal işlev Ethernet bağdaştırıcısı** hello resim aşağıdaki gösterildiği gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="07152-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Cihaz Yöneticisi](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="07152-201">Hızlandırılmış ağ, VM için etkinleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="07152-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="07152-202">Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="07152-202">Create a Linux VM</span></span>
<span data-ttu-id="07152-203">Hello Azure portalında veya Azure kullanabilirsiniz [PowerShell](#linux-powershell) toocreate bir Ubuntu veya SLES VM.</span><span class="sxs-lookup"><span data-stu-id="07152-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="07152-204">RHEL ve CentOS VM'ler için farklı bir iş akışı yok.</span><span class="sxs-lookup"><span data-stu-id="07152-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="07152-205">Merhaba yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="07152-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="07152-206"><a name="linux-portal"></a>Portal</span><span class="sxs-lookup"><span data-stu-id="07152-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="07152-207">Merhaba, 1-5 adımlarını izleyerek Linux Önizleme için ağ hızlandırılmış hello kaydolun [PowerShell bir Linux VM - oluşturma](#linux-powershell) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="07152-208">Merhaba portalında hello Önizleme için kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="07152-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="07152-209">1-8 içinde hello adımları tamamlayın [bir Windows VM - oluşturma portal](#windows-portal) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="07152-210">2. adımda tıklatın **Ubuntu Server 16.04 LTS** yerine **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="07152-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="07152-211">Üretim dağıtımları için ya da kullanabilirsiniz ancak bu öğretici için toouse bir SSH anahtarı yerine bir parola seçin.</span><span class="sxs-lookup"><span data-stu-id="07152-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="07152-212">Varsa **ağ hızlandırılmış** 7. adımını hello tamamladığınızda görünmez [bir Windows VM - oluşturma portal](#windows-portal) bölümünde bu makalede, büyük olasılıkla hello aşağıdaki nedenlerden biri için:</span><span class="sxs-lookup"><span data-stu-id="07152-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="07152-213">Henüz hello Önizleme için kayıtlı değil.</span><span class="sxs-lookup"><span data-stu-id="07152-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="07152-214">Kayıt durumu olduğunu onaylayın **kayıtlı**hello 4 adımda açıklandığı gibi [Powershell bir Linux VM - oluşturma](#linux-powershell) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="07152-215">**Not:** hello hızlandırılmış katıldıysanız Windows VM'ler için Önizleme (buna ait hiçbir uzun gerekli tooregister toouse hızlandırılmış Windows VM'ler için ağ), ağ, otomatik olarak Merhaba hızlandırılmış kayıtlı olmayan için ağ Linux VM'ler Önizleme.</span><span class="sxs-lookup"><span data-stu-id="07152-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="07152-216">Linux VM'ler tooparticipate da Önizleme için hello hızlandırılmış ağ için kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="07152-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="07152-217">Bir VM boyutu, işletim sistemi veya hello listelenen konum seçmediniz [sınırlamalar](#limitations) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="07152-218">Linux için tooinstall hello hızlandırılmış ağ sürücüsü, tam hello adımları hello [yapılandırma Linux](#configure-linux) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="07152-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="07152-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="07152-220">Bir abonelikte hızlandırılmış ağ ile Linux VM'ler oluşturmak ve ardından toocreate hello hızlandırılmış ağ ile bir Windows VM çalışırsanız aynı abonelik hello Windows VM oluşturma başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="07152-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="07152-221">Bu önizleme sırasında ayrı Aboneliklerde hızlandırılmış ağ ile Linux ve Windows VM'ler test önerilir.</span><span class="sxs-lookup"><span data-stu-id="07152-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="07152-222">Hello Azure PowerShell Hello en son sürümünü yüklemek [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modülü.</span><span class="sxs-lookup"><span data-stu-id="07152-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="07152-223">Yeni tooAzure PowerShell değilseniz, hello okuma [Azure PowerShell genel bakış](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.</span><span class="sxs-lookup"><span data-stu-id="07152-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="07152-224">Windows Başlat hello düğmesini tıklatarak bir PowerShell oturumu Başlat yazarak **powershell**, ardından **PowerShell** hello Arama sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="07152-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="07152-225">Merhaba, PowerShell penceresinde girin `login-azurermaccount` Azure oturum komutu toosign [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="07152-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="07152-226">Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="07152-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="07152-227">Azure için ağ hızlandırılmış hello kaydolun hello aşağıdaki adımları tamamlayarak önizleme:</span><span class="sxs-lookup"><span data-stu-id="07152-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="07152-228">Bir e-posta çok gönderme[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) Azure abonelik kimliği ve kullanım.</span><span class="sxs-lookup"><span data-stu-id="07152-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="07152-229">Aboneliğiniz etkinleştirilecek hakkında Microsoft'tan bir e-posta onayı için lütfen bekleyin.</span><span class="sxs-lookup"><span data-stu-id="07152-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="07152-230">Merhaba Önizleme için kayıtlı komutu tooconfirm aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="07152-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="07152-231">Adım 5 kadar ile devam etmeyin **kayıtlı** hello hello önceki komutu girdikten sonra çıktısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="07152-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="07152-232">Devam etmeden önce çıktı hello aşağıdaki gibi çıktı benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="07152-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="07152-233">Merhaba hızlandırılmış katıldıysanız Windows VM'ler için Önizleme (buna ait hiçbir uzun gerekli tooregister toouse hızlandırılmış Windows VM'ler için ağ), ağ, otomatik olarak Merhaba hızlandırılmış kayıtlı olmayan Linux VM'ler Önizleme için ağ.</span><span class="sxs-lookup"><span data-stu-id="07152-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="07152-234">Linux VM'ler tooparticipate da Önizleme için hello hızlandırılmış ağ için kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="07152-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="07152-235">Tarayıcınızda komut dosyası Ubuntu veya SLES istendiği gibi değiştirerek aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="07152-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="07152-236">Yeniden Redhat ve CentOS aşağıda açıklanan farklı bir iş akışı vardır:</span><span class="sxs-lookup"><span data-stu-id="07152-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="07152-237">PowerShell pencerenize toopaste hello komut dosyasını sağ tıklatın ve, yürütülmekte başlatın.</span><span class="sxs-lookup"><span data-stu-id="07152-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="07152-238">Bir kullanıcı adı ve parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="07152-238">You are prompted for a username and password.</span></span> <span data-ttu-id="07152-239">Bu kimlik bilgileri toolog toohello VM hello sonraki adımda tooit bağlanırken kullanın.</span><span class="sxs-lookup"><span data-stu-id="07152-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="07152-240">Merhaba komut başarısız olursa, onaylayın:</span><span class="sxs-lookup"><span data-stu-id="07152-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="07152-241">4. adımda açıklandığı gibi hello Önizleme için kayıtlı</span><span class="sxs-lookup"><span data-stu-id="07152-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="07152-242">VM boyutu, işletim sistemi türü veya konumu değerlerinin hello komut yürütülmeden önce değiştirdiğiniz varsa, hello değerleri hello listelenen [sınırlamalar](#Limitations) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="07152-243">Linux için tooinstall hello hızlandırılmış ağ sürücüsü, tam hello adımları hello [yapılandırma Linux](#configure-linux) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="07152-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="07152-244"><a name="configure-linux"></a>Linux yapılandırın</span><span class="sxs-lookup"><span data-stu-id="07152-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="07152-245">Azure'da hello VM oluşturduktan sonra Linux için hello hızlandırılmış ağ sürücüsü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="07152-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="07152-246">Aşağıdaki adımları hello tamamlamadan önce bir Linux VM ile hızlandırılmış ağ ya da hello kullanarak oluşturduğunuz gerekir [portal](#linux-portal) veya [PowerShell](#linux-powershell) bu makaledeki adımları.</span><span class="sxs-lookup"><span data-stu-id="07152-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="07152-247">Bir Internet tarayıcısından hello Azure açın [portal](https://portal.azure.com) ve Azure ile oturum [hesap](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="07152-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="07152-248">Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="07152-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="07152-249">Merhaba portal, toohello sağındaki hello hello üstündeki *arama kaynakları* çubuğu, hello tıklatın **> _** simgesi toostart Bash bulut Kabuğu (Önizleme).</span><span class="sxs-lookup"><span data-stu-id="07152-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="07152-250">Merhaba Bash bulut Kabuk bölmesi hello altındaki hello portal ve birkaç saniye sonra görünür sunan bir  **username@Azure:~ $** istemi.</span><span class="sxs-lookup"><span data-stu-id="07152-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="07152-251">Bilgisayar, yerine hello bulut Kabuk SSH toohello VM kullanabilirsiniz ancak bu öğreticideki yönergeler hello hello bulut Kabuk kullanmakta olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="07152-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="07152-252">Merhaba portal Hello üstünde hello metin içeren hello kutusunda *arama kaynakları*, türü *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="07152-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="07152-253">Zaman **MyVm** görünür hello arama sonuçlarında tıklatın.</span><span class="sxs-lookup"><span data-stu-id="07152-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="07152-254">Merhaba, **MyVm** görünür, dikey tıklayın hello **Bağlan** hello sol üst köşesindeki hello dikey düğmesini.</span><span class="sxs-lookup"><span data-stu-id="07152-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="07152-255">**Not:** varsa **oluşturma** hello altında görülebilir **Bağlan** düğmesi, Azure henüz tamamlanmadı hello VM oluşturma.</span><span class="sxs-lookup"><span data-stu-id="07152-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="07152-256">Tıklatın **Bağlan** yalnızca artık gördükten sonra **oluşturma** hello altında **Bağlan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="07152-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="07152-257">Azure açılır tooenter hello bildiren bir kutusu `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="07152-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="07152-258">ENTER hello bulut Kabuğu (veya onu görünen hello kutusundan adım 4 kopyalayın ve toohello bulut Kabuğu'nda yapıştırın), bu komutta ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="07152-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="07152-259">ENTER **Evet** toohello soru soran, toocontinue bağlanmak, isterseniz, ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="07152-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="07152-260">Merhaba VM oluştururken girdiğiniz hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="07152-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="07152-261">Gördüğünüz toohello VM, bir kez başarıyla oturum bir adminuser@MyVm:~ $ istemi.</span><span class="sxs-lookup"><span data-stu-id="07152-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="07152-262">Şimdi toohello VM hello bulut kabuk oturumu aracılığıyla kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="07152-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="07152-263">**Not:** 10 dakika işlem yapılmadıktan sonra bulut Kabuk oturumları zaman aşımına uğrar.</span><span class="sxs-lookup"><span data-stu-id="07152-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="07152-264">Bu noktada, hello yönergeleri kullanmakta olduğunuz hello dağıtım göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="07152-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="07152-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="07152-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="07152-266">Merhaba satırına girin `uname -r` ve hello sürümü için onaylayın:</span><span class="sxs-lookup"><span data-stu-id="07152-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="07152-267">Ubuntu olan "4.4.0-77-generic," veya daha büyük</span><span class="sxs-lookup"><span data-stu-id="07152-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="07152-268">SLES "4.4.59-92.20-default" olan veya daha büyük</span><span class="sxs-lookup"><span data-stu-id="07152-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="07152-269">Merhaba standart ağ Vnıc hızlandırılmış hello ağ Vnıc arasındaki bono izleyin çalışan hello komutlarıyla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="07152-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="07152-270">Hello hello bono ağ trafiği üzerinde bazı yapılandırma değişikliklerinin kesilmemesini sağlar ancak hızlandırılmış ağ Vnıc gerçekleştirme daha yüksek ağ trafiği kullanır.</span><span class="sxs-lookup"><span data-stu-id="07152-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="07152-271">60 saniye duraklatmak sonra çalışan hello betik sonra hello VM yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="07152-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="07152-272">Bir kez VM yeniden hello yeniden tooit adımları 5-7'yi yeniden tamamlanıyor.</span><span class="sxs-lookup"><span data-stu-id="07152-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="07152-273">Merhaba çalıştırmak `ifconfig` komut ve bond0 gündeme ve hello arabirimi yukarı gösteren onaylayın.</span><span class="sxs-lookup"><span data-stu-id="07152-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="07152-274">Hızlandırılmış ağ kullanan uygulamalar hello iletişim kurması gerekir *bond0* arabirim, *eth0*.</span><span class="sxs-lookup"><span data-stu-id="07152-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="07152-275">Genel kullanılabilirlik hızlandırılmış ağ erişmeden önce hello arabirim adı değişebilir.</span><span class="sxs-lookup"><span data-stu-id="07152-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="07152-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="07152-276">RHEL/CentOS</span></span>

<span data-ttu-id="07152-277">Red Hat Enterprise Linux veya CentOS 7.3 VM oluşturma tooload hello en son sürücülere SR-IOV ve hello sanal işlev (VF) sürücüsünün hello ağ kartı için gereken bazı ek adımlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="07152-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="07152-278">Merhaba hello yönergeleri ilk aşaması kullanılan toomake olabilir görüntünün bir veya daha fazla sanal hello sürücüleri önceden yüklenmiş olan makine hazırlar.</span><span class="sxs-lookup"><span data-stu-id="07152-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="07152-279">Aşama bir: Red Hat Enterprise Linux veya CentOS 7.3 temel görüntü hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="07152-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="07152-280">Bir olmayan - SRLOV CentOS 7.3 VM Azure sağlama</span><span class="sxs-lookup"><span data-stu-id="07152-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="07152-281">LIS 4.2.2 yükleyin:</span><span class="sxs-lookup"><span data-stu-id="07152-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="07152-282">Yapılandırma dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="07152-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="07152-283">Bu VM yetkisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="07152-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="07152-284">Azure portalından, bu VM'yi durdurun; ve tooVM'ın "disk" gidin, hello OSDisk'ın VHD URİ'si yakalayın.</span><span class="sxs-lookup"><span data-stu-id="07152-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="07152-285">Bu URI hello temel görüntünün VHD adını ve kendi depolama hesabını içerir.</span><span class="sxs-lookup"><span data-stu-id="07152-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="07152-286">İki aşama: sağlama yeni sanal makineleri Azure üzerinde</span><span class="sxs-lookup"><span data-stu-id="07152-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="07152-287">Sağlama ile yeni AzureRMVMConfig dayalı yeni VM'ler kullanarak temel görüntü bir hello vNIC üzerinde etkin AcceleratedNetworking ile evrede VHD hello:</span><span class="sxs-lookup"><span data-stu-id="07152-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="07152-288">Yukarı VM'ler önyükleme sonra "tarafından lspci" Merhaba VF aygıt denetleyin ve hello Mellanox girişi denetleyin.</span><span class="sxs-lookup"><span data-stu-id="07152-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="07152-289">Örneğin, biz bu öğede hello lspci çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="07152-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="07152-290">Merhaba bağlama betiği tarafından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="07152-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="07152-291">Yeniden başlatma yeni VM'ler hello:</span><span class="sxs-lookup"><span data-stu-id="07152-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="07152-292">Merhaba VM hello hızlandırılmış ağ yolu etkin ve yapılandırılmış bond0 ile başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="07152-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="07152-293">Çalıştırma `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="07152-293">Run `ifconfig` tooconfirm.</span></span>
