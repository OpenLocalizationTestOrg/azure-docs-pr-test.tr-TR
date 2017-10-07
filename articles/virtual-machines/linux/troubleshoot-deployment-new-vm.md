---
title: "Linux VM dağıtımı-RM aaaTroubleshoot | Microsoft Docs"
description: "Azure'da yeni bir Linux sanal makine oluşturduğunuzda, Resource Manager dağıtım sorunlarını giderme"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Azure'da yeni bir Linux sanal makine oluşturma ile Resource Manager dağıtım sorunlarını giderme
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Üst sorunları
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

Diğer VM Dağıtım sorunlar ve sorular için bkz: [azure'da dağıtma Linux sanal makine sorunlarını giderme](troubleshoot-deploy-vm.md).
## <a name="collect-activity-logs"></a>Toplama etkinliklerini günlüğe kaydeder
sorun giderme, toostart toplama hello etkinlik hello sorun ilişkili tooidentify hello hata günlüğe kaydeder. Merhaba aşağıdaki bağlantılar hello işlem toofollow ilgili ayrıntılı bilgiler içerir.

[Dağıtım işlemlerini görüntüleme](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Etkinlik günlükleri toomanage Azure görüntülemek kaynakları](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** hello işletim sistemi olan genelleştirilmiş, Linux ve bunu karşıya ve/veya hello ayarı genelleştirilmiş yakalanan durumunda hataları olmayacak. Benzer şekilde, Hello OS Linux özelleştirilmiş ve bunu karşıya ve/veya ile yakalanan ise hello ayarı, özelleştirilmiş olmayacaktır sonra herhangi bir hata.

**Karşıya yükleme hataları:**

**N<sup>1</sup>:** hello OS genelleştirilmiş Linux olarak karşıya ise hello VM aşama sağlama hello takıldı için özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.

**N<sup>2</sup>:** hello OS Linux özelleştirilmiş ve genelleştirilmiş gibi karşıya ise, hello yeni VM hello özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız.

**Çözüm:**

Her iki bu hataları tooresolve karşıya özgün VHD, mevcut şirket içi Merhaba, ile aynı hello hello (genelleştirilmiş/özel) işletim sistemi ayarı. Genelleştirilmiş gibi tooupload unutmayın toorun-ilk sağlamayı sonlandırın.

**Hata yakalama:**

**N<sup>3</sup>:** hello OS genelleştirilmiş Linux olarak yakalanan ise genelleştirilmiş olarak işaretlenen gibi hello özgün VM kullanılabilir olmadığı için özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.

**N<sup>4</sup>:** hello OS Linux özelleştirilmiş ve genelleştirilmiş gibi yakalanan ise, hello yeni VM hello özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız. İşaretlendiğinden ayrıca hello özgün VM kullanılamaz olarak özelleştirilmiş.

**Çözüm:**

tooresolve hem bu hataları hello geçerli görüntü hello Portalı'ndan silmek ve [hello yeniden yakalar geçerli VHD'leri](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ile Merhaba Merhaba OS (genelleştirilmiş/özel) ayarı aynı.

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Sorun: Özel / Galeri / Market görüntüsü; ayırma hatası
Bu hata, istenen hello VM boyutu desteklemiyor veya kullanılabilir boş alanı tooaccommodate hello istekte sabitlenmiş tooa küme Hello yeni VM istek olduğunda durumlarda ortaya çıkar.

**1. neden:** hello küme destekleyemez hello istenen VM boyutu.

**Çözüm 1:**

* Daha küçük bir VM boyutu kullanarak hello isteği yeniden deneyin.
* Merhaba, hello VM değiştirilemez istenen boyut:
  * Merhaba kullanılabilirlik kümesindeki tüm hello VM'ler durdurun.
    Tıklatın **kaynak grupları** > *kaynak grubunuz* > **kaynakları** > *kullanılabilirlik kümesi* > **sanal makineleri** > *sanal makineniz* > **durdurmak**.
  * Tüm sanal makineleri Dur hello sonra hello oluşturmak hello yeni VM istenen boyutu.
  * Başlangıç yeni VM ilk hello ve hello teker tıklayın ve sanal makineleri durdu **Başlat**.

**Neden 2:** hello küme kaynakları serbest bırakmak sahip değil.

**Çözüm 2:**

* Merhaba isteği daha sonra yeniden deneyin.
* Merhaba yeni VM yapabiliyorsanız, farklı bir kullanılabilirlik parçası ayarlanması
  * Farklı bir kullanılabilirlik kümesinde yeni bir VM oluşturun (Merhaba içinde aynı bölge).
  * Merhaba yeni VM toohello eklemek aynı sanal ağ.

## <a name="next-steps"></a>Sonraki adımlar
Durdurulmuş bir Linux VM başlattığınızda veya varolan bir Linux VM azure'da yeniden boyutlandırma sorunlarıyla karşılaşırsanız bkz [başlatma veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma ile ilgili sorunları giderme Resource Manager dağıtım sorunlarını](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

