---
title: Linux sanal makineleri azure'da aaaRedeploy | Microsoft Docs
description: "Nasıl tooredeploy Linux sanal makinelerinin Azure toomitigate SSH bağlantısını keser."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="efa4d-103">Linux sanal makine toonew Azure düğümü yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="efa4d-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="efa4d-104">SSH sorunlarını giderme zorluklarla yüz veya uygulamaya erişim tooa Linux sanal makine (VM) Azure'da hello VM dağıtarak yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="efa4d-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="efa4d-105">Bir VM yeniden dağıtırken hello VM tooa yeni düğümde hello Azure altyapı taşır ve yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="efa4d-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="efa4d-106">Tüm yapılandırma seçenekleri ve ilişkili kaynakları korunur.</span><span class="sxs-lookup"><span data-stu-id="efa4d-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="efa4d-107">Bu makale size nasıl gösterir VM Azure CLI veya hello Azure portal kullanarak bir tooredeploy.</span><span class="sxs-lookup"><span data-stu-id="efa4d-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="efa4d-108">Bir VM dağıtmanız sonra hello geçici disk kaybolur ve sanal ağ arabirimiyle ilişkilendirilmiş dinamik IP adreslerini güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="efa4d-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="efa4d-109">Seçenekler aşağıdaki hello birini kullanarak bir VM'i yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efa4d-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="efa4d-110">Yalnızca VM toochoose bir seçenek tooredeploy gerekir:</span><span class="sxs-lookup"><span data-stu-id="efa4d-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="efa4d-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="efa4d-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="efa4d-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="efa4d-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="efa4d-113">Azure portal</span><span class="sxs-lookup"><span data-stu-id="efa4d-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="efa4d-114">Hello Azure CLI 2.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="efa4d-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="efa4d-115">Son yükleme hello [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="efa4d-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="efa4d-116">VM ile dağıtmanız [az vm dağıtın](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="efa4d-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="efa4d-117">Aşağıdaki örnek yeniden dağıtır hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="efa4d-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="efa4d-118">Hello Azure CLI 1.0 kullanın</span><span class="sxs-lookup"><span data-stu-id="efa4d-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="efa4d-119">Merhaba yüklemek [en son Azure CLI 1.0](../../cli-install-nodejs.md)tooan Azure hesabı oturum ve Kaynak Yöneticisi modunda olduğundan emin olun (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="efa4d-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="efa4d-120">Aşağıdaki örnek yeniden dağıtır hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="efa4d-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="efa4d-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="efa4d-121">Next steps</span></span>
<span data-ttu-id="efa4d-122">Tooyour VM bağlantı sorunları yaşıyorsanız, özel Yardım bulabilirsiniz [SSH bağlantı sorunlarını giderme](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) veya [sorun giderme adımları SSH ayrıntılı](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efa4d-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="efa4d-123">VM üzerinde çalışan bir uygulama, erişemiyor, ayrıca okuyabilirsiniz [uygulama sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efa4d-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

