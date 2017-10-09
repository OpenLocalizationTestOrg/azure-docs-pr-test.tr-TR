---
title: aaaUse bulut init toocustomize bir Linux VM | Microsoft Docs
description: "Nasıl ile oluşturma sırasında bir Linux VM toouse bulut init toocustomize hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="3e673-103">Bulut init toocustomize bir Linux VM oluşturma sırasında kullanın</span><span class="sxs-lookup"><span data-stu-id="3e673-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="3e673-104">Bu makalede nasıl toomake bulut init betik tooset hostname Merhaba, güncelleştirme yüklü paketleri ve hello Azure CLI 2.0 olan kullanıcı hesaplarını yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e673-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="3e673-105">Azure CLI üzerinden bir sanal makine (VM) oluşturduğunuzda hello bulut Init komut adı verilir.</span><span class="sxs-lookup"><span data-stu-id="3e673-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="3e673-106">Daha ayrıntılı bir bakış uygulamaları yükleme hakkında bilgi için bkz: yapılandırma dosyaları yazma ve anahtar kasası, anahtarları injecting [Bu öğretici](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3e673-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="3e673-107">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3e673-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="3e673-108">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="3e673-108">Quick commands</span></span>
<span data-ttu-id="3e673-109">Merhaba hostname ayarlar, tüm paketleri güncelleştirir ve bir sudo kullanıcı tooLinux ekleyen bir bulut init.txt komut dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e673-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```yaml
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

<span data-ttu-id="3e673-110">Bir kaynak grubu toolaunch içine VM'ler ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3e673-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3e673-111">Merhaba aşağıdaki örnek adlı hello kaynak grubu oluşturur *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3e673-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="3e673-112">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak onu hello önyükleme sırasında `--custom-data` parametresi.</span><span class="sxs-lookup"><span data-stu-id="3e673-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="3e673-113">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="3e673-113">Detailed walkthrough</span></span>
<span data-ttu-id="3e673-114">Yeni bir Linux VM başlattığında, özelleştirilmiş veya gereksinimleriniz için hazır herhangi bir şeyin standart bir Linux VM aldıklarından.</span><span class="sxs-lookup"><span data-stu-id="3e673-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="3e673-115">[Bulut init](https://cloudinit.readthedocs.org) standart yol tooinject ilk kez kaydınızı hello önyükleme yapmak, Linux VM bir komut dosyası veya yapılandırma ayarlarını aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3e673-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="3e673-116">Azure üzerinde birkaç farklı yolu vardır toomake değişiklikleri bir Linux VM üzerine olarak dağıtılabilir veya önyüklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="3e673-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="3e673-117">Bulut init kullanarak komut dosyalarını yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="3e673-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="3e673-118">Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3e673-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="3e673-119">Bulut init kullanarak bir Azure şablonu.</span><span class="sxs-lookup"><span data-stu-id="3e673-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="3e673-120">Bir Azure şablonu kullanarak [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="3e673-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="3e673-121">önyükleme sonra herhangi bir zamanda tooinject komut dosyaları:</span><span class="sxs-lookup"><span data-stu-id="3e673-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="3e673-122">SSH toorun doğrudan komutları</span><span class="sxs-lookup"><span data-stu-id="3e673-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="3e673-123">Hello Azure'nı kullanarak betikleri Ekle [VMAccess uzantısını](using-vmaccess-extension.md), imperatively veya bir Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="3e673-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="3e673-124">Yapılandırma yönetimi araçları Ansible, Salt, Chef, Puppet gibi ve.</span><span class="sxs-lookup"><span data-stu-id="3e673-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="3e673-125">VMAccess uzantısını yürütür hello aynı kök gibi bir komut dosyası yolu SSH kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e673-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="3e673-126">Ancak, hello VM uzantısı kullanılarak çeşitli özellikler senaryonuza bağlı olarak yararlı olabilecek Azure sağladığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3e673-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="3e673-127">Azure VM bulut init kullanılabilirliğine hızlı Oluştur görüntü diğer adları:</span><span class="sxs-lookup"><span data-stu-id="3e673-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="3e673-128">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="3e673-128">Alias</span></span> | <span data-ttu-id="3e673-129">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="3e673-129">Publisher</span></span> | <span data-ttu-id="3e673-130">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="3e673-130">Offer</span></span> | <span data-ttu-id="3e673-131">SKU</span><span class="sxs-lookup"><span data-stu-id="3e673-131">SKU</span></span> | <span data-ttu-id="3e673-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="3e673-132">Version</span></span> | <span data-ttu-id="3e673-133">Bulut başlatma</span><span class="sxs-lookup"><span data-stu-id="3e673-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="3e673-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="3e673-134">CentOS</span></span> |<span data-ttu-id="3e673-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="3e673-135">OpenLogic</span></span> |<span data-ttu-id="3e673-136">Centos</span><span class="sxs-lookup"><span data-stu-id="3e673-136">Centos</span></span> |<span data-ttu-id="3e673-137">7.2</span><span class="sxs-lookup"><span data-stu-id="3e673-137">7.2</span></span> |<span data-ttu-id="3e673-138">en son</span><span class="sxs-lookup"><span data-stu-id="3e673-138">latest</span></span> |<span data-ttu-id="3e673-139">Yok</span><span class="sxs-lookup"><span data-stu-id="3e673-139">no</span></span> |
| <span data-ttu-id="3e673-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3e673-140">CoreOS</span></span> |<span data-ttu-id="3e673-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3e673-141">CoreOS</span></span> |<span data-ttu-id="3e673-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3e673-142">CoreOS</span></span> |<span data-ttu-id="3e673-143">Dengeli</span><span class="sxs-lookup"><span data-stu-id="3e673-143">Stable</span></span> |<span data-ttu-id="3e673-144">en son</span><span class="sxs-lookup"><span data-stu-id="3e673-144">latest</span></span> |<span data-ttu-id="3e673-145">Evet</span><span class="sxs-lookup"><span data-stu-id="3e673-145">yes</span></span> |
| <span data-ttu-id="3e673-146">Debian</span><span class="sxs-lookup"><span data-stu-id="3e673-146">Debian</span></span> |<span data-ttu-id="3e673-147">credativ</span><span class="sxs-lookup"><span data-stu-id="3e673-147">credativ</span></span> |<span data-ttu-id="3e673-148">Debian</span><span class="sxs-lookup"><span data-stu-id="3e673-148">Debian</span></span> |<span data-ttu-id="3e673-149">8</span><span class="sxs-lookup"><span data-stu-id="3e673-149">8</span></span> |<span data-ttu-id="3e673-150">en son</span><span class="sxs-lookup"><span data-stu-id="3e673-150">latest</span></span> |<span data-ttu-id="3e673-151">Yok</span><span class="sxs-lookup"><span data-stu-id="3e673-151">no</span></span> |
| <span data-ttu-id="3e673-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3e673-152">openSUSE</span></span> |<span data-ttu-id="3e673-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="3e673-153">SUSE</span></span> |<span data-ttu-id="3e673-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3e673-154">openSUSE</span></span> |<span data-ttu-id="3e673-155">13.2</span><span class="sxs-lookup"><span data-stu-id="3e673-155">13.2</span></span> |<span data-ttu-id="3e673-156">en son</span><span class="sxs-lookup"><span data-stu-id="3e673-156">latest</span></span> |<span data-ttu-id="3e673-157">Yok</span><span class="sxs-lookup"><span data-stu-id="3e673-157">no</span></span> |
| <span data-ttu-id="3e673-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="3e673-158">RHEL</span></span> |<span data-ttu-id="3e673-159">RedHat</span><span class="sxs-lookup"><span data-stu-id="3e673-159">Redhat</span></span> |<span data-ttu-id="3e673-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="3e673-160">RHEL</span></span> |<span data-ttu-id="3e673-161">7.2</span><span class="sxs-lookup"><span data-stu-id="3e673-161">7.2</span></span> |<span data-ttu-id="3e673-162">en son</span><span class="sxs-lookup"><span data-stu-id="3e673-162">latest</span></span> |<span data-ttu-id="3e673-163">Yok</span><span class="sxs-lookup"><span data-stu-id="3e673-163">no</span></span> |
| <span data-ttu-id="3e673-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="3e673-164">UbuntuLTS</span></span> |<span data-ttu-id="3e673-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="3e673-165">Canonical</span></span> |<span data-ttu-id="3e673-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="3e673-166">UbuntuServer</span></span> |<span data-ttu-id="3e673-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="3e673-167">14.04.4-LTS</span></span> |<span data-ttu-id="3e673-168">en son</span><span class="sxs-lookup"><span data-stu-id="3e673-168">latest</span></span> |<span data-ttu-id="3e673-169">Evet</span><span class="sxs-lookup"><span data-stu-id="3e673-169">yes</span></span> |

<span data-ttu-id="3e673-170">Bizim ortakları tooget bulut dahil başlatma çalışmak ve çalışma tooAzure sağladıkları hello görüntülerinde duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="3e673-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="3e673-171">Bir bulut init betik toohello VM oluşturma hello Azure CLI ile ekleme</span><span class="sxs-lookup"><span data-stu-id="3e673-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="3e673-172">Azure üzerinde bir VM oluştururken, bir bulut init komut dosyası toolaunch hello Azure CLI kullanarak hello bulut init dosyasını belirtin `--custom-data` geçin.</span><span class="sxs-lookup"><span data-stu-id="3e673-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="3e673-173">Bir kaynak grubu toolaunch içine VM'ler ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="3e673-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="3e673-174">Merhaba aşağıdaki örnek adlı hello kaynak grubu oluşturur *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3e673-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="3e673-175">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.</span><span class="sxs-lookup"><span data-stu-id="3e673-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="3e673-176">Bir bulut init betik tooset hello ana bilgisayar adını bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e673-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="3e673-177">Merhaba basit ve herhangi bir Linux VM için en önemli ayarları biri hello ana bilgisayar adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3e673-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="3e673-178">Biz kolayca bu bulut init ile bu komut dosyası kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e673-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="3e673-179">Adlı örnek bulut başlatma komut dosyasını `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="3e673-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="3e673-180">Çok hello hostname Hello ilk başlatılırken hello VM, bu bulut başlatma komut dosyasını ayarlar*myservername*.</span><span class="sxs-lookup"><span data-stu-id="3e673-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="3e673-181">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.</span><span class="sxs-lookup"><span data-stu-id="3e673-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="3e673-182">Oturum açma ve hello hello ana doğrulayın yeni VM.</span><span class="sxs-lookup"><span data-stu-id="3e673-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="3e673-183">Bir bulut init komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e673-183">Create a cloud-init script</span></span>
<span data-ttu-id="3e673-184">Güvenlik için Ubuntu VM tooupdate hello ilk önyüklemede istiyor.</span><span class="sxs-lookup"><span data-stu-id="3e673-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="3e673-185">Bulut init kullanarak hello ile Merhaba Linux dağıtım kullandığınıza bağlı olarak kod izleyin yapabiliriz.</span><span class="sxs-lookup"><span data-stu-id="3e673-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="3e673-186">Örnek bulut init betik `cloud_config_apt_upgrade.txt` hello Debian ailesi için</span><span class="sxs-lookup"><span data-stu-id="3e673-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="3e673-187">Linux önyüklendikten sonra tüm yüklü hello paketler aracılığıyla güncelleştirilir **get apt**.</span><span class="sxs-lookup"><span data-stu-id="3e673-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="3e673-188">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.</span><span class="sxs-lookup"><span data-stu-id="3e673-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="3e673-189">Oturum açma ve tüm paketler güncelleştirilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3e673-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="3e673-190">Bir kullanıcı tooLinux bulut init betik tooadd oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e673-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="3e673-191">Yeni bir Linux VM üzerinde hello ilk görevlerden biridir tooadd kendiniz veya tooavoid kullanmak için bir kullanıcı *kök*.</span><span class="sxs-lookup"><span data-stu-id="3e673-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="3e673-192">SSH anahtarları olan kullanılabilirlik ve güvenlik için en iyi uygulama ve toohello eklenen *~/.ssh/authorized_keys* bu bulut init komut dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="3e673-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="3e673-193">Örnek bulut init betik `cloud_config_add_users.txt` Debian ailesi için</span><span class="sxs-lookup"><span data-stu-id="3e673-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="3e673-194">Linux önyüklendikten sonra tüm listelenen hello oluşturulan ve eklenen toohello sudo Grup kullanıcılardır.</span><span class="sxs-lookup"><span data-stu-id="3e673-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="3e673-195">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) bulut init tooconfigure kullanarak, önyükleme sırasında.</span><span class="sxs-lookup"><span data-stu-id="3e673-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="3e673-196">Oturum açma ve yeni oluşturulan hello kullanıcı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3e673-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="3e673-197">Çıktı</span><span class="sxs-lookup"><span data-stu-id="3e673-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="3e673-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e673-198">Next steps</span></span>
<span data-ttu-id="3e673-199">Bulut init bir standart yol toomodify önyükleme, Linux VM'de durumundadır.</span><span class="sxs-lookup"><span data-stu-id="3e673-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="3e673-200">Ayrıca Azure toomodify izin VM uzantıları, LinuxVM önyükleme veya çalışırken sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3e673-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="3e673-201">Örneğin, Hello VM çalışırken hello Azure VMAccessExtension tooreset SSH veya kullanıcı bilgilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e673-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="3e673-202">Bulut başlatma ile bir yeniden başlatma tooreset hello parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e673-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="3e673-203">Sanal makine uzantıları ve özellikleri hakkında</span><span class="sxs-lookup"><span data-stu-id="3e673-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="3e673-204">Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler üzerinde onarım diskleri hello</span><span class="sxs-lookup"><span data-stu-id="3e673-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
