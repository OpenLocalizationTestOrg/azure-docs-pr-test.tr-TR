---
title: "aaaUsing bulut init toocustomize azure'da oluşturma sırasında bir Linux VM | Microsoft Docs"
description: "Nasıl ile oluşturma sırasında bir Linux VM toouse bulut init toocustomize hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="b9621-103">Hello Azure CLI 1.0 ile oluşturma sırasında bulut init toocustomize bir Linux VM kullanın</span><span class="sxs-lookup"><span data-stu-id="b9621-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="b9621-104">Bu makalede nasıl toomake bulut init betik tooset hostname Merhaba, güncelleştirme yüklü paketleri ve kullanıcı hesaplarını yönetme gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9621-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="b9621-105">Merhaba bulut başlatma komut dosyaları hello Azure clı'dan VM oluşturma sırasında denir.</span><span class="sxs-lookup"><span data-stu-id="b9621-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="b9621-106">Merhaba makale gerektirir:</span><span class="sxs-lookup"><span data-stu-id="b9621-106">hello article requires:</span></span>

* <span data-ttu-id="b9621-107">bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="b9621-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b9621-108">Merhaba [Azure CLI](../../cli-install-nodejs.md) oturum açarken `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b9621-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b9621-109">Hello Azure CLI *olmalıdır* Azure Resource Manager moduna `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b9621-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b9621-110">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="b9621-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b9621-111">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="b9621-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b9621-112">[Azure CLI 1.0](#quick-commands) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="b9621-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b9621-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="b9621-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b9621-114">Hızlı Komutlar</span><span class="sxs-lookup"><span data-stu-id="b9621-114">Quick Commands</span></span>
<span data-ttu-id="b9621-115">Merhaba hostname ayarlar, tüm paketleri güncelleştirir ve bir sudo kullanıcı tooLinux ekleyen bir bulut init.txt komut dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9621-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```sh
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```
<span data-ttu-id="b9621-116">Bir kaynak grubu toolaunch içine VM'ler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9621-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="b9621-117">Bulut init tooconfigure kullanarak bir Linux VM oluşturun, önyükleme sırasında.</span><span class="sxs-lookup"><span data-stu-id="b9621-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b9621-118">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="b9621-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="b9621-119">Giriş</span><span class="sxs-lookup"><span data-stu-id="b9621-119">Introduction</span></span>
<span data-ttu-id="b9621-120">Yeni bir Linux VM başlattığında, özelleştirilmiş veya gereksinimleriniz için hazır herhangi bir şeyin standart bir Linux VM aldıklarından.</span><span class="sxs-lookup"><span data-stu-id="b9621-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="b9621-121">[Bulut init](https://cloudinit.readthedocs.org) standart yol tooinject ilk kez kaydınızı hello önyükleme yapmak, Linux VM bir komut dosyası veya yapılandırma ayarlarını aynıdır.</span><span class="sxs-lookup"><span data-stu-id="b9621-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="b9621-122">Azure üzerinde üç farklı yolla toomake bir değişiklik yoktur bir Linux VM üzerine olarak dağıtılabilir veya önyüklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="b9621-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="b9621-123">Bulut init kullanarak komut dosyalarını yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="b9621-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="b9621-124">Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9621-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="b9621-125">Bulut init kullanarak bir Azure şablonu.</span><span class="sxs-lookup"><span data-stu-id="b9621-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="b9621-126">Bir Azure şablonu kullanarak [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b9621-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b9621-127">önyükleme sonra herhangi bir zamanda tooinject komut dosyaları:</span><span class="sxs-lookup"><span data-stu-id="b9621-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="b9621-128">SSH toorun doğrudan komutları</span><span class="sxs-lookup"><span data-stu-id="b9621-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="b9621-129">Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperatively veya bir Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="b9621-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="b9621-130">Yapılandırma yönetimi araçları Ansible, Salt, Chef, Puppet gibi ve.</span><span class="sxs-lookup"><span data-stu-id="b9621-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="b9621-131">: VMAccess uzantısını yürütür hello aynı kök gibi bir komut dosyası yolu SSH kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9621-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="b9621-132">Ancak, hello VM uzantısı kullanılarak çeşitli özellikler senaryonuza bağlı olarak yararlı olabilecek Azure sağladığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9621-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="b9621-133">Azure VM bulut init kullanılabilirliğine hızlı Oluştur görüntü diğer adları:</span><span class="sxs-lookup"><span data-stu-id="b9621-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="b9621-134">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="b9621-134">Alias</span></span> | <span data-ttu-id="b9621-135">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="b9621-135">Publisher</span></span> | <span data-ttu-id="b9621-136">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="b9621-136">Offer</span></span> | <span data-ttu-id="b9621-137">SKU</span><span class="sxs-lookup"><span data-stu-id="b9621-137">SKU</span></span> | <span data-ttu-id="b9621-138">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b9621-138">Version</span></span> | <span data-ttu-id="b9621-139">Bulut başlatma</span><span class="sxs-lookup"><span data-stu-id="b9621-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="b9621-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="b9621-140">CentOS</span></span> |<span data-ttu-id="b9621-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b9621-141">OpenLogic</span></span> |<span data-ttu-id="b9621-142">Centos</span><span class="sxs-lookup"><span data-stu-id="b9621-142">Centos</span></span> |<span data-ttu-id="b9621-143">7.2</span><span class="sxs-lookup"><span data-stu-id="b9621-143">7.2</span></span> |<span data-ttu-id="b9621-144">en son</span><span class="sxs-lookup"><span data-stu-id="b9621-144">latest</span></span> |<span data-ttu-id="b9621-145">Yok</span><span class="sxs-lookup"><span data-stu-id="b9621-145">no</span></span> |
| <span data-ttu-id="b9621-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b9621-146">CoreOS</span></span> |<span data-ttu-id="b9621-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b9621-147">CoreOS</span></span> |<span data-ttu-id="b9621-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b9621-148">CoreOS</span></span> |<span data-ttu-id="b9621-149">Dengeli</span><span class="sxs-lookup"><span data-stu-id="b9621-149">Stable</span></span> |<span data-ttu-id="b9621-150">en son</span><span class="sxs-lookup"><span data-stu-id="b9621-150">latest</span></span> |<span data-ttu-id="b9621-151">Evet</span><span class="sxs-lookup"><span data-stu-id="b9621-151">yes</span></span> |
| <span data-ttu-id="b9621-152">Debian</span><span class="sxs-lookup"><span data-stu-id="b9621-152">Debian</span></span> |<span data-ttu-id="b9621-153">credativ</span><span class="sxs-lookup"><span data-stu-id="b9621-153">credativ</span></span> |<span data-ttu-id="b9621-154">Debian</span><span class="sxs-lookup"><span data-stu-id="b9621-154">Debian</span></span> |<span data-ttu-id="b9621-155">8</span><span class="sxs-lookup"><span data-stu-id="b9621-155">8</span></span> |<span data-ttu-id="b9621-156">en son</span><span class="sxs-lookup"><span data-stu-id="b9621-156">latest</span></span> |<span data-ttu-id="b9621-157">Yok</span><span class="sxs-lookup"><span data-stu-id="b9621-157">no</span></span> |
| <span data-ttu-id="b9621-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b9621-158">openSUSE</span></span> |<span data-ttu-id="b9621-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="b9621-159">SUSE</span></span> |<span data-ttu-id="b9621-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b9621-160">openSUSE</span></span> |<span data-ttu-id="b9621-161">13.2</span><span class="sxs-lookup"><span data-stu-id="b9621-161">13.2</span></span> |<span data-ttu-id="b9621-162">en son</span><span class="sxs-lookup"><span data-stu-id="b9621-162">latest</span></span> |<span data-ttu-id="b9621-163">Yok</span><span class="sxs-lookup"><span data-stu-id="b9621-163">no</span></span> |
| <span data-ttu-id="b9621-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="b9621-164">RHEL</span></span> |<span data-ttu-id="b9621-165">RedHat</span><span class="sxs-lookup"><span data-stu-id="b9621-165">Redhat</span></span> |<span data-ttu-id="b9621-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="b9621-166">RHEL</span></span> |<span data-ttu-id="b9621-167">7.2</span><span class="sxs-lookup"><span data-stu-id="b9621-167">7.2</span></span> |<span data-ttu-id="b9621-168">en son</span><span class="sxs-lookup"><span data-stu-id="b9621-168">latest</span></span> |<span data-ttu-id="b9621-169">Yok</span><span class="sxs-lookup"><span data-stu-id="b9621-169">no</span></span> |
| <span data-ttu-id="b9621-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="b9621-170">UbuntuLTS</span></span> |<span data-ttu-id="b9621-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="b9621-171">Canonical</span></span> |<span data-ttu-id="b9621-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b9621-172">UbuntuServer</span></span> |<span data-ttu-id="b9621-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="b9621-173">14.04.4-LTS</span></span> |<span data-ttu-id="b9621-174">en son</span><span class="sxs-lookup"><span data-stu-id="b9621-174">latest</span></span> |<span data-ttu-id="b9621-175">Evet</span><span class="sxs-lookup"><span data-stu-id="b9621-175">yes</span></span> |

<span data-ttu-id="b9621-176">Microsoft bizim ortakları tooget bulut dahil başlatma çalışmak ve çalışma tooAzure sağladıkları hello görüntülerinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="b9621-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="b9621-177">Bir bulut init betik toohello VM oluşturma hello Azure CLI ile ekleme</span><span class="sxs-lookup"><span data-stu-id="b9621-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="b9621-178">Azure üzerinde bir VM oluştururken, bir bulut init komut dosyası toolaunch hello Azure CLI kullanarak hello bulut init dosyasını belirtin `--custom-data` geçin.</span><span class="sxs-lookup"><span data-stu-id="b9621-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="b9621-179">Bir kaynak grubu toolaunch içine VM'ler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9621-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="b9621-180">Bulut init tooconfigure kullanarak bir Linux VM oluşturun, önyükleme sırasında.</span><span class="sxs-lookup"><span data-stu-id="b9621-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="b9621-181">Bir bulut init betik tooset hello ana bilgisayar adını bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9621-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="b9621-182">Merhaba basit ve herhangi bir Linux VM için en önemli ayarları biri hello ana bilgisayar adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b9621-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="b9621-183">Biz kolayca bu bulut init ile bu komut dosyası kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9621-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="b9621-184">Adlı örnek bulut başlatma komut dosyasını `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="b9621-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="b9621-185">Çok hello hostname Hello ilk başlatılırken hello VM, bu bulut başlatma komut dosyasını ayarlar`myservername`.</span><span class="sxs-lookup"><span data-stu-id="b9621-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="b9621-186">Oturum açma ve hello hello ana doğrulayın yeni VM.</span><span class="sxs-lookup"><span data-stu-id="b9621-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="b9621-187">Bir bulut init betik tooupdate Linux oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9621-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="b9621-188">Güvenlik için Ubuntu VM tooupdate hello ilk önyüklemede istiyor.</span><span class="sxs-lookup"><span data-stu-id="b9621-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="b9621-189">Bulut init kullanarak hello ile Merhaba Linux dağıtım kullandığınıza bağlı olarak kod izleyin yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="b9621-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="b9621-190">Örnek bulut init betik `cloud_config_apt_upgrade.txt` hello Debian ailesi için</span><span class="sxs-lookup"><span data-stu-id="b9621-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="b9621-191">Linux önyüklendikten sonra tüm yüklü hello paketler aracılığıyla güncelleştirilir `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="b9621-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="b9621-192">Oturum açma ve tüm paketler güncelleştirilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b9621-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="b9621-193">Bir kullanıcı tooLinux bulut init betik tooadd oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9621-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="b9621-194">Yeni bir Linux VM üzerinde hello ilk görevlerden biridir tooadd kendiniz veya tooavoid kullanmak için bir kullanıcı `root`.</span><span class="sxs-lookup"><span data-stu-id="b9621-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="b9621-195">SSH anahtarları olan kullanılabilirlik ve güvenlik için en iyi uygulama ve toohello eklenen `~/.ssh/authorized_keys` bu bulut init komut dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="b9621-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="b9621-196">Örnek bulut init betik `cloud_config_add_users.txt` Debian ailesi için</span><span class="sxs-lookup"><span data-stu-id="b9621-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="b9621-197">Linux önyüklendikten sonra tüm listelenen hello oluşturulan ve eklenen toohello sudo Grup kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="b9621-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="b9621-198">Oturum açma ve yeni oluşturulan hello kullanıcı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b9621-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="b9621-199">Çıktı</span><span class="sxs-lookup"><span data-stu-id="b9621-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="b9621-200">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b9621-200">Next Steps</span></span>
<span data-ttu-id="b9621-201">Bulut init bir standart yol toomodify önyükleme, Linux VM'de durumundadır.</span><span class="sxs-lookup"><span data-stu-id="b9621-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="b9621-202">Ayrıca Azure toomodify izin VM uzantıları, LinuxVM önyükleme veya çalışırken sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b9621-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="b9621-203">Örneğin, Hello VM çalışırken hello Azure VMAccessExtension tooreset SSH veya kullanıcı bilgilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9621-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="b9621-204">Bulut başlatma ile bir yeniden başlatma tooreset hello parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9621-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="b9621-205">Sanal makine uzantıları ve özellikleri hakkında</span><span class="sxs-lookup"><span data-stu-id="b9621-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b9621-206">Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello</span><span class="sxs-lookup"><span data-stu-id="b9621-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

