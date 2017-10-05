---
title: "Diskler ve Microsoft Azure Windows VM'ler için VHD'ler hakkında | Microsoft Docs"
description: "Diskleri ve VHD'ler için Windows Azure sanal makineleri temelleri hakkında bilgi edinin."
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
ms.openlocfilehash: c194ca0f31d077ffa998764b9d63b12dd596ac32
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>Diskleri ve Azure Windows VM'ler için VHD'ler hakkında
Yalnızca başka bir bilgisayarda gibi azure'daki sanal makinelerde bir işletim sistemini, uygulamaları ve verileri depolamak için bir yer olarak diskleri kullanın. Tüm Azure sanal makineler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diske sahip. İşletim sistemi diski bir görüntüden oluşturulur ve hem işletim sistemi diski ve görüntünün sanal bir Azure depolama hesabında depolanan sabit diskler (VHD). Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir. 

Bu makalede, biz diskler için farklı kullanımlar hakkında konuşun ve oluşturma ve kullanma disklerinin farklı türleri açıklanmaktadır. Bu makalede ayrıca kullanılabilir [Linux sanal makineleri](about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>VM'ler tarafından kullanılan diskler

Diskleri VM'ler tarafından nasıl kullanıldığı bir bakalım.

### <a name="operating-system-disk"></a>İşletim sistemi diski
Her bir sanal makinede bir ekli işletim sistemi diski var. SATA sürücü olarak kayıtlı ve C: sürücüsündeki varsayılan olarak etiketli. Bu disk 2048 gigabayt (GB) en fazla kapasiteye sahiptir. 

### <a name="temporary-disk"></a>Geçici disk
Her VM geçici disk içerir. Geçici disk uygulamalar ve işlemler için kısa vadeli depolama sağlar ve yalnızca sayfa veya takas dosyaları gibi verileri depolamak için kullanılması amaçlanmıştır. Geçici disk üzerindeki verileri kaybolabilir sırasında bir [bakım olayı](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) veya ne zaman, [VM yeniden](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Sırasında standart yeniden başlatma VM geçici sürücüdeki verilerin kalıcı olması.

Geçici disk varsayılan ve pagefile.sys depolamak için kullanılan tarafından D: sürücü olarak etiketlenir. Farklı bir sürücü harfi için bu diski yeniden eşlemek için bkz: [Windows geçici disk sürücü harfini değiştirin](change-drive-letter.md). Geçici diskin boyutunu, sanal makine boyutuna göre değişir. Daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](sizes.md).

Azure geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Veri diski
Uygulama verileri veya tutmak için gereksinim duyduğunuz diğer veri depolamak için bir sanal makineye bağlı VHD veri disktir. Veri diskleri SCSI sürücüsü olarak kaydedilir ve seçtiğiniz bir harf ile etiketlenir. Her veri diski maksimum 4095 GB kapasitesine sahiptir. Kaç tane veri diskleri ve depolama türü için iliştirebilirsiniz diskleri barındırmak için kullanabileceğiniz sanal makine boyutunu belirler.

> [!NOTE]
> Sanal makineler kapasiteleri hakkında daha fazla bilgi için bkz: [boyutları için Windows sanal makineleri](sizes.md).
> 

Bir görüntüden sanal makine oluşturduğunuzda azure bir işletim sistemi diski oluşturur. Veri diskleri içeren bir görüntü kullanırsanız, sanal makine oluştururken Azure ayrıca veri diskleri oluşturur. Aksi halde, sanal makineyi oluşturduktan sonra veri diski ekleyin.

Veri diski bir sanal makine için herhangi bir zamanda göre ekleyebileceğiniz **ekleme** sanal makineye disk. Karşıya veya depolama hesabınız veya bir Azure sizin için oluşturduğu kopyalanan VHD kullanabilirsiniz. Bir veri diski eklemeyi hala bağlıyken depolama biriminden silinemez şekilde VHD 'kira' koyarak VHD dosyasını VM ile ilişkilendirir.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Bir son öneri: kullanım yönetilmeyen standart disklerle KIRPMA 

Yönetilmeyen standart disk (HDD) kullanırsanız, KIRPMA etkinleştirmeniz gerekir. Yalnızca gerçekten kullandığınız depolama için faturalandırılır şekilde KIRPMA diskte kullanılmayan blokları atar. Büyük dosyaları oluşturmak ve bunları silerseniz bu maliyetleri kaydedebilirsiniz. 

KIRPMA ayarını denetlemek için bu komutu çalıştırabilirsiniz. Windows VM ve türü bir komut istemi açın:


```
fsutil behavior query DisableDeleteNotify
```

Komut 0 döndürürse, KIRPMA doğru şekilde etkinleştirilir. 1 değeri döndürülürse, KIRPMA etkinleştirmek için aşağıdaki komutu çalıştırın:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Not: Windows Server 2012 ile kırpma desteği başlatır / Windows 8 ve yukarıda bkz bkz [yeni API sağlar "KIRPMA ve eşlemesini" ipuçları depolama ortamına göndermek uygulamalar](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want to match next-steps from overview of managed disks -->
## <a name="next-steps"></a>Sonraki adımlar
* [Bir diski kullanıma açın](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VM için ek depolama alanı eklemek için.
* [Windows geçici disk sürücü harfini değiştirin](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) uygulamanız için verileri D: sürücü kullanabilirsiniz.

