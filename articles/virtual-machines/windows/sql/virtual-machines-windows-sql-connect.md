---
title: aaaConnect tooa SQL Server sanal makinesine (Resource Manager) | Microsoft Docs
description: "Bilgi nasıl tooconnect tooSQL Server azure'da sanal makine üzerinde çalışan. Bu konuda hello Klasik dağıtım modeli kullanır. Hello senaryoları hello ağ yapılandırmasını ve hello istemci hello konumunu bağlı olarak farklılık gösterir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="74888-105">Tooa Azure (Kaynak Yöneticisi) SQL Server sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="74888-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74888-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="74888-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="74888-107">Klasik</span><span class="sxs-lookup"><span data-stu-id="74888-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="74888-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="74888-108">Overview</span></span>

<span data-ttu-id="74888-109">Bu konuda nasıl tooconnect tooyour SQL Server örneği bir Azure sanal makine üzerinde çalışan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="74888-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="74888-110">Bazı kapsayan [genel bağlantı senaryoları](#connection-scenarios) ve ardından sağlar [ayrıntılı bir Azure VM'de SQL Server bağlantısı yapılandırma adımları](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="74888-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="74888-111">Hem sağlama hem de bağlantı tam bir gözden geçirme olurdu olup [Azure üzerinde bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="74888-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="74888-112">Bağlantı senaryoları</span><span class="sxs-lookup"><span data-stu-id="74888-112">Connection scenarios</span></span>

<span data-ttu-id="74888-113">Merhaba yolu bir istemci bir sanal makinede çalışan sunucu hello hello istemci ve konumunu hello ağ yapılandırmasına bağlı olarak farklı tooSQL bağlanır.</span><span class="sxs-lookup"><span data-stu-id="74888-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="74888-114">SQL Server VM hello Azure portal ile sağlarsanız, hello türünü belirleyen hello seçeneğiniz **SQL Bağlantısı**.</span><span class="sxs-lookup"><span data-stu-id="74888-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Sağlama sırasında ortak SQL bağlantı seçeneği](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="74888-116">Bağlantı için seçenekleriniz şunlardır:</span><span class="sxs-lookup"><span data-stu-id="74888-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="74888-117">Seçenek</span><span class="sxs-lookup"><span data-stu-id="74888-117">Option</span></span> | <span data-ttu-id="74888-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="74888-118">Description</span></span> |
|---|---|
| <span data-ttu-id="74888-119">**Ortak**</span><span class="sxs-lookup"><span data-stu-id="74888-119">**Public**</span></span> | <span data-ttu-id="74888-120">TooSQL sunucu hello üzerinden bağlanma Internet</span><span class="sxs-lookup"><span data-stu-id="74888-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="74888-121">**Özel**</span><span class="sxs-lookup"><span data-stu-id="74888-121">**Private**</span></span> | <span data-ttu-id="74888-122">Merhaba içinde sunucu tooSQL bağlanmak aynı sanal ağ</span><span class="sxs-lookup"><span data-stu-id="74888-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="74888-123">**Yerel**</span><span class="sxs-lookup"><span data-stu-id="74888-123">**Local**</span></span> | <span data-ttu-id="74888-124">TooSQL sunucu hello yerel olarak bağlanmak aynı sanal makine</span><span class="sxs-lookup"><span data-stu-id="74888-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="74888-125">Merhaba aşağıdaki bölümlerde açıklanmıştır hello **ortak** ve **özel** daha ayrıntılı seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="74888-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="74888-126">TooSQL sunucu hello Internet üzerinden Bağlan</span><span class="sxs-lookup"><span data-stu-id="74888-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="74888-127">Tooconnect tooyour SQL Server veritabanı altyapısı, hello Internet istiyorsanız seçin **ortak** hello için **SQL Bağlantısı** sağlama sırasında hello portalında türü.</span><span class="sxs-lookup"><span data-stu-id="74888-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="74888-128">Merhaba portal otomatik olarak adımları hello:</span><span class="sxs-lookup"><span data-stu-id="74888-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="74888-129">Merhaba TCP/IP Protokolü SQL Server için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="74888-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="74888-130">Bir güvenlik duvarı kuralı tooopen hello SQL Server TCP bağlantı noktası (varsayılan 1433) yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="74888-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="74888-131">SQL Server ortak erişim için gerekli kimlik doğrulamasını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="74888-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="74888-132">Merhaba ağ güvenlik grubu hello hello SQL Server bağlantı noktasında VM tooall TCP trafiğine yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="74888-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74888-133">otomatik olarak hello SQL Server Geliştirici Hello sanal makine görüntülerinin ve Express sürümleri hello TCP/IP Protokolü etkinleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="74888-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="74888-134">Geliştirici ve Express sürümleri için SQL Server Configuration Manager çok kullanmalısınız[el ile Merhaba TCP/IP protokolünü etkinleştirin](#manualtcp) VM hello oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="74888-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="74888-135">İnternet erişimi olan herhangi bir istemci toohello SQL Server örneği hello genel IP adresi hello sanal makinenin veya toothat IP adresi atanmış herhangi bir DNS etiketi belirterek bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="74888-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="74888-136">Merhaba SQL Server bağlantı noktası 1433 ise, toospecify gerekmez hello bağlantı dizesi içinde.</span><span class="sxs-lookup"><span data-stu-id="74888-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="74888-137">bağlantı dizesi aşağıdaki hello tooa SQL VM ile bir DNS etiketi bağlanır, `sqlvmlabel.eastus.cloudapp.azure.com` SQL kimlik doğrulaması (Ayrıca kullanabileceğiniz hello genel IP adresi) kullanarak.</span><span class="sxs-lookup"><span data-stu-id="74888-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="74888-138">Bu bağlantı için istemciler üzerinde sağlar, ancak internet Merhaba, bu herkes tooyour SQL Server bağlanabilir anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="74888-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="74888-139">Dış istemcileri toohello doğru kullanıcı adı ve parolaya sahip.</span><span class="sxs-lookup"><span data-stu-id="74888-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="74888-140">Ancak, ek güvenlik için hello iyi bilinen bağlantı noktası 1433 önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74888-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="74888-141">Örneğin, SQL Server toolisten 1500 bağlantı noktasında ve kurulan uygun güvenlik duvarı ve ağ güvenlik grubu kural yapılandırdıysanız, başlangıç bağlantı noktası numarası toohello sunucu adı eklenerek bağlanamadı.</span><span class="sxs-lookup"><span data-stu-id="74888-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="74888-142">Merhaba aşağıdaki örnek hello önceki bir özel bağlantı noktası numarası ekleyerek değiştirir **1500**, toohello sunucu adı:</span><span class="sxs-lookup"><span data-stu-id="74888-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="74888-143">Üzerinden bir VM'de SQL Server sorguladığınızda Internet, tüm giden veri hello hello Azure ' veri merkezi konu toonormal olan [giden veri aktarımları fiyatlandırma](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="74888-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="74888-144">Bir sanal ağ içinde sunucu tooSQL Bağlan</span><span class="sxs-lookup"><span data-stu-id="74888-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="74888-145">Seçtiğinizde **özel** hello için **SQL Bağlantısı** hello portalındaki Azure türünü yapılandırır aynı hello ayarlarının çoğu çok**ortak**.</span><span class="sxs-lookup"><span data-stu-id="74888-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="74888-146">Merhaba tek fark hiçbir ağ güvenlik grubu kural tooallow hello SQL Server bağlantı noktası (varsayılan 1433) trafiğine dışında olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="74888-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="74888-147">otomatik olarak hello SQL Server Geliştirici Hello sanal makine görüntülerinin ve Express sürümleri hello TCP/IP Protokolü etkinleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="74888-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="74888-148">Geliştirici ve Express sürümleri için SQL Server Configuration Manager çok kullanmalısınız[el ile Merhaba TCP/IP protokolünü etkinleştirin](#manualtcp) VM hello oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="74888-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="74888-149">Özel bağlantı ile birlikte kullanılan genellikle [sanal ağ](../../../virtual-network/virtual-networks-overview.md), birkaç senaryo sağlar.</span><span class="sxs-lookup"><span data-stu-id="74888-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="74888-150">Sanal makineleri aynı sanal ağ, bu durumunda bile sanal makineleri farklı kaynak gruplarında mevcut hello olarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="74888-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="74888-151">İle bir [siteden siteye VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), şirket içi ağlar ve makineler VM'ler bağlayan bir karma mimarisi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74888-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="74888-152">Sanal ağlar, toojoin de Azure Vm'lerde tooa etki alanınızın etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="74888-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="74888-153">Merhaba tek yolu toouse Windows kimlik doğrulaması tooSQL sunucu budur.</span><span class="sxs-lookup"><span data-stu-id="74888-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="74888-154">Merhaba bağlantı gerektiren diğer senaryolar SQL kimlik doğrulaması kullanıcı adları ve parolalar.</span><span class="sxs-lookup"><span data-stu-id="74888-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="74888-155">Sanal ağınıza DNS yapılandırmış olduğunuz varsayılarak hello bağlantı dizesinde hello SQL Server VM bilgisayar adını belirterek tooyour SQL Server örneği bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="74888-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="74888-156">Ayrıca aşağıdaki örneğine hello Windows kimlik doğrulaması da yapılandırılmış ve bu hello kullanıcı erişimi toohello SQL Server örneği verildi varsayar.</span><span class="sxs-lookup"><span data-stu-id="74888-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="74888-157"><a id="change"></a>SQL bağlantı ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="74888-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="74888-158">Hello Azure portal, SQL Server sanal makine için başlangıç bağlantı ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74888-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="74888-159">Hello Azure portal, seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="74888-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="74888-160">SQL Server VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="74888-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="74888-161">Altında **ayarları**, tıklatın **SQL Server yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="74888-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="74888-162">Değişiklik hello **SQL bağlantı düzeyi** gerekli tooyour ayarlama.</span><span class="sxs-lookup"><span data-stu-id="74888-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="74888-163">İsteğe bağlı olarak, bu alanı toochange hello SQL Server bağlantı noktası veya hello SQL kimlik doğrulaması ayarlarını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74888-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![SQL Bağlantısı değiştirme](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="74888-165">Merhaba güncelleştirme toocomplete birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="74888-165">Wait several minutes for hello update toocomplete.</span></span>

   ![SQL VM güncelleştirme bildirimi](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="74888-167"><a id="manualtcp"></a>Geliştirici ve Express sürümleri için TCP/IP'yi etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="74888-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="74888-168">SQL Server bağlantı ayarları değiştirirken, Azure otomatik olarak hello TCP/IP Protokolü SQL Server Developer ve Express sürümleri için izin vermez.</span><span class="sxs-lookup"><span data-stu-id="74888-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="74888-169">nasıl toomanually etkinleştirmek TCP/IP'yi IP adresi ile uzaktan bağlanabilmesi Hello adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="74888-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="74888-170">İlk olarak, Uzak Masaüstü'nü toohello SQL Server makinesinde bağlayın.</span><span class="sxs-lookup"><span data-stu-id="74888-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="74888-171">Ardından, hello TCP/IP protokolü ile etkinleştirmek **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="74888-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="74888-172">SSMS ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="74888-172">Connect with SSMS</span></span>

<span data-ttu-id="74888-173">Merhaba aşağıdaki adımları nasıl toocreate isteğe bağlı bir DNS etiketi Azure VM için Göster ve SQL Server Management Studio (SSMS) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="74888-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="74888-174">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="74888-174">Next Steps</span></span>

<span data-ttu-id="74888-175">Bu bağlantı adımlarını toosee sağlama yönergelere bakın [Azure üzerinde bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="74888-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="74888-176">Azure vm'lerinde SQL Server toorunning ilgili diğer konular için bkz: [Azure Virtual Machines'de SQL Server](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="74888-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
