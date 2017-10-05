---
title: "Azure CLI örnek komut dosyası - yük dengeli sanal Machin ölçek kümesindeki AMPUL yığını dağıtma | Microsoft Docs"
description: "Bir yük AMPUL yığınında dağıtmak için bir özel betik uzantısı kullanın = dengeli sanal makine ölçek Azure üzerinde ayarlayın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: 4007e8c85c0ff24bf5030881eac666582714eae3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="1e137-103">Yük dengeli sanal makine ölçek kümesi AMPUL yığınında dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e137-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="1e137-104">Bu örnek, bir sanal makine ölçek kümesi oluşturur ve her bir sanal makine ölçek kümesindeki AMPUL yığında dağıtmak için özel bir komut dosyası çalıştıran uzantı uygular.</span><span class="sxs-lookup"><span data-stu-id="1e137-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="1e137-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1e137-105">Sample script</span></span>

<span data-ttu-id="1e137-106">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "sanal makine ölçek AMPUL yığınla kümesi oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="1e137-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]</span></span>

## <a name="connect"></a><span data-ttu-id="1e137-107">Bağlan</span><span class="sxs-lookup"><span data-stu-id="1e137-107">Connect</span></span>

<span data-ttu-id="1e137-108">Vm'leriniz ve, Ölçek nasıl bağlayacağınızı görmek için bu kodu kullanın ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e137-108">Use this code to see how to connect to your VMs and your scale set.</span></span>

<span data-ttu-id="1e137-109">[!code-azurecli[Ana](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "erişim sanal makine ölçek kümesi")]</span><span class="sxs-lookup"><span data-stu-id="1e137-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1e137-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="1e137-110">Clean up deployment</span></span> 

<span data-ttu-id="1e137-111">Kaynak grubu, Ölçek kümesini ve sanal makineleri kaldırmak için aşağıdaki komutu çalıştırın ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="1e137-111">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1e137-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1e137-112">Script explanation</span></span>

<span data-ttu-id="1e137-113">Bu komut, bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilişkili kaynakları oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="1e137-113">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="1e137-114">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="1e137-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="1e137-115">Komut</span><span class="sxs-lookup"><span data-stu-id="1e137-115">Command</span></span> | <span data-ttu-id="1e137-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="1e137-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e137-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e137-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1e137-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1e137-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1e137-119">az vmss oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e137-119">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="1e137-120">Bir sanal makine ölçek kümesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="1e137-120">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="1e137-121">az ağ lb kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e137-121">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="1e137-122">Yük dengeli bir uç nokta ekleyin</span><span class="sxs-lookup"><span data-stu-id="1e137-122">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="1e137-123">az vmss uzantı kümesi</span><span class="sxs-lookup"><span data-stu-id="1e137-123">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="1e137-124">VM Dağıtım üzerinde özel komut dosyasını çalıştırır uzantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e137-124">Create the extension that runs the custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="1e137-125">az vmss güncelleştirme-örnekleri</span><span class="sxs-lookup"><span data-stu-id="1e137-125">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="1e137-126">Özel betik uzantısı ölçek kümesi uygulanmadan dağıtılan VM örnekleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1e137-126">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span></span> |
| [<span data-ttu-id="1e137-127">az vmss ölçek</span><span class="sxs-lookup"><span data-stu-id="1e137-127">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="1e137-128">Daha fazla VM örnekleri ekleyerek kümesini ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="1e137-128">Scale up the scale set by adding more VM instances.</span></span> <span data-ttu-id="1e137-129">Bunlar dağıtıldığında özel bir komut dosyası bunlar üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="1e137-129">The custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="1e137-130">az ağ ortak IP listesi</span><span class="sxs-lookup"><span data-stu-id="1e137-130">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="1e137-131">Örneği tarafından oluşturulan VM'ler IP adreslerini alın.</span><span class="sxs-lookup"><span data-stu-id="1e137-131">Get the IP addresses of the VMs created by the sample.</span></span> |
| [<span data-ttu-id="1e137-132">az ağ lb Göster</span><span class="sxs-lookup"><span data-stu-id="1e137-132">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="1e137-133">Ön uç ve arka uç yük dengeleyici tarafından kullanılan bağlantı noktaları alın.</span><span class="sxs-lookup"><span data-stu-id="1e137-133">Get the frontend and backend ports used by the load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1e137-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e137-134">Next steps</span></span>

<span data-ttu-id="1e137-135">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1e137-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1e137-136">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e137-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
