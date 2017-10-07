---
title: Azure VM'ler tooManaged diskleri aaaMigrate | Microsoft Docs
description: "Yönetilmeyen diskleri depolama hesapları toouse yönetilen diskleri kullanılarak oluşturulan Azure sanal makineleri geçirin."
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
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Azure VM'ler tooManaged diskleri Azure geçirme

Azure yönetilen diskleri hello gereksinimini ortadan kaldırarak depolama yönetimini basitleştirir tooseparately depolama hesapları yönetin.  Ayrıca, mevcut Azure VM'ler tooManaged diskleri toobenefit bir kullanılabilirlik kümesindeki VM'lerin daha iyi güvenilirlik geçiş. Bu, farklı sanal makineleri bir kullanılabilirlik kümesindeki hello disklerin her diğer tooavoid tek noktasından hatalar yeterince yalıtılmış olmasını sağlar. Otomatik olarak kümesindeki bir kullanılabilirlik tek depolama ölçek birimi hataları toohardware ve yazılım hatalarına neden hello etkisini sınırlayan farklı depolama ölçek birimlerinin (damgaları ') içindeki farklı VM'ler diskleri yerleştirir.
Gereksinimlerinize bağlı olarak, iki tür depolama seçenekleri arasında seçim yapabilirsiniz:

- [Premium yönetilen diskleri](../../storage/common/storage-premium-storage.md) olan düz durumu sürücüsü (SSD) dayalı depolama medyası, bir highperformance, g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için düşük gecikmeli disk desteği sunar. Merhaba hızı avantajlarından ve bu disklerin geçirme tooPremium yönetilen diskleri tarafından performansını alabilir.

- [Standart yönetilen disk](../../storage/common/storage-standard-storage.md) geliştirme ve Test ve daha az hassas tooperformance değişkenlik olan diğer sık erişim iş yükleri için en uygun ve Sabit Disk sürücüsü (HDD) dayalı depolama medya kullanın.

Aşağıdaki senaryolarda tooManaged diskleri geçirebilirsiniz:

| Geçir...                                            | Belge bağlantı                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tek başına VM'ler ve sanal makineleri bir kullanılabilirlik kümesi toomanaged diskleri dönüştürme   | [Sanal makineleri yönetilen toouse diskleri dönüştürme](convert-unmanaged-to-managed-disks.md) |
| Yönetilen disklerde Klasik tooResource Manager tek bir VM'den     | [Tek bir VM geçirme](migrate-single-classic-to-resource-manager.md)  | 
| Bir sanal ağdan yönetilen disklerde Klasik tooResource Yöneticisi tüm hello Vm'lerde     | [Iaas kaynaklarını Klasik tooResource Yöneticisi geçirme](migration-classic-resource-manager-ps.md) ve ardından [VM yönetilmeyen diskleri toomanaged disklerden Dönüştür](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Plan hello dönüştürme için tooManaged diskleri

Bu bölümde, VM ve disk türleri hakkında toomake hello en iyi karar yardımcı olur.


## <a name="location"></a>Konum

Azure yönetilen diskleri kullanılabildiği bir konum seçin. TooPremium yönetilen diskleri taşıyorsanız, aynı zamanda Premium depolama burada toomove için planlama hello bölgede kullanılabilir olduğundan emin olun. Bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi.

## <a name="vm-sizes"></a>VM boyutları

TooPremium yönetilen diskleri geçiriyorsanız, VM bulunduğu hello bölgede tooupdate hello hello VM tooPremium depolama özellikli boyutu kullanılabilir boyutuna sahip. Premium depolama özellikli hello VM boyutları gözden geçirin. Hello Azure VM boyutu belirtimleri içinde listelenen [sanal makineler için Boyutlar](sizes.md).
Premium Storage ile birlikte çalışmak ve işleminizi iş yükü en çok uyan hello en uygun VM boyutunu seçin sanal makineleri Hello performans özellikleri gözden geçirin. Yeterli bant genişliği kullanılabilir VM toodrive hello disk trafiğinde bulunduğundan emin olun.

## <a name="disk-sizes"></a>Disk boyutları

**Premium yönetilen diskleri**

VM ile kullanılan yönetilen premium diskleri yedi tür vardır ve her belirli IOPS ve üretilen iş sahip sınırlar. Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın hello gereksinimlerine hello Premium disk türü, VM için temel seçerken dikkate.

| Premium diskler türü  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Disk boyutu           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Disk başına IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Disk başına aktarım hızı | Saniye başına 25 MB  | Saniye başına 50 MB  | Saniyede 100 MB | 150 MB / saniye | 200 MB / saniye | Saniye başına 250 MB | Saniye başına 250 MB |

**Standart yönetilen disk**

VM ile kullanılabilecek standart yönetilen disk yedi türü vardır. Bunların her biri farklı kapasiteye sahip ancak aynı IOPS ve üretilen iş sınırı vardır. Standart yönetilen disk uygulamanızın hello kapasite gereksinimlerine göre Hello türünü seçin.

| Standart Disk Türü  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Disk boyutu           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| Disk başına IOPS       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Disk başına aktarım hızı | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | 

## <a name="disk-caching-policy"></a>Önbellek İlkesi disk

**Premium yönetilen diskleri**

Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium diskleri hello için ve *okuma-yazma* hello Premium işletim sistemi diski için toohello VM bağlı. Bu yapılandırma ayarının tooachieve hello en iyi performans için uygulamanızın IOs önerilir. (SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın.

## <a name="pricing"></a>Fiyatlandırma

Gözden geçirme hello [yönetilen diskler için fiyatlandırma](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Premium diskler yönetilen fiyatlandırma hello Premium yönetilmeyen diskleri aynıdır. Ancak standart yönetilen disk için fiyatlandırma standart yönetilmeyen disklerden farklı.



## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [yönetilen diskleri](managed-disks-overview.md)
