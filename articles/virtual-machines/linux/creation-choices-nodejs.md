---
title: "Azure CLI 1.0 ile bir Linux VM oluşturmanın farklı yolları | Microsoft Docs"
description: "Azure üzerinde bir Linux sanal makine oluşturmanın farklı yollarını her bir yöntemin araç ve öğreticilerinin bağlantılarıyla birlikte listeler."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="67d67-103">Azure’da Linux sanal makine oluşturmanın farklı yolları</span><span class="sxs-lookup"><span data-stu-id="67d67-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="67d67-104">Azure’da size uygun araçları ve iş akışlarını kullanarak bir Linux sanal makine (VM) oluşturma esnekliğine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d67-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="67d67-105">Bu makalede bu farklılıklar ve Linux sanal makinelerinizi oluşturmaya yönelik örnekler özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="67d67-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="67d67-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67d67-106">Azure CLI</span></span>
<span data-ttu-id="67d67-107">Azure’da aşağıdaki CLI sürümlerinden birini kullanarak sanal makineler oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="67d67-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="67d67-108">Azure CLI 1.0: Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI’mız (bu makale)</span><span class="sxs-lookup"><span data-stu-id="67d67-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="67d67-109">[Azure CLI 2.0](../windows/creation-choices.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="67d67-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="67d67-110">Azure CLI 1.0 bir npm paketi, distro ile sağlanan paketler veya Docker kapsayıcısı üzerinden çeşitli platformlarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="67d67-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="67d67-111">[Azure CLI yükleme ve yapılandırma](../../cli-install-nodejs.md) hakkında daha fazla bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d67-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="67d67-112">Aşağıdaki öğretiler Azure CLI 1.0 kullanma ile ilgili örnekler sunar.</span><span class="sxs-lookup"><span data-stu-id="67d67-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="67d67-113">Gösterilen CLI hızlı başlatma komutlarına ilişkin daha fazla ayrıntı için her bir makaleyi okuyun:</span><span class="sxs-lookup"><span data-stu-id="67d67-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="67d67-114">Geliştirme ve test için Azure CLI üzerinden bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d67-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="67d67-115">Aşağıdaki örnek, adlandırılmış bir ortak anahtar kullanılarak CoreOS VM oluşturur *azure_id_rsa.pub*:</span><span class="sxs-lookup"><span data-stu-id="67d67-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="67d67-116">Bir Azure şablonu kullanarak güvenli bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d67-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="67d67-117">Aşağıdaki örnekte GitHub’a depolanmış bir şablon kullanılarak bir VM oluşturulmuştur:</span><span class="sxs-lookup"><span data-stu-id="67d67-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="67d67-118">Azure CLI kullanarak eksiksiz bir Linux ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d67-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="67d67-119">Bir yük dengeleyici ve kullanılabilirlik kümesi içinde birden fazla sanal makine oluşturmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="67d67-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="67d67-120">Linux VM’ye disk ekleme</span><span class="sxs-lookup"><span data-stu-id="67d67-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="67d67-121">Aşağıdaki örnek, bir *5* adlı mevcut bir VM'yi Gb diske *myVM*:</span><span class="sxs-lookup"><span data-stu-id="67d67-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="67d67-122">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="67d67-122">Azure portal</span></span>
<span data-ttu-id="67d67-123">[Azure portalı](https://portal.azure.com) sisteminize yüklenecek bir şey olmadığı için sanal makineyi hızlıca oluşturmanıza imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="67d67-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="67d67-124">VM oluşturmak için Azure portalını kullanma:</span><span class="sxs-lookup"><span data-stu-id="67d67-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="67d67-125">Azure portalını kullanarak Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d67-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="67d67-126">İşletim sistemi ve görüntü seçimi</span><span class="sxs-lookup"><span data-stu-id="67d67-126">Operating system and image choices</span></span>
<span data-ttu-id="67d67-127">Bir sanal makine oluşturulurken çalıştırmak istediğiniz işletim sistemini temel alan bir görüntü seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d67-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="67d67-128">Azure ve ortakları, bazıları önyüklü uygulamalar ve araçlarla gelen çok sayıda görüntü sağlar.</span><span class="sxs-lookup"><span data-stu-id="67d67-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="67d67-129">Veya kendi görüntülerinizden birini karşıya yükleyin ([aşağıdaki bölüme](#use-your-own-image) bakın).</span><span class="sxs-lookup"><span data-stu-id="67d67-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="67d67-130">Azure görüntüleri</span><span class="sxs-lookup"><span data-stu-id="67d67-130">Azure images</span></span>
<span data-ttu-id="67d67-131">Yayım, distro sürümü ve derlemelere göre kullanılabilen seçenekleri görmek için `azure vm image` CLI komutlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="67d67-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="67d67-132">Kullanılabilir yayımcıları aşağıdaki gibi listeleyin:</span><span class="sxs-lookup"><span data-stu-id="67d67-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="67d67-133">Belirli bir yayımcının kullanılabilir ürünlerini (teklifler) aşağıdaki gibi listeleyin:</span><span class="sxs-lookup"><span data-stu-id="67d67-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="67d67-134">Belirli bir teklif için kullanılabilir SKU’ları (distro sürümleri) aşağıdaki gibi listeleyin:</span><span class="sxs-lookup"><span data-stu-id="67d67-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="67d67-135">Belirli bir sürüm için kullanılabilir tüm görüntüleri aşağıdaki gibi listeleyin:</span><span class="sxs-lookup"><span data-stu-id="67d67-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="67d67-136">`azure vm quick-create` ve `azure vm create` komutları daha yaygın distro’lara ve en son sürümlerine hızlıca erişmek için kullanabileceğiniz bazı diğer adlara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="67d67-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="67d67-137">Diğer adların kullanılması yayımcı, teklif, SKU ve sürümün bir sanal makine oluşturulan her durumda belirtilmesinden çoğunlukla daha hızlıdır:</span><span class="sxs-lookup"><span data-stu-id="67d67-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="67d67-138">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="67d67-138">Alias</span></span> | <span data-ttu-id="67d67-139">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="67d67-139">Publisher</span></span> | <span data-ttu-id="67d67-140">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="67d67-140">Offer</span></span> | <span data-ttu-id="67d67-141">SKU</span><span class="sxs-lookup"><span data-stu-id="67d67-141">SKU</span></span> | <span data-ttu-id="67d67-142">Sürüm</span><span class="sxs-lookup"><span data-stu-id="67d67-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="67d67-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="67d67-143">CentOS</span></span> |<span data-ttu-id="67d67-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="67d67-144">OpenLogic</span></span> |<span data-ttu-id="67d67-145">Centos</span><span class="sxs-lookup"><span data-stu-id="67d67-145">Centos</span></span> |<span data-ttu-id="67d67-146">7.2</span><span class="sxs-lookup"><span data-stu-id="67d67-146">7.2</span></span> |<span data-ttu-id="67d67-147">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-147">latest</span></span> |
| <span data-ttu-id="67d67-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="67d67-148">CoreOS</span></span> |<span data-ttu-id="67d67-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="67d67-149">CoreOS</span></span> |<span data-ttu-id="67d67-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="67d67-150">CoreOS</span></span> |<span data-ttu-id="67d67-151">Dengeli</span><span class="sxs-lookup"><span data-stu-id="67d67-151">Stable</span></span> |<span data-ttu-id="67d67-152">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-152">latest</span></span> |
| <span data-ttu-id="67d67-153">Debian</span><span class="sxs-lookup"><span data-stu-id="67d67-153">Debian</span></span> |<span data-ttu-id="67d67-154">credativ</span><span class="sxs-lookup"><span data-stu-id="67d67-154">credativ</span></span> |<span data-ttu-id="67d67-155">Debian</span><span class="sxs-lookup"><span data-stu-id="67d67-155">Debian</span></span> |<span data-ttu-id="67d67-156">8</span><span class="sxs-lookup"><span data-stu-id="67d67-156">8</span></span> |<span data-ttu-id="67d67-157">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-157">latest</span></span> |
| <span data-ttu-id="67d67-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="67d67-158">openSUSE</span></span> |<span data-ttu-id="67d67-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="67d67-159">SUSE</span></span> |<span data-ttu-id="67d67-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="67d67-160">openSUSE</span></span> |<span data-ttu-id="67d67-161">13.2</span><span class="sxs-lookup"><span data-stu-id="67d67-161">13.2</span></span> |<span data-ttu-id="67d67-162">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-162">latest</span></span> |
| <span data-ttu-id="67d67-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="67d67-163">RHEL</span></span> |<span data-ttu-id="67d67-164">RedHat</span><span class="sxs-lookup"><span data-stu-id="67d67-164">Redhat</span></span> |<span data-ttu-id="67d67-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="67d67-165">RHEL</span></span> |<span data-ttu-id="67d67-166">7.2</span><span class="sxs-lookup"><span data-stu-id="67d67-166">7.2</span></span> |<span data-ttu-id="67d67-167">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-167">latest</span></span> |
| <span data-ttu-id="67d67-168">SLES</span><span class="sxs-lookup"><span data-stu-id="67d67-168">SLES</span></span> |<span data-ttu-id="67d67-169">SLES</span><span class="sxs-lookup"><span data-stu-id="67d67-169">SLES</span></span> |<span data-ttu-id="67d67-170">SLES</span><span class="sxs-lookup"><span data-stu-id="67d67-170">SLES</span></span> |<span data-ttu-id="67d67-171">12 SP1</span><span class="sxs-lookup"><span data-stu-id="67d67-171">12-SP1</span></span> |<span data-ttu-id="67d67-172">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-172">latest</span></span> |
| <span data-ttu-id="67d67-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="67d67-173">UbuntuLTS</span></span> |<span data-ttu-id="67d67-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="67d67-174">Canonical</span></span> |<span data-ttu-id="67d67-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="67d67-175">UbuntuServer</span></span> |<span data-ttu-id="67d67-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="67d67-176">14.04.4-LTS</span></span> |<span data-ttu-id="67d67-177">en son</span><span class="sxs-lookup"><span data-stu-id="67d67-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="67d67-178">Kendi görüntünüzü kullanma</span><span class="sxs-lookup"><span data-stu-id="67d67-178">Use your own image</span></span>
<span data-ttu-id="67d67-179">Belirli özelleştirmelere ihtiyaç duyuyorsanız, mevcut bir Azure VM’i temel alan bir görüntü kullanabilirsiniz, bunun için söz konusu VM’i *yakalayabilirsiniz*.</span><span class="sxs-lookup"><span data-stu-id="67d67-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="67d67-180">Şirket içinde oluşturduğunuz bir görüntüyü de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67d67-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="67d67-181">Desteklenen distro’lar ve kendi görüntünüzü kullanma ile ilgili daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="67d67-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="67d67-182">Azure destekli dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="67d67-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="67d67-183">Desteklenmeyen dağıtımlarla ilgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="67d67-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="67d67-184">Özel disk görüntüsünden Linux VM yükleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="67d67-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="67d67-185">[Linux sanal makinesini Resource Manager şablonu olarak yakalama](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="67d67-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="67d67-186">Var olan bir sanal makineyi yakalamaya yönelik hızlı başlangıç örnek komutları:</span><span class="sxs-lookup"><span data-stu-id="67d67-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="67d67-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67d67-187">Next steps</span></span>
* <span data-ttu-id="67d67-188">[CLI](quick-create-cli.md) ile [portal](quick-create-portal.md) üzerinden veya [Azure Resource Manager şablonu](../windows/cli-deploy-templates.md) kullanarak bir Linux VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67d67-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="67d67-189">Bir Linux VM oluşturduktan sonra [veri diski ekleyin](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="67d67-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="67d67-190">[Parola veya SSH anahtarlarını sıfırlama ve kullanıcıları yönetme](using-vmaccess-extension.md) ile ilgili hızlı adımlar</span><span class="sxs-lookup"><span data-stu-id="67d67-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

