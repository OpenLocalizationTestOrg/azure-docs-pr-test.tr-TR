---
title: "Azure üzerinde FreeBSD giriş | Microsoft Docs"
description: "Azure üzerinde FreeBSD sanal makineleri kullanma hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 7ada9fddd7ffccc3dcbfe3eac05d99b710b67cbc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="2c1e5-103">Azure üzerinde FreeBSD giriş</span><span class="sxs-lookup"><span data-stu-id="2c1e5-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="2c1e5-104">Bu konuda FreeBSD sanal makine Azure'da çalışan bir genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="2c1e5-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2c1e5-105">Overview</span></span>
<span data-ttu-id="2c1e5-106">Microsoft Azure FreeBSD gelişmiş bilgisayar işletim sisteminin güç modern sunuculara, masaüstü bilgisayarları, kullanılan ve embedded platformları ' dir.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="2c1e5-107">Microsoft Corporation'ın yapmadan FreeBSD görüntülerini kullanılabilir ile azure'da [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="2c1e5-108">Şu anda aşağıdaki FreeBSD sürümleri görüntü olarak Microsoft tarafından sunulan:</span><span class="sxs-lookup"><span data-stu-id="2c1e5-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="2c1e5-109">FreeBSD 10.3-sürüm</span><span class="sxs-lookup"><span data-stu-id="2c1e5-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="2c1e5-110">FreeBSD 11.0-sürüm</span><span class="sxs-lookup"><span data-stu-id="2c1e5-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="2c1e5-111">Aracı FreeBSD VM ve VM ilk kullanımda (kullanıcı adı, parola veya SSH anahtarı, ana bilgisayar adı, vb.) sağlama ve işlevlerini seçmeli VM uzantıları için etkinleştirmek gibi işlemleri için Azure doku arasındaki iletişim için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="2c1e5-112">FreeBSD gelecek sürümlerinde olduğu gibi stratejisi güncel ve FreeBSD yayın mühendislik ekibi tarafından kısa süre içinde yayımladıktan sonra en son sürümlerde kullanılabilir yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="2c1e5-113">FreeBSD sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="2c1e5-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="2c1e5-114">FreeBSD sanal makine dağıtımı Azure portalından Azure Marketi'nden görüntü kullanarak bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="2c1e5-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="2c1e5-115">FreeBSD Azure Market'te 10.3</span><span class="sxs-lookup"><span data-stu-id="2c1e5-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="2c1e5-116">FreeBSD Azure Market'te 11.0</span><span class="sxs-lookup"><span data-stu-id="2c1e5-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="2c1e5-117">Azure CLI 2.0 aracılığıyla bir FreeBSD VM üzerinde FreeBSD oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c1e5-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="2c1e5-118">Yüklemek gereken ilk [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) FreeBSD makinede komutu aşağıdaki olsa.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="2c1e5-119">Bash FreeBSD makinenize yüklü değilse, komutu yüklemeden önce aşağıdaki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="2c1e5-120">Python FreeBSD makinenize yüklü değilse, komutları yüklemeden önce aşağıdaki çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="2c1e5-121">Yükleme sırasında istendiğinde `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="2c1e5-122">Yanıtı verirseniz `y` ve girin `/etc/rc.conf` olarak `a path to an rc file to update`, sorunu karşılayan `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="2c1e5-123">Bu sorunu gidermek için yazma geçerli kullanıcının dosyayı karşı sağdan vermelisiniz `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="2c1e5-124">Şimdi Azure'da oturum ve FreeBSD VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="2c1e5-125">Aşağıda bir FreeBSD 11.0 VM oluşturmak için bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="2c1e5-126">Parametresi de ekleyebilirsiniz `--public-ip-address-dns-name` yeni oluşturulan bir genel IP için genel benzersiz bir DNS adına sahip.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2c1e5-127">Ardından, sizin FreeBSD VM Dağıtım yukarıdaki çıktıda yazdırılan IP adresi üzerinden oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="2c1e5-128">FreeBSD VM uzantıları</span><span class="sxs-lookup"><span data-stu-id="2c1e5-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="2c1e5-129">Desteklenen VM uzantıları FreeBSD aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="2c1e5-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="2c1e5-130">VMAccess</span></span>
<span data-ttu-id="2c1e5-131">[VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) uzantısı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c1e5-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="2c1e5-132">Özgün sudo kullanıcının parolasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="2c1e5-133">Yeni bir sudo kullanıcı belirtilen parolayla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="2c1e5-134">Verilen anahtarla genel ana bilgisayar anahtarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="2c1e5-135">Ana makine anahtarı sağlanmazsa, VM sağlama işlemi sırasında sağlanan genel ana bilgisayar anahtarını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="2c1e5-136">SSH bağlantı noktası (22) açın ve reset_ssh ayarlarsanız sshd_config geri true.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="2c1e5-137">Varolan bir kullanıcı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-137">Remove the existing user.</span></span>
* <span data-ttu-id="2c1e5-138">Diskleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-138">Check disks.</span></span>
* <span data-ttu-id="2c1e5-139">Eklenen bir disk onarın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="2c1e5-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="2c1e5-140">CustomScript</span></span>
<span data-ttu-id="2c1e5-141">[CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) uzantısı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2c1e5-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="2c1e5-142">Sağlanırsa, özel komut dosyaları Azure Storage veya dış ortak depolama (örneğin, GitHub) indirin.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="2c1e5-143">Giriş noktası komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-143">Run the entry point script.</span></span>
* <span data-ttu-id="2c1e5-144">Satır içi komutları destekler.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-144">Support inline commands.</span></span>
* <span data-ttu-id="2c1e5-145">Windows stili yeni satır kabuk ve Python komut dosyaları otomatik olarak dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="2c1e5-146">Ürün reçetesi kabuk ve Python komut dosyaları otomatik olarak kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="2c1e5-147">CommandToExecute gizli verileri koruyun.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="2c1e5-148">FreeBSD VM yalnızca destekler CustomScript sürüm 1.x şimdi tarafından.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="2c1e5-149">Kimlik doğrulaması: kullanıcı adları, parolalar ve SSH anahtarları</span><span class="sxs-lookup"><span data-stu-id="2c1e5-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="2c1e5-150">Azure portalı kullanarak bir FreeBSD sanal makine oluştururken, bir kullanıcı adı, parola veya SSH ortak anahtarı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="2c1e5-151">Azure FreeBSD sanal makine dağıtmak için kullanıcı adları system hesaplarının adlarını değil eşleşmesi gerekir (UID < 100) sanal makine ("Kök", örneğin) zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="2c1e5-152">Şu anda yalnızca RSA SSH anahtarı desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="2c1e5-153">Çok satırlı SSH anahtarı ile başlamalıdır `---- BEGIN SSH2 PUBLIC KEY ----` ve sonunda `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="2c1e5-154">Süper kullanıcı ayrıcalıkları alma</span><span class="sxs-lookup"><span data-stu-id="2c1e5-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="2c1e5-155">Azure üzerinde sanal makine örneği dağıtımı sırasında belirtilen kullanıcı hesabı ayrıcalıklı bir hesaptır.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="2c1e5-156">Sudo paketi yayımlanmış FreeBSD görüntüde yüklendi.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="2c1e5-157">Bu kullanıcı hesabıyla oturum açtınız sonra komut sözdizimini kullanarak kök olarak komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="2c1e5-158">Bir kök Kabuğu'nu kullanarak isteğe bağlı olarak elde edebilirsiniz `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="2c1e5-159">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="2c1e5-159">Known issues</span></span>
<span data-ttu-id="2c1e5-160">[Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) 2.2.2 sahip [bilinen bir sorun] sürüm (https://github.com/Azure/WALinuxAgent/pull/517) neden sağlama hatası Azure FreeBSD sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="2c1e5-161">Düzeltme tarafından yakalanan [Azure VM Konuk aracısının](https://github.com/Azure/WALinuxAgent/) sürüm 2.2.3 ve sonraki sürümlerinde.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2c1e5-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c1e5-162">Next steps</span></span>
* <span data-ttu-id="2c1e5-163">Git [Azure Marketi](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) FreeBSD VM oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="2c1e5-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="2c1e5-164">Azure için kendi FreeBSD duruma getirmek istediğiniz oluştuysa, [Azure FreeBSD VHD oluşturun ve yükleyin](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="2c1e5-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](classic/freebsd-create-upload-vhd.md).</span></span>
