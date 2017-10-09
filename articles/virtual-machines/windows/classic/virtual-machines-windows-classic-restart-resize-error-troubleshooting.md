---
title: "yeniden başlatmadan veya sorunları yeniden boyutlandırma aaaVM | Microsoft Docs"
description: "Yeniden başlatmadan veya mevcut bir Windows sanal makine azure'da yeniden boyutlandırma Klasik dağıtım sorunlarını giderme"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a>Yeniden başlatmadan veya mevcut bir Windows sanal makine azure'da yeniden boyutlandırma Klasik dağıtım sorunlarını giderme
> [!div class="op_single_selector"]
> * [Klasik](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [Resource Manager](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

Toostart durdurulmuş Azure sanal makine (VM) deneyin ya da mevcut bir Azure VM'i yeniden boyutlandırın karşılaştığınız hello ortak bir ayırma hatası hatasıdır. Merhaba küme veya bölgede kullanılabilir kaynakları ya da yok ya da alamazsınız destek hello istenen VM boyutu bu hata oluşur.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Toplama denetim günlüklerini
sorun giderme, toostart toplama hello denetim hello sorun ilişkili tooidentify hello hata günlüğe kaydeder.

Hello Azure portal'ı tıklatın **Gözat** > **sanal makineleri** > *Windows sanal makinenizi*  >   **Ayarları** > **denetim günlüklerini**.

## <a name="issue-error-when-starting-a-stopped-vm"></a>Sorun: durmuş bir VM'yi başlatma sırasında hata
Toostart durmuş bir VM'yi deneyin ancak bir ayırma hatası alır.

### <a name="cause"></a>Nedeni
VM toostart hello durduruldu hello isteği hello bulut hizmeti barındıran hello özgün kümesine çalıştı toobe sahiptir. Ancak, hello küme boş alan kullanılabilir toofulfill hello isteği yok.

### <a name="resolution"></a>Çözüm
* Yeni bir bulut hizmeti oluşturup bir bölge veya bölge tabanlı bir sanal ağ, ancak bir benzeşim grubu ile ilişkilendirin.
* Silme hello VM durduruldu.
* Merhaba yeni bulut hizmeti VM Hello hello diskleri kullanarak yeniden oluşturun.
* Başlangıç hello VM yeniden oluşturulacak.

Yeni bir bulut hizmeti toocreate çalışırken bir hata alırsanız, daha sonra yeniden deneyin veya hello bölge hello bulut hizmeti için değiştirin.

> [!IMPORTANT]
> Bu bilgileri hello mevcut bulut hizmeti için kullandığınız tüm hello bağımlılıklar için bu bilgileri toochange gerekir hello yeni bulut hizmeti yeni bir ad ve VIP, gerekir.
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a>Sorun: mevcut bir VM'yi yeniden boyutlandırılırken hata
Mevcut bir VM'yi tooresize deneyin ancak bir ayırma hatası alır.

### <a name="cause"></a>Nedeni
Merhaba isteği tooresize hello VM toobe sahip hello özgün kümesine, konaklar hello bulut hizmetinin çalıştı. Ancak, hello küme desteklemediği hello istenen VM boyutu.

### <a name="resolution"></a>Çözüm
Azaltmak hello istenen VM boyutu ve Yeniden Dene'yi hello isteği yeniden boyutlandırın.

* Tıklatın **tümüne Gözat** > **sanal makineleri (Klasik)** > *sanal makineniz* > **ayarları** > **boyutu**. Ayrıntılı adımlar için bkz: [hello sanal makine yeniden boyutlandırma](https://msdn.microsoft.com/library/dn168976.aspx).

Olası tooreduce hello VM boyutu değilse, aşağıdaki adımları izleyin:

* Bağlantılı tooan benzeşim grubu olmadığı ve bağlantılı tooan benzeşim grubu olan bir sanal ağ ile ilişkili olmayan sağlayarak yeni bir bulut hizmeti oluşturun.
* Yeni, büyük ölçekli bir VM içinde oluşturun.

Tüm Vm'leriniz birleştirebilir hello aynı bulut hizmeti. Mevcut bulut hizmetiniz bir bölge tabanlı sanal ağ ile ilişkili ise, hello yeni bulut hizmeti toohello mevcut sanal ağa bağlanabilir.

Hello mevcut bulut hizmeti bir bölge tabanlı sanal ağ ile ilişkili değilse, sonra toodelete hello VM'ler hello mevcut bulut hizmetine sahip ve bunların disklerden hello yeni bulut hizmetinde yeniden oluşturun. Ancak, önemli tooremember tooupdate ihtiyacınız olacak şekilde hello yeni bulut hizmeti yeni bir ad ve VIP, bunlar şu anda bu bilgileri hello olan bulut hizmetini kullanan tüm hello bağımlılıklar için sahip olma olasılığı vardır.

## <a name="next-steps"></a>Sonraki adımlar
Azure üzerinde bir Windows VM oluşturduğunuzda sorunlarıyla karşılaşırsanız bkz [Azure'da Windows sanal makine oluşturma ile dağıtım sorunlarını giderme](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

