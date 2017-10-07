---
title: "Azure üzerinde aaaIntroduction tooFreeBSD | Microsoft Docs"
description: "Azure üzerinde FreeBSD sanal makineleri kullanma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="e5a52-103">Azure ile ilgili giriş tooFreeBSD</span><span class="sxs-lookup"><span data-stu-id="e5a52-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="e5a52-104">Bu konuda FreeBSD sanal makine Azure'da çalışan bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5a52-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="e5a52-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e5a52-105">Overview</span></span>
<span data-ttu-id="e5a52-106">Microsoft Azure FreeBSD gelişmiş bilgisayar işletim sistemi toopower modern sunucular, masaüstü bilgisayarları ve katıştırılmış platformları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5a52-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="e5a52-107">Microsoft Corporation'ın yapmadan FreeBSD görüntülerini kullanılabilir Azure'da hello ile [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e5a52-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="e5a52-108">Şu anda hello aşağıdaki FreeBSD sürümlerini görüntüler olarak Microsoft tarafından sunulan:</span><span class="sxs-lookup"><span data-stu-id="e5a52-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="e5a52-109">FreeBSD 10.3-sürüm</span><span class="sxs-lookup"><span data-stu-id="e5a52-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="e5a52-110">FreeBSD 11.0-sürüm</span><span class="sxs-lookup"><span data-stu-id="e5a52-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="e5a52-111">Merhaba FreeBSD VM arasındaki iletişim için Hello Aracısı sorumludur ve hello Azure yapı sağlama gibi işlemler için (kullanıcı adı, parola veya SSH anahtarı, ana bilgisayar adı, vb.) ilk kullanım ve seçmeli VM uzantıları için etkinleştirme işlevselliği VM hello.</span><span class="sxs-lookup"><span data-stu-id="e5a52-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="e5a52-112">FreeBSD gelecek sürümlerinde, olduğu gibi hello stratejisi toostay geçerli olduğundan ve hello FreeBSD yayın mühendislik ekibi tarafından kısa süre içinde yayımladıktan sonra hello en son sürümlerde kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="e5a52-113">FreeBSD sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="e5a52-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="e5a52-114">FreeBSD sanal makine dağıtma hello Azure Marketi hello Azure Portalı'ndan bir görüntüden kullanarak bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="e5a52-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="e5a52-115">Hello Azure Marketi üzerinde FreeBSD 10.3</span><span class="sxs-lookup"><span data-stu-id="e5a52-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="e5a52-116">Hello Azure Marketi üzerinde FreeBSD 11.0</span><span class="sxs-lookup"><span data-stu-id="e5a52-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="e5a52-117">Azure CLI 2.0 aracılığıyla bir FreeBSD VM üzerinde FreeBSD oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5a52-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="e5a52-118">Tooinstall gereken ilk [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) FreeBSD makinede komutu aşağıdaki olsa.</span><span class="sxs-lookup"><span data-stu-id="e5a52-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="e5a52-119">Bash FreeBSD makinenize yüklü değilse, komutu hello yüklemeden önce aşağıdaki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="e5a52-120">Python FreeBSD makinenize yüklü değilse, komutları hello yüklemeden önce aşağıdaki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="e5a52-121">Merhaba yükleme sırasında istendiğinde `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="e5a52-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="e5a52-122">Yanıtı verirseniz `y` ve girin `/etc/rc.conf` olarak `a path tooan rc file tooupdate`, hello sorunu karşılayan `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="e5a52-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="e5a52-123">tooresolve bu sorunu hello yazma sağ toocurrent kullanıcı hello dosya karşı vermelisiniz `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="e5a52-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="e5a52-124">Şimdi Azure'da oturum ve FreeBSD VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5a52-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="e5a52-125">Bir örnek toocreate FreeBSD 11.0 VM aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="e5a52-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="e5a52-126">Merhaba parametresi de ekleyebilirsiniz `--public-ip-address-dns-name` yeni oluşturulan bir genel IP için genel benzersiz bir DNS adına sahip.</span><span class="sxs-lookup"><span data-stu-id="e5a52-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="e5a52-127">Ardından dağıtım yukarıda hello çıktısını yazdırılmıştır hello IP adresi üzerinden tooyour FreeBSD VM olarak oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="e5a52-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="e5a52-128">FreeBSD VM uzantıları</span><span class="sxs-lookup"><span data-stu-id="e5a52-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="e5a52-129">Desteklenen VM uzantıları FreeBSD aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e5a52-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="e5a52-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="e5a52-130">VMAccess</span></span>
<span data-ttu-id="e5a52-131">Merhaba [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) uzantısı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5a52-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="e5a52-132">Merhaba özgün sudo kullanıcı Hello parolasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="e5a52-133">Yeni bir sudo kullanıcı belirtilen hello parolasıyla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5a52-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="e5a52-134">Verilen hello anahtarla Hello genel ana bilgisayar anahtarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="e5a52-135">VM Hello ana makine anahtarı sağlanmazsa, sağlama sırasında sağlanan hello genel ana bilgisayar anahtarını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="e5a52-136">Merhaba SSH bağlantı noktası (22) açın ve reset_ssh tootrue ayarlarsanız hello sshd_config geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e5a52-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="e5a52-137">Merhaba varolan kullanıcı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-137">Remove hello existing user.</span></span>
* <span data-ttu-id="e5a52-138">Diskleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e5a52-138">Check disks.</span></span>
* <span data-ttu-id="e5a52-139">Eklenen bir disk onarın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="e5a52-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="e5a52-140">CustomScript</span></span>
<span data-ttu-id="e5a52-141">Merhaba [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) uzantısı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5a52-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="e5a52-142">Sağlanırsa, özelleştirilmiş hello betikleri Azure Storage veya dış ortak depolama (örneğin, GitHub) indirin.</span><span class="sxs-lookup"><span data-stu-id="e5a52-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="e5a52-143">Merhaba giriş noktası komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-143">Run hello entry point script.</span></span>
* <span data-ttu-id="e5a52-144">Satır içi komutları destekler.</span><span class="sxs-lookup"><span data-stu-id="e5a52-144">Support inline commands.</span></span>
* <span data-ttu-id="e5a52-145">Windows stili yeni satır kabuk ve Python komut dosyaları otomatik olarak dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="e5a52-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="e5a52-146">Ürün reçetesi kabuk ve Python komut dosyaları otomatik olarak kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e5a52-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="e5a52-147">CommandToExecute gizli verileri koruyun.</span><span class="sxs-lookup"><span data-stu-id="e5a52-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="e5a52-148">FreeBSD VM yalnızca destekler CustomScript sürüm 1.x şimdi tarafından.</span><span class="sxs-lookup"><span data-stu-id="e5a52-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="e5a52-149">Kimlik doğrulaması: kullanıcı adları, parolalar ve SSH anahtarları</span><span class="sxs-lookup"><span data-stu-id="e5a52-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="e5a52-150">Hello Azure portal kullanarak bir FreeBSD sanal makine oluştururken, bir kullanıcı adı, parola veya SSH ortak anahtarı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5a52-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="e5a52-151">Azure FreeBSD sanal makine dağıtmak için kullanıcı adları system hesaplarının adlarını değil eşleşmesi gerekir (UID < 100) hello sanal makine ("Kök", örneğin) zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="e5a52-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="e5a52-152">Şu anda yalnızca hello RSA SSH anahtarı desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e5a52-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="e5a52-153">Çok satırlı SSH anahtarı ile başlamalıdır `---- BEGIN SSH2 PUBLIC KEY ----` ve sonunda `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="e5a52-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="e5a52-154">Süper kullanıcı ayrıcalıkları alma</span><span class="sxs-lookup"><span data-stu-id="e5a52-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="e5a52-155">Azure üzerinde sanal makine örneği dağıtımı sırasında belirtilen hello kullanıcı hesabı ayrıcalıklı bir hesaptır.</span><span class="sxs-lookup"><span data-stu-id="e5a52-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="e5a52-156">Merhaba sudo paketi olarak yüklendiği hello yayımlanan FreeBSD görüntü.</span><span class="sxs-lookup"><span data-stu-id="e5a52-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="e5a52-157">Bu kullanıcı hesabıyla oturum açtınız sonra hello komut sözdizimini kullanarak kök olarak komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5a52-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="e5a52-158">Bir kök Kabuğu'nu kullanarak isteğe bağlı olarak elde edebilirsiniz `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="e5a52-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="e5a52-159">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="e5a52-159">Known issues</span></span>
<span data-ttu-id="e5a52-160">Merhaba [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) 2.2.2 sahip [bilinen bir sorun] sürüm (https://github.com/Azure/WALinuxAgent/pull/517) neden hello sağlama hatası Azure FreeBSD sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="e5a52-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="e5a52-161">Merhaba düzeltme tarafından yakalanan [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) sürüm 2.2.3 ve sonraki sürümlerinde.</span><span class="sxs-lookup"><span data-stu-id="e5a52-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e5a52-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5a52-162">Next steps</span></span>
* <span data-ttu-id="e5a52-163">Çok Git[Azure Marketi](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD VM.</span><span class="sxs-lookup"><span data-stu-id="e5a52-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="e5a52-164">Kendi FreeBSD tooAzure toobring istiyorsanız, çok başvuran[oluşturma ve karşıya yükleme FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="e5a52-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
