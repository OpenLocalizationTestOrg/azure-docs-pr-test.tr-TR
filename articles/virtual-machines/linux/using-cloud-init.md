---
title: "Bir Linux VM özelleştirmek için bulut init kullanın | Microsoft Docs"
description: "Azure CLI 2.0 ile oluşturma sırasında bir Linux VM özelleştirmek için bulut init kullanma"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="67d38-103">Bir Linux VM oluşturma sırasında özelleştirmek için bulut init kullanın</span><span class="sxs-lookup"><span data-stu-id="67d38-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="67d38-104">Bu makalede hostname ayarlamak, güncelleştirme yüklü paketleri ve Azure CLI 2.0 olan kullanıcı hesaplarını yönetmek için bir bulut init betik yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="67d38-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="67d38-105">Azure CLI üzerinden bir sanal makine (VM) oluşturduğunuzda, bulut Init komut adı verilir.</span><span class="sxs-lookup"><span data-stu-id="67d38-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="67d38-106">Daha ayrıntılı bir bakış uygulamaları yükleme hakkında bilgi için bkz: yapılandırma dosyaları yazma ve anahtar kasası, anahtarları injecting [Bu öğretici](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="67d38-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="67d38-107">Bu adımları [Azure CLI 1.0](using-cloud-init-nodejs.md) ile de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d38-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="67d38-108">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="67d38-108">Quick commands</span></span>
<span data-ttu-id="67d38-109">Ana bilgisayar adını ayarlar, tüm paketleri güncelleştirir ve bir sudo kullanıcı için Linux ekleyen bir bulut init.txt komut dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67d38-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="67d38-110">İçine VM'ler ile başlatmak için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="67d38-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="67d38-111">Aşağıdaki örnek adlı kaynak grubunu oluşturur *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="67d38-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="67d38-112">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) ile önyükleme sırasında yapılandırmak için bulut init kullanarak `--custom-data` parametresi.</span><span class="sxs-lookup"><span data-stu-id="67d38-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="67d38-113">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="67d38-113">Detailed walkthrough</span></span>
<span data-ttu-id="67d38-114">Yeni bir Linux VM başlattığında, özelleştirilmiş veya gereksinimleriniz için hazır herhangi bir şeyin standart bir Linux VM aldıklarından.</span><span class="sxs-lookup"><span data-stu-id="67d38-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="67d38-115">[Bulut init](https://cloudinit.readthedocs.org) için ilk kez önyükleme gibi bir komut dosyası veya yapılandırma ayarlarını, Linux VM içine eklemesine standart bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="67d38-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="67d38-116">Azure üzerinde olarak bir Linux VM üzerine değişiklik yapmak için birkaç farklı yolu vardır dağıtılan veya önyüklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="67d38-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="67d38-117">Bulut init kullanarak komut dosyalarını yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="67d38-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="67d38-118">Azure kullanarak komut dosyalarını Ekle [VMAccess uzantısını](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="67d38-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="67d38-119">Bulut init kullanarak bir Azure şablonu.</span><span class="sxs-lookup"><span data-stu-id="67d38-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="67d38-120">Bir Azure şablonu kullanarak [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="67d38-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="67d38-121">Komut dosyaları önyükleme sonra herhangi bir zamanda eklemesine:</span><span class="sxs-lookup"><span data-stu-id="67d38-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="67d38-122">SSH komutları doğrudan çalıştırmak için</span><span class="sxs-lookup"><span data-stu-id="67d38-122">SSH to run commands directly</span></span>
* <span data-ttu-id="67d38-123">Azure kullanarak komut dosyalarını Ekle [VMAccess uzantısını](using-vmaccess-extension.md), imperatively veya bir Azure şablonu</span><span class="sxs-lookup"><span data-stu-id="67d38-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="67d38-124">Yapılandırma yönetimi araçları Ansible, Salt, Chef, Puppet gibi ve.</span><span class="sxs-lookup"><span data-stu-id="67d38-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="67d38-125">Kök SSH kullanarak aynı şekilde gibi bir komut dosyası VMAccess uzantısını yürütür.</span><span class="sxs-lookup"><span data-stu-id="67d38-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="67d38-126">Ancak, VM uzantısını kullanarak çeşitli özellikler senaryonuza bağlı olarak yararlı olabilecek Azure sağladığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="67d38-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="67d38-127">Azure VM bulut init kullanılabilirliğine hızlı Oluştur görüntü diğer adları:</span><span class="sxs-lookup"><span data-stu-id="67d38-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="67d38-128">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="67d38-128">Alias</span></span> | <span data-ttu-id="67d38-129">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="67d38-129">Publisher</span></span> | <span data-ttu-id="67d38-130">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="67d38-130">Offer</span></span> | <span data-ttu-id="67d38-131">SKU</span><span class="sxs-lookup"><span data-stu-id="67d38-131">SKU</span></span> | <span data-ttu-id="67d38-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="67d38-132">Version</span></span> | <span data-ttu-id="67d38-133">Bulut başlatma</span><span class="sxs-lookup"><span data-stu-id="67d38-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="67d38-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="67d38-134">CentOS</span></span> |<span data-ttu-id="67d38-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="67d38-135">OpenLogic</span></span> |<span data-ttu-id="67d38-136">Centos</span><span class="sxs-lookup"><span data-stu-id="67d38-136">Centos</span></span> |<span data-ttu-id="67d38-137">7.2</span><span class="sxs-lookup"><span data-stu-id="67d38-137">7.2</span></span> |<span data-ttu-id="67d38-138">en son</span><span class="sxs-lookup"><span data-stu-id="67d38-138">latest</span></span> |<span data-ttu-id="67d38-139">Yok</span><span class="sxs-lookup"><span data-stu-id="67d38-139">no</span></span> |
| <span data-ttu-id="67d38-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="67d38-140">CoreOS</span></span> |<span data-ttu-id="67d38-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="67d38-141">CoreOS</span></span> |<span data-ttu-id="67d38-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="67d38-142">CoreOS</span></span> |<span data-ttu-id="67d38-143">Dengeli</span><span class="sxs-lookup"><span data-stu-id="67d38-143">Stable</span></span> |<span data-ttu-id="67d38-144">en son</span><span class="sxs-lookup"><span data-stu-id="67d38-144">latest</span></span> |<span data-ttu-id="67d38-145">Evet</span><span class="sxs-lookup"><span data-stu-id="67d38-145">yes</span></span> |
| <span data-ttu-id="67d38-146">Debian</span><span class="sxs-lookup"><span data-stu-id="67d38-146">Debian</span></span> |<span data-ttu-id="67d38-147">credativ</span><span class="sxs-lookup"><span data-stu-id="67d38-147">credativ</span></span> |<span data-ttu-id="67d38-148">Debian</span><span class="sxs-lookup"><span data-stu-id="67d38-148">Debian</span></span> |<span data-ttu-id="67d38-149">8</span><span class="sxs-lookup"><span data-stu-id="67d38-149">8</span></span> |<span data-ttu-id="67d38-150">en son</span><span class="sxs-lookup"><span data-stu-id="67d38-150">latest</span></span> |<span data-ttu-id="67d38-151">Yok</span><span class="sxs-lookup"><span data-stu-id="67d38-151">no</span></span> |
| <span data-ttu-id="67d38-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="67d38-152">openSUSE</span></span> |<span data-ttu-id="67d38-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="67d38-153">SUSE</span></span> |<span data-ttu-id="67d38-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="67d38-154">openSUSE</span></span> |<span data-ttu-id="67d38-155">13.2</span><span class="sxs-lookup"><span data-stu-id="67d38-155">13.2</span></span> |<span data-ttu-id="67d38-156">en son</span><span class="sxs-lookup"><span data-stu-id="67d38-156">latest</span></span> |<span data-ttu-id="67d38-157">Yok</span><span class="sxs-lookup"><span data-stu-id="67d38-157">no</span></span> |
| <span data-ttu-id="67d38-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="67d38-158">RHEL</span></span> |<span data-ttu-id="67d38-159">RedHat</span><span class="sxs-lookup"><span data-stu-id="67d38-159">Redhat</span></span> |<span data-ttu-id="67d38-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="67d38-160">RHEL</span></span> |<span data-ttu-id="67d38-161">7.2</span><span class="sxs-lookup"><span data-stu-id="67d38-161">7.2</span></span> |<span data-ttu-id="67d38-162">en son</span><span class="sxs-lookup"><span data-stu-id="67d38-162">latest</span></span> |<span data-ttu-id="67d38-163">Yok</span><span class="sxs-lookup"><span data-stu-id="67d38-163">no</span></span> |
| <span data-ttu-id="67d38-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="67d38-164">UbuntuLTS</span></span> |<span data-ttu-id="67d38-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="67d38-165">Canonical</span></span> |<span data-ttu-id="67d38-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="67d38-166">UbuntuServer</span></span> |<span data-ttu-id="67d38-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="67d38-167">14.04.4-LTS</span></span> |<span data-ttu-id="67d38-168">en son</span><span class="sxs-lookup"><span data-stu-id="67d38-168">latest</span></span> |<span data-ttu-id="67d38-169">Evet</span><span class="sxs-lookup"><span data-stu-id="67d38-169">yes</span></span> |

<span data-ttu-id="67d38-170">Bulut dahil ve Azure'a sağladıkları görüntülerinde çalışma başlatma almak için ortaklarımızın ile çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="67d38-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="67d38-171">Azure CLI ile VM oluşturmak için bir bulut init komut dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="67d38-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="67d38-172">Azure üzerinde bir VM oluştururken, bir bulut başlatma komut dosyasını başlatmak için Azure CLI kullanarak bulut init dosyasını belirtin `--custom-data` geçin.</span><span class="sxs-lookup"><span data-stu-id="67d38-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="67d38-173">İçine VM'ler ile başlatmak için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="67d38-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="67d38-174">Aşağıdaki örnek adlı kaynak grubunu oluşturur *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="67d38-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="67d38-175">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.</span><span class="sxs-lookup"><span data-stu-id="67d38-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="67d38-176">Bir Linux VM konak adı ayarlamak için bir bulut init komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d38-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="67d38-177">Tüm Linux VM için basit ve en önemli ayarlardan birini ana bilgisayar adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="67d38-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="67d38-178">Biz kolayca bu bulut init ile bu komut dosyası kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d38-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="67d38-179">Adlı örnek bulut başlatma komut dosyasını `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="67d38-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="67d38-180">VM ilk başlatma sırasında bu bulut init komut dosyası ana bilgisayar adını ayarlar *myservername*.</span><span class="sxs-lookup"><span data-stu-id="67d38-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="67d38-181">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.</span><span class="sxs-lookup"><span data-stu-id="67d38-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="67d38-182">Oturum açma ve ana bilgisayar yeni bir VM adını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="67d38-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="67d38-183">Bir bulut init komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d38-183">Create a cloud-init script</span></span>
<span data-ttu-id="67d38-184">Güvenlik için ilk önyüklemede güncelleştirmek için Ubuntu VM istiyor.</span><span class="sxs-lookup"><span data-stu-id="67d38-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="67d38-185">Bulut init, kullandığınız Linux dağıtım bağlı olarak izleme komut dosyalarıyla yapabiliriz kullanma.</span><span class="sxs-lookup"><span data-stu-id="67d38-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="67d38-186">Örnek bulut init betik `cloud_config_apt_upgrade.txt` Debian ailesi için</span><span class="sxs-lookup"><span data-stu-id="67d38-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="67d38-187">Linux önyüklendikten sonra yüklü olan paketlerin aracılığıyla güncelleştirilir **get apt**.</span><span class="sxs-lookup"><span data-stu-id="67d38-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="67d38-188">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.</span><span class="sxs-lookup"><span data-stu-id="67d38-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="67d38-189">Oturum açma ve tüm paketler güncelleştirilir doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="67d38-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="67d38-190">Linux için bir kullanıcı eklemek için bir bulut init komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d38-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="67d38-191">Yeni bir Linux VM ilk görevlerde biri kendiniz için bir kullanıcı eklemek veya kullanmaktan kaçınmak için *kök*.</span><span class="sxs-lookup"><span data-stu-id="67d38-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="67d38-192">SSH anahtarları olan kullanılabilirlik ve güvenlik için en iyi uygulama ve eklendikten *~/.ssh/authorized_keys* bu bulut init komut dosyasıyla.</span><span class="sxs-lookup"><span data-stu-id="67d38-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="67d38-193">Örnek bulut init betik `cloud_config_add_users.txt` Debian ailesi için</span><span class="sxs-lookup"><span data-stu-id="67d38-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="67d38-194">Linux önyüklendikten sonra listelenen tüm kullanıcılar oluşturulur ve sudo grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="67d38-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="67d38-195">Bir Linux VM oluşturma [az vm oluşturma](/cli/azure/vm#create) önyükleme sırasında yapılandırmak için bulut init kullanma.</span><span class="sxs-lookup"><span data-stu-id="67d38-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="67d38-196">Oturum açma ve yeni oluşturulan kullanıcı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="67d38-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="67d38-197">Çıktı</span><span class="sxs-lookup"><span data-stu-id="67d38-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="67d38-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67d38-198">Next steps</span></span>
<span data-ttu-id="67d38-199">Bulut init Linux VM'NİZDE önyüklemede değiştirmek için bir standart yolu durumundadır.</span><span class="sxs-lookup"><span data-stu-id="67d38-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="67d38-200">Ayrıca Azure önyükleme veya çalışırken, LinuxVM değiştirmenize izin VM uzantıları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="67d38-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="67d38-201">Örneğin, VM çalışırken SSH veya kullanıcı bilgilerini sıfırlama Azure VMAccessExtension kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d38-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="67d38-202">Bulut başlatma ile parolayı sıfırlamak için bir yeniden başlatma gerekir.</span><span class="sxs-lookup"><span data-stu-id="67d38-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="67d38-203">Sanal makine uzantıları ve özellikleri hakkında</span><span class="sxs-lookup"><span data-stu-id="67d38-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="67d38-204">Kullanıcılar, SSH ve onay yönetmek veya VMAccess uzantısını kullanarak Azure Linux VM'ler disklerde onarın</span><span class="sxs-lookup"><span data-stu-id="67d38-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)