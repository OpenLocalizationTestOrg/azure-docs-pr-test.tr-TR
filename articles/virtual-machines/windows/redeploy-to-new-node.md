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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Windows sanal makine toonew Azure düğümü yeniden dağıtın
Sorunlar karşılıklı Uzak Masaüstü (RDP) sorunlarını giderme bağlantısı veya uygulama erişim tooWindows tabanlı Azure sanal VM yardımcı olabilecek hello dağıtarak makine (VM). Bir VM yeniden dağıtırken hello VM tooa yeni düğümde hello Azure altyapı taşır ve tüm yapılandırma seçenekleri ve ilişkili kaynakları geri korur, çalıştırır. Bu makale size nasıl gösterir Azure PowerShell veya hello Azure portal kullanarak VM bir tooredeploy.

> [!NOTE]
> Bir VM dağıtmanız sonra hello geçici disk kaybolur ve sanal ağ arabirimiyle ilişkilendirilmiş dinamik IP adreslerini güncelleştirilir. 


## <a name="using-azure-powershell"></a>Azure PowerShell’i kullanma
En son Azure PowerShell hello sahip olduğundan emin olun, makinenizde yüklü 1.x. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

Merhaba aşağıdaki örnek dağıtır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Sonraki adımlar
Tooyour VM bağlantı sorunları yaşıyorsanız, özel Yardım bulabilirsiniz [RDP bağlantı sorunlarını giderme](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [sorun giderme adımları RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). VM üzerinde çalışan bir uygulama, erişemiyor, ayrıca okuyabilirsiniz [uygulama sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

