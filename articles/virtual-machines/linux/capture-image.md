---
title: "aaaCapture CLI 2.0 kullanarak azure'da bir Linux VM görüntüsünü | Microsoft Docs"
description: "Bir Azure VM toouse hello Azure CLI 2.0 kullanarak yığın dağıtımları için bir görüntüsünü yakalayın."
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
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a><span data-ttu-id="591bf-103">Nasıl toocreate bir sanal makine ya da VHD görüntüsü</span><span class="sxs-lookup"><span data-stu-id="591bf-103">How toocreate an image of a virtual machine or VHD</span></span>

<!-- generalize, image - extended version of hello tutorial-->

<span data-ttu-id="591bf-104">toocreate, azure'da sanal makine (VM) toouse birden çok kopyasını hello VM görüntüsünü yakalama ya da OS VHD hello.</span><span class="sxs-lookup"><span data-stu-id="591bf-104">toocreate multiple copies of a virtual machine (VM) toouse in Azure, capture an image of hello VM or hello OS VHD.</span></span> <span data-ttu-id="591bf-105">toocreate bir görüntü, birden çok kez daha güvenli toodeploy kolaylaşır kişisel hesap bilgilerini kaldır.</span><span class="sxs-lookup"><span data-stu-id="591bf-105">toocreate an image, you need remove personal account information which makes it safer toodeploy multiple times.</span></span> <span data-ttu-id="591bf-106">Merhaba, mevcut bir VM'yi yetkisini kaldırma adımları izleyerek ayırması ve bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="591bf-106">In hello following steps you deprovision an existing VM, deallocate and create an image.</span></span> <span data-ttu-id="591bf-107">Aboneliğinizi içinde herhangi bir kaynak grubu boyunca bu görüntü toocreate VM'ler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="591bf-107">You can use this image toocreate VMs across any resource group within your subscription.</span></span>

<span data-ttu-id="591bf-108">Yedekleme veya hata ayıklama için toocreate, varolan bir Linux VM kopyasını istediğiniz veya bir şirket içi VM özelleştirilmiş bir Linux VHD'den karşıya yükleme, bkz: [karşıya yükleme ve özel disk görüntüsünden bir Linux VM oluşturma](upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="591bf-108">If you want toocreate a copy of your existing Linux VM for backup or debugging, or upload a specialized Linux VHD from an on-premises VM, see [Upload and create a Linux VM from custom disk image](upload-vhd.md).</span></span>  

<span data-ttu-id="591bf-109">Aynı zamanda **Packer** toocreate özel yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="591bf-109">You can also use **Packer** toocreate your custom configuration.</span></span> <span data-ttu-id="591bf-110">Packer kullanma hakkında daha fazla bilgi için bkz: [nasıl Azure'da toouse Packer toocreate Linux sanal makine görüntüleri](build-image-with-packer.md).</span><span class="sxs-lookup"><span data-stu-id="591bf-110">For more information on using Packer, see [How toouse Packer toocreate Linux virtual machine images in Azure](build-image-with-packer.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="591bf-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="591bf-111">Before you begin</span></span>
<span data-ttu-id="591bf-112">Hello aşağıdaki önkoşulları karşıladığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="591bf-112">Ensure that you meet hello following prerequisites:</span></span>

* <span data-ttu-id="591bf-113">Azure yönetilen diskleri kullanarak hello Resource Manager dağıtım modelinde oluşturulmuş VM'deki gerekir.</span><span class="sxs-lookup"><span data-stu-id="591bf-113">You need an Azure VM created in hello Resource Manager deployment model using managed disks.</span></span> <span data-ttu-id="591bf-114">Bir Linux VM oluşturmadıysanız, hello kullanabilirsiniz [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), veya [Resource Manager şablonları](create-ssh-secured-vm-from-template.md).</span><span class="sxs-lookup"><span data-stu-id="591bf-114">If you haven't created a Linux VM, you can use hello [portal](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), or [Resource Manager templates](create-ssh-secured-vm-from-template.md).</span></span> <span data-ttu-id="591bf-115">Merhaba gerektiği gibi VM yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="591bf-115">Configure hello VM as needed.</span></span> <span data-ttu-id="591bf-116">Örneğin, [veri diski Ekle](add-disk.md)güncelleştirmeleri uygulamak ve uygulamaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="591bf-116">For example, [add data disks](add-disk.md), apply updates, and install applications.</span></span> 

* <span data-ttu-id="591bf-117">Ayrıca toohave hello son gerekir [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="591bf-117">You also need toohave hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and be logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="591bf-118">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="591bf-118">Quick commands</span></span>

<span data-ttu-id="591bf-119">Değerlendirme veya azure'da VM öğrenmeye, test, bu konu, Basitleştirilmiş bir sürümünü için bkz: [hello CLI kullanarak bir Azure VM özel bir görüntü oluşturun](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="591bf-119">For a simplified version of this topic, for testing, evaluating or learning about VMs in Azure, see [Create a custom image of an Azure VM using hello CLI](tutorial-custom-images.md).</span></span>


## <a name="step-1-deprovision-hello-vm"></a><span data-ttu-id="591bf-120">1. adım: Deprovision hello VM</span><span class="sxs-lookup"><span data-stu-id="591bf-120">Step 1: Deprovision hello VM</span></span>
<span data-ttu-id="591bf-121">Merhaba hello Azure VM Aracısı, toodelete makine belirli dosyaları ve verileri kullanarak VM sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="591bf-121">You deprovision hello VM, using hello Azure VM agent, toodelete machine specific files and data.</span></span> <span data-ttu-id="591bf-122">Kullanım hello `waagent` hello komutunu *-deprovision + kullanıcı* kaynağınız Linux VM parametresi.</span><span class="sxs-lookup"><span data-stu-id="591bf-122">Use hello `waagent` command with hello *-deprovision+user* parameter on your source Linux VM.</span></span> <span data-ttu-id="591bf-123">Daha fazla bilgi için bkz: Merhaba [Azure Linux Aracısı Kullanıcı Kılavuzu](../windows/agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="591bf-123">For more information, see hello [Azure Linux Agent user guide](../windows/agent-user-guide.md).</span></span>

1. <span data-ttu-id="591bf-124">Bir SSH istemcisi kullanarak Linux VM tooyour bağlayın.</span><span class="sxs-lookup"><span data-stu-id="591bf-124">Connect tooyour Linux VM using an SSH client.</span></span>
2. <span data-ttu-id="591bf-125">Merhaba SSH penceresinde hello aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="591bf-125">In hello SSH window, type hello following command:</span></span>
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > <span data-ttu-id="591bf-126">Yalnızca bir görüntü olarak toocapture düşündüğünüz bu komutu bir VM üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="591bf-126">Only run this command on a VM that you intend toocapture as an image.</span></span> <span data-ttu-id="591bf-127">Bu hello görüntüyü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtım için uygun garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="591bf-127">It does not guarantee that hello image is cleared of all sensitive information or is suitable for redistribution.</span></span> <span data-ttu-id="591bf-128">Merhaba *+ kullanıcı* parametresi hello son sağlanan kullanıcı hesabının da kaldırır.</span><span class="sxs-lookup"><span data-stu-id="591bf-128">hello *+user* parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="591bf-129">Merhaba VM tookeep hesabı kimlik bilgilerini istiyorsanız, yalnızca kullanın *-deprovision* yerinde tooleave hello kullanıcı hesabı.</span><span class="sxs-lookup"><span data-stu-id="591bf-129">If you want tookeep account credentials in hello VM, just use *-deprovision* tooleave hello user account in place.</span></span>
 
3. <span data-ttu-id="591bf-130">Tür **y** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="591bf-130">Type **y** toocontinue.</span></span> <span data-ttu-id="591bf-131">Merhaba ekleyebilirsiniz **-force** parametresi tooavoid bu onay adımı.</span><span class="sxs-lookup"><span data-stu-id="591bf-131">You can add hello **-force** parameter tooavoid this confirmation step.</span></span>
4. <span data-ttu-id="591bf-132">Merhaba komut tamamlandıktan sonra yazın **çıkmak**.</span><span class="sxs-lookup"><span data-stu-id="591bf-132">After hello command completes, type **exit**.</span></span> <span data-ttu-id="591bf-133">Bu adım hello SSH istemcisi kapatır.</span><span class="sxs-lookup"><span data-stu-id="591bf-133">This step closes hello SSH client.</span></span>

## <a name="step-2-create-vm-image"></a><span data-ttu-id="591bf-134">2. adım: VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="591bf-134">Step 2: Create VM image</span></span>
<span data-ttu-id="591bf-135">Merhaba görüntüsünü yakalamak ve Hello Azure CLI 2.0 toomark hello VM genelleştirilmiş olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="591bf-135">Use hello Azure CLI 2.0 toomark hello VM as generalized and capture hello image.</span></span> <span data-ttu-id="591bf-136">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="591bf-136">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="591bf-137">Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="591bf-137">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

1. <span data-ttu-id="591bf-138">Merhaba, ile sağlaması kaldırılıyor. sağlaması VM serbest bırakma [az vm serbest bırakma](/cli//azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="591bf-138">Deallocate hello VM that you deprovisioned with [az vm deallocate](/cli//azure/vm#deallocate).</span></span> <span data-ttu-id="591bf-139">Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="591bf-139">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. <span data-ttu-id="591bf-140">İşareti hello ile genelleştirilmiş gibi VM [az vm generalize](/cli//azure/vm#generalize).</span><span class="sxs-lookup"><span data-stu-id="591bf-140">Mark hello VM as generalized with [az vm generalize](/cli//azure/vm#generalize).</span></span> <span data-ttu-id="591bf-141">Örnek işaretleri hello hello VM adlı Hello *myVM* adlı hello kaynak grubunda *myResourceGroup* genelleştirilmiş olarak:</span><span class="sxs-lookup"><span data-stu-id="591bf-141">hello following example marks hello hello VM named *myVM* in hello resource group named *myResourceGroup* as generalized:</span></span>
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. <span data-ttu-id="591bf-142">Şimdi hello VM kaynakla görüntüsünü oluşturmak [az görüntü oluşturma](/cli//azure/image#create).</span><span class="sxs-lookup"><span data-stu-id="591bf-142">Now create an image of hello VM resource with [az image create](/cli//azure/image#create).</span></span> <span data-ttu-id="591bf-143">Merhaba aşağıdaki örnekte oluşturur adlı bir resim *myImage* adlı hello kaynak grubunda *myResourceGroup* adlı hello VM kaynağı kullanarak *myVM*:</span><span class="sxs-lookup"><span data-stu-id="591bf-143">hello following example creates an image named *myImage* in hello resource group named *myResourceGroup* using hello VM resource named *myVM*:</span></span>
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > <span data-ttu-id="591bf-144">Merhaba görüntüsü hello aynı oluşturulur kaynağınız VM kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="591bf-144">hello image is created in hello same resource group as your source VM.</span></span> <span data-ttu-id="591bf-145">Bu görüntü aboneliğinizden içinde herhangi bir kaynak grubunda sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="591bf-145">You can create VMs in any resource group within your subscription from this image.</span></span> <span data-ttu-id="591bf-146">Yönetim açısından bakıldığında, belirli bir kaynak grubunun VM kaynakları ve görüntüleri için toocreate isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="591bf-146">From a management perspective, you may wish toocreate a specific resource group for your VM resources and images.</span></span>

## <a name="step-3-create-a-vm-from-hello-captured-image"></a><span data-ttu-id="591bf-147">3. adım: hello yakalanan görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="591bf-147">Step 3: Create a VM from hello captured image</span></span>
<span data-ttu-id="591bf-148">Oluşturduğunuz hello görüntü kullanarak bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="591bf-148">Create a VM using hello image you created with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="591bf-149">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMDeployed* adlı hello görüntüden *myImage*:</span><span class="sxs-lookup"><span data-stu-id="591bf-149">hello following example creates a VM named *myVMDeployed* from hello image named *myImage*:</span></span>

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a><span data-ttu-id="591bf-150">Başka bir kaynak grubunda Hello VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="591bf-150">Creating hello VM in another resource group</span></span> 

<span data-ttu-id="591bf-151">Aboneliğinizi içinde herhangi bir kaynak grubunda bir görüntüden sanal makineleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="591bf-151">You can create VMs from an image in any resource group within your subscription.</span></span> <span data-ttu-id="591bf-152">toocreate farklı bir kaynak grubu hello Görüntü'den bir VM'de hello tam kaynak kimliği tooyour görüntüsünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="591bf-152">toocreate a VM in a different resource group than hello image, specify hello full resource ID tooyour image.</span></span> <span data-ttu-id="591bf-153">Kullanım [az resim listesi](/cli/azure/image#list) tooview bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="591bf-153">Use [az image list](/cli/azure/image#list) tooview a list of images.</span></span> <span data-ttu-id="591bf-154">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="591bf-154">hello output is similar toohello following example:</span></span>

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

<span data-ttu-id="591bf-155">Merhaba aşağıdaki örnek kullanır [az vm oluşturma](/cli/azure/vm#create) toocreate VM hello görüntü kaynak kimliği belirterek hello kaynak görüntüsü daha farklı bir kaynak grubunda:</span><span class="sxs-lookup"><span data-stu-id="591bf-155">hello following example uses [az vm create](/cli/azure/vm#create) toocreate a VM in a different resource group than hello source image by specifying hello image resource ID:</span></span>

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a><span data-ttu-id="591bf-156">Adım 4: hello dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="591bf-156">Step 4: Verify hello deployment</span></span>

<span data-ttu-id="591bf-157">Şimdi SSH toohello, tooverify hello dağıtım ve başlangıç kullanılarak oluşturulan sanal makinenin yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="591bf-157">Now SSH toohello virtual machine you created tooverify hello deployment and start using hello new VM.</span></span> <span data-ttu-id="591bf-158">SSH, aracılığıyla tooconnect Bul hello IP adresi veya FQDN ile vm'nizin [az vm Göster](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="591bf-158">tooconnect via SSH, find hello IP address or FQDN of your VM with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a><span data-ttu-id="591bf-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="591bf-159">Next steps</span></span>
<span data-ttu-id="591bf-160">Kaynak VM görüntüden birden çok VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="591bf-160">You can create multiple VMs from your source VM image.</span></span> <span data-ttu-id="591bf-161">Toomake değişiklikleri tooyour görüntü ihtiyacınız varsa:</span><span class="sxs-lookup"><span data-stu-id="591bf-161">If you need toomake changes tooyour image:</span></span> 

- <span data-ttu-id="591bf-162">Bir VM görüntünüze oluşturun.</span><span class="sxs-lookup"><span data-stu-id="591bf-162">Create a VM from your image.</span></span>
- <span data-ttu-id="591bf-163">Tüm güncelleştirmeler veya yapılandırma değişikliklerini yapın.</span><span class="sxs-lookup"><span data-stu-id="591bf-163">Make any updates or configuration changes.</span></span>
- <span data-ttu-id="591bf-164">İzleyin hello adımları yeniden toodeprovision, serbest bırakma, generalize ve görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="591bf-164">Follow hello steps again toodeprovision, deallocate, generalize, and create an image.</span></span>
- <span data-ttu-id="591bf-165">Bu yeni görüntüyü gelecekteki dağıtımlar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="591bf-165">Use this new image for future deployments.</span></span> <span data-ttu-id="591bf-166">İsterseniz, hello orijinal görüntüyü silin.</span><span class="sxs-lookup"><span data-stu-id="591bf-166">If desired, delete hello original image.</span></span>

<span data-ttu-id="591bf-167">Vm'leriniz hello CLI ile yönetme ile ilgili daha fazla bilgi için bkz: [Azure CLI 2.0](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="591bf-167">For more information on managing your VMs with hello CLI, see [Azure CLI 2.0](/cli/azure/overview).</span></span>
