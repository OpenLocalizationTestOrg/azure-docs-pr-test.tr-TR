---
title: "aaaAbout diskleri ve Microsoft Azure Windows VM'ler için VHD'ler | Microsoft Docs"
description: "Diskleri ve sanal makineleri Azure VHD'ler için Windows hello temelleri hakkında bilgi edinin."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Diskleri ve Azure Windows VM'ler için VHD'ler hakkında
Yalnızca başka bir bilgisayarda gibi azure'daki sanal makinelerde diskleri yer toostore bir işletim sistemi olarak, uygulamaları ve verileri kullanın. Tüm Azure sanal makineler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diske sahip. Merhaba işletim sistemi diski bir görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü sabit bir Azure depolama hesabında depolanan sanal diskler (VHD). Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir. 

Bu makalede, biz hello hello diskler için farklı kullanımlar hakkında konuşun ve hello oluşturma ve kullanma disklerinin farklı türleri açıklanmaktadır. Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](storage-about-disks-and-vhds-linux.md).

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>VM'ler tarafından kullanılan diskler

Merhaba diskleri hello VM'ler tarafından nasıl kullanıldığı bir bakalım.

### <a name="operating-system-disk"></a>İşletim sistemi diski
Her bir sanal makinede bir ekli işletim sistemi diski var. SATA sürücü olarak kayıtlı ve hello C: sürücüsündeki varsayılan olarak etiketli. Bu disk 2048 gigabayt (GB) en fazla kapasiteye sahiptir. 

### <a name="temporary-disk"></a>Geçici disk
Her VM geçici disk içerir. Merhaba geçici disk uygulamalar ve işlemler için kısa vadeli depolama sağlar ve sayfa veya takas dosyaları gibi hedeflenen tooonly deposu veriler. Merhaba geçici disk üzerindeki verileri kaybolabilir sırasında bir [bakım olayı](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) veya ne zaman, [VM yeniden](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Merhaba VM standart yeniden sırasında hello geçici sürücüdeki hello verilerin kalıcı.

Merhaba geçici disk varsayılan ve pagefile.sys depolamak için kullanılan tarafından hello D: sürücü etiketlenir. tooremap bu disk tooa farklı bir sürücü harfi bkz [değişiklik hello sürücü harfi hello Windows geçici disk](../virtual-machines/windows/change-drive-letter.md). Merhaba hello geçici diskin boyutunu, hello hello sanal makine boyutuna göre değişir. Daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](../virtual-machines/windows/sizes.md).

Azure hello geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [hello geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Veri diski
Bir veri diski tookeep gereksinim duyduğunuz diğer veri mi ekli tooa sanal makine toostore uygulama verilerini bir VHD ' dir. Veri diskleri SCSI sürücüsü olarak kaydedilir ve seçtiğiniz bir harf ile etiketlenir. Her veri diski maksimum 4095 GB kapasitesine sahiptir. Merhaba hello sanal makine boyutunu belirler kullanabileceğiniz depolama tooit ve hello türü iliştirebilirsiniz kaç tane veri diskleri toohost hello diskler.

> [!NOTE]
> Sanal makineler kapasiteleri hakkında daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](../virtual-machines/windows/sizes.md).
> 

Bir görüntüden sanal makine oluşturduğunuzda azure bir işletim sistemi diski oluşturur. Veri diskleri içeren bir görüntü kullanırsanız, hello sanal makine oluştururken Azure hello veri diskleri da oluşturur. Aksi takdirde hello sanal makineyi oluşturduktan sonra veri diski ekleyin.

Veri diskleri tooa sanal makine olarak herhangi bir zamanda ekleyebilirsiniz **ekleme** disk toohello sanal makine hello. Karşıya veya tooyour depolama hesabı kopyalanan ya da bir, Azure sizin için oluşturduğu bir VHD kullanabilirsiniz. Bir veri diski eklemeyi hala bağlıyken depolama biriminden silinemez şekilde 'kira' hello VHD üzerinde koyarak hello VHD dosyasını hello VM ile ilişkilendirir.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Bir son öneri: kullanım yönetilmeyen standart disklerle KIRPMA 

Yönetilmeyen standart disk (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir. Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA hello diskte kullanılmayan blokları atar. Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz. 

Bu komut toocheck hello KIRPMA ayarı çalıştırabilirsiniz. Windows VM ve türü bir komut istemi açın:


```
fsutil behavior query DisableDeleteNotify
```

Merhaba komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir. 1 değeri döndürülürse, komut tooenable KIRPMA aşağıdaki hello çalıştırın:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Not: Windows Server 2012 ile kırpma desteği başlatır / Windows 8 ve yukarıda bkz bkz [yeni API apps toosend "KIRPMA ve eşlemesini" ipuçları toostorage medya sağlar](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Sonraki adımlar
* [Bir diski kullanıma açın](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd, VM için ek depolama alanı.
* [Değişiklik hello sürücü harfi hello Windows geçici disk](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) uygulamanız için verileri hello D: sürücü kullanabilirsiniz.

