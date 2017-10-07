---
title: "aaaAzure CLI komut dosyası örneği - VMs yeniden | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yeniden başlatma VM'ler etiketi ve kimliği"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="094bf-103">Sanal makineleri yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="094bf-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="094bf-104">Bu örnek birkaç yolu tooget bazı sanal makineleri gösterir ve bunları yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="094bf-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="094bf-105">Merhaba hello kaynak grubunda ilk tüm hello VM'ler yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="094bf-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="094bf-106">Merhaba ikinci alır hello etiketli kullanarak VM'ler `az resouce list` VM'ler toohello kaynakları filtreler ve bu sanal makineleri yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="094bf-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="094bf-107">Bu örnek, bir Bash kabuğunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="094bf-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="094bf-108">Windows istemcisi üzerinde Azure CLI betikleri çalıştırma seçenekleri için bkz [Windows hello Azure CLI çalıştıran](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="094bf-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="094bf-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="094bf-109">Sample script</span></span>

<span data-ttu-id="094bf-110">Merhaba örnek üç komut dosyasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="094bf-110">hello sample has three scripts.</span></span>
<span data-ttu-id="094bf-111">ilk hello sanal makineler hello.</span><span class="sxs-lookup"><span data-stu-id="094bf-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="094bf-112">Sağlanan her bir VM toobe beklemeden Hello komutu döndürecek şekilde hello Hayır bekleme seçeneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="094bf-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="094bf-113">Merhaba, ikinci tam olarak sağlanan hello VM'ler toobe için bekler.</span><span class="sxs-lookup"><span data-stu-id="094bf-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="094bf-114">sağlanan tüm hello VM'ler Hello üçüncü komut dosyası yeniden başlatır ve ardından sanal makineleri yalnızca hello etiketli.</span><span class="sxs-lookup"><span data-stu-id="094bf-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="094bf-115">Merhaba VM'ler sağlama</span><span class="sxs-lookup"><span data-stu-id="094bf-115">Provision hello VMs</span></span>

<span data-ttu-id="094bf-116">Bu komut dosyasını bir kaynak grubu ve üç VM'ler toorestart oluşturur.</span><span class="sxs-lookup"><span data-stu-id="094bf-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="094bf-117">İki tanesi etiketlenir.</span><span class="sxs-lookup"><span data-stu-id="094bf-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="094bf-118">Wait</span><span class="sxs-lookup"><span data-stu-id="094bf-118">Wait</span></span>

<span data-ttu-id="094bf-119">Bu betik, tüm üç VM'ler sağlanır veya bunlardan birini tooprovision başarısız olana kadar 20 dakikada sağlama durumu hello üzerinde denetler.</span><span class="sxs-lookup"><span data-stu-id="094bf-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="094bf-120">Merhaba sanal makineleri yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="094bf-120">Restart hello VMs</span></span>

<span data-ttu-id="094bf-121">Bu komut tüm hello VM'ler hello kaynak grubunda yeniden başlatır ve yalnızca etiketli hello VM'ler yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="094bf-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="094bf-122">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="094bf-122">Clean up deployment</span></span> 

<span data-ttu-id="094bf-123">Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grupları, sanal makineleri ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="094bf-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="094bf-124">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="094bf-124">Script explanation</span></span>

<span data-ttu-id="094bf-125">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="094bf-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="094bf-126">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="094bf-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="094bf-127">Komut</span><span class="sxs-lookup"><span data-stu-id="094bf-127">Command</span></span> | <span data-ttu-id="094bf-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="094bf-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="094bf-129">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="094bf-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="094bf-130">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="094bf-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="094bf-131">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="094bf-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="094bf-132">Merhaba sanal makineler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="094bf-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="094bf-133">az vm listesi</span><span class="sxs-lookup"><span data-stu-id="094bf-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="094bf-134">İle kullanılan `--query` tooensure hello VM'ler sağlanan yeniden başlatmadan önce ve sonra tooget hello hello VM'ler toorestart kimliklerini bunları.</span><span class="sxs-lookup"><span data-stu-id="094bf-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="094bf-135">az kaynak listesi</span><span class="sxs-lookup"><span data-stu-id="094bf-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="094bf-136">İle kullanılan `--query` tooget hello hello etiketini kullanarak hello VM'ler kimliklerini.</span><span class="sxs-lookup"><span data-stu-id="094bf-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="094bf-137">az vm yeniden başlatma</span><span class="sxs-lookup"><span data-stu-id="094bf-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="094bf-138">Merhaba VM'ler yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="094bf-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="094bf-139">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="094bf-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="094bf-140">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="094bf-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="094bf-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="094bf-141">Next steps</span></span>

<span data-ttu-id="094bf-142">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="094bf-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="094bf-143">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="094bf-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
