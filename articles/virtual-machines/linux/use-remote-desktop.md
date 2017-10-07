---
title: "aaaUse Uzak Masaüstü tooa Azure Linux VM'de | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Azure'da grafik araçları kullanarak Uzak Masaüstü'nü (xrdp) tooconnect tooa Linux VM yapılandırın"
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
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="9e191-103">Yükleme ve Uzak Masaüstü tooconnect tooa Linux VM Azure'da yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e191-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="9e191-104">Azure'daki Linux sanal makineleri (VM'ler) genellikle hello bir güvenli Kabuk (SSH) bağlantısı kullanarak komut satırından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="9e191-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="9e191-105">Zaman yeni tooLinux veya hızlı sorun giderme senaryoları için Uzak Masaüstü hello kullanımını daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e191-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="9e191-106">Bu makale ayrıntıları nasıl tooinstall ve bir masaüstü ortamını yapılandırma ([xfce](https://www.xfce.org)) ve Uzak Masaüstü'nü ([xrdp](http://www.xrdp.org)) hello Resource Manager dağıtım modeli kullanarak, Linux VM için.</span><span class="sxs-lookup"><span data-stu-id="9e191-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9e191-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9e191-107">Prerequisites</span></span>
<span data-ttu-id="9e191-108">Bu makalede, azure'da var olan bir Linux VM gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9e191-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="9e191-109">Toocreate VM gerekiyorsa, yöntemler aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e191-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="9e191-110">Merhaba [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9e191-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="9e191-111">Merhaba [Azure portalı](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9e191-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="9e191-112">Bir masaüstü ortamı, Linux VM olanağına yükle</span><span class="sxs-lookup"><span data-stu-id="9e191-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="9e191-113">Çoğu Linux VM'ler için Azure'da varsayılan olarak yüklenen bir masaüstü ortamı yok.</span><span class="sxs-lookup"><span data-stu-id="9e191-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="9e191-114">Linux VM'ler genellikle bir masaüstü ortamı yerine SSH bağlantısını kullanılarak yönetilir.</span><span class="sxs-lookup"><span data-stu-id="9e191-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="9e191-115">Seçebileceğiniz Linux çeşitli masaüstü ortamlarında vardır.</span><span class="sxs-lookup"><span data-stu-id="9e191-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="9e191-116">Tercih ettiğiniz Masaüstü ortamının bağlı olarak, bunu bir too2 GB disk alanı kullanabilir ve 5 too10 dakika tooinstall alın ve tüm gerekli hello paketler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9e191-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="9e191-117">Merhaba aşağıdaki örnek yükler hello basit [xfce4](https://www.xfce.org/) bir Ubuntu VM Masaüstü ortamı.</span><span class="sxs-lookup"><span data-stu-id="9e191-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="9e191-118">Komutları, diğer dağıtımlar biraz farklılık gösterir (kullanmak `yum` tooinstall Red Hat Enterprise Linux üzerinde ve uygun yapılandırma `selinux` kuralları ya da kullanım `zypper` örneğin SUSE üzerinde tooinstall).</span><span class="sxs-lookup"><span data-stu-id="9e191-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="9e191-119">İlk olarak, SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="9e191-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="9e191-120">Merhaba aşağıdaki örnek bağlayan toohello adlı VM *myvm.westus.cloudapp.azure.com* hello kullanıcı adı ile *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="9e191-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="9e191-121">Windows kullanıyorsanız ve SSH kullanma hakkında daha fazla bilgi için bkz: [nasıl ile Windows toouse SSH anahtarları](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="9e191-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="9e191-122">Ardından, xfce kullanarak yükleyin `apt` gibi:</span><span class="sxs-lookup"><span data-stu-id="9e191-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="9e191-123">Uzak Masaüstü sunucusu yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e191-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="9e191-124">Yüklü bir masaüstü ortamı sahip olduğunuza göre bir Uzak Masaüstü hizmet toolisten gelen bağlantıları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9e191-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="9e191-125">[xrdp](http://xrdp.org) çoğu Linux dağıtımları hakkında kullanılabilir ve çalışır iyi xfce ile bir açık kaynak Uzak Masaüstü Protokolü (RDP) sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="9e191-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="9e191-126">Xrdp Ubuntu VM üzerinde aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9e191-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="9e191-127">Oturumunuz başlattığınızda xrdp hangi masaüstü ortamında toouse söyleyin.</span><span class="sxs-lookup"><span data-stu-id="9e191-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="9e191-128">Xrdp toouse xfce masaüstü ortamınızı aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="9e191-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="9e191-129">Merhaba xrdp hizmeti hello değişiklikleri tootake etkisi için aşağıdaki gibi yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="9e191-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="9e191-130">Bir yerel kullanıcı hesabı parolasını ayarlama</span><span class="sxs-lookup"><span data-stu-id="9e191-130">Set a local user account password</span></span>
<span data-ttu-id="9e191-131">VM'nizi oluşturduğunuzda kullanıcı hesabınız için bir parola oluşturduysanız, bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="9e191-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="9e191-132">Yalnızca SSH anahtar kimlik doğrulaması kullanmak ve yok bir yerel hesap parola ayarlayın, xrdp toolog tooyour VM kullanmadan önce bir parola belirtmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="9e191-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="9e191-133">xrdp kimlik doğrulaması için SSH anahtarları kabul edemez.</span><span class="sxs-lookup"><span data-stu-id="9e191-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="9e191-134">Merhaba aşağıdaki örnekte bir hello kullanıcı hesabının parolasını belirtir *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="9e191-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="9e191-135">Şu anda mevcut değilse parola belirterek SSHD yapılandırma toopermit parolalı oturum açma güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="9e191-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="9e191-136">Güvenlik açısından bakıldığında, tooxrdp bağlanmak ve anahtar tabanlı kimlik doğrulaması kullanarak SSH tüneli ile tooconnect tooyour VM istiyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e191-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="9e191-137">Bu durumda, bir ağ güvenlik grubu kural tooallow Uzak Masaüstü trafiği oluşturma ile ilgili adımı takip hello atlayın.</span><span class="sxs-lookup"><span data-stu-id="9e191-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="9e191-138">Uzak Masaüstü trafiği için ağ güvenlik grubu kural oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e191-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="9e191-139">tooallow Uzak Masaüstü trafiği tooreach Linux VM, bir ağ güvenlik grubu kural oluşturulan toobe izin veren TCP bağlantı noktası 3389 tooreach üzerinde VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e191-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="9e191-140">Ağ güvenlik grubu kuralları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9e191-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="9e191-141">Ayrıca [kullanım hello Azure portal toocreate bir ağ güvenlik grubu kural](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e191-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9e191-142">Merhaba aşağıdaki örnekleri oluşturma sahip bir ağ güvenlik grubu kural [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) adlı *myNetworkSecurityGroupRule* çok*izin* trafiğinde*tcp* bağlantı noktası *3389*.</span><span class="sxs-lookup"><span data-stu-id="9e191-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="9e191-143">Linux VM ile bir Uzak Masaüstü İstemcisi Bağlan</span><span class="sxs-lookup"><span data-stu-id="9e191-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="9e191-144">Yerel, Uzak Masaüstü İstemcisi'ni açın ve toohello IP adresi veya DNS adı Linux VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="9e191-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="9e191-145">Merhaba kullanıcı adı ve parola hello kullanıcı hesabı için VM üzerinde şu şekilde girin:</span><span class="sxs-lookup"><span data-stu-id="9e191-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Uzak Masaüstü İstemcisi'ni kullanarak tooxrdp Bağlan](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="9e191-147">Kimlik doğrulandıktan sonra hello xfce masaüstü ortamını yükleyin ve aşağıdaki örneğine benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="9e191-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![xrdp aracılığıyla xfce Masaüstü ortamı](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="9e191-149">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9e191-149">Troubleshoot</span></span>
<span data-ttu-id="9e191-150">Tooyour bir Uzak Masaüstü istemcisi kullanarak Linux VM bağlanamıyorsanız kullanmak `netstat` , VM için RDP bağlantıları gibi dinliyor, Linux VM tooverify üzerinde:</span><span class="sxs-lookup"><span data-stu-id="9e191-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="9e191-151">Aşağıdaki örnekte gösterildiği hello beklendiği gibi 3389 numaralı TCP bağlantı noktasında dinleme VM hello:</span><span class="sxs-lookup"><span data-stu-id="9e191-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="9e191-152">Merhaba xrdp hizmet dinleme yapmıyorsanız bir Ubuntu VM üzerinde aşağıdaki gibi hello hizmetini yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="9e191-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="9e191-153">Gözden geçirme oturum açtığında */var/log*Thug toowhy hello hizmet olarak göstergeleri için Ubuntu VM üzerinde yanıt.</span><span class="sxs-lookup"><span data-stu-id="9e191-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="9e191-154">Uzak Masaüstü bağlantı denemesi tooview sırasında hataları hello syslog da izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e191-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="9e191-155">Red Hat Enterprise Linux ve SUSE gibi diğer Linux dağıtımları farklı şekillerde toorestart Hizmetleri ve diğer günlük dosyası konumları tooreview olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e191-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="9e191-156">Herhangi bir yanıt, Uzak Masaüstü İstemcisi almaz ve hello sistem günlüğündeki tüm olayları görmüyorsanız, Uzak Masaüstü trafik hello VM ulaşamıyor Bu davranış gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e191-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="9e191-157">Bir kural toopermit TCP bağlantı noktası 3389 sahip, ağ güvenlik grubu kuralları tooensure gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="9e191-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="9e191-158">Daha fazla bilgi için bkz: [uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9e191-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9e191-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e191-159">Next steps</span></span>
<span data-ttu-id="9e191-160">Oluşturma ve Linux VM'ler ile SSH anahtarları kullanma hakkında daha fazla bilgi için bkz: [oluşturma SSH anahtarları Azure Linux VM'ler için](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="9e191-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="9e191-161">Windows SSH kullanma hakkında daha fazla bilgi için bkz: [nasıl ile Windows toouse SSH anahtarları](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="9e191-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

