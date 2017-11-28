---
title: "bir Azure VM tooa ölçek aaaConvert kümesi | Microsoft Docs"
description: "Oluşturun ve hello Azure CLI ile ayarlamak Linux Azure sanal makine ölçek dağıtın."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="2e731-103">Varolan bir Azure sanal makinesi tooa ölçek kümesini Dönüştür</span><span class="sxs-lookup"><span data-stu-id="2e731-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="2e731-104">Bu öğretici bir sanal makine tooa sanal makine ölçek toouse Azure CLI 2.0 tooconvert nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e731-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="2e731-105">Ayrıca, tooautomate hello yapılandırma hello ölçeğinde hello sanal makinelerin nasıl ayarlanacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2e731-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="2e731-106">Azure CLI 2.0 tooinstall nasıl görürüm hakkında daha fazla bilgi için [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2e731-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="2e731-107">Ölçek kümeleri hakkında daha fazla bilgi için bkz: [sanal makine ölçek ayarlar](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e731-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="2e731-108">1. adım - Deprovision hello VM</span><span class="sxs-lookup"><span data-stu-id="2e731-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="2e731-109">SSH tooconnect toohello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e731-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="2e731-110">Deprovision hello VM hello Azure VM Aracısı toodelete dosyaları ve verileri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2e731-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="2e731-111">Sağlamayı kaldırmayı ilişkin ayrıntılı genel bakış için bkz: [Linux sanal makine yakalama](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="2e731-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="2e731-112">2. adım - hello VM bir görüntüsünü yakalama</span><span class="sxs-lookup"><span data-stu-id="2e731-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="2e731-113">Yakalama ilişkin ayrıntılı genel bakış için bkz: [Linux sanal makine yakalama](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="2e731-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="2e731-114">Deallocate VM ile Merhaba [az vm serbest bırakma](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="2e731-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="2e731-115">Generalize VM ile Merhaba [az vm generalize](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="2e731-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="2e731-116">İle Merhaba VM kaynaktan görüntü oluşturma [az görüntü oluşturma](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="2e731-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="2e731-117">3. adım - hello ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e731-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="2e731-118">Merhaba alma **kimliği** hello görüntüsünün.</span><span class="sxs-lookup"><span data-stu-id="2e731-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="2e731-119">Bir VM, görüntü kaynağı ile oluşturmak [az vmss oluşturma](/cli/azure/vmss#create):</span><span class="sxs-lookup"><span data-stu-id="2e731-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="2e731-120">Bu komut ayrıca bir 10 gb veri diski bağlı.</span><span class="sxs-lookup"><span data-stu-id="2e731-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="2e731-121">Merhaba VM bağlı olarak seçilen boyut unutmayın (kullandık **Standard_DS1_v2**), izin verilen veri diski sayısı hello farklıdır.</span><span class="sxs-lookup"><span data-stu-id="2e731-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="2e731-122">Daha fazla bilgi için hello gözden [sanal makine boyutlarını](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2e731-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="2e731-123">Merhaba ölçek sonlandığında ayarladıktan sonra tooit bağlayın.</span><span class="sxs-lookup"><span data-stu-id="2e731-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="2e731-124">IP adresleri listesi SSH ile Merhaba örnekleri alın [az vmss listesi-örnek-bağlantı-bilgisi](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="2e731-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="2e731-125">Toohello sanal makine örneği tooinitialize hello veri diski şimdi bağlan</span><span class="sxs-lookup"><span data-stu-id="2e731-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="2e731-126">4. adım - Initialize hello veri diski</span><span class="sxs-lookup"><span data-stu-id="2e731-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="2e731-127">Merhaba diskle bağlı toohello sanal makine bölüm `fdisk`:</span><span class="sxs-lookup"><span data-stu-id="2e731-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="2e731-128">Merhaba sahip bir dosya sistemi toohello bölüm yazma `mkfs` komutu:</span><span class="sxs-lookup"><span data-stu-id="2e731-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="2e731-129">Böylece hello işletim sisteminde erişilebilir hello yeni diski bağlayın:</span><span class="sxs-lookup"><span data-stu-id="2e731-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="2e731-130">Merhaba disk şimdi doğrulanabilir hello datadrive mountpoint aracılığıyla erişimleri olması `ls /datadrive/`.</span><span class="sxs-lookup"><span data-stu-id="2e731-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="2e731-131">Merhaba SSH oturumunu sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="2e731-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="2e731-132">5. adım - Güvenlik Duvarı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e731-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="2e731-133">Merhaba güvenlik duvarı toohello hello ölçek kümesi tarafından barındırılan Web sunucusu delik del.</span><span class="sxs-lookup"><span data-stu-id="2e731-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="2e731-134">Hello ölçek kümesi oluşturuldu, bir yük dengeleyici da oluşturulmuştur ve onu kullanılan **SSH** toohello tek tek sanal makineleri.</span><span class="sxs-lookup"><span data-stu-id="2e731-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="2e731-135">tooopen bir bağlantı noktası, iki ayrı alabileceğiniz bilgi gereken Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2e731-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="2e731-136">**Ön uç IP adresi havuzu**</span><span class="sxs-lookup"><span data-stu-id="2e731-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="2e731-137">**Arka uç IP adresi havuzu**</span><span class="sxs-lookup"><span data-stu-id="2e731-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="2e731-138">Bu iki adlarıyla bağlantı noktasını açabilirsiniz **80**.</span><span class="sxs-lookup"><span data-stu-id="2e731-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="2e731-139">6. adım - yapılandırmasını otomatikleştirmek</span><span class="sxs-lookup"><span data-stu-id="2e731-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="2e731-140">Merhaba veri diski her sanal makine örneğinde yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e731-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="2e731-141">Biz hello hello hello sanal makinenin yapılandırmasını otomatikleştirebilirsiniz **CustomScript** uzantısı.</span><span class="sxs-lookup"><span data-stu-id="2e731-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="2e731-142">İlk olarak, oluşturma bir *.sh* hello disk biçimi komutları içeren komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2e731-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="2e731-143">Ardından, bu komut dosyası toowhere hello karşıya **CustomScript** uzantısı erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e731-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="2e731-144">Bir kopyasını kullanılabilir [burada](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span><span class="sxs-lookup"><span data-stu-id="2e731-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="2e731-145">Adlı bir yerel dosya oluşturma **settings.json** ve put hello JSON bloğunda aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="2e731-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="2e731-146">Merhaba `flieUris` komut dosyanızı karşıya için toowhere özelliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2e731-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="2e731-147">Bu komut tooyour ölçeği ile Merhaba Ayarla dağıtmak **CustomScript** hello başvuran uzantısı **settings.json** yeni oluşturduğumuz dosya.</span><span class="sxs-lookup"><span data-stu-id="2e731-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="2e731-148">Bu uzantı, tüm geçerli örnekleri ve daha sonra ölçeklendirme tarafından oluşturulan tüm örnekleri otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="2e731-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="2e731-149">7. adım - otomatik ölçeklendirme kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2e731-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="2e731-150">Şu anda, otomatik ölçeklendirme kurallarını Azure CLI ayarlanamaz.</span><span class="sxs-lookup"><span data-stu-id="2e731-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="2e731-151">Kullanım hello [Azure portal](https://portal.azure.com) tooconfigure otomatik ölçeklendirme.</span><span class="sxs-lookup"><span data-stu-id="2e731-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="2e731-152">Adım 8 - yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="2e731-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="2e731-153">Merhaba ölçek kümesini Hello yaşam döngüsü boyunca toorun gerekebilir bir veya daha fazla yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="2e731-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="2e731-154">Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren toocreate komut dosyaları isteyebilir ve hello Azure CLI hızlı şekilde toodo bu görevleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e731-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="2e731-155">Birkaç ortak görevler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="2e731-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="2e731-156">Bağlantı bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="2e731-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="2e731-157">Örnek sayısı (el ile Ölçek) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2e731-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="2e731-158">Kaynak grubunu silme</span><span class="sxs-lookup"><span data-stu-id="2e731-158">Delete resource group</span></span>

<span data-ttu-id="2e731-159">Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.</span><span class="sxs-lookup"><span data-stu-id="2e731-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2e731-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e731-160">Next steps</span></span>
<span data-ttu-id="2e731-161">Merhaba sanal makine ölçek bazıları hakkında daha fazla Bu öğreticide, sunulan özellikler kümesi toolearn bilgisinden hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2e731-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="2e731-162">Azure sanal makine ölçek kümeleri genel bakış</span><span class="sxs-lookup"><span data-stu-id="2e731-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="2e731-163">Azure Load Balancer’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="2e731-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="2e731-164">Ağ güvenlik grupları ile ağ trafiği akışını denetleme</span><span class="sxs-lookup"><span data-stu-id="2e731-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)