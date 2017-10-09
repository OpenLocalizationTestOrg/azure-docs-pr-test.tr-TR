---
title: "AWS ve diğer platformlar tooManaged aaaMigrate diskler Azure'da | Microsoft Docs"
description: "AWS veya diğer sanallaştırma platformları gibi diğer bulut gelen karşıya VHD'lerin azure'da VM'ler oluşturun ve Azure yönetilen diskleri yararlanabilir."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Amazon Web Hizmetleri (AWS) ve diğer platformlar Azure tooManaged diskleri geçirme

AWS veya şirket içi Sanallaştırma Çözümleri tooAzure toocreate yönetilen diskleri yararlanmak VM'ler VHD dosyaları karşıya yükleyebilirsiniz. Azure yönetilen diskleri Azure Iaas VM'ler için toomanaging depolama hesaplarının hello gereksinimini ortadan kaldırır. Hello türü (Premium veya standart) ve duyduğunuz disk boyutunu belirtin tooonly varsa ve Azure oluşturur ve hello disk yönettiğiniz. 

Genelleştirilmiş ve özelleştirilmiş VHD'leri karşıya yükleyebilirsiniz. 
- **VHD genelleştirilmiş** -, sahip tüm kişisel hesap bilgilerinizi Sysprep kullanarak kaldırıldı. 
- **VHD özelleştirilmiş** -hello kullanıcı hesapları, uygulamaları ve diğer özgün VM Durum verilerini korur. 

> [!IMPORTANT]
> Tüm VHD tooAzure karşıya yüklemeden önce uygulamanız gereken [Windows VHD veya VHDX tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Senaryo                                                                                                                         | Belgeler                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Toomigrate tooAzure yönetilen diskleri ister var olan bir AWS EC2 örneğe sahip                                     | [Amazon Web Hizmetleri (AWS) tooAzure bir VM'yi taşıma](aws-to-azure.md)                           |
| Bir sanal makineden ve bir görüntü toocreate olarak toouse toouse istediğiniz diğer sanallaştırma platformu sahip birden fazla Azure VM'yi. | [Genelleştirilmiş bir VHD yüklemek ve Azure'da toocreate yeni VM'ler kullanın](upload-generalized-managed.md) |
| Azure'da toorecreate istediğiniz benzersiz şekilde özelleştirilmiş bir VM var.                                                      | [Özel bir VHD tooAzure karşıya yükleyin ve yeni bir VM oluşturun](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Yönetilen diskleri genel bakış

Azure yönetilen diskleri hello gerek toomanage depolama hesapları kaldırarak VM yönetimini basitleştirir. Diskleri bir kullanılabilirlik kümesindeki VM'lerin daha iyi güvenilirlik avantajı da yönetilen. Bu, farklı sanal makineleri bir kullanılabilirlik kümesindeki hello disklerin her diğer tooavoid tek noktasından hatalar yeterince yalıtılmış olmasını sağlar. Otomatik olarak kümesindeki bir kullanılabilirlik tek depolama ölçek birimi hataları toohardware ve yazılım hatalarına neden hello etkisini sınırlayan farklı depolama ölçek birimlerinin (damgaları ') içindeki farklı VM'ler diskleri yerleştirir. Gereksinimlerinize bağlı olarak, iki tür depolama seçenekleri arasında seçim yapabilirsiniz: 
 
- [Premium yönetilen diskleri](../../storage/common/storage-premium-storage.md) olan düz durumu sürücüsü (SSD) dayalı highperformance, g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için düşük gecikmeli disk desteği sunar, depolama depolama medyası. Merhaba hızı avantajlarından ve bu disklerin geçirme tooPremium yönetilen diskleri tarafından performansını alabilir.  

- [Standart yönetilen disk](../../storage/common/storage-standard-storage.md) geliştirme ve Test ve daha az hassas tooperformance değişkenlik olan diğer sık erişim iş yükleri için en uygun ve Sabit Disk sürücüsü (HDD) dayalı depolama medya kullanın.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Plan hello geçiş için tooManaged diskleri

Bu bölümde, VM ve disk türleri hakkında toomake hello en iyi karar yardımcı olur.


### <a name="location"></a>Konum

Azure yönetilen diskleri kullanılabildiği bir konum seçin. TooPremium yönetilen diskleri geçiriyorsanız, ayrıca Premium depolama burada toomigrate için planlama hello bölgede kullanılabilir olduğundan emin olun. Bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi.

### <a name="vm-sizes"></a>VM boyutları

TooPremium yönetilen diskleri geçiriyorsanız, VM bulunduğu hello bölgede tooupdate hello hello VM tooPremium depolama özellikli boyutu kullanılabilir boyutuna sahip. Premium depolama özellikli hello VM boyutları gözden geçirin. Hello Azure VM boyutu belirtimleri içinde listelenen [sanal makineler için Boyutlar](sizes.md).
Premium Storage ile birlikte çalışmak ve işleminizi iş yükü en çok uyan hello en uygun VM boyutunu seçin sanal makineleri Hello performans özellikleri gözden geçirin. Yeterli bant genişliği kullanılabilir VM toodrive hello disk trafiğinde bulunduğundan emin olun.

### <a name="disk-sizes"></a>Disk boyutları

**Premium yönetilen diskleri**

VM ile kullanılan Premium yönetilen diskleri üç tür vardır ve her belirli IOPS ve üretilen iş sahip sınırlar. Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın hello gereksinimlerine hello Premium disk türü, VM için temel seçerken göz önünde bulundurun.

| Premium diskler türü  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Disk boyutu           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| Disk başına IOPS       | 500               | 2300              | 5000              |
| Disk başına aktarım hızı | Saniyede 100 MB | 150 MB / saniye | 200 MB / saniye |

**Standart yönetilen disk**

VM ile kullanılabilecek standart yönetilen disk beş türü vardır. Bunların her biri farklı kapasiteye sahip ancak aynı IOPS ve üretilen iş sınırı vardır. Standart yönetilen disk uygulamanızın hello kapasite gereksinimlerine göre Hello türünü seçin.

| Standart Disk Türü  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Disk boyutu           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| Disk başına IOPS       | 500              | 500              | 500              | 500              | 500              |
| Disk başına aktarım hızı | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB |

### <a name="disk-caching-policy"></a>Önbellek İlkesi disk 

**Premium yönetilen diskleri**

Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium diskleri hello için ve *okuma-yazma* hello Premium işletim sistemi diski için toohello VM bağlı. Bu yapılandırma ayarının tooachieve hello en iyi performans için uygulamanızın IOs önerilir. (SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın.

### <a name="pricing"></a>Fiyatlandırma

Gözden geçirme hello [yönetilen diskler için fiyatlandırma](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Premium diskler yönetilen fiyatlandırma hello Premium yönetilmeyen diskleri aynıdır. Ancak standart yönetilen disk için fiyatlandırma standart yönetilmeyen disklerden farklı.


## <a name="next-steps"></a>Sonraki Adımlar

- Tüm VHD tooAzure karşıya yüklemeden önce uygulamanız gereken [Windows VHD veya VHDX tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
