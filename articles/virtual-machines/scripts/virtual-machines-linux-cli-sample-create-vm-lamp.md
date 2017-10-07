---
title: "aaaAzure CLI komut dosyası örneği - hello AMPUL yığını yük dengelemeli mimarilerde sanal Machin ölçek kümesindeki dağıtma | Microsoft Docs"
description: "Kullanan bir özel betik uzantısı toodeploy hello AMPUL yığını bir yük dengeli sanal makineyi ölçeği Azure üzerinde Ayarla =."
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
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="739c3-103">Yük dengeli sanal makine ölçek kümesindeki Hello AMPUL yığını dağıtma</span><span class="sxs-lookup"><span data-stu-id="739c3-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="739c3-104">Bu örnek, bir sanal makine ölçek kümesi oluşturur ve bir özel komut dosyası toodeploy hello AMPUL yığını hello ölçek kümesindeki her bir sanal makine üzerinde çalışan bir uzantı uygular.</span><span class="sxs-lookup"><span data-stu-id="739c3-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="739c3-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="739c3-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="739c3-106">Bağlan</span><span class="sxs-lookup"><span data-stu-id="739c3-106">Connect</span></span>

<span data-ttu-id="739c3-107">Bu kod toosee tooconnect tooyour VM'ler ve, Ölçek nasıl ayarlanacağını kullanın.</span><span class="sxs-lookup"><span data-stu-id="739c3-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="739c3-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="739c3-108">Clean up deployment</span></span> 

<span data-ttu-id="739c3-109">Komut tooremove hello kaynak grubu, hello ölçek kümesini ve sanal makineleri ve tüm ilgili kaynaklar aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="739c3-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="739c3-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="739c3-110">Script explanation</span></span>

<span data-ttu-id="739c3-111">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="739c3-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="739c3-112">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="739c3-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="739c3-113">Komut</span><span class="sxs-lookup"><span data-stu-id="739c3-113">Command</span></span> | <span data-ttu-id="739c3-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="739c3-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="739c3-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="739c3-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="739c3-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="739c3-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="739c3-117">az vmss oluşturma</span><span class="sxs-lookup"><span data-stu-id="739c3-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="739c3-118">Bir sanal makine ölçek kümesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="739c3-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="739c3-119">az ağ lb kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="739c3-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="739c3-120">Yük dengeli bir uç nokta ekleyin</span><span class="sxs-lookup"><span data-stu-id="739c3-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="739c3-121">az vmss uzantı kümesi</span><span class="sxs-lookup"><span data-stu-id="739c3-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="739c3-122">VM Dağıtım üzerinde hello özel betik çalıştıran hello uzantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="739c3-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="739c3-123">az vmss güncelleştirme-örnekleri</span><span class="sxs-lookup"><span data-stu-id="739c3-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="739c3-124">Merhaba özel komut dosyası hello uzantısı uygulanmadan önce dağıtılan hello VM örnekleri üzerinde çalıştırma toohello ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="739c3-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="739c3-125">az vmss ölçek</span><span class="sxs-lookup"><span data-stu-id="739c3-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="739c3-126">Daha fazla VM örnekleri ekleyerek ayarlayın hello ölçek ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="739c3-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="739c3-127">Bunlar dağıtıldığında hello özel betik bunlar üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="739c3-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="739c3-128">az ağ ortak IP listesi</span><span class="sxs-lookup"><span data-stu-id="739c3-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="739c3-129">Merhaba hello örneği tarafından oluşturulan VM'ler Hello IP adreslerini alın.</span><span class="sxs-lookup"><span data-stu-id="739c3-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="739c3-130">az ağ lb Göster</span><span class="sxs-lookup"><span data-stu-id="739c3-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="739c3-131">Merhaba ön uç ve arka uç hello yük dengeleyici tarafından kullanılan bağlantı noktaları alın.</span><span class="sxs-lookup"><span data-stu-id="739c3-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="739c3-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="739c3-132">Next steps</span></span>

<span data-ttu-id="739c3-133">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="739c3-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="739c3-134">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="739c3-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
