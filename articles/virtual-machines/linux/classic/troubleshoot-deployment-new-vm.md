---
title: "Linux VM dağıtımı-Klasik aaaTroubleshoot | Microsoft Docs"
description: "Azure'da yeni bir Linux sanal makine oluşturduğunuzda, Klasik dağıtım sorunlarını giderme"
services: virtual-machines-linux
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: c8a963fa-6b2a-4c7a-a1f4-7793adb02b19
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cjiang
ms.openlocfilehash: a642bfd9a543cd6d2104b03fe04193d9352ccae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>Azure'da yeni bir Linux sanal makine oluşturma ile klasik dağıtım sorunlarını giderme
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-selectors](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-selectors-include.md)]

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Merhaba Resource Manager sürümü bu makale için bkz: [burada](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>Toplama denetim günlüklerini
sorun giderme, toostart toplama hello denetim hello sorun ilişkili tooidentify hello hata günlüğe kaydeder.

Hello Azure portal'ı tıklatın **Gözat** > **sanal makineleri** > *Windows sanal makinenizi*  >   **Ayarları** > **denetim günlüklerini**.

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y:** hello işletim sistemi olan genelleştirilmiş, Linux ve bunu karşıya ve/veya hello ayarı genelleştirilmiş yakalanan durumunda hataları olmayacak. Benzer şekilde, Hello OS Linux özelleştirilmiş ve bunu karşıya ve/veya ile yakalanan ise hello ayarı, özelleştirilmiş olmayacaktır sonra herhangi bir hata.

**Karşıya yükleme hataları:**

**N<sup>1</sup>:** hello OS genelleştirilmiş Linux olarak karşıya ise hello VM aşama sağlama hello takıldı için özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.

**N<sup>2</sup>:** hello OS Linux özelleştirilmiş ve genelleştirilmiş gibi karşıya ise, hello yeni VM hello özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız.

**Çözüm:**

Her iki bu hataları tooresolve karşıya özgün VHD, mevcut şirket içi Merhaba, ile aynı hello hello (genelleştirilmiş/özel) işletim sistemi ayarı. Genelleştirilmiş gibi tooupload unutmayın toorun-ilk sağlamayı sonlandırın. Bkz: [oluşturma ve bir Sanal Sabit Disk, CONTAINS hello Linux işletim sistemi yükleme](create-upload-vhd.md) daha fazla bilgi için.

**Hata yakalama:**

**N<sup>3</sup>:** hello OS genelleştirilmiş Linux olarak yakalanan ise genelleştirilmiş olarak işaretlenen gibi hello özgün VM kullanılabilir olmadığı için özelleştirilmiş, sağlama zaman aşımı hatası alırsınız.

**N<sup>4</sup>:** hello OS Linux özelleştirilmiş ve genelleştirilmiş gibi yakalanan ise, hello yeni VM hello özgün bilgisayar adı, kullanıcı adı ve parola ile çalıştığı için sağlama bir hata alırsınız. İşaretlendiğinden ayrıca hello özgün VM kullanılamaz olarak özelleştirilmiş.

**Çözüm:**

tooresolve hem bu hataları hello geçerli görüntü hello Portalı'ndan silmek ve [hello yeniden yakalar geçerli VHD'leri](capture-image.md) ile Merhaba Merhaba OS (genelleştirilmiş/özel) ayarı aynı.

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>Sorun: Özel / Galeri / Market görüntüsü; ayırma hatası
Bu hata, kullanılabilir boş alanı tooaccommodate hello isteği yok tooa küme Hello yeni VM istek gönderildiğinde, durumlarda ortaya çıkar veya istenen hello VM boyutu destekleyemez. Olası toomix farklı serisi olmadığı aynı bulut hizmeti hello alanındaki VM'lerin. Toocreate bulut hizmetiniz desteği ne değerinden farklı bir boyutta yeni bir VM istiyorsanız, bu nedenle hello işlem isteği başarısız olur.

Toocreate kullandığınız hello bulut hizmeti Hello kısıtlamaları bağlı olarak yeni VM Merhaba, iki durumlardan biri nedeniyle hatayla karşılaşabilirsiniz.

**1. neden:** hello bulut hizmeti sabitlenmiş tooa belirli küme ya da bu bağlantılı tooan benzeşim grubu ve bu nedenle sabitlenmiş tooa belirli küme tasarıma göre. Yeni işlem kaynak o benzeşim grubunda bilmediğinden aynı hello mevcut kaynakları barındırıldığı küme hello denenir. Ancak, hello aynı küme ya da olabilir destek hello istenen VM boyutu veya oluşan bir ayırma hata yeterli kullanılabilir alan vardır. Merhaba yeni kaynaklar var olan bir bulut hizmetini veya yeni bir bulut hizmeti aracılığıyla oluşturulan bu geçerlidir.

**Çözüm 1:**

* Yeni bir bulut hizmeti oluşturun ve bir bölge veya bölge tabanlı bir sanal ağ ile ilişkilendirin.
* Yeni bir VM hello yeni bulut hizmeti oluşturun.
  Toocreate yeni bir bulut hizmeti çalışırken bir hata alırsanız, daha sonra yeniden deneyin veya hello bölge hello bulut hizmeti için değiştirin.

> [!IMPORTANT]
> Toocreate var olan bir bulut hizmetinde yeni bir VM çalıştığınız ancak uygulanamadı ve yeni VM için yeni bir bulut hizmeti toocreate vardı, tüm Vm'leriniz tooconsolidate seçebilirsiniz hello aynı bulut hizmeti. toodo bu nedenle, hello VM'ler hello mevcut bulut hizmetindeki silin ve bunların disklerden hello yeni bulut hizmeti onları yeniden yakalar. Ancak, önemli tooremember tooupdate ihtiyacınız olacak şekilde hello yeni bulut hizmeti yeni bir ad ve VIP, bunlar şu anda bu bilgileri hello olan bulut hizmetini kullanan tüm hello bağımlılıklar için sahip olma olasılığı vardır.
> 
> 

**Neden 2:** hello bulut hizmeti, tasarım Sabitlenen tooa belirli küme olacak şekilde bağlantılı tooan benzeşim grubu, bir sanal ağ ile ilişkilendirilmiş. Benzeşim grubundaki tüm yeni işlem kaynak istekleri, bu nedenle aynı hello mevcut kaynakları barındırıldığı küme hello denenir. Ancak, hello aynı küme ya da olabilir destek hello istenen VM boyutu veya oluşan bir ayırma hata yeterli kullanılabilir alan vardır. Merhaba yeni kaynaklar var olan bir bulut hizmetini veya yeni bir bulut hizmeti aracılığıyla oluşturulan bu geçerlidir.

**Çözüm 2:**

* Yeni bir bölgesel sanal ağ oluşturun.
* Oluşturma hello yeni bir sanal ağ içinde yeni VM hello.
* [Varolan sanal ağınıza bağlamak](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/) toohello yeni bir sanal ağ. Daha fazla gördükleri hakkında [bölgesel sanal ağlar](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/). Alternatif olarak, [benzeşim grubuna bağlı sanal ağ tooa bölgesel sanal ağınızı geçirmek](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)ve ardından oluşturun yeni VM hello.

## <a name="next-steps"></a>Sonraki adımlar
Durdurulmuş bir Linux VM başlattığınızda veya varolan bir Linux VM azure'da yeniden boyutlandırma sorunlarıyla karşılaşırsanız bkz [yeniden başlatmayı veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Klasik dağıtım sorunlarını giderme](restart-resize-error-troubleshooting.md).

