---
title: "aaaDifferent yolları toocreate azure'da bir Linux VM | Microsoft Azure"
description: "Merhaba farklı şekillerde toocreate bağlantılar tootools ve her bir yöntemin öğreticiler dahil Microsoft Azure Linux sanal makinede öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a><span data-ttu-id="86924-103">Farklı şekillerde toocreate bir Linux VM</span><span class="sxs-lookup"><span data-stu-id="86924-103">Different ways toocreate a Linux VM</span></span>
<span data-ttu-id="86924-104">Bir Linux araçları ve iş akışları rahat tooyou kullanarak sanal makine (VM) içinde Azure toocreate hello esneklik sahip.</span><span class="sxs-lookup"><span data-stu-id="86924-104">You have hello flexibility in Azure toocreate a Linux virtual machine (VM) using tools and workflows comfortable tooyou.</span></span> <span data-ttu-id="86924-105">Bu makalede, bu farklar ve hello Azure CLI 2.0 dahil olmak üzere, Linux sanal makineleri oluşturmak için örnekler özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="86924-105">This article summarizes these differences and examples for creating your Linux VMs, including hello Azure CLI 2.0.</span></span> <span data-ttu-id="86924-106">Merhaba dahil olmak üzere oluşturma seçeneği de görüntüleyebilirsiniz [Azure CLI 1.0](creation-choices-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="86924-106">You can also view creation choices including hello [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="86924-107">Merhaba [Azure CLI 2.0](/cli/azure/install-az-cli2) bir npm paket, sağlanan distro paketleri ya da Docker kapsayıcısı platformlarda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86924-107">hello [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="86924-108">Ortamınız için en uygun yapı Hello yükleyin ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login)</span><span class="sxs-lookup"><span data-stu-id="86924-108">Install hello most appropriate build for your environment and log in tooan Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="86924-109">Azure CLI 2.0 hello ile bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="86924-109">Create a Linux VM with hello Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="86924-110">[az group create](/cli/azure/group#create) ile *myResourceGroup* adlı bir kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="86924-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="86924-111">Bir VM ile oluşturma [az vm oluşturma](/cli/azure/vm#create) adlı *myVM* kullanarak hello son *UbuntuLTS* görüntü ve bunlar zaten içinde yoksa, SSH anahtarları oluştur *~/.ssh*:</span><span class="sxs-lookup"><span data-stu-id="86924-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using hello latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="86924-112">Azure şablonu ile Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="86924-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="86924-113">Merhaba aşağıdaki örnek kullanır [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) toocreate GitHub üzerinde depolanan bir şablondan VM:</span><span class="sxs-lookup"><span data-stu-id="86924-113">hello following example uses [az group deployment create](/cli/azure/group/deployment#create) toocreate a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="86924-114">Linux VM oluşturma ve cloud-init ile özelleştirme</span><span class="sxs-lookup"><span data-stu-id="86924-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="86924-115">Birden fazla Linux VM üzerinde yük dengeli ve yüksek oranda kullanılabilir bir uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="86924-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="86924-116">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="86924-116">Azure portal</span></span>
<span data-ttu-id="86924-117">Merhaba [Azure portal](https://portal.azure.com) sağlar tooquickly olduğundan hiçbir şey bir VM oluşturun, sisteminizdeki tooinstall.</span><span class="sxs-lookup"><span data-stu-id="86924-117">hello [Azure portal](https://portal.azure.com) allows you tooquickly create a VM since there is nothing tooinstall on your system.</span></span> <span data-ttu-id="86924-118">Hello Azure portal toocreate hello VM kullanın:</span><span class="sxs-lookup"><span data-stu-id="86924-118">Use hello Azure portal toocreate hello VM:</span></span>

* [<span data-ttu-id="86924-119">Hello Azure portal kullanarak bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="86924-119">Create a Linux VM using hello Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="86924-120">İşletim sistemi ve görüntü seçimi</span><span class="sxs-lookup"><span data-stu-id="86924-120">Operating system and image choices</span></span>
<span data-ttu-id="86924-121">Bir VM oluştururken, işletim sistemi toorun istediğiniz hello üzerinde dayanan bir görüntü seçin.</span><span class="sxs-lookup"><span data-stu-id="86924-121">When creating a VM, you choose an image based on hello operating system you want toorun.</span></span> <span data-ttu-id="86924-122">Azure ve ortakları, bazıları önyüklü uygulamalar ve araçlarla gelen çok sayıda görüntü sağlar.</span><span class="sxs-lookup"><span data-stu-id="86924-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="86924-123">Veya, kendi görüntülerinizden birini karşıya yükleyin (bkz [hello bölümde](#use-your-own-image)).</span><span class="sxs-lookup"><span data-stu-id="86924-123">Or, upload one of your own images (see [hello following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="86924-124">Azure görüntüleri</span><span class="sxs-lookup"><span data-stu-id="86924-124">Azure images</span></span>
<span data-ttu-id="86924-125">Kullanım hello [az vm görüntüsü](/cli/azure/vm/image) toosee komutları, yayımcı, distro yayın ve derlemeleri tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="86924-125">Use hello [az vm image](/cli/azure/vm/image) commands toosee what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="86924-126">Kullanılabilir yayımcıların listesi:</span><span class="sxs-lookup"><span data-stu-id="86924-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="86924-127">Belirli bir yayımcının kullanılabilir ürünlerinin (teklifler) listesi:</span><span class="sxs-lookup"><span data-stu-id="86924-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="86924-128">Belirli bir teklif için kullanılabilir SKU’ların (distro sürümleri) listesi:</span><span class="sxs-lookup"><span data-stu-id="86924-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="86924-129">Belirli bir sürüm için kullanılabilir tüm görüntülerin listesi:</span><span class="sxs-lookup"><span data-stu-id="86924-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="86924-130">Gezinme ve geçerli görüntüleri kullanma hakkında daha fazla örnek için bkz: [erişin ve seçin hello Azure CLI ile Azure sanal makine görüntüleri](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="86924-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with hello Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="86924-131">Merhaba [az vm oluşturma](/cli/azure/vm#create) komutu sahip tooquickly erişim kullanabileceğiniz diğer adlar daha yaygın distro'lar ve bunların en son sürümleri hello.</span><span class="sxs-lookup"><span data-stu-id="86924-131">hello [az vm create](/cli/azure/vm#create) command has aliases you can use tooquickly access hello more common distros and their latest releases.</span></span> <span data-ttu-id="86924-132">Diğer adlar genellikle hello publisher, teklif, SKU ve sürümü her zaman bir VM oluşturma belirtmekten daha hızlı kullanmaktır:</span><span class="sxs-lookup"><span data-stu-id="86924-132">Using aliases is often quicker than specifying hello publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="86924-133">Diğer ad</span><span class="sxs-lookup"><span data-stu-id="86924-133">Alias</span></span> | <span data-ttu-id="86924-134">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="86924-134">Publisher</span></span> | <span data-ttu-id="86924-135">Sunduğu</span><span class="sxs-lookup"><span data-stu-id="86924-135">Offer</span></span> | <span data-ttu-id="86924-136">SKU</span><span class="sxs-lookup"><span data-stu-id="86924-136">SKU</span></span> | <span data-ttu-id="86924-137">Sürüm</span><span class="sxs-lookup"><span data-stu-id="86924-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="86924-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="86924-138">CentOS</span></span> |<span data-ttu-id="86924-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="86924-139">OpenLogic</span></span> |<span data-ttu-id="86924-140">Centos</span><span class="sxs-lookup"><span data-stu-id="86924-140">Centos</span></span> |<span data-ttu-id="86924-141">7.2</span><span class="sxs-lookup"><span data-stu-id="86924-141">7.2</span></span> |<span data-ttu-id="86924-142">en son</span><span class="sxs-lookup"><span data-stu-id="86924-142">latest</span></span> |
| <span data-ttu-id="86924-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="86924-143">CoreOS</span></span> |<span data-ttu-id="86924-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="86924-144">CoreOS</span></span> |<span data-ttu-id="86924-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="86924-145">CoreOS</span></span> |<span data-ttu-id="86924-146">Dengeli</span><span class="sxs-lookup"><span data-stu-id="86924-146">Stable</span></span> |<span data-ttu-id="86924-147">en son</span><span class="sxs-lookup"><span data-stu-id="86924-147">latest</span></span> |
| <span data-ttu-id="86924-148">Debian</span><span class="sxs-lookup"><span data-stu-id="86924-148">Debian</span></span> |<span data-ttu-id="86924-149">credativ</span><span class="sxs-lookup"><span data-stu-id="86924-149">credativ</span></span> |<span data-ttu-id="86924-150">Debian</span><span class="sxs-lookup"><span data-stu-id="86924-150">Debian</span></span> |<span data-ttu-id="86924-151">8</span><span class="sxs-lookup"><span data-stu-id="86924-151">8</span></span> |<span data-ttu-id="86924-152">en son</span><span class="sxs-lookup"><span data-stu-id="86924-152">latest</span></span> |
| <span data-ttu-id="86924-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="86924-153">openSUSE</span></span> |<span data-ttu-id="86924-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="86924-154">SUSE</span></span> |<span data-ttu-id="86924-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="86924-155">openSUSE</span></span> |<span data-ttu-id="86924-156">13.2</span><span class="sxs-lookup"><span data-stu-id="86924-156">13.2</span></span> |<span data-ttu-id="86924-157">en son</span><span class="sxs-lookup"><span data-stu-id="86924-157">latest</span></span> |
| <span data-ttu-id="86924-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="86924-158">RHEL</span></span> |<span data-ttu-id="86924-159">RedHat</span><span class="sxs-lookup"><span data-stu-id="86924-159">Redhat</span></span> |<span data-ttu-id="86924-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="86924-160">RHEL</span></span> |<span data-ttu-id="86924-161">7.2</span><span class="sxs-lookup"><span data-stu-id="86924-161">7.2</span></span> |<span data-ttu-id="86924-162">en son</span><span class="sxs-lookup"><span data-stu-id="86924-162">latest</span></span> |
| <span data-ttu-id="86924-163">SLES</span><span class="sxs-lookup"><span data-stu-id="86924-163">SLES</span></span> |<span data-ttu-id="86924-164">SLES</span><span class="sxs-lookup"><span data-stu-id="86924-164">SLES</span></span> |<span data-ttu-id="86924-165">SLES</span><span class="sxs-lookup"><span data-stu-id="86924-165">SLES</span></span> |<span data-ttu-id="86924-166">12 SP1</span><span class="sxs-lookup"><span data-stu-id="86924-166">12-SP1</span></span> |<span data-ttu-id="86924-167">en son</span><span class="sxs-lookup"><span data-stu-id="86924-167">latest</span></span> |
| <span data-ttu-id="86924-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="86924-168">UbuntuLTS</span></span> |<span data-ttu-id="86924-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="86924-169">Canonical</span></span> |<span data-ttu-id="86924-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="86924-170">UbuntuServer</span></span> |<span data-ttu-id="86924-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="86924-171">14.04.4-LTS</span></span> |<span data-ttu-id="86924-172">en son</span><span class="sxs-lookup"><span data-stu-id="86924-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="86924-173">Kendi görüntünüzü kullanma</span><span class="sxs-lookup"><span data-stu-id="86924-173">Use your own image</span></span>
<span data-ttu-id="86924-174">Belirli özelleştirmelere ihtiyaç duyuyorsanız, mevcut bir Azure VM’yi yakalayarak bu VM’yi temel alan bir görüntü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86924-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="86924-175">Şirket içinde oluşturduğunuz bir görüntüyü de yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86924-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="86924-176">Desteklenen distro'lar hakkında daha fazla bilgi ve nasıl toouse kendi görüntüleri görmek hello makaleler:</span><span class="sxs-lookup"><span data-stu-id="86924-176">For more information on supported distros and how toouse your own images, see hello following articles:</span></span>

* [<span data-ttu-id="86924-177">Azure destekli dağıtımlar</span><span class="sxs-lookup"><span data-stu-id="86924-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="86924-178">Desteklenmeyen dağıtımlarla ilgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="86924-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="86924-179">[Nasıl toocreate mevcut bir Azure VM'i görüntüden](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="86924-179">[How toocreate an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="86924-180">Hızlı Başlangıç örnek toocreate mevcut bir Azure VM'i görüntüden komutlar:</span><span class="sxs-lookup"><span data-stu-id="86924-180">Quick-start example commands toocreate an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="86924-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86924-181">Next steps</span></span>
* <span data-ttu-id="86924-182">Merhaba ile bir Linux VM oluşturma [CLI](quick-create-cli.md), hello gelen [portal](quick-create-portal.md), veya kullanarak bir [Azure Resource Manager şablonu](../windows/cli-deploy-templates.md).</span><span class="sxs-lookup"><span data-stu-id="86924-182">Create a Linux VM with hello [CLI](quick-create-cli.md), from hello [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="86924-183">Linux VM oluşturduktan sonra [Azure diskleri ve depolama hakkında bilgi edinin](tutorial-manage-disks.md).</span><span class="sxs-lookup"><span data-stu-id="86924-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="86924-184">Hızlı adımlar çok[bir parola veya SSH anahtarlarını sıfırlama ve kullanıcıları yönetme](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="86924-184">Quick steps too[reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
