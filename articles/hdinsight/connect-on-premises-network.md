---
title: "aaaConnect Hdınsight tooyour şirket içi ağ - Azure Hdınsight | Microsoft Docs"
description: "Tooyour şirket içi ağ bağlanmak ve nasıl toocreate bir Hdınsight kümesi bir Azure sanal ağında öğrenin. Nasıl tooconfigure ad çözümlemesi Hdınsight ve şirket içi ağınız arasında özel bir DNS sunucusu kullanılarak öğrenin."
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a><span data-ttu-id="1cbf2-104">Hdınsight tooyour şirket içi ağa bağlan</span><span class="sxs-lookup"><span data-stu-id="1cbf2-104">Connect HDInsight tooyour on-premise network</span></span>

<span data-ttu-id="1cbf2-105">Nasıl tooconnect Hdınsight tooyour ağ Azure sanal ağlar ve VPN ağ geçidi kullanarak şirket içi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-105">Learn how tooconnect HDInsight tooyour on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="1cbf2-106">Bu belge planlama bilgilerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-106">This document provides planning information on:</span></span>

* <span data-ttu-id="1cbf2-107">Bir Azure sanal tooyour bağlayan ağ içinde Hdınsight kullanarak ağ şirket içi.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-107">Using HDInsight in an Azure Virtual Network that connects tooyour on-premises network.</span></span>

* <span data-ttu-id="1cbf2-108">DNS ad çözümlemesi hello sanal ağ ve şirket içi ağınız arasında yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-108">Configuring DNS name resolution between hello virtual network and your on-premises network.</span></span>

* <span data-ttu-id="1cbf2-109">Ağ güvenlik grupları toorestrict Internet erişimi tooHDInsight yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-109">Configuring network security groups toorestrict internet access tooHDInsight.</span></span>

* <span data-ttu-id="1cbf2-110">Merhaba sanal ağda Hdınsight tarafından sağlanan bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-110">Ports provided by HDInsight on hello virtual network.</span></span>

## <a name="create-hello-virtual-network-configuration"></a><span data-ttu-id="1cbf2-111">Merhaba sanal ağ yapılandırması oluştur</span><span class="sxs-lookup"><span data-stu-id="1cbf2-111">Create hello Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cbf2-112">Bağlama hakkında adım adım kılavuz arıyorsanız, Hdınsight tooyour şirket içi bir Azure sanal ağı kullanarak ağ'yı, hello bkz [bağlanmak Hdınsight tooyour şirket içi ağ](connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-112">If you are looking for step by step guidance on connecting HDInsight tooyour on-premises network using an Azure Virtual Network, see hello [Connect HDInsight tooyour on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="1cbf2-113">Kullanım hello aşağıdaki belgeler toolearn nasıl toocreate bir Azure sanal bağlı tooyour ağ ağ içi:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-113">Use hello following documents toolearn how toocreate an Azure Virtual Network that is connected tooyour on-premises network:</span></span>
    
* [<span data-ttu-id="1cbf2-114">Hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-114">Using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="1cbf2-115">Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="1cbf2-116">Azure CLI’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="1cbf2-117">Ad çözümlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-117">Configure name resolution</span></span>

<span data-ttu-id="1cbf2-118">tooallow Hdınsight ve ada göre birleştirilmiş hello ağ toocommunicate kaynaklarında hello aşağıdaki eylemleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-118">tooallow HDInsight and resources in hello joined network toocommunicate by name, you must perform hello following actions:</span></span>

* <span data-ttu-id="1cbf2-119">Özel bir DNS sunucusu hello Azure sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-119">Create a custom DNS server in hello Azure Virtual Network.</span></span>

* <span data-ttu-id="1cbf2-120">Merhaba sanal ağ toouse hello özel DNS sunucusu hello varsayılan Azure özyinelemeli çözümleyici yerine yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-120">Configure hello virtual network toouse hello custom DNS server instead of hello default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="1cbf2-121">Merhaba özel DNS sunucusu ve şirket içi DNS sunucunuz arasında iletim yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-121">Configure forwarding between hello custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="1cbf2-122">Bu yapılandırma davranışı aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-122">This configuration enables hello following behavior:</span></span>

* <span data-ttu-id="1cbf2-123">Merhaba DNS sonekine sahip tam etki alanı adları için istekleri __hello sanal ağ için__ toohello özel DNS sunucusu iletilir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-123">Requests for fully qualified domain names that have hello DNS suffix __for hello virtual network__ are forwarded toohello custom DNS server.</span></span> <span data-ttu-id="1cbf2-124">Merhaba özel DNS sunucusu, daha sonra bu istekleri toohello başlangıç IP adresi döndürür Azure özyinelemeli çözümleyici iletir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-124">hello custom DNS server then forwards these requests toohello Azure Recursive Resolver, which returns hello IP address.</span></span>

* <span data-ttu-id="1cbf2-125">Tüm diğer isteklerden toohello şirket DNS sunucusuna iletilir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-125">All other requests are forwarded toohello on-premises DNS server.</span></span> <span data-ttu-id="1cbf2-126">Microsoft.com gibi ortak Internet kaynakların bile istekleri toohello şirket içi DNS sunucusu ad çözümlemesi için iletilir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-126">Even requests for public internet resources such as microsoft.com are forwarded toohello on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="1cbf2-127">Diyagram aşağıdaki hello çizgiler hello sanal ağın DNS soneki hello bitiş kaynaklara yönelik isteklerin ' dir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-127">In hello following diagram, green lines are requests for resources that end in hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="1cbf2-128">Mavi satırlar hello şirket içi ağ veya üzerinde kaynaklara yönelik isteklerin genel internet hello gelir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-128">Blue lines are requests for resources in hello on-premises network or on hello public internet.</span></span>

![Bu belgede kullanılan hello yapılandırmasında DNS isteklerine nasıl çözüleceğini diyagramı](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="1cbf2-130">Özel bir DNS sunucusu oluştur</span><span class="sxs-lookup"><span data-stu-id="1cbf2-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1cbf2-131">Oluşturma ve Hdınsight hello sanal ağınıza yüklemeden önce hello DNS sunucusu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-131">You must create and configure hello DNS server before installing HDInsight into hello virtual network.</span></span>

<span data-ttu-id="1cbf2-132">toocreate hello kullanan bir Linux VM [bağlamak](https://www.isc.org/downloads/bind/) DNS yazılım, aşağıdaki adımları kullanın hello:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-132">toocreate a Linux VM that uses hello [Bind](https://www.isc.org/downloads/bind/) DNS software, use hello following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="1cbf2-133">Merhaba aşağıdaki adımları kullanın hello [Azure portal](https://portal.azure.com) toocreate bir Azure sanal makine.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-133">hello following steps use hello [Azure portal](https://portal.azure.com) toocreate an Azure Virtual Machine.</span></span> <span data-ttu-id="1cbf2-134">Diğer yolları toocreate bir sanal makine için hello bkz [VM Oluştur - Azure CLI](../virtual-machines/linux/quick-create-cli.md) ve [VM Oluştur - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-134">For other ways toocreate a virtual machine, see hello [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="1cbf2-135">Merhaba gelen [Azure portal](https://portal.azure.com)seçin  __+__ , __işlem__, ve __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-135">From hello [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Ubuntu sanal makine oluşturma](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="1cbf2-137">Merhaba gelen __Temelleri__ bölümünde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-137">From hello __Basics__ section, enter hello following information:</span></span>

    * <span data-ttu-id="1cbf2-138">__Ad__: Bu sanal makineyi tanımlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="1cbf2-139">Örneğin, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="1cbf2-140">__Kullanıcı adı__: hello SSH hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-140">__User name__: hello name of hello SSH account.</span></span>
    * <span data-ttu-id="1cbf2-141">__SSH ortak anahtarını__ veya __parola__: Merhaba hello SSH hesabı için kimlik doğrulama yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-141">__SSH public key__ or __Password__: hello authentication method for hello SSH account.</span></span> <span data-ttu-id="1cbf2-142">Daha güvenli olarak ortak anahtarları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="1cbf2-143">Daha fazla bilgi için bkz: Merhaba [Linux VM'ler için SSH anahtarları oluşturma ve kullanma](../virtual-machines/linux/mac-create-ssh-keys.md) belge.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-143">For more information, see hello [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="1cbf2-144">__Kaynak grubu__: seçin __var olanı kullan__ve ardından daha önce oluşturduğunuz hello sanal ağ içeren hello kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-144">__Resource group__: Select __Use existing__, and then select hello resource group that contains hello virtual network created earlier.</span></span>
    * <span data-ttu-id="1cbf2-145">__Konum__: Merhaba hello sanal ağ ile aynı konumda seçin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-145">__Location__: Select hello same location as hello virtual network.</span></span>

    ![Sanal makine temel yapılandırma](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="1cbf2-147">Merhaba diğer girişler varsayılan değerleri bırakın ve ardından __Tamam__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-147">Leave other entries at hello default values and then select __OK__.</span></span>

3. <span data-ttu-id="1cbf2-148">Merhaba gelen __bir boyutu seçin__ bölümünde, select hello VM boyutu.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-148">From hello __Choose a size__ section, select hello VM size.</span></span> <span data-ttu-id="1cbf2-149">Bu öğretici için en küçük hello seçin ve seçeneği en düşük maliyeti.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-149">For this tutorial, select hello smallest and lowest cost option.</span></span> <span data-ttu-id="1cbf2-150">toocontinue, kullanım hello __seçin__ düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-150">toocontinue, use hello __Select__ button.</span></span>

4. <span data-ttu-id="1cbf2-151">Merhaba gelen __ayarları__ bölümünde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-151">From hello __Settings__ section, enter hello following information:</span></span>

    * <span data-ttu-id="1cbf2-152">__Sanal ağ__: Merhaba daha önce oluşturduğunuz sanal ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-152">__Virtual network__: Select hello virtual network that you created earlier.</span></span>

    * <span data-ttu-id="1cbf2-153">__Alt ağ__: hello sanal ağ için hello varsayılan alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-153">__Subnet__: Select hello default subnet for hello virtual network.</span></span> <span data-ttu-id="1cbf2-154">Yapmak __değil__ hello hello VPN ağ geçidi tarafından kullanılan alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-154">Do __not__ select hello subnet used by hello VPN gateway.</span></span>

    * <span data-ttu-id="1cbf2-155">__Tanılama depolama hesabı__: mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Sanal ağ ayarları](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="1cbf2-157">Bırakın hello diğer girişler hello varsayılan değerinde sonra seçin __Tamam__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-157">Leave hello other entries at hello default value, then select __OK__ toocontinue.</span></span>

5. <span data-ttu-id="1cbf2-158">Merhaba gelen __satın alma__ bölümü, select hello __satın alma__ düğmesini toocreate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-158">From hello __Purchase__ section, select hello __Purchase__ button toocreate hello virtual machine.</span></span>

6. <span data-ttu-id="1cbf2-159">Merhaba sanal makine oluşturulduktan sonra kendi __genel bakış__ bölümünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-159">Once hello virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="1cbf2-160">Merhaba hello soldaki listesinden __özellikleri__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-160">From hello list on hello left, select __Properties__.</span></span> <span data-ttu-id="1cbf2-161">Merhaba Kaydet __genel IP adresi__ ve __özel IP adresi__ değerleri.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-161">Save hello __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="1cbf2-162">Merhaba sonraki bölümde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-162">It will be used in hello next section.</span></span>

    ![Ortak ve özel IP adresleri](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="1cbf2-164">Yükleme ve bağlama (DNS yazılım) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="1cbf2-165">SSH tooconnect toohello kullanmak __genel IP adresi__ hello sanal makinenin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-165">Use SSH tooconnect toohello __public IP address__ of hello virtual machine.</span></span> <span data-ttu-id="1cbf2-166">Aşağıdaki örnek hello 40.68.254.142 tooa sanal makinenin bağlanır:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-166">hello following example connects tooa virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="1cbf2-167">Değiştir `sshuser` hello SSH kullanıcı hesabı ile Merhaba kümesi oluştururken belirttiğiniz.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-167">Replace `sshuser` with hello SSH user account you specified when creating hello cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1cbf2-168">Yolları tooobtain hello çeşitli vardır `ssh` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-168">There are a variety of ways tooobtain hello `ssh` utility.</span></span> <span data-ttu-id="1cbf2-169">Linux, Unix ve macOS üzerinde hello işletim sisteminin bir parçası sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-169">On Linux, Unix, and macOS, it is provided as part of hello operating system.</span></span> <span data-ttu-id="1cbf2-170">Windows kullanıyorsanız, aşağıdaki seçenekleri şu hello birini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-170">If you are using Windows, consider one of hello following options:</span></span>
    >
    > * [<span data-ttu-id="1cbf2-171">Azure bulut Kabuğu</span><span class="sxs-lookup"><span data-stu-id="1cbf2-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="1cbf2-172">Windows 10 Ubuntu bash</span><span class="sxs-lookup"><span data-stu-id="1cbf2-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="1cbf2-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="1cbf2-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="1cbf2-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="1cbf2-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="1cbf2-175">tooinstall bağlama hello SSH oturumundan komutları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-175">tooinstall Bind, use hello following commands from hello SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="1cbf2-176">tooconfigure bağlama tooforward ad çözümleme istekleri tooyour şirket içi DNS sunucusu kullanın metin hello Merhaba içeriğine aşağıdaki hello `/etc/bind/named.conf.options` dosyası:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-176">tooconfigure Bind tooforward name resolution requests tooyour on-prem DNS server, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="1cbf2-177">Hello başlangıç değerleri değiştirin `goodclients` hello IP adres aralığı bir bölümle hello sanal ağ ve şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-177">Replace hello values in hello `goodclients` section with hello IP address range of hello virtual network and on-premises network.</span></span> <span data-ttu-id="1cbf2-178">Bu bölümde, bu DNS sunucusu gelen istekleri kabul hello adreslerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-178">This section defines hello addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="1cbf2-179">Hello yerine `192.168.0.1` hello girişi `forwarders` hello IP adresine sahip bir bölüm şirket içi DNS sunucunuzun.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-179">Replace hello `192.168.0.1` entry in hello `forwarders` section with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="1cbf2-180">Bu giriş yolları DNS isteklerini tooyour çözümlemesi için DNS sunucusu şirket içi.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-180">This entry routes DNS requests tooyour on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="1cbf2-181">tooedit bu dosya, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-181">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="1cbf2-182">toosave hello dosya, kullanım __Ctrl + X__, __Y__ve ardından __Enter__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-182">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="1cbf2-183">Merhaba SSH oturumundan hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-183">From hello SSH session, use hello following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="1cbf2-184">Bu komut metnini izleyen bir değer benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-184">This command returns a value similar toohello following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="1cbf2-185">Merhaba `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` metindir hello __DNS soneki__ bu sanal ağ için.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-185">hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is hello __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="1cbf2-186">Bu değer daha sonra kullanılmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="1cbf2-187">tooconfigure bağlama tooresolve DNS adlarını hello sanal ağ içindeki kaynakların kullanmak metin hello Merhaba içeriğine aşağıdaki hello `/etc/bind/named.conf.local` dosyası:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-187">tooconfigure Bind tooresolve DNS names for resources within hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="1cbf2-188">Merhaba değiştirmelisiniz `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` daha önce hello DNS soneki.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-188">You must replace hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with hello DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="1cbf2-189">tooedit bu dosya, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-189">tooedit this file, use hello following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="1cbf2-190">toosave hello dosya, kullanım __Ctrl + X__, __Y__ve ardından __Enter__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-190">toosave hello file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="1cbf2-191">toostart bağlama hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-191">toostart Bind, use hello following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="1cbf2-192">bağlama tooverify kaynakların şirket içi ağınızda, aşağıdaki komutları kullanın hello hello adları çözümleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-192">tooverify that bind can resolve hello names of resources in your on-premises network, use hello following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1cbf2-193">Değiştir `dns.mynetwork.net` , şirket içi ağınıza bir kaynak hello tam etki alanı adı (FQDN).</span><span class="sxs-lookup"><span data-stu-id="1cbf2-193">Replace `dns.mynetwork.net` with hello fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="1cbf2-194">Değiştir `10.0.0.4` hello ile __iç IP adresi__ özel DNS sunucunuzun hello sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-194">Replace `10.0.0.4` with hello __internal IP address__ of your custom DNS server in hello virtual network.</span></span>

    <span data-ttu-id="1cbf2-195">Merhaba yanıt metni aşağıdaki benzer toohello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-195">hello response appears similar toohello following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a><span data-ttu-id="1cbf2-196">Merhaba sanal ağ toouse hello özel DNS sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-196">Configure hello virtual network toouse hello custom DNS server</span></span>

<span data-ttu-id="1cbf2-197">tooconfigure hello sanal ağ toouse hello özel DNS sunucusu hello Azure özyinelemeli çözümleyici yerine hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-197">tooconfigure hello virtual network toouse hello custom DNS server instead of hello Azure recursive resolver, use hello following steps:</span></span>

1. <span data-ttu-id="1cbf2-198">Merhaba, [Azure portal](https://portal.azure.com)hello sanal ağ seçin ve ardından __DNS sunucuları__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-198">In hello [Azure portal](https://portal.azure.com), select hello virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="1cbf2-199">Seçin __özel__ve hello girin __iç IP adresi__ hello özel DNS sunucusunun.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-199">Select __Custom__, and enter hello __internal IP address__ of hello custom DNS server.</span></span> <span data-ttu-id="1cbf2-200">Son olarak, seçin __kaydetmek__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-200">Finally, select __Save__.</span></span>

    ![Merhaba ağ Hello özel DNS sunucusunu ayarlayın](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a><span data-ttu-id="1cbf2-202">Merhaba şirket içi DNS sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-202">Configure hello on-premises DNS server</span></span>

<span data-ttu-id="1cbf2-203">Merhaba önceki bölümde hello özel DNS sunucusu tooforward istekleri toohello şirket içi DNS sunucusu yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-203">In hello previous section, you configured hello custom DNS server tooforward requests toohello on-premises DNS server.</span></span> <span data-ttu-id="1cbf2-204">Ardından, hello şirket içi DNS sunucusu tooforward istekleri toohello özel DNS sunucusu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-204">Next, you must configure hello on-premises DNS server tooforward requests toohello custom DNS server.</span></span>

<span data-ttu-id="1cbf2-205">Belirli adımları için tooconfigure DNS sunucunuzun, DNS sunucusu yazılımınızı için hello belgelere.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-205">For specific steps on how tooconfigure your DNS server, consult hello documentation for your DNS server software.</span></span> <span data-ttu-id="1cbf2-206">Merhaba adımları arayın tooconfigure bir __koşullu ileticisi__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-206">Look for hello steps on how tooconfigure a __conditional forwarder__.</span></span>

<span data-ttu-id="1cbf2-207">Koşullu iletme, yalnızca belirli bir DNS soneki isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="1cbf2-208">Bu durumda, iletici hello DNS soneki hello sanal ağ için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-208">In this case, you must configure a forwarder for hello DNS suffix of hello virtual network.</span></span> <span data-ttu-id="1cbf2-209">Bu soneki isteklerinde hello özel DNS sunucusunun IP adresini toohello iletilmesi gereken.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-209">Requests for this suffix should be forwarded toohello IP address of hello custom DNS server.</span></span> 

<span data-ttu-id="1cbf2-210">Merhaba aşağıdaki hello iletici yapılandırması örneği metindir **bağlamak** DNS yazılım:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-210">hello following text is an example of a conditional forwarder configuration for hello **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

<span data-ttu-id="1cbf2-211">DNS kullanma hakkında bilgi için **Windows Server 2016**, hello bkz [Ekle DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) belgelerine...</span><span class="sxs-lookup"><span data-stu-id="1cbf2-211">For information on using DNS on **Windows Server 2016**, see hello [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="1cbf2-212">Merhaba şirket içi DNS sunucusunu yapılandırdıktan sonra kullanabileceğiniz `nslookup` hello şirket içi ağ tooverify hello sanal ağ adları, çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-212">Once you have configured hello on-premises DNS server, you can use `nslookup` from hello on-premises network tooverify that you can resolve names in hello virtual network.</span></span> <span data-ttu-id="1cbf2-213">Aşağıdaki örnek hello</span><span class="sxs-lookup"><span data-stu-id="1cbf2-213">hello following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="1cbf2-214">Kullanan şirket içi DNS sunucusunda 196.168.0.4 hello Bu örnek tooresolve hello hello özel DNS sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-214">This example uses hello on-premises DNS server at 196.168.0.4 tooresolve hello name of hello custom DNS server.</span></span> <span data-ttu-id="1cbf2-215">Başlangıç IP adresi hello şirket içi DNS sunucusu için hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-215">Replace hello IP address with hello one for hello on-premises DNS server.</span></span> <span data-ttu-id="1cbf2-216">Hello yerine `dnsproxy` hello tam olarak nitelenmiş etki alanı adıyla hello özel DNS sunucusunun adresi.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-216">Replace hello `dnsproxy` address with hello fully qualified domain name of hello custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="1cbf2-217">İsteğe bağlı: Denetim ağ trafiği</span><span class="sxs-lookup"><span data-stu-id="1cbf2-217">Optional: Control network traffic</span></span>

<span data-ttu-id="1cbf2-218">Ağ güvenlik grubu (NSG) veya kullanıcı tanımlı yolları (UDR) toocontrol ağ trafiğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-218">You can use network security groups (NSG) or user-defined routes (UDR) toocontrol network traffic.</span></span> <span data-ttu-id="1cbf2-219">Nsg'ler izin toofilter gelen ve giden trafiği ve izin verin veya hello trafiği reddedin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-219">NSGs allow you toofilter inbound and outbound traffic, and allow or deny hello traffic.</span></span> <span data-ttu-id="1cbf2-220">Udr'ler nasıl hello sanal ağınızdaki kaynaklara arasında trafiği akan toocontrol izin, Internet hello ve şirket içi ağ hello.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-220">UDRs allow you toocontrol how traffic flows between resources in hello virtual network, hello internet, and hello on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="1cbf2-221">Hdınsight hello Azure bulut, belirli IP adreslerinden gelen erişim ve sınırsız giden erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-221">HDInsight requires inbound access from specific IP addresses in hello Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="1cbf2-222">Nsg'ler veya Udr'ler toocontrol trafiği kullanırken hello aşağıdaki adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-222">When using NSGs or UDRs toocontrol traffic, you must perform hello following steps:</span></span>
>
> 1. <span data-ttu-id="1cbf2-223">Merhaba IP adresleri sanal ağınızı içeren hello konumunu bulun.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-223">Find hello IP addresses for hello location that contains your virtual network.</span></span> <span data-ttu-id="1cbf2-224">Konuma göre gerekli IP'leri listesi için bkz: [gerekli IP adreslerini](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="1cbf2-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="1cbf2-225">Merhaba IP adreslerinden gelen trafiğe izin verin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-225">Allow inbound traffic from hello IP addresses.</span></span>
>
>    * <span data-ttu-id="1cbf2-226">__NSG__: izin __gelen__ bağlantı noktasında trafik __443__ hello gelen __Internet__.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-226">__NSG__: Allow __inbound__ traffic on port __443__ from hello __Internet__.</span></span>
>    * <span data-ttu-id="1cbf2-227">__UDR__: kümesi hello __sonraki atlama__ hello rota too__Internet__ türü.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-227">__UDR__: Set hello __Next Hop__ type of hello route too__Internet__.</span></span>

<span data-ttu-id="1cbf2-228">Hello Azure PowerShell veya hello Azure CLI toocreate Nsg'leri kullanarak bir örnek için bkz: [genişletmek Hdınsight Azure sanal ağlar ile](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) belge.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-228">For an example of using Azure PowerShell or hello Azure CLI toocreate NSGs, see hello [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-hello-hdinsight-cluster"></a><span data-ttu-id="1cbf2-229">Merhaba Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-229">Create hello HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="1cbf2-230">Hdınsight hello sanal ağında yüklemeden önce hello özel DNS sunucusu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-230">You must configure hello custom DNS server before installing HDInsight in hello virtual network.</span></span>

<span data-ttu-id="1cbf2-231">Kullanım hello adımları hello [hello Azure portal kullanarak bir Hdınsight kümesi oluşturmayı](./hdinsight-hadoop-create-linux-clusters-portal.md) belge toocreate Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-231">Use hello steps in hello [Create an HDInsight cluster using hello Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="1cbf2-232">Küme oluşturma sırasında sanal ağınızı içeren hello konumu seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-232">During cluster creation, you must choose hello location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="1cbf2-233">Merhaba, __Gelişmiş ayarları__ bölümü yapılandırmasına, hello sanal ağ ve daha önce oluşturduğunuz alt seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-233">In hello __Advanced settings__ part of configuration, you must select hello virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-toohdinsight"></a><span data-ttu-id="1cbf2-234">TooHDInsight bağlanma</span><span class="sxs-lookup"><span data-stu-id="1cbf2-234">Connecting tooHDInsight</span></span>

<span data-ttu-id="1cbf2-235">Hdınsight üzerinde çoğu belgelerine hello erişim toohello küme sahip olduğunuzu varsayar Internet.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-235">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="1cbf2-236">Https://CLUSTERNAME.azurehdinsight.net toohello kümesine bağlayabilirsiniz örneğin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-236">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1cbf2-237">Bu adres Nsg'ler kullandınız veya Udr'ler toorestrict erişimden hello Internet kullanılabilir değilse hello ortak ağ geçidi, kullanır.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-237">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="1cbf2-238">toodirectly tooHDInsight hello sanal ağ üzerinden bağlanmasına, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-238">toodirectly connect tooHDInsight through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="1cbf2-239">toodiscover hello iç tam etki alanı adları hello Hdınsight küme düğümlerinin yöntemler aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="1cbf2-239">toodiscover hello internal fully qualified domain names of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. <span data-ttu-id="1cbf2-240">bir hizmet, kullanılabilir toodetermine hello bağlantı noktasına bkz hello [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](./hdinsight-hadoop-port-settings-for-services.md) belge.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-240">toodetermine hello port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1cbf2-241">Merhaba baş düğümler üzerinde barındırılan bazı hizmetler aynı anda yalnızca bir düğümde etkin olur.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-241">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="1cbf2-242">Bir hizmet bir baş düğüm üzerindeki erişmeyi deneyin ve başarısız olursa, diğer baş düğüm toohello geçin.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-242">If you try accessing a service on one head node and it fails, switch toohello other head node.</span></span>
    >
    > <span data-ttu-id="1cbf2-243">Örneğin, Ambari yalnızca aynı anda bir baş düğüm üzerinde etkindir.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="1cbf2-244">Ambari bir baş düğüm üzerinde erişmeyi deneyin ve üzerinde çalıştırıldığı sonra 404 hatası döndürürse diğer baş düğüm hello.</span><span class="sxs-lookup"><span data-stu-id="1cbf2-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on hello other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cbf2-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1cbf2-245">Next steps</span></span>

* <span data-ttu-id="1cbf2-246">Sanal bir ağa Hdınsight kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure sanal ağları kullanarak Hdınsight](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="1cbf2-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="1cbf2-247">Azure sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1cbf2-247">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="1cbf2-248">Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1cbf2-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="1cbf2-249">Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1cbf2-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
