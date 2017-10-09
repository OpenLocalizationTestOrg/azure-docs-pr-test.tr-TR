---
title: "aaaAbout diskleri ve Microsoft Azure Linux VM'ler için VHD'ler | Microsoft Docs"
description: "Merhaba temelleri diskleri ve VHD Linux sanal makinelerinin Azure hakkında bilgi edinin."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 862217e4f15ff8fd2e08de71386c4f367d0c39db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>Diskleri ve Azure Linux VM'ler için VHD'ler hakkında
Yalnızca başka bir bilgisayarda gibi azure'daki sanal makinelerde diskleri yer toostore bir işletim sistemi olarak, uygulamaları ve verileri kullanın. Tüm Azure sanal makineler en az iki disk – Linux işletim sistemi diski ve geçici bir diske sahip. Merhaba işletim sistemi diski bir görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü gerçekte sanal bir Azure depolama hesabında depolanan sabit diskler (VHD). Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir. 

Bu makalede, biz hello hello diskler için farklı kullanımlar hakkında konuşun ve hello oluşturma ve kullanma disklerinin farklı türleri açıklanmaktadır. Bu makalede ayrıca kullanılabilir [Windows sanal makineleri](../windows/about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>VM'ler tarafından kullanılan diskler

Merhaba diskleri hello VM'ler tarafından nasıl kullanıldığı bir bakalım.

## <a name="operating-system-disk"></a>İşletim sistemi diski
Her bir sanal makinede bir ekli işletim sistemi diski var. SATA sürücüsü olarak kaydedilir ve/dev/sda varsayılan olarak etiketlenir. Bu disk 2048 gigabayt (GB) en fazla kapasiteye sahiptir. 

## <a name="temporary-disk"></a>Geçici disk
Her VM geçici disk içerir. Merhaba geçici disk uygulamalar ve işlemler için kısa vadeli depolama sağlar ve sayfa veya takas dosyaları gibi hedeflenen tooonly deposu veriler. Merhaba geçici disk üzerindeki verileri kaybolabilir sırasında bir [bakım olayı](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) veya ne zaman, [VM yeniden](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Merhaba VM standart yeniden sırasında hello geçici sürücüdeki hello verilerin kalıcı.

Linux sanal makinelerde hello genellikle disktir **/dev/sdb** ve biçimlendirilmiş ve çok takılı**/mnt** hello Azure Linux aracısı tarafından. Merhaba hello geçici diskin boyutunu, hello hello sanal makine boyutuna göre değişir. Daha fazla bilgi için bkz: [Linux sanal makineler için Boyutlar](../windows/sizes.md).

Azure hello geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [hello geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>Veri diski
Bir veri diski tookeep gereksinim duyduğunuz diğer veri mi ekli tooa sanal makine toostore uygulama verilerini bir VHD ' dir. Veri diskleri SCSI sürücüsü olarak kaydedilir ve seçtiğiniz bir harf ile etiketlenir. Her veri diski maksimum 4095 GB kapasitesine sahiptir. Merhaba hello sanal makine boyutunu belirler kullanabileceğiniz depolama tooit ve hello türü iliştirebilirsiniz kaç tane veri diskleri toohost hello diskler.

> [!NOTE]
> Sanal makineler kapasiteleri hakkında daha fazla ayrıntı için [Linux sanal makineler için Boyutlar](../windows/sizes.md).
> 

Bir görüntüden sanal makine oluşturduğunuzda azure bir işletim sistemi diski oluşturur. Veri diskleri içeren bir görüntü kullanırsanız, hello sanal makine oluştururken Azure hello veri diskleri da oluşturur. Aksi takdirde hello sanal makineyi oluşturduktan sonra veri diski ekleyin.

Veri diskleri tooa sanal makine olarak herhangi bir zamanda ekleyebilirsiniz **ekleme** disk toohello sanal makine hello. Karşıya veya tooyour depolama hesabı kopyalanan ya da bir, Azure sizin için oluşturduğu bir VHD kullanabilirsiniz. Bir veri diski eklemeyi hala bağlıyken depolama biriminden silinemez şekilde 'kira' hello VHD üzerinde koyarak hello VHD dosyasını hello VM ile ilişkilendirir.

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>Sorun giderme
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Sonraki adımlar
* [Bir diski kullanıma açın](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooadd, VM için ek depolama alanı.
* [Yazılım RAID yapılandırma](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artıklık için.
* [Linux sanal makine yakalama](./classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) VM daha hızlı bir şekilde dağıtabilmek için.

