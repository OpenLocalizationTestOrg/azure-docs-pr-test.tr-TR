---
title: "Azure CLI 1.0 Kullanarak Linux VM Oluşturma | Microsoft Docs"
description: "Azure CLI 1.0 kullanarak Azure'da Linux VM'si oluşturma"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="99068-103">Azure CLI 1.0 kullanarak bir Linux VM'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="99068-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="99068-104">Bu makalede, Azure komut satırı arabiriminde (CLI) `azure vm quick-create` komutunu kullanarak Azure'da bir Linux sanal makinesini (VM) hızlı bir şekilde nasıl dağıtacağınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="99068-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="99068-105">`quick-create` komutu, bir kavramı hızlıca prototipleştirmek veya sınamak için kullanabileceğiniz temel, güvenli bir altyapı içine VM dağıtır.</span><span class="sxs-lookup"><span data-stu-id="99068-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="99068-106">Azure CLI 2.0 sürümünü kullanarak VM oluşturmak için bkz. [Azure CLI ile VM oluşturma](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99068-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="99068-107">[Azure portalını](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) kullanarak da hızlıca bir Linux VM'si dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99068-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="99068-108">Makaleyi gerektiren bir [SSH ortak ve özel anahtar dosyaları](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="99068-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="99068-109">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="99068-109">Quick commands</span></span>

<span data-ttu-id="99068-110">Aşağıdaki örnekte, bir CoreOS VM'sinin nasıl dağıtılacağı ve Secure Shell (SSH) anahtarının nasıl ekleneceği gösterilmektedir. (Bağımsız değişkenleriniz farklı olabilir):</span><span class="sxs-lookup"><span data-stu-id="99068-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="99068-111">Ayrıntılı kılavuz</span><span class="sxs-lookup"><span data-stu-id="99068-111">Detailed walkthrough</span></span>

<span data-ttu-id="99068-112">Aşağıdaki kılavuzda bir UbuntuLTS sanal makinesinin dağıtımı, her adımın sonuçlarına ilişkin açıklamalarla birlikte adım adım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="99068-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="99068-113">VM hızlı oluşturma diğer adları</span><span class="sxs-lookup"><span data-stu-id="99068-113">VM quick-create aliases</span></span>

<span data-ttu-id="99068-114">En yaygın işletim sistemi dağıtımlarıyla eşlenmiş Azure CLI'si diğer adlarını kullanmak, dağıtım seçmenin hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="99068-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="99068-115">Aşağıdaki tabloda diğer adlar listelenmektedir (Azure CLI'sinin 0.10 sürümünden itibaren).</span><span class="sxs-lookup"><span data-stu-id="99068-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="99068-116">`quick-create` kullanan tüm dağıtımlar, daha hızlı sağlama ve daha yüksek performanslı disk erişimi sunan katı hal sürücüsü (SSD) tarafından desteklenen VM'leri varsayılan olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="99068-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="99068-117">(Bu diğer adlar, Azure'da bulunan dağıtımların çok küçük bir bölümünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="99068-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="99068-118">[PowerShell’de](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ya da [web üzerinde](https://azure.microsoft.com/marketplace/virtual-machines/) görüntü arayarak Azure Marketi'nde daha fazla görüntü bulun veya [kendi özel görüntünüzü karşıya yükleyin](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="99068-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="99068-119">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="99068-119">Alias</span></span> | <span data-ttu-id="99068-120">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="99068-120">Publisher</span></span> | <span data-ttu-id="99068-121">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="99068-121">Offer</span></span> | <span data-ttu-id="99068-122">SKU</span><span class="sxs-lookup"><span data-stu-id="99068-122">SKU</span></span> | <span data-ttu-id="99068-123">Sürüm</span><span class="sxs-lookup"><span data-stu-id="99068-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="99068-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="99068-124">CentOS</span></span> |<span data-ttu-id="99068-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="99068-125">OpenLogic</span></span> |<span data-ttu-id="99068-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="99068-126">CentOS</span></span> |<span data-ttu-id="99068-127">7.2</span><span class="sxs-lookup"><span data-stu-id="99068-127">7.2</span></span> |<span data-ttu-id="99068-128">en son</span><span class="sxs-lookup"><span data-stu-id="99068-128">latest</span></span> |
| <span data-ttu-id="99068-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="99068-129">CoreOS</span></span> |<span data-ttu-id="99068-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="99068-130">CoreOS</span></span> |<span data-ttu-id="99068-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="99068-131">CoreOS</span></span> |<span data-ttu-id="99068-132">Dengeli</span><span class="sxs-lookup"><span data-stu-id="99068-132">Stable</span></span> |<span data-ttu-id="99068-133">en son</span><span class="sxs-lookup"><span data-stu-id="99068-133">latest</span></span> |
| <span data-ttu-id="99068-134">Debian</span><span class="sxs-lookup"><span data-stu-id="99068-134">Debian</span></span> |<span data-ttu-id="99068-135">credativ</span><span class="sxs-lookup"><span data-stu-id="99068-135">credativ</span></span> |<span data-ttu-id="99068-136">Debian</span><span class="sxs-lookup"><span data-stu-id="99068-136">Debian</span></span> |<span data-ttu-id="99068-137">8</span><span class="sxs-lookup"><span data-stu-id="99068-137">8</span></span> |<span data-ttu-id="99068-138">en son</span><span class="sxs-lookup"><span data-stu-id="99068-138">latest</span></span> |
| <span data-ttu-id="99068-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="99068-139">openSUSE</span></span> |<span data-ttu-id="99068-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="99068-140">SUSE</span></span> |<span data-ttu-id="99068-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="99068-141">openSUSE</span></span> |<span data-ttu-id="99068-142">13.2</span><span class="sxs-lookup"><span data-stu-id="99068-142">13.2</span></span> |<span data-ttu-id="99068-143">en son</span><span class="sxs-lookup"><span data-stu-id="99068-143">latest</span></span> |
| <span data-ttu-id="99068-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="99068-144">RHEL</span></span> |<span data-ttu-id="99068-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="99068-145">Red Hat</span></span> |<span data-ttu-id="99068-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="99068-146">RHEL</span></span> |<span data-ttu-id="99068-147">7.2</span><span class="sxs-lookup"><span data-stu-id="99068-147">7.2</span></span> |<span data-ttu-id="99068-148">en son</span><span class="sxs-lookup"><span data-stu-id="99068-148">latest</span></span> |
| <span data-ttu-id="99068-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="99068-149">UbuntuLTS</span></span> |<span data-ttu-id="99068-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="99068-150">Canonical</span></span> |<span data-ttu-id="99068-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="99068-151">Ubuntu Server</span></span> |<span data-ttu-id="99068-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="99068-152">14.04.4-LTS</span></span> |<span data-ttu-id="99068-153">en son</span><span class="sxs-lookup"><span data-stu-id="99068-153">latest</span></span> |

<span data-ttu-id="99068-154">Aşağıdaki bölümlerde, Ubuntu 14.04.4 LTS Server'ı dağıtmak üzere **ImageURN** seçeneği (`-Q`) için `UbuntuLTS` diğer adı kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="99068-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="99068-155">Önceki `quick-create` örneğinde, SSH parolaları devre dışı bırakılarak karşıya yüklenecek SSH ortak anahtarını tanımlamak üzere yalnızca `-M` bayrağı çağrılmıştır, bu nedenle sizden aşağıdaki bağımsız değişkenler istenir:</span><span class="sxs-lookup"><span data-stu-id="99068-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="99068-156">kaynak grup adı (ilk Azure kaynak grubunuz için genellikle herhangi bir dize olabilir)</span><span class="sxs-lookup"><span data-stu-id="99068-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="99068-157">VM adı</span><span class="sxs-lookup"><span data-stu-id="99068-157">VM name</span></span>
* <span data-ttu-id="99068-158">konum (`westus` veya `westeurope` iyi varsayılanlardır)</span><span class="sxs-lookup"><span data-stu-id="99068-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="99068-159">linux (Azure'ın hangi işletim sistemini istediğinizi bilmesi için)</span><span class="sxs-lookup"><span data-stu-id="99068-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="99068-160">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="99068-160">username</span></span>

<span data-ttu-id="99068-161">Daha fazla istemin gerekli olmaması için aşağıdaki örnekte tüm değerler belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="99068-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="99068-162">ssh-rsa biçiminde ortak anahtar dosyası olarak `~/.ssh/id_rsa.pub` dosyanız olduğu sürece bu dosyayı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="99068-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="99068-163">Çıktı aşağıdaki çıktı bloğu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="99068-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="99068-164">Yeni sanal makinede oturum açma</span><span class="sxs-lookup"><span data-stu-id="99068-164">Log in to the new VM</span></span>
<span data-ttu-id="99068-165">Çıktıda listelenen genel IP adresini kullanarak VM'inizde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99068-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="99068-166">Listelenen tam etki alanı adını (FQDN) da kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="99068-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="99068-167">Oturum açma işlemi aşağıdaki çıktı bloğuna benzer şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="99068-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="99068-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99068-168">Next steps</span></span>
<span data-ttu-id="99068-169">`azure vm quick-create` komutu, bir Bash kabuğunda oturum açıp çalışmaya başlamanız için VM dağıtmanın hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="99068-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="99068-170">Ancak `vm quick-create` kullanarak kapsamlı bir denetim gerçekleştiremez ve daha karmaşık bir ortam oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="99068-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="99068-171">Altyapınız için özelleştirilmiş bir Linux VM'si dağıtmak üzere şu makalelerden herhangi birine bakın:</span><span class="sxs-lookup"><span data-stu-id="99068-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="99068-172">Azure CLI'si komutlarını doğrudan kullanarak bir Linux VM'si için kendi özel ortamınızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="99068-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="99068-173">Şablonları kullanarak Azure'da SSH Secure ile Güvenliği Sağlanmış Linux VM'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="99068-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="99068-174">[Docker konağı olarak hızlı şekilde bir Linux VM'si oluşturmak için çeşitli komutlara sahip `docker-machine` Azure sürücüsünü](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99068-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
