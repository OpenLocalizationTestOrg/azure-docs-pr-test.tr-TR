---
title: "yeniden başlatma veya yeniden boyutlandırma aaaVM sorunları Azure'da | Microsoft Docs"
description: "Yeniden başlatmadan veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Resource Manager dağıtım sorunlarını giderme"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a>Yeniden başlatmadan veya varolan bir Linux VM azure'da yeniden boyutlandırma ile dağıtım sorunlarını giderme
Toostart durdurulmuş Azure sanal makine (VM) deneyin ya da mevcut bir Azure VM'i yeniden boyutlandırın karşılaştığınız hello ortak bir ayırma hatası hatasıdır. Merhaba küme veya bölgede kullanılabilir kaynakları ya da yok ya da alamazsınız destek hello istenen VM boyutu bu hata oluşur.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a>Toplama etkinliklerini günlüğe kaydeder
sorun giderme, toostart toplama hello etkinlik hello sorun ilişkili tooidentify hello hata günlüğe kaydeder. Aşağıdaki bağlantılar hello hello süreci hakkında ayrıntılı bilgiler içerir:

[Dağıtım işlemlerini görüntüleme](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Etkinlik günlükleri toomanage Azure görüntülemek kaynakları](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a>Sorun: durmuş bir VM'yi başlatma sırasında hata
Toostart durmuş bir VM'yi deneyin ancak bir ayırma hatası alır.

### <a name="cause"></a>Nedeni
VM toostart hello durduruldu hello isteği hello bulut hizmeti barındıran hello özgün kümesine çalıştı toobe sahiptir. Ancak, hello küme boş alan kullanılabilir toofulfill hello isteği yok.

### <a name="resolution"></a>Çözüm
* Merhaba kullanılabilirlik VM'ler ayarlayın ve her VM yeniden başlatma tüm hello durdurun.
  
  1. Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.
  2. Tüm VM'ler Dur Merhaba, durduruldu hello VM'lerin her birinde seçin ve Başlat'ı tıklatın.
* Merhaba yeniden başlatma isteği daha sonra yeniden deneyin.

## <a name="issue-error-when-resizing-an-existing-vm"></a>Sorun: mevcut bir VM'yi yeniden boyutlandırılırken hata
Mevcut bir VM'yi tooresize deneyin ancak bir ayırma hatası alır.

### <a name="cause"></a>Nedeni
Merhaba isteği tooresize hello VM toobe sahip hello özgün kümesine, konaklar hello bulut hizmetinin çalıştı. Ancak, hello küme desteklemediği hello istenen VM boyutu.

### <a name="resolution"></a>Çözüm
* Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.
* Merhaba, hello VM değiştirilemez istenen boyut:
  
  1. Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun.
     
     * Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.
  2. Tüm VM'ler Dur Merhaba, istenen hello VM tooa büyük yeniden boyutlandırın.
  3. Select hello yeniden boyutlandırılabilir tıklayın ve VM **Başlat**, ve ardından VM'ler başlangıcı her hello durduruldu.

## <a name="next-steps"></a>Sonraki adımlar
Azure'da yeni bir Linux VM oluşturma sırasında sorunlarla karşılaşırsanız, bkz: [Azure'da yeni bir Linux sanal makine oluşturma ile dağıtım sorunlarını giderme](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

