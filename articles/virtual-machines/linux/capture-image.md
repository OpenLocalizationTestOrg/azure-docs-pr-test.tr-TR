---
title: "CLI 2.0 kullanarak azure'da bir Linux VM bir görüntüsünü yakalama | Microsoft Docs"
description: "Azure CLI 2.0 kullanarak yığın dağıtımları için kullanmak üzere bir Azure VM görüntüsünü yakalayın."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 19b573f77f2ee84600955d00d30bdb16c84e3623
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="1f681-103">Bir sanal makine ya da VHD görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f681-103">How to create an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of the tutorial-->

<span data-ttu-id="1f681-104">Bir sanal makine Azure'da kullanmak için (VM) birden çok kopyasını oluşturmak için VM veya işletim sistemi VHD bir görüntüsünü yakalayın.</span><span class="sxs-lookup"><span data-stu-id="1f681-104">To create multiple copies of a virtual machine (VM) to use in Azure, capture an image of the VM or the OS VHD.</span></span> <span data-ttu-id="1f681-105">Bir görüntü oluşturmak için birden çok kez dağıtmak daha güvenli hale getiren kişisel hesap bilgileri kaldırmanız.</span><span class="sxs-lookup"><span data-stu-id="1f681-105">To create an image, you need remove personal account information which makes it safer to deploy multiple times.</span></span> <span data-ttu-id="1f681-106">Aşağıdaki adımlarda, mevcut bir VM'yi yetkisini kaldırma, ayırması ve görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1f681-106">In the following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="1f681-107">Bu görüntü, VM'ler aboneliğinizi içinde arasında herhangi bir kaynak grubu oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f681-107">You can use this image to create VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="1f681-108">İstiyorsanız, var olan bir Linux VM için yedekleme veya hata ayıklama, bir kopyasını oluşturun veya bir şirket içi VM özelleştirilmiş bir Linux VHD'den karşıya yükleme, bkz: [karşıya yükleme ve özel disk görüntüsünden bir Linux VM oluşturma](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="1f681-108">If you want to create a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="1f681-109">Aynı zamanda **Packer** özel yapılandırma oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1f681-109">You can also use **Packer** to create your custom configuration.</span></span> <span data-ttu-id="1f681-110">Packer kullanma hakkında daha fazla bilgi için bkz: [Packer Linux sanal makine görüntülerini oluşturmak için nasıl kullanılacağını](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="1f681-110">For more information on using Packer, see [How to use Packer to create Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="1f681-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1f681-111">Before you begin</span></span>
<span data-ttu-id="1f681-112">Aşağıdaki önkoşulları karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="1f681-112">Ensure that you meet the following prerequisites:</span></span>

* <span data-ttu-id="1f681-113">Azure yönetilen diskleri kullanılarak Resource Manager dağıtım modelinde oluşturulmuş VM'deki gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f681-113">You need an Azure VM created in the Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="1f681-114">Bir Linux VM oluşturmadıysanız, kullanabileceğiniz [portal](quick-create-portal.md), [Azure CLI](quick-create-cli.md), veya [Resource Manager şablonları](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="1f681-114">If you haven't created a Linux VM, you can use the [portal](quick-create-portal.md), the [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="1f681-115">VM gerektiği gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1f681-115">Configure the VM as needed.</span></span> <span data-ttu-id="1f681-116">Örneğin, [veri diski Ekle](add-disk.md)güncelleştirmeleri uygulamak ve uygulamaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1f681-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="1f681-117">Ayrıca son sahip olmanız gerekir [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmanız [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="1f681-117">You also need to have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1f681-118">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="1f681-118">Quick commands</span></span>

<span data-ttu-id="1f681-119">Değerlendirme veya azure'da VM öğrenmeye, test, bu konu, Basitleştirilmiş bir sürümünü için bkz: [Azure CLI kullanarak bir VM'nin özel bir görüntü oluşturun](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="1f681-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using the CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-the-vm"></a><span data-ttu-id="1f681-120">1. adım: VM yetkisini kaldırma</span><span class="sxs-lookup"><span data-stu-id="1f681-120">Step 1: Deprovision the VM</span></span>
<span data-ttu-id="1f681-121">Makine belirli dosyaları ve verileri silmek için Azure VM Aracısı'nı kullanarak VM'yi sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="1f681-121">You deprovision the VM, using the Azure VM agent, to delete machine specific files and data.</span></span> <span data-ttu-id="1f681-122">Kullanım `waagent` komutunu *-deprovision + kullanıcı* kaynağınız Linux VM parametresi.</span><span class="sxs-lookup"><span data-stu-id="1f681-122">Use the `waagent` command with the *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="1f681-123">Daha fazla bilgi için bkz: [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="1f681-123">For more information, see the [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="1f681-124">Bir SSH istemcisi kullanarak Linux VM'NİZDE bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1f681-124">Connect to your Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="1f681-125">SSH penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="1f681-125">In the SSH window, type the following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="1f681-126">Yalnızca resim olarak yakalamasına düşündüğünüz bir VM'de bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1f681-126">Only run this command on a VM that you intend to capture as an image.</span></span> <span data-ttu-id="1f681-127">Görüntü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtım için uygun garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="1f681-127">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="1f681-128">*+ Kullanıcı* parametresi son sağlanan kullanıcı hesabının da kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1f681-128">The *+user* parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="1f681-129">VM'yi hesap kimlik bilgilerini tutmak istiyorsanız, yalnızca kullanmak *-deprovision* kullanıcı hesabı bırakın için.</span><span class="sxs-lookup"><span data-stu-id="1f681-129">If you want to keep account credentials in the VM, just use *-deprovision* to leave the user account in place.</span></span>
 
3. <span data-ttu-id="1f681-130">Tür **y** devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="1f681-130">Type **y** to continue.</span></span> <span data-ttu-id="1f681-131">Ekleyebileceğiniz **-force** bu onay adım önlemek için parametre.</span><span class="sxs-lookup"><span data-stu-id="1f681-131">You can add the **-force** parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="1f681-132">Komut tamamlandığında yazın **çıkmak**.</span><span class="sxs-lookup"><span data-stu-id="1f681-132">After the command completes, type **exit**.</span></span> <span data-ttu-id="1f681-133">Bu adım, SSH istemcisi kapatır.</span><span class="sxs-lookup"><span data-stu-id="1f681-133">This step closes the SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="1f681-134">2. adım: VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f681-134">Step 2: Create VM image</span></span>
<span data-ttu-id="1f681-135">VM genelleştirilmiş olarak işaretler ve görüntü yakalamak için Azure CLI 2.0 kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f681-135">Use the Azure CLI 2.0 to mark the VM as generalized and capture the image.</span></span> <span data-ttu-id="1f681-136">Aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1f681-136">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1f681-137">Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="1f681-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="1f681-138">İle sağlaması kaldırılıyor. sağlaması VM serbest bırakma [az vm serbest bırakma](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="1f681-138">Deallocate the VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="1f681-139">Aşağıdaki örnek adlı VM kaldırır *myVM* kaynak grubunda adlı *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1f681-139">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="1f681-140">VM ile genelleştirilmiş olarak işaretle [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="1f681-140">Mark the VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="1f681-141">Aşağıdaki örnek işaretleri adlı VM *myVM* kaynak grubunda adlı *myResourceGroup* genelleştirilmiş olarak:</span><span class="sxs-lookup"><span data-stu-id="1f681-141">The following example marks the the VM named *myVM* in the resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="1f681-142">Şimdi ile VM kaynak görüntüsü oluşturma [az görüntü oluşturma](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="1f681-142">Now create an image of the VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="1f681-143">Aşağıdaki örnek adlı bir resim oluşturur *myImage* kaynak grubunda adlı *myResourceGroup* adlı VM kaynak kullanarak *myVM*:</span><span class="sxs-lookup"><span data-stu-id="1f681-143">The following example creates an image named *myImage* in the resource group named *myResourceGroup* using the VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="1f681-144">Görüntü, kaynak VM ile aynı kaynak grubunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1f681-144">The image is created in the same resource group as your source VM.</span></span> <span data-ttu-id="1f681-145">Bu görüntü aboneliğinizden içinde herhangi bir kaynak grubunda sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f681-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="1f681-146">Yönetim açısından bakıldığında, belirli bir kaynak grubunun VM kaynakları ve görüntüleri oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f681-146">From a management perspective, you may wish to create a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-the-captured-image"></a><span data-ttu-id="1f681-147">3. adım: yakalanan görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f681-147">Step 3: Create a VM from the captured image</span></span>
<span data-ttu-id="1f681-148">Oluşturduğunuz ile görüntü kullanarak bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="1f681-148">Create a VM using the image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="1f681-149">Aşağıdaki örnek, adlandırılmış bir VM'nin oluşturur *myVMDeployed* adlı görüntüden *myImage*:</span><span class="sxs-lookup"><span data-stu-id="1f681-149">The following example creates a VM named *myVMDeployed* from the image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-the-vm-in-another-resource-group"></a><span data-ttu-id="1f681-150">Başka bir kaynak grubunda VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="1f681-150">Creating the VM in another resource group</span></span> 

<span data-ttu-id="1f681-151">Aboneliğinizi içinde herhangi bir kaynak grubunda bir görüntüden sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f681-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="1f681-152">Farklı bir kaynak grubu görüntünün bir VM oluşturmak için görüntünüze tam kaynak kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="1f681-152">To create a VM in a different resource group than the image, specify the full resource ID to your image.</span></span> <span data-ttu-id="1f681-153">Kullanım [az resim listesi](/cli/azure/image#list) görüntüleri listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="1f681-153">Use [az image list](/cli/azure/image#list) to view a list of images.</span></span> <span data-ttu-id="1f681-154">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="1f681-154">The output is similar to the following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="1f681-155">Aşağıdaki örnek kullanır [az vm oluşturma](/cli/azure/vm#create) görüntü kaynak kimliği belirterek bir VM kaynak görüntü daha farklı bir kaynak grubu oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="1f681-155">The following example uses [az vm create](/cli/azure/vm#create) to create a VM in a different resource group than the source image by specifying the image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-the-deployment"></a><span data-ttu-id="1f681-156">4. adım: dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="1f681-156">Step 4: Verify the deployment</span></span>

<span data-ttu-id="1f681-157">Şimdi SSH dağıtım ve yeni VM kullanarak başlangıç doğrulamak için oluşturduğunuz sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="1f681-157">Now SSH to the virtual machine you created to verify the deployment and start using the new VM.</span></span> <span data-ttu-id="1f681-158">SSH bağlanmak için IP adresi veya FQDN ile VM Bul [az vm Göster](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="1f681-158">To connect via SSH, find the IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="1f681-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1f681-159">Next steps</span></span>
<span data-ttu-id="1f681-160">Kaynak VM görüntüden birden çok VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f681-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="1f681-161">Görüntüye değişiklik yapmanız gerekirse:</span><span class="sxs-lookup"><span data-stu-id="1f681-161">If you need to make changes to your image:</span></span> 

- <span data-ttu-id="1f681-162">Bir VM görüntünüze oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1f681-162">Create a VM from your image.</span></span>
- <span data-ttu-id="1f681-163">Tüm güncelleştirmeler veya yapılandırma değişikliklerini yapın.</span><span class="sxs-lookup"><span data-stu-id="1f681-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="1f681-164">Yeniden sağlamayı sonlandırın, serbest bırakma, generalize ve görüntü oluşturma adımlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f681-164">Follow the steps again to deprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="1f681-165">Bu yeni görüntüyü gelecekteki dağıtımlar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f681-165">Use this new image for future deployments.</span></span> <span data-ttu-id="1f681-166">İsterseniz, orijinal görüntüyü silin.</span><span class="sxs-lookup"><span data-stu-id="1f681-166">If desired, delete the original image.</span></span>

<span data-ttu-id="1f681-167">Vm'leriniz CLI ile yönetme ile ilgili daha fazla bilgi için bkz: [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f681-167">For more information on managing your VMs with the CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
