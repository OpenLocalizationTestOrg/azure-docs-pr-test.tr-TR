---
title: "Azure'da bir Linux VM, Uzak Masaüstü'nü kullanın | Microsoft Docs"
description: "Yükleme ve uzak grafik araçları kullanarak azure'da bir Linux VM bağlanmak için Masaüstü (xrdp) yapılandırma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: d8d6130a270285c84c1dd057a3512cdeb39287f6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-remote-desktop-to-connect-to-a-linux-vm-in-azure"></a><span data-ttu-id="33637-103">Yükleme ve azure'da bir Linux VM bağlanmak için Uzak Masaüstü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="33637-103">Install and configure Remote Desktop to connect to a Linux VM in Azure</span></span>
<span data-ttu-id="33637-104">Azure'daki Linux sanal makineleri (VM'ler) genellikle bir güvenli Kabuk (SSH) bağlantısı kullanarak komut satırından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="33637-104">Linux virtual machines (VMs) in Azure are usually managed from the command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="33637-105">Linux veya hızlı sorun giderme senaryoları için yeni, Uzak Masaüstü kullanımını daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="33637-105">When new to Linux, or for quick troubleshooting scenarios, the use of remote desktop may be easier.</span></span> <span data-ttu-id="33637-106">Bu makalede yüklemek ve bir masaüstü ortamını yapılandırma ayrıntıları ([xfce](https://www.xfce.org)) ve Uzak Masaüstü'nü ([xrdp](http://www.xrdp.org)) Resource Manager dağıtım modeli kullanarak, Linux VM için.</span><span class="sxs-lookup"><span data-stu-id="33637-106">This article details how to install and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using the Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="33637-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="33637-107">Prerequisites</span></span>
<span data-ttu-id="33637-108">Bu makalede, azure'da var olan bir Linux VM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="33637-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="33637-109">Bir VM oluşturmanız gerekiyorsa, aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="33637-109">If you need to create a VM, use one of the following methods:</span></span>

- <span data-ttu-id="33637-110">[Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="33637-110">The [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="33637-111">[Azure portalı](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="33637-111">The [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="33637-112">Bir masaüstü ortamı, Linux VM olanağına yükle</span><span class="sxs-lookup"><span data-stu-id="33637-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="33637-113">Çoğu Linux VM'ler için Azure'da varsayılan olarak yüklenen bir masaüstü ortamı yok.</span><span class="sxs-lookup"><span data-stu-id="33637-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="33637-114">Linux VM'ler genellikle bir masaüstü ortamı yerine SSH bağlantısını kullanılarak yönetilir.</span><span class="sxs-lookup"><span data-stu-id="33637-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="33637-115">Seçebileceğiniz Linux çeşitli masaüstü ortamlarında vardır.</span><span class="sxs-lookup"><span data-stu-id="33637-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="33637-116">Tercih ettiğiniz Masaüstü ortamının bağlı olarak, bir için 2 GB disk alanı kullanabilir ve yüklemek ve tüm gerekli paketleri yapılandırmak için 5-10 dakika.</span><span class="sxs-lookup"><span data-stu-id="33637-116">Depending on your choice of desktop environment, it may consume one to 2 GB of disk space, and take 5 to 10 minutes to install and configure all the required packages.</span></span>

<span data-ttu-id="33637-117">Aşağıdaki örnekte basit yükler [xfce4](https://www.xfce.org/) bir Ubuntu VM Masaüstü ortamı.</span><span class="sxs-lookup"><span data-stu-id="33637-117">The following example installs the lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="33637-118">Diğer dağıtımlar biraz farklılık için komutları (kullanmak `yum` Red Hat Enterprise Linux üzerinde yükleme ve uygun yapılandırma `selinux` kuralları ya da kullanım `zypper` SUSE üzerinde örneğin yüklemek için).</span><span class="sxs-lookup"><span data-stu-id="33637-118">Commands for other distributions vary slightly (use `yum` to install on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` to install on SUSE, for example).</span></span>

<span data-ttu-id="33637-119">İlk olarak, SSH, VM.</span><span class="sxs-lookup"><span data-stu-id="33637-119">First, SSH to your VM.</span></span> <span data-ttu-id="33637-120">Aşağıdaki örnek adlı VM'ye bağlayan *myvm.westus.cloudapp.azure.com* kullanıcı adıyla *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="33637-120">The following example connects to the VM named *myvm.westus.cloudapp.azure.com* with the username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="33637-121">Windows kullanıyorsanız ve SSH kullanma hakkında daha fazla bilgi için bkz: [SSH kullanma anahtarları ile Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="33637-121">If you are using Windows and need more information on using SSH, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="33637-122">Ardından, xfce kullanarak yükleyin `apt` gibi:</span><span class="sxs-lookup"><span data-stu-id="33637-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="33637-123">Uzak Masaüstü sunucusu yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="33637-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="33637-124">Yüklü bir masaüstü ortamı sahip olduğunuza göre gelen bağlantılarını dinlemek için bir Uzak Masaüstü hizmetini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="33637-124">Now that you have a desktop environment installed, configure a remote desktop service to listen for incoming connections.</span></span> <span data-ttu-id="33637-125">[xrdp](http://xrdp.org) çoğu Linux dağıtımları hakkında kullanılabilir ve çalışır iyi xfce ile bir açık kaynak Uzak Masaüstü Protokolü (RDP) sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="33637-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="33637-126">Xrdp Ubuntu VM üzerinde aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="33637-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="33637-127">Xrdp oturumunuz başlattığınızda kullanmak için hangi masaüstü ortamını bildirin.</span><span class="sxs-lookup"><span data-stu-id="33637-127">Tell xrdp what desktop environment to use when you start your session.</span></span> <span data-ttu-id="33637-128">Xrdp xfce gibi masaüstü ortamı olarak kullanmak üzere yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="33637-128">Configure xrdp to use xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="33637-129">Değişikliklerin etkili şekilde xrdp hizmetini yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="33637-129">Restart the xrdp service for the changes to take effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="33637-130">Bir yerel kullanıcı hesabı parolasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="33637-130">Set a local user account password</span></span>
<span data-ttu-id="33637-131">VM'nizi oluşturduğunuzda kullanıcı hesabınız için bir parola oluşturduysanız, bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="33637-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="33637-132">Yalnızca SSH anahtar kimlik doğrulaması kullanmak ve yok bir yerel hesap parola ayarlayın, VM'nize oturum açmak için xrdp kullanmadan önce bir parola belirtmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="33637-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp to log in to your VM.</span></span> <span data-ttu-id="33637-133">xrdp kimlik doğrulaması için SSH anahtarları kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="33637-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="33637-134">Aşağıdaki örnekte kullanıcı hesabı için bir parola belirtir *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="33637-134">The following example specifies a password for the user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="33637-135">Bir parola belirterek SSHD yapılandırmanızı şu anda mevcut değilse parola kullanarak oturum açamayan izin verecek şekilde güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="33637-135">Specifying a password does not update your SSHD configuration to permit password logins if it currently does not.</span></span> <span data-ttu-id="33637-136">Güvenlik açısından bakıldığında, anahtar tabanlı kimlik doğrulaması kullanarak SSH tüneli ile VM'nize bağlanmak istediğiniz ve xrdp için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="33637-136">From a security perspective, you may wish to connect to your VM with an SSH tunnel using key-based authentication and then connect to xrdp.</span></span> <span data-ttu-id="33637-137">Bu durumda, Uzak Masaüstü trafiğine izin veren bir ağ güvenlik grubu kural oluşturma ile ilgili aşağıdaki adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="33637-137">If so, skip the following step on creating a network security group rule to allow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="33637-138">Uzak Masaüstü trafiği için ağ güvenlik grubu kural oluşturma</span><span class="sxs-lookup"><span data-stu-id="33637-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="33637-139">Grup Kuralı gereksinimlerini, oluşturulacak Linux VM, ağ güvenliği ulaşmak Uzak Masaüstü trafiğine izin vermek için VM ulaşmak TCP bağlantı noktası 3389 sağlar.</span><span class="sxs-lookup"><span data-stu-id="33637-139">To allow Remote Desktop traffic to reach your Linux VM, a network security group rule needs to be created that allows TCP on port 3389 to reach your VM.</span></span> <span data-ttu-id="33637-140">Ağ güvenlik grubu kuralları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="33637-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="33637-141">Ayrıca [bir ağ güvenlik grubu kural oluşturmak için Azure portal'ı kullanmanızı](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="33637-141">You can also [use the Azure portal to create a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="33637-142">Aşağıdaki örnekler sahip bir ağ güvenlik grubu kural oluşturma [az ağ nsg kuralı oluşturma](/cli/azure/network/nsg/rule#create) adlı *myNetworkSecurityGroupRule* için *izin* trafiğinde*tcp* bağlantı noktası *3389*.</span><span class="sxs-lookup"><span data-stu-id="33637-142">The following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* to *allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="33637-143">Linux VM ile bir Uzak Masaüstü İstemcisi Bağlan</span><span class="sxs-lookup"><span data-stu-id="33637-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="33637-144">Yerel, Uzak Masaüstü İstemcisi'ni açın ve IP adresi ya da Linux VM DNS adı.</span><span class="sxs-lookup"><span data-stu-id="33637-144">Open your local remote desktop client and connect to the IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="33637-145">Kullanıcı adı ve parola kullanıcı hesabı için VM üzerinde şu şekilde girin:</span><span class="sxs-lookup"><span data-stu-id="33637-145">Enter the username and password for the user account on your VM as follows:</span></span>

![Uzak Masaüstü İstemcisi'ni kullanarak xrdp Bağlan](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="33637-147">Kimlik doğrulandıktan sonra xfce masaüstü ortamında yüklemek ve aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="33637-147">After authenticating, the xfce desktop environment will load and look similar to the following example:</span></span>

![xrdp aracılığıyla xfce Masaüstü ortamı](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="33637-149">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="33637-149">Troubleshoot</span></span>
<span data-ttu-id="33637-150">Uzak Masaüstü İstemcisi'ni kullanarak, Linux VM'ime bağlanamıyorum kullanırsanız `netstat` VM gibi RDP bağlantıları dinliyor doğrulamak için Linux VM'de:</span><span class="sxs-lookup"><span data-stu-id="33637-150">If you cannot connect to your Linux VM using a Remote Desktop client, use `netstat` on your Linux VM to verify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="33637-151">Aşağıdaki örnek, beklendiği gibi 3389 numaralı TCP bağlantı noktasında dinleme VM gösterir:</span><span class="sxs-lookup"><span data-stu-id="33637-151">The following example shows the VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="33637-152">Xrdp hizmet dinleme yapmıyorsanız bir Ubuntu VM üzerinde şu şekilde hizmeti yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="33637-152">If the xrdp service is not listening, on an Ubuntu VM restart the service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="33637-153">Gözden geçirme oturum açtığında */var/log*Thug neden hizmeti yanıt vermiyor olabilir ilişkin göstergeleri için Ubuntu VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="33637-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as to why the service may not be responding.</span></span> <span data-ttu-id="33637-154">Syslog hataları görüntülemek için bir Uzak Masaüstü bağlantı girişimi sırasında da izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="33637-154">You can also monitor the syslog during a remote desktop connection attempt to view any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="33637-155">Red Hat Enterprise Linux ve SUSE gibi diğer Linux dağıtımları Hizmetleri ve gözden geçirmek için alternatif günlük dosyası konumları yeniden başlatmak için farklı yollar olabilir.</span><span class="sxs-lookup"><span data-stu-id="33637-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways to restart services and alternate log file locations to review.</span></span>

<span data-ttu-id="33637-156">Herhangi bir yanıt, Uzak Masaüstü İstemcisi almaz ve sistem günlüğündeki tüm olayları görmüyorsanız, Uzak Masaüstü trafik VM ulaşamıyor Bu davranış gösterir.</span><span class="sxs-lookup"><span data-stu-id="33637-156">If you do not receive any response in your remote desktop client and do not see any events in the system log, this behavior indicates that remote desktop traffic cannot reach the VM.</span></span> <span data-ttu-id="33637-157">TCP bağlantı noktası 3389 üzerinde izin vermek için bir kural olmasını sağlamak için ağ güvenlik grubu kurallarınızı gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="33637-157">Review your network security group rules to ensure that you have a rule to permit TCP on port 3389.</span></span> <span data-ttu-id="33637-158">Daha fazla bilgi için bkz: [uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="33637-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="33637-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="33637-159">Next steps</span></span>
<span data-ttu-id="33637-160">Oluşturma ve Linux VM'ler ile SSH anahtarları kullanma hakkında daha fazla bilgi için bkz: [oluşturma SSH anahtarları Azure Linux VM'ler için](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="33637-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="33637-161">Windows SSH kullanma hakkında daha fazla bilgi için bkz: [SSH kullanma anahtarları ile Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="33637-161">For information on using SSH from Windows, see [How to use SSH keys with Windows](ssh-from-windows.md).</span></span>

