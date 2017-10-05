---
title: "Hdınsight, şirket içi ağınıza - Azure Hdınsight bağlanmak | Microsoft Docs"
description: "Bir Azure sanal ağında Hdınsight kümesi oluşturmak ve şirket içi ağınıza bağlayın öğrenin. Özel bir DNS sunucusu kullanarak Hdınsight ile şirket içi ağınız arasında ad çözümleme yapılandırmayı öğrenin."
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
ms.openlocfilehash: 6fc863010cc59e20e7d86ea9344489e574be75f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-hdinsight-to-your-on-premise-network"></a><span data-ttu-id="0abe7-104">Hdınsight, şirket içi ağınıza bağlanmak</span><span class="sxs-lookup"><span data-stu-id="0abe7-104">Connect HDInsight to your on-premise network</span></span>

<span data-ttu-id="0abe7-105">Hdınsight Azure sanal ağlar ve VPN ağ geçidi kullanarak şirket ağınıza bağlanmak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-105">Learn how to connect HDInsight to your on-premises network by using Azure Virtual Networks and a VPN gateway.</span></span> <span data-ttu-id="0abe7-106">Bu belge planlama bilgilerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="0abe7-106">This document provides planning information on:</span></span>

* <span data-ttu-id="0abe7-107">Bir Azure sanal ağındaki şirket içi ağınıza bağlanan Hdınsight kullanma.</span><span class="sxs-lookup"><span data-stu-id="0abe7-107">Using HDInsight in an Azure Virtual Network that connects to your on-premises network.</span></span>

* <span data-ttu-id="0abe7-108">Sanal ağ ve şirket içi ağınız arasında DNS ad çözümlemesini yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="0abe7-108">Configuring DNS name resolution between the virtual network and your on-premises network.</span></span>

* <span data-ttu-id="0abe7-109">Hdınsight için Internet erişimi kısıtlamak için ağ güvenlik gruplarını yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="0abe7-109">Configuring network security groups to restrict internet access to HDInsight.</span></span>

* <span data-ttu-id="0abe7-110">Hdınsight tarafından sağlanan sanal ağ bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="0abe7-110">Ports provided by HDInsight on the virtual network.</span></span>

## <a name="create-the-virtual-network-configuration"></a><span data-ttu-id="0abe7-111">Sanal ağ yapılandırması oluştur</span><span class="sxs-lookup"><span data-stu-id="0abe7-111">Create the Virtual network configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0abe7-112">Bağlama hakkında adım adım kılavuz arıyorsanız, şirket içi Hdınsight'a bir Azure sanal ağı kullanarak ağa, bkz: [şirket içi ağınıza bağlanmak Hdınsight](connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="0abe7-112">If you are looking for step by step guidance on connecting HDInsight to your on-premises network using an Azure Virtual Network, see the [Connect HDInsight to your on-premise network](connect-on-premises-network.md) document.</span></span>

<span data-ttu-id="0abe7-113">Bir Azure sanal şirket içi ağınıza bağlı ağ oluşturmayı öğrenmek için aşağıdaki belgeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-113">Use the following documents to learn how to create an Azure Virtual Network that is connected to your on-premises network:</span></span>
    
* [<span data-ttu-id="0abe7-114">Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="0abe7-114">Using the Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [<span data-ttu-id="0abe7-115">Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="0abe7-115">Using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [<span data-ttu-id="0abe7-116">Azure CLI’yi kullanma</span><span class="sxs-lookup"><span data-stu-id="0abe7-116">Using Azure CLI</span></span>](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a><span data-ttu-id="0abe7-117">Ad çözümlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0abe7-117">Configure name resolution</span></span>

<span data-ttu-id="0abe7-118">Hdınsight ve kaynakları adıyla iletişim kurması için birleştirilmiş ağdaki izin vermek için aşağıdaki eylemleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0abe7-118">To allow HDInsight and resources in the joined network to communicate by name, you must perform the following actions:</span></span>

* <span data-ttu-id="0abe7-119">Özel bir DNS sunucusu, Azure sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0abe7-119">Create a custom DNS server in the Azure Virtual Network.</span></span>

* <span data-ttu-id="0abe7-120">Sanal ağ Azure özyinelemeli çözümleyici varsayılan yerine özel DNS sunucusunu kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0abe7-120">Configure the virtual network to use the custom DNS server instead of the default Azure Recursive Resolver.</span></span>

* <span data-ttu-id="0abe7-121">Özel DNS sunucusu ve şirket içi DNS sunucunuz arasında iletim yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0abe7-121">Configure forwarding between the custom DNS server and your on-premises DNS server.</span></span>

<span data-ttu-id="0abe7-122">Bu yapılandırma aşağıdaki davranışı etkinleştirir:</span><span class="sxs-lookup"><span data-stu-id="0abe7-122">This configuration enables the following behavior:</span></span>

* <span data-ttu-id="0abe7-123">DNS son ekine sahip tam etki alanı adları için istekleri __sanal ağ için__ özel DNS sunucusuna gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-123">Requests for fully qualified domain names that have the DNS suffix __for the virtual network__ are forwarded to the custom DNS server.</span></span> <span data-ttu-id="0abe7-124">Özel DNS sunucusu, daha sonra Azure özyinelemeli IP adresini döndüren çözümleyiciye, bu istekleri iletir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-124">The custom DNS server then forwards these requests to the Azure Recursive Resolver, which returns the IP address.</span></span>

* <span data-ttu-id="0abe7-125">Tüm diğer isteklerden şirket DNS sunucusuna iletilir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-125">All other requests are forwarded to the on-premises DNS server.</span></span> <span data-ttu-id="0abe7-126">Microsoft.com gibi ortak Internet kaynakların bile istekleri için ad çözümlemesi şirket DNS sunucusuna iletilir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-126">Even requests for public internet resources such as microsoft.com are forwarded to the on-premises DNS server for name resolution.</span></span>

<span data-ttu-id="0abe7-127">Aşağıdaki şemada çizgiler sanal ağın DNS soneki bitiş kaynaklara yönelik isteklerin ' dir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-127">In the following diagram, green lines are requests for resources that end in the DNS suffix of the virtual network.</span></span> <span data-ttu-id="0abe7-128">Mavi şirket içi ağ veya ortak Internet kaynakların isteklerdir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-128">Blue lines are requests for resources in the on-premises network or on the public internet.</span></span>

![Bu belgede kullanılan yapılandırmasında DNS isteklerine nasıl çözüleceğini diyagramı](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a><span data-ttu-id="0abe7-130">Özel bir DNS sunucusu oluştur</span><span class="sxs-lookup"><span data-stu-id="0abe7-130">Create a custom DNS server</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0abe7-131">Oluşturma ve Hdınsight sanal ağınıza yüklemeden önce DNS sunucusu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-131">You must create and configure the DNS server before installing HDInsight into the virtual network.</span></span>

<span data-ttu-id="0abe7-132">Kullanan bir Linux VM oluşturmak için [bağlamak](https://www.isc.org/downloads/bind/) DNS yazılım, aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-132">To create a Linux VM that uses the [Bind](https://www.isc.org/downloads/bind/) DNS software, use the following steps:</span></span>

> [!NOTE]
> <span data-ttu-id="0abe7-133">Aşağıdaki adımları kullanın [Azure portal](https://portal.azure.com) bir Azure sanal makine oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0abe7-133">The following steps use the [Azure portal](https://portal.azure.com) to create an Azure Virtual Machine.</span></span> <span data-ttu-id="0abe7-134">Bir sanal makine oluşturmak diğer yolları için bkz: [VM Oluştur - Azure CLI](../virtual-machines/linux/quick-create-cli.md) ve [VM Oluştur - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="0abe7-134">For other ways to create a virtual machine, see the [Create VM - Azure CLI](../virtual-machines/linux/quick-create-cli.md) and [Create VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documents.</span></span>

1. <span data-ttu-id="0abe7-135">Gelen [Azure portal](https://portal.azure.com)seçin  __+__ , __işlem__, ve __Ubuntu Server 16.04 LTS__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-135">From the [Azure portal](https://portal.azure.com), select __+__, __Compute__, and __Ubuntu Server 16.04 LTS__.</span></span>

    ![Ubuntu sanal makine oluşturma](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. <span data-ttu-id="0abe7-137">Gelen __Temelleri__ bölümünde, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="0abe7-137">From the __Basics__ section, enter the following information:</span></span>

    * <span data-ttu-id="0abe7-138">__Ad__: Bu sanal makineyi tanımlayan bir kolay ad.</span><span class="sxs-lookup"><span data-stu-id="0abe7-138">__Name__: A friendly name that identifies this virtual machine.</span></span> <span data-ttu-id="0abe7-139">Örneğin, __DNSProxy__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-139">For example, __DNSProxy__.</span></span>
    * <span data-ttu-id="0abe7-140">__Kullanıcı adı__: SSH hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="0abe7-140">__User name__: The name of the SSH account.</span></span>
    * <span data-ttu-id="0abe7-141">__SSH ortak anahtarını__ veya __parola__: SSH hesabı için kimlik doğrulama yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0abe7-141">__SSH public key__ or __Password__: The authentication method for the SSH account.</span></span> <span data-ttu-id="0abe7-142">Daha güvenli olarak ortak anahtarları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="0abe7-142">We recommend using public keys, as they are more secure.</span></span> <span data-ttu-id="0abe7-143">Daha fazla bilgi için bkz: [Linux VM'ler için SSH anahtarları oluşturma ve kullanma](../virtual-machines/linux/mac-create-ssh-keys.md) belge.</span><span class="sxs-lookup"><span data-stu-id="0abe7-143">For more information, see the [Create and use SSH keys for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md) document.</span></span>
    * <span data-ttu-id="0abe7-144">__Kaynak grubu__: seçin __var olanı kullan__ve ardından daha önce oluşturduğunuz sanal ağı içeren kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-144">__Resource group__: Select __Use existing__, and then select the resource group that contains the virtual network created earlier.</span></span>
    * <span data-ttu-id="0abe7-145">__Konum__: sanal ağ olarak aynı konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-145">__Location__: Select the same location as the virtual network.</span></span>

    ![Sanal makine temel yapılandırma](./media/connect-on-premises-network/vm-basics.png)

    <span data-ttu-id="0abe7-147">Diğer girişler varsayılan değerlerinde bırakın ve ardından __Tamam__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-147">Leave other entries at the default values and then select __OK__.</span></span>

3. <span data-ttu-id="0abe7-148">Gelen __bir boyutu seçin__ bölümünde, VM boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-148">From the __Choose a size__ section, select the VM size.</span></span> <span data-ttu-id="0abe7-149">Bu öğretici için en küçük ve en düşük Maliyeti seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-149">For this tutorial, select the smallest and lowest cost option.</span></span> <span data-ttu-id="0abe7-150">Devam etmek için kullanın __seçin__ düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0abe7-150">To continue, use the __Select__ button.</span></span>

4. <span data-ttu-id="0abe7-151">Gelen __ayarları__ bölümünde, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="0abe7-151">From the __Settings__ section, enter the following information:</span></span>

    * <span data-ttu-id="0abe7-152">__Sanal ağ__: daha önce oluşturduğunuz sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-152">__Virtual network__: Select the virtual network that you created earlier.</span></span>

    * <span data-ttu-id="0abe7-153">__Alt ağ__: sanal ağ için varsayılan alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-153">__Subnet__: Select the default subnet for the virtual network.</span></span> <span data-ttu-id="0abe7-154">Yapmak __değil__ VPN ağ geçidi tarafından kullanılan alt ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-154">Do __not__ select the subnet used by the VPN gateway.</span></span>

    * <span data-ttu-id="0abe7-155">__Tanılama depolama hesabı__: mevcut bir depolama hesabını seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0abe7-155">__Diagnostics storage account__: Either select an existing storage account or create a new one.</span></span>

    ![Sanal ağ ayarları](./media/connect-on-premises-network/virtual-network-settings.png)

    <span data-ttu-id="0abe7-157">Varsayılan değer olarak diğer girişler bırakın ve ardından __Tamam__ devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="0abe7-157">Leave the other entries at the default value, then select __OK__ to continue.</span></span>

5. <span data-ttu-id="0abe7-158">Gelen __satın alma__ bölümünde, select __satın alma__ sanal makine oluşturmak için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0abe7-158">From the __Purchase__ section, select the __Purchase__ button to create the virtual machine.</span></span>

6. <span data-ttu-id="0abe7-159">Sanal makine oluşturulduktan sonra kendi __genel bakış__ bölümünde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-159">Once the virtual machine has been created, its __Overview__ section is displayed.</span></span> <span data-ttu-id="0abe7-160">Sol taraftaki listesinden __özellikleri__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-160">From the list on the left, select __Properties__.</span></span> <span data-ttu-id="0abe7-161">Kaydet __genel IP adresi__ ve __özel IP adresi__ değerleri.</span><span class="sxs-lookup"><span data-stu-id="0abe7-161">Save the __Public IP address__ and __Private IP address__ values.</span></span> <span data-ttu-id="0abe7-162">Sonraki bölümde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0abe7-162">It will be used in the next section.</span></span>

    ![Ortak ve özel IP adresleri](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a><span data-ttu-id="0abe7-164">Yükleme ve bağlama (DNS yazılım) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0abe7-164">Install and configure Bind (DNS software)</span></span>

1. <span data-ttu-id="0abe7-165">SSH bağlanmak için kullandığı __genel IP adresi__ sanal makinenin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-165">Use SSH to connect to the __public IP address__ of the virtual machine.</span></span> <span data-ttu-id="0abe7-166">Aşağıdaki örnek bir sanal makinenin 40.68.254.142 bağlanır:</span><span class="sxs-lookup"><span data-stu-id="0abe7-166">The following example connects to a virtual machine at 40.68.254.142:</span></span>

    ```bash
    ssh sshuser@40.68.254.142
    ```

    <span data-ttu-id="0abe7-167">Değiştir `sshuser` küme oluştururken, belirtilen SSH kullanıcı hesabıyla.</span><span class="sxs-lookup"><span data-stu-id="0abe7-167">Replace `sshuser` with the SSH user account you specified when creating the cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0abe7-168">Bir elde etmek için çeşitli yollar vardır `ssh` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="0abe7-168">There are a variety of ways to obtain the `ssh` utility.</span></span> <span data-ttu-id="0abe7-169">Linux, Unix ve macOS, işletim sisteminin bir parçası sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0abe7-169">On Linux, Unix, and macOS, it is provided as part of the operating system.</span></span> <span data-ttu-id="0abe7-170">Windows kullanıyorsanız, aşağıdaki seçeneklerden birini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="0abe7-170">If you are using Windows, consider one of the following options:</span></span>
    >
    > * [<span data-ttu-id="0abe7-171">Azure bulut Kabuğu</span><span class="sxs-lookup"><span data-stu-id="0abe7-171">Azure Cloud Shell</span></span>](../cloud-shell/quickstart.md)
    > * [<span data-ttu-id="0abe7-172">Windows 10 Ubuntu bash</span><span class="sxs-lookup"><span data-stu-id="0abe7-172">Bash on Ubuntu on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/about)
    > * [<span data-ttu-id="0abe7-173">Git (https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="0abe7-173">Git (https://git-scm.com/)</span></span>](https://git-scm.com/)
    > * [<span data-ttu-id="0abe7-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span><span class="sxs-lookup"><span data-stu-id="0abe7-174">OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. <span data-ttu-id="0abe7-175">Bağ yüklemek için SSH oturumundan aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-175">To install Bind, use the following commands from the SSH session:</span></span>

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. <span data-ttu-id="0abe7-176">Şirket içi DNS sunucunuz için ad çözümleme isteklerini iletmek için bağlama yapılandırmak için aşağıdaki metni içeriğini kullanın `/etc/bind/named.conf.options` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0abe7-176">To configure Bind to forward name resolution requests to your on-prem DNS server, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

        acl goodclients {
            10.0.0.0/16; # Replace with the IP address range of the virtual network
            10.1.0.0/16; # Replace with the IP address range of the on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with the IP address of the on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform to RFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > <span data-ttu-id="0abe7-177">Değerleri değiştirin `goodclients` bölümünü IP adres aralığı ile şirket içi ağ ve sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="0abe7-177">Replace the values in the `goodclients` section with the IP address range of the virtual network and on-premises network.</span></span> <span data-ttu-id="0abe7-178">Bu bölümde, bu DNS sunucusu gelen istekleri kabul adreslerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0abe7-178">This section defines the addresses that this DNS server accepts requests from.</span></span>
    >
    > <span data-ttu-id="0abe7-179">Değiştir `192.168.0.1` girişi `forwarders` şirket içi DNS sunucunuzun IP adresi bölümü.</span><span class="sxs-lookup"><span data-stu-id="0abe7-179">Replace the `192.168.0.1` entry in the `forwarders` section with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="0abe7-180">Bu girdi, çözümleme için şirket DNS sunucusuna DNS isteklerini yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-180">This entry routes DNS requests to your on-premises DNS server for resolution.</span></span>

    <span data-ttu-id="0abe7-181">Bu dosyayı düzenlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-181">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    <span data-ttu-id="0abe7-182">Dosyayı kaydetmek için kullanın __Ctrl + X__, __Y__ve ardından __Enter__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-182">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

4. <span data-ttu-id="0abe7-183">SSH oturumunda aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-183">From the SSH session, use the following command:</span></span>

    ```bash
    hostname -f
    ```

    <span data-ttu-id="0abe7-184">Bu komutu aşağıdaki metni benzer bir değer döndürür:</span><span class="sxs-lookup"><span data-stu-id="0abe7-184">This command returns a value similar to the following text:</span></span>

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    <span data-ttu-id="0abe7-185">`icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` Metin __DNS soneki__ bu sanal ağ için.</span><span class="sxs-lookup"><span data-stu-id="0abe7-185">The `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` text is the __DNS suffix__ for this virtual network.</span></span> <span data-ttu-id="0abe7-186">Bu değer daha sonra kullanılmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-186">Save this value, as it is used later.</span></span>

5. <span data-ttu-id="0abe7-187">Sanal ağ içindeki kaynaklar için DNS adlarını çözümlemek için bağ yapılandırmak için aşağıdaki metni içeriğini kullanın `/etc/bind/named.conf.local` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0abe7-187">To configure Bind to resolve DNS names for resources within the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

        // Replace the following with the DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # The Azure recursive resolver
        };

    > [!IMPORTANT]
    > <span data-ttu-id="0abe7-188">Değiştirmeniz gereken `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` daha önce DNS soneki.</span><span class="sxs-lookup"><span data-stu-id="0abe7-188">You must replace the `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` with the DNS suffix you retrieved earlier.</span></span>

    <span data-ttu-id="0abe7-189">Bu dosyayı düzenlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-189">To edit this file, use the following command:</span></span>

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    <span data-ttu-id="0abe7-190">Dosyayı kaydetmek için kullanın __Ctrl + X__, __Y__ve ardından __Enter__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-190">To save the file, use __Ctrl+X__, __Y__, and then __Enter__.</span></span>

6. <span data-ttu-id="0abe7-191">Bağ başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-191">To start Bind, use the following command:</span></span>

    ```bash
    sudo service bind9 restart
    ```

7. <span data-ttu-id="0abe7-192">Bu bağlama şirket içi ağınızdaki kaynaklara adlarını çözümleyebildiğini doğrulamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-192">To verify that bind can resolve the names of resources in your on-premises network, use the following commands:</span></span>

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0abe7-193">Değiştir `dns.mynetwork.net` , şirket içi ağınıza bir kaynak tam etki alanı adını (FQDN).</span><span class="sxs-lookup"><span data-stu-id="0abe7-193">Replace `dns.mynetwork.net` with the fully qualified domain name (FQDN) of a resource in your on-premises network.</span></span>
    >
    > <span data-ttu-id="0abe7-194">Değiştir `10.0.0.4` ile __iç IP adresi__ özel DNS sunucunuzun sanal ağda.</span><span class="sxs-lookup"><span data-stu-id="0abe7-194">Replace `10.0.0.4` with the __internal IP address__ of your custom DNS server in the virtual network.</span></span>

    <span data-ttu-id="0abe7-195">Yanıt aşağıdakine benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="0abe7-195">The response appears similar to the following text:</span></span>

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-the-virtual-network-to-use-the-custom-dns-server"></a><span data-ttu-id="0abe7-196">Sanal ağ özel DNS sunucusunu kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0abe7-196">Configure the virtual network to use the custom DNS server</span></span>

<span data-ttu-id="0abe7-197">Sanal ağ yerine Azure özyinelemeli çözümleyici özel DNS sunucusunu kullanacak şekilde yapılandırmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-197">To configure the virtual network to use the custom DNS server instead of the Azure recursive resolver, use the following steps:</span></span>

1. <span data-ttu-id="0abe7-198">İçinde [Azure portal](https://portal.azure.com)sanal ağı seçin ve ardından __DNS sunucuları__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-198">In the [Azure portal](https://portal.azure.com), select the virtual network, and then select __DNS Servers__.</span></span>

2. <span data-ttu-id="0abe7-199">Seçin __özel__ve girin __iç IP adresi__ özel DNS sunucusu.</span><span class="sxs-lookup"><span data-stu-id="0abe7-199">Select __Custom__, and enter the __internal IP address__ of the custom DNS server.</span></span> <span data-ttu-id="0abe7-200">Son olarak, seçin __kaydetmek__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-200">Finally, select __Save__.</span></span>

    ![Ağ için özel DNS sunucusunu ayarlayın](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-the-on-premises-dns-server"></a><span data-ttu-id="0abe7-202">Şirket içi DNS sunucusunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0abe7-202">Configure the on-premises DNS server</span></span>

<span data-ttu-id="0abe7-203">Önceki bölümde özel DNS sunucusunu isteklerini şirket DNS sunucusuna iletmek üzere yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="0abe7-203">In the previous section, you configured the custom DNS server to forward requests to the on-premises DNS server.</span></span> <span data-ttu-id="0abe7-204">Ardından, özel DNS sunucu isteklerini iletmek için şirket içi DNS sunucusu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-204">Next, you must configure the on-premises DNS server to forward requests to the custom DNS server.</span></span>

<span data-ttu-id="0abe7-205">DNS sunucunuzu yapılandırma hakkında belirli adımlar için DNS sunucu yazılımınızın belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="0abe7-205">For specific steps on how to configure your DNS server, consult the documentation for your DNS server software.</span></span> <span data-ttu-id="0abe7-206">Yapılandırma adımları arayın bir __koşullu ileticisi__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-206">Look for the steps on how to configure a __conditional forwarder__.</span></span>

<span data-ttu-id="0abe7-207">Koşullu iletme, yalnızca belirli bir DNS soneki isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-207">A conditional forward only forwards requests for a specific DNS suffix.</span></span> <span data-ttu-id="0abe7-208">Bu durumda, sanal ağın DNS soneki için bir iletici yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-208">In this case, you must configure a forwarder for the DNS suffix of the virtual network.</span></span> <span data-ttu-id="0abe7-209">Bu soneki isteklerinde özel DNS sunucusunun IP adresine iletilen.</span><span class="sxs-lookup"><span data-stu-id="0abe7-209">Requests for this suffix should be forwarded to the IP address of the custom DNS server.</span></span> 

<span data-ttu-id="0abe7-210">Aşağıdaki metni için bir koşullu ileticisi yapılandırma örneğidir **bağlamak** DNS yazılım:</span><span class="sxs-lookup"><span data-stu-id="0abe7-210">The following text is an example of a conditional forwarder configuration for the **Bind** DNS software:</span></span>

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The custom DNS server's internal IP address
    };

<span data-ttu-id="0abe7-211">DNS kullanma hakkında bilgi için **Windows Server 2016**, bkz: [Ekle DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) belgelerine...</span><span class="sxs-lookup"><span data-stu-id="0abe7-211">For information on using DNS on **Windows Server 2016**, see the [Add-DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentation...</span></span>

<span data-ttu-id="0abe7-212">Şirket içi DNS sunucusunu yapılandırdıktan sonra kullanabileceğiniz `nslookup` şirket ağından sanal ağda adlarını çözümleyebildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0abe7-212">Once you have configured the on-premises DNS server, you can use `nslookup` from the on-premises network to verify that you can resolve names in the virtual network.</span></span> <span data-ttu-id="0abe7-213">Aşağıdaki örnek</span><span class="sxs-lookup"><span data-stu-id="0abe7-213">The following example</span></span> 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

<span data-ttu-id="0abe7-214">Bu örnek özel DNS sunucu adını çözümlemek için 196.168.0.4 şirket içi DNS sunucusunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="0abe7-214">This example uses the on-premises DNS server at 196.168.0.4 to resolve the name of the custom DNS server.</span></span> <span data-ttu-id="0abe7-215">Bir şirket içi DNS sunucusunun IP adresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-215">Replace the IP address with the one for the on-premises DNS server.</span></span> <span data-ttu-id="0abe7-216">Değiştir `dnsproxy` özel DNS sunucusunun tam etki alanı adı ile adres.</span><span class="sxs-lookup"><span data-stu-id="0abe7-216">Replace the `dnsproxy` address with the fully qualified domain name of the custom DNS server.</span></span>

## <a name="optional-control-network-traffic"></a><span data-ttu-id="0abe7-217">İsteğe bağlı: Denetim ağ trafiği</span><span class="sxs-lookup"><span data-stu-id="0abe7-217">Optional: Control network traffic</span></span>

<span data-ttu-id="0abe7-218">Ağ trafiğini denetlemek için ağ güvenlik grubu (NSG) veya kullanıcı tanımlı yolları (UDR) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0abe7-218">You can use network security groups (NSG) or user-defined routes (UDR) to control network traffic.</span></span> <span data-ttu-id="0abe7-219">Nsg'ler gelen ve giden trafiği filtrelemek ve izin veren veya trafiği reddeden olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0abe7-219">NSGs allow you to filter inbound and outbound traffic, and allow or deny the traffic.</span></span> <span data-ttu-id="0abe7-220">Udr'ler, nasıl sanal ağ, internet ve şirket içi ağ kaynaklarına arasında trafiği akan denetlemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0abe7-220">UDRs allow you to control how traffic flows between resources in the virtual network, the internet, and the on-premises network.</span></span>

> [!WARNING]
> <span data-ttu-id="0abe7-221">Hdınsight Azure bulutta belirli IP adreslerinden gelen erişim ve sınırsız giden erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-221">HDInsight requires inbound access from specific IP addresses in the Azure cloud, and unrestricted outbound access.</span></span> <span data-ttu-id="0abe7-222">Trafiği denetlemek için Nsg'ler veya Udr'ler kullanırken, aşağıdaki adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0abe7-222">When using NSGs or UDRs to control traffic, you must perform the following steps:</span></span>
>
> 1. <span data-ttu-id="0abe7-223">IP adreslerini sanal ağınızı içeren konumunu bulur.</span><span class="sxs-lookup"><span data-stu-id="0abe7-223">Find the IP addresses for the location that contains your virtual network.</span></span> <span data-ttu-id="0abe7-224">Konuma göre gerekli IP'leri listesi için bkz: [gerekli IP adreslerini](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span><span class="sxs-lookup"><span data-stu-id="0abe7-224">For a list of required IPs by location, see [Required IP addresses](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).</span></span>
>
> 2. <span data-ttu-id="0abe7-225">IP adreslerinden gelen trafiğe izin verin.</span><span class="sxs-lookup"><span data-stu-id="0abe7-225">Allow inbound traffic from the IP addresses.</span></span>
>
>    * <span data-ttu-id="0abe7-226">__NSG__: izin __gelen__ bağlantı noktasında trafik __443__ gelen __Internet__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-226">__NSG__: Allow __inbound__ traffic on port __443__ from the __Internet__.</span></span>
>    * <span data-ttu-id="0abe7-227">__UDR__: ayarlamak __sonraki atlama__ yol türünü __Internet__.</span><span class="sxs-lookup"><span data-stu-id="0abe7-227">__UDR__: Set the __Next Hop__ type of the route to __Internet__.</span></span>

<span data-ttu-id="0abe7-228">Nsg'ler oluşturmak için Azure PowerShell veya Azure CLI kullanma örneği için bkz: [genişletmek Hdınsight Azure sanal ağlar ile](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) belge.</span><span class="sxs-lookup"><span data-stu-id="0abe7-228">For an example of using Azure PowerShell or the Azure CLI to create NSGs, see the [Extend HDInsight with Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.</span></span>

## <a name="create-the-hdinsight-cluster"></a><span data-ttu-id="0abe7-229">Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0abe7-229">Create the HDInsight cluster</span></span>

> [!WARNING]
> <span data-ttu-id="0abe7-230">Sanal ağ Hdınsight yüklemeden önce özel DNS sunucusu yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-230">You must configure the custom DNS server before installing HDInsight in the virtual network.</span></span>

<span data-ttu-id="0abe7-231">İçindeki adımları kullanın [Azure portalını kullanarak bir Hdınsight kümesi oluşturmayı](./hdinsight-hadoop-create-linux-clusters-portal.md) Hdınsight kümesi oluşturmak için belge.</span><span class="sxs-lookup"><span data-stu-id="0abe7-231">Use the steps in the [Create an HDInsight cluster using the Azure portal](./hdinsight-hadoop-create-linux-clusters-portal.md) document to create an HDInsight cluster.</span></span>

> [!WARNING]
> * <span data-ttu-id="0abe7-232">Küme oluşturma sırasında sanal ağınızı içeren konuma seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-232">During cluster creation, you must choose the location that contains your virtual network.</span></span>
>
> * <span data-ttu-id="0abe7-233">İçinde __Gelişmiş ayarları__ bölümü yapılandırmasına, daha önce oluşturduğunuz alt ağ ve sanal ağ seçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="0abe7-233">In the __Advanced settings__ part of configuration, you must select the virtual network and subnet that you created earlier.</span></span>

## <a name="connecting-to-hdinsight"></a><span data-ttu-id="0abe7-234">Hdınsight'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="0abe7-234">Connecting to HDInsight</span></span>

<span data-ttu-id="0abe7-235">Hdınsight üzerinde çoğu belgeleri Internet üzerinden kümesine erişimi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="0abe7-235">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="0abe7-236">Https://CLUSTERNAME.azurehdinsight.net konumundaki küme bağlanabileceği bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="0abe7-236">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0abe7-237">Bu adres Nsg'ler veya Udr'ler kullandıysanız internet'ten erişimi kısıtlamak için kullanılabilir olmayan ortak ağ geçidi, kullanır.</span><span class="sxs-lookup"><span data-stu-id="0abe7-237">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="0abe7-238">Hdınsight için sanal ağ üzerinden doğrudan bağlanmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-238">To directly connect to HDInsight through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="0abe7-239">Hdınsight küme düğümlerinin iç tam etki alanı adlarını bulmak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0abe7-239">To discover the internal fully qualified domain names of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

2. <span data-ttu-id="0abe7-240">Hizmet kullanılabilir bağlantı noktasını belirlemek için bkz: [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](./hdinsight-hadoop-port-settings-for-services.md) belge.</span><span class="sxs-lookup"><span data-stu-id="0abe7-240">To determine the port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0abe7-241">Baş düğümler üzerinde barındırılan bazı hizmetler aynı anda yalnızca bir düğümde etkin olur.</span><span class="sxs-lookup"><span data-stu-id="0abe7-241">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="0abe7-242">Bir hizmet bir baş düğüm üzerindeki erişmeyi deneyin ve başarısız olursa, diğer baş düğüme geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="0abe7-242">If you try accessing a service on one head node and it fails, switch to the other head node.</span></span>
    >
    > <span data-ttu-id="0abe7-243">Örneğin, Ambari yalnızca aynı anda bir baş düğüm üzerinde etkindir.</span><span class="sxs-lookup"><span data-stu-id="0abe7-243">For example, Ambari is only active on one head node at a time.</span></span> <span data-ttu-id="0abe7-244">Ambari bir baş düğüm üzerinde erişmeyi deneyin ve bir 404 hatası döndürür, diğer baş düğüm üzerinde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="0abe7-244">If you try accessing Ambari on one head node and it returns a 404 error, then it is running on the other head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0abe7-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0abe7-245">Next steps</span></span>

* <span data-ttu-id="0abe7-246">Sanal bir ağa Hdınsight kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure sanal ağları kullanarak Hdınsight](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="0abe7-246">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

* <span data-ttu-id="0abe7-247">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0abe7-247">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="0abe7-248">Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="0abe7-248">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="0abe7-249">Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0abe7-249">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>
