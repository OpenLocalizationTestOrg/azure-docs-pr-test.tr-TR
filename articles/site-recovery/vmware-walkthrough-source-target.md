---
title: "Kaynak ve hedef VMware Azure'a çoğaltma için Azure Site Recovery ile ayarlama | Microsoft Docs"
description: "Kaynak ve hedef ayarlarını Azure Site Recovery ile Azure depolama çoğaltma işlemi VMware sanal makinelerini ayarlama adımlarını özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 94b629a62c3a54eee69ee397b2f27e3f20b753d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-vmware-replication-to-azure"></a><span data-ttu-id="7220b-103">8. adım: kaynak ve hedef VMware çoğaltma Azure için ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7220b-103">Step 8: Set up the source and target for VMware replication to Azure</span></span>

<span data-ttu-id="7220b-104">Bu makale, şirket içi VMware sanal makinelerini Azure'a çoğaltırken kaynak ve hedef ayarlarını yapılandırmak açıklamaktadır kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="7220b-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="7220b-105">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7220b-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="7220b-106">Kaynak ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="7220b-106">Set up the source environment</span></span>

<span data-ttu-id="7220b-107">Yapılandırma sunucusunu ayarlamayı, kasaya kaydetmek ve Vm'leri bulma.</span><span class="sxs-lookup"><span data-stu-id="7220b-107">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="7220b-108">Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="7220b-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="7220b-109">Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="7220b-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="7220b-110">İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.</span><span class="sxs-lookup"><span data-stu-id="7220b-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="7220b-111">Site Recovery birleşik Kurulumu yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="7220b-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="7220b-112">Kasa kayıt anahtarını indir</span><span class="sxs-lookup"><span data-stu-id="7220b-112">Download the vault registration key.</span></span> <span data-ttu-id="7220b-113">Birleşik Kurulum'u çalıştırdığınızda bu gerekir.</span><span class="sxs-lookup"><span data-stu-id="7220b-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="7220b-114">Anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7220b-114">The key is valid for five days after you generate it.</span></span>

   ![Kaynağı ayarlama](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="7220b-116">Yapılandırma sunucusunu kasaya kaydetmek</span><span class="sxs-lookup"><span data-stu-id="7220b-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="7220b-117">Başlayın, ardından birleştirilmiş yapılandırma sunucusuna işlem sunucusu ve ana hedef sunucusu yüklemek üzere kurulumu çalıştırmadan önce aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="7220b-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span>
    - <span data-ttu-id="7220b-118">Hızlı bir video özeti</span><span class="sxs-lookup"><span data-stu-id="7220b-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="7220b-119">VM yapılandırma sunucusundaki sistem saatinin eşitlendiğinden emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="7220b-119">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="7220b-120">Eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="7220b-120">It should match.</span></span> <span data-ttu-id="7220b-121">Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="7220b-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="7220b-122">Kurulum, VM yapılandırma sunucusunda yerel yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7220b-122">Run setup as a Local Administrator on the configuration server VM.</span></span>
    - <span data-ttu-id="7220b-123">TLS 1.0 VM etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7220b-123">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="7220b-124">Yapılandırma sunucusu da yüklenebilir [komut satırından](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="7220b-124">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-to-vmware-servers"></a><span data-ttu-id="7220b-125">VMware sunucularına bağlanmak</span><span class="sxs-lookup"><span data-stu-id="7220b-125">Connect to VMware servers</span></span>

<span data-ttu-id="7220b-126">Azure Site Recovery, şirket içi ortamınızda çalışan sanal makineleri bulmak izin vermek için VMware vCenter Server veya vSphere ESXi konakları Site Recovery ile bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7220b-126">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="7220b-127">Başlamadan önce aşağıdakilere dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="7220b-127">Note the following before you start:</span></span>

- <span data-ttu-id="7220b-128">VCenter sunucusu veya Site kurtarma vSphere ana yönetici ayrıcalıklarına sahip olmayan bir hesapla sunucuda eklerseniz, hesap etkin Bu ayrıcalıkları gerekir:</span><span class="sxs-lookup"><span data-stu-id="7220b-128">If you add the vCenter server or vSphere hosts to Site Recovery with an account without administrator privileges on the server, the account needs these privileges enabled:</span></span>
    - <span data-ttu-id="7220b-129">Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine, vSphere dağıtılmış anahtar.</span><span class="sxs-lookup"><span data-stu-id="7220b-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="7220b-130">VCenter sunucusu depolama görünümleri izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7220b-130">The vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="7220b-131">Site Recovery VMware sunucular eklediğinizde, 15 dakika alabilir ya da sunumların portalda görünebilmesi daha uzun.</span><span class="sxs-lookup"><span data-stu-id="7220b-131">When you add VMware servers to Site Recovery, it can take 15 minutes or longer for them to appear in the portal.</span></span>

### <a name="add-the-account-for-automatic-discovery"></a><span data-ttu-id="7220b-132">Otomatik bulma hesabı Ekle</span><span class="sxs-lookup"><span data-stu-id="7220b-132">Add the account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="7220b-133">Bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="7220b-133">Set up a connection</span></span>

<span data-ttu-id="7220b-134">Sunuculara şu şekilde bağlanın:</span><span class="sxs-lookup"><span data-stu-id="7220b-134">Connect to servers as follows:</span></span>

1. <span data-ttu-id="7220b-135">Seçin **+ vCenter** bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="7220b-135">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="7220b-136">**vCenter Ekle** menüsünde vSphere konağı veya vCenter sunucusu için bir kolay ad belirtin ve ardından sunucunun IP adresini ya da FQDN’sini belirtin.</span><span class="sxs-lookup"><span data-stu-id="7220b-136">In **Add vCenter**, specify a friendly name for the vSphere host or vCenter server, and then specify the IP address or FQDN of the server.</span></span>
3. <span data-ttu-id="7220b-137">VMware sunucularınız farklı bir bağlantı noktasındaki istekleri dinleyecek şekilde yapılandırılmadıkça bağlantı noktasını 443 olarak bırakın.</span><span class="sxs-lookup"><span data-stu-id="7220b-137">Leave the port as 443 unless your VMware servers are configured to listen for requests on a different port.</span></span> <span data-ttu-id="7220b-138">VMware vCenter veya vSphere ESXi sunucusuna bağlanacak hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="7220b-138">Select the account that is to connect to the VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="7220b-139">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7220b-139">Click **OK**.</span></span>
4. <span data-ttu-id="7220b-140">Site Recovery belirtilen ayarları kullanarak VMware sunucularına bağlanır ve sanal makineleri bulur.</span><span class="sxs-lookup"><span data-stu-id="7220b-140">Site Recovery connects to VMware servers using the specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="7220b-141">Bir sunucu veya vCenter veya ana bilgisayar sunucusunda yönetici ayrıcalıklarına sahip olmayan bir hesapla konak ekliyorsanız, hesabın etkin Bu ayrıcalıkları olduğundan emin olun: Datacenter, veri deposu, klasör, ana bilgisayar, ağ, kaynak, sanal makine ve vSphere dağıtılmış anahtar.</span><span class="sxs-lookup"><span data-stu-id="7220b-141">If you're adding a server or host with an account that doesn't have administrator privileges on the vCenter or host server, make sure that the account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="7220b-142">Ayrıca, VMware vCenter server etkin depolama görünümleri ayrıcalık gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="7220b-142">In addition, the VMware vCenter server needs the Storage Views privilege enabled.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="7220b-143">Hedef ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="7220b-143">Set up the target environment</span></span>

<span data-ttu-id="7220b-144">Hedef ortamını ayarlama önce bir Azure depolama hesabı ve sanal ağ kurulumu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7220b-144">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="7220b-145">**Altyapıyı hazırlama** > **Hedef** seçeneklerine tıklayıp kullanmak istediğiniz Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="7220b-145">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="7220b-146">Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.</span><span class="sxs-lookup"><span data-stu-id="7220b-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="7220b-147">Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="7220b-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Hedef](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="7220b-149">Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, bir kaynak yöneticisi hesabı oluşturun veya satır içi ağ.</span><span class="sxs-lookup"><span data-stu-id="7220b-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7220b-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7220b-150">Next steps</span></span>

<span data-ttu-id="7220b-151">Git [adım 9: bir çoğaltma ilkesini ayarlayın](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="7220b-151">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
