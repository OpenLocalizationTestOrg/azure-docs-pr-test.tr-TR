---
title: "aaaTroubleshoot Azure Windows VM dağıtımı | Microsoft Docs"
description: "Azure'da yeni bir Windows sanal makine oluşturduğunuzda, Resource Manager dağıtım sorunlarını giderme"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: afc6c1a4-2769-41f6-bbf9-76f9f23bcdf4
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c27d4f63b67db2d1c9f117f05a2eba9ef130ef37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-when-creating-a-new-windows-vm-in-azure"></a>Azure'da yeni bir Windows VM oluştururken, dağıtım sorunlarını giderme
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a>Üst sorunları
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

Diğer VM Dağıtım sorunlar ve sorular için bkz: [azure'da dağıtma Windows sanal makine sorunlarını giderme](troubleshoot-deploy-vm.md).

## <a name="collect-activity-logs"></a>Toplama etkinliklerini günlüğe kaydeder
sorun giderme, toostart toplama hello etkinlik hello sorun ilişkili tooidentify hello hata günlüğe kaydeder. Merhaba aşağıdaki bağlantılar hello işlem toofollow ilgili ayrıntılı bilgiler içerir.

[Dağıtım işlemlerini görüntüleme](../../azure-resource-manager/resource-manager-deployment-operations.md)

[Etkinlik günlükleri toomanage Azure görüntülemek kaynakları](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-windows-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-windows-troubleshoot-deployment-new-vm-table.md)]

**Y:** hello işletim sistemi olan genelleştirilmiş, Windows ve bunu karşıya ve/veya hello ayarı genelleştirilmiş yakalanan durumunda hataları olmayacak. Benzer şekilde, Hello işletim sistemi Windows özelleştirilmiş ve bunu karşıya ve/veya ile yakalanan ise hello ayarı, özelleştirilmiş olmayacaktır sonra herhangi bir hata.

**Karşıya yükleme hataları:**

**N<sup>1</sup>:** hello OS genelleştirilmiş Windows olarak karşıya ise özelleştirilmiş, VM takılmış hello OOBE ekranında hello sağlama bir zaman aşımı hatasıyla karşılaşırsınız.

**N<sup>2</sup>:** hello işletim sistemi Windows özelleştirilmiş ve genelleştirilmiş gibi karşıya ise, VM takılmış hello OOBE ekranında hello yeni VM hello özgün bilgisayarla çalıştığından hello ile sağlama bir hata alırsınız adı, kullanıcı adı ve parolası.

**Çözümleme**

Her iki bu hataları tooresolve kullanın [Ekle AzureRmVhd tooupload hello özgün VHD](https://msdn.microsoft.com/library/mt603554.aspx), mevcut şirket içi, hello hello OS (genelleştirilmiş/özel) olarak aynı ayarı. Genelleştirilmiş gibi tooupload toorun sysprep ilk unutmayın.

**Hata yakalama:**

**N<sup>3</sup>:** hello OS genelleştirilmiş Windows olarak yakalanan ise genelleştirilmiş olarak işaretlenen gibi hello özgün VM kullanılabilir olmadığı için özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.

**N<sup>4</sup>:** hello işletim sistemi Windows özelleştirilmiş ve genelleştirilmiş gibi yakalanan ise, hello yeni VM hello özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız. İşaretlendiğinden ayrıca hello özgün VM kullanılamaz olarak özelleştirilmiş.

**Çözümleme**

tooresolve hem bu hataları hello geçerli görüntü hello Portalı'ndan silmek ve [hello yeniden yakalar geçerli VHD'leri](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ile Merhaba Merhaba OS (genelleştirilmiş/özel) ayarı aynı.

## <a name="issue-customgallerymarketplace-image-allocation-failure"></a>Sorun: Galeri/özel/Market görüntüsü; ayırma hatası
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
Durdurulmuş bir Windows VM başlattığınızda veya varolan bir Windows VM Azure ile yeniden boyutlandırın sorunlarıyla karşılaşırsanız bkz [başlatma veya mevcut bir Windows sanal makine azure'da yeniden boyutlandırma ile ilgili sorunları giderme Resource Manager dağıtım sorunlarını](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

