---
title: bir Linux VM hello Azure CLI 2.0 ile aaaHow tooresize | Microsoft Docs
description: "Nasıl tooscale yukarı veya aşağı değiştirerek Linux sanal makine ölçek hello VM boyutu."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="ae203-103">CLI 2.0 kullanarak bir Linux sanal makine yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="ae203-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="ae203-104">Bir sanal makine (VM) sağlama sonra hello VM yukarı veya aşağı hello değiştirerek ölçeklendirmek [VM boyutu][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="ae203-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="ae203-105">Bazı durumlarda, ilk hello VM ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae203-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="ae203-106">Merhaba boyutu hello VM barındırma hello donanım kümede kullanılabilir değil isterseniz toodeallocate hello VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae203-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="ae203-107">Bu makalede, nasıl bir Linux VM tooresize hello Azure CLI 2.0 ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="ae203-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="ae203-108">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae203-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="ae203-109">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="ae203-109">Resize a VM</span></span>
<span data-ttu-id="ae203-110">bir VM tooresize, gereksinim duyduğunuz hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ae203-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="ae203-111">Görünüm hello listesi kullanılabilir VM boyutları ile Merhaba VM barındırıldığı hello donanım kümede [az vm listesi-vm-yeniden boyutlandırma-seçenekleri](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="ae203-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="ae203-112">Merhaba aşağıdaki örnek listeler VM boyutları hello adlı VM için `myVM` hello kaynak grubunda `myResourceGroup` bölge:</span><span class="sxs-lookup"><span data-stu-id="ae203-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="ae203-113">Merhaba VM boyutu listelendiğini isterseniz, yeniden boyutlandırma VM ile Merhaba [az VM'yi yeniden boyutlandırın](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="ae203-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="ae203-114">Aşağıdaki örnek yeniden boyutlandırır hello hello adlı VM `myVM` toohello `Standard_DS3_v2` boyutu:</span><span class="sxs-lookup"><span data-stu-id="ae203-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="ae203-115">Bu işlem sırasında Hello VM yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="ae203-115">hello VM restarts during this process.</span></span> <span data-ttu-id="ae203-116">Merhaba yeniden başladıktan sonra var olan işletim sistemi ve veri diskleri eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ae203-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="ae203-117">Merhaba geçici diskteki herhangi bir şey kaybolur.</span><span class="sxs-lookup"><span data-stu-id="ae203-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="ae203-118">Merhaba VM boyutu listelenmeyen isterseniz, toofirst gereken ayırması VM ile Merhaba [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="ae203-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="ae203-119">Bu işlem, bölge destekler hello ve ardından başlatılan yeniden boyutlandırılan tooany boyutu kullanılabilir hello VM toothen sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae203-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="ae203-120">Merhaba aşağıdaki adımları serbest bırakma, yeniden boyutlandırma ve hello adlı VM Başlat `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="ae203-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="ae203-121">Serbest bırakma hello VM toohello VM atanan dinamik IP adreslerini de serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="ae203-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="ae203-122">Merhaba işletim sistemi ve veri diskleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="ae203-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae203-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ae203-123">Next steps</span></span>
<span data-ttu-id="ae203-124">Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini. Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Linux makineler ölçekleme][scale-set].</span><span class="sxs-lookup"><span data-stu-id="ae203-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
