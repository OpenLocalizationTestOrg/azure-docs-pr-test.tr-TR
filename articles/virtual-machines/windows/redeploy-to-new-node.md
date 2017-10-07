---
title: azure'da Windows sanal makineler aaaRedeploy | Microsoft Docs
description: "Nasıl tooredeploy Windows sanal makinelerin Azure toomitigate RDP bağlantı verir."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="657c0-103">Windows sanal makine toonew Azure düğümü yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="657c0-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="657c0-104">Sorunlar karşılıklı Uzak Masaüstü (RDP) sorunlarını giderme bağlantısı veya uygulama erişim tooWindows tabanlı Azure sanal VM yardımcı olabilecek hello dağıtarak makine (VM).</span><span class="sxs-lookup"><span data-stu-id="657c0-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="657c0-105">Bir VM yeniden dağıtırken hello VM tooa yeni düğümde hello Azure altyapı taşır ve tüm yapılandırma seçenekleri ve ilişkili kaynakları geri korur, çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="657c0-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="657c0-106">Bu makale size nasıl gösterir Azure PowerShell veya hello Azure portal kullanarak VM bir tooredeploy.</span><span class="sxs-lookup"><span data-stu-id="657c0-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="657c0-107">Bir VM dağıtmanız sonra hello geçici disk kaybolur ve sanal ağ arabirimiyle ilişkilendirilmiş dinamik IP adreslerini güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="657c0-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="657c0-108">Azure PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="657c0-108">Using Azure PowerShell</span></span>
<span data-ttu-id="657c0-109">En son Azure PowerShell hello sahip olduğundan emin olun, makinenizde yüklü 1.x.</span><span class="sxs-lookup"><span data-stu-id="657c0-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="657c0-110">Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="657c0-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="657c0-111">Merhaba aşağıdaki örnek dağıtır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="657c0-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="657c0-112">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="657c0-112">Next steps</span></span>
<span data-ttu-id="657c0-113">Tooyour VM bağlantı sorunları yaşıyorsanız, özel Yardım bulabilirsiniz [RDP bağlantı sorunlarını giderme](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [sorun giderme adımları RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="657c0-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="657c0-114">VM üzerinde çalışan bir uygulama, erişemiyor, ayrıca okuyabilirsiniz [uygulama sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="657c0-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

