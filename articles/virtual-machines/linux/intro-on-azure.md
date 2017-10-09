---
title: azure'da aaaIntroduction tooLinux | Microsoft Docs
description: "Linux sanal makineleri Azure üzerinde kullanma hakkında bilgi edinin."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a><span data-ttu-id="73031-103">Azure ile ilgili giriş tooLinux</span><span class="sxs-lookup"><span data-stu-id="73031-103">Introduction tooLinux on Azure</span></span>
<span data-ttu-id="73031-104">Bu konuda Linux sanal makineleri hello Azure bulut kullanmanın bazı yönleri genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="73031-104">This topic provides an overview of some aspects of using Linux virtual machines in hello Azure cloud.</span></span> <span data-ttu-id="73031-105">Linux sanal makine dağıtma hello Galeriden bir görüntü kullanarak bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="73031-105">Deploying a Linux virtual machine is a straightforward process using an image from hello gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="73031-106">Kimlik doğrulaması: Kullanıcı adları, parolalar ve SSH anahtarları</span><span class="sxs-lookup"><span data-stu-id="73031-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="73031-107">Bir ya da kullanıcı adı tooprovide sorulur hello Azure portal kullanarak bir Linux sanal makine oluştururken ve parola veya SSH ortak anahtarı.</span><span class="sxs-lookup"><span data-stu-id="73031-107">When creating a Linux virtual machine using hello Azure portal, you are asked tooprovide a either username and password or an SSH public key.</span></span> <span data-ttu-id="73031-108">Hello Azure Linux sanal makine dağıtmak için bir kullanıcı adı kısıtlaması aşağıdaki konu toohello seçimdir: Sistem hesaplarının adlarını (UID < 100) hello zaten mevcut sanal makine izin verilmez, 'root' örneğin.</span><span class="sxs-lookup"><span data-stu-id="73031-108">hello choice of a username for deploying a Linux virtual machine on Azure is subject toohello following constraint: names of system accounts (UID <100) already present in hello virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="73031-109">Bkz: [Linux çalıştıran bir sanal makine oluşturma](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="73031-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="73031-110">Bkz: [nasıl tooUse Linux Azure üzerinde SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="73031-110">See [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="73031-111">Süper kullanıcı ayrıcalıkları kullanarak alma`sudo`</span><span class="sxs-lookup"><span data-stu-id="73031-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="73031-112">Azure üzerinde sanal makine örneği dağıtımı sırasında belirtilen hello kullanıcı hesabı ayrıcalıklı bir hesaptır.</span><span class="sxs-lookup"><span data-stu-id="73031-112">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="73031-113">Bu hesabı hello kullanarak hello Azure Linux Aracısı toobe mümkün tooelevate ayrıcalıkları tooroot tarafından (Süper kullanıcı hesabı) yapılandırılmış `sudo` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="73031-113">This account is configured by hello Azure Linux Agent toobe able tooelevate privileges tooroot (superuser account) using hello `sudo` utility.</span></span> <span data-ttu-id="73031-114">Bu kullanıcı hesabını kullanarak oturum sonra hello komut sözdizimini kullanarak kök olarak mümkün toorun komutları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="73031-114">Once logged in using this user account, you will be able toorun commands as root using hello command syntax:</span></span>

    # sudo <COMMAND>

<span data-ttu-id="73031-115">Kök Kabuğu'nu kullanarak isteğe bağlı olarak elde edebilirsiniz **sudo -s**.</span><span class="sxs-lookup"><span data-stu-id="73031-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="73031-116">Bkz: [Linux sanal makineleri Azure üzerinde kök ayrıcalıkları kullanma](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="73031-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="73031-117">Güvenlik duvarı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="73031-117">Firewall Configuration</span></span>
<span data-ttu-id="73031-118">Azure hello Azure portal belirtilen bağlantı tooports kısıtlayan bir gelen paket filtresi sağlar.</span><span class="sxs-lookup"><span data-stu-id="73031-118">Azure provides an inbound packet filter that restricts connectivity tooports specified in hello Azure portal.</span></span> <span data-ttu-id="73031-119">Varsayılan olarak, hello yalnızca izin verilen bağlantı noktası SSH şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="73031-119">By default, hello only allowed port is SSH.</span></span> <span data-ttu-id="73031-120">Hello Azure portalında uç noktaları yapılandırarak Linux sanal makinenize erişim tooadditional bağlantı noktalarını açın:</span><span class="sxs-lookup"><span data-stu-id="73031-120">You may open up access tooadditional ports on your Linux virtual machine by configuring endpoints in hello Azure portal:</span></span>

* <span data-ttu-id="73031-121">Bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="73031-121">See: [How tooSet Up Endpoints tooa Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="73031-122">Merhaba Linux hello Azure Galerisi görüntülerinde hello getirmeyin *iptables* Güvenlik Duvarı varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="73031-122">hello Linux images in hello Azure Gallery do not enable hello *iptables* firewall by default.</span></span> <span data-ttu-id="73031-123">İsterseniz, hello güvenlik duvarı yapılandırılabilir tooprovide ek filtreleme.</span><span class="sxs-lookup"><span data-stu-id="73031-123">If desired, hello firewall may be configured tooprovide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="73031-124">Ana bilgisayar adı değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="73031-124">Hostname Changes</span></span>
<span data-ttu-id="73031-125">Linux görüntü örneği başlangıçta dağıtmak için gerekli tooprovide hello sanal makine için bir konak adı olur.</span><span class="sxs-lookup"><span data-stu-id="73031-125">When you initially deploy an instance of a Linux image, you are required tooprovide a host name for hello virtual machine.</span></span> <span data-ttu-id="73031-126">Merhaba sanal makine çalışmaya başladıktan sonra bu ana bilgisayar adı yayımlanan toohello platform DNS sunucuları, böylelikle birden çok sanal makineleri bağlı tooeach diğer IP adresi aramalarını ana bilgisayar adları kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73031-126">Once hello virtual machine is running, this hostname is published toohello platform DNS servers so that multiple virtual machines connected tooeach other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="73031-127">Bir sanal makine dağıtıldıktan sonra ana bilgisayar adı değişiklikleri isterseniz, lütfen hello komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="73031-127">If hostname changes are desired after a virtual machine has been deployed, please use hello command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="73031-128">Hello Azure Linux Aracısı işlevselliği içerir tooautomatically bu ad değişikliği algılamak uygun şekilde hello sanal makine toopersist bu değişikliği yapılandırmak ve bu değişiklik toohello platform DNS sunucularına yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="73031-128">hello Azure Linux Agent includes functionality tooautomatically detect this name change and appropriately configure hello virtual machine toopersist this change and publish this change toohello platform DNS servers.</span></span>

* [<span data-ttu-id="73031-129">Azure Linux Aracısı Kullanıcı Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="73031-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="73031-130">Bulut başlatma</span><span class="sxs-lookup"><span data-stu-id="73031-130">Cloud-Init</span></span>
<span data-ttu-id="73031-131">**Ubuntu** ve **CoreOS** görüntüleri kullanan bir sanal makine önyükleme için ek özellikler sağlayan Azure ile ilgili bulut başlatma.</span><span class="sxs-lookup"><span data-stu-id="73031-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="73031-132">Nasıl tooInject özel veri</span><span class="sxs-lookup"><span data-stu-id="73031-132">How tooInject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="73031-133">Özel veri ve bulut-Init Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="73031-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="73031-134">Bulut Init kullanarak Azure takas bölümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="73031-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="73031-135">Nasıl tooUse CoreOS Azure ile ilgili</span><span class="sxs-lookup"><span data-stu-id="73031-135">How tooUse CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="73031-136">Sanal makine görüntü yakalama</span><span class="sxs-lookup"><span data-stu-id="73031-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="73031-137">Azure görüntüye kullanılan toodeploy ek sanal makine örneklerinin sonradan olabilir hello özelliği toocapture hello var olan bir sanal makinenin durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="73031-137">Azure provides hello ability toocapture hello state of an existing virtual machine into an image that can subsequently be used toodeploy additional virtual machine instances.</span></span> <span data-ttu-id="73031-138">Hello Azure Linux Aracısı bazı hello sağlama işlemi sırasında gerçekleştirilen özelleştirme hello kullanılan toorollback olabilir.</span><span class="sxs-lookup"><span data-stu-id="73031-138">hello Azure Linux Agent may be used toorollback some of hello customization that was performed during hello provisioning process.</span></span> <span data-ttu-id="73031-139">Bir görüntü olarak toocapture bir sanal makine hello adımları izleyebilir:</span><span class="sxs-lookup"><span data-stu-id="73031-139">You may follow hello steps below toocapture a virtual machine as an image:</span></span>

1. <span data-ttu-id="73031-140">Çalıştırma **waagent-deprovision** tooundo özelleştirme sağlama.</span><span class="sxs-lookup"><span data-stu-id="73031-140">Run **waagent -deprovision** tooundo provisioning customization.</span></span> <span data-ttu-id="73031-141">Veya **waagent-deprovision + kullanıcı** toooptionally sağlama ve tüm ilişkili veri sırasında belirtilen hello kullanıcı hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="73031-141">Or **waagent -deprovision+user** toooptionally delete hello user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="73031-142">Aşağı/güç hello sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="73031-142">Shut down/power off hello virtual machine.</span></span>
3. <span data-ttu-id="73031-143">Tıklatın **yakalama** hello Azure portal ya da kullanım hello PowerShell veya CLI toocapture hello sanal makinesini görüntü olarak araçları.</span><span class="sxs-lookup"><span data-stu-id="73031-143">Click **Capture** in hello Azure portal or use hello PowerShell or CLI tools toocapture hello virtual machine as an image.</span></span>
   
   * <span data-ttu-id="73031-144">Bkz: [nasıl tooCapture bir şablon olarak Linux sanal makine tooUse](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="73031-144">See: [How tooCapture a Linux Virtual Machine tooUse as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="73031-145">Diskleri ekleme</span><span class="sxs-lookup"><span data-stu-id="73031-145">Attaching Disks</span></span>
<span data-ttu-id="73031-146">Her bir sanal makine geçici, yerel olan *kaynak disk* bağlı.</span><span class="sxs-lookup"><span data-stu-id="73031-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="73031-147">Kaynak disk üzerindeki verileri yeniden başlatmalar arasında dayanıklı olmayabileceğinden, genellikle uygulama ve geçici için hello sanal makinede çalışan işlemleri tarafından kullanılır ve **geçici** depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="73031-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in hello virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="73031-148">Ayrıca, hello işletim sistemi için kullanılan toostore hello sayfa veya takas dosya sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="73031-148">It is also used toostore hello page or swap files for hello operating system.</span></span>

<span data-ttu-id="73031-149">Linux üzerinde hello kaynak disk genellikle hello Azure Linux aracısı tarafından yönetilmesi ve otomatik olarak çok takılı**/mnt/kaynak** (veya **/mnt** Ubuntu görüntülerinde).</span><span class="sxs-lookup"><span data-stu-id="73031-149">On Linux, hello resource disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="73031-150">Bu hello kaynak diski Not bir **geçici** disk ve silinecek ve hello VM yeniden başlatıldığında yeniden biçimlendirilen.</span><span class="sxs-lookup"><span data-stu-id="73031-150">Note that hello resource disk is a **temporary** disk, and might be deleted and reformatted when hello VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="73031-151">Linux'ta hello veri diski hello çekirdek tarafından adlandırılabilir `/dev/sdc`, ve gereken toopartition, biçimlendirmek ve bu kaynağın bağlayın.</span><span class="sxs-lookup"><span data-stu-id="73031-151">On Linux hello data disk might be named by hello kernel as `/dev/sdc`, and users will need toopartition, format and mount that resource.</span></span> <span data-ttu-id="73031-152">Bu başlangıç Öğreticisi Adım adım ele alınmıştır: [nasıl tooAttach bir sanal makine veri diski tooa](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73031-152">This is covered step-by-step in hello tutorial: [How tooAttach a Data Disk tooa Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="73031-153">**Ayrıca bkz:** [yazılım RAID Linux üzerinde yapılandırma](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [LVM azure'da bir Linux VM yapılandırın](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="73031-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

